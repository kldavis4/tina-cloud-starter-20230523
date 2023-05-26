---
title: 'Simple Augmented Reality With OpenCV, Three.js, And WebSockets'
slug: simple-augmented-reality-with-opencv-a-three-js
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad9c422b-025b-4e2c-ab2c-ce926c4a86e6/augmented-excerpt.jpg
date: 2016-02-25T18:17:59.000Z
author: martinsikora
summary: >-
  In this tutorial, we’ll make use of OpenCV in Python to detect circle-shaped objects in a webcam stream and replace them with 3D Earth in Three.js in a browser window while using WebSockets to join this all together.
description: >-
  In this tutorial, we’ll make use of OpenCV in Python to detect circle-shaped objects in a webcam stream and replace them with 3D Earth in Three.js in a browser window while using WebSockets to join this all together.
categories:
  - Coding
  - JavaScript
  - Apps
  - Augmented Reality
---
Augmented reality is generally considered to be very hard to create. However, it's possible to make visually impressive projects using just open source libraries. In this tutorial, we'll make use of **OpenCV** in Python to detect circle-shaped objects in a webcam stream and replace them with 3D Earth in **Three.js** in a browser window while using **WebSockets** to join this all together.

We want to strictly separate front-end and back-end in order to make it reusable. In a real-world application we could write the front-end in Unity, Unreal Engine or Blender, for example, to make it look really nice. The browser front-end is the easiest to implement and should work on nearly every possible configuration.

To keep things simple we'll split the app into three smaller parts:

1.  **Python back-end with OpenCV**
    OpenCV will read the webcam stream and open multiple windows with camera image after passing it through multiple filters to ease debugging and give us a little insight into what the circle detection algorithm actually sees. Output of this part will be just 2D coordinates and radius of the detected circle.
2.  **JavaScript front-end with Three.js in a browser**
    Step-by-step implementation of Three.js library to render textured Earth with moon spinning around it. The most interesting thing here will be mapping 2D screen coordinates into the 3D world. We'll also approximate the coordinates and radius to increase OpenCV's accuracy.
3.  **WebSockets in both front-end and back-end**
    Back-end with WebSockets server will periodically send messages with detected circle coordinates and radii to the browser client.

{{< vimeo id="156679604" caption="Final result" >}}

{{% feature-panel %}}

## 1. Python Back-End With OpenCV

Our first step will be just importing the OpenCV library in Python and opening a window with a live webcam stream.

We're going to use the newest OpenCV 3.0 ([see installation notes](https://docs.opencv.org/doc/tutorials/introduction/table_of_content_introduction/table_of_content_introduction.html)) with Python 2.7. Please note, that installation on some systems might be problematic and the official documentation isn't very helpful. I tried myself on Mac OS X version 3.0 from [MacPorts](https://www.macports.org/) and the binary had a dependency issue so I had to switch to [Homebrew](https://brew.sh/) instead. Also note that some OpenCV packages might not come with Python binding by default (you need to use some command line options).

With Homebrew I ran:

<pre><code class="language-bash">brew install opencv
</code></pre>

This installs OpenCV with Python bindings by default.

Just to test things out I recommend you run Python in interactive mode (run `python` in CLI without any arguments) and write `import cv2`. If OpenCV is installed properly and paths to Python bindings are correct it shouldn't throw any errors.

Later, we'll also use Python's `numpy` for some simple operations with matrices so we can install it now as well.

<pre><code class="language-bash">pip install numpy
</code></pre>

### Reading The Camera Image

Now we can test the camera:

<pre><code class="language-python">import cv2
capture = cv2.VideoCapture(0)

while True:
    ret, image = capture.read()
    cv2.imshow('Camera stream', image)
    if cv2.waitKey(1) &#038; 0xFF == ord('q'):
        break
</code></pre>

With `cv2.VideoCapture(0)` we get access to the camera on index `0` which is the default (usually the built-in camera). If you want to use a different one, try numbers greater than zero; however, [there's no easy way](https://stackoverflow.com/questions/8044539/listing-available-devices-in-python-opencv) to list all available cameras with the current OpenCV version.

When we call `cv2.imshow('Camera stream', image)` for the first time it checks that no window with this name exists and creates a new one for us with an image from the camera. The same window will be reused for each iteration of the main loop.

Then we used `capture.read()` to wait and grab the current camera image. This method also returns a Boolean property `ret` in case the camera is disconnected or the next frame is not available for some reason.

At the end we have `cv2.waitKey(1)` that checks for 1 millisecond whether any key is pressed and returns its code. So, when we press `q` we break out of the loop, close the window and the app will end.

If this all works, we passed the most difficult part of the back-end app which is getting the camera to work.

### Filtering Camera Images

For the actual circle detection we're going to use **circle Hough Transform** which is implemented in `cv2.HoughCircles()` method and right now is the only algorithm available in OpenCV. The important thing for us is that it needs a grayscaled image as input and uses the **Canny edge detector** algorithm inside to find edges in the image. We want to be able to manually check what the algorithm sees so we'll compose one large image from four smaller images each with a different filter applied.

The Canny edge detector is an algorithm that processes the image in typically four directions (vertical, horizontal and two diagonals) and finds edges. The actual steps that this algorithm makes are [explained in greater detail on Wikipedia](https://en.wikipedia.org/wiki/Canny_edge_detector) or [briefly in the OpenCV docs](https://docs.opencv.org/doc/tutorials/imgproc/imgtrans/canny_detector/canny_detector.html).

In contrast to pattern matching this algorithm detects circular shapes so we can use any objects we have to hand that are circular. I'm going to use a lid from an instant coffee jar and then an orange coffee mug.

We don't need to work with full-size images (depends on your camera resolution, of course) so we'll resize them right between `capture.read()` and `cv2.imshow` to 640px width and height accordingly to keep aspect ratio:

<pre><code class="language-python">width, height = image.shape
scale = 640.0 / width
image = cv2.resize(image, (0,0), fx=scale, fy=scale)
</code></pre>

Then we want to convert it to a grayscaled image and apply first **median blur** which removes noise and retains edges, and then the Canny edge detector to see what the circle detection algorithm is going to work with. For this reason, we'll compose 2x2 grid with all four previews.

<div class="break-out">

<pre><code class="language-python">t = 100 # threshold for Canny Edge Detection algorithm
grey = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
blured = cv2.medianBlur(grey, 15)

# Create 2x2 grid for all previews
grid = np.zeros([2*h, 2*w, 3], np.uint8)

grid[0:h, 0:w] = image
# We need to convert each of them to RGB from greyscaled 8 bit format
grid[h:2*h, 0:w] = np.dstack([cv2.Canny(grey, t / 2, t)] * 3)
grid[0:h, w:2*w] = np.dstack([blured] * 3)
grid[h:2*h, w:2*w] = np.dstack([cv2.Canny(blured, t / 2, t)] * 3)
</code></pre></div>

{{< vimeo id="156682000" caption="Grid with previews. Top-left: raw webcam data; top-right: grayscaled after median blur; bottom-left: grayscaled and Canny edge; bottom-right: grayscaled after median blur and Canny edge." >}}

Even though Canny edge detector uses Gaussian blur to reduce noise, in my experience it's still worth using median blur as well. You can compare the two bottom images. The one on the left is just Canny edge detection without any other filter. The second image is also Canny edge detection but this time after applying median blur. It reduced objects in the background which will help circle detection.

### Detecting Circles With Hough Gradient

Internally, OpenCV uses a more efficient implementation of Hough Circle Transform called Hough Gradient Method that uses edge information from Canny edge detector. The gradient method is described in depth in the book *[Learning OpenCV](https://shop.oreilly.com/product/9780596516130.do)* and the *[Circle Hough Transform on Wikipedia](https://en.wikipedia.org/wiki/Circle_Hough_Transform)*.

Now it's time for the actual circle detection:

<div class="break-out">

<pre><code class="language-python">sc = 1 # Scale for the algorithm
md = 30 # Minimum required distance between two circles
# Accumulator threshold for circle detection. Smaller numbers are more
# sensitive to false detections but make the detection more tolerant.
at = 40
circles = cv2.HoughCircles(blured, cv2.HOUGH_GRADIENT, sc, md, t, at)
</code></pre></div>

This returns an array of all detected circles. For simplicity's sake, we'll care only about the first one. Hough Gradient is quite sensitive to really circular shapes so it's unlikely that this will result in false detections. If it did, increase the `at` parameter. This is why we used median blur above; it removed more noise so we can use a lower threshold, making the detection more tolerant to inaccuracies and with a lower chance of detecting false circles.

We'll print circle center and its radius to the console and also draw the found circle with its center to the image from camera in a separate window. Later, we'll send it via WebSocket to the browser. Note, that `x`, `y` and `radius` are all in pixels.

<div class="break-out">

<pre><code class="language-python">if circles is not None:
    # We care only about the first circle found.
    circle = circles[0][0]
    x, y, radius = int(circle[0]), int(circle[1]), int(circle[2])
    print(x, y, radius)

    # Highlight the circle
    cv2.circle(image, [x, y], radius, (0, 0, 255), 1)
    # Draw a dot in the center
    cv2.circle(image, [x, y], 1, (0, 0, 255), 1)
</code></pre></div>

This will print to console tuples like:

<pre><code class="language-python">(251, 202, 74)
(252, 203, 73)
(250, 202, 74)
(246, 202, 76)
(246, 204, 74)
(246, 205, 72)
</code></pre>

{{< vimeo id="156682432" caption="Webcam stream with circles detected using Hough Gradient." >}}

As you can see on this animation, it failed to find any circles at all. My built-in camera has only 15fps and when I move my hand quickly the image is blurred so it doesn't find circle edges, not even after applying filters.

At the end of this article we'll come back to this problem and talk a lot about camera-specific settings and choice of detection algorithm, but we can already say that even though my setup is very bad (only 15fps, poor lighting, a lot of noise in the background, the object has low contrast), the result is reasonably good.

That's all for now. We have the `x` and `y` coordinates and `radius` in pixels of a circle found in the webcam image.

You can see the [full source code for this part on gist.github.com](https://gist.github.com/martinsik/a3d6142b0392d77c13ab#file-circle_detection-py).

## 2. JavaScript Front-End With Three.js In Browsers

The front-end part is based on the [Three.js](https://threejs.org/) (version r72) library. We'll start by just creating a rotating textured sphere representing Earth in the center of the screen, then add the moon spinning around it. At the end we'll map 2D screen mouse coordinates to the 3D space.

Our HTML page will consist of just a single <code>&lt;canvas&gt;</code> element. see [_index.html_ on gist.github.com](https://gist.github.com/martinsik/a3d6142b0392d77c13ab#file-index-html).

### Creating Earth

JavaScript is going to be a bit longer but it's split into multiple initialization functions where each has single purpose. Earth and moon textures come from [planetpixelemporium.com](https://planetpixelemporium.com/earth.html). Note that when loading textures, CORS rules are applied.

<div class="break-out">

<pre><code class="language-javascript">var scene, camera, renderer, light, earthMesh, earthRotY = 0;

function initScene(width, height) {
    scene = new THREE.Scene();
    // Setup cameta with 45 deg field of view and same aspect ratio
    camera = new THREE.PerspectiveCamera(45, width / height, 0.1, 1000);
    // Set the camera to 400 units along `z` axis
    camera.position.set(0, 0, 400);

    renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
    renderer.setSize(width, height);
    renderer.shadowMap.enabled = true;
    document.body.appendChild(renderer.domElement);
}

function initLight() {
    light = new THREE.SpotLight(0xffffff);
    // Position the light slightly to a side to make shadows look better.
    light.position.set(400, 100, 1000);
    light.castShadow = true;
    scene.add(light);
}

function initEarth() {
    // Load Earth texture and create material from it
    var earthMaterial = new THREE.MeshLambertMaterial({
        map: THREE.ImageUtils.loadTexture("/images/earthmap1k.jpg"),
    });
    // Create a sphere 25 units in radius and 16 segments
    // both horizontally and vertically.
    var earthGeometry = new THREE.SphereGeometry(25, 16, 16);
    earthMesh = new THREE.Mesh(earthGeometry, earthMaterial);
    earthMesh.receiveShadow = true;
    earthMesh.castShadow = true;
    // Add Earth to the scene
    scene.add(earthMesh);
}

// Update position of objects in the scene
function update() {
    earthRotY += 0.007;
    earthMesh.rotation.y = earthRotY;
}

// Redraw entire scene
function render() {
    update();
    renderer.setClearColor(0x000000, 0);
    renderer.render(scene, camera);
    // Schedule another frame
    requestAnimationFrame(render);
}

document.addEventListener('DOMContentLoaded', function(e) {
    // Initialize everything and start rendering
    initScene(window.innerWidth, window.innerHeight);
    initEarth();
    initLight();
    // Start rendering the scene
    requestAnimationFrame(render);
});
</code></pre></div>

[See a live demo here.](https://plnkr.co/edit/baBQZQrbGrv0RiiFGylq?p=preview)

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b47df41-bf21-4324-9ffd-543d2e957e75/threejs-spinning-earth.gif" width="500" height="200" alt="threejs-spinning-earth" /><figcaption>Textured sphere with Three.js. (<a href="https://planetpixelemporium.com/earth.html">Earth texture credit</a>)</figcaption></figure>

This was mostly just basic Three.js stuff. Object and method names are self-explantory (like `receiveShadow` or `castShadow`) but if you've never used it before I strongly recommend you look at [Lee Stemkoski's tutorials](https://stemkoski.github.io/Three.js/).

Optionally, we could also draw an axis in the center of the screen to help us with the coordinate system.

<pre><code class="language-javascript">var axes = new THREE.AxisHelper(60);
axes.position.set(0, 0, 0);
scene.add(axes);
</code></pre>

### Adding The Moon

Creating the moon is going to be very similar. The main difference is that we need to set the moon's position relative to Earth.

<div class="break-out">

<pre><code class="language-javascript">function initMoon() {
    // The same as initEarth() with just different texture
}

// Update position of objects in the scene
function update() {
    // Update Earth position
    // ...

    // Update Moon position
    moonRotY += 0.005;
    radY += 0.03;
    radZ += 0.0005;

    // Calculate position on a sphere
    x = moonDist * Math.cos(radZ) * Math.sin(radY);
    y = moonDist * Math.sin(radZ) * Math.sin(radY);
    z = moonDist * Math.cos(radY);

    var pos = earthMesh.position;
    // We can keep `z` as is because we're not moving the Earth
    // along z axis.
    moonMesh.position.set(x + earthMesh.pos.x, y + earthMesh.pos.y, z);
    moonMesh.rotation.y = moonRotY;
}
</code></pre></div>

[See a live demo here.](https://plnkr.co/edit/u5GuZBgcdkhoDCFBFbga?p=preview)
{{< vimeo id="156683239" caption="Earth and moon with Three.js. (<a href='https://planetpixelemporium.com/earth.html'>Earth and moon textures credit</a>)" >}}

### Mapping 2D Coordinates To A 3D World

So far, everything is pretty obvious. The most interesting part is going to be how to covert 2D screen coordinates coming from OpenCV (see output of circular detection above) to a 3D world? When we were defining radii and positions in Three.js we used some units but these have nothing to do with actual screen pixels. In fact, dimensions of everything we see in the scene are highly dependent on our camera settings (like aspect ratio or field of view).

For this reason, we'll make a flat plane object that will be large enough to cover the entire scene with its center at `[0,0,0]`. For demonstration purposes we'll map 2D mouse coordinates to Earth's position in 3D with a fixed `z` axis. In other words, we'll convert only `x` and `y` and not worry about `z`, which is the distance from the object to our camera.

We'll convert mouse screen positions into a range from `-1.0` to `+1.0` with its center at `[0,0]` because we need to work with normalized vectors.

Later we'll use this exact technique to map the position of the detected circle to 3D and also to match circle size from 2D to 3D.

<div class="break-out">

<pre><code class="language-javascript">var mouse = {};

function initPlane() {
    // The plane needs to be large to always cover entire scene
    var tmpGeometry = new THREE.PlaneGeometry(1000, 1000, 1, 1);
    tmpGeometry.position = new THREE.Vector3(0, 0, 0);
    var tmpMesh = new THREE.Mesh(tmpGeometry);
}

function onDocumentMouseMove(event) {
    // Current mouse position with [0,0] in the center of the window
    // and ranging from -1.0 to +1.0 with `y` axis inverted.
    mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
    mouse.y = - (event.clientY / window.innerHeight) * 2 + 1;
}

function update() {
    // ... the rest of the function

    // We need mouse x and y coordinates to set vector's direction
    var vector = new THREE.Vector3(mouse.x, mouse.y, 0.0);
    // Unproject camera distortion (fov, aspect ratio)
    vector.unproject(camera);
    var norm = vector.sub(camera.position).normalize();
    // Cast a line from our camera to the tmpMesh and see where these
    // two intersect. That's our 2D position in 3D coordinates.
    var ray = new THREE.Raycaster(camera.position, norm);
    var intersects = ray.intersectObject(tmpMesh);

    earthMesh.position.x = intersects[0].point.x;
    earthMesh.position.y = intersects[0].point.y;
}
</code></pre></div>

[See a live demo here.](https://plnkr.co/edit/MEYNOIRp7Y2DrrcyU9Eg?p=preview)

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/667cd428-4304-4681-8370-cf43d4cca9ca/threejs-earth-to-mouse.gif" width="500" height="300" alt="threejs-spinning-earth" /><figcaption>Earth position in 3D mapped to 2D mouse position. (<a href="https://planetpixelemporium.com/earth.html">Earth and moon textures credit</a>)</figcaption></figure>

Since we're checking the intersection with a plane, we know there's always going to be only one.

That's all for this part. At the end of the next part we'll also add WebSockets and a `<video>` element with our camera stream that will be overlaid by the 3D scene in Three.js.

### 3. WebSockets In Both Front-End And Back-End

We can start by implementing WebSockets in the Python back-end by installing `simple-websocket-server` libraries. There're many different libraries like [Tornado](https://www.tornadoweb.org/en/stable/) or [Autobahn](https://autobahn.ws/python/). We'll use `simple-websocket-server` because it's very easy to use and has no dependecies.

<pre><code class="language-bash">pip install git+https://github.com/dpallot/simple-websocket-server.git
</code></pre>

We'll run the WebSocket server in a separate thread and keep track of all connected clients.

<div class="break-out">

<pre><code class="language-python">from SimpleWebSocketServer import SimpleWebSocketServer, WebSocket
clients = [], server = None

class SimpleWSServer(WebSocket):
    def handleConnected(self):
        clients.append(self)

    def handleClose(self):
        clients.remove(self)

def run_server():
    global server
    server = SimpleWebSocketServer(’, 9000, SimpleWSServer,
                                   selectInterval=(1000.0 / 15) / 1000)
    server.serveforever()

t = threading.Thread(target=run_server)
t.start()

# The rest of the OpenCV code ...
</code></pre></div>

We used the `selectInterval` parameter in the server's constructor to make it periodically check for any pending messages. The server sends messages only when receiving data from clients, or it needs to sit on the main thread in a loop. We can't let it block the main thread because OpenCV needs it as well. Since we know that the camera runs only at 15fps we can use the same interval on the WebSocket server.

Then, after we detect the circles, we can iterate all connected clients and send the current position and radius relative to the image size.

<div class="break-out">

<pre><code class="language-python">for client in clients:
    msg = json.dumps({'x': x / w, 'y': y / h, 'radius': radius / w})
    client.sendMessage(unicode(msg))
</code></pre></div>

You can see the [full source code for the server is on gist.github.com](https://gist.github.com/martinsik/a3d6142b0392d77c13ab#file-circle_detection_with_websocket_server-py).

The JavaScript part will mimic the same behavior as we did with mouse position. We'll also keep track of the few messages and calculate a mean value for each axis and radius to improve accuracy.

<div class="break-out">

<pre><code class="language-javascript">var history = [];
var ws = new WebSocket('ws://localhost:9000');
ws.onopen = function() {
    console.log('onopen');
};
ws.onmessage = function (event) {
    var m = JSON.parse(event.data);
    history.push({ x: m.x * 2 - 1, y: -m.y * 2 + 1, radius: m.radius});

    // ... rest of the function.
};
</code></pre></div>

Instead of setting Earth's position to my current mouse position we'll use the `msgHistory` variable.

It's probably not necessary to paste the entire code here, so feel free to look at [implementation details on gist.gihtub.com](https://gist.github.com/martinsik/a3d6142b0392d77c13ab#file-threejs_with_websockets-js).

Then add one `<video>` element with the webcam stream filling the entire window that will be overlaid by our 3D scene with a transparent background.

<div class="break-out">

<pre><code class="language-javascript">var videoElm = document.querySelector('video');
// Make sure the video fits the window.
var constrains = { video: { mandatory: { minWidth: window.innerWidth }}};

if (navigator.getUserMedia) {
    navigator.getUserMedia(constrains, function(stream) {
        videoElm.src = window.URL.createObjectURL(stream);
        // When the webcam stream is ready get it's dimensions.
        videoElm.oncanplay = function() {
            init(videoElm.clientWidth, videoElm.clientHeight);
            // Init everything ...

            requestAnimationFrame(render);
        }
    }, function() {});
}
</code></pre></div>

The final result:
{{< vimeo id="156683592" caption="Final application with Earth mapped to coordinates found by OpenCV." >}}

To quickly recap what we did and what the above video shows:

1.  Python back-end runs a WebSocket server.
2.  Server detects a circle using OpenCV from a webcam stream.
3.  JavaScript client displays the same webcam stream using `<video>` element.
4.  Client renders 3D scene using [Three.js](https://threejs.org/).
5.  Client connects to the server via WebSocket protocol and receives circle position and radius.

The actual code used for this [demo is available on GitHub](https://gist.github.com/martinsik/a3d6142b0392d77c13ab#file-threejs_with_websockets-js). It's slightly more sophisticated and also interpolates coordinates between two messages from the back-end because the webcam stream runs only at 15fps while the 3D scene is rendered at 60fps. You can see the [original video on YouTube](https://www.youtube.com/watch?v=GQNW3BMKOkI).

## Caveats

There are some findings worth noting:

### Circle Detection Isn't Ideal

It's great that it works with any circular object but it's very sensitive to noise and image deformation, although as you can see above our result is pretty good. Also, there are probably no practical examples of circle detection available apart from the most basic usage. It might be better to [use ellipse detection](https://ieeexplore.ieee.org/xpl/articleDetails.jsp?arnumber=1048464) but it's not implemented in OpenCV right now.

### Everything Depends On Your Setup

Built-in webcams are generally pretty bad. 15fps isn't enough and just increasing it to 30fps reduces motion blur significantly and makes detection more reliable. We can break down this point into four more points:

- **Camera distortions**  
Many cameras introduce some image distortion, most commonly a fish-eye effect which has a significant influence on shape detection. OpenCV's documentation has a very straightforward tutorial on how to [reduce distortion by calibrating your camera](https://docs.opencv.org/master/dc/dbb/tutorial_py_calibration.html).
- **There's no official list of devices supported by OpenCV**  
Even if you already have a good camera it might not work with OpenCV without further explanation. I've also read about people using some other library to capture a camera image (like [libdc1394](https://damien.douxchamps.net/ieee1394/libdc1394/) for IEEE 1394-based cameras) and then using OpenCV just to process the images. Brew package manager lets you compile OpenCV directly with libdc1394 support.
- **Some cameras work better with OpenCV than others**  
If you're lucky you can set [some camera options like frames per second](https://docs.opencv.org/master/d8/dfe/classcv_1_1VideoCapture.html#a8c6d8c2d37505b5ca61ffd4bb54e9a7c&gsc.tab=0) directly on your camera but it might also have no effect at all if OpenCV isn't friendly with your device. Again, without any explanation.
- **All parameters depend on a real-world usage**  
When used in a real-world installation, it's highly recommended to test the algorithms and filters in the actual environment because things like lights, background color or object choice have significant effects on the result. This also includes shadows from daylight, people standing around, and so on.

### Pattern Matching Is Usually A Better Choice

If you see any augmented reality used in practice it'll be probably based on pattern matching. It's generally more reliable and not so affected by the problems described above.

### Filters Are Crucial

I think correct usage of filters requires some experience and always a little magic. The processing time of most filters depends on their parameters, although in [OpenCV 3.0](https://docs.opencv.org/3.0.0/) some of them are already rewritten into CUDA C (a C-like language for highly parallel programming with NVIDIA graphics cards) which brings significant performance improvements.

### Filter Data From OpenCV

We've seen that circle detection has some inaccuracies: sometimes it fails to find any circle or it detects the wrong radius. To minimize this type of error it would be worthwhile to implement some more sophisticated method to improve accuracy. In our example we used median for `x`, `y` and `radius`, which is very simple. A commonly used filter with good results is the [Kalman filter](https://en.wikipedia.org/wiki/Kalman_filter), used by autopilots for drones to reduce inaccuracy coming from sensors. However, its implementation isn't as simple as using just `math.mean()` from [https://mathjs.org](https://mathjs.org).

## Conclusion

I first saw a similar application in the [National Museum of Natural History in Madrid](https://www.mncn.csic.es/) two years ago and I wondered how difficult it would be to make something similar.

My core idea behind this demo was to use tools that are common on the web (like WebSockets and Three.js) and don't require any prerequisites so anyone can start using them right away. That's why I wanted to use just circle detection and not pattern matching, which would require to print or have some particular real-world object.

I need to say that I severely underestimated the actual camera requirements. High frames per second and good lighting are more important than resolution. I also didn't expect that camera incompatibility with OpenCV would be an issue.

{{< signature "rb, jb, og, ml" >}}


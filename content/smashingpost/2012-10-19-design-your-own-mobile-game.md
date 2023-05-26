---
title: How To Design A Mobile Game With HTML5
slug: design-your-own-mobile-game
image: >-
  https://www.smashingmagazine.com/inspiration/2014/04/11/get-excited-about-emotional-branding/attachment/why-you-should-get-excited-about-emotional-branding-fb-jpg-12/attachment/mobile-game/
date: 2012-10-19T10:29:47.000Z
author: eoin-mcgrath
description: >-
  Care to make a cross-platform mobile game with HTML5? No need to dabble in Java or Objective-C? Bypass the app stores? Sounds like an instant win! A handful of game developers are pushing the envelope of mobile HTML5 games at the moment. Check out the likes of Nutmeg and Lunch Bug for some shining examples.
categories:
  - Mobile
  - Games
  - HTML5
  - iPhone
---
The great thing about these titles is that they work equally well on both mobile and desktop using the same code. Could HTML5 finally fulfill the holy grail of “write once, run anywhere”?

### Getting Started

Before you start sketching the next <em>Temple Run</em> or <em>Angry Birds</em>, you should be aware of a few things that could dampen your excitement:

{{% feature-panel %}}

*   **Performance**.  Mobile browsers are not traditionally known for their blazing JavaScript engines. With iOS 6 and Chrome beta for Android, though, things are improving fast.
*   **Resolution**.  A veritable cornucopia of Android devices sport a wide range of resolutions. Not to mention the increased resolution and pixel density of the iPhone 4 and iPad 3.
*   **Audio**.  Hope you enjoy the sound of silence. Audio support in mobile browsers is poor, to say the least. Lag is a major problem, as is the fact that most devices offer only a single channel. iOS won’t even load a sound until the user initiates the action. My advice is to hold tight and wait for browser vendors to sort this out.

Now, as a Web developer you’re used to dealing with the quirks of certain browsers and degrading gracefully and dealing with fragmented platforms. So, a few technical challenges won’t put you off, right? What’s more, all of these performance and audio problems are temporary. The mobile browser landscape is changing so quickly that these concerns will soon be a distant memory.

In this tutorial, we’ll make a relatively simple game that takes you through the basics and steers you away from pitfalls. The result will look like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbe8b185-314e-4aab-804a-cfb82abbf15c/iphone.png"><img loading="lazy" decoding="async" class="131242" title="Pop, a very simple game that works on most smartphones as well as modern browsers." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbe8b185-314e-4aab-804a-cfb82abbf15c/iphone.png" alt="Screenshot of finished demo" width="220" height="381" /></a>

*   [Play the demo.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f146e18-7c94-4884-9730-e077aa949f15/final.html)
*   [Download the demo](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75997915-9211-496a-a035-2bb13ee364f0/pop-game-demo.zip) (ZIP).

It’s a fairly simple game, in which the user bursts floating bubbles before they reach the top of the screen. Imaginatively, I’ve titled our little endeavour <em>Pop</em>.

We’ll develop this in a number of distinct stages:

1.  Cater to the multitude of viewports and optimize for mobile;
2.  Look briefly at using the canvas API to draw to the screen;
3.  Capture touch events;
4.  Make a basic game loop;
5.  Introduce sprites, or game “entities”;
6.  Add collision detection and some simple maths to spice things up;
7.  Add a bit of polish and some basic particle effects.</p>

## 1\. Setting The Stage

Enough of the background story. Fire up your favorite text editor, pour a strong brew of coffee, and let’s get our hands dirty.

As mentioned, there is a plethora of resolution sizes and pixel densities across devices. This means we’ll have to <strong>scale our canvas</strong> to fit the viewport. This could come at the price of a loss in quality, but one clever trick is to make the canvas small and then scale up, which provides a performance boost.

Let’s kick off with a basic HTML shim:

<pre><code class="language-markup tmp-html">&lt;!DOCTYPE HTML&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
&lt;meta charset="UTF-8"&gt;

&lt;meta name="viewport" content="width=device-width,
    user-scalable=no, initial-scale=1, maximum-scale=1, user-scalable=0" /&gt;
&lt;meta name="apple-mobile-web-app-capable" content="yes" /&gt;
&lt;meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" /&gt;

&lt;style type="text/css"&gt;
body { margin: 0; padding: 0; background: #000;}
canvas { display: block; margin: 0 auto; background: #fff; }
&lt;/style&gt;

&lt;/head&gt;

&lt;body&gt;

&lt;canvas&gt; &lt;/canvas&gt;
&lt;script&gt;
// all the code goes here
&lt;/script&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre>

The <code>meta</code> viewport tag tells mobile browsers to disable user scaling and to render at full size rather than shrink the page down. The subsequent <code>apple-</code> prefixed meta tags allow the game to be bookmarked. On the iPhone, bookmarked apps do not display the toolbar at the bottom of the page, thus freeing up valuable real estate.

Take a look at the following:

<pre><code class="language-javascript">// namespace our game
var POP = {

    // set up some initial values
    WIDTH: 320,
    HEIGHT:  480,
    // we'll set the rest of these
    // in the init function
    RATIO:  null,
    currentWidth:  null,
    currentHeight:  null,
    canvas: null,
    ctx:  null,

    init: function() {

        // the proportion of width to height
        POP.RATIO = POP.WIDTH / POP.HEIGHT;
        // these will change when the screen is resized
        POP.currentWidth = POP.WIDTH;
        POP.currentHeight = POP.HEIGHT;
        // this is our canvas element
        POP.canvas = document.getElementsByTagName('canvas')[0];
        // setting this is important
        // otherwise the browser will
        // default to 320 x 200
        POP.canvas.width = POP.WIDTH;
        POP.canvas.height = POP.HEIGHT;
        // the canvas context enables us to
        // interact with the canvas api
        POP.ctx = POP.canvas.getContext('2d');

        // we're ready to resize
        POP.resize();

    },

    resize: function() {

        POP.currentHeight = window.innerHeight;
        // resize the width in proportion
        // to the new height
        POP.currentWidth = POP.currentHeight * POP.RATIO;

        // this will create some extra space on the
        // page, allowing us to scroll past
        // the address bar, thus hiding it.
        if (POP.android || POP.ios) {
            document.body.style.height = (window.innerHeight + 50) + 'px';
        }

        // set the new canvas style width and height
        // note: our canvas is still 320 x 480, but
        // we're essentially scaling it with CSS
        POP.canvas.style.width = POP.currentWidth + 'px';
        POP.canvas.style.height = POP.currentHeight + 'px';

        // we use a timeout here because some mobile
        // browsers don't fire if there is not
        // a short delay
        window.setTimeout(function() {
                window.scrollTo(0,1);
        }, 1);
    }

};

window.addEventListener('load', POP.init, false);
window.addEventListener('resize', POP.resize, false);</code></pre>

First, we create the <code>POP</code> namespace for our game. Being good developers, we don’t want to pollute the global namespace. In keeping good practice, we will declare all variables at the start of the program. Most of them are obvious: <code>canvas</code> refers to the <code>canvas</code> element in the HTML, and <code>ctx</code> enables us to access it via the JavaScript canvas API.

In <code>POP.init</code>, we grab a reference to our canvas element, get its context and adjust the canvas element’s dimensions to 480 × 320. The <code>resize</code> function, which is fired on resize and load events, adjusts the canvas’ <code>style</code> attribute for width and height accordingly while maintaining the ratio. Effectively, the canvas is still the same dimensions but has been scaled up using CSS. Try resizing your browser and you’ll see the canvas scale to fit.

If you tried that on your phone, you’ll notice that the address bar is still visible. Ugh! We can fix this by adding a few extra pixels to the document and then scrolling down to hide the address bar, like so:

<pre><code class="language-javascript">// we need to sniff out Android and iOS
// so that we can hide the address bar in
// our resize function
POP.ua = navigator.userAgent.toLowerCase();
POP.android = POP.ua.indexOf('android') &gt; -1 ? true : false;
POP.ios = ( POP.ua.indexOf('iphone') &gt; -1 || POP.ua.indexOf('ipad') &gt; -1  ) ?
    true : false;</code></pre>

The code above sniffs out the user agent, flagging for Android and iOS if present. Add it at the end of <code>POP.init</code>, before the call to <code>POP.resize()</code>.

Then, in the <code>resize</code> function, if <code>android</code> or <code>ios</code> is <code>true</code>, we add another 50 pixels to the document’s height — i.e. enough extra space to be able to scroll down past the address bar.

<pre><code class="language-javascript">// this will create some extra space on the
// page, enabling us to scroll past
// the address bar, thus hiding it.
if (POP.android || POP.ios) {
    document.body.style.height = (window.innerHeight + 50) + 'px';
}</code></pre>

Notice that we do this only for Android and iOS devices; otherwise, nasty scroll bars will appear. Also, we need to delay the firing of <code>scrollTo</code> to make sure it doesn’t get ignored on mobile Safari.

## 2\. A Blank Canvas

Now that we’ve scaled our canvas snuggly to the viewport, let’s add the ability to draw some shapes.

<strong>Note:</strong> In this tutorial, we’re going to stick with basic geometric shapes. iOS 5 and Chrome beta for Android can handle a lot of image sprites at a high frame rate. Try that on Android 3.2 or lower and the frame rate will drop exponentially. Luckily, there is not much overhead when drawing circles, so we can have a lot of bubbles in our game without hampering performance on older devices.

Below, we’ve added a basic <code>Draw</code> object that allows us to clear the screen, draw a rectangle and circle, and add some text. Nothing mind-blowing yet. Mozilla Developers Network has excellent resources as always, <a href="https://developer.mozilla.org/en/Canvas_tutorial/">replete with examples for drawing to the canvas</a>.

<pre><code class="language-javascript">// abstracts various canvas operations into
// standalone functions
POP.Draw = {

    clear: function() {
        POP.ctx.clearRect(0, 0, POP.WIDTH, POP.HEIGHT);
    },

    rect: function(x, y, w, h, col) {
        POP.ctx.fillStyle = col;
        POP.ctx.fillRect(x, y, w, h);
    },

    circle: function(x, y, r, col) {
        POP.ctx.fillStyle = col;
        POP.ctx.beginPath();
        POP.ctx.arc(x + 5, y + 5, r, 0,  Math.PI * 2, true);
        POP.ctx.closePath();
        POP.ctx.fill();
    },

    text: function(string, x, y, size, col) {
        POP.ctx.font = 'bold '+size+'px Monospace';
        POP.ctx.fillStyle = col;
        POP.ctx.fillText(string, x, y);
    }

};</code></pre>

Our <code>Draw</code> object has methods for clearing the screen and drawing rectangles, circles and text. The benefit of abstracting these operations is that we don’t have to remember the exact canvas API calls, and we can now draw a circle with one line of code, rather than five.

Let’s put it to the test:

<pre><code class="language-javascript">// include this at the end of POP.init function
POP.Draw.clear();
POP.Draw.rect(120,120,150,150, 'green');
POP.Draw.circle(100, 100, 50, 'rgba(255,0,0,0.5)');
POP.Draw.text('Hello World', 100, 100, 10, '#000');</code></pre>

Include the code above at the end of the <code>POP.init</code> function, and you should see a couple of shapes drawn to the canvas.</p>

## 3\. The Magic Touch

Just as we have the <code>click</code> event, mobile browsers provide methods for catching touch events.

The interesting parts of the code below are the <code>touchstart</code>, <code>touchmove</code> and <code>touchend</code> events. With the standard <code>click</code> event, we can get the coordinates from <code>e.pageX</code> and <code>e.pageY</code>. Touch events are slightly different. They contain a <code>touches</code> array, each element of which contains touch coordinates and other data. We only want the first touch, and we access it like so: <code>e.touches[0]</code>.

<strong>Note:</strong> Android provides JavaScript access to multi-touch actions only since version 4.

We also call <code>e.preventDefault();</code> when each event is fired to disable scrolling, zooming and any other action that would interrupt the flow of the game.

Add the following code to the <code>POP.init</code> function.

<pre><code class="language-javascript">// listen for clicks
window.addEventListener('click', function(e) {
    e.preventDefault();
    POP.Input.set(e);
}, false);

// listen for touches
window.addEventListener('touchstart', function(e) {
    e.preventDefault();
    // the event object has an array
    // named touches; we just want
    // the first touch
    POP.Input.set(e.touches[0]);
}, false);
window.addEventListener('touchmove', function(e) {
    // we're not interested in this,
    // but prevent default behaviour
    // so the screen doesn't scroll
    // or zoom
    e.preventDefault();
}, false);
window.addEventListener('touchend', function(e) {
    // as above
    e.preventDefault();
}, false);</code></pre>

You probably noticed that the code above passes the event data to an <code>Input</code> object, which we’ve yet to define. Let’s do that now:

<pre><code class="language-javascript">// + add this at the bottom of your code,
// before the window.addEventListeners
POP.Input = {

    x: 0,
    y: 0,
    tapped :false,

    set: function(data) {
        this.x = data.pageX;
        this.y = data.pageY;
        this.tapped = true;

        POP.Draw.circle(this.x, this.y, 10, 'red');
    }

};</code></pre>

Now, try it out. Hmm, the circles are not appearing. A quick scratch of the head and a lightbulb moment! Because we’ve scaled the canvas, we need to account for this when mapping the touch to the screen’s position.

First, we need to subtract the offset from the coordinates.

<pre><code class="language-javascript">var offsetTop = POP.canvas.offsetTop,
    offsetLeft = POP.canvas.offsetLeft;

this.x = data.pageX - offsetLeft;
this.y = data.pageY - offsetTop;</code></pre>

<img loading="lazy" decoding="async" class="131243" title="Offset Diagram" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c754e068-dd85-4ebd-82cb-5a5b14199627/offset-diagram.png" alt="Diagram showing canvas offset relative to the browser window" width="615" height="622" />

Then, we need to take into account the factor by which the canvas has been scaled so that we can plot to the actual canvas (which is still 320 × 480).

<pre><code class="language-javascript">var offsetTop = POP.canvas.offsetTop,
    offsetLeft = POP.canvas.offsetLeft;
    scale = POP.currentWidth / POP.WIDTH;

this.x = ( data.pageX - offsetLeft ) / scale;
this.y = ( data.pageY - offsetTop ) / scale;</code></pre>

<img loading="lazy" decoding="async" class="131244" title="Scaled Canvas Diagram" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb9dc91c-4238-4702-a84e-f8c60ebb53a7/scaled-canvas-diagram.png" alt="Difference between CSS scaled canvas and actual dimensions" width="500" height="750" />

If your head is starting to hurt, a practical example should provide some relief. Imagine the player taps the 500 × 750 canvas above at <code>400,400</code>. We need to translate that to 480 × 320 because, as far as the JavaScript is concerned, those are the dimensions of the canvas. So, the actual <code>x</code> coordinate is 400 divided by the scale; in this case, 400 ÷ 1.56 = 320.5.

Rather than calculating this on each touch event, we can calculate them after resizing. Add the following code to the start of the program, along with the other variable declarations:

<pre><code class="language-javascript">// let's keep track of scale
    // along with all initial declarations
    // at the start of the program
    scale:  1,
    // the position of the canvas
    // in relation to the screen
    offset = {top: 0, left: 0},</code></pre>

In our resize function, after adjusting the canvas’ width and height, we make note of the current scale and offset:

<pre><code class="language-javascript">// add this to the resize function.
POP.scale = POP.currentWidth / POP.WIDTH;
POP.offset.top = POP.canvas.offsetTop;
POP.offset.left = POP.canvas.offsetLeft;</code></pre>

Now, we can use them in the <code>set</code> method of our <code>POP.Input</code> class:

<pre><code class="language-javascript">this.x = (data.pageX - POP.offset.left) / POP.scale;
this.y = (data.pageY - POP.offset.top) / POP.scale;</code></pre>

## 4\. In The Loop

A typical game loop goes something like this:

1.  Poll user input,
2.  Update characters and process collisions,
3.  Render characters on the screen,
4.  Repeat.

We could, of course, use <code>setInterval</code>, but there’s a shiny new toy in town named <code>requestAnimationFrame</code>. It promises smoother animation and is more battery-efficient. The bad news is that it’s not supported consistently across browsers. But Paul Irish has come to the rescue with a <a href="https://paulirish.com/2011/requestanimationframe-for-smart-animating">handy shim</a>.

Let’s go ahead and add the shim to the start of our current code base.

<pre><code class="language-javascript">// https://paulirish.com/2011/requestanimationframe-for-smart-animating
// shim layer with setTimeout fallback
window.requestAnimFrame = (function(){
  return  window.requestAnimationFrame       ||
          window.webkitRequestAnimationFrame ||
          window.mozRequestAnimationFrame    ||
          window.oRequestAnimationFrame      ||
          window.msRequestAnimationFrame     ||
          function( callback ){
            window.setTimeout(callback, 1000 / 60);
          };
})();</code></pre>

And let’s create a rudimentary game loop:

<pre><code class="language-javascript">// Add this at the end of POP.init;
// it will then repeat continuously
POP.loop();

// Add the following functions after POP.init:

// this is where all entities will be moved
// and checked for collisions, etc.
update: function() {

},

// this is where we draw all the entities
render: function() {

   POP.Draw.clear();
},

// the actual loop
// requests animation frame,
// then proceeds to update
// and render
loop: function() {

    requestAnimFrame( POP.loop );

    POP.update();
    POP.render();
}</code></pre>

We call the loop at the end of <code>POP.init</code>. The <code>POP.loop</code> function in turn calls our <code>POP.update</code> and <code>POP.render</code> methods. <code>requestAnimFrame</code> ensures that the loop is called again, preferably at 60 frames per second. Note that we don’t have to worry about checking for input in our loop because we’re already listening for touch and click events, which is accessible through our <code>POP.Input</code> class.

The problem now is that our touches from the last step are immediately wiped off the screen. We need a better approach to remember what was drawn to the screen and where.</p>

## 5\. Spritely Will Do It

First, we add an entity array to keep track of all entities. This array will hold a reference to all touches, bubbles, particles and any other dynamic thing we want to add to the game.

<pre><code class="language-javascript">// put this at start of program
entities: [],</code></pre>

Let’s create a <code>Touch</code> class that draws a circle at the point of contact, fades it out and then removes it.

<pre><code class="language-javascript">POP.Touch = function(x, y) {

    this.type = 'touch';    // we'll need this later
    this.x = x;             // the x coordinate
    this.y = y;             // the y coordinate
    this.r = 5;             // the radius
    this.opacity = 1;       // initial opacity; the dot will fade out
    this.fade = 0.05;       // amount by which to fade on each game tick
    this.remove = false;    // flag for removing this entity. POP.update
                            // will take care of this

    this.update = function() {
        // reduce the opacity accordingly
        this.opacity -= this.fade;
        // if opacity if 0 or less, flag for removal
        this.remove = (this.opacity &lt; 0) ? true : false;
    };

    this.render = function() {
        POP.Draw.circle(this.x, this.y, this.r, 'rgba(255,0,0,'+this.opacity+')');
    };

};</code></pre>

The <code>Touch</code> class sets a number of properties when initiated. The x and y coordinates are passed as arguments, and we set the radius <code>this.r</code> to 5 pixels. We also set an initial opacity to 1 and the rate by which the touch fades to 0.05. There is also a <code>remove</code> flag that tells the main game loop whether to remove this from the entities array.

Crucially, the class has two main methods: <code>update</code> and <code>render</code>. We will call these from the corresponding part of our game loop.

We can then spawn a new instance of <code>Touch</code> in the game loop, and then move them via the update method:

<pre><code class="language-javascript">// POP.update function
update: function() {

    var i;

    // spawn a new instance of Touch
    // if the user has tapped the screen
    if (POP.Input.tapped) {
        POP.entities.push(new POP.Touch(POP.Input.x, POP.Input.y));
        // set tapped back to false
        // to avoid spawning a new touch
        // in the next cycle
        POP.Input.tapped = false;
    }

    // cycle through all entities and update as necessary
    for (i = 0; i &lt; POP.entities.length; i += 1) {
        POP.entities[i].update();

        // delete from array if remove property
        // flag is set to true
        if (POP.entities[i].remove) {
            POP.entities.splice(i, 1);
        }
    }

},</code></pre>

Basically, if <code>POP.Input.tapped</code> is <code>true</code>, then we add a new instance of <code>POP.Touch</code> to our entities array. We then cycle through the entities array, calling the <code>update</code> method for each entity. Finally, if the entity is flagged for removal, we delete it from the array.

Next, we render them in the <code>POP.render</code> function.

<pre><code class="language-javascript">// POP.render function
render: function() {

    var i;

   POP.Draw.rect(0, 0, POP.WIDTH, POP.HEIGHT, '#036');

    // cycle through all entities and render to canvas
    for (i = 0; i &lt; POP.entities.length; i += 1) {
        POP.entities[i].render();
    }

},</code></pre>

Similar to our update function, we cycle through the entities and call their <code>render</code> method to draw them to the screen.

So far, so good. Now we’ll add a <code>Bubble</code> class that will create a bubble that floats up for the user to pop.

<pre><code class="language-javascript">POP.Bubble = function() {

    this.type = 'bubble';
    this.x = 100;
    this.r = 5;                // the radius of the bubble
    this.y = POP.HEIGHT + 100; // make sure it starts off screen
    this.remove = false;

    this.update = function() {

        // move up the screen by 1 pixel
        this.y -= 1;

        // if off screen, flag for removal
        if (this.y &lt; -10) {
            this.remove = true;
        }

    };

    this.render = function() {

        POP.Draw.circle(this.x, this.y, this.r, 'rgba(255,255,255,1)');
    };

};</code></pre>

The <code>POP.Bubble</code> class is very similar to the <code>Touch</code> class, the main differences being that it doesn’t fade but moves upwards. The motion is achieved by updating the <code>y</code> position, <code>this.y</code>, in the update function. Here, we also check whether the bubble is off screen; if so, we flag it for removal.

<strong>Note:</strong> We could have created a base <code>Entity</code> class that both <code>Touch</code> and <code>Bubble</code> inherit from. But, I’d rather not open another can of worms about JavaScript prototypical inheritance versus classic at this point.

<pre><code class="language-javascript">// Add at the start of the program
// the amount of game ticks until
// we spawn a bubble
nextBubble: 100,

// at the start of POP.update
// decrease our nextBubble counter
POP.nextBubble -= 1;
// if the counter is less than zero
if (POP.nextBubble &lt; 0) {
    // put a new instance of bubble into our entities array
    POP.entities.push(new POP.Bubble());
    // reset the counter with a random value
    POP.nextBubble = ( Math.random() * 100 ) + 100;
}</code></pre>

Above, we have added a random timer to our game loop that will spawn an instance of <code>Bubble</code> at a random position. At the start of the game, we set <code>nextBubble</code> with a value of 100. This is subtracted on each game tick and, when it reaches 0, we spawn a bubble and reset the <code>nextBubble</code> counter.</p>

## 6\. Putting It Together

First of all, there is not yet any notion of collision detection. We can add that with a simple function. The math behind this is basic geometry, which you can <a href="https://mathworld.wolfram.com/Circle-CircleIntersection.html">brush up on at Wolfram MathWorld</a>.

<pre><code class="language-javascript">// this function checks if two circles overlap
POP.collides = function(a, b) {

        var distance_squared = ( ((a.x - b.x) * (a.x - b.x)) +
                                ((a.y - b.y) * (a.y - b.y)));

        var radii_squared = (a.r + b.r) * (a.r + b.r);

        if (distance_squared &lt; radii_squared) {
            return true;
        } else {
            return false;
        }
};

// at the start of POP.update, we set a flag for checking collisions
    var i,
        checkCollision = false; // we only need to check for a collision
                                // if the user tapped on this game tick

// and then incorporate into the main logic

if (POP.Input.tapped) {
    POP.entities.push(new POP.Touch(POP.Input.x, POP.Input.y));
    // set tapped back to false
    // to avoid spawning a new touch
    // in the next cycle
    POP.Input.tapped = false;
    checkCollision = true;

}

// cycle through all entities and update as necessary
for (i = 0; i &lt; POP.entities.length; i += 1) {
    POP.entities[i].update();

    if (POP.entities[i].type === 'bubble' &amp;&amp; checkCollision) {
        hit = POP.collides(POP.entities[i],
                            {x: POP.Input.x, y: POP.Input.y, r: 7});
        POP.entities[i].remove = hit;
    }

    // delete from array if remove property
    // is set to true
    if (POP.entities[i].remove) {
        POP.entities.splice(i, 1);
    }
}</code></pre>

The bubbles are rather boring; they all travel at the same speed on a very predictable trajectory. Making the bubbles travel at random speeds is a simple task:

<pre><code class="language-javascript">POP.Bubble = function() {

    this.type = 'bubble';
    this.r = (Math.random() * 20) + 10;
    this.speed = (Math.random() * 3) + 1;

    this.x = (Math.random() * (POP.WIDTH) - this.r);
    this.y = POP.HEIGHT + (Math.random() * 100) + 100;

    this.remove = false;

    this.update = function() {

        this.y -= this.speed;

    // the rest of the class is unchanged</code></pre>

And let’s make them oscillate from side to side, so that they are harder to hit:

<pre><code class="language-javascript">// the amount by which the bubble
    // will move from side to side
    this.waveSize = 5 + this.r;
    // we need to remember the original
    // x position for our sine wave calculation
    this.xConstant = this.x;

    this.remove = false;

    this.update = function() {

        // a sine wave is commonly a function of time
        var time = new Date().getTime() * 0.002;

        this.y -= this.speed;
        // the x coordinate to follow a sine wave
        this.x = this.waveSize * Math.sin(time) + this.xConstant;

    // the rest of the class is unchanged</code></pre>

Again, we’re using some basic geometry to achieve this effect; in this case, a sine wave. While you don’t need to be a math whiz to make games, basic understanding goes a long way. The article “<a href="https://www.smashingmagazine.com/2011/10/04/quick-look-math-animations-javascript/">A Quick Look Into the Math of Animations With JavaScript</a>” should get you started.

Let’s also show some statistics on screen. To do this, we will need to track various actions throughout the game.

Put the following code, along with all of the other variable declarations, at the beginning of the program.

<pre><code class="language-javascript">// this goes at the start of the program
// to track players's progress
POP.score = {
    taps: 0,
    hit: 0,
    escaped: 0,
    accuracy: 0
},</code></pre>

Now, in the <code>Bubble</code> class we can keep track of <code>POP.score.escaped</code> when a bubble goes off screen.

<pre><code class="language-javascript">// in the bubble class, when a bubble makes it to
// the top of the screen
    if (this.y &lt; -10) {
        POP.score.escaped += 1; // update score
        this.remove = true;
    }</code></pre>

In the main update loop, we increase <code>POP.score.hit</code> accordingly:

<pre><code class="language-javascript">// in the update loop
if (POP.entities[i].type === 'bubble' &amp;&amp; checkCollision) {
    hit = POP.collides(POP.entities[i],
                        {x: POP.Input.x, y: POP.Input.y, r: 7});
    if (hit) {
        POP.score.hit += 1;
    }

    POP.entities[i].remove = hit;
}</code></pre>

In order for the statistics to be accurate, we need to record all of the taps the user makes:

<pre><code class="language-javascript">// and record all taps
if (POP.Input.tapped) {
    // keep track of taps; needed to
    // calculate accuracy
    POP.score.taps += 1;</code></pre>

Accuracy is obtained by dividing the number of hits by the number of taps, multiplied by 100, which gives us a nice percentage. Note that <code>~~(POP.score.accuracy)</code> is a quick way (i.e. a hack) to round floats down to integers.

<pre><code class="language-javascript">// Add at the end of the update loop
// to calculate accuracy
POP.score.accuracy = (POP.score.hit / POP.score.taps) * 100;
POP.score.accuracy = isNaN(POP.score.accuracy) ?
    0 :
    ~~(POP.score.accuracy); // a handy way to round floats</code></pre>

Lastly, we use our <code>POP.Draw.text</code> to display the scores in the main update function.

<pre><code class="language-javascript">// and finally in the draw function
POP.Draw.text('Hit: ' + POP.score.hit, 20, 30, 14, '#fff');
POP.Draw.text('Escaped: ' + POP.score.escaped, 20, 50, 14, '#fff');
POP.Draw.text('Accuracy: ' + POP.score.accuracy + '%', 20, 70, 14, '#fff');</code></pre>

## 7\. Spit And Polish

There’s a common understanding that a playable demo can be made in a couple of hours, but a polished game takes days, week, months or even years!

We can do a few things to improve the visual appeal of the game.</p>

### Particle Effects

Most games boast some form of particle effects, which are great for explosions. What if we made a bubble explode into many tiny bubbles when it is popped, rather than disappear instantly?

Take a look at our <code>Particle</code> class:

<pre><code class="language-javascript">POP.Particle = function(x, y,r, col) {

    this.x = x;
    this.y = y;
    this.r = r;
    this.col = col;

    // determines whether particle will
    // travel to the right of left
    // 50% chance of either happening
    this.dir = (Math.random() * 2 &gt; 1) ? 1 : -1;

    // random values so particles do not
    // travel at the same speeds
    this.vx = ~~(Math.random() * 4) * this.dir;
    this.vy = ~~(Math.random() * 7);

    this.remove = false;

    this.update = function() {

        // update coordinates
        this.x += this.vx;
        this.y += this.vy;

        // increase velocity so particle
        // accelerates off screen
        this.vx *= 0.99;
        this.vy *= 0.99;

        // adding this negative amount to the
        // y velocity exerts an upward pull on
        // the particle, as if drawn to the
        // surface
        this.vy -= 0.25;

        // off screen
        if (this.y &lt; 0) {
            this.remove = true;
        }

    };

    this.render = function() {
        POP.Draw.circle(this.x, this.y, this.r, this.col);
    };

};</code></pre>

It’s fairly obvious what is going on here. Using some basic acceleration so that the particles speed up as the reach the surface is a nice touch. Again, this math and physics are beyond the scope of this article, but for those interested, Skookum Digital Works explains it in depth.

To create the particle effect, we push several particles into our <code>entities</code> array whenever a bubble is hit:

<pre><code class="language-javascript">// modify the main update function like so:
if (hit) {
    // spawn an explosion
    for (var n = 0; n &lt; 5; n +=1 ) {
        POP.entities.push(new POP.Particle(
            POP.entities[i].x,
            POP.entities[i].y,
            2,
            // random opacity to spice it up a bit
            'rgba(255,255,255,'+Math.random()*1+')'
        ));
    }
    POP.score.hit += 1;
}</code></pre>

### Waves

Given the underwater theme of the game, adding a wave effect to the top of the screen would be a nice touch. We can do this by drawing a number of overlapping circles to give the illusion of waves:

<pre><code class="language-javascript">// set up our wave effect;
// basically, a series of overlapping circles
// across the top of screen
POP.wave = {
    x: -25, // x coordinate of first circle
    y: -40, // y coordinate of first circle
    r: 50, // circle radius
    time: 0, // we'll use this in calculating the sine wave
    offset: 0 // this will be the sine wave offset
};
// calculate how many circles we need to
// cover the screen's width
POP.wave.total = Math.ceil(POP.WIDTH / POP.wave.r) + 1;</code></pre>

Add the code above to the <code>POP.init</code> function. <code>POP.wave</code> has a number of values that we’ll need to draw the waves.

Add the following to the main update function. It uses a sine wave to adjust the position of the waves and give the illusion of movement.

<pre><code class="language-javascript">// update wave offset
// feel free to play with these values for
// either slower or faster waves
POP.wave.time = new Date().getTime() * 0.002;
POP.wave.offset = Math.sin(POP.wave.time * 0.8) * 5;</code></pre>

All that’s left to be done is to draw the waves, which goes into the render function.

<pre><code class="language-javascript">// display snazzy wave effect
for (i = 0; i &lt; POP.wave.total; i++) {

    POP.Draw.circle(
                POP.wave.x + POP.wave.offset +  (i * POP.wave.r),
                POP.wave.y,
                POP.wave.r,
                '#fff');
}</code></pre>

Here, we’ve reused our sine wave solution for the bubbles to make the waves move gently to and fro. Feeling seasick yet?

## Final Thoughts

Phew! That was fun. Hope you enjoyed this short forage into tricks and techniques for making an HTML5 game. We’ve managed to create a very simple game that works on most smartphones as well as modern browsers. Here are some things you could consider doing:

*   Store high scores using local storage.
*   Add a splash screen and a “Game over” screen.
*   Enable power-ups.
*   Add audio. Contrary to what I said at the beginning of this article, this isn’t impossible, just a bit of a headache. One technique is to use audio sprites (kind of like CSS image sprites); [Remy Sharp breaks it down](https://remysharp.com/2010/12/23/audio-sprites/).
*   Let your imagination run wild!

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Rebuilding An HTML5 Game In Unity](https://www.smashingmagazine.com/2014/04/rebuilding-an-html5-game-in-unity/)
*   [What Web Designers Can Learn From Video Games](https://www.smashingmagazine.com/2011/07/what-web-designers-can-learn-from-video-games/)
*   [Email Marketing For Mobile App Creators](https://www.smashingmagazine.com/2013/08/email-marketing-for-mobile-app-creators/)
*   [Finger-Friendly Design: Ideal Mobile Touchscreen Target Sizes](https://www.smashingmagazine.com/2012/02/finger-friendly-design-ideal-mobile-touchscreen-target-sizes/)

If you are interested in further exploring the possibilities of mobile HTML5 games, I recommend test-driving a couple of frameworks to see what works for you. Juho Vepsäläinen offers a <a href="https://github.com/bebraw/jswiki/wiki/Game-Engines">useful summary of most game engines</a>. If you’re willing to invest a little cash, then <a href="https://impactjs.com">Impact</a> is a great starting point, with thorough documentation and lively helpful forums. And the impressive <a href="https://www.chromeexperiments.com/detail/x-type/">X-Type</a> demonstrates what is possible. Not bad, eh?

<em>(al) (jc)</em>


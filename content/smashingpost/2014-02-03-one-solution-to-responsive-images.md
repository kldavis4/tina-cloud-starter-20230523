---
title: One Solution To Responsive Images
slug: one-solution-to-responsive-images
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b3d6c1f-6d8b-41c8-8497-fc0f6a62a499/dinner-2013-showcase-by-gavmcksnow-639x1024.jpg
date: 2014-02-03T12:27:47.000Z
author: gavyn-mckenzie
description: >-
  Responsive images have been, and are, one of the hardest problems in
  responsive Web design right now. **Until browser vendors have a native
  solution**, we have to think on the fly and come up with our own solutions.
  “Retina” images are especially a challenge because if you have sized your
  layout with ems or percentages (as you should!), then you cannot be sure of
  the exact pixel dimensions of each image being displayed.
categories:
  - Mobile
  - Techniques
  - Optimization
  - Responsive Design
---
Responsive images have been, and are, one of the hardest problems in responsive Web design right now. <strong>Until browser vendors have a native solution</strong>, we have to think on the fly and come up with our own solutions. “Retina” images are especially a challenge because if you have sized your layout with ems or percentages (as you should!), then you cannot be sure of the exact pixel dimensions of each image being displayed.

In this article, we’ll look at one solution to the problem that we implemented on our portfolio website at <a title="Etch Apps" href="https://etchapps.com">Etch</a>, where you can see an early working version in the wild.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Choosing A Responsive Image Solution](https://www.smashingmagazine.com/2013/07/choosing-a-responsive-image-solution/)
*   [Responsive Images Done Right: A Guide To <picture> And srcset](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/)
*   [Leaner Responsive Images With Client Hints](https://www.smashingmagazine.com/2016/01/leaner-responsive-images-client-hints/)
*   [Simple Responsive Images With CSS Background Images](https://www.smashingmagazine.com/2013/07/simple-responsive-images-with-css-background-images/)

## Requirements For Responsive Images

We used a <a title="Jeremy Keith blog post on content first" href="https://adactio.com/journal/4523/">content-first</a> approach on Etch. We knew we wanted to use a lot of images to quickly convey the atmosphere of the company. These would be accompanied by small snippets, or “soundbites,” of text.

{{% feature-panel %}}

The next decision was on image sizes and aspect ratios. To get maximum control over the design, we knew we needed maximum control over the images. We decided to use Instagram as the base for our imagery for the following reasons:

*   The aspect ratio is fixed.
*   Most employees here already use it.
*   Those lovely filters.

Instagram allows for a maximum image size of 600 pixels, so we now had our first set of content constraints to work with: images with a 1:1 aspect ratio, and a maximum image size of 600 × 600. Having constraints on the content side made the design process easier because they limited our options, thus forcing decisions.

When the content was completed, we began looking at the design. Again, to keep maximum control, we decided on an adaptive design style with fixed column sizes. We used grid block elements that match our maximum image size. Each grid block would either be 600 × 600 or 300 × 300, which also conveniently fit our rough plan of a minimum width of 320 pixels for the viewport on the website.

During the rest of the design process, we noticed that we needed two other image sizes: thumbnails at 100 × 100, and hero images that stretch the full width of the content (300, 600, 900, 1200, 1600, 1800). All images would also need to be “Retina” ready — or, to put it another way, compatible with displays with high pixel densities. This gave us the final set of requirements for a responsive images solution for the website:

*   Potential image widths (in pixels) of 100, 300, 600, 900, 1200, 1600, 1800
*   Retina ready
*   Must be crisp with minimal resizing (some people notice a drop in quality with even downsized images)

Having to resize that many images manually, even using a Photoshop script, seemed like too much work. Anything like that should be automated, so that you can focus on fun and interesting coding instead. Automation also removes the chance for human error, like forgetting to do it. The ideal solution would be for us to add an image file once and forget about it.</p>

## Common Solutions

Before going over our solution, let’s look at some common solutions currently being used. To keep up with currently popular methods and the work that the Web community is doing to find a solution to responsive images, head over to the <a title="W3C Responsive Images" href="https://www.w3.org/community/respimg/wiki/Main_Page">W3C Responsive Images Community Group</a>.</p>

### Picture Element

First up, the <a title="Further info on the picture element" href="https://picture.responsiveimages.org/">picture</a> element. While this doesn’t currently have native support and browser vendors are still deciding on <code>picture</code> versus <code>srcset</code> versus whatever else is up for discussion, we can use it with a polyfill.

<pre><code class="language-markup">
&lt;picture alt="description"&gt;
  &lt;source src="small.jpg"&gt;
  &lt;source src="medium.jpg" media="(min-width: 40em)"&gt;
  &lt;source src="large.jpg" media="(min-width: 80em)"&gt;
&lt;/picture&gt;
</code></pre>

The <code>picture</code> element is great if you want to serve images with a different shape, focal point or other feature beyond just resizing. However, you’ll have to presize all of the different images to be ready to go straight in the HTML. This solution also couples HTML with media queries, and we know that coupling CSS to HTML is bad for maintenance. This solution also doesn’t cover high-definition displays

For this project, the <code>picture</code> element required too much configuration and manual creation and storage of the different image sizes and their file paths.</p>

### srcset

Another popular solution, srcset, has recently been made available natively in some WebKit-based browsers. At the time of creating our plugin, this wasn’t available, and it looks like we’ll be waiting a while longer until cross-browser compatibility is good enough to use it without a JavaScript fallback. At the time of writing, <code>srcset</code> is usable only in the Chrome and Safari nightly builds.

<pre><code class="language-markup">
&lt;img src="fallback.jpg" srcset="small.jpg 640w 1x, small-hd.jpg 640w 2x, large.jpg 1x, large-hd.jpg 2x" alt="…"&gt;
</code></pre>

The snippet above shows <code>srcset</code> in use. Again, we see what essentially amounts to media queries embedded in HTML, which really bugs me. We’d also need to create different image sizes before runtime, which means either setting up a script or manually doing it, a tiresome job.</p>

### Server-Side Sniffing

If you’d rather not use JavaScript to decide which image to serve, you could try sniffing out the user agent server-side and automatically send an appropriately sized image. As a blanket rule, we almost always say don’t rely on server-side sniffing. It’s very unreliable, and many browsers contain inaccurate UA strings. On top of that, the sheer number of new devices and screen sizes coming out every month will lead you to maintenance hell.</p>

### Other Solutions in the Wild

We chose to make our own plugin because including layout code in the HTML seemed undesirable and having to create different image sizes beforehand was not enticing.

If you’d like to explore other common solutions to decide which is best for your project, several great articles and examples are available on the Web, including one on this very website.

*   “[Choosing a Responsive Image Solution](https://www.smashingmagazine.com/2013/07/08/choosing-a-responsive-image-solution/),” Sherri Alexander, Smashing Magazine Alexander looks at the high-level requirements for responsive images, and then dissects the variety of solutions currently available in the wild.
*   “[Which Responsive Image Solution Should You Use](https://css-tricks.com/which-responsive-images-solution-should-you-use/),” Chris Coyier, CSS-Tricks Coyer takes us through imaging requirements while suggesting appropriate solutions.
*   [Adaptive Images](https://adaptive-images.com/) A solution very similar to Etch’s in its implementation. It uses a PHP script to size and serve the appropriate images. Unfortunately, this wasn’t available when we were coding the website.
*   [Picturefill](https://www.sitepoint.com/responsive-images-using-picturefill-php/) This is a JavaScript replacement for markup in the style of the `picture` element.
*   “[Responsive Images Using Cookies](https://blog.keithclark.co.uk/responsive-images-using-cookies/),” Keith Clark Clark uses a cookie to store the screen’s size, and then images are requested via a PHP script. Again, it’s similar to our solution but wasn’t available at the time.

Onto our solution.

## Our Solution

With both <code>picture</code> and <code>srcset</code> HTML syntaxes seeming like too much effort in the wrong places, we looked for a simpler solution. We wanted to be able to add a single image path and let the CSS, JavaScript and PHP deal with serving the correct image — instead of the HTML, which should simply have the correct information in place.

At the time of developing the website, no obvious solution matched our requirements. Most centered on emulating <code>picture</code> or <code>srcset</code>, which we had already determined weren’t right for our needs.

The Etch website is very image-heavy, which would make manually resizing each image a lengthy process and prone to human error. Even running an automated Photoshop script was deemed to require too much maintenance.

Our solution was to find the display width of the image with JavaScript at page-loading time, and then pass the <code>src</code> and <code>width</code> to a PHP script, which would resize and cache the images on the fly before inserting them back into the DOM.

We’ll look at an abstracted example of the code, written in HTML, JavaScript, PHP and LESS. You can find a <a title="Demo" href="https://gavyn-mckenzie.co.uk/examples/resize/">working demo</a> on my website. If you’d like to grab the files for the demo, they can be found <a href="https://github.com/gavmck/resize">on GitHub</a>.</p>

## Markup

The markup for the demo can be found in the <code>index.html</code> <a href="https://github.com/gavmck/resize/blob/master/index.html">file on GitHub</a>.

We wrap the highest-resolution version of an image in <code>noscript</code> tags, for browsers with JavaScript turned off. The reason is that, if we think of performance as a feature and JavaScript as an enhancement, then non-JavaScript users would still receive the content, just not an optimized experience of that content. These <code>noscript</code> elements are then wrapped in a <code>div</code> element, with the image’s <code>src</code> and <code>alt</code> properties as data attributes. This provides the information that the JavaScript needs to send to the server.

<pre><code class="language-markup">
&lt;div data-src="img/screen.JPG" data-alt="crispy" class="img-wrap js-crispy"&gt;
    &lt;noscript&gt;&lt;img src="img/screen.JPG" alt="Crispy"&gt;&lt;/noscript&gt;
&lt;/div&gt;
</code></pre>

The background of the image wrapper is set as a loading GIF, to show that the images are still loading and not just broken.

An alternative (which we used in one of our side projects, <a title="PhoSho Instagram Galleries" href="https://phosho.co">PhoSho</a>) is to use the lowest-resolution size of the image that you will be displaying (if known), instead of the loading GIF. This takes slightly more bandwidth because more than one image is being loaded, but it has an appearance similar to that of progressive JPEGs as the page is loading. As always, see what your requirements dictate.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/432e90cd-5b24-42ad-b7d0-f5d99a761a2a/dinner-2013-large-opt.jpg"><img class="aligncenter wp-image-140893 size-large" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9cbc84f-547a-4035-8165-5143807757a3/dinner-2013-showcase-by-gavmcksnow-639x1024.jpg" alt="responsive images" width="500" height="801" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/432e90cd-5b24-42ad-b7d0-f5d99a761a2a/dinner-2013-large-opt.jpg">Large preview</a>)</em>

## JavaScript

The JavaScript communicates for us between the HTML and the server. It fetches an array of images from the DOM, with their corresponding widths, and retrieves the appropriate cached image file from the server.

Our original plugin sent one request to the server per image, but this caused a lot of extra requests. By bundling our images together as an array, we cut down the requests and kept the server happy.

You can find the <a href="https://github.com/gavmck/resize/blob/master/js/resize.js">JavaScript plugin</a> in <code>/js/resize.js</code> in the GitHub repository.

First, we set an array of breakpoints in the plugin that are the same as the breakpoints in the CSS where the image sizes change. We used em values for the breakpoints because they are based on the display font size. This is a good practice because visually impaired users might change their display’s default font size. This also makes it easier to match our CSS breakpoints with the JavaScript ones. If you prefer, the plugin works just fine with pixel-based breakpoints.

<pre><code class="language-coffeescript">
breakpoints: [
    "32em"
    "48em"
    "62em"
    "76em"
]
</code></pre>

As we pass each of these breakpoints, we need to check the images to make sure they are the correct size. At page-loading time, we first set the current breakpoint being displayed to the user using the JavaScript <code>matchMedia</code> function. If you need to support old browsers (Internet Explorer 7, 8 and 9), you might require the <a title="matchMedia polyfill on github" href="https://github.com/paulirish/matchMedia.js/">matchMedia polyfill</a> by Paul Irish.

<pre><code class="language-javascript">
getCurrentBreakpoint: function() {
      var bp, breakpoint, _fn, _i, _len, _ref,
        _this = this;

      bp = this.breakpoints[0];

      _ref = this.breakpoints;

      _fn = function(breakpoint) {
        // Check if the breakpoint passes
        if (window.matchMedia &amp;&amp; window.matchMedia("all and (min-width: " + breakpoint + ")").matches) {
          return bp = breakpoint;
        }
      };

      for (_i = 0, _len = _ref.length; _i &lt; _len; _i++) {
        breakpoint = _ref[_i];
        _fn(breakpoint);
      }

      return bp;
    }
</code></pre>

After setting the current breakpoint, we gather the images to be resized from the DOM by looping through them and adding them to the plugin’s <code>images</code> array.

<pre><code class="language-javascript">
gather: function() {
      var el, els, _i, _len;

      els = $(this.els);

      this.images = [];

      for (_i = 0, _len = els.length; _i &lt; _len; _i++) {
        el = els[_i];
        this.add(el);
      }

      this.grabFromServer();
    }
</code></pre>

The PHP script on the server needs the image’s <code>src</code> and current width in order to resize it correctly, so we created some serialized <code>POST</code> data to send to the server. We use jQuery’s <code>param</code> method to quickly convert the image into a usable query string.

<pre><code class="language-javascript">
buildQuery: function() {
      var image = { image: this.images }
      return $.param(image);
    }
</code></pre>

The images are then sent via an AJAX request to the server to be resized. Note the single request, to minimize server load.

<pre><code class="language-javascript">
grabFromServer: function() {
      var data,
        _this = this;

      data = this.buildQuery();

      $.get("resize.php", data, function(data) {
          var image, _i, _len;
          for (_i = 0, _len = data.length; _i &lt; _len; _i++) {
            image = data[_i];
            _this.loadImage(image);
          }
        }
      );
    }
</code></pre>

Once we have retrieved the images from the server, we can add them to the DOM or replace the image already in place if it has changed. If it’s the same image, then nothing happens and the image won’t need to be redownloaded because it’s already in the browser’s cache.

<pre><code class="language-javascript">
loadImage: function(image) {
      var el, img,
        _this = this;

      el = $("[data-src='" + image.og_src + "']");

      img = $("<img />");

      img.attr("src", image.src).attr("alt", el.attr("data-alt"));

      if (el.children("img").length) {
        el.children("img").attr("src", image.src);
      } else {
        img.load(function() {
          el.append(img);
          el.addClass('img-loaded');
        });
      }
    }
</code></pre>

## PHP

With the JavaScript simply requesting an array of images at different sizes, the PHP is where the bulk of the action happens.

We use two scripts. One is a <a href="https://github.com/gavmck/resize/blob/master/php/lib/resize-class.php"><code>resize</code> class</a> (found in <code>/php/lib/resize-class.php</code> in the demo), which creates cached versions of the image at the sizes we need. The <a href="https://github.com/gavmck/resize/blob/master/resize.php">other script</a> sits in the Web root, calculates the most appropriate size to display, and acts as an interface between the JavaScript and the resizer.

Starting with the sizing and interface script, we first set an array of pixel sizes of the images that we expect to display, as well as the path to the cached images folder. The image sizes are in pixels because the server doesn’t know anything about the user’s current text-zoom level, only what the physical image sizes being served are.

<pre><code class="language-php">
$sizes = array(
    '100',
    '300',
    '600',
    '1200',
    '1500',
);

$cache = 'img/cache/';
</code></pre>

Next, we create a small function that returns the image size closest to the current display size.

<pre><code class="language-php">
function closest($search, $arr) {
    $closest = null;
    foreach($arr as $item) {
        // distance from image width -&gt; current closest entry is greater than distance from  
        if ($closest == null || abs($search - $closest) &gt; abs($item - $search)) {
            $closest = $item;
        }
    }
    $closest = ($closest == null) ? $closest = $search : $closest;
    return $closest;
}
</code></pre>

Finally, we can loop through the image paths posted to the script and pass them to the <code>resize</code> class to get the path to the cached image file (and create that file, if necessary).

<pre><code class="language-php">
$crispy = new resize($image,$width,$cache);
$newSrc = $crispy-&gt;resizeImage();
</code></pre>

We return the original image path in order to find the image again in the DOM and the path to the correctly sized cached image file. All of the image paths are sent back as an array so that we can loop through them and add them to the HTML.

<pre><code class="language-php">
$images[] =  array('og_src' =&gt; $src, 'src' =&gt; '/'.$newSrc);
</code></pre>

In the <code>resize</code> class, we initially need to gather some information about the image for the resizing process. We use <code>Exif</code> to determine the type of image because the file could possibly have an incorrect extension or no extension at all.

<pre><code class="language-php">
function __construct($fileName, $width, $cache) {

    $this-&gt;src = $fileName;
    $this-&gt;newWidth = $width;
    $this-&gt;cache = $cache;
    $this-&gt;path = $this-&gt;setPath($width);

    $this-&gt;imageType = exif_imagetype($fileName);

    switch($this-&gt;imageType)
    {
        case IMAGETYPE_JPEG:
            $this-&gt;path .= '.jpg';
            break;

        case IMAGETYPE_GIF:
            $this-&gt;path .= '.gif';
            break;

        case IMAGETYPE_PNG:
            $this-&gt;path .= '.png';
            break;

        default:
            // *** Not recognized
            break;
    }
}
</code></pre>

The <code>$this-&gt;path</code> property above, containing the cached image path, is set using a combination of the display width, a hash of the file’s last modified time and <code>src</code>, and the original file name.

Upon calling the <code>resizeImage</code> method, we check to see whether the path set in <code>$this-&gt;path</code> already exists and, if so, we just return the cached file path.

If the file does not exist, then we open the image with GD to be resized.

Once it’s ready for use, we calculate the width-to-height ratio of the original image and use that to give us the height of the cached image after having been resized to the required width.

<pre><code class="language-php">
if ($this-&gt;image) {
    $this-&gt;width  = imagesx($this-&gt;image);
    $this-&gt;height = imagesy($this-&gt;image);
}

$ratio = $this-&gt;height/$this-&gt;width;
$newHeight = $this-&gt;newWidth*$ratio;
</code></pre>

Then, with GD, we resize the original image to the new dimensions and return the path of the cached image file to the interface script.

<pre><code class="language-php">
$this-&gt;imageResized = imagecreatetruecolor($this-&gt;newWidth, $newHeight);
imagecopyresampled($this-&gt;imageResized, $this-&gt;image, 0, 0, 0, 0, $this-&gt;newWidth, $newHeight, $this-&gt;width, $this-&gt;height);

$this-&gt;saveImage($this-&gt;newWidth);

return $this-&gt;path;
</code></pre>

## What Have We Achieved?

This plugin enables us to have one single batch of images for the website. We don’t have to think about how to resize images because the process is automated. This makes maintenance and updates much easier, and it removes a layer of thinking that is better devoted to more important tasks. Plug it in once and forget about it.

<abbr title="Too long, didn't read">TL;DR</abbr>? Let’s summarize the functionality once more for good measure.

In our markup, we provide an image wrapper that contains a <code>&lt;noscript&gt;</code> fallback. This wrapper has a data attribute of our original high-resolution image for a reference. We use JavaScript to send an AJAX request to a PHP file on the server, asking for the correctly sized version of this image. The PHP file either resizes the image and delivers the path of the correctly sized image or just returns the path if the image has already been created. Once the AJAX request has been completed, we append the new image to the DOM, or we just update the <code>src</code> if one has already been added. If the user resizes their browser, then we check again to see whether a better image size should be used.</p>

## Pros And Cons

All responsive image solutions have their pros and cons, and you should investigate several before choosing one for your project. Ours happens to work for our very specific set of requirements, and it wouldn’t be our default solution. As far as we can tell, there is no default solution at the moment, so we’d recommend trying out as many as possible.

How does this solution weigh up?

### Pros

*   Fast initial page download due to lower image weight
*   Easy to use once set up
*   Low maintenance
*   Fast once cached files have been created
*   Serves image at correct pixel size (within tolerance)
*   Serves new image when display size changes (within tolerance)

### Cons

*   Unable to choose image focus area
*   Requires PHP and JavaScript for full functionality
*   Can’t cover all possible image sizes if fluid images are used
*   Might not be compatible with some content management systems
*   Resizing all images with one request means that, with an empty cache, you have to wait for all to be resized, rather than just one image
*   The PHP script is tied to breakpoints, so it can’t be dropped in without tweaking

Responsive image solutions have come a long way in recent months, and if we had to do this again, we’d probably look at something like the <a href="https://adaptive-images.com">adaptive images</a> solution because it removes even more non-semantic HTML from the page by modifying <code>.htaccess</code>.</p>

## Wrapping Up

Until we have a native solution for responsive images, there will be no “right” way. Always investigate several options before settling on one for your project. The example here works well for websites with a few common display sizes for images across breakpoints, but it is by no means the definitive solution. Until then, why not have a go at creating your own solution, or play around with this one <a title="Resize on GitHub" href="https://github.com/gavmck/resize">on GitHub</a>?

{{< signature "al, il" >}}

<em>SmashingMag front page image credits: <a href="https://phosho.co/">PhoSho's front page showcase</a>.</em>


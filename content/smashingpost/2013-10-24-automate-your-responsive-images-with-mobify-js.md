---
title: Automate Your Responsive Images With Mobify.js
slug: automate-your-responsive-images-with-mobify-js
image: null
date: 2013-10-24T10:04:32.000Z
author: shawn-jansepar
description: >-
  Responsive images are one of the biggest sources of frustration in the Web
  development community. With good reason, too: The average size of pages has
  grown from 1 MB to a staggering 1.5 MB in the last year alone. Images account
  for more than 60% of that growth, and this percentage will only go up.
categories:
  - Mobile
  - Workflow
  - JavaScript
  - Techniques
  - Responsive Design
---
Responsive images are one of the biggest sources of frustration in the Web development community. With good reason, too: The average size of pages has <a href="https://www.webperformancetoday.com/2013/06/05/web-page-growth-2010-2013/">grown from 1 MB to a staggering 1.5 MB</a> in the last year alone. Images account for more than 60% of that growth, and this <a href="https://httparchive.org/trends.php">percentage will only go up</a>.

<img title="Automate Your Responsive Images With Mobify.js" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f6e22a5-d029-400c-956b-f1520e4ec1fc/manage-measure-mini.png" alt="Automate Your Responsive Images With Mobify.js" width="500" height="337" />

<strong>Much of that page weight could be reduced</strong> if images were conditionally optimized based on device width, pixel density and modern image formats (such as <a href="https://developers.google.com/speed/webp/">WebP</a>). These reductions would result in faster loading times and in users who are more engaged and who would stick around longer. But the debate isn't about whether to optimize images for different devices, but about how to go about doing so.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Simple Responsive Images With CSS Background Images](https://www.smashingmagazine.com/2013/07/simple-responsive-images-with-css-background-images/)
*   [How To Solve Adaptive Images In Responsive Web Design](https://www.smashingmagazine.com/2013/06/clown-car-technique-solving-for-adaptive-images-in-responsive-web-design/)
*   [<span class="headline">Automatically Art-Directed Responsive Images?</span>](https://www.smashingmagazine.com/2016/02/automatically-art-directed-responsive-images-go/)
*   [Responsive Images In WordPress With Art Direction](https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/)

{{% feature-panel %}}

In an ideal world, we would continue using the <code>img</code> tag, and the browser would download exactly what it needs based on the width of the device and the layout of the page. However, no functionality like that currently exists. One way to get functionality similar to that would be to change the <code>src</code> attribute of <code>img</code> elements on the fly with JavaScript, but the <a href="https://blog.cloudfour.com/the-real-conflict-behind-picture-and-srcset/">lookahead pre-parser (or preloader) prevents this</a> from being a viable option.

The first step to overcoming this problem is to create a markup-based solution that allows for alternate image sources to be delivered based on a device’s capabilities. This was solved with the <a href="https://www.w3.org/community/respimg/">introduction of the <code>picture</code> element</a>, created by the W3C Responsive Images Community Group (although no browser currently implements it natively).

However, the <code>picture</code> element introduces a whole new problem: Developers must now generate a separate asset for every image at every breakpoint. What developers really need is <strong>a solution that automatically generates small images for small devices</strong> from a single high-resolution image. Ideally, this automated solution would make only one request per image and would be 100% semantic and backwards-compatible. The Image API in <a href="https://www.mobify.com/mobifyjs/v2/docs/image-resizer/">Mobify.js</a> provides that solution.</p>

## The <picture> Element As The Upcoming Best Practice

The <code>picture</code> element is currently the <a href="https://timkadlec.com/2012/05/wtfwg/">frontrunner to replace the <code>img</code> element</a> because it enables developers to specify different images for different screen resolutions in order to solve the problem of both performance and <a href="https://www.yoav.ws/2013/05/How-Big-Is-Art-Direction">art direction</a> (although the new <a href="https://lists.w3.org/Archives/Public/public-respimg/2013Sep/0087.html">srcN proposal</a> is worth looking into). The typical set-up involves <a href="https://blog.cloudfour.com/sensible-jumps-in-responsive-image-file-sizes/">defining breakpoints</a>, generating images for each breakpoint and then writing the <code>picture</code> markup for the image. Let's see how we can make the following image responsive using a workflow that includes the <code>picture</code> element:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2baad559-7b94-4ccb-9bcf-fd9372e371ad/president-barack-obama-tours-storm-damage-in-new-jersey-2-opt.jpg"><img loading="lazy" decoding="async" class="137482" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1d3fd73-8c3d-472f-b12c-dcbcab09c0f6/responsive-obama-500-opt.jpg" alt="President Obama and Governor Christi" width="500" /></a>

We'll use a baseline of <a href="https://blog.cloudfour.com/how-do-you-pick-responsive-images-breakpoints/comment-page-1/#comment-14803">320, 512, 1024 and 2048</a> pixels.

First, we need to generate a copy of each image for those different resolutions, either by using a command-line interface (CLI) tool such as <a href="https://github.com/toy/image_optim">Image Optim</a> or by saving them with Photoshop's “Save for web” feature. Then, we would use the following markup:

<pre><code class="language-markup">
&lt;picture&gt;
    &lt;source src="responsive-obama-320.png"&gt;
    &lt;source src="responsive-obama-512.png" media="(min-width: 512px)"&gt;
    &lt;source src="responsive-obama-1024.png" media="(min-width: 1024px)"&gt;
    &lt;source src="responsive-obama-2048.png" media="(min-width: 2048px)"&gt;
    &lt;noscript&gt;&lt;img src="responsive-obama-320.png"&gt;&lt;/noscript&gt;
&lt;/picture&gt;
</code></pre>

One problem with this markup is that, in its current configuration, our image would not be optimized for mobile devices. Here is the same image scaled down to 320 pixels wide:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2baad559-7b94-4ccb-9bcf-fd9372e371ad/president-barack-obama-tours-storm-damage-in-new-jersey-2-opt.jpg"><img loading="lazy" decoding="async" class="size-medium wp-image-137482" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ecc5bc27-f3d7-4c2f-a847-d9d2fd4c999e/responsive-obama-300x200.jpg" alt="President Obama and Governor Christi" width="300" height="200" /></a>

Identifying the people in this photo is difficult. To better cater to the smaller screen size, we need to <strong>use the power of art direction to crop this photo for small screens</strong>:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03ec90bd-c9c7-4600-a53b-0afc23daadd1/responsive-obama-mobile-opt.jpg"><img loading="lazy" decoding="async" class="size-medium wp-image-137486" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/490268ad-74a2-4958-aeed-a0d0fb03604f/responsive-obama-mobile-300x222.png" alt="responsive-obama-mobile" width="300" height="222" /></a>

Because this file isn't simply a scaled-down version of the original, the name of the file should be given a different structure (so, <code>responsive-obama-mobile.png</code>, instead of <code>responsive-obama-320.png</code>):

<pre><code class="language-markup">
&lt;picture&gt;
    &lt;source src="responsive-obama-mobile.png"&gt;
    &lt;source src="responsive-obama-512.png" media="(min-width: 512px)"&gt;
    &lt;source src="responsive-obama-1024.png" media="(min-width: 1024px)"&gt;
    &lt;source src="responsive-obama-2048.png" media="(min-width: 2048px)"&gt;
    &lt;noscript&gt;&lt;img src="responsive-obama-512.png"&gt;&lt;/noscript&gt;
&lt;/picture&gt;
</code></pre>

But <strong>what if we want to account for high-DPI (dots per inch) devices?</strong> The <code>picture</code> element’s specification has a <code>srcset</code> attribute that allows us to easily specify different images for different pixel ratios. Below is what our markup would look like if we used the <code>picture</code> element.

<pre><code class="language-markup">
&lt;picture&gt;
    &lt;source srcset="responsive-obama-mobile.png 1x, responsive-obama-mobile-2x.png 2x"&gt;
    &lt;source srcset="responsive-obama-512.png 1x, responsive-obama-1024.png 2x" media="(min-width: 512px)"&gt;
    &lt;source srcset="responsive-obama-1024.png 1x, responsive-obama-1024.png 2x" media="(min-width: 1024px)"&gt;
    &lt;source srcset="responsive-obama-2048.png 1x, responsive-obama-4096.png 2x" media="(min-width: 2048px)"&gt;
    &lt;noscript&gt;&lt;img src="responsive-obama-512.png"&gt;&lt;/noscript&gt;
&lt;/picture&gt;
</code></pre>

Here we have introduced a couple of new files (<code>responsive-obama-mobile-2x.png</code> and <code>responsive-obama-4096.png</code>) that must also be generated. At this point, we’ll have six different copies of the same image.

Let's take this a step further. What if we want to conditionally load our images in a more modern format, such as WebP, according to whether the browser supports it? Suddenly, the total number of files we must generate increases from 6 to 12. Let's be honest: No one wants to generate multiple versions of every image for various resolutions and have to constantly update those versions in the markup. <strong>We need automation!</strong>

## The Ideal Responsive Image Workflow

The ideal workflow is one that allows developers to upload images in the highest resolution possible while still using the <code>img</code> element in such a way that it automatically resizes and compresses the images for different browsers. The <code>img</code> element is great because it is a simple tag for solving a simple problem: displaying images for users on the Web. Continuing to use this element in a way that is performant and backwards-compatible would be ideal. Then, when the need for art direction arises and scaling down images is not enough, we could use the <code>picture</code> element; the branching logic built into its syntax is perfect for that use case.

This ideal workflow is possible using the responsive Image API in <a href="https://www.mobify.com/mobifyjs/v2/docs/image-resizer/">Mobify.js</a>. Mobify.js is an open-source library that improves responsive websites by providing responsive images, JavaScript and CSS optimization, adaptive templating and more. <strong>The Image API automatically resizes and compresses</strong> <code>img</code> and <code>picture</code> elements and, if needed, does it without changing a single line of markup in the back end. Simply upload your high-resolution assets and let the API take care of the rest.</p>

## Automatically Make Images Responsive Without Changing The Back End

The problem of responsive images is a hard one to solve because of the lookahead pre-parser, which prevents us from changing the <code>src</code> attribute of an <code>img</code> element on the fly with JavaScript in a performant way. The pre-parser is a feature of browsers that starts downloading resources as fast as possible by spawning a separate thread outside of the main rendering thread and whose only job is to locate resources and download them in parallel. The way the pre-parser works made a lot of sense prior to responsive design, but in our multi-device world, <strong>images in the markup are not necessarily the images we want users to download</strong>; thus, we need to start thinking of APIs that allow developers to control resource loading without sacrificing the benefits of the pre-parser. For more details on this subject, consider reading Steve Souders’ “<a href="https://www.stevesouders.com/blog/2013/04/26/i/">I &lt;3 Image Bytes</a>.”

One way that many developers avoid the pre-parser is by manually changing the <code>src</code> attribute of each <code>img</code> into <code>data-src</code>, which tricks the pre-parser into not noticing those images, and then changing <code>data-src</code> back to <code>src</code> with JavaScript. With the <a href="https://hacks.mozilla.org/2013/03/capturing-improving-performance-of-the-adaptive-web/">Capturing API</a> in Mobify.js, we can avoid this approach entirely, allowing us to be performant while remaining completely <a href="https://www.vanseodesign.com/web-design/semantic-html/">semantic</a> (no <code>&lt;noscript&gt;</code> or <code>data-src</code> hacks needed). The Capturing technique stops the pre-parser from initially downloading the resources in the page, but it doesn't prevent parallel downloads. Using Mobify.js’ Image API in conjunction with Capturing, we are able to have automatic responsive images with a single JavaScript tag.

Here is what the API call looks like:

<pre><code class="language-javascript">
Mobify.Capture.init(function(capture){
    var capturedDoc = capture.capturedDoc;
    var images = capturedDoc.querySelectorAll('img, picture');
    Mobify.ResizeImages.resize(images, capturedDoc)
    capture.renderCapturedDoc();
});
</code></pre>

This takes any image on the page and rewrites the <code>src</code> to the following schema:

<pre><code class="language-markup">
https://ir0.mobify.com/&lt;format&gt;&lt;quality&gt;/&lt;maximum width&gt;/&lt;maximum height&gt;/&lt;url&gt;
</code></pre>

For example, if this API was running on the latest version of Chrome for Android, with a screen 320 CSS pixels wide and a device pixel ratio of 2, then the following image…

<pre><code class="language-markup">
&lt;img src='cdn.mobify.com/mobifyjs/examples/assets/images/forest.jpg'&gt;
</code></pre>

… would be rewritten to this:

<pre><code class="language-markup">
&lt;img src='//ir0.mobify.com/webp/640/https://cdn.mobify.com/mobifyjs/examples/assets/images/forest.jpg'&gt;
</code></pre>

The image of the forest would be resized to 640 pixels wide, and, because Chrome supports WebP, we would take advantage of that in order to reduce the size of the image even further. After the first request, the image would be cached on Mobify's CDN for the next time it is needed in that particular size and format. Because this image of the forest does not require any art direction, we can continue using the <code>img</code> element.

You can <a href="https://cdn.mobify.com/mobifyjs/examples/resizeImages-img-element/index.html">see an example of automatic image resizing</a> for yourself. Feel free to open your Web inspector to confirm that the original images do not download!

Using this solution, we simplify our workflow. We only upload a high-resolution asset for each image, and then sit back and let the the API take care of resizing them automatically. No proxy in the middle, <strong>no changing of any attributes — just a single JavaScript snippet</strong> that is copied to the website. Go ahead and try it out by copying and pasting the following line of code at the top of your <code>head</code> element. (Please note that it must go before any other tag that loads an external resource.)

<pre><code class="language-javascript">
&lt;script&gt;!function(a,b,c,d,e){function g(a,c,d,e){var f=b.getElementsByTagName("script")[0];a.src=e,a.id=c,a.setAttribute("class",d),f.parentNode.insertBefore(a,f)}a.Mobify={points:[+new Date]};var f=/((; )|#|&amp;|^)mobify=(d)/.exec(location.hash+"; "+b.cookie);if(f&amp;&amp;f[3]){if(!+f[3])return}else if(!c())return;b.write('&lt;plaintext style="display:none"&gt;'),setTimeout(function(){var c=a.Mobify=a.Mobify||{};c.capturing=!0;var f=b.createElement("script"),h="mobify",i=function(){var c=new Date;c.setTime(c.getTime()+3e5),b.cookie="mobify=0; expires="+c.toGMTString()+"; path=/",a.location=a.location.href};f.onload=function(){if(e)if("string"==typeof e){var c=b.createElement("script");c.onerror=i,g(c,"main-executable",h,mainUrl)}else a.Mobify.mainExecutable=e.toString(),e()},f.onerror=i,g(f,"mobify-js",h,d)})}(window,document,function(){var a=/webkit|msies10|(firefox)[/s](d+)|(opera)[sS]*version[/s](d+)|3ds/i.exec(navigator.userAgent);return a?a[1]&amp;&amp;+a[2]&lt;4?!1:a[3]&amp;&amp;+a[4]&lt;11?!1:!0:!1},

// path to mobify.js
"//cdn.mobify.com/mobifyjs/build/mobify-2.0.1.min.js",

// calls to APIs go here
function() {
  var capturing = window.Mobify &amp;&amp; window.Mobify.capturing || false;

  if (capturing) {
    Mobify.Capture.init(function(capture){
      var capturedDoc = capture.capturedDoc;

      var images = capturedDoc.querySelectorAll("img, picture");
      Mobify.ResizeImages.resize(images);

      // Render source DOM to document
      capture.renderCapturedDoc();
    });
  }
});
&lt;/script&gt;
</code></pre>

(Please note that <strong>this script does not have a single point of failure</strong>. If Mobify.js fails to load, then the script will opt out and your website will load as normal. If the image-resizing servers are down or if you are in a development environment and the images are not publicly accessible, then the original images will load.)

You can also make use of the <a href="https://www.mobify.com/mobifyjs/v2/docs/">full documentation</a>. Browser support for the snippet above is as follows: All Webkit/Blink based browsers, Firefox 4+, Opera 11+, and Internet Explorer 10+.

Resizing <code>img</code> elements automatically is great for the majority of use cases. But, as demonstrated in the Obama example, art direction is necessary for certain types of images. How can we continue using the <code>picture</code> element for art direction without having to maintain six versions of the same image? The Image API will also resize <code>picture</code> elements, meaning that you can use the <code>picture</code> element for its greatest strength (art direction) and leave the resizing up to the API.

## Resizing <picture> Elements

While automating the sizes of images for different browsers is possible, automating art direction is impossible. The <code>picture</code> element is the best possible solution for specifying different images at different breakpoints, due to the robust branching logic built into its defined syntax (although as mentioned before, srcN is a more recent proposal that offers very similar features). But, as mentioned, writing the markup for the <code>picture</code> element and <strong>creating six assets for each image gets very complicated</strong>:

<pre><code class="language-markup">
&lt;picture&gt;
    &lt;source srcset="responsive-obama-mobile.png 1x, responsive-obama-mobile-2x.png 2x"&gt;
    &lt;source srcset="responsive-obama-512.png 1x, responsive-obama-1024.png 2x" media="(min-width: 512px)"&gt;
    &lt;source srcset="responsive-obama-1024.png 1x, responsive-obama-1024.png 2x" media="(min-width: 1024px)"&gt;
    &lt;source srcset="responsive-obama-2048.png 1x, responsive-obama-4096.png 2x" media="(min-width: 2048px)"&gt;
    &lt;noscript&gt;&lt;img src="responsive-obama-512.png"&gt;&lt;/noscript&gt;
&lt;/picture&gt;
</code></pre>

When using the Image API in conjunction with the <code>picture</code> element, <strong>we can simplify the markup significantly</strong>:

<pre><code class="language-markup">
&lt;picture&gt;
    &lt;source src="responsive-obama-mobile.png"&gt;
    &lt;source src="responsive-obama.png" media="(min-width: 512px)"&gt;
    &lt;img src="responsive-obama.png"&gt;
&lt;/picture&gt;
</code></pre>

The <code>source</code> elements here will be automatically rewritten in the same way that the <code>img</code> elements were in the previous example. Also, note that the markup above does not require <code>noscript</code> to be used for the fallback image to prevent a second request, because Capturing allows you to keep the markup semantic.

Mobify.js also allows for a modified <code>picture</code> element, which is useful for explicitly defining how wide images should be at different breakpoints, instead of having to rely on the width of devices. For example, if you have an image that is half the width of a tablet’s window, then specifying the width of the image according to the maximum width of the browser would generate an image that is larger than necessary:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bac4d93-147a-43cc-88af-ec7e529ffe62/tablet-example-opt.jpg"><img class="137488 alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4af0324-4fd1-4b43-a001-350cd99ad1ad/tablet-example-1024x787-opt.jpg" alt="tablet-example" width="500" height="384" /></a><br>
<em>In this case, automatically specifying a width according to the browser’s width would create an unnecessarily large image.</em>

To solve this problem, <strong>the Image API allows for alternate <code>picture</code> markup</strong> that enables us to override the width of each <code>source</code> element, instead of specifying a different <code>src</code> attribute for each breakpoint. For example, we could write an element like this:

<pre><code class="language-markup">
&lt;picture data-src="responsive-obama.png"&gt;
    &lt;source src="responsive-obama-mobile.png"&gt;
    &lt;source media="(min-width: 512px)"&gt;
    &lt;source media="(min-width: 1024px)" data-width="512"&gt;
    &lt;source media="(min-width: 2048px)" data-width="1024"&gt;
    &lt;img src="responsive-obama.png"&gt;
&lt;/picture&gt;
</code></pre>

Notice the use of the <code>data-src</code> attribute on the <code>picture</code> element. This gives us a high-resolution original image as a starting point, which we can use to resize into assets for other breakpoints.

<strong>Let's break down how this would actually work in the browser:</strong>

*   If the browser is between 0 and 511 pixels wide (i.e. a smartphone), then use `responsive-obama-mobile.png` (for the purpose of art direction).
*   If the browser is between 512 and 1023 pixels wide, then use `responsive-obama.png`, because `src` is not specified in the `source` element corresponding to that media query. Automatically determine the width because `data-width` isn't specified.
*   If the browser is between 1024 and 2047 pixels wide, then use `responsive-obama.png`, because `src` is not specified in the `source`element corresponding to that media query. Resize to 512 pixels wide, as specified in the `data-width` attribute.
*   If the browser is 2048 pixels or wider, then use `responsive-obama.png`, because `src` is not specified in the `source` element corresponding to that media query. Resize to 1024 pixels wide, as specified in the `data-width` attribute.
*   If JavaScript isn't supported, then fall back to the regular old `img` tag.

The Image API will run on each <code>picture</code> element, transforming the markup into this:

<pre><code class="language-markup">
&lt;picture data-src="https://cdn.mobify.com/mobifyjs/examples/assets/images/responsive-obama-mobile.jpg"&gt;
    &lt;source src="//ir0.mobify.com/webp/400/https://cdn.mobify.com/mobifyjs/examples/assets/images/responsive-obama-mobile.jpg"&gt;
    &lt;source src="//ir0.mobify.com/webp/400/https://cdn.mobify.com/mobifyjs/examples/assets/images/responsive-obama.jpg" media="(min-width: 512px)"&gt;
    &lt;source src="//ir0.mobify.com/webp/512/https://cdn.mobify.com/mobifyjs/examples/assets/images/responsive-obama.jpg" media="(min-width: 1024px)" data-width="512"&gt;
    &lt;source src="//ir0.mobify.com/webp/512/https://cdn.mobify.com/mobifyjs/examples/assets/images/responsive-obama.jpg" media="(min-width: 2048px)" data-width="1024"&gt;
    &lt;img src="responsive-obama.jpg"&gt;
&lt;/picture&gt;
</code></pre>

The Picture polyfill (included in Mobify.js) would then run and select the appropriate image according to the media queries. It will also work well when browser vendors implement the <code>picture</code> element natively.

See a <a href="https://cdn.mobify.com/mobifyjs/examples/resizeImages-picture-element/index.html">page that uses the modified <code>picture</code> element markup</a> for yourself.</p>

## Using the Image API without Capturing

One caveat with Capturing is that it requires the script to be inserted in the <code>head</code> element, which is a blocking JavaScript call that can delay the initial downloading of resources. The total length of delay on first load is approximately <a href="https://www.webpagetest.org/result/130619_MK_20EK/1/details/">0.5 seconds on a device with a 3G connection</a> (i.e. including the DNS lookup and downloading and Capturing), less on 4G or Wi-Fi, and about 60 milliseconds on subsequent requests (since the library will have been cached). But the minor penalty is a small price to pay in exchange for being easy to use, backwards-compatible and semantic.

To use the Image API without Capturing to <strong>avoid the blocking JavaScript request</strong>, you need to change the <code>src</code> attribute of all of your <code>img</code> elements to <code>x-src</code> (you might also want to add the appropriate <code>noscript</code> tags if you're concerned about browsers on which JavaScript has been disabled) and paste the following asynchronous script right before the closing <code>head</code> tag:

<pre><code class="language-javascript">
&lt;script src="//cdn.mobify.com/mobifyjs/build/mobify-2.0.1.min.js"&gt;
&lt;script&gt;
    var intervalId = setInterval(function(){
        if (window.Mobify) {
            var images = document.querySelectorAll('img[x-src], picture');
            if (images.length &gt; 0) {
                Mobify.ResizeImages.resize(images);
            }
            // When the document has finished loading, stop checking for new images
            if (Mobify.Utils.domIsReady()) {
                clearInterval(intervalId)
            }
        }
    }, 100);
&lt;/script&gt;
</code></pre>

This script will load Mobify.js asynchronously, and when finished loading, will start to loading the images as the document loads (it does not need to wait for the entire document to finish loading before kicking off image requests).</p>

## Using The Image API For Web Apps

If you are using a client-side JavaScript model-view-controller (MVC) framework, such as Backbone or AngularJS, you could still use Mobify.js’ Image API. First, include the Mobify.js library in your app:

<pre><code class="language-markup">
&lt;script src="//cdn.mobify.com/mobifyjs/build/mobify-2.0.1.min.js"&gt;&lt;/script&gt;
</code></pre>

Then, rewrite image URLs with the <a href="https://www.mobify.com/mobifyjs/v2/docs/image-resizer/#resizeimagesgetimageurlurl-options">method outlined in Mobify.js’ documentation</a>:

<pre><code class="language-javascript">
Mobify.ResizeImages.getImageUrl(url)
</code></pre>

This method accepts an absolute URL and returns the URL to the resized image. The easiest way to pass images into this method is by creating a template helper (for example, <code>{{image_resize '/obama.png' }}</code> in Handlebars.js) that executes the <code>getImageUrl</code> method in order to generate the image’s URL automatically.</p>

## Using Your Own Image-Resizing Back End

Images are resized through Mobify's <a href="https://cloud.mobify.com/">Performance Suite</a> resizing servers, which provides support for automatic resizing, WebP, CDN caching and more. There is a <span class="removed_link" title="https://cloud.mobify.com/mps/">default limit</span> on how many images you can convert for free per month, but if you're driving a large volume of traffic, then give Mobify a shout and we'll find a way to help. The API also allows you to <a href="https://www.mobify.com/mobifyjs/v2/docs/image-resizer/#resizeimagesgetimageurlurl-options">use a different image-resizing service</a>, such as Sencha.io Src, or your own backend service.</p>

## How Can Browser Vendors Better Support Responsive Images?

The Webkit team has recently implemented the <code>src-set</code> attribute, and so will Blink and Gecko in the coming months. This is a huge step in the right direction, as it means that browser vendors are taking the responsive image problem seriously. However, it doesn't solve the art direction problem, nor does it prevent the issue of needing to generate multiple assets at different resolutions.

The developer community recently <a href="https://www.w3.org/community/respimg/2013/09/18/paris-responsive-images-meetup/">got together to discuss</a> the responsive image problem. One of the more interesting proposals discussed was <a href="https://github.com/igrigorik/http-client-hints">Client Hints</a> from Ilya Grigorik, which is a proposal that involves <strong>sending device properties such as DPR, width and height</strong> in the headers of each request. I like this solution, because it allows us to continue using the <code>img</code> tag as per usual, and only requires us to use the <code>picture</code> (or <code>srcN</code>) when we need branching logic to do art direction. Although valid concerns have been raised about adding additional HTTP headers and <a href="https://groups.google.com/a/chromium.org/forum/#!msg/blink-dev/c38s7y6dH-Q/F4stpsFmih8J">using content negotiation</a> to solve this problem. More importantly, for established websites with thousands of images, it may not be so easy to route those images through a server that can resize using the headers provided by Client Hints. This could be solved by re-writing images at the web server level, or with a proxy, but both of those can be problematic to setup. In my opinion, this is something we should be able to handle on the client through greater control over resource loading.

If developers had <strong>greater control over resource loading</strong>, then responsive images would be a much <a href="https://daverupert.com/2013/06/ughck-images/">simpler problem to tackle</a>. The reason why so many responsive image solutions out there are proxy-based is because the images must be rewritten before the document arrives to the browser. This is to accommodate the pre-parser's attempt to download images as quickly as possible. But proxies can be very problematic in their security and scalability and, really, if we had an easy way to interact with the pre-parser, then many proxy-based solutions would redundant.

How can we get greater control over resource loading while still getting all of the benefits from the pre-parser? The key thing here is that we do not want to simply turn off the pre-parser — its ability to download assets in parallel is a huge win and one of the biggest performance improvements introduced into browsers. (Please note that the Capturing API does <em>not</em> prevent parallel downloads.) One idea is to <strong>provide a <code>beforeload</code> event</strong> that fires before each resource on a page has loaded. This event is actually available when one uses <a href="https://developer.apple.com/library/safari/#documentation/Tools/Conceptual/SafariExtensionGuide/MessagesandProxies/MessagesandProxies.html">Safari browser extensions</a>, and in some browsers it is available in a very limited capacity. If we could use this event to control resource loading in a way that works with the pre-parsing thread, then Capturing would no longer be needed. Here is a basic example of how you might use the <code>beforeload</code> event, if it worked as described:

<pre><code class="language-javascript">
function rewriteImgs(event) {
    if (event.target === "IMG") {
        var img = event.target;
        img.src = "//ir0.mobify.com/" + screen.width + "/" + img.src;
    }
}
document.addEventListener("beforeload", rewriteImgs, true);
</code></pre>

The key challenge is to somehow get the pre-parser to play nice with JavaScript that is executed in the main rendering loop. There <em>is</em> currently a new system being developed in browsers called the <a href="https://github.com/slightlyoff/ServiceWorker">Service Worker</a>, which is intended to allow developers to intercept network requests in order to help build web applications that work offline. However, the current implementation does not allow for intercepting requests on the initial load. This is because loading an external script which controls resource loading would have to block the loading of other resources — but <a href="https://github.com/slightlyoff/ServiceWorker/issues/73">I believe it could be modified</a> to do so in a way that does not sacrifice performance through the use of inline scripts.</p>

## Conclusion

While there are many solutions to the problem of responsive images, the one that automates as much work as possible while still allowing for art direction will be the solution that drives the future of Web development. Consider using Mobify.js to automate responsive images today if you are after a solution that does the following:

*   requires you to generate only one high-resolution image for each asset, letting the API take care of serving smaller images based on device conditions (width, WebP support, etc.);
*   makes only one request per image;
*   allows for 100% semantic and backwards-compatible markup that doesn't require changes to your back end (if using Capturing);
*   has a simplified `picture` element that is automatically resized, so you can focus on using it only for art direction.

<em>(Front page image credits: <a href="https://www.smashingmagazine.com/2013/08/12/creating-high-performance-mobile-websites/">Creating High-Performance Mobile Websites</a>)</em>

{{< signature "al, ea, il" >}}


---
title: Towards A Retina Web
slug: towards-retina-web
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22f01795-72bc-4fb9-9d52-605efd4104f4/desining-for-retina-illu-opt.jpg
date: 2012-08-20T13:26:11.000Z
author: reda-lemeden
description: >-
  With the recent announcement and release of the Retina Macbook Pro, Apple has
  brought double-density screens to all of the product categories in its current
  lineup, significantly paving the way for the next wave of display standards.
categories:
  - Coding
  - CSS
  - Responsive Design
  - HTML
  - SVG
---
With the recent announcement and release of the Retina Macbook Pro, Apple has brought double-density screens to all of the product categories in its current lineup, significantly paving the way for the next wave of display standards. While the fourth-generation iPhone gave us a taste of the “non-Retina” Web in 2010, we had to wait for the third-generation iPad to fully realize how fuzzy and outdated our Web graphics and content images are.

In the confines of Apple’s walled garden, popular native apps get updated with Retina graphics in a timely fashion, with the help of a solid SDK and a well-documented transition process. By contrast, the Web is a gargantuan mass whose very open nature makes the transition to higher-density displays slow and painful. In the absence of industry-wide standards to streamline the process, each Web designer and developer is left to ensure that their users are getting the best experience, regardless of the display they are using.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Better Way To Design For Retina In Photoshop](https://www.smashingmagazine.com/2015/05/retina-design-in-photoshop/)
*   [The Retina Asset Workflow You’ve Always Wanted For Photoshop](https://www.smashingmagazine.com/2016/03/the-retina-asset-workflow-youve-always-wanted-for-photoshop/)
*   [Create Pixel-Perfect Assets For Multiple Scale Factors](https://www.smashingmagazine.com/2014/10/create-assets-for-multiple-scale-factors/)
*   [Free Photoshop Action For Slicing Graphics For HD Screens](https://www.smashingmagazine.com/2013/07/retinize-it-photoshop-action-slicing-graphics-retina/)

Before diving into the nitty gritty, let’s briefly cover some basic notions that are key to understanding the challenges and constraints of designing for multiple display densities.

{{% feature-panel %}}

## Device Pixels

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/472871e0-9b96-49c6-9f87-7e778e408b70/device-pixels.png"><img class="121190" title="Device Pixels" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/472871e0-9b96-49c6-9f87-7e778e408b70/device-pixels.png" alt="Device Pixels" width="500" height="286" /></a>

A <strong>device pixel</strong> (or physical pixel) is the tiniest physical unit in a display. Each and every pixel sets its own color and brightness as instructed by the operating system, while the imperceptible distance between these tiny dots takes care of tricking the eye into perceiving the full image.

<strong>Screen density</strong> refers to the number of device pixels on a physical surface. It is often measured in pixels per inch (PPI). Apple has coined the marketing term “Retina” for its double-density displays, claiming that the human eye can no longer distinguish individual pixels on the screen from a “natural” viewing distance.</p>

## CSS Pixels

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6452bda3-8200-4f89-9d28-ba1092814c1a/css-pixels.png"><img class="121189" title="CSS Pixels" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6452bda3-8200-4f89-9d28-ba1092814c1a/css-pixels.png" alt="CSS Pixels" width="500" height="286" /></a>

A <strong>CSS pixel</strong> is an abstract unit used by browsers to precisely and consistently draw content on Web pages. Generically, CSS pixels are referred to as device-independent pixels (DIPs). On standard-density displays, 1 CSS pixel corresponds to 1 device pixel.

<pre><code class="language-markup tmp-html">&lt;div height="200" width="300"&gt;&lt;/div&gt;</code></pre>

This would use 200 × 300 device pixels to be drawn on screen. On a Retina display, the same <code>div</code> would use 400 × 600 device pixels in order to keep the same physical size, resulting in four times more pixels, as shown in the figure below.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2109b2d4-c9b7-45a1-923b-2c808ddfefbe/css-device-pixels.png"><img class="121188" title="Device Pixels In Retina Displays" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2109b2d4-c9b7-45a1-923b-2c808ddfefbe/css-device-pixels.png" alt="Device Pixels In Retina Displays" width="500" height="286" /></a><br>
<em>On a Retina display, four times as many device pixels are on the same physical surface.</em>

The ratio between device pixels and CSS pixels can be obtained using the following media query and its vendor-specific equivalents:

<pre><code class="language-css">device-pixel-ratio,
     -o-device-pixel-ratio,
   -moz-device-pixel-ratio,
-webkit-device-pixel-ratio {
…
}</code></pre>

Or you can use their future-proof siblings:

<pre><code class="language-css">device-pixel-ratio,
     -o-min-device-pixel-ratio,
   min--moz-device-pixel-ratio,
-webkit-min-device-pixel-ratio {
…
}</code></pre>

In Javascript, <code>window.devicePixelRatio</code> can be used to obtain the same ratio, although browser support is still relatively limited. Both of these techniques will be discussed in depth later in this article.</p>

## Bitmap Pixels

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d1c8bba-b98f-4791-8c73-3b3368733b74/bitmap-pixels.png"><img class="121187" title="Bitmap Pixels" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d1c8bba-b98f-4791-8c73-3b3368733b74/bitmap-pixels.png" alt="Bitmap Pixels" width="500" height="284" /></a>

A bitmap pixel is the smallest unit of data in a raster image (PNG, JPG, GIF, etc). Each pixel contains information on how it is to be displayed, including its position in the image’s coordinate system and its color. Some image formats can store additional per-pixel data, such as opacity (which is the alpha channel).

Beside its raster resolution, an image on the Web has an abstract size, defined in CSS pixels. The browser squeezes or stretches the image based on its CSS height or width during the rendering process.

When a raster image is displayed at full size on a standard-density display, 1 bitmap pixel corresponds to 1 device pixel, resulting in a full-fidelity representation. Because a bitmap pixel can’t be further divided, it gets multiplied by four on Retina displays to preserve the same physical size of the image, losing detail along the way.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d8a3e19-9539-4ddf-8e98-afd0ae190961/css-device-bitmap-pixels.png"><img class="121187" title="Bitmap Pixels On Retina Displays" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d8a3e19-9539-4ddf-8e98-afd0ae190961/css-device-bitmap-pixels.png" alt="Bitmap Pixels On Retina Displays" width="500" height="284" /></a><br>
<em>Each bitmap pixel gets multiplied by four to fill the same physical surface on a Retina display.</em>

## The Tool Chest

Even though we are still in the early stages of this major shift, several approaches to optimizing Web graphics for Retina displays have sprung up, and more are popping up as we speak. Each method makes some degree of compromise between performance, ease of implementation and cross-browser support. As such, choosing a tool should be done case by case, taking into account both quantitative and qualitative factors.</p>

## HTML And CSS Sizing

The most straightforward way to serve Retina-ready Web graphics is to halve the size of your raster assets using CSS or HTML, either manually or programatically. For instance, to serve a 200 × 300-pixel image (remember, those are CSS pixels), you would upload an image with a bitmap resolution of 400 × 600 pixels to your server, then shrink it by exactly 50% using CSS properties or HTML attributes. On a standard-resolution display, the result would be an image rendered with four times fewer pixels than its full bitmap size — a process commonly referred to as downsampling.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9b7c16e-76de-4faf-8a19-f0bfaa35a1d7/downsampling.png"><img class="121191" title="Downsampling" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9b7c16e-76de-4faf-8a19-f0bfaa35a1d7/downsampling.png" alt="How downsampling works" width="500" height="165" /></a><br>
<em>A CSS-sized image gets its dimensions halved during the rendering process.</em>

Because the same image would use four times as many physical pixels on a Retina screen, every physical pixel ends up matching exactly 1 bitmap pixel, allowing the image to render at full fidelity once again.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ddc59f5-51b7-4b20-be09-e864f842baf6/html-sizing.png"><img class="121192" title="HTML Sizing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ddc59f5-51b7-4b20-be09-e864f842baf6/html-sizing.png" alt="How HTML sizing works" width="500" height="168" /></a><br>
<em>CSS-sized images regain their full-detail glory on Retina displays.</em>

There are several ways to achieve this:

### Using HTML

The easiest way to apply CSS sizing would be by using the <code>width</code> and <code>height</code> attributes of the <code>img</code> tag:

<pre><code class="language-markup tmp-html">&lt;img src="example@2x.png" width="200" height="300" /&gt;</code></pre>

Please note that, even though specifying <code>height</code> is optional, it allows the browser to reserve the space required for the image before loading it. This prevents the page layout from changing as the image loads.

<strong>What to use it for?</strong> Single-page websites with few content images.</p>

### Using Javascript

The same result can also be obtained using Javascript by targeting all Retina-ready content images in the document and halving their sizes. With the help of jQuery, this would look like this:

<pre><code class="language-javascript">$(window).load(function() {
  var images = $('img');
    images.each(function(i) {
      $(this).width($(this).width() / 2);
    });
});</code></pre>

<strong>What to use it for?</strong> Websites with few content images.</p>

### Using CSS (SCSS)

If you want to keep all of the presentation code in your CSS files, then the most common technique involves setting the image as the background of another HTML element, usually a <code>div</code>, then specifying its <code>background-size</code> property. You could either set explicit width and height values for the background image or use the <code>contain</code> value if the dimensions of the HTML element are already specified. It is worth noting that the <code>background-size</code> property is not supported in IE 7 or 8.

<pre><code class="language-css">.image {
  background-image: url(example@2x.png);
  background-size: 200px 300px;
  /* Alternatively background-size: contain; */
  height: 300px;
  width: 200px;
}</code></pre>

You could also target a <code>:before</code> or <code>:after</code> pseudo-element instead:

<pre><code class="language-css">.image-container:before {
  background-image: url(example@2x.png);
  background-size: 200px 300px;
  content:’;
  display: block;
  height: 300px;
  width: 200px;
}</code></pre>

This technique works just as well with CSS sprites, as long as the <code>background-position</code> is specified relatively to the CSS size (200 × 300 pixels in this case):

<pre><code class="language-css">.icon {
  background-image: url(example@2x.png);
  background-size: 200px 300px;
  height: 25px;
  width: 25px;

  &amp;.trash {
    background-position: 25px 0;
  }

  &amp;.edit {
    background-position: 25px 25px;
  }
}</code></pre>

When using image sprites, consider any OS-specific limitations.

<strong>What to use it for?</strong> Websites that make limited use of the <code>background-image</code> property, such as those that rely on a single-image sprite.</p>

### HTML and CSS Sizing: Pros

*   Easy to implement
*   Cross-browser compatible

### HTML and CSS Sizing: Cons

*   Non-Retina devices have to download larger assets.
*   Downsampled images might lose some of their sharpness on standard-density screens, depending on the algorithm used.
*   The `background-size` property is not supported in IE 7 or 8.</p>

## Querying Pixel Density

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d29f86cc-d417-4237-ade3-dbe8706c662f/querying.png"><img loading="lazy" decoding="async" class="121194" title="Querying Pixel Density" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d29f86cc-d417-4237-ade3-dbe8706c662f/querying.png" alt="Querying Pixel Density" width="500" height="286" /></a>

Perhaps the most popular way to serve Retina-ready graphics on the Web is by querying the device for its pixel density and then serving assets accordingly. This can be done using either CSS or JavaScript.</p>

### Using CSS Media Queries

As of this writing, almost every major browser vendor has implemented a prefixed variant of <code>device-pixel-ratio</code> and its two siblings, <code>min-device-pixel-ratio</code> and <code>max-device-pixel-ratio</code>. These media queries can be used in conjunction with the <code>background-image</code> property to serve Retina-ready assets to high-density devices:

<pre><code class="language-css">.icon {
  background-image: url(example.png);
  background-size: 200px 300px;
  height: 300px;
  width: 200px;
}

@media only screen and (-Webkit-min-device-pixel-ratio: 1.5),
only screen and (-moz-min-device-pixel-ratio: 1.5),
only screen and (-o-min-device-pixel-ratio: 3/2),
only screen and (min-device-pixel-ratio: 1.5) {
  .icon {
    background-image: url(example@2x.png);
  }
}</code></pre>

By using a ratio of 1.5 instead of 2, you can target other non-Apple devices with the same query.

<strong>What to use it for?</strong> Any website or app that uses the <code>background-image</code> property for graphic assets. Not suitable for content images.</p>

### CSS Querying: Pros

*   Devices download only those assets that target them.
*   Cross-browser compatible
*   Pixel-precise control

### CSS Querying: Cons

*   Tedious to implement, especially on large websites.
*   Displaying content images as backgrounds of other HTML elements is semantically incorrect.</p>

### Using Javascript

The pixel density of the screen can be queried in Javascript using <code>window.devicePixelRatio</code>, which reports the same value as its CSS counterpart. Once a higher-density screen is identified, you can replace every inline image with its Retina counterpart:

<pre><code class="language-javascript">$(document).ready(function(){
  if (window.devicePixelRatio &gt; 1) {
    var lowresImages = $('img');

    images.each(function(i) {
      var lowres = $(this).attr('src');
      var highres = lowres.replace(".", "@2x.");
      $(this).attr('src', highres);
    });
  }
});</code></pre>

<a href="https://retinajs.com">Retina.js</a> is a Javascript plugin that implements roughly the same technique as described above, with some additional features, such as skipping external images and skipping internal images with no <code>@2x</code> counterparts.

Lastly, it is worth noting that <code>devicePixelRatio</code> is <a href="https://www.quirksmode.org/blog/archives/2012/06/devicepixelrati.html#link2">not entirely cross-browser compatible</a>.

<strong>What to use it for?</strong> Any website with content images, such as landing pages and blogs.</p>

### Javascript Querying: Pros

*   Easy to implement
*   Non-Retina devices do not download large assets.
*   Pixel-precise control

### Javascript Querying: Cons

*   Retina devices have to download both standard- and high-resolution images.
*   The image-swapping effect is visible on Retina devices.
*   Does not work on some popular browsers (such as IE and Firefox).</p>

## Scalable Vector Graphics

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d41a6a18-8d71-45c0-8426-dbd44e1cf4cc/svg1.png"><img loading="lazy" decoding="async" class="121195" title="SVG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d41a6a18-8d71-45c0-8426-dbd44e1cf4cc/svg1.png" alt="Scalable Vector Graphics" width="500" height="286" /></a>

Regardless of the method used, raster images remain inherently constrained by their bitmap resolution; they were never meant to be infinitely scalable. This is where vector graphics have the advantage, being a future-proof way to “Retinize” your Web graphics.

As of this writing, the vector XML-based SVG format has <a href="https://caniuse.com/#search=svg">cross-browser support</a> of more than 70% and can be used in several ways on the Web. SVG images can be easily created in and exported from a number of vector-graphic editors, such as Adobe Illustrator and free alternatives such as <a href="https://inkscape.org/">Inkscape</a>.

As far as Web design goes, the most straightforward way to use SVG assets is with the HTML <code>img</code> tag or with the CSS <code>background-image</code> and <code>content:url()</code> properties.

<pre><code class="language-markup tmp-html">&lt;img src="example.svg" width="200" height="300" /&gt;</code></pre>

In the example above, a single SVG image can be used as a universal asset, scaling infinitely up or down as required. This not only saves precious bandwidth (most SVG files tend to be smaller in size than standard-resolution PNGs), but also makes your graphic assets much easier to maintain. The same would apply if used in CSS:

<pre><code class="language-css">/* Using background-image */

.image {
  background-image: url(example.svg);
  background-size: 200px 300px;
  height: 200px;
  width: 300px;
}

/* Using content:url() */

.image-container:before {
  content: url(example.svg);
  /* width and height do not work with content:url() */
}</code></pre>

If you have to support IE 7 or 8 or Android 2.x, then you will need a fallback solution that swaps SVG images with their PNG counterparts. This can be easily done with <a href="https://modernizr.com/docs/#features-misc">Modernizr</a>:

<pre><code class="language-css">.image {
  background-image: url(example.png);
  background-size: 200px 300px;
}

.svg {
  .image {
    background-image: url(example.svg);
  }
}</code></pre>

For best cross-browser results and to avoid some <a href="https://dbushell.com/2012/03/11/svg-all-fun-and-games/">rasterization headaches</a> in Firefox and Opera, make each SVG image at least the size of its parent HTML element.

In HTML, you can implement a similar fallback solution by adding a custom <code>data</code> attribute to your <code>img</code> tag:

<pre><code class="language-markup tmp-html">&lt;img src="example.svg" data-png-fallback="example.png" /&gt;</code></pre>

Then, handle the rest with jQuery and Modernizr:

<pre><code class="language-javascript">$(document).ready(function(){
  if(!Modernizr.svg) {
    var images = $('img[data-png-fallback]');
    images.each(function(i) {
      $(this).attr('src', $(this).data('png-fallback'));
    });
  }
});</code></pre>

This HTML and JavaScript route, however, would not prevent browsers with no SVG support from downloading the SVG assets.

<strong>What to use it for?</strong> Any website or app. Suitable for icons, logos and simple vector illustrations.</p>

### SVG: Pros

*   One universal asset for all devices
*   Easy to maintain
*   Future-proof: infinitely scalable vector graphics

### SVG: Cons

*   No pixel precision due to anti-aliasing
*   Unsuitable for complex graphics due to large file sizes
*   No native support in IE 7 and 8 or early Android versions

## Icon Fonts

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bec43c7-90d0-4326-8f27-973b22e7a190/icon-fonts.png"><img loading="lazy" decoding="async" class="121193" title="Icon Fonts" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bec43c7-90d0-4326-8f27-973b22e7a190/icon-fonts.png" alt="Icon Fonts" width="500" height="135" /></a>

Popularized by Twitter’s <a href="https://twitter.github.com/bootstrap/">Bootstrap</a>, the technique of using <code>@font-face</code> with icon-based fonts has garnered a following of its own as a resolution-independent alternative to bitmap icons. The technique consists of using a custom Web font that replaces the alphabet with monochrome glyphs, which can be styled using CSS, just like any other text on the website.

There is <a href="https://www.delicious.com/stacks/view/SC3hpq">no shortage</a> of comprehensive, good-quality icon fonts that would cover most of your needs. That being said, importing a large font in half a dozen formats only to use a small subset of the icons is a bad idea. Consider building your own custom font with free tools such as <a href="https://fontello.com/">Fontello</a>, <a href="https://github.com/fontello/font-builder">Font Builder</a> or even <a href="https://www.Webdesignerdepot.com/2012/01/how-to-make-your-own-icon-Webfont/">Inkscape</a>.

The most common way to use icon fonts on websites is by assigning an <code>.icon</code> or <code>.glyph</code> class to a particular HTML element — most often a <code>&lt;span&gt;</code> or an <code>&lt;i&gt;</code> — and then using the letter corresponding to the desired icon as its content:

<pre><code class="language-markup tmp-html">&lt;span class="icon"&gt;a&lt;/span&gt;</code></pre>

After having imported your custom font using <code>@font-face</code>, you would declare it:

<pre><code class="language-css">.icon {
  font-family: 'My Icon Font';
}</code></pre>

Another technique consists of using the <code>:before</code> pseudo-element and the <code>content</code> property, with a unique class for each icon:

<pre><code class="language-markup tmp-html">&lt;span class="glyph-heart"&gt;&lt;/span&gt;</code></pre>

<pre><code class="language-css">[class^="glyph-"]:before {
  font-family: 'My Icon Font';
}

.glyph-heart:before {
  content: 'h';
}</code></pre>

<strong>What to use it for?</strong> Websites or apps with a high number of icons, and for rapid prototyping.</p>

### Icon Fonts: Pros

*   Future-proof: infinitely scalable glyphs
*   Cross-browser compatible
*   More flexible than graphic assets: can be used in placeholder text and other form elements, etc.</p>

### Icon Fonts: Cons

*   No pixel precision due to subpixel anti-aliasing
*   Hard to maintain: changing a single icon requires regenerating the whole font.
*   Relies on semantically incorrect markup (unless used with `:before` or `:after` pseudo-elements).</p>

## Favicons

Favicons are getting their fair share of attention, being increasingly used outside of browser chrome as an iconic representation of our websites and apps. To make your favicons Retina-ready, export an <code>.ico</code> file in both 16- and 32-pixel versions. If you are using a Mac, you can create your own <code>.ico</code> files with Apple’s Icon Composer (included in the <a href="https://developer.apple.com/downloads/">Graphic Tools in Xcode</a>) or with <a href="https://itunes.apple.com/us/app/icon-slate/id439697913?mt=12">Icon Slate</a>, a paid third-party application.</p>

## A Glimpse Of The Future

Besides the techniques covered above, several other efforts are being made independently by organizations and individuals alike, not the least of which is Apple’s own <code>-Webkit-image-set</code>, <a href="https://trac.Webkit.org/changeset/111637">introduced</a> last spring. This <a href="https://lists.w3.org/Archives/Public/www-style/2012Feb/1103.html">proposal allows for</a> multiple variants of the same image to be provided in one CSS declaration:

<pre><code class="language-css">.image {
  background-image: -Webkit-image-set(url(example.png) 1x, url(example@2x.png) 2x);
  background-size: 200px 300px;
}</code></pre>

This technique does not, however, cover images inside <code>img</code> tags, and it is Webkit-only as of this writing.

Another notable effort is Scott Jehl’s <a href="https://github.com/scottjehl/picturefill">Picturefill</a>, an HTML and Javascript solution that makes heavy use of <code>data</code> attributes and media queries to serve different images in different media contexts.

<pre><code class="language-markup tmp-html">&lt;div data-picture&gt;
     &lt;div data-src="example.png"&gt;&lt;/div&gt;
     &lt;div data-src="example@2x.png" data-media="(min-device-pixel-ratio: 1.5)"&gt;&lt;/div&gt;

  &lt;!-- Fallback content for non-JS browsers --&gt;
  &lt;noscript&gt;
    &lt;img src="example.png" &gt;
  &lt;/noscript&gt;
&lt;/div&gt;</code></pre>

Even if the markup puts you off, it is a good cross-browser solution to consider if you are dealing with few content images.

Last but not least, the ambitious <code>picture</code> element <a href="https://www.w3.org/community/respimg/wiki/Picture_Element_Proposal">proposal</a> aims to bring responsive images to the Web using a markup-only approach for multiple image sources, coupled with media queries that route each device to the right asset.</p>

### Closing Words

Like other <a href="https://robots.thoughtbot.com/post/23288959017/designing-for-touch">major shifts</a> the Web is currently undergoing, attaining resolution independence will be a long journey. As Web designers and developers, either we can sit down and wait passively for a convention to be standardized, or we can immediately start offering a pleasurable viewing experience to our users. Let’s get to work.

{{< signature "al" >}}


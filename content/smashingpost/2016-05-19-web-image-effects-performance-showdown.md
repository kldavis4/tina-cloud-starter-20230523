---
title: Web Image Effects Performance Showdown
slug: web-image-effects-performance-showdown
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60b8efb4-3283-4c3a-a87b-b5a2f8dc0c5b/01-bird-preview-opt.jpg
date: 2016-05-19T22:04:17.000Z
author: una-kravets
description: >-
  As browsers constantly improve their graphical rendering abilities, the
  ability to truly design within them is becoming more of a reality. A few lines
  of code can now have quick and dramatic visual impact, and **allow for
  consistency without a lot of effort**. And as with most things in web
  development, there are often many ways to achieve the same effect.

  In this post, we'll take a look at one of the most popular image effects,
  grayscale, and assess both the ease of implementation and performance
  implications of HTML canvas, SVG, CSS filters, and CSS blend modes. _Which one
  will win?_
categories:
  - Coding
  - CSS
  - SVG
  - Responsive Images
  - WebGL
---
As browsers constantly improve their graphical rendering abilities, the ability to truly design within them is becoming more of a reality. A few lines of code can now have quick and dramatic visual impact, and **allow for consistency without a lot of effort**. And as with most things in web development, there are often many ways to achieve the same effect.

In this post, we'll take a look at one of the most popular image effects, grayscale, and assess both the ease of implementation and performance implications of HTML canvas, SVG, CSS filters, and CSS blend modes. _Which one will win?_

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Web Image Effects Performance Showdown](https://www.smashingmagazine.com/2016/05/web-image-effects-performance-showdown/)
*   [HTML5: The Facts And The Myths](https://www.smashingmagazine.com/2010/09/html5-the-facts-and-the-myths/)
*   [Efficient Image Resizing With ImageMagick](https://www.smashingmagazine.com/2015/06/efficient-image-resizing-with-imagemagick/)
*   [Clever JPEG Optimization Techniques](https://www.smashingmagazine.com/2009/07/clever-jpeg-optimization-techniques/)

Filters on the web work like a lens laid over an image. They are applied to the image [after the browser renders](https://www.html5rocks.com/en/tutorials/filters/understanding-css/) layout and initial paint. In supporting browsers, [filters can be applied](https://caniuse.com/#feat=css-filters) individually or layered on top of one another. Because they can be applied as image modifications after the initial render, and are likely an enhancement, filters gracefully degrade by merely not being visible in browsers which do not support them.

{{% feature-panel %}}

## CSS Filters

Let's get started with the most straightforward method for producing a grayscale effect: the humble, yet powerful CSS filter.

<figure>
  <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72040248-7892-4a9c-8576-36796f8d733d/01-bird-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60b8efb4-3283-4c3a-a87b-b5a2f8dc0c5b/01-bird-preview-opt.jpg" height="250" width="500" alt="unfiltered bird image"></a><figcaption>Unfiltered image. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72040248-7892-4a9c-8576-36796f8d733d/01-bird-opt.jpg">View large version</a>)</figcaption>
</figure>

To achieve this effect, we add a single line of CSS: `filter: grayscale(1)`. This filter desaturates the image and can be used with any numeric or percentage-based value between 0 and 1 (or 0% to 100%). Note: currently, filters for WebKit-based browsers must be prefixed with `-webkit-`. However, a solution such as [Autoprefixer](https://github.com/postcss/autoprefixer) would eliminate the need to add them by hand.</p>

### Live Demo – CSS Filter

<style>.cssfilter-gray{max-width:500px;min-height:250px;display:block;background:url('https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60b8efb4-3283-4c3a-a87b-b5a2f8dc0c5b/01-bird-preview-opt.jpg');background-repeat:no-repeat;filter:grayscale(1);-webkit-filter:grayscale(1);}</style>

<div class="cssfilter-gray"></div>

<pre><code class="language-css">
.cssfilter-gray {
  -webkit-filter: grayscale(1);
  background: url('img/bird.jpg');
  filter: grayscale(1);
}
</code></pre>

## Background Blend Mode

CSS blend modes provide an endless variety of options for image effect combinations. There are two ways to use blend modes: the `mix-blend-mode` property and the `background-blend-mode` property.

*   `mix-blend-mode` is the property which describes how the element will blend with the content behind it.
*   `background-blend-mode` is used for elements with multiple backgrounds, and describes the relationship between these backgrounds.

We'll use the `background-blend-mode: luminosity` to pull luminosity channels over a gray background in our example, resulting in a grayscale image. One thing to note is that background order is constant: **background images must always be ordered before solid colors or gradient backgrounds for effects to render properly**. [Color must be the last background layer](https://developer.mozilla.org/en-US/docs/Web/CSS/background). This is also a safeguard against older browsers which do not support `background-blend-mode` – the image will still render without the effect.

The only difference with blend modes and the CSS filter is that we now have multiple backgrounds, and are using `background-blend-mode: luminosity`, which grabs the luminosity values from the top image (the bird tester) and layers those brightness values over a gray second background.</p>

### Live Demo – Background Blend Mode

<style>.blendmode-gray{max-width:500px;min-height:250px;display:block;background:url('https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60b8efb4-3283-4c3a-a87b-b5a2f8dc0c5b/01-bird-preview-opt.jpg'),gray;background-repeat:no-repeat;background-blend-mode:luminosity;}</style>

<div class="blendmode-gray"></div>

<pre><code class="language-css">
.cssfilter-gray {
  background: url('img/bird.jpg'), gray;
  background-blend-mode: luminosity;
}
</code></pre>

At the moment, this is the newest and thus [least supported](https://caniuse.com/#search=background-blend-mode) option, though it still works well in Chrome and Firefox, and has partial Safari support. Note: Safari supports all blend modes except for the HSL-based blend modes: hue, saturation, color, and luminosity.</p>

## HTML5 Canvas

HTML5 `<canvas>` allows for a ton of flexibility when it comes to image manipulation, because we have access to each individual pixel's data (specifically through `canvasContext.getImageData`) and can manipulate each one through JavaScript. This method, however, is the most complex and comes with the most overhead. It also has a few nuances in cross-origin issues due to security concerns.

To fix the cross-origin error in Chrome, your image will need to be hosted on a cross-origin resource sharing (CORS) friendly site like GitHub Pages or Dropbox, and specify `crossOrigin="Anonymous"`. See the [live example for a demonstration](https://una.im/filter-perf-tests/04_canvas.html).

The way to achieve a grayscale effect with `<canvas>` is to strip the red, green and blue components from any outlying value in the pixel value while maintaining its luminosity level (brightness). [One way to do this](https://www.ajaxblender.com/howto-convert-image-to-grayscale-using-javascript.html) is to average the RGB values like so: `grayscale = (red + green + blue) / 3;`.

In the example below, we are using the RGBa values in the format `(R,G,B,a)` in the image data; the red channel is `data[0]`, the green channel is `data[1]`, and so on. We then get the luminosity level of each of these channels (the brightness) and average them to turn the image grayscale.</p>

### Live Demo – HTML5 Canvas

<script>url = 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60b8efb4-3283-4c3a-a87b-b5a2f8dc0c5b/01-bird-preview-opt.jpg',src = url,img_obj = new Image();img_obj.crossOrigin = 'anonymous';function drawGreyscale(imageObj, n) {var canvas = document.getElementById('canvas-gray');var context = canvas.getContext('2d');var x = 0;var y = 0;var imgHeight = 300;context.drawImage(imageObj, x, y+(imgHeight*n));var imageData = context.getImageData(x, y, imageObj.width, imageObj.height);var data = imageData.data;for(var i = 0; i < data.length; i += 4) {var brightness = (data[i] + data[i + 1] + data[i + 2])/3;data[i] = brightness;data[i + 1] = brightness;data[i + 2] = brightness;}context.putImageData(imageData, x, y+(imgHeight*n));}img_obj.src = src;img_obj.addEventListener('load', function() {for (var n = 0; n < 10; n++){drawGreyscale(this, n);}}, false);</script>

<canvas id="canvas-gray" width="500" height="250"></canvas>

<style>#canvas-gray{display:block;width:100%;max-width:500px;min-height:250px}</style>

## SVG Filter

[SVG filters have the widest support](https://caniuse.com/#search=SVG%20filter) (even in Internet Explorer and Edge!) and are also (almost) just as easy to use as CSS filters directly. You can use them with the same `filter` property. In fact, [CSS filters stemmed out of SVG filters](https://docs.webplatform.org/wiki/svg/tutorials/smarter_svg_filters). As with canvas, SVG filters allow you to transcend the flat plane of two-dimensional effects, as you can leverage WebGL shading to create even more complex results.

There are a few ways to apply an SVG filter, but in this case we will still use the `filter` property on the background image, just like the CSS filter example for consistency. The biggest difference with SVG filters is that we need to be careful to include and link to this filter with the proper path. This means we need to **import the SVG on the page above the element in which we are using it** (which can be made easier by using templating engine and include statements).</p>

### Live Demo – SVG Filter

<style>.svg-gray{max-width:500px;min-height:250px;display:block;background:url('https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60b8efb4-3283-4c3a-a87b-b5a2f8dc0c5b/01-bird-preview-opt.jpg');background-repeat:no-repeat;-webkit-filter:url(#grayscale-filter);filter:url(#grayscale-filter);}</style>

<div class="svg-gray"></div>

<pre><code class="language-markup">
&lt;svg&gt;
  &lt;filter id="grayscale-filter"&gt;
    &lt;feColorMatrix type="saturate" values="0"/&gt;
  &lt;/filter&gt;
&lt;/svg&gt;
</code></pre>

<pre><code class="language-css">
.svgfilter-gray {
  background: url('img/bird.jpg');
  -webkit-filter: url(#grayscale-filter);
  filter: url(#grayscale-filter);
}
</code></pre>

## Filter Performance

<p>So how do these stack up when it comes to initial render performance? I made a test page for each and used the <a href="https://webpagetest.org">WebPagetest</a> comparison feature in Chrome 47. Keeping in mind that each test gave slightly different results, the overall trend can be summed up as follows:</p>

{{< vimeo id="153739076" >}}

<p>The CSS filter, SVG filter and CSS blend mode methods all loaded in relatively similar time frames. Sometimes the SVG filter was faster than the CSS blend mode (but always barely) and vice versa. The CSS filter was generally among the fastest to load, and <code>&lt;canvas&gt;</code> was always the slowest. This is the most significant insight gleaned. <code>&lt;canvas&gt;</code> was regularly lagging behind the other methods in rendering the image.</p>

<p>For fairness sake, I wanted to also compare load time for multiple images. I created ten renditions of each (instead of just one) and ran the tests again:</p>

{{< vimeo id="153739077" >}}

<p>The results were similar (keep in mind there were slight variations in each test). The CSS filter was 0.1ms slower in this case, showing that between CSS filters, blend modes and SVG filters, the results are inconclusive for the speediest method. However, HTML5 <code>&lt;canvas&gt;</code> lagged noticeably in comparison.</p>

<p>Taking a look deeper into page load time via JavaScript render and paint render time, you can see this trend continuing.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b49a3c1b-b3b4-44ce-ba99-870a1b483d60/timeline-combined.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b62e9e63-14cd-4efb-89f7-81c25b85cd36/timeline-combined-500px.png" width="500" height="347" alt="" title="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b49a3c1b-b3b4-44ce-ba99-870a1b483d60/timeline-combined.png">View large version</a>)</figcaption></figure>

<table class="article-table three-columns">
  <tr>
    <th>Filter Type</th>
    <th>Time to Render</th>
    <th>Time to Paint</th>
  </tr>
  <tr>
    <td>CSS Filter</td>
    <td>12.94ms</td>
    <td>4.28ms</td>
  </tr>
  <tr>
    <td>CSS Blend Mode</td>
    <td>12.10ms</td>
    <td>4.45ms</td>
  </tr>
  <tr>
    <td>SVG Filter</td>
    <td>14.77ms</td>
    <td>5.80ms</td>
  </tr>
  <tr>
    <td>Canvas Filter</td>
    <td>15.23ms</td>
    <td>10.73ms</td>
  </tr>
</table>

<p>Again, <code>&lt;canvas&gt;</code> took the longest time to render and longest time to paint, while the two CSS options were the speediest, SVG coming in the middle.</p>

<p>These results make sense, because <code>&lt;canvas&gt;</code> is taking each individual pixel and performing an operation on it before we are ever able to see any image at all. This takes a lot of processing power at render time. While normally SVGs are used for vector graphics, I would still highly recommend them over <code>&lt;canvas&gt;</code> when dealing with raster image effects. Not only is SVG faster, but it is also <a href="https://www.htmlgoodies.com/html5/other/html5-canvas-vs.-svg-choose-the-best-tool-for-the-job.html#fbid=hYkHGF7HJ2b">much easier to deal with and more flexible within the DOM</a>. Generally, CSS filters are even more optimized than SVG filters, as historically they are shortcuts emerging out of SVG filters and, thus, optimized in browsers.</p>

## #nofilter

<p>What about using no filter? I compared our overall speediest method (adding a CSS filter) to editing your image in photo editing software before uploading it (I used Preview on Mac OS X to remove saturation). When preediting the image, I found a consistent 0.1ms performance improvement in my tests:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/753fb78b-328c-47e7-aa89-d283dd5ef182/02-nofilter-opt.png"><img></a></figure>

<figure class="aspect-ratio">{{< vimeo 153739078 >}}</figure>

## Conclusion

<p>Image filters are a fun and effective way to provide visual unity and aesthetic appeal on the web. Keep in mind that they do come with a slight performance hit, but also with the benefits of speedy design in the browser and the opportunity to design interactions with.</p>

<p>For simple image effects use CSS filters, as they have the widest support and simplest usage. For more complex image effects, check out SVG filters or CSS blend modes. SVG filter effects are particularly nice because of their channel manipulation capabilities and <code><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Element/feColorMatrix">feColorMatrix</a></code>. CSS blend modes also offer some really nice visual effects with overlapping elements on the page. You can use similar blend modes within SVG (such as <code>feBlend</code>), though they are akin to CSS <code>background-blend-mode</code> in the sense that the interaction pertains to the SVG itself and not with surrounding elements, like <code>mix-blend-mode</code> allows. <strong>Just don't use <code>&lt;canvas&gt;</code> for filters.</strong></p>

{{< signature "rb, og, il" >}}


---
title: 'The Humble `<img>` Element And Core Web Vitals'
slug: humble-img-element-core-web-vitals
author: addy-osmani
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7ec5e4a-099e-4a1a-a1a3-b7545835520f/26-humble-img-element-and-core-web-vitals.png
date: 2021-04-29T12:15:00.000Z
summary: >-
  Images have also been a key part of the web. They communicate ideas instantly, but they are also a lot heavier than text to load. This means that it’s essential to get loading and displaying them right, if you want to give your users a fantastic first impression. An excerpt from [Addy's new book](https://www.smashingmagazine.com/2021/04/image-optimization-pre-release/) (also, check a [free PDF preview](https://smashingmagazine.com/provide/eBooks/image-optimization-sample-chapter.pdf)).
description: >-
  Images have also been a key part of the web. They communicate ideas instantly, but they are also a lot heavier than text to load. This means that it’s essential to get loading and displaying them right, if you want to give your users a fantastic first impression. An excerpt from [Addy's new book](https://www.smashingmagazine.com/2021/04/image-optimization-pre-release/) (also, check a [free PDF preview](https://smashingmagazine.com/provide/eBooks/image-optimization-sample-chapter.pdf)).
categories:
  - Performance
  - User Experience
  - Core Web Vitals
  - Next.js
  - Media
disable_ads: true
---

The humble `<img>` element has gained some superpowers over the years. Given how central it is to image optimization on the web, let’s catch up on what it can do and how it can help improve user experience and the [Core Web Vitals](https://web.dev/vitals/). I’ll be covering image optimization in more depth in Smashing Magazine’s [new book on Image Optimization](https://www.smashingmagazine.com/2021/04/image-optimization-pre-release/).

Some tips to get us started:

- For a fast [Largest Contentful Paint](https://web.dev/lcp/):
  - Request your key hero image early.
  - Use srcset + efficient modern image formats.
  - Avoid wasting pixels (compress, don’t serve overly high DPR images).
  - Lazy-load offscreen images (reduce network contention for key resources).
- For a low [Cumulative Layout Shift](https://web.dev/cls/):
  - Set dimensions (width, height) on your images.
  - Use CSS aspect-ratio or aspect ratio boxes to reserve space otherwise.
- For low impact to [First Input Delay](https://web.dev/fid/): 
  - Avoid images causing network contention with other critical resources like CSS and JS. While not render-blocking, they can indirectly impact render performance.

**Note**: *Modern image components that build on `<img>`, like [Next.js `<Image>`](https://nextjs.org/docs/api-reference/next/image) (for React) and [Nuxt image](https://image.nuxtjs.org/) (for Vue) try to bake in as many of these concepts as possible by default. We’ll cover this later. You can of course also do this manually just using the `<img>` element directly. If using 11ty for your static sites, try the [11ty high-performance blog template](https://github.com/google/eleventy-high-performance-blog).*

### How Do Images Impact User Experience And The Core Web Vitals?

You may have heard of Core Web Vitals (CWV). It’s an initiative by Google to share unified guidance for quality signals that can be key to delivering a great user experience on the web. CWV is part of a set of [page experience signals](https://developers.google.com/search/blog/2020/11/timing-for-page-experience) Google Search will be evaluating for ranking. Images can impact the CWV in a number of ways.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7ec5e4a-099e-4a1a-a1a3-b7545835520f/26-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7ec5e4a-099e-4a1a-a1a3-b7545835520f/26-humble-img-element-and-core-web-vitals.png" width="800" height="450" sizes="100vw" caption="Images can impact the Core Web Vitals in a number of ways. E.g. LCP measures when the largest contentful element (images, text) in a user’s viewport, such as one of these images, becomes visible. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7ec5e4a-099e-4a1a-a1a3-b7545835520f/26-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Largest Contentful Paint" >}}

In many modern web experiences, images tend to be the largest visible element when a page completes loading. These include Hero images, images from carousels, stories and banners. [Largest Contentful Paint](https://web.dev/lcp/) (LCP) is a Core Web Vitals metric that measures when the largest contentful element (images, text) in a user’s viewport, such as one of these images, becomes visible.

This allows a browser to determine when **the main content of the page has finished rendering**. When an image is the largest contentful element, how slowly that image loads can impact LCP. In addition to applying image compression (e.g using [Squoosh](https://squoosh.app), [Sharp](https://sharp.pixelplumbing.com/), [ImageOptim](https://imageoptim.com/mac) or an [image CDN](https://web.dev/image-cdns/)), and using a modern image format, you can tweak the `<img>` element to serve the most appropriate responsive version of an image or lazy-load it.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0586dfdb-1e83-485b-92c0-ba38b3df2298/9-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0586dfdb-1e83-485b-92c0-ba38b3df2298/9-humble-img-element-and-core-web-vitals.png" width="800" height="379" sizes="100vw" caption="Largest Contentful Paint displayed in the WebPageTest filmstrip. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0586dfdb-1e83-485b-92c0-ba38b3df2298/9-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Largest Contentful Paint displayed in the WebPageTest filmstrip." >}}

Layout shifts can be distracting to users. Imagine you’ve started reading an article when all of a sudden elements shift around the page, throwing you off and requiring you to find your place again. [Cumulative Layout Shift](https://web.dev/cls) (CLS, a Core Web Vitals metric) measures the instability of content. The most common causes of CLS include images without dimensions (see below) which can push down content when they load and snap into place; ignoring them means the browser may not be able to reserve sufficient space in advance of them loading.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaa1694e-29b1-456f-9b17-e8f75bc702ac/22-humble-img-element-and-core-web-vitals.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b68950a7-bcf0-4e38-8447-ec97aee9a3e4/22-humble-img-element-and-core-web-vitals-800w.gif" width="800" height="450" alt="Cumulative Layout Shift" /></a><figcaption>Generated using <a href='https://defaced.dev/tools/layout-shift-gif-generator/'>Layout Shift GIF Generator</a>. You may also be interested in the <a href='https://webvitals.dev/cls/G1hinueOMKWaKLJFJcQW'>CLS Debugger</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaa1694e-29b1-456f-9b17-e8f75bc702ac/22-humble-img-element-and-core-web-vitals.gif">Large preview</a>)</figcaption></figure>

It’s possible for images to block a user’s bandwidth and CPU on page load. They can get in the way of how critical resources are loaded, in particular on slow connections and lower-end mobile devices leading to bandwidth saturation. [First Input Delay](https://web.dev/fid) (FID) is a Core Web Vitals metric that captures a user’s first impression of a site’s interactivity and responsiveness. By reducing main-thread CPU usage, FID can also be reduced.

{{% feature-panel %}} 

### Lighthouse

In this guide, we will be using Lighthouse to identify opportunities to improve the Core Web Vitals. [Lighthouse](https://github.com/GoogleChrome/lighthouse) is an open-source, automated tool for improving the quality of web pages. You can find it in the [Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools) suite of debugging tools and run it against any web page, public or requiring authentication. You can also find Lighthouse in [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fstore.google.com), [CI](https://github.com/GoogleChrome/lighthouse-ci) and [WebPageTest](https://www.webpagetest.org/easy). 

Keep in mind that Lighthouse is a lab tool. While great for looking at opportunities to improve your user experience, always try to consult [real-world data](https://web.dev/vitals-field-measurement-best-practices/) for a complete picture of what actual users are seeing.

## The Basics

To place an image on a web page, we use the `<img>` element. This is an empty element &mdash; it has **no closing tag** &mdash; requiring a minimum of one attribute to be helpful: `src`, the source. If an image is called *donut.jpg* and it exists in the same path as your HTML document, it can be embedded as follows:

<pre><code class="language-html">&lt;img src="donut.jpg"&gt;</code></pre>

To ensure our image is accessible, we add the **`alt` attribute**. The value of this attribute should be a textual description of the image, and is used as an alternative to the image when it can’t be displayed or seen; for example, a user accessing your page via a screen reader. The above code with an `alt` specified looks as follows:

<pre><code class="language-html">&lt;img src="donut.jpg"
     alt="A delicious pink donut."&gt;</code></pre>

Next, we add **`width` and `height` attributes** to specify the width and height of the image, otherwise known as the image’s dimensions. The dimensions of an image can usually be found by looking at this information via your operating system’s file explorer (`Cmd + I` on macOS).

<pre><code class="language-html">&lt;img src="donut.jpg"
     alt="A delicious pink donut."
     width="400"
     height="400"&gt;</code></pre>

When `width` and `height` are specified on an image, the browser knows how much space to reserve for the image until it is downloaded. Forgetting to include the image’s dimensions **can cause layout shifts**, as the browser is unsure how much space the image will need.

Modern browsers now set the default aspect ratio of images based on an image’s `width` and `height` attributes, so it’s valuable to set them to prevent such layout shifts.

### Identify The Largest Contentful Paint Element

Lighthouse has a “Largest Contentful Paint element” audit that identifies what element was the largest contentful paint. Hovering over the element will highlight it in the main browser window.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb33b855-689f-4bd2-be04-23d1388ffa7d/8-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb33b855-689f-4bd2-be04-23d1388ffa7d/8-humble-img-element-and-core-web-vitals.png" width="800" height="498" sizes="100vw" caption="To identify the Largest Contentful Paint, spot the LCP in the Lighthouse metric. It also shows up on hover in the DevTools Performance panel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb33b855-689f-4bd2-be04-23d1388ffa7d/8-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Lighthouse’s LCP " >}}

If this element is an image, this information is a useful hint you may want to optimize the loading of this image. You might also find this helpful [LCP Bookmarklet](https://gist.github.com/anniesullie/cf2982342337fd1b2be95c2d5fe5ea06) by Annie Sullivan useful for quickly identifying the LCP element with a red rectangle in just one click.  
 
**Note:** The Largest Contentful Paint element candidate [can change](https://web.dev/lcp/) through the page load. For this reason, it’s valuable to not just look at what synthetic tooling like Lighthouse may say, but also consult what [real users](https://web.dev/debug-web-vitals-in-the-field/) see.
 
Hovering over an image in the Chrome DevTools *Elements* panel will display the dimensions of the image as well as the image’s intrinsic size.

{{< rimg breakout="true" ref="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44a6b541-9296-44b4-a751-36e196c85bea/11-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44a6b541-9296-44b4-a751-36e196c85bea/11-humble-img-element-and-core-web-vitals.png" width="800" height="491" sizes="100vw" caption="Hovering over an image in the Chrome DevTools 'Elements' panel will display the dimensions of the image as well as the image’s intrinsic size. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44a6b541-9296-44b4-a751-36e196c85bea/11-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Chrome DevTools Elements panel" >}}

### Identify Layout Shifts From Images Without Dimensions

To [limit](https://web.dev/optimize-cls/#images-without-dimensions) Cumulative Layout Shift being caused by images without dimensions, include width and height size attributes on your images and video elements. This approach ensures that the browser can allocate the correct amount of space in the document while the image is loading. Lighthouse will highlight images without a width and height:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99f5d069-f622-4d88-abf7-4ef8c6102135/28-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99f5d069-f622-4d88-abf7-4ef8c6102135/28-humble-img-element-and-core-web-vitals.png" width="800" height="489" sizes="100vw" caption="It's a good idea to always include width and height size attributes on your images and video elements. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99f5d069-f622-4d88-abf7-4ef8c6102135/28-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Lighthouse highlights images without a width and height" >}}

See [Setting Height And Width On Images Is Important Again](https://www.smashingmagazine.com/2020/03/setting-height-width-images-important-again/) for a good write-up on the importance of thinking about image dimensions and aspect ratio.

## Responsive Images

What about switching image resolution? A standard `<img>` only allows us to supply a single source file to the browser. But with the `srcset` and `sizes` attributes, we can provide many additional source images (and hints) so the browser can pick the most appropriate one. This allows us to supply images that are smaller or larger.

<pre><code class="language-html">&lt;img src="donut-800w.jpg"
     alt="A delicious pink donut."
     width="400"
     height="400"
     srcset="donut-400w.jpg 400w,
             donut-800w.jpg 800w"
     sizes="(max-width: 640px) 400px,
            800px"&gt;</code></pre>

The `srcset` attribute defines the set of images the browser can select from, as well as the size of each image. Each image string is separated by a comma and includes:

- a source filename (`donut-400w.jpg`);
- a space;
- and the image’s intrinsic width specified in pixels (`400w`), or a pixel density descriptor (`1x`, `1.5x`, `2x`, and so on).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4fe95fd-8245-4a33-bc8b-dbe0f0b8ee24/4-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4fe95fd-8245-4a33-bc8b-dbe0f0b8ee24/4-humble-img-element-and-core-web-vitals.png" width="800" height="330" sizes="100vw" caption="From <a href='https://youtu.be/YJGCZCaIZkQ?t=839'>Speed at Scale</a> with Katie Hempenius and I at Google I/O. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4fe95fd-8245-4a33-bc8b-dbe0f0b8ee24/4-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="From Speed at Scale with Katie Hempenius and I at Google I/O." >}}

The `sizes` attribute specifies a set of conditions, such as screen widths, and what image size is best to select when those conditions are met. Above, (`max-width:640px`) is a media condition asking “if the viewport width is 640 pixels or less,” and `400px` is the width of the slot, the image is going to fill when the media condition is true. This typically corresponds to the page’s responsive breakpoints.

### Device Pixel Ratio (DPR) / Pixel Density Capping

Device Pixel Ratio (DPR) represents how a CSS pixel is translated to physical pixels on a hardware screen. [High resolution](https://web.dev/choose-the-right-image-format/#implications-of-high-resolution-screens) and retina screens use more physical pixels to represent CSS pixels for imagery that is sharper and has more detailed visuals.

The human eye may not be capable of distinguishing the difference between images that are a 2x-3x DPR vs. an even higher resolution. Serving overly high DPR images is a common problem for sites leveraging `<img srcset>` and a suite of image sizes.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dc5f7c1-4ccb-4ba0-96a2-38ba56c259f8/21-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dc5f7c1-4ccb-4ba0-96a2-38ba56c259f8/21-humble-img-element-and-core-web-vitals.png" width="800" height="443" sizes="100vw" caption="Twitter capped their image fidelity at 2x, resulting in 33% faster timeline image loading times. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dc5f7c1-4ccb-4ba0-96a2-38ba56c259f8/21-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Device Pixel Ratio" >}}

It may be possible to use DPR-capping to serve your users an image at a 2x or 3x fidelity to prevent large image payloads. Twitter [capped](https://blog.twitter.com/engineering/en_us/topics/infrastructure/2019/capping-image-fidelity-on-ultra-high-resolution-devices.html) their image fidelity at 2x, resulting in 33% faster timeline image loading times. They found that 2x was a sweet spot of both good performance wins with no degradation in quality metrics. 

**Note:** This approach to DPR-capping is currently not possible if using “w” descriptors.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebaff10-259a-46d1-8d34-cb680f3c4a1d/13-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebaff10-259a-46d1-8d34-cb680f3c4a1d/13-humble-img-element-and-core-web-vitals.png" width="800" height="277" sizes="100vw" caption="Twitter's assets for 1×, 2× and 3× scale. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebaff10-259a-46d1-8d34-cb680f3c4a1d/13-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="difference between images 1x, 2x, 3x scale." >}}

### Identify Images That Can Be Better Sized

Lighthouse includes a number of image optimization audits for helping you understand if your images could be better compressed, delivered in a more optimal modern image format, or resized.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afc46056-132d-4f08-a512-734f3e567f01/1-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afc46056-132d-4f08-a512-734f3e567f01/1-humble-img-element-and-core-web-vitals.png" width="800" height="468" sizes="100vw" caption="Lighthouse’ notes on appropriately-sized images. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afc46056-132d-4f08-a512-734f3e567f01/1-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Image optimization audits in the Lighthouse" >}}

Even those images which are responsive (that is, sized relative to the viewport) should have a width and height set. In modern browsers, these attributes establish an aspect ratio that helps prevent layout shifts, even if the absolute sizes are overridden by CSS. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0126a7a6-c948-4009-a696-aca01ee02452/27-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0126a7a6-c948-4009-a696-aca01ee02452/27-humble-img-element-and-core-web-vitals.png" width="800" height="604" sizes="100vw" caption="<a href='https://responsivebreakpoints.com/'>Responsive Breakpoints</a> helps you determine the optimal image breakpoints and generate srcset code for responsive images. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0126a7a6-c948-4009-a696-aca01ee02452/27-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="responsivebreakpoints.com which determines the optimal image breakpoints." >}}

When not using an image CDN or framework, I like to use [responsivebreakpoints.com](https://responsivebreakpoints.com/) to determine the optimal image breakpoints and generate `<img>` srcset code for my responsive images.

{{% ad-panel-leaderboard %}}

## Serving Modern Image Formats

Art direction allows us to serve different images depending on a user’s display. While responsive images load different sizes of the same image, art direction can load very different images based on the display.

The browser can choose which image format to display using the `<picture>` element. The `<picture>` element supports multiple `<source>` elements and a single `<img>` element, which can reference sources for different formats including AVIF, WebP, and eventually JPEG XL.

<pre><code class="language-html">&lt;picture&gt;
    &lt;source srcset="puppy.jxl" type="image/jxl"&gt;
    &lt;source srcset="puppy.avif" type="image/avif"&gt;
    &lt;source srcset="puppy.webp" type="image/webp"&gt;
    &lt;source srcset="puppy.jpg" type="image/jpeg"&gt;
    &lt;img src="puppy.jpg" alt="Cute puppy"&gt;
&lt;/picture&gt;</code></pre>

In this example, the browser will begin to parse the sources and will stop when it has found the first supported match. If no match is found, the browser loads the source specified in `<img>` as the fallback. This approach works well for serving any modern image format not supported in all browsers. Be careful with **ordering `<source>` elements** as order matters. Don’t place modern sources after legacy formats, but instead put them before. Browsers that understand it will use them and those that don’t will move onto more widely supported frameworks.

Understanding the myriad of image format options out there today can be a confusing process, but you may find Cloudinary’s [comparison of modern image formats](https://cloudinary.com/blog/time_for_next_gen_codecs_to_dethrone_jpeg) helpful:

{{< rimg breakout="true" href="https://cloudinary.com/blog/time_for_next_gen_codecs_to_dethrone_jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdff6efa-91ba-43a1-84c0-96d309bd64bc/12-humble-img-element-and-core-web-vitals.png" width="800" height="255" sizes="100vw" caption="There are plenty of format options for images. A <a href='https://cloudinary.com/blog/time_for_next_gen_codecs_to_dethrone_jpeg'>handy overview on Cloudinary blog</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdff6efa-91ba-43a1-84c0-96d309bd64bc/12-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Cloudinary’s comparison of modern image formats." >}}

You may also find Malte Ubl’s [AVIF and WebP quality settings picker](https://avif-webp-quality-setting.industrialempathy.com/) useful for selecting quality settings to match the quality of a JPEG at a particular given quality setting. 

### Identify Images That Could Be Served In A More Modern Format

Lighthouse (below) highlights potential savings from serving images in a next-generation format. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8241f6e4-85b2-4bb8-9e18-d76e9d9ebe40/6-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8241f6e4-85b2-4bb8-9e18-d76e9d9ebe40/6-humble-img-element-and-core-web-vitals.png" width="800" height="380" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8241f6e4-85b2-4bb8-9e18-d76e9d9ebe40/6-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Lighthouse highlights potential savings from serving images in a next-generation format." >}}

**Note:** We have an [open issue](https://github.com/GoogleChrome/lighthouse/issues/12295) to better highlight the potential savings for AVIF in Lighthouse.

You might also find value in using image auditing tools such as [Cloudinary’s image analysis tool](https://webspeedtest.cloudinary.com/) for a deeper look at image compression opportunities for all the images on a page. As a bonus, you can download compressed versions of suggested image formats such as WebP:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c887b50b-adaf-4f63-9457-b028efb0282f/10-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c887b50b-adaf-4f63-9457-b028efb0282f/10-humble-img-element-and-core-web-vitals.png" width="800" height="583" sizes="100vw" caption="<a href='https://webspeedtest.cloudinary.com/'>Cloudinary’s image analysis tool</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c887b50b-adaf-4f63-9457-b028efb0282f/10-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Cloudinary’s image analysis tool" >}}

I also enjoy using [Squoosh](https://squoosh.app/) for its support of bleeding-edge formats, such as JPEG XL as it offers a low-friction way to experiment with modern formats outside of a CLI or CDN.

{{< rimg breakout="true" href="https://squoosh.app/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3080fb2-5664-4e34-962f-134dfbb39571/18-humble-img-element-and-core-web-vitals.png" width="800" height="490" sizes="100vw" caption="<a href='https://squoosh.app/'>Squoosh</a> supports cutting-edge formats, such as JPEG XL, but also AVIF. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3080fb2-5664-4e34-962f-134dfbb39571/18-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Squoosh" >}}

There are multiple ways to approach sizing issues as both srcset and sizes are both usable on `<picture>` and `<img>`. when in doubt, use `<img>` with srcset/sizes for single images that have a simple layout. Use `<picture>` for serving multiple formats, complex layout and art direction.
  
Chrome DevTools allows you to disable modern image formats ([demo](https://twitter.com/addyosmani/status/1327174361942552576?lang=en)), like WebP, AVIF or JPEG XL, to test differing fallbacks for them in the *Rendering* panel:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cce8a527-1562-40fb-8793-15c3dd4a2a9b/3-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cce8a527-1562-40fb-8793-15c3dd4a2a9b/3-humble-img-element-and-core-web-vitals.png" width="800" height="555" sizes="100vw" caption="Chrome DevTools allows you to test differing fallbacks for WebP, AVIF or JPEG XL in the Rendering panel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cce8a527-1562-40fb-8793-15c3dd4a2a9b/3-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Chrome DevTools allows you to test differing fallbacks for WebP, AVIF or JPEG XL in the Rendering panel." >}}

<p>CanIUse has the latest browser support details for <a href="https://caniuse.com/webp">WebP</a>, <a href="https://caniuse.com/avif">AVIF</a> and <a href="https://caniuse.com/jpegxl">JPEG XL</a>.</p>

### Content Negotiation

An alternative to manually handling image format selection using `<picture>` is to rely on the [accept header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept). This is sent by the client, allowing the server to deliver an image format that is the best fit for the user. CDNs such as [Akamai](https://www.akamai.com/de/de/products/performance/image-and-video-manager.jsp), [Cloudinary](https://cloudinary.com/) and [Cloudflare](https://support.cloudflare.com/hc/en-us/articles/360000607372-Using-Cloudflare-Polish-to-compress-images) support it.

## Image Lazy Loading

What about offscreen images that are not visible until a user scrolls down the page? In the example below, all the images on the page are “eagerly loaded” (the default in browsers today), causing the user to download 1.1 MB of images. This can cause users’ data plans to take a hit in addition to affecting performance.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4541861a-1fde-4c81-9bde-158d2e274385/16-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4541861a-1fde-4c81-9bde-158d2e274385/16-humble-img-element-and-core-web-vitals.png" width="800" height="491" sizes="100vw" caption="An image gallery eagerly loading all the images it needs upfront, as shown in the Chrome DevTools <strong>Network</strong> panel. 1.1 MB of images have been downloaded, despite only a small number being visible when the user first lands on the page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4541861a-1fde-4c81-9bde-158d2e274385/16-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="An image gallery eagerly loading all the images it needs upfront, as shown in the Chrome DevTools Network panel. 1.1 MB of images have been downloaded, despite only a small number being visible when the user first lands on the page. " >}}

Using the [loading attribute](https://web.dev/native-lazy-loading/) on `<img>`, we can control the behavior of image loading. `loading="lazy"` lazy-loads images, deferring their loading until they reach a calculated distance from the viewport. `loading="eager"` loads images right away, regardless of their visibility in the viewport. `eager` is the default so doesn’t need to be explicitly added (that is, just use `<img>` for eager loading).

Below is an example of lazy-loading an `<img>` with a single source:

<pre><code class="language-html">&lt;img src="donut.jpg"
     alt="A delicious pink donut."
     loading="lazy"
     width="400"
     height="400"&gt;</code></pre>
     
With native `<img>` lazy-loading, the earlier example now downloads only about 90 KB of images! Just adding `loading="lazy"` to our offscreen images has a huge impact. You ideally want to lazy-load all images present [outside of the initial viewport](https://web.dev/browser-level-image-lazy-loading/#avoid-lazy-loading-images-that-are-in-the-first-visible-viewport) and avoid it for everything that is within the initial viewport.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba1ed82b-e5b9-45a8-b8ba-0bcfaf3a7715/7-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba1ed82b-e5b9-45a8-b8ba-0bcfaf3a7715/7-humble-img-element-and-core-web-vitals.png" width="800" height="491" sizes="100vw" caption="An image gallery using native image lazy-loading on images outside of the viewport. As seen in the Chrome DevTools <strong>Network</strong> panel, the page now only downloads the bare minimum of images users need upfront. The rest of the images are loaded in as users scroll down the page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba1ed82b-e5b9-45a8-b8ba-0bcfaf3a7715/7-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="An image gallery using native image lazy-loading on images outside of the viewport. As seen in the Chrome DevTools Network panel, the page now only downloads the bare minimum of images users need upfront. The rest of the images are loaded in as users scroll down the page." >}}

Lazy loading also works with images that include `srcset`:

<pre><code class="language-html">&lt;img src="donut-800w.jpg"
     alt="A delicious donut"
     width="400"
     height="400"
     srcset="donut-400w.jpg 400w,
             donut-800w.jpg 800w"
     sizes="(max-width: 640px) 400px,
            800px"
     loading="lazy"&gt;</code></pre>

In addition to working on `srcset`, the loading attribute also works on `<img>` inside `<picture>`:

<div class="break-out">

<pre><code class="language-html">&lt;!-- Lazy-load images in &lt;picture&gt;. 
&lt;img&gt; is the one driving image loading so &lt;picture&gt; and srcset fall off of that --&gt;
&lt;picture&gt;
  &lt;source media="(min-width: 40em)" srcset="big.jpg 1x, big-hd.jpg 2x"&gt;
  &lt;source srcset="small.jpg 1x, small-hd.jpg 2x"&gt;
  &lt;img src="fallback.jpg" loading="lazy"&gt;
&lt;/picture&gt;</code></pre>
</div>

The Lighthouse Opportunities section lists any offscreen or hidden images on a page that can be lazy-loaded as well as the potential savings from doing so.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68cad1af-a26e-449a-b3ec-cc02708844d0/23-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68cad1af-a26e-449a-b3ec-cc02708844d0/23-humble-img-element-and-core-web-vitals.png" width="800" height="417" sizes="100vw" caption="Lighthouse Opportunities section lists any offscreen or hidden images on a page that can be lazy-loaded as well as the potential savings from doing so. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68cad1af-a26e-449a-b3ec-cc02708844d0/23-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Lighthouse Opportunities section lists any offscreen or hidden images on a page that can be lazy-loaded as well as the potential savings from doing so." >}}

<p>See <a href="https://caniuse.com/loading-lazy-attr">CanIUse.com</a> for latest browser support for native image lazy-loading.</p>

## Request Your Image Early

Help the browser discover your LCP image early so that it can fetch and render it with minimal delay. Where possible, attempt to solve this by better minimizing the request chains to your LCP image so that the browser doesn’t need to first fetch, parse and execute JavaScript or wait for a component to render/hydrate to discover the image.

`<link rel=preload>` can be used with `<img>` to allow browsers to discover critical resources you want to load as soon as possible, prior to them being found in HTML. 

<pre><code class="language-html">&lt;link rel="preload" as="image" href="donut.jpg"&gt;</code></pre>

If you are optimizing LCP, preload can help boost how soon late-discovered hero images (e.g such as those loaded by JavaScript or background hero images in CSS) are fetched. Preload can make a meaningful difference if you need critical images (like Hero images) to be prioritized over the load of other images on a page. 

**Note:** Use preload sparingly and *always* measure its impact in production. If the preload for your image is earlier in the document than it is, this can help browsers discover it (and order relative to other resources). When used incorrectly, preloading can *cause your image to delay* [*First Contentful Paint*](https://web.dev/fcp) (e.g CSS, Fonts) &mdash; the opposite of what you want. Also note that for such reprioritization efforts to be effective, it also [depends on servers prioritizing requests correctly](https://github.com/andydavies/http2-prioritization-issues#cdns--cloud-hosting-services).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/351c2652-e0f8-4af8-8476-e187c4b607ba/2-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/351c2652-e0f8-4af8-8476-e187c4b607ba/2-humble-img-element-and-core-web-vitals.png" width="800" height="459" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/351c2652-e0f8-4af8-8476-e187c4b607ba/2-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="preload for optimizing LCP." >}}

Preload can be used to fetch sources for an `<img>` of a particular format:

<div class="break-out">

<pre><code class="language-html">&lt;link rel="preload" as="image" href="donut.webp" type="image/webp"&gt;</code></pre>
</div>

**Note:** This approach only preloads the latest format where supported, however cannot be used to preload multiple supported formats as this would preload both of them.

[Preload can also be used to fetch responsive images](https://web.dev/preload-responsive-images/) so the correct source is discovered sooner:

<pre><code class="language-html">&lt;link rel="preload" as="image" 
     href="donut.jpg" 
     imagesrcset="
        poster_400px.jpg 400w, 
        poster_800px.jpg 800w, 
        poster_1600px.jpg 1600w" 
    imagesizes="50vw"&gt;</code></pre>

Take care not to overuse preload (when each resource is considered important, none of them really are). Reserve it for critical resources which the browser’s preload scanner may not be able to quickly find organically.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9bac55c-65c7-4d01-883f-68d7faa2fb0e/15-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9bac55c-65c7-4d01-883f-68d7faa2fb0e/15-humble-img-element-and-core-web-vitals.png" width="800" height="489" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9bac55c-65c7-4d01-883f-68d7faa2fb0e/15-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Preload in the Lighthouse." >}}

Lighthouse suggests opportunities to apply this optimization in Lighthouse 6.5 and above. 
 
See [CanIUse.com](https://caniuse.com/link-rel-preload) for latest browser support for link rel=preload.

{{% ad-panel-leaderboard %}}

## Image Decoding

Browsers need to decode the images they download in order to turn them into pixels on your screen. However, how browsers handle deferring images can vary. At the time of writing, Chrome and Safari present images and text together – synchronously – if possible. This looks correct visually, but images have to be decoded, which can mean text isn’t shown until this work is done. The `decoding` attribute on `<img>` allows you to signal a preference between synchronous and asynchronous image decoding.

<pre><code class="language-html">&lt;img src="donut-800w.jpg"
     alt="A delicious donut"
     width="400"
     height="400"
     srcset="donut-400w.jpg 400w,
             donut-800w.jpg 800w"
     sizes="(max-width: 640px) 400px,
            800px"
     loading="lazy"
     decoding="async"&gt;</code></pre>
     
`decoding="async"` suggests it’s OK for image decoding to be deferred, meaning the browser can rasterize and display content without images while scheduling an asynchronous decode that is off the critical path. As soon as image decoding is complete, the browser can update the presentation to include images. `decoding=sync` hints that the decode for an image should not be deferred, and `decoding="auto"` lets the browser do what it determines is best.

*(Updated: May 5, 2021)*: Decoding images is not *"async"* (not blocking raster) by default. If this were the case, too much content on the web would end up flashing on load. However, all decodes are off the main thread.

**Note**: *See [CanIUse.com](https://caniuse.com/mdn-html_elements_img_decoding) for the latest browser support for the decoding attribute.*

### Placeholders

What if you would like to show the user a placeholder while the image loads? The `background-image` CSS property allows us to set background images on an element, including the `<img>` tag or any parent container elements. We can combine `background-image` with `background-size: cover` to set the size of an element’s background image and scale the image as large as possible without stretching the image.

Placeholders are often inline, Base64-encoded data URLs which are low-quality image placeholders (LQIP) or SVG image placeholders (SQIP). This allows users to get a very quick preview of the image, even on slow network connections, before the sharper final image loads in to replace it.

<pre><code class="language-html">&lt;img src="donut-800w.jpg"
     alt="A delicious donut"
     width="400"
     height="400"
     srcset="donut-400w.jpg 400w,
             donut-800w.jpg 800w"
     sizes="(max-width: 640px) 400px,
            800px"
     loading="lazy"
     decoding="async"
     style="background-size: cover; 
            background-image:
              url(data:image/svg+xml;base64,[svg text]);"&gt;</code></pre>
              
**Note:** Given that Base64 data URLs can be quite long, `[svg text]` is denoted in the example above to improve readability.

With an inline SVG placeholder, here is how the example from earlier now looks when loaded on a very slow connection. Notice how users are shown a preview right away prior to any full-size images being downloaded:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53961d0b-133f-4141-9a79-aa5c1fc9a37d/29-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53961d0b-133f-4141-9a79-aa5c1fc9a37d/29-humble-img-element-and-core-web-vitals.png" width="800" height="491" sizes="100vw" caption="Images loaded on a simulated slow connection, displaying a placeholder approximating the final image as it loads in. This can improve perceived performance in certain cases. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53961d0b-133f-4141-9a79-aa5c1fc9a37d/29-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Images loaded on a simulated slow connection, displaying a placeholder approximating the final image as it loads in. This can improve perceived performance in certain cases." >}}

There are a variety of modern solutions for image placeholders (e.g CSS background-color, LQIP, SQIP, [Blur Hash](https://blurha.sh/), Potrace). Which approach makes the most sense for your user experience may depend on how much you’re attempting to offer a preview of the final content, display progress (e.g progressive loading) or just avoid a visual flash when the image finally loads in. I’m personally excited for [JPEG XL’s support](https://cloudinary.com/blog/time_for_next_gen_codecs_to_dethrone_jpeg) for full progressive rendering.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6d56acc-23b9-4140-992f-535397407d56/19-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6d56acc-23b9-4140-992f-535397407d56/19-humble-img-element-and-core-web-vitals.png" width="800" height="691" sizes="100vw" caption="<a href='https://github.com/WICG/largest-contentful-paint/issues/68#issuecomment-742141525'>Perceptual image loading methods</a> from Gunther Brunner of CyberAgent. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6d56acc-23b9-4140-992f-535397407d56/19-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Perceptual image loading methods from Gunther Brunner of CyberAgent." >}}

Ultimately including an inline data URL for your low-quality placeholder image that is served in the initial HTML within the `<img>`’s styles avoids the need for an additional network request. I’d consider a placeholder size of being <= 1-2KB as being optimal. [LCP will take into account the placeholder image’s intrinsic size](https://web.dev/lcp/#how-is-an-element's-size-determined) so ideally aim for the “preview” to match the intrinsic size of the real image being loaded.

**Note:** There is an [open issue](https://github.com/WICG/largest-contentful-paint/issues/71) to discuss factoring in progressive loading specifically into the Largest Contentful Paint metric. 

## Lazy-render Offscreen Content

Next, let’s discuss the [CSS `content-visibility`](https://web.dev/content-visibility/) property, which allows the browser to skip rendering, layout and paint for elements until they are needed. This can help optimize page load performance if a large quantity of your page’s content is offscreen, including content which uses `<img>` elements. `content-visibility:auto` can [reduce](https://www.industrialempathy.com/posts/image-optimizations/#lazy-rendering) how much CPU work the browser has to do less work upfront, including offscreen image decoding.

<pre><code class="language-css">section {
  content-visibility: auto;
}</code></pre>

The `content-visibility` property can take a number of values, however, `auto` is the one that offers performance benefits. Sections of the page with `content-visibility: auto` get containment for layout, paint and style containment. Should the element be off-screen, it would also get size containment. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b998a72-f23c-473c-9c4a-bfac82fade53/31-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b998a72-f23c-473c-9c4a-bfac82fade53/31-humble-img-element-and-core-web-vitals.png" width="800" height="450" sizes="100vw" caption="When chunking up a page into sections with <code>content-visibility:auto</code>, developers have observed a 7-10x improvement in rendering times as a result &mdash; note the reduction in rendering times above of 937ms to 37ms for a long HTML document. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b998a72-f23c-473c-9c4a-bfac82fade53/31-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Sections of the page with <code>content-visibility:auto</code>" >}}

Browsers don’t paint the image content for content-visibility affected images, so this approach may introduce some savings. 
 

<pre><code class="language-css">section {
  content-visibility: auto;
  contain-intrinsic-size: 700px; 
}</code></pre>

You can pair `content-visibility` with `contain-intrinsic-size` which provides the natural size of the element if it is impacted by size containment. The `700px` value in this example approximates the width and height of each chunked section.  

See [CanIUse.com](https://caniuse.com/css-content-visibility) for latest browser support for CSS content-visibility.

## Next.js Image Component

Next.js now includes an [Image component](https://nextjs.org/docs/api-reference/next/image) with several of the above best practices baked in. The image component handles image optimization, generating responsive images (automating `<img srcset>`) and lazy-loading in addition to many other capabilities. This is just one of the optimizations that has come out of the Chrome and Next.js teams [collaborating](https://nextjs.org/blog/next-10#built-in-image-component-and-automatic-image-optimization) with sites adopting it seeing up to a 60% better LCP and 100% better CLS.

In the below Next.js example, the standard `<img>` element is first used to load 3 donut images downloaded from Unsplash.

<div class="break-out">

<pre><code class="language-javascript">import Head from 'next/head';
export default function Index() {
    return (
        &lt;div&gt;
            &lt;Head&gt;
                &lt;title&gt;Create Next App&lt;/title&gt;
            &lt;/Head&gt;

            &lt;main&gt;
                &lt;div&gt;
                    &lt;img src="/donut1.jpeg" alt="Donut" height={700} width={700} /&gt;
                    &lt;img src="/donut2.jpeg" alt="Donut" height={700} width={700} /&gt;
                    &lt;img src="/donut3.jpeg" alt="Donut" height={700} width={700} /&gt;
                &lt;/div&gt;
            &lt;/main&gt;
        &lt;/div&gt;
    );
}</code></pre>
</div>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38c4e66b-2ab3-4327-9577-979744ee7e86/25-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38c4e66b-2ab3-4327-9577-979744ee7e86/25-humble-img-element-and-core-web-vitals.png" width="800" height="688" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38c4e66b-2ab3-4327-9577-979744ee7e86/25-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Image Component with Next.js" >}}

When this page is loaded with the DevTools network panel open, we see that our images are very large in size (325KB + 4.5MB + 3.6MB = 8.4MB in total), they all load regardless of whether the user can see them and are likely not as optimized as they could be.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9df0857c-602e-4e31-91aa-646287d179a3/14-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9df0857c-602e-4e31-91aa-646287d179a3/14-humble-img-element-and-core-web-vitals.png" width="800" height="403" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9df0857c-602e-4e31-91aa-646287d179a3/14-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="with the DevTools network panel open, we see that our images are very large in size (325KB + 4.5MB + 3.6MB = 8.4MB in total)." >}}

Loading images at these sizes is unnecessary, in particular if our user is on a mobile device. Let’s now use the Next.js image component instead. We import it in from 'next/image' and replace all our `<img>` references with `<Image>`. 

<div class="break-out">

<pre><code class="language-javascript">import Head from 'next/head';
import Image from 'next/image';

export default function Index() {
    return (
        &lt;div&gt;
            &lt;Head&gt;
                &lt;title&gt;Next.js Image Component&lt;/title&gt;
            &lt;/Head&gt;
            &lt;main&gt;
                &lt;div&gt;
                    &lt;Image src="/donut1.jpeg" alt="Donut" height={700} width={700} /&gt;
                    &lt;Image src="/donut2.jpeg" alt="Donut" height={700} width={700} /&gt;
                    &lt;Image src="/donut3.jpeg" alt="Donut" height={700} width={700} /&gt;
                &lt;/div&gt;
            &lt;/main&gt;
        &lt;/div&gt;
    );
}</code></pre>
</div>

We can reload our page and take a second look at the DevTools network panel. Now only 1 image is being loaded by default (the only one visible in the viewport), it’s significantly smaller than the original (&#126;33KB vs 325KB) and uses a more modern format (WebP).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7949bff6-332a-447d-a647-441a9bb05e02/20-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7949bff6-332a-447d-a647-441a9bb05e02/20-humble-img-element-and-core-web-vitals.png" width="800" height="403" sizes="100vw" caption="An image is being loaded by default (the only one visible in the viewport), it’s significantly smaller than the original (approx. 33KB vs 325KB) and uses a more modern format (WebP). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7949bff6-332a-447d-a647-441a9bb05e02/20-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="An image is being loaded by default (the only one visible in the viewport), it’s significantly smaller than the original (approx. 33KB vs 325KB) and uses a more modern format (WebP)." >}}

**Note:** Next.js will optimize images dynamically upon request and store them in a local cache. The optimized image then gets served for subsequent requests until an expiration is reached.

Next.js can also generate several versions of the image to serve media to smaller screens at the right size. When loading the page under mobile emulation (a Pixel phone), an even smaller 16KB image gets served for our first image.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24684a33-bed7-44ab-a87b-11f34803616e/24-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24684a33-bed7-44ab-a87b-11f34803616e/24-humble-img-element-and-core-web-vitals.png" width="800" height="469" sizes="100vw" caption="Next.js generates several versions of the image to serve media to smaller screens at the right size. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24684a33-bed7-44ab-a87b-11f34803616e/24-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Next.js generates several versions of the image to serve media to smaller screens at the right size." >}}

When a user scrolls down the page, the additional images are lazy-loaded in. Note how no additional configuration or tweaking was needed here &mdash; the component just did the right thing by default.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2aae589-0b37-422a-8ae0-ef716bc5ef27/30-humble-img-element-and-core-web-vitals.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2aae589-0b37-422a-8ae0-ef716bc5ef27/30-humble-img-element-and-core-web-vitals.gif" width="800" height="479" alt="Performance optimizations offered by the Next.js image component." /></a></figure>

The performance optimizations offered by the Next.js image component can help improve Largest Contentful Paint. To learn more about the component, including the different layout modes it supports, check out the [Next.js documentation](https://nextjs.org/docs/api-reference/next/image). A component with similar capabilities is available for [Nuxt.js](https://image.nuxtjs.org/).

### What Are Examples Of Businesses Improving LCP Via Image Optimizations?

Vodafone [found](https://web.dev/vodafone/) that a 31% improvement in LCP increased sales by 8%. Their optimizations to improve LCP included resizing their hero image, optimizing SVGs and using media queries to limit loading offscreen images.

Agrofy [found](https://web.dev/agrofy/) that 70% improvement in LCP correlated to a 76% reduction in load abandonment. Their optimizations to LCP included a [2.5s saving](https://mollar-luciano.medium.com/how-agrofy-optimised-core-web-vitals-and-improved-business-metrics-2f73311bca) from switching their first large image from being behind JavaScript (client-side hydration) to being directly in the main HTML document.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56df8cb2-cd85-4ffc-9256-36f191f7eb5f/17-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56df8cb2-cd85-4ffc-9256-36f191f7eb5f/17-humble-img-element-and-core-web-vitals.png" width="800" height="441" sizes="100vw" caption="Agrofy found that 70% improvement in LCP correlated to a 76% reduction in load abandonment. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56df8cb2-cd85-4ffc-9256-36f191f7eb5f/17-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Agrofy found that 70% improvement in LCP correlated to a 76% reduction in load abandonment." >}}

French Fashion house [Chloè](https://www.chloe.com/us) used Link Preload to preload their 1x and 2x Hero images, which were previously bottlenecked by a render-blocking script. This improved their Largest Contentful Paint by 500ms based on Chrome UX Report data over 28 days.

Optimizations to Cumulative Layout Shift helped YAHOO! Japan increased its News page views per session by 15%. They determined shifts were caused after their hero images were loaded and snapped in for the first view. They used [Aspect Ratio Boxes](https://css-tricks.com/aspect-ratio-boxes/) to reserve space before their image was loaded.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ab054bc-3d45-4282-8a62-959bb5f1b0b8/5-humble-img-element-and-core-web-vitals.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ab054bc-3d45-4282-8a62-959bb5f1b0b8/5-humble-img-element-and-core-web-vitals.png" width="800" height="450" sizes="100vw" caption="Optimizations to Cumulative Layout Shift helped YAHOO! Japan increased their News’s page views per session by 15%. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ab054bc-3d45-4282-8a62-959bb5f1b0b8/5-humble-img-element-and-core-web-vitals.png'>Large preview</a>)" alt="Optimizations to Cumulative Layout Shift helped YAHOO! Japan increased their News’s page views per session by 15%." >}}

## Lab Data Is Only Part Of The Puzzle. You Also Need Field Data.

Before we go, I’d love to share a quick reminder about the importance of looking at the image experience your real users might have. Lab tools like Lighthouse measure performance in a synthetic (emulated mobile) environment limited to page load, while field or **real-world data** (e.g. RUM, [Chrome UX Report](https://developers.google.com/web/tools/chrome-user-experience-report/)) are based on real users throughout the lifetime of the page.

It’s important to **check how realistic your lab results are** by comparing them against typical users in the field. For example, if your lab CLS is much lower than the 75th percentile CLS in the field, you may not be measuring layout shifts as real users are experiencing them.

CLS is measured during the **full lifespan of a page**, so user behavior (interactions, scrolls, clicks) can have an impact on the elements that are shifting. For images, lab CLS may not see an improvement from fixing missing image dimensions if the images happen to be far down a page requiring a scroll. This is just one place where it’s worthwhile consulting real-user data.

For LCP it is very possible that the **candidate element can change depending on factors such as load times** (the LCP candidate could initially be a paragraph of text and then a large hero image), personalization or even different screen resolutions. Lighthouse’s LCP audit is a good place to start, but do take a look at what real users see to get the full picture.

Whenever possible, try to **configure your lab tests** to reflect real-user access and behavior patterns. Philip Walton has an excellent guide on [debugging Web Vitals in the field](https://web.dev/debug-web-vitals-in-the-field/) worth checking for more details.

## Editorial Note: Addy's Book on Image Optimization

We’re happy and honored to have teamed up with Addy to publish a dedicated [book on image optimization](https://www.smashingmagazine.com/2021/04/image-optimization-pre-release/), and the book is now finally here. With modern approaches to image compression and image delivery, current and emerging image formats, how browsers load, decode and render images, CDNs, lazy-loading, adaptive media loading and how to optimize for Core Web Vitals. Everything in one, single, 528-pages book. <a href="https://smashingmagazine.com/provide/eBooks/image-optimization-sample-chapter.pdf">Download a free PDF sample</a> (12MB).


<figure style="margin-bottom:0;padding-bottom:0" class="break-out article__image">
    <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b41ae541-7618-44f2-81cd-cc681c64d0d0/image-optimization-header.png" title="Tap for a large preview of the book.">
    <img style="border-radius: 11px" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b41ae541-7618-44f2-81cd-cc681c64d0d0/image-optimization-header.png" alt="Image Optimization">
    </a>
</figure>

{{< book-cta-buttons sku="image-optimization" >}}

[Get the book right away](https://www.smashingmagazine.com/printed-books/image-optimization/) — and thank you for your kind support, everyone! ❤️

* * *

Now that we’ve covered the foundations of the modern `<img>` tag, check out the [pre-release of the Image Optimization book](https://www.smashingmagazine.com/2021/04/image-optimization-pre-release/) to get a deeper understanding of how images can impact performance and UX.

Throughout the [book](https://www.smashingmagazine.com/printed-books/image-optimization/), we will cover advanced image optimization techniques that expand heavily on the above guidance, as well as how to best use elements like `<img>` and `<picture>` to make your images on the web shine.

You may also be interested in reading Malte Ubl’s guide to [image optimization](https://www.industrialempathy.com/posts/image-optimizations/), Jake Archibald’s guide to the [AVIF format](https://jakearchibald.com/2020/avif-has-landed/) and Katie Hempenius’ [excellent](https://web.dev/authors/katiehempenius/) guidance on web.dev.

*With thanks to Yoav Weiss, Rick Viscomi and Vitaly for their reviews.*

{{< signature "vf, yk, il" >}}

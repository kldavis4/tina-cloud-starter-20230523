---
title: 'Using Modern Image Formats: AVIF And WebP'
slug: modern-image-formats-avif-webp
author: addy-osmani
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67b6e428-ea96-41b4-baf2-6be51577910d/modern-image-formats-avif-webp.jpg
date: 2021-09-29T08:25:00.000Z
summary: >-
  In this article, we’ll highlight how modern image formats (AVIF or WebP) can improve compression by up to 50% and deliver better quality per-byte while still looking visually appealing. We’ll compare what’s possible at high-quality, low-quality and file-size targets. 
description: >-
  In this article, we’ll highlight how modern image formats (AVIF or WebP) can improve compression by up to 50% and deliver better quality per-byte while still looking visually appealing. We’ll compare what’s possible at high-quality, low-quality and file-size targets.
categories:
  - Images
  - Browsers
  - Performance
  - Optimization
  - Smashing Books
sponsor:
  title: Image Optimization
  link: https://www.smashingmagazine.com/printed-books/image-optimization/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87fd0cfa-692e-459c-b2f3-15209a1f6aa7/image-optimization-shop-cover-opt.png
  description: >-
    We’ve recently published Addy’s <a href="https://www.smashingmagazine.com/printed-books/image-optimization/">Image Optimization</a> book with <strong>everything you need to know about images</strong>, how to compress, serve and maintain images. Now, shipping with a hand-written personal message, signed by Addy. <strong><a href="https://www.smashingmagazine.com/printed-books/image-optimization/">Jump&nbsp;to&nbsp;the table of contents</a></strong> and <a href="/printed-books/image-optimization/" data-product-sku="image-optimization" data-component="AddToCart" data-product-path="/printed-books/image-optimization/" data-silent="true">get the book right away.</a>
---

Images are the [most popular](https://httparchive.org/reports/state-of-images#reqImg) resource type on the web and are often the largest. Users appreciate high-quality visuals, but care needs to be taken to deliver those hero images, product photos and cat memes as efficiently and effectively as possible. 
 
If you’re optimizing for the [Web Vitals](https://web.dev/vitals/), you might be interested to hear that images account for &#126;[42%](https://paulcalvano.com/2021-06-07-lcp-httparchive/) of the [Largest Contentful Paint](https://web.dev/lcp/) element for websites. Key [user-centric metrics](https://web.dev/vitals/) often depend on the size, number, layout, and loading priority of images on the page. This is why a lot of our guidance on performance talks about image optimization.  
 
A tl;dr of recommendations can be found below.

<blockquote><strong>tl;dr</strong><br /><br /><span style="font-style: normal">
<ul>
<li><a href="https://www.smashingmagazine.com/2021/09/modern-image-formats-avif-webp/#avif">AVIF</a> is a solid first choice if lossy, low-fidelity compression is acceptable and saving bandwidth is the number one priority. Assuming encode/decode speeds meet your needs.</li>
<li><a href="https://www.smashingmagazine.com/2021/09/modern-image-formats-avif-webp/#webp">WebP</a> is more widely supported and may be used for rendering regular images where advanced features like wide color gamut or text overlays are not required.</li>
<li>AVIF may not be able to compress non-photographic images as well as PNG or lossless WebP. Compression savings from WebP may be lower than JPEG for high-fidelity lossy compression.</li>
<li>If both AVIF and WebP are not viable options, consider evaluating MozJPEG (optimize JPEG images), OxiPNG (non-photographic images), or JPEG 2000 (lossy or lossless photographic images).</li>
<li><a href="https://www.smashingmagazine.com/2021/09/modern-image-formats-avif-webp/#progressive-enhancement">Progressive enhancement</a> via <code>&lt;picture&gt;</code> lets the browser choose the first supported format in the order of preference. This implementation is considerably simplified when using image CDN’s where the <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept">Accept Header</a> and content negotiation (e.g. auto-format and quality) can serve the best image.</li></ul></span></blockquote>

## Why Do We Need Modern Formats?

We have a reasonably wide selection of image formats to choose from when rendering images on the web. The essential difference between image formats is that the image codec used to encode or decode each image type is different. An image codec represents the algorithm used to compress and encode images to a specific file type and decode them for display on the screen.

### Evaluating Codecs

You can evaluate which image format is suitable for you based on different parameters.

- **Compression**  
The efficiency of a codec can be mainly measured by how much compression it can achieve. Compression achieved is relevant because the higher the compression, the smaller the file size, and the lower the data required to transfer the image on the network. Smaller file size directly impacts the Largest contentful Paint (LCP) metric for the page as image resources needed by the page get loaded faster.
- **Quality**  
Ideally, compression should not result in any loss of image data; it should be lossless. Compression formats that result in some loss of image data, thereby reducing the quality of the image, are known as lossy. You may use tools like [DSSIM](https://github.com/kornelski/dssim) or [ssimulacra](https://github.com/cloudinary/ssimulacra) to measure the [structural similarity](https://en.wikipedia.org/wiki/Structural_similarity) between images and judge if the loss in quality is acceptable.
- **Encode/Decode Speed**  
Complex compression algorithms may require higher processing power to encode/decode images. This can be complicated by whether encoding is being done ahead of time (static/build) or on-the-fly (on-demand). While encoding may be one-time in the case of static images, the browser still has to decode images before rendering them. A complex decoding process can slow down the rendering of images.
 
Degree of compression, image quality, and decoding speed are key factors to be considered when comparing image performance for the web. Specific use cases may require image formats that support other features like:
 
- Software support: An image format may perform very well but is useless if browsers, CDN’s and other image manipulation tools do not recognize it.
- Animation support may be required for some images on the web (e.g., GIF). However, you should ideally replace such images with [videos](https://web.dev/replace-gifs-with-videos/).
- Alpha Transparency: The ability to create images with different opacity levels using the alpha channel. (e.g., PNG images with transparent backgrounds) 
- It should support [High dynamic range(HDR) imaging and wide color gamut](https://w3c.github.io/ColorWeb-CG/).
- Progressive decoding to load images gradually allows users to get a reasonable preview of the image before it gets refined.
- Depth maps that will enable you to apply effects to the foreground or background of the image. 
- Images with multiple overlapping layers, for example, text overlays, borders, and so on.
 
**Tip:** *When evaluating quality, compression and fine-tuning of modern formats, [Squoosh.app](https://squoosh.app/)’s ability to perform a visual side-by-side comparison is helpful. Zooming in allows you to better appreciate where a format exhibits blockiness or edge-artifacts to reason about trade-offs.*
 
{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d64452e0-f3a6-46be-a86a-579efdc0aacf/1-modern-image-formats.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d64452e0-f3a6-46be-a86a-579efdc0aacf/1-modern-image-formats.png" width="800" height="524" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d64452e0-f3a6-46be-a86a-579efdc0aacf/1-modern-image-formats.png'>Large preview</a>)" alt="Squoosh.app with the ability to perform a visual side-by-side comparison" >}}

## The Old Guards: JPEG And PNG

JPEG has been the most widely supported image format for 25 years. Classic JPEG encoders lead to relatively weak compression, while more modern JPEG encoding efforts (like [MozJPEG](https://github.com/mozilla/mozjpeg)) improve compression but are not quite as optimal as modern formats. JPEG is also a lossy compression format. While decoding speed for JPEGs is excellent, it lacks other desirable features required of images on modern, eye-catching websites. It does not support transparency in images, animation, depth maps, or overlays. 

JPEG works best with photographs, while PNG is its counterpart for other still images. PNG is a lossless format and can support alpha transparency, but the compression achieved, especially for photographs, is considerably low. JPEG and PNG are both used extensively depending on the type of image required.

The target for modern image formats is thus to overcome the limitations of JPEG and PNG by offering better compression and flexibility to support the other features discussed earlier. With this background, let us look at what AVIF and WebP have to offer.

{{% feature-panel id="image-optimization" %}}

## AVIF

The AV1 image file format (AVIF) is an open-source image format for storing still and animated images. It was released in February 2019 by the [Alliance for Open Media](https://aomedia.org/) (AOMedia). AVIF is the image version of the popular AV1 video format. The goal was to develop a new open-source video coding format that is both state-of-the-art and royalty-free. 

### AVIF Benefits

AVIF supports very efficient lossy and lossless compression to produce high-quality images after compression AVIF compresses much better than most popular formats on the web today (JPEG, WebP, JPEG 2000, and so on). Images can be up to ten times smaller than JPEGs of similar visual quality. Some tests have shown that AVIF offers a 50% saving in file size compared to JPEG with **similar perceptual quality**. Note that there can be cases where WebP lossless can be better than AVIF lossless, so do be sure to manually evaluate.

Here, you can see a size comparison between a JPEG image and its corresponding (lossy) AVIF image converted using the [Squoosh](https://squoosh.app/) app:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96da1cce-5594-4fd1-89c9-4edb5608903c/12-modern-image-formats.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96da1cce-5594-4fd1-89c9-4edb5608903c/12-modern-image-formats.png" width="800" height="531" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96da1cce-5594-4fd1-89c9-4edb5608903c/12-modern-image-formats.png'>Large preview</a>)" alt="size comparison between a JPEG image and an AVIF image on Squoosh app" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/982f3a59-ec9a-401c-a6a6-6400f400e9a9/sqoosh-zoomed-in.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/982f3a59-ec9a-401c-a6a6-6400f400e9a9/sqoosh-zoomed-in.png" width="800" height="323" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96da1cce-5594-4fd1-89c9-4edb5608903c/12-modern-image-formats.png'>Large preview</a>)" alt="size comparison between a JPEG image and an AVIF image on Squoosh app" >}}

In addition to superior compression, AVIF also provides the following features:

- AVIF supports animations, live photos, and more through multilayer images stored in image sequences.
- It offers better support for graphical elements, logos, and infographics, where JPEG has limitations.
- It provides better lossless compression than JPEG.
- It supports twelve bits of color depth enabling high dynamic range (HDR) and wide color gamut (WCG) images with a better span of bright and dark tones and a broader range of luminosity.
- It includes support for monochrome images and multichannel images, including transparent images that use the alpha channel.

## Comparing Formats

To better understand the differences in quality and compression offered by the different formats, we can visually compare images and evaluate the differences.

### Evaluating Quality And Compression

We will begin our quality evaluation of JPEG, WebP, and AVIF using the default high-quality output settings of Squoosh for each format &mdash; intentionally untuned to mimic a new user’s experience with them. As a reminder, you should aim to evaluate the quality configuration and formats that best suit your needs. If you’re short on time, image CDNs automate some of this.

In this first test, encoding a 560KB photo of a sunset (with many textures) produces an image that is visually and perceptually quite similar for each. The output comes in at 289KB (JPEG@q75), 206KB (WebP@q75), and 101KB (AVIF@q30) &mdash; up to 81% in compression savings.

Great stuff, but let’s dig deeper.

{{< codepen height="480" theme_id="light" slug_hash="WNOPpbd" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image format comparison 2](https://codepen.io/smashingmag/pen/WNOPpbd) by <a href="https://codepen.io/addyosmani">Addy Osmani</a>.{{< /codepen >}}

Various tools exist for comparing the dissimilarity between different image formats (e.g., DSSIM, simulacra). Using these tools, you can [approximate the comparable quality setting](https://www.industrialempathy.com/posts/avif-webp-quality-settings/) when evaluating, say, JPEG to WebP or WebP to AVIF. Below are the same images encoded at comparable quality, targeting JPEG’s 70% quality. The output is 323KB (JPEG), 214KB (WebP@q75), and 117KB (AVIF@60) &mdash; sizes are a little larger than trusting the defaults, but the compression wins are still significant.

{{< codepen height="480" theme_id="light" slug_hash="NWgopqw" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image format comparison 2a (quality)</a>](https://codepen.io/smashingmag/pen/NWgopqw) by <a href="https://codepen.io/addyosmani">Addy Osmani</a>.{{< /codepen >}}

We can also look at lower-quality across each format, which is really where WebP and AVIF shine. Here’s JPEG@q10 (35KB), WebP@q1 (35KB), AVIF@q17 (36KB) &mdash; the WebP has significantly fewer blocky artifacts compared to the JPEG, while the AVIF is both less blocky and is sharper on key details in the image.

{{< codepen height="480" theme_id="light" slug_hash="GREzWpN" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image format comparison 2d (quality)</a>](https://codepen.io/smashingmag/pen/GREzWpN) by <a href="https://codepen.io/addyosmani">Addy Osmani</a>.{{< /codepen >}}

**Note:** *This sunset is a higher resolution image (`2400`&times;`1595`), and on 2&times; screens, the quality could be much lower and [still](https://jakearchibald.com/2021/serving-sharp-images-to-high-density-screens/) look sharp depending on how users interact with the image (e.g., how much they pinch and zoom).*

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab37fe06-0aad-4c2f-8295-013363a84257/18-modern-image-formats.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab37fe06-0aad-4c2f-8295-013363a84257/18-modern-image-formats.png" width="800" height="516" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab37fe06-0aad-4c2f-8295-013363a84257/18-modern-image-formats.png'>Large preview</a>)" alt="screenshot of an image on the Squoosh app" >}}

For a more extreme example of the differences between JPEG and AVIF, we can look at an example from the Kodak dataset ([evaluated](https://netflixtechblog.com/avif-for-next-generation-image-coding-b1d75675fe4) by Netflix) comparing a JPEG (4:4:4) at 20KB to an AVIF (4:4:4) at 19.8KB. Notice how the JPEG has visible blocky artifacts in the sky and roof. The AVIF is visibly better, containing fewer blocking artifacts. There is, however, a level of texture loss on the roof and some blurriness. It’s still quite impressive, given the overall compression factor is 59x.

{{< codepen height="480" theme_id="light" slug_hash="abwXJvg" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image format comparison 4a (netflix)</a>](https://codepen.io/smashingmag/pen/abwXJvg) by <a href="https://codepen.io/addyosmani">Addy Osmani</a>.{{< /codepen >}}

Next, let’s evaluate the quality of a beach image with many fine details, textures, and areas of low contrast in the clouds. We will compare the original (at 482KB) to what JPEG, WebP, and AVIF can produce with a 45KB file-size limit (with no advanced tuning) &mdash; using Squoosh; this works out at JPEG (MozJPEG) at 50% quality, WebP at 54%, and AVIF at 36%.

{{< codepen height="480" theme_id="light" slug_hash="rNwPyxP" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image format comparison 3a (size)</a>](https://codepen.io/smashingmag/pen/rNwPyxP) by <a href="https://codepen.io/addyosmani">Addy Osmani</a>.{{< /codepen >}}

The JPEG has blocky artifacts and visible color banding in the clouds and water, while the WebP and AVIF have noticeably less of this blockiness observable. In my opinion, the AVIF offers the overall smoothest experience of all three.

{{< codepen height="480" theme_id="light" slug_hash="jOwdBqx" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image format comparison 3a (crop)</a>](https://codepen.io/smashingmag/pen/jOwdBqx) by <a href="https://codepen.io/addyosmani">Addy Osmani</a>.{{< /codepen >}}

Speaking of textures, we can also perform a similar lower-quality evaluation on a Netflix poster for “The Witcher” (targeting 36KB). Notice the blockiness in the clouds for the JPEG and some blurriness around the red text for WebP (which only supports 4:2:0 chroma subsampling without workarounds). The AVIF looks best, followed by the WebP.

{{< codepen height="480" theme_id="light" slug_hash="dyRavXY" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image format comparison 5a (size)</a>](https://codepen.io/smashingmag/pen/dyRavXY) by <a href="https://codepen.io/addyosmani">Addy Osmani</a>.{{< /codepen >}}

Finally, let’s look at a photo with a lot more text elements than previous images &mdash; a poster. When we go down to lower qualities and target a reasonably small size (25KB), we can observe that the JPEG has strong color banding and halos around the text. There are clear blocky artifacts around the edges. The WebP avoids an amount of the blockiness, looking incrementally better. The AVIF preserves the sharp edges a little better than either JPEG or WebP, producing a smooth image.

{{< codepen height="480" theme_id="light" slug_hash="WNOPpxM" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image format comparison 4a (size)</a>](https://codepen.io/smashingmag/pen/WNOPpxM) by <a href="https://codepen.io/addyosmani">Addy Osmani</a>.{{< /codepen >}}

Additional format vs quality comparisons are available for [photography](https://codepen.io/smashingmag/pen/eYRxvzx) and [illustrations](https://codepen.io/smashingmag/pen/gORqmwW).

### AVIF Tooling And Support

Since its release in 2019, the support for AVIF has increased considerably. While there was no direct method to create or view AVIF files earlier, you can easily do so now with the open-source utilities available.

#### AVIF Images In The Browser

AVIF was introduced on the desktop version of Chrome in August 2020 with [Chrome 85](https://developer.chrome.com/blog/new-in-chrome-85/#more). It is also supported on Chrome for Android, Opera and Firefox for desktop, and Opera for Android.  

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e2710d-1598-4566-8568-5e500b73db2b/11-modern-image-formats.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e2710d-1598-4566-8568-5e500b73db2b/11-modern-image-formats.png" width="800" height="531" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e2710d-1598-4566-8568-5e500b73db2b/11-modern-image-formats.png'>Large preview</a>)" alt="AVIF images in the browser" >}}

To include an AVIF image on your page, you can add it as an image element. However, browsers that do not support AVIF cannot render this image.

<pre><code class="language-html">&lt;img src="/images/sky.avif" width="360" height="240" alt="a beautiful sky"&gt;</code></pre>

A workaround to ensure that at least one supported image format is delivered to all browsers is to apply AVIF as a **progressive enhancement**. There are two ways to do this.

##### Progressive Enhancement

1. **Using The `<picture>` Element**  
As `<picture>` allows browsers to skip images they do not recognize, you can include images in your order of preference. The browser selects the first one it supports.

<pre><code class="language-html">&lt;picture&gt;
 &lt;source srcset="img/photo.avif" type="image/avif"&gt;
 &lt;source srcset="img/photo.webp" type="image/webp"&gt;
 &lt;img src="img/photo.jpg" alt="Description" width="360" height="240"&gt;
&lt;/picture&gt;</code></pre>

2. **Using Content Negotiation**  
[Content negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) allows the server to serve different resource formats based on what is supported by the browser. Browsers that support a specific format can announce it by adding the format to their [Accept](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) Request Header. E.g., the Accept Request Header for images in Chrome is:  
  `Accept: image/avif,image/webp,image/apng,image/*,*/*;q=0.8`  
  The code to check if AVIF is supported in the fetch event handler can look something like this:  
  `const hdrAccept = event.request.headers.get("accept");`  
  `const sendAVIF = /image\/avif/.test(hdrAccept);`  
  You can use this value to serve AVIF or any other default format to the client.

Creating the markup for progressive enhancement can be daunting. Image CDN’s offer the option to automatically serve the best format suitable to the client. However, if you are not using an image CDN, you can consider using a tool like [just-gimme-an-img](https://just-gimme-an-img.vercel.app/). This tool can generate the markup for the picture element for a given image with different formats and widths. It also creates the images corresponding to the markup using Squoosh entirely client-side. Note: encoding multiple formats can take a while using it, so you might want to grab a coffee while you wait.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a90fb79-0aa4-4858-995c-f311b3f7a24b/14-modern-image-formats.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a90fb79-0aa4-4858-995c-f311b3f7a24b/14-modern-image-formats.png" width="800" height="298" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a90fb79-0aa4-4858-995c-f311b3f7a24b/14-modern-image-formats.png'>Large preview</a>)" alt="markup for the picture element for a given image with different formats and widths." >}}

**Note:** *Image CDNs are mentioned a few times in this article. CDN servers are often located closer to users than origin servers and can have a [shorter round-trip times](https://web.dev/content-delivery-networks/) (RTT), improving network latency. That said, serving from a different origin can add round-trips and impact performance gains. This may be fine if the CDN is serving other site content, but when in doubt, experiment and measure.*

{{% ad-panel-leaderboard %}}

#### Encode And Decode AVIF Files
 
Several open-source projects provide different methods to encode/decode AVIF files:
 
- **Libraries**  
[Libaom](https://aomedia.googlesource.com/aom/) is the open-source encoder and decoder maintained by AOMedia, the creators of AVIF. The library is continuously updated with new optimizations that aim to reduce the cost of encoding AVIF, especially for frequently loaded or high-priority images. [Libavif](https://github.com/AOMediaCodec/libavif) is an open-source muxer and parser for AVIF used in Chrome for decoding AVIF images. You can use libavif with libaom to create AVIF files from original uncompressed images or transcode them from other formats. There is also [Libheif](https://github.com/strukturag/libheif), a popular AVIF/HEIF encoder/decoder and [Cavif](https://github.com/kornelski/cavif-rs). Thanks to Ben Morss, [libgd](https://libgd.github.io/) supports AVIF and is also coming to PHP in November.
- **Web Apps And Desktop Apps**  
[Squoosh](https://squoosh.app), a web app that lets you use different image compressors, also supports AVIF, making it relatively straightforward to convert and create `.avif` files online. On desktop, [GIMP](https://www.gimp.org/) [supports AVIF exporting](https://avif.io/blog/tutorials/gimp/). ImageMagick and [Paint.net](https://forums.getpaint.net/) also support AVIF while Photoshop community [plugins for AVIF](https://github.com/0xC0000054/avif-format) are also available.
- **JavaScript Libraries**  
  - [AVIF.js](https://github.com/Kagami/avif.js) is an AVIF polyfill for browsers that do not support AVIF yet. It uses Service Worker API to intercept the fetch event and decode AVIF files.
  - [Avif.io](https://avif.io/) is another web utility that can convert files from different image types to AVIF on the [client-side](https://github.com/justinschmitz97/avif.io/). It calls Rust code in the browser using a WebWorker. The converter library is compiled to WASM using wasm-pack.
  - [Sharp](https://sharp.pixelplumbing.com/) is a Node.js module that can convert large images in standard formats to smaller web-friendly images, including AVIF images. 
- **Utilities**  
Image conversion or transformation utilities support the AVIF format. You can use [MP4Box](https://github.com/gpac/gpac/wiki/MP4Box) to create and decode AVIF files.
- **In Code**  
[`go-avif`](https://github.com/Kagami/go-avif) implements an AVIF encoder for Go using `libaom`. It comes with a utility called `avif` which can encode JPEG or PNG files to AVIF.

Anyone interested in learning how to create AVIF images using Squoosh or building the command line encoder [`avifenc`](https://github.com/AOMediaCodec/libavif/blob/master/apps/avifenc.c) can do so at the codelab on [serving AVIF files](https://codelabs.developers.google.com/codelabs/avif#2).

### AVIF And Performance

AVIF can reduce the file size of images due to better compression. As a result, AVIF files download faster and consume lower bandwidth. This can potentially improve performance by reducing the time to load images.

Lighthouse-best practices audit now considers that AVIF image compression can bring significant improvements. It collects all the BMP, JPEG, and PNG images on the page, converts them to WebP and estimates the AVIF file size. This estimate helps Lighthouse report the potential savings under the “Serve images in next-gen formats” section.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6383da02-0562-46f6-802f-c8dfb3c05ca5/9-modern-image-formats.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6383da02-0562-46f6-802f-c8dfb3c05ca5/9-modern-image-formats.png" width="800" height="555" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6383da02-0562-46f6-802f-c8dfb3c05ca5/9-modern-image-formats.png'>Large preview</a>)" alt="Lighthouse-best practices audit under the 'Serve images in next-gen formats' section." >}}

[Tim Vereecke](https://twitter.com/TimVereecke/status/1372210487191085063) reported 25% byte savings and a positive impact on LCP (compared to JPEG) after converting 14 million images on the website to AVIF measured using Real User Monitoring (RUM).

### AVIF Gotchas

The biggest drawback for AVIF at present is that it lacks uniform support across browsers. Introducing AVIF as a [progressive](https://www.smashingmagazine.com/2021/09/modern-image-formats-avif-webp/#avif-tooling-and-support) enhancement helps overcome this. A few other aspects in which AVIF does not meet the ideal standards for a modern file format.
 
- Modern versions of Chrome (Chrome 94+) [do support AVIF progressive rendering](https://bugs.chromium.org/p/chromium/issues/detail?id=1221717) while older versions do not. While at the time of writing there isn’t an encoder that can make these images easily, there is hope this will change. 
- AVIF images take longer to encode and create. This could be a problem for sites that create images files dynamically. However, the AVIF team is working on improving encoding speeds. AVIF contributors at Google have also reported some nice performance gains. Since Jan 1st 2021, AVIF encoding had a &#126;47% improvement in transcode time (this is speed 6, the current default for libavif) and across the calendar year a 73% improvement. Since July, there’s also been a 72% improvement in transcode times at speed 9 (on-the-fly-encoding).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3272f1d2-d85d-416d-88a9-63008f2f30bc/16-modern-image-formats.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3272f1d2-d85d-416d-88a9-63008f2f30bc/16-modern-image-formats.png" width="800" height="438" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3272f1d2-d85d-416d-88a9-63008f2f30bc/16-modern-image-formats.png'>Large preview</a>)" alt="report on AVIF’s improvement in transcode time" >}}

- Decoding AVIF images for display can also take up more CPU power than other codecs, though smaller file sizes may compensate for this.
- Some CDNs do not yet support AVIF by default for their automatic format modes because it can still be slower to generate on the first request.

## WebP

We have mentioned WebP a few times, but let’s briefly cover its history. Google created the WebP format in 2011 as an image format that would help to make the web faster. Over the years, it has been accepted and adopted widely because of its ability to compress images to lower file sizes compared to JPEG and PNG. WebP offers both lossless and lossy compression at an acceptable visual quality and supports alpha-channel transparency and animation.
 
Lossy WebP compression is based on the [VP8](https://static.googleusercontent.com/media/research.google.com/en/us/pubs/archive/37073.pdf) video codec and uses predictive encoding to encode an image. It uses values in the neighboring blocks of pixels to predict the value in a block and encodes only the difference. [Lossless WebP](https://developers.google.com/speed/webp/docs/compression#lossless_webp) images are generated by applying multiple transformation techniques to images to compress them. 

### WebP Benefits

WebP lossless images are generally 26% smaller than PNG, and WebP lossy images are 25&ndash;34% smaller than JPEG images of similar quality. Animation support makes them an excellent replacement for GIF images as well. The following shows a transparent PNG image on the left and the corresponding WebP image on the right generated by the Squoosh app with a 26% size reduction.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6570876c-99cc-4522-8491-c60125c74e39/8-modern-image-formats.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6570876c-99cc-4522-8491-c60125c74e39/8-modern-image-formats.png" width="800" height="377" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6570876c-99cc-4522-8491-c60125c74e39/8-modern-image-formats.png'>Large preview</a>)" alt="the screenshot shows a transparent PNG image on the left and the corresponding WebP image on the right generated by the Squoosh app with a 26% size reduction." >}}

Additionally, WebP offers other benefits like:

- **Transparency**  
WebP has a lossless 8-bit transparency channel with only 22% more bytes than PNG. It also supports lossy RGB transparency, which is a feature unique to WebP.
- **Metadata**  
The WebP file format supports EXIF photo metadata and Extensible Metadata Platform (XMP) digital document metadata. It may also contain an ICC color profile.
- **Animation**  
WebP supports true-color animated images.
 
**Note:** *In the case of transparent, vector-like images such as the above, an optimized SVG may ultimately deliver a sharper, smaller file compared to a raster format.*

{{% ad-panel-leaderboard %}}

### WebP Tooling And Support

Over the years, ecosystems other than Google have adopted WebP, and there are many tools available to create, view and load WebP files.

#### Serving And Viewing WebP Files

WebP is supported on the latest versions of almost all major browsers today.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53671dd1-89ba-47b7-b6cc-af3be817c87a/13-modern-image-formats.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53671dd1-89ba-47b7-b6cc-af3be817c87a/13-modern-image-formats.png" width="800" height="531" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53671dd1-89ba-47b7-b6cc-af3be817c87a/13-modern-image-formats.png'>Large preview</a>)" alt="WebP images in the browser" >}}

If developers wish to serve WebP on other browsers in the future, they can do so using the `<picture>` element or request headers as shown in the section on [AVIF](https://www.smashingmagazine.com/2021/09/modern-image-formats-avif-webp/#avif-tooling-and-support). 

Image Content Delivery Networks (CDN) also support [responsive images](https://cloudinary.com/documentation/responsive_images#responsive_images_with_automatic_format_selection) with automatic format selection for images in WebP or AVIF depending on the browser support. WebP plug-ins are available for other popular stacks like [WordPress](https://wordpress.org/plugins/search/convert+webp/), [Joomla](https://extensions.joomla.org/instant-search/?jed_live%5Bquery%5D=webp), [Drupal](https://www.drupal.org/project/project_module?f%5B0%5D=&f%5B1%5D=&f%5B2%5D=&f%5B3%5D=&f%5B4%5D=sm_field_project_type%3Afull&f%5B5%5D=&f%5B6%5D=&text=webp&solrsort=iss_project_release_usage+desc&op=Search), etc. Initial support for WebP is also available in [WordPress core](https://make.wordpress.org/core/2021/06/07/wordpress-5-8-adds-webp-support/), starting with WordPress 5.8.

You can view WebP images easily by opening them in a browser that supports them. Additionally, you can also preview them on Windows and macOS using an add-on. Installing the [Quick Look plug-in for WebP](https://github.com/Nyx0uf/qlImageSize) (`qlImageSize`) would allow you to preview WebP files using the Quick Look utility. The WebP team has published [precompiled](https://developers.google.com/speed/webp/download) libraries and utilities for the WebP codec for Windows, macOS, and Linux. Using these on Windows allows you to preview WebP images in File Explorer or Windows Photo Viewer.

**Converting images to WebP**

In addition to the libraries provided by the WebP team, several free, open-source, and commercial image editing tools support WebP.

**Utilities:**  
Like AVIF, Squoosh can also convert files to WebP online, as shown in the [previous section](https://www.smashingmagazine.com/2021/09/modern-image-formats-avif-webp/#why-do-we-need-modern-formats). [XnConvert](https://www.xnview.com/en/xnconvert/) is a utility that you can install on the desktop to convert different image formats, including WebP. XnConvert can also help with stripping and editing metadata, cropping and resizing, brightness and contrast, customizing color depth, blurring and sharpening, masks and watermarks, and other transforms.

**Node.js Modules:**  
[Imagemin](https://github.com/imagemin/imagemin) is a popular image minification module with an add-on for converting images to WebP ([imagemin-webp](https://github.com/imagemin/imagemin-webp)). The add-on supports both lossy and lossless WebP modes.

**Others:**  
Several apps for image conversion and manipulation support the WebP format. These include [Sketch](https://www.sketch.com/), [GIMP](https://www.gimp.org/), [ImageMagick](https://imagemagick.org/), etc. A [Photoshop plug-in for WebP](https://github.com/webmproject/WebPShop) is also available.    

### WebP Production Usage

Due to its compression benefits over JPEG and PNG, Many large companies use WebP in production to reduce costs and decrease web page load times. Google reports 30–35% savings using WebP over other lossy compression schemes, serving 43 billion image requests a day, 26% of those being lossless compression. 

To reach its large user base in emerging markets where data is expensive, Facebook started serving WebP images to Android users. They [observed](https://engineering.fb.com/2014/06/19/android/improving-facebook-on-android/), “data savings of 25 to 35 percent compared with JPG, and 80 percent compared with PNG”. 

### WebP Gotchas

In its early days, a substantial downside with WebP was the lack of browser and tooling support. There are still few trade-offs with WebP when considering all the features a modern format should ideally support. 

- WebP is limited to 8-bit color precision. As a result, it cannot support HDR/wide gamut images.
- WebP does not support lossy images without chroma subsampling. Lossy WebP works exclusively with an 8-bit YCbCr 4:2:0, while lossless WebP works with the RGBA format. This can affect images with fine details, chromatic textures, or colored text. See below for an example.
- It does not support progressive decoding, however does support [incremental decoding](https://developers.google.com/speed/webp/faq#does_webp_support_progressive_or_interlaced_display). This can somewhat compensate for that, but the effect on rendering can be different.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1edb68f4-ee79-426e-b90c-a32830e6e98d/5-modern-image-formats.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1edb68f4-ee79-426e-b90c-a32830e6e98d/5-modern-image-formats.png" width="800" height="524" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1edb68f4-ee79-426e-b90c-a32830e6e98d/5-modern-image-formats.png'>Large preview</a>)" alt="generation of WebP files" >}}

You should ideally generate WebP files from the best quality source files available. Converting substandard JPEGs to WebP’s is not very efficient since you lose on quality twice.  

## Summary

Summarizing all the information about the four formats JPEG, PNG, AVIF, and WebP and comparing and quantifying strengths and weaknesses as presented in the previous section, we have come up with the following table.

**Note:** *The number of stars is based on a general opinion and may differ for specific use cases.*

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3e168f7-0c9a-46dc-be3d-bd379be6ad7b/modern-image-formats-3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3e168f7-0c9a-46dc-be3d-bd379be6ad7b/modern-image-formats-3.png" width="800" height="324" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3e168f7-0c9a-46dc-be3d-bd379be6ad7b/modern-image-formats-3.png'>Large preview</a>)" alt="table with the strengths and weaknesses of JPEG, PNG, AVIF, and WebP" >}}

Following are some of the key points to be considered when referring to this table.

- Compression for photographic and non-photographic images may further differ based on the fidelity (quality) of the images. We have indicated an overall score here.
- You should choose quality and chroma subsampling settings based on the purpose of the images. Low to medium-fidelity images may be acceptable in most scenarios on the web, e.g., for news, social media, and e-commerce. Image archival, movie, or photography websites require high fidelity images. You should test the actual savings due to compression for high fidelity before converting to another format.
- Lack of progressive decoding support and speed may be a problem for encoding/decoding AVIF files. For websites with average-sized images, the byte savings due to compression can compensate for speed and the absence of progressive decoding as images get downloaded quickly.
- When comparing compression offered by image formats, compare file sizes at the [same DSSIM](https://www.ctrl.blog/entry/webp-avif-comparison.html#section-results). 
- The quality setting used when encoding need not be the same for different formats to yield the same quality of images. A JPEG encoded at a quality setting of 60 may be similar to an AVIF at a quality setting of 50 and a WebP at a quality setting of 65, as suggested by this [post](https://www.industrialempathy.com/posts/avif-webp-quality-settings/).
- Extensive studies are still required to measure the actual impact on LCP when comparing formats.
- We have not included other formats like JPEG XL and HEIC in this comparison. JPEG XL is still in a relatively nascent stage, and only Apple devices support HEIC (while Safari does not). Royalty and license fees further complicate support for HEIC.

AVIF does check most of the boxes overall, and WebP has better support and offers better compression when compared to JPEG or PNG. As such, you should undoubtedly consider WebP support when optimizing images on your website. Evaluating AVIF if it meets your requirements and introducing it as a progressive enhancement could provide value as the format gets adopted across different browsers and platforms. With quality comparison tooling and improving encoding speeds using AVIF would ultimately get easier.

*With thanks to Leena Sohoni-Kasture for her heavy input into this article as well as Patrick Meenan, Frank Galligan and Yoav Weiss for their reviews.*

## A Smashing Note

Earlier this year, we published a brand new book with Addy on everything you need to know to optimize how you compress, serve and maintain images &mdash; boosting performance along the way. We are **shipping the books for free worldwide**, and if you [get the book now](/printed-books/image-optimization/), you will also receive a **hand-written postcard** by Addy with a personal message.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16be6d44-974d-4700-977b-a2a700fa90f6/picture-perfect-front-opt.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16be6d44-974d-4700-977b-a2a700fa90f6/picture-perfect-front-opt.jpeg" width="800" height="524" sizes="100vw" caption="Each book is now shipped with a hand-written note by Addy Osmani himself. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16be6d44-974d-4700-977b-a2a700fa90f6/picture-perfect-front-opt.jpeg'>Large preview</a>)" alt="Each book is now shipped with a hand-written note by Addy Osmani himself." >}}

<ul>
<li><a href="#about-the-book">Jump to the details&nbsp;&darr;</a></li>
<li><a href="https://smashingmagazine.com/provide/eBooks/image-optimization-sample-chapter.pdf">Download a free PDF sample</a> (12MB)</li>
<li><strong>Free worldwide airmail shipping</strong> for printed books.
<li><strong><a href="/printed-books/image-optimization/" data-product-sku="image-optimization" data-component="AddToCart" data-product-path="/printed-books/image-optimization/" data-silent="true">Get the book right away.</a></strong></li>
</ul>

<figure style="margin-bottom:0;padding-bottom:0" class="break-out article__image">
    <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b41ae541-7618-44f2-81cd-cc681c64d0d0/image-optimization-header.png" title="Tap for a large preview of the book.">
    <img style="border-radius: 11px" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b41ae541-7618-44f2-81cd-cc681c64d0d0/image-optimization-header.png" alt="Image Optimization">
    </a>
</figure>

{{< book-cta-buttons sku="image-optimization" >}}

{{< signature "vf, yk, il" >}}

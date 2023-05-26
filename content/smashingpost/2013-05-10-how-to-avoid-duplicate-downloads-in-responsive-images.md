---
title: How To Avoid Duplicate Downloads In Responsive Images
slug: how-to-avoid-duplicate-downloads-in-responsive-images
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a13443f2-9c24-4818-beb5-6bdc5bd12b44/download-green-illu.jpg
date: 2013-05-10T12:42:13.000Z
author: david-newton
description: >-
  The `<picture>` element is a new addition to HTML5 that’s being championed by
  the W3C’s Responsive Images Community Group (RICG). It is intended to provide
  a declarative, markup-based solution to enable responsive images without the
  need of JavaScript libraries or complicated server-side detection.
categories:
  - Mobile
  - Techniques
  - Responsive Design
  - WebP
---
The <code>&lt;picture&gt;</code> element is a new addition to HTML5 that’s being championed by the W3C’s <a href="https://responsiveimages.org/">Responsive Images Community Group</a> (RICG). It is intended to provide a declarative, markup-based solution to enable responsive images without the need of JavaScript libraries or complicated server-side detection.

The <code>&lt;picture&gt;</code> element supports a number of different types of fallback content, <strong>but the current implementation of these fallbacks is problematic</strong>. In this article, we’ll explore how the fallbacks work, how they fail and what can be done about it.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2013/07/choosing-a-responsive-image-solution/#further-reading-on-smashingmag)

*   [One Solution To Responsive Images](https://www.smashingmagazine.com/2014/02/one-solution-to-responsive-images/)
*   [Simple Responsive Images With CSS Background Images](https://www.smashingmagazine.com/2013/07/simple-responsive-images-with-css-background-images/)
*   [How To Solve Adaptive Images In Responsive Web Design](https://www.smashingmagazine.com/2013/06/clown-car-technique-solving-for-adaptive-images-in-responsive-web-design/)
*   [Responsive Images In WordPress With Art Direction](https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/)

## The `<picture>` Element And Fallback Content

Like <code>&lt;video&gt;</code> and <code>&lt;audio&gt;</code>, <code>&lt;picture&gt;</code> uses <code>&lt;source&gt;</code> elements to provide a set of images that the browser can choose from. The <code>&lt;source&gt;</code> elements may optionally contain <code>type</code> and <code>media</code> attributes to let the browser know the file type and media type of the source, respectively. Given the information in the attributes, the browser should render the first <code>&lt;source&gt;</code> with a supported file type and matching media query. For example:

{{% feature-panel %}}

<pre><code class="language-markup">
&lt;picture&gt;
    &lt;source src="landscape.webp" type="image/webp" media="screen and (min-width: 20em) and (orientation: landscape)" /&gt;
    &lt;source src="landscape.jpg" type="image/jpg" media="screen and (min-width: 20em) and (orientation: landscape)" /&gt;
    &lt;source src="portrait.webp" type="image/webp" media="screen and (max-width: 20em) and (orientation: portrait)" /&gt;
    &lt;source src="portrait.jpg" type="image/jpg" media="screen and (max-width: 20em) and (orientation: portrait)" /&gt;
&lt;/picture&gt;
</code></pre>

For situations in which a browser doesn’t know how to deal with <code>&lt;picture&gt;</code> (or <code>&lt;video&gt;</code> or <code>&lt;audio&gt;</code>) or cannot render any of the <code>&lt;source&gt;</code> elements, a developer can <strong>include fallback content</strong>. This fallback content is often either an image or descriptive text; if the fallback content is an <code>&lt;img&gt;</code>, then a further fallback is provided in the <code>alt</code> attribute (or <code>longdesc</code>), as normal.

<pre><code class="language-markup">
&lt;picture&gt;
    &lt;source type="image/webp" src="image.webp" /&gt;
    &lt;source type="image/vnd.ms-photo" src="image.jxr" /&gt;
    &lt;img src="fallback.jpg" alt="fancy pants"&gt;
&lt;/picture&gt;
</code></pre>

The <code>&lt;picture&gt;</code> element differs from <code>&lt;video&gt;</code> and <code>&lt;audio&gt;</code> in that it also allows <code>srcset</code>. The <code>srcset</code> attribute enables a developer to specify different images based on a device’s pixel density. When creating a responsive image using both <code>&lt;picture&gt;</code> and <code>srcset</code>, we might expect something like the following:

<pre><code class="language-markup">
&lt;picture&gt;
    &lt;source srcset="big.jpg 1x, big-2x.jpg 2x, big-3x.jpg 3x" type="image/jpeg" media="(min-width: 40em)" /&gt;
    &lt;source srcset="med.jpg 1x, med-2x.jpg 2x, med-3x.jpg 3x" type="image/jpeg" /&gt;
    &lt;img src="fallback.jpg" alt="fancy pants" /&gt;
&lt;/picture&gt;
</code></pre>

The idea behind a <code>&lt;picture&gt;</code> example like this is that exactly one image should be downloaded, according to the user’s context:

*   Users with `<picture>` support and a viewport at least 40 ems wide should get the `big` image.
*   Users with `<picture>` support and a viewport narrower than 40 ems should get the `med` image.
*   Users without `<picture>` support should get the fallback image.

If the browser chooses to display the <code>big</code> or <code>med</code> source, it can choose an image at an appropriate resolution based on the <code>srcset</code> attribute:

*   A browser on a low-resolution device (such as an iMac) should show the `1x` image.
*   A browser on a higher-resolution device (such as an iPhone with a Retina display) should show the `2x` image.
*   A browser on a next-generation device with even higher resolution should show the `3x` image.

<strong>The benefit to the user is that only one image file is downloaded</strong>, regardless of feature support, viewport dimensions or screen density.

The <code>&lt;picture&gt;</code> element also has the ability to use non-image fallbacks, which should be great for accessibility: if no image can be displayed or if a user needs a description of an image, then a <code>&lt;p&gt;</code> or <code>&lt;span&gt;</code> or <code>&lt;table&gt;</code> or any other element may be included as a fallback. This allows for more robust and content-appropriate fallbacks than a simple <code>alt</code> attribute.</p>

## The Fallback Problem

Right now, the <code>&lt;picture&gt;</code> element is not supported in any shipped browsers. Developers who want to use <code>&lt;picture&gt;</code> can use <a href="https://scottjehl.com/">Scott Jehl</a>’s <a href="https://github.com/scottjehl/picturefill">Picturefill</a> polyfill. Also, <a href="https://blog.yoav.ws/">Yoav Weiss</a> has created a Chromium-based prototype <a href="https://downloads.responsiveimages.org/">reference implementation</a> that has partial support for <code>&lt;picture&gt;</code>. This Chromium build not only shows that browser support for <code>&lt;picture&gt;</code> is technically possible, but also enables us to check functionality and behavior against our expectations.

When testing examples like the above in his Chromium build, Yoav spotted a problem: even though <code>&lt;picture&gt;</code> is supported, and even though one of the first two <code>&lt;source&gt;</code> elements was being loaded, the fallback <code>&lt;img&gt;</code> was <em>also</em> loaded. <strong>Two images were being downloaded, even though only one was being used.</strong>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/553ddee1-66b3-4a7e-8d44-cb856199d3ab/networkpane1.png"><img loading="lazy" decoding="async" class="136035" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e3b643-322e-41a9-8e6e-966b33faaf19/networkpane1-500.png" alt="networkpane1-500" width="500" height="166" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/553ddee1-66b3-4a7e-8d44-cb856199d3ab/networkpane1.png">Larger view</a>.</em>

This happens because browsers “look ahead” as HTML is being downloaded and immediately start downloading images. As Yoav explains:
<blockquote>"When the parser encounters an img tag it creates an HTMLImageElement node and adds its attributes to it. When the attributes are added, the node is not aware of its parents, and when an ‘src’ attribute is added, an image download is immediately triggered."</blockquote>

This kind of “look ahead” parsing works great most of the time because the browser can start downloading images even before it has finished downloading all of the HTML. But in cases where an <code>img</code> element is a child of <code>&lt;picture&gt;</code> (or <code>&lt;video&gt;</code> or <code>&lt;audio&gt;</code>), the browser wouldn’t (currently) care about the parent element: it would just see an <code>img</code> and start downloading. The problem also occurs if we forget about the parent element and just consider an <code>&lt;img&gt;</code> that has both the <code>src</code> and <code>srcset</code> attributes: the parser would download the <code>src</code> image before choosing and downloading a resource from <code>srcset</code>.

<pre><code class="language-markup">
&lt;picture&gt;
    &lt;source srcset="big.jpg 1x, big-2x.jpg 2x, big-3x.jpg 3x" media="(min-width: 40em)" /&gt;
    &lt;source srcset="med.jpg 1x, med-2x.jpg 2x, med-3x.jpg 3x" /&gt;
    &lt;img src="fallback.jpg" alt="fancy pants" /&gt;
    &lt;!-- fallback.jpg is *always* downloaded --&gt;
&lt;/picture&gt;

&lt;img src="fallback.jpg" srcset="med.jpg 1x, med-2x.jpg 2x, med-3x.jpg 3x" alt="fancy pants" /&gt;
&lt;!-- fallback.jpg is *always* downloaded --&gt;

&lt;video&gt;
    &lt;source src="video.mp4" type="video/mp4" /&gt;
    &lt;source src="video.webm" type="video/webm" /&gt;
    &lt;source src="video.ogv" type="video/ogg" /&gt;
    &lt;img src="fallback.jpg" alt="fancy pants" /&gt;
    &lt;!-- fallback.jpg is *always* downloaded --&gt;
&lt;/video&gt;
</code></pre>

In all of these cases, we would have multiple images being downloaded instead of just the one being displayed. But who cares? Well, your users who are downloading extra content and wasting time and money would care, especially the ones with bandwidth caps and slow connections. And maybe you, too, if you’re paying for the bandwidth you serve.</p>

## A Potential Solution

This problem needs both short- and long-term solutions.

In the long term, we need to make sure that browser implementations of <code>&lt;picture&gt;</code> (and <code>&lt;video&gt;</code> and <code>&lt;audio&gt;</code>) can overcome this bug. For example, <a href="https://berjon.com/">Robin Berjon</a> has suggested that it might be possible to treat the contents of <code>&lt;picture&gt;</code> as inert, like the contents of <code>&lt;template&gt;</code>, and to use the Shadow DOM (see, for example, “<a href="https://www.html5rocks.com/en/tutorials/webcomponents/template/">HTML5’s New Template Tag: Standardizing Client-Side Templating</a>”). Yoav has suggested using an attribute on <code>&lt;img&gt;</code> to indicate that the browser should wait to download the <code>src</code>.

While changing the way the parser works is technically possible, it would make the implementation more complicated. Changing the parser could also affect JavaScript code and libraries that assume a download has been triggered as soon as a <code>src</code> attribute is added to an <code>&lt;img&gt;</code>. These long-term changes would require cooperation from browser vendors, JavaScript library creators and developers.

In the short term, we need a working solution that avoids wasted bandwidth when experimenting with <code>&lt;picture&gt;</code> and <code>srcset</code>, and when using <code>&lt;video&gt;</code> and <code>&lt;audio&gt;</code> with <code>&lt;img&gt;</code> fallbacks. Because of the difficulty and time involved in updating specifications and browsers, a short-term solution would need to rely on existing tools and browser behaviors.

So, what is currently available to us that solves this in the short term? Our old friends <code>&lt;object&gt;</code> and <code>&lt;embed&gt;</code>, both of which can be used to display images. If you load an image using these tags, it will <strong>display properly in the appropriate fallback conditions, but it won’t otherwise be downloaded</strong>.

Different browsers behave differently according to whether we use <code>&lt;object&gt;</code>, <code>&lt;embed&gt;</code> or both. To find the best solution, I tested (using a slightly modified version of <a href="https://gist.github.com/4062299">this gist</a>) in:

*   Android browser 528.5+/4.0/525.20.1 on Android 1.6 (using a virtualized Sony Xperia X10 on BrowserStack)
*   Android browser 533.1/4.0/533.1 on Android 2.3.3 (using a virtualized Samsung Galaxy S II on BrowserStack)
*   Android browser 534.30/4.0/534.30 on Android 4.2 (using a virtualized LG Nexus 4 on BrowserStack)
*   Chrome 25.0.1364.160 on OS X 10.8.2
*   Chromium 25.0.1336.0 (169465) (RICG Build) on OS X 10.8.2
*   Firefox 19.0.2 on OS X 10.8.2
*   Internet Explorer 6.0.3790.1830 on Windows XP (using BrowserStack)
*   Internet Explorer 7.0.5730.13 on Windows XP (using BrowserStack)
*   Internet Explorer 8.0.6001.19222 on Windows 7 (using BrowserStack)
*   Internet Explorer 9.0.8112.16421 on Windows 7 (using BrowserStack)
*   Internet Explorer 10.0.9200.16384 (desktop) on Windows 8 (using BrowserStack)
*   Opera 12.14 build 1738 on OS X 10.8.2
*   Opera Mobile 9.80/2.11.355/12.10 on Android 2.3.7 (using a virtualized Samsung Galaxy Tab 10.1 on Opera Mobile Emulator for Mac)
*   Safari 6.0.2 (8536.26.17) on OS X 10.8.2
*   Safari (Mobile) 536.26/6.0/10B144/8536.25 on iOS 6.1 (10B144) (using an iPhone 4)
*   Safari (Mobile) 536.26/6.0/10B144/8536.25 on iOS 6.1 (10B141) (using an iPad 2)

I ran five tests:

1.  `<picture>` falls back to `<object>`
2.  `<picture>` falls back to `<embed>`
3.  `<picture>` falls back to `<object>`, which falls back to `<embed>`
4.  `<picture>` falls back to `<object>`, which falls back to `<img>`
5.  `<picture>` falls back to `<img>`

<strong>I found the following support:</strong>

<strong>What the user sees</strong><br>
<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th></th>
<th><strong>Test 1</strong></th>
<th><strong>Test 2</strong></th>
<th><strong>Test 3</strong></th>
<th><strong>Test 4</strong></th>
<th><strong>Test 5</strong></th>
</tr>
</thead>
<tbody>
<tr>
<th>Android 1.6</th>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
</tr>
<tr>
<th>Android 2.3</th>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
</tr>
<tr>
<th>Android 4.2</th>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
</tr>
<tr>
<th>Chrome 25</th>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
</tr>
<tr>
<th>Chromium 25 (RICG)</th>
<td>picture/source image</td>
<td>picture/source image</td>
<td>picture/source image</td>
<td>picture/source image</td>
<td>picture/source image</td>
</tr>
<tr>
<th>Firefox 19</th>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
</tr>
<tr>
<th>IE 6</th>
<td>no image</td>
<td>no image</td>
<td>no image</td>
<td>no image</td>
<td>fallback image</td>
</tr>
<tr>
<th>IE 7</th>
<td>no image</td>
<td>no image</td>
<td>no image</td>
<td>no image</td>
<td>fallback image</td>
</tr>
<tr>
<th>IE 8</th>
<td>fallback image</td>
<td>no image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
</tr>
<tr>
<th>IE 9</th>
<td>fallback image</td>
<td>fallback image (cropped and scrollable)</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
</tr>
<tr>
<th>IE 10</th>
<td>fallback image</td>
<td>fallback image (cropped and scrollable)</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
</tr>
<tr>
<th>Opera 12.1</th>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
</tr>
<tr>
<th>Opera Mobile 12.1</th>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
</tr>
<tr>
<th>Safari 6</th>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
</tr>
<tr>
<th>Safari iOS 6 (iPad)</th>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
</tr>
<tr>
<th>Safari iOS 6 (iPhone)</th>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
<td>fallback image</td>
</tr>
</tbody>
</table>
<strong>HTTP requests</strong><br>
<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th></th>
<th><strong>Test 1</strong></th>
<th><strong>Test 2</strong></th>
<th><strong>Test 3</strong></th>
<th><strong>Test 4</strong></th>
<th><strong>Test 5</strong></th>
</tr>
</thead>
<tbody>
<tr>
<th>Android 1.6</th>
<td>1 GET</td>
<td>1 GET</td>
<td>1 GET</td>
<td>2 GETs</td>
<td>1 GET</td>
</tr>
<tr>
<th>Android 2.3</th>
<td>1 GET</td>
<td>1 GET</td>
<td>1 GET</td>
<td>2 GETs</td>
<td>1 GET</td>
</tr>
<tr>
<th>Android 4.2</th>
<td>1 GET</td>
<td>1 GET</td>
<td>1 GET</td>
<td>2 GETs</td>
<td>1 GET</td>
</tr>
<tr>
<th>Chrome 25</th>
<td>1 GET</td>
<td>1 GET</td>
<td>1 GET</td>
<td>2 GETs</td>
<td>1 GET</td>
</tr>
<tr>
<th>Chromium 25 (RICG)</th>
<td>1 GET</td>
<td>1 GET</td>
<td>1 GET</td>
<td>2 GETs</td>
<td>2 GETs</td>
</tr>
<tr>
<th>Firefox 19</th>
<td>1 GET</td>
<td>1 GET</td>
<td>2 GETs</td>
<td>2 GETs</td>
<td>1 GET</td>
</tr>
<tr>
<th>IE 6</th>
<td>1 GET</td>
<td>none</td>
<td>1 GET</td>
<td>1 GET</td>
<td>1 GET</td>
</tr>
<tr>
<th>IE 7</th>
<td>1 GET</td>
<td>none</td>
<td>1 GET</td>
<td>1 GET</td>
<td>1 GET</td>
</tr>
<tr>
<th>IE 8</th>
<td>1 GET</td>
<td>none</td>
<td>1 GET</td>
<td>1 GET</td>
<td>1 GET</td>
</tr>
<tr>
<th>IE 9</th>
<td>1 HEAD, 1 GET</td>
<td>1 GET</td>
<td>1 HEAD, 1 GET</td>
<td>1 HEAD, 2 GETs</td>
<td>1 GET</td>
</tr>
<tr>
<th>IE 10</th>
<td>1 HEAD, 1 GET</td>
<td>1 GET</td>
<td>1 HEAD, 1 GET</td>
<td>1 HEAD, 2 GETs</td>
<td>1 GET</td>
</tr>
<tr>
<th>Opera 12.1</th>
<td>1 GET</td>
<td>1 GET</td>
<td>1 GET</td>
<td>2 GETs</td>
<td>1 GET</td>
</tr>
<tr>
<th>Opera Mobile 12.1</th>
<td>1 GET</td>
<td>1 GET</td>
<td>1 GET</td>
<td>2 GETs</td>
<td>1 GET</td>
</tr>
<tr>
<th>Safari 6</th>
<td>1 GET</td>
<td>1 GET</td>
<td>1 GET</td>
<td>2 GETs</td>
<td>1 GET</td>
</tr>
<tr>
<th>Safari iOS 6 (iPad)</th>
<td>1 GET</td>
<td>1 GET</td>
<td>1 GET</td>
<td>2 GETs</td>
<td>1 GET</td>
</tr>
<tr>
<th>Safari iOS 6 (iPhone)</th>
<td>1 GET</td>
<td>1 GET</td>
<td>1 GET</td>
<td>2 GETs</td>
<td>1 GET</td>
</tr>
</tbody>
</table>
<strong>Image-aware context menu</strong><br>
<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th></th>
<th><strong>Test 1</strong></th>
<th><strong>Test 2</strong></th>
<th><strong>Test 3</strong></th>
<th><strong>Test 4</strong></th>
<th><strong>Test 5</strong></th>
</tr>
</thead>
<tbody>
<tr>
<th>Android 1.6</th>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
</tr>
<tr>
<th>Android 2.3</th>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
</tr>
<tr>
<th>Android 4.2</th>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
</tr>
<tr>
<th>Chrome 25</th>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>yes</td>
</tr>
<tr>
<th>Chromium 25 (RICG)</th>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
</tr>
<tr>
<th>Firefox 19</th>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
</tr>
<tr>
<th>IE 6</th>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>yes</td>
</tr>
<tr>
<th>IE 7</th>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>yes</td>
</tr>
<tr>
<th>IE 8</th>
<td>yes</td>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
</tr>
<tr>
<th>IE 9</th>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
</tr>
<tr>
<th>IE 10</th>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
</tr>
<tr>
<th>Opera 12.1</th>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
</tr>
<tr>
<th>Opera Mobile 12.1</th>
<td>yes</td>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
</tr>
<tr>
<th>Safari 6</th>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>yes</td>
</tr>
<tr>
<th>Safari iOS 6 (iPad)</th>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>yes</td>
</tr>
<tr>
<th>Safari iOS 6 (iPhone)</th>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>yes</td>
</tr>
</tbody>
</table>

## Making Sure The Content Is Accessible

Although the specifics of how to provide fallback content for <code>&lt;picture&gt;</code> are <a href="https://github.com/ResponsiveImagesCG/picture-element/pull/23">still being debated</a> (see also <a href="https://github.com/ResponsiveImagesCG/picture-element/issues/6">this thread</a>), I wanted to test how Apple’s VoiceOver performed with different elements. For these experiments, I checked whether VoiceOver read <code>alt</code> attributes in various places, as well as fallback <code>&lt;span&gt;</code> elements. Unfortunately, I wasn’t able to test using other screen readers or assistive technology, although I’d love to hear about your experiences.

<strong>Read by VoiceOver</strong><br>
<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th></th>
<th><code>alt</code> on <code>picture</code></th>
<th><code>alt</code> on <code>source</code> (<code>picture</code> → <code>source</code>)</th>
<th><code>alt</code> on <code>object</code> (<code>picture</code> → <code>object</code>)</th>
<th><code>alt</code> on <code>embed</code> (<code>picture</code> → <code>embed</code>)</th>
<th><code>alt</code> on <code>embed</code> (<code>picture</code> → <code>object</code> → <code>embed</code>)</th>
</tr>
</thead>
<tbody>
<tr>
<th>Chrome 25</th>
<td>no</td>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
</tr>
<tr>
<th>Chromium 25 (RICG)</th>
<td>yes</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
</tr>
<tr>
<th>Firefox 19</th>
<td>no</td>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
</tr>
<tr>
<th>Opera 12.1</th>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
</tr>
<tr>
<th>Safari 6</th>
<td>no</td>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
</tr>
<tr>
<th>Safari iOS 6 (iPad)</th>
<td>no</td>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
</tr>
<tr>
<th>Safari iOS 6 (iPhone)</th>
<td>no</td>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
</tr>
</tbody>
</table>
<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<caption>Read by VoiceOver</caption>
<thead>
<tr>
<th></th>
<th><code>alt</code> on <code>img</code> (<code>picture</code> → <code>object</code> → <code>img</code>)</th>
<th><code>alt</code> on <code>img</code> (<code>picture</code> → <code>img</code>)</th>
<th><code>span</code> (<code>picture</code> → <code>span</code>)</th>
<th><code>span</code> (<code>picture</code> → <code>object</code> → <code>span</code>)</th>
</tr>
</thead>
<tbody>
<tr>
<th>Chrome 25</th>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
</tr>
<tr>
<th>Chromium 25 (RICG)</th>
<td>no</td>
<td>no</td>
<td>no</td>
<td>no</td>
</tr>
<tr>
<th>Firefox 19</th>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
</tr>
<tr>
<th>Opera 12.1</th>
<td>no</td>
<td>no</td>
<td>yes</td>
<td>no</td>
</tr>
<tr>
<th>Safari 6</th>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
</tr>
<tr>
<th>Safari iOS 6 (iPad)</th>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
</tr>
<tr>
<th>Safari iOS 6 (iPhone)</th>
<td>no</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
</tr>
</tbody>
</table>

## Bulletproof Syntax

Based on these data, I’ve come up with the following “bulletproof” solution:

<pre><code class="language-markup">
&lt;picture alt="fancy pants"&gt;
    &lt;!-- loaded by browsers that support picture and that support one of the sources --&gt;
    &lt;source srcset="big.jpg 1x, big-2x.jpg 2x, big-3x.jpg" type="image/jpeg" media="(min-width: 40em)" /&gt;
    &lt;source srcset="med.jpg 1x, med-2x.jpg 2x, big-3x.jpg" type="image/jpeg" /&gt;

    &lt;!-- loaded by IE 8+, non-IE browsers that don’t support picture, and browsers that support picture but cannot find an appropriate source --&gt;
    &lt;![if gte IE 8]&gt;
    &lt;object data="fallback.jpg" type="image/jpeg"&gt;&lt;/object&gt;
    &lt;span class="fake-alt"&gt;fancy pants&lt;/span&gt;
    &lt;![endif]&gt;

    &lt;!-- loaded by IE 6 and 7 --&gt;
    &lt;!--[if lt IE 8]&gt;
    &lt;img src="fallback.jpg" alt="fancy pants" /&gt;
    &lt;![endif]--&gt;
&lt;/picture&gt;

.fake-alt {
    border: 0;
    clip: rect(0 0 0 0);
    height: 1px;
    margin: -1px;
    overflow: hidden;
    padding: 0;
    position: absolute;
    width: 1px;
}
</code></pre>

Here we have a <code>&lt;picture&gt;</code> element, two sources to choose from for browsers that support <code>&lt;picture&gt;</code>, a fallback for most other browsers using <code>&lt;object&gt;</code> and a <code>&lt;span&gt;</code> (see note just below), and a separate <code>&lt;img&gt;</code> fallback for IE 7 and below. The empty <code>alt</code> prevents the actual image from being announced to screen readers, and the <code>&lt;span&gt;</code> is hidden using CSS (which is equivalent to <a href="https://html5boilerplate.com/">HTML5 Boilerplate</a>’s <code>.visuallyhidden</code> class) but still available to screen readers. The <code>&lt;embed&gt;</code> element is not needed.

(<strong>Note:</strong> The use of the <code>&lt;span&gt;</code> as a fake <code>alt</code> is necessary so that VoiceOver reads the text in Opera. Even though Opera has a relatively small footprint, and even though it’s in the process of being switched to WebKit, I still think it’s worth our consideration. However, if you don’t care about supporting that particular browser, you could get rid of the <code>&lt;span&gt;</code> and use an <code>alt</code> on the <code>&lt;object&gt;</code> instead (even though that isn’t strictly allowed by the specification). This is assuming that the <code>&lt;span&gt;</code> and <code>alt</code> have the same content. If you have a richer fallback element, such as a <code>&lt;table&gt;</code>, using both it <em>and</em> a non-empty <code>alt</code> attribute might be desirable.)

A similar solution should also work with <code>&lt;audio&gt;</code>, although <code>&lt;img&gt;</code> fallbacks for that element are, admittedly, rare. When dealing with <code>&lt;video&gt;</code>, the problem goes away if our fallback image is the same as our poster image. If these may be the same, then the “bulletproof” syntax for <code>&lt;video&gt;</code> would be this:

<pre><code class="language-markup">
&lt;video poster="fallback.jpg"&gt;
    &lt;!-- loaded by browsers that support video and that support one of the sources --&gt;
    &lt;source src="video.mp4" type="video/mp4" /&gt;
    &lt;source src="video.webm" type="video/webm" /&gt;
    &lt;source src="video.ogv" type="video/ogg" /&gt;

    &lt;!-- loaded by browsers that don't support video, and browsers that support video but cannot find an appropriate source --&gt;
    &lt;img src="fallback.jpg" alt="fancy pants" /&gt;
&lt;/video&gt;
</code></pre>

However, if your <code>&lt;video&gt;</code> needs a separate fallback and poster image, then you might want to consider using the same structure as the <code>&lt;picture&gt;</code> solution above.

Note that <code>&lt;video&gt;</code> and <code>&lt;audio&gt;</code> don’t have <code>alt</code> attributes, and even if you add them, they will be ignored by VoiceOver. For accessible video, you might want to look into the work being done with <a href="https://dev.w3.org/html5/webvtt/">Web Video Text Tracks</a> (WebVTT).

Unfortunately, extensive testing with <code>&lt;video&gt;</code> and <code>&lt;audio&gt;</code> elements is beyond the scope of this article, so let us know in the comments if you find anything interesting with these.</p>

## How Good (Or Bad) Is This Solution?

Let’s get the bad out of the way first, shall we? This solution is hacky. It’s obviously not workable as a real, long-term solution. It is crazy verbose; no one in their right mind wants to code all of this just to put an image on a page.

Also, semantically, we really should use an <code>&lt;img&gt;</code> element to display an image, not an <code>&lt;object&gt;</code>. That’s what <code>&lt;img&gt;</code> is for.

And there are some practical issues:

*   Chrome and Safari won’t show proper context menus for the images, meaning that users won’t be able to open or save them easily.
*   IE 9 and 10 send an extra HEAD request along with the GET request.
*   Using a `<span>` as a fake `alt` is pretty sketchy, and although it worked for my tests in VoiceOver, it could potentially cause other accessibility problems.

All that being said, as a short-term solution, it’s not <em>too</em> bad. <strong>We get these benefits:</strong>

*   A visible image in every browser is tested (`<picture>` and `<source>` when supported, and the fallback otherwise).
*   Only one HTTP GET request in every browser is tested (and the extra `HEAD` request and response in IE are tiny).
*   VoiceOver is supported (and is hopefully supported with other screen readers).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ceaa8d91-d357-4564-b241-0eab32930d28/networkpane2.png"><img loading="lazy" decoding="async" class="136037" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9673cae5-20f4-4d03-b1ab-eddc9e39e061/networkpane2-500.png" alt="networkpane2-500" width="500" height="166" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ceaa8d91-d357-4564-b241-0eab32930d28/networkpane2.png">Larger view</a>.</em>

The semantics of the solution, while not ideal, are not horrible either: the <a href="https://www.w3.org/TR/html5/embedded-content-0.html#the-object-element">HTML5 specification</a> states that an <code>&lt;object&gt;</code> “element can represent an external resource, which, depending on the type of the resource, will either be treated as an <strong>image</strong>, as a nested browsing context, or as an external resource to be processed by a plugin” (emphasis mine).

And although the <code>&lt;span&gt;</code> is not as nice as a real <code>alt</code> attribute, using a visually hidden element for accessibility is not uncommon. Consider, for example, “Skip to content” links that are visibly hidden but available to screen readers.</p>

## Next Steps

The best part about this solution, though, is that it highlights how bad the current situation is. This is a real problem, and it deserves a better solution than the monstrosity I’ve proposed.

We need discussion and participation from both developers and browser vendors on this. Getting support from browser makers is crucial; a specification can be written for any old thing, but it doesn’t become real until it is implemented in browsers. <strong>Support from developers is needed</strong> to make sure that the solution is good enough to get used in the real world. This consensus-based approach is what was used to add the <code>&lt;main&gt;</code> element to the specification recently; Steve Faulkner discusses this process a bit in his excellent <a href="https://html5doctor.com/interview-steve-faulkner-html5-editor-new-doctor/">interview with HTML5 Doctor</a>.

If you’re interested in helping to solve this problem, please consider joining the discussion:

*   [Join the RICG](https://www.w3.org/community/respimg/), and participate in the [#respimg IRC channel](irc://irc.w3.org:6665/#respimg) and the [public-respimg mailing list](https://list.responsiveimages.org/).
*   Check out the [RICG on GitHub](https://gh.responsiveimages.org/), and consider adding your voice to the [discussion on this issue](https://github.com/ResponsiveImagesCG/picture-element/issues/5#issuecomment-15807311).
*   Join the [W3C public-html mailing list](https://lists.w3.org/Archives/Public/public-html/) and [the WHATWG mailing list](https://lists.whatwg.org/listinfo.cgi/whatwg-whatwg.org) to follow and contribute to discussions about the specifications.
*   Help fix problems with current implementations by reviewing, patching, commenting on and filing bugs for [WebKit](https://bugs.webkit.org/), [Mozilla](https://bugzilla.mozilla.org/) and [Internet Explorer](https://connect.microsoft.com/IE/).

The next step towards a long-term solution is to achieve consensus among developers and browser vendors on how this should work. Don’t get left out of the conversation.

<em>Thanks to fellow RICG members Yoav Weiss, Marcos Cáceres and Mat Marquis for providing feedback on this article.</em>

{{< signature "al" >}}


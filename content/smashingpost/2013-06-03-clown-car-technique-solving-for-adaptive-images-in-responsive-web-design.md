---
title: How To Solve Adaptive Images In Responsive Web Design
slug: clown-car-technique-solving-for-adaptive-images-in-responsive-web-design
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46febaa3-da60-4f3d-8969-9713786b4f7b/clown-opt1.png'
date: 2013-06-03T05:59:11.000Z
author: estelle-weyl
description: >-
  Adaptive images are the current hot topic in conversations about adaptive and responsive Web design. Why? Because no one likes any of the solutions thus far. New elements and attributes are being discussed as a solution for what is, for most of us, a big headache: to provide every user with one image optimized for their display size and resolution, without wasting time, memory or bandwidth with a client-side solution.
categories:
  - Coding
  - CSS
  - Responsive Design
  - SVG
---
We have foreground and background images. We have large and small displays. We have regular and high-resolution displays. We have high-bandwidth and low-bandwidth connections. We have portrait and landscape orientations.

Some people waste bandwidth (and memory) by sending high-resolution images to all devices. Others send regular-resolution images to all devices, with the images looking less crisp on high-resolution displays.

Recommended reading: [Responsive Images Done Right: A Guide To <picture>And srcset</picture>](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/)

{{% feature-panel %}}

What we really want to do is find the holy grail: the one solution that sends the image with the most appropriate size and resolution based on the browser and device making the request that can also be made accessible.

[caption id="" align="alignnone" width="500"]<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19d98d34-eeaa-483b-a209-96fc8ee70b65/clown-opt.png" alt="Clown Car Technique" width="500" height="465" /> Clown Car Technique[/caption]

The “clown car” technique is the closest thing we’ve got to a holy grail: leveraging well-supported media queries, the SVG format and the <code>&lt;object&gt;</code> element to serve responsive images with a single request. The solution isn’t perfect yet, but it’s getting close.</p>

## Background Images And Media Queries

We’ve solved adaptive background images. Media queries make it simple to tailor the size and resolution of images to a device’s pixel ratio, viewport size and even screen orientation.

By using media queries with our background image styles, we can ensure that only the images that are needed are downloaded from the server. We can limit downloads to the assets that are most appropriate, saving bandwidth, memory and HTTP requests.

Recommended reading: [Simple Responsive Images With CSS Background Images](https://www.smashingmagazine.com/2013/07/simple-responsive-images-with-css-background-images/)

Unfortunately, there has been no solution for foreground images — until now. The technology has been available for a long time. The clown car technique is just a new technique that leverages existing technology.</p>

## Proposed Solutions With New Technology

### New Elements and Attributes

With inline or “content” images, getting the browser to download and display only the appropriate foreground image is a bit more difficult. Most people believe that there is no mechanism for the <code>&lt;img&gt;</code> tag to cause an image of the right size and resolution to be downloaded. To that end, <a href="https://github.com/scottjehl/picturefill">polyfills</a> have been created and <a href="https://sencha.com/products.io">services</a> have been established.

The <a href="https://www.w3.org/TR/html-picture-element/#the-picture-element"><code>&lt;picture&gt;</code> element</a> — which leverages the semantics of the HTML5 <code>&lt;video&gt;</code> element, with its support of media queries to swap in different source files — was proposed:

<pre><code class="language-markup">&lt;<strong>picture</strong> alt="responsive image"&gt;
     &lt;source src="large.jpg" media="(min-width:1600px),
     (min-resolution: 136dpi) and (min-width:800px)"&gt;
     &lt;source src="medium.jpg" media="(min-width:800px),
     (min-resolution: 136dpi) and (min-width:400px)"&gt;
     &lt;source src="small.jpg"&gt;
  &lt;!-- fallback --&gt;
  &lt;img src="small.jpg" alt="responsive image"&gt;
&lt;/picture&gt;
</code></pre>

Another method, using a <code>srcset</code> attribute on the <code>&lt;img&gt;</code> element, has also been proposed. The above <code>&lt;picture&gt;</code> element would be written as this:

<pre><code class="language-markup">&lt;img
    alt="responsive image"
    src="small.jpg"
    srcset="large.jpg 1600w,
          large.jpg 800w 1.95x,
          medium.jpg 800w,
          medium.jpg 400w 1.95x"&gt;
</code></pre>

Both solutions have benefits and drawbacks. Picking one is hard — but we don’t have to anymore. The two solutions have been joined into what’s called “<a href="https://www.w3.org/community/respimg/2012/06/18/florians-compromise/">Florian’s Compromise</a>.” However, the <a href="https://www.brucelawson.co.uk/2013/responsive-images-intrerim-report/">traction isn’t quite there</a> yet.

Google has proposed <a href="https://docs.google.com/presentation/d/1y_A6VOZy9bD2i0VLHv9ZWr0W3hZJvlTNCDA0itjI0yM/edit?pli=1#slide=id.p19">client hints</a> as part of HTTP headers, to enable the right image to be served server-side.</p>

### SVG as an Out-of-the-Box Solution

Many people don’t realize that we already have the technology to create and serve responsive images.

SVG has supported media queries for a long time, and <a href="https://caniuse.com/#search=svg">browsers have supported SVG</a> for… well, long enough, too. Most browsers support media queries in SVG (you can <a href="https://jeremie.patonnier.net/experiences/svg/media-queries/test.html">test your own browser</a>). When it comes to responsive images, the only browsers in the mobile space that don’t support SVG are old versions of the Android browser (Android support for SVG began with Android 3.0).

We can leverage browser support for SVG <em>and</em> SVG support for both media queries and raster images to create responsive images, using media queries in SVG to serve up the right image.

My original experiment should theoretically work, and it does work in Internet Explorer (IE) 10 and Opera. When you mark up the HTML, you add a single call to an SVG file.

<pre><code class="language-markup">&lt;img src="<strong>awesomefile.svg</strong>" alt="responsive image"&gt;
</code></pre>

Now, isn’t that code simple?

SVGs support raster images included with the <code>&lt;image&gt;</code> element and with the CSS <code>background-image</code> property. In our responsive SVG, we would include all of the images that we might need to serve and then show only the appropriate image based on media queries.</p>

### Download a Single Raster Image

My first attempt at SVG used <code>&lt;image&gt;</code> with media queries, hiding them with <code>display: none</code>.

While the SVG works perfectly in terms of responsiveness, it has several problems. Unfortunately, setting <code>display: none</code> on an <code>&lt;image&gt;</code> in SVG, similar to <code>&lt;img&gt;</code> in HTML, does not prevent the resource from being downloaded. If you <a href="https://estelle.github.io/clowncar/local.svg">open the <code>&lt;image&gt;</code> SVG in your browser</a>, all four PNGs will be retrieved from the server, making four HTTP requests, wasting bandwidth and memory.

We know from CSS background images that downloading only the images that are needed is indeed possible. Similarly, to prevent the SVG from downloading all of the included images, we would use CSS background images instead of foreground images in our SVG file:

<pre><code class="language-markup">&lt;svg xmlns="https://www.w3.org/2000/svg"
   <strong>viewBox</strong>="0 0 300 329" <strong>preserveAspectRatio</strong>="xMidYMid meet"&gt;

&lt;title&gt;Clown Car Technique&lt;/title&gt;

&lt;style&gt;
svg {
  background-size: 100% 100%;
  background-repeat: no-repeat;
}

@media screen and (max-width: 400px) {
  svg {
    background-image: url(images/small.png");
  }
}

@media screen and (min-width: 401px) and (max-width: 700px) {
  svg {
    background-image: url(images/medium.png);
  }
}

@media screen and (min-width: 701px) and (max-width: 1000px) {
  svg {
    background-image: url(images/big.png);
  }
}

@media screen and (min-width: 1001px) {
  svg {
    background-image: url(images/huge.png);
  }
}
&lt;/style&gt;
&lt;/svg&gt;
</code></pre>

The above can be included directly as an inline &lt;svg&gt;, or embedded with the <code>&lt;img&gt; <strong>src</strong></code>  attribute or <code>&lt;object&gt; <strong>data</strong></code> attribute.

If you’re familiar with media queries and CSS, most of the code above should make sense. The clown car technique uses the same media queries that you would use elsewhere on your adaptive website.

To preserve the aspect ratio of the containing element and ensure that is scales uniformly, we include the <code><strong>viewbox</strong></code> and <code><strong>preserveAspectRatio</strong></code> attributes.

The value of the <code>viewbox</code> attribute is a list of four space- or comma-separated numbers: <code>min-x</code>, <code>min-y</code>, <code>width</code> and <code>height</code>. By defining the width and height of our viewbox, we define the aspect ratio of the SVG image. The values we set for the <a href="https://developer.mozilla.org/en-US/docs/SVG/Attribute/preserveAspectRatio"><code>preserveAspectRatio</code></a> attribute — 300 × 329 — preserve the aspect ratio defined in <code>viewbox</code>.

Issues with including the above include 1) Chrome and Safari not maintaining the aspect ratio when <a href="https://estelle.github.io/clowncar/inlinesvg.html"><code>&lt;svg&gt;</code> is included</a> inline: instead, defaulting the <code>&lt;svg&gt;</code> to 100% width and height. A <a href="https://code.google.com/p/chromium/issues/detail?id=231622">bug has been submitted</a>. 2) Webkit and Firefox not allowing the inclusion of raster images or scripts in SVGs embedded via the <code>&lt;img&gt;</code> element, and 3) No SVG support in IE &lt;=8 and Android &lt;=2.3.3.

When you <a href="https://estelle.github.io/clowncar/jpeg/jpeg/svg.svg">open the SVG file with just background images</a> defined, the raster image will take up the entire viewport. While the <code>&lt;image&gt;</code> version might look better as a standalone file because it is maintaining its aspect ratio and the <code>background-image</code> version is filling up the viewport, when you include the SVG as a separate document pulled into the HTML, the aspect ratio is preserved by default.  The <code>background-size</code> of <code>contain</code>, <code>cover</code> or <code>100%</code> all work: choose the one that works best for your requirements.

The CSS <code>background-image</code> property solves the HTTP request problem. <a href="https://estelle.github.io/clowncar/object/bgonly.svg">Open the SVG file with just PNG background images</a> (or the <a href="https://estelle.github.io/clowncar/jpeg/jpeg/svg.svg">JPEG version</a> ) and look at the “Network” tab in your developer tools, and you’ll see that the SVG has made only two HTTP requests, rather than five. If your monitor is large, then the browser would have downloaded a small SVG file (676 bytes) and <code>huge.png</code> or <code>huge.jpg</code>.

Our first problem — that all of the different sizes of images are downloaded, even those that aren’t needed — has been resolved. This <code>background-image</code> version downloads only the image required, thereby addressing the concerns about multiple HTTP requests and wasted bandwidth.

The magic happens when we include SVG in a flexible layout. You’ll notice that the first time you resize the image, the browser might flicker white as it requests the next required PNG — because it doesn’t automatically download all assets. Rather, it downloads only the asset it needs. Simply declare either the width or the height of the container (<code>&lt;img&gt;</code>, <code>&lt;svg&gt;</code> or <code>&lt;object&gt;</code>) with CSS within your layout media queries, and the SVG will only pull in the single raster image it needs.

We still have the SVG file itself, which requires an HTTP request when not embedded inline with <code>&lt;svg&gt;</code>. We’ll solve that issue third.

## Content Security Issues

In Opera or in Windows 9 or 10, open the <a href="https://estelle.github.io/clowncar/imagetag/">HTML file containing an SVG raster image</a> that is linked to with the <code>&lt;img&gt;</code> tag. Note in the “Resources” panel of the developer tools that only one JPEG or PNG is being downloaded. Resize your browser. Note that the <code>&lt;img&gt;</code> is responsive. Additional JPEGs or PNGs (we could also have used GIF or WebP) are downloaded only when needed.

If you opened the <a href="https://estelle.github.io/clowncar/imagetag/">HTML file containing an SVG raster image</a> in Firefox or WebKit, you would likely have seen no image. The SVG works in all modern browsers, but the <code>&lt;img&gt;</code> that calls in an SVG pulling in raster images works only in Opera and IE 9+. We’ll first cover how it works in IE and Opera, then we’ll cover the issues with WebKit and Firefox.

The code is simple:

<pre><code class="language-markup">&lt;img src="awesomefile.svg" alt="responsive image"&gt;
</code></pre>

When you include the SVG in your HTML <code>&lt;img&gt;</code> with a flexible width, such as 70% of the viewport, then as you grow and shrink the container by changing the window’s size or the CSS, the image will respond accordingly.

The <code>width</code> media query in the SVG is based on the parent element in which the SVG is contained — the <code>&lt;img&gt;</code>, in this case — not the viewport’s width.

As the window grows and shrinks, the image displayed by the SVG changes. In the SVG file, the images are defined as being 100% of the height and width of the parent, which, in the case above, when we opened the SVG directly, was the viewport. Now, the container is the <code>&lt;img&gt;</code> element. Because we included the <code>viewbox</code> and <code>preserveAspectRatio</code> attributes, as long as at least one length is defined, the SVG will grow or shrink to fit that length, maintaining the declared aspect ratio in the SVG, whatever the image’s size.

These foreground images work perfectly in Opera and IE 9+ (the versions found on mobile devices). In Chrome and Safari, if you open the SVG file first, thereby caching it, then the HTML file that contains the foreground SVG image might work as well.

While we saw earlier that the browser can indeed render the SVG, if the SVG is included in our document via the <code>&lt;img&gt;</code> tag, then this particular type of SVG will fail to render.

Why? To prevent cross-domain scripting attacks, some browsers have content security policies in place to keep SVG from importing media or scripts, in case they’re malicious in nature.

Blocking SVGs from importing scripts and images does make sense: To prevent cross-domain scripting attacks, you don’t want a file to pull potentially malicious content. So, SVG is supported, but in the case of WebKit and FireFox, it is just being prevented from pulling in external raster images. I’ve submitted a <a href="https://code.google.com/p/chromium/issues/detail?id=234082">Chrome bug report</a> to get the ban on importing raster images in SVG lifted.

In Firefox, the responsive SVG also works on its own. Firefox fully supports SVG. However, for security reasons, Firefox blocks the importing of external raster images, even if those images are on the same domain. The rationale is that allowing visitors to upload images and then displaying those images and scripts as part of an SVG constitutes a security risk. I would argue that if a website uses unsecured user-generated content, they’re already doing it wrong.

For right now, this simple line…

<pre><code class="language-markup">&lt;img src="awesomefile.svg" alt="responsive image"&gt;
</code></pre>

… is blocked in some browsers and, therefore, isn’t a viable solution.

All browsers support SVG media queries. They all support SVG as foreground or content images. They all support SVG as background images. The support just isn’t identical because of browser security policies.

All browsers do support the <code>&lt;object&gt;</code> tag. Without changing browser security policies, <code>&lt;img&gt;</code> alone won’t work yet. We can leverage the <code>&lt;object&gt;</code> tag.</p>

### With the &lt;object&gt; Tag

The <code>&lt;object&gt;</code> element allows an external resource to be treated as an image. It can take care of the browser security drawbacks we see with <code>&lt;img&gt;</code>, disallowing the importing of images or scripts into an <code>&lt;img&gt;</code> file. The <code>&lt;object&gt;</code> element allows both.

The code isn’t that much more complex:

<pre><code class="language-markup">&lt;object data="awesomefile.svg" type="image/svg+xml"&gt;&lt;/object&gt;
</code></pre>

By default, the <code>&lt;object&gt;</code> will be as wide as the parent element. However, as with images, we can declare a width or height with the <code>width</code> or <code>height</code> attribute or with the CSS <code>width</code> or <code>height</code> property. For the clown car technique to maintain the declared aspect ratio, simply declare just one length value.

Because of the <code>viewbox</code> and <code>preserveAspectRatio</code> declarations in our SVG file, the <code>&lt;object&gt;</code> will by default maintain the declared aspect ratio. You can overwrite this with HTML or CSS attributes.

As noted earlier, the media queries in the SVG match the SVG’s container, not the viewport. The matched media queries in the SVG file will reflect the parent of the <code>&lt;object&gt;</code> tag, rather than the viewport.

If you look at an <a href="https://estelle.github.io/clowncar/object/bgonly.html">SVG being pulled in as the <code>&lt;object&gt;</code> data</a>, you’ll see that it works in all browsers that support SVG.</p>

### With the &lt;svg&gt; Tag

Instead of including an external SVG file, you can also <a href="https://estelle.github.io/clowncar/inlinesvg.html">include the svg as inline content with the &lt;svg&gt; tag</a>. The benefit is no additional http request for an external .svg file.

Unfortunately, Chrome and Safari render the SVG as a full screen block display element and appear to not support the <code>preserveAspectRatio</code> attribute when included this way (they do support <code>preserveAspectRatio</code> when the SVG is included via the <code>&lt;object&gt;</code> tag).

The other drawback is that, unlike  <code>&lt;object&gt;</code>, we can't include fallback content for browsers that don't support SVG. Instead we would need to include <code>background-image</code>, with <code>height</code> and <code>width</code> on the <code>&lt;svg&gt;</code> for browsers that don't support SVG.</p>

### Fallback for IE

The <code>&lt;object&gt;</code> element is supported in all browsers, even mobile browsers. But this technique works only if the browser supports SVG as well. Therefore, it doesn’t work in IE 8 and below or in Android 2.3 and below. There is a fallback for these older browsers. Also, we are making two HTTP requests to pull in the correct image — one for the SVG file and one for the raster image that we want to show — there is a solution for this, too.

What makes <code>&lt;object&gt;</code> more interesting than <code>&lt;img&gt; </code>or  <code>&lt;svg&gt; </code>is that it is a non-empty element that can include fallback content when a browser fails to support the &lt;object&gt;'s data type. If you want, you can include an <code>&lt;img&gt;</code> tag nested in <code>&lt;object&gt;</code> for browsers that don’t support the SVG.

For IE 8 and below, we’ll include our medium-sized raster image because they’re generally displayed on monitors at a normal DPI:

<pre><code class="language-markup">&lt;object data="awesomefile.svg" type="image/svg+xml"&gt;
  &lt;img src="medium.png" alt="responsive image"&gt;
&lt;/object&gt;
</code></pre>

Unfortunately, content nested within <code>&lt;object&gt;</code> is downloaded even when the object is rendered and the nested content is not needed or rendered. This adds a download of the medium-sized image whether or not it is needed.

To handle this issue, we can use conditional comments for IE.

<pre><code class="language-markup">&lt;object data="awesomefile.svg" type="image/svg+xml"&gt;
  &lt;!--[if lte IE 8]&gt;
  &lt;img src="medium.png" alt="Fallback for IE"&gt;
  &lt;![endif]--&gt;
&lt;/object&gt;
</code></pre>

## A Single HTTP Request

We’ve narrowed the SVG to download a single raster image. The &lt;object&gt; method  downloads both the raster  image and the SVG file. We have two HTTP requests instead of one. To prevent additional HTTP requests, we can create an SVG data URI, instead of calling in an external SVG file.

<pre><code class="language-markup">&lt;object data="data:image/svg+xml,&lt;svg viewBox='0 0 300 329' preserveAspectRatio='xMidYMid meet' xmlns='https://www.w3.org/2000/svg'&gt;&lt;title&gt;Clown Car Technique&lt;/title&gt;&lt;style&gt;svg{background-size:100% 100%;background-repeat:no-repeat;}@media screen and (max-width: 400px){svg{background-image:url(images/small.png);}}@media screen and (min-width: 401px) and (max-width:700px){svg{ background-image:url(images/medium.png);}}@media screen and (min-width: 701px) and (max-width:1000px){svg{background-image:url(images/big.png);}}@media screen and (min-width:1001px){svg{background-image:url(images/huge.png);}}&lt;/style&gt;&lt;/svg&gt;" type="image/svg+xml"&gt;
  &lt;!--[if lte IE 8]&gt;
      &lt;img src="images/medium.png" alt="Fallback for IE"&gt;
  &lt;![endif]--&gt;
&lt;/object&gt;
</code></pre>

The code above looks messy, but it’s simply <code>data:image/svg+xml</code>, followed by the contents of the SVG file, minified. It is the same code we would include had we used the content <code>&lt;svg&gt;,</code> but this method supports the <code>preserveAspectRatio</code> attribute of the SVG.

It works in all browsers that support SVG, except IE. While this is frustrating, it’s actually because Microsoft is trying to follow the specification to the letter. The specification states that the data URI must be escaped. So, to make all browsers, including IE 9 and 10, support the data URI, we escape it:

<pre><code class="language-markup">&lt;object data="data:image/svg+xml,%3Csvg%20viewBox='0%200%20300%20329'%20preserveAspectRatio='xMidYMid%20meet'%20xmlns='https://www.w3.org/2000/svg'%3E%3Ctitle%3EClown%20Car%20Technique%3C/title%3E%3Cstyle%3Esvg%7Bbackground-size:100%25%20100%25;background-repeat:no-repeat;%7D@media%20screen%20and%20(max-width:400px)%7Bsvg%7Bbackground-image:url(images/small.png);%7D%7D@media%20screen%20and%20(min-width:401px)%7Bsvg%7Bbackground-image:url(images/medium.png);%7D%7D@media%20screen%20and%20(min-width:701px)%7Bsvg%7Bbackground-image:url(images/big.png);%7D%7D@media%20screen%20and%20(min-width:1001px)%7Bsvg%7Bbackground-image:url(images/huge.png);%7D%7D%3C/style%3E%3C/svg%3E"
type="image/svg+xml"&gt;
  &lt;!--[if lte IE 8]&gt;
    &lt;img src="images/medium.png" alt="Fallback for IE"&gt;
  &lt;![endif]--&gt;
&lt;/object&gt;
</code></pre>

The markup is ugly, but it works!

Open up <a href="https://estelle.github.io/clowncar/singlerequest.html">our first page</a> and <a href="https://estelle.github.io/clowncar/index2.html">our second page</a>, and then open up the developer tools to inspect the HTTP requests. You’ll notice two HTTP requests: the HTML file, and the PNG that the SVG pulls in. The inspector will show an entry for the SVG file as well. But notice that no HTTP request is being made: the status of the SVG is “success,” and the size over the network is 0 bytes, with the size of the data URI SVG coming in at under 600 bytes.</p>

## Landscape Vs. Portrait

Generally, content images are either landscape or portrait: faces are portrait, groups of people, products and sunsets are landscape. Some people object strongly to the clown car technique because they believe that images don’t change according to orientation. That isn’t necessarily true.

The magic of this technique is that the rendered image changes based on the size of the container. You could set your landscape foreground image to 33% or 240 pixels or whatever else, and your portrait object’s width to 25% or 180 pixels or whatever else. The object’s size is determined by the CSS for your HTML. The raster image served is based on the media queries that match the object’s size.

The aspect ratio remains the same, but you can control which raster image is served by changing the proportions of the SVG container, matching the media queries in the HTML’s CSS with the media queries in the SVG’s CSS.

If you do prefer to serve landscape foreground images when in landscape mode and portrait when in portrait mode, don't use the <code>preserveAspectRatio</code> attribute. Instead, declare absolute heights and widths in your CSS for each breakpoint design size.</p>

## Other Benefits

Another benefit of the clown car technique is that all of the logic remains in the SVG file. Similar to how we separate content from presentation from behavior, this method enables us to separate image logic from content. The <code>&lt;img&gt;</code> or <code>&lt;object&gt;</code> element is part of the content, but the logic that makes it all work can be made separate from the content layer: The logic is in the SVG image, instead of polluting the CSS and HTML. This benefit may make some choose the non-data-URI version of the <code>&lt;object&gt;</code> method, in-spite of the extra http request, because it is so easy and clean.

The technique enables us to neatly organize our images, separating behavior from presentation from content from images. I envision the structure of responsive image files to be something like this:

<pre><code class="language-text">images/
  clowns/
    small.png
    medium.png
    large.png
    svg.svg
  cars/
    small.png
    medium.png
    large.png
    svg.svg
  techniques/
    small.png
    medium.png
    large.png
    svg.svg
</code></pre>

All of our assets for a single image live in a single separate directory. The image file names are consistent, while the folder names vary. We can have responsive foreground images without littering our HTML with extra unused code, thus making image management and updating a breeze.</p>

## Drawbacks Of The Clown Car Technique

We’ve covered the pros of the technique. The technique is still nascent, so I haven’t figured out all of the problems. I am working on solutions to some of the issues that have been found, and I assume new issues will arise.

I am mostly concerned with the ways in which images that arise from the clown car technique fail to behave like regular PNGs, JPEGs and GIFs. The main issues I have noticed are loading order, fallback for Android 2.3.3 and below, accessibility, and the ability to right-click on the image.</p>

### Page Layout

According to John Wilkins, the clown car technique requires the CSS layout to fully render before images start to load. I have not had a chance to compare the loading of regular foreground images versus the <code>&lt;object&gt;</code> element with SVG pulling in raster images, so I cannot comment on the impact of this issue yet.</p>

### Android 2.3 and Below

Android 2.3 and below does not support SVG. I have found three possible solutions, which I have yet to flesh out.

<strong><code>&lt;SVG&gt;</code> with <code>background-image</code></strong>

We can use <code>&lt;svg&gt;</code> as inline content instead of <code>&lt;object&gt;</code>. While  IE 8 and below and Android 2.3 and below do not support SVG, with CSS these browsers can give <code>&lt;svg&gt;</code> layout with <code>height</code> and <code>width</code>, and then declare the raster image as the <code>background-image</code> value.

As our goal is to create responsive foreground images without the use of CSS background images, this backward-compatibility hack doesn't suit our purposes. If this is our solution, why not just use CSS background images instead of the Clown Car Technique for all browsers and devices?

<strong>Conditional Comments</strong>

The first is to include conditional comments to include a medium-sized fallback for IE 8 and below, and a small-sized fallback for all browsers that ignore conditional comments (including IE 10):

<pre><code class="language-markup">&lt;!--[if lte IE 8]&gt;
      &lt;img src="images/medium.png" alt="Fallback for IE"&gt;
    &lt;![endif]--&gt;
    &lt;!--[if !IE]&gt; --&gt;
      &lt;img src="images/small.png" alt="fallback"/&gt;
    &lt;!-- &lt;![endif]--&gt;
</code></pre>

This fallback will show the small PNG to all Android phones. Unfortunately, all browsers other than IE 9 and below will download <code>small.png</code>, even though the image will not be shown. In trying to solve for old Android, we are downloading the small PNG to most devices unnecessarily.

<strong>JavaScript Feature Detection</strong>

The other solution is feature detection with JavaScript — i.e. test for SVG support. Include a <code>.no-svg</code> class in the <code>&lt;html&gt;</code> element if the browser doesn’t support SVG. Using a WebKit-prefixed media query to exclude non-WebKit browsers, targeting as follows:

<pre><code class="language-css">.no-svg object[type*="svg"] {
    width: 300px;
    height: 329px;
    background-image: url(small.png);
}
</code></pre>

The properties above add dimensions and a background image to the <code>&lt;object&gt;</code> object. Again, I haven’t tested this yet, and it’s not accessible, which brings us to the next topic.</p>

### Accessibility

The benefit of <code>&lt;img&gt;</code> is that a simple <code>alt</code> attribute can make it accessible. The <code>&lt;object&gt;</code> element does not have an <code>alt</code> attribute. Ideas to make clown car images accessible include the following:

*   Add a `<title>` and `<desc>` to the SVG file.
*   Add ARIA `role="img"` and other ARIA attributes, such as `aria-label` and `aria-labeled-by`.
*   Include `tab-index="0"` to enable the `<object>` to gain focus without changing tab order.
*   Add `alt` attributes to the fallback images.
*   Add alternative text between the opening and closing `<object>` tags.

Mac OS X's Universal Access's VoiceOver reads the content of the SVG's <code>&lt;title&gt;</code> and value of the   <code>aria-label</code> attribute on the <code>&lt;object&gt;</code> when the <code>&lt;object&gt;</code> includes <code>tabindex="0"</code>.  Testing of the <a href="https://estelle.github.io/clowncar/accessibiltytest.html">accessibility testing page</a> still needs to be done with actual screen readers.</p>

### Right-Click to Save

When you right-click on an image in a desktop browser, you’ll get a menu enabling you to save the image. On some phones, a lingering touch on an image will prompt a save. This does not work with <code>&lt;object&gt;</code> or with background images, which is what our SVG is made of.

This “drawback” might be a feature for people who are wary of their images being stolen. In the brief time that I have contemplated this issue, I have yet to come up with a native way to resolve this issue. It is likely resolvable with JavaScript.

If the inability to right-click to save is your main argument against this technique, then recall that while users can right-click on WebP images in browsers that support WebP (only Chrome and Opera), they can’t do much with those images because native applications don’t support this new format. But this needn’t prevent us from moving forward with these bandwidth-saving techniques and features.</p>

## Why “Clown Car”?

With help from <a title="Christopher Schmitt: Designing Web and Mobile Graphics" href="https://dwmgbook.com/">Christopher Schmitt</a> and <a href="https://precisemoves.com/">Amie Gregory</a>, I’ve named this technique “clown car” because it includes many large images (the clowns) in a single tiny SVG image file (the car).

We need to use the non-semantic <code>&lt;object&gt;</code> element as we encourage browser vendors to support raster images in SVG as an <code>&lt;img&gt;</code> source either via CORS or CSP.

The clown car technique is a solution we can use now. Detractors argue that <code>&lt;picture&gt;</code> and/or <code>srcset</code> are the answer without convincing me that the clown car technique isn’t the right answer. Some argue that the lack of support in Android is its downfall, forgetting that Android 2.3.3 and IE 8 don’t support <code>&lt;picture&gt;</code> or <code>srcset</code> either.

I believe the <code>&lt;object&gt;</code> element can be made accessible. While the lack of semantics is a drawback, I will be satisfied using this technique once accessibility is assured. Testing accessibility is my next priority. While I would like to see this element work with the simpler and more semantic <code>&lt;img&gt;</code> tag, once the accessibility issue is resolved, this technique will be production-ready.

{{< signature "al" >}}


---
title: 'Tools And Resources For Editing, Converting And Optimizing SVGs'
slug: tools-and-resources-for-editing-converting-and-optimizing-svgs
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0db3a000-fc59-4375-85bf-6e4adc6c11c7/svg-tools-and-resources.png
date: 2016-04-27T15:19:39.000Z
author: cosima-mielke
summary: >-
  The power of SVGs lies in their **flexibility to adapt to any size** while remaining crisp and sharp. This makes them perfect for responsive web design and, since users can zoom in without sacrificing quality, meaningful from an accessibility-centered point of view.
description: >-
  SVGs are perfect for responsive web design and, since users can zoom in without sacrificing quality, meaningful from an accessibility-centered point of view.
categories:
  - Tools
  - SVG
---
To help you make best use of this potential and tackle SVGs the right way, this article will provide you with tools and resources to simplify editing, converting, optimizing, and delivering SVGs. We’ll take a look at what you can do to make your SVG code lean and performant, dive deeper into dealing with browser bugs, and provide tips for designing an icon system.

This is by no means an extensive guide on the topic. Instead, the article boils the key takeaways from the mentioned resources down to easily digestible bits that you can squeeze into a coffee break for some **in-between SVG enlightenment**. If you want to dive deeper, Sara Soueidan has written a comprehensive chapter on mastering SVG for responsive web design and beyond for [Smashing Book 5](https://shop.smashingmagazine.com/products/smashing-book-5-real-life-responsive-web-design). Happy SVG’ing!

### <span class="rh">Further Reading</span> on SmashingMag:

- [Rethinking Responsive SVG](https://www.smashingmagazine.com/2014/03/rethinking-responsive-svg/)
- [Styling And Animating SVGs With CSS](https://www.smashingmagazine.com/2014/11/styling-and-animating-svgs-with-css/)
- [A Few Different Ways To Use SVG Sprites In Animation](https://www.smashingmagazine.com/2015/03/different-ways-to-use-svg-sprites-in-animation/)
- [Creating Cel Animations With SVG](https://www.smashingmagazine.com/2015/09/creating-cel-animations-with-svg/)

{{% feature-panel %}}

## Free SVG Editors

Quick SVG edits can be done right in the markup, but if they are a bit more involved, the free and open-source SVG-edit comes in handy. The SVG editor is completely web-based and works in any modern browser. Besides viewing and editing features, it offers a number of drawing options and import functions. Convenient.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b16bcc0-5cbd-47c8-877b-3c106817a192/svg-edit-new.png" alt="SVG-edit" width="500" height="352" /><br>
<figcaption>SVG-edit is entirely web-based and comes with a number of drawing and editing tools — great for quick edits.</figcaption></figure>

<p>A more versatile alternative is <a href="https://inkscape.org">Inkscape</a>. The free, open-source vector graphics editor, provides a number of drawing and object manipulation tools and imports and exports not only SVG but also AI, EPS, PS, and PNG. Its SVG output is among the cleanest.</p>

<p>Another free vector graphics editor is <a href="https://boxy-svg.com/">Boxy SVG</a>. It relies on web technologies and, thus, not only works in Chromium-based web browsers just like on your Mac OS X, Windows, Linux and Chrome OS machine, but also outputs code that was generated with browsers in mind.</p>

## SVG Conversion Tools

<p>If you don’t want to build your SVG from scratch, a number of browser tools help you export existing images to a vector graphic — without the time-consuming hand-tracing process. <a href="https://picsvg.com/">PicSVG</a>, for example, lets you upload your image directly to the site, and the SVG is created instantly. It converts from PNG, JPEG, and GIF.</p>

<p><a href="https://vectormagic.com/home">Vectormagic</a> offers some more sophisticated features. The output is richer in detail and the tool gives you more control by letting you review the result and adjust settings such as the level of detail and color. Two conversions are free after you signed up to the site, for continued use there are monthly subscription plans available starting from $7.95.</p>

<p>In case you need to turn a raster image into an SVG, check out Eric Meyer’s <a href="https://github.com/meyerweb/px2svg">px2svg</a>. The PHP script uses color-run optimization and draws filled rectangles to recreate the 8-bit look of the original image.</p>

## Optimizing & Delivering SVGs

<p>Every extra node, path, decimal point and piece of meta information adds to the total file size of an SVG. This increase might seem negligible, but when you have multiple SVGs on your site, things start adding up. To keep your SVGs lean and prevent them from harming the performance of your site, optimizing SVGs is a must.</p>

### A Primer to Optimizing SVGs for Web Use

<p>A good primer on how to do this comes from Andreas Larsen. His 3-part article series teaches you techniques to shave off file size — already <a href="https://medium.com/larsenwork-andreas-larsen/optimising-svgs-for-web-use-part-1-67e8f2d4035#.7zkp3tpoo">when creating your vector graphic</a> but also <a href="https://medium.com/larsenwork-andreas-larsen/optimising-svgs-for-web-use-part-2-6711cc15df46#.uc8z8o21g">when working with SVGs from other creators and with code exported from a graphics editor</a>. The key takeaway: Optimizing your paths by using fewer nodes and fewer handles, integers and a grid that is only as big as necessary are effective ways to spare you bytes.</p>

<p>Additionally, <a href="https://sarasoueidan.com/blog/svgo-tools/">optimization tools</a> like <a href="https://jakearchibald.github.io/svgomg/">svgo</a> take away a lot of extra bloat from the SVG code (be careful when using them, though: <a href="https://sarasoueidan.com/blog/svg-tips-for-designers/#optimize">optimizing by hand might be the better option</a> when you need to keep a certain structure in your SVG, for example for animation purposes), and as Andreas Larsen describes, you can also open the SVG in Atom with live SVG preview to manually remove excess information such as unnecessary commas and spaces, transparent paths that you don’t need, as well as metadata and classes generated by the editor. Saving more than 85% in file size without any visible changes in appearance is not uncommon with techniques like these as an <a href="https://medium.com/larsenwork-andreas-larsen/optimising-svgs-for-web-use-part-2-1-598815d74f9c#.8yss19gvt">experiment with the LinkedIn logo</a> shows.</p>

<figure><a href="https://medium.com/larsenwork-andreas-larsen/optimising-svgs-for-web-use-part-1-67e8f2d4035#.wkbys6kw8"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9721465f-bb6a-4321-8978-695af9e8311d/optimized-vs-not-optimized-small-opt.png" alt="Optimized and not optimized SVGs of the Twitter logo" width="500" height="224" /></a><figcaption>Official vs. optimized SVG versions of the Twitter logo. The optimized logo gets along with fewer handles and nodes without sacrificing detail. (Image credit: <a href="https://medium.com/larsenwork-andreas-larsen/optimising-svgs-for-web-use-part-1-67e8f2d4035#.wkbys6kw8">Andreas Larsen</a>)</figcaption></figure>

### Creating and Exporting Better SVGs for the Web with Illustrator

<p>In her “<a href="https://sarasoueidan.com/blog/svg-tips-for-designers/">Tips for Creating and Exporting Better SVGs for the Web</a>”, Sara Soueidan provides her top nine tips on making the exported SVG code cleaner. One of them is to use simple shape elements like <code>&lt;circle&gt;</code>, <code>&lt;rect&gt;</code> or <code>&lt;line&gt;</code> instead of <code>&lt;path&gt;</code>s since they are more readable and more editable by hand as their <code>&lt;path&gt;</code> counterparts.</p>

### Exporting Clean SVG Code From Sketch

<p>If you have ever exported an SVG file from Sketch, you know that the code that comes from it is messy and cluttered, which, in the worst case, can have a negative impact on the way the SVG acts if you want to manipulate it in code later on. To resolve this problem, Sean Kesterson came up with a <a href="https://medium.com/sketch-app-sources/exploring-ways-to-export-clean-svg-icons-with-sketch-the-correct-way-752e73ec4694#.86fitxfoi">4-step-workflow</a>.</p>

<p>The key takeaways: Set the position of your artboard to even numbers and don’t use half pixels, otherwise Sketch will add an unnecessary <code>transform</code> to your code. Delete any transparent bounding box and use CSS to do the trick instead, otherwise Sketch will export the box which makes it difficult to scale your SVG. Last but not least, each time you rotate anything in Sketch, it adds a <code>rotate</code> attribute, and, if you try to remove that bit from the code, it automatically rotates your graphic back to the original view. The solution might be a detour, but it seems to be the only way to circumvent the rotation: open your SVG in Illustrator, rotate it there, and drag and drop it back into Sketch.</p>

<figure><a href="https://medium.com/sketch-app-sources/exploring-ways-to-export-clean-svg-icons-with-sketch-the-correct-way-752e73ec4694#.86fitxfoi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc7785db-7e50-4e89-be34-39f2760a6681/sketch-bounding-box-small-opt.png" alt="Removing the bounding box in Sketch" width="500" height="409" /></a><figcaption>One step towards generating clean SVG code with Sketch: Delete any transparent bounding box and let CSS do the magic instead. (Image credit: <a href="https://medium.com/sketch-app-sources/exploring-ways-to-export-clean-svg-icons-with-sketch-the-correct-way-752e73ec4694#.1xsrqu5i3">Sean Kesterson</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2b6d3f4-20f2-43f5-9f36-057e56a8f03c/sketch-bounding-box-opt.png">View large version</a>)</figcaption></figure>

### Optimizing SVG Delivery

<p>Just as critical to the performance of your site as working with clean code is <a href="https://calendar.perfplanet.com/2014/tips-for-optimising-svg-delivery-for-the-web/">how you deliver the SVG</a> in the end, of course. Did you know for example that you can gzip your SVGs and save 80% file size on average? When you plan to provide a fallback PNG for browsers that don’t support SVG, Sara Soueidan also recommends setting the fallback image as a background image to a <code>&lt;div&gt;</code> injected between the opening and closing <code>object</code> tag instead of providing it as a foreground <code>img</code>. By doing so, you prevent SVG-capable browsers from requesting both the SVG and the PNG images and thus avoid one unnecessary HTTP request.</p>

### Fixing SVG Scaling In Internet Explorer

<p>A number of bugs in Internet Explorer 9-11 prevent inline SVGs from scaling properly. A fact that is especially problematic for SVGs with variable widths. <a href="https://nicolasgallagher.com/canvas-fix-svg-scaling-in-internet-explorer/">Nicolas Gallagher’s <code>canvas</code>-based hack</a> provides a workaround. The idea behind it: Since a <code>canvas</code> element with <code>width</code> and <code>height</code> set preserves its aspect ratio even when one dimension is scaled, you can make use of this behavior and use <code>canvas</code> as a scalable frame for preserving the aspect ratio of your SVG. To do so, you position the SVG to fill the space created by this frame and set the height of the <code>canvas</code> to <code>100%</code>. This way, the <code>canvas</code> will scale based on the height of the component’s root element, just like SVGs do in supporting browsers. Clever.</p>

### Creating An SVG Icon System

<p>SVG’s scalability and flexibility make it a great alternative to traditional icon fonts. And compared to icon fonts where a user sees nothing if the font fails, SVG also has the benefit of falling back gracefully to PNG (if a fallback is provided, that is). To create an icon system with SVG, save all your SVGs in one folder, and bundle them into one single SVG file, either by hand — <a href="https://css-tricks.com/svg-sprites-use-better-icon-fonts/">Chris Coyier describes how to do it</a> — or you can let the Grunt plugin <a href="https://github.com/FWeinb/grunt-svgstore">grunt-svgstore</a> or <a href="https://icomoon.io/">IcoMoon</a> do the job. Now you only need to inject the SVG at the top of your document, and you’re ready to use and style your icons any way you like.</p>

<p>What are your favorite tools and resources for a smooth SVG workflow? Let us know in the comments below!</p>

{{< signature "il" >}}

---
title: Styling And Animating SVGs With CSS
slug: styling-and-animating-svgs-with-css
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1adc7a6f-536e-43fe-b5c9-c30ae4a27240/styling-and-animating-svgs-with-css.png
date: 2014-11-03T23:08:06.000Z
author: sarasoueidan
description: >-
  Why is it so important to optimize your SVGs? Also, why even put in the effort to make them accessible? In this article, Sara Soueidan explais why, and also how to style and animate with CSS.
summary: >-
  Why is it so important to optimize your SVGs? Also, why even put in the effort to make them accessible? In this article, Sara Soueidan explais why, and also how to style and animate with CSS.
categories:
  - Coding
  - CSS
  - Techniques
  - SVG
---
CSS can be used to style and animate scalable vector graphics, much like it is used to style and animate HTML elements. In this article, which is a modified transcript of a <a href="https://www.youtube.com/watch?v=lf7L8X6ZBu8">talk I recently gave</a> at CSSconf EU and From the Front, I’ll go over the prerequisites and techniques for working with CSS in SVG. 

I’ll also go over how to export and optimize SVGs, techniques for embedding them and how each one affects the styles and animations applied, and then we’ll actually style and animate with CSS.</p>

## Introduction

Scalable vector graphics (SVG) is an XML-based vector image format for two-dimensional graphics, with support for interactivity and animation. In other words, SVGs are XML tags that render shapes and graphics, and these shapes and graphics can be interacted with and animated much like HTML elements can be.

Animations and interactivity can be added via CSS or JavaScript. In this article, we’ll focus on CSS.

There are many reasons why SVGs are great and why you should be using them today:

{{% feature-panel %}}

*   SVG graphics are **scalable and resolution-independent**. They look great everywhere, from high-resolution “Retina” screens to printed media.
*   SVGs have [very good **browser support**](https://caniuse.com/#feat=svg). Fallbacks for non-supporting browsers are easy to implement, too, as we’ll see later in the article.
*   Because SVGs are basically text, they can be gzipped, making the files smaller that their bitmap counterparts (JPEG and PNG).
*   SVGs are **interactive and styleable** with CSS and JavaScript.
*   SVG comes with **built-in graphics effects** such as clipping and masking operations, background blend modes, and filters. This is basically the equivalent of having Photoshop photo-editing capabilities right in the browser.
*   SVGs are **accessible**. In one sense, they have a very accessible DOM API, which makes them a perfect tool for infographics and data visualizations and which gives them an advantage over HTML5 Canvas because the content of the latter is not accessible. In another sense, you can inspect each and every element in an SVG using your favorite browser’s developer tools, just like you can inspect HTML elements. And SVGs are accessible to screen readers if you make them so. We’ll go over accessibility a little more in the last section of this article.
*   Several **tools** are available for creating, editing and optimizing SVGs. And other tools make it easier to work with SVGs and save a lot of time in our workflows. We’ll go over some of these tools next.</p>

## Exporting SVGs From Graphics Editors And Optimizing Them

The three most popular vector graphics editors are:

1.  Adobe Illustrator,
2.  Inkscape,
3.  [Sketch](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/).

Adobe Illustrator is a paid application from Adobe. It is a highly popular editor, with a nice UI and many capabilities that make it the favorite of most designers.

Inkscape is a popular free alternative. Even though its UI is not as nice as Illustrator’s, it has everything you need to work with vector graphics.

Sketch is a Mac OS X-only graphics app. It is not free either, but it has been <a href="https://medium.com/@jm_denis/discovering-sketch-25545f6cb161">making the rounds</a> among designers lately and <a href="https://hackingui.com/design/sketch-design/why-i-moved-to-sketch/">gaining popularity</a>, with a lot of <a href="https://www.sketchappsources.com/">resources and tools</a> being created recently to improve the workflow.

Choose any editor to create your SVGs. After choosing your favorite editor and creating an SVG but before embedding it on a web page, you need to export it from the editor and clean it up to make it ready to work with.

I’ll refer to exporting and optimizing an SVG created in Illustrator. But the workflow applies to pretty much any editor, except for the Illustrator-specific options we’ll go over next.

To export an SVG from Illustrator, start by going to “File” → “Save as,” and then choose “.svg” from the file extensions dropdown menu. Once you’ve chosen the .svg extension, a panel will appear containing a set of options for exporting the SVG, such as which version of SVG to use, whether to embed images in the graphic or save them externally and link to them in the SVG, and how to add the styles to the SVG (by using presentation attributes or by using CSS properties in a <code>&lt;style&gt;</code> element).

The following image shows the best settings to choose when exporting an SVG for the web:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce3770d1-50c4-49bf-80e0-a23a749b89e3/01-ai-options-quick-preview-opt.png" alt="01-Ai-options-quick-preview-opt" width="500" height="628" /><br>
<figcaption></figcaption></figure>

The reasons why the options above are best are explained in Michaël Chaize’s excellent article “<a href="https://creativedroplets.com/export-svg-for-the-web-with-illustrator-cc/">Export SVG for the Web With Illustrator CC</a>.”

Whichever graphics editor you choose, it will <strong>not output perfectly clean and optimized code</strong>. SVG files, especially ones exported from editors, usually contain a lot of redundant information, such as meta data from the editor, comments, empty groups, default values, non-optimal values and other stuff that can be safely removed or converted without affecting the rendering of the SVG. And if you’re using an SVG that you didn’t create yourself, then the code is almost certainly not optimal, so using a standalone optimization tool is advisable.

Several tools for optimizing SVG code are out there. Peter Collingridge’s <a href="https://petercollingridge.appspot.com/svg-editor">SVG Editor</a> is an online tool that you input SVG code into either directly or by uploading an SVG file and that then provides you with several optimization options, like removing redundant code, comments, empty groups, white space and more. One option allows you to specify the number of decimal places of point coordinates.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/181a2d87-566f-4905-bc13-d59a5fe370af/02-svg-editor-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec041707-eed0-4728-bbbd-d8966a68125b/02-svg-editor-quick-preview-opt.png" alt="02-svg-editor-quick-preview-opt" width="500" height="362" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/181a2d87-566f-4905-bc13-d59a5fe370af/02-svg-editor-large-preview-opt.png">View large version</a>)</figcaption></figure>

Peter’s optimizer can also automatically move inline SVG properties to a style block at the top of the document. The nice thing about it is that, when you check an option, you can see the result of the optimization live, which enables you to better decide which optimizations to make. Certain optimizations could end up <strong>breaking</strong> your SVG. For example, one decimal place <em>should</em> normally be enough. If you’re working with a path-heavy SVG file, reducing the number of decimal places from four to one could slash your file’s size by as much as half. However, it could also entirely break the SVG. So, being able to preview an optimization is a big plus.

Peter’s tool is an online one. If you’d prefer an offline tool, try <a href="https://github.com/svg/svgo">SVGO</a> (the “O” is for “optimizer”), a Node.js-based tool that comes with a nice and simple <a href="https://github.com/svg/svgo-gui">drag-and-drop GUI</a>. If you don’t want to use an online tool, this one is a nice alternative.

The following screenshot (showing the path from the image above) is a simple before-and-after illustration of how much Peter’s tool optimizes SVG.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05c15875-a7da-4a58-ba28-73fbd4181347/03-optimized-path-opt.jpg" alt="03-optimized-path-opt" width="500" height="631" /></figure>

Notice the size of the original SVG compared to the optimized version. Not to mention, the optimized version is much more readable.

After optimizing the SVG, it’s ready to be embedded on a web page and further customized or animated with CSS.</p>

{{% ad-panel-leaderboard %}}

## Styling SVGs With CSS

The line between HTML and CSS is clear: HTML is about content and structure, and CSS is about the look. SVG blurs this line, to say the least. SVG 1.1 did not require CSS to style SVG nodes &mdash; styles were applied to SVG elements using attributes known as “presentation attributes.”

Presentation attributes are a shorthand for setting a CSS property on an element. Think of them as special style properties. They even contribute to the style cascade, but we’ll get to that shortly.

The following example shows an SVG snippet that uses presentation attributes to style the “border” (<code>stroke</code>) and “background color” (<code>fill</code>) of a star-shaped polygon:

<div class="break-out">

 <pre><code class="language-markup">&lt;svg xmlns="https://www.w3.org/2000/svg" version="1.1" width="300px" height="300px" viewBox="0 0 300 300"&gt;
  &lt;polygon
fill = "#FF931E"
stroke = "#ED1C24"
stroke-width = "5"
points = "279.1,160.8 195.2,193.3 174.4,280.8   117.6,211.1 27.9,218.3 76.7,142.7 42.1,59.6 129.1,82.7 197.4,24.1 202.3,114 "/&gt;
&lt;/svg&gt;
</code></pre>
</div>

The <code>fill</code>, <code>stroke</code> and <code>stroke-width</code> attributes are presentation attributes.

In SVG, a subset of all CSS properties may be set by SVG attributes, and vice versa. The SVG specification <a href="https://www.w3.org/TR/SVG/propidx.html">lists the SVG attributes that may be set as CSS properties</a>. Some of these attributes are shared with CSS, such as <code>opacity</code> and <code>transform</code>, among others, while some are not, such as <code>fill</code>, <code>stroke</code> and <code>stroke-width</code>, among others.

In SVG 2, this list will include <code>x</code>, <code>y</code>, <code>width</code>, <code>height</code>, <code>cx</code>, <code>cy</code> and a few other presentation attributes that were not possible to set via CSS in SVG 1.1. The new list of attributes can be found in the <a href="https://www.w3.org/TR/SVG2/styling.html#SVGStylingProperties">SVG 2 specification</a>.

Another way to set the styles of an SVG element is to use CSS properties. Just like in HTML, styles may be set on an element using inline style attributes:

<div class="break-out">

 <pre><code class="language-markup">&lt;svg xmlns="https://www.w3.org/2000/svg" version="1.1" style="width: 300px; height: 300px;" viewBox="0 0 300 300"&gt;
&lt;polygon
  style = "fill: #FF931E; stroke: #ED1C24; stroke-width: 5;"
  points = "279.1,160.8 195.2,193.3 174.4,280.8   117.6,211.1 27.9,218.3 76.7,142.7 42.1,59.6 129.1,82.7 197.4,24.1 202.3,114 "/&gt;
&lt;/svg&gt;
</code></pre>
</div>

Styles may also be set in rule sets in a <code>&lt;style&gt;</code> tag. The <code>&lt;style&gt;</code> tag can be placed in the <code>&lt;svg&gt;</code> tag:

<div class="break-out">

 <pre><code class="language-markup">&lt;svg xmlns="https://www.w3.org/2000/svg" version="1.1" width="300px" height="300px" viewBox="0 0 300 300"&gt;
  &lt;style type="text/css"&gt;
  &lt;![CDATA[
  selector {/* styles */}
  ]]&gt;
  &lt;/style&gt;
  &lt;g id=".."&gt; … &lt;/g&gt;
&lt;/svg&gt;
</code></pre>
</div>

And it can be placed outside of it, if you’re embedding the SVG inline in the document:

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;&lt;!-- HTML5 document --&gt;
&lt;html&gt;
&lt;head&gt; … &lt;/head&gt;
&lt;body&gt;
&lt;style type="text/css"&gt;
  /* style rules */
&lt;/style&gt;
&lt;!-- xmlns is optional in an HTML5 document →
&lt;svg viewBox="0 0 300 300"&gt;
&lt;!-- SVG content --&gt;
&lt;/svg&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>

And if you want to completely separate style from markup, then you could always link to an external style sheet from the SVG file, using the <code>&lt;?xml-stylesheet&gt;</code> tag, as shown below:

<div class="break-out">

 <pre><code class="language-markup">&lt;?xml version="1.0" standalone="no"?&gt;
&lt;?xml-stylesheet type="text/css" href="style.css"?&gt;
&lt;svg xmlns="https://www.w3.org/2000/svg" version="1.1" width=".." height=".." viewBox=".."&gt;
  &lt;!-- SVG content --&gt;
&lt;/svg&gt;
</code></pre>
</div>

### Style Cascades

We mentioned earlier that presentation attributes are sort of special style properties and that they are just shorthand for setting a CSS property on an SVG node. For this reason, it only makes sense that SVG presentation attributes would contribute to the style cascade.

Indeed, presentation attributes count as low-level “author style sheets” and are overridden by any other style definitions: external style sheets, document style sheets and inline styles.

The following diagram shows the order of styles in the cascade. Styles lower in the diagram override those above them. As you can see, presentation attribute styles are overridden by all other styles except for those specific to the user agent.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5acee99-eb1f-4042-8406-fe090d2712c6/04-diagram-opt.jpg" alt="04-diagram-opt" width="500" height="800" /></figure>

For example, in the following code snippet, an SVG circle element has been drawn. The fill color of the circle will be deep pink, which overrides the blue fill specified in the presentation attribute.</p>

<pre><code class="language-markup">&lt;circle cx="100" cy="100" r="75" fill="blue" style="fill:deepPink;" /&gt;
</code></pre>

### Selectors

<em>Most</em> CSS selectors can be used to select SVG elements. In addition to the general type, class and ID selectors, SVGs can be styled using CSS2’s <a href="https://www.w3.org/TR/2008/REC-CSS2-20080411/selector.html#dynamic-pseudo-classes">dynamic pseudo-classes</a> (<code>:hover</code>, <code>:active</code> and <code>:focus</code>) and <a href="https://www.w3.org/TR/2008/REC-CSS2-20080411/selector.html#q15">pseudo-classes</a> (<code>:first-child</code>, <code>:visited</code>, <code>:link</code> and <code>:lang</code>. The remaining CSS2 pseudo-classes, including those having to do with <a href="https://www.w3.org/TR/2008/REC-CSS2-20080411/generate.html">generated content</a> (such as <code>::before</code> and <code>::after</code>), are not part of the SVG language definition and, hence, have no effect on the style of SVGs.

The following is a simple animation of the fill color of a circle from deep pink to green when it is hovered over using the tag selector and the <code>:hover</code> pseudo-class:

<pre><code class="language-markup">&lt;style&gt;
circle {
  fill: deepPink;
  transition: fill .3s ease-out;
}

circle:hover {
  fill: #009966;
}
&lt;/style&gt;
</code></pre>

Much more impressive effects can be created. A simple yet very nice effect comes from the <a href="https://useiconic.com/">Iconic</a> icons set, in which a light bulb is lit up when hovered over. A <a href="https://tutsplus.github.io/Styling-Iconic/styling/index.html">demo of the effect</a> is available.</p>

## Notes

Because presentation attributes are expressed as XML attributes, they are case-sensitive. For example, when specifying the fill color of an element, the attribute must be written as <code>fill="…"</code> and not <code>Fill="…"</code>.

Furthermore, keyword values for these attributes, such as the <code>italic</code> in <code>font-style="italic"</code>, are also case-sensitive and must be specified using the exact case defined in the specification that defines that value.

All other styles specified as CSS properties &mdash; whether in a style attribute or a <code>&lt;style&gt;</code> tag or in an external style sheet &mdash; are subject to the grammar rules specified in the CSS specifications, which are generally less case-sensitive. That being said, the <a href="https://www.w3.org/TR/SVG11/styling.html#StylingWithCSS">SVG “Styling”</a> specification recommends using the exact property names (usually, lowercase letters and hyphens) as defined in the CSS specifications and expressing all keywords in the same case, as required by presentation attributes, and not taking advantage of CSS’s ability to ignore case.</p>

{{% ad-panel-leaderboard %}}

## Animating SVGs With CSS

SVGs can be animated the same way that HTML elements can, using CSS keyframes and animation properties or using CSS transitions.

In most cases, complex animations will usually contain some kind of transformation &mdash; a translation, a rotation, scaling and/or skewing.

In most respects, SVG elements respond to <code>transform</code> and <code>transform-origin</code> in the same way that HTML elements do. However, a few inevitable differences result from the fact that, unlike HTML elements, SVG elements aren’t governed by a box model and, hence, have no margin, border, padding or content boxes.

By default, the transform origin of an HTML element is at <code>(50%, 50%)</code>, which is the element’s center. By contrast, an SVG element’s transform origin is positioned at the origin of the user’s current coordinate system, which is the <code>(0, 0)</code> point, in the top-left corner of the canvas.

Suppose we have an HTML <code>&lt;div&gt;</code> and an SVG <code>&lt;rect&gt;</code> element:

<div class="break-out">

 <pre><code class="language-markup">&lt;!DOCTYPE html&gt;
…
&lt;div style="width: 100px; height: 100px; background-color: orange"&gt; &lt;/div&gt;
&lt;svg style="width: 150px; height: 150px; background-color: #eee"&gt;
  &lt;rect width="100" height="100" x="25" y="25" fill="orange" /&gt;
&lt;/svg&gt;
</code></pre>
</div>

If were were to rotate both of them by 45 degrees, without changing the default transform origin, we would get the following result (the red circle indicates the position of the transform origin):

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32276916-e4f7-4aa8-9eef-fbd3570b051d/05-transform-svg-html-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73f07da4-c034-4eeb-9fdc-442ddb7a6d1a/05-transform-svg-html-quick-preview-opt.png" alt="05-transform-svg-html-quick-preview-opt" width="500" height="152" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32276916-e4f7-4aa8-9eef-fbd3570b051d/05-transform-svg-html-large-preview-opt.png">View large version</a>)</figcaption></figure>

What if we wanted to rotate the SVG element around its own center, rather than the top-left corner of the SVG canvas? We would need to explicitly set the transform origin using the <code>transform-origin</code> property.

Setting the transform origin on an HTML element is straightforward: Any value you specify will be set relative to the element’s border box.

In SVG, the transform origin can be set using either a percentage value or an absolute value (for example, pixels). If you specify a transform-origin value in percentages, then the value will be set relative to the element’s bounding box, which includes the stroke used to draw its border. If you specify the transform origin in absolute values, then it will be set relative to the SVG canvas’ current coordinate system of the user.

If we were to set the transform origin of the <code>&lt;div&gt;</code> and <code>&lt;rect&gt;</code> from the previous example to the center using percentage values, we would do this:

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;style&gt;
  div, rect {
  transform-origin: 50% 50%;
}
&lt;/style&gt;
</code></pre>

The resulting transformation would look like so:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a18f8793-bb8b-4e49-9065-acef626de6a3/06-transform-svg-html-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33cae642-0167-46bd-89f8-0de8b780ce0b/06-transform-svg-html-quick-preview-opt.png" alt="06-transform-svg-html-quick-preview-opt" width="500" height="148" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a18f8793-bb8b-4e49-9065-acef626de6a3/06-transform-svg-html-large-preview-opt.png">View large version</a>)</figcaption></figure>

That being said, at the time of writing, setting the transform origin in percentage values currently does not work in Firefox. This is a <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=891074">known bug</a>. So, for the time being, your best bet is to use absolute values so that the transformations behave as expected. You can still use percentage values for WebKit browsers, though.

In the following example, we have a pinwheel on a stick that we’ll rotate using CSS animation. To have the wheel rotate around its own center, we’ll set its transform origin in pixels and percentages:

<div class="break-out">

 <pre><code class="language-markup">&lt;svg&gt;
&lt;style&gt;
.wheel {
  transform-origin: 193px 164px;
  -webkit-transform-origin: 50% 50%;
  -webkit-animation: rotate 4s cubic-bezier(.49,.05,.32,1.04) infinite alternate;
  animation: rotate 4s cubic-bezier(.49,.05,.32,1.04) infinite alternate;
}

@-webkit-keyframes rotate {
  50% {
    -webkit-transform: rotate(360deg);
  }
}

@keyframes rotate {
  50% {
    transform: rotate(360deg);
  }
}

&lt;/style&gt;
&lt;!-- SVG content --&gt;
&lt;/svg&gt;
</code></pre>
</div>

You can check out the <a href="https://codepen.io/SaraSoueidan/pen/d0f94390e6c9af38fa562974399b6222?editors=100">live result on Codepen</a>. Note that, at the time of writing, CSS 3D transformations are <em>not</em> hardware-accelerated when used on SVG elements; they have the same performance profile as SVG transform attributes. However, Firefox <em>does</em> accelerate transforms on SVGs to some extent.</p>

## Animating SVG Paths

There is no way to animate an SVG path from one shape to another in CSS. If you want to <em>morph</em> paths &mdash; that is, animate from one path to another &mdash; then you will need to use JavaScript for the time being. If you do that, I recommend using <a href="https://snapsvg.io/">Snap.svg</a> by Dmitry Baranovskiy, the same person behind the SVG library Raphaël.

Snap.svg is described as being to SVG what jQuery is to HTML, and it makes dealing with SVGs and its quirks a lot easier.

That being said, you could create an animated line-drawing effect using CSS. The animation would require you to know the total length of the path you’re animating and then to use the <code>stroke-dashoffset</code> and <code>stroke-dasharray</code> SVG properties to achieve the drawing effect. Once you know the length of the path, you can animate it with CSS using the following rules:

<pre><code class="language-css">#path {
stroke-dasharray: pathLength;
stroke-dashoffset: pathLength;
/* transition stroke-dashoffset */
transition: stroke-dashoffset 2s linear;
}

svg:hover #path{
  stroke-dashoffset: 0;
}
</code></pre>

In the example above, the path is drawn over the course of two seconds when the SVG is hovered over.

In the next demo, we’ll use the same technique and then use a CSS transition &mdash; with a delay &mdash; to light up the bulb once the path’s animation ends.</p>

<pre><code class="language-css">#cable {
  stroke: #FFF2B1;
  stroke-dasharray: 4000 4000;  
  stroke-dashoffset: 4000;
  stroke-width: 4;
  transition: stroke-dashoffset 8s linear;
}

svg:hover #cable {
  stroke-dashoffset: 0;
}

/* turn lamp on */
.inner-lamp{
  fill:grey;
  transition: fill .5s ease-in 6s;
}

svg:hover .inner-lamp {
  fill: #FBFFF8;
}
/* … */
</code></pre>

You can view the <a href="https://jsbin.com/haxaqa/1/edit?html,output">live demo on JS Bin</a>. Note that you can also write <code>stroke-dasharray: 4000;</code> instead of <code>stroke-dasharray: 4000 4000</code> &mdash; if the two line and gap values are equal, then you can specify only one value to be applied to both.

Sometimes, you might not know the exact length of the path to animate. In this case, you can use JavaScript to retrieve the length of the path using the <code>getTotalLength()</code> method:

<pre><code class="language-javascript">var path = document.querySelector('.drawing-path');
path.getTotalLength();
//set CSS properties up
path.style.strokeDasharray = length;
path.style.strokeDashoffset = length;
//set transition up
path.style.transition = 'stroke-dashoffset 2s ease-in-out';
// animate
path.style.strokeDashoffset = '0';
</code></pre>

The snippet above is a very simplified example showing that you can do the same thing we did with CSS but using JavaScript.

Jake Archibald has written an <a href="https://jakearchibald.com/2013/animated-line-drawing-svg/">excellent article explaining the technique</a> in more detail. Jake includes a nice interactive demo that makes it easy to see exactly what’s going on in the animation and how the two SVG properties work together to achieve the desired effect. I recommend reading his article if you’re interested in learning more about this technique.</p>

## Embedding SVGs

An SVG can be embedded in a document in six ways, each of which has its own pros and cons.

The reason we’re covering embedding techniques is because the way you embed an SVG will determine whether certain CSS styles, animations and interactions will work once the SVG is embedded.

An SVG can be embedded in any of the following ways:

<p>1. as an image using the <code>&lt;img&gt;</code> tag:</p>

<pre><code>&lt;img src="mySVG.svg" alt="" /&gt;</code></pre>

<p>2. as a background image in CSS: 

<pre><code>.el {background-image: url(mySVG.svg);}</code></pre>

<p>3. as an object using the &lt;object&gt; tag:</p>

<pre><code class="language-html">&lt;figure class="aspect-ratio">&lt;object type="image/svg+xml" data="mySVG.svg">&lt;!-- fallback here --&gt;&lt;/figure&gt;&lt;/object&gt;</code></pre>

<p>4. as an iframe using an <code>&lt;iframe&gt;</code> tag:</p>

<pre><code class="language-html">&lt;iframe src="mySVG.svg">&lt;!-- fallback here --&gt;&lt;/iframe&gt;</code></pre>

<p>5. using the &lt;embed&gt; tag:</p>

<pre><code class="language-html">&lt;embed type="image/svg+xml" src="mySVG.svg" /&gt;</code></pre>

<p>6. inline using the &lt;svg&gt; tag:</p>

<pre><code class="language-html">&lt;svg version="1.1" xmlns="https://www.w3.org/2000/svg" …> <!-- svg content -->&lt;/svg&gt;</code></pre>

<p>The <code>&lt;object&gt;</code> tag is the primary way to include an external SVG file. The main advantage of this tag is that there is a standard mechanism for providing an image (or text) fallback in case the SVG does not render. If the SVG cannot be displayed for any reason &mdash; such as because the provided URI is wrong &mdash; then the browser will display the content between the opening and closing <code>&lt;object&gt;</code> tags.</p>

<pre><code class="language-markup">&lt;object type="image/svg+xml" data="mySVG.svg"&gt;
  &lt;img src="fallback-image.png" alt="…" /&gt;
&lt;/object&gt;
</code></pre>

<p>If you intend using any advanced SVG features, such as CSS or scripting, the then HTML5 <code>&lt;object&gt;</code> tag is your best bet.</p>

Because browsers can render SVG documents in their own right, embedding and displaying an SVG using an iframe is possible. This might be a good method if you want to completely separate the SVG code and script from your main page. However, manipulating an SVG image from your main page’s JavaScript becomes a little more difficult and will be subject to the <a href="https://en.wikipedia.org/wiki/Same-origin_policy">same-origin policy</a>.

The <code>&lt;iframe&gt;</code> tag, just like the <code>&lt;object&gt;</code> tag, comes with a default way to provide a fallback for browsers that don’t support SVG, or those that do support it but can’t render it for whatever reason.</p>

<pre><code class="language-markup">&lt;iframe src="mySVG.svg"&gt;
  &lt;img src="fallback-image.png" alt="…" /&gt;
&lt;/iframe&gt;
</code></pre>

The <code>&lt;embed&gt;</code> tag was never a part of any HTML specification, but it is still widely supported. It is intended for including content that needs an external plugin to work. The Adobe Flash plugin requires the <code>&lt;embed&gt;</code> tag, and supporting this tag is the only real reason for its use with SVG. The <code>&lt;embed&gt;</code> tag does not come with a default fallback mechanism.

An SVG can also be embedded in a document inline &mdash; as a “code island” &mdash; using the <code>&lt;svg&gt;</code> tag. This is one of the most popular ways to embed SVGs today. Working with inline SVG and CSS is a lot easier because the SVG can be styled and animated by targeting it with style rules placed anywhere in the document. That is, the styles don’t need to be included between the opening and closing <code>&lt;svg&gt;</code> tags to work; whereas this condition is necessary for the other techniques.

Embedding SVGs inline is a good choice, as long as you’re willing to add to the size of the page and give up backwards compatibility (since it does not come with a default fallback mechanism either). Also, note that an inline SVG cannot be cached.

An SVG embedded with an <code>&lt;img&gt;</code> tag and one embedded as a CSS background image are treated in a similar way when it comes to CSS styling and animation. Styles and animations applied to an SVG using an external CSS resource will not be preserved once the SVG is embedded.

The following table shows whether CSS animations and interactions (such as hover effects) are preserved when an SVG is embedded using one of the six embedding techniques, as compared to SVG <a href="https://css-tricks.com/guide-svg-animations-smil/">SMIL animations</a>. The last column shows that, in all cases, SVG animations (SMIL) are preserved.

<table class="tablesaw break-out"><caption><em>Table showing whether CSS styles, animations and interactions are preserved for each of the SVG embedding techniques.</em></caption>
  <br />
  <thead>
    <tr>
      <th></th>
      <th><strong>CSS Interactions (e.g. <code>:hover</code>)</strong></th>
      <th><strong>CSS Animations</strong></th>
      <th><strong>SVG Animations (SMIL)</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>&lt;img&gt;</code></td>
      <td>No</td>
      <td>Yes only if inside <code>&lt;svg&gt;</code></td>
      <td>Yes</td>
    </tr>
      <tr>
      <td>CSS background image</td>
      <td>No</td>
      <td>Yes only if inside <code>&lt;svg&gt;</code></td>
      <td>Yes</td>
    </tr>
      <tr>
      <td><code>&lt;object&gt;</code></td>
      <td>Yes only if inside <code>&lt;svg&gt;</code></td>
      <td>Yes only if inside <code>&lt;svg&gt;</code></td>
      <td>Yes</td>
    </tr>
      <tr>
      <td><code>&lt;iframe&gt;</code></td>
      <td>Yes only if inside <code>&lt;svg&gt;</code></td>
      <td>Yes only if inside <code>&lt;svg&gt;</code></td>
      <td>Yes</td>
    </tr>
      <tr>
      <td><code>&lt;embed&gt;</code></td>
      <td>Yes only if inside <code>&lt;svg&gt;</code></td>
      <td>Yes only if inside <code>&lt;svg&gt;</code></td>
      <td>Yes</td>
    </tr>
      <tr>
      <td><code>&lt;svg&gt;</code> (inline)</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

The behavior indicated in the table above is the standard behavior. However, implementations may differ between browsers, and bugs may exist.

Note that, even though SMIL animations will be preserved, SMIL interactions will not work for an SVG embedded as an image (i.e. <code>&lt;img&gt;</code> or via CSS).</p>

## Making SVGs Responsive

After embedding an SVG, you need to make sure it is responsive.

Depending on the embedding technique you choose, you might need to apply certain hacks and fixes to get your SVG to be cross-browser responsive. The reason for this is that the way browsers determine the dimensions of an SVG differs for some embedding techniques, and SVG implementations among browsers also differ. Therefore, the way SVG is handled is different and requires some style tweaking to make it behave consistently across all browsers.

I won’t get into details of browser inconsistencies, for the sake of brevity. I will only cover the fix or hack needed for each embedding technique to make the SVG responsive in all browsers for that technique. For a detailed look at the inconsistencies and bugs, check out <a href="https://tympanus.net/codrops/2014/08/19/making-svgs-responsive-with-css/">my article on Codrops</a>.

Whichever technique you choose, the first thing you’ll need to do is remove the <code>height</code> and <code>width</code> attributes from the root <code>&lt;svg&gt;</code> element.

You will need to preserve the <code>viewBox</code> attribute and set the <code>preserveAspectRatio</code> attribute to <code>xMidYMid meet</code> &mdash; if it isn’t already set to that value. Note that you might not need to explicitly set <code>preserveAspectRatio</code> to <code>xMidYMid meet</code> at all because it will default to this value anyway if you don’t change it.

When an SVG is embedded as a CSS background image, no extra fixes or hacks are needed. It will behave just like any other bitmap background image and will respond to CSS’ background-image properties as expected.

An SVG embedded using an <code>&lt;img&gt;</code> tag will automatically be stretched to the width of the container in all browsers (once the width has been removed from the <code>&lt;svg&gt;</code>, of course). It will then scale as expected and be fluid in all browsers except for Internet Explorer (IE). IE will set the height of the SVG to 150 pixels, preventing it from scaling correctly. To fix this, you will need to explicitly set the width to 100% on the <code>&lt;img&gt;</code>.</p>

<pre><code class="language-markup">&lt;img src="mySVG.svg" alt="SVG Description." /&gt;
img {
  width: 100%;
}
</code></pre>

The same goes for an SVG embedded using an <code>&lt;object&gt;</code> tag. For the same reason, you will also need to set the width of the <code>&lt;object&gt;</code> to 100%:

<pre><code class="language-css">object {
  width: 100%;
}
</code></pre>

Even though <code>&lt;iframe&gt;</code> has a lot in common with <code>&lt;object&gt;</code>, browsers seem to handle it differently. For it, all browsers will default to the <a href="https://www.w3.org/TR/CSS2/visudet.html#inline-replaced-width">default size for replaced elements in CSS</a>, which is 300 by 150 pixels.

The only way to make an iframe responsive while maintaining the aspect ratio of the SVG is by using the “padding hack” pioneered by <a href="https://alistapart.com/article/creating-intrinsic-ratios-for-video/">Thierry Koblentz on A List Apart</a>. The idea behind the padding hack is to make use of the relationship of an element’s padding to its width in order to create an element with an intrinsic ratio of height to width.

When an element’s padding is set in percentages, the percentage is calculated relative to the width of the element, even when you set the top or bottom padding of the element.

To apply the padding hack and make the SVG responsive, the SVG needs to be wrapped in a container, and then you’ll need to apply some styles to the container and the SVG (i.e. the iframe), as follows:

<div class="break-out">

 <pre><code class="language-markup">&lt;!-- wrap svg in a container --&gt;
&lt;div class="container"&gt;
  &lt;iframe src="my_SVG_file.svg"&gt;
    &lt;!-- fallback here --&gt;
  &lt;/iframe&gt;
&lt;/div&gt;

.container {
  /&#42; collapse the container’s height &#42;/
  height: 0;        

  /&#42; specify any width you want (a percentage value, basically) &#42;/     
  width: width-value;    

  /&#42; apply padding using the following formula &#42;/
  /&#42; this formula makes sure the aspect ratio of the container equals that of the SVG graphic &#42;/
  padding-top: (svg-height / svg-width) &#42; width-value;
  position: relative;    /&#42; create positioning context for SVG &#42;/
}
</code></pre>
</div>

The <code>svg-height</code> and <code>svg-width</code> variables are the values of the height and width of the <code>&lt;svg&gt;</code>, respectively &mdash; the dimensions that we removed earlier. And the <code>width-value</code> is any width you want to give the SVG container on the page.

Finally, the SVG itself (the iframe) needs to be positioned absolutely inside the container:

<pre><code class="language-css">iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</code></pre>

We position the iframe absolutely because collapsing the container’s height and then applying the padding to it would push the iframe beyond the boundaries of the container. So, to “pull it back up,” we position it absolutely. You can read more about the details in <a href="https://tympanus.net/codrops/2014/08/19/making-svgs-responsive-with-css/">my article on Codrops</a>.

Finally, an SVG embedded inline in an <code>&lt;svg&gt;</code> tag becomes responsive when the height and width are removed, because browsers will assume a width of 100% and will scale the SVG accordingly. However, IE has the same 150-pixel fixed-height issue for the <code>&lt;img&gt;</code> tag mentioned earlier; unfortunately, setting the width of the SVG to 100% is not sufficient to fix it this time.

To make the inline SVG fluid in IE, we also need to apply the padding hack to it. So, we wrap <code>&lt;svg&gt;</code> in a container, apply the padding-hack rules mentioned above to the container and, finally, position the <code>&lt;svg&gt;</code> absolutely inside it. The only difference here is that we do not need to explicitly set the height and width of <code>&lt;svg&gt;</code> after positioning it.</p>

<pre><code class="language-css">svg {
  position: absolute;
  top: 0;
  left: 0;
}
</code></pre>

## Using CSS Media Queries

SVG accepts and responds to CSS media queries as well. You can use media queries to change the styles of an SVG at different viewport sizes.

However, one important note here is that the viewport that the SVG responds to is the viewport of the SVG itself, not the page’s viewport, unless you are embedding the SVG inline in the document (using <code>&lt;svg&gt;</code>).

An SVG embedded with an <code>&lt;img&gt;</code>, <code>&lt;object&gt;</code> or <code>&lt;iframe&gt;</code> will respond to the viewport established by these elements. That is, the dimensions of these elements will form the viewport inside of which the SVG is to be drawn and, hence, will form the viewport to which the CSS media-query conditions will be applied. This is very similar in concept to element queries.

The following example includes a set of media queries inside an SVG that is then referenced using an <code>&lt;img&gt;</code> tag:

<div class="break-out">

 <pre><code class="language-markup">&lt;svg xmlns="https://www.w3.org/2000/svg" version="1.1" viewBox="0 0 194 186"&gt;
  &lt;style&gt;
    @media all and (max-width: 50em) {
      /* select SVG elements and style them */
    } 
    @media all and (max-width: 30em) {
      /* styles  */
    }
  &lt;/style&gt;
  &lt;!-- SVG elements here --&gt;
&lt;/svg&gt;
</code></pre>
</div>

When the SVG is referenced, it will get the styles specified in the media queries above when the <code>&lt;img&gt;</code> has a <code>max-width</code> of <code>50em</code> or <code>30em</code>, respectively.</p>

<pre><code class="language-markup">&lt;img src="my-logo.svg" alt="Page Logo." /&gt;
</code></pre>

You can learn more about media queries inside SVGs in <a href="https://dev.opera.com/blog/how-media-queries-allow-you-to-optimize-svg-icons-for-several-sizes/">Andreas Bovens’s article for Dev.Opera</a>.</p>

## Final Words

SVGs are images, and just as images can be accessible, so can SVGs. And making sure your SVGs are accessible is important, too.

I can’t emphasize this enough: <strong>Make your SVGs accessible</strong>. You can do several things to make that happen. For a complete and excellent guide, I recommend <a href="https://www.sitepoint.com/tips-accessible-svg/">Leonie Watson’s excellent article on SitePoint</a>. Her tips include using the <code>&lt;title&gt;</code> and <code>&lt;desc&gt;</code> tags in the <code>&lt;svg&gt;</code>, using ARIA attributes and much more.

In addition to accessibility, don’t forget to optimize your SVGs and provide fallbacks for non-supporting browsers. I recommend <a href="https://docs.google.com/presentation/d/1CNQLbqC0krocy_fZrM5fZ-YmQ2JgEADRh3qR6RbOOGk/pub?start=true&amp;loop=false&amp;delayms=5000#slide=id.p">Todd Parker’s presentation</a>.

Last but not least, you can always check support for different SVG features on <a href="https://caniuse.com/#search=svg">Can I Use</a>. I hope you’ve found this article to be useful. Thank you for reading.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Rethinking Responsive SVG](https://www.smashingmagazine.com/2014/03/rethinking-responsive-svg/)
*   [A Few Different Ways To Use SVG Sprites In Animation](https://www.smashingmagazine.com/2015/03/different-ways-to-use-svg-sprites-in-animation/)
*   [Creating Cel Animations With SVG](https://www.smashingmagazine.com/2015/09/creating-cel-animations-with-svg/)
*   [The Guide To CSS Animation: Principles and Examples](https://www.smashingmagazine.com/2011/09/the-guide-to-css-animation-principles-and-examples/)

{{< signature "vf, al, il" >}}

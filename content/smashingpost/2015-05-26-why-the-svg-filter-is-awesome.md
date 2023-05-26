---
title: The Art Of SVG Filters And Why It Is Awesome
slug: why-the-svg-filter-is-awesome
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29cd440a-1104-4bdf-bcc0-b83b9997f960/blop-example-illu-opt.jpg
date: 2015-05-26T21:06:01.000Z
author: dirk-weber
summary: >-
  Wouldn’t it be great if we could style letters the same way we usually style text with CSS? In this article we’ll see how SVG filters help us to create playful, decorative web typography.
description: >-
  Wouldn’t it be great if we could style letters the same way we usually style text with CSS? In this article we’ll see how SVG filters help us to create playful, decorative web typography. 
categories:
  - Coding
  - CSS
  - Responsive Design
  - SVG
---
<p>After almost 20 years of evolution, today’s web typography, with its high-density displays and support for OpenType features, is just a step away from the typographic quality of the offline world. But <strong>there’s still one field of graphic design where we still constantly fall back</strong> to bitmap replacements instead of using native text: display typography, the art of staging letters in illustrative, gorgeous, dramatic, playful, experimental or unexpected ways.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e43727eb-d265-4aec-9bbe-b803b3c0a367/splash-svg.html"><img title="The Art Of SVG Filters And Why It Is Awesome" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8c7eb42-9f88-4df3-899f-39f45a9718ee/3-splash-preview-opt.jpg" alt="SVG Filters" width="500" /></a><figcaption>Liquid type effect (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e43727eb-d265-4aec-9bbe-b803b3c0a367/splash-svg.html">demo</a>)</figcaption></figure>

### A Case For Display Text In HTML

<p>Sure, we’re able choose from thousands of web fonts and use CSS effects for type, some with wide browser support (like drop-shadows and 3D transforms) and others that are more experimental (like <code>background-clip</code> and <code>text-stroke</code>), but that’s basically it. If we want really outstanding display typography on our websites, we’ll usually embed it as an image.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f52e470-ca56-41cb-a896-152017ef36d3/extruded-svg.html"><img title="Woodtype style, created purely with SVG filters." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f82964c2-a3a8-4f0a-9ba0-bfb81feaf6c2/2-woodtype-preview-opt.jpg" alt="Woodtype style, created purely with SVG filters." width="500" /></a><figcaption>Woodtype, a style created purely with SVG filters (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f52e470-ca56-41cb-a896-152017ef36d3/extruded-svg.html">demo</a>)</figcaption></figure>

<p>The disadvantages of using images for type on the web are obvious: file size, lack of feasibility for frequently altered or user-generated content, accessibility, time-consuming production of assets, etc.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Web Image Effects Performance Showdown](https://www.smashingmagazine.com/2016/05/web-image-effects-performance-showdown/)
*   [Animating Clipped Elements In SVG](https://www.smashingmagazine.com/2015/12/animating-clipped-elements-svg/)
*   [Styling And Animating SVGs With CSS](https://www.smashingmagazine.com/2014/11/styling-and-animating-svgs-with-css/)
*   [Rethinking Responsive SVG](https://www.smashingmagazine.com/2014/03/rethinking-responsive-svg/)

<p>Wouldn’t it be great if we could style letters the same way we usually style text with CSS? Apply multiple borders with different colors? Add inner and outer bevels? Add patterns, textures and 3D-effects? Give type a used look? Use multiple colors and distorted type? Give type a distressed look?</p>

{{% feature-panel %}}

### Sophisticated SVG Filters: CSS For Type

<p>Most of this is already possible: The trick is to unleash the magic of SVG filters. SVG filters (and CSS filters) are usually considered a way to spice up bitmaps via blur effects or color manipulation. But they are much more. Like CSS rules, an SVG filter can be a set of directives to add another visual layer on top of conventional text. With the CSS <code>filter</code> property, these effects can be used outside of SVG and be applied directly to HTML content.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/091ac72c-a975-481c-9c5a-f3adf7961f83/3dneon-svg.html"><img title="A 3D vintage effect" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d97073f0-f429-4dc0-9d92-05024a883840/4-west-preview-opt.jpg" alt="A 3D vintage effect" width="500" /></a><figcaption>3D vintage effect (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/091ac72c-a975-481c-9c5a-f3adf7961f83/3dneon-svg.html">demo</a>)</figcaption></figure>

<p>Talking about filters in CSS and SVG can be a bit confusing: SVG filters are defined in an SVG <code>filter</code> element and are usually applied within an SVG document. CSS filters can be applied to any HTML element via the <code>filter</code> property. CSS filters such as <code>blur</code>, <code>contrast</code> and <code>hue-rotate</code> are shortcuts for predefined, frequently used SVG filter effects. Beyond that, <a title="CSS3 Filter Modules at the W3C" href="https://www.w3.org/TR/filter-effects/">the specification</a> allows us to reference user-defined filters from within an SVG. A further point of confusion is the proprietary <code>-ms-</code> <code>filter</code> tag, which was deprecated in Internet Explorer (IE) 9 and removed when IE 10 was released.</p>

<p>This article mostly deals with the first case: SVG filters used in an SVG document embedded on an HTML page, but later we’ll experiment with SVG filters applied to HTML content.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23517f5e-da8d-48b4-ba7f-d4c788661ce7/copperplate-svg.html"><img title="Using feImage to fill text with a repeating pattern" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a0263b2-6126-48a4-a08c-ff4b01974447/5-imagefill-preview-opt.jpg" alt="Using feImage to fill text with a repeating pattern" /></a><figcaption>Using <code>feImage</code> to fill text with a repeating pattern (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23517f5e-da8d-48b4-ba7f-d4c788661ce7/copperplate-svg.html">demo</a>)</figcaption></figure>

<p>The illustrations in this article are taken from demos of SVG filter effects applied to text. Click on any one of them to see the original (modern, SVG-capable browsers only). I call them "sophisticated" SVG filters because under the hood these filters are crafted by combining multiple effects into one output. And even though the appearance of the letters has been altered dramatically, under the hood the text is still crawlable and accessible and can be selected and copied. Because SVG filters are supported in every modern browser, these effects can be displayed in browsers beginning from IE 10.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c75f61a-c1fb-4a2e-ad51-bcfc05e751d2/sketchy-svg.html"><img title="Applying a sketch effect to text" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74cd0a4d-0c8a-418f-a240-486a3b62c9a6/6-sketchy-preview-opt.jpg" alt="Applying a sketch effect to text" /></a><figcaption>A sketchy text effect (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c75f61a-c1fb-4a2e-ad51-bcfc05e751d2/sketchy-svg.html">demo</a>)</figcaption></figure>

<p>Understanding SVG filters is challenging. Even simple effects like drop-shadows require a complicated, verbose syntax. Some filers, such as <code>feColorMatrix</code> and <code>feComposite</code>, are difficult to grasp without a thorough understanding of math and color theory. This article will not be a tutorial on learning SVG filters. Instead I will describe a set of standard <strong>building blocks</strong> to achieve certain effects, but I will keep explanations to the bare minimum, focusing on documenting the individual steps that make up an effect. You will mostly read about the how; for those who want to know the why, I've put a reading list at the end of this article.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2817997-e4b1-4d89-8ff8-ce9830d15bc6/pop-svg.html"><img title="Variations of posterized text effects" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6febc407-5252-42fd-afd1-9adcac577801/7-pop-preview-opt.jpg" alt="Variations of posterized text effects" /></a><figcaption>Some variations of posterized text effects (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2817997-e4b1-4d89-8ff8-ce9830d15bc6/pop-svg.html">demo</a>)</figcaption></figure>

{{% ad-panel-leaderboard %}}

### Constructing A Filter

<p>Below is a sophisticated SVG fiter in action. The output of this filter is a weathered text effect, and we will use this for a step-by-step walkthrough:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a66341ae-9277-4e93-b50b-c99e91a3f083/weathered-svg.html"><img title="Making text look grungy" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c91ecdc-6b59-47ef-95ad-3c29f723f95c/8-grungy-preview-opt.jpg" alt="Making text look grungy" /></a><figcaption>A grungy wall painting (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a66341ae-9277-4e93-b50b-c99e91a3f083/weathered-svg.html">demo</a>)</figcaption></figure>

<p>Let’s break down this effect into its building blocks:</p>

<ol>
  <li>green text;</li>
  <li>red extrusion;</li>
  <li>text and extrusion are separated by a transparent gap;</li>
  <li>text has a grungy, weathered look.</li>
</ol>

<p>Our SVG filter effect will be constructed by combining multiple small modules, so-called "filter primitives." Every building block is constructed from a set of one or more primitives that are then combined into a unified output. This process is easier to understand when shown as a graph:</p>

<figure><img title="Image of an SVG filter graph" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47598183-01aa-4786-aa36-93e6490b5429/9-filtergraph-preview-opt.jpg" alt="Image of an SVG filter graph" width="500" /><br>
<figcaption>The processing steps that make up a sophisticated filter are illustrated best in a graph.</figcaption></figure>

### Adding A Filter

<p>We’ll start with a boilerplate SVG that contains an empty filter and text:</p>

<div class="break-out">

<pre><code class="language-markup">&lt;svg version="1.1" id="Ebene_1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink"&gt;
  &lt;defs&gt;
    &lt;style type="text/css"&gt;
      &lt;![CDATA[
        .filtered{
          filter: url(#myfilter);
          …
        }
      ]]&gt;
    &lt;/style&gt;

    &lt;filter id="myfilter"&gt;
      &lt;!-- filter stuff happening here --&gt;
    &lt;/filter&gt;
  &lt;/defs&gt;

  &lt;g class="filtered"&gt;
    &lt;text x="0" y="200" transform="rotate(-12)"&gt;Petrol&lt;/text&gt;
  &lt;/g&gt;
&lt;/svg&gt;
</code></pre></div>

### The <code>filter</code> Element

<p>We have to start somewhere, and the <code>filter</code> tag is the element to begin with. Between its start and end tag, we will put all of the rules for transformation, color, bitmap manipulation, etc. The filter can then be applied to a target as an attribute or via CSS. The target will usually be an element inside an SVG, but later on we will learn about another exciting option: applying SVG filters to HTML elements.</p>

<p>A handful of attributes exist to control the <code>filter</code> element:</p>

*   x and y positions (default -10%);
*   width and height (default 120%);
*   an ID, which is necessary to refer to later on;
*   `filterRes`, which predefines a resolution (deprecated with the "[Filter Effects Module Level 1](https://www.w3.org/TR/filter-effects/ "CSS3 Filter Modules at the W3C")" specification);
*   relative (`objectBoundingBox` is the default) or absolute (`userSpaceOnUse`) `filterUnits`.</p>

{{% ad-panel-leaderboard %}}

### A Word on Filter Primitives

<p>As we've learned, filter primitives are the building blocks of SVG filters. To have any effect, an SVG filter should contain at least one primitive. A primitive usually has one or two inputs (<code>in</code>, <code>in2</code>) and one output (<code>result</code>). Primitives exist for blurring, moving, filling, combining or distorting inputs.</p>

<p>The specification allows us to take several attributes of the filtered element as an input source. Because most of these do not work reliably across browsers anyway, in this article we will stick with <code>SourceGraphic</code> (the unfiltered source element with colors, strokes, fill patterns, etc.) and <code>SourceAlpha</code> (the opaque area of the alpha channel — think of it as the source graphic filled black), which do have very good browser support.</p>

### How To Thicken The Input Text

<p>The first filter primitive we will get to know is <code>feMorphology</code>, a primitive meant to extend (<code>operator="dilate"</code>) or thin (<code>operator="erode"</code>) an input — therefore, perfectly suited to creating outlines and borders.</p>

<p>Here is how we would fatten the <code>SourceAlpha</code> by four pixels:</p>

<figure><img title="Source fattened by 4 pixels" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/043c6b06-e656-444e-95b9-0dbd38b1dc42/10-walkthrough-01-preview-opt.jpg" alt="Source fattened by 4 pixels" width="500" /><br>
<figcaption>Source fattened by four pixels</figcaption></figure>

<div class="break-out">

<pre><code class="language-markup">&lt;feMorphology operator="dilate" radius="4" in="SourceAlpha" result="BEVEL_10" /&gt;
</code></pre></div>

### Creating an Extrusion

<p>The next step is to create a 3D extrusion of the result from the last primitive. Meet <code>feConvolveMatrix</code>. This filter primitive is one of the mightiest and most difficult to grasp. Its main purpose is to enable you to create your own filter. In short, you would define a pixel raster (a kernel matrix) that alters a pixel according to the values of its neighbouring pixels. This way, it becomes possible to create your own filter effects, such as a blur or a sharpening filter, or to create an extrusion.</p>

<p>Here is the <code>feConvolveMatrix</code> to create a 45-degree, 3-pixel deep extrusion. The <code>order</code> attribute defines a width and a height, so that the primitive knows whether to apply a 3×3 or a 9×1 matrix:</p>

<figure><img title="Using feConvolveMatrix to create an extrusion on the fattened input" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4594bd67-71ad-4893-bd1d-dfc4b843f959/11-walkthrough-02-preview-opt.jpg" alt="Using feConvolveMatrix to create an extrusion on the fattened input" /><figcaption>Using <code>feConvolveMatrix</code> to create an extrusion on the fattened input</figcaption></figure>

<pre><code class="language-markup">&lt;feConvolveMatrix order="3,3" kernelMatrix=
   "1 0 0 
   0 1 0
   0 0 1" in="BEVEL_10" result="BEVEL_20" /&gt;
</code></pre>

<p>Be aware that IE 11 and Microsoft Edge (at the time of writing) cannot handle matrices with an order greater than 8×8 pixels, and they do not cope well with multiline matrix notation, so removing all carriage returns before deploying this code would be best.</p>

<p>The primitive will be applied equally to the left, top, right and bottom. Because we want it to extrude only to the right and bottom, we must offset the result. Two attributes define the starting point of the effect, <code>targetX</code> and <code>targetY</code>. Unfortunately, IE interprets them contrary to all other browsers. Therefore, to maintain compatibility across browsers, we will handle offsetting with another filter primitive, <code>feOffset</code>.</p>

### Offsetting

<p>As the name implies, <code>feOffset</code> takes an input and, well, offsets it:</p>

<pre><code class="language-markup">&lt;feOffset dx="4" dy="4" in="BEVEL_20" result="BEVEL_30"/&gt;
</code></pre>

### Cutting Off the Extruded Part

<p><code>feComposite</code> is one of the few filter primitives that take two inputs. It then combines them by applying a method for composing two images called Porter-Duff compositing. <code>feComposite</code> can be used to mask or cut elements. Here’s how to subtract the output of <code>feMorphology</code> from the output of <code>feConvolveMatrix</code>:<p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dd36e7c-4912-4e8f-92db-8618d6be3043/12-walkthrough-03-preview-opt.jpg" alt="Cutting off the fattened 1st primitive from the extrusion" /><figcaption>Cutting off the fattened first primitive from the extrusion</figcaption></figure>

<div class="break-out">

<pre><code class="language-markup">&lt;feComposite operator="out" in="BEVEL_20" in2="BEVEL_10" result="BEVEL_30"/&gt;
</code></pre></div>

### Coloring The Extrusion

<p>This is a two-step process:</p>

<p>First, we create a colored area with <code>feFlood</code>. This primitive will simply output a rectangle the size of the filter region in a color we define:</p>

<pre><code class="language-markup">&lt;feFlood flood-color="#582D1B" result="COLOR-red" /&gt;
</code></pre>

<p>We then cut off the transparent part of <code>BEVEL_30</code> with one more <code>feComposite</code>:</p>

<figure><img title="Coloring the extrusion" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6da2da6b-f1d0-481d-b079-f320d5aa5013/13-walkthrough-04-preview-opt.jpg" alt="Coloring the extrusion" /><figcaption>Coloring the extrusion</figcaption></figure>

<div class="break-out">

<pre><code class="language-markup">&lt;feComposite in="COLOR-red" in2="BEVEL_30" operator="in" result="BEVEL_40" /&gt;
</code></pre></div>

### Mixing Bevel and Source Into One Output

<p><code>feMerge</code> does just that, mix bevel and source into one output:</p>

<figure><img title="Bevel and source graphic mixed into one output" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26e11204-e777-462c-895f-c7f780078293/14-walkthrough-05-preview-opt.jpg" alt="Bevel and source graphic mixed into one output" /><figcaption>Bevel and source graphic mixed into one output</figcaption></figure>

<pre><code class="language-markup">&lt;feMerge result="BEVEL_50"&gt;
   &lt;feMergeNode in="BEVEL_40" /&gt;
   &lt;feMergeNode in="SourceGraphic" /&gt;
&lt;/feMerge&gt;
</code></pre>

<p>Looks pretty much like the desired result. Let’s make it a little more realistic by giving it a weathered look.</p>

### Adding a Fractal Texture

<p><code>feTurbulence</code> is one of the most fun primitives to play with. However, it can melt your multicore CPU and make your fans rotate like the turbojet engines of a Boeing 747. Use it wisely, especially on a mobile device, because this primitive can have a really, really bad effect on rendering performance.</p>

<p>Like <code>feFlood</code>, <code>feTurbulence</code> outputs a filled rectangle but uses a noisy, unstructured texture.</p>

<p>We have several values on hand to alter the appearance and rhythm of the texture. This way, we can create surfaces that look like wood, sand, watercolor or cracked concrete. These settings have a direct influence on the performance of the filter, so test thoroughly. Here’s how to create a pattern that resembles paint strokes:</p>

<div class="break-out">

<pre><code class="language-markup">&lt;feTurbulence baseFrequency=".05,.004" width="200%" height="200%" top="-50%" type="fractalNoise" numOctaves="4" seed="0" result="FRACTAL-TEXTURE_10" /&gt;
</code></pre></div>

<p>By default, <code>feTurbulence</code> outputs a colored texture — not exactly what we want. We need a grayscale alpha map; a bit more contrast would be nice, too. Let’s run it through an <code>feColorMatrix</code> to increase the contrast and convert it to grayscale at the same time:</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4383f160-e32d-4ac1-a93d-6fe6e4c2bece/15-walkthrough-06-preview-opt.jpg" alt="Finally adding a fractal texture to the result" /><figcaption>Finally, adding a fractal texture to the result</figcaption></figure>

<pre><code class="language-markup">&lt;feColorMatrix type="matrix" values=
   "0 0 0 0 0,
   0 0 0 0 0,
   0 0 0 0 0,
   0 0 0 -1.2 1.1"
   in="FRACTAL-TEXTURE_10" result="FRACTAL-TEXTURE_20" /&gt;
</code></pre>

<p>The last thing to do is compose the textured alpha into the letterforms with our old friend <code>feComposite</code>:</p>

<div class="break-out">

<pre><code class="language-markup">&lt;feComposite in="BEVEL_50" in2="FRACTAL-TEXTURE_20" operator="in"/&gt;
</code></pre></div>

<p>Done!</p>

### How To Apply SVG Filters To SVG Content

<p>There are two methods of applying SVG filters to an SVG <code>text</code> element:</p>

### 1. Via CSS

<pre><code class="language-css">.filtered {
   filter: url(#filter);
}
</code></pre>

### 2. Via Attribute

<pre><code class="language-markup">&lt;text filter="url(#filter)"&gt;Some text&lt;/text&gt;
</code></pre>

### Applying SVG Filters To HTML Content

<p>One of the most exciting features of filters is that it’s possible to embed an SVG, define a filter in it and then apply it to any HTML element with CSS:</p>

<pre><code class="language-css">filter: url(#mySVGfilter);
</code></pre>

<p>At the time of writing, Blink and WebKit require it to be prefixed:</p>

<pre><code class="language-css">-webkit-filter: url(#mySVGfilter);
</code></pre>

<p>As easy as it sounds in theory, this process is a dark art in the real world:</p>

*   SVG filters on HTML content are currently supported in WebKit, Firefox and Blink. IE and Microsoft Edge will display the unfiltered element, so make sure that the default look is good enough.
*   The SVG that contains the filter may not be set to `display: none`. However, you can set it to `visibility: hidden`.
*   Sometimes the size of the SVG has a direct influence on how much of the target element is filtered.
*   Did I say that WebKit, Blink and Firefox understand this syntax? Well, Safari (and its little brother mobile Safari) is a special case. You _can_ get most of these demos working in Safari, but you will pull your hair out and bite pieces out of your desk in the process. At the time of writing, I can’t recommend using SVG filters on HTML content in the current version of Safari (8.0.6). Results are unpredictable, and the technique is not bulletproof. To make things worse, if Safari fails to render your filter for some reason, it will not display the HTML target _at all_, an accessibility nightmare. As a rule of thumb, you increase your chances of getting Safari to display your filter with absolute positioning and fixed sizing of your target. As a proof of concept, I've set up a ["pop" filter effect, optimized for desktop Safari](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a1e4885-c2f1-4e65-8a3b-54a786d165ec/pop-safari.html "POP filter effect, optimized for Safari"). Applying `feImage` to HTML elements seems to be impossible in Safari.</p>

### Previous Demos, Applied To HTML Content

<p>In these demos, the wrappers are set to <code>contenteditable = "true</code> for convenient text editing. (Be aware that these demos are experimental and will not work in Safari, IE or Edge.)</p>

*   [Image filled text](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa053e47-f0a7-48d3-ab28-b9b812624419/copperplate-html.html "outlined and filled with pattern (HTML)")
*   [Extruded and filled with pattern](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4638c73-edac-4887-a943-166a9cbedad4/extruded-html.html "Extruded and filled with pattern (HTML)")
*   [Extruded and illuminated](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9a172a4-bce6-4f8a-9395-bba5d9361bd4/3dneon-html.html "Extruded and illuminated (HTML)")
*   [Grungy look with the help of fractal filters](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/287c889a-ddfc-4d56-ae88-4c460bee4c2d/weathered-html.html "Grungy look with fractal filters (HTML)")
*   [feTurbulence to achieve spilled water effect](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14ac7e82-28ca-4762-a44b-232033759237/splash-html.html "Spilled water effect (HTML)")
*   [Some pop-arty color effects](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8daeb334-bc05-4f2a-b42f-e56769b6a18b/pop-html.html)
*   [Sketchy style](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12ec6d9c-3948-40ef-9819-cd381ed88eef/sketchy-html.html)

### Structuring A Filter

<p>Depending on its complexity, a filter can quickly become a messy thing. During authoring, you could be adding and removing rules and changing their order and values, and soon you’re lost. Here are some rules I've made for myself that help me keep track of what’s going on. People and projects vary; what seems logical and structured for me might be chaotic and incomprehensible for you, so take these recommendations with a grain of salt.</p>

### Grouping

<p>I group my filter primitives into modules depending on their functionality — for example, "border," "fill," "bevel," etc. At the start and end of a module, I put a comment with the name of this group.</p>

### Naming

<p>A good naming convention will help you structure your filter and keep track of what’s going in and outside of a primitive. After experimenting with <a title="BEM" href="https://en.bem.info/method/">BEM-like schemas</a>, I finally settled on a very simple naming structure:</p>

<pre><code class="language-markup">NAME-OF-GROUP_order-number
</code></pre>

<p>For example, you would have <code>BEVEL_10</code>, <code>BEVEL_20</code>, <code>OUTLINE_10</code> and so on. I start with 10 and increment by 10 to make it easier to change the order of primitives or to add a primitive in between or to the beginning of a group. I prefer full caps because they stand out and help me to scan the source faster.</p>

### Always Declare Input and Result

<p>Though not necessary, I always declare an "in" and a "result." (If omitted, the output of a primitive will be the input of its successor.)</p>

### Some Building Blocks

<p>Let’s look at some single techniques to achieve certain effects. By combining these building blocks, we can create new sophisticated filter effects.</p>

### Text Stroke

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/143e7301-77d3-4b99-98e0-e55f93f810fa/outline.svg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acd5d907-e2d8-4638-984d-5c601e7c74d6/16-outline-preview-opt.jpg" alt="SVG filter outline" /></a></figure>

<div class="break-out">

<pre><code class="language-markup">&lt;!-- 1. Thicken the input with feMorphology: --&gt;

&lt;feMorphology operator="dilate" radius="2" 
in="SourceAlpha" result="thickened" /&gt;

&lt;!-- 2. Cut off the SourceAlpha --&gt;

&lt;feComposite operator="out" in="SourceAlpha" in2="thickened" /&gt;
</code></pre></div>

<p>This method is not guaranteed to look good. Especially when you apply <code>dilate</code> in conjunction with big values for <code>radius</code>, the result can look worse than the geometry created via <code>stroke-width</code>. Depending on the situation, a better alternative would be to store the text in a <code>symbol</code> element, and then insert it when needed via <code>use</code>, and thicken the instance with CSS' <code>stroke-width</code> property. Be aware that <code>stroke-width</code> cannot be applied to HTML content, though.</p>

### Torn Look

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faa4becc-4a81-44ed-ac76-32c28878e31d/tornout.svg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c642f0c-4e58-49fb-b1ca-57a9896695fa/17-tornout-preview-opt.jpg" alt="Torn look" /></a></figure>

<div class="break-out">

<pre><code class="language-markup">&lt;!-- 1. create an feTurbulence fractal fill --&gt;

&lt;feTurbulence result="TURBULENCE" baseFrequency="0.08"
numOctaves="1" seed="1" /&gt;

&lt;!-- 2. create a displacement map that takes the fractal fill as an input to distort the target: --&gt;

&lt;feDisplacementMap in="SourceGraphic" in2="TURBULENCE" scale="9" /&gt;
</code></pre></div>

### Color Fill

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9328109a-8d67-47da-bed7-20f1ee4411aa/colorfill.svg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/033c24c3-28df-43e2-a0f2-adef2a19cb8b/18-colorfill-preview-opt.jpg" alt="Tornout look" /></a></figure>

<div class="break-out">

<pre><code class="language-markup">&lt;!-- 1. Create a colored filled area --&gt;

&lt;feFlood flood-color="#F79308" result="COLOR" /&gt;

&lt;!-- 2. Cut off the SourceAlpha --&gt;

&lt;feComposite operator="in" in="COLOR" in2="SourceAlpha" /&gt;
</code></pre></div>

<p>It should be mentioned that, besides <code>feFlood</code>, <code>feColorMatrix</code> is another method of altering the source input’s color, even though that concept is more difficult to grasp.</p>

### Offsetting

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79fe8c3d-9923-4f4f-838c-6b4d713d6495/offset.svg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7672c0cc-f7b9-4831-93d2-137cde36586e/19-offset-preview-opt.jpg" alt="Offsetting the filtered element" /></a></figure>

<div class="break-out">

<pre><code class="language-markup">&lt;!-- Offset the input graphic by the amount defined in its "dx" and "dy" attributes: --&gt;

&lt;feOffset in="SourceGraphic" dx="10" dy="10" /&gt;
</code></pre></div>

### Extrusion

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/940650b6-6e46-4d9a-a0fd-d4b69a4fe6ef/extrude.svg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fa514fc-1cb9-495e-8f8c-6467ac1bb9a4/20-extrude-preview-opt.jpg" alt="Extrude the target" /></a></figure>

<div class="break-out">

<pre><code class="language-markup">&lt;!-- Define a convolve matrix that applies a bevel. --&gt;

&lt;!-- Order defines the depth of the extrusion; angle is defined by the position of "1" in the matrix. Here we see a 45-degree, 4-pixel deep extrusion: --&gt;

&lt;feConvolveMatrix order="4,4" 
   kernelMatrix="
   1 0 0 0
   0 1 0 0
   0 0 1 0 
   0 0 0 1" in="SourceAlpha" result="BEVEL" /&gt;

&lt;!-- offset extrusion: --&gt;

&lt;feOffset dx="2" dy ="2" in="BEVEL" result="OFFSET" /&gt;

&lt;!-- merge offset with Source: --&gt;

&lt;feMerge&gt;
   &lt;feMergeNode in="OFFSET" /&gt;
   &lt;feMergeNode in="SourceGraphic" /&gt;
&lt;/feMerge&gt;
</code></pre></div>

### Noise Fill

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/508996d2-f6f3-4292-b5a4-fb03280e8be0/noisefill.svg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c895c012-3192-4541-8143-dc59213b03a9/21-noisefill-preview-opt.jpg" alt="Create a noise fill" /></a></figure>

<p>The <code>feTurbulence</code> filter primitive will create a noisy texture by applying the so-called Perlin noise algorithm (invented by Ken Perlin during his work on TRON in 1981). This will generate a rectangle filled with noise that looks like what you could see on old TV sets late at night before cable TV was invented.</p>

<p>The appearance of the noise structure can be modified by several parameters:</p>

*   `type` in its default state will produce a liquid texture.
*   `type` can be set to `fractalNoise` instead, which will output a sandy result.
*   `baseFrequency` is there to control x and y pattern repetition.
*   `numOctaves` will increase the level of detail and should have a low value if performance is an issue.
*   The number to start randomization with is determined by `seed`.</p>

<div class="break-out">

<pre><code class="language-markup">&lt;feTurbulence type="fractalNoise" baseFrequency="0.1" numOctaves="5" seed="2" /&gt;
</code></pre></div>

### Image Fill

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50cc74d4-408a-43fd-ae6e-67ada6b103cf/imagefill.svg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b782c613-278b-4023-9b53-bcf284218a15/22-imagefill-preview-opt.jpg" alt="Fill target with an image" /></a></figure>

<p><code>feImage</code>’s purpose is to fill the target with a texture. If we want to apply a repeating pattern, it must be used in conjunction with <code>feTile</code>.</p>

<div class="break-out">

<pre><code class="language-markup">&lt;!-- The following code will create a 100 × 200-pixel square filled with "myfill.svg": --&gt;

&lt;feImage xlink:href="myfill.svg" x="0" y="0" width="100" height="200" result="IMAGEFILL"/&gt;

&lt;!-- We then use this fill as an input for feTile, creating a repeating pattern this way: --&gt;

&lt;feTile in="IMAGEFILL" resulte="TILEPATTERN"/&gt;

&lt;!-- Now we will use feComposite to "cut off" SourceAlpha’s transparent areas from the fill: --&gt;

&lt;feComposite operator="in" in="TILEPATTERN" in2="SourceAlpha" /&gt;
</code></pre></div>

<p>The cool thing about this filter is that the specification allows us to use any SVG element as an input and to create a pattern fill from it. So, in theory, you could create pattern fills from symbols, groups and fragments within your SVG and then apply them as a texture, even to HTML elements. Unfortunately, because of an <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=455986">old bug</a>, Firefox accepts only external resources as input. If you prefer to keep things self-contained and want to avoid the additional HTTP request, there’s hope: Embed the pattern fill as an UTF-8 data URI:</p>

<div class="break-out">

<pre><code class="language-markup">&lt;feImage xlink:href='data:image/svg+xml;charset=utf-8,&lt;svg width="100" height="100"&gt;&lt;rect width="50" height="50 /&gt;&lt;/svg&gt;' /&gt;
</code></pre></div>

<p>Some browsers do not understand UTF-8 data URIs when they aren’t URL-encoded, so make <a title="Eric Meyer’s URL encoder" href="https://meyerweb.com/eric/tools/dencoder/">URL encoding</a> a default:</p>

<div class="break-out">

<pre><code class="language-markup">&lt;feImage xlink:href='data:image/svg+xml;charset=utf-8,%3Csvg%20width%3D%22100%22%20height%3D%22100%22%3E%3Crect%20width%3D%2250%22%20height%3D%2250%20%2F%3E%3C%2Fsvg%3E' /&gt;
</code></pre></div>

<p>If you want to apply <code>feImage</code> to HTML content, be aware that size matters. The SVG that contains the filter must cover the area where it is being applied. The easiest way to achieve this is by making it an absolutely positioned child within the block element it is being applied to:</p>

<pre><code class="language-markup">&lt;style&gt;
  h1{
    position: relative;
    filter: url(#myImageFilter);
  }
  h1 svg{
    position: absolute;
    visibility: hidden;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
  }
&lt;/style&gt;
&lt;h1&gt;
  My Filtered Text
  &lt;svg&gt;
    &lt;filter id="myImageFilter"&gt;…&lt;/filter&gt;
  &lt;/svg&gt;
&lt;/h1&gt;
</code></pre>

### Lighting Effect

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c32d2216-c57c-40fa-9790-e85a37a936a7/lighting.svg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4515dd8-c98b-4f3e-98a0-b9b02b6debd8/23-lighting-preview-opt.jpg" alt="3D Bevel" /></a></figure>

<p>This is one "Wow" effect that quickly becomes boring when used too often. This filter has a serious effect on performance, so use it wisely.</p>

<pre><code class="language-markup">&lt;!--We create a heightmap by blurring the source: --&gt;

&lt;feGaussianBlur stdDeviation="5" in="SourceAlpha" result="BLUR"/&gt;

&lt;!-- We then define a lighting effect with a point light that is positioned at virtual 3D coordinates x: 40px, y: -30px, z: 200px: --&gt;

&lt;feSpecularLighting surfaceScale="6" specularConstant="1" specularExponent="30" lighting-color="#white" in="BLUR" result="SPECULAR"&gt;
    &lt;fePointLight x="40" y="-30" z="200" /&gt;
&lt;/feSpecularLighting&gt;

&lt;!-- We cut off the parts that overlap the source graphic… --&gt;

&lt;feComposite operator="in" in="SPECULAR" in2="SourceAlpha" result="COMPOSITE"/&gt;

&lt;!-- … and then merge source graphic and lighting effect: --&gt;

&lt;feMerge&gt;
    &lt;feMergeNode in="SourceGraphic" /&gt;
    &lt;feMergeNode in="COMPOSITE"/&gt;
&lt;/feMerge&gt;
</code></pre>

### Conclusion

<p>There is a gap between pure CSS layout and custom design elements created in software such as Photoshop or Illustrator. External assets embedded as background images, icon sprites and SVG symbols will always have their place in the design of websites. But sophisticated SVG filters give us more independence from third-party design tools and bridge this gap by enabling us to create visual styles directly in the browser.</p>

<p>In this article we've seen how SVG filters help us to create playful, decorative web typography. But nothing says we have to stop here. Soon, browser support will be good enough for us to use these effects on every HTML element as easily as we use CSS today. Even though the effects behave differently from native CSS techniques (an SVG filter will affect not only an element but all its children), it will be exciting to see how inventive web designers use these techniques in the near future.</p>

### Resources From This Article

*   [Sophisticated Filter Effects](https://github.com/dirkweber/svg-filter-typeeffects "Repo with demos at GitHub"), GitHub The repository of demos
*   [Sophisticated Filter Effects](https://codepen.io/collection/ArxmyO/ "Play with code on Codepen"), Codepen Play around with the code.</p>

### Reading List

*   "[Filter Effects Module Level 1](https://www.w3.org/TR/filter-effects/ "W3C Filter Effects Module Level 1")" (working draft), W3C
*   "[SVG Filters](https://docs.webplatform.org/wiki/svg/tutorials/smarter_svg_filters "Smarter SVG Filters at webplatform.org")," Mike Sierra, WebPlatform.org
*   "[Filter Effects in SVG](https://srufaculty.sru.edu/david.dailey/svg/SVGOpen2010/filters2.htm "Filter Effects in SVG")," David Dailey
*   "[SVG Filters](https://tutorials.jenkov.com/svg/filters.html "Filter Tutorial by Jakob Jenkov")" (tutorial), Jakob Jenkov
*   "[Filter Primitives Overview](https://pythonhosted.org/svgwrite/classes/filter_primitive.html "Filter Primitives Overview")," Manfred Moitzi
*   "[Using Filters to Add Raster Images](https://www.svgbasics.com/filters1.html "SVGBasics: Filters")," SVGBasics
*   "[Filters](https://apike.ca/prog_svg_filters.html "Filters by Matthew Bystedt")," Matthew Bystedt
*   "[Cirque du Filter: A Journey Into Advanced SVG Filter Effects](https://de.slideshare.net/mullany1/cirque-du-filter-cssdevconf-2013 "Cirque du Filter")" (slidedeck), Michael Mullany, CSS Dev Conf 2013
*   "[How to Go Beyond the Basics With SVG Filters](https://www.creativebloq.com/netmag/how-go-beyond-basics-svg-filters-71412280 "How to go beyond the basics with SVG filters")," Michael Mullany, Creative Bloq
*   "[Porter/Duff Compositing and Blend Modes](https://ssp.impulsetrain.com/porterduff.html "Porter/Duff Compositing and Blend Modes")," Søren Sandmann Pedersen
*   "[Matrix Operations for Image Processing](https://graficaobscura.com/matrix/index.html "Matrix Operations for Image Processing")," Paul Haeberli
*   "[Image Processing Using 2D-Convolution](https://williamson-labs.com/convolution-2d.htm "Image Processing using 2D-Convolution")," Williamson Labs
*   "[3×3 Convolution Kernels With Online Demo](https://matlabtricks.com/post-5/3x3-convolution-kernels-with-online-demo#demo "3x3 convolution kernels")," Zoltán Fegyver
*   "The Perlin Noise Math FAQ," Matt Zucker
*   "[A Look at SVG Light Source Filters](https://css-tricks.com/look-svg-light-source-filters/ "SVG Light Source Filters")," Joni Trythall, CSS-Tricks

{{< signature "ds, al, il" >}}

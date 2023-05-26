---
title: Animating Clipped Elements In SVG
slug: animating-clipped-elements-svg
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2223d0e8-cf8e-465f-8e12-b67ee6bc2899/excerpt-shredder-opt.png
date: 2015-12-16T21:39:45.000Z
author: dennisgaebeljr
description: >-
  Scalable Vector Graphics (or SVG) lend developers an incredible ability to
  display crisp, beautiful graphics at any size or resolution. SVG can also be
  animated using various techniques. In combination with clipping paths,
  interesting effects can be achieved.

  This article **explains the difference between an SVG** `clipPath` **and a
  CSS** `clip-path`, including examples to guide and inform you through this
  journey. Finally, I’ll share a few demos both personal and in the wild to help
  you better understand `clipPath` animation and inspire your visions.
categories:
  - Coding
  - Animation
  - SVG
  - Responsive Images
---
Scalable Vector Graphics (or SVG) lend developers an incredible ability to display crisp, beautiful graphics at any size or resolution. SVG can also be animated using various techniques. In combination with clipping paths, interesting effects can be achieved.

This article **explains the difference between an SVG `clipPath` and a CSS `clip-path`**, including examples to guide and inform you through this journey. Finally, I’ll share a few demos both personal and in the wild to help you better understand `clipPath` animation and inspire your visions.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Rethinking Responsive SVG](https://www.smashingmagazine.com/2014/03/rethinking-responsive-svg/)
*   [A Few Different Ways To Use SVG Sprites In Animation](https://www.smashingmagazine.com/2015/03/different-ways-to-use-svg-sprites-in-animation/)
*   [Creating Cel Animations With SVG](https://www.smashingmagazine.com/2015/09/creating-cel-animations-with-svg/)
*   [The Guide To CSS Animation: Principles and Examples](https://www.smashingmagazine.com/2011/09/the-guide-to-css-animation-principles-and-examples/)

## Clipping Facts

When only a portion of an object is visible through a bounding area, we call that a clipping mask. In other words, we get a clipping mask when a portion of a selected surface is “cut out,” making any objects that sit within the bounded region visible to the viewer. Any parts that lie outside of the region are invisible.

{{% feature-panel %}}

Think of a clipping path — CSS or SVG — as a custom viewport, like the porthole of a submarine. Clipping paths can also be considered a special type of mask, [according to the W3C](https://www.w3.org/TR/SVG/masking.html#ClippingPaths)’s “Clipping, Masking and Compositing” specification:

<blockquote>
<p>The clipping path restricts the region to which paint can be applied. Conceptually, any parts of the drawing that lie outside of the region bounded by the currently active clipping path are not drawn. A clipping path can be thought of as a mask wherein those pixels outside the clipping path are black with an alpha value of zero and those pixels inside the clipping path are white with an alpha value of one (with the possible exception of anti-aliasing along the edge of the silhouette).</p>
</blockquote>

If you’re curious how events transpire in an SVG with a `clipPath`, the following diagram depicts how an SVG `clipPath` is structured:

<figure><br>
<svg version="1.1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" viewBox="0 0 337 337"><circle fill="#F0F5F9" cx="168.5" cy="168.5" r="110"></circle><path opacity="0.64" fill="#EF4A35" d="M0,0v337h337V0H0z M168.5,223.3c-30.3,0-54.8-24.5-54.8-54.8c0-30.3,24.5-54.8,54.8-54.8 s54.8,24.5,54.8,54.8C223.3,198.8,198.8,223.3,168.5,223.3z"></path><polygon fill="none" stroke="#000000" stroke-miterlimit="10" points="168,169.5 223,169.5 278,169.5 "></polygon></svg><figcaption>The white portion &mdash; the clip path region &mdash; is clickable to the user, whereas the red portion is not. The black line represents the radius.</figcaption><br>
</figure>

Clipped content requiring interaction, such as event-driven data, operates according to the “[Clipping Paths, Geometry, and Pointer Events](https://www.w3.org/TR/SVG/masking.html#clipPath-geometry)” section of the specification:

<blockquote>
<p>By default, pointer-events must not be dispatched on the clipped (non-visible) regions of a shape. For example, a circle with a radius of 10 which is clipped to a circle with a radius of 5 will not receive “click” events outside the smaller radius.</p>
</blockquote>

## CSS Clip Path

The difference between an [SVG `clipPath`](https://dev.w3.org/fxtf/css-masking-1/#elementdef-clippath) and a [CSS `clip-path`](https://dev.w3.org/fxtf/css-masking-1/#the-clip-path) is important. The latter defines a specific region of an element to display. This is all done within a style sheet.</p>

<pre><code class="language-css">.target-element {
  clip-path: inset(10px 20px 30px 40px);
}
</code></pre>

The values in the bounding parentheses are read as “from top, from right, from bottom, from left.” These values define the clipping shape of the corresponding element.

Of course, we could implement far more intricate clipping patterns using a variety of shapes as our template. For instance, we could clip using an external SVG `clipPath`, referred to by a unique identifier (ID) or a polygon specified as a series of points.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49bcd915-050a-4381-ad62-4315f24cab5d/01-clippy-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf652a6f-7e79-423e-af47-20b15138b501/01-clippy-opt-preview.png" alt="“Clippy”, the in-browser tool that allows developers to visually explore CSS clipping paths" /></a><figcaption>“Clippy”, the in-browser tool that allows developers to visually explore CSS clipping paths. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49bcd915-050a-4381-ad62-4315f24cab5d/01-clippy-opt.png">View large version</a>)</figcaption></figure>

If you want a visual guide, Bennett Feely has made a highly educational and interactive tool, called [Clippy](https://bennettfeely.com/clippy), that allows developers to explore different clipping shapes in the browser.

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;body&gt;
  &lt;svg xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" version="1.1"&gt;
    &lt;clipPath id="#inline-svg-clipPath"&gt;
      &lt;circle cx="150" cy="150" r="50" /&gt;
    &lt;/clipPath&gt;
  &lt;/svg&gt;

  &lt;div class="clipped-element"&gt;&lt;/div&gt;
 &lt;/body&gt;
&lt;/html&gt;
</code></pre>

Below is a list of possible variations using the `clip-path` property in CSS. The first code block represents an SVG located inline with the markup and referred to via an external style sheet. Uncomment each variation to view the result of that approach.</p>

<pre><code class="language-css">.clipped-element {
  width: 100px;
  height: 100px;
  background: black;

  /* Refers to the inline SVG clipPath element above */
  clip-path: url(#inline-svg-clipPath);

  /* Refers to an external SVG using the same contents of the inline SVG above. */
  /*clip-path: url(path/to/image.svg#inline-svg-clipPath);*/

  /* CSS polygon clip-path */
  /*clip-path: polygon(45% 15%, 100% 0%, 100% 75%, 75% 75%, 75% 100%, 50% 75%, 0% 75%); */

  /* CSS circle clip-path */
  /* clip-path: circle(30px at 35px 35px); */

  /* CSS ellipse clip-path */
  /*clip-path: ellipse(65px 30px at 125px 40px);*/
 }
</code></pre>

## SVG Mask Vs. SVG clipPath

<figure>
  <p data-height="350" data-theme-id="0" data-slug-hash="xGMYJY" data-default-tab="result" data-user="dennisgaebel" class="codepen">See the Pen <a href="https://codepen.io/dennisgaebel/pen/xGMYJY/">SVG Mask</a> by Dennis Gaebel (<a href="https://codepen.io/dennisgaebel">@dennisgaebel</a>) on <a href="https://codepen.io">CodePen</a>.</p><figcaption>This is how an SVG mask works using the <code>&lt;text&gt;</code> and <code>&lt;linearGradient&gt;</code> SVG elements, along with a touch of animation for the sweeping effect.</figcaption><br>
</figure>

Just so we don’t confuse an SVG `mask` with an SVG `clipPath`, let’s examine what an SVG `mask` is and how it differs from a `clipPath`. I like to think of masks as a way to accept the visible region already defined by an object’s shape — as if you were to cover an object with a blanket and define the visible region by the object’s shape pressed into this blanket — whereas a clipping path defines the _shape_, not the object. In the latter case, the object would be covered with a blanket, with the visible region already defined, instead of the visible region being inherited from the object. An SVG mask is [defined in the specification](https://www.w3.org/TR/SVG/masking.html#Masking) as follows:

<blockquote>
<p>A “mask” can contain any graphical elements or container elements such as a “g.” […]</p>

<p>Any graphical object which uses/references the given “mask” element will be painted onto the background through the mask, thus completely or partially masking out parts of the graphical object.</p>
</blockquote>

If you’re still pondering what a mask looks like and the mechanics thereof, let’s start with the XML tag:

<pre><code class="language-markup">&lt;mask&gt;&lt;/mask&gt;
</code></pre>

The `mask` element accepts quite a few attributes that take some getting used to, such as `maskUnits`. If you’re curious about the attributes, refer to the [specification](https://www.w3.org/TR/SVG/masking.html#Masking).

Much like a `clipPath`, a `mask` may be reused multiple times, as long as it has been defined in the definitions, `defs`.</p>

<pre><code class="language-markup">&lt;defs&gt;
  &lt;mask id="mask"&gt;
    &lt;rect width="800" height="300" fill="url(#gradient)"/&gt;
  &lt;/mask&gt;
 &lt;/defs&gt;
</code></pre>

As the specification states, “A mask can accept a graphical object.” In this case, a rectangle meets this requirement. The mask’s rectangle has also been filled with a linear gradient.</p>

<pre><code class="language-markup">&lt;use xlink:href="#txt" mask="url(#mask)"/&gt;
</code></pre>

The final steps are to reference this mask using the `mask` attribute and to pass the ID of `mask` within `defs` to the attribute’s `url()` method, which retrieves this `mask` with the corresponding ID. The `use` element allows for portability, which might be familiar to those of you who use SVG icon sprites.</p>

<pre><code class="language-markup">&lt;defs&gt;
  &lt;linearGradient gradientTransform="translate(10)"&gt;…&lt;/linearGradient&gt;
&lt;/defs&gt;
</code></pre>

There are some really crafty ways to animate linear gradients in SVG using the `gradientTransform` attribute. This attribute accepts many `transform` values, including `translate()`, `scale()`, `rotate()` and `matrix()`. If you’d like to dive deeper, the specification lists [all of the accepted values](https://www.w3.org/TR/SVG/pservers.html#LinearGradientElementGradientTransformAttribute).

The `gradientTransform` example shows how values can be passed using the `transform` syntax that you are familiar with.

The gradient’s motion is accomplished through the use of the GreenSock Animation Platform, which manipulates the attribute. The entire discussion surrounding how to animate the gradient is best left for another time, but the demo provides plenty of clues, should you be curious.

## Spinning Globe

<figure><p data-height="370" data-theme-id="0" data-slug-hash="aOXJep" data-default-tab="result" data-user="dennisgaebel" class="codepen">See the Pen <a href="https://codepen.io/dennisgaebel/pen/aOXJep/">Animated SVG clipPath</a> by Dennis Gaebel (<a href="https://codepen.io/dennisgaebel">@dennisgaebel</a>) on <a href="https://codepen.io">CodePen</a>.</p><figcaption>Animated SVG <code>clipPath</code> lending motion to the globe.</figcaption>
</figure>

A clipping path placed strategically over the globe creates the illusion of a sphere spinning 360 degrees when, in fact, it’s two identical paths. These paths (i.e. the map) are moved along the x axis in tandem. Finally, the entire sequence is repeated. An inline SVG clip path — the ellipse — is used to hide the parts of the map that lie outside the view of the globe.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dc57469-ff52-433f-87f6-1e4b7083db42/02-globemapclip-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65a8bee4-0d66-4ac1-b96a-2ca49ac51629/02-globemapclip-opt-preview.png" alt="Exposing the SVG paths when the clipping mask is removed in Illustrator" /></a><figcaption>Exposing the SVG paths when the clipping mask is removed in Illustrator. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dc57469-ff52-433f-87f6-1e4b7083db42/02-globemapclip-opt.png">View large version</a>)</figcaption></figure>

Resting in the `defs` of the SVG is the clipping shape (i.e. ellipse). Directly beneath it is the reference that turns this ellipse into a reusable clipping path. You can also think of it as a reusable symbol.

The `defs` element allows graphical objects to be defined for reuse. When possible, define referenced elements inside this element. Defining graphic visuals such as linear gradients and animations inside these elements promotes both [understanding of the SVG content and accessibility](https://www.w3.org/TR/SVG/struct.html).

Because the clipping path defined in `defs` has an ID, it can be referred to with the `use` element to render these graphical effects anywhere. A clipping path is referred to using the `clip-path` attribute, as follows:

<pre><code class="language-markup">&lt;svg version="1.1" xmlns:xlink="https://www.w3.org/1999/xlink" viewBox="0 0 484.4 261.7"&gt;
    &lt;defs&gt;
    &lt;ellipse id="ellipseClip" cx="239.7" cy="139.2" rx="65" ry="62.5"/&gt;
        &lt;clipPath id="clipPathId"&gt;
      &lt;use xlink:href="#ellipseClip" overflow="visible"/&gt;
    &lt;/clipPath&gt;
    &lt;/defs&gt;

  &lt;g id="globe"&gt;
    &lt;use xlink:href="#ellipseClip" fill="#A4CAE1" overflow="visible"/&gt;
      &lt;g id="middle" clip-path="url(#clipPathId)"&gt;…&lt;/g&gt;
    &lt;g id="left" clip-path="url(#clipPath)"&gt;…&lt;/g&gt;
  &lt;/g&gt;
&lt;/svg&gt;
</code></pre>

In this case, the `use` element is used multiple times, making this technique one of the best parts about SVG. Any graphical elements defined inside `defs` are not directly rendered and can be saved for reuse at another time. The `use` element takes nodes from within the SVG document and duplicates them elsewhere.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2018997-5419-4bd4-849a-52cb38bfeb2a/03-highlighted-clippath-opt.png" alt="A static image that depicts each area used in the demo to make the effect come to life" /><figcaption>A static image that depicts each area used in the demo to make the effect come to life.</figcaption></figure>

I’ve highlighted each part of the SVG where the clipping path occurs. The clip path is an ellipse where the content (in this case, the map of the continents) is clipped into the ellipse shape (the globe). I’ve also included a duplicate map off to the left of the initially visible map, to make this spinning sequence appear as if it is rotating seamlessly.</p>

{{< vimeo id="148883692" caption="Inspect the animation using developer tools to visualize how each path moves from left to right. Use full-screen mode for an enlarged view." >}}

To see this effect for yourself, follow the steps detailed in the video above:

1.  Open Chrome.
2.  Load the [Codepen page](https://codepen.io/dennisgaebel/pen/aOXJep).
3.  Right-click on the globe, then select “Inspect Element.”
4.  In the “Elements” tab of the Developer Tools, find the element `id="continents"` and expand it.
5.  For each of the elements `id="middle"` and `id="left"`, double-click on the code `clip-path="url(#clipPath)"`, select it completely, backspace, then enter.
6.  Now, on the page, watch the two sets of continents move.

Using the [GreenSock Animation Platform](https://greensock.com/gsap) to control the motion and some minor timing adjustments, we can make the globe appear to spin 360 degrees seamlessly.

If you’ve never heard of it, the GreenSock Animation Platform (called GSAP by avid users) is a suite of tools for scripted animation written in JavaScript. [Sarah Drasner](https://davidwalsh.name/gsap-svg) and [Dennis Gaebel](https://webdesign.tutsplus.com/series/the-beginners-guide-to-timelinemax--cms-765) each offer a great series on it for the eager beginner.

If you’re curious how to create a `clipPath` in Illustrator, follow these steps:

1.  Make a shape with the Marquee or Pen tool.
2.  Place an object below the shape.
3.  Right-click the object, and select “Make clipping mask.”

## Folding Fan

See the Pen [Folding Fan](https://codepen.io/dennisgaebel/pen/gpqWRq/) by Dennis Gaebel ([@dennisgaebel](https://codepen.io/dennisgaebel)) on [CodePen](https://codepen.io).

To better understand `clipPath`, let’s examine this SVG fan by [Thoughtbot](https://thoughtbot.github.io/foundry), who has thoroughly cleaned and customized it by hand and strategically placed `clipPath` to identify and animate the visible region.</p>

<figure><br>
<svg xmlns="https://www.w3.org/2000/svg" viewBox="0 0 511.8 512.1"><path id="XMLID_262_" d="M0 0h511.8v512.1H0z" style="opacity:0.37;fill:#5D5D5D;" /><path id="XMLID_261_" d="M220.4 110l-61.2 221.9 237.7 1.3z" style="fill:#8F7FA0;" /><g id="XMLID_204_"><path id="XMLID_259_" d="M136.8 422.1l4.8 14.3 4.8-14.3h2.5l-6.1 16.8h-2.4l-6.1-16.8h2.5z"/><path id="XMLID_256_" d="M150.4 422.1h2.1v2.3h-2.1v-2.3zm0 4.6h2.1v12.2h-2.1v-12.2z"/><path id="XMLID_254_" d="M156.8 435c.1.7.2 1.2.5 1.6.5.7 1.4 1 2.8 1 .8 0 1.5-.2 2.1-.5.6-.3.9-.8.9-1.5 0-.5-.2-.9-.7-1.2-.3-.2-.9-.4-1.8-.6l-1.7-.4c-1.1-.3-1.8-.5-2.3-.9-.9-.6-1.3-1.3-1.3-2.3 0-1.2.4-2.1 1.3-2.8s2-1.1 3.4-1.1c1.9 0 3.2.5 4 1.6.5.7.8 1.4.8 2.2h-1.9c0-.5-.2-.9-.5-1.3-.5-.5-1.3-.8-2.5-.8-.8 0-1.4.1-1.8.4s-.6.7-.6 1.2.3 1 .8 1.3c.3.2.8.4 1.4.5l1.4.3c1.5.4 2.5.7 3 1 .8.5 1.2 1.4 1.2 2.5s-.4 2-1.3 2.8c-.8.8-2.1 1.2-3.8 1.2-1.8 0-3.1-.4-3.9-1.2s-1.2-1.8-1.2-3.1h1.7z"/><path id="XMLID_251_" d="M167.3 422.1h2.1v2.3h-2.1v-2.3zm0 4.6h2.1v12.2h-2.1v-12.2z"/><path id="XMLID_248_" d="M172.3 422h2v6.1c.5-.6 1-1 1.6-1.3.6-.3 1.3-.5 2-.5 1.5 0 2.8.5 3.7 1.6s1.4 2.6 1.4 4.6c0 1.9-.5 3.5-1.4 4.8-.9 1.3-2.2 1.9-3.9 1.9-.9 0-1.7-.2-2.4-.7-.4-.3-.8-.7-1.2-1.3v1.6h-1.9V422zm7.9 14.1c.6-.9.8-2 .8-3.5 0-1.3-.3-2.4-.8-3.2-.6-.8-1.4-1.3-2.4-1.3-.9 0-1.8.3-2.5 1s-1.1 1.8-1.1 3.4c0 1.1.1 2.1.4 2.8.5 1.3 1.6 2 3 2 1.2.1 2-.3 2.6-1.2z"/><path id="XMLID_246_" d="M185.5 422.1h2.1v16.8h-2.1v-16.8z"/><path id="XMLID_243_" d="M198.2 427c.8.4 1.4.9 1.9 1.6.4.6.7 1.3.8 2.2.1.6.2 1.5.2 2.7h-8.9c0 1.2.3 2.2.9 3s1.4 1.1 2.5 1.1 1.9-.4 2.5-1.1c.4-.4.6-.9.8-1.4h2c-.1.4-.2.9-.5 1.5s-.6 1-1 1.4c-.6.6-1.4 1-2.3 1.2-.5.1-1 .2-1.7.2-1.5 0-2.8-.6-3.8-1.7-1.1-1.1-1.6-2.7-1.6-4.7s.5-3.6 1.6-4.8c1.1-1.2 2.4-1.8 4.2-1.8.8 0 1.6.2 2.4.6zm.8 4.8c-.1-.9-.3-1.6-.6-2.1-.6-1-1.5-1.5-2.8-1.5-.9 0-1.7.3-2.4 1s-1 1.5-1 2.6h6.8z"/><path id="XMLID_241_" d="M222.3 423.3c1.2 1.1 1.8 2.4 1.9 3.8H222c-.2-1.1-.7-1.9-1.5-2.6-.7-.6-1.8-.9-3.1-.9-1.6 0-2.9.6-3.9 1.7-1 1.2-1.5 2.9-1.5 5.3 0 2 .5 3.6 1.4 4.8.9 1.2 2.2 1.8 4 1.8 1.6 0 2.9-.6 3.8-1.9.5-.7.8-1.6 1-2.7h2.2c-.2 1.8-.8 3.2-1.9 4.4-1.3 1.4-3.1 2.2-5.3 2.2-1.9 0-3.5-.6-4.9-1.8-1.7-1.6-2.6-4-2.6-7.2 0-2.5.6-4.5 1.9-6.1 1.4-1.7 3.3-2.6 5.8-2.6 2.1.1 3.8.7 4.9 1.8z"/><path id="XMLID_239_" d="M227.1 422.1h2.1v16.8h-2.1v-16.8z"/><path id="XMLID_236_" d="M232.3 422.1h2.1v2.3h-2.1v-2.3zm0 4.6h2.1v12.2h-2.1v-12.2z"/><path id="XMLID_233_" d="M237.3 426.7h2v1.6c.4-.6.9-1 1.4-1.3.7-.5 1.5-.7 2.5-.7 1.4 0 2.6.5 3.5 1.6 1 1.1 1.5 2.6 1.5 4.6 0 2.7-.7 4.6-2.1 5.7-.9.7-1.9 1.1-3.1 1.1-.9 0-1.7-.2-2.3-.6-.4-.2-.8-.6-1.2-1.2v6.2h-2.1v-17zm7.7 9.6c.6-.8 1-2 1-3.6 0-1-.1-1.8-.4-2.5-.5-1.3-1.5-2-2.9-2s-2.4.7-2.9 2.1c-.3.8-.4 1.7-.4 2.9 0 .9.1 1.7.4 2.4.5 1.3 1.5 1.9 2.9 1.9.9 0 1.7-.4 2.3-1.2z"/><path id="XMLID_230_" d="M250.3 426.7h2v1.6c.4-.6.9-1 1.4-1.3.7-.5 1.5-.7 2.5-.7 1.4 0 2.6.5 3.5 1.6 1 1.1 1.5 2.6 1.5 4.6 0 2.7-.7 4.6-2.1 5.7-.9.7-1.9 1.1-3.1 1.1-.9 0-1.7-.2-2.3-.6-.4-.2-.8-.6-1.2-1.2v6.2h-2.1v-17zm7.7 9.6c.6-.8 1-2 1-3.6 0-1-.1-1.8-.4-2.5-.5-1.3-1.5-2-2.9-2s-2.4.7-2.9 2.1c-.3.8-.4 1.7-.4 2.9 0 .9.1 1.7.4 2.4.5 1.3 1.5 1.9 2.9 1.9.9 0 1.7-.4 2.3-1.2z"/><path id="XMLID_227_" d="M263.5 422.1h2.1v2.3h-2.1v-2.3zm0 4.6h2.1v12.2h-2.1v-12.2z"/><path id="XMLID_225_" d="M268.7 426.6h2v1.7c.6-.7 1.2-1.2 1.8-1.5.6-.3 1.4-.5 2.2-.5 1.7 0 2.9.6 3.5 1.8.3.7.5 1.6.5 2.8v7.8h-2.1V431c0-.7-.1-1.3-.3-1.8-.4-.8-1-1.1-2-1.1-.5 0-.9 0-1.2.1-.6.2-1.1.5-1.5 1-.3.4-.6.8-.7 1.2-.1.4-.2 1-.2 1.8v6.4h-2.1v-12z"/><path id="XMLID_222_" d="M288.5 427.1c.4.3.8.7 1.2 1.2v-1.5h1.9v11.1c0 1.6-.2 2.8-.7 3.7-.8 1.7-2.5 2.5-4.8 2.5-1.3 0-2.4-.3-3.3-.9s-1.4-1.5-1.5-2.8h2.1c.1.5.3 1 .6 1.3.5.5 1.2.7 2.2.7 1.6 0 2.6-.6 3.1-1.7.3-.7.4-1.8.4-3.5-.4.6-.9 1.1-1.5 1.4-.6.3-1.3.5-2.3.5-1.3 0-2.5-.5-3.5-1.4-1-.9-1.5-2.5-1.5-4.7 0-2 .5-3.6 1.5-4.8 1-1.1 2.2-1.7 3.6-1.7 1-.1 1.8.2 2.5.6zm.2 2.2c-.6-.7-1.4-1.1-2.4-1.1-1.4 0-2.4.7-3 2 .3.7-.4 1.7-.4 2.8 0 1.4.3 2.4.8 3.1s1.3 1.1 2.2 1.1c1.5 0 2.5-.7 3.1-2 .3-.8.5-1.6.5-2.6.2-1.4-.1-2.5-.8-3.3z"/><path id="XMLID_219_" d="M301.8 422.1h7.6c1.3 0 2.3.2 3.1.6 1.5.7 2.3 2 2.3 4 0 1-.2 1.8-.6 2.5s-1 1.2-1.7 1.5c.7.3 1.1.6 1.5 1.1.3.4.5 1.1.6 2.1l.1 2.2c0 .6.1 1.1.2 1.4.1.5.4.9.7 1v.4h-2.8c-.1-.1-.1-.3-.2-.6s-.1-.7-.1-1.3l-.1-2.8c-.1-1.1-.4-1.8-1.2-2.2-.4-.2-1.1-.3-2-.3h-5v7.2h-2.3v-16.8zm7.3 7.7c1 0 1.9-.2 2.5-.6.6-.4.9-1.2.9-2.3 0-1.2-.4-2-1.3-2.4-.5-.2-1.1-.3-1.8-.3H304v5.7h5.1z"/><path id="XMLID_216_" d="M325.7 427c.8.4 1.4.9 1.8 1.6.4.6.7 1.3.8 2.2.1.6.2 1.5.2 2.7h-8.9c0 1.2.3 2.2.9 3s1.4 1.1 2.5 1.1 1.9-.4 2.5-1.1c.4-.4.6-.9.8-1.4h2c-.1.4-.2.9-.5 1.5s-.6 1-1 1.4c-.6.6-1.4 1-2.3 1.2-.5.1-1 .2-1.7.2-1.5 0-2.8-.6-3.8-1.7s-1.6-2.7-1.6-4.7.5-3.6 1.6-4.8c1.1-1.2 2.4-1.8 4.2-1.8.8 0 1.6.2 2.5.6zm.7 4.8c-.1-.9-.3-1.6-.6-2.1-.6-1-1.5-1.5-2.8-1.5-.9 0-1.7.3-2.4 1-.6.7-1 1.5-1 2.6h6.8z"/><path id="XMLID_213_" d="M337.9 427.1c.4.3.8.7 1.2 1.2v-1.5h1.9v11.1c0 1.6-.2 2.8-.7 3.7-.8 1.7-2.5 2.5-4.8 2.5-1.3 0-2.4-.3-3.3-.9s-1.4-1.5-1.5-2.8h2.1c.1.5.3 1 .6 1.3.5.5 1.2.7 2.2.7 1.6 0 2.6-.6 3.1-1.7.3-.7.4-1.8.4-3.5-.4.6-.9 1.1-1.5 1.4-.6.3-1.3.5-2.3.5-1.3 0-2.5-.5-3.5-1.4-1-.9-1.5-2.5-1.5-4.7 0-2 .5-3.6 1.5-4.8 1-1.1 2.2-1.7 3.6-1.7 1-.1 1.8.2 2.5.6zm.3 2.2c-.6-.7-1.4-1.1-2.4-1.1-1.4 0-2.4.7-3 2-.3.7-.4 1.7-.4 2.8 0 1.4.3 2.4.8 3.1s1.3 1.1 2.2 1.1c1.5 0 2.5-.7 3.1-2 .3-.8.5-1.6.5-2.6.1-1.4-.2-2.5-.8-3.3z"/><path id="XMLID_210_" d="M344.1 422.1h2.1v2.3h-2.1v-2.3zm0 4.6h2.1v12.2h-2.1v-12.2z"/><path id="XMLID_207_" d="M358.2 427.9c1.1 1.1 1.6 2.6 1.6 4.6 0 2-.5 3.6-1.4 4.9-1 1.3-2.4 1.9-4.4 1.9-1.7 0-3-.6-4-1.7s-1.5-2.7-1.5-4.6c0-2.1.5-3.7 1.6-4.9 1-1.2 2.4-1.8 4.2-1.8 1.5 0 2.8.5 3.9 1.6zm-1.3 8.1c.5-1 .8-2.2.8-3.4 0-1.1-.2-2.1-.5-2.8-.6-1.1-1.6-1.7-3-1.7-1.2 0-2.1.5-2.7 1.4s-.8 2.1-.8 3.5c0 1.3.3 2.4.8 3.3s1.5 1.3 2.7 1.3c1.3-.1 2.2-.6 2.7-1.6z"/><path id="XMLID_205_" d="M362.3 426.6h2v1.7c.6-.7 1.2-1.2 1.8-1.5.6-.3 1.4-.5 2.2-.5 1.7 0 2.9.6 3.5 1.8.3.7.5 1.6.5 2.8v7.8h-2.1V431c0-.7-.1-1.3-.3-1.8-.4-.8-1-1.1-2-1.1-.5 0-.9 0-1.2.1-.6.2-1.1.5-1.5 1-.3.4-.6.8-.7 1.2-.1.4-.2 1-.2 1.8v6.4h-2.1v-12z"/></g><g id="XMLID_143_"><path id="XMLID_202_" d="M40 47.3h2.3v16.8H40V47.3z"/><path id="XMLID_200_" d="M45.7 51.8h2v1.7c.6-.7 1.2-1.2 1.8-1.5.6-.3 1.4-.5 2.2-.5 1.7 0 2.9.6 3.5 1.8.3.7.5 1.6.5 2.8v7.8h-2.1v-7.7c0-.7-.1-1.3-.3-1.8-.4-.8-1-1.1-2-1.1-.5 0-.9 0-1.2.1-.6.2-1.1.5-1.5 1-.3.4-.6.8-.7 1.3-.1.4-.2 1-.2 1.8v6.4h-2.1V51.8z"/><path id="XMLID_198_" d="M59.7 51.8l3.3 10 3.4-10h2.2L64 64.1h-2.2l-4.5-12.2h2.4z"/><path id="XMLID_195_" d="M70.4 47.3h2.1v2.3h-2.1v-2.3zm0 4.6h2.1v12.2h-2.1V51.9z"/><path id="XMLID_193_" d="M76.8 60.2c.1.7.2 1.2.5 1.6.5.7 1.4 1 2.8 1 .8 0 1.5-.2 2.1-.5.6-.3.9-.8.9-1.5 0-.5-.2-.9-.7-1.2-.3-.2-.9-.4-1.8-.6l-1.7-.4c-1.1-.3-1.8-.5-2.3-.9-.9-.6-1.3-1.3-1.3-2.3 0-1.2.4-2.1 1.3-2.8s2-1.1 3.4-1.1c1.9 0 3.2.5 4 1.6.5.7.8 1.4.8 2.2h-1.9c0-.5-.2-.9-.5-1.3-.5-.5-1.3-.8-2.5-.8-.8 0-1.4.1-1.8.4s-.6.7-.6 1.2.3 1 .8 1.3c.3.2.8.4 1.4.5l1.4.3c1.5.4 2.5.7 3 1 .8.5 1.2 1.4 1.2 2.5s-.4 2-1.3 2.8c-.8.8-2.1 1.2-3.8 1.2-1.8 0-3.1-.4-3.9-1.2s-1.2-1.8-1.2-3.1h1.7z"/><path id="XMLID_190_" d="M87.3 47.3h2.1v2.3h-2.1v-2.3zm0 4.6h2.1v12.2h-2.1V51.9z"/><path id="XMLID_187_" d="M92.3 47.2h2v6.1c.5-.6 1-1 1.6-1.3.6-.3 1.3-.5 2-.5 1.5 0 2.8.5 3.7 1.6s1.4 2.6 1.4 4.6c0 1.9-.5 3.5-1.4 4.8-.9 1.3-2.2 1.9-3.9 1.9-.9 0-1.7-.2-2.4-.7-.4-.3-.8-.7-1.2-1.3V64h-1.9V47.2zm7.9 14.1c.6-.9.8-2 .8-3.5 0-1.3-.3-2.4-.8-3.2-.6-.8-1.4-1.3-2.4-1.3-.9 0-1.8.3-2.5 1s-1.1 1.8-1.1 3.4c0 1.1.1 2.1.4 2.8.5 1.3 1.6 2 3 2 1.2.1 2-.3 2.6-1.2z"/><path id="XMLID_185_" d="M105.6 47.3h2.1v16.8h-2.1V47.3z"/><path id="XMLID_182_" d="M118.3 52.2c.8.4 1.4.9 1.9 1.6.4.6.7 1.3.8 2.2.1.6.2 1.5.2 2.7h-8.9c0 1.2.3 2.2.9 3s1.4 1.1 2.5 1.1 1.9-.4 2.5-1.1c.4-.4.6-.9.8-1.4h2c-.1.4-.2.9-.5 1.5s-.6 1-1 1.4c-.6.6-1.4 1-2.3 1.2-.5.1-1 .2-1.7.2-1.5 0-2.8-.6-3.8-1.7-1.1-1.1-1.6-2.7-1.6-4.7s.5-3.6 1.6-4.8c1.1-1.2 2.4-1.8 4.2-1.8.7-.1 1.5.2 2.4.6zm.7 4.8c-.1-.9-.3-1.6-.6-2.1-.6-1-1.5-1.5-2.8-1.5-.9 0-1.7.3-2.4 1s-1 1.5-1 2.6h6.8z"/><path id="XMLID_180_" d="M142.3 48.5c1.2 1.1 1.8 2.4 1.9 3.8H142c-.2-1.1-.7-1.9-1.5-2.6-.7-.6-1.8-.9-3.1-.9-1.6 0-2.9.6-3.9 1.7-1 1.2-1.5 2.9-1.5 5.3 0 2 .5 3.6 1.4 4.8s2.2 1.8 4 1.8c1.6 0 2.9-.6 3.8-1.9.5-.7.8-1.6 1-2.7h2.2c-.2 1.8-.8 3.2-1.9 4.4-1.3 1.4-3.1 2.2-5.3 2.2-1.9 0-3.5-.6-4.9-1.8-1.7-1.6-2.6-4-2.6-7.2 0-2.5.6-4.5 1.9-6.1 1.4-1.7 3.3-2.6 5.8-2.6 2.2.1 3.8.7 4.9 1.8z"/><path id="XMLID_178_" d="M147.2 47.3h2.1v16.8h-2.1V47.3z"/><path id="XMLID_175_" d="M152.3 47.3h2.1v2.3h-2.1v-2.3zm0 4.6h2.1v12.2h-2.1V51.9z"/><path id="XMLID_172_" d="M157.3 51.9h2v1.6c.4-.6.9-1 1.4-1.3.7-.5 1.5-.7 2.5-.7 1.4 0 2.6.5 3.5 1.6s1.5 2.6 1.5 4.6c0 2.7-.7 4.6-2.1 5.7-.9.7-1.9 1.1-3.1 1.1-.9 0-1.7-.2-2.3-.6-.4-.2-.8-.6-1.2-1.2v6.2h-2.1v-17zm7.8 9.6c.6-.8 1-2 1-3.6 0-1-.1-1.8-.4-2.5-.5-1.3-1.5-2-2.9-2s-2.4.7-2.9 2.1c-.3.8-.4 1.7-.4 2.9 0 .9.1 1.7.4 2.4.5 1.3 1.5 1.9 2.9 1.9.8 0 1.6-.4 2.3-1.2z"/><path id="XMLID_169_" d="M170.3 51.9h2v1.6c.4-.6.9-1 1.4-1.3.7-.5 1.5-.7 2.5-.7 1.4 0 2.6.5 3.5 1.6s1.5 2.6 1.5 4.6c0 2.7-.7 4.6-2.1 5.7-.9.7-1.9 1.1-3.1 1.1-.9 0-1.7-.2-2.3-.6-.4-.2-.8-.6-1.2-1.2v6.2h-2.1v-17zm7.8 9.6c.6-.8 1-2 1-3.6 0-1-.1-1.8-.4-2.5-.5-1.3-1.5-2-2.9-2s-2.4.7-2.9 2.1c-.3.8-.4 1.7-.4 2.9 0 .9.1 1.7.4 2.4.5 1.3 1.5 1.9 2.9 1.9.8 0 1.6-.4 2.3-1.2z"/><path id="XMLID_166_" d="M183.5 47.3h2.1v2.3h-2.1v-2.3zm0 4.6h2.1v12.2h-2.1V51.9z"/><path id="XMLID_164_" d="M188.7 51.8h2v1.7c.6-.7 1.2-1.2 1.8-1.5.6-.3 1.4-.5 2.2-.5 1.7 0 2.9.6 3.5 1.8.3.7.5 1.6.5 2.8v7.8h-2.1v-7.7c0-.7-.1-1.3-.3-1.8-.4-.8-1-1.1-2-1.1-.5 0-.9 0-1.2.1-.6.2-1.1.5-1.5 1-.3.4-.6.8-.7 1.3s-.2 1-.2 1.8v6.4h-2.1V51.8z"/><path id="XMLID_161_" d="M208.5 52.3c.4.3.8.7 1.2 1.2V52h1.9v11.1c0 1.6-.2 2.8-.7 3.7-.8 1.7-2.5 2.5-4.8 2.5-1.3 0-2.4-.3-3.3-.9-.9-.6-1.4-1.5-1.5-2.8h2.1c.1.5.3 1 .6 1.3.5.5 1.2.7 2.2.7 1.6 0 2.6-.6 3.1-1.7.3-.7.4-1.8.4-3.5-.4.6-.9 1.1-1.5 1.4-.6.3-1.3.5-2.3.5-1.3 0-2.5-.5-3.5-1.4-1-.9-1.5-2.5-1.5-4.7 0-2 .5-3.6 1.5-4.8 1-1.1 2.2-1.7 3.6-1.7 1-.1 1.8.1 2.5.6zm.3 2.2c-.6-.7-1.4-1.1-2.4-1.1-1.4 0-2.4.7-3 2-.3.7-.4 1.7-.4 2.8 0 1.4.3 2.4.8 3.1.6.7 1.3 1.1 2.2 1.1 1.5 0 2.5-.7 3.1-2 .3-.8.5-1.6.5-2.6.1-1.4-.2-2.6-.8-3.3z"/><path id="XMLID_158_" d="M221.8 47.3h7.6c1.3 0 2.3.2 3.1.6 1.5.7 2.3 2 2.3 4 0 1-.2 1.8-.6 2.5s-1 1.2-1.7 1.5c.7.3 1.1.6 1.5 1.1s.5 1.1.6 2.1l.1 2.2c0 .6.1 1.1.2 1.4.1.5.4.9.7 1v.4h-2.8c-.1-.1-.1-.3-.2-.6s-.1-.7-.1-1.3l-.1-2.8c-.1-1.1-.4-1.8-1.2-2.2-.4-.2-1.1-.3-2-.3h-5v7.2h-2.3V47.3zm7.4 7.7c1 0 1.9-.2 2.5-.6s.9-1.2.9-2.3c0-1.2-.4-2-1.3-2.4-.5-.2-1.1-.3-1.8-.3H224V55h5.2z"/><path id="XMLID_155_" d="M245.7 52.2c.8.4 1.4.9 1.8 1.6.4.6.7 1.3.8 2.2.1.6.2 1.5.2 2.7h-8.9c0 1.2.3 2.2.9 3s1.4 1.1 2.5 1.1 1.9-.4 2.5-1.1c.4-.4.6-.9.8-1.4h2c-.1.4-.2.9-.5 1.5s-.6 1-1 1.4c-.6.6-1.4 1-2.3 1.2-.5.1-1 .2-1.7.2-1.5 0-2.8-.6-3.8-1.7-1.1-1.1-1.6-2.7-1.6-4.7s.5-3.6 1.6-4.8c1.1-1.2 2.4-1.8 4.2-1.8.8-.1 1.7.2 2.5.6zm.7 4.8c-.1-.9-.3-1.6-.6-2.1-.6-1-1.5-1.5-2.8-1.5-.9 0-1.7.3-2.4 1-.6.7-1 1.5-1 2.6h6.8z"/><path id="XMLID_152_" d="M257.9 52.3c.4.3.8.7 1.2 1.2V52h1.9v11.1c0 1.6-.2 2.8-.7 3.7-.8 1.7-2.5 2.5-4.8 2.5-1.3 0-2.4-.3-3.3-.9-.9-.6-1.4-1.5-1.5-2.8h2.1c.1.5.3 1 .6 1.3.5.5 1.2.7 2.2.7 1.6 0 2.6-.6 3.1-1.7.3-.7.4-1.8.4-3.5-.4.6-.9 1.1-1.5 1.4-.6.3-1.3.5-2.3.5-1.3 0-2.5-.5-3.5-1.4-1-.9-1.5-2.5-1.5-4.7 0-2 .5-3.6 1.5-4.8 1-1.1 2.2-1.7 3.6-1.7 1-.1 1.8.1 2.5.6zm.3 2.2c-.6-.7-1.4-1.1-2.4-1.1-1.4 0-2.4.7-3 2-.3.7-.4 1.7-.4 2.8 0 1.4.3 2.4.8 3.1.6.7 1.3 1.1 2.2 1.1 1.5 0 2.5-.7 3.1-2 .3-.8.5-1.6.5-2.6.1-1.4-.2-2.6-.8-3.3z"/><path id="XMLID_149_" d="M264.1 47.3h2.1v2.3h-2.1v-2.3zm0 4.6h2.1v12.2h-2.1V51.9z"/><path id="XMLID_146_" d="M278.2 53c1.1 1.1 1.6 2.6 1.6 4.6 0 2-.5 3.6-1.4 4.9-1 1.3-2.4 1.9-4.4 1.9-1.7 0-3-.6-4-1.7s-1.5-2.7-1.5-4.6c0-2.1.5-3.7 1.6-4.9 1-1.2 2.4-1.8 4.2-1.8 1.5.1 2.8.6 3.9 1.6zm-1.3 8.2c.5-1 .8-2.2.8-3.4 0-1.1-.2-2.1-.5-2.8-.6-1.1-1.6-1.7-3-1.7-1.2 0-2.1.5-2.7 1.4-.6 1-.8 2.1-.8 3.5 0 1.3.3 2.4.8 3.3.6.9 1.5 1.3 2.7 1.3 1.3-.1 2.2-.6 2.7-1.6z"/><path id="XMLID_144_" d="M282.3 51.8h2v1.7c.6-.7 1.2-1.2 1.8-1.5.6-.3 1.4-.5 2.2-.5 1.7 0 2.9.6 3.5 1.8.3.7.5 1.6.5 2.8v7.8h-2.1v-7.7c0-.7-.1-1.3-.3-1.8-.4-.8-1-1.1-2-1.1-.5 0-.9 0-1.2.1-.6.2-1.1.5-1.5 1-.3.4-.6.8-.7 1.3s-.2 1-.2 1.8v6.4h-2.1V51.8z"/></g><circle id="XMLID_142_" cx="254.3" cy="255.6" r="5.5"/><circle id="XMLID_141_" cx="94.3" cy="227.6" r="5.5"/><path id="XMLID_140_" d="M254.3 256.1v155" style="stroke:#000000;stroke-miterlimit:10;" /><path id="XMLID_139_" d="M94.3 72.1v155" style="stroke:#000000;stroke-miterlimit:10;" /></svg>

</figure>

The diagram helps us to understand the `clipPath` shape by revealing what remains visible and invisible to the viewer as the folding action takes place. The individual blades don’t fold because the motion is fast enough to fool the eye — the entire section of blades is moved outside the clipping path through the power of rotation. The `clipPath` is nothing more than a simple polygon shape. Anything that resides within the bounding area is visible to the viewer, and anything outside of this region is invisible.</p>

<pre><code class="language-markup">&lt;svg version="1.1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" viewBox="0 0 92 92.1"&gt;
  &lt;defs&gt;
    &lt;polyline id="fan-clipShape" points="12.5,79.5 89.2,86.6 89.2,2.5 12.5,2.5    "/&gt;

   &lt;clipPath id="fan-clipPath"&gt;
  &lt;use xlink:href="#fan-clipShape"/&gt;
    &lt;/clipPath&gt;
  &lt;/defs&gt;

  &lt;g id="fan" clip-path="url(#fan-clipPath)"&gt;…&lt;/g&gt;
  &lt;g id="handles"&gt;…&lt;/g&gt;
&lt;/svg&gt;
</code></pre>

The SVG uses a `polyline` element to create the defining shape. A `clipPath` is then created around it, defining the bounding region, a square. Finally, the shape is laid over the portion of the artwork where the clipping effect is desired — that is, directly over the fan blades, designated with an ID of `fan` and referred to by the `clip-path` attribute.</p>

## Clips And Paths To Create The Illusion Of A Morph

See the Pen [SVG Paper Shredder](https://codepen.io/chrisgannon/pen/bdGqBo/) by Chris Gannon ([@chrisgannon](https://codepen.io/chrisgannon)) on [CodePen](https://codepen.io).

In this demo, Chris Gannon animates clipping paths to make paper appear as though it’s being shredded or morphed into another form, although the strips themselves are not created with clip paths. Investigating the HTML panel of this demo, you’ll see that the individual parts of this SVG reside in a single vector file.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a180680e-7c8a-4704-8122-7533e145f7c0/04-shredder-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d8ce89a-0426-4d7c-943a-de74f1c6e176/04-shredder-opt-preview.png" alt="Shredder by Chris Gannon" /></a><figcaption>Shredder by Chris Gannon. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a180680e-7c8a-4704-8122-7533e145f7c0/04-shredder-opt.png">View large version</a>)</figcaption></figure>

If you’re still asking yourself how this trick is done, the following image illustrates the effect:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fff761d1-6f7f-418f-bd08-a95ee8e73ad0/05-shredderclip-breakdown-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02897a7d-e0d6-40de-975f-700ccfacfc4c/05-shredderclip-breakdown-opt-preview.png" alt="A breakdown depicting the XML required for the clipPath, which creates the paper-shredding effect" /></a><figcaption>A breakdown depicting the XML required for the <code>clipPath</code>, which creates the paper-shredding effect. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fff761d1-6f7f-418f-bd08-a95ee8e73ad0/05-shredderclip-breakdown-opt.png">View large version</a>)</figcaption></figure>

The clipping paths are simply SVG rectangles, nothing more! This means that anything within the boundaries of the defined rectangle will be visible to the viewer, and anything that lies outside of this space will be invisible.

All that’s left to do is move the bits within these clipping regions along the y axis from top to bottom. Just before the full sheet of paper reaches the end of its sequence, a call is made to the next sequence of the animation, whereupon the paper is chopped up and ejected from the shredder.</p>

## Clipping Animations With Mouse Events

See the Pen [X-ray me (SVG Experiment)](https://codepen.io/noeldelgado/pen/ByxQjL/) by Noel Delgado ([@noeldelgado](https://codepen.io/noeldelgado)) on [CodePen](https://codepen.io).

This demo was posted quite a while back, but it’s worth sharing because it shows another great use of the clip path. It’s also a pretty fun way to combine SVG clips with user interaction. Move your mouse over the girl to see the effect.

See the Pen [SVG Space Rocket!](https://codepen.io/chrisgannon/pen/QbLMxz/) by Chris Gannon ([@chrisgannon](https://codepen.io/chrisgannon)) on [CodePen](https://codepen.io).

Here is the same concept that we previously saw, but combined with a bit of animation to enhance the effect.</p>

## Conclusion

Clip paths open up a wide array of exciting possibilities. Understanding the simple mechanics and how everything moves relative to each other can help you create some powerful and captivating interactions for your users. Try this out with text, imagery, scrolling and more! Have fun, and don’t be scared to take chances.

_(ds, ml, al); Smashing Magazine would like to thank [Sarah Drasner](https://www.smashingmagazine.com/author/sarahdrasner/) for her expert assistance with code examples in this article._


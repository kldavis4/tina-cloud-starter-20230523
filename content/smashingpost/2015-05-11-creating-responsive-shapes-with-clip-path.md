---
title: Creating Responsive Shapes With Clip-Path And Breaking Out Of The Box
slug: creating-responsive-shapes-with-clip-path
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/292d7d88-d067-4abd-b735-17c7a603da50/example-pic-for-code-pen-illu.jpg
date: 2015-05-11T20:46:02.000Z
author: karenmenezes
description: >-
  [CSS](https://www.smashingmagazine.com/2014/11/03/styling-and-animating-svgs-with-css/2/)’
  `clip-path` property is your ticket to shape-shifting the monotonous, boxy
  layouts traditionally associated with flat, responsive design. **You will
  begin to think outside the box**, literally, and hexagons, stars and octagons
  will begin to take form on your web pages. Once you get your hands dirty with
  `clip-path`, there’s no end to the shapes you can generate, simply by tweaking
  a few values.

  While the focus of this article is on `clip-path` using polygons with CSS, all
  of the demos provide a reference to an inline SVG, in order to gain additional
  support on Firefox. Generating a [responsive
  SVG](https://www.smashingmagazine.com/2014/03/05/rethinking-responsive-svg/)
  clipped shape is trivial once you have created a responsive shape with CSS’
  `clip-path`. We’ll look at this in detail later.
categories:
  - Coding
  - CSS
  - Responsive Design
---
CSS’ <code>clip-path</code> property is your ticket to shape-shifting the monotonous, boxy layouts traditionally associated with flat, responsive design. <strong>You will begin to think outside the box</strong>, literally, and hexagons, stars and octagons will begin to take form on your web pages. Once you get your hands dirty with <code>clip-path</code>, there’s no end to the shapes you can generate, simply by tweaking a few values.

While the focus of this article is on <code>clip-path</code> using polygons with CSS, all of the demos provide a reference to an inline SVG, in order to gain additional support on Firefox. Generating a responsive SVG clipped shape is trivial once you have created a responsive shape with CSS’ <code>clip-path</code>. We’ll look at this in detail later.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Adventures In The Third Dimension: CSS 3D Transforms](https://www.smashingmagazine.com/2012/01/adventures-in-the-third-dimension-css-3-d-transforms/)
*   [Animating Clipped Elements In SVG](https://www.smashingmagazine.com/2015/12/animating-clipped-elements-svg/)
*   [Designing an Interactive Exhibition With CSS Clip Paths](https://www.smashingmagazine.com/2015/06/the-making-of-in-pieces/)
*   [The Illusion Of Life: An SVG Animation Case Study](https://www.smashingmagazine.com/2016/07/an-svg-animation-case-study/)

## Clip-Path, In A Nutshell

Clipping, with the <code>clip-path</code> property, is akin to cutting a shape (like a circle or a pentagon) from a rectangular piece of paper. The property belongs to the “<a href="https://www.w3.org/TR/css-masking-1">CSS Masking Module Level 1</a>” specification. The spec states, “CSS masking provides two means for partially or fully hiding portions of visual elements: masking and clipping”.

{{% feature-panel %}}

The first part, i.e. masking, has to do with using a graphical element, such as a PNG image, CSS gradient or SVG element, as a mask to conceal sections of another element.

The second part, i.e. <code>clip-path</code>, involves a closed vector path, which could be a basic shape defined in CSS or an SVG using the <code class="inline-block">clipPath</code> tag. The region inside this path is displayed, and everything beyond or outside it is clipped out.</p>

<strong>Note:</strong> Masking is beyond the scope of this article, but <a href="https://css-tricks.com/clipping-masking-css">CSS-Tricks</a> and <a href="https://www.html5rocks.com/en/tutorials/masking/adobe/">HTML5 Rocks</a> have more information.

Below is a simple visualization of how <code>clip-path</code> works:

{{< codepen height="250" theme_id="0" slug_hash="KpdomO" default_tab="result" user="imohkay" >}}See the Pen <a href="https://codepen.io/imohkay/pen/KpdomO/">Visualizing clip-path</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

<strong>Note:</strong> The demos in this article, including the one above, will work in Firefox and in WebKit and Blink browsers, including Chrome, Safari and Opera.</p>

## Clip-Path Is Not Clip

There is an <a href="https://www.w3.org/TR/CSS21/visufx.html#clipping">older CSS 2.1 <code>clip</code> property</a>, which is rather restrictive, notably because it supports only rectangular shapes. It has been <a href="https://www.w3.org/TR/css-masking-1/#clip-property">deprecated in favor of <code>clip-path</code></a>.

Articles about clipping that use the deprecated syntax feature code that looks like this:

<pre><code class="language-css">
.element {
  clip: rect(30px, 30px, 20px, 20px);
}
</code></pre>

## Support For Clip-Path

In August 2014, the “CSS Masking Module” was published as a “Candidate Recommendation,” which is a step up from the earlier “Last Call Working Draft” stage. Before we look at browser support, it’s important to consider the multiple ways in which <code>clip-path</code> can be applied to an element, because browser support varies for each method.

There are two ways to use <code>clip-path</code>:

1.  **with CSS** Basic shapes from the “[CSS Shapes Module](https://www.w3.org/TR/css-shapes-1/#typedef-basic-shape)” provide a convenient way to use `clip-path`. The different shapes available are `polygon`, `circle`, `ellipse` and `inset`; `inset` is for rectangular shapes.
2.  **with SVG** One can, alternatively, create a shape using SVG and then clip an element to this shape via the URL syntax. There are two ways to do this:
    *   with a reference to an inline SVG (i.e. the SVG markup exists on the page itself),
    *   with a reference to an external SVG document.In both cases, the `clipPath` element within the SVG is used to wrap the element that determines the clipping path, be it a circle, polygon, path or other element. Compare the demo below in Firefox and in a WebKit or Blink browser such as Chrome to spot the differences. Square images imply a lack of browser support. **Note**: The third image does not show up in Safari. Despite extensive debugging, I'm unable to resolve the issue. I'd appreciate a note in the comments section if you come across the solution.

{{< codepen height="400" theme_id="0" slug_hash="GJpxXY" default_tab="result" user="imohkay" >}}See the Pen <a href="https://codepen.io/imohkay/pen/GJpxXY/">Clip-path: Browser support</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

As you may have gathered from observing the demo above in different browsers, <a href="https://caniuse.com/#search=clip-path">support for clipping paths</a> is quirky and currently depends on the means by which you choose to clip an element:

*   **with CSS**: Chrome 24+, Safari 7+, Opera 15+, iOS 7.1+, Android 4.4+, Opera Mobile 24+ (Note that all supported browsers currently require the `-webkit` vendor prefix.)
*   **with SVG**: all of the browsers listed above and Firefox 3.5+

The <code>clip-path</code> property is not yet supported in Internet Explorer but is currently <a href="https://status.modern.ie/masks?term=masks">under consideration</a> as part of the “Masking Module.”

<strong>Note:</strong> There is a caveat with support for SVG clipping path. Modern WebKit and Blink browsers support clipping paths with SVGs only if they are declared inline (i.e. within the document). References to external SVGs are supported only in Firefox, as evidenced in the demo above. The Chromium project is <a href="https://code.google.com/p/chromium/issues/detail?id=109212">tracking this bug</a>.

Let’s examine the <strong>advantages of CSS versus SVG</strong> with <code>clip-path</code>.</p>

### Advantages of CSS

*   The lucid syntax is easy to grasp due to the relative simplicity of basic shapes.
*   Responsiveness is easily achieved with relative units, such as percentages.</p>

### Advantages of SVG

*   Browser support is better, with the addition of Firefox.
*   You can clip with complex shapes, multiple shapes and text.

While CSS offers a <code>background-clip</code> property that provides us with some options (including a non-standard way to clip text), neither <code>background-clip</code> nor CSS’ <code>clip-path</code> match what SVG clipping can achieve in modern browsers. Getting acquainted with <code>clip-path</code> via CSS, however, is less intimidating (especially if you aren’t familiar with manipulating SVGs) and will prepare you for the intricacies of clipping paths with SVG, as well as the “<a href="https://www.w3.org/TR/css-shapes/">CSS Shapes Module</a>,” where content aligns itself to the shape of an element.</p>

<strong>Note:</strong> If you can’t wait to delve into the matrix of clipping with SVG, <a href="https://sarasoueidan.com/blog/css-svg-clipping/">Sara Soueidan’s overview</a> is a good starting point.

Let’s look at the <strong>pros and cons</strong> of using <code>clip-path</code> to progressively enhance our designs.</p>

### Pros

*   Browsers that don’t support the `clip-path` property will ignore it. If you use it with care, users on non-supporting browsers won’t suspect a thing!
*   Once a clipping-path shape is generated, the specification states that pointer events must not be dispatched outside the clipping area (which is ideal). So, the click event is [restricted to the shape and its outer boundary](https://www.w3.org/TR/css-masking-1/#clipping-paths). We will look at this in the demos below.
*   You can use percentages or any length unit, such as pixels or ems, to define your coordinates with basic shapes using CSS. Fluid units such as percentages can be used to create responsive shapes, perfect for adaptive layouts.</p>

### Cons

*   All borders, shadows and outlines [outside the clipping region will be clipped](https://www.w3.org/TR/css-masking-1/#clipping-paths). You can’t add a border and expect it to be honored. We’ll look at some alternatives below.
*   The specification has not yet reached the “Recommendation” stage, so there’s always a chance that the syntax will change in the interim.
*   A few bugs have been reported with `clip-path` and 3D transforms, transitions and opacity, which are covered in the demos below. Be aware of these, and avoid combining properties that replicate these bugs.</p>

## Clip-Path With Polygons: Usage And Syntax

The demos below focus on using different kinds of polygons in a design. The syntax for the other basic shapes (i.e. inset, circle and ellipse) is quite simple, and you can go only so far with them. Polygons, however, open the door to a practically infinite numbers of shapes.

The syntax for a basic polygon shape is this:

<pre><code class="language-css">
.element { clip-path: polygon(x1 y1, x2 y2, x3 y3, ...); }
</code></pre>

Each argument pair in the list represents the x-axis and y-axis coordinates of that particular vertex of the polygon.

Here’s how we’d write it in the real world (minus the currently supported WebKit-prefixed version):

<pre><code class="language-css">
.element { clip-path: polygon(0 100%, 0 0, 100% 0, 80% 100%); }
</code></pre>

Let’s add support for Firefox with a reference to an inline SVG:

<pre><code class="language-css">
.element { clip-path: url("#clip-shape"); }
</code></pre>

Here’s how our selector will finally look, with cross-browser support:

<pre><code class="language-css">
.element {
  -webkit-clip-path: polygon(0 100%, 0 0, 100% 0, 80% 100%);
  clip-path: polygon(0 100%, 0 0, 100% 0, 80% 100%);
  -webkit-clip-path: url("#clip-shape"); /* required for Webkit/Blink browsers if you're using only inline SVG clipping paths, but not CSS clip-path */
  clip-path: url("#clip-shape");
}
</code></pre>

Below is the code for the inline SVG, which we will need to insert anywhere in the markup.</p>

<pre><code class="language-markup">
&lt;svg width="0" height="0"&gt;
  &lt;defs&gt;
	&lt;clipPath id="clip-shape" clipPathUnits="objectBoundingBox"&gt;
	  &lt;polygon points="0 1, 0 0, 1 0, 0.8 1" /&gt;
	&lt;/clipPath&gt;
  &lt;/defs&gt;
&lt;/svg&gt;
</code></pre>

Here is the final demo.

{{< codepen height="268" theme_id="0" slug_hash="pJjVob" default_tab="result" user="imohkay" >}}See the Pen <a href="https://codepen.io/imohkay/pen/pJjVob/">Clip-path: Demo</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

You can create a responsive SVG clipping path in the following manner:

*   Set the width and height of the SVG to `0`.
*   Set an ID on the `clipPath` element inside the SVG, which can then be referenced with CSS. You can use inline or external SVG, keeping in mind the browser support mentioned above.
*   Reuse the percentage coordinate values of the polygon defined with CSS `clip-path`. Just divide them by 100 and add as unitless polygon points to the SVG.
*   Set the value of the `clipPathUnits` attribute to `objectBoundingBox`, so that the clipping path honors the boundaries of the HTML element that references it.</p>

<a href="https://demosthenes.info/blog/1007/Combining-CSS-clip-path-and-Shapes-for-New-Layout-Possibilities">Dudley Storey has more</a> on this process.

Let’s look at a demo to understand <strong>how to plot coordinates for a polygon</strong>.

Below we have an image that is clipped. The background color represents the dimensions of the original image. The black boxes with the coordinates are simply absolutely positioned divs whose locations match the polygon’s vertices in percentages. You will see that they maintain their positions, even if you resize your browser window to a narrow width (for example, 400 pixels or greater).

{{< codepen height="700" theme_id="0" slug_hash="pJjVgE" default_tab="result" user="imohkay" >}}See the Pen <a href="https://codepen.io/imohkay/pen/pJjVgE/">Clip-path: Polygon coordinates</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## Real-World Examples With Clip-Path

<strong>Note:</strong> Every demo in this article uses <code>clip-path</code> with CSS but also has inline SVG in the markup with a class of <code>clip-svg</code>, which simply resets the width and height of the SVG to <code>0</code>. You could, alternatively, remove the class and set the width and height attributes directly in the SVG markup.</p>

### Example 1: Clip An Image to Various Polygon Shapes

In case you need a quick definition of a polygon, it’s a 2D shape that’s closed and consists of straight lines.

Therefore, a shape cannot be a polygon if it has curves, is open or has fewer than three lines. Some famous polygons in history are triangles, quadrilaterals, pentagons and hexagons. Even star shapes are polygons, since the boundaries of a polygon can cross each other.</p>

<strong>Note:</strong> The images in the demo are responsive. By using the good ol’ responsive image solution of <code>img { max-width: 100%; height: auto; }</code> and adaptive clipping paths via CSS and SVG, we make our polygons blissfully scale up and down.

This demo is the result of an exercise to understand plotting coordinates to make polygon shapes. I’ve added several shapes that you can use for your designs in the demo below. On hovering over each image, you will see the aspect ratio of the original image.

Nothing beats the exceptional <a href="https://bennettfeely.com/clippy">Clippy</a>, a GUI tool by Bennett Feely to visualize shapes. All coordinates for all of the existing shapes are provided in percentages, and there’s also a custom polygon option. This one’s a game-changer. You can use Clippy to generate clipped shapes and create SVGs for yourself based on them, for better browser support.

{{< codepen height="500" theme_id="0" slug_hash="RPWyjz" default_tab="result" user="imohkay" >}}See the Pen <a href="https://codepen.io/imohkay/pen/RPWyjz/">Clip-path: Polygon shapes</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### Example 2: Animate a Basic Shape With CSS Transition

Hover over the purple hexagon. It transforms to an octagon. However, the CSS transition specified has not taken effect.

{{< codepen height="268" theme_id="0" slug_hash="ZGbjbz" default_tab="result" user="imohkay" >}}See the Pen <a href="https://codepen.io/imohkay/pen/ZGbjbz/">Clip-path: shape transition: Part 1</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

The reason for this is explained in <a href="https://sarasoueidan.com/blog/animating-css-shapes/">Sara Soueidan’s article on animating CSS shapes</a>: “The number of points defining the final shape must be the same as the number of points defining the initial shape.” Makes perfect sense!

Because a hexagon has six pairs of coordinate points, let’s add two pairs through duplication to make them eight, to match the number of pairs for an octagon. These duplicated pairs won’t affect the shape of the hexagon.

This is the declaration for a hexagon in the form of a default polygon with six pairs of coordinate points:

<pre><code class="language-css">
clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
</code></pre>

And this is the declaration for a hexagon in the form of a polygon with eight pairs of coordinates, the first two of which have been duplicated:

<pre><code class="language-css">clip-path: polygon(50% 0%, 50% 0%, 100% 25%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
</code></pre>

Now the transition will be smooth as the shapes transform, as seen in the demo below.</p>

<strong>Note:</strong> For browsers that support clipping paths only with SVG (currently Firefox), we need to add a SMIL animation to obtain a seamless transition on hover. According to the SMIL specification, declarative animations can be used to animate paths and polygon points in SVG, which is currently impossible with CSS.

Keep in mind that some people are <a href="https://groups.google.com/a/chromium.org/forum/#!topic/blink-dev/5o0yiO440LM">discussing deprecating SMIL in Chrome and Chromium</a> and focusing on implementing the <a href="https://www.w3.org/TR/web-animations/">Web Animations API</a>, which is unfortunately at the early draft stage.

In the demo below (background image courtesy of <a href="https://www.morguefile.com/archive/display/946871">morgueFile</a>), you can see that we have animated the polygon points between the <code>mouseover</code> and <code>mouseout</code> events over a duration of 0.2 seconds. Look for the <code>&lt;animate&gt;</code> tag in the SVG markup.

{{< codepen height="350" theme_id="0" slug_hash="ZGbjyG" default_tab="result" user="imohkay" >}}See the Pen <a href="https://codepen.io/imohkay/pen/ZGbjyG/">Clip-path: shape transition: Part 2</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### Example 3: Add a Border to a Clipped Object

To make a long story short, borders, outlines and box-shadows that lie outside the clipping region are removed.

I was a little saddened by this, and I pinged the W3C members on the working group for CSS. However, the conclusion is that there’s no way to do this when you’re using basic shapes. <a href="https://blog.dschulze.com">Dirk Schulze</a> responded to my query: “Yes, all drawing operations belonging to the element get clipped. This includes outlines and borders.”

See the demo below. Hover over the rhomboid with a partial border to see the original, unclipped version with the entire border.

{{< codepen height="300" theme_id="0" slug_hash="zGvLjo" default_tab="result" user="imohkay" >}}See the Pen <a href="https://codepen.io/imohkay/pen/zGvLjo/">Clip-path: Borders</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Of course, we can always use a CSS hack to get a border, which is what I finally resorted to — good ol’ generated content.

The demo below creates a copy of the element via a pseudo-element (<code>content:after</code>) and absolutely positions it. This creates the illusion of a border, enabling us to simulate interesting effects, such as the gradient border seen in the second octagon and the inset box-shadow via a CSS filter on the third one (not very pretty, but functional). Note that CSS filters currently work only in Firefox and in WebKit and Blink browsers.

{{< codepen height="470" theme_id="0" slug_hash="MwaBBK" default_tab="result" user="imohkay" >}}See the Pen <a href="https://codepen.io/imohkay/pen/MwaBBK/">Clip-path: Border simulation</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### Example 4: Use clip-path to Create a Diamond Grid Over a Rhombus

Below is the image we will use.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00511dce-9995-4904-aafe-410780c6b4a8/clip-img-large-preview-opt.jpg"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6da6dd8-f1f6-4e9d-852c-46327a44b1e3/clip-img-opt.jpg" alt="clip-image-demo" width="500" height="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00511dce-9995-4904-aafe-410780c6b4a8/clip-img-large-preview-opt.jpg">View large version</a>)</figcaption></figure>

This is the effect we’re aiming for. Upon hovering over the bottom three boxes, you’ll see the background color fade to reveal the background.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd54e2ae-fd5f-433f-80fc-e6d622f8ebb6/diamond-demo-large-preview-opt.jpg"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ed457b9-77da-4c78-9154-166298901337/diamond-demo-opt.jpg" alt="demo-clip-diamond" width="500" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd54e2ae-fd5f-433f-80fc-e6d622f8ebb6/diamond-demo-large-preview-opt.jpg">View large version</a>)</figcaption></figure>

The actual size of the image is 600 × 600 pixels. Thus, let’s start with four empty divs of 300 pixels each and apply the same background image to them. Let’s add a parent wrapper of 604 pixels and lay out the images with the <code>inline-block</code> property.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7d54c3c-d88b-4bdf-8e40-4f4a2d490432/diamond1-large-preview-opt.jpg"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7462af65-90fc-4acb-958f-c8b37d46d849/diamond1-opt.jpg" alt="demo-clip-diamond1" width="500" height="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7d54c3c-d88b-4bdf-8e40-4f4a2d490432/diamond1-large-preview-opt.jpg">View large version</a>)</figcaption></figure>

Let’s now change the value of the <code>background-position</code> property for each image to <code>top</code>, <code>left</code>, <code>right</code> and <code>bottom</code>, respectively.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3419756-dfd6-40f7-adfc-73e603fc5707/diamond2-large-preview-opt.jpg"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d05722d2-f458-4b74-8a2f-c976d9a42ceb/diamond2-opt.jpg" alt="demo-clip-diamond2" width="500" height="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3419756-dfd6-40f7-adfc-73e603fc5707/diamond2-large-preview-opt.jpg">View large preview</a>)</figcaption></figure>

Let’s clip each box into the shape of a rhombus. We will overlay an absolutely positioned layer on each of the bottom three images, with some text.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12aebae7-272b-4e20-92ff-6ab992385243/diamond3-large-preview-opt.jpg"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f03a16c3-1dd5-4668-88a7-5a7fba42bac8/diamond3-opt.jpg" alt="demo-clip-diamond3" width="500" height="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12aebae7-272b-4e20-92ff-6ab992385243/diamond3-large-preview-opt.jpg">View large version</a>)</figcaption></figure>

Now we will move the images into rows — the second and third image into one row, and the first and fourth into their own individual rows.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d64fb758-f9fb-454c-9997-510eafbfd7a9/diamond4-large-preview-opt.jpg"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04ab445b-5af6-47f8-8439-98ed3f9aca0d/diamond4-opt.jpg" alt="demo-clip-diamond4" width="500" height="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d64fb758-f9fb-454c-9997-510eafbfd7a9/diamond4-large-preview-opt.jpg">View large version</a>)</figcaption></figure>

Finally, we will use negative margins to push up the second and third rows, so that they are laid out as in the final demo below. We can remove the width value of 604 pixels on the parent wrapper, and we can structure our media query so that the four diamond boxes move from a stacked layout on small screens to inline blocks on larger ones.

{{< codepen height="350" theme_id="0" slug_hash="KpdBrw" default_tab="result" user="imohkay" >}}See the Pen <a href="https://codepen.io/imohkay/pen/KpdBrw/">Clip-path: Diamond grid</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

While working on this demo, I noticed a bug in Chrome with pointer events being dispatched outside the clipped region, which <a href="https://www.w3.org/TR/css-masking-1/#clipping-paths">violates the specification</a>: “By default, pointer events must not be dispatched on the clipped-out (non-visible) regions of a shape.” I have <a href="https://code.google.com/p/chromium/issues/detail?id=468613">filed the bug</a>. The issue with this demo was solved by using the <code>pointer-events</code> property with a value of <code>none</code> on the overlay. Alternatively, you could apply the same <code>clip-path</code> value to the overlay to resolve the issue.

Due to the negative margins applied, this demo would look odd in browsers that don’t support <code>clip-path</code>. You would have to use some sort of feature detection to apply the margins (although I haven’t experimented with this) or the <code>@supports</code> CSS feature query, although I wouldn’t recommend the latter in production code.</p>

### Example 5: Create a Dummy Profile Page With Hexagons

Our final page should look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c2b5e08-4692-4f67-b454-1f692c25e4d6/hexagons-demo-large-preview-opt.jpg"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afea52db-e6d4-4f62-b66e-145bcc144b81/hexagons-demo-opt.jpg" alt="hexagon-demo" width="500" height="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c2b5e08-4692-4f67-b454-1f692c25e4d6/hexagons-demo-large-preview-opt.jpg">View large version</a>)</figcaption></figure>

We’ll start by adding a background image of hexagon tiles to the body (the image courtesy of <a href="https://subtlepatterns.com">Subtle Patterns</a>).

The hexagon <code>clip-path</code> values can be obtained from one of the demos above or with the Clippy tool.

The first hexagon uses a background image (because we’re blending a dull maroon into the background using the <code class="inline-block">background-blend-mode</code> property). Using generated content, an absolutely positioned overlay is clipped to a maroon triangle shape, which you can see on the bottom. It disappears on hover.

The second hexagon, with the word “work,” simply has a dark grey background that changes on hover.

The third hexagon has a gradient border, similar to the one in the demo on creating borders with <code>clip-path</code>.

The hexagons stack on small screens and are vertically centered on larger ones. I’ve used a combination of <code>display: table</code> and the absolute centering transforms hack — of course, you could use flexbox, floats or whatever else floats your layouting boat.

Here’s the final demo.

{{< codepen height="900" theme_id="0" slug_hash="ZGbmoQ" default_tab="result" user="imohkay" >}}See the Pen <a href="https://codepen.io/imohkay/pen/ZGbmoQ/">Clip-path: Hexagon shapes for dummy profile page</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

I <a href="https://code.google.com/p/chromium/issues/detail?id=446901">discovered a bug</a> with <code>clip-path</code> while creating this demo. Altering the value of <code>opacity</code> in combination with the CSS transition causes a flicker and artifacts on the page. Be aware of this if you’re using <code>clip-path</code> to progressively enhance a design.

There is also a bug with <code>clip-path</code> and the <code>backface-visibility</code> property when set to hidden. This <a href="https://code.google.com/p/chromium/issues/detail?id=350724">bug is documented in Chromium</a>’s issue tracker and I have been able to replicate it using the basic shape syntax in Chrome on Linux. Keep this in mind if you’re using a <code>clip-path</code> shape to do a cool 3D flip or anything that uses CSS 3D transforms.

While clipping with SVG wins hands down for its flexibility and options, nothing beats the ease with which elements can be clipped with CSS. In fact, the same polygon coordinates can be effortlessly recycled to create responsive SVG for even better browser support. With <code>clip-path</code>, you can dramatically alter the look and feel of a page, without having to worry much about non-supporting browsers, where it will gracefully degrade. If you choose to use <code>clip-path</code> for design enhancements, keep an eye on the specification as it advances towards “Recommendation” status.</p>

## Resources, Tools And Inspiration

*   “[CSS Masking Module Level 1](https://www.w3.org/TR/css-masking-1),” W3C This is the ultimate source of truth and the best reference, when in doubt.
*   “[Clipping in CSS and SVG: The `clip-path` Property and `<clipPath>` Element](https://sarasoueidan.com/blog/css-svg-clipping),” Sara Soueidan Soueidan has the definitive guide to clipping paths. While the focus is largely on SVG, this article is a fantastic introduction, with plenty of information for both intermediate and advanced readers.
*   “[clip-path](https://tympanus.net/codrops/css_reference/clip-path),” Sara Soueidan, Codrops Soueidan’s well-researched and comprehensive article over on Codrops breaks down a fairly complicated module into something that is easy to understand and assimilate.
*   “[Clipping and Masking in CSS](https://css-tricks.com/clipping-masking-css/),” Chris Coyier, CSS-Tricks Coyier’s article, peppered with several helpful demos, explains both clipping and masking.
*   [Clippy](https://bennettfeely.com/clippy) Bennett Feely’s fab clip-path maker can generate a plethora of predefined and custom polygon shapes, circles and ellipses for CSS’ `clip-path`. All values are in percentages and, hence, useful for responsive layouts.
*   [Clip Path Generator](https://cssplant.com/clip-path-generator) CSS Plant offers a rather comprehensive graphical interface to clip or mask an element. Cross-browser support is provided for Firefox, Chrome, Safari and old iOS. Clips are in pixels, not percentages.
*   [Species in Pieces](https://www.species-in-pieces.com) So breathtaking it borders on the spiritual, this showcase of 30 endangered species was crafted entirely with CSS’ `clip-path`, without a hint of canvas or WebGL. View it in a WebKit or Blink browser until the other ones catch up.

{{< signature "ds, il, al" >}}


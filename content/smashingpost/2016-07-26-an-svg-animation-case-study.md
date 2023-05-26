---
title: 'The Illusion Of Life: An SVG Animation Case Study'
slug: an-svg-animation-case-study
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef4811ef-46cc-4e02-8823-d2ea5ba59835/02-transformations-opt.jpg
date: 2016-07-26T17:57:51.000Z
author: michaelngo
description: >-
  With flat design becoming the ever visible trend of 2016, it’s clear why
  there’s been a resurgence in SVG usage. The benefits are many:
  resolution-independence, cross-browser compatibility and accessible DOM nodes.
  In this article, we’ll take a look at **how we can use SVGs** to create
  seemingly complex animations from simple illustrations.

  This project began as a simple thought experiment: **How far can we push SVG
  animation?** At the time, designer Chris Halaska and I were colleagues working
  on an illustration-heavy campaign website. While aesthetically pleasing, the
  designs lacked the required “oomph” that all creatives search for.
categories:
  - Coding
  - SVG
---
With flat design becoming the ever visible trend of 2016, it’s clear why there’s been a resurgence in SVG usage. The benefits are many: resolution-independence, cross-browser compatibility and accessible DOM nodes. In this article, we’ll take a look at how we can use SVGs to create seemingly complex animations from simple illustrations.</p>

## The Brief

<figure><br>
<div data-height="400" data-theme-id="18342" data-slug-hash="QNgZdx" data-default-tab="result" data-user="hellomichael" data-embed-version="2" class="codepen">See the Pen <a href="https://codepen.io/hellomichael/pen/QNgZdx/">The Illusion of Life: An SVG Animation Case Study</a> by Michael Ngo (<a href="https://codepen.io/hellomichael">@hellomichael</a>) on <a href="https://codepen.io">CodePen</a>.</div>
<figcaption>Figure 1. What are we creating? Seemingly complex animations from simple SVG illustrations.</figcaption></figure>

This project began as a simple thought experiment: **How far can we push SVG animation?**

At the time, designer [Chris Halaska](https://www.chrishalaska.com/) and I were colleagues working on an illustration-heavy campaign website. While aesthetically pleasing, the designs lacked the required “oomph” that all creatives search for. We found the answer in “[The Camera Collection](https://vimeo.com/41336551),” a motion graphics animation that had just gone viral. We could use animations to bring illustrations to life, and SVGs were the perfect medium to do this.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Rethinking Responsive SVG](https://www.smashingmagazine.com/2014/03/rethinking-responsive-svg/)
*   [A Few Different Ways To Use SVG Sprites In Animation](https://www.smashingmagazine.com/2015/03/different-ways-to-use-svg-sprites-in-animation/)
*   [Creating Cel Animations With SVG](https://www.smashingmagazine.com/2015/09/creating-cel-animations-with-svg/)
*   [The Guide To CSS Animation: Principles and Examples](https://www.smashingmagazine.com/2011/09/the-guide-to-css-animation-principles-and-examples/)

The problem we were facing, which still exists very much today, is that SVG animation is either delegated to a front-end developer who is attempting art direction or to a designer who is attempting JavaScript. Of course, neither of these scenarios is inherently wrong, but with animation being visual in nature and with very few applications tackling the problem, we wanted to bridge the gap between code and design.

Our idea was to create a **data-driven process that enables designers to quickly prototype animations from static illustrations**.</p>

## The Rules Of Animation

In [_The Illusion of Life_](https://en.wikipedia.org/wiki/Disney_Animation:_The_Illusion_of_Life), Disney outlines 12 basic principles to add character to animation. Squash and stretch, anticipation, slow in and slow out, timing, and exaggeration all serve to bring any object, inanimate or otherwise, to life. We wanted to follow these principles in our project, moving away from the rigidness of the DOM to something more fluid and natural. By creating a system around **transformations, timing and easing**, we were able to create animations that were stylistically uniform, but each with a character of its own.</p>

### Transformations

The flat design trend lends itself so well to SVG usage because of the simplicity of the illustrations. We mimicked this characteristic in animation, pairing geometric shapes with simple geometric movements. We had a single rule: use **basic transformations** (`translate`, `rotate`, `scale`) with **basic origins** (`left`, `right`, `top`, `bottom` and `center`).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef4811ef-46cc-4e02-8823-d2ea5ba59835/02-transformations-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef4811ef-46cc-4e02-8823-d2ea5ba59835/02-transformations-opt.jpg" alt="transformations" width="500" height="301" /></a><figcaption>Figure 2. The nine possible animation origins, using a combination of left, right, center, top and bottom.</figure>

### Timing

To maintain a similar cadence and rhythm, we constrained ourselves to very specific increments of time. Animations lasted 2 seconds and comprised 10 individual steps. A **tween**, an animation of just a single transformation (translate, rotate and scale) had to begin and end on one of these steps, which we defined as **keyframes**.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfdcbedb-53bc-4a39-8d1e-798fb5b411f7/03-timing-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfdcbedb-53bc-4a39-8d1e-798fb5b411f7/03-timing-opt.jpg" alt="timing" width="500" height="301" /></a><figcaption>Figure 3. An example animation in which each step increments by 200 milliseconds with three overlapping tweens.</figcaption></figure>

### Easing

While transformations and timing are enough to create the visual perception of motion, easing brings everything to life. We found that three easing formulas provided more than enough variation to add character to the movements: `easeOutBack`, `easeInOutBack` and `easeOutQuint`.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d415f43f-fe13-41ac-b698-33500702c958/04-easing-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d415f43f-fe13-41ac-b698-33500702c958/04-easing-opt.gif" alt="easing" width="500" height="301" /></a><figcaption>Figure 4. A visual comparison of animations with and without easing. Note that using any variation of <code>easingBack</code> will influence the transformations to some extent. </figcaption></figure>

## Let’s Get Started

### Preparing the Assets

Though the illustration app landscape has matured in recent years, with [Sketch](https://www.sketchapp.com/) and [Inkscape](https://inkscape.org/en/) becoming increasingly popular, we opted to create our SVGs in Adobe Illustrator.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a417154-a0bf-4c82-b874-ec9ab1472015/05-breakdown-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a417154-a0bf-4c82-b874-ec9ab1472015/05-breakdown-opt.jpg" alt="breakdown" width="500" height="301" /></a><figcaption>Figure 5. A breakdown of the elements that make up the final animation.</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b82dd322-e260-4a77-adc4-1b2a0dd4f517/06-illustrator-layers-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b82dd322-e260-4a77-adc4-1b2a0dd4f517/06-illustrator-layers-opt.jpg" alt="illustrator layers" width="500" height="301" /></a><figcaption>Figure 6. Illustrator automatically creates IDs from layer names when exporting to SVG.</figcaption></figure>

Before you export to SVG, **group and label every layer**. Illustrator will automatically creates IDs from the layer names during the exporting process. For every animated element, the output should look similar to the XML shown below. Note that even if an element doesn’t have any children, it still needs to be grouped under a `g` tag. This is in preparation for [adding SVG transform groups](#svg-transform-groups), explained later on.</p>

<pre><code class="language-markup">&lt;g id=&quot;zipper&quot;&gt;
&lt;path fill=&quot;#272C40&quot; d=&quot;…&quot;/&gt;
&lt;/g&gt;</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50126440-b3cb-4349-a116-9f5ab6f61549/07-illustrator-exporting-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50126440-b3cb-4349-a116-9f5ab6f61549/07-illustrator-exporting-opt.jpg" alt="illustrator exporting" width="500" height="301" /></a><figcaption>Figure 7. The SVG export settings used. We unchecked “responsive” because the animation units are pixel-based.</figcaption></figure>

### Handling Masks

You may have noticed the `<Clip Group>` layer in figure 6\. These are essentially clipping masks created in Illustrator. When exported to SVG, they automatically become predefined `clipPaths` that can be used to mask elements in the exact same way.</p>

<pre><code class="language-markup">&lt;g&gt;
&lt;defs&gt;
  &lt;rect id=&quot;SVGID_1_&quot; x=&quot;235&quot; y=&quot;-106.3&quot; width=&quot;500&quot; height=&quot;309&quot;/&gt;
&lt;/defs&gt;

&lt;clipPath id=&quot;SVGID_2_&quot;&gt;
  &lt;use xlink:href=&quot;#SVGID_1_&quot;  overflow=&quot;visible&quot;/&gt;
&lt;/clipPath&gt;

&lt;g id=&quot;strap-right&quot; clip-path=&quot;url(#SVGID_2_)&quot;&gt;
  &lt;path fill=&quot;#93481F&quot; stroke=&quot;#000000&quot; stroke-width=&quot;1.5&quot; stroke-miterlimit=&quot;10&quot; d=&quot;…&quot;
    /&gt;
&lt;/g&gt;
&lt;/g&gt;</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/200d70db-f12c-4b40-a57a-a4df2da8e442/08-clippath-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/200d70db-f12c-4b40-a57a-a4df2da8e442/08-clippath-opt.gif" alt="clipPath" width="500" height="301" /></a><figcaption>Figure 8. The use of <code>clipPath</code> to hide the belt straps before animation. </figcaption></figure>

## Prototype, Prototype, Prototype

With the assets prepared, we were ready to build. We began an iterative process of creating prototypes and testing various technologies to find a solution. Here, we’ll briefly outline each of our attempts, the pros and cons, and why we pivoted from one solution to the next.</p>

### CSS and Velocity.js

Our initial attempts at using CSS to create animations were promising. We believed that with hardware-accelerated transformations, the animations would run smoothly and the implementation would be straightforward, without the need for external libraries. While we were able to create a functioning version in Chrome, the solution **failed in all other browsers**.

Firefox would not respect the [`transform-origin` property of SVGs](https://bugzilla.mozilla.org/show_bug.cgi?id=923193), while Internet Explorer’s support for SVG CSS animation is [completely non-existent](https://stackoverflow.com/questions/24302615/css3-animation-is-not-working). Lastly, with CSS and JavaScript being so tightly coupled, we found ourselves jumping back and forth between too many files for the solution to be considered elegant.

In a similar vein, we ran into the same problems with [Velocity.js](https://julian.com/research/velocity/). Because the animation engine also uses CSS transformations, the Firefox and Internet Explorer issues remained unresolved.</p>

### GSAP

[GSAP](https://greensock.com/gsap) has been an industry standard since its Flash days, and its popularity has risen even more so since being ported to JavaScript. With its chainable syntax, extensive SVG support and unparalleled performance, GSAP was an obvious contender — save for one issue: It was **overkill**. Importing TweenMax and TimelineMax immediately doubled the size of our project and proved to be excessive. [Chris Gannon](https://twitter.com/ChrisGannon/status/757997386035789824) let us know that TimelineMax is included in TweenMax and combined is only 37kb, a misunderstanding on our end.</p>

### Snap.svg

In our final attempt, we used [Snap.svg](https://snapsvg.io/), the successor to [Raphael](https://raphaeljs.com/). Snap offers **extensive functionality in DOM manipulation but the bare minimum in animation support**. Though we recognized this as a setback, the deficiencies led us to roll our own JavaScript to fill in the gaps. This resulted in a lightweight solution that was still capable of achieving the fidelity of animations we were striving for.</p>

### Mo.js, Anime and Web Animations API

Since writing this article, three very promising SVG animation libraries have been gaining traction in the community: [Mo.js](https://mojs.io/), [Anime](https://anime-js.com) and the [Web Animations API](https://github.com/web-animations/web-animations-js). If we get the chance to revisit the problem, these alternatives would definitely be taken into consideration. Nonetheless, the concepts behind this article should be transferable to any animation library you wish to use.</p>

## The Scaffold

We’ll begin by importing a basic style sheet and the Snap.svg library into our project. We’ll also include a port of [Robert Penner’s easing functions](https://github.com/overjase/snap-easing/blob/master/README) for later use.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9e01329-3cb1-4e82-8893-509045905ac5/09-folder-structure-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9e01329-3cb1-4e82-8893-509045905ac5/09-folder-structure-opt.jpg" alt="folder structure" width="500" height="301" /></a><figcaption>Figure 9. The final folder structure of our project. The  “Hello world” scaffold begins with just the highlighted files.</figcaption></figure>

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html lang=&quot;en&quot; class=&quot;no-js&quot;&gt;
&lt;head&gt;
  &lt;meta charset=&quot;UTF-8&quot; /&gt;
  &lt;meta http-equiv=&quot;X-UA-Compatible&quot; content=&quot;IE=edge,chrome=1&quot;&gt;
  &lt;meta name=&quot;viewport&quot; content=&quot;width=device-width, initial-scale=1.0&quot;&gt;
  &lt;title&gt;The Illusion of Life: An SVG Animation Case Study&lt;/title&gt;

  &lt;!-- Styles --&gt;
  &lt;link rel=&quot;stylesheet&quot; type=&quot;text/css&quot; href=&quot;css/style.css&quot; /&gt;

  &lt;!-- Libraries --&gt;
  &lt;script src=&quot;js/libs/snap.svg.min.js&quot;&gt;&lt;/script&gt;
  &lt;script src=&quot;js/libs/snap.svg.easing.min.js&quot;&gt;&lt;/script&gt;&lt;/html&gt;
&lt;/head&gt;
&lt;/html&gt;</code></pre>

<pre><code class="language-css">/* Full screen */
html, body {
  position: relative;
  width: 100%;
  height: 100%;
  margin: 0;
  overflow: hidden;
  background-color: #E6E6E6;
  font-family: sans-serif;
}

/* Centered canvas */
#canvas {
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translateX(-50%) translateY(-50%);
  -ms-transform: translateX(-50%) translateY(-50%);
  transform: translateX(-50%) translateY(-50%);
  overflow: hidden;
}</code></pre>

## Hello World

*   “[Hello World](https://github.com/hellomichael/svgAnimation/tree/hello-world),” GitHub

“Hello world” — a small, simple win. For us, that just meant getting something on the screen. We first instantiated a new `Snap` object, with a DOM ID representing our canvas. We use the [`Snap.load` function](https://snapsvg.io/docs/#Snap.load) to indicate the external SVG source and an anonymous callback that will append the nodes to the DOM tree.</p>

<pre><code class="language-markup">&lt;body&gt;
&lt;div id=&quot;canvas&quot;&gt;&lt;/div&gt;

&lt;script&gt;
  (function() {
    var s = Snap('#canvas');

    Snap.load(&quot;svg/backpack.svg&quot;, function (data) {
      s.append(data);
    });
  })();
&lt;/script&gt;
&lt;/body&gt;
</code></pre>

## Making A Simple Plugin

*   [Plugin](https://github.com/hellomichael/svgAnimation/tree/plugin), GitHub

To create a reusable component for multiple animations, we create a “plugin” using the **prototype pattern**. Using an **immediately invoked function expression** (IIFE) ensures data encapsulation, while still adding `SVGAnimation` to the global namespace. If we place the code we have so far into a separate `init` function, we will have the basis for `SVGAnimation`.</p>

<pre><code class="language-javascript">; (function(window) {
'use strict';

var svgAnimation = function () {
  var self = this;
  self.init();
};

svgAnimation.prototype = {
  constructor: svgAnimation,

  init: function() {
    var s = Snap('#canvas');

    Snap.load(&quot;svg/backpack.svg&quot;, function (data) {
      s.append(data);
    });
  }
};

// Add to global namespace
window.svgAnimation = svgAnimation;
})(window);</code></pre>

See the Pen [Simple Plugin](https://codepen.io/hellomichael/pen/aZJMmr/) by Michael Ngo ([@hellomichael](https://codepen.io/hellomichael)) on [CodePen](https://codepen.io).</p>

## Adding Options

*   [Options](https://github.com/hellomichael/svgAnimation/tree/options), GitHub

Dissecting `Snap.load`, we can see two potential parameters that can be passed in as options, a canvas and an external SVG source. Let’s create a separate `loadSVG` function to handle just that.</p>

<pre><code class="language-javascript">/*
Loads the SVG into the DOM
@param {Object}   canvas
@param {String}   svg
*/
loadSVG: function(canvas, data) {
Snap.load(svg, function(data) {
  canvas.append(svg);
});
}</code></pre>

### Objects as Parameters

Now we need a way to pass these options into `SVGAnimation`. There are several ways to do this, the standard way being to pass individual parameters.</p>

<pre><code class="language-javascript">var backpack = new svgAnimation(Snap('#canvas'), 'svg/backpack.svg');</code></pre>

But there’s a better solution. By passing in objects instead, the code becomes not only more readable, but also more flexible. We no longer need to keep track of the order; we can make parameters optional; and we can also reuse the object later. So, let’s rewrite the previous snippet, passing in an `options` object instead.</p>

<pre><code class="language-javascript">var backpack = new svgAnimation({
canvas:       new Snap('#canvas'),
svg:          'svg/backpack.svg'
});</code></pre>

### Merging Objects

Now that we have the `options` object, we need to make the values accessible to the rest of the plugin. But before we do this, let’s merge the passed-in object with our own defaults. Even though we’ve chosen to set both values to `null`, we’ll still include them as a reference for the type of values we expect to receive.</p>

<pre><code class="language-javascript">svgAnimation.prototype = {
constructor: svgAnimation,

options: {
  canvas:     null,
  svg:        null
}
};</code></pre>

With the defaults now set, we’ll use an `extend` function to merge both objects. Essentially, the function will loop through all of the properties of one object and copy them over to another.</p>

<pre><code class="language-javascript">/*
Merges two objects
@param  {Object}  a
@param  {Object}  b
@return {Object}  sum
https://stackoverflow.com/questions/11197247/javascript-equivalent-of-jquerys-extend-method
*/
function extend(a, b) {
for (var key in b) {
  if (b.hasOwnProperty(key)) {
    a[key] = b[key];
  }
}

return a;
}</code></pre>

With the `extend` function defined, let’s amend the `SVGAnimation` constructor. One thing you’ll notice is that `self` is set to `this`. We’ll cache the original `this` to ensure that inner scopes have access to the current object’s data and methods.</p>

<pre><code class="language-javascript">var svgAnimation = function (options) {
var self = this;
self.options = extend({}, self.options);
extend(self.options, options);
self.init();
}</code></pre>

Lastly, we’ll update `init` to call `loadSVG`, passing in the `canvas` and `svg` reference we set during instantiation.</p>

<pre><code class="language-javascript">init: function() {
var self = this;

self.loadSVG(self.options.canvas, self.options.svg);
}</code></pre>

See the Pen [Adding Options](https://codepen.io/hellomichael/pen/oLZVYg/) by Michael Ngo ([@hellomichael](https://codepen.io/hellomichael)) on [CodePen](https://codepen.io).</p>

## Hardcoded Prototype

*   [Hardcoded prototype](https://github.com/hellomichael/svgAnimation/tree/hard-coded), GitHub

### Adding SVG Transformation Groups

As mentioned earlier, Snap.svg’s animation engine is quite primitive and, just like CSS, only supports transform strings as a single request. This means that if you’re looking to animate more than one type of transformation, it must happen either sequentially or all at once (sharing duration and easing). Though not the most elegant solution, adding extra nodes to the DOM tree solves this problem. With a separate grouped element for each translate, rotate and scale transformation, we can now independently control each tween. The example that best illustrates this use case is the zipper, which also serves as our initial prototype.

We begin by passing the `zipper` element to the `createTransformGroup` function, which we then go on to define.</p>

<pre><code class="language-javascript">var $zipper = canvas.select(&quot;#zipper&quot;);
self.createTransformGroup($zipper);</code></pre>

After we’ve selected all child nodes, we can use the [`Snap.g` function](https://snapsvg.io/docs/#Paper.g) to nest the contents within each respective transform group.</p>

<pre><code class="language-javascript">/*
Create scale, rotate and transform groups around an SVG DOM node
@param {object} Snap element
*/

createTransformGroup: function(element) {
if (element.node) {
  var childNodes = element.selectAll('*');

  element.g().attr('class', 'translate')
    .g().attr('class', 'rotate')
    .g().attr('class', 'scale')
    .append(childNodes);
}
}</code></pre>

This results in the creation of independent transformation groups, which we can target in our animations.</p>

<pre><code class="language-markup">&lt;!-- Old node --&gt;
&lt;g id=&quot;zipper&quot;&gt;
&lt;path fill=&quot;#272C40&quot; d=&quot;…&quot;/&gt;
&lt;/g&gt;

&lt;!-- New node --&gt;
&lt;g id=&quot;zipper&quot;&gt;
&lt;g class=&quot;translate&quot;&gt;
  &lt;g class=&quot;rotate&quot;&gt;
    &lt;g class=&quot;scale&quot;&gt;
      &lt;path fill=&quot;#272C40&quot; d=&quot;…&quot;&gt;&lt;/path&gt;
    &lt;/g&gt;
  &lt;/g&gt;
&lt;/g&gt;
&lt;/g&gt;</code></pre>

### A Snap.svg Animation

We’re finally ready to animate our first element. Snap.svg provides two functions to do this: [`transform`](https://snapsvg.io/docs/#Element.transform) and [`animate`](https://snapsvg.io/docs/#Snap.animate). We’ll use `transform` to place the animation at the first keyframe, and then use `animate` to get us to the last.

Snap.svg supports standard SVG transform notation, but we’ve opted to use **transform strings** as a means to set parameters instead. Explanations are sparse on the official website, but [legacy documentation](https://raphaeljs.com/reference.html#Element.transform) can be found on Raphael’s. The initial uppercase letter is an abbreviation of the transformation. The parameters `x`, `y` and `angle` represent the values we are animating to, with `cx` and `cy` being the center of origin.</p>

<pre><code class="language-javascript">// Scale
Snap.animate({transform: 'S x y cx cy'}, duration, easing, callback);

// Rotation
Snap.animate({transform: 'R angle cx cy'}, duration, callback);

// Translate
Snap.animate({transform: 'T x y'}, duration, callback);</code></pre>

### Calculating Origins

We ran into an interesting problem with defining origins, however. In Snap.svg, the `animate` and `transform` functions only accept parameters as pixel values, making it extremely difficult to measure. Ideally, as our brief outlined, we wanted to define the origin as a combination of `top`, `right`, `bottom`, `left` and `center`.

Fortunately, Snap.svg provides [getBBox](https://snapsvg.io/docs/#Element.getBBox), which measures the bounding box of any given element, returning a multitude of descriptors, including the values we’re searching for. We’ll write two functions, `getOriginX` and `getOriginY`, that accept a `bBox` object and a `direction` string as parameters, returning pixel values as needed.</p>

<pre><code class="language-javascript">/*
Translates the horizontal origin from a string to pixel value
@param {Object}     Snap bBox
@param {String}     &quot;left&quot;, &quot;right&quot;, &quot;center&quot;
@return {Object}    pixel value
*/

getOriginX: function (bBox, direction) {
if (direction === 'left') {
  return bBox.x;
}

else if (direction === 'center') {
  return bBox.cx;
}

else if (direction === 'right') {
  return bBox.x2;
}
},

/*
Translates the vertical origin from a string to pixel value
@param {Object}     Snap bBox
@param {String}     &quot;top&quot;, &quot;bottom&quot;, &quot;center&quot;
@return {Object}    pixel value
*/

getOriginY: function (bBox, direction) {
if (direction === 'top') {
  return bBox.y;
}

else if (direction === 'center') {
  return bBox.cy;
}

else if (direction === 'bottom') {
  return bBox.y2;
}
}</code></pre>

### Animation in Practice

Let’s see this all in practice with a scaling animation. We first select the corresponding transform group using its class name, scale it down until it’s hidden, and then animate it back to its original size. You’ll notice that we are scaling from the top of the zipper, with a duration of 400 milliseconds, and setting the custom easing to `easeOutBack`.</p>

<pre><code class="language-javascript">// Scale Tween
var $scaleElement = $zipper.select('.scale');
var scaleBBox = $scaleElement.getBBox();
$scaleElement.transform('S' + 0 + ' ' + 0 + ' ' + self.getOriginX(scaleBBox, 'center') + ' ' + self.getOriginY(scaleBBox, 'top'));
$scaleElement.animate({transform: 'S' + 1 + ' ' + 1 + ' ' + self.getOriginX(scaleBBox, 'center') + ' ' + self.getOriginY(scaleBBox, 'top')}, 400, mina['easeOutBack']);
</code></pre>

Rotation follows the same pattern, with a few complexities. In this case, we have three tweens that play consecutively. When each animation is finished, we use its callback function to play the next animation in queue.</p>

<pre><code class="language-javascript">// Rotate Tween
var $rotateElement = $zipper.select('.rotate');
var rotateBBox = $rotateElement.getBBox();
$rotateElement.transform('R' + 45 + ' ' + rotateBBox.cx + ' ' + rotateBBox.cy);

$rotateElement.animate({ transform: 'R' + -60 + ' ' + self.getOriginX(rotateBBox, 'center') + ' ' + self.getOriginY(rotateBBox, 'top')}, 400, mina['easeOutBack'], function() {
$rotateElement.animate({ transform: 'R' + 30 + ' ' + self.getOriginX(rotateBBox, 'center') + ' ' + self.getOriginY(rotateBBox, 'top')}, 400, mina['easeOutBack'], function() {
  $rotateElement.animate({ transform: 'R' + 0 + ' ' + self.getOriginX(rotateBBox, 'center') + ' ' + self.getOriginY(rotateBBox, 'top')}, 400, mina['easeInOutBack']);
});
});</code></pre>

The translate tween mimics both scale and rotation, with one key difference. Because the translate animation doesn’t begin immediately, we use `setTimeout` to delay the starting time by 400 milliseconds.</p>

<pre><code class="language-javascript">// Translate Tween
var $translateElement = $zipper.select('.translate');
$translateElement.transform('T' + 110 + ' ' + 0);

setTimeout(function() {
$translateElement.animate({ transform: 'T' + 0 + ' ' + 0 }, 600, mina['easeOutQuint']);
}, 400);</code></pre>

See the Pen [Hard-coded Prototype](https://codepen.io/hellomichael/pen/KMWENR/) by Michael Ngo ([@hellomichael](https://codepen.io/hellomichael)) on [CodePen](https://codepen.io).</p>

## Keyframes Are Key

At this point, you might be wondering, “Well, that was fairly complex for such a simple animation.” We wouldn’t disagree.

Our goal was to create a **data-driven** process to rapidly prototype animations. By creating a separate tween class and introducing the concept of keyframes, we can go from code like this…

<pre><code class="language-javascript">// Translate Tween
var $translateElement = $zipper.select('.translate');
$translateElement.transform('T' + 110 + ' ' + 0);

setTimeout(function() {
$translateElement.animate({ transform: 'T' + 0 + ' ' + 0 }, 600, mina['easeOutQuint']);
}, 400);</code></pre>

… to code like this:

<pre><code class="language-javascript">// Translate Tween
new svgTween({
element: $zipper.select('.translate'),
keyframes: [
  {
    &quot;step&quot;: 2,
    &quot;x&quot;: 110,
    &quot;y&quot;: 0
  },

  {
    &quot;step&quot;: 5,
    &quot;x&quot;: 0,
    &quot;y&quot;: 0,
    &quot;easing&quot;: &quot;easeOutQuint&quot;
  }
],
duration: 2000/10
});</code></pre>

As we subdivide each animation into individual steps, we begin to see how this format might make prototyping easier. Let’s break down the parameters of this translate tween and explain where these numbers come from.

In our original code, you might have noticed that the durations and delays were all divisible by a factor of 200 milliseconds. That wasn’t a coincidence. If the entirety of an animation lasts 2000 milliseconds and consists of 10 steps, we simply need to divide the former by the latter to calculate the duration of a single step. We can now use the same logic to determine why the keyframes start at step 2 and end at step 5\. The `setTimeout`, which lasts 400 milliseconds, corresponds to two steps, the initial delay. Furthermore, the duration of the animation is 600 milliseconds, which is calculated to be three steps, the difference between steps 2 and 5.</p>

## svgTween: Translate

*   [Tween translate](https://github.com/hellomichael/svgAnimation/tree/tween-translate), GitHub

With the output of our black box defined, let’s write the functionality for the `SVGTween` class. Using the same pattern as `SVGAnimation`, we’re able to quickly flesh out a basic scaffold.</p>

<pre><code class="language-javascript">/*
svgTween.js v1.0.0
Licensed under the MIT license.
https://www.opensource.org/licenses/mit-license.php

Copyright 2015, Smashing Magazine
https://www.smashingmagazine.com/
https://www.hellomichael.com/
*/

; (function(window) {
'use strict';

var svgTween = function (options) {
  var self = this;
  self.options = extend({}, self.options);
  extend(self.options, options);
  self.init();
};

svgTween.prototype = {
  constructor: svgTween,

  options: {
    element:    null,
    keyframes:  null,
    duration:   null
  },

  init: function () {
    var self = this;
  }
};

/*
  Merges two objects
  @param {Object} a
  @param {Object} b
  @return {Object} sum
  https://stackoverflow.com/questions/11197247/javascript-equivalent-of-jquerys-extend-method
*/
function extend(a, b) {
  for (var key in b) {
    if (b.hasOwnProperty(key)) {
      a[key] = b[key];
    }
  }

  return a;
}

// Add to namespace
window.svgTween = svgTween;
})(window);</code></pre>

Using the same algorithm as before, we’ll set the animation to the first initial hidden state, then animate from there. Instead of using Snap.svg’s `transform` and `animate` functions, we’ll rewrite them as `resetTween` and `playTween` to handle keyframes instead.

`resetTween` will accept an element and the `keyframes` array. The only difference is that, instead of directly setting the values in the `transform` string, we’ll use the values in the first `keyframe`.</p>

<pre><code class="language-javascript">/*
Resets the animation to the first keyframe

@param {Object} element
@param {Array}  keyframes
*/
resetTween: function (element, keyframes) {
var self = this;

var translateX = keyframes[0].x;
var translateY = keyframes[0].y;

element.transform('T' + translateX + ',' + translateY);
}</code></pre>

Because Snap.svg doesn’t provide chainable animation methods, we’ll have to use callbacks for consecutive animations.</p>

<pre><code class="language-javascript">Snap.animation(attr, duration, [easing], [callback]);
</code></pre>

However, this instantly becomes unruly if we have more than two keyframes, essentially sending us into a form of **callback hell**. To handle this problem, we’ll implement `playTween` as a **recursive function**, allowing us to loop through animations without necessarily having to nest them.

Let’s start by defining the parameters of our animation. Just as with `resetTween`, we’ll set the values in our `transform` string to the keyframe values. Easing is done very much in the same way. Duration is either set to the pause leading up to the first animation or calculated as the span of time between steps.</p>

<pre><code class="language-javascript">/*
Recursively loop through keyframes to create pauses or tweens

@param {Object} element
@param {Array}  keyframes
@param {Int}    duration
@param {Int}    index
*/
playTween: function(element, keyframes, duration, index) {
var self = this;

// Set keyframes we’re transitioning to
var translateX = keyframes[index].x;
var translateY = keyframes[index].y;

// Set easing parameter
var easing = mina[keyframes[index].easing];

// Set duration as an initial pause or the difference of steps between keyframes
var newDuration = index ? ((keyframes[index].step - keyframes[(index-1)].step) * duration) : (keyframes[index].step * duration);
}</code></pre>

With the parameters prepared, let’s write conditional statements that pause, play or kill an animation. Our first conditional statement checks whether the animation begins immediately at step 0\. If it does, we’ll move on, because the `transform` function already handles this first keyframe. If we tried to animate to the same values as `resetTween`, we would sometimes see a brief flicker, a bug that took us ages to find. The next two conditional statements check whether we should delay the animation or begin playing tweens. The one thing to note is the use of nested conditional statements that check whether the recursive function should fire again. Without them, `playTween` could run indefinitely.</p>

<pre><code class="language-javascript">// Play first tween immediately if starts on step 0
if (index === 0 &amp;&amp; keyframes[index].step === 0) {
self.playTween(element, keyframes, duration, (index + 1));
}

// Or pause tween if initial keyframe
else if (index === 0 &amp;&amp; keyframes[index].step !== 0) {
setTimeout(function() {
  if (index !== (keyframes.length - 1)) {
    self.playTween(element, keyframes, duration, (index + 1));
  }
}, newDuration);
}

// Or animate tweens if keyframes exist
else {
element.animate({
  transform: 'T' + translateX + ' ' + translateY
}, newDuration, easing, function() {
  if (index !== (keyframes.length - 1)) {
    self.playTween(element, keyframes, duration, (index + 1));
  }
});
}</code></pre>

The last step is to update our `init` function to call `resetTween` and `playTween`.</p>

<pre><code class="language-javascript">init: function () {
var self = this;

self.resetTween(self.options.element, self.options.keyframes);
self.playTween(self.options.element, self.options.keyframes, self.options.duration, 0);
}</code></pre>

See the Pen [svgTween - Translate](https://codepen.io/hellomichael/pen/jrBJVz/) by Michael Ngo ([@hellomichael](https://codepen.io/hellomichael)) on [CodePen](https://codepen.io).</p>

## svgTween: Rotation And Scale

*   [Tween: rotate and scale](https://github.com/hellomichael/svgAnimation/tree/tween-rotate-scale), GitHub

With our zipper now moving from right to left, it’s time to add rotation and scale to the mix. Let’s amend our options to include `type`, `originX` and `originY`. Because `svgTween` will now handle all transformations, we’ll include a `type` variable to specify which one. We’ll also track `originX` and `originY` to set the correct `transform-origin`s for scale and rotation. Translation is never affected by `transform-origin`, so it is always set to `center center` by default.</p>

<pre><code class="language-javascript">options: {
element:    null,
type:       null,
keyframes:  null,
duration:   null,
originX:    null,
originY:    null
}</code></pre>

Let’s update `resetTween` and `playTween` to handle these new values. We’ll first check the type and then construct the respective `transform` strings. We’ll create separate `translateX`, `translateY`, `rotationAngle`, `scaleX` and `scaleY` variables, so that it is visually identifiable how our transform strings are generated.</p>

<pre><code class="language-javascript">/*
Resets the animation to the first keyframe

@param {Object} element
@param {String} type - &quot;scale&quot;, &quot;rotate&quot;, &quot;translate&quot;
@param {Array}  keyframes
@param {String} originX - &quot;left&quot;, &quot;right&quot;, &quot;center&quot;
@param {String} originY - &quot;top&quot;, &quot;bottom&quot;, &quot;center&quot;
*/
resetTween: function (element, type, keyframes, originX, originY) {
var transform, translateX, translateY, rotationAngle, scaleX, scaleY;

if (type === 'translate') {
  translateX = keyframes[0].x;
  translateY = keyframes[0].y;
  transform = 'T' + translateX + ' ' + translateY;
}

else if (type === 'rotate') {
  rotationAngle = keyframes[0].angle;
  transform = 'R' + rotationAngle + ' ' + originX + ' ' + originY;
}

else if (type === 'scale') {
  scaleX = keyframes[0].x;
  scaleY = keyframes[0].y;
  transform = 'S' + scaleX + ' ' + scaleY + ' ' + originX + ' ' + originY;
}

element.transform(transform);</code></pre>

We’ll mimic the same pattern in `playTween`, replacing the relevant index from the recursive function. We’ll also update the `function` calls with the new `type`, `originX` and `originY` parameters.</p>

<pre><code class="language-javascript">/*
Recursively loop through keyframes to create pauses or tweens

@param {Object} element
@param {String} type - &quot;scale&quot;, &quot;rotate&quot;, &quot;translate&quot;
@param {Array}  keyframes
@param {String} originX - &quot;left&quot;, &quot;right&quot;, &quot;center&quot;
@param {String} originY - &quot;top&quot;, &quot;bottom&quot;, &quot;center&quot;
@param {Int}    duration
@param {Int}    index
*/
playTween: function(element, type, keyframes, originX, originY, duration, index) {
var self = this;

// Set keyframes we're transitioning to
var transform, translateX, translateY, rotationAngle, scaleX, scaleY;

if (type === 'translate') {
  translateX = keyframes[index].x;
  translateY = keyframes[index].y;
  transform = 'T' + translateX + ' ' + translateY;
}

else if (type === 'rotate') {
  rotationAngle = keyframes[index].angle;
  transform = 'R' + rotationAngle + ' ' + originX + ' ' + originY;
}

else if (type === 'scale') {
  scaleX = keyframes[index].x;
  scaleY = keyframes[index].y;
  transform = 'S' + scaleX + ' ' + scaleY + ' ' + originX + ' ' + originY;
}

// Set easing parameter
var easing = mina[keyframes[index].easing];

// Set duration as an initial pause or the difference of steps between keyframes
var newDuration = index ? ((keyframes[index].step - keyframes[(index-1)].step) * duration) : (keyframes[index].step * duration);

// Skip first tween if animation immediately starts on step 0
if (index === 0 &amp;&amp; keyframes[index].step === 0) {
  self.playTween(element, type, keyframes, originX, originY, duration, (index + 1));
}

// Or pause tween if initial keyframe
else if (index === 0 &amp;&amp; keyframes[index].step !== 0) {
  setTimeout(function() {
    if (index !== (keyframes.length - 1)) {
      self.playTween(element, type, keyframes, originX, originY, duration, (index + 1));
    }
  }, newDuration);
}

// Or animate tweens if keyframes exist
else {
  element.animate({
    transform: transform
  }, newDuration, easing, function() {
    if (index !== (keyframes.length - 1)) {
      self.playTween(element, type, keyframes, originX, originY, duration, (index + 1));
    }
  });
}
}</code></pre>

Lastly, we’ll update our `init` function to set `type`, `originX` and `originY`, before calling `resetTween` and `playTween`. We can set `type` simply by adopting the class of the passed-in element. At this point, we can transfer over `getOriginX` and `getOriginY` from `SVGAnimation`. We then use a **ternary operator** to set our origin, defaulting to `center` if the values are undefined.</p>

<pre><code class="language-javascript">init: function () {
var self = this;

// Set type
self.options.type = self.options.element.node.getAttributeNode('class').value;

// Set bbox to specific transform element (.translate, .scale, .rotate)
var bBox = self.options.element.getBBox();

// Set origin as specified or default to center
self.options.originX = self.options.keyframes[0].cx ? self.getOriginX(bBox, self.options.keyframes[0].cx) : self.getOriginX(bBox, 'center');
self.options.originY = self.options.keyframes[0].cy ? self.getOriginY(bBox, self.options.keyframes[0].cy) : self.getOriginY(bBox, 'center');

// Reset and play tween
self.resetTween(self.options.element, self.options.type, self.options.keyframes, self.options.originX, self.options.originY);
self.playTween(self.options.element, self.options.type, self.options.keyframes, self.options.originX, self.options.originY, self.options.duration, 0);
}</code></pre>

Let’s finalize our zipper animation by instantiating new tweens for both rotation and scale. As with translate, we can calculate the keyframes and duration by the number of steps and overall length of the animation. In reality, we defined all of these parameters much more organically: by viewing the animations as they progressed and constantly fine-tuning the numbers.</p>

<pre><code class="language-javascript">// Rotate tween
new svgTween({
element: $zipper.select('.rotate'),
keyframes: [
  {
    &quot;step&quot;: 0,
    &quot;angle&quot;: 45,
    &quot;cy&quot;: &quot;top&quot;
  },

  {
    &quot;step&quot;: 2,
    &quot;angle&quot;: -60,
    &quot;easing&quot;: &quot;easeOutBack&quot;
  },

  {
    &quot;step&quot;: 4,
    &quot;angle&quot;: 30,
    &quot;easing&quot;: &quot;easeOutQuint&quot;
  },

  {
    &quot;step&quot;: 6,
    &quot;angle&quot;: 0,
    &quot;easing&quot;: &quot;easeOutBack&quot;
  }
],
duration: duration
});</code></pre>

<pre><code class="language-javascript">// Scale tween
new svgTween({
element: $zipper.select('.scale'),
keyframes: [
  {
    "step": 0,
    "x": 0,
    "y": 0,
    "cy": "top"
  },

  {
    "step": 2,
    "x": 1,
    "y": 1,
    "easing": "easeOutBack"
  }
],
duration: duration
});</code></pre>

See the Pen [svgTween: Rotation and Scale](https://codepen.io/hellomichael/pen/ezvXBQ/) by Michael Ngo ([@hellomichael](https://codepen.io/hellomichael)) on [CodePen](https://codepen.io).</p>

## JSON Config

*   [JSON](https://github.com/hellomichael/svgAnimation/tree/json), GitHub

The very last step of our build is to extract the hardcoded values from `SVGAnimation` and add them to our constructor instead. Let’s add the keyframes, `duration` and number of `steps` in the instantiation.</p>

<pre><code class="language-javascript">(function() {
var backpack = new svgAnimation({
  canvas:       new Snap('#canvas'),
  svg:          'svg/backpack.svg',
  data:         'json/backpack.json',
  duration:     2000,
  steps:        10
});
})();</code></pre>

By passing in a JSON file to define keyframes, a designer can immediately create a prototype without having to dive into documentation. In fact, this concept could be completely library-agnostic if you replace Snap.svg with GSAP, Mo.js or the Web Animations API.

The JSON file is formatted into separate tweens, consisting of element IDs and keyframes. We include the zipper animation as an example, but the `backpack.json` file includes arrays for all of the elements (zipper, pockets, logo, etc.).</p>

<pre><code class="language-javascript">{
&quot;animations&quot;: [
  {
    &quot;id&quot;: &quot;#zipper&quot;,
    &quot;keyframes&quot;: {
      &quot;translateKeyframes&quot;: [
        {
          &quot;step&quot;: 6,
          &quot;x&quot;: 110,
          &quot;y&quot;: 0
        },

        {
          &quot;step&quot;: 9,
          &quot;x&quot;: 0,
          &quot;y&quot;: 0,
          &quot;easing&quot;: &quot;easeOutQuint&quot;
        }
      ],

      &quot;rotateKeyframes&quot;: [
        {
          &quot;step&quot;: 4,
          &quot;angle&quot;: 45,
          &quot;cy&quot;: &quot;top&quot;
        },

        {
          &quot;step&quot;: 6,
          &quot;angle&quot;: -60,
          &quot;easing&quot;: &quot;easeOutBack&quot;
        },

        {
          &quot;step&quot;: 8,
          &quot;angle&quot;: 30,
          &quot;easing&quot;: &quot;easeOutQuint&quot;
        },

        {
          &quot;step&quot;: 10,
          &quot;angle&quot;: 0,
          &quot;easing&quot;: &quot;easeOutBack&quot;
        }
      ],

      &quot;scaleKeyframes&quot;: [
        {
          &quot;step&quot;: 4,
          &quot;x&quot;: 0,
          &quot;y&quot;: 0,
          &quot;cy&quot;: &quot;top&quot;
        },

        {
          &quot;step&quot;: 6,
          &quot;x&quot;: 1,
          &quot;y&quot;: 1,
          &quot;easing&quot;: &quot;easeOutBack&quot;
        }
      ]
    }
  }
]
}</code></pre>

<pre><code class="language-javascript">options: {
data:                 null,
canvas:               null,
svg:                  null,
duration:             null,
steps:                null
}</code></pre>

The details of how to [load a JSON file](https://codepen.io/KryptoniteDove/post/load-json-file-locally-using-pure-javascript) are beyond the scope of this article, but what’s significant is the use of a callback function to return the JSON data for future use — in our case, passing the animations array to `loadSVG`.

  <pre><code class="language-javascript">/*
Get JSON data and populate options
@param {Object}   data
@param {Function} callback
*/
loadJSON: function(data, callback) {
var self = this;

// XML request
var xobj = new XMLHttpRequest();
xobj.open('GET', data, true);

xobj.onreadystatechange = function() {
  // Success
  if (xobj.readyState === 4 &amp;&amp; xobj.status === 200) {
    var json = JSON.parse(xobj.responseText);

    if (callback &amp;&amp; typeof(callback) === &quot;function&quot;) {
      callback(json);
    }
  }
};

xobj.send(null);
}</code></pre>

We’re now able to update `loadSVG` to loop through our `animations` array, creating `svgTweens` dynamically. If any of `translateKeyframes`, `rotateKeyframes` or `scaleKeyframes` are defined, we instantiate a new `svgTween`, passing in the keyframes and duration from our `options` file.</p>

<pre><code class="language-javascript">loadSVG: function(canvas, svg, animations, duration) {
var self = this;

Snap.load(svg, function(data) {
  // Placed SVG into the DOM
  canvas.append(data);

  // Create tweens for each animation
  animations.forEach(function(animation) {
    var element = canvas.select(animation.id);

    // Create scale, rotate and transform groups around an SVG node
    self.createTransformGroup(element);

    // Create tween based on keyframes
    if (animation.keyframes.translateKeyframes) {
      self.options.tweens.push(new svgTween({
        element: element.select('.translate'),
        keyframes: animation.keyframes.translateKeyframes,
        duration: duration
      }));
    }

    if (animation.keyframes.rotateKeyframes) {
      self.options.tweens.push(new svgTween({
        element: element.select('.rotate'),
        keyframes: animation.keyframes.rotateKeyframes,
        duration: duration
      }));
    }

    if (animation.keyframes.scaleKeyframes) {
      self.options.tweens.push(new svgTween({
        element: element.select('.scale'),
        keyframes: animation.keyframes.scaleKeyframes,
        duration: duration
      }));
    }
  });
});
}</code></pre>

Finally, we update our `init` function to call `loadJSON`, which in turn calls `loadSVG`, finishing our tutorial for good.</p>

<pre><code class="language-javascript">init: function() {
var self = this;

self.loadJSON(self.options.data, function (data) {
  self.loadSVG(self.options.canvas, self.options.svg, data.animations, (self.options.duration/self.options.steps));
});
}
</code></pre>

See the Pen [JSON Config](https://codepen.io/hellomichael/pen/xOqBRo/) by Michael Ngo ([@hellomichael](https://codepen.io/hellomichael)) on [CodePen](https://codepen.io).</p>

## A Note On Performance

Our goal was to see how far we could push SVG animation; so, we favored animation fidelity over performance. We stand by this because it enabled us to push our animations much further than anticipated. However, we didn’t ignore performance completely.

Looking at the Chrome DevTools timeline, we see that the animation plays at a steady 60 frames per second, with a few hiccups in between. If we break down the backpack animation, there are 19 elements with 3 possible transforms. That means, at worst, there are 57 possible tweens happening at once. Fortunately, this isn’t the case because the tweens are staggered over the lifetime of the animation. We can visually see this in the CPU graph, as its usage steadily ramps up, peaks where the animations overlap the most, and then diminishes as each tween ends. Visually, Firefox and Internet Explorer were able to play the animations with no discernible differences in performance.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c74381dc-fb92-4828-99b1-900634515acd/10-desktop-performance-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c74381dc-fb92-4828-99b1-900634515acd/10-desktop-performance-opt.jpg" alt="desktop performance" width="500" height="301" /></a><figcaption>Figure 10. The Chrome DevTools timeline, showing CPU usage and the frame rate for desktop.</figcaption></figure>

As expected, mobile devices took a performance hit. Using remote debugging on an old Android device, our frame rate dropped from 60 per second, hovering between 30 and 60\. Though not perfect, we felt this was more than satisfactory for our needs. There is a silver lining, though, because our latest tests on an iPhone 5 and iPhone 6 performed flawlessly.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/004c2fe8-8359-4843-a664-99b7586323e8/11-mobile-performance-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/004c2fe8-8359-4843-a664-99b7586323e8/11-mobile-performance-opt.jpg" alt="mobile performance" width="500" height="301" /></a><figcaption>Figure 11. Remote debugging on Android, showing weaker performance on mobile.</figcaption></figure>

## What’s Next?

Unfortunately, the campaign was dropped before completion, so we never had a chance to dive deeper into the project. As is, the source code provided isn’t quite production-ready; we would have liked to have addressed a few key issues.</p>

### Event-Driven

Our Codepen embed provides a “rerun” button, but our implementation isn’t event-driven. Ideally, the animations wouldn’t immediately play back until initiated via some type of interaction (mouse click, waypoint, etc.).</p>

### Mobile Devices

While these animations do run on mobile devices, as mentioned, they are processor-heavy. So, consider their importance in the overall design of your project. Performance and file size could be saved significantly by excluding them. If they’re an absolute necessity, consider further how they could be made responsive for mobile viewports.</p>

### Fallbacks

The solution for our animations works in all modern browsers and has been tested in Internet Explorer 9+, Firefox and Chrome. This is primarily due to Snap.svg support. If your project requires the use of older browsers, you could try using Snap.svg’s predecessor, Raphael. The more accessible approach is progressive enhancement, serving a static SVG initially and then adding animation for those with capable browsers.</p>

## Signing Off

Well, there you have it, from simple illustration to complex animation. You can download the entire [code base on GitHub](https://github.com/hellomichael/SVGAnimation).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53edb631-abe6-4025-8d9a-ac25908e7c2c/backpack-animation.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53edb631-abe6-4025-8d9a-ac25908e7c2c/backpack-animation.gif" width="500" height="301" alt="Backpack Full Animation" /></a></figure>

_Last but not least, a big thank you to Rey Bango of the Smashing Magazine team, [Chris Halaska](https://www.chrishalaska.com/) for the amazing illustrations, [Matt Harwood](https://www.morningharwood.com/) for the code review, and Rhiana Chan for the much-needed editing._

{{< signature "rb, ml, al, il" >}}


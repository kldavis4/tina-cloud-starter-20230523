---
title: What You Need To Know About Behavioral CSS
slug: what-you-need-to-know-about-behavioral-css
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe9fea1b-0b03-4fd0-87f1-b5fc7d37a2f1/css6.jpg
date: 2009-12-19T11:57:18.000Z
author: tim-wright
description: >-
  As we move forward with the Web and browsers become capable of rendering more advanced code, we gradually get closer to the goal of universal standards across all platforms and computers. Not only will we have to spend less time making sure our box model looks right in IE6, but we create an atmosphere ripe for innovation and free of hacks and heavy front-end scripting.
categories:
  - Coding
  - CSS
---
The Web is an extremely adaptive environment and is surrounded by a collaborative community with a wealth of knowledge to share. If we collectively want to be able to have rounded corners, we make it happen. If we want to have <a href="https://www.protocoder.com/css/css-multiple-backgrounds-background-layering-with-jquery/">multiple background images</a>, we make it happen. If we want border images, we make that happen, too. So desire is not the issue. If it was, we would all still be using tables to lay out our pages and using heavy over-the-top code. We all know that anything can be done on the Web.

### Made for the Web

CSS 3 properties like <a href="https://www.css3.info/preview/rounded-border/">border-radius</a>, <a href="https://www.css3.info/preview/box-shadow/">box-shadow</a>, and <a href="https://www.css3.info/preview/text-shadow/">text-shadow</a> are starting to gain momentum in WebKit (Safari, Chrome, etc.) and Gecko (Firefox) browsers. They are already creating more lightweight pages and richer experiences for users, not to mention that they degrade pretty gracefully; but they are only the tip of the iceberg of what we can do with CSS 3.

{{% feature-panel %}}

In this article, we will take those properties a step further and explore <strong>transformations, transitions, and animations</strong>. We'll go over the code itself, available support and some examples to show exactly how these new properties improve not only your designs but the overall user experience.</p>

## CSS Transformations

CSS transformations are a W3C oddity. It is the first time I have sat down to read the <a href="https://www.w3.org/TR/css3-3d-transforms/">full specifications</a> on something and didn't feel like I had a handle on the subject afterward. The specs are written with the level of technical jargon you would expect from the W3C, but it focuses on the graphic (as in graph drawing) element of transformations and matrices. Having not dealt with a matrix since freshman-year Calculus, I had to do a lot of good old-fashioned browser testing and <strong>guessing and checking</strong> for this section.

After going through every tutorial I could find and too many browser tests to count, I came out with some useful information on <strong>CSS transformations</strong> that I think we can all benefit from.</p>

### transform();

The <code>transform</code> property allows for the kind of functions also allowed by <a href="https://www.w3.org/Graphics/SVG/">SVG</a>. It can be applied to both <strong>inline and block-level elements</strong>. It allows us to twist, zoom in on and move elements, all with one line of CSS.

One of the biggest complaints about cutting-edge design is that the text is not selectable. This is no longer a problem when you use the <code>transform</code> property to manipulate text, because it is pure CSS and so any text within the element remains selectable. This is a huge advantage of CSS over using an image (or background image).

Some interesting and useful transform functions (that are supported):

*   **rotate**.  Rotate allow you to turn an object by passing a degree value through the function.
*   **scale**.  Scale is a zooming function and can make any element larger. It takes positive and negative values as well as decimals.
*   **translate**.  Translate essentially repositions an element based on X and Y coordinates.

Let's look at each of these in more detail.</p>

### Rotate

The transform property has many uses, one of which is to <strong>rotate</strong>. Rotation turns an object based on a degree value and can be applied to both inline and block-level elements, It makes for a pretty cool effect.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8ec8964-0bd6-4256-8d9d-d5dcc8d29b27/transform-rotate.png" alt="text rotation example" />

<pre><code class="language-css">#nav {
    -webkit-transform: rotate(-90deg);
    -moz-transform: rotate(-90deg);
    filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=3);
    }</code></pre>

Please notice that in IE 8 (when not in standards mode) it’s required that you type “-ms-filter” instead of just “filter” in your CSS.

<strong>Support</strong>
Support for <code>transform: rotate</code> is surprisingly widespread. In the CSS snippet above, we directly target <code>-webkit-</code> and <code>-moz-</code> and rotate the <code>#nav</code> element by -90 degrees.

Pretty straightforward, right? The only problem is that the rotation is for a pretty important design element, and many designers will be reluctant to use it if Internet Explorer does not recognize it.

Luckily, <strong>IE has a filter for this</strong>: the image transform filter. It can take four rotation values: 0, 1, 2, and 3. You won't get the same fine-grained control that comes with Webkit and Gecko, but your design will remain consistent across older browsers (even IE6).

<strong>Is it okay to use?</strong>
Yes, but make sure it is thoroughly tested.</p>

### Scale

Scaling does exactly what you think it would do: zoom in and out on an element. The scale function takes both width and height values, and those values can be positive, negative or decimals.

Positive values scale up the element, as you would expect, based on the width and height specified.

Negative values do not shrink the element, but rather reverse it (e.g. text is turned backwards) and then scaled accordingly. You can, however, use decimal values lower than 1 (e.g. .5) to shrink or zoom out of an element.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74953e3d-618f-4225-97e0-cec2d97f8764/transform-scale.png" alt="transform scale example" />

<pre><code class="language-css">#nav {
/* The nav element width and height will double in size */
-webkit-transform: scale(2);
-moz-transform: scale(2);
}

#nav {
/* The nav element width will double in size, but the height will remain unchanged*/
-webkit-transform: scale(2, 1);
-moz-transform: scale(2, 1);
}

#nav {
/* The nav element width will double in size and flip horizontally,
but the height will remain unchanged */
-webkit-transform: scale(-2, 1);
-moz-transform: scale(-2, 1);
}</code></pre>

<strong>Support</strong>
The scale transformation is supported in<strong> Firefox, Safari and Chrome</strong>, but not any version of Internet Explorer (yet) as far as I could tell. Scaling an object is a fairly significant design choice, but it can be applied with progressive enhancement using <code>:hover</code>, which can add a little pop to your navigation especially.

<pre><code class="language-css">#nav li a:hover{
/* This should make your navigation links zoom slightly on hover */
-webkit-transform: scale(1.1);
-moz-transform: scale(1.1);
}</code></pre>

<strong>Is it okay to use?</strong>
From time to time, yes. But not with critical design elements.</p>

### Translate

The name "translate" is a little misleading. It is actually a method of positioning elements using <strong> X and Y values</strong>.

It looks much the same as the other kinds of transformation but adds an extra dimension to your website.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/487ec0ca-416c-42dc-bb8d-bda2da819e84/transform-translate.png" alt="transform translate example" />

<pre><code class="language-css">#nav{
/* This will move the #nav element left 10 pixels and down 20 pixels. */
-moz-transform: translate(10px, 20px);
-webkit-transform: translate(10px, 20px);
}</code></pre>

<strong>Support</strong>
Translate is currently supported in <strong>Firefox, Safari and Chrome</strong> when you use the vender extensions <code>-moz-</code> and <code>-webkit-</code>.

<strong>Is it okay to use?</strong>
Yes, but normal X/Y positioning is just as effective in many situations.</p>

### Chaining Transformations

Transformations are great individually, but if you want multiple transformations, the code can pile up pretty quickly, especially with the vendor extensions. Luckily, we have some built-in shortcuts:

<pre><code class="language-css">#nav{
-moz-transform: translate(10, 25);
-webkit-transform: translate(10, 25);
-moz-transform: rotate(90deg);
-webkit-transform: rotate(90deg);
-moz-transform: scale(2, 1);
-webkit-transform: scale(2, 1);
}</code></pre>

These <strong>transformations can be chained together</strong> to make your CSS more efficient:

<pre><code class="language-css">#nav{
-moz-transform: translate(10, 25) rotate(90deg) scale(2, 1);
-webkit-transform: translate(10, 25) rotate(90deg) scale(2, 1);
}</code></pre>

The real power of these properties is in combining and chaining them. You can move, turn, zoom in on and manipulate any inline or block-level element without JavaScript. Once support for these properties becomes widespread, we'll be able to build and design even richer and more lightweight interfaces and applications.</p>

## Transition

A basic transition refers to a CSS property that define and moves an element from its inactive state (e.g. dark-blue background) to its hover or active state (e.g. light-blue background).

Transitions can be coupled with transformations (and trigger events such as <code>:hover</code> or <code>:focus</code>) to create a kind of animation. Fading the background color, sliding a block and spinning an object can all be done with CSS transitions.

<pre><code class="language-css">#nav a{
background-color:red;
}

#nav a:hover,
#nav a:focus{
background-color:blue;

/* tell the transition to apply to background-color (looks like a CSS variable, doesn't it? #foreshadowing)*/
-webkit-transition-property:background-color;

/* make it 2 seconds long */
-webkit-transition-duration:2s;
}</code></pre>

<strong>Support</strong>
As cool as the transition property is, support is mostly limited to <strong>WebKit</strong> browsers. <code>-moz-transition</code> already works in the latest nightly build of Firefox 3.7 (so it’s guaranteed for the future). So it's safe to assume that it is right behind WebKit on this. So you may as well add <code>-moz-transition</code> to your CSS for future enhancements. And even a version without a vendor extension, just in case.

<strong>Is it okay to use?</strong>
For subtle enhancements, yes, but not for dramatic effects.</p>

## Animation

Animations are where the real action in CSS 3 is. You can combine all of the elements we've talked about above with animation properties like <code>animation-duration</code>, <code>animation-name</code> and <code>animation-timing-function</code> to create Flash-like animations with pure CSS.

<pre><code class="language-css">#rotate {
margin: 0 auto;
width: 600px;
height: 400px;

/* Ensures we're in 3-D space */
-webkit-transform-style: preserve-3d;

/*
Make the whole set of rows use the x-axis spin animation
for a duration of 7 seconds, running infinitely and linearly.
*/

-webkit-animation-name: x-spin;
-webkit-animation-duration: 7s;
-webkit-animation-iteration-count: infinite;
-webkit-animation-timing-function: linear;
}

/* Defining the animation to be called. */
@-webkit-keyframes x-spin {
   0%    { -webkit-transform: rotateX(0deg); }
   50%   { -webkit-transform: rotateX(180deg); }
   100%  { -webkit-transform: rotateX(360deg); }
}</code></pre>

All this fantastic CSS animation code and a live example can be found at <a href="https://webkit.org/blog-files/3d-transforms/poster-circle.html">CSS3.info demo</a>. The demo is viewable in any browser, but the animation works only in the <a href="https://nightly.webkit.org/">nightly build of WebKit</a>. It looks just like the video above, but it's worth installing WebKit to see it for yourself (it's pretty awesome).

<strong>Support</strong>There is, unfortunately, only a limited support for CSS animations yet. 2D CSS animations work in Safari 4 (Leopard), Chrome 3, Safari Mobile, Shira and other Webkit browsers. Safari 4 (Snow Leopard) supports 3D animations.</p>

## Conclusion

Right now, JavaScript bridges the gap until CSS 3 comes into full effect. Unfortunately, getting full browser support for these great properties will be a long journey. Until that day comes, we can take advantage of some serious <strong>progressive enhancement</strong> and rely on JavaScript to enhance our websites and applications. That's not a bad thing; just how it is at the moment.

With the recent <span class="removed_link" title="https://www.readwriteweb.com/archives/microsoft_announces_ie9_html5_css4_javascript_performance.php">announcement of IE9</span>, I wouldn't be surprised if the IE team include some of these properties in the new version of the browser especially since talks for CSS3 integration have already begun (border-radius).

The future of the Web is bright, especially with these highly experimental properties such as <strong>animation</strong>. Although many of the properties are not usable for client or high-level production work, they sure are fun to play with! We can all look forward to the day when we have support across the board to build some really great lightweight applications.</p>

## References And Resources

*   [Adventures In The Third Dimension: CSS 3D Transforms](https://www.smashingmagazine.com/2012/01/adventures-in-the-third-dimension-css-3-d-transforms/)
*   [Applying Transformations To Responsive Web Design](https://www.smashingmagazine.com/2014/02/applying-xsl-transformations-to-responsive-web-design/)
*   [The Guide To CSS Animation: Principles and Examples](https://www.smashingmagazine.com/2011/09/the-guide-to-css-animation-principles-and-examples/)
*   [An Introduction To CSS3 Keyframe Animations](https://www.smashingmagazine.com/2011/05/an-introduction-to-css3-keyframe-animations/)

<em>We express sincere gratitude to Andy Clarke and Hugh Isaacs II for corrections to this article.</em>

{{< signature "al" >}}


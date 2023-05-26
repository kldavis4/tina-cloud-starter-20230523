---
title: Absolute Horizontal And Vertical Centering In CSS
slug: absolute-horizontal-vertical-centering-css
image: null
date: 2013-08-10T06:10:59.000Z
author: stephen-shaw
summary: >-
  In this article, Stephen Shaw introduces a technique for perfect horizontal and vertical centering in CSS, at any width or height. The techniques works with percentage-based width/height, min-/max- width, images, position: fixed and even variable content heights.
description: >-
  In this article, Stephen Shaw introduces a technique for perfect horizontal and vertical centering in CSS, at any width or height. The techniques works with percentage-based width/height, min-/max- width, images, position: fixed and even variable content heights.
categories:
  - CSS
  - Techniques
  - Tables
  - Flexbox
disable_newsletterbox: true
---
_This article was updated on January 31, 2019 to update the below provided information. The old information is not wrong, however is the newest version less hacky and does make use of Flexbox, one of the new standards of [modern web layouts](/2018/05/guide-css-layout/)_. 

**[Update]** 

<div class="break-out">

 <pre><code class="language-css">.Absolute-Center {
  display: flex; // make us of Flexbox
  align-items: center; // does vertically center the desired content
  justify-content: center; // horizontally centers single line items
  text-align: center; // optional, but helps horizontally center text that breaks into multiple lines
}  
</code></pre>
</div>

**[End of Update]**


_Here's the original article from August 2013_: 

We've all seen <code>margin: 0 auto;</code> for horizontal centering, but <code>margin: auto;</code> has refused to work for vertical centering... <em>until now!</em> But actually (spoiler alert!) absolute centering <strong>only requires a declared height and these styles</strong>:

<pre><code class="language-css">.Absolute-Center {
  margin: auto;
  position: absolute;
  top: 0; left: 0; bottom: 0; right: 0;
}</code></pre>

I'm not the pioneer of this method (yet I have dared to name it <em>Absolute Centering</em>), and it may even be a common technique, however, most vertical centering articles never mention it and I had never seen it until I dug through the comments section of a particular article.

There, Simon</a> linked to this <a href="https://jsfiddle.net/mBBJM/1/">jsFiddle</a> that blew every other method out of the water (the same method was also mentioned by Priit in the comments). Researching further, I had to use very specific keywords to find <a href="https://www.vanseodesign.com/css/vertical-centering/">some</a> <a href="https://www.student.oulu.fi/~laurirai/www/css/middle/">other</a> sources for this method.

Having never used this technique before, I put it to the test and discovered how incredible Absolute Centering really is.

<p><em>Find additional demos, a comparison table, and more on <a href="https://codepen.io/shshaw/details/gEiDt">CodePen</a>.</em></p>

{{% feature-panel %}}

### Advantages

- Cross-browser (including IE8-10)
- No special markup, minimal styles
- Responsive with percentages and min-/max-
- Use one class to center any content
- Centered regardless of padding (without <code>box-sizing</code>!)
- Blocks can easily be resized
- Works great on images

### Caveats

- Height must be declared (see <a href="https://www.smashingmagazine.com/2013/08/09/absolute-horizontal-vertical-centering-css/2#Height">Variable Height</a>)
- Recommend setting <code>overflow: auto</code> to prevent content spillover (see <a href="#Overflow">Overflow</a>)
- Doesn't work on Windows Phone

### Browser Compatibility:

<strong> Chrome, Firefox, Safari, Mobile Safari, IE8-10.</strong>
Absolute Centering was tested and works flawlessly in the latest versions of Chrome, Firefox, Safari, Mobile Safari, and even IE8-10.

## Explanation

After researching specs and documentation, this is my understanding of how Absolute Centering works:

- In the <a href="https://taligarsiel.com/Projects/howbrowserswork1.htm#Layout">normal content flow</a>, <code>margin: auto;</code> equals '0' for the top and bottom.
<a href="https://www.w3.org/TR/CSS2/visudet.html#normal-block">W3.org</a>: If 'margin-top', or 'margin-bottom' are 'auto', their used value is 0.
- <code>position: absolute;</code> breaks the block out of the typical content flow, rendering the rest of the content as if that block weren't there.
<a href="https://developer.mozilla.org/en-US/docs/Web/CSS/position#Absolute_positioning">Developer.mozilla.org</a>: ...an element that is positioned absolutely is taken out of the flow and thus takes up no space
- Setting <code>top: 0; left: 0; bottom: 0; right: 0;</code> gives the browser a new bounding box for the block. At this point the block will fill all available space in its offset parent, which is the body or <code>position: relative;</code> container. <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/position#Notes">Developer.mozilla.org</a>: For absolutely positioned elements, the top, right, bottom, and left properties specify offsets from the edge of the element's containing block (what the element is positioned relative to).
- Giving the block a <code>width</code> or a <code>height</code> prevents the block from taking up all available space and forces the browser to calculate <code>margin: auto</code> based on the new bounding box. <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/position#Notes">Developer.mozilla.org</a>: The margin of the [absolutely positioned] element is then positioned inside these offsets.
- Since the block is absolutely positioned and therefore out of the normal flow, the browser gives equal values to <code>margin-top</code> and <code>margin-bottom</code> centering the element in the bounds set earlier.
<a href="https://www.w3.org/TR/CSS2/visudet.html#abs-non-replaced-height">W3.org</a>: If none of the three [top, bottom, height] are 'auto': If both 'margin-top' and 'margin-bottom' are 'auto', solve the equation under the extra constraint that the two margins get equal values.</q> AKA: center the block vertically

Absolute Centering appears to be the intended use for <code>margin: auto;</code> based on the spec and should therefore work in every standards compliant browser.

<strong>TL;DR:</strong> Absolutely positioned elements aren't rendered in the normal flow, so <code>margin: auto;</code> centers vertically within the bounds set by <code>top: 0; left: 0; bottom: 0; right: 0;</code>.

## Within Container

<pre><code class="language-css">.Center-Container {
  position: relative;
}

.Absolute-Center {
  width: 50%;
  height: 50%;
  overflow: auto;
  margin: auto;
  position: absolute;
  top: 0; left: 0; bottom: 0; right: 0;
}</code></pre>

With Absolute Centering, you can place your content block inside of a <code>position: relative</code> container to align the block within the container!

<strong>The rest of the demos will assume these styles are already included and will provide add-on classes to implement various features.</strong><br>

### Absolute Center, Within Container

This box is absolutely centered, horizontally and vertically, within its container using
<code>position: relative</code>.

## Within Viewport

<pre><code class="language-css">.Absolute-Center.is-Fixed {
  position: fixed;
  z-index: 999;
}</code></pre>

Want the content block centered in the viewport? Set it to <code>position: fixed</code> and give it a high z-index, like the modal on this page.

- <strong>Mobile Safari:</strong> The content block will be centered vertically in the whole document, not the viewport, if it is not within a <code>position: relative</code> container.

## Offsets

<pre><code class="language-css">.Absolute-Center.is-Right {
  left: auto; right: 20px;
  text-align: right;
}

.Absolute-Center.is-Left {
  right: auto; left: 20px;
  text-align: left;
}</code></pre>

If you have a fixed header or need to add other offsets, simply add it in your content block's styles like <code>top: 70px;</code>. As long as <code>margin: auto;</code> is declared, the content block will be vertically centered within the bounds you declare with <code>top</code> <code>left</code> <code>bottom</code> and <code>right</code>.

You can also stick your content block to the right or left while keeping it vertically centered, using <code>right: 0; left: auto;</code> to stick to the right or <code>left: 0; right: auto;</code> to stick to the left.

### Vertical Center, Align Right

This box is absolutely centered vertically within its container, but stuck to the right with
<code>right: 0; left: auto;</code>.

## Responsive

<pre><code class="language-css">.Absolute-Center.is-Responsive {
  width: 60%;
  height: 60%;
  min-width: 200px;
  max-width: 400px;
  padding: 40px;
}
</code></pre>

Perhaps the best benefit of Absolute Centering is percentage based width/heights work perfectly! Even <code>min-width/max-width</code> and <code>min-height/max-height</code> styles behave as expected for more responsive boxes.

Go ahead, add padding to the element; Absolute Centering doesn't mind!

### Absolute Center, Percentage Based

This box is absolutely centered, horizontally and vertically, even with percentage based widths &amp; height, min-/max-, and padding!

## Overflow

<pre><code class="language-css">.Absolute-Center.is-Overflow {
  overflow: auto;
}</code></pre>

Content taller than the block or container (viewport or a <code>position: relative</code> container) will overflow and may spill outside the content block and container or even be cut off. Simply adding <code>overflow: auto</code> will allow the content to scroll within the block as long as the content block itself isn't taller than its container (perhaps by adding <code>max-height: 100%;</code> if you don't have any padding on the content block itself).

## Resizing

<pre><code class="language-css">.Absolute-Center.is-Resizable {
  min-width: 20%;
  max-width: 80%;
  min-height: 20%;
  max-height: 80%;
  resize: both;
  overflow: auto;
}</code></pre>

You can resize your content block with other classes or Javascript without having to recalculate the center manually! Adding the <code>resize</code> property will even let your content block be resized by the user.

Absolute Centering keeps the block centered no matter how the block is resized. Setting min-/max- will limit the block's size to what you want and prevent it from overflowing the window/container.

If you don't use <code>resize: both</code>, you can add a <code>transition</code> to smoothly animate between sizes. Be sure to set <code>overflow: auto</code> since the block could be resized smaller than the content.

Absolute Centering is the only vertical centering technique tested that successfully supports the <code>resize: both</code> property.

### Caveats

- Set your <code>max-width/max-height</code> to compensate for any padding on the content block itself, otherwise it will overflow its container.
- The <code>resize</code> property is not supported on mobile browsers or in IE 8-10 so make sure your users have an alternate way of resizing if that is essential to user experience.
- Combining <code>resize</code> and <code>transition</code> properties causes a delay equal to the transition time when the user attempts to resize.

## Images

<strong>HTML:</strong>

<pre><code class="language-markup">&lt;img src="https://placekitten.com/g/500/200" class="Absolute-Center is-Image" alt="" /&gt;</code></pre>

<strong>CSS:</strong>

<pre><code class="language-css">.Absolute-Center.is-Image {
  height: auto;
}

.Absolute-Center.is-Image img {
  width: 100%;
  height: auto;
}</code></pre>

Images work too! Apply the class/style to the image itself and set <code>height: auto;</code> like you would with a responsively-sized image to let it resize with the container.

Note that <code>height: auto;</code> works for images, but causes a regular content block to stretch to fill the container unless you use the <a href="#Height">variable height technique</a>. It's likely that because browsers have to calculate the height for the image rendered image, so <code>margin: auto;</code> ends up working as if you'd declared the height in all tested browsers.

## Variable Height

<strong>Javascript:</strong>

<pre><code class="language-javascript">/* Modernizr Test for Variable Height Content */
Modernizr.testStyles('#modernizr { display: table; height: 50px; width: 50px; margin: auto; position: absolute; top: 0; left: 0; bottom: 0; right: 0; }', function(elem, rule) {
  Modernizr.addTest('absolutecentercontent', Math.round(window.innerHeight / 2 - 25) === elem.offsetTop);
});
</code></pre>

<strong>CSS:</strong>

<pre><code class="language-css">.absolutecentercontent .Absolute-Center.is-Variable {
  display: table;
  height: auto;
}</code></pre>

Absolute Centering does require a declared height, however the height can be percentage based and controlled by <code>max-height</code>. This makes it ideal for responsive scenarios, just make sure you set an appropriate <a href="#Overflow">overflow</a>.

One way around the declared height is adding <code>display: table</code>, centering the content block regardless of content length. This causes issues in a few browsers (IE and Firefox, mainly), so my buddy <a href="https://stackoverflow.com/users/2539605/kalley">Kalley</a> at <a href="https://ellcreative.com">ELL Creative</a> wrote a Modernizr test to check if the browser supports this method of centering. Now you can progressively enhance

### Caveats

This will break cross-browser compatibility. You may want to consider an <a href="#Other">alternate technique</a> if the Modernizr test doesn't meet your needs.

- Not compatible with the <a href="#Resizing">Resizing</a> technique.
- <strong>Firefox/IE8:</strong> Using <code>display: table</code> aligns the content block to the top, but is still centered horizontally.
- <strong>IE9/10:</strong> Using <code>display: table</code> aligns the content block to the top left.
- <strong>Mobile Safari:</strong> The content block is centered vertically, but becomes slightly off-center horizontally when using percentage based widths.

### Absolute Center, Variable Height

This box is absolutely centered vertically within its container, regardless of content height.

## Other Techniques

<em>Absolute Centering</em> is a great solution for centering, but there are other methods that may fit more specific needs. The most commonly used or recommended methods are <a href="#Negative-Margins">Negative Margins</a>, <a href="#Transforms">Transforms</a>, <a href="#Table-Cell">Table-Cell</a>, <a href="#Inline-Block">Inline-Block</a>, and now <a href="#Flexbox">Flexbox</a>. They are covered more in depth in other articles, so I'll only cover the basics here.

## Negative Margins

<pre><code class="language-css">.is-Negative {
        width: 300px;
        height: 200px;
        padding: 20px;
        position: absolute;
        top: 50%; left: 50%;
        margin-left: -170px; /* (width + padding)/2 */
        margin-top: -120px; /* (height + padding)/2 */
}</code></pre>

Perhaps the most common technique. If exact dimensions are known, setting a negative margin equal to half the width/height (plus padding, if not using <code>box-sizing: border-box</code>) along with <code>top: 50%; left: 50%;</code> will center the block within a container.

It should be noted that this is the only method tested that worked as expected in IE6-7.

### Advantages

- Works well cross-browser, including IE6-7
- Requires minimal code

### Caveats

- Not responsive. Doesn't work for percentage based dimensions and can't set min-/max-
- Content can overflow the container
- Have to compensate for <code>padding</code> or use <code>box-sizing: border-box</code>

### Absolute Center, Negative Margins

This box is absolutely centered vertically within its container using negative margins.

## Transforms

<pre><code class="language-css">.is-Transformed {
  width: 50%;
  margin: auto;
  position: absolute;
  top: 50%; left: 50%;
  -webkit-transform: translate(-50%,-50%);
      -ms-transform: translate(-50%,-50%);
          transform: translate(-50%,-50%);
}</code></pre>

One of the simplest techniques with about the same benefits as Absolute Centering, but supports variable height. Give the content block <code>transform: translate(-50%,-50%)</code> with the required vendor prefixes along with <code>top: 50%; left: 50%;</code> to get it centered.

### Advantages

- Variable height content
- Requires minimal code

### Caveats

- Won't work in IE8
- Need vendor prefixes
- Can interfere with other <code>transform</code> effects
- Results in blurry rendering of edges and text in some cases

### Absolute Center, Translate(-50%,-50%)

This box is absolutely centered vertically within its container using <code>translate(-50%,-50%)</code>.

## Table-Cell

<strong>HTML:</strong>

<pre><code class="language-markup">&lt;div class="Center-Container is-Table"&gt;
  &lt;div class="Table-Cell"&gt;
    &lt;div class="Center-Block"&gt;
    &lt;!-- CONTENT --&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;</code></pre>

<strong>CSS:</strong>

<pre><code class="language-css">.Center-Container.is-Table { display: table; }
.is-Table .Table-Cell {
  display: table-cell;
  vertical-align: middle;
}
.is-Table .Center-Block {
  width: 50%;
  margin: 0 auto;
}</code></pre>

This may be the best technique overall, simply because the height can vary with the content and browser support is great. The main disadvantage is the extra markup, requiring a total of three elements to get the final one centered.

### Advantages

- Variable height content
- Content overflows by stretching the parent element
- Works well cross-browser

### Caveats

- Requires extra markup

### Absolute Center, Table/Table-Cell

This box is absolutely centered vertically within its <code>display: table-cell</code> parent, which is within a <code>display: table</code> container.

## Inline-Block

<strong>HTML:</strong>

<pre><code class="language-markup">&lt;div class="Center-Container is-Inline"&gt;
  &lt;div class="Center-Block"&gt;
    &lt;!-- CONTENT --&gt;
  &lt;/div&gt;
&lt;/div&gt;</code></pre>

<strong>CSS:</strong>

<pre><code class="language-css">.Center-Container.is-Inline {
  text-align: center;
  overflow: auto;
}

.Center-Container.is-Inline:after,
.is-Inline .Center-Block {
  display: inline-block;
  vertical-align: middle;
}

.Center-Container.is-Inline:after {
  content: ’;
  height: 100%;
  margin-left: -0.25em; /* To offset spacing. May vary by font */
}

.is-Inline .Center-Block {
  max-width: 99%; /* Prevents issues with long content causes the content block to be pushed to the top */
  /* max-width: calc(100% - 0.25em) /* Only for IE9+ */
}</code></pre>

By popular demand: Inline-Block centering. The basic idea is using <code>display: inline-block</code>, <code>vertical-align: middle</code> and a psuedo element to center your content block inside of a container. My implementation has a few new tricks here that I haven't seen elsewhere that help solve a few issues.

The content block's width must be declared to be no wider than 100% of the container minus 0.25em if the content is wider than the container. like a block with long paragraph text. Otherwise, the content block will be pushed to the top, which is the reason for using <code>:after</code>. Using <code>:before</code> caused the content to be pushed down 100%!

If your content block needs take up as much available horizontal space as possible, you can add either <code>max-width: 99%;</code>, which works for bigger containers, or <code>max-width: calc(100% - 0.25em)</code> depending on the browsers you support and the width of the container.

The benefits are mostly the same as the <a href="#Table-Cell">Table-Cell</a> technique, but I initially left this method out because it's very much a hack. Regardless, browser support is great and it proves to be a popular technique.

### Advantages

- Variable height content
- Content overflows by stretching the parent element
- Works well cross-browser, and can be adapted for IE7 support (view <a href="https://codepen.io/shshaw/pen/gEiDt">the CSS</a> to see)

### Caveats

- Requires a container
- Relies on <code>margin-left: -0.25em;</code> to horizontally center correctly, but may need to be adjusted for different fonts/sizes
- Content block's width must be declared to be no wider than 100% of the container minus 0.25em.

### Absolute Center, Inline-Block

This box is absolutely centered vertically using <code>display: inline-block</code>, <code>vertical-align: middle</code> and a psuedo element.

## Flexbox

<pre><code class="language-css">.Center-Container.is-Flexbox {
  display: -webkit-box;
  display: -moz-box;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  -webkit-box-align: center;
     -moz-box-align: center;
     -ms-flex-align: center;
  -webkit-align-items: center;
          align-items: center;
  -webkit-box-pack: center;
     -moz-box-pack: center;
     -ms-flex-pack: center;
  -webkit-justify-content: center;
          justify-content: center;
}</code></pre>

The future of layout in CSS, Flexbox is the latest CSS spec designed to solve common layout problems such as vertical centering. Smashing Magazine already has a great article on <a href="https://www.smashingmagazine.com/2013/05/22/centering-elements-with-flexbox/">Centering Elements with Flexbox</a> that you should read to for a more complete overview. Keep in mind that Flexbox is more than just a way to center, it can be used for columns and all sorts of crazy layout problems.

### Advantages

- Content can be any width or height, even overflows gracefully
- Can be used for more advanced layout techniques.

### Caveats

- No IE8-9 support
- Requires a container or styles on the body

### Absolute Center, Flexbox

This Flexbox box is absolutely centered vertically within its container.

## Recommendations

Each technique has their advantages. Which one you choose mainly boils down to which browsers you support and what your existing markup looks like, but use the <a href="https://codepen.io/shshaw/full/gEiDt#Comparison-Table">comparison table</a> to make the right choice to match the features you need.

<em>Absolute Centering</em> works great as a simple drop-in solution with no-fuss. Anywhere you used Negative Margins before, use Absolute Centering instead. You won't have to deal with pesky math for the margins or extra markup, and you can size your boxes responsively.

If your site requires variable height content with the best browser compatibility, try out the <a href="#Table-Cell">Table-Cell</a>, <a href="#Inline-Block">Inline-Block</a> techniques. If you're on the bleeding edge, give <a href="#Flexbox">Flexbox</a> a try and reap the benefits of its advanced layout techniques.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Definitive Guide to Using Negative Margins](https://www.smashingmagazine.com/2009/07/the-definitive-guide-to-using-negative-margins/)
*   [Flexbox Is As Easy As Pie – Designing CSS Layouts](https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/)
*   [The Mystery Of The CSS Float Property](https://www.smashingmagazine.com/2009/10/the-mystery-of-css-float-property/)

{{< signature "vf" >}}

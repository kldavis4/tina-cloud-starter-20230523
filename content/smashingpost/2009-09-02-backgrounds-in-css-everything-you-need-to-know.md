---
title: CSS Background – Everything You Need To Know
slug: backgrounds-in-css-everything-you-need-to-know
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0754757-233f-41f6-9b3e-2416c39840c1/illucsswidth.gif
date: 2009-09-02T11:02:52.000Z
author: michael-martin
description: >-
  **Backgrounds** are a core part of CSS. They are one of the fundamentals that
  you simply need to know. In this article, we will cover the basics of using
  CSS backgrounds, including properties such as `background-attachment`. We'll
  show some common tricks that can be done with the background as well as what's
  in store for **backgrounds in CSS 3** (including four new background
  properties!).
categories:
  - Coding
  - CSS
  - Backgrounds
  - Essentials
---
The CSS Background is one of the fundamentals that you simply need to know. We will cover the basics of using CSS backgrounds, including properties such as <code>background-attachment</code>. We'll show some common tricks that can be done with the background as well as what's in store for <strong>background in CSS 3</strong> (including four new background properties!).

You may also want to check out the following Smashing Magazine articles:

*   [Simple Responsive Images With CSS Background Images](https://www.smashingmagazine.com/2013/07/simple-responsive-images-with-css-background-images/)
*   [[Ask SM] Transparent Background, Positioning Problem](https://www.smashingmagazine.com/2009/04/ask-sm-css-auto-refreshing-content-transparent-backgrounds-positioning/)
*   [Backgrounds In Web Design: Examples And Best Practices](https://www.smashingmagazine.com/2009/03/backgrounds-in-web-design-examples-and-best-practices-2/)
*   [CSS: Innovative Techniques and Practical Solutions](https://www.smashingmagazine.com/2011/02/css-useful-coding-techniques-and-design-solutions/)

## Working With Background in CSS 2

### Overview

We have five main background properties to use in CSS 2. They are as follows:

{{% feature-panel %}}

*   `background-color`: specifies the solid color to fill the background with.
*   `background-image`: calls an image for the background.
*   `background-position`: specifies where to place the image in the element's background.
*   `background-repeat`: determines whether the image is tiled.
*   `background-attachment`: determines whether the image scrolls with the page.

These properties can all be merged into one <strong>short-hand</strong> property: <code>background</code>. One important thing to note is that the background accounts for the contents of the element, including the padding and border. It does not include an element's margin. This works as it should in Firefox, Safari and Opera, and now in IE8. But in IE7 and IE6 the background does not include the border, as illustrated below.

<img loading="lazy" decoding="async"  class="alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a7fd475-24d3-4213-a8f2-4f73c8ec9088/css-background-border.jpg" alt="css background" width="380" height="280" /><br>
<em>Background does not extend to the borders in IE7 and IE6.</em>

### Basic Properties

<strong>Background color</strong>
The <code>background-color</code> property fills the background with a <strong>solid color</strong>. There are a number of ways to specify the color. The follow commands all have the same output:

<pre><code class="language-css">background-color: blue;
background-color: rgb(0, 0, 255);
background-color: #0000ff;</code></pre>

The <code>background-color</code> property can also be set to <code>transparent</code>, which makes any elements underneath it visible instead.

<strong>Background image</strong>
The <code>background-image</code> property allows you to <strong>specify an image</strong> to be displayed in the background. This can be used in conjunction with <code>background-color</code>, so if your image is not tiled, then any space that the image doesn't cover will be set to the background color. Again, the code is very simple. Just remember that the path is relative to the style sheet. So, in the following snippet, the image is in the same directory as the style sheet:

<pre><code class="language-css">background-image: url(image.jpg);</code></pre>

But if the image was in a sub-folder named <em>images</em>, then it would be:

<pre><code class="language-css">background-image: url(images/image.jpg);</code></pre>

<strong>Background repeat</strong>
By default, when you set an image, the image is repeated both horizontally and vertically until the entire element is filled. This may be what you want, but sometimes you want an image to be displayed only once or to be tiled in only one direction. The possible values (and their results) are as follows:

<pre><code class="language-css">background-repeat: repeat;  /* The default value. Will tile the image in both directions. */
background-repeat: no-repeat;   /* No tiling. The image will be used only once. */
background-repeat: repeat-x;  /* Tiles horizontally (i.e. along the x-axis) */
background-repeat: repeat-y;  /* Tiles vertically (i.e. along the y-axis) */
background-repeat: inherit; /* Uses the same background-repeat property of the element's parent. */</code></pre>

<strong>Background position</strong>
The <code>background-position</code> property controls where a background image is located in an element. The trick with <code>background-position</code> is that you are actually specifying where the top-left corner of the image will be positioned, relative to the top-left corner of the element.

In the examples below, we have set a background image and are using the <code>background-position</code> property to control it. We have also set <code>background-repeat</code> to <code>no-repeat</code>. The measurements are all in pixels. The first digit is the x-axis position (horizontal) and the second is the y-axis position (vertical).

<pre><code class="language-css">/* Example 1: default. */
background-position: 0 0; /* i.e. Top-left corner of element. */

/* Example 2: move the image to the right. */
background-position: 75px 0;

/* Example 3: move the image to the left. */
background-position: -75px 0;

/* Example 4: move the image down. */
background-position: 0 100px;</code></pre>

<img loading="lazy" decoding="async"  class="alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebbeb757-92d2-4108-9bee-9f32d51209bd/css-background-position.jpg" alt="css background" width="406" height="548" /><br>
<em>The image can be set to any position you like.</em>

The <code>background-position</code> property also works with other values, <strong>keywords and percentages</strong>, which can be useful, especially when an element's size is not set in pixels.

The keywords are self-explanatory. For the x-axis:

*   left
*   center
*   right

And for the y-axis:

*   top
*   center
*   bottom

Their order is exactly like that of the pixels values, x-axis value first, and y-axis value second, as so:

<pre><code class="language-css">background-position: top right;</code></pre>

Percentage values are similar. The thing to remember here is that when you specify a percentage, the browser sets <strong>the part of the image at that percentage</strong> to align with that percentage of the element. This makes more sense in an example. Let's say you specify the following:

<pre><code class="language-css">background-position: 100% 50%;</code></pre>

This goes 100% of the way across the image (i.e. the very right-hand edge) and 100% of the way across the element (remember, the starting point is always the top-left corner), and the two line up there. It then goes 50% of the way down the image and 50% of the way down the element to line up there. The result is that the image is aligned to the right of the element and exactly half-way down it.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c00ff31f-8801-4248-b0a8-5917cab807d0/css-background-position2.jpg" alt="" width="207" height="254" /><br>
<em>The smiley face is aligned as it would be if it was set to <code>right center</code>.</em>

<strong>Background attachment</strong>
The <code>background-attachment</code> property determines what happens to an image when the user scrolls the page. The three available properties are <code>scroll</code>, <code>fixed</code> and <code>inherit</code>. <code>Inherit</code> simply tells the element to follow the <code>background-attachment</code> property of its parent.

To understand <code>background-attachment</code> properly, we need to first think of how the page and view port interact. The view port is the section of your browser that displays the Web page (think of it like your browser but without all the toolbars). The view port is set in its position and <strong>never moves</strong>.

When you scroll down a Web page, the view port does not move. Instead, the content of the page scrolls upward. This makes it seem as if the view port is scrolling down the page. Now, when we set background-attachment:scroll;, we are telling the background that when the element scrolls, the background must scroll with it. In simpler terms, the background sticks to the element. This is the default setting for <code>background-attachment</code>.

Let's see an example to make it clearer:

<pre><code class="language-css">background-image: url(test-image.jpg);

background-position: 0 0;
background-repeat: no-repeat;
background-attachment: scroll;</code></pre>

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd80961b-61df-408f-a794-300419d41d21/css-background-attachment1.jpg" alt="" width="287" height="417" /><br>
<em>As we scroll down the page, the background scrolls up until it disappears.</em>

But when we set the <code>background-attachment</code> to <code>fixed</code>, we are telling the browser that when the user scrolls down the page, the background should stay fixed where it is — i.e. not scroll with the content.

Let's illustrate this with another example:

<pre><code class="language-css">background-image: url(test-image.jpg);
background-position: 0 100%;
background-repeat: no-repeat;
background-attachment: fixed;</code></pre>

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09fc8fb4-7bca-4da4-ba49-60b0bcfb23eb/css-background-attachment2.jpg" alt="" width="287" height="417" /><br>
<em>We have scrolled down the page here, but the image remains visible.</em>

The important thing to note however is that the background image only appears in areas where its parent element reaches. Even though the image is positioned relative to the view port, it will not appear if it's parent element is not visible. This can be shown with another example. In this one, we have aligned the image to the bottom-left of the view port. But only the area of the image inside the element is visible.

<pre><code class="language-css">background-image: url(test-image.jpg);
background-position: 0 100%;
background-repeat: no-repeat;
background-attachment: fixed;</code></pre>

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/929c5be8-2ead-465b-b1c6-5404fd48e512/css-background-attachment3.jpg" alt="" width="287" height="417" /><br>
<em>Part of the image has been cut off because it begins outside of the element.</em>

<strong>The Background Shorthand Property</strong>
Instead of writing out all of these rules each time, we can combine them into a single rule. It takes the following format:

<pre><code class="language-css">background: &lt;color&gt; &lt;image&gt; &lt;position&gt; &lt;attachment&gt; &lt;repeat&gt;</code></pre>

For example, the following rules...

<pre><code class="language-css">background-color: transparent;
background-image: url(image.jpg);
background-position: 50% 0 ;
background-attachment: scroll;
background-repeat: repeat-y;</code></pre>

... could be combined into the following single line:

<pre><code class="language-css">background: transparent url(image.jpg) 50% 0 scroll repeat-y;</code></pre>

And you don't have to specify every value. If you leave a property out, its default value is used instead. For example, the line above has the same output as:

<pre><code class="language-css">background: url(image.jpg) 50% 0 repeat-y;</code></pre>

## Common Uses Of Backgrounds

Aside from their obvious use of making elements more attractive, backgrounds can be used for other purposes.</p>

### Faux Columns

When using the CSS property of <code>float</code> to position layout elements, ensuring that two (or more) columns <strong>are the same length</strong> can be difficult. If the lengths are different, then the background of one of the columns will be shorter than the background of the other, spoiling your design.

Faux columns is a very simple background trick that was first written up on <a href="https://www.alistapart.com/articles/fauxcolumns/">A List Apart</a>. The idea is simple: instead of applying a separate background for each column, apply one background image to the <strong>parent element</strong> of the columns with that image containing the designs for each column.</p>

### Text Replacement

Our choice of fonts on the Web is very limited. We could get custom fonts by using tools such as <a href="https://www.mikeindustries.com/blog/sifr/">sIFR</a>, but they require users to have JavaScript enabled. An easier solution that works on any browser is to <strong>create an image of the text</strong> in the font you want and use it as the background instead. This way, the text still appears in the markup for search engines and screen readers, but browsers will show your preferred font.

For example, your <strong>HTML</strong> markup could look like this:

<pre><code class="language-css">&lt;h3 class="blogroll"&gt;Blogroll&lt;/h3&gt;</code></pre>

If we have a 200 by 75 pixel image of this text in a nicer font, then we could display that instead using the CSS as follows:

<pre><code class="language-css">h3.blogroll {
  width: 200px;
  height: 75px; /* So that the element will show the whole image. */
  background:url(blogroll-text.jpg) 0 0 no-repeat;  /* Sets the background image */
  text-indent: -9999px; /* Hides the regular text by moving it 9999 pixels to the left */
  }</code></pre>

### Easier Bullet Points

Bullet in an unordered list can look clunky. Instead of dealing with all of the different list-style properties, we can simply <strong>hide the bullets</strong> and replace them with a background image. Because the image can be anything you like, the bullets will <strong>look much nicer</strong>.

Here, we turn a regular unordered list into one with sleek bullets:

<pre><code class="language-css">ul {
  list-style: none; /* Removes default bullets. */
  }

ul li {
  padding-left: 40px; /* Indents list items, leaving room for background image on the left. */
  background: url(bulletpoint.jpg) 0 0 no-repeat;
  }</code></pre>

## Backgrounds in CSS 3

CSS 3 has many changes in store for backgrounds. The most obvious is the option for multiple background images, but it also comes with <strong>four new properties</strong> as well as adjustments to current properties.</p>

### Multiple Background Images

In CSS 3, you will be able to use more than one image for the background of an element. The code is the same as CSS 2, except you would <strong>separate images with a comma</strong>. The first declared image is positioned at the top of the element, with subsequent images "layered" beneath it, like so:

<pre><code class="language-css">background-image: url(top-image.jpg), url(middle-image.jpg), url(bottom-image.jpg);</code></pre>

### New Property: Background Clip

This brings us back to the issue discussed at the beginning of this article, about <strong>backgrounds being shown beneath the border</strong>. This is described as the "background painting area."

The <code>background-clip</code> property was created to give you more <strong>control over where backgrounds are displayed</strong>. The possible values are:

*   `background-clip: border-box;` backgrounds displayed beneath the border.
*   `background-clip: padding-box;` backgrounds displayed beneath the padding, not the border.
*   `background-clip: content-box;` backgrounds displayed only beneath content, not border or padding.
*   `background-clip: no-clip;` the default value, same as border-box.</p>

### New Property: Background Origin

This is used in conjunction with <code>background-position</code>. You can have the <code>background-position</code> calculated from the border, padding or content boxes (like <code>background-clip</code>).

*   `background-origin: border-box;` background-position is calculated from the border.
*   `background-origin: padding-box;` background-position is calculated from the padding box.
*   `background-origin: content-box;` background-position is calculated from the content.

A good explanation of the differences between <code>background-clip</code> and <code>background-origin</code> is available on <a href="https://www.css3.info/preview/background-origin-and-background-clip/">CSS3.info</a>.</p>

### New Property: Background Size

The <code>background-size</code> property is used to resize your background image. There are a number of possible values:

*   `background-size: contain;` scales down image to fit element (maintaining pixel aspect ratio).
*   `background-size: cover;` expands image to fill element (maintaining pixel aspect ratio).
*   `background-size: 100px 100px;` scales image to the sizes indicated.
*   `background-size: 50% 100%;` scales image to the sizes indicated. Percentages are relative to the size of containing element.

You can read up on some examples of special cases on the <a href="https://www.w3.org/TR/css3-background/#background-size">CSS 3 specifications</a> website.</p>

### New Property: Background Break

In CSS 3, elements can be split into separate boxes (e.g. to make an inline element span across several lines). The <code>background-break</code> property controls how the background is shown across the different boxes.

The possible values are:

*   `Background-break: continuous;`: the default value. Treats the boxes as if no space is between them (i.e. as if they are all in one box, with the background image applied to that).
*   `Background-break: bounding-box;`: takes the space between boxes into account.
*   `Background-break: each-box;`: treats each box in the element separately and re-draws the background individually for each one.</p>

### Changes to Background Color

The <code>background-color</code> property has a slight enhancement in CSS 3. In addition to specifying the background color, you can specify a "fall-back color" that is used if the bottom-layer background image of the element cannot be used.

This is done by adding a forward slash before the fall-back color, like so

<pre><code class="language-css">background-color: green / blue;</code></pre>

In this example, the background color would be green. However, if the bottom-most background image cannot be used, then blue would be shown instead of green. If you do not specify a color before the slash, then it is <strong>assumed to be transparent</strong>.</p>

### Changes to Background Repeat

When an image is repeated in CSS 2, it is often <strong>cut off</strong> at the end of the element. CSS 3 introduces two new properties to fix this:

*   `space`: an equal amount of space is applied between the image tiles until they fill the element.
*   `round`: the image is scaled down until the tiles fit the element.

An example of <code>background-repeat: space;</code> is available on the <a href="https://www.w3.org/TR/css3-background/#background-repeat">CSS 3 specifications</a> website.</p>

### Changes to Background Attachment

The <code>background-attachment</code> has a new possible value: <code>local</code>. This comes into play with elements that can scroll (i.e. are set to <code>overflow: scroll;</code>). When <code>background-attachment</code> is set to <code>scroll</code>, the background image will not scroll when the element's content is scrolled.

With <code>background-attachment:local</code> now, the background scrolls when the element's content is scrolled.</p>

## Conclusion On CSS B<span data-sheets-value="{&quot;1&quot;:2,&quot;2&quot;:&quot;css background&quot;}" data-sheets-userformat="{&quot;2&quot;:513,&quot;3&quot;:{&quot;1&quot;:0},&quot;12&quot;:0}">ackground</span>

To sum up, there is a lot to know about backgrounds in CSS. But once you wrap your head around it, the techniques and naming conventions <strong>all make good sense</strong> and it quickly becomes second nature.

If you're new to CSS, just keep practicing and you'll get the hang of backgrounds fast enough. If you're a seasoned pro, I hope you're <strong>looking forward to CSS 3</strong> as much as I am!

{{< signature "al" >}}


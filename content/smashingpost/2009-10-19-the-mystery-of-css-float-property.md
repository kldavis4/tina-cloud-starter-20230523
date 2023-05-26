---
title: The Mystery Of The CSS Float Property
slug: the-mystery-of-css-float-property
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/891d68ad-8f88-40a0-be10-444f1d28b85a/80-ajax.png
date: 2009-10-19T12:36:19.000Z
author: louis-lazaris
summary: >-
  Without the CSS <code>float</code> property, table-less layouts would be, at worst, impossible, and, at best, unmaintainable. Floats will continue to be prominent in CSS layouts, even as CSS3 begins to gain prominence.
description: >-
  Without the CSS <code>float</code> property, table-less layouts would be, at worst, impossible, and, at best, unmaintainable. Floats will continue to be prominent in CSS layouts, even as CSS3 begins to gain prominence.
categories:
  - Coding
  - CSS
  - Essentials
---
<p>Years ago, when developers first started to make the transition to HTML layouts without tables, one CSS property that suddenly took on a very important role was the <code>float</code> property. The reason that the <code>float</code> property became so common was that, by default, block-level elements will not line up beside one another in a column-based format. Since columns are necessary in virtually every CSS layout, this property started to get used &mdash; and even overused &mdash; prolifically.</p>

## What Is A CSS Float Property?

<p>The <strong>CSS <code>float</code> property</strong> allows a developer to incorporate table-like columns in an HTML layout without the use of tables.</p>

<p>If it were not for the CSS <code>float</code> property, CSS layouts would not be possible except using absolute and relative positioning &mdash; which would be messy and would make the layout unmaintainable.</p>

<p>In this article, <strong>we’ll discuss exactly what the <code>float</code> property is and how it affects elements</strong> in particular contexts. We’ll also take a look at some of the differences that can occur in connection with this property in the most commonly-used browsers. Finally, we’ll showcase a few practical uses for the CSS <code>float</code> property. This should provide a well-rounded and thorough discussion of this property and its impact on CSS development.</p>

{{% feature-panel %}}

## Definition And Syntax

<p>The purpose of the CSS <code>float</code> property is, generally speaking, to push a block-level element to the left or right, taking it out of the flow in relation to other block elements. This allows naturally-flowing content to wrap around the floated element. This concept is similar to what you see every day in print literature, where photos and other graphic elements are aligned to one side while other content (usually text) flows naturally around the left- or right-aligned element.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f95970b5-fb84-46c6-9578-c3e4a127f217/print.jpg" alt="Screenshot" width="500" height="333" /><br><figcaption>Flickr photo by presentday</figcaption></figure>

<p>The photo above shows the "Readers' sites" section of late <del>.net magazine</del>, which displayd 3 readers' photos each aligned left in their respective columns with text wrapping around the aligned images. That is the basic idea behind the <code>float</code> property in CSS layouts, and demonstrates one of the ways it has been used in table-less design.</p>

<p>The effectiveness of using floats in multi-columned layouts was explained by Douglas Bowman in 2004 in his classic presentation <em>No More Tables</em>:</p>

<figure><img title="No More Tables - Floats" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/598d7187-6329-48a9-a8a5-732458a6ecbc/stopdesign-float.jpg" alt="No More Tables - Floats" width="500" height="435" /></figure>

<p>Bowman explained the principles behind table-less design, using Microsoft’s old site as a case study. Floats were used prominently in his mock overhaul of the Microsoft layout.</p>

### Syntax

<p>The <code>float</code> CSS property can accept one of 4 values: <code>left</code>, <code>right</code>, <code>none</code>, and <code>inherit</code>. It is declared as shown in the code below.</p>

<pre><code class="language-css">#sidebar {
  float: left;
}
</code></pre>

<p>The most commonly-used values are <code>left</code> and <code>right</code>. A value of <code>none</code> is the default, or initial <code>float</code> value for any element in an HTML page. The value <code>inherit</code>, which can be applied to nearly any CSS property, does not work in Internet Explorer versions up to and including 7.</p>

<p>The <code>float</code> property does not require the application of any other property on a CSS element for <code>float</code> to function correctly, however, <code>float</code> will work more effectively under specific circumstances.</p>

<p>Generally, a floated element <strong>should have an explicitly set width</strong> (unless it is a <a href="https://reference.sitepoint.com/css/replacedelements">replaced element</a>, like an image). This ensures that the float behaves as expected and helps to avoid issues in certain browsers.</p>

<pre><code class="language-css">#sidebar {
  float: left;
  width: 350px;
}</code></pre>

### Specifics on Floated Elements

<p>Following is a list of exact behaviours of floated elements according to <a href="https://www.w3.org/TR/CSS1/#floating-elements">CSS2 Specifications</a>:</p>

<ul>
 	<li>A left-floated box will shift to the left until its leftmost margin edge (or border edge if margins are absent) touches either the edge of the containing block, or the edge of another floated box</li>
 	<li>If the size of the floated box exceeds the available horizontal space, the floated box will be shifted down</li>
 	<li>Non-positioned, non-floated, block-level elements act as if the floated element is not there, since the floated element is out of flow in relation to other block elements</li>
 	<li>Margins of floated boxes do not collapse with margins of adjacent boxes</li>
 	<li>The root element (<code>&lt;html&gt;</code>) cannot be floated</li>
 	<li>An inline element that is floated is converted to a block-level element</li>
</ul>

## Float In Practice

<p>One of the most common uses for the <code>float</code> property is to float an image with text wrapping it. Here is an example:</p>

<div style="border: 1px solid #aaaaaa;margin: 15px 0pt 0pt;padding: 0pt 15px 15px;background: #dddddd none repeat scroll 0% 0%;width: 470px">

<img style="float: left;margin: 15px 15px 5px 0;border: solid 1px #bbb" title="Float - Lifesaver" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faad51dc-f367-4252-8bf4-2160b5b9ff01/lifesaver.jpg" alt="Float - Lifesaver" width="200" height="222" />Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper.

Aenean ultricies mi vitae est. Mauris placerat eleifend leo. Quisque sit amet est et sapien ullamcorper pharetra. Vestibulum erat wisi, condimentum sed, commodo vitae, ornare sit amet, wisi. Aenean fermentum, elit eget tincidunt condimentum, eros ipsum rutrum orci, sagittis tempus lacus enim ac dui.

Donec non enim in turpis pulvinar facilisis. Ut felis. Praesent dapibus, neque id cursus faucibus, tortor neque egestas augue, eu vulputate magna eros eu erat. Aliquam erat volutpat. Nam dui mi, tincidunt quis, accumsan porttitor, facilisis luctus, metus.
</div>

<p>The CSS applied to the image in the box above is as follows:</p>

<pre><code class="language-css">img {
  float: left;
  margin: 0 15px 5px 0;
  border: solid 1px #bbb;
}</code></pre>

<p>The only property required to make this effect work is the <code>float</code> property. The other properties (margin and border) are there for aesthetic reasons. The other elements inside the box (the <code>&lt;p&gt;</code> tags with text inside them) do not need any styles applied to them.</p>

<p>As mentioned earlier, floated elements are taken out of flow in relation to other block elements, and so other block elements remain in flow, acting as if the floated element is not even there. This is demonstrated visually below:</p>

<div style="border: 1px solid #aaaaaa;margin: 15px 0pt 0pt;padding: 0pt 15px 15px;background: #dddddd none repeat scroll 0% 0%;overflow: hidden;width: 470px"><br>
<div style="border: 1px solid #000000;margin: 5px 15px 5px -5px;width: 200px;height: 222px;float: left">
<p style="text-align: center;line-height: 200px">This box is floated left
</div>
<p style="background: #fff">This <code>&lt;p&gt;</code> element has a different background color to show that it spans the width of its parent, ignoring the floated element. This inline text, however, wraps around the floated box.
</div>

<p>In the above example, the <code>&lt;p&gt;</code> element is a block-level element, so it ignores the floated element, spanning the width of the container (minus padding). All non-floated, block-level elements will behave in like manner.</p>

<p>The text in the paragraph is inline, so it flows around the floated element. The floated box is also given margin settings to offset it from the paragraph, making it visually clear that the paragraph element is ignoring the floated box.</p>

{{% ad-panel-leaderboard %}}

## Clearing Floats

<p>Layout issues with floats are commonly fixed using the CSS <code>clear</code> property, which lets you "clear" floated elements from the left or right side, or both sides, of an element.</p>

<p>Let’s take a look at an example that commonly occurs &mdash; a footer wrapping to the right side of a 2-column layout:</p>

<div style="border: 1px solid #aaaaaa;margin: 15px 0pt 0pt;background: #dddddd none repeat scroll 0% 0%;overflow: hidden;width: 500px"><br>
<div style="background: #666666 none repeat scroll 0% 0%;float: left;width: 200px;height: 400px;color: #ffffff">
<p style="text-align: center">Left column floated left

</div>
<div style="float: left;width: 300px;height: 400px">
<p style="text-align: center">Right column also floated left

</div>
<div style="background: #888888 none repeat scroll 0% 0%;width: 500px;height: 30px">
<p style="text-align: center;line-height: 30px;color: #fff;margin: 0">Footer

</div>
</div>

<p>If you view this page in IE6 or IE7, you won’t see any problems. The left and right columns are in place, and the footer is nicely tucked underneath. But in Firefox, Opera, Safari, and Chrome, you’ll see the footer jump up beside the left column. This is caused by the float applied to the columns. This is the correct behaviour, even though it is a more problematic one. To resolve this issue, we use the aforementioned <code>clear</code> property, applied to the footer:</p>

<pre><code class="language-css">#footer {
  clear: both;
}</code></pre>

The result is shown below:
<div style="border: 1px solid #aaaaaa;margin: 15px 0pt 0pt;background: #dddddd none repeat scroll 0% 0%;overflow: hidden;width: 500px"><br>
<div style="background: #666666 none repeat scroll 0% 0%;float: left;width: 200px;height: 400px;color: #ffffff">
<p style="text-align: center">Left column floated left

</div>
<div style="float: left;width: 300px;height: 400px">
<p style="text-align: center">Right column also floated left

</div>
<div style="background: #888888 none repeat scroll 0% 0%;width: 500px;height: 30px;clear: both">
<p style="text-align: center;line-height: 30px;color: #fff;margin: 0">Footer

</div>
</div>

<p>The <code>clear</code> property will clear only floated elements, so applying <code>clear: both</code> to both columns would not cause the footer to drop down, because the footer is not a floated element.</p>

<p>So use <code>clear</code> on non-floated elements, and even occasionally on floated elements, to force page elements to occupy their intended space.</p>

## Fixing The Collapsed Parent

<p>One of the most common symptoms of float-heavy layouts is the "collapsing parent". This is demonstrated in the example below:</p>

<div style="background: #ddd;border: solid 1px #aaa;margin: 15px 0 0 0;padding: 0 15px 15px 15px"><img style="float: left;margin: 15px 15px 5px 0;border: solid 1px #bbb" title="Float - Lifesaver" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faad51dc-f367-4252-8bf4-2160b5b9ff01/lifesaver.jpg" alt="Float - Lifesaver" width="200" height="222" />Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper.</div>

Notice that the bottom of the floated image appears outside its parent. The parent does not fully expand to hold the floated image. This is caused by what we discussed earlier: the floated element is out of the flow in relation to other block elements, so all block elements will render as if the floated element is not even there. This is not a CSS bug; it’s in line with CSS specifications. All browsers render the same in this example. It should be pointed out that, in this example, adding a width to the container prevents the issue from occurring in IE, so this would normally be something you would have to resolve in Firefox, Opera, Safari, or Chrome.

### Solution 1: Float the container

<p>The easiest way to fix this problem is to float the containing parent element:</p>

<div style="background: #ddd;border: solid 1px #aaa;margin: 15px 0 0 0;padding: 0 15px 15px 15px;float: left"><img style="float: left;margin: 15px 15px 5px 0;border: solid 1px #bbb" title="Float - Lifesaver" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faad51dc-f367-4252-8bf4-2160b5b9ff01/lifesaver.jpg" alt="Float - Lifesaver" width="200" height="222" />Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper.</div>

<p>Now the container expands to fit all the child elements. But unfortunately this fix will only work in a limited number of circumstances, since floating the parent may have undesirable effects on your layout.</p>

### Solution 2: Adding Extra Markup

<p>This is an outdated method, but is an easy option. Simply add an extra element at the bottom of the container and "clear" it. Here’s how the HTML would look after this method is implemented:</p>

<div class="break-out">

 <pre><code class="language-html">&lt;div id="container"&gt;
&lt;img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faad51dc-f367-4252-8bf4-2160b5b9ff01/lifesaver.jpg" width="200" height="222" alt="" /&gt;
&lt;p&gt;Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper.&lt;/p&gt;

  &lt;div class="clearfix"&gt;&lt;/div&gt;
&lt;/div&gt;
</code></pre>
</div>

<p>And the resulting CSS applied to the new element:</p>

<pre><code class="language-css">.clearfix {
  clear: both;
}</code></pre>

<p>You could also do this by means of a <code>&lt;br /&gt;</code> tag with an inline style. In any case, you will have the desired result: the parent container will expand to enclose all of its children. But this method is not recommended since it adds nonsemantic code to your markup.</p>

### Solution 3: The <code>:after</code> Pseudo-Element

<p>The <code>:after</code> pseudo-element adds an element to the rendered HTML page. This method has been used quite extensively to resolve float-clearing issues. Here is how the CSS looks:</p>

<pre><code class="language-css">.clearfix:after {
    content: ".";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
}</code></pre>

<p>The CSS class "clearfix" is applied to any container that has floating children and does not expand to enclose them.</p>

<p>But this method does not work in Internet Explorer up to version 7, so an IE-only style needs to be set with one of the following rules:</p>

<pre><code class="language-css">.clearfix {
  display: inline-block;
}

.clearfix {
  zoom: 1;
}</code></pre>

<p>Depending on the type of issue you’re dealing with, one of the above two solutions will resolve the issue in Internet Explorer. It should be noted that the <code>zoom</code> property is a non-standard Microsoft proprietary property, and will cause your CSS to become invalid.</p>

<p>So, because the <code>:after</code> pseudo-element solution does not work in IE6/7, is a little bit bloated code-wise, and requires additional invalid IE-only styles, this solution is not the best method, but is probably the best we’ve considered so far.</p>

### Solution 4: The Overflow Property

<p>By far the best, and easiest solution to resolve the collapsing parent issue is to add <code>overflow: hidden</code> or <code>overflow: auto</code> to the parent element. It’s clean, easy to maintain, works in almost all browsers, and does not add extra markup.</p>

<p>You’ll notice I said "almost" all browsers. This is because it does not work in IE6. But, in many cases, the parent container will have a set width, which fixes the issue in IE6. If the parent container does not have a width, you can add an IE6-only style with the following code:</p>

<pre><code class="language-css">// This fix is for IE6 only
.clearfix {
  height: 1%;
  overflow: visible;
}</code></pre>

<p>In IE6, the <code>height</code> property is incorrectly treated as <code>min-height</code>, so this forces the container to enclose its children. The <code>overflow</code> property is then set back to "visible", to ensure the content is not hidden or scrolled.</p>

<p>The only drawback to using the <code>overflow</code> method (in any browser) is the possibility that the containing element will have scrollbars or hide content. If there are any elements with negative margins or absolute positioning inside the parent, they will be obscured if they go beyond the parent’s borders, so this method should be used carefully. It should also be noted that if the containing element has to have a specified <code>height</code>, or <code>min-height</code>, then you would definitely not be able to use the <code>overflow</code> method.</p>

<p>So, there really is no simple, cross-browser solution to the collapsing parent issue. But almost any float clearing issue can be resolved with one of the above methods.</p>

{{% ad-panel-leaderboard %}}

## Float-Related Bugs In Internet Explorer

<p>Over the years, there have been numerous articles published online that discuss common bugs in connection with floats in CSS layouts. All of these, not surprisingly, deal with problems specific to Internet Explorer. Below, you’ll find a list of links to a number of articles that discuss float-related issues in-depth:</p>

<ul>
 	<li><a href="https://css-class.com/articles/explorer/guillotine/index.htm">The Internet Explorer Guillotine Bug</a></li>
 	<li><a href="https://www.positioniseverything.net/explorer/doubled-margin.html">The IE5/6 Doubled Float-Margin Bug</a></li>
 	<li><a href="https://www.maratz.com/blog/archives/2006/11/11/ie-7-quirks-floats-and-margins/">IE7 Bottom Margin Bug</a></li>
 	<li><a href="https://www.positioniseverything.net/explorer/escape-floats.html">The IE Escaping Floats Bug</a></li>
 	<li><a href="https://www.positioniseverything.net/explorer/peekaboo.html">The IE6 Peekaboo Bug</a></li>
 	<li><a href="https://www.impressivewebs.com/ie6-ghost-text-bug-with-multiple-solutions/">The IE6 "Ghost Text" Bug</a></li>
 	<li><a href="https://www.positioniseverything.net/explorer/expandingboxbug.html">The IE6 Expanding Box Problem</a></li>
 	<li><a href="https://www.positioniseverything.net/explorer/threepxtest.html">The IE6 3-pixel Gap</a></li>
</ul>

## Changing the Float Property with JavaScript

<p>To change a CSS value in JavaScript, you would access the <code>style</code> object, converting the intended CSS property to "camel case". For example, the CSS property "margin-left" becomes <code>marginLeft</code>; the property <code>background-color</code> becomes <code>backgroundColor</code>, and so on. But with the <code>float</code> property, it’s different, because <code>float</code> is already a reserved word in JavaScript. So, the following would be incorrect:</p>

<pre><code class="language-javascript">myDiv.style.float = "left";</code></pre>

<p>Instead, you would use one of the following:</p>

<pre><code class="language-javascript">// For Internet Explorer
myDiv.style.styleFloat = "left";

// For all other browsers
myDiv.style.cssFloat = "left";</code></pre>

## Practical Uses For Float

<p>Floats can be used to resolve a number of design challenges in CSS layouts. Some examples are discussed here.</p>

### 2-Column, Fixed-Width Layout

<p>Roger Johansson of <a href="https://www.456bereastreet.com/">456 Berea Street</a> outlines an 8-step tutorial to create a simple, cross-browser, 2-column, horizontally centered layout. The <code>float</code> property is integral to the chemistry of this layout.</p>

<blockquote>"The layout consists of a header, a horizontal navigation bar, a main content column, a sidebar, and a footer. It is also horizontally centered in the browser window. A pretty basic layout, and not at all difficult to create with CSS once you know how to deal with the inevitable Internet Explorer bugs."</blockquote>

<figure><a href="https://www.456bereastreet.com/lab/developing_with_web_standards/csslayout/2-col/"><img title="2-Column Layout" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b720c3b-944d-41b4-acf0-cef1448f64de/2-column-layout.jpg" alt="2-Column Layout" width="500" height="385" /></a><figcaption><a href="https://www.456bereastreet.com/lab/developing_with_web_standards/csslayout/2-col/">Simple 2 column CSS layout</a></figcaption></figure>

### 3-Column, Equal-Height Layout

<p>Petr Stanicek of <a href="https://www.pixy.cz">pixy.cz</a> demonstrates a cross-browser 3-column layout, again using <code>float</code>:</p>

<blockquote>"No tables, no absolute positioning (no positioning at all), no hacks(!), same height of all columns. The left and right columns have fixed width (150px), the middle one is elastic."</blockquote>

<figure><a href="https://www.pixy.cz/blogg/clanky/css-3col-layout/"><img title="3-Column Layout" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3142bbe-9780-439d-b29d-c49d67c82165/3-column-layout.jpg" alt="3-Column Layout" width="500" height="328" /></a><figcaption><a href="https://www.pixy.cz/blogg/clanky/css-3col-layout/">3-Column Layout with CSS</a></figcaption></figure>

### Floated Image With Caption

<p>Similar to what we discussed earlier under "Float in Practice", <a href="https://www.maxdesign.com.au/">Max Design</a> describes how to float an image with a caption, allowing text to wrap around it naturally.</p>

<figure><a href="https://css.maxdesign.com.au/floatutorial/tutorial0211.htm"><img title="Floated Image with Caption" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f2bd303-b50c-4d7d-a20e-55aa3b8f3001/floated-image.jpg" alt="Floated Image with Caption" width="500" height="439" /></a><figcaption><a href="https://css.maxdesign.com.au/floatutorial/tutorial0211.htm">Floating an Image and Caption</a></figcaption></figure>

### Horizontal Navigation With Unordered Lists

<p>The <code>float</code> property is a key ingredient in coding sprite-based horizontal navigation bars. Chris Spooner of <a href="https://line25.com/">Line25</a> describes how to create a <a href="https://line25.com/tutorials/how-to-create-a-css-menu-using-image-sprites">Menu of Awesomeness</a>, in which the <code>&lt;li&gt;</code> elements that hold the navigation buttons are floated left:</p>

<figure><a href="https://line25.com/tutorials/how-to-create-a-css-menu-using-image-sprites"><img title="Menu of Awesomeness" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bc710c4-e9b6-4604-8ddd-0cba95c9de8e/menu.jpg" alt="Menu of Awesomeness" width="500" height="372" /></a><figcaption><a href="https://line25.com/tutorials/how-to-create-a-css-menu-using-image-sprites">How to Create a CSS Menu Using Image Sprites</a></figcaption></figure>

<p>To demonstrate the importance of the <code>float</code> property in this example, here is a screen shot of the same image after using firebug to remove the <code>float: left</code>:</p>

<figure><img title="Menu of Awesomeness without Float" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/796a56f4-ebbc-4150-a3c6-62def6f06666/menu-nofloat.jpg" alt="Menu of Awesomeness without Float" width="500" height="430" /></figure>

### Grid-Based Photo Galleries

<p>A simple use for the <code>float</code> property is to left-float a series of photos contained in an unordered list, which gets the same result as what you would see in a table-based layout.</p>

<figure><img title="Foremost Canada" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/119c0a7d-56ae-4555-9f2f-47d691b8f06e/foremost.jpg" alt="Foremost Canada" width="500" height="500" /></figure>

<p>Foremost Canada’s product page (above) displays their products in grid-based format, next to a left-column sidebar. The photos are displayed in an unordered list with the float property for all <code>&lt;li&gt;</code> elements set to <code>float: left</code>. This works better than a table-based grid, because the number of photos in the gallery can change and the layout would not be affected.</p>

<figure><img title="Paragon Furniture" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc5a7aad-217b-435b-9fec-f8c5aa42249b/paragon.jpg" alt="Paragon Furniture" width="500" height="500" /></figure>

<p>Paragon Furniture’s futons page (above) is another example of a product page using an unordered list with floated list items.</p>

<figure><a href="https://www.istockphoto.com/file_search.php?text=trees&amp;action=file"><img title="iStockphoto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61a3b45c-05e5-4d3c-b87e-738f147327d7/istockphoto.jpg" alt="iStockphoto" width="500" height="466" /></a></figure>

<p><a href="https://www.istockphoto.com/file_search.php?text=trees&amp;action=file">iStockphoto’s search results page</a> (above) is a similarly-structured grid of photos, but this time the photos are contained in left-floated <code>&lt;div&gt;</code> elements, instead of <code>&lt;li&gt;</code> elements.</p>

### Aligning an &lt;input&gt; Field with a Button

<p>Default styling on form elements across different browsers can be a pain to deal with. Often times, in a single-field form like a search form, it is necessary to place the <code>&lt;input&gt;</code> element next to the submit button. Here is a simple search form, with an image used for the submit button:</p>

<p>In every browser, the result is the same: The button appears slightly higher than the input field. Changing margins and padding does nothing. The simple way to fix this is to float the input field left, and add a small right margin. Here is the result:</p>

## Conclusion

<p>As was mentioned at the outset, without the CSS <code>float</code> property, table-less layouts would be, at worst, impossible, and, at best, unmaintainable. Floats will continue to be prominent in CSS layouts, even as CSS3 begins to gain prominence &mdash; even though there have been a few discussions about <a href="https://tjkdesign.com/articles/float-less_css_layouts.asp">layouts without the use of floats</a>.</p>

<p>Hopefully this discussion has simplified some of the mysteries related to floats, and provided some practical solutions to a number of issues faced by CSS developers today.</p>

### Further Reading

<ul>
 	<li><a href="https://reference.sitepoint.com/css/float">Sitepoint CSS Reference: Float</a></li>
 	<li><a href="https://css-tricks.com/all-about-floats/">All About Floats on CSS-Tricks</a></li>
 	<li><a href="https://www.sitepoint.com/blogs/2005/02/26/simple-clearing-of-floats/">Simple Clearing of Floats</a></li>
 	<li><a href="https://www.w3.org/TR/CSS2/visuren.html#floats">Visual Formatting Model: Floats</a></li>
 	<li><a href="https://reference.sitepoint.com/css/floatclear">Floating and Clearing</a></li>
</ul>

{{< signature "il" >}}

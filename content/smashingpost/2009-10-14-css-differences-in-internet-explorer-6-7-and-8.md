---
title: 'CSS Differences in Internet Explorer 6, 7 and 8'
slug: css-differences-in-internet-explorer-6-7-and-8
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee31d118-ac23-4cfb-93f4-8a39a8220bc1/illuie9.png
date: 2009-10-14T10:07:37.000Z
author: louis-lazaris
description: >-
  One of the most bizarre statistical facts in relation to browser use has to be
  the virtual widespread numbers that currently exist in the use of **Internet
  Explorer** versions 6, 7 and 8\. As of this writing, Internet Explorer holds
  about a 65% market share combined across all their currently used browsers. In
  the web development community, this number is much lower, showing about a 40%
  share.

  The interesting part of those statistics is that the numbers across IE6, IE7,
  and IE8 are very close, preventing a single Microsoft browser from dominating
  browser stats — contrary to what has been the trend in the past. Due to these
  unfortunate statistics, it is imperative that developers do thorough testing
  in all currently-used Internet Explorer browsers when working on websites for
  clients, and on personal projects that target a broader audience.

  This article will attempt to provide an **exhaustive, easy-to-use reference
  for developers desiring to know the differences in CSS support for IE6, IE7
  and IE8**.
categories:
  - Coding
  - CSS
  - Testing
  - Internet Explorer
  - Essentials
---
One of the most bizarre statistical facts in relation to browser use has to be the virtual widespread numbers that currently exist in the use of <strong>Internet Explorer</strong> versions 6, 7 and 8. As of this writing, <a href="https://marketshare.hitslink.com/browser-market-share.aspx?qprid=0">Internet Explorer holds about a 65% market share</a> combined across all their currently used browsers. In the web development community, this number is much lower, showing <a href="https://www.w3schools.com/browsers/browsers_stats.asp">about a 40% share</a>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e4d9b44-1c32-4f35-aeb7-53883dc973c6/ie.jpg" alt="Screenshot" width="500" height="441" />

The interesting part of those statistics is that the numbers across IE6, IE7, and IE8 are very close, preventing a single Microsoft browser from dominating browser stats — contrary to what has been the trend in the past. Due to these unfortunate statistics, it is <strong>imperative that developers do thorough testing in all currently-used Internet Explorer browsers</strong> when working on websites for clients, and on personal projects that target a broader audience.

You may also be interested in the following articles we published later:

*   [It’s Time To Stop Blaming Internet Explorer](https://www.smashingmagazine.com/2012/07/its-time-to-stop-blaming-internet-explorer/)
*   [CSS3 Solutions for Internet Explorer](https://www.smashingmagazine.com/2010/04/css3-solutions-for-internet-explorer/)
*   [The Life, Times (and Death?) of Internet Explorer 6 (Comic Strip)](https://www.smashingmagazine.com/2010/02/the-life-times-and-death-of-internet-explorer-6-comic-strip/)

{{% feature-panel %}}

Thanks to the many available JavaScript libraries, JavaScript testing across different browsers has become as close to perfect as the current situation will allow. But this is not true in CSS development, particularly in relation to the three currently used versions of Internet Explorer.

This article will attempt to provide an <strong>exhaustive, easy-to-use reference for developers desiring to know the differences in CSS support for IE6, IE7 and IE8</strong>. This reference contains brief descriptions and compatibility for:

*   Any item that is supported by one of the three browser versions, but not the other two
*   Any item that is supported by two of the three browser versions, but not the other one

This article does not discuss:

*   Any item that is not supported by any of the three browser versions
*   Proprietary or vendor-specific CSS

Therefore, the focus is on <em>differences</em> in the three, not necessarily lack of support. The list is divided into five sections:

*   [Selectors & Inheritance](#selectors)
*   [Pseudo-Classes and Pseudo-Elements](#pseudo_classes)
*   [Property Support](#property)
*   [Other Miscellaneous Techniques](#other)
*   [Significant Bugs and Incompatibilities](#bugs)

## Selectors & Inheritance

### Child Selectors

#### Example

<pre><code class="language-css">body&gt;p {
  color: #fff;
}</code></pre>

#### Description

The child selector selects all elements that are immediate children of a specified parent element. In the example above, <code>body</code> is the parent, and <code>p</code> is the child.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

#### Bugs

In IE7, the child selector will not work if there is an HTML comment between the parent item and the child.</p>

### Chained Classes

#### Example

<pre><code class="language-css">.class1.class2.class3 {
  background: #fff;
}</code></pre>

#### Description

Chained classes are used when the same HTML element has multiple classes declared, like this:
<pre class="html"> 
&lt;div class="class1 class2 class3"&gt;
&lt;p&gt;Content here.&lt;/p&gt;
&lt;/div&gt;
</pre>

#### Support

<div style="overflow: hidden">
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

#### Bugs

IE6 appears to support this property, because it matches the last class in the chain to an element having that class, however, it does not restrict the class to an element that has all the classes in the chain, like it should.</p>

### Attribute Selectors

#### Example

<pre><code class="language-css">a[href] {
  color: #0f0;
}</code></pre>

#### Description

This selector allows an element to be targeted only if it has the specified attribute. In the example above, all anchor tags that have <code>href</code> attributes would qualify, but not anchor tags that did not have <code>href</code> attributes.

#### Support

<div style="overflow: hidden">
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Adjacent Sibling Selectors

#### Example

<pre><code class="language-css">h1+p {
  color: #f00;
}</code></pre>

#### Description

This selector targets siblings that are adjacent to the specified element. The example above would target all paragraph tags that are siblings of, and come directly after, primary heading tags. For example:
<pre class="html"> 
&lt;h1&gt;heading&lt;/h1&gt;
&lt;p&gt;Content here.&lt;/p&gt;
&lt;p&gt;Content here.&lt;/p&gt;
</pre>

In the code above, the CSS styles specified would target only the first paragraph, because it is a sibling to the &lt;h1&gt; tag and is adjacent. The second paragraph is a sibling, but is not adjacent.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

#### Bugs

In IE7, the adjacent sibling selector will not work if there is an HTML comment between the siblings.</p>

### General Sibling Selectors

#### Example

<pre><code class="language-css">h1~p {
  color: #f00;
}</code></pre>

#### Description

This selector targets all siblings that appear after a specified element. Applying this selector to the HTML example given in the previous section will select both paragraph tags, however, if one of the paragraphs appeared before the heading, that paragraph would not be targeted.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

## Pseudo-Classes and Pseudo-Elements

### Descendant Selector After :hover Pseudo-Class

#### Example

<pre><code class="language-css">a:hover span {
  color: #0f0;
}</code></pre>

#### Description

An element can be targeted with a selector after a :hover pseudo class, similar to how any descendant selector works. The above example would change the font color inside all <code>&lt;span&gt;</code> elements inside of anchor elements while the anchor is hovered over.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Chained Pseudo-Classes

#### Example

<pre><code class="language-css">a:first-child:hover {
  color: #0f0;
}</code></pre>

#### Description

Pseudo-classes can be chained to narrow element selection. The above example would target every anchor tag that is the first child of its parent and apply a hover class to it.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### :hover on Non-Anchor Elements

#### Example

<pre><code class="language-css">div:hover {
  color: #f00;
}</code></pre>

#### Description

The <code>:hover</code> pseudo-class can apply a hover, or rollover state, to any element, not just anchor tags.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### :first-child Pseudo-Class

#### Example

<pre><code class="language-css">div li:first-child {
  background: blue;
}</code></pre>

#### Description

This pseudo-class targets each specified element that is the first child of its parent.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

#### Bugs

In IE7, the first-child pseudo-class will not work if an HTML comment appears before the targeted first child element.</p>

### :focus Pseudo-Class

#### Example

<pre><code class="language-css">a:focus {
  border: solid 1px red;
}</code></pre>

#### Description

This pseudo-class targets any element that has keyboard focus.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### :before and :after Pseudo-Elements

#### Example

<pre><code class="language-css">#box:before {
  content: "This text is before the box";
}

#box:after {
  content: "This text is after the box";
}</code></pre>

#### Description

This pseudo-element places generated content before or after the specified element, used in conjunction with the <code>content</code> property.

#### Support

<div style="overflow: hidden">
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

## Property Support

### Virtual Dimensions Determined by Position

#### Example

<pre><code class="language-css">#box {
  position: absolute;
  top: 0;
  right: 100px;
  left: 0;
  bottom: 200px;
  background: blue;
}</code></pre>

#### Description

Specifying <code>top</code>, <code>right</code>, <code>bottom</code>, and <code>left</code> values for an absolutely positioned element will give the element "virtual" dimensions (width and height), even if width and height are not specified.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Min-Height & Min-Width

#### Example

<pre><code class="language-css">#box {
  min-height: 500px;
  min-width: 300px;
}</code></pre>

#### Description

These properties specify minimum values for either height or width, allowing a box to be larger, but not smaller, than the specified minimum values. They can be used together or individually.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Max-Height & Max-Width

#### Example

<pre><code class="language-css">#box {
  max-height: 500px;
  max-width: 300px;
}</code></pre>

#### Description

These properties specify maximum values for either height or width, allowing a box to be smaller, but not larger, than the specified minimum values. They can be used together or individually.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Transparent Border Color

#### Example

<pre><code class="language-css">#box {
  border: solid 1px transparent;
}</code></pre>

#### Description

A transparent border color allows a border to occupy the same space as would be occupied if the border was visible, or opaque.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Fixed-Position Elements

#### Example

<pre><code class="language-css">#box {
  position: fixed;
}</code></pre>

#### Description

This value for the <code>position</code> property allows an element to be positioned absolutely relative to the viewport.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Fixed-Position Background Relative to Viewport

#### Example

<pre><code class="language-css">#box {
  background-image: url(images/bg.jpg);
  background-position: 0 0;
  background-attachment: fixed;
}</code></pre>

#### Description

A <code>fixed</code> value for the <code>background-attachment</code> property allows a background image to be positioned absolutely relative to the viewport.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
Yes</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

#### Bugs

IE6 incorrectly fixes the background image in relation to the containing parent of the element that has the background set, therefore this value only works in IE6 when its used on the root element.</p>

### Property Value "inherit"

#### Example

<pre><code class="language-css">#box {
  display: inherit;
}</code></pre>

#### Description

Applying the value <code>inherit</code> to a property allows an element to inherit the computed value for that property from its containing element.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

#### Bugs

IE6 and IE7 do not support the value <code>inherit</code> except when applied to the <code>direction</code> and <code>visibility</code> properties.</p>

### Border Spacing on Table Cells

#### Example

<pre><code class="language-css">table td {
  border-spacing: 3px;
}</code></pre>

#### Description

This property sets the spacing between the borders of adjacent table cells.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Rendering of Empty Cells in Tables

#### Example

<pre><code class="language-css">table {
  empty-cells: show;
}</code></pre>

#### Description

This property, which only applies to elements that have their <code>display</code> property set to <code>table-cell</code>, allows empty cells to be rendered with their borders and backgrounds, or else hidden.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Vertical Position of a Table Caption

#### Example

<pre><code class="language-css">table {
  caption-side: bottom;
}</code></pre>

#### Description

This property allows a table caption to appear at the bottom of a table, instead of at the top, which is the default.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Clipping Regions

#### Example

<pre><code class="language-css">#box {   
    clip: rect(20px, 300px, 200px, 100px)   
}</code></pre>

#### Description

This property specifies an area of a box that is visible, making the rest "clipped", or invisible.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

#### Bugs

Interestingly, this property works in IE6 and IE7 if the deprecated comma-less syntax is used (i.e. whitespace between the clipping values instead of commas)

### Orphaned and Widowed Text in Printed Pages

#### Example

<pre><code class="language-css">p {
  orphans: 4;
}

p {
  widows: 4;
}</code></pre>

#### Description

The <code>orphans</code> property specifies the minimum number of lines to display at the bottom of a printed page. The <code>widows</code> property specifies the minimum number of lines to display at the top of a printed page.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Page Breaks Inside Boxes

#### Example

<pre><code class="language-css">#box {
  page-break-inside: avoid;
}</code></pre>

#### Description

This property specifies whether a page break should occur inside of a specified element or not.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Outline Properties

#### Example

<pre><code class="language-css">#box {
  outline: solid 1px red;
}</code></pre>

#### Description

<code>outline</code> is the shorthand property that encompasses <code>outline-style</code>, <code>outline-width</code>, and <code>outline-color</code>. This property is preferable to the <code>border</code> property since it does not affect document flow, thus better aiding debugging of layout issues.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Alternative Values for the Display Property

#### Example

<pre><code class="language-css">#box {
  display: inline-block;
}</code></pre>

#### Description

The <code>display</code> property is usually set to <code>block</code>, <code>inline</code>, or <code>none</code>. Alternative values include:

*   `inline-block`
*   `inline-table`
*   `list-item`
*   `run-in`
*   `table`
*   `table-caption`
*   `table-cell`
*   `table-column`
*   `table-column-group`
*   `table-footer-group`
*   `table-header-group`
*   `table-row`
*   `table-row-group`

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Handling of Collapsible Whitespace

#### Example

<pre><code class="language-css">p {
  white-space: pre-line;
}

div {
  white-space: pre-wrap;
}</code></pre>

#### Description

The <code>pre-line</code> value for the <code>white-space</code> property specifies that multiple whitespace elements collapse into a single space, while allowing explicitly set line breaks. The <code>pre-wrap</code> value for the <code>white-space</code> property specifies that multiple whitespace elements do not collapse into a single space, while allowing explicitly set line breaks.

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

## Other Miscellaneous Techniques

### Media Types for @import

#### Example

<pre><code class="language-css">@import url("styles.css") screen;</code></pre>

#### Description

A media type for an imported style sheet is declared after the location of the style sheet, as in the example above. In this example, the media type is "screen".

#### Support

<div style="overflow: hidden"><br>
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

#### Bugs

Although IE6 and IE7 support <code>@import</code>, they fail when a media type is specified, causing the entire <code>@import</code> rule to be ignored.</p>

### Incrementing of Counter Values

#### Example

<pre><code class="language-css">h2 {
  counter-increment: headers;
}

h2:before {
  content: counter(headers) ". ";
}</code></pre>

#### Description

This CSS technique allows auto-incrementing numbers to appear before specified elements, and is used in conjunction with the <code>before</code> pseudo-element.

#### Support

<div style="overflow: hidden">
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

### Quote Characters for Generated Content

#### Example

<pre><code class="language-css">q {
  quotes: "'" "'";
}

q:before {
  content: open-quote;
}

q:after {
  content: close-quote;
}</code></pre>

#### Description

Specifies the quote characters to use for generated content applied to the <code>q</code> (quotation) tag.

#### Support

<div style="overflow: hidden">
<div style="float: left;border: solid 1px #ccc;padding: 15px;text-align: center;width: 50px"><strong>IE6</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE7</strong>
No</div>
<div style="float: left;border: solid 1px #ccc;padding: 15px;margin: 0 0 0 -1px;text-align: center;width: 50px"><strong>IE8</strong>
Yes</div>
</div>

## Significant Bugs and Incompatibilities

Following is a brief description of various <strong>bugs that occur in IE6 and IE7 that are not described</strong> or alluded to above. This list does not include items that lack support in all three browsers.</p>

### IE6 Bugs

*   Doesn't support styling of the `<abbr>` element
*   Doesn't support classes and IDs that begin with a hyphen or underscore
*   `<select>` elements always appear at the top of the stack, unaffected by `z-index` values
*   `:hover` pseudo-class values are ignored if anchor pseudo-classes are not in the correct order (`:link`, `:visited`, `:hover`)
*   An `!important` declaration on a property is overridden by a 2nd declaration of the same property in the same rule set that doesn't use `!important`
*   `height` behaves like `min-height`
*   `width` behaves like `min-width`
*   Left and right margins are doubled on floated elements that touch their parents' side edges
*   Dotted borders appear identical to dashed borders
*   `line-through` value for `text-decoration` property appears higher on the text than on other browsers
*   List items for an ordered list that have a layout will not increment their numbers, leaving all list items preceded by the number "1"
*   List items don't support all possible values for `list-style-type`
*   List items with a specified `list-style-image` will not display the image if they are floated
*   Offers only partial support for `@font-face`
*   Some selectors will wrongly match comments and the doctype declaration
*   If an ID selector combined with a class selector is unmatched, the same ID selector combined with different class selectors will also be treated as unmatched

### IE7 Bugs

*   List items for an ordered list that have a layout will not increment their numbers, leaving all list items preceded by the number "1"
*   List items don't support all possible values for `list-style-type`
*   List items with a specified `list-style-image` will not display the image if they are floated
*   Offers only partial support for `@font-face`
*   Some selectors will wrongly match comments and the doctype declaration

Some IE bugs not mentioned here occur only under particular circumstances, and are not specific to one particular CSS property or value. See the references below for some of those additional issues.</p>

## Further Resources

*   [Details of Changes in Internet Explorer 8](https://www.howtocreate.co.uk/ie8.html)
*   [CSS Compatibility for Internet Explorer (MSDN)](https://msdn.microsoft.com/en-us/library/cc351024(VS.85).aspx)
*   [CSS Improvements in Internet Explorer 8 (MSDN)](https://msdn.microsoft.com/en-us/library/cc304082(VS.85).aspx)
*   [Internet Explorer Exposed - CSS Bugs @ Position Is Everything](https://www.positioniseverything.net/explorer.html)
*   [SitePoint CSS Reference](https://reference.sitepoint.com/css)
*   [CSS Contents and Browser Compatibility](https://www.quirksmode.org/css/contents.html)
*   [10 Useful CSS Properties Not Supported By Internet Explorer](https://www.impressivewebs.com/10-useful-css-properties-not-supported-by-internet-explorer/)


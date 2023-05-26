---
title: 'Mastering CSS Coding: Getting Started'
slug: mastering-css-coding-getting-started
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/149f4fb5-992e-4ee3-8a2b-6a5e5d0a3d93/60-usable.png
date: 2009-10-05T13:16:55.000Z
author: soh-tanaka
summary: >-
  CSS has become the standard for building websites in today's industry. Whether you are a hardcore developer or designer, you should be familiar with it. CSS is the bridge between programming and design, and any Web professional must have some general knowledge of it.
description: >-
  CSS has become the standard for building websites in today's industry. It is the bridge between programming and design, and any Web professional must have some general knowledge of it.
categories:
  - Coding
  - CSS
  - Essentials
---
If you are getting your feet wet with CSS, this is the perfect time to fire up your favorite text editor and follow along in this tutorial as we cover the most common and practical uses of CSS.

We'll start with what you could call the <strong>fundamental</strong> properties and capabilities of CSS, ones that we commonly use to build CSS-based websites:

1.  [Padding vs. margin](#CSS-Basics1)
2.  [Floats](#CSS-Basics2)
3.  [Center alignment](#CSS-Basics3)
4.  [Ordered vs. unordered lists](#CSS-Basics4)
5.  [Styling headings](#CSS-Basics5)
6.  [Overflow](#CSS-Basics6)
7.  [Position](#CSS-Basics7)

Once you are comfortable with the basics, we will kick it up a notch with some neat tricks to build your CSS website from scratch and make some <strong>enhancements</strong> to it.

1.  [Background images](#CSS-Basics8)
2.  [Image enhancement](#CSS-Basics9)
3.  [PSD to XHTML](#CSS-Basics10)

### <span class="rh">Further Reading</span> on SmashingMag:

*   [70 Expert Ideas For Better CSS Coding](https://www.smashingmagazine.com/2007/05/expert-ideas-better-css-coding/)
*   [CSS3 Flexible Box Layout Explained](https://www.smashingmagazine.com/2011/09/css3-flexible-box-layout-explained/)
*   [Challenging CSS Best Practices](https://www.smashingmagazine.com/2013/10/challenging-css-best-practices-atomic-approach/)
*   [The Mystery Of The CSS Float Property](https://www.smashingmagazine.com/2009/10/the-mystery-of-css-float-property/)

{{% feature-panel %}}

## 1. Padding vs. Margin

Most beginners get <a href="https://www.w3schools.com/css/css_padding.asp">padding</a> and <a href="https://www.w3schools.com/CSS/css_margin.asp">margins</a> mixed up and use them incorrectly. Practices such as using the <code>height</code> to create padding or margins also lead to bugs and inconsistencies. Understanding padding and margins is fundamental to using CSS.</p>

### What Is Padding And Margin?

Padding is the <strong>inner</strong> space of an element, and margin is the <strong>outer</strong> space of an element.

The difference becomes clear once you apply backgrounds and borders to an element. Unlike padding, margins are not covered by either the background or border because they are the space outside of the actual element.

Take a look at the visual below:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90828274-8b32-4d2f-a41b-6a09472f6951/1-a.gif" alt="Box Model" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb6352fb-2e09-4ca3-b153-5ea2a840e5f1/1-c.gif" alt="Padding/Margin Values" /><br>
<em>Margin and padding values are set clockwise, starting from the top.</em>

<strong>Practical example</strong>: Here is an <code>&lt;h2&gt;</code> heading between two paragraphs. As you can see, the margin creates white space between the paragraphs, and the padding (where you see the background gray color) gives it some breathing room.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df3e2b60-5944-43be-ad19-a4f00e25a9de/1-b.gif" alt="Box Model - Example" />

### Margin And Padding Values

In the above example of the heading, the values for the margin and padding would be:

<pre><code class="language-css">margin: 15px 0 15px 0;
padding: 15px 15px 15px 15px;</code></pre>

To optimize this line of code further, we use an optimization technique called "<a href="https://www.smashingmagazine.com/2008/08/18/7-principles-of-clean-and-optimized-css-code/">shorthand</a>," which cuts down on repetitive code. Applying the shorthand technique would slim the code down to this:

<pre><code class="language-css">margin: 15px 0; /*--top and bottom = 15px | right and left = 0 --*/
padding: 15px; /*--top, right, bottom and left = 15px --*/</code></pre>

Here is what the <strong>complete CSS</strong> would look like for this heading:

<pre><code class="language-css">h2 {
background: #f0f0f0;
border: 1px solid #ddd;
margin: 15px 0;
padding: 15px;
}</code></pre>

### Quick Tip

Keep in mind that padding <strong>adds to the total width</strong> of your element. For example, if you had specified that the element should be 100 pixels wide, and you had a left and right padding of 10 pixels, then you would end up with 120 pixels in total.

100px (content) + 10px (left padding) + 10px (right padding) = 120px (total width of element)

Margin, however, expands the box model but does not directly affect the element itself. This tip is especially handy when lining up columns in a layout!

Additional resources:

*   [Box Model](https://www.w3.org/TR/CSS2/box.html)
*   [Margins and Padding](https://htmldog.com/guides/cssbeginner/margins/)
*   [The Definitive Guide to Using Negative Margins](https://www.smashingmagazine.com/2009/07/27/the-definitive-guide-to-using-negative-margins/)
*   [CSS Shorthand Guide](https://www.dustindiaz.com/css-shorthand/)
*   [CSS Margin](https://www.tizag.com/cssT/margin.php)
*   [CSS Padding](https://www.tizag.com/cssT/padding.php)

{{% ad-panel-leaderboard %}}

## 2. Floats

Floats are a fundamental element in building CSS-based websites and can be used to align images and build layouts and columns. If you recall how to align elements left and right in HTML, floating works in a similar way.

According to <a href="https://htmldog.com/reference/cssproperties/float/">HTML Dog</a>, the <code>float</code> property "specifies whether a fixed-width box should float, shifting it to the right or left, with surrounding content flowing around it."

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67dff816-1cfe-498b-95ff-e5df0db298d5/2-a.jpg" alt="Float" />

The <code>float: left</code> value aligns elements to the left and can also be used as a solid container to create layouts and columns. Let's look at a practical situation in which you can use <code>float: left</code>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c3c44d9-8f8c-4358-918a-7552e538c0ce/2-b.jpg" alt="Float to Create Layouts" />

The <code>float: right</code> value aligns elements to the right, with surrounding elements flowing to the left.

<strong>Quick tip:</strong> Because block elements typically span 100% of their parent container's width, floating an element <strong>to the right</strong> knocks it down to the next line. This also applies to plain text that runs next to it because the floated element cannot squeeze in the same line.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc10133c-9403-4b13-aa51-5c74b8ce38fc/2-c.gif" alt="Floating right bug" />

You can correct this issue in one of two ways:

1.  **Reverse the order of the HTML markup** so that you call the floated element first, and the neighboring element second. ![Floating right fix](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c186120-2312-4ee3-85e7-097b33162036/2-c1.gif)
2.  **Specify an exact width for the neighboring element** so that when the two elements sit side by side, their combined width is less than or equal to the width of their parent container. ![Floating right fix](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acd02a30-6f56-4f0e-b0ed-d8de3943e42d/2-c2.gif)

Internet Explorer 6 (IE6) has been known to <strong>double</strong> a floated element's margin. So, what you originally specified as a 5-pixel margin becomes 10 pixels in IE6.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0eb20c8b-2272-4879-85f4-8f2db9966a0d/upd-2-d.gif" alt="Double Margin Bug - IE6" />

A simple trick to get around this bug is to add <code>display: inline</code> to your floated element, like so:

<pre><code class="language-css">.floated_element {
float: left;
width: 200px;
margin: 5px;
display: inline; /*--IE6 workaround--*/
}</code></pre>

Additional resources:

*   [Floatutorial](https://css.maxdesign.com.au/floatutorial/)
*   [Clearing Floats](https://www.quirksmode.org/css/clearing.html)
*   [CSS Float Theory: Things You Should Know](https://www.smashingmagazine.com/2007/05/01/css-float-theory-things-you-should-know/)
*   [CSS-Tricks: All About Floats](https://css-tricks.com/all-about-floats/)
*   [Containing Floats](https://www.complexspiral.com/publications/containing-floats/)
*   W3Schools: Clear
*   W3Schools: Float

## 3. Center Alignment

The days of using the <code>&lt;center&gt;</code> HTML tag are long gone. Let's look at the various ways of center-aligning an element.</p>

### Horizontal Alignment

You can horizontally align text elements using the <code>text-align</code> property. This is quite simple to do, but keep in mind when center-aligning <a href="https://en.wikipedia.org/wiki/HTML_element#Inline_elements">inline</a> <a href="https://htmlhelp.com/reference/html40/inline.html">elements</a> that you must add <code>display: block</code>. This allows the browser to determine the boundaries on which to base its alignment of your element.

<pre><code class="language-css">.center {
text-align: center;
display: block; /*--For inline elements only--*/
}</code></pre>

To horizontally align non-textual elements, use the <a href="https://www.w3schools.com/CSS/css_margin.asp"><code>margin</code></a> property.

The <a href="https://www.w3.org/TR/CSS21/visudet.html#blockwidth">W3C</a> says, "If both <code>margin-left</code> and <code>margin-right</code> are <code>auto</code>, their used values are equal. This horizontally centers the element with respect to the edges of the containing block."

Horizontal alignment can be achieved, then, by setting the left and right margins to <code>auto</code>. This is an ideal method of horizontally aligning non-text-based elements; for example, layouts and images. But when center-aligning a layout or element without a specified width, you must specify a width in order for this to work.

To center-align a layout:

<pre><code class="language-css">.layout_container {
margin: 0 auto;
width: 960px;
}</code></pre>

To center-align an image:

<pre><code class="language-css">img.center {
margin: 0 auto;
display: block; /*--Since IMG is an inline element--*/
}</code></pre>

### Vertical Alignment

You can vertically align text-based elements using the <code>line-height</code> property, which specifies the amount of vertical space between lines of text. This is ideal for vertically aligning headings and other text-based elements. Simply match the <code>line-height</code> with the height of the element.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e9f3207-8fa5-4420-ac22-5c1aaa9690d5/3-a.jpg" alt="Line-height" />

<pre><code class="language-css">h1 {
font-size: 3em;
height: 100px;
line-height: 100px;
}</code></pre>

To vertically align non-textual elements, use absolute positioning.

The trick with this technique is that you must specify the exact height and width of the centered element.

With the <code>position: absolute</code> property, an element is positioned according to its base position (<strong>0,0</strong>: the top-left corner). In the image below, the red point indicates the 0,0 base of the element, before a negative margin is applied.

By applying negative top and left margins, we can now perfectly align this element both vertically and horizontally.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fac5bc9a-a572-437d-ab7b-0cbc0298f340/upd3-b.gif" alt="Absolute Position" />

Here is the complete CSS for horizontal and vertical alignment:

<pre><code class="language-css">.vertical {
width: 600px; /*--Specify Width--*/
height: 300px; /*--Specify Height--*/
position: absolute; /*--Set positioning to absolute--*/
top: 50%; /*--Set top coordinate to 50%--*/
left: 50%; /*--Set left coordinate to 50%--*/
margin: -150px 0 0 -300px; /*--Set negative top/left margin--*/
}</code></pre>

Related articles:

*   Vertical Centering With CSS
*   [Centering Things](https://www.w3.org/Style/Examples/007/center)
*   [CSS Centering 101](https://simplebits.com/notebook/2004/09/08/centering.html)
*   [CSS Centering: Fun for All!](https://www.maxdesign.com.au/presentation/center/)
*   Two Simple Ways to Vertically Align with CSS

{{% ad-panel-leaderboard %}}

## 4. Ordered vs. Unordered Lists

An ordered list, <code>&lt;ol&gt;</code>, is a list whose items are marked with numbers.

An unordered list, <code>&lt;ul&gt;</code>, is a list whose items are marked with bullets.

By default, both of these list item styles are plain and simple. But with the help of CSS, you can easily customize them.

To keep the code semantic, lists should be used only for content that is itemized in a list-like fashion. But they can be extended to create multiple columns and navigation menus.</p>

### Customizing Unordered Lists

Plain bullets are dull and may not draw enough attention to the content they accompany. You can fix this with a simple yet effective technique: remove the default bullets and apply a background image to each list item.

Here is the CSS for custom bullets:

<pre><code class="language-css">ul.product_checklist {
list-style: none; /*--Takes out the default bullets--*/
margin: 0;
padding: 0;
}
ul.product_checklist li {
padding: 5px 5px 5px 25px; /*--Adds padding around each item--*/
margin: 0;
background: url(icon_checklist.gif) no-repeat left center; /*--Adds a bullet icon as a background image--*/
}</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d893ba4a-216f-4e6f-b6ff-13d5836082f2/4-a.gif" alt="Custom List Items" />

Resources for list items:

*   [Style Your Ordered List](https://www.webdesignerwall.com/tutorials/style-your-ordered-list/)
*   [CSS Design: Taming Lists](https://www.alistapart.com/articles/taminglists/)

### Using Unordered Lists for Navigation

Most CSS-based navigation menus are now built as lists. Here is a breakdown of how to turn an ordinary list into a horizontal navigation menu.

<strong>HTML:</strong> begin with a simple unordered list, with links for each list item.

<pre><code class="language-css">&lt;ul id="topnav"&gt;
&lt;li&gt;&lt;a href="#"&gt;Home&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;Services&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;Portfolio&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;About&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;Contact&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;</code></pre>

<strong>CSS:</strong> we remove the default bullets (as we did when we made custom bullets) by specifying <code>list-style: none</code>. Then, we float each list item to the left so that the navigation menu appears horizontal, flowing from left to right.

<pre><code class="language-css">ul#topnav {
list-style: none;
float: left;
width: 960px;
margin: 0; padding: 0;
background: #f0f0f0;
border: 1px solid #ddd;
}
ul#topnav li {
float: left;
margin: 0; padding: 0;
border-right: 1px solid #ddd;
}
ul#topnav li a {
float: left;
display: block;
padding: 10px;
color: #333;
text-decoration: none;
}
ul#topnav li a:hover {
background: #fff;
}</code></pre>

Additional resources:

*   [CSS-Based Navigation Menus: Modern Solutions](https://www.smashingmagazine.com/2007/03/14/css-based-navigation-menus-modern-solutions/)
*   [30 Exceptional CSS Navigation Techniques](https://sixrevisions.com/css/30-exceptional-css-navigation-techniques/)
*   Using CSS and Unordered List Items to Do Just About Anything
*   [Nifty Navigation Tricks Using CSS](https://www.sitepoint.com/article/navigation-using-css/)
*   [Centering List Items Horizontally](https://css-tricks.com/centering-list-items-horizontally-slightly-trickier-than-you-might-think/)
*   Digg-Like Navigation Bar Using CSS

## 5. Styling Headings

The heading HTML tag is important for SEO. But regular headings can look dull. Why not spice them up with CSS and enjoy the best of both worlds?

Once you have the main styling properties set for your headings, you can now <strong>nest inline elements</strong> to target specific text for extra styling.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/645d4e91-51f9-45cd-8574-62a21c3f3526/5-a.gif" alt="Styling Headings" />

Your HTML would look like this:

<pre><code class="language-css">&lt;h1&gt;&lt;span&gt;CSS&lt;/span&gt; Back to Basics &lt;small&gt;Tips, Tricks, &amp;amp; Practical Uses of CSS&lt;/small&gt;&lt;/h1&gt;</code></pre>

And your CSS would look like this:

<pre><code class="language-css">h1 {
font: normal 5.2em Georgia, "Times New Roman", Times, serif;
margin: 0 0 20px;
padding: 10px 0;
font-weight: normal;
text-align: center;
text-shadow: 1px 1px 1px #ccc; /*--Not supported by IE--*/
}
h1 span {
color: #cc0000;
font-weight: bold;

}
h1 small {
font-size: 0.35em;
text-transform: uppercase;
color: #999;
font-family: Arial, Helvetica, sans-serif;
text-shadow: none;
display: block; /*--Keeps the small tag on its own line--*/
}</code></pre>

Additional typography-related resources:

*   [10 Examples of Beautiful CSS Typography, and How They Did It](https://www.3point7designs.com/blog/2008/06/02/10-examples-of-beautiful-css-typography-and-how-they-did-it/)
*   [12 CSS Tools and Tutorials for Beautiful Web Typography](https://webdesignledger.com/resources/12-css-tools-and-tutorials-for-beautiful-web-typography)
*   [CSS Gradient Text Effect](https://www.webdesignerwall.com/tutorials/css-gradient-text-effect/)
*   [50 Useful Design Tools For Beautiful Web Typography](https://www.smashingmagazine.com/2009/01/27/css-typographic-tools-and-techniques/)
*   [6 Ways to Improve Your Web Typography](https://net.tutsplus.com/tutorials/html-css-techniques/six-ways-to-improve-your-web-typography/)
*   [8 Simple Ways to Improve Typography in Your Designs](https://www.aisleone.net/2009/design/8-ways-to-improve-your-typography/)
*   [How to Size Text in CSS](https://www.alistapart.com/articles/howtosizetextincss/)

## 6. Overflow

The <code>overflow</code> property can be used in various ways and is one of the most useful properties in the CSS arsenal.</p>

### What Is Overflow?

According to W3Schools.com, "the overflow property specifies what happens if content overflows an element's box."

Take a look at the following examples to see how this works.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2325c4c-5107-4c99-9875-d38658c98d13/6-a.jpg" alt="Overflow" />

Visually, <code>overflow: auto</code> looks like an iframe but is much more useful and SEO-friendly. It automatically adds a scroll bar (horizontal, vertical or both) when the content within an element exceeds the element's box or boundary.

The <code>overflow: scroll</code> property works the same but forces a scroll bar to appear regardless of whether or not the content exceeds the element's boundary.

And the <code>overflow: hidden</code> property masks or hides an element's content if it exceeds the element's boundary.

Quick tip: have you ever had a parent element that did not fully wrap around its child element? You can fix this by making the parent container a floated element.

In some cases, though, floating left or right is not a workable solution -- for example, if you want to center-align the container or do not want to specify an exact width. In this case, use <code>overflow: hidden</code> on your parent container to completely wrap any floated child elements within it.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc626e45-8914-4ea0-82e2-64caa8e940c4/6-b.jpg" alt="Overflow" />

Additional resources:

*   [HTML Dog: Overflow](https://htmldog.com/reference/cssproperties/overflow/)
*   W3Schools: Overflow
*   [CSS Globe: Create Resizing Thumbnails](https://cssglobe.com/create-resizing-thumbnails-using-overflow-property)
*   [CSS-Tricks: CSS Overflow Breakdown](https://css-tricks.com/the-css-overflow-property/)

## 7. Position

Positioning (relative, absolute and fixed) is one of the most powerful properties in CSS. It allows you to position an element using exact coordinates, giving you the freedom and creativity to design out of the box.

You have to do three basic things when using positioning:

1.  **Set the coordinates** (i.e. define the positioning of the x and y coordinates).
2.  **Choose the right value for the situation**: relative, absolute, fixed or static.
3.  **Set a value for the z-index property:** to layer elements (optional).

With <code>position: relative</code>, an element is placed in its natural position. For example, if a relatively positioned element sits to the left of an image, setting the top and left coordinates to <code>10px</code> would move the element just 10 pixels from the top and 10 pixels from the left of that exact spot.

Relative positioning is also commonly used <strong>to define the new point of origin (the x and y coordinates)</strong> of absolutely positioned nested elements. By default, the base position of every element is the top-left corner (0,0) of the browser's view port. When you give an element relative positioning, then the base position of any child elements with absolute positioning will be positioned relative to their parent element -- i.e. 0,0 is now the top-left corner of the parent element, not the browser's view port.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1d91282-fc48-4556-b144-93751b4b9239/7-a.gif" alt="Relative Position" />

An element with a value of <code>position: absolute</code> can be placed anywhere using x and y coordinates. By default, its base position (0,0) is the top-left corner of the browser's view port. It ignores all natural flow rules and is not affected by surrounding elements.

The base position of an element with a <code>position: fixed</code> value is also the top-left corner of the browser's view port. The difference with fixed positioning is that <strong>the element will be fixed to its location and remain in view even when the user scrolls up or down.</strong>

The <code>z-index</code> property specifies the stack order of an element. The higher the value, the higher the element will appear.

Think of z-index stacking as layering. Check out the image below for an example:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2e09df5-d47f-44ff-909d-5a6c2fa7d035/7-b.gif" alt="z-index" />

Additional resources:

*   [W3Schools: CSS Positioning](https://www.w3schools.com/Css/css_positioning.asp)
*   [CSS-Tricks: Absolute, Relative, Fixed Positioning](https://css-tricks.com/absolute-relative-fixed-positioining-how-do-they-differ/)
*   Stopping the CSS Positioning Panic
*   [Learn CSS Positioning in Ten Steps](https://www.barelyfitz.com/screencast/html-training/css/positioning/)
*   [In-Depth Coverage of CSS Layers, Z-Index, Relative and Absolute Positioning](https://www.onextrapixel.com/2009/05/29/an-indepth-coverage-on-css-layers-z-index-relative-and-absolute-positioning/)

## Adding Flavor With CSS

Now that you understand the basics, step up your game by adding a bit of flavor to your CSS. Below are some common techniques for enhancing and polishing your layout and images. We'll also challenge you to create your own website from scratch using pure CSS.</p>

## 9. Background Images

Background images come in handy for many visual effects. Whether you add a repeating background image to cover a large area or add stylish icons to your navigation, the property makes your page come to life.

Note, though, that the default print setting excludes the background property. When creating printable pages, be mindful of which elements have background images and include image tags.</p>

### Using Large Backgrounds

With monitor sizes getting bigger and bigger, large background images for websites have become quite popular.

Check out this detailed tutorial by <a href="https://www.ndesign-studio.com/">Nick La</a> of <a href="https://www.webdesignerwall.com/">WebDesigner Wall</a> on how to achieve this effect:

<a href="https://www.webdesignerwall.com/tutorials/how-to-css-large-background/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/959242c3-141e-496d-8e03-82df70ec0ce9/8-a.jpg" alt="Large Backgrounds in Web Design" /></a>

Also be sure to read the article on Webdesigner Depot about the "<a href="https://www.webdesignerdepot.com/2008/11/dos-and-donts-of-large-website-backgrounds/">Do's and Don'ts of Large Website Backgrounds</a>."

### Text Replacement

You may be aware that not all standard browsers yet support custom fonts embedded on a website. But you can replace text with an image in <a href="https://www.mezzoblue.com/tests/revised-image-replacement/">various ways</a>. One rather simple technique is to use the <code><a href="https://www.w3schools.com/Css/pr_text_text-indent.asp">text-indent</a></code> property.

Most commonly seen with headings, this technique replaces structured HTML text with an image.

<pre><code class="language-css">h1 {
background: url(home_h1.gif) no-repeat;
text-indent: -99999px;
}</code></pre>

You may sometimes need to specify a width and height (as well as <code>display: block</code> if the element is inline).

<pre><code class="language-css">.replacethis {
background: url(home_h1.gif) no-repeat;
text-indent: -99999px;
width: 100%;
height: 60px;
display: block; /*--Needed only for inline elements--*/
}</code></pre>

<pre><code class="language-css">ul.product_checklist {
list-style: none; /*--Takes out the default bullets--*/
margin: 0;
padding: 0;
}
ul.product_checklist li {
padding: 5px 5px 5px 25px; /*--Adds padding around each item--*/
margin: 0;
background: url(icon_checklist.gif) no-repeat left center; /*--Adds a bullet icon as a background image--*/
}</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d893ba4a-216f-4e6f-b6ff-13d5836082f2/4-a.gif" alt="Custom List Items" />

Resources for list items:

*   [Style Your Ordered List](https://www.webdesignerwall.com/tutorials/style-your-ordered-list/)
*   [CSS Design: Taming Lists](https://www.alistapart.com/articles/taminglists/)

### Using Unordered Lists for Navigation

Most CSS-based navigation menus are now built as lists. Here is a breakdown of how to turn an ordinary list into a horizontal navigation menu.

<strong>HTML:</strong> begin with a simple unordered list, with links for each list item.

<pre><code class="language-css">&lt;ul id="topnav"&gt;
&lt;li&gt;&lt;a href="#"&gt;Home&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;Services&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;Portfolio&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;About&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;Contact&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;</code></pre>

<strong>CSS:</strong> we remove the default bullets (as we did when we made custom bullets) by specifying <code>list-style: none</code>. Then, we float each list item to the left so that the navigation menu appears horizontal, flowing from left to right.

<pre><code class="language-css">ul#topnav {
list-style: none;
float: left;
width: 960px;
margin: 0; padding: 0;
background: #f0f0f0;
border: 1px solid #ddd;
}
ul#topnav li {
float: left;
margin: 0; padding: 0;
border-right: 1px solid #ddd;
}
ul#topnav li a {
float: left;
display: block;
padding: 10px;
color: #333;
text-decoration: none;
}
ul#topnav li a:hover {
background: #fff;
}</code></pre>

Additional resources:

*   [CSS-Based Navigation Menus: Modern Solutions](https://www.smashingmagazine.com/2007/03/14/css-based-navigation-menus-modern-solutions/)
*   [30 Exceptional CSS Navigation Techniques](https://sixrevisions.com/css/30-exceptional-css-navigation-techniques/)
*   Using CSS and Unordered List Items to Do Just About Anything
*   [Nifty Navigation Tricks Using CSS](https://www.sitepoint.com/article/navigation-using-css/)
*   [Centering List Items Horizontally](https://css-tricks.com/centering-list-items-horizontally-slightly-trickier-than-you-might-think/)
*   Digg-Like Navigation Bar Using CSS

## 5. Styling Headings

The heading HTML tag is important for SEO. But regular headings can look dull. Why not spice them up with CSS and enjoy the best of both worlds?

Once you have the main styling properties set for your headings, you can now <strong>nest inline elements</strong> to target specific text for extra styling.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/645d4e91-51f9-45cd-8574-62a21c3f3526/5-a.gif" alt="Styling Headings" />

Your HTML would look like this:

<pre><code class="language-css">&lt;h1&gt;&lt;span&gt;CSS&lt;/span&gt; Back to Basics &lt;small&gt;Tips, Tricks, &amp;amp; Practical Uses of CSS&lt;/small&gt;&lt;/h1&gt;</code></pre>

And your CSS would look like this:

<pre><code class="language-css">h1 {
font: normal 5.2em Georgia, "Times New Roman", Times, serif;
margin: 0 0 20px;
padding: 10px 0;
font-weight: normal;
text-align: center;
text-shadow: 1px 1px 1px #ccc; /*--Not supported by IE--*/
}
h1 span {
color: #cc0000;
font-weight: bold;

}
h1 small {
font-size: 0.35em;
text-transform: uppercase;
color: #999;
font-family: Arial, Helvetica, sans-serif;
text-shadow: none;
display: block; /*--Keeps the small tag on its own line--*/
}</code></pre>

Additional typography-related resources:

*   [10 Examples of Beautiful CSS Typography, and How They Did It](https://www.3point7designs.com/blog/2008/06/02/10-examples-of-beautiful-css-typography-and-how-they-did-it/)
*   [12 CSS Tools and Tutorials for Beautiful Web Typography](https://webdesignledger.com/resources/12-css-tools-and-tutorials-for-beautiful-web-typography)
*   [CSS Gradient Text Effect](https://www.webdesignerwall.com/tutorials/css-gradient-text-effect/)
*   [50 Useful Design Tools For Beautiful Web Typography](https://www.smashingmagazine.com/2009/01/27/css-typographic-tools-and-techniques/)
*   [6 Ways to Improve Your Web Typography](https://net.tutsplus.com/tutorials/html-css-techniques/six-ways-to-improve-your-web-typography/)
*   [8 Simple Ways to Improve Typography in Your Designs](https://www.aisleone.net/2009/design/8-ways-to-improve-your-typography/)
*   [How to Size Text in CSS](https://www.alistapart.com/articles/howtosizetextincss/)

## 6. Overflow

The <code>overflow</code> property can be used in various ways and is one of the most useful properties in the CSS arsenal.</p>

### What Is Overflow?

According to W3Schools.com, "the overflow property specifies what happens if content overflows an element's box."

Take a look at the following examples to see how this works.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2325c4c-5107-4c99-9875-d38658c98d13/6-a.jpg" alt="Overflow" />

Visually, <code>overflow: auto</code> looks like an iframe but is much more useful and SEO-friendly. It automatically adds a scroll bar (horizontal, vertical or both) when the content within an element exceeds the element's box or boundary.

The <code>overflow: scroll</code> property works the same but forces a scroll bar to appear regardless of whether or not the content exceeds the element's boundary.

And the <code>overflow: hidden</code> property masks or hides an element's content if it exceeds the element's boundary.

Quick tip: have you ever had a parent element that did not fully wrap around its child element? You can fix this by making the parent container a floated element.

In some cases, though, floating left or right is not a workable solution -- for example, if you want to center-align the container or do not want to specify an exact width. In this case, use <code>overflow: hidden</code> on your parent container to completely wrap any floated child elements within it.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc626e45-8914-4ea0-82e2-64caa8e940c4/6-b.jpg" alt="Overflow" />

Additional resources:

*   [HTML Dog: Overflow](https://htmldog.com/reference/cssproperties/overflow/)
*   W3Schools: Overflow
*   [CSS Globe: Create Resizing Thumbnails](https://cssglobe.com/create-resizing-thumbnails-using-overflow-property)
*   [CSS-Tricks: CSS Overflow Breakdown](https://css-tricks.com/the-css-overflow-property/)

## 7. Position

Positioning (relative, absolute and fixed) is one of the most powerful properties in CSS. It allows you to position an element using exact coordinates, giving you the freedom and creativity to design out of the box.

You have to do three basic things when using positioning:

1.  **Set the coordinates** (i.e. define the positioning of the x and y coordinates).
2.  **Choose the right value for the situation**: relative, absolute, fixed or static.
3.  **Set a value for the z-index property:** to layer elements (optional).

With <code>position: relative</code>, an element is placed in its natural position. For example, if a relatively positioned element sits to the left of an image, setting the top and left coordinates to <code>10px</code> would move the element just 10 pixels from the top and 10 pixels from the left of that exact spot.

Relative positioning is also commonly used <strong>to define the new point of origin (the x and y coordinates)</strong> of absolutely positioned nested elements. By default, the base position of every element is the top-left corner (0,0) of the browser's view port. When you give an element relative positioning, then the base position of any child elements with absolute positioning will be positioned relative to their parent element -- i.e. 0,0 is now the top-left corner of the parent element, not the browser's view port.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1d91282-fc48-4556-b144-93751b4b9239/7-a.gif" alt="Relative Position" />

An element with a value of <code>position: absolute</code> can be placed anywhere using x and y coordinates. By default, its base position (0,0) is the top-left corner of the browser's view port. It ignores all natural flow rules and is not affected by surrounding elements.

The base position of an element with a <code>position: fixed</code> value is also the top-left corner of the browser's view port. The difference with fixed positioning is that <strong>the element will be fixed to its location and remain in view even when the user scrolls up or down.</strong>

The <code>z-index</code> property specifies the stack order of an element. The higher the value, the higher the element will appear.

Think of z-index stacking as layering. Check out the image below for an example:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2e09df5-d47f-44ff-909d-5a6c2fa7d035/7-b.gif" alt="z-index" />

Additional resources:

*   [W3Schools: CSS Positioning](https://www.w3schools.com/Css/css_positioning.asp)
*   [CSS-Tricks: Absolute, Relative, Fixed Positioning](https://css-tricks.com/absolute-relative-fixed-positioining-how-do-they-differ/)
*   Stopping the CSS Positioning Panic
*   [Learn CSS Positioning in Ten Steps](https://www.barelyfitz.com/screencast/html-training/css/positioning/)
*   [In-Depth Coverage of CSS Layers, Z-Index, Relative and Absolute Positioning](https://www.onextrapixel.com/2009/05/29/an-indepth-coverage-on-css-layers-z-index-relative-and-absolute-positioning/)

## Adding Flavor With CSS

Now that you understand the basics, step up your game by adding a bit of flavor to your CSS. Below are some common techniques for enhancing and polishing your layout and images. We'll also challenge you to create your own website from scratch using pure CSS.</p>

## 9. Background Images

Background images come in handy for many visual effects. Whether you add a repeating background image to cover a large area or add stylish icons to your navigation, the property makes your page come to life.

Note, though, that the default print setting excludes the background property. When creating printable pages, be mindful of which elements have background images and include image tags.</p>

### Using Large Backgrounds

With monitor sizes getting bigger and bigger, large background images for websites have become quite popular.

Check out this detailed tutorial by <a href="https://www.ndesign-studio.com/">Nick La</a> of <a href="https://www.webdesignerwall.com/">WebDesigner Wall</a> on how to achieve this effect:

<a href="https://www.webdesignerwall.com/tutorials/how-to-css-large-background/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/959242c3-141e-496d-8e03-82df70ec0ce9/8-a.jpg" alt="Large Backgrounds in Web Design" /></a>

Also be sure to read the article on Webdesigner Depot about the "<a href="https://www.webdesignerdepot.com/2008/11/dos-and-donts-of-large-website-backgrounds/">Do's and Don'ts of Large Website Backgrounds</a>."

### Text Replacement

You may be aware that not all standard browsers yet support custom fonts embedded on a website. But you can replace text with an image in <a href="https://www.mezzoblue.com/tests/revised-image-replacement/">various ways</a>. One rather simple technique is to use the <code><a href="https://www.w3schools.com/Css/pr_text_text-indent.asp">text-indent</a></code> property.

Most commonly seen with headings, this technique replaces structured HTML text with an image.

<pre><code class="language-css">h1 {
background: url(home_h1.gif) no-repeat;
text-indent: -99999px;
}</code></pre>

You may sometimes need to specify a width and height (as well as <code>display: block</code> if the element is inline).

<pre><code class="language-css">.replacethis {
background: url(home_h1.gif) no-repeat;
text-indent: -99999px;
width: 100%;
height: 60px;
display: block; /*--Needed only for inline elements--*/
}</code></pre>

Articles on text replacement:

*   [Nine Techniques for CSS Image Replacement](https://css-tricks.com/css-image-replacement/)
*   [Using background-image to Replace Text](https://stopdesign.com/archive/2003/03/07/replace-text.html)
*   [Image Placement vs. Image Replacement](https://www.tjkdesign.com/articles/tip.asp)
*   [Revised Image Replacement](https://www.mezzoblue.com/tests/revised-image-replacement/)

### CSS Sprites

<a href="https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/">CSS Sprites</a> is a technique in which you use background positioning to show only a small area of a larger single background image (the larger image being actually multiple images laid out in a grid and merged into one file).

<a href="https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27a20526-37b4-4860-a66c-a37c2171166c/8-c.gif" alt="CSS Sprites" /></a>

CSS Sprites are commonly used with icons and the hover and active states of images that have replaced links and navigation items.

<a href="https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f288a7ed-904d-43bb-b862-0419e70588d9/8-d.gif" alt="CSS Sprites" /></a>

<strong>Why use CSS Sprites?</strong> CSS Sprites save loading time and cut down on CSS and and HTTP requests. To learn more about CSS Sprites, check out the resources below!

Articles on CSS Sprites:

*   [The Mystery Of CSS Sprites: Techniques, Tools and Tutorials](https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/)
*   [Advanced CSS Menu](https://www.webdesignerwall.com/tutorials/advanced-css-menu/)
*   [CSS Sprite Navigation Tutorial](https://www.ehousestudio.com/blog/2008/06/27/css-sprite-navigation-tutorial/)
*   Creating Easy and Useful CSS Sprites
*   [Building Faster Websites with CSS Sprites](https://www.tutorial9.net/web-tutorials/building-faster-websites-with-css-sprites/)
*   [CSS Sprites: Image Slicing’s Kiss of Death](https://www.alistapart.com/articles/sprites)
*   [CSS Sprites: How Yahoo.com and AOL.com Improve Web Performance](https://www.websiteoptimization.com/speed/tweak/css-sprites/)
*   [What Are CSS Sprites?](https://www.peachpit.com/articles/article.aspx?p=447210)

## 10. Image Enhancement

You can style images with CSS in various ways, and some designers have made a lot of effort to create very stylish image templates.

One simple trick is the double-border technique, which does not require any additional images and is pure CSS.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5effd202-8bc8-420a-beb1-38ab5c60f803/9-b.jpg" alt="Double Border Technique" />

Your HTML would look like this:

<pre><code class="language-css">&lt;img class="double_border" src="sample.jpg" alt="" /&gt;</code></pre>

And your CSS would look like this:

<pre><code class="language-css">img.double_border {
border: 1px solid #bbb;
padding: 5px; /*Inner border size*/
background: #ddd; /*Inner border color*/
}</code></pre>

Nick La of WebDesigner Wall has <a href="https://www.webdesignerwall.com/tutorials/css-decorative-gallery/">a great tutorial</a> on clever tricks to enhance your images. Do check it out!

<a href="https://www.webdesignerwall.com/tutorials/css-decorative-gallery/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe8c3531-d526-444f-b662-dcc1e732c04e/9-a.gif" alt="CSS Sprites" /></a>

## 11. PSD to HTML

Now that you have learned the fundamentals of CSS, it's time to test your skill and build your own website from scratch! Below are some hand-picked tutorials from the best of the Web.

*   [Coding a Clean and Illustrative Web Design from Scratch](https://sixrevisions.com/tutorials/web-development-tutorials/coding-a-clean-illustrative-web-design-from-scratch/)[![PSD to HTML Tutorial](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfec2071-c276-472d-8854-cd4435d71868/10-d.jpg)](https://sixrevisions.com/tutorials/web-development-tutorials/coding-a-clean-illustrative-web-design-from-scratch/)
*   [Converting a Photoshop Mockup: Part Two, Episode One](https://css-tricks.com/video-screencasts/12-converting-a-photoshop-mockup-part-two-episode-one/)[![PSD to HTML Tutorial](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97d462c3-b87d-438e-aed0-e9a7496ca43a/10-g.jpg)](https://css-tricks.com/video-screencasts/12-converting-a-photoshop-mockup-part-two-episode-one/)

## Conclusion

Developing a strong foundation early on is critical to mastering CSS. Given how fast Web technology advances, there is no better time than now to get up to speed on the latest standards and trends.

Hopefully, the techniques we've covered here will give you a head start on becoming the ultimate CSS ninja. Good luck, stay hungry and keep learning!

{{< signature "al, il" >}}
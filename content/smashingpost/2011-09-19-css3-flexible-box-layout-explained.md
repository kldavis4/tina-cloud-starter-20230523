---
title: 'CSS3 Flexible Box Layout: Everything I Wish I Knew When I Started'
slug: css3-flexible-box-layout-explained
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e181ef46-ffef-4173-b223-bb1fe655bf1d/fruitblog.jpg
date: 2011-09-19T09:19:24.000Z
author: richard-shepherd
summary: >-
  Offering a range of new features that help us break free of the float, the flexbox model is another step forward for the layout of modern Web pages and applications. By experimenting with these new techniques now, you can actively contribute to its development.
description: >-
  Offering a range of new features that help us break free of the float, the flexbox model is another step forward for the layout of modern Web pages and applications. By experimenting with these new techniques now, you can actively contribute to its development.
categories:
  - Coding
  - Layouts
  - CSS
  - Flexbox
---

The flexible box layout module &mdash; or “flexbox,” to use its popular nickname &mdash; is an interesting part of the W3C Working Draft. The flexbox specification is still a draft and subject to change, so keep your eyes on the W3C, but it is part of a new arsenal of properties that will revolutionize how we lay out pages. At least it will be when cross-browser support catches up.

{{% feature-panel %}}

## The Display Property

So what *is* flexbox, and why was it created? First, let’s look at how we currently lay out pages and some of the problems with that model.

Until last year, most of us were using tables to lay out our pages. Okay, maybe not last year! But I suspect that many of you reading this have been guilty of relying on tables at some point in your career. At the same time, it actually made a lot of sense. And let’s face it: it worked… to a point. However, we all then faced the reality that tables were semantically dubious and incredibly inflexible. And through the haze of this mark-up hangover, we caught a glimpse of the future: the CSS box model. Hurray!

The CSS box model allowed us to tell the browser how to display a piece of content, and in particular how to display it as a box. We floated left and right, we tried to understand what <code>inline-block</code> meant, and we read countless articles about <code>clearfix</code>, before just copying and pasting the <code>clearfix</code> hack-du-jour into our CSS.

For those of us testing our websites back to IE6, we had to grapple with <code>hasLayout</code> and triggering it with the following or some similar fix:

<pre><code class="language-css">* html #element {
height: 1%;
}</code></pre>

The box model worked, and in most cases it worked well. But as the Web entered its teenage years, it demanded more complex ways of laying out content and &mdash; thanks to a certain Mr. Ethan Marcotte &mdash; of responding to the size of the browser and/or device.

### Percentage + Padding + Border = Trouble

Here’s another problem with the current box model: absolute values for padding, margin and border all affect the width of a box. Take the following:

<pre><code class="language-css">#element {
width: 50%;
border 1px solid #000;
padding: 0 5px;
}</code></pre>

This will *not* give us a box that is 50% of its parent. It will actually render an element that is 50% of the parent’s width *plus* 12 pixels (2-pixel border + 10-pixel padding). You could set the padding as a percentage value (although not for input elements in Firefox!), but adding percentage values of widths to the pixel values of borders can cause mathematical problems.

There are two ways to fix this problem. The first is to use the new CSS3 <code>box-sizing</code> property, and setting it to <code>border-box</code>:

<pre><code class="language-css">#element {
box-sizing: border-box;
width: 50%;
border 1px solid #000;
padding: 0 5px;
}</code></pre>

This new CSS3 panacea effectively tells the browser to render the element at the specified width, *including* the border width and padding.

The second way to fix this problem is to use flexbox.

### Many Problems, Many Solutions

The W3C responded with a suite of answers: the flexible box model, columns, templates, positioned floats and the grid. Adobe <a href="https://labs.adobe.com/technologies/cssregions/">added regions</a> to the mix, but they are <a href="https://dev.w3.org/csswg/css3-regions/">not yet supported</a> by any browser.

The <a href="https://www.w3.org/TR/CSS2/visuren.html#display-prop"><code>display</code> property</a> already has no less than a staggering 16 values: <code>inline</code>, <code>block</code>, <code>list-item</code>, <code>inline-block</code>, <code>table</code>, <code>inline-table</code>, <code>table-row-group</code>, <code>table-header-group</code>, <code>table-footer-group</code>, <code>table-row</code>, <code>table-column-group</code>, <code>table-column</code>, <code>table-cell</code>, <code>table-caption</code>, <code>none</code> and <code>inherit</code>.

And now we can add a 17th: <code>box</code>.

## Living In A Box

Let’s take a look at flexbox, which brings with it a brand new value for the display property (<code>box</code>) and no less than 8 new properties. Here’s how the W3C defines the new module:
<blockquote>“In this new box model, the children of a box are laid out either horizontally or vertically, and unused space can be assigned to a particular child or distributed among the children by assignment of <code>flex</code> to the children that should expand. Nesting of these boxes (horizontal inside vertical, or vertical inside horizontal) can be used to build layouts in two dimensions.”</blockquote>

Sounds exciting! The Working Draft expands on this a little:
<blockquote>“Flexbox… lacks many of the more complex text or document-formatting properties that can be used in block layout, such as “float” and “columns,” but in return it gains more simple and powerful tools for aligning its contents in ways that Web apps and complex Web pages often need.”</blockquote>

Now this is beginning to sound interesting. The flexbox model picks up where the box model leaves off, and the W3C reveals its motivation by noting that “Web apps and complex Web pages” need a better layout model. Here’s a list of the new flexbox properties:

*   `box-orient`,
*   `box-pack`,
*   `box-align`,
*   `box-flex`,
*   `box-flex-group`,
*   `box-ordinal-group`,
*   `box-direction`,
*   `box-lines`.

For the sake of brevity, I will use only the official spec’s properties and values, but do remember to add the vendor prefixes to your work. (See the section on “Vendor Prefixes and Cross-Browser Support” below.)

You might also want to check out <a href="https://prefixr.com/">Prefixr</a> from Jeffrey Way, which can help generate some of the CSS for you. However, I found that it incorrectly generated the <code>display: box</code> property, so check all of its code.

### Everything Will Change

If you take the time to read or even browse the latest Working Draft (from 22 March 2011), you’ll notice a lot of red ink, and with good reason. This spec has issues and is still changing; we are in unchartered waters.

It’s worth noting that the syntax used in this article, and by all *current* browsers, is already out of date. The Working Draft has undergone changes to much of the syntax used in the flexbox model. For example:

<pre><code class="language-css">display: box;</code></pre>

This will become:

<pre><code class="language-css">display: flexbox;</code></pre>

Other changes include some properties being split (<code>box-flex</code> will become <code>flex-grow</code> and <code>flex-shrink</code>), while others will be combined (<code>box-orient</code> and <code>box-direction</code> will become <code>flex-direction</code>). Indeed, anything that starts <code>box-</code> will be changed to <code>flex-</code>. So, keep your eyes on <a href="https://www.w3.org/TR/css3-flexbox/">the spec</a> and on browser implementations. (<a href="https://caniuse.com/#search=flex">CanIUse</a> helps, but it doesn’t cover all of the properties.)

### PaRappa The Wrapper

Using flexbox often requires an extra div or two, because the parent of any flexbox element needs to have <code>display</code> set to <code>box</code>. Before, you could get away with the following:

<pre><code class="language-markup tmp-html">&lt;div style="float: left; width: 250px;"&gt; Content here &lt;/div&gt;
&lt;div style="float: right; width: 250px;"&gt; Content here &lt;/div&gt;</code></pre>

Now with flexbox, you’ll need:

<pre><code class="language-markup tmp-html">&lt;div style="display: box"&gt;
  &lt;div style="width: 250px"&gt; Content here &lt;/div&gt;
  &lt;div style="width: 250px"&gt; Content here &lt;/div&gt;
&lt;/div&gt;</code></pre>

Many of you have already turned away, insulted by this extra mark-up that is purely for presentation. That’s understandable. But here’s the thing: once you master the CSS, this extra containing div becomes a small price to pay. Indeed, you’ll often already have a containing element (not necessarily a div) to add <code>display: box</code> to, so there won’t be a trade-off at all.

On a broader note, sometimes you *need* presentational mark-up. It’s just the way it goes. I’ve found that, particularly when working on cross-browser support for a page, I have to add presentational mark-up for browsers such as IE6. I’m not saying to contract “div-itis,” but because we all use HTML5 elements in our mark-up, we find that sections often need div containers. That’s fine, as long as it’s kept to a minimum.

With this in mind, let’s get busy with some code. I’ve put together a demo page, and you can download all of the <a href="https://github.com/richardshepherd/CSS3-Flexbox-Tutorial">source files</a>.

<img title="Our fictional Fruit Blog" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e181ef46-ffef-4173-b223-bb1fe655bf1d/fruitblog.jpg" alt="screenshot" width="550" height="400" />

Over the next few paragraphs, we’ll use the new flexbox model to create a basic home page for a blog. You might want to launch a latest-generation browser, though, because we’re now coding at the cutting edge. And it’s an exciting place to be.

### box-flex

Let’s start with the basics: <code>box-flex</code>. Without <code>box-flex</code>, very little can be achieved. Simply put, it tells the browser how to resize an element when the element is too big or small for its parent.

Consider the following classic problem. You have a container with three children that you want to position side by side. In other words, you float them left. If the total width of these boxes is wider than that of the parent &mdash; perhaps because of padding, margin or a border &mdash; then you need to either specify exact widths in pixels (which is not flexible) or work in percentages (and the sometimes mind-bending calculations that come with them!).

Here’s the problem we have on our Fruit Blog, with three 320-pixel-wide asides (plus padding and margin) inside a 920-pixel-wide container:

<img title="Without flexbox" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f07eba3-6409-46f7-ad5a-2c3b753169f6/asidespreflexbox.png" alt="screenshot" width="550" height="138" />

As you can see, the content is wider than the parent. However, if we set set the parent to <code>display: box</code> and each of these asides to <code>box-flex: 1</code>, then the browser takes care of the math and renders the following:

<img title="With flexbox" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a39316c2-3d72-4960-afbb-4942adadf0ec/asidespostflexbox.png" alt="screenshot" width="550" height="166" />

So, what exactly has happened here?

The <code>box-flex</code> property refers to how the browser will treat the width of the box &mdash; or, more specifically, the **unused space** (even if that space is negative &mdash; i.e. even if the rendered boxes are too big for the container) &mdash; after the box has rendered. The value (<code>1</code> in our example) is the *ratio*. So, with each aside set to a ratio of <code>1</code>, each box is scaled in exactly the same way.

In the first instance, each aside was 320 pixels + 20 pixels of padding on the left and right. This gave us a total width of 360 pixels; and for three asides, the width was 1080 pixels. This is 160 pixels *wider* than the parent container.

Telling the browser that each box is flexible (with <code>box-flex</code>) will make it shrink the *width* of each box &mdash; i.e. it will not change the padding. This calculation is a fairly easy one:
<blockquote>160 pixels ÷ 3 asides = 53.333 pixels to be taken off each aside.

320 pixels - 53.333 = 266.667 pixels</blockquote>

And, if we look in Chrome Developer tools, we will see this is exactly how wide the box now is (rounded up to the nearest decimal):

<img title="267px wide" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f76997f6-7c8a-4b5f-af76-e24c73148f9c/267px.png" alt="screenshot" width="174" height="69" />

The same would be true if each aside had a width of 100 pixels. The browser would expand each element until it filled the **unused space**, which again would result in each aside having a width of 266.667 pixels.

This is invaluable for flexible layouts, Because it means that your padding, margin and border values will always be honored; the browser will simply change the width of the elements until they fit the parent. If the parent changes in size, so will the flexible boxes within it.

Of course, you can set <code>box-flex</code> to a different number on each element, thus creating different ratios. Let’s say you have three elements side by side, each 100 pixels wide, with 20 pixels padding, inside a 920-pixel container. It looks something like this:

<img title="100px wide" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/955aa629-b22f-4b2e-b2fb-8c005e5ba040/asides100px.png" alt="screenshot" width="550" height="143" />

Now, let’s set the <code>box-flex</code> ratios:

<pre><code class="language-css">.box1 { box-flex: 2; }
.box2 { box-flex: 1; }
.box3 { box-flex: 1; }</code></pre>

Here’s what it looks like:

<img title="Flexbox with 2:1:1 ratio" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b9d5a32-fa36-42b7-abd1-6d02663fc503/flexbox2to1.png" alt="screenshot" width="550" height="161" />

What just happened?!

Well, each aside started off as 140-pixels wide (100 pixels + 40 pixels padding), or 420 pixels in total. This means that 500 pixels were left to fill once we’d made them flexible boxes.

However, rather than split the 500 pixels three ways, we told the browser to assign the first aside with a <code>box-flex</code> of <code>2</code>. This would grow it by 2 pixels for every 1 pixel that the other two boxes grow, until the parent is full.

Perhaps the best way to think of this is that our ratio is 2:1:1. So, the first element will take up 2/4 of the unused space, while the other two elements will take up 1/4 of the unused space (2/4 + 1/4 + 1/4 = 1).

2/4 of 500 pixels is 250, and 1/4 is 125 pixels. The final widths, therefore, end up as:
<blockquote><code>.box1</code> = <strong>350px (100px + <em>250px</em>)</strong> + 40px padding
<code>.box2</code> = <strong>225px<strong> (100px + <em>125px</em>)</strong></strong> + 40px padding
<code>.box3</code> = <strong>225px<strong> (100px + <em>125px</em>)</strong></strong> + 40px padding</blockquote>

Add all of these values up and you reach the magic number of 920 pixels, the width of our parent.

An important distinction to make is that the ratio refers to how the additional pixels (or unused space) are calculated, *not* the widths of the boxes themselves. This is why the widths are 350:225:225 pixels, and not 460:230:230 pixels.

The wonderful thing about the flexbox model is that you don’t have to remember &mdash; or even particularly understand &mdash; much of the math. While the Working Draft goes into detail on the calculation and distribution of free space, you can work safe in the knowledge that the browser will take care of this for you.

### Animating Flexible Boxes

A simple and elegant effect is already at your fingertips. By making the <code>li</code> elements in a navigation bar flexible, and specifying their width on <code>:hover</code>, you can create a nice effect whereby the highlighted <code>li</code> element expands and all the other elements shrink. Here’s the CSS for that:

<pre><code class="language-css">nav ul {
display: box;
width: 880px;
}

nav ul li {
padding: 2px 5px;
box-flex: 1;
-webkit-transition: width 0.5s ease-out;
min-width: 100px;
}

nav ul li:hover {
width: 200px;
}</code></pre>

<img title="Expanding Menus" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ceb34af0-28d0-4041-9c91-34ca2f36e644/expandingmenus1.jpg" alt="screenshot" width="550" height="121" />

You’ll spot a <code>min-width</code> on the <code>li</code> element, which is used to fix a display bug in Chrome.

### Equal-Height Columns: The Happy Accident!

As we’ll see, all flexbox elements inherit a default value of <code>box-align: stretch</code>. This means they will all stretch to fill their container.

For example, two flexbox columns in a parent with <code>display: box</code> will always be the same height. This has been the subject of CSS and JavaScript hacks for years now.

There are a number of practical implementations of this fortunate outcome, not the least of which is that sidebars can be made the same height as the main content. Now, a <code>border-left</code> on a right-hand sidebar will stretch the full length of the content. Happy days!

### box-orient and box-direction

The <code>box-orient</code> property defines how boxes align within their parent. The default state is <code>horizontal</code> or, more specifically, <code>inline-axis</code>, which is horizontal and left-to-right in most Western cultures. Likewise, <code>vertical</code> is the same as <code>block-axis</code>. This will make sense if you think about how the browser lays out inline and block elements.

You can change the <code>box-orient</code> value to <code>vertical</code> to make boxes stack on top of each other. This is what we’ll do with the featured articles on our fruit blog.

Here is what our articles look like with <code>box-orient</code> set to its default setting:

<img title="box-orient: horizontal" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03197261-c7b2-420c-ae0e-deeb469623c7/articleshorizontal.png" alt="screenshot" width="550" height="109" />

Ouch! As you can see, the articles are stacking next to each other and so run off the side of the page. It also means that they sit on top of the sidebar. But by quickly setting the parent div to <code>box-orient: vertical</code>, the result is instant:

<img title="box-orient: vertical" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a1de1da-2273-4429-b620-c4c79e68f718/articles213.png" alt="screenshot" width="550" height="268" />

A related property is <code>box-direction</code>, which specifies the direction in which the boxes are displayed. The default value is <code>normal</code>, which means the boxes will display as they appear in the code. But if you change this value to <code>reverse</code>, it will reverse the order, and so the last element in the code will appear first, and the first last.

While <code>box-orient</code> and <code>box-direction</code> are essential parts of the model, they will not likely appear in the final specification, because they are being merged into the <a href="https://www.w3.org/TR/css3-flexbox/#flex-direction"><code>flex-direction</code> property</a>, which will take the following values: <code>lr</code>, <code>rl</code>, <code>tb</code>, <code>bt</code>, <code>inline</code>, <code>inline-reverse</code>, <code>block</code> and <code>block-reverse</code>. Most of these are self-explanatory, but as yet they don’t work in any browser.

### box-ordinal-group

Control over the order in which boxes are displayed does not stop at <code>normal</code> and <code>reverse</code>. You can specify the exact order in which each box is placed.

The value of <code>box-ordinal-group</code> is set as a positive integer. The lower the number (<code>1</code> being the lowest), the higher the layout priority. So, an element with <code>box-ordinal-group: 1</code> will be rendered before one with <code>box-ordinal-group: 2</code>. If elements share the same <code>box-ordinal-group</code>, then they will be rendered in the order that they appear in the HTML.

Let’s apply this to a classic blog scenario: the sticky post (i.e. content that you want to keep at the top of the page). Now we can tag sticky posts with a <code>box-ordinal-group</code> value of <code>1</code> and all other posts with a <code>box-ordinal-group</code> of <code>2</code> or lower. It might look something like this:

<pre><code class="language-css">article {
box-ordinal-group: 2;
}

article.sticky {
box-ordinal-group: 1;
}</code></pre>

So, any article with <code>class="sticky"</code> is moved to the top of the list, without the need for any front-end or back-end jiggering. That’s pretty impressive and incredibly useful.

We’ve used this code in our example to stick a recent blog post to the top of the home page:

<img title="box-ordinal-group changes the order" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5aab3275-e868-4e96-a731-fce7a4406aed/articles213closeup.png" alt="screenshot" width="550" height="375" />

### box-pack and box-align

The <code>box-pack</code> and <code>box-align</code> properties help us position boxes on the page.

The default value for <code>box-align</code> is <code>stretch</code>, and this is what we’ve been using implicitly so far. The <code>stretch</code> value stretches the box to fit the container (together with any other siblings that are flexible boxes), and this is the behavior we’ve seen so far. But we can also set <code>box-align</code> to <code>center</code> and, depending on the <code>box-orient</code> value, the element will be centered either vertically or horizontally.

For example, if a parent inherits the default <code>box-align</code> value of <code>horizontal</code> (<code>inline-axis</code>), then any element with <code>box-align</code> set to <code>center</code> will be centered vertically.

We can use this in our blog example to vertically center the search box in the header. Here’s the mark-up:

<pre><code class="language-markup tmp-html">&lt;header&gt;
  &lt;form id="search"&gt;
    &lt;label for="searchterm"&gt;Search&lt;/label&gt;
    &lt;input type="search" placeholder="What’s your favourite fruit…" name="searchterm" /&gt;
    &lt;button type="submit"&gt;Search!&lt;/button&gt;
  &lt;/form&gt;
&lt;/header&gt;</code></pre>

And to vertically center the search box, we need just one line of CSS:

<pre><code class="language-css">header {
display: box; box-align: center;
}

header #search {
display: box; box-flex: 1;
}</code></pre>

The height of <code>#search</code> has not been set and so depends on the element’s content. But no matter what the height of <code>#search</code>, it will always be vertically centered within the header. No more CSS hacks for you!

<img title="Centered Search" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/092f95c4-3b70-4b65-9a0d-d7022cfe0536/fifth-sixth-link.jpg" alt="screenshot" width="400" height="192" />

The other three properties of <code>box-align</code> are <code>start</code>, <code>end</code> and <code>baseline</code>.

When <code>box-orient</code> is set to <code>horizontal</code> (<code>inline-axis</code>), an element with <code>box-align</code> set to <code>start</code> will appear on the left, and one with <code>box-align</code> set to <code>end</code> will appear on the right. Likewise, when <code>box-orient</code> is set to <code>vertical</code> (<code>block-axis</code>), an element with <code>box-align</code> set to <code>start</code> will appear at the top, and one with <code>box-align</code> set to <code>end</code> will move to the bottom. However, <code>box-direction: reverse</code> will flip all of these rules on their head, so be warned!

Finally, we have <code>baseline</code>, which is best explained by the specification:
<blockquote>Align all flexbox items so that their baselines line up, then distribute free space above and below the content. This only has an effect on flexbox items with a horizontal baseline in a horizontal flexbox, or flexbox items with a vertical baseline in a vertical flexbox. Otherwise, alignment for that flexbox item proceeds as if <code>flex-align: auto</code> had been specified.</blockquote>

Another property helps us with alignment: <code>box-pack</code>. This enables us to align elements on the axis that is perpendicular to the axis they are laid out on. So, as in the search-bar example, we have vertically aligned objects whose parent have <code>box-orient</code> set to <code>horizontal</code>.

But what if we want to horizontally center a box that is already horizontally positioned? For this tricky task, we need <code>box-pack</code>.

If you look at the navigation on our fruit blog, you’ll see that it’s only 880 pixels wide, and so it naturally starts at the left of the container.

<img title="The nav bar on the left" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db71f4c4-63da-4fa0-9d4a-42fef5d1a53b/left-of-the-container.jpg" alt="screenshot" width="552" height="75" />

We can reposition this <code>ul</code> by applying <code>box-pack</code> to its parent. If we apply <code>box-pack: center</code> to the navigation element, then the navigation moves nicely to the center of the container.

<img title="Nav bar centered" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ca3ca77-1233-4b1e-ab38-30b3bbcc1e0b/centre-of-the-rotation.jpg" alt="screenshot" width="552" height="71" />

This behaves much like <code>margin: 0 auto</code>. But with the margin trick, you must specify an explicit width for the element. Also, we can do more than just center the navigation with <code>box-pack</code>. There are three other values: <code>start</code>, <code>end</code> and <code>justify</code>. The <code>start</code> and <code>end</code> values do what they do for <code>box-align</code>. But <code>justify</code> is slightly different.

The <code>justify</code> value acts the same as <code>start</code> if there is only one element. But if there is more than one element, then it does the following:

*   It adds no additional space in front of the first element,
*   It adds no additional space after the last element,
*   It divides the remaining space between each element evenly.

{{% ad-panel-leaderboard %}}

### box-flex-group and box-lines

The final two properties have limited and/or no support in browsers, but they are worth mentioning for the sake of thoroughness.

Perhaps the least helpful is <code>box-flex-group</code>, which allows you to specify the priority in which boxes are resized. The lower the value (as a positive integer), the higher the priority. But I have yet to see an implementation of this that is either useful or functional. If you know different, please say so in the comments.

On the other hand, <code>box-lines</code> is a bit more practical, if still a little experimental. By default, <code>box-lines</code> is set to <code>single</code>, which means that all of your boxes will be forced onto one row of the layout (or onto one column, depending on the <code>box-orient</code> value). But if you change it to <code>box-lines: multiple</code> whenever a box is wider or taller than its parent, then any subsequent boxes will be moved to a new row or column.

## Vendor Prefixes And Cross-Browser Support

It will come as no surprise to you that Internet Explorer does not (yet) support the flexbox model. Here’s how <a href="https://caniuse.com/#search=flexbox">CanIUse</a> sees the current browser landscape for flexbox:

<img title="CanIUse.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc21331d-5d8c-4678-836e-40a18b12d05b/caniuser.png" alt="screenshot" width="550" height="317" />

The good news is that Internet Explorer 10 is coming to the party. Download the <a href="https://ie.microsoft.com/testdrive/Info/Downloads/Default.html">platform preview</a>, and then check out <a href="https://ie.microsoft.com/testdrive/HTML5/Flexin/Default.html">some interesting examples</a>.

Also, we need to add a bunch of vendor prefixes to guarantee the widest possible support among other “modern” browsers. In a perfect world, we could rely on the following:

<pre><code class="language-css">#parent {
display: box;
}

#child {
flex-box: 1;
}</code></pre>

But in the real world, we need to be more explicit:

<pre><code class="language-css">#parent {
display: -webkit-box;
display: -moz-box;
display: -o-box;
display: box;
}

#child {
-webkit-flex-box: 1;
-moz-flex-box: 1;
-o-flex-box: 1;
flex-box: 1;
}</code></pre>


### Helper Classes

A shortcut to all of these vendor prefixes &mdash; and any page that relies on the flexbox model will have many of them &mdash; is to use helper classes. I’ve included them in the source code that accompanies this article. Here’s an example:

<pre><code class="language-css">.box {
display: -webkit-box;
display: -moz-box;
display: -o-box;
display: box;
}

.flex1 {
-webkit-flex-box: 1;
-moz-flex-box: 1;
-o-flex-box: 1;
flex-box: 1;
}

.flex2 {
-webkit-flex-box: 2;
-moz-flex-box: 2;
-o-flex-box: 2;
flex-box: 2;
}</code></pre>

This allows us to use this simple HTML:

<pre><code class="language-markup tmp-html">&lt;div class='box'&gt;
  &lt;div class='flex2' id="main"&gt;
   &lt;!-- Content here --&gt;
 &lt;/div&gt;
  &lt;div class="flex1" id="side”&gt;
    &lt;!-- Content here --&gt;
  &lt;/div&gt;
&lt;/div&gt;</code></pre>

Using non-semantic helper classes is considered bad practice by many; but with so many vendor prefixes, the shortcut can probably be forgiven. You might also consider using a “mixin” with <a href="https://sass-lang.com/">Sass</a> or <a href="https://lesscss.org/">Less</a>, which will do the same job. This is something that Twitter sanctions in its *preboot.less* file.

### Flexie.js

For those of you who want to start experimenting with flexbox now but are worried about IE support, a JavaScript polyfill is available to help you out.

<a href="https://flexiejs.com/">Flexie.js</a>, by <a href="https://doctyper.com/">Richard Herrera</a>, is a plug-and-play file that you simply need to include in your HTML (download it on <a href="https://github.com/doctyper/flexie">GitHub</a>). It will then search through your CSS files and make the necessary adjustments for IE &mdash; no small feat given that it is remapping much of the layout mark-up on the page.

<img title="Flexie.js" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f0f7f22-9bfd-4344-8bc5-032a864408b6/flexie.png" alt="screenshot" width="550" height="497" />

### A Word On Firefox

The flexbox model was, at least originally, based on a syntax that Mozilla used in its products. That syntax, called <a href="https://developer.mozilla.org/En/XUL">XUL</a>, is a mark-up language designed for user interfaces.

The irony here is that Firefox is still catching up, and its rendering of some flexbox properties can be buggy. Below are some issues to watch out for, which future releases of Firefox will fix. Credit here must go to the uber-smart Peter Gasston and Oli Studholme, giants on whose shoulders I stand.

*   Flexbox ignores `overflow: hidden` and expands the flexbox child when the content is larger than the child’s width.
*   The setting `display: box` is treated as `display: inline-box` if there is no width.
*   The outline on flexbox children is padded as if by a transparent border of the same width.
*   The setting `box-align: justify` does not work in Firefox.
*   If you set `box-flex` to `0`, Firefox forces the element to act like it’s using the quirks-mode box model.

## Summary

The flexbox model is another exciting development in the CSS3 specification, but the technology is still very much cutting-edge. With buggy support in Firefox and no support in Internet Explorer until version 10 moves beyond the platform preview, it is perhaps of limited use in the mainstream.

Nevertheless, the spec is still a working document. So, by experimenting with these new techniques now, you can actively contribute to its development.

It’s hard to recommend the flexbox model for production websites, but envelopes need pushing, and it might well be the perfect way to lay out a new experimental website or idea that you’ve been working on.

Offering a range of new features that help us break free of the float, the flexbox model is another step forward for the layout of modern Web pages and applications. It will be interesting to see how the specification develops and what other delights for laying out pages await the Web design community in the near future.

*Special thanks to <a href="https://www.timdavey.com">Tim Davey</a> for the artwork.*

{{% ad-panel-leaderboard %}}

### Further Reading

From floats to flexbox, here’s everything else you need to know:

*   [CSS Float Theory: Things You Should Know](/2007/05/01/css-float-theory-things-you-should-know/),” 
*   [Flexbox Is As Easy As Pie &ndash; Designing CSS Layouts](https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/)
*   [CSS Grid, Flexbox And Box Alignment: System For Web Layout](https://www.smashingmagazine.com/2016/11/css-grids-flexbox-and-box-alignment-our-new-system-for-web-layout/)
*   [Laying Out A Flexible Future For Web Design With Flexbox](https://www.smashingmagazine.com/2015/08/flexible-future-for-web-design-with-flexbox/)
*   [The Flexbox Reading List: Techniques And Tools](https://www.smashingmagazine.com/2016/02/the-flexbox-reading-list/)

{{< signature "al, mrn" >}}

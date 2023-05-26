---
title: Equal Height Column Layouts With Borders And Negative Margins In CSS
slug: equal-height-columns-using-borders-and-negative-margins-with-css
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af049792-fd67-4ed9-8129-85633f479eac/screenshot-31.png'
date: 2010-11-08T15:04:45.000Z
author: thierry-koblentz
summary: >-
  “What? Another ‘Equal Height Column’ article? Enough already!” If this is what you think, then think again because this solution is <em>different</em>. It does not rely on any of the usual tricks. It does not use <a title="Faux columns" href="https://www.alistapart.com/articles/fauxcolumns/">images</a>, nor <a title="Ultimate multi-column liquid layouts" href="https://matthewjamestaylor.com/blog/ultimate-multi-column-liquid-layouts-em-and-pixel-widths">extra markup</a>, nor <a title="Doug Neiner Method" href="https://css-tricks.com/fluid-width-equal-height-columns/">CSS3</a>, nor <a title="Nicolas Gallagher Method" href="https://css-tricks.com/fluid-width-equal-height-columns/">pseudo-classes</a>, nor <a title="Balance your CSS Columns with JavaScript" href="https://www.paulbellows.com/getsmart/balance_columns/">Javascript</a>, nor <a title="Absolute Columns" href="https://24ways.org/2008/absolute-columns">absolute positioning</a>. All it uses is <code>border</code> and <code>negative margin</code>.<br /><br />Please note that this article will also demonstrate different construct techniques and will brush up on a few concepts.
description: >-
  Please note that this article also demonstrates different construct techniques and brushes up on a few concepts.
categories:
  - CSS
  - Browsers
  - Techniques
---

## 1\. Centering Columns Without A Wrapper `div`

This layout will be built without a wrapper <code>div</code>:

<a title="Live Demo" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3108a036-4f20-48fb-9415-95160be24660/step-4.html"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec2715b7-11a8-438e-bf3c-4944ee1c4fa9/screenshot-1.png" alt="Two column layout" width="540" height="290" /></a>

### The basics

We use the background of <code>body</code> and the border of one of the columns to create background colors that vertically fill the "row".

### The markup

<pre><code class="language-markup tmp-xml">&lt;div id="header"&gt;
	&lt;h2&gt;&lt;a href="#"&gt;Header&lt;/a&gt;&lt;/h2&gt;
	&lt;p&gt;Lorem ipsum...&lt;/p&gt;
&lt;/div&gt;

&lt;div id="sidebar"&gt;
	&lt;h2&gt;&lt;a href="#"&gt;Sidebar&lt;/a&gt;&lt;/h2&gt;
	&lt;p&gt;Lorem ipsum...&lt;/p&gt;
&lt;/div&gt;

&lt;div id="main"&gt;
	&lt;h2&gt;&lt;a href="#"&gt;Main&lt;/a&gt;&lt;/h2&gt;
	&lt;p&gt;Lorem ipsum...&lt;/p&gt;
&lt;/div&gt;

&lt;div id="footer"&gt;
	&lt;h2&gt;&lt;a href="#"&gt;Footer&lt;/a&gt;&lt;/h2&gt;
	&lt;p&gt;Lorem ipsum...&lt;/p&gt;
&lt;/div&gt;</code></pre>

<strong>Tip</strong>: always include links within your dummy text to spot stacking context issues.

{{% feature-panel %}}

About using `body` as a wrapper:

*   always style `html` with a background to prevent the background of body from extending beyond its boundaries and be painted across the viewport.
*   never style `html` with `height: 100%` or the background of body will be painted no taller than the viewport.

### The CSS

<pre><code class="language-css">html {
  background: #9c9965;
}

body {
  width: 80%;
  margin: 20px auto;
  background: #ffe3a6;
}

#header {
  background: #9c9965;
}

#sidebar {
  float: left;
  width: 200px;
  background: #d4c37b;
}

#main {
  border-left: 200px solid #d4c37b;
}

#footer {
  clear: left;
  background: #9c9965;
}</code></pre>

What do these rules do exactly?

*   We style `html` with a background to prevent the browser from painting the background color of `body` _outside_ our layout.
*   We style `body` with auto margin to center the layout; the width is set using percentage. The background declaration is for `#main`.
*   We style the background of `#header` to mask the background color of body (the same goes for `#footer`).
*   The background color of `#sidebar` matches the border color of `#main`. This is the trick we use to make our columns appear as being of equal height.
*   The footer clears any previous float so it stays below the columns, at the bottom of the layout.

If you take a look at this <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3de528fa-dc56-47be-bbc6-d299fa560fc0/step-1.html">first step</a>, you’ll notice that the heading in <code>#sidebar</code> is not vertically aligned with the heading in <code>#main</code> and that we have some gap at the top and bottom of the <code>#sidebar</code>. This is because out of these two containers, only one is a <a href="https://www.tjkdesign.com/articles/block-formatting-contexts_and_hasLayout.asp">block formatting context</a>. So margins do not collapse in <code>#sidebar</code> while they do in <code>#main</code>. This also means that <code>#main</code> will not contain floats and that applying <code>clear:left</code> to any nested element in there will clear <code>#sidebar</code> as well.

So to prevent any float and margin collapsing issues we make all the main boxes block formatting contexts.

<pre><code class="language-css">#header,
#footer {
  overflow: hidden;
  zoom: 1;
}

#main {
  float: left;
}

#sidebar {
  margin-right: -200px;
}</code></pre>

<strong>Note</strong>: if things look a bit different in IE 6 and 7 it is because in these browsers <em>default</em> margins do collapse inside block-formatting contexts. The following should also be considered:

*   `overflow` and `zoom` on `#header` and `#footer` make these elements new block formatting contexts.
*   For `#main` we use `float` rather than `overflow` to prevent potential issues if we had to offset some nested content.
*   The negative margin keeps `#main` into place because now that it is a float, its border box comes _next_ to the margin box of `#sidebar` (the negative vlaue must match the dimension of the said box).

If you look at <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c0c2a27-d68d-4fc8-a7d8-fe6e3030e8d0/step-2.html">the second step</a>, you’ll see that the border of <code>#main</code> hides <code>#sidebar</code>. This is because of the stacking context. In the flow (tree order), <code>#main</code> comes after <code>#sidebar</code> so the former overlaps the latter.

Positioning #sidebar brings it up in the stack.

<pre><code class="language-css">#sidebar {
  position: relative;
}</code></pre>

<strong>Note:</strong> if you make <code>#main</code> a new containing block you’ll revert to the original stack order. In this case, you’ll need to use <code>z-index</code> to keep <code>#sidebar</code> on top of <code>#main</code>.

If you look at <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1f81241-76a2-4109-bf84-93ac288f9c55/step-3.html">step three</a>, you’ll see that we are almost there. The last things to do are mostly cosmetic. I’ve inserted a <a href="https://thinkvitamin.com/design/setting-rather-than-resetting-default-styling/">base styles sheet</a>:

<div class="break-out">

 <pre><code class="language-markup tmp-xml">&lt;link rel="stylesheet" type="text/css" href="https://tjkdesign.com/ez-css/css/base.css"&gt;
</code></pre>
</div>

and then added these rules:

<pre><code class="language-css">html {
  height: auto;
}

body {
  border: 1px solid #efefef;
}

#header,
#main,
#sidebar,
#footer {
  padding-bottom: 2em;
}</code></pre>

<strong>Why do we need these rules?</strong>

*   We can reset the height on `html` so the background of `#main` is not cut-off at the fold (this styling is inherited from the base styles sheet).
*   We can draw a border all around the layout.
*   Because the base styles sheet only sets top margins, we can create gaps at the bottom of the main boxes via padding.

<strong>Note:</strong> The rule for <code>html</code> is shown here, but it makes more sense to <em>remove</em> that rule from the base styles sheet rather than overwriting the declaration here.

This is the <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3108a036-4f20-48fb-9415-95160be24660/step-4.html">last step</a> for this first layout. It relies on these simple rules:

<div class="break-out">

 <pre><code class="language-css">html {
  height: auto;
  background: #45473f;
}

body {
  width: 80%;
  margin: 20px auto;
  background: #ffe3a6;
  border: 1px solid #efefef;
}

#sidebar {
  float: left;
  position: relative;
  width: 200px;
  margin-right: -200px;
  background: #d4c37b; /* color must match #main’s left border */
}

#main {
  float: left;
  border-left: 200px solid #d4c37b; /* color must match #sidebar’s background */
}

#header,
#footer {
  clear: left;
  overflow: hidden;
  zoom: 1;
  background: #9c9965;
}

#header,
#main,
#sidebar,
#footer {
  padding-bottom:2em;
}</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## 2\. Creating a 2-col-layout with two borders in between the columns

We’ll build this one with a single wrapper for our two columns, and we want to paint a vertical border between the two columns.

<a title="Live Demo" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bc61387-64da-4d01-9a9a-a5ec8f387165/step-3.html"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62deb08e-3676-4c7c-b75e-5e79ed8e44b3/screenshot-2.png" alt="Two column layout with two vertical borders" width="540" height="290" /></a>

### The basics

The wrapper <code>div</code> allows us to be a bit more creative here. The background of the wrapper is used to paint the background of one column, while its left border is used to paint the background color of the other column. The vertical border will be done by overlapping the right border of the left column with the left border of the right column.

<strong>Note:</strong> if you have use a fixed width layout (vs. fluid like here), then the wrapper can be used to create the two background colors as well as the vertical border at the same time. This is done by using the left border for the left column, the right border for the right column and the background for the vertical border. Yes, this means the content box is one pixel wide and that negative margins are used to pull the columns into place.

### Markup

<pre><code class="language-markup tmp-xml">&lt;div id="header"&gt;
	&lt;h2&gt;&lt;a href="#"&gt;Header&lt;/a&gt;&lt;/h2&gt;
	&lt;p&gt;Lorem ipsum...&lt;/p&gt;
&lt;/div&gt;

&lt;div id="wrapper"&gt;
  &lt;div id="sidebar"&gt;
  	&lt;h2&gt;&lt;a href="#"&gt;Sidebar&lt;/a&gt;&lt;/h2&gt;
  	&lt;p&gt;Lorem ipsum...&lt;/p&gt;
  &lt;/div&gt;
  &lt;div id="main"&gt;
  	&lt;h2&gt;&lt;a href="#"&gt;Main&lt;/a&gt;&lt;/h2&gt;
  	&lt;p&gt;Lorem ipsum...&lt;/p&gt;
  &lt;/div&gt;
&lt;/div&gt;

&lt;div id="footer"&gt;
	&lt;h2&gt;&lt;a href="#"&gt;Footer&lt;/a&gt;&lt;/h2&gt;
	&lt;p&gt;Lorem ipsum...&lt;/p&gt;
&lt;/div&gt;</code></pre>

### CSS

We start with the generic rules from the previous demo:

<pre><code class="language-css">html {
  background: #45473f;
}

body {
  width: 80%;
  margin: 20px auto;
  background: #ffe3a6;
}

#header,
#footer {
  overflow: hidden;
  zoom: 1;
  background: #9c9965;
}

#sidebar {
  float: left;
  width: 200px;
}

#main {
  float: left;
}</code></pre>

To which we add <code>position: relative</code>:

<pre><code class="language-css">#wrapper {
  display: inline-block;
  border-left: 200px solid #d4c37b;
  position: relative;
}

#sidebar {
  margin-left: -200px;
  position: relative;
}</code></pre>

<strong>Note:</strong> there is no need to use <code>clear</code> on the footer since <code>#wrapper</code> <em>contains</em> both floats.

*   Rather than using `overflow`/`zoom`, we use `inline-block` to create a new block formatting context (this declaration also triggers hasLayout). The left border will paint a background color behind `#sidebar`.
*   Negative margin is used to bring `#sidebar` outside the content box of the parent’s container (to make it overlap the border of `#wrapper`).

<strong>The case of IE6:</strong> If the above rules use <code>position: relative</code> (twice), it is because of IE 6. It is applied on <code>#wrapper</code> to prevent <code>#sidebar</code> from being clipped outside of its content box. It is also applied on <code>#sidebar</code> to make sure that the elements are "always" painted with the proper offset.

If you look at this <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73de2e6c-4c37-4d44-9a98-ef24ba7e579e/step-1.html">first step</a>, you’ll see that we have everything working, but the vertical border is in between the columns. You should also notice that in browsers other than IE 6 and 7, there is a small gap at the bottom of <code>#sidebar</code> (at the bottom <code>#wrapper</code> actually). This is because <code>#wrapper</code> is styled with <code>inline-block</code> so it is sitting on the baseline of the line box. The gap you see is the "descender space" (the space reserved for descenders in lowercase letters).

So these are the rules to remove the gap and create the vertical border:

<pre><code class="language-css">#wrapper {
  vertical-align: bottom;
}

#sidebar {
  margin-right: -1px;
  border-right: 1px solid #888;
}

#main {
  border-left:1px solid #888;
}</code></pre>

<strong>What do these rules do?</strong>

*   `vertical-align: bottom` makes `#wrapper` sit at the bottom of the line box rather than the baseline.
*   the two borders (for `#sidebar` and `#main`) overlap because of the negative _right_ margin set on `#sidebar`. This overlap guarantees that this "common" border will be as tall as the tallest column.

If you look at <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18f7af94-c7fa-4bb9-afab-27465bb95e3b/step-2.html">step two</a>, things look much better. The last things to do is to add the <a href="https://thinkvitamin.com/design/setting-rather-than-resetting-default-styling/">base styles sheet</a> and the same rules we used at the end of the first demo:

<pre><code class="language-markup tmp-xml">&lt;link rel="stylesheet" type="text/css" href="https://tjkdesign.com/ez-css/css/base.css"&gt;</code></pre>

and then add these rules:

<pre><code class="language-css">html {
  height: auto;
}

body {
  border: 1px solid #efefef;
}

#header,
#main,
#sidebar,
#footer {
  padding-bottom: 2em;
}</code></pre>

This <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bc61387-64da-4d01-9a9a-a5ec8f387165/step-3.html">last demo</a> for this layout includes the above rules.

## 3\. Creating a three column layout with a border in between the columns

We’ll build a layout with a single <code>#main</code>-wrapper, one containing <strong>all the divs</strong>. This approach complicates things a bit, but it also allows to tackle new challenges. Please note that with this layout, the vertical borders will not show in IE 6 and 7.

<a title="Live Demo" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3009e52c-04ab-4885-bd7c-542f11e2d214/step-5.html"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/903f6d74-4386-42ed-98ec-da2a711f97f9/screenshot-3.png" alt="Three column layout with vertical borders" width="540" height="290" /></a>

### The basics

We use the wrapper to create the background of the three columns. The left and right borders of the wrapper will be used for the two side bars while its background will be used for the main content.

### The markup

<pre><code class="language-markup tmp-xml">&lt;div id="wrapper"&gt;
  &lt;div id="header"&gt;&lt;h2&gt;&lt;a href="#"&gt;Header&lt;/a&gt;&lt;/h2&gt;&lt;p&gt;Lorem ipsum...&lt;/p&gt;&lt;/div&gt;
  &lt;div id="sidebar"&gt;&lt;h2&gt;&lt;a href="#"&gt;Sidebar&lt;/a&gt;&lt;/h2&gt;&lt;p&gt;Lorem ipsum...&lt;/p&gt;&lt;/div&gt;
  &lt;div id="aside"&gt;&lt;h2&gt;&lt;a href="#"&gt;Aside&lt;/a&gt;&lt;/h2&gt;&lt;p&gt;Lorem ipsum...&lt;/p&gt;&lt;/div&gt;
  &lt;div id="main"&gt;&lt;h2&gt;&lt;a href="#"&gt;Main&lt;/a&gt;&lt;/h2&gt;&lt;p&gt;Lorem ipsum...&lt;/p&gt;&lt;/div&gt;
  &lt;div id="footer"&gt;&lt;h2&gt;&lt;a href="#"&gt;Footer &lt;/a&gt;&lt;/h2&gt;&lt;p&gt;Lorem ipsum...&lt;/p&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>

### CSS

We start with the generic rules from the previous demos:

<pre><code class="language-css">html {
  background: #45473f;
}

body {
  width: 80%;
  margin: 20px auto;
  background: #ffe3a6;
}

#header,
#footer {
  overflow: hidden;
  zoom: 1;
  background: #9c9965;
}

#sidebar {
  float: left;
  width: 200px;
}

#main {
  float: left;
}</code></pre>

To which we add:

<pre><code class="language-css">#wrapper {
  border-left: 200px solid #D4C37B;
  background-color: #ffe3a6;
  border-right: 200px solid #D4C37B;
}</code></pre>

This code sets the background color for the three columns. In the same sequence as the above declarations.

If you look at this <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdc789dd-acc3-4c7d-9540-46f4a371d525/step-1.html">first step</a>, you’ll see that we have achieved the background effect we are looking for, but things look pretty broken. Everything shows inside the wrapper’s content box.

These next rules should fix the display of the three columns (<code>zoom: 1</code> for the <code>#wrapper</code> and <code>position: relative</code> for <code>#sidebar</code> and <code>#aside</code>):

<pre><code class="language-markup tmp-xml">#wrapper {
  zoom: 1;
}

#sidebar {
  margin-left:-200px;
  position: relative;
}

#aside {
  float: right;
  width: 200px;
  margin-right: -200px;
  position: relative;
}</code></pre>

#aside is given a width and floated to the right. The negative margins pull each side bar over the wrapper’s border — outside of the content box.

<strong>Note:</strong>IE 6 and 7 needs <code>#wrapper</code> to have a layout, hence the use of <code>zoom</code>. IE 6 needs the two <code>position</code> declarations for the same reason as in the previous demos.

If you look at <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec742587-37f1-4a3d-9651-6d967c605c6b/step-2.html">step two</a>, you’ll see that <code>#header</code> does not stretch across the entire layout and that <code>#footer</code> is nowhere to be found.

These two rules should take care of everything:

<pre><code class="language-css">#header,
#footer {
	margin-left: -200px;
	margin-right: -200px;
	position: relative;
}

#footer {
  clear: both;
}</code></pre>

The negative margin on both sides of <code>#header</code> and <code>#footer</code> stretches the two boxes outside of the wrapper’s content box. <code>clear:both</code> makes the footer clears all the columns. This is <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64bd6370-4f36-4ba8-9d8d-d57b76b6cb23/step-3.html">step three</a>.

Once again, the <code>position</code> declaration is for IE 6. Just remember to always position elements that you offset.

### What’s next?

You know the drill. We insert a base styles sheet in the document:

<pre><code class="language-markup tmp-xml">&lt;link rel="stylesheet" type="text/css" href="https://tjkdesign.com/ez-css/css/base.css"&gt;</code></pre>

and add the usual:

<pre><code class="language-css">html {
  height: auto;
}

body {
  border: 1px solid #efefef;
}

#header,
#main,
#sidebar,
#footer {
  padding-bottom: 2em;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8e02efd-0b04-4114-8fb8-6208cfa0ab01/step-4.html">Step four</a> shows how things look before we tackle the vertical borders.

### Adding vertical borders

The following technique is inspired from the <a href="https://www.satzansatz.de/cssd/companions.html">companion columns</a> technique (Ingo Chao) and the <a href="https://css-tricks.com/fluid-width-equal-height-columns/">Nicolas Gallagher method</a>.

To get the effect we want (two borders touching each other), we use generated content to which we apply a background color and a border.

### The CSS

<pre><code class="language-css">html:before {
	content: ".";
	position: absolute;
	height: 20px;
	background: #45473f;
	left: 0;
	right: 0;
	z-index: 2;
}
</code></pre>

If you look at this <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73de2e6c-4c37-4d44-9a98-ef24ba7e579e/step-1.html">first step</a>, you’ll see that we have everything working, but the vertical border is in between the columns. You should also notice that in browsers other than IE 6 and 7, there is a small gap at the bottom of <code>#sidebar</code> (at the bottom <code>#wrapper</code> actually). This is because <code>#wrapper</code> is styled with <code>inline-block</code> so it is sitting on the baseline of the line box. The gap you see is the "descender space" (the space reserved for descenders in lowercase letters).

So these are the rules to remove the gap and create the vertical border:

<pre><code class="language-css">#wrapper {
  vertical-align: bottom;
}

#sidebar {
  margin-right: -1px;
  border-right: 1px solid #888;
}

#main {
  border-left:1px solid #888;
}</code></pre>

<strong>What do these rules do?</strong>

*   `vertical-align: bottom` makes `#wrapper` sit at the bottom of the line box rather than the baseline.
*   the two borders (for `#sidebar` and `#main`) overlap because of the negative _right_ margin set on `#sidebar`. This overlap guarantees that this "common" border will be as tall as the tallest column.

If you look at <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18f7af94-c7fa-4bb9-afab-27465bb95e3b/step-2.html">step two</a>, things look much better. The last things to do is to add the <a href="https://thinkvitamin.com/design/setting-rather-than-resetting-default-styling/">base styles sheet</a> and the same rules we used at the end of the first demo:

<pre><code class="language-markup tmp-xml">&lt;link rel="stylesheet" type="text/css" href="https://tjkdesign.com/ez-css/css/base.css"&gt;</code></pre>

and then add these rules:

<pre><code class="language-css">html {
  height: auto;
}

body {
  border: 1px solid #efefef;
}

#header,
#main,
#sidebar,
#footer {
  padding-bottom: 2em;
}</code></pre>

This <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bc61387-64da-4d01-9a9a-a5ec8f387165/step-3.html">last demo</a> for this layout includes the above rules.

{{% ad-panel-leaderboard %}}

## 3\. Creating a three column layout with a border in between the columns

We’ll build a layout with a single <code>#main</code>-wrapper, one containing <strong>all the divs</strong>. This approach complicates things a bit, but it also allows to tackle new challenges. Please note that with this layout, the vertical borders will not show in IE 6 and 7.

<a title="Live Demo" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3009e52c-04ab-4885-bd7c-542f11e2d214/step-5.html"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/903f6d74-4386-42ed-98ec-da2a711f97f9/screenshot-3.png" alt="Three column layout with vertical borders" width="540" height="290" /></a>

### The basics

We use the wrapper to create the background of the three columns. The left and right borders of the wrapper will be used for the two side bars while its background will be used for the main content.

### The markup

<pre><code class="language-markup tmp-xml">&lt;div id="wrapper"&gt;
  &lt;div id="header"&gt;&lt;h2&gt;&lt;a href="#"&gt;Header&lt;/a&gt;&lt;/h2&gt;&lt;p&gt;Lorem ipsum...&lt;/p&gt;&lt;/div&gt;
  &lt;div id="sidebar"&gt;&lt;h2&gt;&lt;a href="#"&gt;Sidebar&lt;/a&gt;&lt;/h2&gt;&lt;p&gt;Lorem ipsum...&lt;/p&gt;&lt;/div&gt;
  &lt;div id="aside"&gt;&lt;h2&gt;&lt;a href="#"&gt;Aside&lt;/a&gt;&lt;/h2&gt;&lt;p&gt;Lorem ipsum...&lt;/p&gt;&lt;/div&gt;
  &lt;div id="main"&gt;&lt;h2&gt;&lt;a href="#"&gt;Main&lt;/a&gt;&lt;/h2&gt;&lt;p&gt;Lorem ipsum...&lt;/p&gt;&lt;/div&gt;
  &lt;div id="footer"&gt;&lt;h2&gt;&lt;a href="#"&gt;Footer &lt;/a&gt;&lt;/h2&gt;&lt;p&gt;Lorem ipsum...&lt;/p&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>

### CSS

We start with the generic rules from the previous demos:

<pre><code class="language-css">html {
  background: #45473f;
}

body {
  width: 80%;
  margin: 20px auto;
  background: #ffe3a6;
}

#header,
#footer {
  overflow: hidden;
  zoom: 1;
  background: #9c9965;
}

#sidebar {
  float: left;
  width: 200px;
}

#main {
  float: left;
}</code></pre>

To which we add:

<pre><code class="language-css">#wrapper {
  border-left: 200px solid #D4C37B;
  background-color: #ffe3a6;
  border-right: 200px solid #D4C37B;
}</code></pre>

This code sets the background color for the three columns. In the same sequence as the above declarations.

If you look at this <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdc789dd-acc3-4c7d-9540-46f4a371d525/step-1.html">first step</a>, you’ll see that we have achieved the background effect we are looking for, but things look pretty broken. Everything shows inside the wrapper’s content box.

These next rules should fix the display of the three columns (<code>zoom: 1</code> for the <code>#wrapper</code> and <code>position: relative</code> for <code>#sidebar</code> and <code>#aside</code>):

<pre><code class="language-markup tmp-xml">#wrapper {
  zoom: 1;
}

#sidebar {
  margin-left:-200px;
  position: relative;
}

#aside {
  float: right;
  width: 200px;
  margin-right: -200px;
  position: relative;
}</code></pre>

`#aside` is given a width and floated to the right. The negative margins pull each side bar over the wrapper’s border — outside of the content box.

<p><strong>Note</strong>: <em>IE 6 and 7 need</em> <code>#wrapper</code> <em>to have a layout, hence the use of</em> <code>zoom</code>. <em>IE 6 needs the two</em> <code>position</code> <em>declarations for the same reason as in the previous demos.</em></p>

If you look at <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec742587-37f1-4a3d-9651-6d967c605c6b/step-2.html">step two</a>, you’ll see that <code>#header</code> does not stretch across the entire layout and that <code>#footer</code> is nowhere to be found.

These two rules should take care of everything:

<pre><code class="language-css">#header,
#footer {
	margin-left: -200px;
	margin-right: -200px;
	position: relative;
}

#footer {
  clear: both;
}</code></pre>

The negative margin on both sides of <code>#header</code> and <code>#footer</code> stretches the two boxes outside of the wrapper’s content box. <code>clear:both</code> makes the footer clears all the columns. This is <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64bd6370-4f36-4ba8-9d8d-d57b76b6cb23/step-3.html">step three</a>.

Once again, the <code>position</code> declaration is for IE 6. Just remember to always position elements that you offset.

### What’s next?

You know the drill. We insert a base styles sheet in the document:

<pre><code class="language-markup tmp-xml">&lt;link rel="stylesheet" type="text/css" href="https://tjkdesign.com/ez-css/css/base.css"&gt;</code></pre>

and add the usual:

<pre><code class="language-css">html {
  height: auto;
}

body {
  border: 1px solid #efefef;
}

#header,
#main,
#sidebar,
#footer {
  padding-bottom: 2em;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8e02efd-0b04-4114-8fb8-6208cfa0ab01/step-4.html">Step four</a> shows how things look before we tackle the vertical borders.

### Adding vertical borders

The following technique is inspired from the <a href="https://www.satzansatz.de/cssd/companions.html">companion columns</a> technique (Ingo Chao) and the <a href="https://css-tricks.com/fluid-width-equal-height-columns/">Nicolas Gallagher method</a>.

To get the effect we want (two borders touching each other), we use generated content to which we apply a background color and a border.

### The CSS

<pre><code class="language-css">html:before {
	content: ".";
	position: absolute;
	height: 20px;
	background: #45473f;
	left: 0;
	right: 0;
	z-index: 2;
}

body {
  border-top: 0;
}

#header {
  border-top: 1px solid #fff;
}

#wrapper {
  position: relative;
}

#header,
#footer {
  z-index: 1;
}

#wrapper:before,
#wrapper:after {
  content: ".";
  position: absolute;
  width: 1px;
  height: 2000px;
  background: #9c9965;
  bottom: 0;
}

#wrapper:before {
  left: 0;
  border-left: 1px solid #fff;
}

#wrapper:after {
  right: 0;
  border-right: 1px solid #fff;
}

body {
	position: relative9;
	z-index: -1;
}</code></pre>

OK, so what’s going on here?

*   The fake borders get out of the container (at the top), so the first rule paints generated content on top of them. Note that we would not need this rule if the color of the fake borders was the same as the page’s background (`html`), or if there was no gap between the top of the viewport and the layout.
*   Because these borders are painted over the border around `body`, we move the top border from `body` to `#header`.
*   To properly position the fake borders, we need to make the wrapper the containing block for the generated content.
*   We bring `#header` and `#footer` above the stack so they hide the fake borders which are painted inside the wrapper (**from bottom to top**).
*   This is the generated content we use to create the columns.

<p><strong>The case of IE 8:</strong> The last rule is for IE 8. Without this, IE 8 would not paint the generated content over the borders that escape the wrapper (at the top). If this declaration is sandboxed via the "9" hack, it is because Gecko browsers would make everything unclickable/unselectable.

<p><strong>Note:</strong> <em>These pseudo-classes are not supported by IE 6 and 7, so in these browsers, there are no borders between the columns.</em>

## Things To Consider

<p>The third layout uses one <em>main</em> wrapper, but it would make more sense to use a <em>inner</em> wrapper instead to hold only the columns. In case this route was taken here, then it was only for those of you who are stuck with this type of construct, but want to implement this solution for equal height columns.</p>

<p>When absolutely positioning elements inside a containing block with wide columns like in the last two demos, remember that the reference is the padding box, so <code>0</code> for <code>right</code> or <code>left</code> may not be the value you would want to use.</p>

### Further Reading

*   [Faux columns](https://www.alistapart.com/articles/fauxcolumns/)
*   [Ultimate multi-column liquid layouts](https://matthewjamestaylor.com/blog/ultimate-multi-column-liquid-layouts-em-and-pixel-widths)
*   [Doug Neiner Method](https://css-tricks.com/fluid-width-equal-height-columns/)
*   [Nicolas Gallagher Method](https://css-tricks.com/fluid-width-equal-height-columns/)
*   [Balance your CSS Columns with JavaScript](https://www.paulbellows.com/getsmart/balance_columns/)
*   [Absolute Columns](https://24ways.org/2008/absolute-columns)
*   [Companion columns](https://www.satzansatz.de/cssd/companions.html)

### <span class="rh">Related Reading</span> on SmashingMag:

*   [The Definitive Guide to Using Negative Margins](https://www.smashingmagazine.com/2009/07/the-definitive-guide-to-using-negative-margins/)
*   [Flexbox Is As Easy As Pie – Designing CSS Layouts](https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/)
*   [CSS Float Theory: Things You Should Know](https://www.smashingmagazine.com/2007/05/css-float-theory-things-you-should-know/)

{{< signature "vf, il" >}}

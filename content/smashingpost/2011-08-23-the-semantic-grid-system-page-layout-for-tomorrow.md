---
title: 'The Semantic Grid System: Page Layout For Tomorrow'
slug: the-semantic-grid-system-page-layout-for-tomorrow
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21fab4e4-9ae6-4111-b4dc-b0def16805b1/semantic-grid1.jpg
date: 2011-08-23T07:00:12.000Z
author: tyler-tate
summary: >-
  Understand the three seemingly insurmountable flaws currently affecting CSS grids and then have a look at what you can do with LESS: use variables, perform operations, and develop reusable mixins.
description: >-
  Understand the three seemingly insurmountable flaws currently affecting CSS grids and then have a look at what you can do with LESS: use variables, perform operations, and develop reusable mixins.
categories:
  - Coding
  - Layouts
  - CSS
  - Grids
  - Semantics
---

CSS grid frameworks can make your life easier, but they’re not without their faults. Fortunately for us, modern techniques offer a new approach to constructing page layouts. But before getting to the solution, we must first understand the three seemingly insurmountable flaws currently affecting CSS grids.

{{% feature-panel %}}

## Problems

### Problem #1: They’re Not Semantic

The biggest complaint I’ve heard from purists since I created <a href="https://1kbgrid.com/">The 1KB CSS Grid</a> two years ago is that CSS grid systems don’t allow for a proper separation of mark-up and presentation. Grid systems require that Web designers add <code>.grid_x</code> CSS classes to HTML elements, mixing presentational information with otherwise semantic mark-up.

Floated elements must also be cleared, often requiring unnecessary elements to be added to the page. This is illustrated by the “clearing” div that ships with <a href="https://960.gs/">960.gs</a>:

<pre><code class="language-markup tmp-html">&lt;div class="grid_3"&gt;
	220
&lt;/div&gt;
&lt;div class="grid_9"&gt;
	700
&lt;/div&gt;
&lt;div class="clear"&gt;&lt;/div&gt;</code></pre>

### Problem #2: They’re Not Fluid

While CSS grids work well for fixed-width layouts, dealing with fluid percentages is trickier. While most grid systems do provide a fluid option, they break down when nested columns are introduced. In the 1KB CSS Grid example below, <code>.grid_6</code> would normally be set to a width of 50%, while <code>.grid_3</code> would typically be set to 25%.

But when <code>.grid_3</code> appears inside of a <code>.grid_6</code> cell, the percentages must be recalculated. While a typical grid system needs just 12 CSS rules to specify the widths of all 12 columns, a fluid grid would need 144 rules to allow for just one level of nesting: possible, but not very convenient.

<pre><code class="language-markup tmp-html">&lt;div class="column grid_6"&gt;
	&lt;div class="row"&gt;
		&lt;div class="column grid_3"&gt; &lt;/div&gt;
		&lt;div class="column grid_3"&gt; &lt;/div&gt;
	&lt;/div&gt;
&lt;/div&gt;</code></pre>

### Problem #3: They’re Not Responsive

Responsive Web design is the buzzword of the year. While new tools such as 1140 CSS Grid and <a href="https://adapt.960.gs/">Adapt.js</a> are springing up that enable you to alter a page’s layout based on screen size or device type, an optimal solution has yet to arrive.

## Blame It On The Tools

All three of these problems directly result from the limitations of our existing tools. CSS leaves us with the ultimatum of either compromising our principles by adding presentational classes to mark-up, or sticking to our guns and forgoing a grid system altogether. But, hey, we can’t do anything about it, right?

Well, not so fast. While we wait for browsers to add <a href="https://www.netmagazine.com/features/future-css-layouts">native CSS support</a> for this flawed <a href="https://www.markboulton.co.uk/journal/comments/rethinking-css-grids">grid layout module</a>, a futuristic version of CSS is available *today* that’s already supported by every CSS-enabled browser: <a href="https://lesscss.org/">LESS CSS</a>.

<figure><a href="https://lesscss.org/"><img class="105539 " title="less-css" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e9c0c1e-1e0b-4674-b0ad-877b825df537/less-css.jpg" alt="screenshot" width="500" height="300" /></a><figcaption>LESS brings powerful new features to CSS.</figcaption></figure>

## LESS What?

You’ve probably heard of LESS but perhaps have never given it a try. Similar to <a href="https://sass-lang.com/docs/yardoc/file.INDENTED_SYNTAX.html">SASS</a>, LESS is *extends* CSS by giving you the ability to use variables, perform operations and develop reusable mixins. Below are a few examples of what it can do.

**Variables**

Specify a value once, and then reuse it throughout the style sheet by defining variables.

<pre><code class="language-css">// LESS
@color: #4D926F;

#header {
  color: @color;
}</code></pre>

The above example would compile as follows:

<pre><code class="language-css">/* Compiled CSS */
#header {
  color: #4D926F;
}</code></pre>

### Operations

Multiply, divide, add and subtract values and colors using operations.

<pre><code class="language-css">// LESS
@border-width: 1px;

#header {
	border-left: @border-width * 3;
}</code></pre>

In this example, <code>1px</code> is multiplied by <code>3</code> to yield the following:

<pre><code class="language-css">/* Compiled CSS */
#header {
	border-left: 3px;
}</code></pre>

### Mixins

Most powerful of all, mixins enable entire snippets of CSS to be reused. Simply include the class name of a mixin within another class. What’s more, LESS allows parameters to be passed into the mixin.

<pre><code class="language-css">// LESS
.rounded(@radius) {
    -webkit-border-radius: @radius;
    -moz-border-radius: @radius;
    border-radius: @radius;
}

#header {
    .rounded(5px);
}</code></pre>

Verbose, browser-specific CSS3 properties demonstrate the benefit that mixins bring:

<pre><code class="language-css">/* Compiled CSS */
#header {
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
}</code></pre>

### Downsides To LESS

Having been skeptical of LESS at first, I’m now a strong advocate. LESS style sheets are concise and readable, and they encourage code to be reused. However, there are some potential downsides to be aware of:

1.  It has to be compiled. This is one extra step that you don’t have to worry about with vanilla CSS.
2.  Depending on how LESS documents are structured, the compiled CSS file might be slightly larger than the equivalent hand-crafted CSS file.

### A Note On Compiling LESS

There are three approaches to compiling LESS style sheets into CSS:

*   **Let the browser do the compiling.**  
As its name suggests, [LESS.js](https://lesscss.org/) is written in JavaScript and can compile LESS into CSS directly in the user’s browser. While this method is convenient for development, using one of the next two methods before going into production would be best (because compiling in the browser can take a few hundred milliseconds).
*   **Use a server-side compiler.**  
LESS.js can also compile server-side with [Node.js](https://nodejs.org/), and it has been ported to several other sever-side languages.
*   **Use a desktop app.**  
[LESS.app](https://incident57.com/less/) is a Mac app that compiles local files as they’re saved on your computer.

{{% ad-panel-leaderboard %}}

## Introducing The Semantic Grid System

The innovations that LESS brings to CSS are the foundation for a powerful new approach to constructing page layouts. That approach is the <a href="https://semantic.gs/">The Semantic Grid System</a>. This new breed of CSS grid shines where the others fall short:

1.  It’s semantic;
2.  It can be either fixed or fluid;
3.  It’s responsive;
4.  It allows the number of columns, column widths and gutter widths to be modified instantly, directly in the style sheet.

<figure><a href="https://semantic.gs/"><img class="105540" title="semantic-grid" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79d7e821-eae1-4beb-ad15-58ad58d1f3bf/semantic-grid.jpg" alt="screenshot" width="500" height="267" /></a><figcaption>The Semantic Grid System uses LESS CSS to offer a new approach to page layout.</figcaption></figure>

### Configuring The Grid

Sounds too good to be true? Here’s how it works.

First, import the semantic grid into your working LESS style sheet.

<pre><code class="language-css">@import 'grid.less';</code></pre>

Next, define variables for the number of columns, and set the desired widths for the column and gutter. The values entered here will result in a 960-pixel grid system.

<pre><code class="language-css">@columns: 12;
@column-width: 60;
@gutter-width: 20;</code></pre>

The grid is now configured and ready to be used for page layout.

### Using The Grid

Now that the grid has been configured, consider two elements on an HTML page that you would like to lay out side by side.

<pre><code class="language-markup tmp-html">&lt;body&gt;
	&lt;article&gt;Main&lt;/article&gt;
	&lt;section&gt;Sidebar&lt;/section&gt;
&lt;/body&gt;</code></pre>

The side-by-side layout can be achieved by passing the desired number of grid units to the <code>.column()</code> mixin (which is defined in the *grid.less* file).

<pre><code class="language-css">// LESS
@import 'grid.less';

@columns: 12;
@column-width: 60;
@gutter-width: 20;

article {
	.column(9);
}
section {
	.column(3);
}</code></pre>

The above LESS would be compiled to CSS as the following:

<pre><code class="language-css">/* Compiled CSS */
article {
	display: inline;
	float: left;
	margin: 0px 10px;
	width: 700px;
}
section {
	display: inline;
	float: left;
	margin: 0px 10px;
	width: 220px;
}</code></pre>

<a href="https://semantic.gs/examples/fixed/fixed.html">This page</a> demonstrates the result. What makes this approach so different is that it does away with ugly <code>.grid_x</code> classes in the mark-up. Instead, column widths are set directly in the style sheet, enabling a clean separation between declarative mark-up and presentational style sheets. (It’s called the *semantic* grid for a reason, after all.)

### So, What’s Behind The Curtain?

For the curious among you, below are the mixins at the center of it all. Fortunately, these functions are hidden away in the *grid.less* file and need not ever be edited.

<pre><code class="language-css">// Utility variable — you will never need to modify this
@_gridsystem-width: (@column-width*@columns) + (@gutter-width*@columns) * 1px;

// Set @total-width to 100% for a fluid layout
@total-width: @_gridsystem-width;

// The mixins
.row(@columns:@columns) {
   display: inline-block;
   overflow: hidden;
   width: @total-width*((@gutter-width + @_gridsystem-width)/@_gridsystem-width);
   margin: 0 @total-width*(((@gutter-width*.5)/@_gridsystem-width)*-1);
}
.column(@x,@columns:@columns) {
   display: inline;
   float: left;
   width: @total-width*((((@gutter-width+@column-width)*@x)-@gutter-width) / @_gridsystem-width);
   margin: 0 @total-width*((@gutter-width*.5)/@_gridsystem-width);
}</code></pre>

## Fluid Layouts

The example above demonstrates a fixed pixel-based layout. But fluid percentage-based layouts are just as easy. To switch from pixels to percentages, simply add one variable:

<pre><code class="language-css">// LESS
@total-width: 100%;</code></pre>

With no other changes, the compiled CSS then becomes this:

<pre><code class="language-css">/* Compiled CSS */
article {
	display: inline;
	float: left;
	margin: 0px 1.04167%;
	width: 72.9167%;
}
section {
	display: inline;
	float: left;
	margin: 0px 1.04167%;
	width: 22.9167%;
}</code></pre>

<a href="https://semantic.gs/examples/fluid/fluid.html">This example</a> shows how the percentages are dynamically calculated using LESS operations, which also applies to nested columns.

## Responsive Layouts

No modern grid system would be complete unless we had the ability to adapt the layout of the page to the size of the user’s screen or device. With Semantic.gs, manipulating the grid using media queries <a href="https://semantic.gs/examples/responsive/responsive.html">couldn’t be any easier</a>:

<pre><code class="language-css">article { .column(9); }
section { .column(3); }

@media screen and (max-width: 720px) {
	article { .column(12); }
	section { .column(12); }
}</code></pre>

## Try It For Yourself

Just a couple of days ago Twitter released a project called <a href="https://twitter.github.com/bootstrap/">Bootstrap</a> which provides similar (but more limited) grid system built using LESS variable and mixins. The future of the CSS grid seems to be taking shape before us.

The Semantic Grid System delivers the best of both worlds: the power and convenience of a CSS grid and the ideal separation of mark-up and presentation. <a href="https://semantic.gs">Download the grid</a> for yourself, fork it on <a href="https://github.com/twigkit/semantic.gs">GitHub</a>, and let us know what you think!

<figure><a href="https://semantic.gs"><img class="105544" title="semanticgs" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/695e0ccb-8f2c-48bd-a377-f8376b9eb27b/semanticgs.jpg" alt="" width="500" height="465" /></a><figcaption>Download the grid from Semantic.gs.</figcaption></figure>

{{% ad-panel-leaderboard %}}

### Other Resources

*   [Semantic.gs](https://semantic.gs) Download the grid system.
*   [LESS](https://lesscss.org) Find out more about LESS.
*   “[Responsive Web Design](https://www.alistapart.com/articles/responsive-web-design/),” Ethan Marcotte
*   1140 CSS Grid and [Adapt.js](https://adapt.960.gs/) Two other approaches to responsive layouts.
*   “[Rethinking CSS Grids](https://www.markboulton.co.uk/journal/comments/rethinking-css-grids),” Mark Boulton
*   “[Best Practices Are Killing Us](https://www.lukew.com/ff/entry.asp?1379)” Nicole Sullivan’s contrarian views on semantics, as described by Luke Wroblewski.
*   [1KB CSS Grid](https://1kbgrid.com/) Play with Tyler Tate’s original CSS grid.

### Further Reading

*   [Grid-Based Web Design, Simplified](https://www.smashingmagazine.com/2010/04/grid-based-web-design-simplified/)
*   [Designing With Grid-Based Approach](https://www.smashingmagazine.com/2007/04/designing-with-grid-based-approach/)
*   [Semantic CSS With Intelligent Selectors](https://www.smashingmagazine.com/2013/08/semantic-css-with-intelligent-selectors/)

{{< signature "al, mrn" >}}

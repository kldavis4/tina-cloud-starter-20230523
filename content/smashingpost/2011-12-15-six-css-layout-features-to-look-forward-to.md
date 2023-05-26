---
title: Six CSS Layout Features To Look Forward To
slug: six-css-layout-features-to-look-forward-to
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8afc12dd-34ab-4ae5-81c5-9c4021f0cabe/column-span-all1.jpg
date: 2011-12-15T14:23:41.000Z
author: divya-manian
description: >-
  A few concerns keep bobbing up now and then for Web developers, one of which relates to how to lay out a given design. Developers have made numerous attempts to do so with existing solutions. Several articles have been written on finding the holy grail of CSS layouts, but to date, not a single solution works without major caveats.
categories:
  - Coding
  - Layouts
  - CSS
  - CSS3
---
At W3Conf, I gave a talk on how the CSS Working Group is attempting to solve the concerns of Web developers with multiple proposals. There are six layout proposals that are relevant to us, all of which I described in the talk. Here is a little more about these proposals and how they will help you in developing websites in the future.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Killer Responsive Layouts With CSS Regions](https://www.smashingmagazine.com/2013/11/killer-responsive-layouts-with-css-regions/)
*   [CSS Inheritance, The Cascade And Global Scope](https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/)
*   [Using Sketch For Responsive Web Design](https://www.smashingmagazine.com/2015/04/using-sketch-for-responsive-web-design-case-study/)
*   [CSS Grid, Flexbox And Box Alignment](https://www.smashingmagazine.com/2016/11/css-grids-flexbox-and-box-alignment-our-new-system-for-web-layout/)

## Generated Content For Paged Media

*   [W3C Editor’s Draft](https://dev.w3.org/csswg/css3-gcpm/)
*   [Demo](https://people.opera.com/howcome/2011/reader/)

{{% feature-panel %}}

This proposal outlines a set of features that would modify the contents of any element to flow as pages, like in a book. A <a href="https://youtube.com/watch?v=e_xpbQHtVGE">video demonstration</a> shows how to use paged media to generate HTML5 slideshows (look at the demos for GCPM in the <a href="https://people.opera.com/howcome/2011/reader/">Opera Labs Build</a> to play with the features more). To make the content of an element be paged, you would use this syntax:

<pre><code class="language-css">@media paged {
  html {
    width: 100%;
    overflow-style: paged-x;
    padding: 5%;
    height: 100%;
    box-sizing: border-box;
  }
}</code></pre>

This would make the content look something like this:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce620e2e-60a3-445c-a4b9-368a22ec42df/6d8decb25ed55a951d41653f79b59bbb.png" alt="screenshot" />

Here, <code>@media paged</code> indicates that the browser understands paged media and that all of the selectors specified for it should have their styles applied when paged media is supported. Then, you indicate which selector you want to be paged (in the above example, the selector is the <code>html</code> element itself) by specifying the property <code>overflow-style: paged-x</code>. This will simply make the content paged; if you want paged controls to be visible, you need to specify <code>overflow-style: paged-x-controls</code>.

The properties <code>break-before</code>, <code>break-after</code> <code>break-inside</code> can be used to control where the content falls within the pages. For example, if you want headings to only appear with their corresponding content and never at the end of the page or standing alone, you can specify that:

<pre><code class="language-css">h3, h2 {
break-after: avoid;
}</code></pre>

This ensures that if a heading occurs on the last line of a page, it will be pushed to the next page with the content that it introduces.</p>

### API

Two properties are available on an element whose content is paged: <code>currentPage</code> and <code>pageCount</code>. You can set the <code>currentPage</code> property via JavaScript, which would trigger a page change on that element. This would then trigger an <code>onpagechange</code> event on that element, which you could use to run other scripts that are required when the page changes. The <code>pageCount</code> property stores the total number of pages in the paged element. These properties are useful for implementing callbacks that should be triggered on page change; for example, to render notes for a particular slide in a slide deck.</p>

## Multiple Columns

*   [W3C Editor’s Draft](https://dev.w3.org/csswg/css3-multicol/)
*   [Demo](https://people.opera.com/pepelsbey/experiments/multicol/)
*   Browser support: Opera 11.1+, Firefox 2+, Chrome 4+, Safari 3.1+, IE 10+

Multiple columns are now available in most browsers (including IE10!), which makes them pretty much ready to use on production websites. You can render the content of any element into multiple columns simply by using <code>column-width: &lt;length unit&gt;</code> or <code>column-count: &lt;number&gt;</code>. As with paged content, you can use <code>break-before</code>, <code>break-after</code> or <code>break-inside</code> to control how the content displays within each column. You can also make one of the child elements span the whole set of columns by using <code>column-span: all</code>. Here is how that would look:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d03b2bb-edf3-4666-8d21-caf124793663/column-span-all.png" alt="screenshot" width="500" />

Columns are balanced out with content by default. If you would prefer that columns not be balanced, you can set that by using <code>column-fill: auto</code> property. Here is an example of the default behaviour (i.e. <code>column-fill: balanced</code>):

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1ed5617-59df-4d87-9d23-4a45e5cca41d/column-fill-balance.png" alt="screenshot" width="500" />

And here is an example of the <code>column-fill: auto</code> behavior:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c8803d3-7897-44a5-91b0-86ce1404295f/column-fill-auto.png" alt="screenshot" width="500" />

Note that the last column is empty, and each column is filled one after the other.</p>

## Regions

*   [W3C Editor’s Draft](https://dev.w3.org/csswg/css3-regions/)
*   [Demo](https://ie.microsoft.com/testdrive/Graphics/hands-on-css3/hands-on_regions.htm)
*   Browser support: IE 10+, Chrome 15+, Safari 6+

The closest equivalent to regions would be InDesign’s linking of text frames. With the properties in this proposal, you can make the content of selected elements flow through another set of elements. In other words, your content need not be tied to the document flow any longer.

To begin, you need to select elements whose content will be part of a “named flow,” like this:

<pre><code class="language-css">article.news { flow-into: article_flow; }</code></pre>

Here, all of the content in the <code>article</code> element with the class name <code>news</code> will belong to the flow named <code>article_flow</code>.

Then, you select elements that will render the contents that are part of this named flow:

<pre><code class="language-css">#main {
flow-from: article_flow;
}</code></pre>

Here, the element with the ID <code>main</code> will be used to display the content in the flow named <code>article_flow</code>. This element has now become a region that renders the content of a named flow. Note that any element that is a region establishes new “block-formatting contexts” and “stacking contexts.” For example, if a child element is part of a flow and is absolutely positioned, it will now only be absolutely positioned with respect to the region it belongs to, and not to the whole viewport.

You can also tweak the styles of content that flows through a region:

<pre><code class="language-css">@region #main {
  p { color: indianred; }
}</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/beea7763-7334-4010-b71e-43ba02f87db0/region-styling.png" alt="screenshot" width="500" />

### API

An interface named <code>getNamedFlow</code> and an event named <code>regionLayoutUpdate</code> are available for elements that are regions.</p>

### getNamedFlow

This returns the flow that that particular region is associated with. The properties available are:

*   `overflow`A read-only boolean that tells you whether all of the content of the named flow fits within the regions that are part of the flow or whether it overflows.
*   `contentNodes`A NodeList of all the content elements that belong to the flow.
*   `getRegionsByContentNode`This returns all of the regions that a particular content element would flow through. A very long paragraph might flow through more than one region; with this method, you can retrieve all of the regions that that paragraph element flows through.
*   `regionLayoutUpdate`This event gets triggered every time an update is made to the layout of a region. If the region’s dimensions are altered, then the child content elements that are part of that region might alter, too (for example, a few might move to another region, or more child elements might become part of the region).</p>

## Exclusions

*   [Draft specification](https://dev.w3.org/csswg/css3-exclusions/) (a combination of two proposals: “Exclusions” and “Positioned Floats”)
*   [Demo](https://ie.microsoft.com/testdrive/Graphics/hands-on-css3/hands-on_positionedfloats.htm)
*   Browser support: IE 10+

Exclusions allow inline content to be wrapped around or within custom shapes using CSS properties. An element becomes an “exclusion element” when <code>wrap-flow</code> is set to a value that is not <code>auto</code>. It can then set the “wrapping area” for inline text outside or within it, according to various CSS properties. The <code>wrap-flow</code> can take the following values: <code>left</code>, <code>right</code>, <code>maximum</code>,<code>both</code>, <code>clear</code> or the default value of <code>auto</code>. Here is how each of these values would affect the inline content around the exclusion element:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3eb8c5f2-3a4a-43da-ba48-508e0623270c/exclusion-wrap-side-auto.png" alt="screenshot" width="429" height="342" />

<em><code>wrap-flow: auto</code></em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/222cd55c-4a68-4639-8e5b-71bd22f9ff99/exclusion-wrap-side-right.png" alt="screenshot" width="426" height="347" />

<em><code>wrap-flow: right</code></em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6860803-fdcb-4ca3-8b1c-7595d9ce6ed5/exclusion-wrap-side-both.png" alt="screenshot" width="443" height="345" />

<em><code>wrap-flow: both</code></em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06221495-cc68-4281-ba0b-2ac2306fc4f2/exclusion-wrap-side-clear.png" alt="screenshot" width="425" height="335" />

<em><code>wrap-flow: clear</code></em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62e6bc20-8f47-40f7-990c-68f78c4d28b8/exclusion-wrap-side-maximum-l.png" alt="screenshot" width="426" height="348" />

<em><code>wrap-flow: maximum</code></em>

The <code>wrap-margin</code> property can be used to offset the space between the boundary of the exclusion element and the inline text <em>outside</em> of it. The <code>wrap-padding</code> property is used to offset the space between the boundary of the exclusion element and the inline text <em>inside</em> it.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06eeb606-88a7-48bc-bf70-a401ffae36ca/exclusions-padding-margin.png" alt="screenshot" width="372" height="301" />

In the above image, the space between the content outside of the red dashed circular border and the black text outside of it is determined by the <code>wrap-margin</code>, while the space between the red dashed circular border and the blue text within it is determined by the <code>wrap-padding</code>.

Now comes the fun part: specifying custom shapes for the wrapping area. You can use two properties: <code>shape-outside</code> lets you set the wrapping area for inline text outside of the exclusion element, while <code>shape-inside</code> lets you set the wrapping area for inline text inside the exclusion element.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94558c35-9b41-4fc0-a021-4f197819253a/exclusions-shapes.png" alt="screenshot" width="478" height="399" />

Both of these properties can take SVG-like syntax (<code>circle(50%, 50%, 100px);</code>) or image URLs to set the wrapping area.

Exclusions make magazine-like layouts on the Web a trivial matter and could spark the kind of creative use of content that we are used to seeing in print!

## Grid

*   [W3C Editor’s Draft](https://dev.w3.org/csswg/css3-grid-align/)
*   [Demo](https://ie.microsoft.com/testdrive/Graphics/hands-on-css3/hands-on_grid.htm)
*   Browser support: IE 10+

Grid properties allow you to throw block-level elements into a grid cell, irrespective of the flow of content within the grid parent element. An element becomes a grid when <code>display</code> is set to <code>grid</code>. You can then set the number of columns and rows with the <code>grid-columns</code> and <code>grid-rows</code> properties, respectively. You can then declare each child selector itself as part of a grid cell, like so:

<pre><code class="language-css">#title {
grid-column: 1; grid-row: 1;
}

#score {
grid-column: 2; grid-row: 1;
}</code></pre>

You can also use a template to plan the grid:

<pre><code class="language-css">body {
  grid-template: "ta"
                 "sa"
                 "bb"
                 "cc";
}</code></pre>

In this syntax, each string refers to a row, and each character refers to a grid cell. In this case, the content of grid cell represented by the character <code>a</code> spans two rows but just one column, and the content represented by <code>b</code> spans two columns but just one row.

Now you can set any of the child element’s <code>grid-cell</code> position:

<pre><code class="language-css">#title {
grid-cell: 't';
}</code></pre>

This will make the element with the ID <code>title</code> within the body element to be positioned in the grid cell represented by the character <code>t</code> in the <code>grid-template</code> property.

If you are not using <code>grid-template</code>, you can also declare how many columns or rows a particular element should occupy with the <code>grid-row-span</code> and <code>grid-column-span</code> properties.</p>

## Flexbox

*   [W3C Editor’s Draft](https://dev.w3.org/csswg/css3-flexbox/)
*   [Demo](https://ie.microsoft.com/testdrive/html5/griddle/default.html)

Flexbox allows you to distribute child elements anywhere in the box (giving us the much-needed vertical centering), along with flexible units that let you control the fluidity of the child elements’ dimensions.

Note that this specification has changed substantially since it was first proposed. Previously, you would invoke Flexbox for an element with <code>display: box</code>, but now you would use <code>display: Flexbox</code> to do so. Child elements can be vertically aligned to the center with <code>flex-pack: center</code> and horizontally aligned to the center with <code>flex-align: center</code>. Also note that all elements that obey the Flexbox need to be block-level elements.</p>

## How Do Various Properties Interact With Each Other?

You might wonder how to use these properties in combination. The following table shows which of these features can be combined.
<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th></th>
<th>Paged Media</th>
<th>Multiple Columns</th>
<th>Regions</th>
<th>Exclusions</th>
<th>Grid</th>
<th>Flexbox</th>
</tr>
</thead>
<tbody>
<tr>
<th>Paged Media</th>
<td class="yes">✓</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<th>Multiple Columns</th>
<td class="yes">✓</td>
<td class="yes">✓</td>
<td class="yes">✓</td>
<td class="yes">✓</td>
<td></td>
<td></td>
</tr>
<tr>
<th>Regions</th>
<td></td>
<td class="yes">✓</td>
<td class="yes">✓</td>
<td class="yes">✓</td>
<td></td>
<td></td>
</tr>
<tr>
<th>Exclusions</th>
<td></td>
<td class="yes">✓</td>
<td class="yes">✓</td>
<td class="yes">✓</td>
<td></td>
<td></td>
</tr>
<tr>
<th>Grid</th>
<td></td>
<td></td>
<td></td>
<td></td>
<td class="yes">✓</td>
<td></td>
</tr>
<tr>
<th>Flexbox</th>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td class="yes">✓</td>
</tr>
</tbody>
</table>

As you can see, the multiple-column properties can be used in conjunction with generated content for paged media, regions and exclusions. <del>But grid, Flexbox and regions are mutually exclusive (i.e. if an element is a grid, it cannot be a Flexbox or region).</del> Do note that, as <a href="https://www.smashingmagazine.com/2011/12/15/six-css-layout-features-to-look-forward-to/#comment-562612">Alan Stearns says in the comments</a>, while a grid container cannot be a Flexbox or a region, a grid cell could become a region, or a Flexbox child item could be a region.</p>

### A Note Before You Rush Out To Use Them In Client Projects

The specifications are always changing, so be careful with them. Except for multiple columns, I would recommend using these strictly in personal projects and demos. The syntaxes and properties used in some of the demos are different from what you would find in the actual specifications, because they have changed since the builds that support a previous version of the specification came out. Also, because they are still unstable, all of these properties are vendor-prefixed, which means you have to add support for each prefix as support is added.

If you do use these features, just make sure that the content is readable in browsers that do not support them. The easiest way to do this would be to use <a href="https://modernizr.com">feature detection</a> and then use CSS to make the content readable when the feature is unsupported.</p>

## Help The Working Group!

Do these layout proposals sound exciting to you? Jump on the <a href="https://lists.w3.org/Archives/Public/www-style/">www-style</a> mailing list to provide feedback on them! Just note that the mailing list will flood your inbox, and you should carefully filter the emails so that you pay attention only to the drafts you are interested in.

Write demos and test how these work, and if you find bugs in the builds that have these properties, provide feedback to the browser vendors and submit bug reports. If you have suggestions for changing or adding properties to these proposals, do write in in the mailing list (or you can <a href="https://twitter.com/divya">bug me on Twitter</a>)!

These are exciting times, and within a few years the way we lay out Web pages will have changed dramatically! Perhaps this will finally sound the death knell of print. (Just kidding.)

{{< signature "al" >}}


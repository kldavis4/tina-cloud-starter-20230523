---
title: Device-Agnostic Approach To Responsive Web Design
slug: device-agnostic-approach-to-responsive-web-design
image: null
date: 2012-03-22T13:55:44.000Z
author: thierry-koblentz
description: >-
  This is a different take on Responsive Web design. This article discusses how
  we can better embrace what the Web is about by ignoring the big elephant in
  the room; that is, how we can rely on media queries and breakpoints without
  any concern for devices.
categories:
  - Coding
  - Techniques
  - Responsive Design
---
This is a different take on Responsive Web design. This article discusses how we can better embrace what the Web is about by ignoring the big elephant in the room; that is, how we can rely on media queries and breakpoints without any concern for devices.</p>

## The Challenge

Let's start our journey by looking at these online tools:

*   [Responsive Design Testing](https://mattkersley.com/responsive/)
*   [Responsive.is](https://responsive.is/)
*   [Responsinator](https://www.responsinator.com/)
*   [BriCSS](https://www.benjaminkeen.com/misc/bricss/)

Those pages let people check websites through a set of pre-built views based on various device sizes or orientations. <a href="https://www.benjaminkeen.com/misc/bricss/">Bricss</a> goes one step further as it allows you to "customize" viewports by setting any dimensions you want.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [Design Process In The Responsive Age](https://www.smashingmagazine.com/2012/05/design-process-responsive-age/)
*   [Responsive Web Design Techniques, Tools and Design Strategies](https://www.smashingmagazine.com/2011/07/responsive-web-design-techniques-tools-and-design-strategies/)
*   [12 Factors In Selecting A Mobile Prototyping Tool](https://www.smashingmagazine.com/2016/04/factors-selecting-mobile-prototyping-tool/)

Now check <a href="https://punchcut.com/perspectives/the-great-tablet-flood">the-great-tablet-flood of 2011</a>.

Do you get my drift? Trying to check layouts against specific sets of dimensions is a losing battle. Besides, using existing devices to set break-points is not what I'd call a "future proof" approach, as there is no for standard sizes or ratios.

I don't want to go the "<a href="https://meyerweb.com/eric/comment/chech.html">consider it to be harmful</a>" route, but I want to point out that tools like these, or articles promoting a device approach (i.e. <a href="https://www.metaltoad.com/blog/simple-device-diagram-responsive-design-planning">Device Diagram for Responsive Design Planning</a>), make people focus on the wrong end of the problem, reinforcing the idea that <em>responsive</em> is all about devices.

To me, it seems more realistic to check our layouts through viewports of arbitrary dimensions and shapes. We don't need anything fancy, we can simply drag the bottom right corner of our favorite desktop browser to enter: "Device Agnostic Mode".</p>

## The Goal

The goal is to surface content, to style boxes as columns so they bring sections above the fold. The question is: when should we bring a box "up"?

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [The State Of Responsive Web Design](https://www.smashingmagazine.com/2013/05/the-state-of-responsive-web-design/)
*   [Design Process In The Responsive Age](https://www.smashingmagazine.com/2012/05/design-process-responsive-age/)

## Content Is King!

If we consider that content is king, then it makes sense to look at it as the corner stone of the solution. In other words, we should set break-points according to <strong>content</strong> instead of devices.</p>

### The Principle

The content of a box <em>dictates</em> its width. It is the minimum width of adjacent containers that create break points (a size at which we can display boxes next to each other).

Decisions are made keeping these points in mind:

*   The width of a box should be as small or as wide as possible without impairing readability.
*   The max-width of a box should take into consideration the importance of following boxes. This is because the wider the box, the wider the viewport must be to reveal subsequent boxes.
*   The goal is **not** to bring everything above the fold (we don't want to fill the viewport with clutter).</p>

## In Practice

### Markup

For this exercise, we will consider 5 main blocks:

<pre><code class="language-markup">&lt;div class="grid-block" id="header"&gt;&lt;/div&gt;
&lt;div id="wrapper"&gt;
    &lt;div class="grid-block" id="main"&gt;&lt;/div&gt;
    &lt;div class="grid-block" id="complementary"&gt;&lt;/div&gt;
    &lt;div class="grid-block" id="aside"&gt;&lt;/div&gt;
&lt;/div&gt;
&lt;div class="grid-block" id="contentinfo"&gt;&lt;/div&gt;</code></pre>

The wrapper will allow us to:

*   mix percentages and pixels to style boxes on the same row
*   set a maximum width for a group of boxes

### CSS

To build our grid we will rely on <code>display:inline-block</code> mainly for horizontal alignment and inline flow. But note that this choice also gives us an extra edge to play with (more on this later).

Also note that we will override this styling with <code>float</code> to achieve some specific layouts.

<pre><code class="language-css">body {
        margin:auto;            /* you'll see why later */
        text-align:center;      /* to center align grid boxes */
        letter-spacing: -0.31em;/* webkit: collapse white-space between units */
        *letter-spacing: normal;/* reset IE &lt; 8 */
        word-spacing: -0.43em;  /* IE &lt; 8 &amp;&amp; gecko: collapse white-space between units */
    }
    .grid-block {
        letter-spacing: normal; /* reset */
        word-spacing: normal;   /* reset */
        text-align:left;        /* reset */
        display:inline-block;   /* styling all grid-wrapper as inline blocks */
        vertical-align:top;     /* aligning those boxes at the top */
        *display:inline;        /* IE hack to mimic inline-block */
        zoom:1;                 /* part of the above hack for IE */
        width:100%;             /* boxes would shrink-wrap */
    }

    /**
     * rules below are meant to paint the boxes
     */

    .grid-block {
        height: 150px;
    }
    #header {
        background: #d6cac1;
    }
    #main {
        background: #ad9684;
    }
    #complementary {
        background: #7a6351;
    }
    #aside {
        background: #000000;
    }
    #contentinfo {
        background: #3d3128;
    }</code></pre>

This produces a <a href="https://www.css-101.org/articles/responsive_design/demos/step-1.html">bunch of rows</a>.</p>

### Content-Driven Process

We define the width of each box according to its content. These values will then be used to set breakpoints. Note that the values below take into consideration a 10px gutter between columns.
<dl>
 	<dt><strong>Header</strong></dt>
    <dd>content: logo, navigation, search box</dd>
    <dd>type: banner</dd>
 	<dd>minimum width: n/a</dd>
 	<dd>maximum width: n/a</dd>
 	<dt><strong>Main</strong></dt>
    <dd>content: diverse (article, blog entry, comments, etc.)</dd>
    <dd>type: main box that holds the meat of the page</dd>
 	<dd>minimum width: 420px [<a href="#footnote">1</a>]</dd>
 	<dd>maximum width: 550px [<a href="#footnote">1</a>]</dd>
 	<dt><strong>Complementary</strong></dt>
    <dd>content: directory entries, tweets, etc.</dd>
    <dd>type: multi-line text box with media</dd>
 	<dd>minimum width: 280px</dd>
 	<dd>maximum width: 380px</dd>
 	<dt><strong>Aside</strong></dt>
    <dd>content: Ads</dd>
    <dd>type: 230px wide images</dd>
 	<dd>fixed width: 250px or 490px (2 ads side by side)</dd>
 	<dt><strong>Contentinfo</strong></dt>
    <dd>content: resources, blog roll, etc.</dd>
    <dd>type: lists of links</dd>
 	<dd>minimum width: 220px</dd>
 	<dd>maximum width: 280px</dd>
</dl>
The minimum and maximum widths above only come into play when the box is displayed as a column.</p>

## Breakpoints

The width of the containers establishes our breakpoints. Breakpoints are viewport's widths at which we decide to display a box as a column (instead of a row).</p>

### How Do We "Pick" Breakpoints?

Until we are able to use something like <a href="https://www.google.com/url?sa=t&amp;rct=j&amp;q=&amp;esrc=s&amp;source=web&amp;cd=1&amp;cts=1330897432181&amp;ved=0CDEQFjAA&amp;url=http%3A%2F%2Fdev.w3.org%2Fcsswg%2Fcss3-grid-align%2F&amp;ei=weFTT5GwKbGPigKm3sm0Bg&amp;usg=AFQjCNEH7KSiARjkdtGd1vgBuESld-hUYg">grid layout</a>, we are pretty much stuck with the HTML flow, and thus should rearrange boxes while respecting their source order. So we go down our list, and based on the minimum width values, we create various combinations. The values below show widths at which we rearrange the layout, styling rows as columns, or changing the width of a specific column.

#### 470px

*   header
*   Main
*   Complementary
*   Aside (250) + Contentinfo (220)

#### 530px

*   header
*   Main
*   Complementary (280) + Aside (250)
*   Contentinfo

#### 700px

*   header
*   Main (420) + Complementary (280)
*   Aside
*   Contentinfo

or:

*   header
*   Main (420) + Complementary (280)
*   Aside + Contentinfo

#### 950px

*   Main (420) + Complementary (280) + Aside (250)
*   Contentinfo

#### 1170px

*   Main (420) + Complementary (280) + Aside (250) + Contentinfo (220)

#### 1190px

*   Main (420) + Complementary (280) + Aside (490)
*   Contentinfo

#### 1410px

*   Head (240) Main (420) + Complementary (280) + Aside (250) + Contentinfo (220)

All of the above are potential breakpoints — each value could be used to create different layouts for the page. But is that something we <em>should</em> automatically do? I think not. At least not without considering these two points:

<strong>How close are the breakpoints?</strong>
We have 2 that are 20 pixels apart (1170px and 1190px); should we set both of them or should we drop one? I think that above 900px, chances are that desktop users may easily trigger a re-flow in that range, so I would not implement both. In other words, I think it's okay to go with close breakpoints if the values are below 800px — as there is less chance to confuse users when they resize their browser window.

<strong>Should we try to create as many columns as we can?</strong>
Bringing more ads above the fold may make more sense than bringing up a list of links that you'd generally keep buried in your footer. Also, you may choose to give more breathing room to your main content before bringing up boxes that the user does not really care for.</p>

### Getting Ready for Media Queries

For the purpose of this article, we'll use every single one of our breakpoints to create a new layout, which should also demonstrate that it is not necessarily a good idea.

<pre><code class="language-css">/**
 * 470
 */
@media only screen and (min-width: 470px) and (max-width: 529px) {
    #aside {
        width: 250px;
        float: left;
    }
    #contentinfo {
        display: block;
        width: auto;
        overflow: hidden;
    }
}

/**
 * 530
 */
@media only screen and (min-width: 530px) and (max-width: 699px) {
    #wrapper {
        display:block;
        margin: auto;
        max-width: 550px; /* see comment below */
    }
    #complementary {
        -webkit-box-sizing: border-box;
        -moz-box-sizing: border-box;
        box-sizing: border-box;
        padding-right: 250px;
        margin-right: -250px;
    }
    #aside {
        width: 250px;
    }
}

/**
 * 700
 */
@media only screen and (min-width: 700px) and (max-width: 949px) {
    #wrapper {
        display:block;
        margin: auto;
        max-width: 830px; /* see comment below */
    }
    #main {
        float: left;
        -webkit-box-sizing: border-box;
        -moz-box-sizing: border-box;
        box-sizing: border-box;
        padding-right: 280px;
        margin-right: -280px;
        height: 300px;
    }
    #aside,
    #complementary {
        float: right;
        width: 280px;
    }
    #contentinfo {
        clear: both;
    }
}

/**
 * 950
 */
@media only screen and (min-width: 950px) and (max-width: 1169px) {
    #wrapper {
        display:block;
        -webkit-box-sizing: border-box;
        -moz-box-sizing: border-box;
        box-sizing: border-box;
        padding-right: 250px;
        margin: auto;
    }
    #main {
        width: 60%;
    }
    #complementary {
        width: 40%;
    }
    #aside {
        width: 250px;
        margin-right: -250px;
    }
}

/**
 * 1170
 */
@media only screen and (min-width: 1170px) and (max-width: 1189px) {

    #main,
    #complementary,
    #aside,
    #contentinfo {
        float: left; /* display:inline here leads to rounding errors */
    }
    #main {
        width: 36%;
    }
    #complementary {
        width: 24%;
    }
    #aside {
        width: 21%;
    }
    #contentinfo {
        width: 19%;
    }
}

/**
 * 1190
 */
@media only screen and (min-width: 1190px) and (max-width: 1409px) {
    #wrapper {
        display:block;
        box-sizing: border-box;
        padding-right: 490px;
        margin: auto;
    }
    #main {
        width: 60%;
    }
    #complementary {
        width: 40%;
    }
    #aside {
        width: 490px;
        margin-right: -490px;
    }
}

/**
 * 1410
 */
@media only screen and (min-width: 1410px) {
    body {
        max-width: 1740px;
    }
    #wrapper {
        float: left;
        -webkit-box-sizing: border-box;
        -moz-box-sizing: border-box;
        box-sizing: border-box;
        width:100%;
        padding-left: 17%;
        padding-right: 16%;
        margin-right: -16%;
        border-right: solid 250px transparent;
    }
    #header {
        float: left;
        width:17%;
        margin-right: -17%;
    }
    #main {
        width: 60%;
    }
    #complementary {
        width: 40%;
    }
    #aside {
        width: 250px;
        margin-right: -250px;
    }
    #contentinfo {
        width: 16%;
    }
}</code></pre>

For the 530px and 700px breakpoints, there is a design choice to make. Without a max-width, we'd get everything flush, but the main box (<code>#main</code>) would be larger than the maximum width we originally set.</p>

## Demo

Please feel free to check out the <a href="https://www.css-101.org/articles/responsive_design/demos/demo.html">demo</a> of this technique.

The last thing to do is to create a layout to cater for IE6/7/8, as these browsers will ignore the media queries. To do so, we can use a Conditional Comment:

<pre><code class="language-css">&lt;!--[if lt IE 9]&gt;
    &lt;style&gt;
    body {
        margin: auto;
        min-width: 850px;
        max-width: 1000px;
        _width: 900px;
    }
    #main {
        width: 55%;
    }
    #complementary {
        width: 25%;
        *margin-right: -1px; /* rounding error */
    }
    #aside {
        width: 20%;
    }
    #contentinfo {
        clear:both;
    }
    &lt;/style&gt;
&lt;![endif]--&gt;</code></pre>

## Conclusion

Not once in this article I referenced the width of a device, be it an iPad, a Xoom, or something else. Building a "content-aware grid" is a simple matter of choosing the "<a href="https://www.lukew.com/ff/entry.asp?1514">layout patterns</a>" that you want, based on breakpoints that you set according to page content.

After I sent this piece to Smashing Magazine, I ran into <a href="https://www.tangledindesign.com/blog/deciding-what-responsive-breakpoints-to-use/">Deciding What Responsive Breakpoints To Use</a> by @Stephen_Greig. So obviously, we are at least two who share the sentiment that relying on devices to create layouts is the wrong approach. But I'm curious to know what everyone else is doing, or even thinking? If we had more people pushing for this, the community could be less device-centric, and could start focusing on content again.</p>

### Next Step: Responsive Media

*   [Polyfilling picture without the overhead](https://www.w3.org/community/respimg/2012/03/15/polyfilling-picture-without-the-overhead/)
*   [Experimenting with Context-Aware Image Sizing](https://filamentgroup.com/lab/responsive_images_experimenting_with_context_aware_image_sizing/)
*   [Responsive Design Guidelines](https://www.smashingmagazine.com/responsive-web-design-guidelines-tutorials/) on Smashing Magazine

### Footnotes

[1] According to [Ideal line length for content](https://www.maxdesign.com.au/articles/em/) this box should be styled width a min-width of 25em and a max-width of 33em. So if your base font-size is 16px (as [it should be](https://www.smashingmagazine.com/2011/10/07/16-pixels-body-copy-anything-less-costly-mistake/)), this translates as 400 pixels and 528 pixels.

<em>(jvb) (il) (vf)</em>


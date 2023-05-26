---
title: 'Progressively Enhancing CSS Layout: From Floats To Flexbox To Grid'
slug: enhancing-css-layout-floats-flexbox-grid
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/632a6339-4fc2-4298-a94c-bb4c4179deea/holy-grid-pptwcu-c-scale-w-1050.png
date: 2017-07-24T14:03:03.000Z
author: manuelmatuzovic
summary: >-
  Take a look on CSS grid layout for making websites with a demo to see different levels of enhancement. Manuel Matuzović explains how floating, flexbox and grid work inviting to provide an accesible and usable experience for various browsers. Integrate progressive enhancement so you can build resilient websites!
description: >-
  In this article, Manuel Matuzović explains how floating, flexbox and grid work inviting to provide an accesible and usable experience for various browsers. Integrate progressive enhancement so you can build resilient websites!
categories:
  - Coding
  - CSS
  - Tutorials
  - CSS Grid
---

I’d like to share with you the statements and questions I’ve heard in the last few weeks:

*   “When can I start using CSS grid layout?”
*   “Too bad that it’ll take some more years before we can use grid in production.”
*   “Do I need Modernizr in order to make websites with CSS grid layout?”
*   “If I wanted to use grid today, I’d have to build two to three versions of my website.”
*   “Progressive enhancement sounds great in theory, but I don’t think it’s possible to implement in real projects.”
*   “How much does progressive enhancement cost?”

These are all good questions, and not all of them are easy to answer, but I’m happy to share my approach. The CSS grid layout module is one of the most exciting developments since responsive design. We should try to get the best out of it as soon as possible, if it makes sense for us and our projects.

## Demo: Progressively Enhanced Layout

Before going into detail and expounding my thoughts on the questions and statements above, I want to present a little [demo](https://s.codepen.io/matuzo/debug/Emddvx) I’ve made.

**Disclaimer**: *It would be best to open the demo on a device with a large screen. You won’t see anything of significance on a smartphone.*

<figure><a href="https://s.codepen.io/matuzo/debug/Emddvx"><img
sizes="(max-width: 2834px) 100vw, 2834px"
srcset="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/168db4c7-41e6-49ee-b434-2ae671615d4a/holy-grid-pptwcu-c-scale-w-200.png 200w, https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/632a6339-4fc2-4298-a94c-bb4c4179deea/holy-grid-pptwcu-c-scale-w-1050.png 1050w, https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61353ebc-3fc9-45e2-b597-cca06b8c7fff/holy-grid-pptwcu-c-scale-w-1574.png 1574w, https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99af676f-8f37-482a-941a-bcaafebec1cf/holy-grid-pptwcu-c-scale-w-2004.png 2004w, https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/005943b3-a4e8-420e-bbb1-619fe448af60/holy-grid-pptwcu-c-scale-w-2437.png 2437w"
src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/632a6339-4fc2-4298-a94c-bb4c4179deea/holy-grid-pptwcu-c-scale-w-1050.png"
alt="Progressively enhanced CSS Layout, with Flexbox and CSS Grid."></a><figcaption>The home page of an example website, with an adjustable slider to switch between different layout techniques.</figcaption></figure>

When you open the demo, you’ll find yourself on the home page of a website with a very basic layout. You can adjust the slider in the top left to enhance the experience. The layout switches from being very basic to being a float-based layout to being a flexbox layout and, finally, to being one that uses grid.

It’s not the most beautiful or complex design, but it’s good enough to demonstrate which shapes a website can take based on a browser’s capabilities.

This demo page is built with CSS grid layout and **doesn’t use any prefixed properties or polyfills**. It’s accessible and usable for users in Internet Explorer (IE) 8, Opera Mini in Extreme mode, UC Browser and, of course, the most popular modern browsers. You can perfectly use CSS grid layout today if you don’t expect exactly the same appearance in every single browser, which isn’t possible to achieve nowadays anyway. I’m well aware that this decision isn’t always up to us developers, but I believe that our clients are willing to accept those differences if they understand the benefits (future-proof design, better accessibility and better performance). On top of that, I believe that our clients and users have &mdash; thanks to responsive design &mdash; already learned that websites don’t look the same in every device and browser.

In the following sections, I’m going to show you how I built parts of the demo and why some things just work out of the box.

**Quick side note**: *I had to add a few lines of JavaScript and CSS (an HTML5 shim) in order to make the page work in IE 8. I couldn’t resist, because IE 8+ just sounds more impressive than IE 9+.*

{{% feature-panel %}}

## CSS Grid Layout And Progressive Enhancement

Let’s take a deeper look at how I built the "**four levels of enhancement**” component in the center of the page.

### HTML

I started off by putting all items into a `section` in a logical order. The first item in the section is the heading, followed by four subsections. Assuming that they represent separate blog posts, I wrapped each of them in an `article` tag. Each article consists of a heading (`h3`) and a linked image. I used the `picture` element here because I want to serve users with a different image if the viewport is wide enough. Here, we already have the first example of good ol’ progressive enhancement in action. If the browser doesn’t understand `picture` and `source`, it will still show the `img`, which is also a child of the `picture` element.

<pre><code class="language-markup">&lt;section&gt;
  &lt;h2&gt;Four levels of enhancement&lt;/h2&gt;
  &lt;article&gt;&lt;h3&gt;No Positioning&lt;/h3&gt;&lt;a href="#"&gt;  &lt;picture&gt;    &lt;source srcset="320_480.jpg" media="(min-width: 600px)"&gt;    &lt;img src="480_320.jpg" alt="image description"&gt;  &lt;/picture&gt;&lt;/a&gt;
  &lt;/article&gt;
&lt;/section&gt;
</code></pre>

### Float Enhancements

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94683811-5a48-4002-a554-a366cd9f86ed/component-float-800w-opt.jpg" alt="A component of the demo page built with float" /><figcaption>All items in the “four levels of enhancement” component, floated left.</figcaption></figure>

On larger screens, this component works best if all items are laid out next to each other. In order to achieve that for browsers that don’t understand flexbox or grid, I float them, give them a size and some margin, and clear the floating after the last floated item.

<pre><code class="language-css">article {
  float: left;
  width: 24.25%;
}

article:not(:last-child) {
  margin-right: 1%;
}

section:after {
  clear: both;
  content: "";
  display: table;
}
</code></pre>

## Flexbox Enhancements

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a829b244-64b3-4f39-9d09-e11337f99898/component-flex-800w-opt.jpg" alt="A component of the demo page built with flexbox" /><figcaption>All items in the “four levels of enhancement” enhanced with flexbox.</figcaption></figure>

In this example, I actually don’t need to enhance the general layout of the component with flexbox, because floating already does what I need. In the design, the headings are below the images, which is something that’s achievable with flexbox.

<pre><code class="language-css">article {
  display: flex;
  flex-direction: column;
}

h3 {
  order: 1;
}
</code></pre>

We have to be very cautious when reordering items with flexbox. We should use it only for visual changes, and make sure that reordering doesn’t change the user experience for keyboard or screen-reader users for the worse.

{{% ad-panel-leaderboard %}}

## Grid Enhancements

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fef98c71-b0a6-49e4-8afa-52c9050fcda2/component-grid-800w-opt.jpg" alt="A component of the demo page built with grid" /><figcaption>All items in the “four levels of enhancement” enhanced with CSS grid.</figcaption></figure>

Everything looks pretty good now, but the heading still needs some positioning. There are many ways to position the heading right above the second item. The easiest and most flexible way I found is to use CSS grid layout.

First, I drew a four-column grid, with a 20-pixel gutter on the parent container.

<pre><code class="language-css">section {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 20px;
}
</code></pre>

Because all articles still have a width of `24.25%`, I reset this property for browsers that understand grid.

<pre><code class="language-css">@supports(display: grid) {
  article {width: auto;
  }
}
</code></pre>

Then, I put the heading in the first row and second column.

<pre><code class="language-css">h2 {
  grid-row: 1;
  grid-column: 2;
}
</code></pre>

To work against grid’s auto-placement, I also put the second `article` explicitly in the second row and second column (below the heading).

<pre><code class="language-css">article:nth-of-type(2) {
  grid-column: 2;
  grid-row: 2 / span 2;
}
</code></pre>

Finally, in order for the gap between the heading and the second item to be removed, all the other items have to span two rows.

<pre><code class="language-css">article {
  grid-row: span 2;
}
</code></pre>

That’s it. You can [see the final layout on Codepen](https://codepen.io/matuzo/pen/PjYKXW?editors=1100).

If I extract the extra lines that I need to make this thing work in IE 9+, then we’ll get a total of eight lines (three of which are actually for the clearfix and are reusable). Compare that to the overhead you get when you use prefixes.

<pre><code class="language-css">article {
  float: left;
  width: 24.25%;
}

@supports(display: grid) {
  article {width: auto;
  }
}

section:after {
  clear: both;
  content: "";
  display: table;
}
</code></pre>

I know that that’s just a simple example and not a complete project, and I know that a website has way more complex components. However, imagine how much more time it would take to build a layout that would look pixel-perfectly the same across all the various browsers.

## You Don’t Have To Overwrite Everything

In the preceding example, `width` was the only property that had to be reset. One of the great things about grid (and flexbox, too, by the way) is that certain properties lose their power if they’re applied to a flex or grid item. `float`, for example, has no effect if the element it’s applied to is within a grid container. That’s the same for some other properties:

*   `display: inline-block`
*   `display: table-cell`
*   `vertical-align`
*   `column-*` properties

Check “[Grid ‘Fallbacks’ and Overrides](https://rachelandrew.co.uk/css/cheatsheets/grid-fallbacks)” by amazing [Rachel Andrew](https://rachelandrew.co.uk) for more details.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89b0a8a6-546a-4fc8-b6c3-a371a27c481d/caniuse-featurequeries-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69cf1af2-a2c2-4431-95d7-6055f9112b08/caniuse-featurequeries-800w-opt.png" alt="Table showing the browser support of CSS Feature Queries" /></a><figcaption>CSS feature queries are supported in every major browser. (Image: <a href="https://caniuse.com/">Can I Use</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89b0a8a6-546a-4fc8-b6c3-a371a27c481d/caniuse-featurequeries-large-opt.png">Large preview</a>)</figcaption></figure>

If you do have to overwrite properties, use [feature queries](https://hacks.mozilla.org/2016/08/using-feature-queries-in-css/). In most cases, you’ll only need them to overwrite properties such as `width` or `margin`. [Support for feature queries](https://caniuse.com/#feat=css-featurequeries) is really good, and the best part is that they’re supported by every browser that understands grid as well. You don’t need [Modernizr](https://modernizr.com/) for that.

Also, you don’t have to put all grid properties in a feature query, because older browsers will simply [ignore properties and values they don’t understand](https://www.w3.org/TR/css-syntax-3/).

The only time when it got a little tricky for me while working on the demo was when there was a flex or grid container with a clearfix applied to it. [Pseudo-elements with content become flex or grid items as well](https://codepen.io/matuzo/pen/mmQxEx). It may or may not affect you; just be aware of it. As an alternative, you can clear the parent with `overflow: hidden`, if that works for you.

## Measuring The Costs Of Progressive Enhancement

Browsers already do a lot of progressive enhancement for us. I already mentioned the `picture` element, which falls back to the `img` element. Another example is the `email` input field, which falls back to a simple `text` input field if the browser doesn’t understand it. Another example is the range slider that I’m using in the demo. In most browsers, it’s rendered as an adjustable slider. The input type `range` isn’t supported in IE 9, for example, but it’s still usable because it falls back to a simple `input` field. The user has to enter the correct values manually, which isn’t as convenient, but it works.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df2fc528-977e-444f-b85c-99f0a9e55c4d/slider-preview-opt.jpg" alt="Range input type comparison in Chrome and IE 9" /><figcaption>Comparison of how the <code>range</code> input type is rendered in Chrome and IE 9.</figcaption></figure>

{{% ad-panel-leaderboard %}}

### Some Things Are Taken Care of by the Browser, Others by Us

While preparing the demo, I came to the realization that it’s incredibly helpful to really understand CSS, instead of just throwing properties at the browser and hoping for the best. The better you understand how floating, flexbox and grid work and the more you know about browsers, the easier it’ll be for you to progressively enhance.

<blockquote>
<p>Becoming someone who understands CSS, rather than someone who just uses CSS, will give you a huge advantage in your work.

<p><a href="https://rachelandrew.co.uk/archives/2017/05/24/a-very-good-time-to-understand-css-layout/">Rachel Andrew</a>
</blockquote>

Also, if progressive enhancement is already deeply integrated into your process of making websites, then it would be difficult to say how much extra it costs, because, well, that’s just how you make websites. Aaron Gustafson shares a few stories of some projects he has worked on in his post “[The True Cost of Progressive Enhancement](https://medium.com/@AaronGustafson/the-true-cost-of-progressive-enhancement-d395b6502979)” and on the [Relative Paths podcast](https://www.relativepaths.uk/ep48-progressive-enhancement-with-aaron-gustafson/). I highly recommend that you listen to and read about his experiences.

### Resilient Web Development

<blockquote>
<p>“Your website’s only as strong as the weakest device you’ve tested it on.”<br /><br />&mdash; <a href="https://ethanmarcotte.com/wrote/left-to-our-own-devices/">Ethan Marcotte</a>
</blockquote>

Progressive enhancement might involve some work in the beginning, but it can save you time and money in the long run. We don’t know which devices, operating systems or browsers our users will be using next to access our websites. If we provide an accessible and usable experience for less capable browsers, then we’re building products that are resilient and better prepared for new and [unexpected developments](https://www.theverge.com/2017/2/26/14742150/nokia-3310-mwc-2017).

<div class="c-felix-the-cat">
<h4 class="h3">Building Production-Ready CSS Grid Layouts Today</h4>
<p>CSS Grid is the new layout standard for the web. Let’s start using CSS Grids and Flexbox in production websites today! <a href="https://www.smashingmagazine.com/2017/06/building-production-ready-css-grid-layout/" class="btn btn--medium btn--blue">Read a related article â†’</a>
</div>

## Summary

I have the feeling that some of us forget what our job is all about and maybe even forget that what we’re actually doing is “just“ a job. We’re not rock stars, ninjas, artisans or gurus, and what we do is ultimately about putting content online for people to consume as easily as possible.

<blockquote>
<p>Content is the reason we create websites.

<p><a href="https://alistapart.com/article/understandingprogressiveenhancement">Aaron Gustafson</a>
</blockquote>

That sounds boring, I know, but it doesn’t have to be. We can use the hottest cutting-edge technologies and fancy techniques, as long as we don’t forget who we are making websites for: users. Our users aren’t all the same, nor do they use the same device, OS, browser, Internet provider or input device. By providing a basic experience to begin with, we can get the best out of the modern web without compromising accessibility.

<figure><a href="https://caniuse.com/#search=grid"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30a24676-7230-45e8-bb2e-31570e230d5e/caniuse-grid-800w-opt.png" alt="Table showing the browser support of CSS grid layout" /></a><figcaption>CSS grid layout is supported in almost every major browser. (Image: <a href="https://caniuse.com/">Can I Use</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea7cb1ad-746d-4382-8690-253b3c895dd5/caniuse-grid-large-opt.png">Large preview</a>)</figcaption></figure>

Grid, for example, is [available in almost every major browser](https://caniuse.com/#search=grid), and we shouldn’t wait more years still until coverage is 100% in order to use it in production, because it’ll never be there. That’s just not how the web works.

[Grid is awesome](https://gridbyexample.com/examples/). Use it now!

### Screenshots

Here are some screenshots of the demo page in various browsers:

- [Internet Explorer 8, Windows 7](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c528beb9-597e-4354-916e-6042672f6c10/ie8-win7-large-opt.png)
- [Internet Explorer 9, Windows 7](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd1a5429-35dc-4b25-8860-4cf3d2ff947c/ie9-win7-large-opt.png)
- [Internet Explorer 10, Windows 7](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54391307-d600-4f1c-bf1d-3a3cebc7cbfc/ie10-win7-large-opt.png)
- [Internet Explorer 11, Windows 8](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdefcb94-e3a4-48ab-a079-1bbfdaac5cc4/ie11-win8-large-opt.png)
- [Opera Mini 42 (Extreme), Android 7](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1dfb2007-ec54-4dc6-8bac-3487e0b5c172/opera-mini-large-opt.png)
- [UC Browser 11, Android 7](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c79cba61-af66-4d95-9d79-529b7fe9397f/uc-browser-large-opt.png)

### Resources and Further Reading

*   [Crippling the Web](https://timkadlec.com/2013/07/crippling-the-web/), Tim Kadlec
*   [Browser Support for Evergreen Websites](https://rachelandrew.co.uk/archives/2017/01/12/browser-support-for-evergreen-websites/), Rachel Andrew
*   [The Experimental Layout Lab of Jen Simmons](https://labs.jensimmons.com/) (demos), Jen Simmons
*   [World Wide Web, Not Wealthy Western Web, Part 1](https://www.smashingmagazine.com/2017/03/world-wide-web-not-wealthy-western-web-part-1/), Bruce Lawson
*   [Resilience](https://www.youtube.com/watch?v=W7wj7EDrSko) (video), Jeremy Keith, View Source conference 2016

*Thanks to my mentor Aaron Gustafson for helping me with this article, to Eva Lettner for proofreading and to Rachel Andrew for her countless posts, demos and talks.*

{{< signature "al, il, mrn" >}}

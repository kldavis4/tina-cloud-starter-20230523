---
title: 'New CSS Features In 2022'
slug: new-css-features-2022
author: michelle-barker
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14419af2-69ab-4150-8cf3-bca2cd2291ad/new-css-features-2022.jpg
date: 2022-03-01T13:00:00.000Z
summary: >-
   2022 is shaping up to be a pretty great year for CSS, with a plethora of new features on the horizon. Some are already starting to land in browsers, others are likely to gain widespread browser support in 2022, while for one or two the process may be a little longer. In this article we’ll take a look at a few of them.
description: >-
  2022 is shaping up to be a pretty great year for CSS, with a plethora of new features on the horizon. Some are already starting to land in browsers, others are likely to gain widespread browser support in 2022, while for one or two the process may be a little longer. In this article we’ll take a look at a few of them.
categories:
  - CSS
  - Browsers
  - Guides
---

Container queries enable us to style an element depending on the size of its parent &mdash; a crucial difference from media queries, which only query the viewport. This has long been a problem for responsive design, as often we want a component to adapt to its context.

Think of a card which might be shown in a wide content area or a narrow sidebar. We’d probably want to show something more akin to the card’s mobile layout in the sidebar, while perhaps showing style when there is sufficient horizontal space. But media queries aren’t aware of the component’s context. For this reason, container queries have been on many a developer’s wish list for some time.

## Container Queries

### How Do We Use Them?

For a container query, we need to specify an element as our container, using the `container` property (shorthand for `container-type` and `container-name`). The `container-type` can be `width`, `height`, `inline-size` or `block-size`. `inline-size` and `block-size` are [logical properties](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties), which may produce different results according to the document’s [writing mode](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Writing_Modes).

<pre><code class="language-css">main, aside {
    container: inline-size;
}</code></pre>

Then we can use the `@container` at-rule in a way that’s similar to a media query. Note the different way the rule can be expressed within the brackets (`inline-size > 30em` rather than `min-width: 30em`). This is part of the [Media Queries Level 4 specification](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries#syntax_improvements_in_level_4). For the card layout example above, when the container is wider than 30rem we switch to a horizontal layout using flexbox:

<pre><code class="language-css">@container (inline-size > 30em) {
    .card {
        display: flex;
    }
}</code></pre>

The [CSS Containment Level 3 specification](https://www.w3.org/TR/css-contain-3/) is currently in working draft, which means the syntax could change at any point &mdash; in fact, it’s changed since some articles on container queries were published on it last year. The examples here are in line with the proposed syntax at the time of writing.

### Can I Use Them?

Chrome claims to support container queries behind a flag, but the working implementation doesn’t appear to be consistent with the current spec. There’s [a polyfill](https://css-tricks.com/a-new-container-query-polyfill-that-just-works/), but it doesn’t work with the latest syntax. So the short answer is “no”, I would definitely urge you to wait a while before using them in production. But there’s a lot of momentum behind container queries, so I would expect more general support soon.

### Resources

- [CSS Containment Module Level 3](https://www.w3.org/TR/css-contain-3) (official specification)
- [A Primer on Container Queries](https://www.smashingmagazine.com/2021/05/complete-guide-css-container-queries/) by Stephanie Eckles
- [CSS Container Queries: A First Look](https://www.bram.us/2021/03/28/css-container-queries-a-first-look-and-demo/) by Bramus Van Damme
- [Say Hello to Container Queries](https://ishadeed.com/article/say-hello-to-css-container-queries/) by Ahmad Shadeed (The syntax referred to in this post is now outdated, but it still contains some good examples.)

## `:has()`

### What Is It?

Often known as the “parent selector”, this pseudo-class enables us to select an element depending on its descendants. As Bramus Van Damme [wrote last year](https://www.bram.us/2021/12/21/the-css-has-selector-is-way-more-than-a-parent-selector/), it has some pretty interesting use cases beyond that. For instance, we could style an image differently in a `<figure>`depending on whether or not it’s accompanied by a `<figcaption>`. Or we could target labels in a form that are followed by invalid inputs. The possibilities are endless.

### How Do We Use It?

To style `<section>` elements that contain an `<h2>`:

<pre><code class="language-css">section:has(h2) {
    background: lightgray;
}</code></pre>

To style an `<img>`, only if its parent `<section>` also contains an `<h2>`:

<pre><code class="language-css">section:has(h2) img {
    border: 5px solid lime;
}</code></pre>

### Can I Use It?

No mainstream browser support yet, but you can play with it to your heart’s content in [Safari Technology Preview](https://developer.apple.com/safari/technology-preview/). Check out [this demo](https://codepen.io/michellebarker/pen/poWpWOz) in supporting browsers.

### Resources

- [CSS Selectors Level 4](https://www.w3.org/TR/selectors-4/) (official specification)
- [The CSS :has() selector is way more than a “Parent Selector”](https://www.bram.us/2021/12/21/the-css-has-selector-is-way-more-than-a-parent-selector/) by Bramus van Damme
- [The CSS :has() selector](https://css-tricks.com/the-css-has-selector/) by Robin Rendle (CSS Tricks)

{{% feature-panel %}}

## `@when/@else`

### What Is It?

An at-rule for conditionals in CSS, similar to if/else logic in other programming languages. It could make writing complex media queries far more logical, for example. `@when` was chosen instead of `@if` to avoid conflict with Sass.

### How Do We Use It?

We can query for multiple media conditions or supported features, such as whether a user’s viewport is over a certain width *and* their browser supports subgrid. When using `@when/@else`, we drop the `@` from the query rule:

<div class="break-out">

<pre><code class="language-css">@when media(min-width: 30em) and supports(display: subgrid) {
    /* Styles for viewports over 30em, where the browser also supports subgrid */
} @else {
    /* Styles for browsers that do not meet the condition */
}</code></pre>
</div>

### Can I Use It?

Not yet. It’s *very* early days, and still under discussion. I wouldn’t expect browser support to be widely rolled out this year, but it’s definitely one to watch.

### Resources

- [CSS Conditional Rules Module Level 5](https://www.w3.org/TR/css-conditional-5) (official specification)
- [Extending CSS when/else chains: A first look](https://blog.logrocket.com/extending-css-when-else-chains-first-look/) by Kingsley Ubah (LogRocket blog)
- [Proposal for CSS @when](https://css-tricks.com/proposal-for-css-when/) by Chris Coyier (CSS Tricks)

{{% ad-panel-leaderboard %}}

## `accent-color`

### What Is It?

The `accent-color` property makes it quick and easy to roll out our brand colors to certain form inputs by leveraging user agent styles. Think checkboxes, radio buttons, range inputs and progress bars. Historically, these are kind of a pain to style, and all browsers render them slightly differently. As developers the go-to option, more often than not, is hiding the default input and [rolling our own using pseudo-elements](https://moderncss.dev/pure-css-custom-styled-radio-buttons/). `accent-color` enables us to keep the browser’s default input, but apply a color to fit with our brand.

### How Do We Use It?

Usage is simple, and the property is inherited, so you can set it at the root level to apply it everywhere:

<pre><code class="language-css">:root {
    accent-color: lime;
}</code></pre>

Or on individual elements:

<pre><code class="language-css">form {
    accent-color: lime;
}

input[type="checkbox"] {
    accent-color: hotpink;
}</code></pre>

### Can I Use It?

Yes! `accent-color` is supported in Chrome, Edge, Firefox and Safari Technology Preview. Browsers that don’t support it will simply get the default colors, and the inputs will remain perfectly usable &mdash; great for progressive enhancement.

### Resources

- [CSS Basic User Interface Module Level 4](https://www.w3.org/TR/css-ui-4/) (official specification)
- “[CSS accent-color](https://web.dev/accent-color/)”, Adam Argyle
- “[Simplifying Form Styles With accent-color](https://www.smashingmagazine.com/2021/09/simplifying-form-styles-accent-color/)”, Michelle Barker

## New CSS Color Functions

### What Are They?

You might already be familiar with Hex, RGB and HSL color formats. The CSS Color Module Levels [4](https://www.w3.org/TR/css-color-4) and [5](https://www.w3.org/TR/css-color-5) include a whole host of new color functions that enable us to specify and manipulate colors in CSS like never before. They include:

- `hwb()`: Hue, Whiteness, Blackness.
- `lab()`: Lightness, along with *a* and *b* values, which determine the hue.
- `lch()`: Lightness, Chroma, Hue.
- `color-mix()`: Mix two colors together.
- `color-contrast()`: From a list of colors, output the one with the highest contrast compared to the first argument.
- `color()`: Specify a color in a different color space (e.g.`display-p3`).

There’s *a lot* to dig into this illuminating subject — I wrote [an article all about](https://www.smashingmagazine.com/2021/11/guide-modern-css-colors/) it last year.
Added to that, there’s also [relative color syntax](https://www.w3.org/TR/css-color-5/#relative-colors), which lets us take a color and tweak it to make another.

### How Do We Use It?

`hwb()`, `lab()` and `lch()` can be used much in the same way as the `rgb()` and `hsl()` functions we’re accustomed to, with an optional *alpha* parameter:

<div class="break-out">

<pre><code class="language-javascript">.my-element {
  background-color: lch(80% 100 50); // opaque color
}

.my-element {
  background-color: lch(80% 100 50 / 0.5); // color with 50% transparency
}</code></pre>
</div>

`color-mix()` outputs a color as a result of mixing two others. We need to specify a color interpolation method as the first argument:

<pre><code class="language-css">.my-element {
  background-color: color-mix(in lch, blue, lime);
}</code></pre>

`color-contrast()` requires a base color with which to compare the others. It will output the color with the highest contrast, or in the case where an additional keyword is provided, the first color in the list that meets the corresponding contrast ratio:

<div class="break-out">

<pre><code class="language-css">/&#42; Output the color with the highest contrast &#42;/
.my-element {
    color: white;
    background-color: color-contrast(white vs, lightblue, lime, blue);
}

/&#42; Output the first color that meets AA contrast ratio &#42;/
.my-element {
    color: white;
    background-color: color-contrast(white vs, lightblue, lime, blue to AA);
}</code></pre>
</div>

This is great for accessible color schemes. For example, we can let our CSS select whether black or white text is most suitable (i.e. provides the most contrast) for a button with a given background color.

### Can I Use Them?

Safari is leading the way on browser support right now, with `hwb()`, `lch()`, `lab()`, and `color()` all supported since version 15. `color-mix()` and `color-contrast()` can be enabled with a flag. Firefox supports `hwb()`, and also has flagged support for `color-mix()` and `color-contrast()`. The surprising outlier is Chrome, which doesn’t support any of these right now. However, it’s not too hard to provide fallbacks in your code: Given two color rules, the browser will ignore the second one if it doesn’t support it.

<pre><code class="language-css">.my-element {
    background-color: rgb(84.08% 0% 77.36%);
    background-color: lch(50% 100 331);
}</code></pre>

It means that when support does come in, your code will be ready.

### Resources

- [CSS Color Module Level 4](https://www.w3.org/TR/css-color-4/) (official specification)
- [CSS Color Module Level 5](https://www.w3.org/TR/css-color-5) (official specification)
- [A Guide To Modern CSS Colors With RGB, HSL, HWB, LAB And LCH](https://www.smashingmagazine.com/2021/11/guide-modern-css-colors/) by Michelle Barker
- [LCH colors in CSS: what, why, and how?](https://lea.verou.me/2020/04/lch-colors-in-css-what-why-and-how/) by Lea Verou
- [LCH color picker](https://css.land/lch/) by Lea Verou
- [Create a color theme with CSS Relative Color Syntax, CSS color-mix(), and CSS color-contrast()](https://www.bram.us/2021/04/28/create-a-color-theme-with-css-relative-color-syntax-css-color-mix-and-css-color-contrast/) by Bramus van Damme

## Cascade Layers

### What Are They?

Cascade Layers give us more power to manage the “cascading” part of CSS. Currently, there are several factors that determine which styles will be applied in your CSS code, including selector specificity and order of appearance. Cascade layers allow us to effectively group our CSS into chunks (or “layers”, if you will). Code within a layer lower down in the order will take precedence over code in a higher layer, even if a selector in the higher layer has higher specificity. If all of this is a little hard to wrap your head around, Miriam Suzanne has written a [comprehensive guide for CSS-Tricks](https://css-tricks.com/css-cascade-layers/#browser-support-and-fallbacks).

I like to think of it as kind of like `z-index` for the cascade. If you understand how `z-index` works, you’ll probably grasp cascade layers pretty quickly.

### How Do I Use Them?

As Bramus explains in his tutorial, you could create discrete layers consistent with the ITCSS methodology.

<pre><code class="language-css">/* Create the layers, in the desired order */
@layer reset, base, theme;

/* Append the CSS to each of the layers */
@layer reset {
  /* Append to 'reset' layer */
}

@layer base {
  /* Append to 'base' layer */
  h1.title {
      font-size: 5rem;
  }
}

@layer theme {
  /* Append to 'theme' layer */
  h1 {
      font-size: 3rem;
  }
}</code></pre>

The CSS `font-size` declaration for `h1` in the `theme` layer would win over the one in `base`, despite the latter having a higher specificity.

### Can I Use Them?

Cascade Layers are supported in the latest version of Firefox, and can be enabled with a flag in Chrome and Edge (with full support coming to Chrome in version 99). It looks like all the major browsers are getting on board with this specification, so expect more widespread support soon. So you can absolutely start playing with Cascade Layers right away, but it might be some time before we can confidently use them in production. It’s difficult to see how to easily provide fallbacks to older browsers without including a separate stylesheet, or perhaps polyfills will emerge in time. Miriam Suzanne has some thoughts in [this explainer](https://css.oddbird.net/layers/explainer/).

### Resources

- [CSS Cascading and Inheritance Level 5](https://www.w3.org/TR/css-cascade-5/) (official specification)
- [A Complete Guide to CSS Cascade Layers](https://css-tricks.com/css-cascade-layers/) by Miriam Suzanne (CSS Tricks)
- [Cascade Layers are Coming to Your Browser](https://developer.chrome.com/blog/cascade-layers/) by Una Kravets (Chrome developer blog)
- [The Future of CSS: Cascade Layers (CSS @layer)](https://www.bram.us/2021/09/15/the-future-of-css-cascade-layers-css-at-layer/#more-notes--important) by Bramus van Damme
- [Getting Started With CSS Cascade Layers](https://www.smashingmagazine.com/2022/01/introduction-css-cascade-layers/) by Stephanie Eckles

{{% ad-panel-leaderboard %}}

## Subgrid

### What Is It?

When CSS Grid was first being talked about years ago, many developers thought it would enable us to lay out every part of our UI on a single grid, just like the typical 12-column layouts we receive from designers. In practice, that would involve completely flattening your markup, breaking semantics — not recommended! Part of the CSS Grid Layout Module 2 specification, subgrid enables an element to inherit the grid of its parent, either on the row or column axis.
In theory, you could nest grids all the way down, aligning every component to the same grid. In reality, we probably don’t need to do this as often as we thought, as we (hopefully) embrace more flexible, intrinsic web design that priorities content, UX and accessibility over rigid adherence to a grid. But subgrid is still incredibly useful for solving all sorts of UI challenges.

For instance, take this row of images with captions. The captions are varying lengths, but using subgrid we can have them all line up with each other, without coding a fixed height.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5ce2781-9f44-4488-9483-629fc2694bc1/1-new-css-features-2022.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5ce2781-9f44-4488-9483-629fc2694bc1/1-new-css-features-2022.png" width="800" height="275" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5ce2781-9f44-4488-9483-629fc2694bc1/1-new-css-features-2022.png'>Large preview</a>)" alt="Three images of birds with captions which vary by length" >}}

### How Do We Use It?

Specify the grid of the parent element using Grid’s regular properties. Use the keyword `subgrid` for the `grid-template-columns` or `grid-template-rows` property on the nested item that you want to inherit the parent grid:

<pre><code class="language-css">.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(2, auto);
}

.grid > figure {
    display: grid;
    grid-template-rows: subgrid;
}

.grid figcaption {
    grid-row: 2;
}</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="YzERyor" default_tab="result" breakout="true" user="michellebarker" editable="true" data-editable="true" >}}See the Pen [Subgrid captions](https://codepen.io/michellebarker/pen/YzERyor) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

### Can I Use It?

Remarkably, subgrid has been supported in Firefox since 2019, yet no other browser has followed suit nearly three years later. There are indications that the Chromium team are finally getting around to implementing it, so we might be lucky enough to see it land in Chrome and Edge this year. ([Keep track of the issue here](https://bugs.chromium.org/p/chromium/issues/detail?id=618969).) I’m less hopeful for Safari support, but with Jen Simmons spearheading the CSS effort over at Apple, anything’s possible. There’s nothing to stop you using subgrid in production, but it’s best to treat it as progressive enhancement for now.

### Resources

- [CSS Grid Layout Module Level 2](https://www.w3.org/TR/css-grid-2/) (official specification)
- [MDN Subgrid page](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Subgrid)
- “[CSS Grid Level 2: Here Comes Subgrid](https://www.smashingmagazine.com/2018/07/css-grid-2/)”, Rachel Andrew

## Scroll Timeline

### What Is It?

You’ve probably seen a lot of cool websites that implement fancy scroll-linked animations. There are plenty of JS libraries to help us implement this kind of thing &mdash; I’m a big fan of [Greensock]’s ScrollTrigger plugin. Imagine if we could do all of that within CSS? With `@scroll-timeline` we can!

### How Do We Use It?

We need a few things:

- a keyframe animation,
- the `@scroll-timeline` at-rule,
- the `animation-timeline` property on the element we’re animating (or specify the timeline in the shorthand `animation` property).

Here’s an example:

<div class="break-out">

<pre><code class="language-css">/&#42; Set up keyframe animation &#42;/
@keyframes slide {
    to { transform: translateX(calc(100vw - 2rem)); }
}

/&#42; Configure our scroll timeline. Here we're giving it the name `slide-timeline` &#42;/
@scroll-timeline slide-timeline {
  source: auto; /&#42; the scrollable element that triggers the scroll-linked animation (the document by default) &#42;/
  orientation: vertical; /&#42; the scroll orientation (vertical by default) &#42;/
  scroll-offsets: 0%, 100%; /&#42; an array of progress intervals in which the timeline is active &#42;/
}

/&#42; Specify the keyframe animation and the scroll timeline &#42;/
.animated-element {
  animation: 1s linear forwards slide slide-timeline;
}</code></pre>
</div>

We can alternatively use element-based offsets for the `scroll-offsets` property, to trigger the timeline when a particular element scrolls into view:

<div class="break-out">

<pre><code class="language-css">@scroll-timeline slide-timeline {
    scroll-offsets: selector(#element) end 0, selector(#element) start 1;
}</code></pre>
</div>

Once again, Bramus has us covered with a [comprehensive introduction](https://css-tricks.com/practical-use-cases-for-scroll-linked-animations-in-css-with-scroll-timelines/) and some great use cases.

### Can I Use It?

If you’re interested in playing around with `@scroll-timeline` it can be enabled with a flag in Chrome. The specification is in editor’s draft, so there’s a good chance it might change before it gets recommended status.

There are likely to be cases that necessitate reaching for a JS library for scroll-based animation (think managing complex animation timelines). But for relatively simple cases, this could save on a whole lot of unnecessary imports.

### Resources

- [Scroll-linked Animations](https://drafts.csswg.org/scroll-animations-1/) (official specification)
- [MDN page](https://developer.mozilla.org/en-US/docs/Web/CSS/@scroll-timeline)
- “[Practical Use Cases for Scroll-Linked Animations in CSS with Scroll Timelines](https://css-tricks.com/practical-use-cases-for-scroll-linked-animations-in-css-with-scroll-timelines/)”, Bramus Van Damme

## Nesting

### What Is It?

If you’re familiar with Sass, you’ll know the convenience of being able to nest selectors — essentially, writing a child rule inside a parent. Nesting helps us to keep our code organised &mdash; although if over-used can sometimes be a hindrance! Now it looks like nesting is finally coming to native CSS.

### How Do We Use It?

Syntactically it’s similar to Sass, so shouldn’t feel like too much of a leap. The nested rule here targets a h2 inside an element with a class of `card`:

<pre><code class="language-css">.card {
    color: red;

    & h2 {
        color: blue;
    }
}</code></pre>

Or we can use it for pseudo-classes and pseudo-elements:

<pre><code class="language-css">.link {
    color: red;

    &:hover,
    &:focus {
        color: blue;
    }
}</code></pre>

The equivalent in today’s CSS would be:

<pre><code class="language-css">.link {
    color: red;
}

.link:hover,
.link:focus {
    color: blue;
}</code></pre>

### Can I Use It?

Not natively. No browsers yet support it, even behind a flag. But if you use PostCSS, you can try it out with the `postcss-preset-env` plugin.

### Resources

- [CSS Nesting Module](https://www.w3.org/TR/css-nesting-1/)
- “[CSS Nesting, specificity and you](https://kilianvalkhof.com/2021/css-html/css-nesting-specificity-and-you/)”, Killian Valkhof

## The Future of CSS

It’s fair to say that we’re in a booming era for CSS right now. As I write this, I notice that many of these new features have some things in common. Yes, they often help us write better, cleaner and more efficient code. Some draw upon the features of preprocessing tools (like Sass), rendering these tools less of a necessity as time goes on. But they also allow us &mdash; even encourage us &mdash; to embrace the inherent flexibility of the web, and be considerate of the many different ways that our users might be browsing. Today’s users might be using any one of the millions of different devices available. They might prefer higher contrast, a dark color scheme, or reduced motion. They might use a screenreader, an older device, or a mixture of all of the above. 

Rather than being prescriptive with our designs, and lamenting an unattainable “pixel-perfection”, we can use CSS to give hints and suggestions, and let the browser decide how best to display our webpage. These ideas have been summarised by Jen Simmons and Una Kravets (among others), who have coined the terms “[Intrinsic](https://noti.st/jensimmons/h0XWcf/everything-you-know-about-web-design-just-changed)” web design and “[New responsive](https://web.dev/new-responsive/)” web design respectively. 

CSS appears to be reaching a level of maturity where the challenge is no longer whether something **can** be done in CSS, but rather training and arming a new generation of developers to understand the tools we have at our disposal, know **when** to reach for them, and how to make user-centered development decisions.

{{< signature "vf, yk, il" >}}

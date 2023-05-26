---
title: 'The Flexbox Reading List: Techniques And Tools'
slug: the-flexbox-reading-list
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a58846d7-988f-4ce6-9ad5-d2d62205ae06/flexbox.png'
date: 2016-02-23T23:58:01.000Z
author: cosima-mielke
description: >-
  Flexbox gives us a new kind of control over our
  [layouts](https://www.smashingmagazine.com/2015/08/flexible-future-for-web-design-with-flexbox/),
  making coding challenges that were hard or impossible to solve with CSS alone
  straightforward and intuitive. It provides us with the means to build **grids
  that are flexible** and aware of [dynamic
  content](https://www.smashingmagazine.com/2016/02/design-mock-ups-need-dynamic-content-tools-plugins/),
  and thus, give us the freedom to focus on the creation process instead of
  hacking our way towards a layout.

  To give you a head start into Flexbox and provide you with ideas on how to use
  it to master common coding challenges, we have collected **tips, tricks, and
  tools** that help you get the most out of its power already today. The list is
  by no means complete but includes the resources which we found helpful and
  useful.
categories:
  - Coding
  - CSS
  - Flexbox
---
Flexbox gives us a new kind of control over our [layouts](https://www.smashingmagazine.com/2015/08/flexible-future-for-web-design-with-flexbox/ "Flexbox Is As Easy As Pie – Designing CSS Layouts"), making coding challenges that were hard or impossible to solve with CSS alone straightforward and intuitive. It provides us with the means to build **grids that are flexible** and aware of [dynamic content](https://www.smashingmagazine.com/2016/02/design-mock-ups-need-dynamic-content-tools-plugins/), and thus, give us the freedom to focus on the creation process instead of hacking our way towards a layout.

To give you a head start into Flexbox and provide you with ideas on how to use it to master common coding challenges, we have collected **tips, tricks, and tools** that help you get the most out of its power already today. The list is by no means complete but includes the resources which we found helpful and useful.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Designing Layouts with Flexbox](https://www.smashingmagazine.com/2015/08/flexible-future-for-web-design-with-flexbox/)
*   [Horizontal And Vertical Centering with CSS and Flexbox](https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/)
*   [Quantity Queries wit CSS and Flexbox](https://www.smashingmagazine.com/2015/07/quantity-ordering-with-css/)
*   [User Interface Modules (Dropdowns, Sticky Footers etc.)](https://www.smashingmagazine.com/2015/11/flexbox-interfaces-tracks-case-study/)
*   [Flexbox Modules for Web Apps](https://www.smashingmagazine.com/2015/03/harnessing-flexbox-for-todays-web-apps/)

## Getting Started

### Using Flexbox Today

A great primer on the power of Flexbox and how to make use of it, is Chris Wright’s article “[Using Flexbox Today](https://chriswrightdesign.com/experiments/using-flexbox-today/).” As Chris points out, there is a distinct gap between what we build today and how we’ll approach tomorrow. So to get more people to use Flexbox today, he outlines a strategy for adding its value to your projects and provides examples of how to enhance current layouts with Flexbox, among them card layouts, split screen layouts, pinned layouts, newspaper and ad units, multi-column layouts as well as dashboards.

{{% feature-panel %}}

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e5cb0e9-1eaf-47dc-b987-1a5389764be9/flexbox-guardian-opt.png" alt="Flexbox in use on The Guardian’s site" width="500" height="335" /><figcaption>Flexbox out in the wild on the Guardian’s newspaper and ad units. One of the examples in <a href="https://chriswrightdesign.com/experiments/using-flexbox-today/">Chris Wright’s post about Flexbox</a>. (Image credit: <a href="https://chriswrightdesign.com/experiments/using-flexbox-today/">Chris Wright</a>)</figcaption></figure>

### Learn Flexbox The Fun Way

Honestly, despite (or because of?) its grand potential, Flexbox can be quite daunting if you are just about to get started. A fun way to grasp its properties and elements is [Flexbox Froggy](https://flexboxfroggy.com/), a browser game that teaches you the Flexbox basics by using it to guide a little frog to its lilypad.</p>

## Practical Tips And Tricks

You’ve wrapped your head around the [Flexbox basics](https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/) and are ready to dive deeper? The following resources provide practical solutions for common coding challenges.</p>

### Solved By Flexbox

Think of all those things that CSS hackers have tried to solve for years: the Holy Grail Layout, full-width fluid input pairs, media objects that get by without any overflow, clearfixing or block formatting hacks, footers that stick to the bottom even of sparsely contented pages, [vertical centering](https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/#example-horizontal-and-vertical-centering-or-the-holy-grail-of-web-design) — well, Flexbox solves all of these, for good and without any hacks. Philipp Walton has compiled a [showcase of these challenges and their Flexbox solutions](https://philipwalton.github.io/solved-by-flexbox/). Great to keep on hand for your next project.</p>

### Creating Finessed Grids

At the heart of Flexbox is its ability to produce wrappable grids that are tolerant of [dynamic content](https://www.smashingmagazine.com/2016/02/design-mock-ups-need-dynamic-content-tools-plugins/). You can use basic wrapping techniques to [distribute children automatically in a grid](https://www.heydonworks.com/article/flexbox-grid-finesse#basic-wrapping), and thus, cater for a decent layout no matter the number of children. [Element queries](https://www.smashingmagazine.com/2013/06/media-queries-are-not-the-answer-element-query-polyfill/#the-element-query) help make your grids entirely responsive with [children expanding to hit a minimal width](https://www.heydonworks.com/article/flexbox-grid-finesse#element-queries), and the possibility to reshuffle the elements in the grid guarantees that a [grid never ends with a single element row](https://www.heydonworks.com/article/flexbox-grid-finesse#dealing-with-remainders-of-1).</p>

### Flexbox And Quantity Queries

Aaron Gustafson experimented with [Flexbox and quantity queries](https://www.smashingmagazine.com/2015/07/quantity-ordering-with-css/#quantity-queries) to come up with a [flexible grid layout with visual enhancements](https://www.aaron-gustafson.com/notebook/playing-with-flexbox-and-quantity-queries/). In Aaron’s case, the grid layout flexes to highlight one to two of his upcoming speaking appearances and allows others to flow in at the default grid size. Also a nice idea for a portfolio page or recent blog posts, for example.</p>

<figure><a href="https://www.aaron-gustafson.com/notebook/playing-with-flexbox-and-quantity-queries/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b6ed25c-d3df-4671-a837-f363e9703ffe/grids-opt-500.png" width="500" height="242" alt="Aaron Gustafson’s flexible grid layout" /></a><figcaption>Aaron Gustafson’s flexible grid layout in action. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dd55af6-4d43-49c6-a70b-a1d0a589facc/grids-opt.png">View the large version</a>.</figcaption></figure>

### Alignment Shifting Wrapping

Imagine the following problem: You have a main title and a subtitle sitting on the same line. You want the main title to be left-, the subtitle right-aligned, and the subtitle should wrap under the main title when there is not enough space.</p>

<figure><a href="https://css-tricks.com/useful-flexbox-technique-alignment-shifting-wrapping/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01d3272a-f902-4052-a753-31ddf56b8402/wrapping-opt-500.png" width="500" height="349" alt="Alignment Shifting Wrapping" /></a><figcaption>More often than not, alignment issues are easy to solve with Flexbox. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ca5fb4d-ef3f-4f07-a406-821867854c85/wrapping-opt.png">View the large version</a>.</figcaption></figure>

That’s the situation Chris Coyier ran into. His [alignment shifting wrapping technique](https://css-tricks.com/useful-flexbox-technique-alignment-shifting-wrapping/) solves the problem by giving the title a flex-container with `display:flex;` and the title itself `flex-grow: 1;`, so the subtitle is pushed to the right. And since flex-containers can wrap, it only takes a `flex-wrap: wrap;` to make the subtitle behave as intended on small screens. One of those moments where Flexbox excels at making something hard incredibly simple. Also applicable to other responsive design challenges.</p>

### Overriding `justify-content`

One of Flexbox’s best-kept secrets is probably how to override `justify-content` to position a flex-item independently along the main axis. The solution: [auto margins](https://medium.com/@samserif/flexbox-s-best-kept-secret-bd3d892826b6#.byxqvyhah)! They aren’t new to CSS, of course, but in combination with Flexbox they unveil an entirely new power. When applied to a flex item, the item will automatically extend its specified margin to occupy the extra space in the flex container depending on the direction in which the auto-margin is applied.</p>

### Re-Imagining UI Patterns With Flexbox

That the power of Flexbox goes beyond common layouting tasks, shows an [experiment by Zell Liew](https://zellwk.com/blog/star-rating). He used Flexbox to re-imagine a UI pattern which you’ll find everywhere: the star rating element. His Flexbox version gets by with only 50 lines of code and five stars in SVG and was brought to life using a combination of the sibling selector `~`, the `flex-flow` property and `row-reverse`. Nifty!

[Flexbox Patterns](https://www.flexboxpatterns.com/home) by CJ Cenizal also shows ways of using the power of Flexbox to build UI components. It provides interactive examples and the source code you’ll need to get started with stepper inputs, tabs, form footers, centered prompts, sidebars and more.</p>

## Tools And Further Resources

### Calculating The Width of Flex Items

If calculating the width of flex items gives you headaches, then [Flexbox Tester](https://madebymike.com.au/demos/flexbox-tester/) is for you. Just enter values for `flex-grow`, `flex-shrink` and `flex-basis` for three flex items to see how they behave.</p>

### Dealing With Bugs And Workarounds

Like any technique, Flexbox isn’t free of bugs, of course. For those moments when you run into one, [Flexbugs](https://github.com/philipwalton/flexbugs) is bound to cater for a fix. The community-curated list of Flexbox issues is regularly updated to provide solutions and browser workarounds. If you discover a bug that’s not listed yet, you can report it via GitHub. Speaking of browser workarounds: The [Flexibility polyfill](https://github.com/10up/flexibility) provides a fix for older versions of Internet Explorer that don’t support Flexbox. It detects flex-affected elements on the page and restyles them accordingly in IE 8 and 9.

You have something to add to the list? Let us know about your favorite Flexbox resources in the comments section below.

{{< signature "cm" >}}


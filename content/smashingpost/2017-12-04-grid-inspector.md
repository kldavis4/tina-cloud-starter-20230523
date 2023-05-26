---
title: Debugging CSS Grid Layouts With Firefox Grid Inspector
author: huijing-chen
slug: grid-inspector
image: >-
  https://www.smashingmagazine.com/wp-content/uploads/2017/11/can-i-use-import-data-500w-opt.png
date: 2017-12-04T14:56:33+01:00
summary: >-
  This article covers known and obscure features of Firefox DevTools that can come in handy when you're building and debugging shiny new CSS Grid layouts.
description: >-
  Whether you're starting to learn about CSS Grid or already use it in production, Firefox's Grid Inspector is very useful. This article covers known and obscure features of Firefox DevTools that can come in handy when you're building and debugging CSS Grid layouts.
categories:
  - CSS
  - CSS Grid
  - Browsers
  - Testing
  - Debugging
---
You may have heard quite a bit of talk about a CSS feature called "Grid" this year. If you are someone who cringes when you hear the words "CSS" and "grid" in the same sentence, then I highly suggest you check out this new CSS module called CSS Grid.

Browsers render HTML elements as boxes according to the CSS box model, and CSS Grid is a new layout model that provides authors the ability to control the size and position of these boxes and their contents. The module introduces a series of properties that allow us to create grid structures and <strong>control the placement and sizing of grid items using CSS</strong>.

As [Rachel Andrew](https://rachelandrew.co.uk/) has said many times before, “Grid works from the container in“ while “Other layout methods start with the item.” This way of thinking about Grid really stuck with me because I'm used to designing directly in the browser. Before the advent of CSS Grid, it was expected that every HTML element was to be rendered one after another, and that was the mental model I'd settled upon.

After playing around with Grid for a bit, I realized my approach to designing layouts had changed. I found myself sketching on paper, thinking about the layout design in its entirety. By the time my fingers were doing their dance across the keyboard, I already knew exactly how my layout would look like.

One of the things I had to wrap my head around was the fact that the grid we define on the grid container is not visible. You can apply borders to your grid items, but you cannot apply a border to your grid lines to see them. This is when a DevTools function like Grid Inspector comes in really handy.

{{% feature-panel %}}

## Brief History Of Grid Inspector

I had first heard of a Grid Inspector tool when [Jen Simmons](https://jensimmons.com/) 
 [tweeted about it](https://twitter.com/jensimmons/status/775992991253204992) back in September 2016, but the team at Mozilla had already been discussing the [development of a Grid Inspector tool](https://bugzilla.mozilla.org/show_bug.cgi?id=1181227) since July 2015. [Matt Claypotch](https://mozillians.org/en-US/u/potch/) and Jen Simmons had worked on a Firefox add-on called the [CSS Grid Inspector](https://addons.mozilla.org/nn-NO/firefox/addon/css-grid-inspector/), which was released in April 2016. It gave the team some working code build upon, as well as a means of gathering feedback from a larger base of developers.

Although other browsers like Chrome and Internet Explorer each had their respective Grid implementations at the time, with Chrome's behind a flag, and Internet Explorer using the original specification, Firefox was the only browser that was working on a Grid DevTool along with the Grid implementation itself.

The in-depth discussions by the team at Mozilla regarding the Grid Inspector tool covered features like having different colors for different grids on the same page, detection of grid gaps, display of line numbers, and so on. This is a significant reason why the Grid Inspector tool in Firefox has so many advanced features in the latest Nightly (58.0a1, at time of writing), and was one of the features the team had been thinking about and worked on for more than a year.

They have collectively been implemented into a stand-alone Layout panel, which also includes a rendering of the Box Model of a selected HTML element plus the CSS properties related to Box Model. This article will cover these useful features and how they can help when troubleshooting grids.</p>

## Overview Of The Layout Panel

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61841416-5446-4263-9c5c-cae10d27356d/layout-panel-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b623435f-a9a0-4af2-b9a5-00189697f4a7/layout-panel-800w-opt.png" width="800" height="451" alt="Firefox DevTools layout panel"/></a><figcaption>Firefox DevTools layout panel (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61841416-5446-4263-9c5c-cae10d27356d/layout-panel-large-opt.png">Large preview</a>)</figcaption></figure>

### Overlay Grid

The first section you will see in the layout panel is **Overlay Grid**, which will show you all the elements on the page with `display: grid` applied. You will be able to turn on the grid overlay on each grid by checking their respective checkbox. For now, only one grid overlay can be displayed at any one time, but having multiple grid overlays is [a feature on the roadmap](https://bugzilla.mozilla.org/show_bug.cgi?id=1317102).</p>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/018ad8f0-28e6-4961-882b-6b002aafe40e/name-tooltip.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/018ad8f0-28e6-4961-882b-6b002aafe40e/name-tooltip.gif" width="600" height="321" alt="Toggle grid overlay"/></a><figcaption>Toggle grid overlay (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/018ad8f0-28e6-4961-882b-6b002aafe40e/name-tooltip.gif">Large preview</a>)</figcaption></figure>

Every additional grid will have a different color from the default purple, but you are free to change the colors of your grid overlays by clicking on the colored circle on the right of each grid element. The grid overlay will show all the grid tracks and grid gaps of the selected grid.</p>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d38b35ff-af60-479e-ba7e-e63cf9798c23/grid-colour-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d38b35ff-af60-479e-ba7e-e63cf9798c23/grid-colour-opt.png" width="800" height="454" alt="Customize grid overlay color"/></a><figcaption>Customize grid overlay color (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d38b35ff-af60-479e-ba7e-e63cf9798c23/grid-colour-opt.png">Large preview</a>)</figcaption></figure>

Once you select a grid, a rendering of the selected grid will appear in the space below in the color of the grid overlay. This rendering will show you each section of the grid you defined and hovering over any section will highlight its corresponding area on the actual page. There will also be a tool-tip that shows you the line number of the row and column of the highlighted grid item.</p>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b1ebc23-af32-4109-8d52-b0c1fac373ff/area-highlight.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b1ebc23-af32-4109-8d52-b0c1fac373ff/area-highlight.gif" width="600" height="324" alt="Visual highlighting tool"/></a><figcaption>Visual highlighting tool (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b1ebc23-af32-4109-8d52-b0c1fac373ff/area-highlight.gif">Large preview</a>)</figcaption></figure>

Most of us would be in the _Rules_ panel when examining the CSS on our site, and you can toggle the grid overlay from there as well. Select the element which has `display: grid` applied to it, and click on the waffle-like icon on the property. The options for display of line numbers or grid area names that have been set on the _Layout Panel_ will be respected when the grid overlay is toggled in this manner.

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac31ebd3-06ac-4e7c-ad2f-8667e3f38776/waffle-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e86b78d-f9a9-4428-a1b1-7645ec3684cb/waffle-800w-opt.png" width="800" height="434" alt="Toggle Grid overlay via Rules panel"/></a><figcaption>Toggle Grid overlay via Rules panel (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac31ebd3-06ac-4e7c-ad2f-8667e3f38776/waffle-large-opt.png">Large preview</a>)</figcaption></figure>

### Grid Display Settings

The next section on the panel is the **Grid Display Settings**, which allows us to toggle three options for now. The display of _line numbers_, the display of _area names_ and the option to _extend grid lines_ indefinitely.

The basic premise of how Grid works is that you first define a grid, then proceed to place your grid items within that grid. You can either place those grid items manually or let the browser do it for you. The position of the grid items depends on their `grid-row` and `grid-column` values. Grid lines are referred to by their numerical index which starts from 1.</p>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/046701eb-7642-4302-b8b5-77eebc6d5834/grid-overlay.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/046701eb-7642-4302-b8b5-77eebc6d5834/grid-overlay.gif" width="600" height="323" alt="Toggle line numbers"/></a><figcaption>Toggle line numbers (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/046701eb-7642-4302-b8b5-77eebc6d5834/grid-overlay.gif">Large preview</a>)</figcaption></figure>

Once _Display line numbers_ is active, the selected grid overlay will display the line numbers of the grid in the color of each respective grid overlay. Each grid has their own numerical grid index which starts from 1, different grids will not share the same numerical grid index.</p>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4276e69-2868-4a57-9b6a-33cfd0d5e784/cutoff1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56023254-f2a2-4ae4-8b74-67a415e1dc3f/cutoff1-800w-opt.png" width="800" height="531" alt="Line numbers cut off at the top edge"/></a><figcaption>Line numbers cut off at the top edge (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4276e69-2868-4a57-9b6a-33cfd0d5e784/cutoff1-large-opt.png">Large preview</a>)</figcaption></figure>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2a30dd2-fddc-4666-a89c-6bb3b7ebb946/cutoff2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d5d7f3c-8103-415d-a6f2-80fcab66fbb8/cutoff2-800w-opt.png" width="800" height="531" alt="Line numbers cut off at the side edge"/></a><figcaption>Line numbers cut off at the side edge (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2a30dd2-fddc-4666-a89c-6bb3b7ebb946/cutoff2-large-opt.png">Large preview</a>)</figcaption></figure>

If your grid extends the width or height of the viewport, you will notice that the line numbers get cut off at the edges. The Mozilla team is aware of this issue and it is being tracked under [Bug 1396666](https://bugzilla.mozilla.org/show_bug.cgi?id=1396666).

You can also define a grid using the `grid-template-areas` property, which gives us the ability to name the areas on our grids. The syntax for this property also provides a visualization of the grid structure in the CSS itself, making it easier to understand the layout of the grid from your code.</p>

<p class="no-margin">Take the following block of CSS for example:</p>

<pre class="language-css"><code>.subgrid1 {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-auto-rows: 5em;
  grid-template-areas: "apple banana pear"
                       "grape watermelon pineapple"
                       "strawberry peach kiwi"
}</code></pre>

This creates a 3 by 3 grid and each section is named according to how they are laid out in the `grid-template-areas` property. If the sections are named, they will be displayed as a second tool-tip when you hover over the rendering of the grid in the layout panel.</p>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/018ad8f0-28e6-4961-882b-6b002aafe40e/name-tooltip.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/018ad8f0-28e6-4961-882b-6b002aafe40e/name-tooltip.gif" width="600" height="321" alt="Grid area name tool-tip"/></a><figcaption>Grid area name tool-tip (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/018ad8f0-28e6-4961-882b-6b002aafe40e/name-tooltip.gif">Large preview</a>)</figcaption></figure>

We can also toggle the display of the grid area names on the grid overlay by checking that option in **Grid Display Settings**. According to Mozilla, this feature was inspired by [CSS Grid Template Builder](https://codepen.io/anthonydugois/full/RpYBmy), which was created by [Anthony Dugois](https://anthonydugois.com/).</p>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41ebab13-b262-4517-ad9c-f845f49cf70b/area-name.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41ebab13-b262-4517-ad9c-f845f49cf70b/area-name.gif" width="600" height="323" alt="Toggle grid area names"/></a><figcaption>Toggle grid area names (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41ebab13-b262-4517-ad9c-f845f49cf70b/area-name.gif">Large preview</a>)</figcaption></figure>

Fun fact. You can use emojis for grid area names and everything will work just fine.</p>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73a9983b-b8c5-40d2-b099-4da089efc08d/area-name-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22007de6-20dd-4e86-81fe-385ec0696458/area-name-800w-opt.png" width="800" height="434" alt="Emoji grid names"/></a><figcaption>Emoji grid names (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73a9983b-b8c5-40d2-b099-4da089efc08d/area-name-large-opt.png">Large preview</a>)</figcaption></figure>

The last option you can toggle is to extend grid lines indefinitely. By default, the grid lines on each grid are constrained to within the bounds of the grid container. But sometimes it can be useful to see how the grid aligns in the context of the entire page.</p>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fd6f005-18ad-4dcf-9773-fedf576f34d7/extend-lines.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fd6f005-18ad-4dcf-9773-fedf576f34d7/extend-lines.gif" width="600" height="324" alt="Extend grid lines indefinitely"/></a><figcaption>Extend grid lines indefinitely (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fd6f005-18ad-4dcf-9773-fedf576f34d7/extend-lines.gif">Large preview</a>)</figcaption></figure>

## A Better Box Model Tool

The Box Model section under the _Layout Panel_ shows a rendering of the dimensions of the selected element, its padding, borders, and margins. In addition to that, it also shows the CSS properties that affect the position, size and geometry of the selected element, namely `box-sizing`, `display`, `float`, `line-height`, `position`, and `z-index`. A convenience when it comes to troubleshooting layout-related CSS issues.

The computed value of the height and width of the selected element and its current positioning value is displayed below the box model outline. You can also directly manipulate the margins, borders, and paddings of the element from the diagram itself.</p>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b32f0e28-bb83-4bb1-a3e2-2d62d8719e49/box-model.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b32f0e28-bb83-4bb1-a3e2-2d62d8719e49/box-model.gif" width="600" height="324" alt="Tweak layout properties"/></a><figcaption>Tweak layout properties (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b32f0e28-bb83-4bb1-a3e2-2d62d8719e49/box-model.gif">Large preview</a>)</figcaption></figure>

If you use CSS lengths other than pixels, the DevTools will convert the values into pixels automatically based on the computed value, which is really nifty.</p>

## Grid Inspector Plays Well With Transforms

There are many instances where Grid will be used in combination with other CSS layout properties, like transforms, for example. The Grid Inspector tool plays well with CSS transforms and the grid overlay will adjust to it, however, the selected element has been transformed. You will be able to see how the Grid has been rotated, skewed, scaled or translated.</p>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/585195a7-0a8f-4905-8de5-5099d99dd86a/transforms.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/585195a7-0a8f-4905-8de5-5099d99dd86a/transforms.gif" width="600" height="323" alt="Grid Inspector and Transforms"/></a><figcaption>Grid Inspector and Transforms (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/585195a7-0a8f-4905-8de5-5099d99dd86a/transforms.gif">Large preview</a>)</figcaption></figure>

## Help Make The Grid Inspector Tool Better

As with any other browser feature, the Grid Inspector tool will inevitably have bugs as the team is hard at work adding new features and polishing existing ones. If you do encounter any such issues, please raise an issue at [Bugzilla](https://bugzilla.mozilla.org/), Mozilla's bug tracking tool.

The metabug, which tracks all Grid Inspector related issues, is [Bug 1181227](https://bugzilla.mozilla.org/show_bug.cgi?id=1181227). You can search for the term _Grid Inspector_ to see the list of related bugs as well.</p>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3adcb67-df5f-46c5-8c86-fec5f8fe2da5/bugzilla-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04abb6ee-250a-4551-979e-587acdb47641/bugzilla-800w-opt.png" width="800" height="394" alt="Grid Inspector bugs"/></a><figcaption>Grid Inspector bugs (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3adcb67-df5f-46c5-8c86-fec5f8fe2da5/bugzilla-large-opt.png">Large preview</a>)</figcaption></figure>

If you have any suggestions or feedback on the Grid Inspector tool or the Firefox DevTools in general, Mozilla is on [Discourse](https://discourse.mozilla.org/c/devtools). Or you can also tweet at [@FirefoxDevTools](https://twitter.com/FirefoxDevTools).</p>

## Resources

* [CSS Grid and Grid Inspector in Firefox](https://www.mozilla.org/en-US/developer/css-grid/)
* [CSS Grid Inspector: Examine grid layouts](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Examine_grid_layouts)
* [Powerful New Additions to the CSS Grid Inspector in Firefox Nightly](https://hacks.mozilla.org/2017/06/new-css-grid-layout-panel-in-firefox-nightly/)
* [The Firefox Grid Inspector, July 2017 edition](https://jensimmons.com/post/jul-26-2017/firefox-grid-inspector-july-2017-edition)

{{< signature "rb, ra, il" >}}


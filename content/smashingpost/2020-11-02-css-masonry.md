---
title: 'Native CSS Masonry Layout In CSS Grid'
slug: native-css-masonry-layout-css-grid
author: rachel-andrew
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bc43aa2-0d1c-4780-b5df-b0a022aa92fc/native-css-masonry-layout-css-grid.png
date: 2020-11-02T12:00:00.000Z
summary: >-
  There is now a specification for native CSS masonry layout, as part of the Grid Layout spec. In this article, Rachel Andrew explains how it works with the help of a couple of demos you can try out in Firefox Nightly.
description: >-
  There is now a specification for native CSS masonry layout, as part of the Grid Layout spec. In this article, Rachel Andrew explains how it works with the help of a couple of demos you can try out in Firefox Nightly.
evergreen: true
last-updated: 2020-11-02T13:00:00.000Z
updated-by: rachel-andrew
categories:
  - CSS
  - CSS Grid
  - Browsers
  - Guides
disable_panels: true
---

A [Level 3 of the CSS Grid specification](https://drafts.csswg.org/css-grid-3/) has been published as an Editor’s Draft, this level describes a way to do Masonry layout in CSS. In this article, I’ll explain the draft spec, with examples that you can try out in Firefox Nightly. While this is a feature you won’t be able to use in production right now, your feedback would be valuable to help make sure it serves the requirements that you have for this kind of layout. So let’s take a look.

## What Is A Masonry Layout?

A masonry layout is one where items are laid out one after the other in the inline direction. When they move onto the next line, items will move up into any gaps left by shorter items in the first line. It’s similar to a grid layout with auto-placement, but without sticking to a strict grid for the rows.

The most well-known example of masonry is on [Pinterest](https://www.pinterest.co.uk/), and you will sometimes hear people refer to the layout as a "Pinterest layout".

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e87678a-4d85-4e82-9574-259d8c7d41b6/pintrest.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e87678a-4d85-4e82-9574-259d8c7d41b6/pintrest.jpg" sizes="100vw" caption="Pintrest" alt="An example layout from the Pintrest website" >}}

There are a number of JavaScript tools to help you create this kind of layout, such as David DeSandro’s [Masonry plugin](https://masonry.desandro.com/).

## Can’t We Already Do This In CSS?

We can come close to a masonry layout in a couple of ways. The closest way to achieve the look of this type of layout is to use Multi-column Layout. In the example below, you see something which looks visually like a masonry layout. However, the order of the boxes runs down the columns. Therefore, if the first items have the highest priority (e.g. if this were search results), then the apparent _first_ items in the top row aren’t actually the ones that came back first.

{{< codepen breakout="true" height="476" theme_id="light" slug_hash="QWEmPvK" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/QWEmPvK">Masonry Multicol example</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

When designers first saw Grid layout, they often thought that auto-placement along with the dense packing mode might achieve masonry. While you can fill all of the gaps in this way, the layout is still a grid and therefore there is no way to cause items to rise up into the gaps left by shorter items.

{{< codepen breakout="true" height="476" theme_id="light" slug_hash="mdExgmZ" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/mdExgmZ">Masonry autoflow example</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Therefore, in order to achieve masonry, it still requires JavaScript. Doing layout with JavaScript &mdash; in particular with the large number of items that often benefit from this type of layout &mdash; is never going to perform well. I initially noted that web developers were asking for the feature [back in January 2017](https://github.com/w3c/csswg-drafts/issues/945), and while I have some concerns as to whether this really is a grid thing (and also the potential for accessibility problems due to content reordering), I am glad it is moving forward.

## The Masonry Feature Of Grid Layout

This is a new specification, so things may well change before this ships in more browsers. However, we are in a nice position in that there is already an implementation of Masonry in Firefox. Get a copy of Firefox Nightly, and enable the `layout.css.grid-template-masonry-value.enabled` flag in `about:config` to play with it. Once you have done that and returned to this page using Firefox, all the demos will work.

To use masonry layout, one of your grid axes needs to have the value `masonry`. This will then be referred to as the `masonry` axis, the other axis will have rows or column tracks defined as normal, this will be the grid axis. The CSS below creates a four-column grid, with the rows set to `masonry`. The masonry items will be displayed in the four columns of my grid axis.

<pre><code class="language-css">.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: masonry;
}
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef37005c-198f-4f82-87ab-a921df4b0879/pure-css-masonry.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef37005c-198f-4f82-87ab-a921df4b0879/pure-css-masonry.jpg" sizes="100vw" caption="Our Pure CSS Masonry Layout" alt="A simple masonry layout" >}}

That’s all you need to do to get a simple masonry layout. Using Firefox, you can see that in the CodePen example below.

{{< codepen breakout="true" height="476" theme_id="light" slug_hash="wvWmZWB" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/wvWmZWB">Basic CSS Masonry</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

We could stop there, however, adding masonry into CSS Grid means that we might expect some other grid things to work even when we are in a masonry layout. Therefore, the spec needs to define those things.

### Behavior On The Grid Axis

The axis which has defined tracks behaves in exactly the same way as a regular grid. Therefore you can size tracks, name lines, and use alignment in the same way that you would in a regular grid.

You can also position items using line-based placement on this axis. These will be placed first before the masonry items are placed. In the next example, I have placed the image with a caption of 5 between the line named `box-start` and the line named `box-end`. The masonry items are placed around it.

{{< codepen breakout="true" height="476" theme_id="light" slug_hash="PozRvZb" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/PozRvZb">Masonry with positioned item</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

It is also possible to span tracks as normal on the grid axis. In the next example, I have some elements that have a class of `landscape`. These items are spanning two column tracks when placed in the masonry layout.

{{< codepen breakout="true" height="476" theme_id="light" slug_hash="QWEmPMK" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/QWEmPMK">Masonry spanning example</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### The `masonry-auto-flow` property

The masonry specification adds some additional properties to Grid layout. The `masonry-auto-flow` property is not yet in the Firefox implementation. When implemented this property will give you control over the flow of items in the masonry layout.

Using `masonry-auto-flow: next` will place the item in the next location on the grid axis rather than packing it into the column with the most space as happens by default.

Using `masonry-auto-flow: ordered` will cause masonry to ignore items with a definite placement and lay the items out using **order-modified document order**; that is, in the order that they are in the document unless ordered with the `order` property.

{{% ad-panel-leaderboard %}}

### The `justify-tracks` and `align-tracks` properties

These properties work to some extent in Firefox Nightly at the time of writing. These are additional alignment properties for masonry layouts. If you have masonry in the block direction then you can use `align-tracks`, if you have masonry in the inline direction use `justify-tracks`.

If you have extra space in your grid container in the dimension being laid out using masonry, you will then discover that the items align to the start of the container. The initial value of `align-tracks` (in our case with masonry being created for rows) is `start`.

These properties work alongside `align-content` and `justify-content`. To show how, I have an example where the grid container has a height of 200vh. I have set the `align-tracks` value to `end`.

If `align-content` is `normal` (which it will be if I have not added the property), then the masonry tracks will end up at the end of the container.

{{< codepen breakout="true" height="476" theme_id="light" slug_hash="eYzMwPd" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/eYzMwPd">Masonry align-tracks</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

If I add `align-content: start`, the masonry tracks return to the start of the container. However, the “rough edges” of the layout are now at the top rather than the bottom because the masonry tracks are aligned to the end.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb742041-4654-4e45-8d85-2aee587ad6b7/align-tracks-content.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb742041-4654-4e45-8d85-2aee587ad6b7/align-tracks-content.jpg" sizes="100vw" caption="Aligning the masonry items to the end" alt="A simple masonry layout aligned to the end of the container" >}}

**Note**: *You can use any of the values used for `align-content` for `align-tracks` and `justify-tracks`. There are some nice examples in the spec of different combinations.*

If you set `align-tracks: stretch`, then any auto-sized items in the layout will stretch. The masonry effect is retained, but anything with a definite size on that axis will not be stretched out of shape.

{{< codepen breakout="true" height="476" theme_id="light" slug_hash="dyXmBre" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/dyXmBre">Masonry align-tracks: stretch</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

<p class="c-pre-sidenote--left">The <code>align-tracks</code> and <code>justify-tracks</code> properties can take multiple values. One for each track in the grid axis. This means that in our four-track grid we could have the first track stretching, the second aligned to start, the third aligned to end, and the fourth aligned to center. </p><p class="c-sidenote c-sidenote--right">This did not seem to work at the time of writing in Firefox.</p>

The spec details that if there are fewer values than tracks, the remaining tracks will use the final specified value. If there are more values than tracks, additional ones will be ignored.

### Fallback Behavior

The inclusion of this feature into the grid specification has a definite benefit where creating a fallback layout is concerned. As masonry behaves in a similar way to auto-placement, if a browser doesn’t support masonry then regular auto-placement can be used instead. This is likely to create the gaps in the layout as seen in the earlier example, but is certainly not terrible.

You can see this in action by looking at any of the demos so far using a browser with no support for masonry. You still get a layout. If you wanted to do something entirely different then you could check for support for masonry with feature queries. You could perhaps do the layout with multicol for non-supporting browsers.

<pre><code class="language-css">@supports (grid-template-rows: masonry) {
  /* masonry code here */
}
</code></pre>

If the masonry layout is vital then you could check for masonry support using [CSS.supports](https://developer.mozilla.org/en-US/docs/Web/API/CSS/supports) and only use the JavaScript masonry script if there is no support. This would mean that as browsers implement native masonry they would lose the overhead of the scripted version, but it would be there as a polyfill.

{{% ad-panel-leaderboard %}}

### Potential Accessibility Concerns

While masonry in CSS is exciting, it is yet another place where content reordering and a disconnection of the document order from the visual order may happen. [As I noted](https://github.com/w3c/csswg-drafts/issues/5675#issuecomment-718070949) on a recent issue that was raised, I feel that we are creating exciting layout possibilities and then needing to tell people to be very careful how they use them.

I’ve written about this problem in [Grid, content reordering, and accessibility](https://rachelandrew.co.uk/archives/2019/06/04/grid-content-re-ordering-and-accessibility/). I hope that as we move forward with this specification, there are also renewed efforts to find a good way forward with regard to content vs. display order.

## Your Feedback Is Needed

We are really lucky to not only have this new spec, but to have a browser implementation to test it in. If you have examples where you have used masonry, why not try replacing your JavaScript with the grid version and see if it works for you? If you run into problems or can’t do something you were able to do in your previous implementation, please let the CSSWG know by [raising an issue](https://github.com/w3c/csswg-drafts/issues/).

While things are in an experimental state, this is your chance to help influence any changes and point out any problems. So please do, and help make this really great feature even better!

{{< signature "il" >}}

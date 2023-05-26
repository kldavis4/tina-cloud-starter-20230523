---
title: 'CSS News July 2020'
slug: css-news-july-2020
author: rachel-andrew
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/512efbbb-1ef9-4eb4-8f34-9d5a0dcb3df9/css-news-july-2020.png
date: 2020-07-07T10:30:00.000Z
summary: >-
  In this article, Rachel Andrew takes a look at some of the interesting CSS features that are making their way into browsers right now.
description: >-
  In this article, Rachel Andrew takes a look at some of the interesting CSS features that are making their way into browsers right now.
categories:
  - CSS
  - Browsers
---

Things move a lot faster than they used to in terms of the implementation of Web Platform features, and this post is a round-up of news about CSS features that are making their way into the platform. If you are the sort of person who doesn’t like reading about things if you can’t use them _now_, then this article probably isn’t for you &mdash; we have many others for you to enjoy instead! However, if you like to know what is on the way and read more about the things you can play with in a beta version of a browser, read on!

## Flexbox Gaps

Let’s start with something that is implemented in the shipping version of one browser, and in beta in another. In CSS Grid, we can use the `gap`, `column-gap` and `row-gap` properties to define the gaps between rows and columns or both at the same time. The `column-gap` feature also appears in the [Multi-column layout](https://www.smashingmagazine.com/2019/01/css-multiple-column-layout-multicol/) to create gaps between columns.

While you can use margins to space out grid items, the nice thing about the `gap` feature is that you only get gaps _between_ your items; you do not end up with additional space to account for at the start and end of the grid. Adding margins has typically been how we have created space between flex items. To create a regular space between flex items, we use a margin. If we do not want a margin at the start and end, we have to use a negative margin on the container to remove it.

It would be really nice to have that gap feature in Flexbox as well, wouldn’t it? The good news is that we do have &mdash; it’s already implemented in Firefox and is in the Beta version of Chrome.

{{% feature-panel %}}

In the next CodePen, you can see all three options. The first are flex items using margins on each side. This creates a gap at the start and end of the flex container. The second uses a negative margin on the flex container to pull that margin outside of the border. The third dispenses with margins altogether and instead uses `gap: 20px`, creating a gap between items but not on the start and end edge.

{{< codepen breakout="true" height="476" theme_id="light" slug_hash="GRoOOGm" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/GRoOOGm">Flex Items with margins and negative margin, and the gap feature</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### Mind The Gap

The Flexbox `gap` implementation highlights a few interesting things. Firstly, you may well remember that when the gap feature was first introduced to Grid Layout, the properties were:

- `grid-gap`
- `grid-row-gap`
- `grid-column-gap`

These properties were shipped when grid first appeared in browsers. However, in much the same way as the alignment features (`justify-content`, `align-content`, `align-items`, and so on) first appeared in Flexbox and then became available to Grid (once it was decided the gap features were useful to more than grid), they were moved and renamed.

Along with those alignment features, the gap properties are now in the Box Alignment specification. The specification deals with alignment and space distribution so is a natural home for them. To prevent us from having multiple properties prefixed with a spec name, they were also renamed to drop the `grid-` prefix.

If you have the `grid-` prefixed versions in your code, you don’t need to worry. They have been kept as an alias of the properties so your code won’t break. For new projects, however, the unprefixed versions are implemented in all browsers.

### Detecting Gap Support For Flexbox

You might be thinking that you could use the gap feature in Flexbox and use Feature Queries to test for support by using a margin as fallback. Sadly, this isn’t the case because feature queries test for a name and value. For example, if I want to test for grid support, I can use the following query:

<pre><code class="language-css">@supports (display: grid) {
  .grid {
    /* grid layout code here */
  }
}
</code></pre>

If I were to test for `gap: 20px`, however, I would get a positive response in Chrome which currently does not support gap in Flexbox but _does_ support it in Grid. All those feature queries do is check to see if the browser recognizes the property and value. They have no way to test for support within a particular layout mode. I raised this as [an issue](https://github.com/w3c/csswg-drafts/issues/3559) in the CSS WG, however, it turns out to not be an easy thing to fix, and there are limited places currently where we have this partial implementation problem.

## Aspect Ratio Unit

Some things have an aspect ratio that we want to preserve, and image or a video for example. If you place an image or video directly on the page using the HTML `img` or `video` element, then it nicely keeps the aspect ratio it arrives with (unless you forcibly change the width or height). However, we sometimes want to add an element with no intrinsic aspect ratio while making one dimension flexible with the other retaining a specific aspect ratio. This most often happens when we embed a video with an iframe, however, you might also want to make perfectly square areas on your grid (something which also requires that one dimension can react to another).

The way we currently deal with this is by way of the [padding hack](https://css-tricks.com/aspect-ratio-boxes/). This uses the fact that padding in the block direction is copied from the inline direction when we use a percentage. It’s a not very elegant solution to the problem, but it works.

The aspect ratio unit seeks to solve that by allowing us to specify an aspect ratio for a length. Chrome has implemented this in Canary, so you can take a look at the demo below using Canary if you enable the *Experimental Web Platform Features* flag.

I have created a grid layout and set my grid items to use a `1 / 1` aspect ratio. The width of the items is determined by their grid column track size (as is flexible). The height is then being copied from that to make a square. Just for fun, I then rotated the items.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0ce6091-4840-44f4-a09d-31009a7bf7ed/smashing-grid-aspect-ratio.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0ce6091-4840-44f4-a09d-31009a7bf7ed/smashing-grid-aspect-ratio.png" sizes="100vw" alt="A grid of square items" >}}

In Canary, you can take a look in the demo and see how the items remain square even as their track grows and shrinks, due to the fact that the block size is using a `1/1` ratio of the inline size.

{{< codepen breakout="true" height="600" theme_id="light" slug_hash="WNrRZaV" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/WNrRZaV">Grid using the aspect ratio for items (needs Chrome Canary and Exp Web Platform Features flag)</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### Native Masonry Support 

Developers often ask if CSS Grid can be used to create a Masonry- or Pinterest-styled layout. While some demos look a bit like that, Grid was never designed to do Masonry.

To explain, you need to know what a Masonry layout is. In a typical Masonry layout, items display by row. Once the first row is filled, new items populate another row. However, if some of the items in the first row are shorter than others, the second-row items will rise up to fill the gap. The [Masonry library](https://masonry.desandro.com/) is how many people achieve this using JavaScript.

If you try to create this layout using CSS Grid and auto-placement, you will see that you lose that block direction rearrangement of items. They lay themselves out in strict rows and columns because that is what a grid does.

So could grid ever be used as a Masonry layout? One of the engineers at Mozilla thinks so, and has created a prototype of the functionality. You can test it out by using Firefox Nightly with the flag **layout.css.grid-template-masonry-value.enabled** set to `true` by going to `about:config` in the Firefox Nightly URL bar.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b754c44-8acf-4992-ad63-c7982668c041/smashing-masonry.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b754c44-8acf-4992-ad63-c7982668c041/smashing-masonry.png" sizes="100vw" alt="Masonry Layout in Firefox Nightly" >}}

{{< codepen breakout="true" height="600" theme_id="light" slug_hash="XWmVgwV" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/XWmVgwV">Proposed Masonry (needs Firefox Nightly and the )</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

While this is very exciting for anyone who has had to create this kind of layout using JavaScript, a number of us do wonder if the grid specification is the place to define this very specific layout. You can read some of my thoughts in my article “[Does Masonry Belong In The CSS Grid Specification?](https://rachelandrew.co.uk/archives/2020/05/05/does-masonry-belong-in-the-css-grid-specification/)”.

{{% ad-panel-leaderboard %}}

## Subgrid 

We have had support for the `subgrid` value of `grid-template-columns` and `grid-template-rows` in Firefox for some time. Using this value means that you can inherit the size and number of tracks from a parent grid down through child grids. Essentially, as long as a grid item has `display: grid`, it can inherit the tracks that it covers rather than creating new column or row tracks.

The feature can be tested in Firefox, and I have lots of examples that you can test out. The article “[Digging Into The Display Property: Grids All The Way Down](https://www.smashingmagazine.com/2019/05/display-grid-subgrid/)” explains how subgrid differs from nested grids, and “[CSS Grid Level 2: Here Comes Subgrid](https://www.smashingmagazine.com/2018/07/css-grid-2/)” introduces the specification. I also have a set of broken-down examples at “<a href="https://gridbyexample.com/examples/#css-grid-level-2-examples">Grid by Example</a>”.

However, the first question people have when I talk about subgrid is, "When will it be available in Chrome?" I still can’t give you a _when_, but some good news is on the horizon. On June 18th in a [Chromium blog post](https://blog.chromium.org/2020/06/improving-chromiums-browser.html), it was announced that the Microsoft Edge team (now working on Chromium) are working to reimplement Grid Layout into the LayoutNG engine, i.e. Chromium’s next-generation layout engine. Part of this work will involve also added subgrid support.

Adding features to browsers isn’t a quick process, however, the Microsoft team brought us Grid Layout in the first place &mdash; along with the early prefixed implementation that shipped in IE10. So this is great news and I look forward to being able to test the implementation when it ships in Beta.

## `prefers-reduced-data`

**Not yet implemented in any browser** &mdash; but with [a bug listed for Chrome](https://bugs.chromium.org/p/chromium/issues/detail?id=1051189) with recent activity&mdash; is the `prefers_reduced_data` media feature. This will allow CSS to check if the visitor has enabled data saving in their device and adjust the website accordingly. You might, for example, choose to avoid loading large images.

<pre><code class="language-css">@media (prefers-reduced-data: reduce) {
  .image {
    background-image: url("images/placeholder.jpg");
  }
}
</code></pre>

The `prefers_reduced_data` media feature works in the same way as some of the already implemented [user preference media features](https://drafts.csswg.org/mediaqueries-5/#mf-user-preferences) in the Level 5 Media Queries Specification. For example, the media features `prefers_reduced_motion` and `prefers_color_scheme` allow you to test to see if the visitor has requested to reduce motion or a dark mode in their operating system and tailor your CSS to suit.

{{% ad-panel-leaderboard %}}

## <code>::marker</code> 

The `::marker` pseudo-element allows us to target the list marker. At a very straightforward level, this means that we can target the list bullet and change its color or size. (This was previously impossible due to the fact that you could only target the entire list item &mdash; text and marker.)

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="mdVRXBx" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/mdVRXBx">::marker</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Support for `::marker` is already available in Firefox, and can now be found in Chrome Beta, too.

In addition to styling bullets on actual lists, you can use `::marker` on other elements. In the example below, I have a heading which has been given `display: list-item` and therefore has a marker which I have replaced with an emoji. 

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="pogRaRX" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/pogRaRX">display: list-item and ::marker</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

**Note**: *You can read more about `::marker` and other list-related things in my article “[CSS Lists, Markers and Counters](https://www.smashingmagazine.com/2019/07/css-lists-markers-counters/)” here on Smashing Magazine.*

## Please Test New Features

While it’s fun to have a little peek into what is coming up, I recommend testing out the implementations if you have a use case for any of these things. You may well find a bug or something that doesn’t work as you expect. Browser vendors and the CSS Working Group would love to know. If you think you have found a bug in a browser &mdash; perhaps you are testing `::marker` in Chrome and find it displays differently to the implementation in Firefox &mdash; then raise an issue with the browser: “[How To File A Good Bug](https://web.dev/how-to-file-a-good-bug/)” explains how. If you think that the specification could do something it doesn’t yet, then raise an issue against the specification over at the [CSS Working Group GitHub repository](https://github.com/w3c/csswg-drafts/issues).

{{< signature "il" >}}

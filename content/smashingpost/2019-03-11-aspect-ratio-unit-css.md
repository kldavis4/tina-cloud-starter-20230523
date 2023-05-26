---
title: 'Designing An Aspect Ratio Unit For CSS'
slug: aspect-ratio-unit-css
author: rachel-andrew
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d383950-3f49-4daa-98e6-0a71dcf73564/rachel-andrew-aspect-ratio-unit-css.png
date: 2019-03-11T15:00:41+01:00
summary: >-
  The CSS Working Group have designed an aspect ratio unit for CSS. While this isn’t in browsers yet, this article takes a look at the process of designing a new sizing method and explains how it will work.
description: >-
  What problems will the new aspect ratio unit solve? A look at the design of a new CSS feature.
categories:
  - CSS
  - Browsers
---
One of the things that come up again and again in CSS is the fact that there is no way to size things based on their aspect ratio. In particular when working with responsive designs, you often want to be able to set the width to a percentage and have the height correspond to some aspect ratio. This is something that the folks who are responsible for designing CSS (i.e. the CSS Working Group) have recently been discussing and a proposed solution was agreed upon at a recent CSSWG meeting in San Francisco.

This is a new resolution, so we have no browser implementations yet, but I thought it would be worth writing up the proposal in case anyone in the wider web community could see a showstopping issue with it. It also gives something of an insight into the work of the CSSWG and how issues like this are discussed, and new features designed.

## What Is The Problem We Are Trying To Solve?

The issue in in regard to non-replaced elements, which do not have an intrinsic aspect ratio. Replaced elements are things like images or a video placed with the `<video>` element. They are different to other boxes in CSS as they have set dimensions, and their own behavior. These replaced elements are said to have an intrinsic aspect ratio, due to them having dimensions.

A div or some other HTML element which may contain your content has no aspect ratio, you have to give it a width and a height. There is no way to say that you want to maintain a 16 / 9 aspect ratio, and that whatever the width is, the height should be worked out using the given aspect ratio.

{{% feature-panel %}}

A very common situation is when you want to embed an iframe in order to display a video from a video sharing site such as YouTube. If you use the `<video>` element then the video has an aspect ratio, just like an image. This isn’t the case if the video is elsewhere and you are using an embed. What you want is for your video to be responsive, yet remain at the correct aspect ratio for the video. What you get however, if you set width to 100%, is the need to then set a height. Your video ends up stretched or squished.

Let’s also look at a really simple case of creating a grid layout with square cells. If we were using fixed column track sizes, then it is easy to get our square cells as we can define rows to be the same size as the column tracks. We could also make our row tracks auto-sized, and have items and set the height on the items.

{{< codepen height="480" theme_id="light" slug_hash="BbNXzW" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="[https://codepen.io/smashing-magazine/pen/BbNXzW/](https://codepen.io/rachelandrew/pen/BbNXzW)">Aspect Ratios Example 1</a> by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

The problem comes when we want to use `auto-fill` and fill a container with as many column tracks as will fit. We now can’t simply give the items a height, as we don’t know what the width is. Our items are no longer square.

{{< codepen height="480" theme_id="light" slug_hash="aMOemx" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="[https://codepen.io/smashing-magazine/pen/aMOemx/](https://codepen.io/rachelandrew/pen/aMOemx)">Aspect Ratios Example 2</a> by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

Being able to size things based on their aspect ratio would mean we could calculate the correct aspect ratio once the grid item is laid out. Thus making the grid items as tall as they are wide, so that they always maintain as a square no matter what their width.

## Current Aspect Ratio Solutions

Web developers have been coping with the lack of any aspect ratio in CSS in various ways &mdash; the main one being the "padding hack". This solution uses the fact that padding % in the block direction (so top and bottom padding in a horizontal top to bottom language) is calculated from the inline size (width).

The article “[Aspect Ratio Boxes](https://css-tricks.com/aspect-ratio-boxes/)” on CSS-Tricks has a good rundown of the current methods of creating aspect ratio boxes. The padding hack works in many cases but does require a bunch of hoops to jump through in order to get it working well. It’s also not in the slightest bit intuitive &mdash; even if you know why and how it works. It’s those sort of things that we want to try and solve in the CSS Working Group. Personally, I feel that the more we get elegant solutions for layout in CSS, the more the messy hacks stand out as something we should fix.

For the video situation, you can use JavaScript. A very popular solution is to use [FitVids](https://fitvidsjs.com/) &mdash; as also described in the CSS-Tricks article. Using JavaScript is a reasonable solution, but there’s more script to load, and also something else to remember to do. You can’t simply plonk a video into your content and it _just works_.

{{% ad-panel-leaderboard %}}

## The Proposed Solution

What we are looking for is a generic solution that will work for regular block layouts (such as a video in an iframe or a div on the page). It should also work if the item is a grid or flex item. There is a different issue of wanting grid tracks to maintain an aspect ratio (having the row tracks match the columns), this solution would fix many cases, however, where you might want that (you would be working from the item out rather than the track in).

The soluion will be part of the CSS Sizing Specification, and is being written up in the [CSS Sizing 4 specification](https://drafts.csswg.org/css-sizing-4/#ratios). This is the first step for new features being designed by the CSS Working Group, the idea is discussed, and then written up in a specification. An initial proposal for this feature was brought to the group by Jen Simmons, and you can see her slide deck which goes through many of the use cases discussed in this article [here](https://noti.st/jensimmons/FnU3KJ/adding-explicit-aspect-ratios-to-css).

The new property introduced to the Sizing specification is the `aspect-ratio` property. This property will accept a value which is an aspect ratio such as `16/9`. For example, if you want a square box with the same width and height, you would use the following:

<pre><code class="language-css">.box {
  width: 400px;
  height: auto;
  aspect-ratio: 1/1;
}</code></pre>

For a 16 / 9 box (such as for a video):

<pre><code class="language-css">.box {
  width: 100%;
  height: auto;
  aspect-ratio: 16/9;
}</code></pre>

For the example with the square items in a grid layout, we leave our grid tracks auto-sized, which means they will take their size from the items; we then make our items sized with the `aspect-ratio` unit.

<pre><code class="language-css">.grid {
    display: grid;
    grid-template-columns: repeat(autofill, minmax(200px, 1fr));
}

.item {
    aspect-ratio: 1/1;
}</code></pre>

Features often go through various iterations before browsers start to implement them. Having discussed the need for an aspect ratio unit previously, this time we were looking at one particular concern around the proposal.

What happens if you specify an aspect ratio box, but then add too much content to the box? This same issue is brought up in the CSS-Tricks article about the padding hack &mdash; with equally unintuitive solutions required to fix it.

{{% ad-panel-leaderboard %}}

### Dealing With Overflow

What we are dealing with here is overflow, as is so often the case on the web. We want to have a nice neatly sized box: our design asks for a nice neatly sized box, our content is less well behaved and turns out to be bigger than we expected and breaks out of the box. In addition to specifying how we ask for an aspect ratio in one dimension, we also have to specify what happens if there is too much content, and how the web developer can tell the browser what to do about that overflowing content.

There is a general design principle in CSS that we use in order to avoid data loss. Data loss in a CSS context is where some of your content vanishes. That might either be because it gets poked off the side of the viewport, or is cropped when it overflows. It’s generally preferable to have a messy overflow (as you will notice it and do something about it). If we cause something to vanish, you may not even realize it, especially if it only happens at one breakpoint.

We have a similar issue in grid layout which is nicely fixed with the `minmax()` function for track sizes. You can define grid tracks with a fixed height using a length unit. This will give you a lovely neat grid of boxes, however, as soon as someone adds more content than you expected into one of those boxes, you will get overflow.

{{< codepen height="480" theme_id="light" slug_hash="aMOepr" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="[https://codepen.io/smashing-magazine/pen/aMOepr/](https://codepen.io/rachelandrew/pen/aMOepr)">Aspect Ratios Example 3</a> by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

The fix for this in grid layout is to use `minmax()` for your track size, and make the max value `auto`. In this case, `auto` can be thought of as "big enough to fit the content". What you then get is a set of neat looking boxes that, if more content than expected gets in, grow to accept that content. (Infinitely better than a messy overflow or cropped content.)

In the example below, you can see that while the first row with the box with extra content has grown, the second row is sized at 100 pixels.

{{< codepen height="480" theme_id="light" slug_hash="PLqMmp" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="[https://codepen.io/smashing-magazine/pen/PLqMmp/](https://codepen.io/rachelandrew/pen/PLqMmp)">Aspect Ratios Example 4</a> by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

We need something similar for our aspect ratio boxes, and the suggestion turns out to be relatively straightforward. If you do nothing about overflow, then the default behavior will be that the content is allowed to grow past the height that is inferred by the aspect ratio. This will give you the same behavior as the grid tracks size with `minmax()`. In the case of height, it will be at least the height defined by the aspect ratio, i.e. if the content is taller, the height can grow to fit it.

If you don’t want that, then you can change the value of [overflow](https://developer.mozilla.org/en-US/docs/Web/CSS/overflow) as you would normally do. For example hiding the overflow, or allowing it to scroll.

## Commenting On Proposals In Progress

I think that this proposal covers the use cases detailed in the CSS-Tricks article and the common things that web developers want to do. It gives you a way to create aspect ratio-sized boxes in various layout contexts, and is robust. It will cope with the real situation of content on the web, where we don’t always know how much content we have or how big it is.

If you spot some real problem with this, or have some other use case that you think can’t be solved, you can directly comment on the proposal by raising an issue in the [CSSWG GitHub repo](https://github.com/w3c/csswg-drafts/issues). If you don’t want to do that, you can always comment here, or post to your own blog and link to it here so I can see it. I'd be very happy to share your thoughts with the working group as this feature is discussed.

{{< signature "il" >}}
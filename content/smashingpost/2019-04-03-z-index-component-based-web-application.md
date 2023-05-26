---
title: 'Managing Z-Index In A Component-Based Web Application'
slug: z-index-component-based-web-application
author: pavel-pomerantsev
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b7f42b5-5d9d-4edc-8004-c9b00b3acaac/z-index-sharing-card-pavel.png
date: 2019-04-03T14:00:08+02:00
summary: >-
  The `z-index` property, despite all that’s written about it, is still widely misunderstood and mishandled. Stacking issues in a complex single-page web application can become a major pain. Adhering to some principles, however, we can easily avoid these issues.
description: >-
  The `z-index` property, despite all that’s written about it, is still widely misunderstood and mishandled. Stacking issues in a complex single-page web application can become a major pain. Adhering to some principles, however, we can easily avoid these issues.
categories:
  - CSS
  - Apps
  - UI
---
If you’ve done any complex web UI development, you must have at least once furiously tried driving an element’s `z-index` up to thousands, only to see that it’s not helping position it on top of some other element, whose `z-index` is lower or even not defined at all.

Why does that happen? And more importantly, how to avoid such issues?

In this article, I’ll recap what `z-index` actually is and how you can stop guessing whether it might work in any specific case and start treating it just like any other convenient tool.

## The Hierarchy Of Stacking Contexts

If you imagine the webpage as having three dimensions, then `z-index` is a property that defines the `z` coordinate of an element (also called its “stacking order”): the larger the value, the closer the element is to the observer. You can also think of it as a property affecting paint order, and this will in fact be more correct since the screen is a two-dimensional grid of pixels. So, the larger the `z-index` value, the later the element is painted on the page.

There is, however, one major complication. The `z-index` value space is not flat &mdash; it’s hierarchical. An element can create a stacking context which becomes the root for `z-index` values of its descendants. It would be best to explain the concept of stacking contexts by using an example.

{{% feature-panel %}}

The document body has five `div` descendants: `div1`, `div2`, `div3`, `div1-1`, and `div2-1`. They’re all absolutely positioned and overlap with each other. `div1-1` is a child of `div1`, and `div2-1` is a child of `div2`.

{{< codepen height="480" theme_id="light" slug_hash="bJEmvG" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/bJEmvG/">stacking-contexts</a> by <a href="https://codepen.io/pavelp">Pavel Pomerantsev</a>.{{< /codepen >}}

Let’s try to understand why we see what we see. There are quite elaborate [rules to determine paint order](https://www.w3.org/TR/CSS2/zindex.html), but here we only need to compare two things:

- `z-index` **Values**  
If an element has a higher `z-index`, it’s painted later.
- **Source Order**  
If `z-index` values are the same, then the later it’s in the source, the later it’s painted.

So if we don’t take stacking contexts into account, the order should be as follows:

- `div1`
- `div2`
- `div3`
- `div1-1`
- `div2-1`

Note that `div2-1` is in fact overlapped by `div3`. Why is that happening?

If an element is said to create a **stacking context**, it creates a basis for its children’s `z-index` values, so they’re never compared with anything outside the stacking context when determining paint order. To put it another way, when an element creating a stacking context is painted, all its children are painted right after it and before any of its siblings.

Going back to the example, the actual paint order of `body`’s descendant divs is:

- `div1`
- `div2`
- `div3`
- `div1-1`

Notice the absence of `div2-1` in the list &mdash; it’s a child of `div2` which creates a stacking context (because it’s an absolutely positioned element with a `z-index` other than the default value of `auto`), so it’s painted after `div2`, but before `div3`.

`div1` doesn’t create a stacking context, because its implicit `z-index` value is `auto`, so `div1-1` (its child) is painted after `div2` and `div3` (since its `z-index`, 10, is larger than that of `div2` and `div3`).

Don’t worry if you didn’t fully grasp this on first reading. There’s a bunch of online resources that do a great job in explaining these concepts in more detail:

- “[The Stacking Context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context),” MDN web docs, Mozilla
- “[What No One Told You About Z-Index](https://philipwalton.com/articles/what-no-one-told-you-about-z-index/),” Philip Walton

**Note**: *It’s also great to be familiar with [general paint order rules](https://www.w3.org/TR/CSS2/zindex.html) (which are actually quite complex).*

{{% ad-panel-leaderboard %}}

The main point of this piece, however, is how to deal with `z-index` when your page is composed of dozens and hundreds of components, each potentially having children with `z-index` defined.

One of the most popular articles on `z-index` proposes [grouping all `z-index` values in one place](https://css-tricks.com/handling-z-index/), but comparing those values doesn’t make sense if they don’t belong to the same stacking context (which might not be easy to achieve in a large application).

Here’s an example. Let’s say we have a page with header and main sections. The main section for some reason has to have `position: relative` and `z-index: 1`.

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="XQWLLN" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/XQWLLN/">z-index-step1</a> by <a href="https://codepen.io/pavelp">Pavel Pomerantsev</a>.{{< /codepen >}}

We’re using a component architecture here, so CSS for the root component and every child component is defined in dedicated sections. In practice, components would live in separate files, and the markup would be generated using a JavaScript library of your choice, like React, but for demonstration purposes it’s fine to have everything together.

Now, imagine we’re tasked with creating a dropdown menu in the header. It has to be stacked on top of the main section, of course, so we’ll give it a `z-index` of `10`:

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="VNwJoX" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/VNwJoX/">z-index-step2</a> by <a href="https://codepen.io/pavelp">Pavel Pomerantsev</a>.{{< /codepen >}}

Now, a few months later, in order to make something unrelated work better, we apply the [`translateZ`](https://aerotwist.com/blog/on-translate3d-and-layer-creation-hacks/) hack to the header.

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="jROgOE" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/jROgOE/">z-index-step3</a> by <a href="https://codepen.io/pavelp">Pavel Pomerantsev</a>.{{< /codepen >}}

As you can see, the layout is now broken. An element with `z-index: 1` sits on top of an element with `z-index: 10`, in the absence of any other `z-index` rules. The reason is that the header now creates a stacking context &mdash; it’s an element with a `transform` property whose value is anything other than `none` ([see full rules](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)) and its own `z-index` (`0` by default) is lower than that of the main section (`1`).

The solution is straightforward: give the header a `z-index` value of `2`, and it’ll be fixed.

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="qwBeEV" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/qwBeEV/">z-index-step4</a> by <a href="https://codepen.io/pavelp">Pavel Pomerantsev</a>.{{< /codepen >}}

The question is, how are we supposed to come to this solution if we have components within components within components, each having elements with different z-indices? How can we be sure that changing `z-index` of the header won’t break anything else?

The answer is a convention that eliminates the need for guesswork, and it’s the following: changing z-indices within a component **should only affect that component**, and nothing else. To put it differently, when dealing with `z-index` values in a certain CSS file, we should ideally only concern ourselves with other values in that same file.

Achieving it is easy. We should simply make sure that the root of every component creates a stacking context. The easiest way to do it is to give it `position` and `z-index` values other than the default ones (which are `static` and `auto`, respectively).

Here’s one of the ways to structure the application. It uses more elements than the previous one, but computation associated with extra DOM elements is cheap whereas developer’s time (a lot of which can sometimes be spent on debugging stacking issues) is definitely not.

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="gyOVpq" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/gyOVpq/">z-index-step5</a> by <a href="https://codepen.io/pavelp">Pavel Pomerantsev</a>.{{< /codepen >}}

- `header__container` and `main__container` both have `position: relative` and `z-index: 0`;
- `header__overlay` now has `z-index: 1` (we don’t need a large value since it’s only going to compete for stacking order with other elements within the header);
- `root__header` now has `z-index: 2`, whereas `root__main` keeps its `z-index: 1`, and this is what makes the two siblings stack correctly.

(Note also that both have `position: relative` since [`z-index` doesn’t apply to statically positioned elements](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index).)

{{% ad-panel-leaderboard %}}

If we look at the header code now, we’ll notice that we can remove the `z-index` property from both the container and the overlay altogether because [the overlay is the only positioned element](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/Stacking_without_z-index) there. Likewise, the `z-index` is not required on the main container. This is the biggest benefit of the proposed approach: when looking at z-indices, it’s only the component itself that matters, not its context.

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="WWNVwN" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/WWNVwN/">z-index-step6</a> by <a href="https://codepen.io/pavelp">Pavel Pomerantsev</a>.{{< /codepen >}}

Such an architecture is not without its drawbacks. It makes the application more predictable at the expense of some flexibility. For example, you won’t be able to create such overlays inside both the header and the main section:

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="GLRVqz" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/GLRVqz/">z-index-step7</a> by <a href="https://codepen.io/pavelp">Pavel Pomerantsev</a>.{{< /codepen >}}

In my experience, however, this is rarely a problem. You could make the overlay in the main section go down instead of up, in order for it to not intersect with the header. Or, if you really needed it to go up, you could inject the overlay HTML at the end of the body and give it a large `z-index` (“large” being whatever’s larger than those of other sections at the top level). In any case, if you’re not in a competition to build the most complicated layout, you should be fine.

To recap:

- **Isolate components** in terms of `z-index` values of elements by making the root of each component a stacking context;
- You don’t have to do it if no element within a component needs a `z-index` value other than `auto`;
- Within a component’s CSS file, **maintain** `z-index` **values any way you like**. It might be consecutive values, or you could give them a step of 10, or you can use variables &mdash; it all depends on your project’s conventions and the size of the component (although making components smaller is never a bad thing). Preferably, only assign `z-index` to sibling elements. Otherwise, you may inadvertently introduce more stacking contexts within a component, and you’re faced with the same issue again, luckily on a smaller scale;
- **Debugging becomes easy**. Find the first ancestor component of the two elements that are not stacked correctly, and change z-indices within that component as necessary.

This approach will hopefully bring back some sanity to your development process.

{{< signature "dm, ra, il" >}}
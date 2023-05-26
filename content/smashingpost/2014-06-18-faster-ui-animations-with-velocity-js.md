---
title: Faster UI Animations With Velocity JS
slug: faster-ui-animations-with-velocity-js
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84fac24e-1de4-48fd-a1d5-2cf9c04c5b6e/velocity-header-2-opt.jpg
date: 2014-06-18T19:51:58.000Z
author: julianshapiro
description: >-
  From a motion design perspective, Facebook.com is phenomenally static. It's
  purposefully dumbed down for the broadest levels of compatibility and user
  comfort. Facebook’s iOS apps, on the other hand, are fluid. They prioritize
  the design of motion; they feel like living, breathing apps.

  This article serves to demonstrate that this dichotomy does not need to exist;
  websites can benefit from the same level of interactive and performant motion
  design found on mobile apps. Before diving into examples, let's first address
  why motion design is so beneficial.
categories:
  - Coding
  - CSS
  - JavaScript
  - Techniques
---
From a motion design perspective, Facebook.com is phenomenally static. It's purposefully dumbed down for the broadest levels of compatibility and user comfort. Facebook’s iOS apps, on the other hand, are fluid. They prioritize the design of motion; they feel like living, breathing apps.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec87e60d-bce6-499e-b83c-b7ab87f8843a/velocity-header-3-opt.jpg" alt="velocity js" title="Faster UI Animations With Velocity js" width="500" height="333" /></figure>

This article serves to demonstrate that this dichotomy does not need to exist; websites can benefit from the same level of interactive and performant motion design found on mobile apps.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Quick Look Into The Math Of Animations With JavaScript](https://www.smashingmagazine.com/2011/10/quick-look-math-animations-javascript/)
*   [The State Of Animation 2014](https://www.smashingmagazine.com/2014/11/the-state-of-animation-2014/)
*   [GPU Animation: Doing It Right](https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/)
*   [We’re Gonna Need A Bigger API!](https://www.smashingmagazine.com/2013/03/animating-web-gonna-need-bigger-api/)

Before diving into examples, let's first address why motion design is so beneficial:

{{% feature-panel %}}

*   **Improved feedback loops**.  As a UI and UX designer, you should use patterns as much as possible since users will be subconsciously looking for them. Responsive motion patterns, in particular, are the key to pleasurable interactions: When a button has been clicked, do you feel that it has reacted to the pressure of your mouse? When a file has been saved, do you get the strong sense that your data has truly been transferred and stored?
*   **Seamless content transitions**.  Motion design allows you to avoid contextual breaks; modals fading in and out (as opposed to switching pages entirely) are a popular example of this.
*   **Filled dead spots**.  When users are performing an unengaging task on your page, you can raise their level of arousal through sound, colors, and movement. Diverting a user’s attention is a great way to make a pot boil faster.
*   **Aesthetic flourishes**.  For the same aesthetic reasons that UI designers spend hours perfecting their pages' color and font combinations, motion designers perfect their animations' transition and easing combinations: Refined products simply feel superior.

In the examples below, we'll be using [Velocity JS](https://velocityjs.org "Velocity.js") — a popular animation engine that drastically improves the speed of UI animation. (Velocity.js behaves identically to jQuery’s `$.animate()` function, while outperforming both jQuery animation and CSS animation libraries.) In particular, this article focuses on Velocity.js’ [UI pack](https://velocityjs.org/#uiPack "UI Pack"), which allows you to quickly inject motion design into your pages. You may optionally watch this article’s [accompanying codecast](https://www.youtube.com/watch?v=CdwvR6a39Tg&hd=1) (5 minutes) for a preview of what we’ll cover.</p>

## UI Pack Overview

After including the UI pack (only 1.8 KB ZIP’ed) on your page, you’ll gain access to UI effects that are organized into two categories:

### Callouts

Callouts are effects that call attention to an element in order to heighten user experience, such as shaking an element to indicate an input error, flashing an element to indicate that something has changed on the page, or bouncing an element to indicate that a message awaits the user.

See the Pen [Velocity.js - UI Pack: Callout](https://codepen.io/julianshapiro/pen/Fybjq/) by Julian Shapiro ([@julianshapiro](https://codepen.io/julianshapiro)) on [CodePen](https://codepen.io).</p>

### Transitions

Transitions are effects that cause an element to appear in or out of view. Every transition is associated with either an “in” or “out” direction. The value of transitions is in revealing and hiding content in a way that’s visually richer than merely animating an element’s opacity. Here’s `slideUpIn`, a transition that incorporates a subtle slide effect:

See the Pen [Velocity.js - UI Pack: Transition](https://codepen.io/julianshapiro/pen/aLhFC/) by Julian Shapiro ([@julianshapiro](https://codepen.io/julianshapiro)) on [CodePen](https://codepen.io).

If you’ve paid attention to the evolution of iOS’ UI motion design, you’ll have noticed that over a dozen transition effects help make iOS’ interface pleasurable to interact with. This diversity of transitions is what Velocity.js’ UI pack brings to everyday websites.

Note that, thanks to Velocity.js’ performance, as well as the optimizations afforded by the UI pack, all of the pack’s effects are 100% ready for large-scale production use.

Let’s dive into some simple code examples.

## Using The UI Pack

Callouts and transitions are referenced via Velocity’s first parameter: Pass in an effect’s name instead of passing in a standard property map. For comparison, here’s the syntax of a _normal_ Velocity.js call, which behaves identically to jQuery’s `$.animate()`:

<pre><code class="language-javascript">
$elements.velocity({ opacity: 0.5 });
</code></pre>

In contrast, below are Velocity.js calls using effects from the UI pack:

<pre><code class="language-javascript">
/* Shake an element. */
$elements.velocity("callout.shake");

/* Transition an element into view using slideUp. */
$elements.velocity("transition.slideUpIn");
</code></pre>

Just as with normal Velocity.js calls, UI effects may be chained onto each other and may take options:

<pre><code class="language-javascript">
/* Call the shake effect with a 2000ms duration, then slide the elements out of view. */
$elements
	.velocity("callout.shake", 2000)
	.velocity("transition.slideDownOut");
</code></pre>

Effects from the UI pack optionally take three unique options: `stagger`, `drag` and `backwards`.</p>

### Stagger

Specify `stagger` in milliseconds to successively delay the animation of each element in a set by the specified amount. (Setting a `stagger` value prevents elements from animating in parallel, which tends to lack elegance.)

<pre><code class="language-javascript">
/* Animate elements into view with intermittent delays of 250ms. */
$divs.velocity("transition.slideLeftIn", { stagger: 250 });
</code></pre>

See the Pen [Velocity.js - UI Pack: Stagger](https://codepen.io/julianshapiro/pen/mqsnk/) by Julian Shapiro ([@julianshapiro](https://codepen.io/julianshapiro)) on [CodePen](https://codepen.io).</p>

### Drag

Set `drag` to `true` to successively increase the animation duration of each element in a set. The last element will animate with a duration equal to the animation’s original value, whereas the elements prior to the last will have their duration values gradually approach the original value.

The result is a cross-element easing effect. (If you’ve ever been wowed by motion typography demos made with After Effects, drag is a key yet subtle component behind their visual richness.)

See the Pen [Velocity.js - UI Pack: Drag](https://codepen.io/julianshapiro/pen/lxfie/) by Julian Shapiro ([@julianshapiro](https://codepen.io/julianshapiro)) on [CodePen](https://codepen.io).</p>

### Backwards

Set `backwards` to `true` to animate starting with the last element in a set. This option is ideal for an effect that transitions elements out of view, because the `backwards` option mirrors the behavior of elements transitioning into view (which, by default, animate in a forward direction, from the first element to the last).

See the Pen [Velocity.js - UI Pack: Backwards](https://codepen.io/julianshapiro/pen/fEKsw/) by Julian Shapiro ([@julianshapiro](https://codepen.io/julianshapiro)) on [CodePen](https://codepen.io).

Together, these three options bring the power of motion design suites to the Web. When used sparingly, the results are beautiful — so long as you design with user experience in mind:

## Designing For UX

Spicing up a page with motion design can [escalate quickly](https://www.youtube.com/watch?v=FONN-0uoTHI). Here are a few considerations to keep in mind:

*   **Make them finish quickly**.  When applying transitions, developers often make the mistake of letting them run too long, causing users to wait needlessly. Never let UI flourishes slow down the apparent speed of your page. If you have a lot of content fading in, keep the animation’s total duration short.
*   **Use an appropriate effect**.  For example, don’t use a playful bounce effect on a page that features formal content.
*   **Use them sparingly**.  Having transitions in every corner of your page is overkill.
*   **Avoid extreme repetition**.  Avoid transitions of medium-to-long duration in places where they’ll be repeatedly triggered.
*   **Experiment**.  Find the right duration, stagger, drag and backwards combinations that will produce the right fit for each of your individual animations.</p>

## Benefits Of JavaScript-Based Animation

Let’s step back and contextualize why powering these types of UI transitions through JavaScript is a good idea in the first place. After all, up until now, these effects have been most commonly applied using pre-made CSS classes from libraries such as [Animate.css](https://github.com/daneden/animate.css):

*   Because the UI pack’s effects behave identically to standard animation calls in Velocity.js, they can be chained and take options. (Doing this with raw CSS can be cumbersome.)
*   The effects have all been optimized for performance (minimal DOM interaction).
*   Elements animated via the UI pack automatically switch to `display: none` after transitioning out, and back to `display: block` or `inline` before transitioning in. (Doing this via CSS requires multiple calls and messy code.)
*   Velocity.js doesn’t leave your text blurry. If you’ve applied transition effects via CSS before, then you’ll know that text can look fuzzy when you’re done animating and haven’t removed the associated class. This doesn’t happen in Velocity.js because its underlying engine completely clears unneeded transformation effects upon completion of an animation.
*   The effects work everywhere but Internet Explorer 8, where they gracefully fall back to simply fading in and out.

With all of these benefits, including the effects' great performance across all browsers and devices (including older mobile devices), you have no excuse to not start experimenting with motion design on your sites. Enjoy!

**Note**: Look through [Velocity.js’ documentation](https://velocityjs.org/#uiPack) to play around with all of the UI pack’s effects.</p>

### Links

*   [Download Velocity on GitHub](https://github.com/julianshapiro/velocity)
*   [Velocity demo gallery](https://codepen.io/collection/tIjGb/)

_Front page image credits: [Unsplash.com](https://unsplash.com/)_

{{< signature "al, il" >}}


---
title: JavaScript Awesomeness — Or How To Animate Without jQuery
slug: animating-without-jquery
image: null
date: 2014-09-04T21:11:04.000Z
author: julianshapiro
description: >-
  JavaScript-based animation is often as fast as CSS-based
  animation — sometimes even faster. CSS animation only appears to have a leg up
  because it’s typically compared to jQuery’s `$.animate()`, which is, in fact,
  very slow. However, JavaScript animation libraries that bypass jQuery deliver
  incredible performance by avoiding DOM manipulation as much as possible. These
  libraries can be up to 20 times faster than jQuery.
categories:
  - Coding
  - Tools
  - JavaScript
  - Techniques
  - jQuery
---
There’s a false belief in the web development community that CSS animation is the only performant way to animate on the web. <strong>This myth has coerced many developers to abandon JavaScript-based animation altogether</strong>, thereby (1) forcing themselves to manage complex UI interaction within style sheets, (2) locking themselves out of supporting Internet Explorer 8 and 9, and (3) forgoing the beautiful motion design physics that are possible only with JavaScript.

Reality check: JavaScript-based animation is often as fast as CSS-based animation — sometimes even faster. CSS animation only appears to have a leg up because it’s typically compared to jQuery’s <code>$.animate()</code>, which is, in fact, very slow. However, JavaScript animation libraries that bypass jQuery deliver incredible performance by avoiding DOM manipulation as much as possible. These libraries can be up to 20 times faster than jQuery.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Quick Look Into The Math Of Animations With JavaScript](https://www.smashingmagazine.com/2011/10/quick-look-math-animations-javascript/)
*   [The State Of Animation 2014](https://www.smashingmagazine.com/2014/11/the-state-of-animation-2014/)
*   [GPU Animation: Doing It Right](https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/)
*   [We’re Gonna Need A Bigger API!](https://www.smashingmagazine.com/2013/03/animating-web-gonna-need-bigger-api/)

So, <strong>let’s smash some myths</strong>, dive into some real-world animation examples and improve our design skills in the process. If you love designing practical UI animations for your projects, this article is for you.

{{% feature-panel %}}

## Why JavaScript?

CSS animations are convenient when you need to sprinkle property transitions into your style sheets. Plus, they deliver fantastic performance out of the box — without your having to add libraries to the page. However, when you use CSS transitions to power rich motion design (the kind you see in the latest versions of iOS and Android), they become too difficult to manage or their features simply fall short.

Ultimately, CSS animations limit you to what the specification provides. In JavaScript, by the very nature of any programming language, you have an infinite amount of logical control. JavaScript animation engines leverage this fact to provide novel features that let you pull off some very useful tricks:

*   [cross-browser SVG support](https://codepen.io/sol0mka/full/jpecs/),
*   [physics-based loader animations](https://codepen.io/timothyrourke/full/wojke/),
*   [timeline control](https://codepen.io/GreenSock/full/yhEmn/),
*   [Bezier translations](https://codepen.io/GreenSock/full/LuIJj/).

<strong>Note</strong>: If you’re interested in learning more about performance, you can read Julian Shapiro’s “<a href="https://davidwalsh.name/css-js-animation">CSS vs. JS Animation: Which Is Faster?</a>” and Jack Doyle’s “<a href="https://css-tricks.com/myth-busting-css-animations-vs-javascript/">Myth Busting: CSS Animations vs. JavaScript</a>.” For performance demos, refer to the <a href="https://velocityjs.org">performance pane</a> in Velocity’s documentation and GSAP’s “<a href="https://codepen.io/GreenSock/full/srfxA/">Library Speed Comparison</a>” demo.</p>

## Velocity and GSAP

The two most popular JavaScript animation libraries are <a href="https://velocityjs.org">Velocity.js</a> and <a href="https://greensock.com/gsap/">GSAP</a>. They both work with and without jQuery. When these libraries are used alongside jQuery, there is no performance degradation because they completely bypass jQuery’s animation stack.

If jQuery is present on your page, you can use Velocity and GSAP just like you would jQuery’s <code>$.animate()</code>. For example, <code>$element.animate({ opacity: 0.5 });</code> simply becomes <code>$element.velocity({ opacity: 0.5 })</code>.

These two libraries also work when jQuery is not present on the page. This means that instead of chaining an animation call onto a jQuery element object — as just shown — you would pass the target element(s) to the animation call:

<pre><code class="language-javascript">
/* Working without jQuery */

Velocity(element, { opacity: 0.5 }, 1000); // Velocity

TweenMax.to(element, 1, { opacity: 0.5 }); // GSAP
</code></pre>

As shown, Velocity retains the same syntax as jQuery’s <code>$.animate()</code>, even when it’s used without jQuery; just shift all arguments rightward by one position to make room for passing in the targeted elements in the first position.

GSAP, in contrast, uses an object-oriented API design, as well as convenient static methods. So, you can get full control over animations.

In both cases, you’re no longer animating a jQuery element object, but rather a raw DOM node. As a reminder, you access raw DOM nodes by using <code>document.getElementByID</code>, <code>document.getElementsByTagName</code>, <code>document.getElementsByClassName</code> or <code>document.querySelectorAll</code> (which works similarly to jQuery’s selector engine). We’ll briefly work with these functions in the next section.</p>

## Working Without jQuery

(Note: If you need a basic primer on working with jQuery’s <code>$.animate()</code>, refer to the first few panes in <a href="https://velocityjs.org/#arguments">Velocity’s documentation.</a>)

Let’s explore <code>querySelectorAll</code> further because it will likely be your weapon of choice when selecting elements without jQuery:

<pre><code class="language-javascript">
document.querySelectorAll("body"); // Get the body element
document.querySelectorAll(".squares"); // Get all elements with the "square" class
document.querySelectorAll("div"); // Get all divs
document.querySelectorAll("#main"); // Get the element with an id of "main"
document.querySelectorAll("#main div"); // Get the divs contained by "main"
</code></pre>

As shown, you simply pass <code>querySelectorAll</code> a CSS selector (the same selectors you would use in your style sheets), and it will return all matched elements in an array. Hence, you can do this:

<pre><code class="language-javascript">
/* Get all div elements. */
var divs = document.querySelectorAll("div");

/* Animate all divs at once. */
Velocity(divs, { opacity: 0.5 }, 1000); // Velocity
TweenMax.to(divs, 1, { opacity: 0.5 }); // GSAP
</code></pre>

Because we’re no longer attaching animations to jQuery element objects, you may be wondering how we can chain animations back to back, like this:

<pre><code class="language-javascript">
$element // jQuery element object
	.velocity({ opacity: 0.5 }, 1000)
	.velocity({ opacity: 1 }, 1000);
</code></pre>

In Velocity, you simply call animations one after another:

<pre><code class="language-javascript">
/* These animations automatically chain onto one another. */
Velocity(element, { opacity: 0.5 }, 1000);
Velocity(element, { opacity: 1 }, 1000);
</code></pre>

Animating this way has no performance drawback (as long as you cache the element being animated to a variable, instead of repeatedly doing <code>querySelectorAll</code> lookups for the same element).

(Tip: With Velocity’s UI pack, you can create your own multi-call animations and give them custom names that you can later reference as Velocity’s first argument. See Velocity’s <a href="https://velocityjs.org/#uiPack">UI Pack documentation</a> for more information.)

This one-Velocity-call-at-a-time process has a huge benefit: If you’re using <a href="https://velocityjs.org/#promises">promises</a> with your Velocity animations, then each Velocity call will return an actionable promise object. You can learn more about working with promises in <a href="https://www.html5rocks.com/en/tutorials/es6/promises/">Jake Archibald’s article</a>. They’re incredibly powerful.

In the case of GSAP, its expressive object-oriented API allows you to place your animations in a timeline, giving you control over scheduling and synchronization. You’re not limited to one-after-the-other chained animations; you can nest timelines, make animations overlap, etc:

<pre><code class="language-javascript">
var tl = new TimelineMax();
/* GSAP tweens chain by default, but you can specify exact insertion points in the timeline, including relative offsets. */
tl
  .to(element, 1, { opacity: 0.5 })
  .to(element, 1, { opacity: 1 });
</code></pre>

## JavaScript Awesomeness: Workflow

Animation is inherently an experimental process in which you need to <strong>play</strong> with timing and easings to get exactly the feel that your app needs. Of course, even once you think a design is perfect, a client will often request non-trivial changes. In these situations, a manageable workflow becomes critical.

While CSS transitions are impressively easy to sprinkle into a project for effects such as hovers, they become unmanageable when you attempt to sequence even moderately complex animations. That’s why CSS provides <strong>keyframe animations</strong>, which allow you to group animation logic into sections.

However, a core deficiency of the keyframes API is that you must define sections in <strong>percentages</strong>, which is unintuitive. For example:

<pre><code class="language-javascript">
@keyframes myAnimation {
   0% {
      opacity: 0;
      transform: scale(0, 0);
   }
   25% {
      opacity: 1;
      transform: scale(1, 1);
   }
   50% {
      transform: translate(100px, 0);
   }
   100% {
      transform: translate(100px, 100px);
   }
}

#box {
   animation: myAnimation 2.75s;
}
</code></pre>

What happens if the client asks you to make the <code>translateX</code> animation 1 second longer? Yikes. That requires redoing the math and changing all (or most) of the percentages.

Velocity has its <a href="https://velocityjs.org/#uiPack">UI pack</a> to deal with multi-animation complexity, and GSAP offers <a href="https://greensock.com/sequence-video">nestable timelines</a>. These features allow for entirely new workflow possibilities.

But let’s stop preaching about workflow and actually dive into fun animation examples.</p>

## JavaScript Awesomeness: Physics

Many powerful effects are achievable exclusively via JavaScript. Let’s examine a few, starting with physics-based animation.

The utility of physics in motion design hits upon the core principle of what makes for a great UX: interfaces that flow naturally from the user’s input — in other words, interfaces that adhere to how motion works in the real world.

GSAP offers physics plugins that adapt to the constraints of your UI. For example, the ThrowPropsPlugin tracks the dynamic velocity of a user’s finger or mouse, and when the user releases, ThrowPropsPlugin matches that corresponding velocity to naturally glide the element to a stop. The resulting animation is a standard tween that can be time-manipulated (paused, reversed, etc.):

See the Pen [Draggable (Mini)](https://codepen.io/GreenSock/pen/f5005e85b22ae5b7d5b1075c488cedde/) by GreenSock ([@GreenSock](https://codepen.io/GreenSock)) on [CodePen](https://codepen.io).

Velocity offers an easing type based on spring physics. Typically with easing options, you pass in a named easing type; for example, <code>ease</code>, <code>ease-in-out</code> or <code>easeInOutSine</code>. With spring physics, you pass a two-item array consisting of tension and friction values (in brackets below):

<pre><code class="language-javascript">
Velocity(element, { left: 500 }, [ 500, 20 ]); // 500 tension, 20 friction
</code></pre>

A higher tension (a default of 500) increases the total speed and bounciness. A lower friction (a default of 20) increases ending vibration speed. By tweaking these values, you can separately fine-tune your animations to have different personalities. Try it out:

See the Pen [Velocity.js - Easing: Spring Physics (Tester)](https://codepen.io/julianshapiro/pen/hyeDg/) by Julian Shapiro ([@julianshapiro](https://codepen.io/julianshapiro)) on [CodePen](https://codepen.io).</p>

## JavaScript Awesomeness: Scrolling

In Velocity, you can enable the user to scroll the browser to the edge of any element by passing in <code>scroll</code> as Velocity’s first argument (instead of a properties map). The <code>scroll</code> command behaves identically to a standard Velocity call; it can take options and can be queued.

<pre><code class="language-javascript">
Velocity(element, "scroll", { duration: 1000 };
</code></pre>

See the Pen [Velocity.js - Command: Scroll w/ Container Option](https://codepen.io/julianshapiro/pen/kBuEi/) by Julian Shapiro ([@julianshapiro](https://codepen.io/julianshapiro)) on [CodePen](https://codepen.io).

You can also scroll elements within containers, and you can scroll horizontally. See Velocity’s <a href="https://velocityjs.org/#scroll">scroll documentation</a> for further information.

GSAP has ScrollToPlugin, which offers similar functionality and can automatically relinquish control when the user interacts with the scroll bar.</p>

## JavaScript Awesomeness: Reverse

Both Velocity and GSAP have reverse commands that enable you to animate an element back to the values prior to its last animation.

In Velocity, pass in <code>reverse</code> as Velocity’s first argument:

<pre><code class="language-javascript">
// Reverse defaults to the last call's options, which you can extend
Velocity(element, "reverse", { duration: 500 });
</code></pre>

Click on the “JS” tab to see the code that powers this demo:

See the Pen [Velocity.js - Command: Reverse](https://codepen.io/julianshapiro/pen/hBFbc/) by Julian Shapiro ([@julianshapiro](https://codepen.io/julianshapiro)) on [CodePen](https://codepen.io).

In GSAP, you can retain a reference to the animation object, then invoke its <code>reverse()</code> method at any time:

<pre><code class="language-javascript">
var tween = TweenMax.to(element, 1, {opacity:0.5});
tween.reverse();
</code></pre>

## Transform Control

With CSS animation, all transform components — scale, translation, rotation and skew — are contained in a single CSS property and, consequently, cannot be animated independently using different durations, easings and start times.

For rich motion design, however, independent control is imperative. Let’s look at the dynamic transform control that’s achievable only in JavaScript. Click the buttons at any point during the animation:

See the Pen [Independent Transforms](https://codepen.io/GreenSock/pen/kingu/) by GreenSock ([@GreenSock](https://codepen.io/GreenSock)) on [CodePen](https://codepen.io).

Both Velocity and GSAP allow you to individually animate transform components:

<pre><code class="language-javascript">
// Velocity
/* First animation */
Velocity(element, { translateX: 500 }, 1000);
/* Trigger a second (concurrent) animation after 500 ms */
Velocity(element, { rotateZ: 45 }, { delay: 500, duration: 2000, queue: false });

// GSAP
/* First animation */
TweenMax.to(element, 1, { x: 500 });
/* Trigger a second (concurrent) animation after 500 ms */
TweenMax.to(element, 2, { rotation: 45, delay: 0.5 });
</code></pre>

## Wrapping Up

*   Compared to CSS animation, JavaScript animation has better browser support and typically more features, and it provides a more manageable workflow for animation sequences.
*   Animating in JavaScript doesn’t entail sacrificing speed (or hardware acceleration). Both Velocity and GSAP deliver blistering speed and hardware acceleration under the hood. No more messing around with `null-transform` hacks.
*   You don’t need to use jQuery to take advantage of dedicated JavaScript animation libraries. However, if you do, you will not lose out on performance.</p>

### Final Note

Refer to <a href="https://velocityjs.org">Velocity</a> and GSAP’s documentation to master JavaScript animation.

{{< signature "al, il" >}}

<em>Front page image credits: <a href="https://www.flickr.com/photos/gsfc/6962625139">NASA Goddard Space Flight Center </a>.</em>


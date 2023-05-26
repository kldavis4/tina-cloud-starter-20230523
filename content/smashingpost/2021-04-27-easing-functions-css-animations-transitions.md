---
title: 'Understanding Easing Functions For CSS Animations And Transitions'
slug: easing-functions-css-animations-transitions
author: adrian-bece
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/140e292f-c3a2-438d-ae33-90d09a421f9c/easing-functions-css-animations-transitions.jpg
date: 2021-04-27T12:00:00.000Z
summary: >-
  Easing functions can change the look and feel of an animation by affecting the rate, or speed, of an animation. As human beings, we are accustomed to a natural, non-linear motion. Using those custom-easing functions in the animations can lead to an improved impression on users and a more delightful user experience. In this article, we’re going to take a deep dive into easing functions and see how we can use them to create those natural and stunning animations.
description: >-
  Easing functions can change the look and feel of an animation by affecting the rate, or speed, of an animation. In this article, we’re going to take a deep dive into easing functions and see how we can use them to create those natural and stunning animations.
categories:
  - CSS
  - Animation
---

Have you ever noticed how smooth and delightful animations look on a well-made, professional project? I am reminded of the [In Pieces](https://www.species-in-pieces.com/) website where animations are used not just for decoration, but they also convey the message about the endangered species in an impactful way. Not only is the animation design and style beautiful, but they also flow nicely and harmoniously. It is precisely that flow in combination with the design and presentation which makes the animation look stunning and natural. That is the power of easing functions, which are also called timing functions.

{{< vimeo id="538872497" >}}

When writing transition and animation properties in CSS, we usually go for the pre-defined easing functions like `ease-out` because it's simple, they look alright and they work well for most cases. However, having a dozen or more elements on a page with an animation that features the same duration and easing function values may make the UI a bit bland and monotone. Humans respond better to natural motion, so making the animation and transition more varied and natural will result in a better user experience. 

If we go back to the [In Pieces](https://www.species-in-pieces.com/) example and inspect the [stylesheet](https://www.species-in-pieces.com/css/main.css), we can notice that various custom `cubic-bezier` easing functions are used in combination with the pre-defined `linear` and `ease-in` timing functions to achieve that beautiful animation flow. Animations wouldn’t look as good if only pre-defined easing functions were used instead of custom easing functions. Following video showcases In Pieces website with all easing functions set to  `ease-out`. Even though there is nothing wrong with the animations, notice how they are not as stunning nor exciting as the original animations.

{{< vimeo id="538892682" >}}

In this article, we’re going to take a deep dive into CSS easing functions, types of easing functions, and how to create custom easing functions using Cubic Bézier curves.

{{% feature-panel %}}

## Under The Hood

In order to get a better understanding of easing functions, we need to take a step back and take a look at the animation basics in CSS. 

Animation is defined by **keyframes** which determine how an element should look and be positioned at certain points. CSS Transitions use two keyframes (starting and ending value), while CSS animations allow more precise control with the `@keyframes` rule.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5fed2eb-8c2c-45b6-9c11-f4d4228554a7/3-easing-functions-css-animations-transitions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5fed2eb-8c2c-45b6-9c11-f4d4228554a7/3-easing-functions-css-animations-transitions.png" width="800" height="528" sizes="100vw" caption="Example of animation output (keyframes) of a box that moves from 0px (0% animation output) to 500px (100% animation output) from left to right. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5fed2eb-8c2c-45b6-9c11-f4d4228554a7/3-easing-functions-css-animations-transitions.png'>Large preview</a>)" alt="Example of animation output (keyframes) of a box that moves from 0px (0% animation output) to 500px (100% animation output) from left to right" >}}

**Animation duration** determines the amount of time for the animation to go from the first keyframe to the last. The following graph shows the connection between the animation keyframes and duration.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8067d81-7657-4714-886c-4681fd663396/04-easing-functions-css-animations-transitions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8067d81-7657-4714-886c-4681fd663396/04-easing-functions-css-animations-transitions.png" width="525" height="487" sizes="100vw" caption="Example of animation output of a box that moves from 0px (0% animation output) to 500px (100% animation output) with 1000ms duration. The two points are connected by a straight line. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8067d81-7657-4714-886c-4681fd663396/04-easing-functions-css-animations-transitions.png'>Large preview</a>)" alt="Example of animation output of a box that moves from 0px (0% animation output) to 500px (100% animation output) with 1000ms duration. The two points are connected by a straight line." >}}

There are many ways in which animation can progress between two keyframes. For example, animation can have a constant speed or it can move quickly at the start and slow down near the end, or move slowly at the start and then speed up until it reaches the end, etc. This [rate, or speed](https://www.w3.org/TR/css-easing-1/#introduction) is defined with the **easing functions (timing functions)**. If we take a look at the previous graph, the easing function is represented by the shape of the line connecting the two points. We’ve used the linear function (straight line) for the previous example, but we can also use a curve to connect the keyframes.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/725924ac-22d0-42cc-aa91-87261d4593c5/05-easing-functions-css-animations-transitions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/725924ac-22d0-42cc-aa91-87261d4593c5/05-easing-functions-css-animations-transitions.png" width="525" height="487" sizes="100vw" caption="Example of animation output of a box that moves from 0px (first keyframe) to 500px (last keyframe) with 1000ms duration. Animation will accelerate on the starting keyframe and decelerate near the last keyframe. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/725924ac-22d0-42cc-aa91-87261d4593c5/05-easing-functions-css-animations-transitions.png'>Large preview</a>)" alt="Example of animation output of a box that moves from 0px (first keyframe) to 500px (last keyframe) with 1000ms duration. Animation will accelerate on the starting keyframe and decelerate near the last keyframe." >}}

As you can see, there are lots of possible options and variations for animation easing functions and we’ll take a look at them next.

## Types Of Easing Functions

There are three main types of easing functions that can be used in CSS:

- Linear functions (`linear`),
- Cubic Bézier functions (includes `ease`, `ease-in`, `ease-out` and `ease-in-out`),
- Staircase functions (`steps`).

### Linear Functions

We’ve covered linear functions in one of the previous examples, so let’s do a quick recap. With the linear timing function, the animation is going through the keyframes at a constant speed. As you might already know, the linear timing function can be easily set in CSS by using the `linear` keyword.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/032ffd9f-1652-44cb-9f94-541d840a11aa/004-easing-functions-css-animations-transitions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/032ffd9f-1652-44cb-9f94-541d840a11aa/004-easing-functions-css-animations-transitions.png" width="525" height="487" sizes="100vw" caption="Example of animation output of a box that moves from 0px (0% animation output) to 500px (100% animation output) with 1000ms duration. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/032ffd9f-1652-44cb-9f94-541d840a11aa/004-easing-functions-css-animations-transitions.png'>Large preview</a>)" alt="Example of animation output of a box that moves from 0px (0% animation output) to 500px (100% animation output) with 1000ms duration." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b45f4b3c-9f20-4cf4-888f-1052518f4a32/07-easing-functions-css-animations-transitions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b45f4b3c-9f20-4cf4-888f-1052518f4a32/07-easing-functions-css-animations-transitions.png" width="525" height="487" sizes="100vw" caption="Example of animation output of a box that moves from 0px (first keyframe) to 200px (second keyframe) and then to 500px (final keyframe) with 1000ms duration. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b45f4b3c-9f20-4cf4-888f-1052518f4a32/07-easing-functions-css-animations-transitions.png'>Large preview</a>)" alt="Example of animation output of a box that moves from 0px (first keyframe) to 200px (second keyframe) and then to 500px (final keyframe) with 1000ms duration." >}}

{{< codepen height="480" theme_id="light" slug_hash="Bapbgxg" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Animation - linear](https://codepen.io/smashingmag/pen/Bapbgxg) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

## Cubic Bézier Functions

Although linear timing functions have their use-cases, they can make the animations look bland and unnatural if used incorrectly or used too often. As we’ve seen from the [In Pieces](https://www.species-in-pieces.com/) example, **users respond better to natural motion**, i.e. non-linear timing functions which can accelerate and decelerate. 

[Bézier curves](https://en.wikipedia.org/wiki/B%C3%A9zier_curve) are commonly used in vector graphics, animations and robotics to easily create smooth curves and trajectories. In CSS we are using Bézier curves defined by four points, which are known as **Cubic Bézier** curves.

Commonly-used pre-defined easing functions like `ease`, `ease-in`, `ease-out`, and `ease-in-out` belong to the Cubic Bézier functions. They can be used as a quick way to set a non-linear easing function. Even a linear function can be defined using a `cubic-bezier` function.

<table class="tablesaw break-out">
	<thead>
		<tr>
			<th>Easing Function</th>
			<th><code>cubic-bezier</code> Value</th>
			<th>Starting Speed</th>
			<th>Middle Speed</th>
			<th>Ending Speed</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><code>linear</code></td>
			<td><code>cubic-bezier(0.0, 0.0, 1.0, 1.0)</code></td>
			<td>constant</td>
			<td>constant</td>
			<td>constant</td>
		</tr>
		<tr>
			<td><code>ease</code></td>
			<td><code>cubic-bezier(0.25, 0.1, 0.25, 1.0)</code></td>
			<td>fast acceleration</td>
			<td>fast acceleration</td>
			<td>slow acceleration</td>
		</tr>
		<tr>
			<td><code>ease-in</code></td>
			<td><code>cubic-bezier(0.42, 0, 1.0, 1.0)</code></td>
			<td>slow acceleration</td>
			<td>fast acceleration</td>
			<td>full speed</td>
		</tr>
		<tr>
			<td><code>ease-out</code></td>
			<td><code>cubic-bezier(0, 0, 0.58, 1.0)</code></td>
			<td>full speed</td>
			<td>slow acceleration</td>
			<td>slow acceleration</td>
		</tr>
		<tr>
			<td><code>ease-in-out</code></td>
			<td><code>cubic-bezier(0.42, 0, 0.58, 1.0)</code></td>
			<td>slow acceleration</td>
			<td>full speed</td>
			<td>fast acceleration</td>
		</tr>
	</tbody>
</table>

Even though pre-defined values work well for many cases, knowing how to create custom **Cubic Bézier functions gives you even more control** over the look and feel of the animation which can make the animation look even more impressive and impactful.

{{% ad-panel-leaderboard %}}

In the following example, I’ve edited the animations for In Pieces example to use a different Cubic Bézier function with different values. You can see how vastly different the animation looks and feels with this easing function.

<pre><code class="language-css">cubic-bezier(0, 1.2, 1, 0.2)</code></pre>

{{< vimeo id="538900629" breakout="true" >}}

Let’s take a look at the `cubic-bezier` function which is used to define Cubic Bézier curves in CSS. Cubic Bézier function is defined by four points (x and y coordinate pairs), but we only define 2 points in `cubic-bezier` function. Why is that?

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ab6c48f-b1ea-4fad-8ce9-42112f2f70a7/09-easing-functions-css-animations-transitions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ab6c48f-b1ea-4fad-8ce9-42112f2f70a7/09-easing-functions-css-animations-transitions.png" width="289" height="332" sizes="100vw" caption="Cubic Bezier curve example for CSS animation. (Image source: <a href='https://developer.mozilla.org/en-US/docs/Web/CSS/easing-function'>MDN Web docs</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ab6c48f-b1ea-4fad-8ce9-42112f2f70a7/09-easing-functions-css-animations-transitions.png'>Large preview</a>)" alt="Cubic Bezier curve example for CSS animation." >}}

This is because the first (P0) and last points (P3) are fixed to the start (initial animation state) and the end (final animation state) of the curve, as the animation needs to end on a specified keyframe and within the specified duration. With the two remaining points (P1 and P2), we can fine-tune the curve and easing of the function, resulting with non-linear animation speed.

<pre><code class="language-css">cubic-bezier(x1, y1, x2, y2)</code></pre>

X coordinates (`x1` and `x2`) represent time ratio and are limited to values between 0 and 1 (the animation cannot begin sooner or last longer than specified), while Y coordinates (`y1` and `y2`) represent the animation output and their values, which are usually set somewhere between 0 and 1 but are not limited to that range. We can use the `y1` and `y2` values that are outside the 0 and 1 range to create bouncing effects.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98d8f477-6b54-49d7-93d0-103f23f31dc8/10-easing-functions-css-animations-transitions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98d8f477-6b54-49d7-93d0-103f23f31dc8/10-easing-functions-css-animations-transitions.png" width="800" height="375" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98d8f477-6b54-49d7-93d0-103f23f31dc8/10-easing-functions-css-animations-transitions.png'>Large preview</a>)" alt="animation with bouncing effects" >}}

If the animation consists of several keyframes, defined in CSS `@keyframes` property, the easing function will be applied to each curve between the two points. If we are applying `ease-out` function to an animation with 3 keyframes, the animation will accelerate at the start of the first keyframe, and decelerate near the second keyframe and the same motion will be repeated for the next pair of keyframes (second keyframe and the last keyframe).

{{< codepen height="265" theme_id="light" slug_hash="zYNbVME" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Cubic-bezier functions 2 keyframes](https://codepen.io/smashingmag/pen/zYNbVME) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

Notice how the easing function is repeated between each keyframe pair &mdash; first and second keyframes (first pair), and second keyframe and last keyframe (second pair). The animation duration is the same for both the previous and the following examples.

{{< codepen height="365" theme_id="light" slug_hash="KKaEjbM" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Cubic Bezier functions 3 keyframes](https://codepen.io/smashingmag/pen/KKaEjbM) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

Creating these functions can be a complex task, so you probably won’t be adjusting the coordinates by guessing the `cubic-bezier` parameters. You’ll have to use a tool to help you nail those magic numbers in order to create a timing function that perfectly fits your animation. Luckily, there are numerous browser and online tools to help us out. We’ll talk about them in one of the following sections in this article.

{{% ad-panel-leaderboard %}}

### Staircase Functions

Staircase functions enable animation to jump between the specific number of frames in a non-continuous way. You can think of it as a “ticking” animation.

For example, if we take a look at one of the previous examples where a box moves from 0px to 500px and we limit the animations to 5 steps, the animation will jump between the following 5 keyframes &mdash; 0px, 100px, 200px, 300px and 400px positions.

We can easily achieve this with `steps` function in CSS.

<pre><code class="language-css">steps(number_of_frames)</code></pre>

<pre><code class="language-css">steps(5)</code></pre>

This function has an additional option for controlling which keyframes are included. As you have seen from the previous example, the animation of a box moving from 0px to 500px with 5 steps will end in a 400px position. If we want the animation to start from 100px and end in a 500px position, we can use the **jump term** option as a second argument. Jump term affects how the keyframes will be selected from the animation timeline.

<pre><code class="language-css">steps(number_of_frames, jump_term)</code></pre>

<pre><code class="language-css">steps(5, jump-start)</code></pre>

Following jump term options can be used in CSS `steps` function:

- `jump-start`    
Animation jumps right from the starting point and the starting point is not visible t. From our example example, keyframes will be 100px, 200px, 300px, 400px, 500px.
- `jump-end`    
Last jump happens when animation ends and is not visible. From our example example, keyframes will be 0px, 100px, 200px, 300px, 400px.
- `jump-both`    
Both the first and last jump will happen as animation starts and ends respectively, so they won’t be visible. All 5 jumps will happen between staring and ending points. From our example, those keyframes will be 80px, 165px, 250px, 335px, 420px.
- `jump-none`    
Both first and last jump will be visible. From our example, those keyframes will be 0px, 125px, 250px, 375px, 500px.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ae6ded8-42b5-45ce-9921-2d27b8152bd9/011-easing-functions-css-animations-transitions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ae6ded8-42b5-45ce-9921-2d27b8152bd9/011-easing-functions-css-animations-transitions.png" width="525" height="487" sizes="100vw" caption="Timeline of step(5) animation with 1000ms duration. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ae6ded8-42b5-45ce-9921-2d27b8152bd9/011-easing-functions-css-animations-transitions.png'>Large preview</a>)" alt="Timeline of step (5) animation with 1000ms duration" >}}

The following example showcases how various jump terms affect the animation behavior. Various jump terms are applied to the 5-step animation with the same duration.

{{< codepen height="265" theme_id="light" slug_hash="ZELPdPK" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Step function](https://codepen.io/smashingmag/pen/ZELPdPK) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

## Debugging Animations And Useful Tools

As we’ve seen from the Cubic Bézier example, we need some kind of tool that will help us fine-tune the Cubic Bézier curve parameters so we can achieve the look and feel of the animation that we want.

In this section, we’ll take a look at the browser tools, websites, and CSS styles that should help us do just that.

### Browser Tools

Browser developer tools provide useful easing function editing features out of the box. Please note that only Cubic Bézier functions are available for editing. These tools offer a quick and simple animation preview so that the developer can get instant feedback and fine-tune the easing function.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03c061ce-0a29-4cda-9cda-441415f77691/12-easing-functions-css-animations-transitions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03c061ce-0a29-4cda-9cda-441415f77691/12-easing-functions-css-animations-transitions.png" width="800" height="240" sizes="100vw" caption="Chrome, Safari, Firefox. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03c061ce-0a29-4cda-9cda-441415f77691/12-easing-functions-css-animations-transitions.png'>Large preview</a>)" alt="Chrome, Safari, Firefox." >}}

[Chrome](https://developer.chrome.com/docs/devtools/css/animations/), [Safari](https://webkit.org/blog/10266/web-animations-in-safari-13-1/) and [Firefox](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Work_with_animations) also offer a dedicated Animations tab in developer tools that offers a more detailed overview, including animation properties, duration, timeline, keyframes, delay, etc.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d940149a-e4da-4a77-9af2-dedbd395a5d0/13-easing-functions-css-animations-transitions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d940149a-e4da-4a77-9af2-dedbd395a5d0/13-easing-functions-css-animations-transitions.png" width="800" height="221" sizes="100vw" caption="Chrome, Safari, Firefox. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d940149a-e4da-4a77-9af2-dedbd395a5d0/13-easing-functions-css-animations-transitions.png'>Large preview</a>)" alt="Chrome, Safari, Firefox." >}}

### Useful Tools And Websites

There are plenty of useful online resources and easing presets that can give much more variety to easing functions.

More popular online resources include [Easing Functions Cheat Sheet](https://easings.net/) by Andrey Sitnik and Ivan Solovev and [CSS Easing Animation Tool](https://matthewlein.com/tools/ceaser) by Matthew Lein. These tools offer a wide range of presets that you can use as a foundation for your easing function and then fine-tune the curve to fit your animation timeline.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02de9f56-5d84-4ef2-8a19-17fdfcaed801/14-easing-functions-css-animations-transitions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02de9f56-5d84-4ef2-8a19-17fdfcaed801/14-easing-functions-css-animations-transitions.png" width="800" height="432" sizes="100vw" caption="Easing Functions Cheat Sheet contains 30 useful function presets. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02de9f56-5d84-4ef2-8a19-17fdfcaed801/14-easing-functions-css-animations-transitions.png'>Large preview</a>)" alt="Easing Functions Cheat Sheet contains 30 useful Cubic Bézier function presets" >}}

## Animations & Accessibility

When working with easing functions and animations in general, it’s important to address accessibility requirements. [Some people](https://www.w3.org/WAI/WCAG21/Understanding/animation-from-interactions.html) prefer browsing the web with reduced motion, so we should provide a proper fallback. This can be easily done with widely-supported [prefers-reduced-motion](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion) media query. This media query allows us to either remove the animation or assign a different animation based on user preference.

<pre><code class="language-javascript">.animated-element {
  animation: /* Regular animation */;
}

@media (prefers-reduced-motion) {
  .animated-element {
    /* Accessible animation with reduced motion */
  }
}</code></pre>

I’ve modified an analog clock [example](https://codepen.io/alvaromontoro/pen/jGYQoP) by [Alvaro Montoro](https://codepen.io/alvaromontoro) to include alternative animation for users with `prefers-reduced-motion` flag set.

{{< codepen height="265" theme_id="light" slug_hash="QWdoXPN" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [CSS Analog Clock with prefers reduced motion](https://codepen.io/smashingmag/pen/QWdoXPN) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

On a default animation, the seconds hand of the clock is constantly moving which may cause difficulties for some users. We can easily make the animation much more accessible by changing the animation timing function to `steps`. In the following example, users with `prefers-reduced-motion` flag set will be displayed an animation where seconds arm ticks every five seconds. 

<pre><code class="language-javascript">@media (prefers-reduced-motion) {
  .arm.second {
    animation-timing-function: steps(12);
  }
}</code></pre>

{{< vimeo id="538919516" >}}

## Conclusion

Easing functions, or timing functions, change the animation’s look and feel by affecting the animation rate (speed). Easing functions enable us to create animations that resemble natural motion which can result in improved, more delightful UX and having a better impression on the users. We’ve seen how we can use pre-defined values like `linear`, `ease-out`, `ease`, etc. to quickly add a timing function and how to create custom easing functions with `cubic-bezier` function for more impressive and impactful animations. We’ve also covered staircase functions that can be used to create “ticking” animation and are rarely used. When creating animations, it’s important to keep accessibility in mind and provide an alternative, less distracting animations with less motion to users with `prefers-reduced-motion` flag set.

There are plenty of browser and online tools that can simplify and streamline creating custom easing functions, so creating animations with a beautiful flow is easier than ever. If you haven’t done so already, I would recommend experimenting with various easing functions and creating your own easing function library.

### References

- [`<easing-function>`](https://developer.mozilla.org/en-US/docs/Web/CSS/easing-function), MDN Web Docs
- “[Work With Animations](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Work_with_animations),” MDN Web Docs
- “[Web Animations In Safari 13.1](https://webkit.org/blog/10266/web-animations-in-safari-13-1/),” Antoine Quint, WebKit
- “[The Basics Of Easing](https://developers.google.com/web/fundamentals/design-and-ux/animations/the-basics-of-easing),” Paul Lewis, Web Fundamentals, Google Developers
- “[Inspect Animations](https://developer.chrome.com/docs/devtools/css/animations/),” Kayce Basques, Chrome DevTools, Chrome Developers

{{< signature "vf, yk, il" >}}

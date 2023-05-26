---
title: Upgrading CSS Animation With Motion Curves
slug: css-animations-motion-curves
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/128c3b65-7a3c-4a3c-9b0e-6eed2f955313/bezier-animation-demo-opt.png
date: 2016-08-25T18:58:24.000Z
author: nashvail
description: >-
  There is UI animation, and then there is _good_ UI animation. Good animation
  makes you go “Wow!” — it’s smooth, beautiful and, most of all, natural, not
  blocky, rigid or robotic. If you frequent Dribbble or
  [UpLabs](https://www.uplabs.com), you’ll know what I am talking about.

  With so many amazing designers creating such beautiful animations, any
  developer would naturally want to recreate them in their own projects. Now,
  CSS does provide some presets for
  [`transition-timing-function`](https://developer.mozilla.org/en/docs/Web/CSS/transition-timing-function),
  such as `ease-in`, `ease-out` and `ease-in-out`, which add some level of
  smoothness and realism, but they are very generic, aren’t they? How boring
  would it be if every animation on the web followed the same three timing
  functions?
categories:
  - CSS
  - Techniques
  - Animation
---
There is UI animation, and then there is _good_ UI animation. Good animation makes you go “Wow!” — it’s smooth, beautiful and, most of all, natural, not blocky, rigid or robotic. If you frequent Dribbble or [UpLabs](https://www.uplabs.com), you’ll know what I am talking about.</p>

## <span class="rh">Further Reading</span> on Smashing:

*   [SVG and CSS animations with clip-path](https://www.smashingmagazine.com/2015/12/animating-clipped-elements-svg/)
*   [Practical Animation Techniques](https://www.smashingmagazine.com/2015/06/practical-techniques-on-designing-animation/)
*   [Creating 'hand-drawn' Animations With SVG](https://www.smashingmagazine.com/2015/09/creating-cel-animations-with-svg/)
*   [The new Web Animation API](https://www.smashingmagazine.com/2014/11/the-state-of-animation-2014/)

With so many amazing designers creating such beautiful animations, any developer would naturally want to recreate them in their own projects. Now, CSS does provide some presets for [`transition-timing-function`](https://developer.mozilla.org/en/docs/Web/CSS/transition-timing-function), such as `ease-in`, `ease-out` and `ease-in-out`, which add some level of smoothness and realism, but they are very generic, aren’t they? How boring would it be if every animation on the web followed the same three timing functions?

<figure class="fwi"><div class="aspect-ratio">{{< vimeo 178888112 >}}<figcaption>(Credit: <a href="https://dribbble.com/LukasStranak">Lukáš Straňák</a>)</div></figure>

{{% feature-panel %}}

One of the properties of `transition-timing-function` is `cubic-bezier(n1, n2, n3, n4)`, in which you can pass four numbers to create your very own timing function. Towards the end of this article, you’ll know exactly what these four numbers represent — still, believe me, coming up with four numbers to capture the transition you are imagining in your head is nowhere close to being easy. But thanks to [`cubic-bezier`](https://cubic-bezier.com) and [Ceasar](https://matthewlein.com/ceaser/), you don’t have to. These tools bring motion curves to the web.</p>

<figure class="fwi"><div class="aspect-ratio">{{< vimeo 178895904 >}}</div></figure>

Motion curves are primarily used by animators (for example, in [Adobe After Effects](https://www.adobe.com/products/aftereffects.html)) to create advanced, realistic animations. With `cubic-bezier` and Ceasar, you can simply manipulate the shape of a curve, and those four numbers (`n1, n2, n3, n4`) will be filled in for you, which is absolutely great! Still, to use and make the most out of motion curves, you need to understand how they work, and that’s what we’re going to do in this article. Let’s begin.</p>

## Understanding Motion Curves

A motion curve is nothing but a plot between any [animatable property](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties) and time. A motion curve defines how the speed of an animation running under its influence varies over time.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79d2dfb3-e7fd-4283-a12d-038b9912edc7/css-animations-motion-curves-fig26-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79d2dfb3-e7fd-4283-a12d-038b9912edc7/css-animations-motion-curves-fig26-large-opt.png" width="500" height="375" alt="Motion curve is a plot between animatable property and time." /></a><figcaption>A motion curve is a plot between an animatable property and time. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79d2dfb3-e7fd-4283-a12d-038b9912edc7/css-animations-motion-curves-fig26-large-opt.png">View large version</a>)</figcaption></figure>

Let’s take [distance (`translateX`)](https://css-tricks.com/almanac/properties/t/transform/#article-header-id-3) as an example of an animatable property. (The explanation holds true for any other animatable property.)

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d5093df-827f-43c1-8ad7-88024011e483/css-animations-motion-curves-fig27-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d5093df-827f-43c1-8ad7-88024011e483/css-animations-motion-curves-fig27-large-opt.png" width="500" height="375" alt="Calculating speed at time t1 on a distance-time plot." /></a><figcaption>Calculating speed at time t1 on the distance-time plot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d5093df-827f-43c1-8ad7-88024011e483/css-animations-motion-curves-fig27-large-opt.png">View large version</a>)</figcaption></figure>

If you’ve had any experience with physics and basic calculus, you’ll know that deciphering speed from a distance-time graph is very simple. The first derivative of **distance as a function of time**, with respect to **time**, is speed, which means that an object following a distance-time curve would have greater speed in places where the curve is steep and lower in places where the curve is flatter. If you know how that works, great! You’re all set and can skip to the next section.

Now, I am aware that design and development is a diverse field, and not everyone has the same background. Perhaps the two paragraphs above were all jargon to you. Don’t fret. We’ll keep going and make sense of the jargon.

Consider the red box below. Let’s get a little callow here and call the red box “Boxy”; it’ll be easier to refer to it that way. All right, so Boxy is going to move from one edge of the screen to the other in a linear fashion, and we are going to analyze its motion.

One of the presets of `transition-timing-function` is `linear`. To make Boxy move, all we do is add the following class.</p>

<pre><code class="language-css"> .moveForward {
	transform: translateX(1000px);
}
</code></pre>

To control the animation, we would set the `transition` property for Boxy as follows:

<pre><code class="language-css">#boxy {
	width: 200px;
	height: 200px;
	background: red;
	transition-property: transform;
	transition-duration: 1s;
	transition-timing-function: linear;
}</code></pre>

That’s a very verbose way to specify `transition`. In reality, you will almost always find `transition` written in its shorthand form:

<pre><code class="language-css">#boxy {
	width: 200px;
	height: 200px;
	background: red;
	transition: transform 1s linear;
}</code></pre>

Let’s see it go.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2eadafa1-846f-43e3-ba6a-e0cd48f5621e/tnndmje.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2eadafa1-846f-43e3-ba6a-e0cd48f5621e/tnndmje.gif" alt="Boxy undergoing linear motion" /></a><figcaption>Box undergoing linear motion.</figcaption></figure>

Robotic, isn’t it? You could say that this motion feels robotic because it’s linear, which is a perfectly plausible answer. But could you explain why? We can see that setting `linear` results in robotic motion, but what exactly is happening behind the scene? That’s what we’ll figure out first; we’re going to get to the innards and understand why this motion feels robotic, blocky and not natural.

Let’s start by graphing Boxy’s motion to see if we can gain some insight. Our graph will have two axes, the first being distance, and the second time. Boxy covers a total distance of 1000 pixels (distance) in 1 second (time). Now, don’t get scared by all the math below — it’s very simple.

Here is our very simple graph, with the axes as mentioned.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98d5c3c3-44a8-4605-b4d0-6b11cc8ba361/css-animations-motion-curves-fig1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98d5c3c3-44a8-4605-b4d0-6b11cc8ba361/css-animations-motion-curves-fig1-large-opt.png" width="500" height="375" alt="Empty graph with axes" /></a><figcaption>Empty graph with axes (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98d5c3c3-44a8-4605-b4d0-6b11cc8ba361/css-animations-motion-curves-fig1-large-opt.png">View large version</a>)</figcaption></figure>

Right now, it’s empty. Let’s fill it up with some data.

To start off with, we know that at 0 seconds, when the animation has not yet started, Boxy is in its initial position (0 pixels). And after 1 second has passed, Boxy has travelled a total of 1000 pixels, landing at the opposite edge of the display.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea958ea0-8fcf-4fb3-b2b4-fc6e5da82999/css-animations-motion-curves-fig2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea958ea0-8fcf-4fb3-b2b4-fc6e5da82999/css-animations-motion-curves-fig2-large-opt.png" width="500" height="205" alt="Boxy's initial and final positions" /></a><figcaption>Boxy’s initial and final positions (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea958ea0-8fcf-4fb3-b2b4-fc6e5da82999/css-animations-motion-curves-fig2-large-opt.png">View large version</a>)</figcaption></figure>

Let’s plot this data on the graph.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f551841f-dfec-4605-b490-20e14caf5d41/css-animations-motion-curves-fig3-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f551841f-dfec-4605-b490-20e14caf5d41/css-animations-motion-curves-fig3-large-opt.png" width="500" height="375" alt="Graph with Boxy's initial and final positions plotted" /></a><figcaption>Graph with Boxy’s initial and final positions plotted (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f551841f-dfec-4605-b490-20e14caf5d41/css-animations-motion-curves-fig3-large-opt.png">View large version</a>)</figcaption></figure>

So far so good. But two data points are not enough — we need more. The following figure shows the positions of Boxy at different points of time (all thanks to my high-speed camera).</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b93380c0-214d-4ab7-9ece-c69b7b3981e3/css-animations-motion-curves-fig4-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b93380c0-214d-4ab7-9ece-c69b7b3981e3/css-animations-motion-curves-fig4-large-opt.png" width="500" height="205" alt="Boxy's positions at different points of time" /></a><figcaption>Boxy’s positions at different points of time (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b93380c0-214d-4ab7-9ece-c69b7b3981e3/css-animations-motion-curves-fig4-large-opt.png">View large version</a>)</figcaption></figure>

Let’s add this data to our graph.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7c6afdf-0849-44f2-9c4a-4bff0fd898c4/css-animations-motion-curves-fig5-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7c6afdf-0849-44f2-9c4a-4bff0fd898c4/css-animations-motion-curves-fig5-large-opt.png" width="500" height="375" alt="Graph with different positions plotted" /></a><figcaption>Graph with different positions plotted (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7c6afdf-0849-44f2-9c4a-4bff0fd898c4/css-animations-motion-curves-fig5-large-opt.png">View large version</a>)</figcaption></figure>

You could, of course, have many more data points for different times (for example, 0.375 seconds, 0.6 seconds, etc.) but what we have is enough to complete our graph. By joining all of the points, we have completed the graph. High five!

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05cb329e-0c21-496b-8776-c4d9e859c1a2/css-animations-motion-curves-fig6-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05cb329e-0c21-496b-8776-c4d9e859c1a2/css-animations-motion-curves-fig6-large-opt.png" width="500" height="375" alt="Final graph" /></a><figcaption>Final graph (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05cb329e-0c21-496b-8776-c4d9e859c1a2/css-animations-motion-curves-fig6-large-opt.png">View large version</a>)</figcaption></figure>

Cool, but what does this tell us? Remember that we started our investigation with the goal of understanding why Boxy’s linear motion feels unnatural and robotic? At a glance, this graph we’ve just constructed doesn’t tell us anything about that. We need to go deeper.

Keep the graph in mind and let’s talk for a minute about speed. I know you know what speed is — I’d just like to put it in mathematical terms. As it goes, the formula for speed is this:

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3685e683-d431-48d5-ac85-3d767fb01238/css-animations-motion-curves-fig7-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3685e683-d431-48d5-ac85-3d767fb01238/css-animations-motion-curves-fig7-large-opt.png" width="500" height="171" alt="Mathematical formula for speed" /></a><figcaption>Mathematical formula for speed (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3685e683-d431-48d5-ac85-3d767fb01238/css-animations-motion-curves-fig7-large-opt.png">View large version</a>)</figcaption></figure>

Therefore, if a car covers a distance of 100 kilometers in 1 hour, we say its speed is 100 kilometers per hour.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/329d8947-db03-4803-99f8-f922aadcda16/css-animations-motion-curves-fig8-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/329d8947-db03-4803-99f8-f922aadcda16/css-animations-motion-curves-fig8-large-opt.png" width="500" height="129" alt="Representing speed" /></a><figcaption>Representing speed (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/329d8947-db03-4803-99f8-f922aadcda16/css-animations-motion-curves-fig8-large-opt.png">View large version</a>)</figcaption></figure>

If the car doubles its speed, it will start covering double the distance (200 kilometers) in the same interval (1 hour), or, in other words, it will cover the original distance of 100 kilometers in half the time (0.5 hours). Make sense?

Similarly, if the car halved its speed (that is, slowed down by half), it would start covering a distance of 50 kilometers in the same interval (1 hour), or, in other words, it would cover the original distance of 100 kilometers in twice the time (2 hours).

Great! With that out of the way, let’s pick up where we left off. We were trying to figure out how the graph between distance and time can help us understand why Boxy’s linear motion feels robotic.

Hey, wait a second! We have a graph between distance and time, and speed can be calculated from distance and time, can’t it? Let’s try to calculate Boxy’s speed at different time intervals.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d740c26-10a9-4caa-99e0-149a0cfd84ff/css-animations-motion-curves-fig9-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d740c26-10a9-4caa-99e0-149a0cfd84ff/css-animations-motion-curves-fig9-large-opt.png" width="500" height="375" alt="Calculating speed at different intervals" /></a><figcaption>Calculating speed at different intervals (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d740c26-10a9-4caa-99e0-149a0cfd84ff/css-animations-motion-curves-fig9-large-opt.png">View large version</a>)</figcaption></figure>

Here, I’ve chosen three different time intervals: one near the start, one in the middle and one at the end near the final position. As is evident, at all three intervals, Boxy has exactly the same speed (s1 = s2 = s3) of 1000 pixels per second; that is, no matter what interval you choose in the graph above, you will find Boxy moving at 1000 pixels per second. Isn’t that odd? Things in real life don’t move at a constant speed; they start out slowly, gradually increase their speed, move for a while, and then slow down again before stopping, but Boxy abruptly starts with a speed of 1000 pixels per second, moving with the same speed and abruptly stopping at exactly the same speed. This is why Boxy’s movement feels robotic and unnatural. We are going to have to change our graph to fix this. But before diving in, we’ll need to know how changes to the speed will affect the graph drawn between distance and time. Ready? This is going to be fun.

Let’s double Boxy’s speed and see how the appearance of the graph changes in response. Boxy’s original speed, as we calculated above, is 1000 pixels per second. Because we have doubled the speed, Boxy will now be able to cover the distance of 1000 pixels in half the time — that is, in 0.5 seconds. Let’s put that on a graph.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb08b3e0-0104-4ddb-a0b7-6aef0fa7fd3a/css-animations-motion-curves-fig10-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb08b3e0-0104-4ddb-a0b7-6aef0fa7fd3a/css-animations-motion-curves-fig10-large-opt.png" width="500" height="375" alt="Graph showing double speed" /></a><figcaption>Graph showing double speed (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb08b3e0-0104-4ddb-a0b7-6aef0fa7fd3a/css-animations-motion-curves-fig10-large-opt.png">View large version</a>)</figcaption></figure>

What if we tripled the speed? Boxy now covers 1000 pixels in one third of the time (a third of a second).</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f710dc7-f013-4549-80bc-9de184aeb5cf/css-animations-motion-curves-fig11-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f710dc7-f013-4549-80bc-9de184aeb5cf/css-animations-motion-curves-fig11-large-opt.png" width="500" height="375" alt="Graph showing triple speed" /></a><figcaption>Graph showing triple speed (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f710dc7-f013-4549-80bc-9de184aeb5cf/css-animations-motion-curves-fig11-large-opt.png">View large version</a>)</figcaption></figure>

Hmm, notice something? Notice how, when the graph changes, the angle that the line makes with the time axis increases as the speed increases.

All right, let’s go ahead and halve Boxy’s speed. Halving its speed means that Boxy will be able to cover only 500 pixels (half the original distance) in 1 second. Let’s put this on a graph.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01cb3ea0-b3db-4407-a1a0-6287e9618185/css-animations-motion-curves-fig12-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01cb3ea0-b3db-4407-a1a0-6287e9618185/css-animations-motion-curves-fig12-large-opt.png" width="500" height="375" alt="Graph showing half speed" /></a><figcaption>Graph showing half speed (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01cb3ea0-b3db-4407-a1a0-6287e9618185/css-animations-motion-curves-fig12-large-opt.png">View large version</a>)</figcaption></figure>

Let’s slow down Boxy a little more, making the speed one third of the original. Boxy will be able to cover one third of the original distance in 1 second.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94c0aa66-2671-40ee-865e-ecfd241cac28/css-animations-motion-curves-fig13-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94c0aa66-2671-40ee-865e-ecfd241cac28/css-animations-motion-curves-fig13-large-opt.png" width="500" height="375" alt="Graph showing a third of the speed" /></a><figcaption>Graph showing a third of the speed (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94c0aa66-2671-40ee-865e-ecfd241cac28/css-animations-motion-curves-fig13-large-opt.png">View large version</a>)</figcaption></figure>

See a pattern? The line gets steeper and steeper as we increase Boxy’s speed, and starts to flatten out as we slow Boxy down.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be293f03-7f57-40a0-bff1-eb3bcc1808c4/css-animations-motion-curves-fig14-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be293f03-7f57-40a0-bff1-eb3bcc1808c4/css-animations-motion-curves-fig14-large-opt.png" width="500" height="375" alt="Line gets steeper as speed increases and flattens out as speed decreases" /></a><figcaption>Line gets steeper as speed increases and flattens out as speed decreases. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be293f03-7f57-40a0-bff1-eb3bcc1808c4/css-animations-motion-curves-fig14-large-opt.png">View large version</a>)</figcaption></figure>

This makes sense because, for a steeper line, a little progress in time produces a much higher change in distance, implying greater speed.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89e4a6e7-6ee2-4b3c-938a-78c9ca9fe3d0/css-animations-motion-curves-fig15-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89e4a6e7-6ee2-4b3c-938a-78c9ca9fe3d0/css-animations-motion-curves-fig15-large-opt.png" width="500" height="375" alt="A small change in time produces a relatively large change in distance, making for a steeper graph." /></a><figcaption>A small change in time produces a relatively large change in distance, making for a steeper graph. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89e4a6e7-6ee2-4b3c-938a-78c9ca9fe3d0/css-animations-motion-curves-fig15-large-opt.png">View large version</a>)</figcaption></figure>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7562361-f8fd-4097-ab69-d7ea571e0be5/css-animations-motion-curves-fig16-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7562361-f8fd-4097-ab69-d7ea571e0be5/css-animations-motion-curves-fig16-large-opt.png" width="500" height="202" alt="A small change in time produces a relatively large change in distance, making for a steeper graph." /></a><figcaption>A small change in time produces a relatively large change in distance, making for a steeper graph. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7562361-f8fd-4097-ab69-d7ea571e0be5/css-animations-motion-curves-fig16-large-opt.png">View large version</a>)</figcaption></figure>

On the other hand, for a line that is less steep, a large change in time produces only a little change in distance, meaning a lower speed.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaa390a2-ed81-4f37-8848-c7b47ce47f41/css-animations-motion-curves-fig17-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaa390a2-ed81-4f37-8848-c7b47ce47f41/css-animations-motion-curves-fig17-large-opt.png" width="500" height="375" alt="Change in time verus change in distance in a graph that is less steep" /></a><figcaption>Change in time versus change in distance in a graph that is less steep (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaa390a2-ed81-4f37-8848-c7b47ce47f41/css-animations-motion-curves-fig17-large-opt.png">View large version</a>)</figcaption></figure>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51fbd981-b7c2-42f3-bc73-fe0c2e84bee8/css-animations-motion-curves-fig18-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51fbd981-b7c2-42f3-bc73-fe0c2e84bee8/css-animations-motion-curves-fig18-large-opt.png" width="500" height="202" alt="Change in time versus change in distance in a graph that is less steep" /></a><figcaption>Change in time versus change in distance in a graph that is less steep (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51fbd981-b7c2-42f3-bc73-fe0c2e84bee8/css-animations-motion-curves-fig18-large-opt.png">View large version</a>)</figcaption></figure>

With all of the changes we have made, Boxy is still moving in a linear fashion, just at different speeds. However, with our newly gained knowledge of how changes to distance versus time can affect speed, we can experiment and draw a graph that makes Boxy move in a way that looks natural and realistic.

Let’s take it step by step. First, things in real life start out slow and slowly increase in speed. So, let’s do that.

In all of the iterations of the graph shown below, you will notice that the points at opposite corners remain fixed. This is because we are not changing the duration for which the animation runs, nor are we changing the distance that Boxy travels.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66c454b6-80e7-48ee-bd6d-123c04279d09/css-animations-motion-curves-fig19-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66c454b6-80e7-48ee-bd6d-123c04279d09/css-animations-motion-curves-fig19-large-opt.png" width="500" height="375" alt="Constructing a custom motion curve" /></a><figcaption>Constructing a custom motion curve (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66c454b6-80e7-48ee-bd6d-123c04279d09/css-animations-motion-curves-fig19-large-opt.png">View large version</a>)</figcaption></figure>

If Boxy is to follow the graph above, it will move at a slower speed for 0.25 seconds, because the line is less steep starting from 0 to 0.25 seconds, and then it will abruptly switch to a higher speed after 0.25 seconds (the reason being that the line in the graph gets steeper after 0.25 seconds). We will need to smoothen this transition, though; we don’t want any corners — it’s called a motion _curve_, after all. Let’s convert that corner to a curve.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92e09258-711a-42b6-b404-123faacde14f/css-animations-motion-curves-fig20-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92e09258-711a-42b6-b404-123faacde14f/css-animations-motion-curves-fig20-large-opt.png" width="500" height="375" alt="Constructing a custom motion curve" /></a><figcaption>Constructing a custom motion curve (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92e09258-711a-42b6-b404-123faacde14f/css-animations-motion-curves-fig20-large-opt.png">View large version</a>)</figcaption></figure>

Notice the smooth transition that Boxy undergoes from being at rest to gradually increasing in speed.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae327f6e-0792-47eb-8899-b038dd6952e4/xs6l6ow.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae327f6e-0792-47eb-8899-b038dd6952e4/xs6l6ow.gif" alt="Boxy following the motion curve above" /></a><figcaption>Box following the motion curve above (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae327f6e-0792-47eb-8899-b038dd6952e4/xs6l6ow.gif">View large version</a>)</figcaption></figure>

Good! Next, objects in real life progressively slow down before stopping. Let’s change the graph to make that happen. Again, we’ll pick up a point in time after which we would like Boxy to start slowing down. How about around 0.6 seconds? I have smoothened out the transition’s corner to a curve here already.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1d0e42b-17c5-4c57-a6ce-e167349f7ff4/css-animations-motion-curves-fig21-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1d0e42b-17c5-4c57-a6ce-e167349f7ff4/css-animations-motion-curves-fig21-large-opt.png" width="500" height="375" alt="Final custom motion curve" /></a><figcaption>Final custom motion curve (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1d0e42b-17c5-4c57-a6ce-e167349f7ff4/css-animations-motion-curves-fig21-large-opt.png">View large version</a>)</figcaption></figure>

Look at Boxy go! A lot more natural, isn’t it?

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ca2295b-e2f2-4dc1-8f6d-8ef22205362b/ii5mrff.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ca2295b-e2f2-4dc1-8f6d-8ef22205362b/ii5mrff.gif" alt="Boxy following the custom motion curve" /></a><figcaption>Boxy following the custom motion curve (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ca2295b-e2f2-4dc1-8f6d-8ef22205362b/ii5mrff.gif">View large version</a>)</figcaption></figure>

The curve we drew in place of the corner is actually a collection of many small line segments; and, as you already know, the steeper the line on the graph, the higher the speed, and the flatter the line, the slower the speed. Notice how in the left part of the image, the line segments that make up the curve get steeper and steeper, resulting in a gradual increase in speed, and progressively flatten out on the right side, resulting in the speed progressively decreasing?

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf0c65b-479f-496e-adec-ec38a3b4dfad/css-animations-motion-curves-fig22-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf0c65b-479f-496e-adec-ec38a3b4dfad/css-animations-motion-curves-fig22-large-opt.png" width="500" height="128" alt="A curve is nothing but a collection of many line segments." /></a><figcaption>A curve is nothing but a collection of many line segments. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf0c65b-479f-496e-adec-ec38a3b4dfad/css-animations-motion-curves-fig22-large-opt.png">View large version</a>)</figcaption></figure>

With all of this knowledge, making sense of motion curves becomes much easier. Let’s look at a few examples.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8147bd3-b313-4791-a031-c823d8a4a214/css-animations-motion-curves-fig23-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8147bd3-b313-4791-a031-c823d8a4a214/css-animations-motion-curves-fig23-large-opt.png" width="500" height="375" alt="" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8147bd3-b313-4791-a031-c823d8a4a214/css-animations-motion-curves-fig23-large-opt.png">(View Large version)</a></figcaption></figure>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/546bc656-aff9-4720-8e68-a5861a9c9bb2/ij44ebg.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/546bc656-aff9-4720-8e68-a5861a9c9bb2/ij44ebg.gif" alt="Example 1" /></a><figcaption>Example 1 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/546bc656-aff9-4720-8e68-a5861a9c9bb2/ij44ebg.gif">View large version</a>)</figcaption></figure>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39a01bb1-e052-4947-8c32-74b81f0f386b/css-animations-motion-curves-fig24-large-opt-78x59.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39a01bb1-e052-4947-8c32-74b81f0f386b/css-animations-motion-curves-fig24-large-opt-78x59.png" width="500" height="375" alt="" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39a01bb1-e052-4947-8c32-74b81f0f386b/css-animations-motion-curves-fig24-large-opt-78x59.png">(View Large version)</a></figcaption></figure>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf1131cc-b30e-41f0-9362-28fb4f793a30/f4ve4xl.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf1131cc-b30e-41f0-9362-28fb4f793a30/f4ve4xl.gif" alt="Example 2" /></a><figcaption>Example 2 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf1131cc-b30e-41f0-9362-28fb4f793a30/f4ve4xl.gif">View large version</a>)</figcaption></figure>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ea3a8fb-2e6a-46a1-b38f-6740831161dd/css-animations-motion-curves-fig25-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ea3a8fb-2e6a-46a1-b38f-6740831161dd/css-animations-motion-curves-fig25-large-opt.png" width="500" height="375" alt="" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ea3a8fb-2e6a-46a1-b38f-6740831161dd/css-animations-motion-curves-fig25-large-opt.png">(View Large version)</a></figcaption></figure>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59a49d02-7773-4f9d-8c85-7ab249c9d105/a0yyl8i.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59a49d02-7773-4f9d-8c85-7ab249c9d105/a0yyl8i.gif" alt="Example 3" /></a><figcaption>Example 3 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59a49d02-7773-4f9d-8c85-7ab249c9d105/a0yyl8i.gif">View large version</a>)</figcaption></figure>

## Using Motion Curves In UI Animation

The next time you have to animate a UI element, you will have the power of motion curves at your disposal. Whether it’s a slide-out bar, a modal window or a dropdown menu, adding the right amount of animation and making it look smooth and natural will increase the quality of your user interface greatly. It will make the user interface just _feel_ good. Take the slide-out menu below:

{{< codepen height="350" caption="A Pen by Nash Vail (<a href='https://codepen.io/nashvail'>@nashvail</a>)." theme_id="8287" slug_hash="qNYmLG" default_tab="result" user="nashvail" >}}See the Pen <a href='https://codepen.io/nashvail/pen/qNYmLG/'>nJial</a> by Nash Vail (<a href='https://codepen.io/nashvail'>@nashvail</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}

Clicking on the hamburger menu brings in the menu from left, but the animation feels blocky. Line 51 of the CSS shows that the animation has `transition-timing-function` set to `linear`. We can improve this. Let’s head on over to [cubic-bezier](https://cubic-bezier.com) and create a custom timing function.

If you’re reading this, it’s safe to assume that you’re a designer or a developer or both and, hence, no stranger to cubic bezier curves; there’s a good chance you’ve encountered them at least once. Bezier curves are a marvel. They are used primarily in computer graphics to draw shapes and are used in tools such as [Sketch](https://www.sketchapp.com/) and [Adobe Illustrator](https://www.adobe.com/in/products/illustrator.html) to draw vector graphics. The reason why cubic bezier curves are so popular is that they are so easy to use: Just modify the positions of the four different points, and create the kind of curve you need.

Because we always know the initial and final states of the animated object, we can fix two of the points. That leaves just two points whose positions we have to modify. The two fixed points are called anchor points, and the remaning two are control points.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48aaf223-70d6-44ba-ab39-105e93717097/css-animations-motion-curves-fig28-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48aaf223-70d6-44ba-ab39-105e93717097/css-animations-motion-curves-fig28-large-opt.png" width="500" height="375" alt="Parts of a bezier curve" /></a><figcaption>Parts of a bezier curve (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48aaf223-70d6-44ba-ab39-105e93717097/css-animations-motion-curves-fig28-large-opt.png">View large version</a>)</figcaption></figure>

As you remember, `cubic-bezier` accepts four numbers (`n1, n2, n3, n4`) when you create a custom `transition-timing-function`. These four numbers represent nothing but the positions of the two control points: `n1, n2` represents the x and y coordinates of the first control point, and `n3, n4` represents the coordinates of the second control point. Because changing the position of the control points will change the shape of the curve and, hence, our animation overall, the result is the same when any or all of `n1, n2, n3, n4` is modified. For example, the figure below represents `cubic-bezier(.14, .78, .89, .35)`:

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffcabcf6-1f7d-4f6b-8838-2c920bfe6f84/css-animations-motion-curves-fig29-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffcabcf6-1f7d-4f6b-8838-2c920bfe6f84/css-animations-motion-curves-fig29-large-opt.png" width="500" height="375" alt="A cubic bezier curve representing (.14, .78, .89, .35)." /></a><figcaption>A cubic bezier curve representing <code>(.14, .78, .89, .35)</code> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffcabcf6-1f7d-4f6b-8838-2c920bfe6f84/css-animations-motion-curves-fig29-large-opt.png">View large version</a>)</figcaption></figure>

The [math behind these seemingly simple curves](https://medium.freecodecamp.com/nerding-out-with-bezier-curves-6e3c0bc48e2f#.113c4usq9) is fascinating.

All right, all right, let’s get back to where we were going with [cubic-bezier](https://cubic-bezier.com): creating a custom `transition-timing-function`. I want the kind of animation in which the menu slides in very quickly and then gracefully slows down and ends:

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b7bbb79-6a99-4a32-bdd5-dca56c6426b0/bezierdemo.gif"><img data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70d36fef-bace-4145-b63d-e018755ae318/ezgif-1175095003.gif" width="500" height="230" alt="Adjusting the cubic bezier curve" /></a><figcaption>Adjusting the cubic bezier curve (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b7bbb79-6a99-4a32-bdd5-dca56c6426b0/bezierdemo.gif">View large version</a>)</figcaption></figure>

This looks good. The animation will start out fast and then slow down, rather than move at a constant speed throughout. I am simply going to copy `cubic-bezier(.05, .69, .14, 1)` from the top of the page and replace `linear` with it.

{{< codepen height="350" caption="A Pen by Nash Vail (<a href='https://codepen.io/nashvail'>@nashvail</a>)." theme_id="8287" slug_hash="rLvymO" default_tab="result" user="nashvail" >}}See the Pen <a href='https://codepen.io/nashvail/pen/rLvymO/'>nJial</a> by Nash Vail (<a href='https://codepen.io/nashvail'>@nashvail</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}

See the difference? The second iteration feels much more natural and appealing. Imagine if every animation in your UI followed a natural timing function. How great would that be?

As we’ve seen, motion curves aren’t tricky at all. They are very easy to understand and use. With them, you can take your UI to the next level.

I hope you’ve learned how motion curves work. If you were going through a lot of trial and error to get motion curves to work the way you want, or if you were not using them at all, you should now be comfortable bending them to your will and creating beautiful animations. Because, after all, animation matters.

{{< signature "al" >}}


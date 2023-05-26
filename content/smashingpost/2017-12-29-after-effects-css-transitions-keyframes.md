---
title: 'Making The Transition From After Effects To CSS Transitions And Keyframes'
slug: after-effects-css-transitions-keyframes
image:
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90f47af2-7298-4634-a602-5dd2972d2fc5/animated-red-ball-opt.png
date: 2017-12-29T13:05:22+01:00
author: christopherng
description: >-
  As web developers, we need a good foundation to create animations that are both performant and maintainable, which is paramount to the native web app landscape. In this article find out how to go from After Effects to CSS transitions, animations and keyframes.
summary: >-
  As web developers, we need a good foundation to create animations that are both performant and maintainable, which is paramount to the native web app landscape. In this article find out how to go from After Effects to CSS transitions, animations and keyframes.
categories:
  - JavaScript
  - Animation
  - CSS
---
Websites are looking more and more like mobile apps. Users are also increasingly expecting a more app-like experience. From push notifications to offline mode, native web apps are getting there.

Once web apps function like native apps, the design interactions would also change to address the use case — namely, the ubiquity of animations. Animations drive interactions in all of our favourite apps, from Uber to Lyft and Snapchat to Instagram.</p>

<div class="c-felix-the-cat">
<h4 class="h3">Practical Techniques On Designing Animation</h4>
<p>What happens when a button has been activated? Does the user have to wait, not knowing if the form worked? A button with a loader could keep the viewer engaged while data is loaded in the background. <a href="/2015/06/practical-techniques-on-designing-animation/" class="btn btn--medium btn--blue">Read a related article →</a></p>
</div>

As web developers, we need a good foundation to create animations that are both performant and maintainable, which is paramount to the native web app landscape. We need to be able to go from After Effects to CSS transitions, animations and keyframes.</p>

## What Is After Effects?

After Effects is an industry-standard product from Adobe used by graphic and motion designers to key, compose and track animations. It is the _de facto_ tool used by many designers to communicate ideas to a team by exporting the animation layers into an easy-to-visualize sample video, with a reference table of the animation start and end times to accompany it.

Together, the demo video and the reference table give the development team a good baseline for how to implement the animation. The video is used to see the overall picture, while the reference table provides the minute details that make or break the animation interaction.

{{% feature-panel %}}

### Things We Can Do With After Effects

What we can create with After Effects is limited only by our imagination. It can provide an endless number of post-production effects for an image or video. In the scope of the web, it provides a platform for ideas to be shared.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/583d56e7-4e32-4c7e-aaec-937337ef6095/movement.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/583d56e7-4e32-4c7e-aaec-937337ef6095/movement.gif" width="720" height="200" alt="Red ball moving from left to right." /></a><figcaption>Demonstration of an animation done using After Effects.
</figcaption></figure>

Consider the red ball above. The ball is animated using After Effects to slowly roll to the middle, pause for a second, and then slowly accelerate to exit the viewport. The classic web animations of movement, scaling, rotation and even color change are easily done in After Effects and serve as an instantly generated requirements document (or video or GIF) for the animations to be implemented.</p>

## Tools You Need To Get Started

With JavaScript, HTML5, CSS3 and many other languages becoming standard across most major user agents that a website receives traffic from, using these tools wholesale is becoming increasingly feasible. Below are some key technologies to keep in mind when implementing animations.</p>

### CSS Transitions

CSS transitions provide a way to control how fast a change in CSS property is applied to an element. Instead of applying a style immediately (without transitions), it could be applied gradually over a defined acceleration curve using customization rules. An example would be changing a background color from black to white over a period of time.</p>

<pre><code class="language-css">transition-property: background-color;
transition-duration: 3s;</code></pre>

With this rule on the element, the background color would take three seconds to change, gradually changing from black to white, going through shades of gray. This can further be customized by adding [transition-timing-function](https://www.smashingmagazine.com/2016/08/css-animations-motion-curves), to calculate intermediate values, and [transition-delay](https://www.smashingmagazine.com/2014/04/understanding-css-timing-functions/), to delay the start of the animation.

CSS transitions are good for **simple interactions**, such as changing the background color or moving an element to a new location.</p>

### Using CSS Animations

CSS animations provide even finer control over the intermediate steps between an animation, using waypoints. Waypoints (or keyframes) are pinned points in time, during the animation, when we apply certain styles to an element. We then use the defined keyframes to lay out what the animation should look like.

Suppose we want an element to animate as a bounce. The element needs to move up, move back to the original position, move back up a little, and then move back to the original position. Using keyframes, we can break down that elastic effect into percentages of time that the animation will take.</p>

<pre><code class="language-css">@keyframes bounce {
  0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
  40% { transform: translateY(-25px); }
  60% { transform: translateY(-15px); }
}

.element {
  animation-name: bounce;
  animation-duration: 3s;
}</code></pre>

As with CSS transitions, there are plenty of options for developers to configure. We can make animations repeat indefinitely using `animation-iteration-count`, with the value `infinite`, or even control the direction in which the animation flows, using the property `animation-direction`. Plenty of [CSS animation properties](https://www.smashingmagazine.com/2011/09/the-guide-to-css-animation-principles-and-examples/) give us fine-grained control to match an animation to the design.

CSS animations are useful for **short repeating animations**, such as expansion, rotation and bounces.</p>

### Using JavaScript

JavaScript has a multitude of uses, from Raspberry Pi servers to client-side code, but one of its core uses remains changing class names on elements. Changing a class name is a trivial yet effective way to manage the state of an element.

An example is the simple addition of an `active` class that signals an initially hidden component to start animating. Consider the ball below. We use JavaScript to add a class that triggers the animation using CSS transition properties.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9fff0d3-db02-4363-8235-b637991b1f90/scaling.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9fff0d3-db02-4363-8235-b637991b1f90/scaling.gif" width="720" height="200" alt="Red ball increasing scale in size and then decreasing back to its original size." /></a><figcaption>A red ball animates by increasing in size and then decreasing back to its original size.
</figcaption></figure>

The first part of this animation can be replicated using a simple combination of HTML, CSS and JavaScript.

HTML:

<pre><code class="language-markup">&lt;div class="ball"&gt;&lt;/div&gt;</code></pre>

CSS:

<pre><code class="language-css">.ball {
  width: 100px;
  height: 100px;
  color: red;
  transform: scale(0.25);
  transition: all 1s ease-in;
}

.ball.active {
  transform: scale(1.25);
}</code></pre>

JavaScript:

<pre><code class="language-javascript">setTimeout(function() {
  document.querySelector('.ball').addClass('active');
}, 500);</code></pre>

When the timeout (of `500ms`) expires, a class of `active` is added to the ball `div`, which changes the `transform` property, which then triggers the `transition` property, which is watching the `transform` property on the ball element. Changing CSS classes using JavaScript not only helps us to manage the state of a component, but also gives us further control over animations [beyond CSS animations and transitions](https://www.smashingmagazine.com/2014/11/the-state-of-animation-2014/).

Controlling animations using JavaScript is beneficial for **managing state**, to trigger events based on dynamic factors such as user input or application state.

## From Idea To After Effects To CSS And JavaScript

Imagine we had a task in which we had to animate an element on the page. Let’s make this element a red ball. The ball would have to rotate around the page, as well as scale up and down.

After Effects allows us to create mockups of what the interaction would look like when the animation is triggered. The ball in motion below is an example of that. Notice how the red ball first slightly scales up, then begins accelerating around a circular loop and decelerates back into its original position. Only then does the ball scale down to its original size.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f891eb0-3d3b-49f8-821c-6ac1bdc0d16c/rotation.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f891eb0-3d3b-49f8-821c-6ac1bdc0d16c/rotation.gif" width="720" height="200" alt="Red ball rotating around in a circle." /></a><figcaption>A red ball animates by increasing in size, moving around in a circle, and then decreasing back to its original size.
</figcaption></figure>

Consider the shift in scale above where the ball grows or shrinks before moving or stopping. This is a tiny feature that the designer has crafted in After Effects and needs to be communicated to the developer clearly so that the minute details are not missed.

That is why some preparation would need to be done before going from After Effects to the developer. We couldn’t simply create a video file of the animation in action, share it with the developer and call it a day.

One way to convey our ideas clearly is to create a **spreadsheet detailing the steps** needed for the animation. Depending on the complexity of the animation, it could be simple scribbles on a ticket, a text file containing a list or a full-blown spreadsheet.</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
  <tr>
    <th data-tablesaw-priority="persist">Step</th>
    <th>Animation</th>
    <th>Time</th>
    <th>Details</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>1</td>
    <td>Ball scales up</td>
    <td>1 second</td>
    <td>Scale 1.25 with shadow</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Ball moves in a circle</td>
    <td>2 seconds</td>
    <td>Scale 1.25 with a radius of 25 pixels</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Ball scales down</td>
    <td>1 second</td>
    <td>Scale back to 1</td>
  </tr>
</tbody>
</table>

Another way to convey information about the animation is to **embed it in the video** itself. You can do this right in After Effects, adding crucial information such as how much to scale, the number of steps and other information as it is happening, to give context to the implementer. This enables us to use the **demo video as a universal source of truth**.

This exported video file from After Effects acts as a form of a contract between designer and developer. With a common understanding in place, we can use the tools discussed to implement it — namely, CSS classes, JavaScript events, CSS transitions, CSS animations and JavaScript animations.</p>

### 1\. Break Down The Animation

**Look for patterns and note the timings.**

The first thing to do is draw the timeline of the animations for each of the elements (or group of elements). We need to understand where animations intersect in order to synchronize the timing and animation lifecycle around them. Planning is key to a complex animation, so that we can incrementally build our solution in a maintainable way for future requirements.

From the information above, we break it down as the following steps:

1.  Initialize the component and wait for a trigger.
2.  Once triggered, scale up in size and expand the drop shadow.
3.  After that, move around in a circle with `ease-in-out`.
4.  Then, scale down in size and decrease the drop shadow.

The benefit of outlining is that we understand which components must live outside of the animating elements — for example, the drop shadow must be independent of the ball. Similar to outlining an essay, breaking down the animation organizes our thoughts on the work we have to do. **Outlines demonstrate the thinking process** behind an animation and doubly serves as documentation for our work.</p>

### 2\. Negotiate With Stakeholders

Can we simplify some areas? Which parts of the animation are a must? Can we synchronize timings?

Once we have investigated the work needed to accomplish the task, we bargain. Bargaining with the designer and the product owner is every developer’s responsibility. The implementer has a complete understanding of the key low-hanging fruit, what can be done and what is not practical to do.

Animation is tricky because removing seemingly minute details from an animation could change the user experience. To give a development-based example, changing how an animation behaves is akin to changing the response payload we might receive from an API call: Certain things could be changed, but some parts must be there.

This is a case-by-case situation, based on our relationship with the designer, as well as with the product owner given the timeline for launching. Asking for certain animations to be removed is not recommended because this would be beyond our area of expertise.

A good approach to bargaining would be to synchronize timings or to **simplify animations that the browser might not be capable of doing natively**, and avoiding animations that use JavaScript because they would be hard to maintain and could result in janky performance. We can and should ask for these concessions instead.</p>

### 3\. Plan The Attack

Know what the start and end state of each element should be. Look at where each transition timing is supposed to happen. Leverage BEM in CSS classes to apply animations clearly. Understand the reasons why JavaScript should be limited in favor of CSS.

Let’s examine the animation described earlier. Five states jump out at us:

1.  the initial state, with the red ball and some drop shadow;
2.  the scaled-up version of the ball with a longer drop shadow;
3.  the movement of the ball around a circle;
4.  scaling down of the ball, along with its drop shadow;
5.  the return to the initial state, waiting to be triggered.

For all five states, we should look at what the style is before and what it should be after. This will provide us with information on what kind of animation tools we would need in order to implement it.

To do this, we start with the base case style. This could be nothing, if the element appears out of nowhere, or it could be the previous style, in the case of chained animations.</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
  <tr>
    <th data-tablesaw-priority="persist">State</th>
    <th>Class names</th>
    <th>Duration</th>
    <th>Animation timing</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>1</td>
    <td>ball</td>
    <td>(n/a, waiting for trigger)</td>
    <td>n/a</td>
  </tr>
  <tr>
    <td>2</td>
    <td>ball, ball--scale-up</td>
    <td>1 second</td>
    <td>ease-out</td>
  </tr>
  <tr>
    <td>3</td>
    <td>ball, ball--scale-up, ball--circling</td>
    <td>2 second</td>
    <td>ease-in-out</td>
  </tr>
  <tr>
    <td>4</td>
    <td>ball, ball-scale-up, ball--circling, ball--scale-down</td>
    <td>1 second</td>
    <td>ease-in</td>
  </tr>
  <tr>
    <td>5</td>
    <td>ball</td>
    <td>(n/a, waiting for trigger)</td>
    <td>n/a</td>
  </tr>
</tbody>
</table>

**Keep it simple** by having very few changes in styles between states. Once we have identified the start and end states, we need to label them as CSS classes, so that they can be applied to the element easily. This gives us the flexibility to use JavaScript to handle the application of classes based on data received from AJAX calls that the element might depend on.

[BEM CSS](https://getbem.com/) is ideal for our naming strategy because of how we would represent the states of our animations in progress with modifiers. If the animation is generic enough, BEM is also a good methodology to maintain [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) (“don't repeat yourself”) CSS classes that work across code bases. We’d start off with just the block and element markers and then layer in modifiers as we progress through the animation.

Here is a sample template class journey:

<pre><code class="language-markup">// State 1
&lt;div class="ball"&gt;&lt;/div&gt;
// State 2
&lt;div class="ball ball--scale-up"&gt;&lt;/div&gt;
// State 3
&lt;div class="ball ball--scale-up ball--circling"&gt;&lt;/div&gt;
// State 4
&lt;div class="ball ball--scale-up ball--circling ball--scale-down"&gt;&lt;/div&gt;
// State 5
&lt;div class="ball"&gt;&lt;/div&gt;</code></pre>

We start off with the container element with the class ball, which would represent the red ball we are animating. As the **animation iterates across the experience, so too do our BEM class names**, from scaling up to moving in a circle. This is a method to keep track of what the element is supposed to look like when the styles are applied.</p>

### 4\. Steady Implementation

With an outline on hand and tools ready to use, we should chip away at the project state by state.

We can iteratively tackle each state as a separate item, building upon the previous state as needed. With each state clearly defined, we can focus more on making our code DRY and easy to read, rather than on details of implementation. And, of course, it would be nice to add tests to cover our logic.

**Initial State**

We start with a simple red ball, with a slight drop shadow.</p>

<pre><code class="language-css">.ball {
  background-color: #D24D57;
  width: 25px;
  height: 25px;
  margin: 5px;
  display: inline-block;
  border-radius: 50%;
  box-shadow: 0 8px 6px -6px #6C7A89;
}</code></pre>

**Scaling Up**

There are two parts to scaling up: the size of the element and its drop shadow. We use a keyframe, named `scale`, that is shared by both the scaling up and down for DRY-ness to handle this animation.</p>

<pre><code class="language-css">@keyframes ball-scale {
  from {
    transform: scale(1);
    box-shadow: 0 8px 6px -6px #6C7A89;
  }
  to {
    transform: scale(1.25);
    box-shadow: 0 10px 6px -6px #6C7A89;
  }
}

.ball--scale-up {
  animation: ball-scale 1s ease-out forwards;
}</code></pre>

**Circling (After Scaling-Up Animation Is Applied)**

We use a keyframe, named `circular`, as well as move its `transform-origin` property to move the element around in a circle, starting from the beginning. Keep in mind that circling only happens when the scaling-up animation has completed.</p>

<pre><code class="language-css">@keyframes ball-circular {
  from {
    box-shadow: 0 10px 6px -6px #6C7A89;
    transform-origin: 50% -450%;
    transform: scale(1.25) rotate(0deg) translateY(-100%) rotate(0deg);
  }
  to {
    box-shadow: 0 10px 6px -6px #6C7A89;
    transform-origin: 50% -450%;
    transform: scale(1.25) rotate(360deg) translateY(-100%) rotate(-360deg);
  }
}

.ball--circling {
  animation: ball-circular 2s ease-in-out forwards;
}</code></pre>

**Scaling Down (After Circling and Scaling-Up Animations Are Applied)**

To scale down, we reuse the keyframe scale, with `animation-direction: reverse` to do the opposite of what the scale-up class does. This brings us back to our original state.</p>

<pre><code class="language-css">.ball--scale-down {
  animation: ball-scale 1s ease-in forwards;
  animation-direction: reverse;
}</code></pre>

**Working Demo**

If we combine all of these classes into a sequence, we would have a CSS representation of the rendering done in After Effects.

Click on the ball to start.</p>

<p data-height="265" data-theme-id="0" data-slug-hash="LzbeeB" data-default-tab="result" data-user="chrisrng" data-embed-version="2" data-pen-title="Animating Ball" class="codepen">See the Pen <a href="https://codepen.io/chrisrng/pen/LzbeeB/">Animating Ball</a> by Chris Ng (<a href="https://codepen.io/chrisrng">@chrisrng</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

## Conclusion

The tools covered in this article are hardly cutting-edge, but they are generally supported across most major browsers, which makes them usable today.

Previously, implementing animations was hard because it meant using external tools such as [jQuery Animate](https://api.jquery.com/animate/) to do simple things such as moving elements around on the page. Today, CSS transitions and animations can be done natively and efficiently, [leveraging the GPU](https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/).

Animations are always a tug of war between developer, designer and product owner. The trick is to find the middle ground, where all stakeholders are happy with the quality of the product. Hopefully, this guide will help you make that transition.

{{< signature "rb, yk, al, ra, il" >}}


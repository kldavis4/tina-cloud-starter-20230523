---
title: 'An Introduction To CSS Keyframes Animation'
slug: an-introduction-to-css3-keyframe-animations
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/777c7dcc-b668-4b1a-80e3-79911bfb5167/css3-styling-opt.jpg
date: 2011-05-17T10:06:16.000Z
author: louis-lazaris
summary: >-
  In this article, Louis Lazaris covers all the important parts of the syntax for CSS animations.  If you haven’t yet started using CSS keyframe animations, here’s your chance to start!
description: >-
  In this article, Louis Lazaris covers all the important parts of the syntax for CSS animations.  If you haven’t yet started using CSS keyframe animations, here’s your chance to start!
categories:
  - Coding
  - CSS
  - Animation
  - CSS3
  - Responsive Images
---

By now you’ve probably heard at least something about animation in CSS3 using keyframe-based syntax. The <a href="https://www.w3.org/TR/css3-animations/">CSS3 animations module</a> in the specification has been around for a couple of years now, and it has the potential to become a big part of Web design.

Using CSS keyframe animations, developers can create smooth, maintainable animations that perform relatively well and that don’t require reams of scripting. It’s just another way that CSS3 is helping to solve a real-world problem in an elegant manner. If you haven’t yet started learning the syntax for CSS animations, here’s your chance to prepare for when this part of the CSS3 spec moves past the <a href="https://en.wikipedia.org/wiki/W3C_recommendation#Working_Draft_.28WD.29">working draft</a> stage.

In this article, we’ll cover all the important parts of the syntax, and we’ll fill you in on browser support so that you’ll know when to start using it.

<figure><a href="https://www.impressivewebs.com/demo-files/css3-animated-scene/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbdf449a-d889-460c-b456-2e0e338773ae/animated-scene.jpg" alt="CSS Keyframes Animated Landscape Scene" width="500" height="500" /></a><figcaption>CSS Keyframes Animated Landscape Scene.</figcaption></figure>

{{% feature-panel %}}

## A Simple Animated Landscape Scene

For the purpose of this article, I’ve created a simple animated landscape scene to introduce the various aspects of the syntax. You can <a href="https://www.impressivewebs.com/demo-files/css3-animated-scene/">view the demo page</a> to get an idea of what I’ll be describing. The page includes a sidebar that displays the CSS code used for the various elements (sun, moon, sky, ground and cloud). Have a quick look, and then follow along as I describe the different parts of the CSS3 animations module.

(NOTE: Versions of Safari prior to 5.1 have a bug that prevents the animation from finishing correctly. See more under the heading “The Animation’s Fill Mode”.)

I’ll describe the CSS related to only one of the elements: the animated sun. That should suffice to give you a good understanding of keyframe-based animations. For the other elements in the demo, you can examine the code on the demo page using the tabs.

## The @keyframes At-Rule

The first unusual thing you’ll notice about any CSS3 animation code is the <code>keyframes</code> @ rule. According to the spec, this specialized CSS @ rule is followed by an identifier (chosen by the developer) that is referred to in another part of the CSS.

The @ rule and its identifier are then followed by a number of rule sets (i.e. style rules with declaration blocks, as in normal CSS code). This chunk of rule sets is delimited by curly braces, which nest the rule sets inside the @ rule, much as you would find with <a href="https://reference.sitepoint.com/css/atrulesref">other @ rules</a>.

Here’s the @ rule we’ll be using:

<pre><code class="language-css">@keyframes sunrise {
	/* rule sets go here … */
}</code></pre>

The word <code>sunrise</code> is an identifier of our choosing that we’ll use to refer to this animation.

Notice that I’m using not using any vendor prefixes for all of the code examples here and in the demo. I’ll discuss browser support at the end of this article, but for now just realize that currently no browser supports this standard syntax, so to get the code working, you have to include all the vendor prefixes.

## The Keyframe Selectors

Let’s add some rule sets inside the @ rule:

<pre><code class="language-css">@keyframes sunrise {
   0% {
      bottom: 0;
      left: 340px;
      background: #f00;
   }

   33% {
      bottom: 340px;
      left: 340px;
      background: #ffd630;
   }

   66% {
      bottom: 340px;
      left: 40px;
      background: #ffd630;
   }

   100% {
      bottom: 0;
      left: 40px;
      background: #f00;
   }
}</code></pre>

With the addition of those new rule sets, we’ve introduced the keyframe selector. In the code example above, the keyframe selectors are <code>0%</code>, <code>33%</code>, <code>66%</code>, and <code>100%</code>. The <code>0%</code> and <code>100%</code> selectors could be replaced by the keywords “from” and “to,” respectively, and you would get the same results.

Each of the four rule sets in this example represents a different snapshot of the animated element, with the styles defining the element’s appearance at that point in the animation. The points that are not defined (for example, from 34% to 65%) comprise the transitional period between the defined styles.

Although the spec is still in development, some rules have been defined that user agents should follow. For example, the order of the keyframes doesn’t really matter. The keyframes will play in the order specified by the percentage values, and not necessarily the order in which they appear. Thus, if you place the “to” keyframe before the “from” keyframe, the animation would still play the same way. Also, if a “to” or “from” (or its percentage-based equivalent) is not declared, the browser will automatically construct it. So, the rule sets inside the @ rule are not governed by the cascade that you find in customary CSS rule sets.

### The Keyframes That Animate the Sun

For the purpose of animating the sun in this demo, I’ve set four keyframes. As mentioned, the code above includes comments that describe the changes.

In the first keyframe, the sun is red (as if it were just rising or setting), and it is positioned below ground (i.e. not visible). Naturally, the element itself must be positioned relatively or absolutely in order for the <code>left</code> and <code>bottom</code> values to have any effect. I’ve also used <a href="https://www.smashingmagazine.com/2009/09/15/the-z-index-css-property-a-comprehensive-look/">z-index</a> to stack the elements (to make sure, for example, that the ground is above the sun). Take note that the only styles shown in the keyframes are the styles that are animated. The other styles (such as <code>z-index</code> and <code>position</code>, which aren’t animated) are declared elsewhere in the style sheet and thus aren’t shown here.

<pre><code class="language-css">0% {
	bottom: 0; /* sun at bottom */
	left: 340px; /* sun at right */
	background: #f00; /* sun is red */
}</code></pre>

About one third of the way into the animation (33%), the sun is on the same horizontal plane but has risen and changed to a yellow-orange (to represent full daylight):

<pre><code class="language-css">33% {
	bottom: 340px; /* sun rises */
	left: 340px;
	background: #ffd630; /* changes color */
}</code></pre>

Then, at about two thirds into the animation (66%), the sun has moved to the left about 300 pixels but stays on the same vertical plane. Notice something else in the 66% keyframe: I’ve repeated the same color from the 33% keyframe, to keep the sun from changing back to red too early.

<pre><code class="language-css">66% {
	bottom: 340px;
	left: 40px; /* sun moves left across sky */
	background: #ffd630; /* maintains its color */
}</code></pre>

Finally, the sun gradually animates to its final state (the full red) as it disappears below the ground.

<pre><code class="language-css">100% {
	bottom: 0; /* sun sets */
	left: 40px;
	background: #f00; /* back to red */
}</code></pre>

## Associating The Animation Name With An Element

Here’s the next chunk of code we’ll add in our example. It associates the animation name (in this case, the word <code>sunrise</code>) with a specific element in our HTML:

<pre><code class="language-css">#sun.animate {
	animation-name: sunrise;
}</code></pre>

Here we’re introducing the <code>animation-name</code> property. The value of this property must match an identifier in an existing <code>@keyframes</code> rule, otherwise no animation will occur. In some circumstances, you can use JavaScript to set its value to <code>none</code> (the only keyword that has been reserved for this property) to prevent an animation from occurring.

The object we’ve targeted is an element with an id of <code>sun</code> and a class of <code>animate</code>. The reason I’ve doubled up the id and class like this is so that I can use scripting to add the class name <code>animate</code>. In the demo, I’ve started the page statically; then, with the click of a button, all of the elements with a particular class name will have another class appended called <code>animate</code>. This will trigger all of the animations at the same time and will allow the animation to be controlled by the user.

Of course, that’s just one way to do it. As is the case with anything in CSS or JavaScript, there are other ways to accomplish the same thing.

{{% ad-panel-leaderboard %}}

## The Animation’s Duration And Timing Function

Let’s add two more lines to our CSS:

<pre><code class="language-css">#sun.animate {
	animation-name: sunrise;
	animation-duration: 10s;
	animation-timing-function: ease;
}</code></pre>

You can specify the duration of the animation using the <code>animation-duration</code> property. The duration represents the time taken to complete a single iteration of the animation. You can express this value in seconds (for example, <code>4s</code>), milliseconds (<code>2000ms</code>), and seconds in decimal notation (<code>3.3s</code>).

The specification doesn’t seem to specify all of the available units of time measurement. However, it seems unlikely that anyone would need anything longer than seconds; and even then, you could express duration in minutes, hours or days simply by calculating those units into seconds or milliseconds.

The <code>animation-timing-function</code> property, when declared for the entire animation, allows you to define how an animation progresses over a single iteration of the animation. The values for <code>animation-timing-function</code> are <code>ease</code>, <code>linear</code>, <code>ease-out</code>, <code>step-start</code> and many more, <a href="https://dev.w3.org/csswg/css3-animations/#animation-timing-function">as outlined in the spec</a>.

For our example, I’ve chosen <code>ease</code>, which is the default. So in this case, we can leave out the property and the animation will look the same.

Additionally, you can apply a specific timing function to each keyframe, like this:

<pre><code class="language-css">@keyframes sunrise {
   0% {
      background: #f00;
      left: 340px;
      bottom: 0;
      animation-timing-function: ease;
   }

   33% {
      bottom: 340px;
      left: 340px;
      background: #ffd630;
      animation-timing-function: linear;
   }

   66% {
      left: 40px;
      bottom: 340px;
      background: #ffd630;
      animation-timing-function: steps(4);
   }

   100% {
      bottom: 0;
      left: 40px;
      background: #f00;
      animation-timing-function: linear;
   }
}</code></pre>

A separate timing function defines each of the keyframes above. One of them is the <code>steps</code> value, which jerks the animation forward a predetermined number of steps. The final keyframe (<code>100%</code> or <code>to</code>) also has its own timing function, but because it is for the final state of a forward-playing animation, the timing function applies only if the animation is played in reverse.

In our example, we won’t define a specific timing function for each keyframe, but this should suffice to show that it is possible.

## The Animation’s Iteration Count And Direction

Let’s now add two more lines to our CSS:

<pre><code class="language-css">#sun.animate {
	animation-name: sunrise;
	animation-duration: 10s;
	animation-timing-function: ease;
	animation-iteration-count: 1;
	animation-direction: normal;
}</code></pre>

This introduces two more properties: one that tells the animation how many times to play, and one that tells the browser whether or not to alternate the sequence of the frames on multiple iterations.

The <code>animation-iteration-count</code> property is set to <code>1</code>, meaning that the animation will play only once. This property accepts an integer value or <code>infinite</code>.

In addition, the <code>animation-direction</code> property is set to <code>normal</code> (the default), which means that the animation will play in the same direction (from start to finish) each time it runs. In our example, the animation is set to run only once, so the property is unnecessary. The other value we could specify here is <code>alternate</code>, which makes the animation play in reverse on every other iteration. Naturally, for the <code>alternate</code> value to take effect, the iteration count needs to have a value of <code>2</code> or higher.

## The Animation’s Delay And Play State

Let’s add another two lines of code:

<pre><code class="language-css">#sun.animate {
	animation-name: sunrise;
	animation-duration: 10s;
	animation-timing-function: ease;
	animation-iteration-count: 1;
	animation-direction: normal;
	animation-delay: 5s;
	animation-play-state: running;
}</code></pre>

First, we introduce the <code>animation-delay</code> property, which does exactly what you would think: it allows you to delay the animation by a set amount of time. Interestingly, this property can have a negative value, which moves the starting point partway through the animation according to negative value.

The <code>animation-play-state</code> property, which <a href="https://www.w3.org/TR/css3-animations/#animation-play-state">might be removed</a> from the spec, accepts one of two possible values: <code>running</code> and <code>paused</code>. This value has limited practical use. The default is <code>running</code>, and the value <code>paused</code> simply makes the animation start off in a paused state, until it is manually played. You can’t specify a <code>paused</code> state in the CSS for an individual keyframe; the real benefit of this property becomes apparent when you use JavaScript to change it in response to user input or something else.

## The Animation’s Fill Mode

We’ll add one more line to our code, the property to define the “fill mode”:

<pre><code class="language-css">#sun.animate {
	animation-name: sunrise;
	animation-duration: 10s;
	animation-timing-function: ease;
	animation-iteration-count: 1;
	animation-direction: normal;
	animation-delay: 5s;
	animation-play-state: running;
	animation-fill-mode: forwards;
}</code></pre>

The <code>animation-fill-mode</code> property allows you to define the styles of the animated element before and/or after the animation executes. A value of <code>backwards</code> causes the styles in the first keyframe to be applied before the animation runs. A value of <code>forwards</code> causes the styles in the last keyframe to be applied after the animation runs. A value of <code>both</code> does both.

**UPDATE:** The <code>animation-fill-mode</code> property is not in the latest draft of the spec, but it is found in the <a href="https://dev.w3.org/csswg/css3-animations/#the-animation-fill-mode-property-">editors draft</a>. Also, certain versions of Safari (5.0 and older) will only apply a value of “forwards” if there are exactly two keyframes defined. These browsers always seems to use the 2nd keyframe as the “forwards” state, which is not how other browsers do it; the correct behaviour uses the final keyframe. This is fixed in Safari 5.1.

## Shorthand

Finally, the specification describes <a href="https://www.w3.org/TR/css3-animations/#the-animation-shorthand-property-">shorthand notation</a> for animations, which combines six of the properties described above. This includes everything except <code>animation-play-state</code> and <code>animation-fill-mode</code>.

## Some Notes On The Demo Page And Browser Support

As mentioned, the code in this article is for animating only a single element in the demo: the sun. To see the full code, visit the <a href="https://www.impressivewebs.com/demo-files/css3-animated-scene/">demo page</a>. You can view all of the source together or use the tabs in the sidebar to view the code for individual elements in the animation.

The demo does not use any images, and the animation does not rely on JavaScript. The sun, moon and cloud are all created using CSS3’s <code>border-radius</code>, and the only scripting on the page is for the tabs on the right and for the button that lets users start and reset the animation.

Here are the browsers that support CSS3 keyframe animations:

*   Chrome 2+,
*   Safari 4+,
*   Firefox 5+,
*   IE10 PP3,
*   iOS Safari 3.2+,
*   Android 2.1+.

Although no official announcement has been made, support in Opera is expected.

If you code your animations using a single vendor-based syntax, you can use a tool like <a href="https://prefixr.com/">Prefixr</a> or Animation Fill Code to automatically fill in the extra code for you.

{{% ad-panel-leaderboard %}}

## Further Reading On CSS Keyframes

*   “[CSS Animations Module Level 3](https://www.w3.org/TR/css3-animations/),” W3C
*   “[CSS3 Animations](https://robertnyman.com/2010/05/06/css3-animations/),” Robert Nyman
*   “[CSS3 Animator](https://css3animator.com/),” Anthony Calzadilla A website “dedicated solely to CSS3/JavaScript animation and how to realistically use it in your projects today.”
*   “[Adding Delight to Your Design with CSS3 and Webkit Keyframe Animation](https://www.viget.com/inspire/adding-delight-to-your-design-with-css3-and-webkit-keyframe-animation/),” Jason Garber
*   “[Using CSS3 Transitions, Transforms and Animation](https://css3.bradshawenterprises.com/)” (with examples), Rich Bradshaw
*   “[Creating Awesome CSS3 Animations](https://mir.aculo.us/2010/08/27/creating-awesome-css3-animations/),” by Thomas Fuchs

### Further Reading

*   [The State Of Animation 2014](https://www.smashingmagazine.com/2014/11/the-state-of-animation-2014/)
*   [The Guide To CSS Animation: Principles and Examples](https://www.smashingmagazine.com/2011/09/the-guide-to-css-animation-principles-and-examples/)
*   [Let’s Play With Hardware-Accelerated CSS](https://www.smashingmagazine.com/2012/06/play-with-hardware-accelerated-css/)
*   [Upgrading CSS Animation With Motion Curves](https://www.smashingmagazine.com/2016/08/css-animations-motion-curves/)

{{< signature "al, vf, il, mrn" >}}

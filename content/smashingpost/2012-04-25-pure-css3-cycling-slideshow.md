---
title: A Pure CSS3 Cycling Slideshow
slug: pure-css3-cycling-slideshow
image: null
date: 2012-04-25T13:06:43.000Z
author: alessio-atzeni
description: >-
  Thanks to CSS3, we can create effects and animations without using JavaScript,
  which will facilitate the work of many designers.
categories:
  - Coding
  - Animation
  - CSS3
---
Thanks to CSS3, we can create effects and animations without using JavaScript, which will facilitate the work of many designers.

But we must be careful to avoid abusing CSS3, not only because old browsers do not support all of its properties. In any case, we all see the potential of CSS3, and in this article we’ll discuss how to create an infinitely looping slider of images using only <strong>CSS3 animation</strong>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [An Exploration Of Carousel Usage On Mobile E-Commerce Websites](https://www.smashingmagazine.com/2015/02/carousel-usage-exploration-on-mobile-e-commerce-websites/)
*   [<span class="headline">Thank God We Have A Specification!</span>](https://www.smashingmagazine.com/2013/04/css3-transitions-thank-god-specification/)
*   [An Introduction To CSS3 Keyframe Animations](https://www.smashingmagazine.com/2011/05/an-introduction-to-css3-keyframe-animations/)
*   [Create An Animated Bar Graph With HTML, CSS And jQuery](https://www.smashingmagazine.com/2011/09/create-an-animated-bar-graph-with-html-css-and-jquery/)

### Sections of This Article

To get a solid sense of the process from beginning to end, below is an outline of the article. Please note that this effect will <strong>only work properly in modern browsers that support the CSS3 properties</strong> being used.

{{% feature-panel %}}

1.  [Introduction](#1 "Introduction") Learn basic concepts related to CSS3 transitions and keyframe animation.
2.  [HTML markup](#2 "HTML markup") Create the HTML markup for the sliding images.
3.  [CSS styles](#3 "CSS styles") Create the style sheet to display the slider.
4.  [CSS3 keyframe animation](#4 "CSS3 keyframe animation") Add animation to the slider (we’ll explain the various processes happening here).
5.  [Progress bar](#5 "Progress bar") Add a progress bar for our slider.
6.  [Tooltip](#6 "Tooltip") Add a tooltip to display the title of the image.
7.  [CSS3 transitions](#7 "CSS3 transitions") Animate the tooltip using CSS3 transitions to make it appear to hover over the image.
8.  [Pause and restart](#8 "Pause and restart") Pause the slider and restart it on hover.
9.  [Demo](#9 "Demo") Check out the slider in action.
10.  [Conclusion](#10 "Conclusion") Final considerations.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d911f1cf-c26a-462b-a6a4-5f15a97e204f/final-slider.jpg"><img loading="lazy" decoding="async" class="116935" title="Pure CSS3 Cycle Slider" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d911f1cf-c26a-462b-a6a4-5f15a97e204f/final-slider.jpg" alt="Pure CSS3 Cycle Slider" width="500" height="550" /></a><br>
<em>Screenshot of the pure <a href="https://www.alessioatzeni.com/CSS3-Cycle-Image-Slider/">CSS3 cycling slideshow</a>.</em>

<a id="1" name="1"></a>

## 1\. Introduction

To follow this tutorial, having a basic understanding of CSS, especially CSS3 transitions and keyframe animation, is important. Using this simple concept, we will see how to make a functional image slider.</p>

### Basic Concepts of CSS3 Transitions

Normally when you change a CSS value, the change is instant. Now, thanks to the <strong>transition</strong> property, we can easily animate from the old to new state.

We can use four transition properties:

1.  `transition-property` Defines the name(s) of the CSS properties to which the transitions should be applied.
2.  `transition-duration` Defines the duration over which the transitions should occur.
3.  `transition-timing-function` Determines how intermediate values of the transition are calculated. The effects from the timing function are commonly called easing functions.
4.  `transition-delay` Defines when the transition starts.

At the moment, CSS3 transitions are supported in Safari 3.2+, Chrome, Firefox 4+, Opera 10.5+ and IE 10. Because the technology is still relatively new, <strong>prefixes for browsers are required</strong>. So far, the syntax is exactly the same for each browser, with only a prefix change required. We will omit them in the snippets in this article, but please remember to include the prefixes in your code.

Let's see how to apply a simple transition to a link:

<pre><code class="language-css">a {
   color: #000;
   transition-property: color;
   transition-duration: 0.7s;
   transition-timing-function: ease-in;
   transition-delay: 0.3s;
}

a:hover {
   color: #fff;
}</code></pre>

When assigning an animation to an element, you can also use the shorthand:

<pre><code class="language-css">a  {
   color: #000;
   transition: color 0.7s ease-in 0.3s;
}

a:hover {
   color: #fff;
}</code></pre>

The W3C has a list of all “<a title="Animatable Properties" href="https://www.w3.org/TR/css3-transitions/#properties-from-css-">Animatable Properties</a>.”

### Basic Concepts of CSS3 Animations

CSS animation enables us to create animations without JavaScript by using a set of <strong>keyframes</strong>.

Unlike CSS transitions, keyframe animations are currently supported only in Webkit browsers and Firefox and soon in IE 10. Unsupported browsers will simply ignore your animation code.

The animation property has eight subproperties:

1.  `animation-delay` Defines when the animation starts.
2.  `animation-direction` Sets the animation to play in reverse on alternate cycles.
3.  `animation-duration` Defines the length of time an animation takes to complete one cycle.
4.  `animation-iteration-count` Defines the number of times an animation cycle should play before stopping.
5.  `animation-name` Specifies the name of the `@keyframes` rule.
6.  `animation-play-state` Determines whether an animation is running or paused.
7.  `animation-timing-function` Describes how an animation progresses over one cycle.
8.  `animation-fill-mode` Specifies how a CSS animation should apply styles to its target before and after executing.

Let's see how to apply a simple animation to a div.

<pre><code class="language-css">/* This is the element we are applying the animation to. */

div {
   animation-name: move;
   animation-duration: 1s;
   animation-timing-function: ease-in-out;
   animation-delay: 0.5s;
   animation-iteration-count: 2;
   animation-direction: alternate;

   -moz-animation-name: move;
   -moz-animation-duration: 1s;
   -moz-animation-timing-function: ease-in-out;
   -moz-animation-delay: 0.5s;
   -moz-animation-iteration-count: 2;
   -moz-animation-direction: alternate;

   -webkit-animation-name: move;
   -webkit-animation-duration: 1s;
   -webkit-animation-timing-function: ease-in-out;
   -webkit-animation-delay: 0.5s;
   -webkit-animation-iteration-count: 2;
   -webkit-animation-direction: alternate;
}

/* This is the animation code. */

@keyframes move {
   from {
      transform: translateX(0);
   }
   to {
      transform: translateX(100px);
   }
}

@-moz-keyframes move {
   from {
      -moz-transform: translateX(0);
   }
   to {
      -moz-transform: translateX(100px);
   }
}

@-webkit-keyframes move {
   from {
      -webkit-transform: translateX(0);
   }
   to {
      -webkit-transform: translateX(100px);
   }
}</code></pre>

But we can use the shorthand property to conveniently set all of the animation properties at once.

<pre><code class="language-css">div {
   animation: move 1s ease-in-out 0.5s 2 alternate;
   -moz-animation: move 1s ease-in-out 0.5s 2 alternate;
   -webkit-animation: move 1s ease-in-out 0.5s 2 alternate;
}</code></pre>

### Keyframes

Each keyframe describes how an animated element should render at a given point in the animation sequence. The <strong>keyframes</strong> take a percentage value to specify time: <code>0%</code> is the start of the animation, while <code>100%</code> is the end. You can optionally add keyframes for intermediate animations.

<pre><code class="language-css">/* Animation from 0% to 100% */

@keyframes move {
   0% { transform: translateX(0); }
   100% { transform: translateX(100px); }
}

/* Animation with intermediate keyframes */

@keyframes move {
   0% { transform: translateX(0); }
   50% { transform: translateX(20px); }
   100% { transform: translateX(100px); }
}</code></pre>

The W3C has a lot of useful and detailed information on “<a title="CSS3 Animation" href="https://www.w3.org/TR/css3-animations/">CSS3 Animations</a>.”

### Basic Structure of Our Slider

Now that we know how transitions and animation work, let’s see how to create our slider using only CSS3. This sketch shows how the animation should work:

<img loading="lazy" decoding="async" class="119152" title="Sketch animation slider function" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/828657c7-44a2-4f80-95d7-06c96fe81474/sketch-1.jpg" alt="Sketch animation slider function" width="500" height="550" /><br>
<em>How the animation slider functions</em>

As you can see, the slider will be a container inside of which the images will be displayed.

The animation is very simple: the image follow a predefined path, animating the <code>top</code> property and changing the <code>z-index</code> and <code>opacity</code> properties when the image returns to its initial position.

Let’s dive right into the HTML markup to create the slider.

<a id="2" name="2"></a>

## 2\. HTML Markup

The HTML markup is very simple; it’s all organized and SEO-friendly. Let's see the full code first and then figure out in detail how everything works.

<pre><code class="language-markup tmp-xml">&lt;div class="container"&gt;
   &lt;div id="content-slider"&gt;
      &lt;div id="slider"&gt;  &lt;!-- Slider container --&gt;
         &lt;div id="mask"&gt;  &lt;!-- Mask --&gt;

         &lt;ul&gt;
         &lt;li id="first" class="firstanimation"&gt;  &lt;!-- ID for tooltip and class for animation --&gt;
         &lt;a href="#"&gt; &lt;img src="images/img_1.jpg" alt="Cougar"/&gt; &lt;/a&gt;
         &lt;div class="tooltip"&gt; &lt;h1&gt;Cougar&lt;/h1&gt; &lt;/div&gt;
         &lt;/li&gt;

         &lt;li id="second" class="secondanimation"&gt;
         &lt;a href="#"&gt; &lt;img src="images/img_2.jpg" alt="Lions"/&gt; &lt;/a&gt;
         &lt;div class="tooltip"&gt; &lt;h1&gt;Lions&lt;/h1&gt; &lt;/div&gt;
         &lt;/li&gt;

         &lt;li id="third" class="thirdanimation"&gt;
         &lt;a href="#"&gt; &lt;img src="images/img_3.jpg" alt="Snowalker"/&gt; &lt;/a&gt;
         &lt;div class="tooltip"&gt; &lt;h1&gt;Snowalker&lt;/h1&gt; &lt;/div&gt;
         &lt;/li&gt;

         &lt;li id="fourth" class="fourthanimation"&gt;
         &lt;a href="#"&gt; &lt;img src="images/img_4.jpg" alt="Howling"/&gt; &lt;/a&gt;
         &lt;div class="tooltip"&gt; &lt;h1&gt;Howling&lt;/h1&gt; &lt;/div&gt;
         &lt;/li&gt;

         &lt;li id="fifth" class="fifthanimation"&gt;
         &lt;a href="#"&gt; &lt;img src="images/img_5.jpg" alt="Sunbathing"/&gt; &lt;/a&gt;
         &lt;div class="tooltip"&gt; &lt;h1&gt;Sunbathing&lt;/h1&gt; &lt;/div&gt;
         &lt;/li&gt;
         &lt;/ul&gt;

         &lt;/div&gt;  &lt;!-- End Mask --&gt;
         &lt;div class="progress-bar"&gt;&lt;/div&gt;  &lt;!-- Progress Bar --&gt;
      &lt;/div&gt;  &lt;!-- End Slider Container --&gt;
   &lt;/div&gt;
&lt;/div&gt;</code></pre>

1.  `div id="slider"` This is the main container of the slider. It does not have a particular function, but we will need it to pause the animation.
2.  `div id="mask"` We will use this to hide everything that happens outside of the slider. In addition to hiding the content, the mask allows us to display the contents of the slider.
3.  `li id="first" class="firstanimation"` Every list item has an ID and a class. The ID displays the tooltip, and the class is tied to the animation that has to occur.
4.  `div class="tooltip"` This simply displays the title of the image. You can modify it to your needs; for example, by making it clickable and adding a short description.
5.  `div class="progress-bar"` This contains the function that shows the progress of the animation.

Now it’s time for the CSS file.

<a id="3" name="3"></a>

## 3\. CSS Style

Let’s create the basic structure of the slider. It will have the same image size. The border property will be useful to create a frame around the image.

<pre><code class="language-css">/* SLIDER STRUCTURE */

#slider {
   background: #000;
   border: 5px solid #eaeaea;
   box-shadow: 1px 1px 5px rgba(0,0,0,0.7);
   height: 320px;
   width: 680px;
   margin: 40px auto 0;
   overflow: visible;
   position: relative;
}</code></pre>

The <code>mask</code> class will hide all of the elements that lie outside of the slider; its height must be equal to the height of the slider.

<pre><code class="language-css">/* HIDE ALL OUTSIDE OF THE SLIDER */

#mask {
   overflow: hidden;
   height: 320px;
}</code></pre>

Finally, to sort the list of images, we’ll have <code>position: absolute</code> and <strong>top: -325px</strong> so that all of the images are positioned outside of the slider.

<pre><code class="language-css">/* IMAGE LIST */

#slider ul {
   margin: 0;
   padding: 0;
   position: relative;
}

#slider li {
   width: 680px;  /* Width Image */
   height: 320px; /* Height Image */
   position: absolute;
   top: -325px; /* Original Position - Outside of the Slider */
   list-style: none;
}</code></pre>

With these few lines of code, we have created our slider. Now we just need to add the animation.

<a id="4" name="4"></a>

## 4\. CSS3 Keyframes Animation

<img loading="lazy" decoding="async" class="118691" title="Slider Animation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc3456d5-71e3-47d9-afba-fbd860ce36e1/slider-animation.jpg" alt="Slider Animation" width="500" height="550" /><br>
<em>Image animation for the slider</em>

Before we begin with the animation, we have to specify some parameters in order to get the right view of the animation.

As we know, the total duration of the animation will be 25 seconds, but we have to know how many keyframes equals 1 second.

So, let’s work out a series of operations that gives us the exact number of keyframes based on the images we have and the total duration of the animation. Here are the calculations:

1.  **Define the total number of images to use in the slider** 5
2.  **Define the length of animation for each image** 5 seconds
3.  **Define the total duration of the animation** Multiply the total number of images by the duration of each image: 5 images × 5 seconds = 25 seconds
4.  **Calculate how many keyframes equals one second** Divide the total number of keyframes by the total duration of the animation. 100 keyframes / 25 seconds = 4 keyframes 4 keyframes = 1 second

With all of this math, we can now apply the CSS animation to the slider. We will be able to put the animation on infinite loop because each image will follow its own animation that activates once it comes up in the slider.

<pre><code class="language-css">#slider li.firstanimation {
   animation: cycle 25s linear infinite;
}

#slider li.secondanimation {
   animation: cycletwo 25s linear infinite;
}

#slider li.thirdanimation {
   animation: cyclethree 25s linear infinite;
}

#slider li.fourthanimation {
   animation: cyclefour 25s linear infinite;
}

#slider li.fifthanimation {
   animation: cyclefive 25s linear infinite;
}</code></pre>

Once the properties of the animation have been assigned, we need to use keyframes to set the animation in motion.

Following this principle, we can connect the animations to each other even though they are separate, which will give us an infinite loop.

I’ve added the <code>opacity</code> and <code>z-index</code> properties to make the transition from one image to the next more attractive.

As you can see in the code, the first animation has more keyframes than the rest. The reason for this is that when the gallery is started, the first image is positioned to make way for the second image; but when the last image has finished its animation, the first image has to have additional keyframes in order for the user not to see a break between animation cycles.

Here is all of the code for the animations:

<pre><code class="language-css">/* ANIMATION */

@keyframes cycle {
   0%  { top: 0px; } /* When you start the slide, the first image is already visible */
   4%  { top: 0px; } /* Original Position */
   16% { top: 0px; opacity:1; z-index:0; } /* From 4% to 16 % = for 3 seconds the image is visible */
   20% { top: 325px; opacity: 0; z-index: 0; } /* From 16% to 20% = for 1 second exit image */
   21% { top: -325px; opacity: 0; z-index: -1; } /* Return to Original Position */
   92% { top: -325px; opacity: 0; z-index: 0; }
   96% { top: -325px; opacity: 0; } /* From 96% to 100% = for 1 second enter image*/
   100%{ top: 0px; opacity: 1; }
}

@keyframes cycletwo {
   0%  { top: -325px; opacity: 0; } /* Original Position */
   16% { top: -325px; opacity: 0; }/* Starts moving after 16% to this position */
   20% { top: 0px; opacity: 1; }
   24% { top: 0px; opacity: 1; }  /* From 20% to 24% = for 1 second enter image*/
   36% { top: 0px; opacity: 1; z-index: 0; }   /* From 24% to 36 % = for 3 seconds the image is visible */
   40% { top: 325px; opacity: 0; z-index: 0; } /* From 36% to 40% = for 1 second exit image */
   41% { top: -325px; opacity: 0; z-index: -1; }   /* Return to Original Position */
   100%{ top: -325px; opacity: 0; z-index: -1; }
}

@keyframes cyclethree {
   0%  { top: -325px; opacity: 0; }
   36% { top: -325px; opacity: 0; }
   40% { top: 0px; opacity: 1; }
   44% { top: 0px; opacity: 1; }
   56% { top: 0px; opacity: 1; }
   60% { top: 325px; opacity: 0; z-index: 0; }
   61% { top: -325px; opacity: 0; z-index: -1; }
   100%{ top: -325px; opacity: 0; z-index: -1; }
}

@keyframes cyclefour {
   0%  { top: -325px; opacity: 0; }
   56% { top: -325px; opacity: 0; }
   60% { top: 0px; opacity: 1; }
   64% { top: 0px; opacity: 1; }
   76% { top: 0px; opacity: 1; z-index: 0; }
   80% { top: 325px; opacity: 0; z-index: 0; }
   81% { top: -325px; opacity: 0; z-index: -1; }
   100%{ top: -325px; opacity: 0; z-index: -1; }
}
@keyframes cyclefive {
   0%  { top: -325px; opacity: 0; }
   76% { top: -325px; opacity: 0; }
   80% { top: 0px; opacity: 1; }
   84% { top: 0px; opacity: 1; }
   96% { top: 0px; opacity: 1; z-index: 0; }
   100%{ top: 325px; opacity: 0; z-index: 0; }
}</code></pre>

Having created the animations, we have to add a progress bar to display the duration of each animation.

<a id="5" name="5"></a>

## 5\. Progress Bar

<img loading="lazy" decoding="async" class="118688" title="Progress Bar Animation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da6fc4a1-2613-4f13-87ff-7fd3bd08ce15/progress-bar.jpg" alt="Progress bar Animation for each image" width="500" height="550" /><br>
<em>The progress bar for each animation</em>

The process of animating the progress bar is the same as it was for the slider. First, we create the progress bar itself:

<pre><code class="language-css">/* PROGRESS BAR */

.progress-bar {
   position: relative;
   top: -5px;
   width: 680px;
   height: 5px;
   background: #000;
   animation: fullexpand 25s ease-out infinite;
}</code></pre>

Don’t be afraid of the syntax here. It has the same function as <code>from to</code>; you can see that the keyframes set the appearance and disappearance of each image.

<pre><code class="language-css">/* ANIMATION BAR */

@keyframes fullexpand {
   /* In these keyframes, the progress-bar is stationary */
   0%, 20%, 40%, 60%, 80%, 100% { width: 0%; opacity: 0; }

   /* In these keyframes, the progress-bar starts to come alive */
   4%, 24%, 44%, 64%, 84% { width: 0%; opacity: 0.3; }

   /* In these keyframes, the progress-bar moves forward for 3 seconds */
   16%, 36%, 56%, 76%, 96% { width: 100%; opacity: 0.7; }

   /* In these keyframes, the progress-bar has finished his path */
   17%, 37%, 57%, 77%, 97% { width: 100%; opacity: 0.3; }

   /* In these keyframes, the progress-bar will disappear and then resume the cycle */
   18%, 38%, 58%, 78%, 98% { width: 100%; opacity: 0; }
}</code></pre>

<a id="6" name="6"></a>

## 6\. Tooltip

<a id="4" name="4"></a>

## 4\. CSS3 Keyframes Animation

<img loading="lazy" decoding="async" class="118691" title="Slider Animation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc3456d5-71e3-47d9-afba-fbd860ce36e1/slider-animation.jpg" alt="Slider Animation" width="500" height="550" /><br>
<em>Image animation for the slider</em>

Before we begin with the animation, we have to specify some parameters in order to get the right view of the animation.

As we know, the total duration of the animation will be 25 seconds, but we have to know how many keyframes equals 1 second.

So, let’s work out a series of operations that gives us the exact number of keyframes based on the images we have and the total duration of the animation. Here are the calculations:

1.  **Define the total number of images to use in the slider** 5
2.  **Define the length of animation for each image** 5 seconds
3.  **Define the total duration of the animation** Multiply the total number of images by the duration of each image: 5 images × 5 seconds = 25 seconds
4.  **Calculate how many keyframes equals one second** Divide the total number of keyframes by the total duration of the animation. 100 keyframes / 25 seconds = 4 keyframes 4 keyframes = 1 second

With all of this math, we can now apply the CSS animation to the slider. We will be able to put the animation on infinite loop because each image will follow its own animation that activates once it comes up in the slider.

<pre><code class="language-css">#slider li.firstanimation {
   animation: cycle 25s linear infinite;
}

#slider li.secondanimation {
   animation: cycletwo 25s linear infinite;
}

#slider li.thirdanimation {
   animation: cyclethree 25s linear infinite;
}

#slider li.fourthanimation {
   animation: cyclefour 25s linear infinite;
}

#slider li.fifthanimation {
   animation: cyclefive 25s linear infinite;
}</code></pre>

Once the properties of the animation have been assigned, we need to use keyframes to set the animation in motion.

Following this principle, we can connect the animations to each other even though they are separate, which will give us an infinite loop.

I’ve added the <code>opacity</code> and <code>z-index</code> properties to make the transition from one image to the next more attractive.

As you can see in the code, the first animation has more keyframes than the rest. The reason for this is that when the gallery is started, the first image is positioned to make way for the second image; but when the last image has finished its animation, the first image has to have additional keyframes in order for the user not to see a break between animation cycles.

Here is all of the code for the animations:

<pre><code class="language-css">/* ANIMATION */

@keyframes cycle {
   0%  { top: 0px; } /* When you start the slide, the first image is already visible */
   4%  { top: 0px; } /* Original Position */
   16% { top: 0px; opacity:1; z-index:0; } /* From 4% to 16 % = for 3 seconds the image is visible */
   20% { top: 325px; opacity: 0; z-index: 0; } /* From 16% to 20% = for 1 second exit image */
   21% { top: -325px; opacity: 0; z-index: -1; } /* Return to Original Position */
   92% { top: -325px; opacity: 0; z-index: 0; }
   96% { top: -325px; opacity: 0; } /* From 96% to 100% = for 1 second enter image*/
   100%{ top: 0px; opacity: 1; }
}

@keyframes cycletwo {
   0%  { top: -325px; opacity: 0; } /* Original Position */
   16% { top: -325px; opacity: 0; }/* Starts moving after 16% to this position */
   20% { top: 0px; opacity: 1; }
   24% { top: 0px; opacity: 1; }  /* From 20% to 24% = for 1 second enter image*/
   36% { top: 0px; opacity: 1; z-index: 0; }   /* From 24% to 36 % = for 3 seconds the image is visible */
   40% { top: 325px; opacity: 0; z-index: 0; } /* From 36% to 40% = for 1 second exit image */
   41% { top: -325px; opacity: 0; z-index: -1; }   /* Return to Original Position */
   100%{ top: -325px; opacity: 0; z-index: -1; }
}

@keyframes cyclethree {
   0%  { top: -325px; opacity: 0; }
   36% { top: -325px; opacity: 0; }
   40% { top: 0px; opacity: 1; }
   44% { top: 0px; opacity: 1; }
   56% { top: 0px; opacity: 1; }
   60% { top: 325px; opacity: 0; z-index: 0; }
   61% { top: -325px; opacity: 0; z-index: -1; }
   100%{ top: -325px; opacity: 0; z-index: -1; }
}

@keyframes cyclefour {
   0%  { top: -325px; opacity: 0; }
   56% { top: -325px; opacity: 0; }
   60% { top: 0px; opacity: 1; }
   64% { top: 0px; opacity: 1; }
   76% { top: 0px; opacity: 1; z-index: 0; }
   80% { top: 325px; opacity: 0; z-index: 0; }
   81% { top: -325px; opacity: 0; z-index: -1; }
   100%{ top: -325px; opacity: 0; z-index: -1; }
}
@keyframes cyclefive {
   0%  { top: -325px; opacity: 0; }
   76% { top: -325px; opacity: 0; }
   80% { top: 0px; opacity: 1; }
   84% { top: 0px; opacity: 1; }
   96% { top: 0px; opacity: 1; z-index: 0; }
   100%{ top: 325px; opacity: 0; z-index: 0; }
}</code></pre>

Having created the animations, we have to add a progress bar to display the duration of each animation.

<a id="5" name="5"></a>

## 5\. Progress Bar

<img loading="lazy" decoding="async" class="118688" title="Progress Bar Animation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da6fc4a1-2613-4f13-87ff-7fd3bd08ce15/progress-bar.jpg" alt="Progress bar Animation for each image" width="500" height="550" /><br>
<em>The progress bar for each animation</em>

The process of animating the progress bar is the same as it was for the slider. First, we create the progress bar itself:

<pre><code class="language-css">/* PROGRESS BAR */

.progress-bar {
   position: relative;
   top: -5px;
   width: 680px;
   height: 5px;
   background: #000;
   animation: fullexpand 25s ease-out infinite;
}</code></pre>

Don’t be afraid of the syntax here. It has the same function as <code>from to</code>; you can see that the keyframes set the appearance and disappearance of each image.

<pre><code class="language-css">/* ANIMATION BAR */

@keyframes fullexpand {
   /* In these keyframes, the progress-bar is stationary */
   0%, 20%, 40%, 60%, 80%, 100% { width: 0%; opacity: 0; }

   /* In these keyframes, the progress-bar starts to come alive */
   4%, 24%, 44%, 64%, 84% { width: 0%; opacity: 0.3; }

   /* In these keyframes, the progress-bar moves forward for 3 seconds */
   16%, 36%, 56%, 76%, 96% { width: 100%; opacity: 0.7; }

   /* In these keyframes, the progress-bar has finished his path */
   17%, 37%, 57%, 77%, 97% { width: 100%; opacity: 0.3; }

   /* In these keyframes, the progress-bar will disappear and then resume the cycle */
   18%, 38%, 58%, 78%, 98% { width: 100%; opacity: 0; }
}</code></pre>

<a id="6" name="6"></a>

## 6\. Tooltip

The slider is more or less complete, but let’s add a few details to make it more functional. We’ll insert tooltips for the image titles that will be visible on hover.

<img loading="lazy" decoding="async" class="118689" title="Simple Tooltip" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/913ffc02-49ee-4a4b-8bba-1b3041b1334a/simple-tooltip.jpg" alt="Simple Tooltip on image" width="500" height="550" /><br>
<em>Simple tooltip</em>

Here is the CSS for the tooltips:

<pre><code class="language-css">#slider .tooltip {
   background: rgba(0,0,0,0.7);
   width: 300px;
   height: 60px;
   position: relative;
   bottom: 75px;
   left: -320px;
}

#slider .tooltip h1 {
   color: #fff;
   font-size: 24px;
   font-weight: 300;
   line-height: 60px;
   padding: 0 0 0 10px;
}</code></pre>

Here we’ve made only the image titles visible, but you can do the same to custom text, links or whatever you like.

<a id="7" name="7"></a>

## 7\. CSS3 Transitions

<img loading="lazy" decoding="async" class="118687" title="Tooltip Animation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee34bad0-04b0-46ef-ab79-93772cb0676f/tooltip-animation.jpg" alt="Tooltip Animation" width="500" height="550" /><br>
<em>Animate the tooltip on hover</em>

We have seen how to apply CSS3 transitions to elements; now let’s do it to the tooltips.

If you remember, we added an ID to each list (<code>first</code>, <code>second</code>, etc.) to have only the tooltip associated with an image appear on hover, rather than all of the tooltips appear together.

<pre><code class="language-css">#slider .tooltip {
…
   transition: all 0.3s ease-in-out;
}

#slider li#first: hover .tooltip,
#slider li#second: hover .tooltip,
#slider li#third: hover .tooltip,
#slider li#fourth: hover .tooltip,
#slider li#fifth: hover .tooltip {
   left: 0px;
}</code></pre>

<a id="8" name="8"></a>

## 8\. Pause And Restart

<img loading="lazy" decoding="async" class="118690" title="Stop slider on mouse hover" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03c658b6-bd09-4b73-8282-d6e84f39e9c1/stop-slider.jpg" alt="Stop slider on mouse hover" width="500" height="550" /><br>
<em>Stop slider on mouse hover</em>

To allow users to pause to read content or look at an image, we should stop the animation when they hover over an image. (We’ll also have to stop the animation of the progress bar.)

<pre><code class="language-css">#slider: hover li,
#slider: hover .progress-bar {
   animation-play-state: paused;
}</code></pre>

<a id="9" name="9"></a>

## 9\. Demo

Finally, we’ve reached the end of the tutorial. The slider is now 100% complete!

<a href="https://www.alessioatzeni.com/CSS3-Cycle-Image-Slider/"><img loading="lazy" decoding="async" class="116935" title="Pure CSS3 Cycle Slider" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d911f1cf-c26a-462b-a6a4-5f15a97e204f/final-slider.jpg" alt="Pure CSS3 Cycle Slider" width="500" height="550" /></a><br>
<em>Pure CSS3 cycling slider demo</em>

<a title="Pure CSS3 Cycle Slider" href="https://www.alessioatzeni.com/CSS3-Cycle-Image-Slider/">Check out the demo</a>. It works in Firefox 5+, Safari 4+ and Google Chrome, as well as the iPhone and iPad. You can also <a href="https://www.alessioatzeni.com/CSS3-Cycle-Image-Slider/CSS3-Slider.zip">download the ZIP file</a>.

Thanks to <a title="Massimo Righi" href="https://www.massimorighi.com">Massimo Righi</a> for his images.

<a id="10" name="10"></a>

## 10\. Conclusion

The effect is impressive, but admittedly, this slider is not very versatile. For instance, to add more images, you have to edit all of keyframes. CSS3 has great potential, but it does have limits, and sometimes JavaScript is preferable, depending on your target users.

This slider has some interesting features, such as pausing on hover and uniques link for the images, which allow users to interact with the slider. If you want <strong>full support among browsers</strong>, this is not possible, so JavaScript is recommended. Unfortunately, CSS3 animation has many limitations; its lack of flexibility in particular will prevent its widespread use for now. Hopefully this will spur you on to further study of CSS3.

Feel free to share your thoughts in the comments section below!

<em>(al) (il)</em>


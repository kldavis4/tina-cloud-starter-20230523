---
title: 'Introducing Jelly Navigation Menu: When Canvas Meets PaperJS'
slug: jelly-navigation-menu-canvas-paperjs
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb229513-51e6-45f1-8154-cb1f616878c4/illu-jelly.jpg'
date: 2013-08-15T15:00:59.000Z
author: oleg-solomka
description: >-
  In this article, I would like to share my experience and story of
  how I brought the "Jelly Navigation Menu" to life.
categories:
  - Coding
  - CSS
  - JavaScript
  - HTML
---
There is no doubt that the Web helps designers and developers find the best inspiration and resources for their projects. Even though there are a bunch of different tutorials and tips available online, I feel that HTML5 canvas techniques are missing the most. Good news: I had the chance to fulfill this wide gap. In this article, I would like to share my experience and story of how I brought the "Jelly Navigation Menu" to life. Credits go to [Capptivate.co](https://capptivate.co/2013/07/12/making-3/) and [Ashleigh Brennan's](https://dribbble.com/ash-brennan) icons — they were my inspiration for this project.</p>

### Before We Start

The source code for this project was originally written in CoffeeScript — I believe it's a better way to express and share JavaScript code that way. I will refer to CoffeScript's source in code sections within this post and you'll also notice links to CodePens that have been rewritten in JavaScript and represent local parts of code as well. I recommend downloading the [source code on GitHub](https://github.com/sol0mka/paperjs-scroll-sections) so you can easily follow me while I explain the necessary code in detail.

I used [PaperJS](https://paperjs.org/) for the canvas graphics and [TweenJS](https://github.com/sole/tween.js/) for the animations. Both of them tend to freak out some folks, but don't worry, they are really intuitive and easy to understand. If you'd like to learn how to set up PaperJS and TweenJS environments, you can fork this cool [bootstrap pen](https://codepen.io/sol0mka/pen/Ivisr) for online fun or this [git repo](https://github.com/sol0mka/paperjs-scroll-sections) if you want to experiment locally.

{{% feature-panel %}}

[![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a458fd8-0b1f-4b6d-80ae-9356cc261fab/jelly-menu1.png)](https://codepen.io/sol0mka/pen/Jsyxq)  
_A preview of the [Jelly Navigation Menu](https://codepen.io/sol0mka/pen/Jsyxq)._

## First Step: Changing The Section Shape

Our first aim is to change the menu section shape by manipulating the curves. Every object is made up of [anchor points](https://youtube.com/watch?v=5BPrGoJZ8WI). These points are connected with each other by curves. So each point has "In" and "Out" handles to define the location and direction of specific curves. Folks who work with vector editors should feel comfortable with this step.

[![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad240202-1f1c-4ca5-b6c5-22d3fca11123/handle-out.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad240202-1f1c-4ca5-b6c5-22d3fca11123/handle-out.png)  
_In Paper.js, paths are represented by a sequence of segments that are connected by curves. A segment consists of a point and two handles, defining the location and direction of the curves. [See the handles in action](https://paperjs.org/tutorials/paths/working-with-path-items/)._

All we need to do is to change the `handleOut` position of the `top-left` and `bottom-right` points. To achieve this, I wrote simple so-called "toppie" and "bottie" functions:

  <pre><code class="language-javascript">
toppie:(amount)-&gt;
  @base.segments[1].handleOut.y = amount
  @base.segments[1].handleOut.x = (@wh/2)

bottie:(amount)-&gt;
  @base.segments[3].handleOut.y = amount
  @base.segments[3].handleOut.x = - @wh/2

# @wh/2 is section center.
# @base variable holds section's rectangle path.</code></pre>

It's important to set the handle's X position to exactly the middle of the section, so that the curve will turn out to be symmetrical.</p>

## Second Step: Calculating The Scrolling Speed

So the next thing that needs to be done is to calculate the scrolling speed and direction, and then pass this data to the `bottie` and `toppie` functions. We can listen to the container's scrolling event and determine the current scrolling position (in my case the "container" is a `#wrapper` element whereas it is a window object in the pen examples).

<pre><code class="language-javascript">
# get current scroll value
window.PaperSections.next = window.PaperSections.$container.scrollTop()

# and calculate the difference with previous scroll position
window.PaperSections.scrollSpeed = (window.PaperSections.next - window.PaperSections.prev)

# to make it all work, all we have left to do is to save current scroll position to prev variable
window.PaperSections.prev = window.PaperSections.next</code></pre>

This is repeated for every scrolling event. In this code snippet, `window.PaperSections` is just a global variable. I also made a few minor additions in my implementation:

*   A silly coefficient to increase scroll speed by multiplying it by `1.2` (just played around with it),
*   I sliced the scroll speed result by its maximum so that it is not larger than `sectionHeight/2`,
*   I also added a direction coefficient (it could be `1` or `-1`, you can change it in `dat.gui` on the top right of the page). This way you can control the reaction direction of sections.

  Here is the final code:

<pre><code class="language-javascript">
if window.PaperSections.i % 4 is 0
  direction = if window.PaperSections.invertScroll then -1 else 1
  window.PaperSections.next = window.PaperSections.$container.scrollTop()
  window.PaperSections.scrollSpeed = direction*window.PaperSections.slice 1.2*(window.PaperSections.next - window.PaperSections.prev), window.PaperSections.data.sectionheight/2
  window.PaperSections.prev = window.PaperSections.next
  window.PaperSections.i++</code></pre>

In this example, `if window.PaperSections.i % 4 is 0` helps us react on every fourth scroll event — similar to a filter. That function lives in `window.PaperSections.scrollControl`.

That's it! We're almost done! It couldn't be any easier, right? Try out the scrolling [here](https://codepen.io/sol0mka/pen/zIBGr).</p>

## Step Three: Make It Jelly!

In this final step, we need to animate the `toppie` and `bottie` functions to `0` with TweenJS' elastic easing everytime the scrolling stops.</p>

### 3.1 Determine When Scrolling Stops

To do this, let's add the `setTimeout` function to our `window.PaperSections.scrollControl` function (or `scroll`) with 50ms delay. Each time when the scrolling event fires up, the Timeout is cleared except for the last one, i.e. once scrolling stops, the code in our timeout will execute.

  <pre><code class="language-javascript">
clearTimeout window.PaperSections.timeOut
window.PaperSections.timeOut = setTimeout -&gt;
  window.PaperSections.$container.trigger 'stopScroll'
  window.PaperSections.i = 0
  window.PaperSections.prev = window.PaperSections.$container.scrollTop()
    , 50</code></pre>

The main focus here is the `window.PaperSections.$container.trigger` `stopScroll` event. We can subscribe to it and launch the animation appropriately. The other two lines of code are simply being used to reset helper variables for later `scrollSpeed` calculations.</p>

### 3.2 Animate Point's handleOut To “0”

Next, we'll write the `translatePointY` function to bring our jelly animation to life. This function will take the object as a parameter with the following key-value sets:

  <pre><code class="language-javascript">
{
  // point to move (our handleOut point)
  point: @base.segments[1].handleOut,

  // destination point
  to: 0, duration
}</code></pre>

The function body is made up of the following:

  <pre><code class="language-javascript">
translatePointY:(o)-&gt;
  # create new tween(from point position) to (options.to position, with duration)
  mTW = new TWEEN.Tween(new Point(o.point)).to(new Point(o.to), o.duration)

  # set easing to Elastic Out
  mTW.easing TWEEN.Easing.Elastic.Out

  # on each update set point's Y to current animation point
  mTW.onUpdate -&gt;
    o.point.y = @y

  # finally start the tween
  mTW.start()</code></pre>

The `TWEEN.update()` function also has to be added to every frame of the PaperJS animation loop:

  <pre><code class="language-javascript">
onFrame = -&gt;
  TWEEN.update()</code></pre>

Also, we need to stop all animations on scrolling. I added the following line to the scroll listener function:

  <pre><code class="language-javascript">TWEEN.removeAll()</code></pre>

Finally, we need to subscribe to the `stopScroll` event and launch the animations by calling our `translatePointY` function:

  <pre><code class="language-javascript">
window.PaperSections.$container.on 'stopScroll', =&gt;
  # calculate animation duration
  duration = window.PaperSections.slice(Math.abs(window.PaperSections.scrollSpeed*25), 1400) or 3000

  # launch animation for top left point
  @translatePointY(
    point:      @base.segments[1].handleOut
    to:           0
    duration: duration
  ).then =&gt;
    # clear scroll speed variable after animation has finished
    # without it section will jump a little when new scroll event fires
    window.PaperSections.scrollSpeed = 0

  # launch animation for bottom right point
  @translatePointY
    point:      @base.segments[3].handleOut
    to:           0
    duration: duration</code></pre>

_Et voilà!_

> **Note**: In my [source code](https://github.com/sol0mka/paperjs-scroll-sections) of the `translatePointY` function, I added a deferred object for chaining, optional easing and onUpdate function. It is omitted here for the sake of simplicity.</p>

## In Conclusion

Last but not least, a class for the sections has to be added. Of course, you can make as many instances of it as you like; you just need to define initial Y offset and colors. Also, you will need to make sure that the section in your layout has the same height as the section in canvas. Then we can just apply `translated3d` to both on the `scroll` event and animations. This will cause HTML sections to move properly, just like the canvas sections, and hence produce a realistic animation.

[![HTML Sections](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53d51315-acdd-45c0-afe3-a496c99caee3/html-sections.png "HTML Sections")](https://codepen.io/sol0mka/full/Jsyxq)

The reason why we need to use `translate3d` instead of `translateY` is to make sure that Webkit rendering engines use hardware acceleration while rendering them, so we do not drop out of the 60fps animation budget. But keep your eyes wide open if your sections contain any text. 3D transforms will drop anti-aliasing from subpixel to grayscale, so it may look a bit blurry!

### Feedback

I look forward to your thoughts, questions and/or your feedback to the [Jelly Navigation Menu](https://codepen.io/sol0mka/full/Jsyxq) in the comments section below. You can also reach out to me via Twitter anytime!

<em>(vf) (il)</em>


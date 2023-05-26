---
title: Using Motion For User Experience On Apps And Websites
slug: using-motion-for-ux-on-apps-and-websites
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbc9dd57-5f1a-44af-9382-a02775c1615d/ios-apps-illu-opt.jpg
date: 2015-01-19T22:43:56.000Z
author: andrew-thomas
description: >-
  Digital experiences are emulating real life more and more every day. This may
  seem counterintuitive, considering the hate that rains down on skeuomorphic
  visual design, but there's a lot more to emulating real life than aesthetics.

  Interface designers can emulate real-life physics and movement on a digital
  screen. This type of motion is becoming more common, which is **why it's
  becoming easier for people to understand computers**. We're not getting
  better, the interfaces are!
categories:
  - UX
  - Mobile
  - Apps
  - Usability
  - UX
---
Digital experiences are emulating real life more and more every day. This may seem counterintuitive, considering the hate that rains down on skeuomorphic visual design, but there's a lot more to emulating real life than aesthetics. Interface designers can emulate real-life physics and movement on a digital screen. This type of motion is becoming more common, which is **why it's becoming easier for people to understand computers**. We're not getting better, the interfaces are!

A quick and common example is how iOS opens and closes apps. The transitions are very subtle, but they're realistic. Tapping an app icon doesn't just snap a new app on to the screen. Instead, users see the app physically grow out of the icon. In reverse, pressing the home key shrinks the app back into the icon.

Those interactions are based on properties of the real world. The app appears to come from somewhere physical and disappear back to that place. The high quality and realistic transitions here go a long way toward helping the user understand what's happening and why.</p>

<figure class="video-container"><iframe loading="lazy" style="float: left; display: inline-block; margin-right: 10px;" src="//player.vimeo.com/video/116757193?byline=0&amp;portrait=0&amp;loop=1" width="240" height="426" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe><iframe loading="lazy" style="display: inline-block;" src="//player.vimeo.com/video/116757194?byline=0&amp;portrait=0&amp;loop=1" width="240" height="426" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe><figcaption>Opening an iOS app without a transition vs. with the transition.</figcaption></figure>

In this article, I'll cover a little bit of the history of motion on the web, why that's important, and what the future of motion on the web will look like. (Hint: motion is really important for usability, and it's changing everything.) Then I'll explain the CSS behind motion and how to use motion well.

{{% feature-panel %}}

## The History Of Motion On The Web

It was only 2011 when all major browsers officially recognized CSS animation, and even now it requires browser prefixes to work everywhere. In large part, the push for CSS-driven animation was sparked by the death of Flash, where “movement was common” is an understatement.

In the days of Flash, some websites were basically movies. There was a lot of movement and animation, but most of it was unnecessary to navigate and absorb the content. It was for wow effect at best.

Flash was eventually forced out of the picture, but designers and developers were left without any really good tools for movement and animation on the web.

JavaScript and jQuery became really popular, and they were huge leaps forward, but there are all kinds of reasons not to rely on JavaScript for your site to function. Plus, JavaScript animation was, and in some ways still is, taxing for browsers. Some motion was possible, but it needed to be used sparingly.

It wasn't long before the CSS3 animation and transitions specs were accepted and implemented by modern browsers.

Designers now have **the ability to take advantage of hardware acceleration** and can control movement with their style sheets, further separating content and visual markup. In addition, today's average computers are more than capable of rendering complex animations, and even phones are powerful enough to process an impressive amount of movement.</p>

## The Future Of Motion On The Web

The combination of capable machines and evolving CSS specs means things are going to change in interface design. Websites and apps are going to start taking advantage of motion and what it can do for usability. It's already happening in a lot of ways, but here are some examples to look out for.</p>

### Layers

Layers are everywhere in modern web and app interfaces. Apple really pushed the concept of layers with iOS7\. An example is the Control Center, which slides up from the bottom as a new layer that partially covers whatever's on the screen.</p>

<figure class="video-container"><iframe loading="lazy" src="//player.vimeo.com/video/116756637?byline=0&amp;portrait=0&amp;loop=1" width="338" height="600" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe><figcaption>The iOS Control Center slides in over the current screen as a new layer.</figcaption><br>
</figure>

Although layers aren't movement in themselves, they go hand in hand because they work best when they animate in and animate out.

Layers are important because designers can keep information hidden on another layer until it's called on, instead of refreshing the entire page to display large amounts of new information. This allows users to think less and understand more. It gives them context, which is the next thing you'll start to see a lot of with motion.

### Context

Context is a broad term. For this discussion, I use it to refer to elements and pages that don't just snap from one state to another without showing where they came from and why. **Context helps us remove the digital mystery** and therefore it helps users' brains focus less on interpreting the interface and more on the content and their goals.

To illustrate how transitions can convey context, take a look at the Instacart iOS app. Tapping on an item to see more detail about it doesn't just snap open a new view with the item details.

While that would likely be understood by most users, take a look at the GIF below to see what happens instead. We see the item's picture move from its current position to a new position above the details view. We completely understand what happened and how it relates to the previous view. In fact, this doesn't even feel like we're switching from one view to another. This seems much more natural than that.</p>

<figure class="video-container"><iframe loading="lazy" src="//player.vimeo.com/video/116757192?byline=0&amp;portrait=0&amp;loop=1" width="338" height="600" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe><figcaption>The transition into the detail view in the Instacart app helps to give the user context.</figcaption></figure>

The effect is subtle, but it has huge usability implications. Another example is the newly popular drawer menu, where clicking a hamburger icon reveals a full menu.

If the user taps the icon and their entire screen is instantly replaced by the menu, they have no context as to where that menu came from and why. It won't completely derail anyone, but it's not a good user experience.

All it needs is to slide in from the left and suddenly the user has context for what's happening: “Oh, the menu was just sitting offscreen, waiting to be called.”

You can see a drawer menu example in almost every popular app these days and on most mobile versions of websites. The GMail and Facebook apps are both excellent examples of this concept.</p>

### The Single Page Application

The next trend we'll see are single page applications (SPAs). As we add motion and transitions to parts of our user interfaces, we'll start to want more control of the interface as a whole (not the interface within each page). Websites can now handle all kinds of transitions from state to state within a page, but what about the transition from page to page? Any small gap when the screen goes white or shifts content around hurts usability.

That explains **the rising popularity of the single page application**. Right now, there are a lot of popular frameworks to build SPAs, and they're more like native mobile applications than webpages (at least in some ways).

The sign-in and sign-up process for Dance It Yourself (an SPA I'm currently building) illustrates this well. If you go to [https://app.danceityourself.com](https://app.danceityourself.com), you'll see the page initially loads like a normal website, but if you tap the Sign Up button, instead of refreshing the page, the content either slides up from the bottom (on smaller screens) or in from the left (larger screens). The technique uses JavaScript to add a class to the Sign Up page, which triggers a CSS transition.

The result is a smooth, fast and logical transition from one screen to another. Once you sign in to the app, the entire experience is treated the same way. All the movement and transitions are driven by logic and context, and they make this web application feel more like a native application than a website.

## How To Do CSS Motion

Single page applications present a good opportunity to take advantage of CSS motion, but there are plenty of other places to use it, including potentially every element on every website you make from now on. But how do we actually do it? What does the CSS look like?

To understand the basics of CSS motion, **it's important to start simple**. What follows are explanations with examples, but they're definitely _minimum viable examples_. Follow some of the links to learn much more about the in-depth aspects of each type of CSS motion.</p>

### CSS Transitions

There are many times when a little transition can go a long way. Instead of changing properties of an element in a split second, a transition gives the user some real context and a visual clue as to what's happening and why.

This helps usability because it removes the mystery behind digital state change. In real life, based on physics, there is always a transition from any one thing to another. The human brain understands this, so it's important to translate that visual information into our interfaces.

To start explaining CSS transitions, let's first look at a state change without any transition.</p>

<pre><code class="language-css">button {
   margin-left:0;
}

button:hover {
   margin-left:10px;
}</code></pre>

When the user hovers over the button, it jumps 10 pixels to the right. Check out the [demo to see it in action](https://codepen.io/drewbrolik/pen/opskq).

Now let's add the most basic form of a transition. I've left out browser prefixes, but they're in the demos, because we still need to use them in production code.</p>

<pre><code class="language-css">button {
   margin-left:0;
   transition: margin-left 1s;
}

button:hover {
   margin-left:10px;
}</code></pre>

That code will animate the `margin-left` CSS property when a user hovers over the button. It will animate from 0 to 10px in 1 second.

Here's a [demo for that](https://codepen.io/drewbrolik/pen/ivzfK). Notice how unnatural it looks, though.

Next, we'll make the motion look a little more realistic with just a small adjustment.</p>

<pre><code class="language-css">button {
   margin-left:0;
   transition: margin-left .25s ease-out;
}

button:hover {
   margin-left:10px;
}</code></pre>

Here's [that demo](https://codepen.io/drewbrolik/pen/LFijf). This example looks nice and natural. There's probably little reason to animate the `margin-left` property of a button. You can imagine how this can apply to many different circumstances.

The last important thing to know about CSS transitions (and CSS animation for that matter), is that we can't animate every CSS property. As time goes on, we'll be able to animate more and more, but for now, we need to stick to a select few. Here's [a list of all the properties that will animate using the CSS `transition` property](https://css3.bradshawenterprises.com/transitions/#animatable).

When we talk about the hover state, it's easy to see how CSS transitions apply, but also consider triggering transitions by adding an additional class to an element. This trick will come in handy. How the class gets added has to do with your implementation, but any time a class is added or removed, it will trigger the CSS transition.</p>

<pre><code class="language-css">button {
   margin-left:0;
   transition: margin-left .25s ease-out;
}

button.moveRight {
   margin-left:10px;
}</code></pre>

### CSS Animations

The basic CSS for an animation is a little more complicated, but it's similar to CSS transitions in a lot of ways.

The reasons to use CSS animations are also similar to transitions, but there are some different applications. We want to emulate real life as much as possible so that human brains can do less work to understand what's going on. Unlike transitions, however, animations can be looped and can move independently of user input. Therefore, **we can use animation to draw attention to elements on a page**. Or we can add subtle movement to illustrations or background elements to give our interfaces some life.

Animation benefits may seem less tangible, but they're equally as important. It pays to add some fun to our interfaces. Users should love to use our products, and animation can have a big impact on the overall user experience.

Here's a shorthand example of a CSS animation. We use a block of CSS keyframes and give it a name, and we assign that keyframe animation to an element. Again, since browser prefixes add a lot of code, I didn't include them. I did, however, include them in the demo, because, unfortunately, we still need to include all browser prefixes in the real world.</p>

<pre><code class="language-css">div.circle {
   background:#000;
   border-radius:50%;
   animation:circleGrow 800ms ease-in-out infinite alternate both;
}

@keyframes circleGrow {
   0% {
      height:2px;
      width:2px;
   }
   50% {
      height:40px;
      width:40px;
   }
   100% {
      height:34px;
      width:34px;
   }
}</code></pre>

Here's the [animation demo](https://codepen.io/drewbrolik/pen/mJgqb).

To break it down, there are really only two things going on here.

First, there's the `animation` property itself. It's very much like the `transition` property, but it has a lot more that we can control. I used the shorthand version in my example, but just like the `transition` property, each part can be controlled as a separate CSS property (you probably do this with `background` all the time).</p>

<p>The shorthand <code>animation</code> property breaks down like this:<p>

<blockquote>animation: [animation name (from keyframe block)] [duration] [timing function] [delay] [number of times the animation repeats] [animation direction] [fill mode]
<br />
&#8594; <a href="https://www.css3files.com/animation/">Here's a more thorough explanation of all the different CSS animation properties</a>.</blockquote>

<p>The second thing going on is the keyframes block. At a very basic level, this is self explanatory. Set any number of percentages from 0–100 to represent how far through the animation we are from start (0%) to finish (100%). Then add any styles for that stage of the animation. When the animation runs, all styles will animate between the values you specify at each percentage number.</p>

<p>Again, not all properties animate, but as times goes on, we'll be able to do more and more.</p>

## How To Do CSS Motion Well

<p>Now that you know how to write the CSS for motion, it's time to think about using motion well. All of the concepts here will fail if executed improperly. Transition and animation need to feel real. If they don't, they'll be surprisingly distracting, and the distraction will actually hurt usability.</p>

<p>The trick to making motion look natural is two-fold: easing and object weight.</p>

### Easing

<p>You may have noticed the easing part in the code examples. In real life, objects start moving gradually and slow to a stop. Things don't just start moving at 100% speed. That's where the third property for the transition style comes in from the examples: <code>ease-out</code> or <code>ease-in</code>. Sometimes, your best bet is actually <code>ease-in-out</code> (<a href="https://css3.bradshawenterprises.com/transitions/#differentTiming">here's a list of all the possible easing (timing) functions</a>).</p>

### Weight

<p>Weight, on the other hand, is not a specific property of the transition or animation style. Weight mainly affects motion speed, and the basic concept is that smaller objects would have less physical weight in real life, so they'd move faster than larger objects. That's why we increased the transition speed on the button from the second to the third example above. A small button seems really slow when it takes 1 second to move 10 pixels. A quarter of a second seems much more natural. (You can also use milliseconds, as in the example below.)</p>

<pre><code class="language-css">transition: margin-left 250ms ease-out;</code></pre>

## A Tip If You're Just Getting Started

<p>This all may seem like a lot. If you're new to CSS transitions and animation, I'd recommend one important thing. Build in steps. If you write an entire, complex keyframes block in one shot and then add timing, easing and looping into the animation property, you'll find out very quickly that you're confused. It will be hard to tweak and edit that animation. Start simple, and build the animation up by testing and iterating.</p>

## Coming Full Circle

<p>When you're up and running and using CSS motion, you'll start to notice all kinds of different uses for these techniques. In most cases, it's much more than a bell and whistle or a superfluous add-on. Movement is a tool, and it conveys context, meaning, importance and more. It can be just as important as any other usability technique that we use today.</p>

<p>As interface designers take advantage of motion, and as interfaces start to behave more like objects and environments in the real world, usability and user experience will improve as well. Humans will have to think less about computer interfaces and therefore the interfaces will be easier to learn and easier to use. Users may feel like they're getting smarter or more tech savvy, but really, the interfaces are just conforming more to the ideas and concepts they're already familiar with in real life.</p>

<p>So <strong>take advantage of CSS motion as a usability tool</strong>. Help your users by giving them realism and context. The world on the small screen doesn't have to be so different from the real world around us, and the more similar it is, the easier it is for users to understand it.</p>

{{< signature "da, ml, og, il" >}}


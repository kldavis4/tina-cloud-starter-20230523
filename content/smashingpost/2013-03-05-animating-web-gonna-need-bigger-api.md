---
title: We’re Gonna Need A Bigger API!
slug: animating-web-gonna-need-bigger-api
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/557ffc85-4231-4dfa-85a7-7c293f95a207/intro1.jpg'
date: 2013-03-05T00:05:26.000Z
author: jake-archibald
description: >-
  Everyone likes stuff that moves about on the Web, right? Remember how you cried joyful tears when you first used `<marquee>`? I do. I nearly sobbed all the water out of my body as I gazed upon “JAKE’S COOL WEBSITE” bobbing back and forth in uppercase serif.
categories:
  - Coding
  - CSS
  - JavaScript
  - Animation
---
Of course, we’re more mature as an industry these days.

We’ve learned that <strong>users don’t want websites to look like a CSI console having a personal crisis</strong>; instead, we go for smooth transitions that enhance the experience, rather than being the experience themselves. In terms of animation APIs, we’ve been poorly catered to, leaving us to hack around with timers that weren’t really built for animation. Things have been steadily improving in that area, but the new <a href="https://dvcs.w3.org/hg/FXTF/raw-file/tip/web-anim/index.html">Web Animation specification</a> looks set to shake things up a lot.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Guide To CSS Animation: Principles and Examples](https://www.smashingmagazine.com/2011/09/the-guide-to-css-animation-principles-and-examples/)
*   [CSS3 Transitions: Thank God We Have A Specification!](https://www.smashingmagazine.com/2013/04/css3-transitions-thank-god-specification/)
*   [The State Of Animation 2014](https://www.smashingmagazine.com/2014/11/the-state-of-animation-2014/)
*   [An Introduction To CSS3 Keyframe Animations](https://www.smashingmagazine.com/2011/05/an-introduction-to-css3-keyframe-animations/)

So, why do we need a new animation spec? Don’t we have enough ways to animate things already?

{{% feature-panel %}}

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32900479-4fe8-490f-b455-e194386e63bc/intro.jpg"><img loading="lazy" decoding="async" class="125499" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32900479-4fe8-490f-b455-e194386e63bc/intro.jpg" alt="Optimizing the way to makes things move" width="500" height="350" /></a><br>
<em>Optimizing the way to make things move. (<a href="https://www.smashingmagazine.com/2011/09/14/the-guide-to-css-animation-principles-and-examples/">Image source</a>)</em>

## Let’s Animate A Thing!

Imagine we wanted to animate something horizontally from one left position to another, over three seconds, and then do something on completion. We can do this without JavaScript, using CSS animations, but if the start and end positions are programmatically determined, then we’ll need something that we can control from script.</p>

### Using `requestAnimationFrame`

If you’re performing visual updates with JavaScript, then you should be using <code>requestAnimationFrame</code>. It synchronizes itself to real screen updates, giving you as much time as possible to get everything ready for rendering. If the browser is on a 60 Hz screen (most are) and your frames can be constructed in less than a 60th of a second, then you’ll get 60 frames per second (FPS). <code>requestAnimationFrame</code> prevents you creating frames that don’t have time to display. Synchronizing to the screen’s rate is important; 30 FPS looks smoother than 40 FPS because 40 doesn’t divide into the screen’s native 60 Hz. HTML5 Rocks has a <a href="https://www.html5rocks.com/en/tutorials/speed/rendering/">great article on syncing to the screen</a>.

Unfortunately, jQuery <a href="https://github.com/jquery/jquery/blob/caac041fcc31724b8b579939e8053966559483ca/src/effects.js#L692">uses <code>setInterval</code></a>, which isn’t as smooth as <code>requestAnimationFrame</code>. <code>requestAnimationFrame</code> doesn’t trigger while the tab or window isn’t visible, which is <em>A Good Thing™</em>. Unfortunately, this has created backwards incompatibility with websites that rely on <code>setInterval</code>’s less optimal behavior of continuing to run in the background. You can opt into <code>requestAnimationFrame</code> via a <a href="https://github.com/gnarf37/jquery-requestAnimationFrame">plugin</a>. Go and add that to all of your pages using jQuery animation now — I promise to wait for you — just make sure that switching tabs doesn’t break your animations.

<strong>Anyway, enough chatting</strong>. Here’s a <a href="https://jsbin.com/iliket/14/quiet">simple animation using <code>raf</code></a>, moving a box horizontally from <code>250px</code> to <code>500px</code>. Note that the box starts at <code>0px</code>, so there’s a jump to <code>250px</code> when the animation starts; this proves we can start the animation from a point other than its current rendered position.

Here’s the code:
<pre class=" language-javascript"><code class=" language-javascript"><span class="token comment">// On button press…
</span><span class="token function">animateLeft<span class="token punctuation">(</span></span>elm<span class="token punctuation">,</span> <span class="token string">'250px'</span><span class="token punctuation">,</span> <span class="token string">'500px'</span><span class="token punctuation">,</span> <span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  console<span class="token punctuation">.</span><span class="token function">log<span class="token punctuation">(</span></span><span class="token string">"Done!"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span><span class="token comment">

// The implementation
</span><span class="token keyword">function</span> <span class="token function">animateLeft<span class="token punctuation">(</span></span>elm<span class="token punctuation">,</span> from<span class="token punctuation">,</span> to<span class="token punctuation">,</span> done<span class="token punctuation">)</span> <span class="token punctuation">{</span>
<span class="token comment">  // Turn our CSS values into numbers
</span><span class="token comment">  // We're being lazy and assuming they're in px
</span>  from <span class="token operator">=</span> <span class="token function">parseInt<span class="token punctuation">(</span></span>from<span class="token punctuation">,</span> <span class="token number">10</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  to <span class="token operator">=</span> <span class="token function">parseInt<span class="token punctuation">(</span></span>to<span class="token punctuation">,</span> <span class="token number">10</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token comment">  // Work out the amount we need to move the box
</span>  <span class="token keyword">var</span> diff <span class="token operator">=</span> to <span class="token operator">-</span> from<span class="token punctuation">;</span>

  <span class="token keyword">var</span> duration <span class="token operator">=</span> <span class="token number">3000</span><span class="token punctuation">;</span>
  <span class="token keyword">var</span> startTime <span class="token operator">=</span> performance<span class="token punctuation">.</span><span class="token function">now<span class="token punctuation">(</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">  // Set initial position
</span>  elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transform <span class="token operator">=</span> <span class="token string">'translate('</span> <span class="token operator">+</span> from <span class="token operator">+</span> <span class="token string">'px, 0)'</span><span class="token punctuation">;</span>

  <span class="token keyword">function</span> <span class="token function">frame<span class="token punctuation">(</span></span>time<span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token comment">  // How long has the animation been running?
</span>    <span class="token keyword">var</span> animTime <span class="token operator">=</span> time <span class="token operator">-</span> startTime<span class="token punctuation">;</span>
  <span class="token comment">  // Are we done?
</span>    <span class="token keyword">if</span> <span class="token punctuation">(</span>animTime <span class="token operator">&gt;</span><span class="token operator">=</span> duration<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token comment">  // It's likely that the last rendered position wasn't the
</span>    <span class="token comment">  // final position, so we set it here.
</span>      elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transform <span class="token operator">=</span> <span class="token string">'translate('</span> <span class="token operator">+</span> to <span class="token operator">+</span> <span class="token string">'px, 0)'</span><span class="token punctuation">;</span>

      <span class="token function">done<span class="token punctuation">(</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">else</span> <span class="token punctuation">{</span>
    <span class="token comment">  // What position should the box be in?
</span>      <span class="token keyword">var</span> position <span class="token operator">=</span> from <span class="token operator">+</span> <span class="token punctuation">(</span>animTime <span class="token operator">/</span> duration <span class="token operator">*</span> diff<span class="token punctuation">)</span><span class="token punctuation">;</span>
      elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transform <span class="token operator">=</span> <span class="token string">'translate('</span> <span class="token operator">+</span> position <span class="token operator">+</span> <span class="token string">'px, 0)'</span><span class="token punctuation">;</span>
    <span class="token comment">  // Request our next frame
</span>      <span class="token function">requestAnimationFrame<span class="token punctuation">(</span></span>frame<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
  <span class="token punctuation">}</span>
<span class="token comment">  // request our first frame
</span>  <span class="token function">requestAnimationFrame<span class="token punctuation">(</span></span>frame<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>

The above is the ideal according-to-specification code. In the working example, I had to deal with vendor prefixes on <code>requestAnimationFrame</code> and <code>transform</code>. We’re animating using <code>transform</code> and <code>translate</code>, rather than <code>left</code>, because they allow for <a href="https://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/">subpixel positioning and, therefore, smoother animation</a>, one of the advantages that Flash had over HTML for so long.

This is a <strong>pretty large and stinky chunk of code</strong> to simply animate a thing, and it would get a lot larger if we handled differing CSS units and easing. Of course, you could stick all of the complicated bits in a library and give yourself a simpler API. Here’s the frame-by-frame breakdown:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9772314-6a17-4ba0-9c5a-13d5a7ca72a8/image02.png"><img loading="lazy" decoding="async" class="124838" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e95dacbd-26ce-4ef5-a0c1-86d241aee773/image02-500.png" alt="image02-500" width="500" height="327" /></a>

This is the timeline view of Chrome Developer Tools while the animation is running. Each frame executes some JavaScript, recalculates the style and layout, paints the box, and then sends that to the GPU, which composites it to the page. The draw time spikes a few times, resulting in a jolt in the animation. This is caused by delays in interacting with the GPU (the gray spikes) or delays caused by other JavaScript (the yellow spikes).

This highlights a performance bottleneck of JavaScript-driven animation:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2e6f05e-1736-4f18-b2d4-adfb9649f12f/image01.png"><img loading="lazy" decoding="async" class="124840" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02cb6139-7677-4571-abab-9e22dcb4c744/image01-500.png" alt="image01-500" width="500" height="392" /></a>

Here, another bit of JavaScript does some stuff and takes 250 milliseconds to do it. While this is happening, our animation can’t move. In the real world, <strong>this could be a social-media button waking up and doing something slow</strong>, or it could be some of your own script triggered by a user interaction. In the example above, I made a <a href="https://jsbin.com/iliket/21/quiet">button that performs a <code>while</code> loop for 250 milliseconds</a> (I’m pretty sure this code is in every social-media button). If you press it during the animation, it will block the animation and look nasty.

I recently <a href="https://calendar.perfplanet.com/2012/snow-in-canvas-land/">sung the praises of <code>requestAnimationFrame</code> for animating canvas</a>, so why am I hatin’ on it now? JavaScript-driven animations aren’t a bad practice — they give you full control frame by frame and pixel by pixel when combined with <code>&lt;canvas&gt;</code> — but returning to JavaScript land 60 times a second is overkill for DOM animations that have a defined start and end. Ideally, we want to tell the browser all about our animation and <strong>leave it to do its thing</strong>, while we get on with something else.

Of course, we kinda have this already.</p>

### Using CSS Transitions

<pre class=" language-css"><code class=" language-css"><span class="token selector">.whatever </span><span class="token punctuation">{</span>
   <span class="token property">transform</span><span class="token punctuation">:</span> translate(250px, 0)<span class="token punctuation">;</span>
   <span class="token property">transition</span><span class="token punctuation">:</span> transform 3s linear<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
<span class="token selector">.whatever:hover </span><span class="token punctuation">{</span>
   <span class="token property">transform</span><span class="token punctuation">:</span> translate(500px, 0)<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>

CSS transitions and animations let the browser make all kinds of optimizations because it knows the end point of the animation. They’re not blocked by JavaScript on some platforms, such as Chrome for Android and desktop Chrome with threaded compositing enabled in <code>about:flags</code> (expect threaded compositing to arrive in more browsers).

Let’s script it!
<pre class=" language-javascript"><code class=" language-javascript"><span class="token keyword">function</span> <span class="token function">animateLeft<span class="token punctuation">(</span></span>elm<span class="token punctuation">,</span> from<span class="token punctuation">,</span> to<span class="token punctuation">,</span> done<span class="token punctuation">)</span> <span class="token punctuation">{</span>
 <span class="token comment"> // Set initial position
</span>  elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transform <span class="token operator">=</span> <span class="token string">'translate('</span> <span class="token operator">+</span> from <span class="token operator">+</span> <span class="token string">', 0)'</span><span class="token punctuation">;</span>
 <span class="token comment"> // Define the transition type
</span>  elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transition <span class="token operator">=</span> <span class="token string">'all 3s linear'</span><span class="token punctuation">;</span>

  <span class="token keyword">function</span> <span class="token function">transitionEnd<span class="token punctuation">(</span></span>event<span class="token punctuation">)</span> <span class="token punctuation">{</span>
   <span class="token comment"> // Beware of bubbled events
</span>    <span class="token keyword">if</span> <span class="token punctuation">(</span>event<span class="token punctuation">.</span>target <span class="token operator">!</span><span class="token operator">=</span> elm<span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token keyword">return</span><span class="token punctuation">;</span> <span class="token punctuation">}</span>
   <span class="token comment"> // Clear the transition
</span>    elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transition <span class="token operator">=</span> <span class="token string">’</span><span class="token punctuation">;</span>
   <span class="token comment"> // We don't want that listener firing for future anims
</span>    elm<span class="token punctuation">.</span><span class="token function">removeEventListener<span class="token punctuation">(</span></span><span class="token string">'transitionend'</span><span class="token punctuation">,</span> transitionEnd<span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token function">done<span class="token punctuation">(</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>

 <span class="token comment"> // Listen for end of transition
</span>  elm<span class="token punctuation">.</span><span class="token function">addEventListener<span class="token punctuation">(</span></span><span class="token string">'transitionend'</span><span class="token punctuation">,</span> transitionEnd<span class="token punctuation">)</span><span class="token punctuation">;</span>
 <span class="token comment"> // start the transition
</span>  elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transform <span class="token operator">=</span> <span class="token string">'translate('</span> <span class="token operator">+</span> to <span class="token operator">+</span> <span class="token string">', 0)'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>

Here’s a <a href="https://jsbin.com/iliket/16/quiet">live example</a>. It’s much simpler than our <code>raf</code> example, but a bug has crept in. The <code>from</code> is ignored; the animation starts from the element’s current position, even though we’ve explicitly set it to something else. Why?
<pre class=" language-javascript"><code class=" language-javascript"><span class="token comment">// Set initial position
</span>elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transform <span class="token operator">=</span> <span class="token string">'translate('</span> <span class="token operator">+</span> from <span class="token operator">+</span> <span class="token string">', 0)'</span><span class="token comment">;
// Define the transition type
</span>elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transition <span class="token operator">=</span> <span class="token string">'all 3s linear'</span><span class="token comment">;
// …and later…
</span><span class="token comment">// Start the transition
</span>elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transform <span class="token operator">=</span> <span class="token string">'translate('</span> <span class="token operator">+</span> to <span class="token operator">+</span> <span class="token string">', 0)'</span><span class="token punctuation">;</span>
</code></pre>

Changing properties in the <code>style</code> object doesn’t change the element’s computed style. The style is computed only when the browser needs to know the impact that those styles will have on the page (for example, when the element needs to be drawn). The element doesn’t need to be drawn between the two assignments to <code>elm.style.transform</code>, so the first assignment is ignored.

Of course, <strong>we can hack it</strong>:
<pre class=" language-javascript"><code class=" language-javascript"><span class="token comment">// Set initial position
</span>elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transform <span class="token operator">=</span> <span class="token string">'translate('</span> <span class="token operator">+</span> from <span class="token operator">+</span> <span class="token string">', 0)'</span><span class="token comment">;
// Abracadabra!
</span>elm<span class="token punctuation">.</span>offsetWidth<span class="token comment">;
// Define the transition type
</span>elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transition <span class="token operator">=</span> <span class="token string">'all 3s linear'</span><span class="token comment">;
// …and later…
</span><span class="token comment">// start the transition
</span>elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transform <span class="token operator">=</span> <span class="token string">'translate('</span> <span class="token operator">+</span> to <span class="token operator">+</span> <span class="token string">', 0)'</span><span class="token punctuation">;</span>
</code></pre>

<code>offsetWidth</code> returns the rendered width of an element, including padding. To calculate this, the browser needs to take into account all of the styles on the page, including the <code>transform</code> that we set for the initial position. That works. Check out the <a href="https://jsbin.com/iliket/17/quiet">live example</a>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ceb8edc-7f9b-4b4f-9f01-691dea36399f/image03.png"><img loading="lazy" decoding="async" class="124842" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f78b356b-4360-4367-bc51-b7b7524e8c7b/image03-500.png" alt="image03-500" width="500" height="279" /></a>

Performance is steady at 60 FPS. And we can see that each frame is a simple composite; all of the heavy lifting is farmed out to the GPU.

However, relying on <code>offsetWidth</code> to force the element into its starting position is hacky, and it’s conceivable that a <strong>future browser release will find a way to optimize out the reflow</strong>, breaking our hack.

Reflows are not without cost either:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22bea546-dadf-4106-9ae6-34d379db33f8/image00.png"><img loading="lazy" decoding="async" class="124844" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/360b1622-bcf0-4d06-9d95-7971e462734a/image00-500.png" alt="image00-500" width="500" height="279" /></a>

The Developer Tools warn us about this use of <code>offsetWidth</code>, because the browser calculates a layout that it never draws. The test page is very basic, so the layout cost is cheap, but things can be very different in the real world.

So, is there a less hacky, more reliable way?

### Enter CSS Animations

<a href="https://developer.mozilla.org/en-US/docs/CSS/Tutorials/Using_CSS_animations">CSS animations</a> have explicit keyframe values. Let’s script them:
<pre class=" language-javascript"><code class=" language-javascript"><span class="token keyword">function</span> <span class="token function">animateLeft<span class="token punctuation">(</span></span>elm<span class="token punctuation">,</span> from<span class="token punctuation">,</span> to<span class="token punctuation">,</span> done<span class="token punctuation">)</span> <span class="token punctuation">{</span>
 <span class="token comment"> // Create a style element for our animation
</span>  <span class="token keyword">var</span> style <span class="token operator">=</span> document<span class="token punctuation">.</span><span class="token function">createElement<span class="token punctuation">(</span></span><span class="token string">'style'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
 <span class="token comment"> // Generate a unique name
</span>  <span class="token keyword">var</span> animName <span class="token operator">=</span> <span class="token string">'anim'</span> <span class="token operator">+</span> Date<span class="token punctuation">.</span><span class="token function">now<span class="token punctuation">(</span></span><span class="token punctuation">)</span> <span class="token operator">+</span> Math<span class="token punctuation">.</span><span class="token function">floor<span class="token punctuation">(</span></span>Math<span class="token punctuation">.</span><span class="token function">random<span class="token punctuation">(</span></span><span class="token punctuation">)</span> <span class="token operator">*</span> <span class="token number">10000</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

 <span class="token comment"> // Build the CSS
</span>  style<span class="token punctuation">.</span>textContent <span class="token operator">=</span> <span class="token string">’</span> <span class="token operator">+</span>
    <span class="token string">'@keyframes '</span> <span class="token operator">+</span> animName <span class="token operator">+</span> <span class="token string">' { '</span> <span class="token operator">+</span>
      <span class="token string">'from { '</span> <span class="token operator">+</span>
        <span class="token string">'transform: translate('</span> <span class="token operator">+</span> from <span class="token operator">+</span> <span class="token string">', 0);'</span> <span class="token operator">+</span>
      <span class="token string">'}'</span> <span class="token operator">+</span>
      <span class="token string">'to {'</span>
        <span class="token string">'transform: translate('</span> <span class="token operator">+</span> to <span class="token operator">+</span> <span class="token string">', 0);'</span> <span class="token operator">+</span>
      <span class="token string">'}'</span> <span class="token operator">+</span>
    <span class="token string">'}'</span><span class="token punctuation">;</span>

 <span class="token comment"> // Add it to the page
</span>  document<span class="token punctuation">.</span>head<span class="token punctuation">.</span><span class="token function">appendChild<span class="token punctuation">(</span></span>style<span class="token punctuation">)</span><span class="token punctuation">;</span>

  <span class="token keyword">function</span> <span class="token function">transitionEnd<span class="token punctuation">(</span></span>event<span class="token punctuation">)</span> <span class="token punctuation">{</span>
   <span class="token comment"> // Beware of bubbled events
</span>    <span class="token keyword">if</span> <span class="token punctuation">(</span>event<span class="token punctuation">.</span>target <span class="token operator">!</span><span class="token operator">=</span> elm<span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token keyword">return</span><span class="token punctuation">;</span> <span class="token punctuation">}</span>
   <span class="token comment"> // Clear the animation
</span>    elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>animation <span class="token operator">=</span> <span class="token string">’</span><span class="token punctuation">;</span>
   <span class="token comment"> // Clean up the DOM
</span>    document<span class="token punctuation">.</span>head<span class="token punctuation">.</span><span class="token function">removeChild<span class="token punctuation">(</span></span>style<span class="token punctuation">)</span><span class="token punctuation">;</span>
   <span class="token comment"> // Retain the final position
</span>    elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transform <span class="token operator">=</span> <span class="token string">'translate('</span> <span class="token operator">+</span> to <span class="token operator">+</span> <span class="token string">', 0)'</span><span class="token punctuation">;</span>
   <span class="token comment"> // We don't want that listener firing for future anims
</span>    elm<span class="token punctuation">.</span><span class="token function">removeEventListener<span class="token punctuation">(</span></span><span class="token string">'animationend'</span><span class="token punctuation">,</span> transitionEnd<span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token function">done<span class="token punctuation">(</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>

 <span class="token comment"> // Listen for end of transition
</span>  elm<span class="token punctuation">.</span><span class="token function">addEventListener<span class="token punctuation">(</span></span><span class="token string">'animationend'</span><span class="token punctuation">,</span> transitionEnd<span class="token punctuation">)</span><span class="token punctuation">;</span>

 <span class="token comment"> // Start the animation
</span>  elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>animation <span class="token operator">=</span> animName <span class="token operator">+</span> <span class="token string">' 3s linear forwards'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>

<strong>Ugh! All of that just to move a thing?</strong> <a href="https://jsbin.com/iliket/18/quiet">It works</a>, but all of that DOM work is heavy-handed for what we’re trying to achieve. Also, if an animation is cancelled halfway through (for example, if the animation style is changed), then <code>animationend</code> will not fire — meaning that our <code>done</code> callback won’t fire or, worse, it’ll fire at the end of some future unrelated animation. There is no <code>animationcancel</code> event.</p>

### Web Animations, Save Us From This Mess!

It’s early days for the <a href="https://dvcs.w3.org/hg/FXTF/raw-file/tip/web-anim/index.html">Web Animations specification</a>, but it’s pretty exciting. It brings a boatload of animation performance and synchronization features natively to the DOM that JavaScript libraries currently have to hack their way through.

The specification itself is kinda terrifying. My heart sank as I opened the page and watched the scrollbar get smaller and smaller. But, thankfully, most of it is implementation detail.

Here’s how we’d script our animation <strong>in the brave new world of Web Animation</strong>:
<pre class=" language-javascript"><code class=" language-javascript"><span class="token comment">// Set our start position
</span>elm<span class="token punctuation">.</span>style<span class="token punctuation">.</span>transform <span class="token operator">=</span> <span class="token string">'translate(250px, 0)'</span><span class="token comment">;
// Animate to the end position
</span><span class="token keyword">var</span> anim <span class="token operator">=</span> elm<span class="token punctuation">.</span><span class="token function">animate<span class="token punctuation">(</span></span><span class="token punctuation">{</span>
  transform<span class="token punctuation">:</span> <span class="token string">'translate(500px, 0)'</span>
<span class="token punctuation">}</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">)</span><span class="token comment">;
// Do something on completion
</span>anim<span class="token punctuation">.</span>onend <span class="token operator">=</span> <span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  console<span class="token punctuation">.</span><span class="token function">log<span class="token punctuation">(</span></span><span class="token string">'Done!'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>
</code></pre>

Here, <code>elm</code> is an <code>HTMLElement</code>. The API is intuitive, especially if you’ve created animations with something like jQuery.

Like CSS animations and transitions, it <strong>gives the browser the full story up front</strong>, so we get all of the same optimizations without having to dynamically build CSS. Web Animations solves this by allowing us to tell the browser the full story of what we’re going to do. Then, the browser can go off and animate things itself.

Web Animations give us the scripting API to browser-driven animation that’s sorely missing. Above is the “Hello world” example. The <a href="https://dvcs.w3.org/hg/FXTF/raw-file/tip/web-anim/index.html">specification</a> includes advanced easing, path-based animation, parallelization, synchronization, interrupting and adapting, all in a way that the browser can take away from JavaScript land and optimize accordingly.

It’s still very early days, so don’t throw out your animation libraries yet. But if you want to experiment with the new API and provide feedback, a <a href="https://github.com/web-animations/web-animations-js">polyfill is tracking</a> the rapidly evolving spec. Exciting times!

{{< signature "al" >}}


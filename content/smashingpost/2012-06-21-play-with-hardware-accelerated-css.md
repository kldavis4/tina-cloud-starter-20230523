---
title: Let's Play With Hardware-Accelerated CSS
slug: play-with-hardware-accelerated-css
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2251b1b-9f49-48a1-b9bc-a663ad020ca9/css-practices-realworld.jpg
date: 2012-06-21T11:15:28.000Z
author: martin-kool
description: >-
  If you’re a developer of mobile Web apps, then you’ve heard this before: Native apps perform better than Web apps. But what does “perform better” mean?
categories:
  - Mobile
  - Optimization
  - CSS3
---
In the context above, performance is usually about measurable aspects such as loading time and responsiveness to user interaction. But more often than not, statements about performance lie within the realm of animations and transitions and how smooth they are. [Links checked February/21/2017]

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Hardware Hacking With JavaScript](https://www.smashingmagazine.com/2016/02/hardware-hacking-with-javascript-internet-of-things/)
*   [GPU Animation: Doing It Right](https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/)
*   [Prioritizing Devices: Testing And Responsive Web Design](https://www.smashingmagazine.com/2014/07/testing-and-responsive-web-design/)

## How Do We Get Smoother Transitions In A Mobile Web App?

We humans tend to perceive a transition as being “smooth” when the number of frames per second (FPS) drawn on the screen is above a certain cognitive threshold — about 30 or so, arguably. And one of the things that native apps have been particularly better at than Web apps is keeping the FPS high while swiping, tapping, pinching, executing and all other such verbs that were nonexistent a little over six years ago.

{{% feature-panel %}}

This is possible because native applications can access the device’s graphical processing unit (GPU) to make pixels fly. Web applications, on the other hand, run in the context of the browser, which lets the software do most (if not all) of the rendering, resulting in less horsepower for transitions. But the Web has been catching up, and most browser vendors now provide graphical hardware acceleration by means of particular CSS rules.

Knowing this is the key to getting smoother transitions on mobile Web apps. But this is old news, you say?

For some it may be, because it has been around for a while and has found its way into respected mobile Web frameworks such as <a href="https://www.sencha.com">Sencha</a>’s line of products. But if you’re doing any custom CSS or jQuery magic, then knowing how to kick those FPS up a notch manually is useful. So, in the name of science (and some good fun), let’s get our hands dirty.</p>

## Time To Roll Up Our Sleeves

We’re going to build a fun little slideshow that…

1.  uses hardware acceleration
2.  to present five full-screen slides
3.  of kittens
4.  to swipe through
5.  with a perfect touch:pixel ratio,
6.  that snap smoothly from one slide to the next,
7.  and that work on desktops, phones and tablets
8.  in portrait and landscape mode
9.  and throws Apple’s patented rubber-band-effect in the mix as a bonus,
10.  all in under 50 lines of code.

Really? Yes. Let’s get started!

First, we’ll create a simple HTML page that provides five full-screen slides of kittens, courtesy of <a href="https://placekitten.com/">placekitten</a>, and allows you to scroll through them. The page will consist of a single <code>#slides</code> container with five <code>.slide</code> elements, each of which has a background image stretched by CSS to fully cover the slide.

<pre><code class="language-markup tmp-html">&lt;!doctype html&gt;
&lt;html&gt;
   &lt;head&gt;
      &lt;meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no"/&gt;
      &lt;link href="style.css" type="text/css" rel="stylesheet" /&gt;
   &lt;/head&gt;
   &lt;body&gt;
      &lt;div id="slides"&gt;
         &lt;div class="slide"&gt;&lt;/div&gt;
         &lt;div class="slide"&gt;&lt;/div&gt;
         &lt;div class="slide"&gt;&lt;/div&gt;
         &lt;div class="slide"&gt;&lt;/div&gt;
         &lt;div class="slide"&gt;&lt;/div&gt;
      &lt;/div&gt;
   &lt;/body&gt;
&lt;/html&gt;</code></pre>

Most of this is fairly straightforward.  We’re using <a href="https://developer.apple.com/library/safari/#documentation/appleapplications/reference/SafariHTMLRef/Articles/MetaTags.html">well-known <code>viewport</code> meta tag</a> to prevent user scaling:

<pre><code class="language-markup tmp-html">&lt;meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no"/&gt;</code></pre>

<strong>Note</strong>: We’ll use the <code>-webkit-</code> vendor prefix in the demo files just for the sake of keeping the code short, and we'll stick to vanilla <code>div</code> elements and forget about user scaling to limit the scope of this article. This article does not attempt to be an example of how to make a cross-browser example for all mobile devices out there, but to illustrate the difference that GPU acceleration can make on mobile devices and—as the title suggests—“play” with it and get your coding hands dirty. In general, <strong>we should use prefixes for all browsers</strong> (at least the major ones) that support that feature (or plan to do so in near future): <code>-moz-</code>, <code>-ms-</code>, <code>-o-</code>, and <code>-webkit-</code>.

The <code>style.css</code> file will start with the following:

<pre><code class="language-css">html, body {
  height: 100%;
}

body {
  margin: 0;
  overflow: visible;
  background: #333;
}

#slides {
  width: 100%; height: 100%;
  white-space: nowrap;
  font-size: 0;
  -webkit-transform: translate3d(0,0,0);
  -moz-transform: translate3d(0,0,0);
  -ms-transform: translate3d(0,0,0);
  -o-transform: translate3d(0,0,0);
  transform: translate3d(0,0,0);
}

.slide {
  width: 100%; height: 100%;
  display: inline-block;
  background-size: cover;
}

.animate {
  -webkit-transition: all .3s ease-out;
  -moz-transition: all .3s ease-out;
  -ms-transition: all .3s ease-out;
  -o-transition: all .3s ease-out;
  transition: all .3s ease-out;
}

.slide:nth-child(1) { background: url(https://placekitten.com/640/480);}
.slide:nth-child(2) { background: url(https://placekitten.com/641/480);}
.slide:nth-child(3) { background: url(https://placekitten.com/642/480);}
.slide:nth-child(4) { background: url(https://placekitten.com/643/480);}
.slide:nth-child(5) { background: url(https://placekitten.com/644/480);}</code></pre>

Let’s look at the <code>#slides</code> declaration:

<pre><code class="language-css">#slides {
  width: 100%; height: 100%;
  white-space: nowrap;
  font-size: 0;
  -webkit-transform: translate3d(0,0,0);
  -moz-transform: translate3d(0,0,0);
  -ms-transform: translate3d(0,0,0);
  -o-transform: translate3d(0,0,0);
  transform: translate3d(0,0,0);
}</code></pre>

Our <code>#slides</code> div is set to be full screen. Because we’re using the <code>html</code> doctype, we also needed to make our <code>html</code> and <code>body</code> elements take up 100% of the width and height. The <code>#slides</code> container requires that none of its <code>.slide</code> children wrap, and the <code>0</code> font size removes any gaps between the slides when displayed horizontally.

The slides will be aligned like so:

<img class="111723 alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f2a4de8-d23a-44e1-92c2-1606523ff462/2-all-slides.png" alt="The alignment of images used in our demo." width="500" height="75" /><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f2a4de8-d23a-44e1-92c2-1606523ff462/2-all-slides.png"><br>
<em>The alignment of images used in our demo.</em></a>

However, only one slide will be visible at a time in full screen. The semi-transparent red box below represents the browser’s full screen.

<img class="111725" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d22cefd-c863-4db2-8501-9979b1e0aa50/3-onlye-1-slide-visible.png" alt="Only one slide will be visible at a time." width="500" height="78" /><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d22cefd-c863-4db2-8501-9979b1e0aa50/3-onlye-1-slide-visible.png"><br>
<em>Only one slide will be visible at a time.</em></a>

Then we’ll use the hardware-accelerated <code>-webkit-transform: translate3d</code> CSS rule to “translate” the slides’ horizontal (<code>x</code>) position to the left or right.

The WebKit blog <a href="https://www.webkit.org/blog/386/3d-transforms/">describes <code>translate3d</code> as follows</a>:
<blockquote><strong>translate3d(x, y, z), translateZ(z)</strong>
Move the element in x, y and z, and just move the element in z. Positive z is towards the viewer. Unlike x and y, the z value cannot be a percentage.</blockquote>

The fun part is that WebKit also offers a simpler 2D method that does the same thing: <code>translate(x, y)</code>. But <code>translate3d(x, y, z)</code> uses the GPU, and that’s what we want. For now, we’ll set it to <code>(0,0,0)</code>:

<pre><code class="language-javascript">transform: translate3d(0,0,0);</code></pre>

The following line makes sure that the slide’s background covers the entire element, regardless of its width or height:

<pre><code class="language-css">background-size: cover;</code></pre>

The combination of our <code>viewport</code> meta tag that sets the page’s width to <code>device-width</code> and each slide being 100% in width and height makes our application work full screen on desktops, tablets and mobiles, regardless of the viewport’s initial width. For instance, if you open up the page on an iPhone and scroll just a tiny bit to the left, you’ll see that the next slide is already entering the screen from the right:

<img class="111724" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/176048d7-422e-4e7e-b543-5903d9cf4798/3-iphone.png" alt="Screenshot of our app on the iPhone, scrolled just a tiny bit to the left." width="320" height="480" /><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/176048d7-422e-4e7e-b543-5903d9cf4798/3-iphone.png"><br>
<em>Screenshot of our app on the iPhone, scrolled just a tiny bit to the left.</em></a>

It doesn’t even matter whether you start in portrait or landscape mode (although today we won’t be adding support for adjusting to changes in orientation once the app has loaded).

To animate the slides to snap into view, we’ll define an extra class, named <code>animate</code>:

<pre><code class="language-css">.animate {
  transition: all .3s ease-out;
}</code></pre>

This is a CSS3 transition that tells Webkit to animate all of its properties using the <code>ease-out</code> path over 300 milliseconds.

We use the CSS3 <a href="https://www.w3.org/TR/selectors/#nth-child-pseudo"><code>nth-child</code></a> pseudo-class to make each slide display a different kitten in an image of the given width and height. We specify different dimensions in order to get different images because that’s how placekitten works.

<pre><code class="language-css">.slide:nth-child(1) { background: url(https://placekitten.com/640/480);}
.slide:nth-child(2) { background: url(https://placekitten.com/641/480);}
.slide:nth-child(3) { background: url(https://placekitten.com/642/480);}
.slide:nth-child(4) { background: url(https://placekitten.com/643/480);}
.slide:nth-child(5) { background: url(https://placekitten.com/644/480);}</code></pre>

Let’s open this up in Chrome or Safari on a desktop. This is what you should be seeing right now:

<img class="111722" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76918dba-759e-4503-aae8-02be45389337/1-basic-scrollable.png" alt="Our Web app so far, without any code" width="500" height="375" /><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76918dba-759e-4503-aae8-02be45389337/1-basic-scrollable.png"><br>
<em>Our Web app so far, without any code.</em></a>

That’s right. We see only one kitten presented full screen and a large horizontal scroll bar that grants access to the other four slides. Right now, there’s no animation and no sliding other than the default scrolling behavior.

## Adding The Page Slide Effect

Our approach to swiping each slide into view is for the user to hold down their finger or mouse and then move the entire <code>#slide</code> container, along with all of the slides in it. When the user stops moving, we let the browser animate the next (or previous) slide into view by means of a CSS transition. You can fine-tune or add to this basic set-up a lot afterwards if you like.

OK, first we need change <code>overflow: visible</code> to <code>overflow: hidden</code> in the <code>body</code> element’s CSS declaration to get rid of the default scrolling functionality.

<pre><code class="language-css">body {
  margin: 0;
  overflow: hidden;
  background: #333;
}</code></pre>

Then, we include jQuery and our own <code>script.js</code> file <a href="https://stackoverflow.com/questions/436411/where-is-the-best-place-to-put-script-tags-in-html-markup">just before the closing <code>body</code> tag</a>:

<pre><code class="language-markup tmp-html">&lt;script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js"&gt;&lt;/script&gt;
&lt;script src="script.js"&gt;&lt;/script&gt;</code></pre>

Below is the entire contents of <code>script.js</code>. It consists of three methods: <code>slideStart</code>, <code>slide</code> and <code>slideEnd</code>.

<pre><code class="language-javascript">$(function () {
  var sliding = startClientX = startPixelOffset = pixelOffset = currentSlide = 0,
  slideCount = $('.slide').length;

$('html').live('mousedown touchstart', slideStart);
  $('html').live('mouseup touchend', slideEnd);
  $('html').live('mousemove touchmove', slide);

function slideStart(event) {
    if (event.originalEvent.touches)
      event = event.originalEvent.touches[0];
    if (sliding == 0) {
      sliding = 1;
      startClientX = event.clientX;
    }
  }

 function slide(event) {
    event.preventDefault();
    if (event.originalEvent.touches)
      event = event.originalEvent.touches[0];
     var deltaSlide = event.clientX - startClientX;

if (sliding == 1 &amp;&amp; deltaSlide != 0) {
      sliding = 2;
      startPixelOffset = pixelOffset;
    }

if (sliding == 2) {
      var touchPixelRatio = 1;
      if ((currentSlide == 0 &amp;&amp; event.clientX &gt; startClientX) ||
          (currentSlide == slideCount - 1 &amp;&amp; event.clientX &lt; startClientX))
        touchPixelRatio = 3;
      pixelOffset = startPixelOffset + deltaSlide / touchPixelRatio;
      $('#slides').css('transform', 'translate3d(' + pixelOffset + 'px,0,0)').removeClass();
    }
  }

function slideEnd(event) {
    if (sliding == 2) {
      sliding = 0;
      currentSlide = pixelOffset &lt; startPixelOffset ? currentSlide + 1 : currentSlide - 1;
      currentSlide = Math.min(Math.max(currentSlide, 0), slideCount - 1);
      pixelOffset = currentSlide * -$('body').width();
      $('#temp').remove();
      $('&lt;style id="temp"&gt;#slides.animate{transform:translate3d(' + pixelOffset + 'px,0,0)}&lt;/style&gt;').appendTo('head');
      $('#slides').addClass('animate').css('transform', ’);
    }
  }
});</code></pre>

### Our Code Explained

Let’s go over these lines of code, shall we?

Within the local scope that jQuery so kindly presents us with <code>$(function() { … });</code>, we start by defining a few required variables, which we’ll explain later. We’ll add cross-platform listeners for basic “dragging” functionality, which we’ll use to do the page sliding:

<pre><code class="language-javascript">$('html').live('mousedown touchstart', slideStart);
$('html').live('mouseup touchend', slideEnd);
$('html').live('mousemove touchmove', slide);</code></pre>

### The slideStart Method

The <code>slideStart</code> method is triggered on a <code>mousedown</code> or <code>touchstart</code> event; and for cross-platform-ness, we’ll redefine the <code>event</code> parameter to the first touch property in our <code>touches</code> collection (i.e. the first finger) — if we’re on a mobile device, that is:

<pre><code class="language-javascript">function slide(event) {
  if (event.originalEvent.touches)
    event = event.originalEvent.touches[0];</code></pre>

Then, we detect whether the user is not sliding yet (<code>sliding == 0</code>) and store the mouse or touch position where the user initiated the slide:

<pre><code class="language-javascript">if (sliding == 0) {
  sliding = 1;
  startClientX = event.clientX;
}</code></pre>

### The Slide Method

Next, we’ll look at the <code>slide</code> method. This line stores the number of pixels that we’ve moved since our <code>mousedown</code> or <code>touchstart</code> event:

<pre><code class="language-javascript">var deltaSlide = event.clientX - startClientX;</code></pre>

So, if <code>sliding</code> was recently set to <code>1</code> and <code>deltaSlide</code> is not <code>0</code>, then that means the user has moved for the first time! We can consider this the actual “slide start” event. Then, we set <code>sliding</code> to <code>2</code> (which means the user is actually moving), and we store the current pixels that the entire <code>#slides</code> container was already changed to:

<pre><code class="language-javascript">sliding = 2;
startPixelOffset = pixelOffset;</code></pre>

If <code>sliding</code> is set to <code>2</code>, then that means the user was already moving. So, we set <code>touchPixelRatio</code> to its initial value of <code>1</code>, which means that the user is sliding exactly 1 pixel for every pixel of mouse or touch movement:

<pre><code class="language-javascript">if (sliding == 2) {
  var touchPixelRatio = 1;</code></pre>

So, what does the following code do then?

<pre><code class="language-javascript">if ((currentSlide == 0 &amp;&amp; event.clientX &gt; startClientX) ||
    (currentSlide == slideCount - 1 &amp;&amp; event.clientX &lt; startClientX))
  touchPixelRatio = 3;</code></pre>

Setting <code>touchPixelRatio</code> to <code>3</code> means the user has to move their mouse or finger by 3 pixels just to offset the slides by 1 pixel. See what we’re getting at here? Exactly: Apple’s rubber-band effect! The code above checks whether the user is sliding the first slide to the right or the last slide to the left. If they’re doing this, then we set <code>touchPixelRatio</code> to <code>3</code>.

Then, we calculate the number of pixels that we need to offset <code>#slides</code>.

<pre><code class="language-javascript">pixelOffset = startPixelOffset + deltaSlide / touchPixelRatio;</code></pre>

To make the offset in pixels visible, we could use CSS <code>left</code> positioning or a negative left margin, but neither is hardware accelerated. That’s why we’ll use <code>transform:translate3d(x, y, z)</code> to make the offset final:

<pre><code class="language-javascript">$('#slides').css('transform', 'translate3d(' + pixelOffset + 'px,0,0)').removeClass();</code></pre>

So, we move x by the <code>pixelOffset</code>’s number of pixels, and we leave y and z alone. The <code>removeClass()</code> will remove the snapping <code>.animation</code> class that we will add in the <code>slideEnd</code> method, which we’ll now dive into.</p>

### The slideEnd Method

When the user stops sliding, we want the previous or next slide to smoothly animate into view. First, we need to know which slide should be in view:

<pre><code class="language-javascript">function slideEnd(event) {
  if (sliding == 2) {
    sliding = 0;
    currentSlide = pixelOffset &lt; startPixelOffset ? currentSlide + 1 : currentSlide - 1;</code></pre>

Then we <code>min</code> and <code>max</code> it out between <code>0</code> and <code>slideCount</code>:

<pre><code class="language-javascript">currentSlide = Math.min(Math.max(currentSlide, 0), slideCount - 1);</code></pre>

The value of the final <code>pixelOffset</code> is simple: it’s the viewport’s full width in pixels multiplied by the <code>currentSlide</code>’s number. And because we’re offsetting pixels to the left, we want the negative result:

<pre><code class="language-javascript">pixelOffset = currentSlide * -$('body').width();</code></pre>

Almost there. First, take a look at this line of code:

<pre><code class="language-javascript">$('&lt;style id="temp"&gt;#slides.animate{transform:translate3d(' + pixelOffset + 'px,0,0)}&lt;/style&gt;').appendTo('head');</code></pre>

This is the simplest approach to dynamically adding a new CSS rule. We create a <code>style</code> element, with an <code>animate</code> class applied to <code>#slides</code>, which would have changed its <code>translate3d</code> offset to the full slide’s <code>pixeloffset</code>. But because our original <code>style.css</code> file has this line…

So, what does the following code do then?

<pre><code class="language-javascript">if ((currentSlide == 0 &amp;&amp; event.clientX &gt; startClientX) ||
    (currentSlide == slideCount - 1 &amp;&amp; event.clientX &lt; startClientX))
  touchPixelRatio = 3;</code></pre>

Setting <code>touchPixelRatio</code> to <code>3</code> means the user has to move their mouse or finger by 3 pixels just to offset the slides by 1 pixel. See what we’re getting at here? Exactly: Apple’s rubber-band effect! The code above checks whether the user is sliding the first slide to the right or the last slide to the left. If they’re doing this, then we set <code>touchPixelRatio</code> to <code>3</code>.

Then, we calculate the number of pixels that we need to offset <code>#slides</code>.

<pre><code class="language-javascript">pixelOffset = startPixelOffset + deltaSlide / touchPixelRatio;</code></pre>

To make the offset in pixels visible, we could use CSS <code>left</code> positioning or a negative left margin, but neither is hardware accelerated. That’s why we’ll use <code>transform:translate3d(x, y, z)</code> to make the offset final:

<pre><code class="language-javascript">$('#slides').css('transform', 'translate3d(' + pixelOffset + 'px,0,0)').removeClass();</code></pre>

So, we move x by the <code>pixelOffset</code>’s number of pixels, and we leave y and z alone. The <code>removeClass()</code> will remove the snapping <code>.animation</code> class that we will add in the <code>slideEnd</code> method, which we’ll now dive into.</p>

### The slideEnd Method

When the user stops sliding, we want the previous or next slide to smoothly animate into view. First, we need to know which slide should be in view:

<pre><code class="language-javascript">function slideEnd(event) {
  if (sliding == 2) {
    sliding = 0;
    currentSlide = pixelOffset &lt; startPixelOffset ? currentSlide + 1 : currentSlide - 1;</code></pre>

Then we <code>min</code> and <code>max</code> it out between <code>0</code> and <code>slideCount</code>:

<pre><code class="language-javascript">currentSlide = Math.min(Math.max(currentSlide, 0), slideCount - 1);</code></pre>

The value of the final <code>pixelOffset</code> is simple: it’s the viewport’s full width in pixels multiplied by the <code>currentSlide</code>’s number. And because we’re offsetting pixels to the left, we want the negative result:

<pre><code class="language-javascript">pixelOffset = currentSlide * -$('body').width();</code></pre>

Almost there. First, take a look at this line of code:

<pre><code class="language-javascript">$('&lt;style id="temp"&gt;#slides.animate{transform:translate3d(' + pixelOffset + 'px,0,0)}&lt;/style&gt;').appendTo('head');</code></pre>

This is the simplest approach to dynamically adding a new CSS rule. We create a <code>style</code> element, with an <code>animate</code> class applied to <code>#slides</code>, which would have changed its <code>translate3d</code> offset to the full slide’s <code>pixeloffset</code>. But because our original <code>style.css</code> file has this line…

<pre><code class="language-css">.animate {
  -webkit-transition: all .3s ease-out;
  -moz-transition: all .3s ease-out;
  -o-transition: all .3s ease-out;
  -ms-transition: all .3s ease-out;
  transition: all .3s ease-out;
}</code></pre>

… then a CSS animation will kick in using the hardware-accelerated <code>translate3d</code> property. Yay!

To clean up, we remove any existing <code>#temp</code> style elements from the <code>head</code> section prior to creating a new one:

<pre><code class="language-javascript">$('#temp').remove();</code></pre>

So, now we’ve got the current (runtime) style set to the current <code>pixelOffset</code> value, and the <code>animate</code> class is set to point <code>#slides</code> to the final position. All we need to do now is swap the style for a class, and the transition will take over:

<pre><code class="language-javascript">$('#slides').addClass('animate').css('transform', ’);</code></pre>

See? We’ve added the <code>animate</code> class and reset the <code>style</code> property of <code>webkit-transform</code> to nothing.</p>

## What Do We Have Now?

If all has gone well, we can open up our work in Chrome, Safari, iPad or iPhone and swipe through these kittens with ease. For those of you who didn’t code along, you can still <a href="https://webkitten.handcraft.com">see the result</a>.

Remember when we hadn’t yet included our own JavaScript?

Our current result seems very similar to the result as viewed on an iPad or iPhone, doesn’t it? You can swipe to scroll, and it has rubber-banding. But our app snaps in between slides, and the fact that the smoothness of its scrolling is comparable to a native app’s means that hardware acceleration has indeed kicked up the user experience a few notches and brought it closer to the result otherwise seen only in native apps.

And that’s what we set out to do, isn’t it?

As icing on the cake, we can now add features such as a permanent scrub bar at the bottom; round bullets to indicate the number of slides and which slide is active; and a transparent logo to overlay the screen and have the slides move underneath it. I’ve gone ahead and added such features here, so you can <a title="Icing on the Cake" href="https://webkitten2.handcraft.com">view the source</a> if you like.

<a href="https://webkitten2.handcraft.com/"><img loading="lazy" decoding="async" class="111913" title="Icing On The Cake" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9c9d774-595c-46ba-b3b2-b64fc1e2190e/icing.png" alt="" width="501" height="494" /></a><br>
<em><a href="https://webkitten2.handcraft.com/">View Web app</a>.</em>

## Want Proof That Hardware Acceleration Is Enabled?

If the experience itself doesn’t convince you or your coworker, here’s how to know for sure that the GPU is doing the work. Surf to <code>about:flags</code> in Chrome, enable the FPS counter, and hit the “Relaunch now” button at the bottom of the page.

<img class="111728" title="about-flags" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd5fd68f-799e-4343-a083-9f2ac1ae6979/about-flags.png" alt="Chrome offers an FPS counter when hardware acceleration is active." width="500" height="375" /><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd5fd68f-799e-4343-a083-9f2ac1ae6979/about-flags.png"><br>
<em>Chrome offers an FPS counter when hardware acceleration is active.</em></a>

Chrome will now show a red FPS counter in the top-left corner of any screen whenever the GPU is active. If you open our demo now, this is what you’ll see:

<img loading="lazy" decoding="async" class="111727" title="5-gpu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8060e7e0-1b24-4050-a149-77de0678569e/5-gpu.png" alt="Chrome with its FPS counter turned on, which is only visible when the GPU is active" width="500" height="375" /><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8060e7e0-1b24-4050-a149-77de0678569e/5-gpu.png"><br>
<em>Chrome with its FPS counter turned on, which is visible only when the GPU is active.</em></a>

To see what happens when we do not access the GPU, we need to make some alterations. In <code>style.css</code>, remove this line from the <code>#slides</code> declaration entirely:

<pre><code class="language-css">transform: translate3d(0,0,0);</code></pre>

In <code>script.js</code>, replace the two occurrences of this…

<pre><code class="language-css">translate3d(' + pixelOffset + 'px,0,0)</code></pre>

… with this:

<pre><code class="language-css">translate(' + pixelOffset + 'px,0)</code></pre>

Note that the replacement <code>translate</code> method takes two arguments (<code>x</code> and <code>y</code>) instead of three.

Now, if you refresh the page in Chrome, you’ll see that the FPS counter is not active:

<img class="111726" title="4-no-gpu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6fee083-bed6-4ff8-9a83-8d7fd7ca8f11/4-no-gpu.png" alt="Our Web app with no FPS counter anymore." width="500" height="375" /><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6fee083-bed6-4ff8-9a83-8d7fd7ca8f11/4-no-gpu.png"><br>
<em>Our Web app with no FPS counter anymore.</em></a>

Now that you’ve changed the sliding mechanism from <code>translate3d</code> to <code>translate</code>, try to swipe the kittens again. Notice the jagged behavior?

## What Are The Cons?

We have demonstrated that using certain CSS3 properties will kick in the GPU. We have experienced smoother interaction and transitions as a result, so that’s pretty cool. But are there disadvantages to this approach?

Two come to mind — one of which might actually be a pro.</p>

### Stability

One thing to keep in mind is that the positive results we’ve seen might not be present in all hardware combinations, because these 3D CSS techniques are relatively new to the Web. On some machines you might experience no hardware acceleration, a garbled screen or no content at all depending on your GPU chip and its support by the browser.

Lucky for us, this does work on all (modern) iOS devices and quite a few newer Android gadgets. I did encounter hiccups on one iMac at the office, but its hardware chip seems to have been whitelisted recently because it seemed to work all of a sudden after the browser (Chrome) updated.

All other PCs and Macs that I tested showed positive results.</p>

### Battery Life

To be honest I don’t have statistics on this one. Using the GPU will use battery life, but it saves on CPU cycles, so I guess it could go either way. If you have any information or statistics on this, please share it in the comments below.</p>

## Final Thoughts

Knowing when and how to apply hardware acceleration to Web-based transitions and effects can be very helpful when building a mobile Web application or even a game. As the Web evolves, your options grow for creating a friendly experience for end users by speeding up basic things such as the page-sliding transitions that we covered here. And while you can safely use existing Web development frameworks and rely on them to make use of hardware-accelerated CSS when appropriate, having some hands-on experience with tweaking Web applications even further is useful.

<em>(al) (jc)</em>


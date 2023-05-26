---
title: 'Orbit and Reveal: jQuery Plug-Ins For Image Sliders and Modal Windows'
slug: orbit-and-reveal-jquery-plug-ins-that-will-breathe-life-into-your-pages
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8379ba5-d65c-47b2-847a-6515e2acc0d1/orbit-screen.png
date: 2011-07-15T11:32:55.000Z
author: vitaly-friedman
summary: >-
   Two jQuery plug-ins that were developed exclusively for Smashing Magazine readers to liven up your developer tool belts: Orbit, a slider; and Reveal, a modal plug-in.
description: >-
   A visitor comes to your website all giddy to learn more about your product, when suddenly a snazzy slideshow loads with some snap. Impressed, they go to register and are greeted by a most elegant modal window. At this point they are finally overjoyed by the velociraptor that suddenly charges across their screen. They don’t know why but they like it.
categories:
  - Coding
  - JavaScript
  - jQuery
---

Crafting a polished and unique experience for your users is becoming ever more critical as the Web gets more  overloaded. Standing out is hard. To the rescue come frameworks such as jQuery, which offer a modular, highly customizable experience for your visitors.

Today, we are thrilled to introduce two new **jQuery plug-ins that were developed exclusively for Smashing Magazine readers** to liven up your developer tool belts: *Orbit*, a new slider; and *Reveal*, a modal plug-in.

{{% feature-panel %}}

## Why Create Our Own?

Quickly, before diving into the details, some background would be helpful. There are hundreds of jQuery image and content sliders and probably thousands of modal plug-ins. So, why create our own? We wrote these for **a number of reasons**, the most important ones being:

*   **Flexibility**.  We use these plug-ins for clients, internal projects, our apps and a number of other places. We can easily tweak and re-use the code for specific and special implementations.
*   **Experience**.  There is no better way to learn how to create better plug-ins and code than to do it yourself and release it publicly. Orbit has undergone a number of iterations and rewrites, which we learned from. Reveal has undergone only a few. We got Raptorize right the first time and haven’t had to update it.
*   **Better interactions and development**.  Perhaps the biggest driver was that, across our team, we used a number of plug-ins that have different quirks and features, but none of them nailed the features and interactions that we wanted. Developing plug-ins allowed us to work from a uniform codebase, iterate and optimize our work.

Have a look at a couple of our previous articles:

*   [Spicing Up Your Website with jQuery Goodness](https://www.smashingmagazine.com/2010/06/15/spice-up-your-website-with-jquery-goodness/ "Spicing up your website with jQuery goodness")  
Demonstrates several creative techniques for increasing usability with jQuery.
*   [Stronger, Better, Faster Design with CSS3](https://www.smashingmagazine.com/2009/12/stronger-better-faster-design-with-css3/ "Stronger, Better, Faster Design with CSS3")  
Introduces some powerful uses of the upcoming CSS3 standard.

## Orbit: jQuery Image Slider

First up is our new jQuery slider, Orbit. At a mere 4 KB, Orbit can handle images, linked images and straight-up content blocks. Setting it up takes just a few minutes, and it has some styles out of the box. We started working on Orbit because of all the many jQuery image sliders, none seemed straightforward to implement or had nice default styles. After several iterations and releases, the addition and removal of a number of features and some serious learning, we had a plug-in that perfectly fit our needs.

Let’s dive into the code, shall we?

<figure><a href="https://www.zurb.com/playground/orbit-jquery-image-slider"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28bd07b2-0a2a-4554-8975-236c451d8f17/orbit-screen.png" alt="Orbit jQuery Image Slider"></a><figcaption>Orbit jQuery Image Slider.</figcaption></figure>

### The Code

To get started, you’ll need <a title="Download jQuery" href="https://jquery.com">jQuery</a> and the <a title="Download Orbit Plugin" href="https://matt.zurb.s3.amazonaws.com/orbit-1.2.3.zip">Orbit plug-in</a> (make sure jQuery is attached first).

<pre><code class="language-markup tmp-xml">&lt;script src="js/jquery.min.js" type="text/javascript"&gt;&lt;/script&gt;
&lt;script src="js/jquery.orbit.min.js" type="text/javascript"&gt;&lt;/script&gt;</code></pre>

Now we can quickly hook up the CSS that we need:

<pre><code class="language-markup tmp-xml">&lt;link rel="stylesheet" href="css/orbit.css"&gt;</code></pre>

Finally, let’s dig into the mark-up.

<pre><code class="language-markup tmp-xml">&lt;div id="featured"&gt;
   &lt;img src="overflow.jpg" alt="Overflow: Hidden No More" /&gt;
   &lt;img src="captions.jpg"  alt="HTML Captions" /&gt;
   &lt;img src="features.jpg" alt="and more features" /&gt;
&lt;/div&gt;</code></pre>

Just a couple of notes before moving on:

1.  Orbit will dynamically determine the height and width of your set of images and scale accordingly, but make sure that all of your images are the same size or else the larger ones will peek out at the sides.
2.  You’ll notice that the `id` of the parent div is `featured`, but it doesn’t have to be. When you call the Orbit plug-in, you can set your own selector, and then the magical `orbit` class will be applied.

All we need to do now is activate the Orbit plug-in.

<pre><code class="language-javascript">&lt;script type="text/javascript"&gt;
   $(window).load(function() {
      $('#featured').orbit();
   });
&lt;/script&gt;</code></pre>

There you have it: Orbit, implemented and ready to be used with all of the default settings. To see more options, clean up the slider and do more advanced customization, please continue reading.

### Neato Options

Of course, you’ll want some other features like HTML captions, bullet navigation (with thumbnails), and using content instead of images. Here’s the low-down on how to get these going.

Here are all of the **plug-in parameters** and their default states. The options are commented out to the right. Go nuts!

<pre><code class="language-javascript">$('#featured').orbit({
  animation: 'fade',               // fade, horizontal-slide, vertical-slide, horizontal-push
  animationSpeed: 800,             // how fast animations are
  timer: true,                     // true or false to have the timer
  advanceSpeed: 4000,              // if timer is enabled, time between transitions
  pauseOnHover: false,             // if you hover pauses the slider
  startClockOnMouseOut: false,     // if clock should start on MouseOut
  startClockOnMouseOutAfter: 1000, // how long after MouseOut should the timer start again
  directionalNav: true,            // manual advancing directional navs
  captions: true,                  // do you want captions?
  captionAnimation: 'fade',        // fade, slideOpen, none
  captionAnimationSpeed: 800,      // if so how quickly should they animate in
  bullets: false,                  // true or false to activate the bullet navigation
  bulletThumbs: false,             // thumbnails for the bullets
  bulletThumbLocation: '',         // location from this file where thumbs will be
  afterSlideChange: function(){}   // empty function
});</code></pre>

### Full HTML Captions

Orbit has **full HTML captions**, so you can add styles, links, lists or whatever else your coding heart desires.

1.  Add a span with the class `orbit-caption` and an ID of your choosing after the slider div. Put whatever HTML you’d like to appear in the caption inside. They’re block level, so anything goes.
2.  Add the span ID you chose to the `data-caption` attribute of the corresponding image tag.

Check it out:

<pre><code class="language-markup tmp-xml">&lt;div id="featured"&gt;
   &lt;img src="overflow.jpg" alt="Overflow: Hidden No More" /&gt;
   &lt;img src="captions.jpg"  alt="HTML Captions" data-caption="#htmlCaption" /&gt;
   &lt;img src="features.jpg" alt="and more features" /&gt;
&lt;/div&gt;
&lt;!-- Captions for Orbit --&gt;
&lt;span class="orbit-caption" id="htmlCaption"&gt;I'm a badass caption&lt;/span&gt;</code></pre>

<strong>Want to animate those captions?</strong> Just change the <code>captionAnimation</code> parameter (<code>fade</code>, <code>slideOpen</code>, <code>none</code>).

### Bullet Navigation

Getting a new bullet navigation is as easy as passing a parameter when you call the Orbit function. The bullet navigation is natively an unordered list, but in the example and in the kit we’ve replaced them with nice little round bullets. (Changing this is a just a matter of changing the CSS to whatever you’d like.)

<pre><code class="language-javascript">&lt;script type="text/javascript"&gt;
   $(window).load(function() {
      $('#featured').orbit({
         bullets: true
      });
   });
&lt;/script&gt;</code></pre>

Orbit can now **pull thumbnails** for your bullet navigation! First, create your thumbnail and save it somewhere in your file directory. Below is the HTML, CSS and JavaScript to make it work:

<pre><code class="language-markup tmp-xml">&lt;!-- THE MARKUP --&gt;

&lt;div id="featured"&gt;
   &lt;img src="overflow.jpg" alt="Overflow: Hidden No More" /&gt;
   &lt;img src="captions.jpg"  alt="HTML Captions" data-thumb="captions-thumb.jpg"/&gt;
   &lt;img src="features.jpg" alt="and more features" /&gt;
&lt;/div&gt;

// The JS
&lt;script type="text/javascript"&gt;
$(window).load(function() {
   $('#featured').orbit({
      'bullets' : true,
      'bulletThumbs': true,
      'bulletThumbLocation': 'orbit/'
   });
});
&lt;/script&gt;

/* The CSS: Just provide a width and height for the thumb.
All bullet navigation thumbs will have a class added "has-thumb"
*/

.orbit-bullets li.has-thumb {
   width: 100px;
   height: 75px; }</code></pre>

{{% ad-panel-leaderboard %}}

### Using Text

Orbit is **text-compatible**, too. It can be mixed with images, but just make sure your text is in a <code>div</code> tag and has a background of some type (otherwise the images behind it will be visible). To make the text look nice, give it a background (so that other images in Orbit don’t bleed behind it). Just drop it right into the mark-up, this way:

<pre><code class="language-markup tmp-xml">&lt;div id="featured"&gt;
   &lt;div class="content" style=""&gt;
      &lt;h1&gt;Orbit does content now.&lt;/h1&gt;
      &lt;h3&gt;Highlight me: I'm text.&lt;/h3&gt;
   &lt;/div&gt;
   &lt;img src="overflow.jpg" alt="Overflow: Hidden No More" /&gt;
   &lt;img src="captions.jpg"  alt="HTML Captions" /&gt;
   &lt;img src="features.jpg" alt="and more features" /&gt;
&lt;/div&gt;</code></pre>

**Using only text?** Orbit relies on image sizes to get its dimensions. However, you can just go into the Orbit CSS and find the <code>.orbit</code> div declaration and set it to the exact pixel width and height you want.

### Making Orbit Shine

Orbit looks fairly reasonable out of the box (so to speak), but getting a real polish requires a couple more bits of work: in particular, getting a load before images pop in, and adding fixes for some less fortunate browsers (i.e. IE).

### Glorious, Seamless Loading State

For those in pursuit of the ultimate polish, we’ve made it easy to create a simple loading state for your slider. Add the following declaration anywhere in the CSS (just replace <code>featured</code> with your slider’s ID, and use your own images’ widths and heights):

<pre><code class="language-css">#featured {
      width: 940px;
      height: 450px;
      background: #000 url('orbit/loading.gif') no-repeat center center; overflow: hidden; }
   #featured img,
   #featured div { display: none; }</code></pre>

Apply the CSS to your unique slider ID, because the plug-in won’t know the ID until after it loads. Adding this CSS will prevent any unstyled content from flashing before the plug-in finishes loading. These styles are in the demo CSS in the kit.

### Non-Relative Positioning

The way Orbit works is that your container gets wrapped by another container. This means that if you are positioning your slider <code>absolute</code> or want to center it with <code>margin: 0 auto</code>, applying these to your slider’s ID (<code>#featured</code> in this example) won’t work. The best way to solve this is to put all positioning pieces on your ID and <code>div.orbit-wrapper</code>.

<pre><code class="language-css">#featured, div.orbit-wrapper {
   position: absolute;
   top: 50px;
   left: 50px;
}</code></pre>

**Note:** You could also just position the parent container of the Orbit slider if there is one.

As we all know, **IE<** is not a designer or developer’s best friend, but we’ll try to make it easy on you. As of version 1.1, Orbit **works in IE7+**, but because CSS3 transforms and RGBa aren’t available, we have to perform some magic to fix the timer and caption default background. The easiest way to fix these issues is to hide the timer and to use Microsoft’s proprietary alpha solution. You can use the following conditional declaration in the header of your document.

<pre><code class="language-markup tmp-xml">&lt;!--[if IE]&gt;
   &lt;style type="text/css"&gt;
      .timer { display: none !important; }
      div.caption { background:transparent;
      filter:progid:DXImageTransform.Microsoft.gradient(startColorstr=#99000000,endColorstr=#99000000);
      zoom: 1; }
   &lt;/style&gt;
&lt;![endif]--&gt;</code></pre>


<a href="https://www.zurb.com/playground/orbit-jquery-image-slider">Orbit: jQuery Image Slider</a>

Orbit helps you make your images slide around.  Check out our demo to see the plug-in in action. It works best in Chrome, Safari, Firefox 3.5+ (but is tested for IE 7+, Firefox 3.5+, Chrome and Safari).

<a href="https://www.zurb.com/playground/orbit-jquery-image-slider">Live demo</a>

<figure><a href="https://www.zurb.com/playground/orbit-jquery-image-slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5333a168-fa4d-40f7-8ecd-e7d6569b9106/orbit-small-thumb.jpg" alt="Orbit: jQuery Image Slider" /></a><figcaption>Orbit: jQuery Image Slider.</figcaption></figure>

## Reveal: jQuery Modals Made Easy

You can create **beautiful modal windows** on your page with our jQuery Reveal plug-in. Modal windows allow developers to make critical information stand out. Setting up Reveal modals takes only three easy steps. Attach the needed files, drop in the modal mark-up, then add an attribute to your button.

We created Reveal because we couldn’t find a simple solid solution. We often used and reused our own scripts to create modals because existing plug-ins were too heavy (they allowed for Flash integration and a hundred other things), and they didn’t use basic CSS to create flexible, reusable code. We think we’ve solved both of these issues with Reveal.

<figure><a href="https://www.zurb.com/playground/reveal-modal-plugin"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08967b13-9c19-4306-b20a-a04d87214c6d/reveal-screen.png" alt="Reveal modal plug-in" /></a><figcaption>Reveal modal plug-in.</figcaption></figure>

Reveal is useful because it’s easy to implement, compatible with modern browsers (with some graceful degradation, of course) and lightweight (coming in at only 1.75 KB). What this means for you is that it’s fast, sexy and just works.

Let’s see how you can get Reveal working!

### Step 1: Attach the Required Files

<pre><code class="language-markup tmp-xml">/* Attach the Reveal CSS */
&lt;link rel="stylesheet" href="reveal.css"&gt;

/* jQuery needs to be attached */
&lt;script src="jquery.min.js" type="text/javascript"&gt;&lt;/script&gt;

/* Then just attach the Reveal plug-in */
&lt;script src="jquery.reveal.js" type="text/javascript"&gt;&lt;/script&gt;</code></pre>

Clearly, you need the Reveal kit (.zip) to do this, so please download it first.

### Step 2: The Modal Mark-Up

<pre><code class="language-markup tmp-xml">&lt;div id="myModal" class="reveal-modal"&gt;
   &lt;h1&gt;Modal Title&lt;/h1&gt;
   &lt;p&gt;Any content could go in here.&lt;/p&gt;
   &lt;a class="close-reveal-modal"&gt;&#215;&lt;/a&gt;
&lt;/div&gt;</code></pre>

Just give your modal div the class <code>reveal-modal</code> and a unique ID (we’ll use the ID to launch this modal). The anchor with the class <code>close-reveal-modal</code> provides a button to close the modal (although by default, clicking the faded black background will also close the modal). Placing the mark-up just before the closing <code>body</code> tag is usually best.

### Step 3: Attach Your Handler

<pre><code class="language-javascript">&lt;a href="#" data-reveal-id="myModal"&gt;Click Me For A Modal&lt;/a&gt;</code></pre>

By putting the <code>data-reveal-id</code> attribute on the anchor, the plug-in, when clicked, matches the value of the <code>data-reveal-id</code> attribute (in this case, <code>myModal</code>) with an HTML element with that ID. Basically, put the <code>data-reveal-id</code> attribute on an object, and make its value the ID of your modal.

While the <code>data-reveal-id</code> is a great way to make firing a modal easy, it will often need to be fired programatically. That’s easy enough, too:

<pre><code class="language-javascript">/* Programmatic Launching Of Reveal */

&lt;script type="text/javascript"&gt;
$(document).ready(function() {
   $('#myButton').click(function(e) {
      e.preventDefault();
      $('#myModal').reveal();
   });
});
&lt;/script&gt;</code></pre>

### Options

Good plug-ins have options, and this one has just a few, but important ones:

<pre><code class="language-javascript">$('#myModal').reveal({
   animation: 'fadeAndPop',                 // fade, fadeAndPop, none
   animationspeed: 300,                     // how fast animations are
   closeonbackgroundclick: true,            // if you click background will modal close?
   dismissmodalclass: 'close-reveal-modal'  // the class of a button or element that will close an open modal
});</code></pre>

If you are wondering how to use the options when you’re using the <code>data-reveal-id</code> implementation, it’s easy: just take the option and add the <code>data-</code> before it, and pass a valid value. Here it is with the default values:

<pre><code class="language-markup tmp-xml">&lt;a href="#" data-reveal-id="myModal"
data-animation="fadeAndPop" data-animationspeed="300"
data-closeonbackgroundclick="true" data-dismissmodalclass="close-reveal-modal"
&gt;Click for a modal&lt;/a&gt;</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74eb023a-b3ea-4f5b-a5c1-e0229d0d3803/reveal-medium.jpg">Reveal: jQuery Modal Plug-In</a>

Surprise your visitors with some elegant modal windows. Download our lightweight modal plug-in and start popping up informative and varied dialogs on your pages. Check out the demo to see this plug-in in action.

<a href="https://www.zurb.com/playground/reveal-modal-plugin">Live demo</a> 

<figure><a href="https://www.zurb.com/playground/reveal-modal-plugin"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74eb023a-b3ea-4f5b-a5c1-e0229d0d3803/reveal-medium.jpg" alt="Reveal Modal Plugin" /></a><figcaption>Reveal modal plug-in.</figcaption></figure>

## Bonus: Raptorize jQuery Plug-In

We’ve all been there: sitting at your desk, coding a large website, knee-deep in <a title="Extreme Cheddar Doritos" href="https://youtube.com/watch?v=eGS1-2T-wUU">Extreme Cheddar Doritos</a>, sipping on a liter of Code Red Mountain Dew, when you realize that this page would be…

<figure><a href="https://www.zurb.com/playground/jquery-raptorize"><img loading="lazy" decoding="async" title="So much more awesome with a velociraptor" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0711994b-b9c4-407c-880b-3750ba73e07e/so-much-more.png" alt="screenshot" width="580" height="200" /></a><figcaption>Bonus: Raptorize jQuery Plug-In.</figcaption></figure>

You immediately race home to grab your Jurassic Park DVDs, so that you can screencap a velociraptor attack. Then you realize how hard it would be to make a raptor run across the website you’re coding. Plus, how will you get that distinctive velociraptor screech? We’ll let you in on a little secret…

We’ve already done it.

Raptorize was created because there was a meme going around the design community about putting velociraptors in visual designs, and we thought there was serious potential for that to live in code. We also wanted to play with some animations, HTML5 audio tags and the Konami Code!

<figure><img loading="lazy" decoding="async" title="Demo of Raptorize on a page" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28f6e4f9-1f05-4f7d-b04e-d86c3c47582e/raptorize-screen.png" alt="screenshot" width="323" height="305" />
<figcaption>Demo of Raptorize on a page.</figcaption></figure>

First things first: you need to download the Raptorize kit. It has:

- An awesome raptor graphic, courtesy of <a href="https://raptorize.com/">Raptorize</a>;
- MP3 and OGG audio files for the HTML5 audio on Webkit and Firefox;
- Our jQuery plug-in, which makes the magic happen;
- The jQuery library, to make all of the pieces work together;
- An sample HTML file that has all of the set-up pieces.

First, attach the scripts and activate the plug-in in the head of your document:

<pre><code class="language-markup tmp-xml">&lt;script src="https://ajax.googleapis.com/ajax/libs/jquery/1.4.3/jquery.min.js"&gt;&lt;/script&gt;
&lt;script&gt;!window.jQuery &amp;&amp; document.write('&lt;script src="jquery-1.4.3.min.js"&gt;&lt;/script&gt;')&lt;/script&gt;
&lt;script src="jquery.raptorize.1.0.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript"&gt;
   $(window).load(function() {
      $('.myButton').raptorize();
   });
&lt;/script&gt;</code></pre>

The only thing to know here is that you need an anchor or element with the class <code>myButton</code>.

And there you have it. You’re done!

### The Options

What’s that? You want to be able to control the entrance handler? You can! Raptorize can be activated on a click event (which is the default), on a timer that fires only after the page has loaded, or on the legendary Konami Code. Our personal favorite is the Konami Code (but it only works once per page load).

<pre><code class="language-javascript">//The options for this plug-in
&lt;script type="text/javascript"&gt;
   $(window).load(function() {
      $('.button').raptorize({
         'enterOn' : 'click', //timer, konami-code, click
         'delayTime' : 5000 //time before raptor attacks on timer mode
   });
});
&lt;/script&gt;</code></pre>

Go ahead, try the **Konami Code: ↑ ↑ ↓ ↓ ← → ← → B A**.

If you don’t want to store the Raptor image and sound files in the same directory as your JavaScript, just open the plug-in and edit the location of the assets in the first two variables of the code (<code>raptorImageMarkup</code> and <code>raptorAudioMarkup</code>).

While the awesomeness that is the Raptorize plug-in is 100% original code, the idea of including a glorious raptor in a design is not. We owe credit to **Phil Coffman and Noah Stokes** for the raptor assets and the brilliance of adding a raptor to a design.

<a href="https://www.zurb.com/playground/jquery-raptorize">Raptorize: jQuery Plug-In</a>

Want to relive the glorious ’90s cinematic action-adventure dinosaur flicks on the pages of your website? We have the solution for you.

<a href="https://www.zurb.com/playground/jquery-raptorize">Live demo &raquo;</a> 

<figure><a href="https://www.zurb.com/playground/jquery-raptorize"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c28610f4-018f-4d0e-b6ef-bfac2bf859c9/raptorize-thumb.jpg" alt="Orbit Image Slider Left Arrow Button" /><figcaption>Raptorize: jQuery Plug-In.</figcaption></figure>

Hopefully these tasty new treats will liven up your pages and make for a more enjoyable experience for you and your visitors.

{{% ad-panel-leaderboard %}}

### Further Reading

- [Freebie: Responsive jQuery Slider Plugin Flexslider](https://www.smashingmagazine.com/2011/08/freebie-responsive-jquery-slider-plugin-flexslider/)
- [How To Migrate From jQuery To Next.js](https://www.smashingmagazine.com/2021/07/migrate-jquery-nextjs/)
- [JavaScript Awesomeness — Or How To Animate Without jQuery](https://www.smashingmagazine.com/2014/09/animating-without-jquery/)
- [Replacing jQuery With Vue.js: No Build Step Necessary](https://www.smashingmagazine.com/2018/02/jquery-vue-javascript/)

{{< signature "kw, mrn" >}}

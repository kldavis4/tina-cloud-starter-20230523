---
title: Pushing Your Buttons With Practical CSS3
slug: pushing-your-buttons-with-practical-css3
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1be44bb7-03d7-4c20-8142-171272161a50/buttons2.png
date: 2009-12-02T14:45:15.000Z
author: dmitry-dragilev
description: >-
  CSS3 is the partially implemented sequel to the CSS2 spec we all know and
  love. It's already popping up in new browsers such as Firefox 3.5, Safari 4
  and Chrome. In this article, the first of the articles that explore practical
  (and even far-fetched) implementation of CSS3, we start by applying CSS3 to
  something we all have to create: **buttons**.

  Calls to action are critical for any website, and a compelling,
  attention-grabbing, clickable button goes a long way toward driving that
  engagement. In the past, really awesome buttons needed extra markup, sliding
  doors or other trickery. We'll show you here how to **create nice button
  styles without any hacks or cheats**.
categories:
  - Coding
  - Buttons
  - CSS
  - Techniques
  - CSS3
---
CSS3 is the partially implemented sequel to the CSS2 spec we all know and love. It's already popping up in new browsers such as Firefox 3.5, Safari 4 and Chrome. In this article, the first of the articles that explore practical (and even far-fetched) implementation of CSS3, we start by applying CSS3 to something we all have to create: <strong>buttons</strong>.

Calls to action are critical for any website, and a compelling, attention-grabbing, clickable button goes a long way toward driving that engagement. In the past, really awesome buttons needed extra markup, sliding doors or other trickery. We'll show you here how to create nice button styles without any hacks or cheats.

*   [Designing CSS Buttons: Techniques and Resources](https://www.smashingmagazine.com/2009/11/designing-css-buttons-techniques-and-resources/)
*   [Mastering CSS, Part 1: Styling Design Elements](https://www.smashingmagazine.com/2009/08/mastering-css-styling-design-elements/)
*   [Designing “Read More” And “Continue Reading” Links](https://www.smashingmagazine.com/2009/07/designing-read-more-and-continue-reading-links/)
*   [Web Design Elements: Examples And Best Practices](https://www.smashingmagazine.com/web-design-essentials-examples-and-best-practices/)

## Step 1: The Super-Awesome Button

Some time ago we published a post titled "<a href="https://www.zurb.com/article/266/super-awesome-buttons-with-css3-and-rgba">Super Awesome Buttons with CSS3 and RGBa</a>." Those buttons will be our first step to creating buttons that really click. We will briefly review the technique and then extend it, fixing the problems that we have encountered along the way.

{{% feature-panel %}}

### Using Box-Shadow and RGBa

Our first goal when we were about to create a versatile family of buttons was to eliminate the problem that HEX-based drop-shadows have on different backgrounds. As you can see below, we can use <em>box-shadow</em> to create a drop-shadow, but the shadow color doesn't work on both dark and light backgrounds. To get around that, we used a color model that is available in new browsers: <strong>RGBa</strong>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af8c2260-503f-43a3-8de7-f1ec15c67e61/buttons-1.png" alt="Screenshot" />

RGBa works like the standard RGB model — <em>255, 255, 255</em> for white, for example — but has a fourth property that controls the alpha, or transparency, channel. In the buttons above, the gray shadow that we created for the white background is much too light against the dark background. However, using RGBa we can create a black shadow that is transparent. This allows the shadow to work against any kind of background:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9820b5b2-c78b-420f-b795-ab5f8bebea7d/buttons-2.png" alt="Screenshot" />

<pre><code class="language-css">button.awesome, .button.awesome {
	…
	-moz-box-shadow: 0 1px 3px rgba(0,0,0,0.5);
	-webkit-box-shadow: 0 1px 3px rgba(0,0,0,0.5);
	text-shadow: 0 -1px 1px rgba(0,0,0,0.25);
	…
}</code></pre>

That solves our <em>box-shadow</em> problems. All that's left is a dash of CSS properties and a simple PNG overlay to create a finished button that can be restyled with any color, on any background, and that will work just fine.</p>

### The Amazing Border-Radius

Creating objects with rounded edges has always been a mess on the Web; after all, every object on the Web is a rectangle. CSS3 makes our lives a little easier by implementing an incredibly easy way to round off objects without sliding doors or obnoxious background elements. With these buttons, we're using a standard background color and a PNG overlay to give them depth. We are <em>not</em> using a background image to round the edges.

<pre><code class="language-css">button.awesome, .button.awesome {
	…
	-moz-border-radius: 5px;
	-webkit-border-radius: 5px;
	…
}</code></pre>

Currently, Webkit (Safari, Chrome) and Firefox have slightly different implementations of <em>border-radius</em>. Webkit will round off functional elements (like images), while Firefox will not. However, both will very cleanly <strong>round off an object and mask the background image, color or both</strong> (as with our buttons).

If you get in close, you can see that the borders behave a little strangely at the pixel level, but for the most part <em>border-radius</em> is a great way to bring rounded edges into your design without the mess. Here's the complete CSS for these buttons:

<pre><code class="language-css">button.awesome, .button.awesome {
	…
	background: #222 url(/images/alert-overlay.png) repeat-x;
	display: inline-block;
	padding: 5px 10px 6px;
	color: #fff;
	text-decoration: none;
	font-weight: bold;
	line-height: 1;
	-moz-border-radius: 5px;
	-webkit-border-radius: 5px;
	-moz-box-shadow: 0 1px 3px rgba(0,0,0,0.5);
	-webkit-box-shadow: 0 1px 3px rgba(0,0,0,0.5);
	text-shadow: 0 -1px 1px rgba(0,0,0,0.25);
	border-bottom: 1px solid rgba(0,0,0,0.25);
	position: relative;
	cursor: pointer;
	…
}</code></pre>

### Final Touches

We've created the standard buttons you can see above, but another great thing about buttons that don't use images is that we can create any color we want and with some simple class names generate an entire repertoire of buttons that we can call on any time. This is great for creating a reusable set of buttons that can be adapted to your or your clients' style guide. Check out the color codes that we are using:

<pre><code class="language-css">.blue.awesome {
	background-color: #2daebf;
}

.red.awesome {
	background-color: #e33100;
}

.magenta.awesome {
	background-color: #a9014b;
}

.orange.awesome {
	background-color: #ff5c00;
}

.yellow.awesome {
	background-color: #ffb515;
}</code></pre>

These simple classes allow us to quickly call on the button we want to get the action we need users to take. We've used similar methods in the buttons we'll walk through in the next few sections.

Our last step is sizing. Without a sliding-doors situation our button size is only limited by the size of our overlay image (and in future buttons, not even by that). We'll use a few classes (<code>small</code>, <code>medium</code> and <code>large</code>) to create sizes that we can call in different situations.

<a href="https://www.zurb.com/playground/super-awesome-buttons"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce0eb41b-1808-49fe-ac26-51d85187f78e/various-buttons.png" alt="Screenshot" width="498" height="411" /></a><br>
<em>The buttons in various sizes: an overview.</em>

And that's it! A scalable, easily configured set of buttons that works in all browsers (through graceful degradation) and will get you the impact you want. In the next few sections we'll build on these buttons to show you how CSS3 can push these even further in some interesting directions.
<div style="padding: 25px 15px;background: #fafafafa none repeat scroll 0% 0%">

<a href="https://www.zurb.com/playground/super-awesome-buttons"><img loading="lazy" decoding="async" style="float: left;margin-right: 15px" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/622aee30-3af4-4d14-a066-d3c29429fb6c/super-awesome-buttons.jpg" alt="Screenshot" /></a><br>
#### <a href="https://www.zurb.com/playground/super-awesome-buttons">See the live demo »</a>
We've created a live demo page for these buttons; it's in a playground, where we create small side projects and cool toys. We'll be linking to the playground examples throughout this post and the rest of our series.

</div><br>
<em><strong>A note about compatibility:</strong> true to form, IE8 does not support <em>border-radius</em>. At ZURB, we've adopted a "graceful degradation" paradigm, so these corners will be square in IE. In our experience, the additional development cost for elements like this is not worth it, and we rely on these properties to cleanly degrade and not damage the layout or readability. These buttons are no exception: they are still as clickable in IE as anywhere else, just not quite as pretty.</em>

## Step 2: Radioactive Buttons

Now that we've gotten our feet wet with CSS3, let's go in a different direction. For a recent client project, we wanted to create a stylized, attractive and eye-catching call to action for the home page. <strong>We came up with the idea of a radioactive button</strong>, a button that actually pulses on the page for more attention.

<a href="https://www.zurb.com/playground/radioactive-buttons"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cabfe709-97f1-4743-8f1d-20ba4e0ced8c/radioactive-buttons.png" alt="Screenshot" /></a>

Kitschy? Maybe a little. But despite its impracticality, for some websites and clients, the "Wow" factor—that feeling the user gets when they arrive at a website and say, "Oooh, ahhh!"—can't be ignored. Where we only used to have , thanks to some tricks we've already covered (and one we haven't), we can move beyond that terrifically obnoxious <em>blink</em> tag and explore a whole new range of opportunities to animate using pure CSS.</p>

### Animation: No JavaScript Required

The secret to the radioactive button is in a new CSS3 property called <em>animation</em> (or, as it currently exists, <em>-webkit-animation</em> and <em>-moz-animation</em>). Our radioactive buttons are structurally and stylistically identical to the buttons in step 1, but with one important change. In lieu of a static drop-shadow, we've used the <em>box-shadow</em> property to create a glow around the button. With "glowing shadow" added, the next step is to use CSS3 animation to dim and brighten it.</p>

### Creating the Animation

The first step in our radioactive awesomeness is to create a timed event that modifies existing CSS properties. Check out this odd-looking property:

<pre><code class="language-css">@-webkit-keyframes greenPulse
{
	from {
		background-color: #749a02;
		-webkit-box-shadow: 0 0 9px #333;
	}
	50% {
		background-color: #91bd09;
		-webkit-box-shadow: 0 0 18px #91bd09;
	}
	to {
		background-color: #749a02;
		-webkit-box-shadow: 0 0 9px #333;
	}
}</code></pre>

Here's how the code works:

*   _@-webkit-keyframes_ tells the browser that we're defining an animation based on keyframes, or points in the animation to where properties will change. The browser then knows to smoothly transition between those frames.
*   _greenPulse_ is the name of the animation. We need this to attach to objects later on.
*   _from { ... }_ defines the starting point of the animation; in our case, a certain background color for the button and a box-shadow color (particularly, one that disappears into the background).
*   _50% { ... }_ means that one change happens halfway through the animation.
*   _to { ... }_ defines the last frame of the animation. Note that animations always return to their _from_ state—they don't stop on the last frame. This means that a smooth animation needs to begin and end with the same properties and values.

All right, we've created the animation. It takes an object and over a set time changes the box-shadow color to green and then back to gray. Now, we just have to make it active by applying the animation to our buttons.

<pre><code class="language-css">.green.button {
	…
	-webkit-animation-name: greenPulse
	-webkit-animation-duration: 2s;
	-webkit-animation-iteration-count: infinite;
	…
}</code></pre>

Pretty cool, isn't it? <em>-webkit-animation</em> has many potential uses and, when combined with some very simple JavaScript (like <em>onclick</em>), you can create very rich effects and interaction without resorting to a JavaScript effects library.
<div style="padding: 15px;background: #fafafa none repeat scroll 0% 0%">

<a href="https://www.zurb.com/playground/radioactive-buttons"><img loading="lazy" decoding="async" style="float: left;margin-right: 15px" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5106d899-65b6-4f46-87e5-26852a448270/inline-labels.png" alt="Screenshot" /></a><br>
#### <a href="https://www.zurb.com/playground/radioactive-buttons">See the live demo »</a>
Check out the live demo of radioactive buttons in our playground. For maximum awesomeness, check it out in Safari 4; radioactive buttons use some Webkit-specific properties that aren't implemented well in Chrome quite yet.

</div>

## Nice, Simple, User-Friendly Buttons, Google-Style

Our last example was inspired by some recent changes made to one of the most trafficked pages on the Web: the Google search page. In addition to enlarging the search field and text size, Google also rolled out some new buttons for Webkit-based browsers (notably its own, Chrome).

These buttons incorporate everything that makes our buttons in this article great, with one cool trick: <strong>no images at all.</strong> Google has used a new property called <em>-webkit-gradient</em> to generate a gradient using only CSS.

<a href="https://www.zurb.com/playground/google-buttons"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e04d17e2-a802-4fa2-b0c7-9d45579cd0af/google-buttons.png" alt="Screenshot" /></a>

### Using CSS Gradients

Gradients in CSS are cool because they are a CSS function, much like <em>url()</em>, which means that we can use gradients anywhere images go, including in the background or in borders (don't worry, we'll get to <em>border-image</em> in a later post). <strong>Here's how gradients work:</strong>

<pre><code class="language-css">.g-button {
	…
	background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(rgb(255, 255, 255)), to(rgb(98,202,227)));
	…
}</code></pre>

Let's break this down:

*   _linear_ means this is a linear gradient, as opposed to radial. This changes the color across a single axis, rather than in concentric circles.
*   _0% 0%, 0% 100%_ are coordinates. We're saying that the gradient begins at 0% X, 0% Y and ends at 0% X, 100% Y: top-left corner to bottom-left corner. We could use _top-left, bottom-left_ just as well.
*   _from(rgb(255, 255, 255))_ is the starting color for the gradient. If the syntax looks familiar, it should be: it's very similar to the syntax for _@-webkit-keyframes_.
*   _to(rgb(221, 221, 221))_ is the ending color. While we have only used RGB here, you can see how gradients could get really interesting if we use RGBa and are able to control the opacity of points on the gradient.

The rest of the button is ordinary: padding, <em>border-radius</em> and all the fun things we've gone over so far. Gradients is the star here, though, and it has thousands of potential uses. Here, we've created (albeit in Google's footsteps) rich, engaging buttons that are 100% CSS, no images required.
<div style="padding: 15px;background: #fafafa none repeat scroll 0% 0%">

<a href="https://www.zurb.com/playground/google-buttons"><img loading="lazy" decoding="async" style="float: left;margin-right: 15px" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/217cbf37-9a77-4396-80ed-eeebfc9a5f46/google-buttons.jpg" alt="Screenshot" /></a><br>
#### <a href="https://www.zurb.com/playground/google-buttons">See the live demo »</a>
You can see a live demo of these buttons in the playground, or simply visit the Google search home page in a Webkit browser.

</div>

## Coming Up: Better, Stronger, Faster Design

This is the first of the articles that take advantages of the powerful new features coming in CSS 3. In the following posts, we'll show you how CSS3 not only can make implementation faster and easier, but can help you really fly off the rails and push CSS to its breaking point while creating impressive visual effects.

<a href="https://answers.polldaddy.com/poll/2330515/">Would you like to see more similar posts on Smashing Magazine in the future?</a><span style="font-size: 9px">(<a href="https://answers.polldaddy.com">opinion</a>)</span>

### References and Resources

*   [RGBa Browser Support at CSS-Tricks](https://css-tricks.com/rgba-browser-support/)
*   [Introduction to CSS Animation at Surfin' Safari](https://webkit.org/blog/138/css-animation/)
*   [CSS3 Animation Tutorial at ZURB](https://www.zurb.com/article/221/css3-animation-will-rock-your-world)
*   [Introduction to CSS Transitions at CSS3.info](https://www.css3.info/webkit-introduce-more-new-features/)
*   [Safari Visual Effects Documentation](https://developer.apple.com/safari/library/documentation/InternetWeb/Conceptual/SafariVisualEffectsProgGuide/Introduction/Introduction.html)
*   [Using border-radius at The Art of Web](https://www.the-art-of-web.com/css/border-radius/)

{{< signature "al" >}}


---
title: Designing For Emotion With Hover Effects
slug: designing-emotion-hover-effects
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a0063ae-8cca-4284-b48c-8abafb51f4a1/illu-hovereffects.jpg
date: 2013-09-02T13:22:37.000Z
author: dudley-storey
description: >-
  Of the many factors that must be considered in Web design, emotional
  interaction is an important, but frequently neglected, component. In the real
  world, we experience the sensual interaction of design all the time.
categories:
  - Coding
  - CSS
  - JavaScript
  - jQuery
  - Emotional Design
  - HTML
---
Of the many factors that must be considered in Web design, emotional interaction is an important, but frequently neglected, component. In the real world, <strong>we experience the sensual interaction of design all the time</strong>. Reflect for a moment on the emotional engagement of slipping behind the wheel of a powerful luxury car: the welcoming embrace of the driving seat, the tactile experience of running your hands over the leather on the steering wheel, the subtle gleam reflected in the controls.

There is no technical requirement for any of these finely crafted details: The vehicle would perform equally well without them. Yet this singular focus on sensual and emotional engagement is what separates luxury goods from all others and what inspires deep loyalty from customers.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Definitive Guide To Styling Web Links](https://www.smashingmagazine.com/2010/02/the-definitive-guide-to-styling-web-links/)
*   [Not Just Pretty: Building Emotion Into Your Websites](https://www.smashingmagazine.com/2012/04/building-emotion-into-your-websites/)
*   [An Ultimate Guide To CSS Pseudo-Classes And Pseudo-Elements](https://www.smashingmagazine.com/2016/05/an-ultimate-guide-to-css-pseudo-classes-and-pseudo-elements/)
*   [Give Your Website Soul With Emotionally Intelligent Interactions](https://www.smashingmagazine.com/2012/03/give-your-website-soul-with-emotionally-intelligent-interactions/)

This <strong>drive for emotional design can be discovered in the most surprising places</strong>. Take the power light on the next to last-generation Apple MacBook. The company deserves credit for helping thousands of users avoid entanglements with power cords though the MagSafe connector, but the deeper emotional intimacy is held in the tiniest of details: the power status light on the front of the laptop. When in sleep mode, the light pulses, and not randomly: It does so 10 times a minute, the breathing rate of a resting human being.

{{% feature-panel %}}

<a href="https://www.flickr.com/photos/mjs/3046240921"><img loading="lazy" decoding="async" class="128666" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3401cf19-be07-45f2-b841-72d85ead38d1/macbook-sleep-light-mini.jpg" alt="macbook sleep light_mini" width="500" height="333" /></a><br>
<em>The blink rate of Apple's MacBook in sleep mode falls within the average breathing rate of a resting adult. (Image source: <a href="https://www.flickr.com/photos/mjs/3046240921">Michael Stillwell</a>)</em>

To take another example: The front of a car is not two headlights and a grill. It is a face, one with its own character and communication. Look at cars and vans marketed to suburban mothers, on which lines tend to be round, curved, welcoming and friendly.

The front of the vehicle often demonstrates the neotenic effect: We regard “eyes” (headlights) that are larger than the body as being cute, safe, loveable. Compare this to the visual communication of vehicles marketed to men, particularly sports cars: Those lines are angular and aggressive, right down to the slitted eyes.

<a href="https://www.flickr.com/photos/tonyshek/8454936722"><img loading="lazy" decoding="async" class="128676" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/877079b4-a842-4a4d-8a39-ca077768c48d/sport-car-front-mini.jpg" alt="sport car front_mini" width="500" height="359" /></a><br>
<em>Note how a sports car's front interacts with you on an emotional level. (Image source: <a href="https://www.flickr.com/photos/tonyshek/8454936722">GabboT</a>)</em>

## Designing For Emotion

We can strive to achieve the same emotional engagement on websites — a promise to delight, surprise and affect users without resorting to manipulation or being too saccharine. While the digital realm lacks many sensual cues, it is possible to impart an emotional experience through a careful selection of color, stroke and typography.

<strong>CSS transitions help us to make interactions more human</strong>: Rather than flicking from one state to another, we can ease the motion of an element over a few hundred milliseconds to make a website feel more inviting. Paradoxically, the same techniques can also make a website feel faster, especially if we use the opportunity to preload content.

In creating such experiences, we must avoid the mistakes of the past: The engagement should encourage the visitor to explore the website, but should never hide important components such as navigation. Rewards for exploration should be a treated as a bonus, rather than a required interaction. Any information shared should also be accessible to those who don’t have the time or ability to use the interface.</p>

## Surprise In Boxes

(Please <a href="https://codepen.io/dudleystorey/pen/bkKDp">see the demo at “Hover Effect on Images From Different Directions Using Pure CSS,”</a> on CodePen.)

One way to design for emotional surprise and stimulation might be to present different panes of information according to the way the user hovers over a responsive image. For this example, I’ll use a photo of the spiral galaxy NGC 1309, added to an HTML5 page:

<pre><code class="language-markup">
&lt;img src="ngc-1309.jpg" alt=""&gt;
</code></pre>

(Note that I’ve intentionally left the <code>alt</code> value of the image blank. We’ll return to that attribute shortly.)

The information panels are created from four <code>span</code> elements, with the entire group wrapped in a <code>div</code> tag that includes a <code>class</code>:

<pre><code class="language-markup">
&lt;div class="multi-hover"&gt;
    &lt;span&gt;Spiral Galaxy NGC 1309&lt;/span&gt;
    &lt;span&gt;Approximately 120 million light years from Earth&lt;/span&gt;
    &lt;span&gt;Home to several Cephid variable stars&lt;/span&gt;
    &lt;span&gt;Member of the Eridanus galactic cloud&lt;/span&gt;
    &lt;img src="ngc-1309.jpg" alt=""&gt;
&lt;/div&gt;
</code></pre>

We’ll write the CSS transition code sans vendor prefixes: Internet Explorer 10 does not use prefixes for animation, Firefox no longer requires them, Chrome is not far behind, and a piece of JavaScript magic such as Lea Verou’s <a href="https://leaverou.github.com/prefixfree/">-prefix-free</a> will take care of those browsers that still do.

<pre><code class="language-css">
.multi-hover {
	position: relative;
	font-family: Orbitron, sans-serif;
	max-width: 500px;
	line-height: 0;
}

.multi-hover img {
	max-width: 100%;
}

.multi-hover span {
	position: absolute;
	width: 100%;
	height: 100%;
	line-height: 1.5;
	font-weight: 100;
	text-align: center;
	box-sizing: border-box;
	font-size: 3em;
	transition: .3s linear;
	color: white;
	padding: 15%;
	opacity: 0;
}
</code></pre>

The CSS takes advantage of the rule that <strong>absolutely positioned elements inside relative containers will be transformed relative to their parent</strong>. Because the image determines the height and width of the <code>div</code>, the <code>span</code> elements will always be exactly the same size, protected from growing further by the use of <code>box-sizing</code>, <code>max-width</code> and <code>line-height: 0</code>. In this example, I’m using <a href="https://www.theleagueofmoveabletype.com/orbitron">Orbitron</a> by <a href="https://www.theleagueofmoveabletype.com/">The League of Moveable Type</a> as an appropriate typeface.

Next, locate the <code>span</code> elements, so that each lies just over the inner edge of the image. We’ll do so by writing offsets from the containing <code>div</code> in percentages, to keep everything responsive:

<pre><code class="language-css">
.multi-hover span:nth-child(1) {
	top: 0;
	left: 90%;
	background: hsla(0,70%,50%,0.6);  } /* right panel */

.multi-hover span:nth-child(2) {
	top: -90%;
	left: 0;
	background: hsla(90,70%,50%,0.6); } /* top panel */

.multi-hover span:nth-child(3) {
	top: 0;
	left: -90%;
	background: hsla(180,70%,50%,0.6); } /* left panel */

.multi-hover span:nth-child(4) {
	top: 90%;
	left: 0;
	background: hsla(270,70%,50%,0.6); } /* bottom panel */
</code></pre>

As you’ll see in a moment, the order of the panel declarations matters. The result looks something like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17365cef-a35b-4281-b61e-31663ccb0176/span-array-full-large-mini.jpg"><img loading="lazy" decoding="async" class="128656" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2987e177-634c-442b-9b14-7e1a460b1b47/span-array-full-500-mini.jpg" alt="Positioned span elements with text." width="500" height="501" /></a><br>
<em>Positioned span elements with text. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17365cef-a35b-4281-b61e-31663ccb0176/span-array-full-large-mini.jpg">Large view</a>)</em>

To clip the outside edges of the panels, use <code>overflow: hidden</code> on the containing <code>div</code>:

<pre><code class="language-css">
.multi-hover {
	position: relative;
        overflow: hidden;
	font-family: Orbitron, sans-serif;
</code></pre>

Now, the result appears like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fe915d1-8234-465f-96fe-8b3988206c1b/span-array-hit-areas-mini.jpg"><img loading="lazy" decoding="async" class="128660" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fe915d1-8234-465f-96fe-8b3988206c1b/span-array-hit-areas-mini.jpg" alt="Span elements clipped to image." width="500" height="497" /></a>

The colored sections we can see for now will function as the “hit areas” of our panels. Increasing the size of these areas will increase the panel’s ability to respond to quicker and broader mouse movements, but will also increase the overlap between them, making it more likely that a different panel will be activated than the one expected.

Finally, we’ll hide the panels entirely by setting their <code>opacity</code> to <code>0</code> and moving them on <code>hover</code>, taking advantage of the fact that transparent elements still respond to mouse events.

<pre><code class="language-css">
.multi-hover span {
	position: absolute;
	width: 100%;
	height: 100%;
	line-height: 1.5;
	font-weight: 100;
        z-index: 2;
	text-align: center;
	box-sizing: border-box;
	font-size: 3em;
	transition: .3s linear;
	color: white;
	padding: 15%;
	opacity: 0;
}

.multi-hover span:hover {
	opacity: 1;
}

.multi-hover span:nth-child(odd):hover {
	left: 0;
        z-index: 3;
}

.multi-hover span:nth-child(even):hover {
	top: 0;
        z-index: 3;
}
</code></pre>

The <code>odd</code> and <code>even</code> declarations set each panel to the opposite side of the box, positioning them entirely over the image and completing the design. Note that this interface pattern requires exploratory mouse movement from the outside of the box inwards to activate each panel; alternately, a completely “in box” exploration model could be created by lowering the <code>z-index</code> of the <code>:hover</code> states to 1.

## Accessibility Testing

Making the panels invisible brings up the issue of accessibility. Partially sighted users <em>might</em> be able to see and interact with the panels, but blind users obviously will not.

Screen readers treat such content as being truly “invisible” (leaving them, therefore, unread), depending on the context; content that is set to <code>display: none</code> is usually left unread, for example. However, opacity does <em>not</em> trigger this behavior. On a Mac, you can easily test this by activating VoiceOver and having it read the page we’ve created in the browser:

*   `Command + F5` to start VoiceOver,
*   `Control + Option + A` to read Web page content,
*   `Command + F5` to stop VoiceOver.

You’ll hear the <code>span</code> content being read in the order that it appears on the page; all that’s missing is a description of the image at the end:

<pre><code class="language-markup">
&lt;div class="multi-hover"&gt;
&lt;span&gt;Spiral Galaxy NGC 1309&lt;/span&gt;
&lt;span&gt;Approximately 120 million light years from Earth&lt;/span&gt;
&lt;span&gt;Home to several Cephid variable stars&lt;/span&gt;
&lt;span&gt;Member of the Eridanus galactic cloud&lt;/span&gt;
&lt;img src="ngc-1309.jpg" alt="Photograph of NGC 1309"&gt;
&lt;/div&gt;
</code></pre>

Note that this only treats the visual aspects of accessibility. There are other important areas (cognitive, motor and language) that I will leave unaddressed in this example for the sake of space but that have been <a href="https://www.smashingmagazine.com/search-results/?q=accessibility&amp;cx=partner-pub-6779860845561969%3A5884617103&amp;cof=FORID%3A10&amp;ie=UTF-8">detailed by other Smashing Magazine authors</a>.</p>

## Adding Touch Support

The majority of mobile devices that depend on touch interfaces do not support a pure “hover” state: <strong>An element is either “in touch” or not.</strong> With rare exceptions, there is no registration of a fingertip being just above the screen of a mobile device. A brief touch <em>might</em> be interpreted as a hover event by mobile browsers, but this behavior is not perfectly predictable. As such, our interface will not work on most tablets or phones, at least as it currently exists.

To solve this issue, <strong>we’ll add a little JavaScript</strong> (by way of jQuery) to the page:

<pre><code class="language-markup">
&lt;script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"&gt;
&lt;/script&gt;
&lt;script&gt;
function is_touch_device() {
  return !!('ontouchstart' in window)
      || !!('onmsgesturechange' in window);
};

$(document).ready(function() {
  if (is_touch_device()) {
    $('span').unbind('mousenter mouseleave touchend touchstart');
    $('span').bind('touchstart', function() {
      $('span').removeClass('hover');
      $(this).addClass('hover');
    });
  }
});
&lt;/script&gt;
</code></pre>

The JavaScript applies a class of <code>hover</code> to any <code>span</code> element that is touched. So, we just need to alter our CSS declarations to make this <code>class</code> equivalent to the <code>:hover</code> event:

<pre><code class="language-css">
.multi-hover span:hover { opacity: 1; }
.multi-hover span:nth-child(odd):hover { left: 0; z-index: 3; }
.multi-hover span:nth-child(odd).hover { left: 0; z-index: 1; }
.multi-hover span:nth-child(even):hover { top: 0; z-index: 3; }
.multi-hover span:nth-child(even).hover { top: 0; z-index: 1; }
}
</code></pre>

Note that in the mobile version, the extended panel goes "under" the level of those that are retracted, allowing them to be tapped.

Disengaging the copy controls on handheld devices might also be wise. This is not some futile pursuit of DRM, but a practical response to the fact that <strong>longer touch times on mobile devices can bring up copy prompts</strong> that could get in the way of the user interface:

<pre><code class="language-css">
.multi-hover span {
  -ms-touch-action: none;
  -webkit-touch-callout: none;
  -webkit-user-select: none;
}
</code></pre>

This user interface pattern of exploration on a mobile device may now be described as “tap on edge.” This could be further enhanced by increasing the overlap of the original position of the <code>span</code> elements in an <code>@media</code> query to provide larger hotspots, making the panels easier to activate, along with further improvements for smartphones. This code is not the only way to achieve this effect either: Ana Tudor has written an <a href="https://codepen.io/thebabydino/pen/mIxhv">alternative technique using CSS transforms and SASS</a>.</p>

## Conclusion

Crafting an element of surprise on Web pages can <strong>raise visitor engagement</strong> without obfuscating important content, sidelining mobile visitors or disadvantaging users who require accessibility features. Naturally, this must always be balanced with the need to guide users through the website: Visitors will only be surprised by the effects described here if they explore the page for themselves, or are led to it. How much users should be led and how much opportunity they should be given to discover a delight on their own initiative is a central question of user experience design.

<em>(al) (ea)</em>


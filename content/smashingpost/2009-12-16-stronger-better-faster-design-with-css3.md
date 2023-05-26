---
title: 'Stronger, Better, Faster Design with CSS3'
slug: stronger-better-faster-design-with-css3
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f513816f-1e6b-41a8-b052-a1e28ab09084/css3-2.jpg
date: 2009-12-16T13:44:52.000Z
author: dmitry-dragilev
description: >-
  In our last article about CSS3, ["Pushing Your Buttons With Practical CSS3](https://www.smashingmagazine.com/2009/12/02/pushing-your-buttons-with-practical-css3/), we talked about using new CSS3 techniques like gradients, border-radius and drop-shadows to create compelling, flexible and (in some cases) hilarious buttons. 
categories:
  - Coding
  - CSS
  - CSS3
---
In this second article we're going to focus on using those CSS techniques (and a little JavaScript) to <strong>create some practical elements and layouts</strong>. As before, <em>caveat coder</em> — a lot of the CSS properties we're going to use have limited support, if any, in IE6/7 and probably 8. Firefox 3.5+ and Safari 4 are your best bet right now to see all the cool stuff going on in CSS right now (Chrome does a pretty good job, too).

Be sure to check out the following articles:

*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/take-your-design-to-the-next-level-with-css3/)
*   [Push Your Web Design Into The Future With CSS3](https://www.smashingmagazine.com/2009/01/push-your-web-design-into-the-future-with-css3/)
*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)

Why bother with CSS that has such limited support? It won't always have limited support, and these articles are all about preparing for the future of web design (and just doing some really cool stuff). Apparently, if you are one of those people who is waiting until using progressive CSS is safe because all major browsers support the same CSS at the same time, <a href="https://www.stuffandnonsense.co.uk/blog/about/you8217re_living_in_a_fantasy_world/">you are living in a fantasy world</a>, so it's just the right time to get things rolling with CSS3.

{{% feature-panel %}}

Ready? Let's roll.</p>

## Inline Form Labels

Everyone's familiar with inline form labels — storing the label of the field in the <code>value</code> attribute and using some minor JavaScript to erase the text when the field gains focus. This works...okay, but the major problem is that as soon as the user clicks, they lose the label entirely. If they tabbed right into it they may not even have read the label, in which case they're just guessing.

The first site we saw that fixed this was <a href="https://www.me.com">MobileMe</a> from Apple, on their login screen.

<a href="https://www.me.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8707100b-cea7-4036-a7e4-3a4931473819/inline-1.jpg" width="638" height="214" /></a>

What happens with Apple is that clicking into the field fades the label back, but doesn't erase it. Cooler still is that the cursor stays positioned left so you can start typing, and the JavaScript making that happen is not overly complex — it's just layout tricks. They position a label behind the input containing the name of the field.<a href="https://www.zurb.com/article/271/making-forms-convert-through-awesome-inli"><img style="float: right;margin: 20px 0px 20px 20px" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a914f51-950a-4e99-8ae4-026108eb0b99/inline-2.jpg" width="200" height="176" /></a> When you click into the field they use JavaScript to apply a class to the label that knocks it back, and another class as you start typing to make the label vanish.

We wrote a <a href="https://www.zurb.com/article/271/making-forms-convert-through-awesome-inli">blog post</a> about this effect some time ago, describing how you could replicate it yourself. The problem is that over time setting up the page to support this isn't as turnkey as we'd like, so we've revised and rebuilt it just for you (and, of course, for us).</p>

### The New Inline Label

Our new approach is considerably easier — to use it in our own products (like <a href="https://www.notableapp.com">Notable</a> and Scrumptious) we simply add <code>class="inlined"</code> to the label and voila! Here's how we do it.

Start with a regular label and input:

<pre><code class="language-css">&lt;label for="demoForm1"&gt;Email Address&lt;/label&gt;
	&lt;input class="input-text" id="demoForm1" /&gt;</code></pre>

In previous iterations of this technique we went to the trouble of wrapping the label and input in a block-level element and used absolute positioning to put the label behind the input. Not anymore. First, we'll add the "inlined" class to <em>only</em> the label:

<pre><code class="language-css">&lt;label for="demoForm1" class="inlined"&gt;Email Address&lt;/label&gt;
	&lt;input class="input-text" id="demoForm1" /&gt;</code></pre>

Now we need to do a couple of things to get our labels to display correctly. First, we use negative margins to pull the input up and over the label. We'll do this by using the CSS <strong>adjacent</strong> selector, which looks like this:

<pre><code class="language-css">label.inlined + input.input-text {
		margin-top: -22px;
		background-color: transparent;
		position: relative; z-index: 2;
	}</code></pre>

That code tells the browser to apply the style to any <code>input.input-text</code> which immediately follows a <code>label.inlined</code> — this way we can use the negative margin to pull the input up and over the label itself. We also set the background color to <code>transparent</code> and give the input a relative position and a <code>z-index</code> value.

Next we need to style the label itself. You'll need to adapt the styling here to mirror your input text style — the goal is for the text inside the label to appear as though it is actually part of the input. Here are the critical pieces:

<pre><code class="language-css">label.inlined {
		padding-left: 6px;
		font: normal 12px/18px "Helvetica Neue";
		position: relative; z-index: 1;
		opacity: 0.75;
		-webkit-transition: opacity 0.15s linear;
	}</code></pre>

Let's break that down. Padding and font are simply to mirror the input style. The positioning and z-index make sure the label stays behind the input — otherwise the input can't be selected. Now the fun parts: <code>opacity</code> and <code>-webkit-transition</code>.

Our form labels work by fading back the label at different points. We start with the label faded back a little, hence the <code>opacity: 0.75</code>. You could also use <code>color</code> to drop the label back, but opacity works regardless of the font color. We add in the <code>-webkit-transition</code> so that whenever the opacity changes, the browser (Safari or Chrome, in this case) will change the opacity smoothly over about 1/8th of a second. So when does the opacity change?

Two times — when the user focuses on the field, and when they start typing. Let's create two CSS classes we can apply for those states: <code>focus</code> and <code>has-text</code>.

<pre><code class="language-css">label.focus {
		opacity: 0.35;
	}

	label.has-text {
		opacity: 0.0;
		-webkit-transition-duration: 0s;
	}</code></pre>

As you can see, we reduce the opacity of the label when the user clicks in, then make it invisible when they start to type. We change the duration of our transition so that as a user starts to type, the label disappears immediately, rather than fading back as they type. Now that we have our fields structurally set up and styled the way we want, the last step is a little bit of JavaScript.</p>

### Adding the JavaScript

Even though CSS3 has added new tricks like animations and transitions, JavaScript is still king when it comes to interaction. To get our labels to behave, we need to use a few simple JavaScript functions. In these examples we'll be writing for <a href="https://www.jquery.com">jQuery</a>, but they're easy to adapt to Prototype or straight JavaScript.

The JavaScript needs to do three things:

1.  Add the `focus` class to the label when the user clicks into a field
2.  Add the `has-text` class as soon as they start typing
3.  Bring the label back if they leave the field empty and switch to another field.

<pre><code class="language-css">$(document).ready(function(){
	$("label.inlined + input.input-text").each(function (type) {

		$(this).focus(function () {
			$(this).prev("label.inlined").addClass("focus");
		});

		$(this).keypress(function () {
			$(this).prev("label.inlined").addClass("has-text").removeClass("focus");
		});

		$(this).blur(function () {
			if($(this).val() == "") {
				$(this).prev("label.inlined").removeClass("has-text").removeClass("focus");
			}
		});
	});
});
</code></pre>

We won't pore over the JavaScript much — it's pretty self-explanatory. jQuery let's us quickly target the inputs we want by recognizing the same selector we're using in CSS, but otherwise it's all cut and dried. And there it is: inline labels that appear as refined versions of standard inline labels, but have much smoother interaction. Going forward now we can make any label inline by adding <code>class="inlined"</code> to the label — CSS and JavaScript will take care of the rest.
<div style="padding: 25px 15px;background: #fafafafa none repeat scroll 0% 0%"><a href="https://www.zurb.com/playground/inline-form-labels"><img style="float: left;margin-right: 15px" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71784016-7ce8-4002-b89f-b8c219c88382/inline-form-labels.jpg" width="210" height="162" /></a><br>
#### <a href="https://www.zurb.com/playground/inline-form-labels">See the Live Demo »</a>
We've created a live demo page for these forms in our Playground, a place for us to create small side projects and examples of cool toys. We'll be linking to the Playground examples throughout this post and the rest of the series.

</div>

## Fast, Easy Drop-in Modals

Next we'll show you how to create easy modals that you can control with just one line of JavaScript. We use modals to great effect in our feedback tool, <a href="https://www.notableapp.com">Notable</a>, and while in Notable we use Ajax to load modals on the fly, this example will show you how easy it is to create an on-page modal.

The basic structure of our modals is a <code>div.modal</code> containing whatever we want. It could be an alert triggered by your page, a sign-in or sign-up form, or other information or actions that we don't want to trigger a full page load. We'll use some of our new CSS3 styles to make the modals look awesome and feel...well, modal, then turn them on with a single line of JavaScript.</p>

### The Simple Modal

Our first modal example is a simpler style, with a simpler animation. We'll style the <code>div</code> to resemble a padded, floating box with a standard drop shadow so it appears to hover over the page. To make it appear, we'll fade it up from an opacity of 0, and to close it, we'll dismiss it immediately.

<a href="https://www.zurb.com/playground/drop-in-modals"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f275dcc-d032-4103-87c1-d3aa08e687dd/modal-1.jpg" width="639" height="181" /></a>

The modal style here uses a couple new CSS3 elements: <code>-webkit-box-shadow</code> to create the drop shadow and <code>-webkit-transition</code> (which you'll recognize from the inline labels above) to fade it in without using JavaScript animation. Below are the styles for the modal; we'll go over the new pieces in a second.

<pre><code class="language-css">div#simpleModal {
		width: 560px;
		position: absolute; top: 40px; left: 170px;
		padding: 20px;
		border: solid 1px #bbb;
		background: #fff;
		-webkit-box-shadow: 0px 3px 6px rgba(0,0,0,0.25);
		-webkit-transition: -opacity 0.0s ease-out;
	}

	div#simpleModal.shown {
		opacity: 1.0;
		z-index: 100;
		-webkit-transition-duration: 0.25s;
	}</code></pre>

Most of the styling here is pretty standard — size and position as well as decent padding and a light grey border. The new pieces here are <code>-webkit-box-shadow</code> and <code>-webkit-transition</code>. We covered both of those new attributes in <a href="https://www.smashingmagazine.com/2009/12/02/pushing-your-buttons-with-practical-css3/">our article on CSS3 buttons</a> so we'll go over them quickly.

<code>-webkit-box-shadow</code> (or <code>box-shadow</code> as it will be called when the CSS3 spec is finalized and implemented) takes a few arguments. The first two properties are the offset, X and Y. In this case no X offset, 3px of Y offset. This puts the shadow just below the object. The next argument, 6px, sets the spread size: 6 pixels out from the box shape.

Finally we set a box-shadow color using RGBa, which lets us set an RGB color (black, in this case) and then set an opacity, or alpha channel. By using black with 25% opacity we can be sure it will darken whatever color it overlays; if we used something like <code>#333</code> it would actually appear to glow on a black background, rather than look like a shadow.</p>

### The Fancy Modal

That modal is okay — it gets the job done and once you know it, the pieces can be put together in less than 5 minutes. We wanted to do a little more for Notable, so we cooked up a fancier style using a few other CSS tricks like <code>-webkit-gradient</code> and <code>-webkit-transform</code>.

<a href="https://www.zurb.com/playground/drop-in-modals"><img style="border-top: solid 1px #bbb" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68d84312-005a-4f1c-898f-038328da879f/modal-2.jpg" width="639" height="172" /></a>

This modal is a little flashier and more akin to a desktop app in terms of interaction: it slides down from the top and gets a little more chroming than the simple modal. We accomplish this through a couple of cool tricks.

<pre><code class="language-css">div#fancyModal {
		display: block; width: 560px;
		position: absolute; top: -310px; left: 170px;
		padding: 90px 20px 20px 20px;
		border: solid 1px #999;
		background: -webkit-gradient(linear, left top, left bottom, from(rgb(255,255,255)), to(rgb(230,230,230)));
		-webkit-box-shadow: 0px 3px 6px rgba(0,0,0,0.25);
		-webkit-border-bottom-left-radius: 6px;
		-webkit-border-bottom-right-radius: 6px;
		-webkit-transition: -webkit-transform 0.25s ease-out;
		-webkit-transform: translateY(-570px);
		-moz-box-shadow: 0px 3px 6px rgba(0,0,0,0.25);
		-moz-border-radius: 0 0 6px 6px;
		-moz-transform: translateY(-570px);
	}</code></pre>

First we generate a gradient for the background. Obviously we could just create a tiling background image for the gradient, but where's the fun in that? We'll have the browser create one using <code>-webkit-gradient</code>, which is a CSS function that creates a gradient you can use anywhere you would use an image. As you can see above, <code>-webkit-gradient</code> has quite a few attributes; it's not as bad as it seems. Let's break it down:

*   `linear` means that this gradient goes from one point to another, in a straight line. You can also use `radial` to create a circular gradient.
*   `left top, left bottom` are the coordinates for starting and stopping, in this case going from top to bottom with no angle. If we used `left top, right bottom` the gradient would stretch diagonally across the div.
*   `from(rgb(255,255,255))` is the starting color, in this case white.
*   `to(rgb(230,230,230))` is the ending color. We could also put `color-stop` elements in between if we wanted to vary the color as we went.

That wasn't so hard! Gradients are going to be a great way to add those flourishes to design without having to futz around with image backgrounds - these are easily created and modified in just a couple of lines. Now let's look at the fancier part of this modal: the appearance animation.

<pre><code class="language-css">div#fancyModal {
		…
		-webkit-transition: -webkit-transform 0.25s ease-out;
		-webkit-transform: translateY(-570px);
	}</code></pre>

What we're doing here is using a property called <code>-webkit-transform</code> to move the modal up and out of the viewport. Since transforms don't impact the DOM we don't get any weird effects or problems — the <code>div</code> just moves up without impacting anything else. So when the page loads, our <code>div</code> will be located above the page. When we add <code>class="shown"</code> to the <code>div</code>, it will get a new transform position, and the <code>-webkit-transition</code> will cause the transformation to be applied over a quarter of a second — this is what causes the modal to slide down from the top of the page.

As you can see, creating a fairly fancy modal style is pretty easy with these new CSS3 effects. Our last step is a simple line of JavaScript to apply a <code>shown</code> class to the modal. For our simple modal, it changes the opacity to 1; for our fancy modal, it changes the transform position to 0 (rather than -570px). Our transition then takes care of the actual animation.

&nbsp;
<div style="padding: 25px 15px;background: #fafafafa none repeat scroll 0% 0%"><a href="https://www.zurb.com/playground/drop-in-modals"><img style="float: left;margin-right: 15px" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56f40dd7-8531-4047-a259-4427c844e423/drop-in-modals.jpg" width="210" height="162" /></a><br>
#### <a href="https://www.zurb.com/playground/drop-in-modals">See the Live Demo »</a>
You can check out the live demo on the Playground. We've got the source code and clickable examples of the two modals (requires WebKit).

</div>

## Newspaper Layouts with Columns and Image Masks

Our final example in this article will demonstrate how to use a couple of new CSS attributes and functions to create a cool newspaper layout — in this case the <a href="https://www.zurb.com/playground/newspaper-layout">Super Awesome Times</a>.

The faux-newspaper look goes in and out of style online pretty frequently, but these tricks can be used for quite a few cool applications. What we'll talk about here is using <code>-webkit-mask-image</code> and <code>-webkit-column-count</code>.</p>

### Using Image Masks

Image masking is a way to affect the alpha channel of a block-level element by masking it with another image (or anything that can take the place of an image, like a gradient). For the Super Awesome Times we wanted to apply a subtle gradient to the masthead. We could simply render an image, but that's no fun. Instead we masked the text (which in this case is an image, but with <code>@font-face</code> you could use text instead) with a generated gradient. Check it out:

<pre><code class="language-css">div#masthead img {
	-webkit-mask-image:
		-webkit-gradient(
			linear, 
			left top, left bottom, 
			from(rgba(0,0,0,.75)), to(rgba(0,0,0,1)));
	}</code></pre>

The only property we need is <code>-webkit-mask-image</code> — the browser will use whatever you supply to create an alpha mask for the image or block element you've applied the mask to. In this case we use a gradient, which causes the masthead to fade from 75% opacity to 100%. Below is the masthead with the mask, and without — so you can see the difference:

<a href="https://www.zurb.com/playground/newspaper-layout"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c50018d3-ff48-4443-82d2-ef4d2e971d52/newspaper-1.jpg" width="639" height="165" /></a>

It's a subtle change, but some added depth can go a long way. There's a <a href="https://webkit.org/blog/181/css-masks/">great introduction to using masks</a> over on Surfin' Safari, the official WebKit blog. You can see how masks can be used for all sorts of interesting effects — even masking out an actual playing video.</p>

### Stunningly Easy Text Columns

Finally, we'll show you how to use a new (and very poorly supported, so far) property in CSS3: text columns. Not the floated <code>div</code> kind, but the kind where you can simply set the number of columns and the gutter and have the browser do the rest.

<a style="padding: 10px;border: solid 1px #ccc" href="https://www.zurb.com/playground/newspaper-layout"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ace4e695-c650-48ed-896e-a4dc7cd883fd/newspaper-2.jpg" width="594" height="202" /></a><br>
<em>3 columns, no fuss.</em>

In the example above you can see three columns of text, but if you click through to the live example and view the source code, you'll see that we've used just one <code>div</code> containing a number of paragraphs. Nothing tricky, no floats, no bizarre height manipulations — we're just telling the browser to put the content of that block into 3 columns with 15px of space between them. Here's how:

<pre><code class="language-css">div.three-col {
		-webkit-column-count: 3;
		-webkit-column-gap: 15px;
		-moz-column-count: 3;
		-moz-column-gap: 15px;
	}</code></pre>

That's it! Simple, easy markup and styling. The catch here is that even in forward-thinking browsers this property has pretty poor support — there are a number of other properties (like dividers, breakers, etc) that haven't been implemented or at all supported yet. This is just a taste of what's to come — simple columns are on the way, but not here just yet.

&nbsp;
<div style="padding: 25px 15px;background: #fafafafa none repeat scroll 0% 0%"><a href="https://www.zurb.com/playground/newspaper-layout"><img style="float: left;margin-right: 15px" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b98118ae-f7fe-42b3-b62b-4a20dce1acff/newspaper-layout-th.jpg" width="210" height="162" /></a><br>
#### <a href="https://www.zurb.com/playground/newspaper-layout">See the Live Demo »</a>
Check out the Super Awesome Times on the Playground – just creating this prototype got some cool ideas kicking for our own site and blog.

</div>

## Coming Up in CSS3...

We hope you enjoyed this further foray into CSS3. You can still check out our article on CSS3 buttons (including one which, no kidding, glows radioactively). Stay tuned for the third and final article in the series, where we'll take the CSS properties and really go to town with polaroids, an OS X dock, vinyl album music players and more.</p>

### References and Resources:

*   [Pushing Your Buttons with Practical CSS3](https://www.smashingmagazine.com/2009/12/02/pushing-your-buttons-with-practical-css3/)
*   [Using -webkit-mask-image at Surfin' Safari](https://webkit.org/blog/181/css-masks/)
*   [Introduction to Columns at CSS3.info](https://www.css3.info/preview/multi-column-layout/)
*   [RGBa Browser Support at CSS-Tricks](https://css-tricks.com/rgba-browser-support/)
*   [Introduction to CSS Animation at Surfin' Safari](https://webkit.org/blog/138/css-animation/)
*   [Introduction to CSS Transitions at CSS3.info](https://www.css3.info/webkit-introduce-more-new-features/)
*   [Safari Visual Effects Documentation](https://developer.apple.com/safari/library/documentation/InternetWeb/Conceptual/SafariVisualEffectsProgGuide/Introduction/Introduction.html)


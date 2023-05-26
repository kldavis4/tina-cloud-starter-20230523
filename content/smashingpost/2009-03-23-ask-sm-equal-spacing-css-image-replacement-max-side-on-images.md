---
title: '[Ask SM: CSS] Equal Spacing, CSS Font Replacement'
slug: ask-sm-equal-spacing-css-image-replacement-max-side-on-images
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71e56000-ecf3-46ea-bd70-8e34d6c3f081/cssr.jpg
date: 2009-03-23T07:02:45.000Z
author: chris-coyier
description: >-
  This is our fourth installment of Ask SM, **featuring reader questions about
  Web design**, focusing on HTML, CSS and JavaScript. In this post we’ll cover
  how you can distribute the horizontal space between elements evenly, how you
  can achieve maximum sides on images; you'll also learn best practices for CSS
  font replacement and answers to a couple of quickfire questions.

  If you have a question about CSS or JavaScript, feel free to reach me (Chris
  Coyier) via one of these methods: a) Send an email to _ask [at]
  smashingmagazine [dot] com_ with your question; b) [post your question in our
  forum](https://forum.smashingmagazine.com/viewtopic.php?f=10&t=272), c) or, if
  you have a quick question, just tweet us
  [@smashingmag](https://twitter.com/smashingmag) or
  [@chriscoyier](https://twitter.com/chriscoyier).

  [![floaties](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ceb456ab-3c95-4049-a3ff-ac990dfbe751/equidistant.png)](https://www.smashingmagazine.com/2009/03/23/ask-sm-equal-spacing-css-image-replacement-max-side-on-images/)

  Antoine Nicolas writes: _Do you know how to perfectly and **dynamically
  distribute objects horizontally** in a container using CSS?_ This is a classic
  example of something that is fairly difficult to do in CSS but probably
  shouldn't be. I have approached this problem in a number of different ways [in
  the past](https://css-tricks.com/equidistant-objects-with-css/). I have
  revisited it a little now, and I'll present what I believe is the best
  solution here.
categories:
  - Coding
  - CSS
---
This is our fourth installment of Ask SM, featuring reader questions about Web design, focusing on HTML, CSS and JavaScript. In this post we’ll cover how you can distribute the horizontal space between elements evenly, how you can achieve maximum sides on images; you'll also learn best practices for CSS font replacement and answers to a couple of quickfire questions. If you have a question about CSS or JavaScript, feel free to reach me (Chris Coyier) via one of these methods:

1.  Send an email to **ask [at] smashingmagazine [dot] com** with your question.
2.  Post your question in our forum.
3.  Or, if you have a quick question, just tweet us [@smashingmag](https://twitter.com/smashingmag) or [@chriscoyier](https://twitter.com/chriscoyier).

Please note: I will do what I can to answer questions, but I will certainly not be able to answer all of them. However, I hope you use the forums to post questions because that gives you the best opportunity to get help from the community.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [CSS Baseline: The Good, The Bad And The Ugly](https://www.smashingmagazine.com/2012/12/css-baseline-the-good-the-bad-and-the-ugly/)
*   [<span class="headline">Using White Space For Readability In HTML And CSS</span>](https://www.smashingmagazine.com/2013/02/using-white-space-for-readability-in-html-and-css/)
*   [Space Yourself](https://www.smashingmagazine.com/2015/10/space-yourself/)
*   [The Principles Of Cross-Browser CSS Coding](https://www.smashingmagazine.com/2010/06/the-principles-of-cross-browser-css-coding/)

{{% feature-panel %}}

## Distributing the horizontal space between elements evenly

<em>Antoine Nicolas</em> writes:
<blockquote>Do you know how to perfectly and dynamically distribute objects horizontally in a container using CSS?</blockquote>

Hi Antoine, this is a classic example of something that is fairly difficult to do in CSS but probably shouldn't be. I have approached this problem in a number of different ways <a href="https://css-tricks.com/equidistant-objects-with-css/">in the past</a>. I have revisited it a little now, and I'll present what I believe is the best solution here.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ceb456ab-3c95-4049-a3ff-ac990dfbe751/equidistant.png" alt="equal distance" />

Let's review the specific goals:

*   The _left-most_ object is **left-aligned** with its parent element.
*   The _right-most_ object is **right-aligned** with its parent element.
*   All objects are **equidistant** from each other at all times.
*   The objects will **stop short of overlapping** each other as the browser window narrows (ideally).
*   The objects **will not wrap** down as the browser window narrows (ideally).
*   The technique will work in a **fluid-width environment**, even one that is **centered**.

The theory is that the first object will be left-aligned, and the rest of the objects will be right-aligned inside equal-sized boxes that take up the rest of the space. Here is an illustration of what I mean:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4ba67a0-8e33-4f6c-862a-53627ef9e609/floatytechnqiue.png" alt="floaties" />

The HTML markup:

<pre><code class="language-css">name="code"&gt;&lt;div id="row"&gt;
	&lt;img src="images/shape-red.png"&gt;
	&lt;div id="movers-row"&gt;
		&lt;div&gt;&lt;img src="images/shape-green.png"&gt;&lt;/div&gt;
		&lt;div&gt;&lt;img src="images/shape-yellow.png"&gt;&lt;/div&gt;
		&lt;div&gt;&lt;img src="images/shape-blue.png"&gt;&lt;/div&gt;
	&lt;/div&gt;
&lt;/div&gt;</code></pre>

The CSS:

<pre><code class="language-css">name="code"&gt;#row {
    min-width: 480px;
}

#movers-row {
	margin: -120px 0 0 120px;
}

#movers-row div {
	width: 33.3%;
	float: left;
	min-width: 120px;
}

#movers-row div img {
	float: right;
}</code></pre>

And here is a live demo.</p>

## Maximum Sides on Images

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac7d68ad-587f-47e0-86ae-c9a96e687b57/maxside.png" alt="max side" />

<em>J.J. Sylvia IV</em> writes:
<blockquote>Is there a way to determine the dimensions of an image being displayed and change the &lt;img width="" /&gt; setting based on the overall width? Sometimes I have images with a really large height, and I need them to be displayed with a much smaller width than other images.</blockquote>

I talked with J.J. a little more about this to clarify the problem. The problem actually relates to <strong>height</strong>: you have a lot of images, and all of them have different dimensions. You could set a max-width to make sure they keep their ratio and all get squeezed to the right width, but that leaves "jagged" heights. In other words, when you control <strong>only</strong> the width, you get the benefit of maintaining the image ratio, but you cannot control the height and may end up with very tall images screwing up your layout.

So how do you control <strong>both</strong> the height and width while maintaining ratio? We will need to lean on some JavaScript because we have to perform some calculations. As I happen to be a jQuery guy, we'll use that. jQuery is a good choice here anyway, though, because we need to target every single image on the page and do stuff do it, and jQuery makes that very easy and rips through the job.

The best route is to turn this into a plug-in, which will make it a very easy call, as well as allow it to be chained and all that good stuff. We'll call it "maxSide". It looks at each element it calls on and figures out which dimension is larger. If it's the width, it sets the width to the "maxSide" (with the pixel setting passed in). If it's the height, it sets the height to the "maxSide".

Here is the plug-in:

<pre><code class="language-css">name="code"&gt;(function($) {

   $.fn.maxSide = function(settings) {

   // if no paramaters supplied...
   settings = $.extend({
      maxSide: 100
   }, settings);

   return this.each(function() {

      var maximum = settings.maxSide;
      var thing = $(this);
      var thewidth = thing.width();
      var theheight = thing.height();

      if (thewidth &gt;= theheight) {
         if (thewidth &gt;= maximum) {
            thing.attr({
               width: maximum
            });
         }
      }

      if (theheight &gt;= thewidth) {
         if (theheight &gt;= maximum) {
            thing.attr({
               height: maximum
            });
         }
      }

   });	

};

})(jQuery);</code></pre>

Since we intend to call this plug-in with images, we need to make sure all of the images have loaded first. So, instead of calling it when the DOM is ready, like you see in most jQuery, we need to call it once the window has loaded.

<pre><code class="language-css">name="code"&gt;$(window).bind("load", function() {
	$("img").maxSide({ maxSide: "100" });
});;</code></pre>

This may cause some unsightly flashes of large images... C'est la vie. If it's really really awful, you may wish to hide the images with CSS and only reveal them (with jQuery) after the plug-in has run.

Here is a <a href="https://css-tricks.com/examples/MaxSide/">live example</a> of this plug-in at work.

## CSS Font Replacement

<em><a href="https://twitter.com/juliuskoroll">@juliuskoroll</a></em> writes:
<blockquote>I would like to hear font replacement via CSS explained by you guys.</blockquote>

Hi Julius, you got it! We all know we can include images on pages just by including an image tag like this: &lt;img src="https://www.smashingmagazine.com/images/ask-sm-css/..." alt="..." /&gt;. That image can be anything. It can be a logo, a picture of a nice cup of tea, a puppy or even a line of text in a custom font acting as a header. If we want to have headers with nice custom fonts on our website, one option available to us is to just insert them in the page with &lt;img .. /&gt; tags. While this solution has no visual penalty, it has problems. The proper HTML tag to use for headers is the header tag (e.g. &lt;h1&gt;, &lt;h2&gt;, etc). This is best for accessibility as well as SEO (search engine optimization).

You may also be aware that CSS allows us to place background images on elements. This is what gives us the power to have the best of both worlds. We can use a proper header tag, but also use an image. The problem now is that the text within the header tag is sitting right on top of the image. We need to somehow hide the text so that only the image is visible. As it turns out, there are quite a few different ways to do this, and each comes with its own theory. I once did some reasearch on this subject and came up with <a href="https://css-tricks.com/nine-techniques-for-css-image-replacement/">Nine Techniques for CSS Image Replacement</a>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27331293-c9f6-4b53-80d9-7aeb04c26ed1/fontreplacement.png" alt="font replacement" />

The most popular method, in my experience, is known as the Phark method. While it may not be the absolute best method, it works and is very easy to understand.

HTML:

<pre><code class="language-css">name="code"&gt;&lt;h1 class="replace"&gt;
	Smashing Magazine
&lt;/h1&gt;</code></pre>

CSS:

<pre><code class="language-css">name="code"&gt;h1.replace {
	width: 350px; height: 75px;
	background: url("images/header-image.jpg");
	text-indent: -9999px;
}</code></pre>

## Quickfire Questions!

Here are a few questions I wrote down from random sources. Like most Web design questions, they could be answered with a book. But instead, I'll answer them with a single sentence (or two) and a link!
<blockquote><strong>1)</strong> Is there a way to make drop-down menus without JavaScript for IE 6?</blockquote>

Yes, there is, perhaps most famously done by Stu Nicholls of CSSplay, with his <a href="https://www.cssplay.co.uk/menus/final_drop.html">ULTIMATE CSS only drop-down menu</a>.
<blockquote><strong>2)</strong> Is there a way to get PNG transparency without JavaScript or HTC solution in IE 6?</blockquote>

To clarify, this means <strong>alpha</strong> transparency. Regular ol' transparency (think GIFs) works fine with PNGs without any hacks, even in IE 6. Most PNG hacks do indeed use JavaScript or HTC. The root of these techniques is to apply a proprietary CSS "filter" called "AlphaImageLoader" through the "behavior" attribute in CSS. Some of these fixes are incredibly easy to implement, but if you want to avoid them all together, it is a little-known fact that Fireworks can save PNG-8's with alpha transparency.
<blockquote><strong>3)</strong> Is there a way to remove the "Click to activate this control" message for some versions of IE with Flash content?</blockquote>

Yep, inserting Flash objects on your page with <a href="https://code.google.com/p/swfobject/">SWFObject</a> clears up this issue.
<blockquote><strong>4)</strong> Is there a way to have alternate sidebars in WordPress?</blockquote>

Sure, if you have a special page template that you want to display a different sidebar other than your regular one, you can do that. The default WordPress function that calls the sidebar looks like this:

<pre><code class="language-php">&lt;?php get_sidebar(); ?&gt;</code></pre>

It may look like a magical WordPress function, and I suppose it is, but all it does is grab the <em>sidebar.php</em> file from your theme and plop it in. That's it. So, instead, duplicate that <em>sidebar.php</em> file, call it something like <em>sidebar-alternate.php</em> and call it from your special page template like this:

<pre><code class="language-php">&lt;?php include (TEMPLATEPATH . '/sidebar-alternate.php'); ?&gt;</code></pre>

That does about the same exact thing. You can use that same bit of code to include any file from your theme folder.
<blockquote><strong>5)</strong> Can you style "alt" tags using CSS?</blockquote>

The "alt" attribute for elements is only ever displayed if (for whatever reason) the element to which it is applied cannot be rendered. This is most common for &lt;img .. /&gt; elements, but also for &lt;area&gt; elements and optionally for inputs (because they can sometimes be images). So, the only reason you'd ever see "alt text" is when an image link is broken or you are browsing the Web intentionally without images (e.g. using accessibility software).

The answer is <strong>yes</strong>, you can style "alt" text CSS. Simply apply text styling CSS attributes to whatever element it is. I think this is a rather clever idea actually. Images are very eye-catching on Web pages, so when an image is unavailable, why not replace it with very descriptive and eye-catching text.

It seems a little weird, but:

<pre><code class="language-css">name="code"&gt;img {
   color: red;
   font: italic 200% Georgia, Serif;
}</code></pre>

This will sure make that "alt" text pop!

{{< signature "al" >}}


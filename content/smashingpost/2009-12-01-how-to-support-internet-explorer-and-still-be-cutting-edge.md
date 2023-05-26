---
title: How To Support Internet Explorer and Still Be Cutting Edge
slug: how-to-support-internet-explorer-and-still-be-cutting-edge
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ffacc9a-c0ce-4f57-9fcd-9e34ebd7104a/ie.jpg
date: 2009-12-01T14:02:13.000Z
author: inayaili-de-leon
description: >-
  Everyone has been going on about how we should **use CSS3 more** and all of the possibilities and flexibility that come with it, but that we should still consider IE6 and other troubling browsers.
categories:
  - Coding
  - CSS
  - Testing
  - Internet Explorer
---
But how do we actually do that? How do we create websites that are up to date with the latest coding techniques but that are also usable for people experiencing the Web on Internet Explorer?

In this article, we’ll see what measures we can take to <strong>provide a good experience for IE users</strong> but keep moving on. We will mainly focus on the CSS part but will also provide some handy tips on dealing with overall markup.

Also consider our previous articles:

*   [CSS3 Solutions for Internet Explorer](https://www.smashingmagazine.com/2010/04/css3-solutions-for-internet-explorer/)
*   [Taming Advanced CSS Selectors](https://www.smashingmagazine.com/2009/08/17/taming-advanced-css-selectors/)
*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/15/take-your-design-to-the-next-level-with-css3/)
*   [Push Your Web Design Into The Future With CSS3](https://www.smashingmagazine.com/2009/01/08/push-your-web-design-into-the-future-with-css3/)

{{% feature-panel %}}

## The Content Is What Matters

Jeffrey Zeldman once <a href="https://twitter.com/zeldman/statuses/804159148">said</a>, "content precedes design. Design in the absence of content is not design; it's decoration." In fact, the most important thing on your website is the <strong>content</strong>. This is what everyone should be able to get, no matter which browser they’re using.

Using CSS3 doesn’t mean we should forget about older browsers and lock visitors out of our websites. We should check our websites on browsers as old as maybe IE5 or 5.5 and make sure the content is accessible for every user.

This doesn’t mean we should quit the fight to eradicate IE6 either. We can still follow the example of websites such as Twitter and YouTube and add visible but not dead-end warnings to upgrade.

<a href="https://youtube.com"><img loading="lazy" decoding="async" class="16698" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f39f6392-f37c-4540-9344-5e72de811e3e/02youtube.jpg" alt="YouTube's IE6 warning message" width="500" height="93" /></a>

<a href="https://twitter.com"><img loading="lazy" decoding="async" class="16697" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/936120e5-23d5-4e76-a40a-e728c00264b7/01twitter.jpg" alt="Twitter IE6 warning message" width="500" height="273" /></a><br>
<em>YouTube and Twitter warning messages for IE6 users</em>

And remember: each profession has the duty to <strong>educate</strong> those who are not familiar with their trade. We must explain how stuff works to our clients without being patronizing. It’s not their job to know this after all.</p>

## Basics First: The Three Layers (HTML, CSS and JavaScript)

When we create a new website, we do it in steps. First, the HTML. We will mark up our content in the most <strong>semantic</strong> way possible: titles should be marked up as headings, lists as lists, etc. The bottom line is that our content should be perfectly readable and its hierarchy understandable with only this part of the coding done. The content has to make sense, and we must never forget that <strong>this layer is the foundation</strong> on which we will develop all the rest.

Secondly, we add the <strong>style</strong>, the CSS. In this step, we add the visual elements to our design; we give the website its personality. We also make sure that the content is accessible without the third layer.

And finally, the third layer, the JavaScript, the <strong>behavior</strong>. Here we add the interactive elements to our website. We make the experience richer using things such as tabs, sliders, lightboxes, etc.

With this path in mind, our content will always be accessible in any browser. We make sure that older browsers get only the basic content and disregard more complex layers that could hamper their users' access to it.</p>

## Adding Basic Style For Old Browsers

So our semantic markup is done, and we know that some browsers cannot render CSS properly or at all, such as browsers before Netscape 4.0 or Internet Explorer 4.0. For those browsers, displaying the bare content—the naked version—is the safest choice.

Some people say that, today, there is no need to do this. But if you’d like to make sure that these people on these browsers don’t run into any problems, just link to a basic version of your CSS with the <code>link</code> tag and then to the more advanced file with the <code>@import</code> declaration:

<pre><code class="language-markup tmp-xml">&lt;link rel="stylesheet" type="text/css" href="basic.css" media="screen" /&gt;</code></pre>

<pre><code class="language-css">&lt;style type="text/css"&gt;
	@import "advanced.css";
&lt;/style&gt;</code></pre>

You can also skip the <code>link</code> tag altogether and leave them with a text-only version of the website:

<pre><code class="language-css">&lt;style type="text/css"&gt;
	@import "style.css";
&lt;/style&gt;</code></pre>

## Embracing The Differences

Now let’s deal with the black sheep of commonly used browsers: Internet Explorer 6.

You’ve got two options:

1.  If only a negligible percentage of your audience is browsing the Web with it and you don’t want to throw your client’s money down the drain, you could create a basic style sheet for IE6.
2.  Acknowledge that your design will _not_ look the same in IE6, and make decisions on what to leave out: which IE6 quirks will you fix and which will you leave be.

If you choose to feed IE6 a basic style sheet, the best course is to use the <a href="https://code.google.com/p/universal-ie6-css/">Universal IE6 CSS</a>. Your website will have virtually no design, but this style sheet makes sure that the body has a readable width, that heading sizes are reasonable and that the content has some nice white space surrounding it.

In your HTML, you will have to add some conditional comments to link to the style sheet and to hide the other sheets from IE6:

<pre><code class="language-markup tmp-xml">
	&lt;link rel="stylesheet" type="text/css" href="styles.css" media="screen" /&gt;
&lt;!--

	&lt;link rel="stylesheet" type="text/css"
	href="https://universal-ie6-css.googlecode.com/files/ie6.0.3.css" media="screen" /&gt;
</code></pre>

In the first conditional comment, we link our main style sheet to all browsers that are not IE6 (hence the “<code>!</code>”). And in the second comment, we link directly to the Universal IE6 style sheet on Google’s repository (and save some bandwidth at that!).

<a href="https://makephotoshopfaster.com/"><img loading="lazy" decoding="async" class="16752" title="Make Photoshop Faster on Firefox" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44e02f02-d215-46f2-a636-75f2cef115ca/19makepsfaster-1.jpg" alt="Make Photoshop Faster on Firefox" width="500" height="349" /></a>

<a href="https://makephotoshopfaster.com/"><img loading="lazy" decoding="async" class="16753" title="Make Photoshop Faster on IE6" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed4e3d28-19eb-4a35-a59c-3cfddc5895e7/19makepsfaster-2.jpg" alt="Make Photoshop Faster on IE6" width="500" height="345" /></a><br>
<em>The Make Photoshop Faster website uses the Universal style sheet for IE6</em>

If you prefer the second route, you must be prepared to embrace the differences between browser renderings. Know that some details of your design will not be visible or render as nicely in IE6, or even IE7 and 8. And <strong>don’t be upset</strong> about it.

## Resets

As you know, all browsers have different default styles for the various HTML elements. This is why using a reset style sheet is wise, so that we can <strong>start with a clean slate</strong>.

Plenty of style sheets are around on the Internet for anyone’s benefit. The one that is usually considered the standard and most often implemented is <strong><a href="https://meyerweb.com/eric/thoughts/2007/05/01/reset-reloaded/">Eric Meyer’s reset</a></strong>, or some variation of it.

<a href="https://meyerweb.com/eric/thoughts/2007/05/01/reset-reloaded/"><img loading="lazy" decoding="async" class="16702" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/986af0ac-97a5-4557-a759-fab145bce174/04ericmeyer.jpg" alt="Eric Meyer's CSS Reset" width="500" height="356" /></a>

With the advent of HTML5, <strong>including the new HTML elements</strong> in your CSS reset is also a good idea. <a href="https://html5doctor.com/html-5-reset-stylesheet/">html5doctor</a> provides a good update to Eric Meyer’s reset that you can use for free in your projects.

<a href="https://html5doctor.com/html-5-reset-stylesheet/"><img loading="lazy" decoding="async" class="16703" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49ea2b42-85ee-414d-8780-2096269dac9f/05html5doctor.jpg" alt="html5doctor's CSS reset" width="500" height="340" /></a>

You can use a CSS reset either by embedding it at the top of your own CSS file, or, if you like to keep things tidy, by importing it from your style sheet:

<pre><code class="language-markup tmp-xml">@import url(reset.css);</code></pre>

## CSS Differences That Could Break Your Layout

If you decide to use the Universal IE6 CSS, you’ve just saved yourself many a headache. But don’t let the shiny logos of IE7 and 8 fool you: if you intend to use the latest CSS techniques, you still have to do a lot to cater to them.</p>

### IE6 and PNG support

We all know that PNG images with alpha-channel transparency (i.e. the good-looking ones) don’t play nice on IE6. We’ve all seen that annoying light-blue background on our carefully crafted logos.

You can choose from among a few workarounds to this problem so that IE6 can display PNGs. Each is fairly quick to implement and does make a difference in the overall design.

Here are a few of the best scripts and techniques for dealing with this issue:

*   [DD_belatedPNG](https://www.dillerdesign.com/experiment/DD_belatedPNG/)
*   [Supersleight jQuery Plugin](https://allinthehead.com/retro/338/supersleight-jquery-plugin)
*   [PNG 8-bit technique (Fireworks)](https://www.sitepoint.com/blogs/2007/09/18/png8-the-clear-winner/)
*   [Clever PNG Optimization Techniques](https://www.smashingmagazine.com/2009/07/15/clever-png-optimization-techniques/)
*   [PNG Optimization Guide: More Clever Techniques](https://www.smashingmagazine.com/2009/07/25/png-optimization-guide-more-clever-techniques/)

That said, we should mention that more and more Web designers nowadays opt not to fix the PNG issue on IE6:

<a href="https://www.31three.com/"><img loading="lazy" decoding="async" class="16704" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2ac1beb-1a18-40a4-8e82-84321e628ff7/06-31three.jpg" alt="31three website on IE6" width="500" height="501" /></a><br>
<em>The newly revamped 31three website doesn’t apply any fix for PNGs in IE6.</em>

### Advanced Selectors

These selectors are almost the definition of smooth CSS development by themselves, because they hold the <strong>true power</strong> of CSS and can make our lives as developers so much easier (and our budgets so much lower!).

The decision of whether to make them work on Internet Explorer or not depends largely on what you are using them for.

For example, if you are using them to add extra detail to your designs, such as small icons to represent different file types, it won't make a lot of difference if the icons don't display on some browsers. Visitors to your website won’t know what they are missing, and the links will still be perfectly usable.

These selectors are also widely used to enhance typographic detail, and lack of support for them won't be a big issue for your designs.

<a href="https://www.hicksdesign.co.uk/journal/"><img loading="lazy" decoding="async" class="16705" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38307943-a883-4cf9-86aa-ae90171e9d7b/07hicksdesign.jpg" alt="Comparison of the rendering of the Hicksdesign website on Firefox and IE" width="479" height="246" /></a><br>
<em>Hicksdesign uses advanced selectors for numbered bullets in its navigation menu, and they simply aren’t visible for IE6 users</em>

<strong>Which browsers don’t support this?</strong> Internet Explorer 6 will not see styles applied with virtually any advanced selector. It only really understands simple descendant combinators and classes and ID selectors. It even struggles with multiple classes applied to the same element! It’s not to be trusted.

IE7 ignores the <code>:lang</code> selector and pseudo-elements, such as <code>:first-line</code>, <code>:first-letter</code>, <code>:before</code> and <code>:after</code>. But it <em>does</em> understand all attribute selectors.

Also, none of the Internet Explorer releases to date supports the <code>:target</code> pseudo-class, UI element states pseudo-classes (<code>:enabled</code>, <code>:disabled</code>, etc.), structural pseudo-classes (like <code>:nth-child</code>, <code>:nth-of-type</code> or <code>:first-child</code>) or the negation pseudo-element.</p>

### Box-Sizing

Box-sizing allows you to tell the browser how you want it to calculate the width and height of an element.

For example, if you set the <code>box-sizing</code> property to <code>border-box</code>, then the paddings and borders will be subtracted from the specified width and height of that element, instead of added to them (as stated in the W3C's specifications for the <strong>standard box model</strong>).

This can make it easier to control the size of elements and to make sizes behave the same across different browsers.

If you believe that your website renders in IE in quirks mode (and therefore renders with the <em>non-standard</em> box model), you may want to use this property in your style sheets to make all browsers uniform.

Make sure to add the standard property and the vendor-specific ones:

<pre><code class="language-css">div {
	-moz-box-sizing: border-box;
	-webkit-box-sizing: border-box;
	box-sizing: border-box;
}</code></pre>

<strong>Which browsers don’t support this?</strong> If the website is rendered in quirks mode, IE6 will render using the non-standard box model, so it will already be rendering as if it had the “<code>border-box</code>” property on. You can force IE6 to render in quirks mode. There are a few ways of doing this; one way is by adding an HTML comment before the <code>doctype</code> declaration of your HTML pages.</p>

### Media Queries

Media queries <strong>aren’t fully supported</strong> by most browsers, and Internet Explorer doesn’t support them at all.

However, because they are mostly used to call variations of style sheets for handheld devices, such as the iPhone, this fact is almost irrelevant in that case.

If you use media queries mainly to cater to the iPhone, the fact that they are not supported by other browsers makes no difference anyway, and their use is highly encouraged.

If you are using them to create a more flexible website design that adapts to changes in, say, window size, then know that only Safari, Firefox and Opera support them (partially).

<strong>Which browsers don’t support this?</strong> Internet Explorer and, in some instances, Safari and Firefox.</p>

## CSS Differences That Are Mainly Decorative

These are the issues that are <strong>best left alone</strong> for non-supporting browsers, because the lack of support won’t be a problem for users who want to access your content (i.e. your pages won’t break).

This has to do mainly with some of the new CSS3 properties, such as <code>border-radius</code>, <code>text-shadow</code> and <code>border-image</code>.</p>

### Border-radius

This is the first CSS3 property that designers learned to live without on Internet Explorer, because of its clearly decorative nature. With <code>border-radius</code>, you are better off not trying to replicate it on IE at all. Just let it be.

<img loading="lazy" decoding="async" class="16772" title="Gowalla's homepage on Firefox" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77ec6957-83ae-4d52-8655-109d59a9f7b4/08gowalla-1.jpg" alt="Gowalla's homepage on Firefox" width="449" height="155" />

<img loading="lazy" decoding="async" class="16773" title="Gowalla's homepage on IE6" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bb6a093-ece8-445c-b02b-fe09fa25901b/08gowalla-2.jpg" alt="Gowalla's homepage on IE6" width="449" height="155" /><br>
<em>Gowalla uses <code>border-radius</code> on its website, but Internet Explorer users don’t see it.</em>

<strong>Which browsers don’t support this?</strong> All Internet Explorer browsers. Opera, too.</p>

### Font-face

Font-face can be used with IE, but you may need to use <a href="https://www.microsoft.com/typography/WEFT.mspx">Microsoft’s Web Embedding Fonts tool</a> to convert your fonts to EOT.

<a href="https://www.microsoft.com/typography/WEFT.mspx"><img loading="lazy" decoding="async" class="16708" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7c13692-f93a-434b-a00d-4efb1e342f92/09microsoft-tool.jpg" alt="Microsoft Web Embedding Fonts Tool (WEFT)" width="500" height="247" /></a>

If you are including both font formats in your website, your CSS will probably follow this structure:

<pre><code class="language-css">@font-face {
	  font-family: "Delicious";
	  src: url("Delicious-Roman.eot");
	  src: local("Delicious"), url("Delicious-Roman.otf") format("opentype");
}</code></pre>

Usually, a browser not being able to render the first font in a font stack shouldn’t break the website or hamper in any way the user's access to the content. So, the recommendation here is to <strong>carefully ponder which fonts</strong> you want the visitor to see if their browser doesn’t support <code>font-face</code> and has to rely on the fonts you have declared in the style sheet.

<a href="https://elliotjaystocks.com"><img loading="lazy" decoding="async" class="16774" title="Elliot Jay Stock's website on Firefox" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcc2bdd1-c952-4a88-bffb-e9ebe96c16aa/10elliot-1.jpg" alt="Elliot Jay Stock's website on Firefox" width="500" height="151" /></a>

<a href="https://elliotjaystocks.com"><img loading="lazy" decoding="async" class="16775" title="Elliot Jay Stock's website on IE" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/842c75f0-195f-4e15-bd3b-d99a4b136639/10elliot-2.jpg" alt="Elliot Jay Stock's website on IE" width="500" height="122" /></a><br>
<em>A browser that doesn’t support <code>font-face</code> simplys show the next available font in the font stack</em>

<strong>Which browsers don’t support this?</strong> If you use the EOT version for IE, even IE users will see the correct fonts.</p>

### Multiple Columns

Rather than create multiple floating <code>DIV</code>s to organize your text into columns, you can create columns automatically by using the multiple column properties in CSS3. But this means that some browsers won’t see them.

Multiple columns are better used for text, not layout. If you use them on your website, the worst thing that will happen is that visitors see a <strong>wider line of text</strong>.

If you're dealing only with short text, than why not go ahead and use it and finish the job in two minutes? But if it would seriously impair the readability of your content, then your best option is to stick to the regular <code>DIV</code>s to create columns.

<a href="https://yaili.com"><img loading="lazy" decoding="async" class="16777" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/406df9df-273d-469b-b9c5-34b86c5815ae/11yaili-1.jpg" alt="Multiple columns on Firefox" width="500" height="126" /></a>

<a href="https://yaili.com"><img loading="lazy" decoding="async" class="16778" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1bf007f-8f65-4bab-9e42-036c0395c2fe/11yaili-2.jpg" alt="Multiple columns not rendered on IE" width="500" height="127" /></a><br>
<em>Here, the introductory text is displayed using CSS multiple columns. IE users will see normal single-column text.</em>

<strong>Which browsers don’t support this?</strong> Internet Explorer and Opera.</p>

### RGBa and Opacity

RGBa colors are bliss. Rather than use hard-to-update PNG files for backgrounds, you can create the same <strong>transparency effect with CSS</strong>. But IE doesn’t get it. IE6 doesn’t even understand the PNGs to begin with.

It’s safe to assume that these transparencies won’t usually be applied to elements that cover important content; in which case, the content shouldn’t be behind another element in the first place.

So, when using RGBa colors, make sure to <strong>include a normal color before the RBGa one</strong>, so that browsers that don’t understand it will still have a fallback color:

<pre><code class="language-css">div {
	background-color:  #FFFFFF;
	background-color: rgba(255,255,255,.5);
}</code></pre>

Opacity can be applied to IE using the opacity filter, but IE filters work only on elements that have layout:

<pre><code class="language-css">div {
	filter: alpha(opacity = 50);
}</code></pre>

Also, remember that <strong>opacity works differently than RGBa colors</strong>: all of the elements enclosed in this DIV will be rendered transparent.

<a href="https://24ways.org"><img loading="lazy" decoding="async" class="16780" title="24ways website on FIrefox" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/705fa5ae-02eb-4e8b-af0f-da78bf583766/12-24ways-1.jpg" alt="24ways website on FIrefox" width="500" height="189" /></a>

<a href="https://24ways.org"><img loading="lazy" decoding="async" class="16781" title="24ways website on IE8" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73641712-7206-4e19-9457-460d11893532/12-24ways-2.jpg" alt="24ways website on IE8" width="500" height="189" /></a><br>
<em>24ways uses RGBa colors and alpha transparency heavily, even though Internet Explorer doesn't render the transparency.</em>

<strong>Which browsers don’t support this?</strong> Every browser sees opacity, provided that filters are applied. IE doesn’t see RGBa colors.</p>

### Text-shadow

This is an easy call: ignore it. Assuming that the text is still readable, trying to recreate <code>text-shadow</code> any other way than with CSS is a Herculean task. So, unless missing <code>text-shadow</code> would seriously reduce the clarity of a large amount of text, or a small amount (in which case you could use image replacement), you’re better off without it.

<a href="https://brokersdirect.net"><img loading="lazy" decoding="async" class="16783" title="Brokers Direct website on Firefox with text-shadow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f126d97-efd9-4998-8ce2-2ffde12c1507/13brokersdirect-1.jpg" alt="Brokers Direct website on Firefox with text-shadow" width="500" height="103" /></a>

<a href="https://brokersdirect.net"><img loading="lazy" decoding="async" class="16784" title="Brokers Direct website on IE with no text-shadow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66e0d736-f9bc-4b89-8c39-5032277d8ee7/13brokersdirect-2.jpg" alt="Brokers Direct website on IE with no text-shadow" width="500" height="103" /></a><br>
<em>The white text-shadow on Brokers Direct’s website is not visible on Internet Explorer.</em>

<strong>Which browsers don’t support this?</strong> Internet Explorer.</p>

### Border-image

The <code>border-image</code> property gives us an easy way to add beautiful borders to our elements that would otherwise be a nightmare to implement (and that in most instances we would probably choose not to implement).

Because the property is almost always decorative, the best option would be to include a fallback for browsers that don’t support it using the normal <code>border</code> property, and adding the enhanced CSS after it for other browsers.

<a href="https://www.blog.spoongraphics.co.uk/"><img loading="lazy" decoding="async" class="16785" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79b94683-125f-4e91-a553-fade12330dd8/14spoongraphics-1.jpg" alt="SpoonGraphics blog on Firefox with border-image" width="499" height="152" /></a>

<a href="https://www.blog.spoongraphics.co.uk/"><img loading="lazy" decoding="async" class="16786" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07bfe1ee-6cc6-481b-bf85-ce22ed4fceb7/14spoongraphics-2.jpg" alt="SpoonGraphics blog on IE with no border-image" width="499" height="152" /></a><br>
<em>SpoonGraphics uses <code>border-image</code>, but it is not visible in Internet Explorer.</em>

<strong>Which browsers don’t support this?</strong> Answering the opposite question is easier: for now, only Safari and Firefox support this feature.</p>

### Multiple Backgrounds

This feature depends on the design of your website, but in a lot of cases, the lack of a second or even third background will not affect the readability of the page.

Multiple backgrounds in CSS saves us a lot of the development headaches that were caused by having to use different HTML hooks and nested elements to achieve the same effect. So, if you opt to use multiple backgrounds, <strong>you are already choosing</strong> which browsers to display the results to.

If all users seeing all of the backgrounds is important to you, then do it the old way and apply different backgrounds to different elements.

If not, your best bet is to give a fallback to browsers that don’t support it: pick the background that you feel is most important or that best fits the overall design and add that property before the multiple backgrounds one. Browsers that don't support it will ignore the second property.

<strong>Which browsers don’t support this?</strong> Internet Explorer, Opera and Firefox up until version 3.5 (version 3.6 is currently in beta, but it supports multiple backgrounds!).</p>

## Tools

### Modernizr

<a href="https://www.modernizr.com/"><img loading="lazy" decoding="async" class="16715" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f0cdaca-28a8-49f3-84b3-e02d1157057f/15modernizr.jpg" alt="Modernizr homepage" width="500" height="217" /></a>

<a href="https://www.modernizr.com/">Modernizr</a> is a little JavaScript that is quite useful if you are using advanced CSS properties. It adds some classes to the <code>html</code> tag in your pages, to see whether a browser supports certain CSS features, such as:

*   `@font-face`
*   `rgba()`
*   `hsla()`
*   `border-image`
*   `border-radius`
*   `box-shadow`
*   Multiple backgrounds
*   `opacity`
*   CSS animations
*   CSS columns
*   CSS gradients
*   CSS reflections
*   CSS 2-D transforms
*   CSS 3-D transforms
*   CSS transitions

Take <code>border-image</code>. When a page loads in a browser that supports the property, it output <code>borderimage</code>. If the browser doesn’t support it, it outputs <code>no-borderimage</code>.

Modernizr doesn’t <em>enable</em> these features in browsers that don’t support them, but rather gives you important information (in the form of classes) that you can use in your style sheets to apply distinct selectors and properties to elements.</p>

### IE-7.js

<a href="https://code.google.com/p/ie7-js/">IE-7.js</a> makes IE5+ behave like IE8, supporting more advanced selectors and fixing some rendering bugs. Here's an excerpt from the <a href="https://dean.edwards.name/IE7/">creator's website</a>:

*   Added support for advanced selectors: `>`, `+` and `~`; attribute selectors; `:hover`, `:active`, `:focus` for all elements; `:first-child`, `:last-child`, `:only-child`, `:nth-child`, `:nth-last-child`; `:checked`, `:disabled`, `:enabled`; `:empty`, `:not`; `:before`, `:after`, `:content`; `:lang`.
*   It uses the standard box model in standards and quirks mode.
*   Supports `min-` and `max-width` and `-height`.
*   Supports PNG alpha transparency (but doesn’t solve the PNG problem for repeated or positioned backgrounds).

The disadvantage of this technique is that JavaScript has to be enabled for it to work, which is unfortunate. So, you will have to be careful to give users who have disabled JavaScript an acceptable version of your website, especially if some behaviors will not work or, worse, if the lack of JavaScript will break your layout.</p>

## Examples

As they say it, this is easier said than done. So, we’ll show that these ideas can actually be <strong>put into practice</strong> with some nice examples. These are websites we’ve come across that <strong>render differently in different browsers</strong>. In some cases, the differences are quite noticeable, but the developers have chosen to embrace those differences.</p>

### Twitter

<a href="https://twitter.com"><img loading="lazy" decoding="async" class="16730" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c732b3f5-877e-4f5c-a66b-5eed04efa5ca/16twitter-1.jpg" alt="Twitter on Firefox" width="500" height="323" /></a><br>
<em>Twitter in Firefox</em>

<a href="https://twitter.com"><img loading="lazy" decoding="async" class="16731" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/853fdd32-78ad-4bc0-aacb-65e649164241/16twitter-2.jpg" alt="Twitter on IE6" width="500" height="329" /></a><br>
<em>Twitter in IE6</em>

### WordPress

<a href="https://wordpress.org"><img loading="lazy" decoding="async" class="16732" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c24b592e-0340-449b-91bb-131867dd8ff4/17wordpress-1.jpg" alt="WordPress on Firefox" width="500" height="301" /></a><br>
<em>WordPress in Firefox</em>

<a href="https://wordpress.org"><img loading="lazy" decoding="async" class="16733" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b2f27d7-8313-4726-90ba-c0e30c073711/17wordpress-2.jpg" alt="WordPress on IE6" width="500" height="301" /></a><br>
<em>WordPress in IE6</em>

### WWF

<a href="https://panda.org"><img loading="lazy" decoding="async" class="16735" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e14bab0e-6256-46f6-8947-237f26ccd2fb/18wwf-1.jpg" alt="WWF on Firefox" width="500" height="238" /></a><br>
<em>WWF in Firefox</em>

<a href="https://panda.org"><img loading="lazy" decoding="async" class="16736" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91a23b0a-234d-400f-a654-91c36077f447/18wwf-2.jpg" alt="WWF on IE6" width="500" height="238" /></a><br>
<em>WWF in IE6</em>

## Conclusion

Remember that the purpose of this post is not to teach you how to hack IE or deal with its quirks or even how to achieve effects by resorting to JavaScript. Rather, it is to explain how we can design and build websites knowing that differences will arise between browsers.

You won’t see people rioting over the lack of rounded corners on Twitter or WordPress; they aren’t even upset by it, because those differences don’t fundamentally break the websites. People can still use the websites and have a good experience. In most cases, they won’t even notice it!

All we have to do now is explain this politely <strong>but seriously</strong> to our clients, so that we can all contribute to the ever-evolving Web.</p>

## Further Reading And References

*   [Quirks Mode and Strict Mode](https://www.quirksmode.org/css/quirksmode.html)
*   [On Having Layout](https://www.satzansatz.de/cssd/onhavinglayout.html)
*   [The IE6 Equation](https://24ways.org/2008/the-ie6-equation)
*   [Ultimate IE6 Cheatsheet: How to Fix 25+ Internet Explorer 6 Bugs](https://www.virtuosimedia.com/tutorials/ultimate-ie6-cheatsheet-how-to-fix-25-internet-explorer-6-bugs)
*   [Definitive Guide to Taming the IE6 Beast](https://sixrevisions.com/web-development/definitive-guide-to-taming-the-ie6-beast/)
*   [How to Use Modernizr](https://webdesignernotebook.com/css/how-to-use-modernizr/)

## Do your designs have a support for older versions of Internet Explorer (<= 7.0)?

<a href="https://answers.polldaddy.com/poll/2325530/">Do your designs have a support for older versions of Internet Explorer (&lt;=7)?</a><span style="font-size:9px">(<a href="https://www.polldaddy.com">poll</a>)</span>

## Related posts

You may be interested in the following related posts:

*   [Taming Advanced CSS Selectors](https://www.smashingmagazine.com/2009/08/17/taming-advanced-css-selectors/)
*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/15/take-your-design-to-the-next-level-with-css3/)
*   [Push Your Web Design Into The Future With CSS3](https://www.smashingmagazine.com/2009/01/08/push-your-web-design-into-the-future-with-css3/)

{{< signature "al" >}}


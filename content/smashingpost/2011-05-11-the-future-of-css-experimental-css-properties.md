---
title: 'The Future Of CSS: Experimental CSS Properties'
slug: the-future-of-css-experimental-css-properties
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0b62b86-26d0-4223-ac28-d33c40e031fe/title1.jpg
date: 2011-05-11T10:35:25.000Z
author: christian-krammer
summary: >-
  Hidden deep within the treasure chests of browsers are heavily underrated properties which can be quite useful. Have a look at some of the less known CSS 2.1 and CSS3 properties and their support in modern browsers.
description: >-
  Hidden deep within the browsers are heavily underrated properties which can be quite useful. Have a look at some of the less known CSS 2.1 and CSS3 properties and their support in modern browsers.
categories:
  - Coding
  - CSS
  - Resources
---

Despite contemporary browsers supporting a wealth of CSS3 properties, most designers and developers seem to focus on the quite harmless properties such as <code>border-radius</code>, <code>box-shadow</code> or <code>transform</code>. These are well documented, well tested and frequently used, and so it’s almost impossible to not stumble on them these days if you are designing websites.

But hidden deep within the treasure chests of browsers are advanced, heavily underrated properties that don’t get that much attention. Perhaps some of them rightly so, but others deserve more recognition. The greatest wealth lies under the hood of WebKit browsers, and in the age of iPhone, iPad and Android apps, getting acquainted with them can be quite useful.

Even the Gecko engine, used by Firefox and the like, provides some distinct properties. In this article, we will look at some of the less known CSS 2.1 and CSS3 properties and their support in modern browsers.

{{% feature-panel %}}

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0b62b86-26d0-4223-ac28-d33c40e031fe/title1.jpg" alt="" width="500" height="334" /><figcaption>The future of CSS.</figcaption></figure>

**Some explanation:** For each property, I state the support: “**WebKit**” means that it is available only in browsers that use the WebKit engine (Safari, Chrome, iPhone, iPad, Android), and “**Gecko**” indicates the availability in Firefox and the like. Finally, certain properties are part of the official <a href="https://www.w3.org/TR/CSS21">**CSS 2.1.**</a> specification, which means that a broad range of browsers, even older ones, support them. Finally, a label of <a href="https://www.w3.org/Style/CSS/current-work">**CSS3**</a> indicates adherence to this specification, supported by the latest browser versions, such as Firefox 4, Chrome 10, Safari 5, Opera 11.10 and Internet Explorer 9.

## WebKit-Only Properties

### -webkit-mask

This property is quite extensive, so a detailed description is beyond the scope of this article and is certainly worth a more detailed examination, especially because it could turn out to be a time-saver in practical applications.

<code>-webkit-mask</code> makes it possible to apply a mask to an element, thereby enabling you to create a cut-out of any shape. The mask can either be a CSS3 gradient or a semi-transparent PNG image. An alpha value of <code>0</code> would cover the underlying element, and <code>1</code> would fully reveal the content behind. Related properties like <code>-webkit-mask-clip</code>, <code>-webkit-mask-position</code> and <code>-webkit-mask-repeat</code> rely heavily on the syntax of the ones from <code>background</code>. For more info, see the <a href="https://www.webkit.org/blog/181/css-masks">Surfin’ Safari blog</a> and the link below.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34ca5f42-e5c1-4663-b117-c1383a00fd7f/webkitmask.jpg"><img loading="lazy" decoding="async" class="98928" title="webkitmask" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90c860f4-0012-4f79-ad8f-6a22d96fcd3c/webkitmask2.jpg" alt="-webkit-mask" width="500" height="320" /></a><figcaption>-webkit-mask &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34ca5f42-e5c1-4663-b117-c1383a00fd7f/webkitmask.jpg">Large preview</a></figcaption></figure>

**Example**

Image mask:

<pre><code class="language-css">.element {
   background: url(img/image.jpg) repeat;
   -webkit-mask: url(img/mask.png);
}</code></pre>

**Example**

Gradient mask:

<pre><code class="language-css">.element2 {
   background: url(img/image.jpg) repeat;
   -webkit-mask: -webkit-gradient(linear, left top, left bottom, from(rgba(0,0,0,1)), to(rgba(0,0,0,0)));
}</code></pre>

**Further reading**: <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266-SW17">Safari Developer Library</a>

### -webkit-text-stroke

One of the shortcomings of CSS borders is that only rectangular ones are possible. A ray of hope is <code>-webkit-text-stroke</code>, which gives text a border. Setting not only the width but the color of the border is possible. And in combination with <code>color: transparent</code>, you can create outlined text.

**Examples**

Assigns a blue border with a 2-pixel width to all <code>&lt;h1&gt;</code> headings:

<pre><code class="language-css">h1 {-webkit-text-stroke: 2px blue}</code></pre>

Another feature is the ability to smooth text by setting a transparent border of 1 pixel:

<pre><code class="language-css">h2 {-webkit-text-stroke: 1px transparent}</code></pre>

Creates text with a red outline:

<pre><code class="language-css">h3 {
   color: transparent;
   -webkit-text-stroke: 4px red;
}</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fa66442-195b-4058-9e75-e2b36dc3d569/webkittextstroke.jpg"><img loading="lazy" decoding="async" class="98929" title="webkittextstroke" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fa66442-195b-4058-9e75-e2b36dc3d569/webkittextstroke.jpg" alt="-webkit-text-stroke" width="496" height="53" /></a><figcaption>-webkit-text-stroke &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fa66442-195b-4058-9e75-e2b36dc3d569/webkittextstroke.jpg">Large preview</a></figcaption></figure>

**Further reading**: <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/css/property/-webkit-text-stroke">Safari Developer Library</a>

### -webkit-nbsp-mode

Wrapping can be pretty tricky. Sometimes you want text to break (and not wrap) at certain points, and other times you don’t want this to happen. One property to control this is <code>-webkit-nbsp-mode</code>. It lets you change the behavior of the <code>&amp;nbsp;</code> character, forcing text to break even where it is used. This behavior is enabled by the value <code>space</code>.

**Further reading**: <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266--webkit-nbsp-mode">Safari Developer Library</a>

### -webkit-tap-highlight-color

This one is just for iOS (iPhone and iPad). When you tap on a link or a JavaScript clickable element, it is highlighted by a semi-transparent gray background. To override this behavior, you can set <code>-webkit-tap-highlight-color</code> to any color. To disable this highlighting, a color with an alpha value of <code>0</code> must be used.

**Example**

Sets the highlight color to red, with a 50% opacity:

<pre><code class="language-css">-webkit-tap-highlight-color: rgba(255,0,0,0.5);</code></pre>

**Supported by**: iOS only (iPhone and iPad).

**Further reading**: <a href="https://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266-_webkit_tap_highlight_color">Safari Developer Library</a>

### zoom: reset

Normally, <code>zoom</code> is an Internet Explorer-only <a href="https://reference.sitepoint.com/css/zoom/demo">property</a>. But in combination with the value <code>reset</code>, WebKit comes into play (which, funny enough, IE doesn’t support). It enables you to override the standard behavior of zooming on websites. If set with a CSS declaration, everything except the given element is enlarged when the user zooms on the page.

**Further reading**: <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266-SW15">Safari Developer Library</a>

### -webkit-margin-collapse

Here is a property with a quite limited practical use, but it is still worth mentioning. By default, the margins of two adjacent elements collapse, which means that the bottom distance of the first element and the top distance of the second element merge into a single gap.

The best example is two <code>&lt;p&gt;</code>s that share their margins when placed one after another. To control this behavior, we can use <code>-webkit-margin-collapse</code>, <code>-webkit-margin-top-collapse</code> or <code>-webkit-margin-bottom-collapse</code>. The standard value is <code>collapse</code>. The <code>separate</code> value stops the sharing of margins, which means that both the bottom margin of the first element and the top margin of the second are included.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baa21d3b-ede4-43b0-8c0c-c7e03c2961a3/webkitmargincollapse.jpg"><img loading="lazy" decoding="async" class="98927" title="webkitmargincollapse" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baa21d3b-ede4-43b0-8c0c-c7e03c2961a3/webkitmargincollapse.jpg" alt="-webkit-margin-collapse" width="495" height="242" /></a><figcaption>-webkit-margin-collapse &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baa21d3b-ede4-43b0-8c0c-c7e03c2961a3/webkitmargincollapse.jpg">Large preview</a></figcaption></figure>

**Further reading**: <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266--webkit-margin-collapse">Safari Developer Library</a>

### -webkit-box-reflect

Do you remember the days when almost every website featured a reflection of either its logo or some text in the header? Thankfully, those days are gone, but if you’d like to make a subtle use of this technique for your buttons, navigation or other UI elements with CSS, then <code>-webkit-box-reflect</code> is the property for you.

It accepts the keywords <code>above</code>, <code>below</code>, <code>left</code> and <code>right</code>, which set where the reflection is drawn, as well as a numeric value that sets the distance between the element and its reflection. Beyond that, mask images are supported as well (see <a href="#mask"><code>-webkit-mask</code></a> for an explanation of masks). The reflection is created automatically and has no effect on the layout. Following elements are created using only CSS, and the second button is reflected using the <code>-webkit-box-reflect</code>-property.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb5596f6-f112-4df8-8177-1ac5fabdc63a/webkitboxreflect.jpg"><img loading="lazy" decoding="async" class="98926" title="webkitboxreflect" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb5596f6-f112-4df8-8177-1ac5fabdc63a/webkitboxreflect.jpg" alt="-webkit-box-reflect" width="421" height="265" /></a><figcaption>-webkit-box-reflect &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb5596f6-f112-4df8-8177-1ac5fabdc63a/webkitboxreflect.jpg">Large preview</a></figcaption></figure>

**Examples**

This reflection would be shown under its parent element and have a spacing of 5 pixels:

<pre><code class="language-css">-webkit-box-reflect: below 5px;</code></pre>

This reflection would be cast on the right side of the element, with no distance (<code>0</code>); additionally, a mask would be applied (<code>url(mask.png)</code>):

<pre><code class="language-css">-webkit-box-reflect: right 0 url(mask.png);</code></pre>

**Further reading**: <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266-SW16">Safari Developer Library</a>

### -webkit-marquee

Here is another property that recalls the good ol’ days when marquees were quite common. Interesting that this widely dismissed property turns out to be be useful today, when we shift content on tiny mobile screens that would otherwise not be fully visible without wrapping.

The weather application by <a href="https://i.ozpda.com/ozweather/">ozPDA</a> makes great use of it. (If you don’t see shifting text, just select another city at the bottom of the app. WebKit browser required.)

**Example**

<pre><code class="language-css">.marquee {
   white-space: nowrap;
   overflow:-webkit-marquee;
   width: 70px;
   -webkit-marquee-direction: forwards;
   -webkit-marquee-speed: slow;
   -webkit-marquee-style: alternate;
}</code></pre>

There are some prerequisites for the marquee to work. First, <code>white-space</code> must be set to <code>nowrap</code> if you want the text to be on one line. Also, <code>overflow</code> must be set to <code>-webkit-marquee</code>, and <code>width</code> set to something narrower than the full length of the text.

The remaining properties ensure that the text scrolls from left to right (<code>-webkit-marquee-direction</code>), shifts back and forth (<code>-webkit-marquee-style</code>) and moves at a slow rate (<code>-webkit-marquee-speed</code>). Additional properties are <code>-webkit-marquee-repetition</code>, which sets how many iterations the marquee should pass through, and <code>-webkit-marquee-increment</code>, which defines the degree of speed in each increment.

**Further reading**: <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266-_webkit_marquee">Safari Developer Library</a>

## Gecko-Only Properties

### font-size-adjust

Unfortunately, this useful CSS3 property is supported only by Firefox at the moment. We can use it to specify that the font size for a given element should relate to the height of lowercase letters (x-height) rather than the height of uppercase letters (cap height). For example, Verdana is much more legible at the same size than Times, which has a much shorter x-height. To compensate for this behavior, we can adjust the latter with <code>font-size-adjust</code>.

This property is particularly useful in CSS font stacks whose fonts have different x-heights. Even if you’re careful to use only similar fonts, <code>font-size-adjust</code> can provide a solution when problems arise.

**Example**

If Verdana is not installed on the user’s machine for some reason, then Arial is adjusted so that it has the same aspect ratio as Verdana, which is 0.58 (at a font size of 12px, differs on other sizes).

<pre><code class="language-css">p {
   font-family:Verdana, Arial, sans-serif;
   font-size: 12px;
   font-size-adjust: 0.58;
}</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce4c8b87-7d46-48b3-b4eb-4ed257727333/fontsizeadjust.jpg"><img loading="lazy" decoding="async" class="98919" title="fontsizeadjust" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce4c8b87-7d46-48b3-b4eb-4ed257727333/fontsizeadjust.jpg" alt="font-size-adjust" width="485" height="78" /></a><figcaption>font-size-adjust &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce4c8b87-7d46-48b3-b4eb-4ed257727333/fontsizeadjust.jpg">Large preview</a></figcaption></figure>

**Supported by**: Gecko.

**Further reading**: <a href="https://developer.mozilla.org/en/CSS/font-size-adjust">Mozilla Developer Network</a>

### image-rendering

A few years ago, images that were not displayed at their original size and were scaled by designers, could appear unattractive or just plain wrong in the browser, depending on the size and context. Nowadays, browsers have a much better algorithm for displaying resized images, however, it’s great to have a full control over the ways your images will be displayed when scaled, especially with responsive images becoming a de facto standard in responsive Web designs.

This Gecko-specific property is particularly useful if you have an image with sharp lines and want to maintain them after resizing. The relevant value would be <code>-moz-crisp-edges</code>. The same algorithm is used at <code>optimizeSpeed</code>, whereas <code>auto</code> and <code>optimizeQuality</code> indicate the standard behavior (which is to resize elements with the best possible quality). The <code>image-rendering</code> property can also be applied to <code>&lt;video&gt;</code> and <code>&lt;canvas&gt; </code> elements, as well as background images. It is a CSS3 property, but is currently supported only by Firefox.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afe5c87e-564a-4f9a-9555-81164abdb136/imagerendering.jpg"><img loading="lazy" decoding="async" class="98920" title="imagerendering" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afe5c87e-564a-4f9a-9555-81164abdb136/imagerendering.jpg" alt="image-rendering" width="500" height="351" /></a><figcaption>image-rendering &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afe5c87e-564a-4f9a-9555-81164abdb136/imagerendering.jpg">Large preview</a></figcaption></figure>

It’s also worth mentioning <code>-ms-interpolation-mode: bicubic</code>, although it is a proprietary Internet Explorer property. Nevertheless, it enables Internet Explorer 7 to render images at a much higher quality after resizing which is useful because by default this browser handles such tasks pretty poorly.

**Supported by**: Gecko.

**Further reading**: <a href="https://developer.mozilla.org/en/CSS/image-rendering">Mozilla Developer Network</a>

### -moz-border-top-colors

This property could be filed under ‘eye-candy’. It allows you to assign different colors to borders that are wider than 1 pixel. Also available are <code>-moz-border-bottom-colors</code>, <code>-moz-border-left-colors</code> and <code>-moz-border-right-colors</code>.

Unfortunately, there is no condensed version like <code>-moz-border-colors</code> for this property, so the <code>border</code> property must be set in order for it to work, whereas <code>border-width</code> should be the same as the number of the given color values. If it is not, then the last color value is taken for the rest of the border.

**Example**

Below, the element’s border would have a standard color of orange applied to the left and right side (because <code>-moz-border-left-colors</code> and <code>-moz-border-right-colors</code> are not set). The top and bottom borders have a kind of gradient, with the colors red, yellow and blue.

<pre><code class="language-css">div {
   border: 3px solid orange;
   -moz-border-top-colors: red yellow blue;
   -moz-border-bottom-colors: red yellow blue;
}</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eddace95-5d6c-4212-b9ab-88b36a32ecd7/mozbordercolors.jpg"><img loading="lazy" decoding="async" class="98921" title="mozbordercolors" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eddace95-5d6c-4212-b9ab-88b36a32ecd7/mozbordercolors.jpg" alt="-moz-border-top-colors" width="421" height="155" /></a><figcaption>-moz-border-top-colors &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eddace95-5d6c-4212-b9ab-88b36a32ecd7/mozbordercolors.jpg">Large preview</a></figcaption></figure>

**Supported by**: Gecko.

**Further reading**: <a href="https://developer.mozilla.org/en/CSS/-moz-border-top-colors">Mozilla Developer Network</a>

{{% ad-panel-leaderboard %}}

## Mixed Properties

### -webkit-user-select and -moz-user-select

There might be times when you don’t want users to be able to select text, whether to protect it from copying or for another reason. One solution is to set <code>-webkit-user-select</code> and <code>-moz-user-select</code> to <code>none</code>. Please use this property with caution: since most users are looking for information that they can copy and store for future reference, this property is neither helpful nor effective. In the end, the user could always look up the source code and take the content even if you have forbidden the traditional copy-and-paste. We do not know why this property exists in both WebKit and Gecko browsers.

**Supported by**: WebKit, Gecko.

**Further reading**: <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266--webkit-user-select">Safari Developer Library</a>, <a href="https://developer.mozilla.org/en/CSS/-moz-user-select">Mozilla Developer Network</a>

### -webkit-appearance and -moz-appearance

Ever wanted to easily camouflage an image to look like a radio button? Or an input field to look like a checkbox? Then <code>appearance</code> will come in handy. Even if you wouldn’t always want to mask a link so that it looks like a button (see example below), it’s nice to know that you can do it if you want.

**Example**

<pre><code class="language-css">a {
   -webkit-appearance: button;
   -moz-appearance: button;
}</code></pre>

**Supported by**: WebKit, Gecko.

**Further reading**: <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266-_webkit_appearance">Safari Developer Library</a>, <a href="https://developer.mozilla.org/en/CSS/-moz-appearance">Mozilla Developer Network</a>

### text-align: -webkit-center/-moz-center

This is one property (or value, to be exact) whose existence is quite surprising. To center a block-level element, one would usually set <code>margin</code> to <code>0 auto</code>. But you could also set the <code>text-align</code> property of the element’s container to <code>-moz-center</code> and <code>-webkit-center</code>. You can align left and right with <code>-moz-left</code> and <code>-webkit-left</code> and then <code>-moz-right</code> and <code>-webkit-right</code>, respectively.

**Supported by**: WebKit, Gecko.

**Further reading**: <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266-text-align">Safari Developer Library</a>, <a href="https://developer.mozilla.org/en/CSS/text-align">Mozilla Developer Network</a>

## CSS 2.1\. Properties

### counter-increment

How often have you wished you could automatically number an ordered list or all of the headings in an article? Unfortunately, there is still no CSS3 property for that. But let’s look back to CSS 2.1, in which <code>counter-increment</code> provides a solution. That means it’s been around for several years, and even supported in Internet Explorer 8. Did you know that? Me neither.

In conjunction with the <code>:before</code> pseudo-element and the <code>content</code> property, <code>counter-increment</code> can add automatic numbering to any HTML tag. Even nested counters are possible.

**Example**

For numbered headings, first reset the counter to start at 1:

<pre><code class="language-css">body {counter-reset: thecounter}</code></pre>

Every <code>&lt;h1&gt;</code> would get the prefix “Section,” including a counter that automatically increments by <code>1</code> (which is default and can be omitted), where <code>thecounter</code> is the name of the counter:

<pre><code class="language-css">.counter h1:before {
   counter-increment: thecounter 1;
   content:"Section"counter(thecounter)":";
}</code></pre>

**Example**

For a nested numbered list, the counter is reset and the automatic numbering of <code>&lt;ol&gt;</code> is switched off because it features no nesting:

<pre><code class="language-css">ol {
    counter-reset: section;
    list-style-type: none;
}</code></pre>

Then, every <code>&lt;li&gt;</code> is given automatic incrementation, and the separator is set to be a point (.), followed by a blank.

<pre><code class="language-css">li:before {
    counter-increment: section;
    content: counters(section,".")"";
}</code></pre>

<pre><code class="language-markup tmp-xml">&lt;ol&gt;
   &lt;li&gt;item&lt;/li&gt;        &lt;!-- 1 --&gt;
   &lt;li&gt;item            &lt;!-- 2 --&gt;
      &lt;ol&gt;
         &lt;li&gt;item&lt;/li&gt;  &lt;!-- 1.1 --&gt;
         &lt;li&gt;item&lt;/li&gt;  &lt;!-- 1.2 --&gt;
      &lt;/ol&gt;
   &lt;/li&gt;
   &lt;li&gt;item&lt;/li&gt;        &lt;!-- 3 --&gt;
&lt;ol&gt;</code></pre>

**Supported by**: CSS 2.1., all modern browsers, IE 7+.

**Further reading**: <a href="https://www.w3.org/TR/CSS21/generate.html#counters">W3C</a>

### quotes

Are you tired of using wrong quotes just because your CMS doesn’t know how to properly convert them to the right ones? Then start using the <code>quotes</code> property to set them how you want. This way, you can use any character. You would then assign the quotes to the desired element using the <code>:before</code> and <code>:after</code> pseudo-elements. Unfortunately, the otherwise progressive WebKit browsers don’t support this property, which means no quotes are shown at all.

**Example**

The first two characters determine the quotes for the first level of a quotation, the last two for the second level, and so on:

<pre><code class="language-css">q {
   quotes: '«' '»' "‹" "›";
}</code></pre>

These two lines assign the quotes to the selected element:

<pre><code class="language-css">q:before {content: open-quote}
q:after  {content: close-quote}</code></pre>

So, <code>&lt;p&gt;&lt;q&gt;This is a very &lt;q&gt;nice&lt;/q&gt; quote.&lt;/q&gt;&lt;/p&gt; </code> would give us:
**«This is a very ‹nice› quote.»**

**Supported by**: CSS 2.1., all browsers except WebKit, even IE 7+.

**Further reading**: <a href="https://www.w3.org/TR/CSS2/generate.html#quotes">W3C</a>

**Question:** To add the character directly, does the CSS document have to have a UTF-8 character set? That’s a tough one. Unfortunately, I can’t give a definitive answer. My experimentation has shown that no character set has to be set for the <code>quotes</code> property to work properly. However the <code>utf-8</code> character set doesn’t work because it shows “broken” characters (for example, “»”). With the <code>iso-8859-1</code> character set, everything works fine.

This is how the W3C <a href="https://www.w3.org/TR/CSS21/generate.html">describes it</a>: “While the quotation marks specified by ‘quotes’ in the previous examples are conveniently located on computer keyboards, high-quality typesetting would require different ISO 10646 characters.”

## CSS3 Properties You May Have Heard About But Can’t Remember

To round out things, let’s go over some CSS3 properties that are not well known and maybe not as appealing as the classic ones <code>border-radius</code> and <code>box-shadow</code>.

### text-overflow

Perhaps you’re familiar with this problem: a certain area is too small for the text that it contains, and you have to use JavaScript to cut the string and append “…” so that it doesn’t blow out the box.

Forget that! With CSS3 and <code>text-overflow: ellipsis</code>, you can force text to automatically end with “…” if it is longer than the width of the container. The only requirement is to set <code>overflow</code> to <code>hidden</code>. Unfortunately, this is not supported by Firefox but will hopefully be implemented in a coming release.

**Example**

<pre><code class="language-css">div {
   width: 100px;
   text-overflow: ellipsis;
}</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3912573a-d571-4ed2-855a-91ad51eea16d/textoverflow.jpg"><img loading="lazy" decoding="async" class="98924" title="textoverflow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3912573a-d571-4ed2-855a-91ad51eea16d/textoverflow.jpg" alt="text-overflow" width="500" height="190" /></a><figcaption>text-overflow &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3912573a-d571-4ed2-855a-91ad51eea16d/textoverflow.jpg">Large preview</a></figcaption></figure>

**Supported by**: CSS 3, all browsers except Firefox, even IE6+.

**Further reading**: <a href="https://www.w3.org/TR/2010/WD-css3-text-20101005/#text-overflow">W3C</a>

### word-wrap

With text in a narrow column, sometimes portions of it are too long to wrap correctly. Link URLs especially cause trouble. If you don’t want to hide the overflowing text with <code>overflow: hidden</code>, then you can set <code>word-wrap</code> to <code>break-word</code>, which causes it to break when it reaches the limit of the container.

**Example**

<pre><code class="language-css">div {
   width: 50px;
   word-wrap: break-word;
}</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/346f2702-659e-4a72-8aba-ea030a0543cc/wordwrap.jpg"><img loading="lazy" decoding="async" class="98930" title="wordwrap" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/346f2702-659e-4a72-8aba-ea030a0543cc/wordwrap.jpg" alt="word-wrap" width="484" height="189" /></a><figcaption>word-wrap &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/346f2702-659e-4a72-8aba-ea030a0543cc/wordwrap.jpg">Large preview</a></figcaption></figure>

**Supported by**: CSS 3, all browsers, even IE6+.

**Further reading**: <a href="https://www.w3.org/TR/2011/WD-css3-text-20110215/#word-wrap">W3C</a>

### resize

If you use Firefox or Chrome, then you must have noticed that text areas by default have a little handle in the bottom-right corner that lets you resize them. This standard behavior is achieved by the CSS3 property <code>resize: both</code>.

But it’s not limited to text areas. It can be used on any HTML element. The <code>horizontal</code> and <code>vertical</code> values limit the resizing to the horizontal and vertical axes, respectively. The only requirement is that <code>overflow</code> be set to anything other than <code>visible</code>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8290fa0-2643-4c05-ac07-2ffadd8a1bce/resize.jpg"><img loading="lazy" decoding="async" class="98922" title="resize" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8290fa0-2643-4c05-ac07-2ffadd8a1bce/resize.jpg" alt="resize" width="443" height="166" /></a><figcaption>resize &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8290fa0-2643-4c05-ac07-2ffadd8a1bce/resize.jpg">Large preview</a></figcaption></figure>

**Supported by**: CSS3, all the latest browsers except Opera and Internet Explorer.

**Further reading**: <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266-resize">Safari Developer Library</a>

### background-attachment

When you assign a background image to an element that is set to <code>overflow: auto</code>, it is fixed to the background and doesn’t scroll. To disable this behavior and enable the image to scroll with the content, set <code>background-attachment</code> to <code>local</code>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff4a3867-567e-4cd0-8cdb-834dcca96363/backgroundattachment.jpg"><img loading="lazy" decoding="async" class="98918" title="backgroundattachment" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff4a3867-567e-4cd0-8cdb-834dcca96363/backgroundattachment.jpg" alt="background-attachment" width="500" height="213" /></a><figcaption>background-attachment &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff4a3867-567e-4cd0-8cdb-834dcca96363/backgroundattachment.jpg">Large preview</a></figcaption></figure>

**Supported by**: CSS 3, all the latest browsers except Firefox.

**Further reading**: <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266-background-attachment">Safari Developer Library</a>

### text-rendering

With more and more websites rendering fonts via the <code>@font-face</code> attribute, legibility becomes a concern. Problems can occur particularly at small font sizes. While there is still no CSS property to control the subtle details of displaying fonts online, you can enable <a href="https://en.wikipedia.org/wiki/Kerning">kerning</a> and <a href="https://en.wikipedia.org/wiki/Typographic_ligature">ligatures</a> via <code>text-rendering</code>.

Gecko and WebKit browsers handle this property quite differently. The former enables these features by default, while you have to set it to <code>optimizeLegibility</code> in the latter.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be69c3b8-6568-471a-9806-1dacd97641d3/textrendering.jpg"><img loading="lazy" decoding="async" class="98925" title="textrendering" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be69c3b8-6568-471a-9806-1dacd97641d3/textrendering.jpg" alt="text-rendering" width="461" height="169" /></a><figcaption>text-rendering &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be69c3b8-6568-471a-9806-1dacd97641d3/textrendering.jpg">Large preview</a></figcaption></figure>

**Supported by**: CSS3, all WebKit browsers and Firefox.

**Further reading**: <a href="https://developer.mozilla.org/en/CSS/text-rendering">Mozilla Developer Network</a>

### transform: rotateX/transform: rotateY

If you’ve already dived into CSS3 and transformations a bit, then you’re probably familiar with <code>transform: rotate()</code>, which rotates an element around its z-axis.

But did you know that it is also possible to spin it “into the deep” (i.e. around its x-axis and y-axis)? These transformations are particularly useful in combination with <code>-webkit-backface-visibility: hidden</code>, if you want to rotate an element and reveal another one at its back. This technique is described by Andy Clarke in his latest book, <em>Hardboiled Web Design</em>.

**Example**

If you hover over the element, it will turn by 180°, revealing its back:

<pre><code class="language-css">div:hover {
   transform: rotateY(180deg);
}</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8804a107-9dce-4deb-8dfa-ec6f28b77225/rotate.jpg"><img loading="lazy" decoding="async" class="98923" title="rotate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8804a107-9dce-4deb-8dfa-ec6f28b77225/rotate.jpg" alt="transform: rotate" width="425" height="293" /></a><figcaption>transform: rotateY &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8804a107-9dce-4deb-8dfa-ec6f28b77225/rotate.jpg">Large preview</a></figcaption></figure>

**Quick tip:** To just mirror an element, you can either set <code>transform</code> to <code>rotateX(180deg)</code> (and respectively <code>rotateY</code>) or set <code>transform</code> to <code>scaleX(-1)</code> (and respectively <code>scaleY</code>).

**Supported by**: CSS3, only WebKit browsers, in combination with <code>-webkit-backface-visibility</code> only Safari and iOS (iPhone and iPad).

**Further reading**: Safari Developer Library (<a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/Functions.html#//apple_ref/doc/uid/TP40007955-SW17">transform: rotate</a>, <a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266-_webkit_backface_visibility">-webkit-backface-visibility</a>)

## Some Last Words

As you hopefully have seen, there are many unknown properties that range from being nice to hav to being very useful. Many of them are still at an experimental stage and may never leave it or even be discarded in future browser releases. Others will hopefully be adopted by all browser manufacturers in coming versions.

While it is hard to justify using some of them, the WebKit-specific ones are gaining more and more importance with the success of the iOS devices and Android. And of course some CSS3 properties are more or less ready to be used now.

And if you don’t like vendor-specific properties, you can see them as experiments that still could be implemented in the code to improve the user experience for users browsing with the modern browsers. By the way, <a href="https://lists.w3.org/Archives/Public/www-validator-css/2011Jan/0020.html">CSS validator</a> from the W3C now also supports vendor-specific properties, which result in warnings rather than errors.

Happy experimenting!

{{% ad-panel-leaderboard %}}

### Further Reading

*   [An Ultimate Guide To CSS Pseudo-Classes And Pseudo-Elements](https://www.smashingmagazine.com/2016/05/an-ultimate-guide-to-css-pseudo-classes-and-pseudo-elements/)
*   [Houdini: Maybe The Most Exciting Development In CSS](https://www.smashingmagazine.com/2016/03/houdini-maybe-the-most-exciting-development-in-css-youve-never-heard-of/)
*   [Learning CSS3: A Reference Guide](https://www.smashingmagazine.com/learning-css3-useful-reference-guide/)
*   [Start Using CSS3 Today: Techniques and Tutorials](https://www.smashingmagazine.com/2010/06/start-using-css3-today-techniques-and-tutorials/)

{{< signature "al, mrn" >}}

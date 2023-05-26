---
title: Take Your Design To The Next Level With CSS3
slug: take-your-design-to-the-next-level-with-css3
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2eb272b-9cfe-4cdd-b775-ddc93c12744d/css3.jpg
date: 2009-06-15T08:20:27.000Z
author: inayaili-de-leon
description: >-
  Cascading Style Sheets were introduced 13 years ago, and the widely adopted CSS 2.1 standard has existed for 11 years now. When we look at websites that were created 11 years ago, it's clear that we are a thousand miles away from that era. It is quite remarkable how much Web development has evolved over the years, in a way we would never have imagined then.
categories:
  - Coding
  - CSS
  - Techniques
  - CSS3
---
So why is it that, when it comes to CSS, we're stuck in the past and so afraid of experimenting? Why is it that we still use inconvenient CSS hacks and JavaScript-dependent techniques for styling? Why can't we <strong>make use of the rich CSS3 features and tools available in modern Web browsers</strong> and take the quality of our designs to the next level?

It's time to introduce CSS3 features into our projects and not be afraid to gradually incorporate CSS3 properties and selectors in our style sheets. Making our clients aware of the <strong>advantages of CSS3</strong> (and letting older deprecated browsers fade away) is in our power, and we should act on it, especially if it means making websites more flexible and reducing development and maintenance costs.

In this article, we'll look at the advantages of CSS3 and some examples of how Web designers are already using it. By the end, we'll know a bit of what to expect from CSS3 and how we can use its new features in our projects.

Please also consider reading our previous, related article:

{{% feature-panel %}}

*   [Learning CSS3: A Reference Guide](https://www.smashingmagazine.com/learning-css3-useful-reference-guide/)
*   [Push Your Web Design Into The Future With CSS3](https://www.smashingmagazine.com/2009/01/08/push-your-web-design-into-the-future-with-css3/)
*   [Why We Should Start Using CSS3 And HTML5 Today](https://www.smashingmagazine.com/2010/12/why-we-should-start-using-css3-and-html5-today/)

## Using Browser-Specific Properties

To use most CSS3 properties today, we have to use <strong>vendor-specific extensions</strong> together with the original properties. The reason is that until now, browsers have only partially implemented new CSS3 properties. Unfortunately, some properties may not even become W3C recommendations in the end, so it's important to target browser-specific properties by differentiating them from standard properties to (and then replacing them with the standardized ones when they become superfluous).

The disadvantages to this approach are, of course, a messy style sheet and inconsistent design across Web browsers. After all, we do not want to revive the need for proprietary browser hacks in our style sheets. Internet Explorer's infamous <code>&lt;marquee&gt;</code>, <code>&lt;blink&gt;</code> and other tags were employed in many style sheets and became legendary in the 1990s; they still make many existing websites inconsistent or even unreadable. And we don't want to put ourselves in the same situation now, right?

However, websites <a href="https://dowebsitesneedtolookexactlythesameineverybrowser.com/">do not</a> have to look exactly the same in all browsers. And using browser-specific properties to achieve particular effects in certain browsers sometimes makes sense.

The <strong>most common extensions</strong> are the ones used for Webkit-based browsers (for example, Safari), which start with <code>-webkit-</code>, and Gecko-based browsers (for example, Firefox), which start with <code>-moz-</code>. Konqueror (<code>-khtml-</code>), Opera (<code>-o-</code>) and Internet Explorer (<code>-ms-</code>) have their own proprietary extensions.

As professional designers, we have to bear in mind that <strong>using these vendor-specific properties will make our style sheets invalid</strong>. So putting them in the final version of a style sheet is rarely a sound idea for design purists. But in some cases, like when experimenting or learning, we can at least consider including them in a style sheet together with standardized CSS properties.</p>

### Useful Links

*   [Vendor-specific extensions and W3C](https://www.w3.org/TR/CSS21/syndata.html#vendor-keywords)
*   [Vendor-specific extensions to CSS3](https://www.css3.info/vendor-specific-extensions-to-css3/)
*   [Vendor-specific properties](https://reference.sitepoint.com/css/vendorspecific)

## 1\. Selectors

CSS Selectors are an incredibly powerful tool: they allow us to <strong>target specific HTML elements in our markup</strong> without having to rely on unnecessary classes, IDs and JavaScripts. Most of them aren't new to CSS3 but are not as widely used as they should be. Advanced selectors can be helpful if you are trying to achieve a clean, lightweight markup and better separation of structure and presentation. They can reduce the number of classes and IDs in the markup and make it easier for designers to maintain a style sheet.

### Attribute selectors

Three new kinds of attribute selectors are a part of CSS3 specs:

*   `[att^="value"]` Matches elements to an attribute that starts with the specified value.
*   `[att$="value"]` Matches elements to an attribute that ends with the specified value.
*   `[att*="value"]` Matches elements to an attribute that contains the specified value.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17de4385-e0b1-42bc-90ae-ff8e9a8858f4/css3-tweetcc-2.jpg" alt="tweetCC targeted link" width="500" height="329" />

tweetCC uses an attribute selector to target links that have a title attribute ending in the words "tweetCC":

<pre><code class="language-css">a[title$="tweetCC"] { 
    position: absolute; 
    top: 0; 
    right: 0; 
    display: block; 
    width: 140px; 
    height: 140px; 
    text-indent: -9999px; 
    }</code></pre>

<strong>Browser support:</strong> The only browser that doesn't support CSS3 attribute selectors is IE6. Both IE7 and IE8, Opera and Webkit- and Gecko-based browsers do. So using them in your style sheet is definitely safe.</p>

### Combinators

The only new kind of combinator introduced in CSS3 is the general sibling selector. It targets all siblings of an element that have the same parent.

For example, to add a gray border to all images that are a sibling of a particular <code>div</code> (and both the <code>div</code> and the images should have the same parent), defining the following in your style sheet is enough:

<pre><code class="language-css">div~img {
	border: 1px solid #ccc;
	}</code></pre>

<strong>Browser support:</strong> All major browsers support the general sibling selector except our favorite: Internet Explorer 6.</p>

### Pseudo-Classes

Probably the most extensive new addition to CSS are new pseudo-classes. Here are some of the most interesting and useful ones:

*   `:nth-child(n)` Lets you target elements based on their positions in a parent's list of child elements. You can use a number, a number expression or the `odd` and `even` keywords (perfect for Zebra-style table rows). So, if you want to match a group of three elements after the forth element, you can simply use:

        name="code">:nth-child(3n+4) { background-color: #ccc; }

*   `:nth-last-child(n)` Follows the same idea as the previous selector, but matches the last children of a parent element. For example, to target the last two paragraphs in a `div`, we would use the following selector:

        name="code">div p:nth-last-child(-n+2)

*   `:last-child` Matches the last child of a parent, and is equivalent to

        name="code">:nth-last-child(1)

*   `:checked` Matches elements that are checked; for example, checked boxes.
*   `:empty` Matches elements that have no children or are empty.
*   `:not(s)` Matches all elements that do not match the specified declaration(s). For example, if we want to make all paragraphs that aren't of the class "lead" to appear black, we would write:

        name="code">p:not([class*="lead"]) { color: black; }

    .

On his website, <a href="https://andreagandino.com/">Andrea Gandino</a> uses the <code>:last-child</code> pseudo-selector to target the last paragraph of each blog post and apply a margin of 0 to it:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/308bbe93-b868-435e-9874-df8339674620/andrea.jpg" alt="Andrea Gandino uses the :last-child pseudo-element on his blog post paragraphs" width="500" height="337" />

<pre><code class="language-css">#primary .text p:last-child { 
    margin: 0; 
    }</code></pre>

<strong>Browser support:</strong> Webkit-based and Opera browsers support all new CSS3 pseudo-selectors. Firefox 2 and 3 (Gecko-based) only support <code>:not(s)</code>, <code>:last-child</code>, <code>:only-child</code>, <code>:root</code>, <code>:empty</code>, <code>:target</code>, <code>:checked</code>, <code>:enabled</code> and <code>:disabled</code>, but Firefox 3.5 will have wide support of CSS3 selectors. Trident-based browsers (Internet Explorer) have virtually no support of pseudo-selectors.</p>

### Pseudo-Elements

The only pseudo-element introduced in CSS3 is <code>::selection</code>. It lets you target elements that have been highlighted by the user.

<strong>Browser support:</strong> No current Internet Explorer or Firefox browsers support the <code>::selection</code> pseudo-element. Safari, Opera and Chrome do.</p>

### Useful Links

*   [Selectors Level 3: W3C Working Draft](https://www.w3.org/TR/css3-selectors/)
*   [CSS3: Attribute selectors: CSS3.info](https://www.css3.info/preview/attribute-selectors/)
*   [Compatibility table: CSS3 Selectors](https://www.css3.info/modules/selector-compat/)
*   [CSS selectors and pseudo selectors browser compatibility](https://kimblim.dk/css-tests/selectors/)
*   [CSS3 Attribute Selectors](https://reference.sitepoint.com/css/css3attributeselectors)
*   [::selection](https://reference.sitepoint.com/css/pseudoelement-selection)
*   [General Sibling Selector](https://reference.sitepoint.com/css/generalsiblingselector)
*   [CSS3 Pseudo-classes](https://reference.sitepoint.com/css/css3psuedoclasses)

## 2\. RGBA And Opacity

RGBA lets you specify not only the color but the <strong>opacity of an element</strong>. Some browsers still don't support it, so it's good practice to specify before the RGBa color another color without transparency that older browsers will understand.

<a href="https://timvandamme.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22d17acf-3193-4120-a951-61cda4905bf8/rgba.jpg" alt="Tim Van Damme's hover effects" width="500" height="337" /></a><br>
<em>Tim Van Damme uses RGBA colors on hover effects on links</em>

On his website, <a href="https://timvandamme.com/">Tim Van Damme</a> uses RGBA colors on hover effects; for example, on the network links on his home page:

<pre><code class="language-css">#networks li a:hover,
#networks li a:focus {
    background: rgba(164, 173, 183, .15);
    }</code></pre>

When setting an RGBA color, we must specify the red, blue and green values either with an integer value between 0 and 255 or with percentages. The alpha value should be between 0.0 and 1.0; for example, 0.5 for a 50% opacity.

The difference between RGBA and opacity is that the former applies transparency only to a particular element, whereas the latter affects the element we target and all of its children.

Here is an example of how we would add 80% opacity to a <code>div</code>:

<pre><code class="language-css">div { 
	opacity: 0.8; 
	}</code></pre>

<strong>Browser support:</strong> RGBA is supported by Webkit-based browsers. No Internet Explorer browser supports it. Firefox 2 does't support it either, but Firefox 3 does, as does Opera 9.5. Opacity is supported by Opera and Webkit- and Gecko-based browsers, but is not supported by either IE release.</p>

### Useful Links

*   [CSS Color Module Level 3: W3C Working Draft](https://www.w3.org/TR/css3-color/)
*   [RGBA colors: CSS3.info](https://www.css3.info/preview/rgba/)
*   [RGBa Browser Support](https://css-tricks.com/rgba-browser-support/)
*   [RGBA color space](https://en.wikipedia.org/wiki/RGBA_color_space)
*   [Is CSS3 RGBa ready to rock?](https://forabeautifulweb.com/blog/about/is_css3_rgba_ready_to_rock)
*   [Super-Awesome Buttons with CSS3 and RGBA](https://www.zurb.com/article/266/super-awesome-buttons-with-css3-and-rgba)

## 3\. Multi-Column Layout

This new CSS3 selector lets you achieve multi-column layouts without having to use multiple <code>div</code>s. The browser interprets the properties and create the columns, giving the text a newspaper-like flow.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/072e0aa9-b310-4eb8-8540-f0e750e3b870/css3-tweetcc.jpg" alt="tweetCC's home page" width="500" height="241" /><br>
<em>tweetCC uses CSS3 multi-column selector on its home page</em>

tweetCC displays introductory text in four columns on its home page. The four columns aren't floated <code>div</code>s; instead, the Web designer uses the CSS3 multi-column layout as follows:

<pre><code class="language-css">.index #content div { 
    -webkit-column-count : 4; 
    -webkit-column-gap : 20px; 
    -moz-column-count : 4; 
    -moz-column-gap : 20px; 
    }</code></pre>

We can define three things with this selector: the number of columns (<code>column-count</code>), the width of each column (<code>column-width</code>, not used in the example) and the gap between columns (<code>column-gap</code>). If <code>column-count</code> is not set, the browser accommodates as many columns that fit in the available width.

To add a vertical separator between columns, we can use the <code>column-rule</code> property, which functions pretty much as a border property:

<pre><code class="language-css">div {
    column-rule: 1px solid #00000;
    }</code></pre>

Browsers that don't support these properties render the content as simple text, as if there were no columns.

Related properties: <code>column-break-after</code>, <code>column-break-before</code>, <code>column-span</code>, <code>column-fill</code>.

<strong>Browser support:</strong> Multi-column layouts are supported by Safari 3 and 4 and Firefox 1.5+.</p>

### Useful Links

*   [CSS3 module: Multi-column layout: W3C Working Draft](https://www.w3.org/TR/css3-multicol/)
*   [Columns](https://www.quirksmode.org/css/multicolumn.html)
*   CSS3 - Multi-Column Layout Demonstration
*   [CSS3 Columns](https://developer.mozilla.org/en/CSS3_Columns)
*   [Designing tweetCC](https://forabeautifulweb.com/blog/about/designing_tweetcc/)
*   [Introduction to CSS3 - Part 5: Multiple Columns](https://designshack.co.uk/tutorials/introduction-to-css3-part-5-multiple-columns)

## 4\. Multiple Backgrounds

CSS3 lets you apply multiple layered backgrounds to an element using multiple properties such as <code>background-image</code>, <code>background-repeat</code>, <code>background-size</code>, <code>background-position</code>, <code>background-origin</code> and <code>background-clip</code>.

The easiest way to add multiple backgrounds to an element is to use the shorthand code. You can specify all of the above properties in a single declaration, but the most commonly used are image, position and repeat:

<pre><code class="language-css">div {
	background: url(example.jpg) top left no-repeat, 
		url(example2.jpg) bottom left no-repeat, 
		url(example3.jpg) center center repeat-y;
	}</code></pre>

The first image will be the one "closest" to the user.

A more complex version of the same property would be:

<pre><code class="language-css">div {
	background: url(example.jpg) top left (100% 2em) no-repeat, 
		url(example2.jpg) bottom left (100% 2em) no-repeat, 
		url(example3.jpg) center center (10em 10em) repeat-y;
	}</code></pre>

In this case, <code>(100% 2em)</code> is the <code>background-size</code> value; the background image in the top-left corner would stretch the full width of the <code>div</code> and be <code>2em</code> high.

Because very few browsers support it, and because not displaying backgrounds on a website can really impair a website's visual impact, this is not a widely used CSS3 property. However, it could greatly improve a Web designer's workflow and significantly reduce the amount of markup that would otherwise be needed to achieve the same effect.

<strong>Browser support:</strong> multiple backgrounds only work on Safari and Konqueror.</p>

### Useful Links

*   [Layering multiple background images](https://www.w3.org/TR/css3-background/#layering)
*   [Multiple backgrounds with CSS3 and CSS3.info](https://www.css3.info/preview/multiple-backgrounds/)
*   [Introduction to CSS3, Part 6: Backgrounds](https://designshack.co.uk/tutorials/introduction-to-css3-part-6-backgrounds)

## 5\. Word Wrap

The <code>word-wrap</code> property is used to <strong>prevent long words from overflowing</strong>. It can have one of two values: <code>normal</code> and <code>break-word</code>. The <code>normal</code> value (the default) breaks words only at allowed break points, like hyphens. If <code>break-word</code> is used, the word can be broken where needed to fit the given space and prevent overflowing.

<a href="https://wordpress.org"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b443fea-2396-46e3-b316-171836a4d2d9/css3-wordpress-admin-2.jpg" alt="WordPress admin area" width="500" height="201" /></a><br>
<em>The WordPress admin area uses <code>word-wrap</code> in data tables</em>.

In the <a href="https://wordpress.org">WordPress</a> admin area, the <code>word-wrap</code> property is used for elements in tables; for example, in lists on Posts and Pages:

<pre><code class="language-css">.widefat * {
    word-wrap: break-word;
    }</code></pre>

<strong>Browser support:</strong> <code>word-wrap</code> is supported by Internet Explorer and Safari. Firefox will support it in version 3.5.</p>

### Useful Links

*   [Force Wrapping: the 'word-wrap' property — CSS Text Level 3: W3C Working Draft](https://www.w3.org/TR/css3-text/#word-wrap)
*   [word-wrap: CSS3.info](https://www.css3.info/preview/word-wrap/)
*   <span class="removed_link" title="https://www.css3.com/css-word-wrap/">CSS word-wrap</span>
*   [word-wrap: Mozilla Developer Center](https://developer.mozilla.org/en/CSS/word-wrap)

## 6\. Text Shadow

Despite existing since CSS2, <code>text-shadow</code> is not a widely used CSS property. But it will very likely be widely adopted with CSS3. The property gives designers a new cross-browser tool to add dimension to designs and make text stand out.

You need to make sure, though, that the text in your design is readable in case the user's browser doesn't support advanced CSS3 properties. Give the text and background color enough contrast in case the <code>text-shadow</code> property isn't rendered or understood properly by the browser.

<a href="https://beakapp.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/921e88c5-24a7-41b5-b21d-bf11d46acfe9/beak.gif" alt="Beak uses the text-shadow-property of CSS 3" width="498" height="270" /></a><br>
<em>Beakapp uses the <code>text-shadow</code> property on its website: for the content area</em>.

<a href="https://beakapp.com/">BeakApp.com</a> uses the <code>text-shadow</code> property for the content area, <strong>adding depth and dimension to the text</strong> and making it stand out without the use of an image replacement technique. This property is visible only in Safari and Google Chrome.

The CSS for the website's main navigation shows the following:

<pre><code class="language-css">.signup_area p {
	text-shadow: rgba(0,0,0,.8) 0 1px 0;
}</code></pre>

Here, we have the shadow color (using RGBA, see above), followed by the right (x coordinate) and bottom (y coordinate) offset, and finally the blur radius.

To apply multiple shadows to a text, separate the shadows with a comma. For example:

<pre><code class="language-css">p {
    text-shadow: red 4px 4px 2px, 
		yellow -4px -4px 2px, 
		green -4px 4px 2px;
    }</code></pre>

<strong>Browser support:</strong> Webkit-based browsers and Opera 9.5 support <code>text-shadow</code>. Internet Explorer doesn't support it, and Firefox will only support it in version 3.5.</p>

### Useful Links

*   [Text Shadows: the 'text-shadow' property — W3C Working Draft](https://www.w3.org/TR/css3-text/#text-shadow)
*   [Text shadows: Web Style Sheets CSS tips and tricks](https://www.w3.org/Style/Examples/007/text-shadow)
*   [Text-shadow, Photoshop like effects using CSS — CSS3.info](https://www.css3.info/preview/text-shadow/)
*   [Make Cool And Clever Text Effects With CSS Text-Shadow](https://www.kremalicious.com/2008/04/make-cool-and-clever-text-effects-with-css-text-shadow/)
*   [Safari's Text-Shadow Anti-Aliasing CSS Hack](https://sam.brown.tc/entry/348/safaris-text-shadow-anti-aliasing-css-hack)
*   [text-shadow](https://reference.sitepoint.com/css/text-shadow)
*   [text-shadow: Mozilla Developer Center](https://developer.mozilla.org/en/CSS/text-shadow)

## 7\. @font-face-Attribute

Despite being <strong>one of the most highly anticipated CSS3 features</strong> (even though it's been around since CSS2), <code>@font-face</code> is still not as widely adopted on the Web as other CSS3 properties. This is due mainly to font licensing and copyright issues: embedded fonts are easily downloaded from the Web, a major concern to type foundries.

However, a solution to the licensing issues seems to be on the way. <a href="https://blog.typekit.com/2009/05/27/introducing-typekit/">TypeKit</a> promises to come up with a solution that would make it easier for designers and type foundries to agree on licensing issues that would significantly enrich the typography in Web design and make the <code>@font-face</code> attribute usable in practice.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/945353af-ac6a-4f85-ac90-d880e2fb1ac8/css3-mozillajetpack.jpg" alt="Mozilla Labs JetPack font" width="500" height="397" /><br>
<em>Mozilla Labs JetPack website resorts to the <code>font-face</code> rule to use the DroidSans typeface</em>

One of the few websites that use the property is the new JetPack MozillaLabs.

<pre><code class="language-css">@font-face{
    font-family: 'DroidSans'; 
    src: url('../fonts/DroidSans.ttf') format('truetype');
    }</code></pre>

To use embedded fonts on your websites, you have to declare each style separately (for example, <em>normal</em>, <em>bold</em> and <em>italic</em>). Make sure to only use fonts that have been licensed for such use on the Web and to give the designer credit when required.

After the <code>@font-face</code> rule, you can call the font with a normal <code>font-family</code> property in your style sheet:

<pre><code class="language-css">p {
    font-family: "DroidSans";
    }</code></pre>

If a browser doesn't support <code>@font-face</code>, it will revert to the next font specified in the <code>font-family</code> property (CSS font stacks). This may be okay for some websites, if the <code>@font-face</code> font is a luxury for supported browsers; but if the font plays a major role in the design or is a key part of the visual identity of the company, you will probably want to use another solution, such as sIFR or <a href="https://wiki.github.com/sorccu/cufon/about">Cufón</a>. Bear in mind, though, that these tools are more appropriate for headings and short passages of text, and copying and pasting this kind of content is difficult and not user-friendly.

<a href="https://mezzoblue.com/archives/2009/05/07/font_embeddi/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c3cd457-b99f-43db-82c2-20b94a5e05f7/font-embedding.gif" alt="Font embedding on MezzoBlue.com" width="500" height="337" /></a><br>
<em>Wouldn't it be nice to have such type for body copy on the Web? Dave Shea experiments with <a href="https://wiki.github.com/sorccu/cufon/about">Cufón</a> and <a href="https://www.josbuivenga.demon.nl/museosans.html">Museo Sans</a>. Beautiful!</em>

<strong>Browser support:</strong> <code>@font-face</code> is supported by Safari 3.1+. Internet Explorer supports it if <abbr title="Embedded OpenType">EOT</abbr> fonts are used. Opera 10 and Firefox 3.5 should support it.</p>

### Useful Links

*   [Font Descriptions and @font-face — W3C Working Draft](https://www.w3.org/TR/css3-webfonts/#font-descriptions)
*   [Web fonts with @font-face](https://www.css3.info/preview/web-fonts-with-font-face/)
*   [@font-face — Sitepoint](https://reference.sitepoint.com/css/at-fontface)
*   Fonts available for @font-face embedding
*   [@font-face](https://nickcowie.com/2008/font-face/)
*   [beautiful fonts with @font-face](https://hacks.mozilla.org/2009/06/beautiful-fonts-with-font-face/)
*   [Introducing Typekit](https://blog.typekit.com/2009/05/27/introducing-typekit/)

## 8\. Border Radius

Border-radius <strong>adds curved corners to HTML elements</strong> without background images. Currently, it is probably the most widely used CSS3 property for the simple reason that rounded corners are just nice to have and aren't critical to design or usability.

Instead of adding cryptic JavaScript or unnecessary HTML markup, just add a couple of extra properties in CSS and hope for the best. The solution is cleaner and more efficient and can save you from having to spend a couple of hours finding clever browser workarounds for CSS and JavaScript-based rounded corners.

<a href="https://sam.brown.tc/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6636d8bc-f2d5-49f2-923f-6c1c0d781f08/css3-sambrown.jpg" alt="Sam Brown's blog categories" width="500" height="106" /></a><br>
<em>Sam Brown's blog using <code>border-radius</code> on headings, categories and links</em>.

On his website, <a href="https://sam.brown.tc/">Sam Brown</a> uses the <code>border-radius</code> property heavily on headings, links and <code>div</code>s. Achieving this effect with images would be time-consuming. This is one of the reasons why using CSS3 properties in our projects is such an <strong>important step towards efficiency in Web development</strong>.

To add rounded corners to category links, Sam uses the following CSS snippet:

<pre><code class="language-css">h2 span { 
	color: #1a1a1a; 
	padding: .5em; 
	-webkit-border-radius: 6px; 
	-moz-border-radius: 6px; 
	}</code></pre>

We can go one step further and add the original CSS3 property and Konqueror proprietary extension, making it:

<pre><code class="language-css">h2 span {
    color: #1a1a1a;
    padding: .5em; 
    -webkit-border-radius: 6px; 
    -moz-border-radius: 6px; 
    -khtml-border-radius: 6px; 
    border-radius: 6px; 
    }</code></pre>

If we want to apply the property to certain corners of our element, we can target each corner separately:

<pre><code class="language-css">div {	
    -moz-border-radius-topright: 6px;
    -moz-border-radius-topleft: 6px;
    -moz-border-radius-bottomright: 6px;
    -moz-border-radius-bottomleft: 6px;
    -webkit-border-top-right-radius: 6px;
    -webkit-border-top-left-radius: 6px;
    -webkit-border-bottom-right-radius: 6px;
    -webkit-border-bottom-left-radius: 6px;
    border-top-right-radius: 6px;
    border-top-left-radius: 6px;
    border-bottom-right-radius: 6px;
    border-bottom-left-radius: 6px;
    }</code></pre>

<strong>Browser support:</strong> <code>border-radius</code> is supported by Webkit- and Gecko-based browsers but not by any version of Internet Explorer or Opera.</p>

### Useful Links

*   [border-radius: W3C Working Draft](https://www.w3.org/TR/css3-background/#border-radius)
*   [Border-radius: create rounded corners with CSS! — CSS3.info](https://www.css3.info/preview/rounded-border/)
*   [Introduction to CSS3, Part 2: Borders](https://designshack.co.uk/tutorials/introduction-to-css3-part-2-borders)
*   [An Ode to border-radius](https://webdesignernotebook.com/css/an-ode-to-border-radius/)
*   CSS3 Border-Radius and Rounded Corners

## 9\. Border Image

The <code>border-image</code> property allows you to <strong>specify an image for the border of an element</strong>, freeing you from the usual <code>solid</code>, <code>dotted</code> and other border styles. This property gives designers a better tool with which to consistently style the borders of design elements, being better than the <code>background-image</code> property (for advanced designs) or rigid default border styles. We can also explicitly define how a border should be scaled or tiled.

<a href="https://www.blog.spoongraphics.co.uk/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2c171d7-6c93-489c-97a4-ac0a7d3cce7c/css3-spoongraphics.jpg" alt="SpoonGraphics blog's border-image" width="500" height="171" /></a><br>
<em>The SpoonGraphics blog uses the <code>border-image</code> property for its images borders</em>

On the <a href="https://www.blog.spoongraphics.co.uk/">SpoonGraphis blog</a>, <code>border-image</code> is used for the images borders as follows:

<pre><code class="language-css">#content .post img {
    border: 6px solid #f2e6d1;
    -webkit-border-image: url(main-border.png) 6 repeat;
    -moz-border-image: url(main-border.png) 6 repeat;
    border-image: url(main-border.png) 6 repeat;
    }</code></pre>

To define the <code>border-image</code>, we must specify the image location, which part of the image should be cropped and used for each side of the element and how the image should be scaled and tiled.

To create a <code>div</code> that uses the image below as its border, we would use the following code (we will add in the Opera and Konqueror extensions for this example):

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2378b4e4-67aa-40b1-831c-8acebdaa40ab/border-image.gif" alt="Image used as border-image" width="361" height="240" />

<pre><code class="language-css">div {
    border-width: 18px 25px 25px 18px;
    -webkit-border-image: url(example.png) 18 25 25 18 stretch stretch;
    -moz-border-image: url(example.png) 18 25 25 18 stretch stretch;
    -o-border-image: url(example.png) 18 25 25 18 stretch stretch;
    -khtml-border-image: url(example.png) 18 25 25 18 stretch stretch;
    border-image: url(example.png) 18 25 25 18 stretch stretch;
	}</code></pre>

The last value of this property can be <code>stretch</code> (default), <code>round</code> (only a whole number of repeated images will fit the space allowed) or <code>repeat</code>. In our example, the top, bottom, left and right border images are stretched. If we want only the top and bottom sides to stretch, we would use this CSS:

<pre><code class="language-css">div {
    (...)
    border-image: url(example.png) 18 25 25 18 stretch repeat;
	}</code></pre>

We can also target each corner separately if we want to use a different image for each:

<pre><code class="language-css">div {
    border-top-image: url(example.png) 5 5 stretch;
    border-right-image: url(example.png) 5 5 stretch;
    border-bottom-image: url(example.png) 5 5 stretch;
    border-left-image: url(example.png) 5 5 stretch;
    border-top-left-image: url(example.png) 5 5 stretch;
    border-top-right-image: url(example.png) 5 5 stretch;
    border-bottom-left-image: url(example.png) 5 5 stretch;
    border-bottom-right-image: url(example.png) 5 5 stretch;
    }</code></pre>

If a browser doesn't support the <code>border-image</code> property, it will ignore it and only apply the other defined border properties, such as <code>border-width</code> and <code>border-color</code>.

<strong>Browser support:</strong> <code>border-image</code> is currently only supported by Webkit-based browsers. Support in the next release of Firefox is not certain.</p>

### Useful Links

*   [The ‘border-image’ property: W3C Working Draft](https://www.w3.org/TR/css3-background/#the-border-image)
*   [Border-image: using images for your border — CSS3.info](https://www.css3.info/preview/border-image/)
*   [border-image in Firefox](https://ejohn.org/blog/border-image-in-firefox/)
*   border-image demonstration page
*   Replicating iPhone Buttons the "webkit" way!

## 10\. Box Shadow

The <code>box-shadow</code> property <strong>adds shadows to HTML elements</strong> without extra markup or background images. Like the <code>text-shadow</code> property, it enhances the detail of a design; and because it doesn't really affect the readability of content, it could be a good way to add that extra touch.

<a href="https://10to1.be/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4a06d8e-0d2d-4bca-a574-485f95b4ea45/css3-10to1.jpg" alt="10to1 navigation" width="500" height="127" /></a><br>
<em>10to1 uses the <code>box-shadow</code> property for its navigation background and hover states</em>.

<a href="https://10to1.be/">10to1</a> adds a simple shadow to its navigation area and uses the property for a hover effect on the navigation links:

<pre><code class="language-css">#navigation {
	-webkit-box-shadow: 0 0 10px #000;
	-moz-box-shadow: 0 0 10px #000;
	}
	#navigation li a:hover,
	#navigation li a:focus {
	-webkit-box-shadow: 0 0 5px #111;
	-moz-box-shadow: 0 0 5px #111;
	}</code></pre>

The <code>box-shadow</code> property can have multiple values: horizontal offset, vertical offset, blur radius, spread radius and shadow color. Horizontal and vertical offset and shadow color are the most commonly used.

To apply a red shadow positioned four pixels to the right and bottom of a <code>div</code>, with no blur, we would need the following code:

<pre><code class="language-css">div {
    -moz-box-shadow: 4px 4px 0 #f00;
    -webkit-box-shadow: 4px 4px 0 #f00;
    box-shadow: 4px 4px 0 #f00;
    }</code></pre>

<strong>Browser support:</strong> <code>box-shadow</code> is currently supported only by Webkit-based browsers, but the upcoming Firefox 3.5 will very likely support it as well.</p>

### Useful Links

*   [The ‘box-shadow’ property — W3C Working Draft](https://www.w3.org/TR/css3-background/#the-box-shadow)
*   [Box-shadow, one of CSS3’s best new features — CSS3.info](https://www.css3.info/preview/box-shadow/)
*   [Box Shadow — Surfin’ Safari blog](https://webkit.org/blog/86/box-shadow/)

## 11\. Box Sizing

According to CSS 2.1 specifications, when calculating the overall dimensions of a box, the borders and padding of the element should be added to the width and height. But legacy browsers are well known for interpreting this specification in their own and quite creative ways. The <code>box-sizing</code> property lets you specify <strong>how the browser calculates the width and height of an element</strong>.

<a href="https://wordpress.org"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47228a18-d48b-4129-8212-be2f1fd8e91b/css3-wordpress-admin.jpg" alt="WordPress input and textarea tags" width="500" height="263" /></a><br>
<em>WordPress uses the <code>border-box</code> property in all input fields (text type) and text area elements in the admin panel</em>.

The <a href="https://wordpress.org">WordPress</a> admin area demonstrates this property in all its <code>input</code> tags with a text type and <code>textarea</code> tags (among other elements):

<pre><code class="language-css">input[type="text"],
	textarea {
	-moz-box-sizing: border-box;
	-webkit-box-sizing: border-box;
	-ms-box-sizing: border-box;
	box-sizing: border-box;
	}</code></pre>

The third property (<code>-ms-box-sizing</code>) only works in Internet Explorer 8. With other selectors, the WordPress style sheet also adds the Konqueror property: <code>-khtml-box-sizing</code>.

The <code>box-sizing</code> property can have one of two values: <code>border-box</code> and <code>content-box</code>. Content-box renders the width as specified in CSS 2.1. Border-box subtracts the padding and border from the specified width and height (as done by legacy browsers).

<strong>Browser support:</strong> <code>box-sizing</code> is supported by IE8, Opera and Gecko- and Webkit-based browsers.</p>

### Useful Links

*   ['box-sizing' property: W3C Candidate Recommendation](https://www.w3.org/TR/css3-ui/#box-sizing)
*   [Box-sizing, box-model fixes for the simple people: CSS3.info](https://www.css3.info/preview/box-sizing/)
*   [CSS3 box-sizing attribute](https://helephant.com/2008/10/css3-box-sizing-attribute/)

## 12\. Media Queries

Media queries let you define different styles for different devices based on their capabilities. For example, you may want your website's sidebar to appear under the main content when viewed on devices with a viewport narrower than 480 pixels, in which case it shouldn't be floated and displayed on the right side:

<pre><code class="language-css">#sidebar {
	float: right;
	display: inline; /* IE Double-Margin Bugfix */
	}

@media all and (max-width:480px) {
	#sidebar {
		float: none;
		clear: both;
		}
	}</code></pre>

You can also target devices with color screens:

<pre><code class="language-css">a {
	color: grey;
	}

@media screen and (color) {
	a {
		color: red;
		}
	}</code></pre>

The possibilities are endless. This property is useful because you no longer have to write separate style sheets for different devices, nor do you have to use JavaScript to determine the capabilities and properties of each user's browser. A more popular JavaScript-based solution to achieve a flexible layout would be to use an <a href="https://www.smashingmagazine.com/2009/06/09/smart-fixes-for-fluid-layouts/">adaptive fluid layout</a>, making the layout more responsive to the user's browser resolution.

<strong>Browser support:</strong> Media queries are supported by Webkit-based browsers and Opera. Firefox plans to support them in version 3.5. Internet Explorer currently doesn't support them and doesn't plan to support them in upcoming versions.</p>

### Useful Links

*   [Media Queries: W3C Candidate Recommendation](https://www.w3.org/TR/css3-mediaqueries/)
*   [Media Queries: CSS3.info](https://www.css3.info/preview/media-queries/)
*   [The bleeding edge of web: media queries](https://helephant.com/2008/07/the-bleeding-edge-of-web-media-queries/)
*   [Media types](https://www.howtocreate.co.uk/tutorials/css/mediatypes)

## 13\. Speech

The speech module in CSS3 lets you <strong>specify the speech style of screen readers</strong>. You can control various aspects of the speech, such as:

*   `voice-volume` Set a volume using a number from 0 to 100 (0 being silence), percentages or a keyword (`silent`, `x-soft`, `soft`, `medium`, `loud` and `x-loud`).
*   `voice-balance` Control which channel sound comes from (if the user's sound system supports stereo).
*   Speak Instruct the screen reader to spell out particular words, digits or punctuation. Available keywords are `none`, `normal`, `spell-out`, `digits`, `literal-punctuation`, `no-punctuation` and `inherit`.
*   Pauses and rests Set a pause or rest before or after an element's content is spoken. You can use either time units (for example, "2s" for 2 seconds) or keywords (`none`, `x-weak`, `weak`, `medium`, `strong` and `x-strong`).
*   Cues Use sounds to delimit particular elements and control their volume.
*   `voice-family` Set specific types of voices and voice combinations (as you do with fonts).
*   `voice-rate` Control the speed at which elements are spoken. This can be defined as a percentage or keyword: `x-slow`, `slow`, `medium`, `fast` and `x-fast`.
*   `voice-stress` Indicate any emphasis that should be applied, using different keywords: `none`, `moderate`, `strong` and `reduced`.

For example, to tell a screen reader to read all <code>h2</code> tags in a female voice, from the left speaker, in a soft tone and followed by a particular sound, set the CSS as follows:

<pre><code class="language-css">h2 {
	voice-family: female;
	voice-balance: left;
	voice-volume: soft;
	cue-after: url(sound.au);
	}</code></pre>

Unfortunately, this property has very little support now but is definitely worth keeping in mind so that we might improve the accessibility of our websites in future.

<strong>Browser support:</strong> Currently, only Opera browsers for Windows XP and 2000 support some of the speech module properties. To use them, use the <code>-xv-</code> prefix; for example, <code>-xv-voice-balance: right</code>.</p>

### Useful Links

*   [CSS3 Speech Module — W3C Working Draft](https://www.w3.org/TR/css3-speech/)
*   [CSS3 Speech — CSS3.info](https://www.css3.info/preview/speech/)
*   [Aural CSS: Support for CSS 2 Aural Style Sheets / CSS 3 Speech Module](https://lab.dotjay.co.uk/notes/css/aural-speech/)

## Conclusion

<strong>CSS3 properties can greatly improve your workflow</strong>, making some of the most time-consuming CSS tasks a breeze and allowing for better, cleaner and more lightweight markup. Some properties are still not widely supported, even by the most recent browsers, but that doesn't mean we shouldn't experiment with them or give visitors with modern browsers advanced features and CSS styling.

In this regard, keep in mind that <strong>educating our clients</strong> is both useful and necessary: websites don't have to look exactly the same in every browser, and if a difference doesn't negatively affect the aesthetics or usability of a website, it should be considered. If we continue to waste valuable time and money making every detail pixel-perfect (instead of adopting more flexible and future-oriented solutions), users won't have an incentive to upgrade their browsers, in which case we would have to wait a long time before older browsers become legacy browsers and robust modern browsers become the standard.

The earlier we experiment with and adapt new CSS3 properties, the earlier they will be supported by popular browsers and the earlier we'll be able to use them widely.</p>

## Further Reading And References

- [Responsively Retrofitting An Existing Site With RWD Retrofit](https://www.smashingmagazine.com/2013/03/18/retrofit-a-website-to-be-responsive-with-rwd-retrofit/)
- [The State Of Responsive Web Design](https://www.smashingmagazine.com/2013/05/the-state-of-responsive-web-design/)
- [Design Process In The Responsive Age](https://www.smashingmagazine.com/2012/05/design-process-responsive-age/)

{{< signature "al" >}}


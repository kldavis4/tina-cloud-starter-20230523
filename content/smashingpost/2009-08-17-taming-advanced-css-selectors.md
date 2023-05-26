---
title: Taming Advanced CSS Selectors
slug: taming-advanced-css-selectors
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb86f3cb-359e-40b2-bd88-0f0ec5a7b1a5/redesign-the-web.png
date: 2009-08-17T09:50:03.000Z
author: inayaili-de-leon
summary: >-
  CSS is one of the most powerful tools that is available to web designers (if not the most powerful). With it, we can completely transform the look of a website in just a couple of minutes &mdash; without even having to touch the markup. But despite the fact that we are all well aware of its usefulness, CSS selectors are still not used to their full potential and we sometimes have the tendency to litter our HTML with excessive and unnecessary classes and ids, divs and spans.
description: >-
  CSS is one of the most powerful tools that is available to web designers. With it, we can completely transform the look of a website in just a couple of minutes &mdash; without even having to touch the markup.
categories:
  - Coding
  - CSS
---

The best way to avoid these plagues spreading in your markup and keep it clean and semantic, is by using more complex CSS selectors, ones that can target specific elements without the need of a class or an id, and by doing that <strong>keep our code and our stylesheets flexible</strong>.

## CSS Specificity

Before delving into the realms of advanced CSS selectors, it's important to understand how CSS specificity works, so that we know how to properly use our selectors and to avoid us spending hours debugging for a CSS issue that could be easily fixed if we had only payed attention to the specificity.

{{% feature-panel %}}

When we are writing our CSS we have to keep in mind that <strong>some selectors will rank higher</strong> than others in the cascade, the latest selector that we wrote will not always override the previous ones that we wrote for the same elements.

So how do you <strong>calculate the specificity</strong> of a particular selector? It's fairly straightforward if you take into account that specificity will be represented as four numbers separated by commas, like: 1, 1, 1, 1 or 0, 2, 0, 1

1.  The first digit (a) is always zero, unless there is a style attribute applied to that element within the markup itself
2.  The second digit (b) is the sum of the number of IDs in that selector
3.  The third digit (c) is the sum of other attribute selectors and pseudo-classes in that selector. Classes (`.example`) and attribute selectors (eg. `li[id=red])` are included here.
4.  The fourth digit (d) counts the elements (like `table`, `p`, `div`, etc.) and pseudo-elements (like `:first-line`)
5.  The universal selector (*) has a specificity of zero
6.  If two selectors have the same specificity, the one that comes last on the stylesheet will be applied

Let's take a look at a few examples, to make it easier to understand:

*   `#sidebar h2` — 0, 1, 0, 1
*   `h2.title` — 0, 0, 1, 1
*   `h2 + p` — 0, 0, 0, 2
*   `#sidebar p:first-line` — 0, 1, 0, 2

From the following selectors, the first one is the one who will be applied to the element, because it has the higher specificity:

*   `#sidebar p#first { color: red; }` — 0, 2, 0, 1
*   `#sidebar p:first-line { color: blue; }` — 0, 1, 0, 2

It's important to have at least a basic understanding of how specificity works, but tools like <strong>Firebug</strong> are useful to let us know which selector is being applied to a particular element by listing all the CSS selectors in order of their specificity when you are inspecting an element.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efbd0baf-068f-489f-a282-4c0f71f4fb2d/firebug.jpg" alt="css selectors" width="535" height="256" /><br>
<em>Firebug lets you easily see which selector is being applied to an element.</em>

Useful links:

*   [CSS Specificity: Things You Should Know](https://www.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/)
*   [Link Specificity¯MeyerWeb](https://meyerweb.com/eric/css/link-specificity.html)
*   [CSS: Specificity Wars](https://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html)
*   [Assigning property values, Cascading, and Inheritance—W3C](https://www.w3.org/TR/CSS2/cascade.html)

{{% feature-panel %}}

## 1\. Attribute selectors

Attribute selectors let you target an element based on its attributes. You can specify the element's attribute only, so all the elements that <em>have</em> that attribute — whatever the value — within the HTML will be targeted, or be more specific and <strong>target elements that have particular values on their attributes</strong> — and this is where attribute selectors show their power.

There are 6 different types of attribute selectors:

*   `[att=value]`  
The attribute has to have the exact value specified.
*   `[att~=value]`  
The attribute's value needs to be a whitespace separated list of words (for example, class="title featured home"), and one of the words is exactly the specified value.
*   `[att|=value]`  
The attribute's value is exactly "value" or starts with the word "value" and is immediately followed by "-", so it would be "value-".
*   `[att^=value]`  
The attribute's value starts with the specified value.
*   `[att$=value]`  
The attribute's value ends with the specified value.
*   `[att*=value]`  
The attribute's value contains the specified value.

For example, if you want to <strong>change the background color of all the div elements that are posts</strong> on your blog, you can use the attribute selector that targets every <code>div</code> whose <code>class</code> attribute starts with "post":

<pre><code class="language-css">div[class*="post"] {
  background-color: #333;
  }</code></pre>

This will match all the <code>div</code> elements whose class attribute contains the words "post" in any position.

Another useful usage of attribute selectors is to <strong>target different types of <code>input</code> elements</strong>. For example, if you want your text inputs to have a different width from the others, you can use a simple attribute selector:

<pre><code class="language-css">input[type="text"] {
  width: 200px;
  }</code></pre>

This will target all the <code>input</code> elements whose <code>type</code> attribute is exactly "text".

Now let's say you want to <strong>add a different icon next to each different type of file</strong> your website is linking to, so your website's visitors know when they'll get an image, a PDF file, a Word document, etc. This can be done by using an attribute selector:

<pre><code class="language-css">a[href$=".jpg"] {
  background: url(jpeg.gif) no-repeat left 50%;
  padding: 2px 0 2px 20px;
  }

a[href$=".pdf"] {
  background: url(pdf.gif) no-repeat left 50%;
  padding: 2px 0 2px 20px;
  }

a[href$=".doc"] {
  background: url(word.gif) no-repeat left 50%;
  padding: 2px 0 2px 20px;
  }</code></pre>

In this example, we've used an attribute selector that will target all the links (<code>a</code>) whose <code>href</code> attribute ends (<code>$</code>) with .jpg, .pdf or .doc.

<strong>Notes on browser support</strong>
Apart from Internet Explorer 6, all major browsers support attribute selectors. This means that when you are using attribute selectors on your stylesheets, you should <strong>make sure that IE6 users will still be provided with a usable site</strong>. Take our third example: adding an icon to your links adds another level of usability to your site, but the site will still be usable if the links don't show any icons.

{{% ad-panel-leaderboard %}}

## 2\. Child selector

The child selector is represented by the sign "&gt;". It allows you to <strong>target elements that are direct children of a particular element</strong>.

For example, if you want to match all the <code>h2</code> elements that are a direct child of your sidebar <code>div</code>, but not the <code>h2</code> elements that may be also within the <code>div</code>, but that are grandchildren (or later descendants) of your element, you can use this selector:

<pre><code class="language-css">div#sidebar &gt; h2 {
  font-size: 20px;
  }</code></pre>

You can also use both child and descendant selectors combined. For example, if you want to target only the <code>blockquote</code> elements that are within divs that are direct grandchildren of the <code>body</code> element (you may want to match blockquotes inside the main content <code>div</code>, but not if they are outside it):

<pre><code class="language-css">body &gt; div &gt; div blockquote {
  margin-left: 30px;
  }</code></pre>

<strong>Notes on browser support</strong>
Like the attribute selectors, the child selector is not supported by Internet Explorer 6. If the effect you are trying to achieve by using it is crucial for the website's usability or overall aesthetics, you can consider using a class selector with it, or on a IE-only stylesheet, but that would detract from the purpose of using child selectors.</p>

## 3\. Sibling combinators

There are two types of sibling combinators: adjancent sibling combinators and general sibling combinators.</p>

### Adjacent sibling combinator

This selector uses the plus sign, "+", to combine two sequences of simple selectors. The elements in the selector have <strong>the same parent</strong>, and <strong>the second one must come immediately after the first</strong>.

The adjacent sibling combinator can be very useful, for example, when <strong>dealing with text</strong>. Lets say you want to add a top margin to all the <code>h2</code> tags that follow a paragraph (you don’t need to add a top margin if the heading comes after an <code>h1</code> tag or if it’s the first element on that page):

<pre><code class="language-css">p + h2 {
  margin-top: 10px;
  }</code></pre>

You can be even more specific and say that you only want this rule applied if the elements are within a particular <code>div</code>:

<pre><code class="language-css">div.post p + h2 {
  margin-top: 10px;
  }</code></pre>

Or you can add another level of complexity: say you want the first line of the paragraphs of every page to be in small caps.

<pre><code class="language-css">.post h1 + p:first-line {
  font-variant: small-caps;
  }</code></pre>

Because you know that the first paragraph of every post immediately follows an <code>h1</code> tag, you can refer to the <code>h1</code> on your selector.</p>

### General sibling combinator

The general sibling combinator works pretty much the same as the adjacent sibling combinator, but with the difference that <strong>the second selector doesn’t have to immediately follow the first one</strong>.

So if you need to target all the <code>p</code> tags that are within a particular <code>div</code> and that follow the <code>h1</code> tag (you may want those <code>p</code> tags to be larger than the ones that come before the title of your post), you can use this selector:

<pre><code class="language-css">.post h1 ~ p {
  font-size: 13px;
  }</code></pre>

<strong>Notes on browser support</strong>
Internet Explorer 6 doesn’t understand sibling combinators, but, as for the other cases, if your audience includes a small percentage of IE6 users, and if the website’s layout isn’t broken or severely affected by its lack of support, this is a much easier way of achieving lots of cool effects without the need of cluttering your HTML with useless classes and ids.</p>

{{% ad-panel-leaderboard %}}

## 4\. Pseudo-Classes

### Dynamic pseudo-classes

These are called dynamic pseudo-classes because they actually do not exist within the HTML: they are only present <strong>when the user is or has interacted</strong> with the website.

There are two types of dynamic pseudo-classes: <strong>link</strong> and <strong>user action</strong> ones. The link are <code>:link</code> and <code>:visited</code>, while the user action ones are <code>:hover</code>, <code>:active</code> and <code>:focus</code>.

From all the CSS selectors mentioned in this post, these will probably be <strong>the ones that are most commonly used</strong>.

The <strong><code>:link</code></strong> pseudo-class applies to links that haven’t been visited by the user, while the <strong><code>:visited</code></strong> pseudo-class applies to links that have been visited, so they are mutually exclusive.

The <strong><code>:hover</code></strong> pseudo-class applies when the user moves the cursor over the element, without having to activate or click on it. The <strong><code>:active</code></strong> pseudo-class applies when the user actually clicks on the element. And finally the <strong><code>:focus</code></strong> pseudo-class applies when that element is on focus — the most common application is on form elements.

You can use more than one user action dynamic pseudo-class in your stylesheets, so you can have, for example, a different background color for an input field depending on whether the user’s cursor is only hovering over it or hovering over it while in focus:

<pre><code class="language-css">input:focus {
  background: #D2D2D2;
  border: 1px solid #5E5E5E;
  }

input:focus:hover {
  background: #C7C7C7;
  }</code></pre>

<strong>Notes on browser support</strong>
The dynamic pseudo-classes are supported by all modern browsers, even IE6. But bear in mind that IE6 only allows the <code>:hover</code> pseudo-class to be applied to link elements (<code>a</code>) and only IE8 accepts the <code>:active</code> state on elements other than links.</p>

### :first-child

The <code>:first-child</code> pseudo-class allows you to target an element that is <strong>the first child of another element</strong>. For example, if you want to add a top margin to the first <code>li</code> element of your unordered lists, you can have this:

<pre><code class="language-css">ul &gt; li:first-child {
  margin-top: 10px;
  }</code></pre>

Let’s take another example: you want all your <code>h2</code> tags in your sidebar to have a top margin, to separate them from whatever comes before them, but the first one doesn’t need a margin. You can use the following code:

<pre><code class="language-css">#sidebar &gt; h2 {
  margin-top: 10px;
  }

#sidebar &gt; h2:first-child {
  margin-top: 0;
  }</code></pre>

<strong>Notes on browser support</strong>
IE6 doesn’t support the <code>:first-child</code> pseudo-class. Depending on the design that the pseudo-class is being applied to, it may not be a major cause for concern. For example, if you are using the <code>:first-child</code> selector to remove top or bottom margins from headings or paragraphs, your layout will probably not break in IE6, it will only look sightly different. But if you are using the <code>:first-child</code> selector to remove left and right margins from, for example, a floated sequence of divs, that may cause more disruption to your designs.</p>

### The language pseudo-class

The language pseudo-class, <strong><code>:lang()</code></strong>, allows you to match an element based on its language.

For example, lets say you want a specific link on your site to have a different background color, depending on that page’s language:

<pre><code class="language-css">:lang(en) &gt; a#flag {
  background-image: url(english.gif);
  }

:lang(fr) &gt; a#flag {
  background-image: url(french.gif);
  }</code></pre>

The selectors will match that particular link if the page’s language is either equal to “en” or “fr” or if it starts with “en” or “fr” and is immediately followed by an “-”.

<strong>Notes on browser support</strong>
Not surprisingly, the only version of Internet Explorer that supports this selector is 8. All other major browsers support the language pseudo-selector.</p>

## 5\. CSS 3 Pseudo-classes

### :target

When you’re <strong>using links with fragment identifiers</strong> (for example, <code>https://www.smashingmagazine.com/2009/08/02/bauhaus-ninety-years-of-inspiration/#comments</code>, where “#comments” is the fragment identifier), you can style the target by using the <code>:target</code> pseudo-class.

For example, lets imagine you have a long page with lots of text and <code>h2</code> headings, and there is an index of those headings at the top of the page. It will be much easier for the user if, when clicking on a particular link within the index, that heading would become highlighted in some way, when the page scrolls down. Easy:

<pre><code class="language-css">h2:target {
  background: #F2EBD6;
  }</code></pre>

<strong>Notes on browser support</strong>
This time, Internet Explorer is really annoying and has no support at all for the <code>:target</code> pseudo-class. Another glitch is that Opera doesn’t support this selector when using the back and forward buttons. Other than that, it has support from the other major browsers.</p>

### The UI element states pseudo-classes

Some HTML elements have an enable or disabled state (for example, input fields) and checked or unchecked states (radio buttons and checkboxes). These states can be targeted by the <strong><code>:enabled</code></strong>, <strong><code>:disabled</code></strong> or <strong><code>:checked</code></strong> pseudo-classes, respectively.

So you can say that any <code>input</code> that is disabled should have a light grey background and dotted border:

<pre><code class="language-css">input:disabled {
  border:1px dotted #999;
  background:#F2F2F2;
  }</code></pre>

You can also say that all checkboxes that are checked should have a left margin (to be easily seen within a long list of checkboxes):

<pre><code class="language-css">input[type=”checkbox”]:checked {
  margin-left: 15px;
  }</code></pre>

<strong>Notes on browser support</strong>
All major browsers, except our usual suspect, Internet Explorer, support the UI element states pseudo-classes. If you consider that you are only <strong>adding an extra level of detail</strong> and improved usability to your visitors, this can still be an option.</p>

## 6\. CSS 3 Structural Pseudo-Classes

### :nth-child

The <code>:nth-child()</code> pseudo-class allows you to <strong>target one or more specific children of a parent element</strong>.

You can target a single child, by defining its value as an <strong>integer</strong>:

<pre><code class="language-css">ul li:nth-child(3) {
  color: red;
  }</code></pre>

This will turn the text on the third <code>li</code> item within the <code>ul</code> element red. Bear in mind that if a different element is inside the <code>ul</code> (not a <code>li</code>), it will also be counted as its child.

You can target a parent’s children <strong>using expressions</strong>. For example, the following expression will match every third <code>li</code> element starting from the fourth:

<pre><code class="language-css">ul li:nth-child(3n+4) {
  color: yellow;
  }</code></pre>

In the previous case, the first yellow <code>li</code> element will be the fourth. If you just want to start counting from the first <code>li</code> element, you can use a simpler expression:

<pre><code class="language-css">ul li:nth-child(3n) {
  color: yellow;
  }</code></pre>

In this case, the first yellow <code>li</code> element will be the third, and every other third after it. Now imagine you want to target only the first four <code>li</code> elements within the list:

<pre><code class="language-css">ul li:nth-child(-n+4) {
  color: green;
  }</code></pre>

The value of <code>:nth-child</code> can also be defined as <strong>“even” or “odd”</strong>, which are the same as using “2n” (every second child) or “2n+1” (every second child starting from the first), respectively.</p>

### :nth-last-child

The <code>:nth-last-child</code> pseudo-class works basically as the <code>:nth-child</code> pseudo-class, but it starts <strong>counting the elements from the last one</strong>.

Using one of the examples above:

<pre><code class="language-css">ul li:nth-child(-n+4) {
  color: green;
  }</code></pre>

Instead of matching the first four <code>li</code> elements in the list, this selector will match the <em>last</em> four elements.

You can also use the values “even” or “odd”, with the difference that in this case they will count the children starting from the last one:

<pre><code class="language-css">ul li:nth-last-child(odd) {
  color: grey;
  }</code></pre>

### :nth-of-type

The <code>:nth-of-type</code> pseudo-class works just like the <code>:nth-child</code>, with the difference that it <strong>only counts children that match the element</strong> in the selector.

This can be very useful if we want to target elements that may contain different elements within them. For example, let’s imagine we want to turn every second paragraph in a block of text blue, but we want to ignore other elements such as images or quotations:

<pre><code class="language-css">p:nth-of-type(even) {
  color: blue;
  }</code></pre>

You can use the same values as you would use for the <code>:nth-child</code> pseudo-class.</p>

### :nth-last-of-type

You guessed it! The <code>:nth-last-of-type</code> pseudo-class can be <strong>used exactly like the aforementioned <code>:nth-last-child</code></strong>, but this time, it will only target the elements that match our selector:

<pre><code class="language-css">ul li:nth-last-of-type(-n+4) {
  color: green;
  }</code></pre>

We can be even more clever, and <strong>combine more than one of these pseudo-classes</strong> together on a massive selector. Let’s say all images within a post <code>div</code> to be floated left, except for the first and last one (let’s image these would full width, so they shouldn’t be floated):

<pre><code class="language-css">.post img:nth-of-type(n+2):nth-last-of-type(n+2) {
  float: left;
  }</code></pre>

So in the first part of this selector, we are targeting every image starting from the second one. In the second part, we are targeting every image except for the last one. Because the selectors aren’t mutually exclusive, we can use them both on one selector thus excluding both the first and last element at once!

### :last-child

The <code>:last-child</code> pseudo-class works just as the <code>:first-child</code> pseudo-class, but instead targets the <strong>last child of a parent element</strong>.

Let’s image you don’t want the last paragraph within your post <code>div</code> to have a bottom margin:

<pre><code class="language-css">.post &gt; p:last-child {
  margin-bottom: 0;
  }</code></pre>

This selector will target the last paragraph that is a direct <em>and</em> the last child of an element with the class of “post”.</p>

### :first-of-type and :last-of-type

The <code>:first-of-type</code> pseudo-class is used to target an element that is <strong>the first of its type within its parent</strong>.

For example, you can target the first paragraph that is a direct child of a particular <code>div</code>, and capitalize its first line:

<pre><code class="language-css">.post &gt; p:first-of-type:first-line {
  font-variant: small-caps;
  }</code></pre>

With this selector you make sure that you are targeting only paragraphs that are direct children of the “post” <code>div</code>, and that are the first to match our <code>p</code> element.

The <code>:last-of-type</code> pseudo-class works exactly the same, but targets the <em>last</em> child of its type instead.</p>

### :only-child

The <code>:only-child</code> pseudo-class represents an element that is <strong>the only child of its parent</strong>.

Let’s say you have several boxes (“news”) with paragraphs of text inside them. When you have more than one paragraph, you want the text to be smaller than when you have only one:

<pre><code class="language-css">div.news &gt; p {
  font-size: 1.2em;
  }

div.news &gt; p:only-child {
  font-size: 1.5em;
  }</code></pre>

In the first selector, we are defining the overall size of the <code>p</code> elements that are direct children of a “news” <code>div</code>. On the second one, we are overriding the previous font-size by saying, if the <code>p</code> element is the only child of the “news” <code>div</code>, its font size should be bigger.</p>

### :only-of-type

The <code>:only-of-type</code> pseudo-class represents an element that is <strong>the only child of its parent with the same element</strong>.

How can this be useful? Image you have a sequence of posts, each one represented by a <code>div</code> with the class of “post”. Some of them have more than one image, but others have only one image. You want the image within the later ones to be aligned to the center, while the images on posts with more than one image to be floated. That would be quite easy to accomplish with this selector:

<pre><code class="language-css">.post &gt; img {
  float: left;
  }

.post &gt; img:only-of-type {
  float: none;
  margin: auto;
  }</code></pre>

### :empty

The <code>:empty</code> pseudo-class represents <strong>an element that has no content</strong> within it.

It can be useful in a number of ways. For example, if you have multiple boxes in your “sidebar” <code>div</code>, but don’t want the empty ones to appear on the page:

<pre><code class="language-css">#sidebar .box:empty {
  display: none;
  }</code></pre>

Beware that even if there is a single space in the “box” <code>div</code>, it will not be treated as empty by the CSS, and therefore will not match the selector.

<strong>Notes on browser support</strong>
Internet Explorer (up until version 8) has no support for structural pseudo-classes. Firefox, Safari and Opera support these pseudo-classes on their latest releases. This means that if what it’s being accomplished with these selectors is fundamental for the <strong>website’s usability and accessibility</strong>, or if the larger part of the website’s audience is using IE and you don’t want to deprive them of some design details, it's be wise to keep using regular classes and simpler selectors to cater for those browsers. If not, you can just go crazy!

## 7\. The negation pseudo-class

The negation pseudo-class, <strong><code>:not()</code></strong>, lets you target elements that <strong>do not match</strong> the selector that is represented by its argument.

For example, this can be useful if you need to style all the <code>input</code> elements within a form, but you don’t want your input elements with the type submit to be styled — you want them to be styled in a different way —, to look more like buttons:

<pre><code class="language-css">input:not([type="submit"]) {
  width: 200px;
  padding: 3px;
  border: 1px solid #000000;
  }</code></pre>

Another example: you want all the paragraphs within your post <code>div</code> to have a larger font-size, except for the one that indicates the time and date:

<pre><code class="language-css">.post p:not(.date) {
  font-size: 13px;
  }</code></pre>

Can you image the number of possibilities this selector brings with it, and the amount of useless selectors you could strip out off your CSS files were it widely supported?

<strong>Notes on browser support</strong>
Internet Explorer is our usual party pooper here: no support at all, not even on IE8. This probably means that this selector will still have to wait a while before some developers lose the fear of adding them to their stylesheets.</p>

## 8\. Pseudo-elements

Pseudo-elements allow you to access <strong>elements that don’t actually exist in the HTML</strong>, like the first line of a text block or its first letter.

Pseudo-elements exist in CSS 2.1, but the CSS 3 specifications state that they should be used with the double colon “::”, to distinguish them from pseudo-classes. In CSS 2.1, they are used with only one colon, “:”. Browsers should be able accept both formats, except in the case of pseudo-elements that may be introduced only in CSS 3.</p>

### ::first-line

The <code>::first-line</code> pseudo-element will match the <strong>first line of a block</strong>, inline-block, table-caption or table-cell level element.

This is particularly useful to <strong>add subtle typographical details</strong> to your text blocks, like, for example, transforming the first line of an article into small caps:

<pre><code class="language-css">h1 + p::first-line {
  font-variant: small-caps;
  }</code></pre>

If you’ve been paying attention, you’ll know that this means the paragraph that comes <em>immediately after</em> an <code>h1</code> tag (“+”) should have its first line in small caps.

You could also refer to the first line of a particular <code>div</code>, without having to refer to the actual paragraph tag:

<pre><code class="language-css">div.post p::first-line { font-variant: small-caps; }</code></pre>

Or go one step farther and target specifically the <em>first</em> paragraph within a particular <code>div</code>:

<pre><code class="language-css">div.post &gt; p:first-child::first-line {
  font-variant: small-caps;
  }</code></pre>

Here, the “&gt;” symbol indicates that you are targeting a direct child the post <code>div</code>, so if the paragraph were to be inside a second <code>div</code>, it wouldn’t match this selector.</p>

### ::first-letter

The <code>::first-letter</code> pseudo-element will match the <strong>first letter of a block</strong>, unless it’s preceded by some other content, like an image, on the same line.

Like the <code>::first-line</code> pseudo-element, <code>::first-letter</code> is commonly used to <strong>add typographical details</strong> to text elements, like drop caps or initials.

Here is how you could use the <code>::first-letter</code> pseudo-element to create a <strong>drop cap</strong>:

<pre><code class="language-css">p {
  font-size: 12px;
  }

p::first-letter {
  font-size: 24px;
  float: left;
  }</code></pre>

Bear in mind that if you use both <code>::first-line</code> and <code>::first-letter</code> in the same element, the <code>::first-letter</code> properties will override the same properties inherited from <code>::first-line</code>.

This element can sometimes produce unexpected results, if you’re not aware of the W3C specs: it’s actually the CSS selector with the longest spec! So <strong>it’s a good idea to read them carefully</strong> if you’re planning on using it (as it is for all the other selectors).</p>

### ::before and ::after

The <code>::before</code> and <code>::after</code> pseudo-elements are used to <strong>insert content</strong> before or after an element’s content, purely via CSS.

These elements will inherit many of the properties of the elements that they are being attached to.

Image you want to the words “Graphic number x:” before the descriptions of graphs and charts on your page. You could achieve this without having to write the words “Graphic number”, or the number itself yourself:

<pre><code class="language-css">.post {
  counter-reset: image;
  }

p.description::before {
  content: "Figure number " counter(image) ": ";
  counter-increment: image;
  }</code></pre>

What just happened here?

First, we tell the HTML to <strong>create the “image” counter</strong>. We could have added this property to the body of the page, for example. Also, we can call this counter whatever name we want to, as long as we always reference it by the same name: try it for yourself!

Then we say that we want to add, before every paragraph with the class “description”, this piece of content: “Figure number ” — notice that only what we wrote between quotes will be created on the page, so we need to add the spaces as well!

After that, we have <code>counter(image)</code>: this will pick up the property we’ve already defined in the <code>.post</code> selector. It will by default start with the number one (1).

The next property is there so that the counter knows that for each <code>p.description</code>, it needs to increment the image counter by 1 (<code>counter-increment: image</code>).

It’s not as complicated as it looks, and it can be quite useful.

The <code>::before</code> and <code>::after</code> pseudo-elements are often only <strong>used with the content property</strong>, to add small sentences or typographical elements, but here it’s shown how we can use it in a more powerful way in conjunction with the <code>counter-reset</code> and <code>counter-increment</code> properties.

<strong>Fun fact:</strong> the <code>::first-line</code> and <code>::first-letter</code> pseudo-elements will match the content added by the <code>::before</code> pseudo-element, if present.

<strong>Notes on browser support</strong>
These pseudo-elements are supported by IE8 (not IE7 or 6), if the single colon format is used (for example, <code>:first-letter</code>, not <code>::first-letter</code>). All the other major browsers support these selectors.</p>

## CSS S<span data-sheets-value="{&quot;1&quot;:2,&quot;2&quot;:&quot;css selectors&quot;}" data-sheets-userformat="{&quot;2&quot;:513,&quot;3&quot;:{&quot;1&quot;:0},&quot;12&quot;:0}">electors</span> Conclusion

Enough with the boring talk, now it's time for <em>you</em> to grab the information on this post and go <strong>try it for yourself</strong>: start by creating an experimental page and test all of these selectors, come back here when in doubt and make sure to always refer to the W3C specs, but don't just sit there thinking that because these selectors aren't yet widely supported you might as well ignore them.

If you're a bit more <strong>adventurous</strong>, or if you're not afraid of letting go of the past filled with useless and non-semantic classes and ids, why not sneak one or two of these powerful CSS selectors into your next project? We promise you'll never look back.</p>

## References

*   [CSS 2 Selectors — W3C](https://www.w3.org/TR/CSS2/selector.html)
*   [CSS 3 Selectors Level 3 — W3C](https://www.w3.org/TR/css3-selectors/)
*   [Comparison of layout engines (Cascading Style Sheets) — Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_layout_engines_%28Cascading_Style_Sheets%29)
*   [Generated content, automatic numbering, and lists — W3C](https://www.w3.org/TR/CSS2/generate.html)

## Further Resources

*   [Keeping Your Elements’ Kids in Line with Offspring — A List Apart](https://www.alistapart.com/articles/keepelementskidsinlinewithoffspring/)
*   [Selectutorial - CSS selectors](https://css.maxdesign.com.au/selectutorial/index.htm)
*   CSS 2.1 selectors, [Part 1](https://www.456bereastreet.com/archive/200509/css_21_selectors_part_1/) and [Part 2](https://www.456bereastreet.com/archive/200510/css_21_selectors_part_2/)
*   [CSS 3 selectors explained](https://www.456bereastreet.com/archive/200601/css_3_selectors_explained/)
*   [CSS selectors and pseudo selectors browser compatibility](https://kimblim.dk/css-tests/selectors/)
*   [10 Useful CSS Properties Not Supported By Internet Explorer](https://www.impressivewebs.com/10-useful-css-properties-not-supported-by-internet-explorer/)
*   [Styling a Poem with Advanced CSS Selectors](https://webdesignernotebook.com/css/styling-a-poem-with-advanced-css-selectors/)

*You may also want to take a look at the following related posts:*

*   [Semantic CSS With Intelligent Selectors](https://www.smashingmagazine.com/2013/08/semantic-css-with-intelligent-selectors/)
*   [CSS Specificity And Inheritance](https://www.smashingmagazine.com/2010/04/css-specificity-and-inheritance/)
*   [CSS Specificity: Things You Should Know](https://www.smashingmagazine.com/2007/07/css-specificity-things-you-should-know/)
*   [CSS Inheritance, The Cascade And Global Scope](https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/)

{{< signature "al, il" >}}

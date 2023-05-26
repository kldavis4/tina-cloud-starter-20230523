---
title: How To Set Up A Print Style Sheet
slug: how-to-set-up-a-print-style-sheet
image: null
date: 2011-11-24T10:18:03.000Z
author: christian-krammer
description: >-
  In a time when everyone seems to have a tablet, which makes it possible to
  consume everything digitally, and the only real paper we use is bathroom
  tissue, it might seem odd to write about the long-forgotten habit of printing
  a Web page. Nevertheless, as odd as it might seem to visionaries and tablet
  manufacturers, we’re still far from the reality of a paperless world. [Links
  checked February/08/2017]

  [![Infinitum](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a5ffb6b-6f0f-4a29-b0c2-144ed91c4a80/print-screenshot-mainpage.png)](https://www.smashingmagazine.com/2011/11/24/how-to-set-up-a-print-style-sheet/)

  In fact, tons of paper float out of printers worldwide every day, because not
  everyone has a tablet yet and a computer isn’t always in reach. Moreover, many
  of us feel that written text is just better consumed offline. Because I love
  to cook, sometimes I print recipes at home, or emails and screenshots at work,
  even though I do so as rarely as possible out of consideration for the
  environment.
categories:
  - Coding
  - CSS
  - Techniques
  - Print
---
In a time when everyone seems to have a tablet, which makes it possible to consume everything digitally, and the only real paper we use is bathroom tissue, it might seem odd to write about the long-forgotten habit of printing a Web page. Nevertheless, as odd as it might seem to visionaries and tablet manufacturers, we’re still far from the reality of a paperless world.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Designing For Print With CSS](https://www.smashingmagazine.com/2015/01/designing-for-print-with-css/)
*   [Designing CSS Layouts With Flexbox Is As Easy As Pie](https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/)
*   [Web Design Industry Jargon: Glossary and Resources](https://www.smashingmagazine.com/2009/05/web-design-industry-jargon-glossary-and-resources/)
*   [Taking Pattern Libraries To The Next Level](https://www.smashingmagazine.com/taking-pattern-libraries-next-level/)

In fact, tons of paper float out of printers worldwide every day, because not everyone has a tablet yet and a computer isn’t always in reach. Moreover, many of us feel that written text is just better consumed offline. Because I love to cook, sometimes I print recipes at home, or emails and screenshots at work, even though I do so as rarely as possible out of consideration for the environment.

A print style sheet is useful and sometimes even necessary. Some readers might want to store your information locally as a well-formatted PDF to refer to the information later on, when they don’t have an Internet connection. However, <a href="https://evolt.org/ResponsiveWebAndPrint">print styles are often forgotten</a> in the age of responsive Web design. The good news is that a print style sheet is actually very easy to craft: you can follow a couple of simple <a href="https://www.smashingmagazine.com/responsive-web-design-guidelines-tutorials/">CSS techniques to create a good experience</a> for readers and show them that you’ve gone the extra mile to deliver just a slightly better user experience. So, how do we start?

{{% feature-panel %}}

## Getting Started

Let’s look at the process of setting up a print style sheet. The best method is to start from scratch and rely on the default style sheet of the browser, which takes care of the printed output pretty well by default. In this case, insert all declarations for printing at the end of your main style sheet, and enclose them with this distinct rule:

<pre><code class="language-css">
@media print {
   …
}
</code>
</pre>

For this to work, we have to prepare two things:

1.  Include all screen styles in the separate `@media screen {…}` rule;
2.  Omit the media type for the condensed style sheet: `<link rel="stylesheet" href="css/style.css"/>`

In rare cases, using screen styles for printing is the way to approach the design of the print style sheet. Although making the two outputs similar in appearance would be easier this way, the solution is not optimal because screen and print are different kettles of fish. Many elements will need to be reset or styled differently so that they look normal on a sheet of paper. But the biggest constraints are the limited page width and the need for an uncluttered, clear output. Building print styles separately from screen styles is better. This is what we will do throughout this article.

Of course, you could separate the declarations for screen and print into two CSS files. Just set the media type for the screen output to <code>media="screen"</code> and the media type for printing to <code>media="print"</code>, omitting it for the first one if you want to build on the screen style sheet.

To illustrate, I have set up a simple website of the fictional <a href="https://www.css3files.com/smashing-winery">Smashing Winery</a>.

<a href="https://www.css3files.com/smashing-winery"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/098e587f-bb2f-4603-8c9c-2c669402c465/1.jpg" alt="screenshot" width="500" /></a><br>
<em>Our example website.</em>

Everything needed for a proper screen display is in place. But as soon as the environment changes from virtual pixels to real paper, the only thing that matters is the actual content.

<img loading="lazy" decoding="async" class="alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36af094e-6714-417e-b2cb-e125b6a3cd20/21.jpg" alt="print style sheet" width="500" height="380" /><br>
<em>The two pages of the unaltered print preview. The header is not yet optimal, and both the main navigation and footer are superfluous.</em>

Therefore, as a first task, we will hide all the clutter: namely, the main navigation and footer.

<pre><code class="language-css">
header nav, footer {
display: none;
}
</code></pre>

Depending on the type of website, you could also consider hiding images by default. If the images are big, this would be wise, to save your users some printing costs. But if the images mainly support the content, and removing them would compromise the meaning, just leave them in. Whatever you decide, limit the images to a certain width, so that they don’t bleed off the paper. I’ve found that 500 pixels is a good compromise.

<pre><code class="language-css">
img {
max-width: 500px;
}
</code></pre>

Alternatively you could also rely on the tried and trusted <code>max-width: 100%</code>, which displays images at their maximum size but not bigger than the page width.

You might want to use a simple trick to get high-quality images when printing. Just provide a higher-resolution version of every image needed and resize it to the original size with CSS. Read more about this technique in the article “<a href="https://www.alistapart.com/articles/hiresprinting/">High-Resolution Image Printing</a>” on A List Apart.

Of course, we should hide video and other interactive elements, because they are useless on paper. These include <code>&lt;video&gt;</code>, <code>&lt;audio&gt;</code>, <code>&lt;object&gt;</code> and <code>&lt;embed&gt;</code> elements. You might want to consider replacing each video element with an image in the print style sheet, too.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f856db5-7433-4957-a142-07ad9a40abd0/print-stylesheet-33.jpg" alt="screenshot" width="500" /><br>
<em>With the main navigation, footer and images gone, the actual text is getting ever closer to center stage. But work remains to be done, especially with the header.</em>

## Adjusting To The Right Size

To define page margins, you can use <code>@page</code> rule to simply apply a margin all the way around the page. E.g.:

<pre><code class="language-css">
@page {
margin: 0.5cm;
}
</code></pre>

will set the page margin on all sides to 0.5cm. You can also adjust the margins for every other page. The following code sets the left page (1, 3, 5, etc.) and right page (2, 4, 6, etc.) margins independently.

<pre><code class="language-css">
@page :left {
margin: 0.5cm;
}

@page :right {
margin: 0.8cm;
}
</code></pre>

You can also use the <code>:first</code> page pseudo-class that describes the styling of the first page when printing a document:

<pre><code class="language-css">
@page :first {
  margin: 1cm 2cm;
}
</code></pre>

Unfortunately, <code>@page</code> is not supported in Firefox, but supported in Chrome 2.0+, IE 8.0+, Opera 6.0+ and Safari 5.0+. <code>@page :first</code> is supported only in IE8+ and Opera 9.2+. (<em>thanks for the tip, <a href="https://designshack.net/articles/css/6-thinks-i-learned-about-print-stylesheets-from-html5-boilerplate/">Designshack</a></em>)

Now let’s tweak some general settings for the fonts. Most browsers set the default to Times New Roman, because serif fonts are considered to be easier on the eyes when read on paper. We can use Georgia at 12-point font size and a slightly higher line height for better legibility.

<pre><code class="language-css">
body {
font: 12pt Georgia, "Times New Roman", Times, serif;
line-height: 1.3;
}
</code></pre>

However, to retain some control, we should explicitly set the font sizes below. The <a href="https://reeddesign.co.uk/test/points-pixels.html">chart on ReedDesign</a> gives us a feel for this; but with all of the screen sizes and resolutions out there, these are only rough estimates.

<pre><code class="language-css">
h1 {
font-size: 24pt;
}

h2 {
font-size: 14pt;
margin-top: 25px;
}

aside h2 {
font-size: 18pt;
}
</code></pre>

Apart from special cases (like the <code>&lt;h2&gt;</code> heading, which would otherwise be too close to the preceding paragraph), we don’t need to touch the margins or appearance of any elements, because they are handled quite nicely by the default settings. If you don’t like that certain elements are indented, such as <code>&lt;blockquote&gt;</code>, <code>&lt;ul&gt;</code> and <code>&lt;figure&gt;</code>, you could always reset their margins:

<pre><code class="language-css">
blockquote, ul {
margin: 0;
}
</code></pre>

Or you could override the default bullet style in unordered lists…

<pre><code class="language-css">
ul {list-style: none}
</code></pre>

…and replace it with a custom one; for example, a double arrow (and a blank space to give it some room):

<pre><code class="language-css">
li {
content: "» ";
}
</code></pre>

You could also make <code>&lt;blockquote&gt;</code> stand out a bit by enlarging it and italicizing the text.

## The Header

Currently, the remaining things to be dealt with in the header are the <code>&lt;h1&gt;</code> title and the logo. The first is there just for <a href="https://shop.smashingmagazine.com/products/pre-release-inclusive-design-patterns-by-heydon-pickering">accessibility</a> purposes and is hidden for screen display using CSS. While we could use it as a sort of header in the print-out to indicate the source of the content, let’s try something more attractive. Wouldn’t it be nice to display the actual logo, instead of the boring text?

Unfortunately, the “Winery” part of the logo is white and therefore not ideal for printing on light-colored paper. That’s why two versions of the logo are in the source code, one for screen display, one for printing. The latter image has no <code>alt</code> text, otherwise screen readers would repeat reading out “Smashing Winery.”

<pre><code class="language-markup">&lt;a href="/" title="Home" class="logo"&gt;
   &lt;img src="img/logo.png" alt="Smashing Winery" class="screen"/&gt;
   &lt;img src="img/logo_print.png" alt="" class="print"/&gt;
&lt;/a&gt;
</code></pre>

First, we need to hide the screen logo and the <code>&lt;h1&gt;</code> heading. Depending on the relevance of the images, we might have already decided to hide them along with other unneeded elements:

<pre><code class="language-css">
header h1, header nav, footer, img {
display: none;
}
</code></pre>

In this case, we have to bring back the print logo. Of course, you could use the adjacent sibling selector for the job (<code>header img + img</code>) to save the class name and live with it not working in Internet Explorer 6.

<pre><code class="language-css">
header .print {
display: block;
}
</code></pre>

Otherwise, you could just use <code>header .screen</code> (or <code>header :first-child</code>) to hide the main logo. And then the second logo would remain. Keep in mind that in print layouts, only images embedded via the <code>&lt;img&gt;</code> tag are displayed. Background images are not.

Voilà! Now we have a nice header for our print-out that clearly shows the source of everything. Alternatively, you could still remove the second logo from the source code and use the header’s <code>&lt;h1&gt;</code> heading that we switched off earlier (in other words, remove it from the <code>display: none</code> line). Perhaps you’ll need to hide the remaining logo as we did before. Additionally, the font size could be enlarged so that it is clearly recognized as the title of the website.

<pre><code class="language-css">
header h1 {
font-size: 30pt;
}
</code></pre>

As a little extra, the header in the print-out could show the URL of the website. This is done by applying the <code>:after</code> pseudo-element to the <code>&lt;header&gt;</code> tag, which unfortunately won’t work in IE prior to version 8; but because this is just a little bonus, we can live with IE’s shortcoming.

<pre><code class="language-css">
header:after {
content: "www.smashing-winery.com";
}
</code></pre>

To see what else these pseudo-elements can do, read the <a href="https://developer.mozilla.org/en/CSS/Pseudo-elements">description on the Mozilla Developer Network</a>.

Another thing about IE 6 to 8 is that HTML5 tags can’t be printed. Because we’re using these tags on the example website, we’ll have to apply Remy Sharp’s <a href="https://code.google.com/p/html5shiv/">HTML5shiv</a> in the header. The shiv allows you not only to style HTML5 tags but to print them as well. If you’re already using <a href="https://modernizr.com">Modernizr</a>, that’s perfect, because the shiv is included in it.

<pre><code class="language-markup">
&lt;script src="js/html5.js"&gt;&lt;/script&gt;
</code></pre>

Unfortunately, the behavior of the IEs is still a bit buggy even when this shiv is applied. HTML5 tags that were styled for the screen layout need to be reset, or else the styling will be adopted for the print-out.

Some developers add a short message as a supplement (or an alternative) to the displayed URL, reminding users where they were when they printed the page and to check back for fresh content. We can do this with the <code>:before</code> pseudo-element, so that it appears before the logo. Again, this won’t work in IE 6 or 7.

<pre><code class="language-css">
header:before {
display: block;
content: "Thank you for printing our content at www.smashing-winery.com. Please check back soon for new offers on delicious wine from our winery.";
margin-bottom: 10px;
border: 1px solid #bbb;
padding: 3px 5px;
font-style: italic;
}
</code></pre>

To distinguish it from the actual content, we’ve given it a gray border, a bit of padding and italics. Lastly, I’ve made it a block element, so that the border goes all around it, and given the logo a margin.

To make it more discreet, we could move this message to the bottom of the page and append it to main container of the page, which has the <code>.content</code> class. If so, we would use the <code>:after</code> element and a top margin to keep it distinct from the sidebar’s content. As far as I’m concerned, the URL is indication enough, so I would rely on that and omit the message.

Finally, we need to remove the border of the logo to prevent it from showing in legacy browsers, and move the <code>&lt;header&gt;</code> away from the content:

<pre><code class="language-css">
img {
border: 0;
}

header {
margin-bottom: 40px;
}
</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/942a5d86-113a-4456-a3d3-c902eb0c9fcb/print-stylesheet-52.jpg" alt="screenshot" width="500" /><br>
<em>The header shown two different ways, one with a logo and simple URL, and the other with a message and the title in plain text.</em>

## The Missing Link

Obviously, on paper, links aren’t clickable and so are pretty useless. You could try to build a workaround, replacing links with QR codes on the fly, but the solution may not be feasible. To put the links to use, you could display the URL after each string of anchor text. But text littered with URLs can be distracting and can impair the reading experience; and sparing the reader excessive information where possible is advisable.

The best solution is the <code>:after</code> pseudo-element. It displays the URL after each anchor text, surrounded by brackets. And the font size is reduced to make it less intrusive.

<pre><code class="language-css">
p a:after {
content: " (" attr(href) ")";
font-size: 80%;
}
</code></pre>

We’ve limited this technique to links within <code>&lt;p&gt;</code> elements as a precaution. To go a step further, we could choose to show only the URLs of external links. An <a href="https://developer.mozilla.org/en/CSS/Attribute_selectors">attribute selector</a> is perfect for this:

<pre><code class="language-css">
p a[href^="https://"]:after {
content: " (" attr(href) ")";
font-size: 90%;
}
</code></pre>

The possibilities for links in printed documents seem to be almost endless, so let’s try some more. To distinguish all internal links, let’s precede them with the website’s domain (omitting all the other properties, to keep things concise and clear):

<pre><code class="language-css">
p a:after {
content: " " attr(href) ")";
}
</code></pre>

Then, we can hide internal links (<code>#</code>), because there is not much to display:

<pre><code class="language-css">
p a[href^="#"]:after {
display: none;
}
</code></pre>

Also, external links will be appended as is, like above. Let’s consider SSL-secured websites, too (i.e. ones that begin with <code>https://</code>):

<pre><code class="language-css">
p a[href^="https://"]:after, a[href^="https://"]:after {
content: " (" attr(href) ")";
}
</code></pre>

But there is one thing to remember, especially with external links. Some are very long, such as the ones in the <a href="https://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266--webkit-border-radius">Safari Developer Library</a>. Such links can easily break a layout, like at the screen output. Luckily, a special property takes care of this:

<pre><code class="language-css">
p a {
word-wrap: break-word;
}
</code></pre>

This breaks long URLs when they reach a certain limit or, as in our case, when they exceed the page’s width. Just add this property to the first of the above declarations. Although this property is basically supported in a wide range of browsers — even IE 6 — it works only in Chrome when printing. While Firefox automatically breaks long URLs, Internet Explorer has no capability for this.

Finally, we set the link color to black to improve the experience for readers.

<pre><code class="language-css">
a {
color: #000;
}
</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23056fa2-c883-4ad1-a33a-4798eedb19b4/6.jpg" alt="screenshot" width="500" /><br>
<em>URLs, whether internal or external, now show up beside links with special treatment.</em>

Aaron Gustafson went one step further and built the little script Footnote Links. According to the description:
<blockquote>This script builds a list of URIs from any tags within a specified container and appends the list as footnotes to the document in a specified location. Any referenced elements are given a dynamically-assigned number which corresponds to the link in the footnote list.</blockquote>

Aaron’s article on A List Apart “<a href="https://www.alistapart.com/articles/improvingprint/">Improving Link Display for Print</a>” gives more insight into the idea behind this script.

While we’re at it, letting readers know where quotes come from, such as those wrapped in <code>&lt;blockquote&gt;</code> and <code>&lt;q&gt;</code> tags, would be thoughtful. Just append the <code>cite</code> attribute (which will be the URL) after quotation marks, like so:

<pre><code class="language-css">
q:after {
content: " (Source: " attr(cite) ")";
}
</code></pre>

## Side By Side

We haven’t yet dealt with the sidebar content. Even though it appears after the main content by default, let’s give it some special treatment. To keep it distinct, we’ll give the sidebar a gray top border and a safe buffer of 30 pixels. The last property, <code>display: block</code>, ensures that the border shows up properly.

<pre><code class="language-css">
aside {
border-top: 1px solid #bbb;
margin-top: 30px;
display: block;
}
</code></pre>

To separate it even more, we could set a special print property:

<pre><code class="language-css">
page-break-before: always;
</code></pre>

This will move the contents of the sidebar to a new page when printed. If we do this, we can omit all of the other properties.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a21a1d3-911a-476e-9db4-df4ee38b5832/7.jpg" alt="screenshot" width="500" /><br>
<em>The sidebar on screen (left) and printed out (right). I’ve grayed out everything else to make it more obvious here.</em>

We could do the same for comments. Comments don’t appear in the example, but they’re still worth touching on. Because they sometimes run long, omitting them in the print-out might be reasonable (just set <code>display: none</code> for the whole container). If you do want to show the comments, at least set <code>page-break-before</code>. You can also use <code>page-break-after: always</code> if there is content to print on a new page. The <code>page-break-before</code> and <code>page-break-after</code> properties are supported in all major browsers.

We can also use <code>widows</code> and <code>orphans</code> properties. The terms derive from traditional printing, and they take numbers as values. The <code>widows</code> property sets the minimum number of lines in a paragraph to leave at the top of a page before moving them entirely to a new page. The <code>orphans</code> property sets the number of lines for the bottom of the page. The <code>orphans</code> and <code>widows</code> properties are supported in IE 8+ and Opera 9.2+, but unfortunately not in Firefox, Safari or Chrome.

Now that we have taken care of the sidebar, the print style sheet is ready! You can <a href="https://www.css3files.com/smashing-winery/css/print.css">download it here</a>. The file is fully documented and so can serve as a helpful reference or starting point.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="106667" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2403bd1-a8d0-425d-aaaa-d7fa99a55b69/8.jpg" alt="screenshot" width="550" height="380" /><br>
<em>The completed print style sheet.</em>

## Just For Fun

You might be asking, “Why can’t we just put the sidebar next to the main content, like on the website itself?” Well, the screen and print outputs are a bit different. Unlike the former, print-outs aren’t very wide and thus don’t have much space to fill. But depending on the font size, the line length could exceed the maximum of 75 characters and so be <a href="https://baymard.com/blog/line-length-readability">more difficult to read</a>.

In this case, we could, of course, limit the width of the main content (preferably not too much — we shouldn’t set the line length to fall below about 55 characters) and then absolutely position the sidebar just below it, just like in the screen display. But describing this method falls beyond the scope of this article, so please consult the <a href="https://css3files.com/smashing-winery/css/style.css">screen style sheet</a> of the example website (line numbers 112 and 141 and down).

In my humble opinion, avoid such experiments. While in principle, print layouts have endless possibilities, focusing on the content and removing everything else is better. The better way to ensure an optimal line length is just to shrink the page’s width or enlarge the font size.</p>

### Preview Made Easy

<a href="https://github.com/etimbo/jquery-print-preview-plugin">Print Preview</a> by Tim Connell is a handy little jQuery plugin that replicates the built-in print-preview function, but with one difference. Instead of opening a separate page, it shows a sleek overlay, with “Close” and “Print” buttons at the top. It also has the convenient “P” shortcut. You might want to check out the <a href="https://etimbo.github.com/jquery-print-preview-plugin/example/index.html">demo page</a>, too.</p>

## A Missed Opportunity

Imagine that you were able to visit any page, hit “Print” and get an optimized version of the page to enjoy on paper. Unfortunately, we don’t live in this perfect world. Some websites still rely on JavaScript to generate print versions, and many other designers simply don’t care. But this is a missed opportunity. A carefully composed print style sheet could be used not only for printing but to optimize legibility for screen reading.

As the website owner, you can determine the images to display (if any), the optimal font and size, and the presentation of other elements. You could make the content more appealing than the versions produced by Instapaper and Readability by giving the print version the extra attention it deserves.</p>

### The Future

While using CSS3 for screen layouts is pretty common nowadays, it hasn’t quite established itself in the print environment yet. The W3C has an extensive description of “<a href="https://www.w3.org/TR/css3-page/">Paged Media</a>,” but unfortunately support is very limited at the moment, Opera and Chrome being the only browsers that enable a few of its related properties. With decent support, it would be possible to use the <code>@page</code> rule to set the dimensions of the page, switch to a landscape view, alter the margins, and do much more. Even <a href="https://www.w3.org/TR/css3-page/#page-size-media-query">media queries</a> are were conceived to respond to different page sizes.</p>

## Websites Designed Well For Print

Let's take a look at some examples of websites optimized for print.

<a href="https://alistapart.com/">A List Apart</a>
The slick multi-column design is simplified into a single column, full width, which intuitively mirrors the website’s sensible hierarchy. Article titles and authors are no longer active links. And beautiful clean typography is kept intact, thanks to the compatible fonts and simple colors; no font change is necessary, although the font-size value increases slightly. Advertising and affiliate styles are hidden, and the result is a simple, clean printed page that easily conforms well to any printer or page set-up in the document. A List Apart is exemplary, save for one important point: the logo does not appear anywhere in the print-out.

<a href="https://www.alistapart.com/articles/a-checklist-for-content-work/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93162" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d010023-4103-4a65-8e98-1fd4bf9d69c9/a-list-apart-screenshot.jpg" alt="A List Apart" width="500" height="282" /></a>

<a href="https://www.alistapart.com/articles/a-checklist-for-content-work/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93163" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c77a15b6-2475-42f8-9558-16b538d62d5c/a-list-apart-printview.jpg" alt="A List Apart" width="500" height="278" /></a>

<a href="https://lostworldsfairs.com/">Lost World’s Fairs</a>
The smooth printed page helps to carry the visuals of the website for Lost World’s Fairs. The main title and its colorful background are swapped for a simplified version in the print-preview style. However, some images could be removed to save some expensive printer ink. (<em>Updated</em>).

<a href="https://lostworldsfairs.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93208" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73e390e6-b92f-4c3f-b747-04a09d68371d/lost-worlds-fairs.jpg" alt="Lost World's Fairs" width="500" height="350" /></a>

<a href="https://lostworldsfairs.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93209" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8db2732e-e4ed-43ac-a85f-b74677aa493a/lost-worlds-fairs-print.jpg" alt="Lost World's Fairs" width="500" height="381" /></a>

<a href="https://www.themorningnews.org/">The Morning News</a>
One would expect most news websites to employ the print-preview function, yet that isn’t the case. The Morning News has prepared its content for print without much concern, happily excluding background images and color, while still getting its message across.

<a href="https://www.themorningnews.org/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93210" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f1c6ae3-2fb4-477b-aa82-dd31d10ad8e3/the-morning-news.jpg" alt="The Morning News" width="500" height="313" /></a>

<a href="https://www.themorningnews.org/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93210" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9befc147-723d-414f-81d0-fb1e98116543/morning-news-print.jpg" alt="The Morning News" width="500" height="275" /></a>

James Li
James Li has designed his personal website exceptionally well for this purpose, carefully preserving all spacing and key elements. The logo is a part of the printed product, whereas the navigation links are not: very clever, because navigation has no value on a printed page unless it is informative in and of itself. Non-Web fonts are converted to simple printable ones (see “Other Stuff…”). Brilliantly executed for print.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93212" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/166e7151-edc2-4fe8-9b95-5b6f8826c391/infinitum-screenshot.jpg" alt="Infinitum" width="500" height="384" />

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93213" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cf12174-5567-42e6-8045-8dffa8e4d4bc/infinitum-print.jpg" alt="Infinitum" width="500" height="409" />

<a href="https://www.techcrunch.com">TechCrunch</a>
TechCrunch's recent redesign tweaked not only the visual design of the site, but also the small details that have to be considered when the site is viewed on mobile or printed out. The print layout is very clean and minimalistic, without unnecessary details, yet also without links to the actual page that was printed out. The TechCrunch logo is omitted as well.

<a href="https://www.techcrunch.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93212" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99a385e9-794e-4fa2-9702-3d4120a89032/t-crunch-main.jpg" alt="TechCrunch" width="500" height="278" /></a>

<a href="https://www.techcrunch.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93212" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb3c0a25-1d34-4e1b-9133-12816179829e/t-crunch-print.jpg" alt="TechCrunch" width="500" height="349" /></a>

<a href="https://www.rga.com/">R/GA</a>
Although the logo isn’t present in the printed version of this website, attention is paid to the spacing of the content within. While the Web version has simple lines and a clean space, the printed page tightens up elements in order to best use the space. A strong grid and effective typography add to the effect. In this example, some images could be removed as well.

<a href="https://www.rga.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93214" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d18a18a0-fa05-4ec8-b92f-961420d54fa8/r-g-a-fwd-main.jpg" alt="r/ga" width="500" height="257" /></a>

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93214" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57fda570-bfe0-4169-990d-503176482ee1/r-g-a-fwd-print.jpg" alt="r/ga" width="500" height="464" />

<a href="https://www.studiomister.com/index.php">Studio Mister</a>
An excellent job of the print-preview function. The page has been meticulously designed to a grid and requires little in order to prepare it for print; some attention to the background color of text and not much else. Unfortunately, though, the logo is a background image and thus excluded.

<a href="https://www.studiomister.com/index.php"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93216" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9259c274-b2e5-46d8-ac27-145042ef7738/studio-mister-mainpage.jpg" alt="Studio Mister" width="500" height="292" /></a>

<a href="https://www.studiomister.com/index.php"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93217" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf1e57f6-3ec8-4748-b0e3-60578c28142b/studio-mister-print.jpg" alt="Studio Mister" width="500" height="343" /></a>

<a href="https://bottlerocketcreative.com/">Bottlerocket Creative</a>
Although this logo isn’t represented in the print-out either, the folks at Bottlerocket Creative have done very well to adapt their typographic style for offline viewing. Assuming the design was created mainly with images would be easy, but meticulous attention to type is evident upon closer inspection.

<a href="https://bottlerocketcreative.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93218" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/068f469b-8599-40a4-b65b-15d3243b5370/bottlerocket-main.jpg" alt="Bottle Rocket" width="500" height="370" /></a>

<a href="https://bottlerocketcreative.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93219" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb593cce-5f89-4018-a4d2-22d23245266f/bottlerocket-printview.jpg" alt="Bottle Rocket" width="500" height="283" /></a>

<a href="https://omniti.com">OmniTI</a>
OmniTI has optimized its content for print not by shrinking the main column, but by increasing the size of the text and not crowding the images together. The playful look adheres to good spacing. The only drawback? Many of the line breaks have been eliminated, causing some words and sentences to run into each other.

<a href="https://omniti.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93225" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fdd27ff-e541-4e18-b120-c38f162bb315/omniti-main.jpg" alt="Omni TI" width="500" height="300" /></a>

<a href="https://omniti.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="93226" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/749cb8bb-6cf7-4fef-a050-cd837f63a568/omniti-print.jpg" alt="Omni TI" width="500" height="414" /></a>

### In Conclusion

There’s a lot to consider when preparing your website to be printed out by readers. The process forces you to scrutinize every element of your content like never before, all because someone will want a hard copy of your work. Yet most of all, it’s important to recognize the difference between printing and actually reading. Perhaps these techniques hold merit in helping you visualize content for mobile devices. What better way to kill two birds with one stone than to work out your layout for the mobile while considering printing view at the same time to make sure that your content prints flawlessly for offline archival? The time you invest could double in value.

For more information on preparing content for print, including by modifying CSS, check out the following articles:

*   [The Definitive Guide](https://www.webcredible.co.uk/user-friendly-resources/css/print-stylesheet.shtml), Trenton Moss, Webcredible
*   [6 Things I Learned About Print CSS From HTML5 Boilerplate](https://designshack.net/articles/css/6-thinks-i-learned-about-print-stylesheets-from-html5-boilerplate/), Joshua Johnson, DesignShack
*   [CSS-Tricks Finally Gets a Print CSS](https://css-tricks.com/css-tricks-finally-gets-a-print-stylesheet/), Chris Coyier, CSS-Tricks
*   [CSS Print Profile](https://www.w3.org/TR/css-print/), W3C
*   [Media Queries](https://www.w3.org/TR/css3-mediaqueries/), W3C

<em>(al) (vf) (il)</em>


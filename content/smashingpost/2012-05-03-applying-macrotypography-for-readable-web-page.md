---
title: How To Apply Macrotypography For A More Readable Web Page
slug: applying-macrotypography-for-readable-web-page
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7123ae46-4978-45b7-8d81-764005d9e743/shift-logogs.jpg
date: 2012-05-03T00:24:02.000Z
author: nathan-ford
description: >-
  Any application of typography can be divided into two arenas: _micro_ and
  _macro_. Understanding the difference between the two is especially useful
  when crafting a reading experience, because it allows the designer to know
  when to focus on legibility and when to focus on readability.
categories:
  - Typography
  - Web Design
  - Graphic Design
  - Readability
---
Any application of typography can be divided into two arenas: <em>micro</em> and <em>macro</em>. Understanding the difference between the two is especially useful when crafting a reading experience, because it allows the designer to know when to focus on legibility and when to focus on readability.

<img loading="lazy" decoding="async" title="How To Apply Macrotypography For A More Readable Web Page" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8f3ca1a-83d3-471f-87c6-9fb88f94cfb1/readable-frontpage.jpg" alt="How To Apply Macrotypography For A More Readable Web Page" width="500" height="289" />

This article focuses mostly on a few simple macrotypographic techniques—with a dash of micro—and on how to combine them all to build a more harmonious, adaptable and, most importantly, <em>readable</em> Web page.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [10 Principles For Readable Web Typography](https://www.smashingmagazine.com/2009/03/10-principles-for-readable-web-typography/)
*   [16 Pixels: For Body Copy. Anything Less Is A Costly Mistake](https://www.smashingmagazine.com/2011/10/16-pixels-body-copy-anything-less-costly-mistake/)
*   [Designing For The Reading Experience](https://www.smashingmagazine.com/2013/02/designing-reading-experience/)
*   [<span class="headline">Using White Space For Readability In HTML And CSS</span>](https://www.smashingmagazine.com/2013/02/using-white-space-for-readability-in-html-and-css/)

{{% feature-panel %}}

First, some definitions. Microtypography has to do with the details; setting the right glyph, getting the appropriate kerning and tracking, and making stylistic choices such as when to use small-caps. Micro techniques have received <a title="The Future of Screen Typography Is in Your Hands, by Andreas Carlsson and Jaan Orvet" href="https://www.smashingmagazine.com/2012/01/30/the-future-of-screen-typography-is-in-your-hands/">a lot of attention recently</a>, as browser makers adopt new CSS attributes that allow for <a title="Internet Explorer is leading the charge" href="https://ie.microsoft.com/testdrive/Graphics/opentype/Default.html">finer control over Web type</a>. Microtypography deals mainly with legibility and can be thought of as the design of <em>letters</em> and <em>words</em>.

Macrotypography focuses on how type is arranged on the page. Most macro techniques have been achievable through CSS for quite some time, but because our understanding of the Web page is changing, the way we use these techniques must adapt. Macrotypography deals mainly with readability and can be thought of as the design of <em>paragraphs</em> and the <em>page</em>.</p>

## The Importance Of Readability

For the designer’s purpose, readability refers to the ease with which a body of text can be consumed, and it correlates closely to the reader’s eye strain. This should not be confused with <a title="Learn more about the differences at Sitepoint" href="https://www.sitepoint.com/typography-readability-and-legibility-part-1/">legibility</a>, which refers to the degree to which individual glyphs in text can be discerned. The techniques for creating a great reading experience are complementary to those for creating a great user experience (UX), and vice versa. They also both share the same symptoms of failure. Poor readability on a website can lead to confusion, frustration and ultimately abandonment, while a great reading experience is invisible, supportive and engaging.

As with UX design, every website design would benefit from some measure of concern for readability. For example, text-heavy websites—such as blogs, newspapers and magazines—should uphold readability as a priority, while websites for events and e-commerce might just need to tweak line heights and font sizes. Whatever level of importance you place on readability, you should undertake a continual process of refinement towards an effortless reading experience.</p>

## Techniques For Improving Readability

The foundation of great reading experiences on the Web lies in the study of book design. After all, books are where readable typography was honed. Personally, I hold <em>The Form of the Book</em> by Jan Tschichold as the ultimate resource for good taste in book design, and I am <a title="Jason Santa Maria is a fan" href="https://jasonsantamaria.com/reading/the-form-of-the-book">certainly</a> not <a title="Mandy Brown is a fan, too" href="https://aworkinglibrary.com/library/archives/the_form_of_the_book/">alone</a>.

Many of the techniques we’ll cover here have been adapted for the Web page from lessons introduced in this book. Sadly, the book has been out of print for about 20 years (at least in the US), and a copy can cost around <a title="The Form of the Book on Amazon.com" href="https://www.amazon.com/Form-Book-Morality-Classic-Typography/dp/0881791164/ref=sr_1_1?ie=UTF8&amp;qid=1330421526&amp;sr=8-1">$150 on Amazon’s marketplace</a>. I have <a title="The Form of the Book, Digested on Art=Work" href="https://artequalswork.com/posts/form-of-the-book.php">created a digest of it</a>, but if you want to read the full text, you could always try your local library or university (which is how I finally got my hands on it).

Now, let’s look at the various macro techniques—and a few micro techniques—to make your website’s content more readable. I have chosen an article that is typical of the kinds of reading experiences users encounter. I have removed the header and some branding elements, but it remains mostly as I found it.

In our example, important content (navigation, advertising, related links) lies on either side of the reading area. For optimum readability, a less obtrusive placement of these elements would be best, but this is not always possible. We will, therefore, not rearrange the layout, but work within it. Here is what we are starting with:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a14b562-b70e-4fe5-b429-5975c53807f1/macrotype-examples-1.jpg"><img class="130880" title="macrotype-examples-1-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c8b40f0-c50d-4c67-8e97-97b023b84c93/macrotype-examples-1-sm.jpg" alt="" width="500" height="404" /></a>

As we learn about each technique, we will apply it to our example. But keep in mind that this exercise is to improve only the <strong>reading experience</strong>, not the overall design.</p>

## Command Your Margins

Margins give the eye room to maneuver. They provide a buffer between the main content and ancillary elements—such as related links and ads—allowing the reader to focus on the text. Beyond this purely functional purpose, margins can also bring deeper harmony to the layout.

Margins comprise negative space; they afford the designer an opportunity to build a relationship between a body of text (the figure) and its surroundings (the ground). As Tschichold tells us, “Harmony between page size and the type area is achieved when both have the same proportions.” Now, the proportions of a page in a book are much different than those of most digital displays (especially ones in landscape orientation), so to adapt this concept to the Web, we can work towards a harmony between our text and its immediate visual container.</p>

### In Practice

On our example page, the margins are not very generous. Also, the main content is crammed in between two very loud columns. First, we can add more space to the right of the text, giving the reader room to go from the end of one line to the beginning of the next without being distracted by the secondary content on the right. And adding more margin to the left of the text allows the reader to easily find the start of the next line and to scan the article for topics they are interested in.

Margins can be set intuitively by increasing the amount on each side until the content feels comfortable. Applying this to our <code>article</code> element is easily achieved by adding <code>padding</code> in our CSS (rather than <code>margin</code>, in this case). For now, we will just double the <code>padding</code> on the left and right:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfea7f6b-3b14-4a68-ac1f-5fe27c577810/macrotype-examples-2.jpg"><img class="130881" title="macrotype-examples-2-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/963476a3-2cc1-4040-ae4d-eaa8cde67f9b/macrotype-examples-2-sm.jpg" alt="" width="500" height="404" /></a>

<pre><code class="language-css">article {
   padding-left: 20px;
   padding-right: 40px;
}</code></pre>

In our adjustment of the margins, we can create still greater harmony between the copy and its surroundings, but first we must visualize an invisible container around the content. This will be our “page” with which to build harmony in the reading area:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52334590-5033-4d19-8293-3f451d2c9a4d/macrotype-examples-3.jpg"><img class="130882" title="macrotype-examples-3-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/873f00f1-0ebb-4501-92e7-3a546c86db98/macrotype-examples-3-sm.jpg" alt="" width="500" height="404" /></a>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92619be9-c123-44e7-98ea-28ee4a10ff39/page-text-ratio.jpg"><img class="size-medium wp-image-130644" style="float: right; padding: 0 0 0.5em 1em;" title="page-text-ratio" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a75e369-f028-448d-a080-bcd2ba30a54a/page-text-ratio-175x300.jpg" alt="" width="175" height="300" /></a>

The way to create harmonious proportion between text and its container is to give them the same shape. The content should have the same proportions—only smaller—as its containing element. Tschichold surveyed a mountain of book proportions and concluded that the most harmonious proportions for margins are roughly 2:3:4:6 (top:right:bottom:left) for the left-facing page (recto) of a book. Given that we do not have facing pages on the Web, we can make the margins symmetrical and adjust the ratio to 2:3:4:3 by shaving off a bit of the left margin. Web text does not need as much side margins as book text because Web pages do not need to accommodate the reader’s thumbs.

Though they may seem the obvious unit of measure, percentages for <code>padding</code> will only measure in relation to the <em>width</em> of our <code>article</code> element’s container, skewing our top, bottom and side proportions to an inappropriate degree. Therefore it’s best work with <code>padding</code> in ems or pixels until the reading area has the same proportions as its container. To keep things simple, let’s start with 2em for the top padding in our example. After applying our adjusted ratio from above, our <code>article</code>’s <code>padding</code> can be written as <code>2em 3em 4em 3em</code> or <code>2em 3em 4em</code> in CSS shorthand. Given the fluid nature of content on the Web, this is just an approximation of Tschichold’s proportions. For a typical body of text on the web—which is taller than it is wide—the margin should be generally less on top, even on the sides, and most at the bottom:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/712e0d2a-ca14-4024-b5d2-012bcfdf23fe/macrotype-examples-41.jpg"><img class="130883" title="macrotype-examples-4-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0e0baee-3e61-410a-a747-3b6582a48cfa/macrotype-examples-4-sm.jpg" alt="" width="500" height="404" /></a>

<pre><code class="language-css">article {
   padding: 2em 3em 4em;
}</code></pre>

We can also move the lead image to the right. This allows the body copy to hold its shape better and allows for even easier scanning of the article. We can break this principle to draw attention to images and figures, of course, but for our example the image is too distracting on the left when placed early in the article.

If we want, we can bring the text forward on the z axis, putting even more focus on our copy and de-emphasizing the ancillary content by creating a visible container for our text. This is a tactic we can easily use in Web design that books do not need:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c635a7c-ca10-4919-a375-bd56e23a1503/macrotype-examples-6.jpg"><img class="130885" title="macrotype-examples-6-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeb7239c-b82d-4ecb-9ab7-da6457c97ecb/macrotype-examples-6-sm.jpg" alt="" width="500" height="404" /></a>

<pre><code class="language-css">body {
   background: #fcfcfc;
}

article {
   background: #fff;
   border: 1px solid #eee;
   padding: 2em 3em 4em;
}</code></pre>

Our page already feels more balanced and less intimidating, but we can use more techniques in the body of the text to further enhance readability.

## Choose Readable Fonts

Font selection is a micro concern, but it has a tremendous impact on the macro appearance. In <a title="Detail in typography on Amazon.com" href="https://www.amazon.com/Detail-Typography-Jost-Hochuli/dp/0907259340"><em>Detail in Typography</em></a>, Jost Hochuli best outlines this interdependence: “In typography, details can never be considered in isolation.”

The font for the body copy should be chosen for its on-screen readability, before any concern for style. The headings and pull quotes are perfect opportunities to flex your typographic creativity, but leave the long runs of copy to dependably readable workhorses such as Georgia, Arial and Myriad, which were all designed for optimal reading on a back-lit screen.

Fonts that are more readable on digital screens typically exhibit the following attributes:

*   Tall x-height;
*   Slightly wider em width, but not condensed or extended;
*   Mostly devoid of style;
*   Serifs for larger type, and sans-serif for smaller type.

All of these rules have exceptions, but they should be your guiding principles when choosing a font for the body copy. Here are some font stacks that I find give some flavor of style, provide appropriate fallbacks and are all highly readable:

*   `"[Proxima Nova Regular](https://typekit.com/fonts/proxima-nova "Proxima Nova on Typekit")", "Helvetica Neue", Arial, Helvetica, sans-serif;` (As used right here on Smashing Magazine)
*   `"[Myriad Pro](https://typekit.com/fonts/myriad-pro "Myriad Pro on Typekit")", Arial, Helvetica, sans-serif;` (As used on [my website](https://artequalswork.com "My site"))
*   `"[Fanwood Text"](https://www.google.com/webfonts/specimen/Fanwood+Text "Fanwood Text on Google Fonts")", Georgia, Times, "Times New Roman", serif;`
*   `"[PT Sans](https://www.google.com/webfonts/specimen/PT+Sans "PT Sans on Google Fonts")", "Trebuchet MS", Arial, sans-serif;`

### In Practice

Let’s apply Myriad Pro to the body text on our page:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90753060-2eba-415a-9399-75b0dd68fd95/macrotype-examples-6a.jpg"><img class="130886" title="macrotype-examples-6a-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18bf5923-e8a7-4a17-8076-4531c4d3a6af/macrotype-examples-6a-sm.jpg" alt="" width="500" height="404" /></a>

<pre><code class="language-css">article {
   background: #fff;
   border: 1px solid #eee;
   font-family: "Myriad Pro", Arial, Helvetica, sans-serif;
   padding: 2em 3em 4em;
}</code></pre>

## Keep It Measured

In setting any block of text, we must consider its measure. Measure is defined by either the number of characters per line or the number of words. I use words because they are easier to count, and I try to follow Tshichold’s suggestion of 8 to 12 words per line. If you base your measure on characters, then 45 to 85 characters per line is ideal. Once the margins and widths have been set, proper measure can be achieved through two attributes in the CSS, <code>font-size</code> and <code>word-spacing</code>.

When deciding on a size, strike a balance between making the font small enough that the reader is not too distracted when jumping to the next line, but big enough that they do not have to lean in to read the text on the screen. For most fonts, 16 pixels works well. Other factors might lead you to making it larger or smaller, but 16 pixels is a great place to begin. As for word spacing, most browsers do a decent job of setting this for you, but if you are having trouble getting an appropriate measure, cheating this attribute slightly either way can be handy.</p>

### In Practice

On our page, let’s add a 16-pixel font size, and cheat the word spacing in just a tiny bit to achieve a proper measure (<code>word-spacing</code> is supported in <a title="word-spacing support" href="https://reference.sitepoint.com/css/word-spacing">all major browsers</a>). You might instead want to use ems or <a title="A great method from Jonathan Snook for using rems" href="https://snook.ca/archives/html_and_css/font-size-with-rem">rems</a> here so that the layout remains flexible whatever the font size set by the user as their default.

Until we set a new line height, our page will look like a jumbled mess, so let’s just look at the code at this point:

<pre><code class="language-css">article {
   background: #fff;
   border: 1px solid #eee;
   font-family: "Myriad Pro", Arial, Helvetica, sans-serif;
   font-size: 16px;
   padding: 2em 3em 4em;
   word-spacing: -0.05em;
}</code></pre>

## Set An Appropriate Line Height

Once the font size is set, you can determine the appropriate line height. On the Web, we work in terms of line height, which by default is an equal amount of space above and below text on a line. Not to be confused with leading in print design, which generally refers to the amount of space below a line of text. The governing rule for line height (and leading) is, the <strong>longer</strong> the line length, the <strong>taller</strong> the line height should be. And vice versa: the <strong>shorter</strong> the line length, the <strong>shorter</strong> the line height.

Find an appropriate line height by first determining the point at which the ascenders and descenders of the lines of text do not touch, yet the lines are close enough that the reader requires no effort to find the next line. Then adjust until the height feels balanced with the line length. Some may leave the <code>line-height</code> attribute to the browser’s default, while some may set a global <code>line-height</code> on the <code>body</code> element. Both approaches make sense because the line height would then stay proportional to the element’s font size; but both also assume that the line width of the content will stay consistent, which could lead to situations that violate our governing rule.</p>

### In Practice

Let’s add a line height of 1.3 ems to our example, using ems so that our line height stays proportional to the font size, and see how the font size and line height work together:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20764c96-f939-44d9-8c7f-bcbadd3df70d/macrotype-examples-7.jpg"><img class="130887" title="macrotype-examples-7-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/deb5c43c-1a69-4ce1-bd0b-d60acc1c566f/macrotype-examples-7-sm.jpg" alt="" width="500" height="404" /></a>

<pre><code class="language-css">article {
   background: #fff;
   border: 1px solid #eee;
   font-family: "Myriad Pro", Arial, Helvetica, sans-serif;
   font-size: 16px;
   line-height: 1.3em;
   padding: 2em 3em 4em;
   word-spacing: -0.05em;
}</code></pre>

It is important to note that readable line heights can be especially tricky to keep consistent in responsive layouts, as line lengths will vary based on device widths. To solve this issue, Tim Brown has proposed an idea he calls “<a title="Molten Leading on Nice Web Type" href="https://nicewebtype.com/notes/2012/02/03/molten-leading-or-fluid-line-height/">Molten Leading</a>,” which would allow line heights to increase proportionally based on the screen width. His post links through to a couple of Javascript implementations of this idea. In lieu of Javascript intervention, you can also manually find the screen widths at which the line heights become uncomfortable, use a media query to target that width, and set a more readable <code>line-height</code> in the CSS.</p>

## Find The Proper Paragraph Styles

We need to figure out which paragraph style best fits the content. Jon Tan has done a fantastic job of outlining <a title="12 Examples of Paragraph Typography" href="https://jontangerine.com/silo/typography/p/">various styles</a> and how to craft them with CSS. The appropriate style for a piece of content varies based on the flavor of the content and the rhythm of the paragraphs. I have written about my <a title="Island of Thought in Macrotypography, on Art=Work" href="https://artequalswork.com/posts/islands-of-thought.php">preference for using indents</a>, rather than line breaks, when setting long-form text. This helps to keep the flow between ideas, but it can be distracting when the paragraphs are short or the line length is long. Deciding what constitutes the <a title="The Perfect Paragraph, by Heydon Pickering on Smashing Mag" href="https://www.smashingmagazine.com/2011/11/29/the-perfect-paragraph/">perfect paragraph</a> for your content is up to you.</p>

### In Practice

Our page is a news article, where the flow between paragraphs is dictated more by chronology than by ideas, so line breaks are still appropriate. We could easily apply indents, if appropriate, to the paragraphs with one simple CSS rule:

<pre><code class="language-css">article p + p {
   text-indent: 2em;
}</code></pre>

We specify <code>p + p</code> rather than just applying the rule to all <code>p</code> tags because we want to indent only those paragraphs that follow other paragraphs. Ones that follow headings, images and so on should not be indented.

Instead of indenting, though, we just want to shrink the line breaks a bit so that each paragraph is not so disconnected from the last. For our page, let’s use half of the line height:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c1e648b-5012-4087-8903-9915f4dc1b81/macrotype-examples-82.jpg"><img class="130888" title="macrotype-examples-8-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83a959af-667b-4d87-9cd1-92d8da8f9f70/macrotype-examples-8-sm.jpg" alt="" width="500" height="404" /></a>

<pre><code class="language-css">article p {
   margin-bottom: 0.5em;
}</code></pre>

## Balance The Text’s Contrast

One final consideration for content is text color. Contrast is a major contributing factor in <a title="More on Contrast and Readability" href="https://www.writer2001.com/colwebcontrast.htm">eye strain</a> and so greatly impacts readability. Low contrast between text and background causes more squinting and blinking among readers, a sure sign of strain. Black on yellow has the highest contrast, but we have been conditioned to view this as a sign of warning or alarm, thus increasing anxiety among readers. Black on white is high in contrast, too, but too harsh for extended reading on back-lit screens. For long-form text, I have found dark-gray text (around <code>#333</code>) on a white or light-gray background (no darker than <code>#EEE</code>) to be optimal. This is a gross simplification of color theory to suit the purposes of this article. To learn more about color, <a title="Mark’s Site" href="https://www.markboulton.co.uk/">Mark Boulton</a> has written a great primer on color theory for the Web; you can also find many great examples in Smashing Magazine’s <a title="Color Theory for Designers, pt. 1" href="https://www.smashingmagazine.com/2010/01/28/color-theory-for-designers-part-1-the-meaning-of-color/">series on color</a>.</p>

### In Practice

Our article already has a white background (serving as a boundary for the margins), set against a wider light-gray background. We should probably keep the white, and lessen the darkness of the text to <code>#444</code>. We can then use <code>#000</code> on the headings to give them slightly more emphasis:

<pre><code class="language-css">article p {
   margin-bottom: 0.5em;
   color: #444;
}

article h1 {
   color: #000;
}</code></pre>

## The Result

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62ef45c8-3f32-426b-a092-53e00d549f00/macrotype-examples-91.jpg"><img class="130889" title="macrotype-examples-9-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e9e11f3-178c-42fe-9ebc-ffaa1372fa8e/macrotype-examples-9-sm.jpg" alt="" width="500" height="404" /></a>

We now have a much more readable page that invites users into the content. We could employ many more techniques across the entire website, but we have focused here on the main content block. <a title="Posts by Harry Roberts" href="https://www.smashingmagazine.com/author/harry-roberts/" rel="author">Harry Roberts</a> has written a <a title="Technical Web Typography, by Harry Roberts for Smashing Magazine" href="https://www.smashingmagazine.com/2011/03/14/technical-web-typography-guidelines-and-techniques/">great overview of these techniques</a> and more for Smashing Magazine, which will give you a deeper understanding of everything covered here.

With a clean reading experience, people will better absorb the ideas being presented and will undoubtedly come back for more—that is, if your content is worth reading… but I can’t help you there.</p>

## Excellent Reading Experiences On The Web

Readability is not a new concept, of course. If you are just discovering what makes for a good reading experience, then congratulations, and welcome to all the discomforts of recognizing cramped and neglected type on the Web. It’s not all pain, though. Plenty of well-considered blocks of content are to be found. Let’s look at a few great ones and a couple that could be great with slight tweaks.

<strong>Please note:</strong> In the interest of showcasing only the reading experience, we have cropped each page to a scrolled view of the main content.

<a title="Great example of creating a 'page'" href="https://24ways.org/2011/crafting-the-front-end">24 Ways</a>
The reading experience on 24 Ways is quite nice. The text contrast is well balanced, the measure is not too long, and the font size is generous. At all responsive breakpoints, the design is a perfect example of a page with sufficient and balanced margins around the main reading area.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51cf9317-a2ad-40d2-9ddc-09730800f811/macrotype-example-24ways1.jpg"><img class="130890" title="macrotype-example-24ways-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b40d609a-1433-434e-a209-527f461137c2/macrotype-example-24ways-sm.jpg" alt="" width="500" height="375" /></a>

<em>Desktop view</em>

<a title="Take a look at any long-form article on CNN" href="https://edition.cnn.com/">CNN</a>
Long-form articles on CNN are good examples of how readability can work well on news websites. The layout does not show a visible container for the article—which in this case might have been distracting on a page already laden with so much content—but the margins are generous. Also, the line breaks for the paragraph styles are completely appropriate, because most online news stories are collated and updated from many sources and are not linear ideas. The font size (currently 14 pixels for the body copy) could stand to be a bit bigger, though.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37f25fe2-701e-4666-a2ab-34dd3bb1c6d1/macrotype-example-cnn1.jpg"><img class="130892" title="macrotype-example-cnn-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7624481d-d1b3-4319-96c8-5641641a172e/macrotype-example-cnn-sm.jpg" alt="" width="500" height="375" /></a>

<a title="A post on Contents magazine" href="https://contentsmagazine.com/articles/space-to-breathe/">Contents</a>
The tablet view of Contents magazine is a wonderful experience all around. The measure is perfect, the line height and font size play together nicely, and the paragraph styles are perfectly suited to the content. The measure does get too long at desktop sizes, but with all of the other factors working so well, the effect on overall readability is negligible.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df15a28d-ad27-436c-b39e-9b1227bc5215/macrotype-example-contents-tab1.jpg"><img class="130894" title="macrotype-example-contents-tab-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e9425fc-9762-45e6-aa10-d3170e822b80/macrotype-example-contents-tab-sm.jpg" alt="" width="500" height="375" /></a><br>
<em>Tablet view</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa641af1-fa45-43b1-85e5-d5dbc93d8f3e/macrotype-example-contents-desk1.jpg"><img class="130893" title="macrotype-example-contents-desk-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e59c369b-3d6e-4de3-a6f9-e915808a491f/macrotype-example-contents-desk-sm.jpg" alt="" width="500" height="375" /></a><br>
<em>Desktop view</em>

<a title="A post on Elliot’s blog" href="https://elliotjaystocks.com/blog/dog-days/">Elliot Jay Stocks</a>
Elliot does quite a few things well on his website. The measure is right, the font (Skolar) is very readable and set at a comfortable size (16 pixels), and the line height is just tall enough to accommodate the link style. Generous margins create harmony between the main content and its container, while the side margins are uneven, making the page look like the recto of a book and giving the layout a unique character.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/763e70b6-aab7-4eb6-b8b9-526d108c38e8/macrotype-example-elliot1.jpg"><img class="130895" title="macrotype-example-elliot-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fc56d5a-cc95-49d4-ac29-a17f5bb075f1/macrotype-example-elliot-sm.jpg" alt="" width="500" height="375" /></a>

<a title="An article on Esquire.com" href="https://www.esquire.com/blogs/mens-fashion/colorful-clothes-for-men-2012?click=mid">Esquire</a>
Most articles on Esquire are great, but the reading experience is merely good. The margins are ample, the font is readable, and the contrast is high. All of these go a long way towards establishing good readability, but a few simple tweaks would make it great. Increasing the right padding would shorten the measure, which is a bit too long as it is. The font size could also be increased by a couple of pixels. And given that most Esquire articles are a linear progression of ideas, I would suggest paragraph indents rather than line breaks.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c84dbbb-1f99-4cd6-b0f2-c783a30c0778/macrotype-example-esquire1.jpg"><img class="130896" title="macrotype-example-esquire-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cd2d64b-2bfc-4835-a8eb-12f52e4a1189/macrotype-example-esquire-sm.jpg" alt="" width="500" height="375" /></a>

<a title="An article on Guardian.co.uk" href="https://www.guardian.co.uk/business/2012/mar/04/pension-funds-infrastructure-osborne">The Guardian</a>
The design team over at The Guardian pays attention to crafting great all-around experiences. Readability is no exception. Measure, contrast and paragraph styles all work together to create a focused and comfortable reading experience in the midst of what could be an overwhelming amount of content.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e28657fa-5267-4d6a-975f-5fcf65b0d490/macrotype-example-guardian1.jpg"><img class="130897" title="macrotype-example-guardian-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b20f70a6-20bc-4a09-8917-80e8c3a7a71c/macrotype-example-guardian-sm.jpg" alt="" width="500" height="375" /></a>

<a title="An article on A Working Library" href="https://aworkinglibrary.com/library/archives/deploy/">A Working Library</a>
A Working Library is one of the best reading experiences on the Web. Every aspect of readability discussed in this article has been well considered and executed. The harmony between text and its container is pitch perfect.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a63da1b-b12b-4129-9414-9b658663e570/macrotype-example-workinglibrary1.jpg"><img class="130898" title="macrotype-example-workinglibrary-sm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6387891e-d685-4368-a5dd-ef5456de1696/macrotype-example-workinglibrary-sm.jpg" alt="" width="500" height="375" /></a>

## Refining Towards The Ideal

With the examples above, we have tried to show how readability can excel in a few different digital environments: blogs, news websites and online magazines. Some of these website do not have many of the constraints (such as ads and related content) of more commercial websites, so it could be argued that these designs exist in a vacuum, without pragmatic application or real-world pressures. We need these shining examples, though, to help us find the ideal reading experience for each project; and once we know that ideal, we should do our best to reach it.

In a recent talk on “What Is Reading For?” the famous typographer and poet <a title="More about Bringhurst" href="https://en.wikipedia.org/wiki/Robert_Bringhurst">Robert Bringhurst</a> stated, “Books are and have to be utilitarian objects. They have to be <em>used</em>.” The same could be said of Web pages. Ideal reading experiences create better user experiences. Our job as designers is to refine the aesthetic qualities of the Web’s content in order to speed the process of consumption, thereby facilitating deeper understanding. Tired eyes all over the Web are counting on us.

{{< signature "al" >}}


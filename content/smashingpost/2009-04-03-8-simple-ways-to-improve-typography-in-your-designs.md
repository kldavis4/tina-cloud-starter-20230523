---
title: 8 Simple Typography Tips For Your Designs
slug: 8-simple-ways-to-improve-typography-in-your-designs
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de1ae6ca-28a9-4c90-aeb2-18219107fdae/typografie-a2poster.jpg
date: 2009-04-03T17:46:35.000Z
author: antonio-carusone
description: >-
  Many people, designers included, think that **typography** consists of only
  selecting a typeface, choosing a font size and whether it should be regular or
  bold. For most people it ends there. But there is much more to achieving good
  typography and it's in the details that designers often neglect.
categories:
  - Coding
  - Typography
  - CSS
---
Many people, designers included, think that <strong>typography</strong> consists of only selecting a typeface, choosing a font size and whether it should be regular or bold. For most people it ends there. But there is much more to achieving good typography and it's in the details that designers often neglect. 

These details give the designer total control, allowing them to create beautiful and consistent typography in their designs. While these details can be applied across different types of media, in this articles we're going to focus on how to apply them to web design using CSS. Here are <strong>8 simple tips you can use CSS to improve your typography</strong> and hence the overall usability of your designs.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [10 Principles For Readable Web Typography](https://www.smashingmagazine.com/2009/03/10-principles-for-readable-web-typography/)
*   [Applying Macrotypography For A More Readable Web Page](https://www.smashingmagazine.com/2012/05/applying-macrotypography-for-readable-web-page/)
*   [16 Pixels: For Body Copy. Anything Less Is A Costly Mistake](https://www.smashingmagazine.com/2011/10/16-pixels-body-copy-anything-less-costly-mistake/)
*   [How To Choose The Right Face For A Beautiful Body](https://www.smashingmagazine.com/2012/05/how-to-choose-the-right-face-for-a-beautiful-body/)

## 1\. Measure

The measure is the length of a line of type. To a reader's eye, long or short lines can be tiring and distracting. A long measure disrupts the rhythm because the reader has a hard time locating the next line of type. The only time a narrow measure is acceptable is with a small amount of text. For optimum readability you want the measure to be between 40-80 characters, including spaces. <strong>For a single-column design 65 characters is considered ideal</strong>.

{{% feature-panel %}}

![typography tips](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7efa6777-106a-489b-9a88-579f9fb54bda/image1.jpg)

A simple way to calculate the measure is to use Robert Bringhurst's method which multiples the type size by 30. So if the type size is 10px, multiplying it by 30 gives you a measure of 300px or around 65 characters per line. The code would look something like this:

<pre><code class="language-css">p {
  font-size: 10px;
  max-width: 300px;
}</code></pre>

<em>I'm using px because it makes the math easier but this also works with em's.</em>

## 2\. Leading

Leading is the space between the lines of type in a body of copy that plays a big role in readability. Correctly spaced lines make it easier for a reader to follow the type and improves the overall appearance of the text. Leading also alters typographic color, which is the density or tone of a composition.

Many factors affect leading: typeface, type size, weight, case, measure, wordspacing, etc. The longer the measure, the more leading is needed. Also, the larger the type size, the less leading is required. A good rule is to set the leading <strong>2-5pt larger than the type size</strong>, depending on the typeface. So if you set the type at 12pt, a 15pt or 16pt leading should work well on the web.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dd16b7e-2a0e-4f9d-866a-b1cd04fe5072/image2.jpg)

This takes some finessing to get the right spacing but here is an example of what the code would look like:

<pre><code class="language-css">body {
  font-family: Helvetica, sans-serif;
  font-size: 12px;
  line-height: 16px;
}</code></pre>

## 3\. Hanging Quotes

Hang quotes in the margin of the body of text. By not doing so a quotation mark that is flush with the text will interrupt the left margin and disrupt the rhythm of the reader. Hanging quotes keeps the left alignment intact and balanced therefore increasing readability.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df78f01e-c6dc-4f76-b4f1-5fd4625b72d2/image3.jpg)

This is achieved very easily with CSS using the blockquote element:

<pre><code class="language-css">blockquote {
  text-indent: -0.8em;
  font-size: 12px;
}</code></pre>

The negative indent will vary depending on the typeface, type size and margins.</p>

## 4\. Vertical Rhythm

A baseline grid is the foundation for consistent typographic rhythm on a page. It allows the readers to easily follow the flow of the text, which in turn increases readability. A <strong>continuous rhythm in the vertical space</strong> keeps all the text on a consistent grid so that proportion and balance are retained throughout the page, no matter the type size, leading or measure.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/561aa93b-21c4-44d7-9a39-f68f1749ecd9/image4.jpg)

To keep a vertical rhythm in CSS, you want the spacing between elements and the line-spacing (leading) to equal the size of the <strong>baseline grid</strong>. For example, lets say you're using a 15px baseline grid, meaning that there are 15px between each baseline. The line-spacing would be 15px and the space between each paragraph would also be 15px. Here is an example:

<pre><code class="language-css">body {
  font-family: Helvetica, sans-serif;
  font-size: 12px;
  line-height: 15px;
}

p {
  margin-bottom: 15px;
}</code></pre>

This allows each paragraph element to align with the grid, keeping the vertical rhythm of the text.</p>

## 5\. Widows and Orphans

A <strong>widow</strong> is a short line or single word at the end of a paragraph. An orphan is a word or short line at the beginning or end of a column that is separated from the rest of the paragraph. Widows and Orphans create awkward rags, interrupt the reader's eye and affect readability. They can be avoided by adjusting the type size, leading, measure, wordspacing, letterspacing or by entering manual line breaks.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94951ff0-b132-4e39-a108-e540a5d83b4a/image5.jpg)

Unfortunately, there is no easy way to prevent typographic widows and orphans with CSS. One way to remove them has been mentioned above, but there is also a jQuery plug-in called <a href="https://davecardwell.co.uk/javascript/jquery/plugins/jquery-widont/">jQWidon’t</a> that places a non-breaking space between the last two words of an element.

## 6\. Emphasis

Giving emphasis to a word <strong>without interrupting the reader</strong> is important. Italic is widely considered to be the ideal form of emphasis. Some other common forms of emphasis are: bold, caps, small caps, type size, color, underline or a different typeface. No matter which you choose, try to limit yourself to using only one. Combinations such as caps-bold-italic are disruptive and look clumsy.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c3221a5-06e6-4663-99bb-04935226c68e/image6.jpg)

Here are some difference ways of creating emphasis with CSS:

<pre><code class="language-css">span {
  font-style: italic;
}

h1 {
  font-weight: bold;
}

h2 {
  text-transform: uppercase;
}

b {
  font-variant: small-caps;
}</code></pre>

Keep in mind that the font-variant style only works if the font supports the small-caps variant.</p>

## 7\. Scale

Always compose with a scale, whether it's the traditional scale developed in the sixteenth century that we're all familiar with, or one you create on your own. A scale is important because it <strong>establishes a typographic hierarchy</strong> that improves readability and creates harmony and cohesiveness within the text.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3e8a497-6877-495c-9813-9e5e856bdfc4/image7.jpg)

An example of a typographic scale defined in CSS:

<pre><code class="language-css">h1 {
  font-size: 48px;
}

h2 {
  font-size: 36px;
}

h3 {
  font-size: 24px;
}

h4 {
  font-size: 21px;
}

h5 {
  font-size: 18px;
}

h6 {
  font-size: 16px;
}

p {
  font-size: 14px;
}</code></pre>

## 8\. Clean Rags

When setting a block of text unjustified with a left or right alignment, be sure to keep the rag (the uneven side) balanced without any sudden "holes" or awkward shapes. A bad rag can be unsettling to the eye and distract the reader. A good rag has a "soft" unevenness, without any lines that are too long or too short. There is no way of controlling this in CSS, so to achieve a good rag you must make manual adjustments to the block of text.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e15119e-7a94-49be-8263-664c711ca490/image8.jpg)

<strong>Hyphenation</strong> can also help with producing clean rags, but unfortunately CSS can't handle this at the moment. Maybe in the near future we'll see <a href="https://www.w3.org/TR/css3-text/#hyphenate">some control in CSS 3</a>. Not all is lost though. There are some server and client side solutions for auto hyphenation like phpHyphenator and <a href="https://code.google.com/p/hyphenator/">Hyphenator</a> as well as <a href="https://yellowgreen.de/soft-hyphenation-generator">online generators</a>.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2643c21-d3f9-42be-948b-6bc662c67479/hp.gif)](https://code.google.com/p/hyphenator/) _[Hyphenator.js](https://code.google.com/p/hyphenator/) is a Javascript-library that implements an automatic client-side hyphenation of Web-pages._

## Further Resources

Here's a list of related articles and books to further help you with the details.

*   [Compose to a Vertical Rhythm](https://24ways.org/2006/compose-to-a-vertical-rhythm) Richard Rutter - 24 Ways
*   [Setting Type on the Web to a Baseline Grid](https://www.alistapart.com/articles/settingtypeontheweb) Wilson Minor - A List Apart
*   [Setting Web Type to a Baseline Grid](https://dev.opera.com/articles/view/setting-web-type-to-a-baseline-grid/) Craig Grannell - Opera
*   [The Elements of Typographic Style Applied to the Web](https://webtypography.net/) Robert Bringhurst
*   [How to Size Text in CSS](https://www.alistapart.com/articles/howtosizetextincss) Richard Rutter - A List Apart
*   [Baseline Rhythm Calculator](https://topfunky.com/baseline-rhythm-calculator/) Geoffrey Grosenbach
*   [Detail In Typography](https://www.amazon.com/Detail-Typography-Jost-Hochuli/dp/0907259340) Jost Hochuli
*   [The Elements of Typographic Style](https://www.amazon.com/Elements-Typographic-Style-Robert-Bringhurst/dp/0881791326) Robert Bringhurst
*   [Thinking with Type](https://www.amazon.com/Thinking-Type-Critical-Designers-Students/dp/1568984480) Ellen Lupton
*   [Grid Systems in Graphic Design](https://www.amazon.com/Systems-Graphic-Systeme-Visuele-Gestaltung/dp/3721201450) Josef Müller-Brockmann


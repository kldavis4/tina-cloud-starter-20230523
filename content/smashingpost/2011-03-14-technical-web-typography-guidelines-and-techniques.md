---
title: 'Technical Web Typography: Guidelines and Techniques'
slug: technical-web-typography-guidelines-and-techniques
image: null
date: 2011-03-14T13:00:46.000Z
author: harry-roberts
description: >-
  Unfortunately, for every person who is obsessed with even the tiniest details of typography, a dozen or so people seem to be indifferent. It’s a shame; if you’re going to spend time writing something, don’t you want it to look great and be easy to read?
categories:
  - Coding
  - Typography
  - CSS
  - Techniques
---
<em>Editor's Note: This article is a bit out of date — please proceed reading with caution.</em>

The Web is <a href="https://www.informationarchitects.jp/en/the-web-is-all-about-typography-period/">95% typography</a>, or so they say. I think this is a pretty accurate statement: we visit websites largely with the intention of reading. That’s what you’re doing now — reading. With this in mind, does it not stand to reason that your typography should be one of the most considered aspects of your designs?

Unfortunately, for every person who is obsessed with even the tiniest details of typography, a dozen or so people seem to be indifferent. It’s a shame; if you’re going to spend time writing something, don’t you want it to look great and be easy to read?

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Mind Your En And Em Dashes: Typographic Etiquette](https://www.smashingmagazine.com/2011/08/mind-your-en-and-em-dashes-typographic-etiquette/)
*   [Macrotypography For A More Readable Web Page](https://www.smashingmagazine.com/2012/05/applying-macrotypography-for-readable-web-page/)
*   [How To Choose A Typeface — A Step-By-Step Guide!](https://www.smashingmagazine.com/2011/03/how-to-choose-a-typeface/)
*   [Respect Thy Typography](https://www.smashingmagazine.com/2012/03/respect-thy-typography/)

{{% feature-panel %}}

### Creative and Technical Typography

I’m not sure these two categories are recognized in the industry but, in my mind, the two main types of typography are <em>creative</em> and <em>technical</em>.

<em>Creative typography</em> involves making design decisions such as which face to use, what mood the type should create, how it should be set, what tone it should have — for example, should it be airy, spacious and open (light) or condensed, bold and tight, with less white space (dark)? These decisions must be made on a per-project basis. You probably wouldn’t use the same font on a girl’s party invitation and an obituary. For me, this is creative typography: it is design-related and changes according to its application.

<em>Technical typography</em> is like type theory; certain rules and practices apply to party invitations just as well as they do to obituaries. These are little rules that always hold, are proven to work and are independent of design. The good news is that, because they are rules, even the most design-challenged people can make use of them and instantly raise the quality of their text from bog-standard to bang-tidy.

We’ll focus on technical type in this article. We’ll discuss the intricacies and nuances of a small set of rules while learning the code to create them.

We’ll learn about:

*   [How to choose a font face](#tt-face)
*   [How to choose a font size](#tt-font size)
*   [Using a grid](#tt-grid)
*   [Working out the measure](#tt-measure)
*   [Vertical rhythm and baseline grids](#tt-rhythm)
*   [Choosing a typographic scale](#tt-scale)
*   [How to use proper quotes](#tt-quotes)
*   [How to use proper dashes](#tt-dashes)
*   [How to use proper ellipses](#tt-ellipses)
*   [How to hang punctuation](#tt-hanging)
*   [Dealing with images in grids](#tt-images)

<em>Fair warning</em>: this is an in-depth article. It requires some basic CSS knowledge. If you’d rather learn a little at a time, use the links above to jump from section to section.

If any of the code examples seem out of context or confusing, then <span class="removed_link" title="https://www.smashingmagazine.com/wp-content/uploads/technical-type/index.html">here is the final piece</span> that we’re going to create (merely for your reference).</p>

## Setting Things Up

To begin, copy and paste this into an <em>index.html</em> file, and save it to your desktop:

<pre><code class="language-markup tmp-xml">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="utf-8" /&gt;
  &lt;title&gt;Your Name&lt;/title&gt;
  &lt;link rel="stylesheet" type="text/css" href="css/style.css" /&gt;
&lt;/head&gt;
&lt;body&gt;

  &lt;h1&gt;Your Name&lt;/h1&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre>

Next, copy and paste this (slightly modified) CSS reset into your <em>style.css</em> sheet, and save that to your machine, too:

<pre><code class="language-css">/*------------------------------------*
  RESET
*------------------------------------*/
body, div, dl, dt, dd, ul, ol, li,
h1, h2, h3, h4, h5, h6,
pre, form, fieldset, input, textarea,
p, blockquote, th, td { 
  margin: 0;
  padding: 0;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
fieldset, img {
  border: 0;
}
address, caption, cite, dfn, th, var {
  font-style: normal;
  font-weight: normal;
}
caption, th {
  text-align: left;
}
h1, h2, h3, h4, h5, h6 {
  font-size: 100%;
  font-weight: normal;
}
q:before, q:after {
  content: '';
}
abbr, acronym {
  border: 0;
}

/*------------------------------------*
  MAIN
*------------------------------------*/
html {
  background: #fff;
  color: #333;
}</code></pre>

## Choosing A Font Face

First, let’s choose a face in which to set our project. There is, as you know, a solid base of Web-safe fonts to choose from. There are also amazing services like <a href="https://fontdeck.com/">Fontdeck</a> and <a href="https://typekit.com/">Typekit</a> that leverage <code>@font-face</code> to add non-standard fonts in a fairly robust way.

We’re not going to use any of those, though. To prove that technical type can make <em>anything</em> look better, let’s restrict ourselves to a typical font stack.

Let’s use a serif stack for this project, because technical type works wonders on serif faces:

<pre><code class="language-css">html {
  font-family: Cambria, Georgia, "Times New Roman", Times, serif;
  background: #fff;
  color: #333;
}</code></pre>

Cambria is a beautiful font, specifically designed for on-screen reading and to be aesthetically pleasing when printed at small sizes. If you want to alter this or use a sans-serif stack, be my guest.</p>

### On Using Helvetica

If you’d like to use Helvetica in your stack, remember that Helvetica looks awful as body copy on a PC. To alleviate this, use the following trick to serve Helvetica to Macs and Arial to PCs (you can find more details about this trick in Chris Coyier's recent article <a href="https://css-tricks.com/sans-serif/">Sans-Serif</a>):

<pre><code class="language-css">html {
  font-family: sans-serif; /* Serve the machine’s default sans face. */
  background: #fff;
  color: #333;
}</code></pre>

Beware! This is a hack. It works by using a system’s default sans font as the font for the page. By default, a Mac will use Helvetica and a PC will use Arial. However, if a user has changed their system preferences, this will not be the case, so use with caution.

## Choosing A Font Size

Oliver Reichenstein authored <a title="The 100% Easy-2-Read Standard" href="https://www.informationarchitects.jp/en/100e2r/">an inspiring article</a>, way back in 2006, stating that the ideal size for type on the Web is 16 pixels: the user agents’ standard [2018 Update: it’s now being considered to be 22px_]. This insightful article changed the way I work with type; it’s well worth a read. We’ll use 16 pixels as a base size, then. If you want to use another font size, feel free, but if you stick with 16 pixels, your CSS should look something like this:

<pre><code class="language-css">html {
  font-family: Cambria, Georgia, "Times New Roman", Times, serif;
  background: #fff;
  color: #333;
}</code></pre>

If you want to use, say, 12 pixels, it will look like this:

<pre><code class="language-css">html {
  font-family: Cambria, Georgia, "Times New Roman", Times, serif;
  font-size: 0.75em; /* 16 * 0.75 = 12 */
  background: #fff;
  color: #333;
}</code></pre>

You’ll be left with a <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ded92d0-c922-428a-92b8-88129220fbc1/technical-web-typography-guidelines-and-techniques-01.jpg">basic layout (demo)</a>.</p>

## Choosing A Grid System

The grid is an amazing tool, and it’s not just for typographical ventures. It ensures order and harmony in your designs.

Some grid systems out there, in my opinion, go a little overboard and offer 30 or more columns, all awkwardly sized. For this tutorial, we’ll use <a href="https://sonspring.com/">Nathan Smith’s</a> 16-column <a href="https://960.gs/">960 Grid System</a> (<a href="https://960.gs/demo.html">demo</a>). 960.gs is amazing; its beauty lies in its simplicity. It is an ideal size for designs narrower than 1020 pixels, it has a good number of columns, and the numbers are easy to work with. You might also notice that the 960 Grid System only has 940 pixels of usable space. “960” comes from the 10 pixels of gutter space on either side.

Update your CSS to use a <span class="removed_link" title="https://www.smashingmagazine.com/wp-content/uploads/2011/03/technical-web-typography-guidelines-and-techniques-css/grid-01.png">guide background image</span>:

<pre><code class="language-css">html {
  font-family: Cambria, Georgia, "Times New Roman", Times, serif;
  background: url(…/img/css/grid-01.png) center top repeat-y #fff;
  color: #333;
  width: 940px;
  padding: 0 10px;
  margin: 0 auto;
}</code></pre>

You should now have something like this:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb840c54-579e-4490-943c-29c14483bc41/technical-web-typography-guidelines-and-techniques-02.jpg" alt="Screenshot" /></figure>

## Choosing A Measure

We have our font size, so now we need to work out our ideal line length, or “measure.” Robert Bringhurst writes in <em>The Elements of Typographic Style</em> that, “anything from 45 to 75 characters is widely regarded as a satisfactory length of line….”

A measure that is too short causes the eye to jump awkwardly from the end of line <em>x</em> to the start of line <em>x + 1</em>, and a measure that’s too long can cause the reader’s eye to double back. You can circumvent this somewhat by following these rules of thumb:

*   for a longer measure, use slightly greater [leading](#tt-rhythm);
*   for a shorter measure, use slightly smaller [leading](#tt-rhythm).

So, a measure of 45 to 75 characters is the optimum for readability in columns of text. I can pretty much guarantee that after you learn this, every massively, overly long measure you see on the Web will annoy you spectacularly.

Here are 69 characters, a nice middle ground between the recommended 45 and 75:

<pre><code class="language-markup tmp-xml">Lorem ipsum dolor sit amet, consectetuer adipiscing elit accumsan</code></pre>

Paste that into your page, and count how many red columns it covers. This is how wide your measure will be:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61e8f1ff-714a-4b29-bfb7-daf220f48e92/technical-web-typography-guidelines-and-techniques-03.jpg" alt="Screenshot" /></figure>

Here we have text spanning eight columns, which is 460 pixels of 960.gs. Update your CSS to read as follows:

<pre><code class="language-css">/*------------------------------------*
  MAIN
*------------------------------------*/

html {
  font-family: Cambria, Georgia, "Times New Roman", Times, serif;
  background: url(…/img/css/grid-01.png) center top repeat-y #fff;
  color: #333;
}

body {
  width: 460px;
  margin: 0 auto;
}</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c57d73a-1ee8-47a1-94dc-3118106931f1/technical-web-typography-guidelines-and-techniques-04.jpg" alt="Screenshot" /></figure>

If you picked a font size other than 16 pixels, make sure your measurements reflect this!

## Vertical Rhythm: Setting A Baseline

Leading (which rhymes with “wedding”) is a typographical term from way back when typographers manually set type in letterpress machines and the like. The term refers to the act of placing lead between lines of type in order to add vertical space. In CSS, we call this <code>line-height</code>.

Line height should be around 140%. This isn’t a great number to work with, and it’s only a general rule, so we’ll use 150% (or <code>1.5 em</code>). This way, we simply need to multiply the font size by one and a half to determine our leading.

Some general rules for leading:

*   with continuous copy, use large leading;
*   with light text on dark background, use large leading;
*   with long line lengths, use large leading;
*   with large _x_-height, use large leading;
*   with short burst of information, use small leading.

If you used a 16-pixel font size, then your line height will be 24 pixels (16 pixels × 1.5 em = 24 pixels). If you used a 12-pixel font size, then your line height will be 18 pixels (12 pixels × 1.5 em = 18 pixels).</p>

### The Magic Number

For math-based tips on typography, check out <a href="https://vimeo.com/17079380">this video on Web type</a> by Tim Brown. The fun starts at 13:35.

The pixel value for your line height (24 pixels) will now be your magic number. This number means <em>everything</em> to your design. All line heights and margins will be this number or multiples thereof. I find it useful to always keep it in mind and stick to it.

Now that we know our general line height, we can define a baseline grid. The grid we currently have aligns only the elements in the <em>y</em> axis (up and down). A baseline grid aligns in the <em>x</em> axis, too. We need to update our background image now to be 24 pixels high and have a solid 1-pixel line at the bottom, like <span class="removed_link" title="https://www.smashingmagazine.com/wp-content/uploads/2011/03/technical-web-typography-guidelines-and-techniques-css/grid.png"> this</span>.

Again, if you chose a font size of 12 pixels and your line height became 18 pixels, then your background image needs to be 18 pixels high with a solid horizontal line on the 18th row of pixels.

Your CSS should now look something like this:

<pre><code class="language-css">html {
  …
}

body {
  width: 460px;
  margin: 0 auto;
  line-height: 1.5em;
}</code></pre>

Your page should now look something like this:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb42e0ff-a2a1-4646-be94-8837ef766324/technical-web-typography-guidelines-and-techniques-05.jpg" alt="Screenshot" /></figure>

As you can see, the text hovers slightly above the horizontal guideline. This doesn’t mean that anything is set incorrectly; it is merely the offset. This could hinder the process, so either tweak the padding on the <code>body</code> to move the page or alter the position of the background image to move it around a little. Some tinkering in Firebug tells me that the CSS needs to be as follows:

<pre><code class="language-css">html {
  …
  background: url(…/img/css/grid.png) center -6px repeat-y #fff;
  …
}</code></pre>

That gives me the following — and everything lines up perfectly:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a98d5066-4ca7-4e68-a0fa-9f98441cba92/technical-web-typography-guidelines-and-techniques-06.jpg" alt="Screenshot" /></figure>

Now, let's get back to the magic number. Maybe you think the text is sitting too close to the top of the screen? Well, to remedy that, we’ll move the text down the page by a multiple of that magic number — let’s say 72 (3 × 24 = 72 pixels). Now adjust your CSS to read:

<pre><code class="language-css">body {
  width: 460px;
  margin: 0 auto;
  line-height: 1.5em;
  padding-top: 72px;
}</code></pre>

Substitute your own magic number if you used a different font size.

We should get this:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62da1272-e2de-46b7-9c04-fe865ecc61a6/technical-web-typography-guidelines-and-techniques-07.jpg" alt="Screenshot" /></figure>

It took some doing, but our canvas is ready at last!

## Setting A Scale

Okay, our reset has made our <code>h1</code> and <code>p</code> the same size. We need to get some basic font styles in there. Add this block of code to the end of your CSS:

<pre><code class="language-css">/*------------------------------------*
  TYPE
*------------------------------------*/
/*--- HEADINGS ---*/

h1, h2, h3, h4, h5, h6 {
  margin-bottom: 24px;
  font-weight: bold;
}

/*--- PARAGRAPHS ---*/

p {
  margin-bottom: 24px;
}</code></pre>

Recognize your magic number? Let's refresh the page and take a look:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a66d52bf-8b24-4918-87c4-766b6d23c65a/technical-web-typography-guidelines-and-techniques-08.jpg" alt="Screenshot" /></figure>

Your magic number will now be the default <code>margin-bottom</code> value for all of your elements. This, combined with the line height, will keep everything on the baseline grid.

What we now need, though, are some different font sizes for the headings. We need a typographic scale. I suggest this:

*   h1 = 24 pixels,
*   h2 = 22 pixels,
*   h3 = 20 pixels,
*   h4 = 18 pixels,
*   h5 = 16 pixels,
*   h6 = 16 pixels.

Many people work in pixels, but I much prefer working in ems. An em is proportional to the current size of the font: 1 em in 72-point Georgia is 72 points, and 1 em in 8-point Garamond is 8 points.

So, if our base font size is 16 pixels (1 em), then 24 pixels would be 1.5 ems (24 ÷ 16 = 1.5). If we continue, we end up with:

*   h1 = 24 pixels → 24 ÷ 16 = **1.5 ems**
*   h2 = 22 pixels → 22 ÷ 16 = **1.375 ems**
*   h3 = 20 pixels → 20 ÷ 16 = **1.25 ems**
*   h4 = 18 pixels → 18 ÷ 16 = **1.125 ems**
*   h5 = 16 pixels → 16 ÷ 16 = **1 ems**
*   h6 = 16 pixels → 16 ÷ 16 = **1 ems**

Next, we need to make sure the line height of each is 24 pixels. This means that the <code>h1</code> at a 24-point font size will have a line height of 1 em. Here’s the math:
<blockquote>(magic number) ÷ (font size) = (line height)</blockquote>

Using our scale, the full CSS for the headings (including the math) is:

<pre><code class="language-css">/*--- HEADINGS ---*/
h1, h2, h3, h4, h5, h6 {
  margin-bottom: 24px;
  font-weight: bold;
}

h1 {
  font-size: 1.5em; /* 24px --&gt; 24 ÷ 16 = 1.5 */
  line-height: 1em; /* 24px --&gt; 24 ÷ 24 = 1 */
}

h2 {
  font-size: 1.375em; /* 22px --&gt; 22 ÷ 16 = 1.375 */
  line-height: 1.0909em; /* 24px --&gt; 24 ÷ 22 = 1.090909(09) */
}

h3 {
  font-size: 1.25em; /* 20px --&gt; 20 ÷ 16 = 1.25 */
  line-height: 1.2em; /* 24px --&gt; 24 ÷ 20 = 1.2 */
}

h4 {
  font-size: 1.125em; /* 18px --&gt; 18 ÷ 16 = 1.125 */
  line-height: 1.333em; /* 24px --&gt; 24 ÷ 18 = 1.3333333(3) */
}

h5, h6 {
  font-size: 1em; /* 16px --&gt; 16 ÷ 16 = 1 */
  line-height: 1.5em; /* 24px --&gt; 24 ÷ 16 = 1.5 */
}</code></pre>

There’s our typographic scale.

Now, to test it, let’s try the following markup:

<pre><code class="language-markup tmp-xml">&lt;body&gt;

  &lt;h1&gt;Your Name&lt;/h1&gt;

  &lt;h2&gt;Your Name&lt;/h2&gt;

  &lt;h3&gt;Your Name&lt;/h3&gt;

  &lt;h4&gt;Your Name&lt;/h4&gt;

  &lt;h5&gt;Your Name&lt;/h5&gt;

  &lt;h6&gt;Your Name&lt;/h6&gt;

  &lt;p&gt;Lorem ipsum dolor sit amet, consectetuer adipiscing elit accumsan&lt;/p&gt;

&lt;/body&gt;</code></pre>

You might notice that not all of the lines of text sit perfectly on a gridline, but that’s okay because they all honor the baseline! This is what I get:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/549d74ff-f09f-4552-9857-305560441b51/technical-web-typography-guidelines-and-techniques-09.jpg" alt="Screenshot" /></figure>

You might think that something has gone wrong. But if you look, the paragraph lies just fine once you get back to the normal font size. To be honest, I’m not entirely sure about what causes this effect; the numbers we used are all correct, and the vertical rhythm as a whole remains intact, but individual lines of larger text appear to be offset from the baseline. I think this could be due, in part, to the glyphs’ setting in their em box.</p>

## What Next?

Head back into your markup and remove everything except the <code>h1</code>. Now we’re ready to do something useful. Let’s make a little "About you"-page.

The <code>h1</code> is the name. And the markup can simply be:

<pre><code class="language-markup tmp-xml">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="utf-8" /&gt;
  &lt;title&gt;Harry Roberts&lt;/title&gt;
  &lt;link rel="stylesheet" type="text/css" href="css/style.css" /&gt;
&lt;/head&gt;

&lt;body&gt;

  &lt;h1&gt;Harry Roberts&lt;/h1&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre>

Now let's add a little introductory paragraph about yourself. Mine reads:

<pre><code class="language-markup tmp-xml">&lt;p&gt;Hi there. My name is Harry Roberts.
I am a Web developer and type geek from the UK.
I love all things Web dev, and I am a huge advocate
of Web standards and proper ethics.&lt;/p&gt;</code></pre>

Let’s experiment with altering the font size arbitrarily. Add this to your CSS:

<pre><code class="language-css">*--- PARAGRAPHS ---*/
p {
  margin-bottom: 24px;
}

body &gt; p:first-of-type {
  font-size: 1.125em;
    /* 18px → 18 ÷ 16 = 1.125 */

  line-height: 1.333em;
    /* 24px → 24 ÷ 18 = 1.3333(3) */
}</code></pre>

Here we’re giving the first paragraph — a direct descendant of the <code>body</code> element — a font size of 18 pixels and a line height of 24 pixels. See, there’s your magic number again!

You might again see slight oddities with the paragraph sitting on the baseline. To make sure the vertical rhythm is still intact, duplicate the paragraph once more. You should get this:

<figure class="fwi"><a href="#"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91abecde-a46d-4590-b659-0068795f85bd/technical-web-typography-guidelines-and-techniques-10.jpg" alt="A screenshot of Harry’s demo" /></a><figcaption>Here you can see that the vertical rhythm is still intact and working correctly.</figcaption></figure>

<p>Now for the best bits.</p>

## Tips on Technical Typography

There’s a good chance that you won’t want the grid to always be on, so change this CSS:

<pre><code class="language-css">/*------------------------------------*
  MAIN
*------------------------------------*/

html {
  font-family: Cambria, Georgia, "Times New Roman", Times, serif;
  background: url(…/img/css/grid.png) center -6px repeat-y #fff;
  color: #333;
}

body {
  width: 460px;
  margin: 0 auto;
  line-height: 1.5em;
  padding-top: 72px;
}</code></pre>

… to this:

<pre><code class="language-css">/*------------------------------------*
  MAIN
*------------------------------------*/

html {
  font-family: Cambria, Georgia, "Times New Roman", Times, serif;
  color: #333;
}

body {
  width: 460px;
  margin: 0 auto;
  line-height: 1.5em;
  padding-top: 72px;
  background: #fff;
}

body:hover {
  background: url(…/img/css/grid.png) center -6px repeat-y #fff;
}</code></pre>

This will show the grid when you hover over the <code>body</code>, and hide it when you don’t.
## Spacing And Setting Paragraphs

We’ve sorted out the magic number, and we know we should use it to space the elements, but there’s more than one way to denote the beginning of a new paragraph. One is the method we’re already using: inserting a blank space (one magic number) between the paragraphs. The second is indentation.

Typically, you would indent every paragraph except the first in a body of text; the first paragraph has no indent and the second, third, fourth and so on do have an indent (typically with a width of 1 em).

Enric Jardi writes in <em>Twenty-Two Tips on Typography</em> that, “… you must not use both indentation and a line break at the same time; that is redundant.”

Here’s some quick CSS for indenting only the second and subsequent paragraphs in a body of text:

<pre><code class="language-css">p {
  margin-bottom: 24px;
}

p+p {
  text-indent: 1em;
  margin-top: -24px;
}</code></pre>

For an explanation of how and why this works, refer to my other article, “<a href="https://csswizardry.com/2010/12/mo-robust-paragraph-indenting/">Mo’ Robust Paragraph Indenting</a>.” You might also want to look at <a href="https://jontangerine.com/silo/typography/p/">Jon Tan’s silo</a>.

### Alignment

When setting type on the Web, use a range-left, ragged-right style. This basically means left-justifying the type. If you use a sufficiently long measure, then your rags (the uneven edges on the right side of a left-aligned paragraph) will generally be clean; the raggedness of their appearance can, however, be exacerbated at short measures, where a large percentage of each line could end up as white space.

Justified typesetting can look great but lead to unsightly “rivers” in the text. To avoid this, rewrite the copy to remove them, or use something like <a href="https://code.google.com/p/hyphenator/">Hyphenator.js</a>, which is remarkably effective.
## Proper Quotations Marks, Dashes And Ellipses

### Quotation Marks

Many people are unaware that there are proper quotation marks and “ambidextrous” quotation marks. The single- and double-quotation keys on your keyboard are not, in fact, true quotation marks. They are catch-alls that can function as both left and right single and double quotation marks; they are, essentially, four glyphs in one key.

The reason behind this is simply space. A keyboard cannot feasibly fit proper left and right single and double quotation marks.

So, what is a proper quotation mark? A curly (or “book”) quotation mark is rounded and more angular than an ambidextrous (keyboard-style) quotation mark. Left single and left double quotation marks look like this: ‘ and “ (<code>&amp;lsquo;</code> and <code>&amp;ldquo;</code>, respectively). Right single and right double quotation marks look like this: ’ and ” (<code>&amp;rsquo;</code> and <code>&amp;rdquo;</code>, respectively).

Many people incorrectly refer to ambidextrous quotation marks as “primes,” but a prime is a different glyph. Single and double primes look like this: ′ and ″ (<code>&amp;prime;</code> and <code>&amp;Prime;</code>, respectively). They are used to denote feet and inches (e.g. 5′10″).

I said that one key incorporates four glyphs. In fact, two keys incorporate six glyphs.

### Which Quotation Marks Should You Use?

The type of quotation marks to use (double or single) varies from country to country and style guide to style guide. Double quotation marks are typically used to quote a written or spoken source, and single quotation marks are used for quotes within quotes.

However, I much prefer Jost Hochuli’s advice in <em><a href="https://www.dealpond.com/books/compare/0907259340">Detail in Typography</a></em>: “… the appearance is improved by using the more obtrusive double quotation marks for the less frequent quotations within quotations.” Which basically means, for a nicer appearance, use single quotation marks, and then double quotation marks for quotes within quotes. (If I had a penny for every time I said <em>quotes</em> in this section.)

For example:
<blockquote>‘And then he said to me, “Do you like typography?” And naturally I said that I did.’</blockquote>

Use a right single quotation mark where you’d normally use an apostrophe in text: “I’m a massive typography nerd!” (<code>I&amp;rsquo;m a massive typography nerd!</code>)

In short, stop using those horrible keyboard quotation marks, and start using lovely curly marks in your work.

### Non-English Quotation Marks

The quotation marks we’ve covered are used in English, but quotes look different in other languages.

French and Spanish use <em>guillemets</em>, «like this» (<code>&amp;laquo;like this&amp;raquo;</code>). In Danish, they are used »like this« (<code>&amp;raquo;like this&amp;laquo;</code>). In German, using a combination of bottom and regular double quotation marks is common, „like this“ (<code>&amp;bdquo;like this&amp;ldquo;</code>).

For a great overview of other non-English quotation marks, see the Wikipedia entry on “<a href="https://en.wikipedia.org/wiki/Non-English_usage_of_quotation_marks">Non-English Usage of Quotation Marks</a>.”
### Dashes

We know that keyboards can’t accommodate all quotation marks; and they can’t accommodate all types of dashes either. The hyphen key (-) is another catch-all. There are three main types of dash: the em dash, en dash and hyphen.

The em dash (<code>&amp;mdash;</code>) denotes a break in thought—like this. It’s called the “em” dash because, traditionally, it is one em wide. Em dashes are usually set without spaces on either side (as above).

The en dash (<code>&amp;ndash;</code>) is traditionally half the width of an em dash. It is used to denote ranges, as in “please read pages 17–25” (<code>17&amp;ndash;25</code>). It can also denote relational phrases, as in “father–son” or “New York–London.”

The hyphen simply ties together compound words, as in “front-end developer.”

The em dash, en dash and hyphen are different, and each has unique uses.
### Ellipsis

An ellipsis is used to denote a thought trailing off. It is also used as a placeholder for omitted text in lengthy quotations.

The ellipsis has become the bane of my life. I often come across people who use a series of dots (periods) in place of a proper ellipsis, like so......

An ellipsis is not three dots. It is <strong>one glyph</strong> that looks like three dots. Its HTML entity is <code>&amp;hellip;</code> (as in horizontal ellipsis).

So there were a few glyphs for you to use with quotes, primes, dashes and ellipses. Let’s recap:
<table id="tt-punctuation">
<thead>
<tr>
<th>Name/Glyph</th>
<th>HTML entity</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr id="tt-summary-quotes">
<th colspan="3">Quotes and primes</th>
</tr>
<tr>
<td>Left single quote ‘ and right single quote ’</td>
<td><code>&amp;lsquo;</code> and <code>&amp;rsquo;</code></td>
<td>‘Hey, this is a quote!’</td>
</tr>
<tr>
<td>Left double quote “ and right double quote ”</td>
<td><code>&amp;ldquo;</code> and <code>&amp;rdquo;</code></td>
<td>‘Hey, this is a quote “within another” quote!’</td>
</tr>
<tr>
<td>Single prime ′ and double prime ″</td>
<td><code>&amp;prime;</code> and <code>&amp;Prime;</code></td>
<td>The girl is 7′10″!</td>
</tr>
<tr id="tt-summary-dashes">
<th colspan="3">Dashes</th>
</tr>
<tr>
<td>Em dash —</td>
<td><code>&amp;mdash;</code></td>
<td>A break in thought—like this</td>
</tr>
<tr>
<td>En dash –</td>
<td><code>&amp;ndash;</code></td>
<td>Ages 2–5</td>
</tr>
<tr>
<td>Hyphen -</td>
<td>- key</td>
<td>front-end developer</td>
</tr>
<tr id="tt-summary-ellipses">
<th colspan="3">Ellipsis</th>
</tr>
<tr>
<td>Ellipsis …</td>
<td><code>&amp;hellip;</code></td>
<td>To be continued…</td>
</tr>
</tbody>
</table>

In addition to these common glyphs, there are numerous others: from the division symbol (÷ or <code>&amp;divide;</code>) to the section symbol (§ or <code>&amp;sect;</code>). If you’re interested in special characters and glyphs, then Wikipedia’s article on “<a href="https://en.wikipedia.org/wiki/Punctuation">Punctuation</a>” is a good place to start (just keep clicking from there).
## Hanging Punctuation

Punctuation should be hung; quotation marks and bullet points should be clear of the edges of surrounding text. If that doesn’t make sense, don’t worry! Let’s add a new section to your page. Remove that duplicated paragraph and replace it with a list of facts about yourself. Mine looks like this:

<pre><code class="language-markup tmp-xml">&lt;ul&gt;
  &lt;li&gt;
    Web development
    &lt;ul&gt;
      &lt;li&gt;HTML(5)&lt;/li&gt;
      &lt;li&gt;CSS(3)&lt;/li&gt;
      &lt;li&gt;Accessibility&lt;/li&gt;
      &lt;li&gt;Progressive enhancement&lt;/li&gt;
    &lt;/ul&gt;
  &lt;/li&gt;
  &lt;li&gt;
    Web design
    &lt;ul&gt;
      &lt;li&gt;Typography&lt;/li&gt;
      &lt;li&gt;Grids&lt;/li&gt;
    &lt;/ul&gt;
  &lt;/li&gt;
&lt;/ul&gt;</code></pre>

Add this to the end of your CSS sheet:

<pre><code class="language-css">/*--- LISTS ---*/
ul, ol {
  margin-bottom: 24px;
    /* Remember, if your magic number is
    different to this, use your own. */
}

ul {
  list-style: square outside;
}

ul ul,
ol ol {
  margin: 0 0 0 60px;
}</code></pre>

My page now looks like this:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c4b708b-a892-4f03-8125-738b07d51d53/technical-web-typography-guidelines-and-techniques-11.jpg" alt="Screenshot" /></figure>We’ve given the lists our magic number as a margin, set the bullets to be hung outside of the text (i.e. the bullets will sit in the white of the gutter, not the pink of the column) and indented lists within lists by one grid column.

Experiment by nesting lists more and more deeply:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1b0c51c-f083-44d5-bcf1-b31a4e12c9cd/technical-web-typography-guidelines-and-techniques-12.jpg" alt="Screenshot" /></figure>Hang quotation marks as well as bullets. Let’s add some more text and a quote to our page:

<pre><code class="language-markup tmp-xml">&lt;p&gt;Vestibulum adipiscing lectus ut risus adipiscing
mattis sed ac lectus. Cras pharetra lorem eget diam
consectetur sit amet congue nunc consequat. Curabitur
consectetur ullamcorper varius. Nulla sit amet sem ac
velit auctor aliquet. Quisque nec arcu non nulla adipiscing
rhoncus ut nec lorem. Vestibulum non ipsum arcu. Quisque
dapibus orci vitae massa fringilla sit amet viverra nulla.&lt;/p&gt;

&lt;blockquote&gt;

  &lt;p&gt;&amp;ldquo;Lorem ipsum dolor sit amet,
  consectetuer adipiscing elit. In accumsan diam
  vitae velit. Aliquam vehicula, turpis sed egestas
  porttitor, est ligula egestas leo, at interdum
  leo ante ut risus.&amp;rdquo;
  &lt;b&gt;&amp;mdash;Joe Bloggs&lt;/b&gt;&lt;/p&gt;

&lt;/blockquote&gt;</code></pre>

The markup here is pretty straightforward: a <code>blockquote</code> surrounding a paragraph. You might also notice the use of a <code>b</code> element to mark up the name. The <a href="https://html.spec.whatwg.org/multipage/semantics.html#the-b-element">HTML spec</a> states that “The <code>b</code> element [is used for] spans of text whose typical typographic presentation is boldened.” This is a loose definition, so its use for bolding the name of a person is acceptable.

Now, add this to the end of your CSS sheet:

<pre><code class="language-css">/*--- QUOTES ---*/
blockquote {
  margin: 0 60px 0 45px;
  border-left: 5px solid #ccc;
  padding-left: 10px;
  text-indent: -0.4em;
}

blockquote b {
  display: block;
  text-indent: 0;
}</code></pre>

Here we indent the quote by 60 pixels from the left and right (i.e. 45-pixel margin + 5-pixel border + 10-pixel padding = 60 pixels), taking it in by one column of the grid. We then use a negative <code>text-indent</code> to make the opening quote hang outside of the body of text. The number I used works perfectly for Cambria, but you can experiment with the font of your choice. (Don’t forget to remove the <code>text-indent</code> on the <code>b</code>.) Now we know how to hang bullets and quotation marks.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8aefe07-eb34-4c8a-83bc-53b8f1bbaef6/technical-web-typography-guidelines-and-techniques-13.jpg" alt="Screenshot" /></figure>Maybe you’re wondering why I’m using double quotation marks here after recommending single quotation marks. The reason is purely aesthetic. Hanging double quotation marks in <code>blockquote</code> tags simply looks nicer.
## Guillemets

<p>Now that we’ve done that, let’s add a “Read more” link to get us from this little page to, say, our portfolio’s full “About” page. We want to imply direction or movement with this link because it’s going to take us elsewhere. We could, as many people do, use a <a href="https://en.wikipedia.org/wiki/Guillemets">guillemet</a> (», <code>&amp;raquo;</code>), but — as we covered earlier — French, German and <a href="https://en.wikipedia.org/wiki/Guillemets#Uses">other languages</a> use this glyph as a quotation mark. Therefore, it shouldn’t be used stylistically. Add this markup to your page:</p>

<pre><code class="language-markup tmp-xml">&lt;p&gt;&lt;a href="https://csswizardry.com/about/"
class="read-more"&gt;Read more&lt;/a&gt;&lt;/p&gt;</code></pre>

Add this to the end of your CSS file:

<pre><code class="language-css">/*--- LINKS ---*/
a {
  color: #09f;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

a:active,
a:focus {
  position: relative;
  top: 1px;
}

.read-more:after {
  content: "0A000BB"; /* Insert a space then right angled-quote */
}</code></pre>

This simply places <a href="https://www.evotech.net/articles/testjsentities.html">an encoded space and right-angled quotation mark</a> after the “Read more” link by using CSS, which means you don’t have to add that quotation mark to your markup.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3145e81-56c5-4c1a-ab10-cefa035ac57c/technical-web-typography-guidelines-and-techniques-14.jpg" alt="Screenshot" /></figure>You can use <code>content:"";</code> to <a href="https://csswizardry.com/2010/09/keeping-code-clean-with-content/">keep the markup clean</a>. This means that other things, such as stylistic right-angled quotation marks and other decorative items of type, can be added with CSS to keep the markup free of non-semantic elements.

Let’s say you wanted to add tildes to either side of a heading:

<pre><code class="language-css">h1 {
  text-align: center;
}
h1:before {
  content: "07E0A0"; /* Insert an tilde, then a space. */
}
h1:after {
  content: "0A007E"; /* Insert a space, then an tilde. */
}</code></pre>

## Some Images

Elements such as tables and images are notoriously difficult to fit into baseline grids unless you save every one as a multiple of your magic number. However, we can float images left and right within the <em>y</em> axis of the grid and allow text to fit the baseline around it. Grab an image of yourself (or your cat or whatever) and crop it to a width that fits our <a href="https://960.gs/demo.html">16-column 960.gs</a>. I’m going to use a 160-pixel-wide image (i.e. three grid columns).

Place it in the markup just after your <code>h1</code>, thus:

<pre><code class="language-markup tmp-xml">…
&lt;body&gt;

  &lt;h1&gt;Harry Roberts&lt;/h1&gt;

  &lt;img src="img/me.jpg" alt="A photo of me." id="me" /&gt;</code></pre>

If you hit “Refresh” now, it will likely break the baseline. Never fear — add this CSS:

<pre><code class="language-css">/*------------------------------------*
  IMAGES
*------------------------------------*/

#me {
  float: right;
  margin: 0 0 0 20px;
  display: block;
  width: 148px;
  height: auto;
  padding: 5px;
  border: 1px solid #ccc;

  -moz-border-radius: 2px;
  -webkit-border-radius: 2px;
  -o-border-radius: 2px;
  border-radius: 2px;
}</code></pre>

Notice how the image doesn’t appear to sit on the baseline, but the rest of the text does? Beautiful, isn't it?

So, there you have it. Using nothing more than plain ol’ browser text, one image, a lot of typography knowledge and some careful, caring attention, you’ve made a full page of typographic splendor — a page that uses a grid, a baseline, proper punctuation and glyphs, an ideal measure and leading and a typographic scale.

Now get in there! Add elements, subtract them, add colors, add your own creative type. Just remember the few simple rules and your magic number, and you’re away!

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9120d8b-5016-46f6-b78a-29918c70ad8e/technical-web-typography-guidelines-and-techniques-15.jpg" alt="Screenshot" /><br>
<figcaption>The final piece, with the grid.</figcaption></figure><figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7fd355b-b736-4731-81b0-c70535ddd5ba/technical-web-typography-guidelines-and-techniques-16.jpg" alt="Screenshot" /><br>
<figcaption>The final piece, without the grid.</figcaption></figure>

## Final Words

In this admittedly long piece, we have discussed only <em>technical</em> typography. Everything in this article can be applied to almost any project. None of it was speculation; these are tried and tested methods and proven tips for beautiful Web type.

If you’d like to see more creative applications of Web type, then check out the work of the following creatives (each of whom has had much influence on my career so far):
<ul>
 	<li>Oliver Reichenstein of <a href="https://informationarchitects.jp/">Information Architects</a>
A huge inspiration to me and a very knowledgeable guy who has a passion and talent for readable, sensible and beautiful type on the Web.</li>
 	<li><a href="https://jontangerine.com/">Jon Tan</a>
Jon’s website is gorgeous. He is a member of the International Society of Typographic Designers (ISTD), and his writings and “silo” (on his personal website) are a hive of typographical information.</li>
 	<li><a href="https://exljbris.com/">Jos Buivenga</a>
Not strictly a Web-type guy, but Jos is the creator of some of the most beautiful (and free!) fonts in existence. His work got me hooked on typography.</li>
 	<li><a href="https://www.subtraction.com/">Khoi Vinh</a>
His timelessly beautiful website spurred my love for grids. He also recently wrote <a href="https://www.dealpond.com/books/compare/0321703537">a book</a> on that very subject.</li>
</ul>
Keep in mind that you don’t have to be the world’s best designer to create beautiful type. You just have to <em>care</em>.

### Further Reading

<ul>
 	<li><a href="https://www.dealpond.com/books/compare/0881792063"><em>The Elements of Typographic Style</em></a></li>
 	<li><a href="https://www.dealpond.com/books/compare/0907259340"><em>Detail in Typography</em></a></li>
 	<li><a href="https://ilovetypography.com/">I Love Typography</a></li>
 	<li><a href="https://jontangerine.com/">Jon Tangerine</a></li>
 	<li><a href="https://www.markboulton.co.uk/">Mark Boulton</a></li>
</ul>

{{< signature "al" >}}

</figure>


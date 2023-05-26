---
title: The Perfect Paragraph
slug: the-perfect-paragraph
image: null
date: 2011-11-29T15:35:29.000Z
author: heydon-pickering
description: >-
  In this article, I’d like to reacquaint you with the humble workhorse of communication that is the paragraph. Paragraphs are everywhere. In fact, at the high risk of stating the obvious, you are reading one now. Despite their ubiquity, **we frequently neglect their presentation**. This is a mistake.
categories:
  - UX
  - Typography
  - Design
  - CSS
---
This is a mistake. Here, we’ll refer to some time-honored typesetting conventions, with an <strong>emphasis on readability</strong>, and offer guidance on adapting them effectively for devices and screens. We’ll see that the ability to embed fonts with <code>@font-face</code> is not by itself a solution to all of our typographic challenges.

Be sure to check out the following articles:

*   [8 Simple Ways to Improve Typography In Your Designs](https://www.smashingmagazine.com/2009/04/8-simple-ways-to-improve-typography-in-your-designs/)
*   [How To Become a Better Reader](https://www.smashingmagazine.com/2011/02/become-better-reader/)
*   [Photoshop-Inspired Techniques with 100% CSS](https://www.smashingmagazine.com/2010/11/photoshop-inspired-techniques-100-css/)
*   [Applying Macrotypography For A More Readable Web Page](https://www.smashingmagazine.com/2012/05/applying-macrotypography-for-readable-web-page/)

## A Web Of Words

In 1992, Tim Berners-Lee circulated a document titled “<a href="https://www.w3.org/History/19921103-hypertext/hypertext/WWW/MarkUp/Tags.html">HTML Tags</a>,” which outlined just 20 tags, many of which are now obsolete or have taken other forms. The first surviving tag to be defined in the document, after the crucial anchor tag, is the paragraph tag. It wasn’t until 1993 that a <a href="https://1997.webhistory.org/www.lists/www-talk.1993q1/0182.html">discussion emerged</a> on the proposed image tag.

{{% feature-panel %}}

Bursting with imagery, motion, interaction and distraction though it is, today’s World Wide Web is still primarily a conduit for textual information. In HTML5, the <strong>focus on writing and authorship</strong> is more pronounced than ever. It’s evident in the very way that new elements such as <code>article</code> and <code>aside</code> are named. HTML5 asks us to treat the HTML document more as… well, a document.

It’s not just the specifications that are changing, either. Much has been made of <a href="https://googlewebmastercentral.blogspot.com/2011/04/high-quality-sites-algorithm-goes.html">permutations to Google’s algorithms</a>, which are beginning to favor better written, more authoritative content (and making work for the growing <a href="https://www.alistapart.com/articles/thedisciplineofcontentstrategy/">content strategy</a> industry). Google’s bots are now charged with <a href="https://googlewebmastercentral.blogspot.com/2011/05/more-guidance-on-building-high-quality.html">asking questions</a> like, “Was the article edited well, or does it appear sloppy or hastily produced?” and “Does this article provide a complete or comprehensive description of the topic?,” the sorts of questions one might expect to be posed by an earnest college professor.

This increased support for quality writing, allied with the book-like convenience and tactility of smartphones and tablets, means there has never been a better time for reading online. The remaining task is to make the writing itself a joy to read.</p>

## What Is The Perfect Paragraph?

As designers, we are frequently and incorrectly reminded that our job is to “make things pretty.” We are indeed designers — not artists — and there is no place for <a href="https://en.wikipedia.org/wiki/Formalism_%28art%29">formalism</a> in good design. Web design has a function, and that function is to <a href="https://www.lukew.com/ff/entry.asp?232">communicate the message</a> for which the Web page was conceived. The medium is not the message.

Never is this principle more pertinent than when dealing with type, the bread and butter of Web-borne communication. A well-set paragraph of text is not supposed to wow the reader; the wowing should be left to the idea or observation for which the paragraph is a vehicle. In fact, <strong>the perfect paragraph is unassuming</strong> to the point of near <a href="https://speakerdeck.com/u/smashingmag/p/the-invisible-side-of-design">invisibility</a>. That is not to say that the appearance of your text should have no appeal at all. On the contrary: well-balanced, comfortably read typography is a thing of beauty; it’s just not the <em>arresting</em> sort of beauty that might distract you from reading.

<a href="https://www.flickr.com/photos/mwichary/2251302479/sizes/l/in/photostream/"><img loading="lazy" decoding="async" class="109379" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91c595b0-0a04-430b-bd7c-54be130903a5/press.jpg" alt="Archaic Typographic Implements" width="500" height="330" /></a><br>
<em>(Image: <a href="https://www.flickr.com/photos/mwichary/2251302479/sizes/l/in/photostream/">Marcin Wichary</a>)</em>

As a young industry that champions innovation and rates its practitioners based on their ability to apprehend (sorry, “grok”) the continual emergence of new technologies, frameworks, protocols and data models, we are not particularly familiar with tradition. However, the practice of arranging type for optimal pleasure and comfort is a centuries-old discipline. As long ago as 1927, the noted typographer <a href="https://en.wikipedia.org/wiki/Jan_Tschichold">Jan Tschichold</a> spoke of the typesetting “methods and rules upon which it is impossible to improve” — a set of rules it would be foolish to ignore.

So, please put your <code>canvas</code> element and data visualization <abbr title="Application Programming Interface">API</abbr> to one side just for a short while. We are about to spend a little time brushing up on our typesetting skills. It’s called “hyper<em>text</em>,” after all.</p>

## Setting Your Paragraphs

### The Typeface

Your choice of font is important, but the <em>kind</em> of “family” you choose is project-specific, and we won’t discuss it here except to make one point: the conventional wisdom among Web designers that only <a href="https://en.wikipedia.org/wiki/Sans-serif">sans-serif</a> fonts are suitable for body text is just a rule of thumb. Although serif fonts, with their greater complexity, may tend to be less effective at small sizes, there are many other factors to consider. A diminutive <a href="https://en.wikipedia.org/wiki/X-height">x-height</a>, for example, could impair the readability of a font from either camp. Some serif fonts are highly legible and attractive for paragraph text if they are set properly. <a href="https://en.wikipedia.org/wiki/Matthew_Carter">Matthew Carter’s</a> screen-sympathetic <a href="https://www.will-harris.com/verdana-georgia.htm">Georgia</a> is a case in point.

<a href="https://www.flickr.com/photos/adactio/5739318101/sizes/l/in/photostream/"><img loading="lazy" decoding="async" class="109380" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27f0409c-1189-43d1-a89e-342c752a4ad8/x-height2.jpg" alt="Typographic Anatomy" width="500" height="330" /></a><br>
<em>X-height is the distance between the baseline and midline — a measure of lowercase character height. (Image: <a href="https://www.flickr.com/photos/adactio/5739318101/sizes/l/in/photostream/">adactio</a>)</em>

Having dispensed with the subject of preference, let’s cover some important technical issues relating to one’s choice of typeface.

The first thing to consider when choosing a Web font (read: <code>@font-face</code> font) is <strong>the breadth of the family</strong>. Does the font include all of the necessary bold, italic (or even better, semi-bold and bold-italic) styles? One style is fine for headings, but paragraphs need greater variety. Without these variations at your disposal, not only will your text look insipid, but the lack of proper emphasis will make your writing difficult to follow.

<a href="https://www.fontsquirrel.com/fonts/Bitstream-Vera-Sans"><img loading="lazy" decoding="async" class="109408" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2173945-f637-4dab-bc1f-a93a53235149/h-bitstream.jpg" alt="bitstream" width="500" height="123" /></a><br>
<em>I personally don’t like <a href="https://www.fontsquirrel.com/fonts/Bitstream-Vera-Sans">Bitstream</a>, but it is fully functional for paragraph text</em>

With the full gamut of stylistic variations at your disposal, you will not have to rely on the unsatisfactory “faux” styles that are applied to a regular font when <code>font-style: italic</code> or <code>font-weight: bold</code> is called. Typefaces are not designed to be contorted in this way. Using the proper styles provided by a family like Bitstream (above) will make your typography not only more attractive but more accessible: dedicated italic glyphs have a <strong>much clearer intent</strong> than text that is simply “leaned over a bit.”

The trick is to make sure that the declaration of, for example, <code>font-style: italic</code> requests the italic resource rather than triggers the faux style. It should be as effortless as using a system font family such as Georgia. This is probably best explained, like so many things, in commented code. For brevity, we’ll set up just a regular font and an italic (not bold) style variation.

<pre><code class="language-css">@font-face {
   font-family: 'MyWebfont';  /* Change this to whatever you like. */
   src: url('mywebfont-regular.ttf') format('truetype');  /* The "regular" font resource. */
   font-style: normal;  /* Associates values of "normal" with this resource. */
   font-weight: normal;  /* As above for weight. */
}

@font-face {
   font-family: 'MyWebfont';  /* Importantly, the same as in the above block; the family name. */
   src: url('mywebfont-italic.ttf') format('truetype');
   font-style: italic;  /* Associates values of "italic" with this resource. */
   font-weight: normal;  /* ... It's not a bold-italic font style. */
}

body {
   font-family:'MyWebfont', georgia, serif;  /* Provides a system font fallback. */
}

em {
   font-style: italic;  /* If @font-face is supported, the italic Web font is used. If not, the italic Georgia style is lifted from the user's computer. Either way, a faux style is not allowed to creep in. */
}</code></pre>

Our second typeface consideration <strong>relates to rendering</strong>. Some fonts, replete with beautiful glyphs and exceptional <a href="https://type.method.ac/">kerning</a> as they may be, simply don’t render very well at small sizes. You will have noticed that embedded fonts are often reserved for headings, while system fonts (such as <a href="https://en.wikipedia.org/wiki/Verdana">Verdana</a> here) are relied on for body text.

One of the advantages of Verdana is that it is a “well-hinted” font. <a href="https://www.fontshop.com/glossary.php?def=Delta%20hinting">Delta hinting</a> is the provision of information within a font that specifically enhances the way it renders at small sizes on screen. The smaller the font, the fewer the pixels that make up individual glyphs, requiring intelligent reconfiguration to keep the font legible. It’s an art that should be familiar to any Web designer who’s ever tried to make tiny icons comprehensible.

Hinting is a tricky and time-consuming process, and not many Web fonts are hinted comprehensively. Note the congealed upper portion of the <a href="https://www.fontshop.com/glossary.php?ltr=b">bowl</a> in the lowercase “b” in the otherwise impressive <a href="https://www.fontsquirrel.com/fontfacedemo/Crimson">Crimson</a> font, for instance. This small unfortunate glitch is distracting and slightly detracts from a comfortable reading experience. The effect is illustrated below and can be seen in context <a href="https://www.fontsquirrel.com/fontfacedemo/Crimson">as a demo</a>.

<img loading="lazy" decoding="async" class="109409" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25511e92-f490-418e-873e-0bf5d40c7a6d/h-hinting.jpg" alt="Unsatisfactory Hinting" width="500" height="123" /><br>
<em>Slightly unsatisfactory hinting for the Crimson Roman style. I love Crimson all the same.</em>

The good news is that, as font embedding becomes more commonplace, font designers are increasingly taking care of rendering and are supplying ever better hinting instructions. <a href="https://blog.typekit.com/2011/01/20/new-and-updated-fonts-from-exljbris/">Typekit</a> itself has even intervened by manually re-hinting popular fonts such as <a href="https://new.myfonts.com/fonts/exljbris/museo/">Museo</a>. Your best bet is to view on-page demonstrations of the fonts you are considering, to see how well they turn out. Save time by avoiding, sight unseen, any fonts with the words “thin” or “narrow” in their names.</p>

### Font Size and Measure

As a <a href="https://www.smashingmagazine.com/2011/10/07/16-pixels-body-copy-anything-less-costly-mistake/">recent Smashing Magazine article</a> compellingly attests, you put serious pressure on readability by venturing below a 16-pixel font size for paragraph text. All popular browsers render text at 16 pixels by default. This is a good enough indication (given the notorious tendency among browser makers to disagree) that <strong>16 pixels is a clear standard</strong>. What’s more, the standard is given credence by an equivalent convention in print typography, as the article points out.

We often express <code>16px</code> as <code>100%</code> in the <a href="https://www.blooberry.com/indexdot/css/syntax/declaration.htm">declaration block</a> for the <code>body</code> in our CSS reset style sheets. This makes perfect sense, because it is like saying, “100% the same as the browser would have chosen for you.” If you want the paragraph text to be bigger than 16 pixels, just edit this value in the <code>body</code> block using a percentage value that equates to a “whole pixel.” Why whole pixels? Two reasons. First, whole numbers are less ungainly and are easier to use as multipliers in style sheets. Secondly, browsers tend to round “sub-pixel” values differently, giving <a href="https://ejohn.org/blog/sub-pixel-problems-in-css/">inconsistent results</a>. An 18-pixel font size expressed as a percentage is <code>112.5%</code> (1.125 × 16).

Normalizing the size of default text (or “paragraph text,” if you’re being good and semantic) in such a way is extremely important because it sets us up to use <a href="https://en.wikipedia.org/wiki/Em_%28typography%29">ems</a> as a multiplier for the size of surrounding headings and other textual elements. For instance, to render an <code>h3</code> heading at 1.5 times the font size of the paragraph, we should give it the value of <code>1.5em</code>. Because ems (pronounced as in “Emma,” not E.M. Forster) are relative units, they change according to the default font size. This makes it much easier to maintain style sheets and, more pertinently, ensures that the perceived importance of headings is not increased or diminished by adjusting the size of the paragraph text.

<img loading="lazy" decoding="async" class="109410" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32f063f3-ec72-48c5-862c-86aa1729c1d2/h-measure.jpg" alt="An illustration of optimal line length, or measure" width="500" height="123" />

The “measure” is the number of characters in a line of text. Choosing a <a href="https://webtypography.net/Rhythm_and_Proportion/Horizontal_Motion/2.1.2/">comfortable measure</a> is important for usability, because if lines are too long, then scanning back to find the start of the next line can be awkward. Without conscious effort, <strong>the reader might miss or reread lines</strong>. In <a href="https://www.amazon.com/Elements-Typographic-Style-Robert-Bringhurst/dp/0881792063/ref=sr_1_1?ie=UTF8&amp;qid=1317888735&amp;sr=8-1"><em>The Elements of Typographic Style</em></a>, Robert Bringhurst puts a good measure at somewhere between 45 and 75 characters. It is the main reason why we use the <code>max-width</code> property when designing elastic layouts.

Whatever your page’s ideal maximum width, it is likely much narrower than what you are used to seeing. According to an <a href="https://www.smashingmagazine.com/2009/08/20/typographic-design-survey-best-practices-from-the-best-blogs/">in-depth study</a> of typographic design patterns published on Smashing Magazine, the average website exhibits a measure of 88.74 characters, far exceeding the optimal range.</p>

### Leading and Vertical Rhythm

<a href="https://www.flickr.com/photos/andrec/6067541623/sizes/l/in/photostream/"><img loading="lazy" decoding="async" class="109382" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2962aa0c-6c28-4ef1-bf2e-d486f64cefca/leading.jpg" alt="Glyphs made from lead" width="500" height="330" /></a><br>
<em>(Image: <a href="https://www.flickr.com/photos/andrec/6067541623">andrechinn</a>)</em>

<a href="https://en.wikipedia.org/wiki/Leading">Leading</a> (pronounced “ledding”) is the spacing between consecutive lines of text. Leading has a similar impact on readability as “measure,” because it helps to define and demarcate the rows of glyphs that one must traverse from left to right and back again. The trick with leading is to <strong>avoid adding too much</strong>: text with lines that are too far apart appears fragmented, and the intent of a judicious use of leading is undone by a negative result.

In mechanical typesetting, leading was set by inserting strips of lead metal (hence the pronunciation) between lines. In CSS, the <code>line-height</code> property is the tool we use, and exposure to it is much less likely to make you go mad.

Instead of accounting for space between lines, as with leading, <code>line-height</code> is a vertical measure of the whole line — including the text itself and any spacing to follow. There are three ways to set it: the wrong way, the redundant way and the right way.

The wrong way to set <code>line-height</code> is in pixels. By introducing an absolute value, we would undo all of the good work from the previous section. As the <code>font-size</code> increases (either in the style sheet or the user’s browser settings), the <code>line-height</code> would persist. This produces an interesting effect:

<img loading="lazy" decoding="async" class="109411" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e026bfc5-fa0c-4fc4-88b3-bc342a3aa646/h-values.jpg" alt="An illustration of optimal line length, or measure" width="500" height="123" /><br>
<em>Absolute and relative values do not mix.</em>

So, should we use the same em multipliers that we saw in the last section? This is the redundant way. Although the method would work, providing an em unit is not necessary. Rather, a value of <code>1.5</code> for the <code>line-height</code> that is 1.5 times that of the font size will suffice. The <code>line-height</code> property belongs to an exclusive club of CSS properties that accept unit-less numeric values.

<pre><code class="language-css">p {
   font-size:; /* Silence is golden; implicity 1em. */
   line-height: 1.5;
}</code></pre>

The attentive among you will have noticed that so far I have only mentioned font sizes that are even numbers. The reason is that I favor a line height of <code>1.5</code>. So, a font size of 18 pixels means lines with a height of 27 pixels or, if you prefer, lead strips that are 9 pixels thick. Using even numbers is another bid to maintain whole pixel values — I know that any even number multiplied by 1.5 will result in a whole number. A <code>line-height</code> stated in whole pixels is particularly important, because it is the key value used to achieve “vertical rhythm.”

<img loading="lazy" decoding="async" class="109391" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe8b1375-931e-4166-9642-4e963eda88e4/vertical.jpg" alt="a vertical rhythm illustration" width="500" height="284" /><br>
<em>All components on the page should have a height divisible by the height of one line of paragraph text.</em>

Maintaining vertical rhythm (or composing to a <a href="https://www.alistapart.com/articles/settingtypeontheweb">baseline grid</a>) is the practice of making sure that the height of each textual element on the page (including lists, headings and block quotes) is <strong>divisible by a common number</strong>. This common number (the single beat in a series of musical bars, if you will) is typically derived from the height of one paragraph line. You should be able to see by now why an impossible value like 26.5 pixels would be a mistake for such an integral measure.

The benefits of vertical rhythm to readability are much subtler than those of hinting, measure or leading, but they are still important. <strong>Vertical rhythm gives the page decorum</strong>. Because we have made sure so far that all of our measurements are co-dependent and relative, altering the font size for the body (all the way up at the top of the <a href="https://reference.sitepoint.com/css/cascade">cascade</a>) will not damage the page’s vertical rhythm.

It is worth noting that, although a line height of 1.5 is fairly dependable, not all fonts are made equal. Fonts with a tall x-height or long <a href="https://www.fontshop.com/glossary.php?ltr=d">descenders</a> might benefit from more generous, separative leading. When basic readability is at stake, adopting a more complex vertical rhythm algorithm is worth it.</p>

### Word Spacing and Justification

Without intervention, paragraph text on Web pages is set “ragged right” (<code>text-align: left</code> in CSS): the start of each line is flush with the left margin, but the lengths of the lines vary, giving an uneven “ragged” effect on the right side. If you’re like me, you prefer the tidiness of <a href="https://en.wikipedia.org/wiki/Justification_%28typesetting%29">full justification</a> (illustrated below). But implementing justification without impairing readability is not as straightforward in HTML as it is by using desktop-publishing software.

<img loading="lazy" decoding="async" class="109392" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65523d23-bc49-4bf7-91c0-a67f25157f93/narrow.jpg" alt="justified" width="500" height="123" /><br>
<em>Fully justified text necessitates, arguably, a narrower measure than text set ragged right.</em>

The problem with justified text in HTML (<code>text-align: justify</code>) is word spacing. In print media (such as newspapers), hyphenation is used to break up long words. This results in more components (words or part words) per line, thus <strong>improving distribution</strong> and curbing aggressive word spacing. Browsers do not hyphenate automatically, and the <a href="https://en.wikipedia.org/wiki/Soft_hyphen">soft hyphen</a> (<code>&amp;shy;</code>) is implemented inconsistently. Besides, imagine having to manually insert <code>&amp;shy;</code> all the way through your copy. CSS3’s <span class="removed_link" title="https://www.css3.com/css-text-justify/">text-justify</span> property, which aims to give us more control over <code>text-align: justify</code>, could ease the problem by enabling inter-character distribution. Bizarrely, it is currently available only with Internet Explorer.

<a href="https://code.google.com/p/hyphenator/"><img loading="lazy" decoding="async" class="109403" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f06a10e0-4ad2-42c1-b728-03233b7cc414/hyphenator1.jpg" alt="Hyphenator" width="500" height="86" /></a><br>
<em><a href="https://code.google.com/p/hyphenator/">Hyphenator.js</a></em>

Thankfully, Firefox and Safari <a href="https://blog.fontdeck.com/post/9037028497/hyphens">now support</a> the CSS3 property <code>hyphens</code>, which can automatically insert hyphens much as you would manually with <code>&amp;shy;</code>. In fact, you can revert to manual hyphenation in a document set to <code>hyphens: auto</code> by using the <code>hyphens: manual</code> override. Browser prefixes are required, but <a href="https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/">Lea Verou can help</a> you with that.

Until the other browsers catch up, a consistent cross-browser solution is currently possible only with JavaScript. <a href="https://code.google.com/p/hyphenator/">Hyphenator.js</a> is a powerful tool that takes a library of syllabic patterns specific to each language and uses them to dynamically insert soft hyphens in the correct places. It is a bit pricey (two scripts at a total of 72 KB uncompressed just for the English implementation), but it does work. Its effect is shown in the first screenshot for this section.</p>

### Finishing Touches (Styling Contextually)

Now that we have dealt with the important business of sizing, setting and distributing our paragraphs compellingly, you may wish to apply a few small enhancements and decorations for the purpose of signposting the document. These nuances concern only certain paragraphs, and choosing which paragraphs to set off is a question of context. With the help of special selectors and combinators, we are able to target specific paragraphs depending on where they appear on the page, making sure that the difference in their design is consistent with their intended role and meaning.

<img loading="lazy" decoding="async" class="109401" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5bc50bf-116e-45c6-9729-1fc3a0ab9afc/indent1.jpg" alt="Indent" width="500" height="123" /><br>
<em>Paragraphs separated with a margin (such as <code>margin: 0 0 1.5em;</code>) do not require indentation. With paragraphs, margins and indentation serve the same purpose.</em>

Let’s use <a href="https://en.wikipedia.org/wiki/Paragraph#Paragraph_breaks">indentation</a> as an introductory example. Although less common in Web typography than in print, indenting the first line of each paragraph is a conventional method of grouping paragraphs into chunks of information. In terms of rhythm, it is also a sort of punctuation: <strong>the reader is invited to pause briefly</strong> before each paragraph. Because no indentation is required for the first paragraph — why pause before we’ve even started? — we should exclude this paragraph from our CSS rule. Using the <a href="https://eriwen.com/css/css-adjacent-sibling-selectors/">adjacent sibling combinator</a>, we are able to target only paragraphs with a preceding paragraph, and so the convention that has been familiar to book typography over the centuries is ably reproduced.

<pre><code class="language-css">p + p {
   text-indent: 1.5em  /* I like to keep the indentation length equal to the line height. */
}</code></pre>

In the next example, I have combined the adjacent sibling combinator with the <code>:first-letter</code> pseudo-class to create a pronounced introductory glyph or “elevated cap”:

<pre><code class="language-css">h1 + p:first-letter {
   font-size: 2em;
   line-height: 0;  /* The line-height must be adjusted to compensate for the increased font size, otherwise the leading for the overall line is disrupted. I find that any values below 0.4 work. */
}</code></pre>

<img loading="lazy" decoding="async" class="109395" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a394174-1f9f-4c6c-b431-417f50618593/main-heading.jpg" alt="Example of an elevated cap" width="500" height="123" />

The beauty of adding these refinements (many more of which are <a href="https://jontangerine.com/silo/typography/p/#continuous">demonstrated by Jon Tan</a>, including “drop caps” and “outdents”) contextually is that they are activated only when semantically meaningful and appropriate. For instance, our <code>:first-letter</code> style above is appropriate only for introductory copy. Because the introductory paragraph is always (in this particular schema) preceded by an <code>h1</code> heading, we have a way to bind its style to its particular role in the document’s flow. In other words, we can honor its meaning through its design.

As long as we rigorously adhere to <a href="https://en.wikipedia.org/wiki/Semantic_HTML">semantic HTML</a>, we can employ many nuances that are impervious to both the rearrangement of the page itself and the introduction of dynamic content.</p>

## Conclusion

<a href="https://www.flickr.com/photos/primatage/4590087621/sizes/l/in/photostream/"><img loading="lazy" decoding="async" class="109416" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6b870fd-4441-4d92-97cc-bb20687fb437/h-library.jpg" alt="Library isle" width="500" height="325" /></a><br>
<em>(Image: <a href="https://www.flickr.com/photos/primatage/4590087621/sizes/l/in/photostream/">primatage</a>)</em>

Walking down an aisle in a library, I no more than glance at the vast majority of books shelved on either side of me. Only a madman would suggest that my disregard of these books should sanction their pages being torn out. Nonetheless, because <a href="https://www.useit.com/alertbox/percent-text-read.html">research has shown</a> that visitors don’t read the average Web page in full, and because the “success” of a page is more easily measured by user action than cognition, we are often encouraged to marginalize our writing in favor of visual signifiers or action cues.

Sure, most people will “bounce” your content, but if you really have something to say, don’t alienate the people who are willing to give your writing a chance. <strong>Good typography does justice to your words</strong>, and good wording does justice to your ideas. If readers are comfortable reading your type, then they will more likely be comfortable with what you are writing about.


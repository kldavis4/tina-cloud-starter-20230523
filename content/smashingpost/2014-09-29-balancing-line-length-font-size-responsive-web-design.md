---
title: 'Size Matters: Balancing Line Length And Font Size In Responsive Web Design'
slug: balancing-line-length-font-size-responsive-web-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cab4db09-db1f-4ebc-8166-95566d86c308/distance-lines-illu.png
date: 2014-09-29T20:51:29.000Z
author: laura-franz
description: >-
  As we refine our methods of responsive web design, we’ve increasingly focused on **measure** (another word for “line length”) and its relationship to how people read.
categories:
  - Mobile
  - Typography
  - Fonts
  - Design
  - Readability
---
As we refine our methods of responsive web design, we’ve increasingly focused on <strong>measure</strong> (another word for “line length”) and its relationship to how people read.

The popularization of the “ideal measure” has led to advice such as “Increase font size for large screens and reduce font size for small screens.” While a good measure does improve the reading experience, it’s only one rule for good typography. Another rule is to maintain a comfortable font size.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [16 Pixels: For Body Copy. Anything Less Is A Costly Mistake](https://www.smashingmagazine.com/2011/10/16-pixels-body-copy-anything-less-costly-mistake/)
*   [Designing For The Elderly](https://www.smashingmagazine.com/2015/02/designing-digital-technology-for-the-elderly/)
*   [10 Principles For Readable Web Typography](https://www.smashingmagazine.com/2009/03/10-principles-for-readable-web-typography/)
*   [The Perfect Paragraph](https://www.smashingmagazine.com/2011/11/the-perfect-paragraph/)

## How People Read

People read online text to serve their own needs: to find the information they seek, to discover new ideas and to confirm their notions about life.

{{% feature-panel %}}

### People Read in Three Ways

In 2006, the Nielsen Norman group released images of heat maps from eye-tracking studies. The areas where people looked at the most while reading are red, areas with fewer views are yellow, and the least-viewed areas are blue. As you can see below, the red and yellow areas form three variations of an F-shaped pattern. These variations aren’t surprising because people read in three different ways.

People read <strong>casually</strong>, skimming over text, reading words and sentences here and there to get a sense of the content. The heat map below shows the eye movements of someone casually reading about a product. The reader spent time looking at the image of the product, reading the first couple of sentences, then scanning through the bulleted list.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c72bdc2-fcf4-4ec6-bcf2-838c75f6790e/1-casual-reading-large-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07125e21-caa4-4f0c-8f9a-3172bee5f6ab/1-casual-reading-preview-opt.jpg" alt="1-casual-reading-preview-opt" width="500" height="222" /></a><figcaption>The Nielsen Norman Group explored the F-shaped pattern for casual reading in 2006. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c72bdc2-fcf4-4ec6-bcf2-838c75f6790e/1-casual-reading-large-preview-opt.jpg">View large version</a>)</figcaption></figure>

People also <strong>scan with purpose</strong>, jumping from section to section, looking for a particular piece of information. They might only read a word or the first couple of characters of a word as they scan the screen. The heat map below shows the eye movements of someone scanning the results of a Google search with purpose. The person read the first two results more slowly. Then, their eyes jumped from section to section, looking for the search term. Therefore, we do not see a strong vertical stroke along the left edge of the text.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a715d1b4-49b4-4c4a-883f-b66251e18417/2-scanning-with-purpose-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/740ec677-9089-4dc1-8343-655ca5f92677/2-scanning-with-purpose-preview-opt.jpg" alt="2-scanning-with-purpose-preview-opt" width="500" height="222" /></a><figcaption>The Nielsen Norman Group explored the F-shaped pattern for purposeful scanning in 2006. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a715d1b4-49b4-4c4a-883f-b66251e18417/2-scanning-with-purpose-large-opt.jpg">View large version</a>)</figcaption></figure>

Finally, people read in an <strong>engaged manner</strong>. When they find an article or blog post they are interested in, they will slow down and read the whole text, perhaps even going into a trance-like state. The heat map below shows the eye movements of a person reading in an engaged manner. The tone is more continuous. There is more red (meaning more time spent reading) and less jumping around the page. When the intensity of reading dwindled because they lost interest (the corporate “About us” page might not have aligned with their interests), their eyes continued along the left edge of the text.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9525a8fb-49bc-4261-abf0-83a508eb8135/3-reading-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26c6e9b0-3dd1-453e-8a1a-813303e32178/3-reading-preview-opt.jpg" alt="3-reading-preview-opt" width="500" height="222" /></a><figcaption>The Nielsen Norman Group explored the F-shaped pattern for reading in an engaged manner in 2006. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9525a8fb-49bc-4261-abf0-83a508eb8135/3-reading-large-opt.jpg">View large version</a>)</figcaption></figure>

###  Reading Is a Complex Process

We know that people read in three different ways, but let’s look more closely at how people read — how the F-shaped patterns are formed.

We know that people. Don’t. Read. Each. Individual. Word. Instead, they use their foveal (or central) vision to focus on a word, while using their peripheral vision to find the next spot on which to focus.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bc34f1f-374f-4af7-abd7-4526191d381e/4-reading-preview-opt.gif" alt="4-reading-preview-opt" width="500" height="400" /><br>
<figcaption> People don’t read each word individually.</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/551da0a6-c5d8-4326-8d26-bbce70b865c8/5-reading-preview-opt.gif" alt="5-reading-preview-opt" width="500" height="400" /><br>
<figcaption>People use their foveal (central) and peripheral vision to read. </figcaption></figure>

We also know that people don’t fixate on every word, but tend to skip words (their eyes take little leaps, called “saccades”) and fill in the rest. This is especially true of those who read casually or scan with purpose.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bbec11c-cad8-4bb0-866e-77edc7b5a3a8/6-skipping-words-preview-opt.gif" alt="6-skipping-words-preview-opt" width="500" height="400" /><br>
<figcaption> People skip words and fill in the rest.</figcaption></figure>

Finally, we know that readers anticipate the next line while moving their eyes horizontally along a line; so, their eyes are drawn down the left edge of the text. This constant struggle between horizontal and vertical motion contributes to the F-shaped reading patterns.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49fbae44-7b47-4854-a54e-e755ebc391dc/7-f-shape-pattern-preview-opt.png" alt="7-F-shape-pattern-preview-opt" width="500" height="269" /><br>
<figcaption>The constant struggle between horizontal and vertical eye movement results in the F-shaped patterns .</figcaption></figure>

## Line Length (Measure) And Reading

Typographers have been writing about the relationship between horizontal and vertical eye motion for almost a century. In 1928, Jan Tschichold dismissed centered text and advocated for left-aligned text. He argued that this would assist readers by providing a consistent left (vertical) edge for the eye to return to after finishing each (horizontal) line.</p>

### The Ideal Measure: 45 to 75 Characters

We have multiple “rules” for facilitating a horizontal reading motion, one of which is to set text at a reasonable measure. As James Craig wrote in his book <em>Designing With Type</em> (originally published in 1971, now it its fifth edition):
<blockquote>Reading a long line of type causes fatigue: the reader must move his head at the end of each line and search for the beginning of the next line.… Too short a line breaks up words or phrases that are generally read as a unit.</blockquote>

If a casual reader gets tired of reading a long horizontal line, then they’re more likely to skim the left edge of the text. If an engaged reader gets tired of reading a long horizontal line, then they’re more likely to accidentally read the same line of text twice (a phenomenon known as “doubling”).

65 characters (2.5 times the Roman alphabet) is often referred to as the perfect measure. Derived from this number is the ideal range that all designers should strive for: 45 to 75 characters (including spaces and punctuation) per line for print. Many web designers (including me) apply that rule directly to the web. I’ve found, however, that we can reliably broaden the range to 45 to 85 characters (including spaces and punctuation) per line for web pages.</p>

### Measure and Web Type

Web designers have started to embrace a reasonable measure for text. Resources abound. Early writings include Mark Boulton’s more poetic approach to typography, which he refers to as “knowing your hanging punctuation from your em-dash” (“<a href="https://www.markboulton.co.uk/journal/five-simple-steps-to-better-typography">Five Simple Steps to Better Typography</a>”). Later writings include Harry Roberts’ more technical approach to typography (“<a href="https://www.smashingmagazine.com/2011/03/14/technical-web-typography-guidelines-and-techniques/">Technical Web Typography: Guidelines and Techniques</a>”).

The most recent (and, dare I say, exciting) development in measure? Its role in responsive web design. More designers are using line length to help determine break points in a responsive structure! Chris Coyer recently developed his bookmarklet to test line length in order to help responsive web designers keep an eye on their measure (“<a href="https://css-tricks.com/bookmarklet-colorize-text-45-75-characters-line-length-testing/">Bookmarklet to Colorize Text Between 45 and 75 Characters</a>”).

But a good measure is only one rule for setting readable text.

## Font Size And Reading

A good, comfortable font size is also necessary for setting readable text. This rule is old news. But given the number of responsive websites out there that make text too small or too big in order to achieve an ideal measure, the rule bears repeating.</p>

### Static Web Pages and Font Size

One benefit of a responsive web structure is readable text — text that people on hand-held devices don’t have to pinch and zoom to read. If a structure is static (like the two-column page shown below), then an ideal measure won’t do the trick. The text will simply be way too tiny to read on a small device such as a phone.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/879a217c-1104-4afa-a89b-f967cd9dc23e/8-structure-preview-opt.png" alt="8-structure-preview-opt" width="500" height="360" /><br>
<figcaption>Left: The main column has a good measure (45 to 85 characters are highlighted in yellow). But without a responsive structure, the text is too small to read on a small device without pinching and zooming. Right: The font size (13-pixel Verdana for the left column, 18-pixel Georgia for the introduction and 16-pixel Georgia for the article) is comfortable to read on a laptop.</figcaption></figure>

### Small Devices and Font Size

When designing a responsive website, start with a comfortable font size and an ideal measure to help determine break points. But when the time comes (as it always does), let the ideal measure go.

Text already looks smaller on hand-held devices than on larger devices. This is fine because people tend to hold small devices closer when reading. Current popular wisdom is to preserve the measure by further reducing the font sizes for held-held devices. In practice, retaining a comfortable font size as much as possible better preserves readability. The result will be a less-than-ideal measure but a more comfortable reading experience.

A responsive structure won’t help if small text on a hand-held device encourages readers to pinch and zoom!

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7dde0feb-d2d7-46c1-b95e-c0285f9ba8e0/9-font-size-preview-opt.png" alt="9-font-size-preview-opt" width="500" height="657" /><br>
<figcaption>Left: To retain an ideal measure, the font size is reduced to 12-pixel Verdana and 14-pixel Georgia for hand-held devices. The text is harder to read. Right: The font size is 13-pixel Verdana and 17-pixel Georgia for hand-held devices. The measure is no longer ideal, but the text is easier to read.</figcaption></figure>

###  Large Devices and Font Size

When designing a responsive website, remember that measure and font size affect not only people using hand-held devices. The majority of people still use larger devices, such as laptops and desktop computers.

Some simple responsive structures keep text in a single column that expands and contracts with the size of the device. This can be an elegant, appropriate solution — except when the font size (instead of the column’s width) is used to preserve the ideal measure.

We’ve learned not to set text too small, but text that’s too big also poses a problem. When type gets too big, the reader’s eyes try to follow their usual pattern. But a font size that’s too large takes up more horizontal space, and it interferes with the horizontal flow that readers have established using their foveal vision and their pattern of skipping words.

We’re used to setting online text larger than printed text. This is fine because people tend to place large devices on their lap or on a desk while reading. But overly large text forces the reader to slow down and adjust how far they skip ahead as they read. Reading horizontally becomes cumbersome, and the reader will start to skip vertically down the left edge of the text.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad6080ab-9d5a-40ef-81cd-e3a01694a362/10-horizontal-rhythm-preview-opt.png" alt="10-horizontal-rhythm-preview-opt" width="500" height="429" /><br>
<figcaption>When type gets too big, the reader tries to follow their usual horizontal rhythm. This forces them to read parts of words instead of entire words and to slow down and adjust their reading pattern.  </figcaption></figure>

Current popular advice is to preserve the measure by increasing the font size for large devices. For example, the one-column structure below has an ideal measure. But to achieve this ideal measure on large devices, we’ve had to set the text to 19-pixel Verdana, 22-pixel Georgia for the article, and a whopping 26-pixel Georgia for the introduction!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b368b7d0-584a-41c0-9e88-0bf5ff352fab/11-single-column-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d2dbb0f-c425-495a-b927-374fb7983435/11-layout-at-hundred-percent-preview-opt.png" alt="11-layout-at-hundred-percent-preview-opt" width="500" height="607" /></a><figcaption>In the layout above, details show the text at 100% size. The text on this web page is way too big for comfortable reading! Simple one-column responsive structures should use a narrower column on large devices, keeping the font size smaller and easier to read. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b368b7d0-584a-41c0-9e88-0bf5ff352fab/11-single-column-large-opt.jpg">View large version</a>)</figcaption></figure>

In practice, retaining a comfortable font size as much as possible and simply narrowing the column’s width instead are better. Look at what happens to <a href="https://alistapart.com">A List Apart</a> when it’s viewed on a hand-held device and on a laptop.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fe773db-ed5b-426a-9c8f-22ce9f6845c9/12-alistapart-example-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04c48d3d-76a1-4fd0-bbb3-23ca1b0411ac/13-alistapart-example-preview-opt.png" alt="12-alistapart-example-large-opt" width="500" height="374" /></a><figcaption>A List Apart is perfectly readable on a hand-held device. But on a laptop, the text gets too big to be comfortably read. A shorter measure and a smaller font size would help people follow their usual horizontal rhythm. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fe773db-ed5b-426a-9c8f-22ce9f6845c9/12-alistapart-example-large-opt.png">View large version</a>)</figcaption></figure>

## Bonus Section: Line Height And Reading

So far, our focus has been on the relationship between font size and measure in responsive web structures. But line height also affects how people read.</p>

### Line Height Affects Horizontal Motion

Because readers scan content both horizontally and vertically, lines of text should feel like horizontal lines, not like woven fabric.

A line height that is too tight could undermine horizontal eye movement and encourage scanning down the left edge. It could also force people to reread lines of text. On the other hand, a line height that is too loose could make lines of text visually “float away” from each other. The lines will no longer feel like a cohesive unit, and vertical scanning becomes more difficult.

While there is no perfect line height, a good rule of thumb is to set it at approximately 150% of the font size.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/706c1ff6-89c3-447b-b565-cac34c17e83a/15-line-height-preview-opt.png" alt="15-line-height-preview-opt" width="500" height="141" /><br>
<figcaption>While there is no perfect line height, a good rule of thumb is to set it at approximately 150% of the font size.</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63076e6c-8552-4e77-959b-7efc5b59a0a8/14-tight-height-preview-opt.png" alt="14-tight-height-preview-opt" width="500" height="276" /><br>
<figcaption>Top: When the line height is too tight, it undermines the horizontal reading flow and increases doubling. Bottom: When the line height is too loose, lines of text visually float away from each other.</figcaption></figure>

### Line Height and Font Size

Setting line height is a complex balance of variables (font family, measure, font size, language). The most important variable when creating a responsive web structure is — surprise! — font size.

Smaller type tends to need more line height, not less. A generous line height helps the eye to recognize small word shapes more easily, and it encourages horizontal motion when the eye gets tired of reading small text.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d947a581-cc15-4542-889a-d7f69f48342d/16-line-height-at-hundred-fifty-percent-preview-opt.png" alt="16-line-height-at-hundred-fifty-percent-preview-opt" width="500" height="387" /><br>
<figcaption>Left: A line height set at 150% is a bit too tight on an iPhone. Right: The exact same text with a slightly looser line height promotes horizontal movement and helps the reader to recognize word shapes.</figcaption></figure>

## Look Closely, Break Rules

When we design a responsive structure, testing it on a large device is easy; we can change a desktop browser’s size quickly. But designing on a desktop or laptop browser means that we are spending most of our time at an arm’s length from the text, and we don’t spend much time seeing how the text renders on small devices.

If you’re using measure to find break points in your responsive website, then you probably care about type and reading. Keep using measure! It’s a great starting point. But to see whether your type truly works, <strong>spend some time looking at it closely, on a smaller device</strong>. Balance measure, line height and font size as needed.

Remember that all rules are meant to be broken. Heck, Jan Tschichold broke his own rule and used centered text for much of his career. When the time comes, sacrifice measure for a comfortable font size. A good font size (not too small) is readable. A good font size (not too big) promotes horizontal eye motion. A good font size with the proper line height will help your readers find what they’re looking for.</p>

### Further Resources

*   “[Five Simple Steps to Better Typography](https://www.markboulton.co.uk/journal/five-simple-steps-to-better-typography),” Mark Boulton
*   “[Technical Web Typography Guidelines and Techniques](https://www.smashingmagazine.com/2011/03/14/technical-web-typography-guidelines-and-techniques/),” Harry Roberts, Smashing Magazine
*   “[Choose a Comfortable Measure](https://webtypography.net/2.1.2),” The Elements of Typographic Style Applied to the Web
*   “[How We Read](https://alistapart.com/article/how-we-read),” Jason Santa Maria, A List Apart
*   “[Bookmarklet to Colorize Text Between 45 and 75 Characters (For Line-Length Testing)](https://css-tricks.com/bookmarklet-colorize-text-45-75-characters-line-length-testing/),” Chris Coyier
*   “[How I Test Type and Layout](https://jordanm.co.uk),” Jordan Moore

{{< signature "il, al" >}}


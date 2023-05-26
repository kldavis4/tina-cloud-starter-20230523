---
title: 'Mind Your En And Em Dashes: Typographic Etiquette'
slug: mind-your-en-and-em-dashes-typographic-etiquette
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcc10d79-4f08-41df-864f-e408db987de7/type-98.jpg
date: 2011-08-15T14:37:39.000Z
author: david-kadavy
summary: >-
  Based upon a chapter from David Kadavy’s upcoming book, find a few rules of thumb that will have you using typography more lucidly than ever before. 
description: >-
  Find a few rules that will have you using typography more lucidly than ever before. Remember that an understanding of typographic etiquette separates the master designers from the novices.
categories:
  - Typography
  - Design
  - Fonts
---

An understanding of typographic etiquette separates the master designers from the novices. A well-trained designer can tell within moments of viewing a design whether its creator knows how to work with typography. Typographic details aren’t just inside jokes among designers.

They have been built up from thousands of years of written language, and applying them holds in place long-established principles that enable typography to communicate with efficiency and beauty.

Handling these typographic details on the Web brings new challenges and restrictions that need to be considered. Below are a few rules of thumb that will have you using typography more lucidly than ever before.

{{% feature-panel %}}

## Setting Body Copy

Good typography comes down to communicating information, and the basis of information is good old-fashioned body copy &ndash; simple blocks of text. Here are a few ways to make your blocks of text nice and clean.

### Indentation Or Space After A Paragraph?

When signalling the end of a paragraph and the beginning of another, you can generally either indent or insert a space between the paragraphs. Doing both is redundant and creates awkward, irregular chunks of white space.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84ac96aa-31d9-453e-ada4-e951d2d26474/paragraphs.png" alt="indent vs. space after paragraph" /></figure>

**Indentation**  
Indent the first line of a new paragraph about 1 em (if your font size is <code>12px</code>, then that would amount to 12 pixels). Indenting the opening paragraph of a new section would be redundant, because that paragraph would be the first in that page or section anyway.

**Space after paragraph**  
A full line break of 1 em (like when you hit the “Return” key twice) is generally more than enough to signal a new paragraph. About 0.8 ems is sufficient.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b732eeb2-70d2-42e8-88fc-322985d49d9a/ragged-right.png" alt="flush left vs. justified type" /><figcaption>Text set flush left (or ragged-right) creates an even texture and is easier to read. Because the Web allows for less typographic control, justified type usually creates rivers and big gaps in blocks of text.</figcaption></figure>

**Flush left (ragged-right)**  
In text set flush left, the lines will break naturally, resulting in a “ragged” right side of the column. This is generally considered easier to read because the eye can better distinguish one line from the next, because of the different line lengths. Additionally, studies have shown that readers score higher in comprehension and recall when text is flush left. Hyphenation should not be used with text that is flush left, because that would defeat the whole point of a ragged right.

**Avoid justified type on the Web**  
Justified text is spaced out so that each line is of the same length. Because all lines have to be set at the same length, some variation in letter spacing (i.e. the space between letters), and word spacing (the space between words) is done to lengthen and shorten lines. This changes the overall texture of the body copy, making it less even.

High-end desktop publishing applications (such as Adobe InDesign) have sophisticated systems for justifying type so that it doesn’t produce “rivers” (large gaps in the text from too much word spacing). They use a combination of letter spacing, word spacing, hyphenation and glyph scaling (i.e. very slightly adjusting the width of individual letters) to produce an even texture in the body copy.

But there is no hyphenation control in CSS. Beyond <a href="https://carlos.bueno.org/2010/04/sweet-justice.html">JavaScript libraries that handle hyphenation</a> and CSS3’s <code>text-justify</code> property, browsers don’t have very sophisticated measures for maintaining an even texture in blocks of text. This makes justified text on the Web highly susceptible to big holes and rivers in the body text.

Avoiding justified type on the Web is generally a good idea. At the optimal line length for reading (about 50 to 80 characters or 8 to 15 words), making lines of text all the same length, without hyphenation or subtle letter spacing, nearly always results in rivers.

## One Space After A Period. Not Two.

Very few typographic debates match the intensity of whether there should be one or two spaces after a sentence.

This practice is a holdover from typographers of the Victorian era. The practice began when typewriters were introduced. Because early typewriters used monospaced fonts (meaning that the spaces between letters were always the same length), typists used two spaces to mimic the slightly wider spaces that typesetters were using after periods. Now that computers (and the fonts on them) are equipped with proportionally spaced (rather than monospaced) fonts, this practice is outdated, and it creates awkward breaks in the body text.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bf394cb-4895-497a-9d09-1f431ceb9cd8/one-space.png" alt="One space vs. Two spaces" /><figcaption>One space after a period is plenty to signal the end of a sentence. It also keeps the text block even.</figcaption></figure>

For those who are still skeptical, consider this: the beginning of a new sentence is already indicated by a period, a full space and a capital letter. Adding yet another space merely pokes a hole in the body text and interrupts the flow of reading.

The typist may wish to continue using two spaces after a period, but the typographer should not.

## Use Dashes Dashingly

Most fonts are equipped with at least two dashes: an en dash (&ndash;, <code>&amp;ndash;</code>, which is the width of a lowercase “n”) and an em dash (&mdash;, <code>&amp;mdash;</code>, which is the width of a lowercase “m”). Don’t confuse these with the hyphen (-), which isn’t a dash at all but a punctuation mark.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fe4a973-f32c-4be3-89ea-2ed83aa78605/dashes.png" alt="Dashes: hyphen, en dash, em dash" /></figure>

### The Hyphen

Hyphens and dashes are confused to the point that they are now used almost interchangeably by some. Some fonts, such as Adobe Garamond Pro, retain hyphens in their original form; those hyphens look more like the diagonal stroke of a calligrapher’s pen than a straight horizontal line. You’ll also often see hyphens used as a replacement for a minus sign; however, a longer character is available in some fonts for this purpose.

Although the hyphen does look quite a bit like a dash or minus sign, it is a punctuation mark. It should be used primarily to hyphenate words in justified type. On the Web, this isn’t much of a concern because, as mentioned, there is no standard hyphenation control in browsers. The hyphen should also be used in compound modifiers (such as “fine-tuned”), to join digits in phone numbers, and in a few other rare cases (covered in detail on <a href="https://en.wikipedia.org/wiki/Hyphen">Wikipedia</a>).

### The En Dash And The Em Dash

In *The Elements of Typographic Style* &ndash; which is the unofficial bible of the modern typographer &ndash; Robert Bringhurst recommends that dashes in text should be the en dash flanked by two spaces. This is much less visually disruptive than using the em dash with no space&mdash;which is recommended in editorial style books such as *The Chicago Manual of Style* &mdash; because there is less tension between the dash and the characters on either side of it.

Why go against *The Chicago Manual of Style* in this case? The reason is that style manuals are concerned mostly with punctuation, not typography. An en dash surrounded by spaces achieves the same effect as an em dash with no spaces, but typographically it is less disruptive. This was a big debate between my editor and me when I was writing <a href="https://www.amazon.com/Design-Hackers-Reverse-Engineering-Beauty/dp/1119998956">my book</a>.

The practice of using two hyphens for a dash is a holdover from the days of typewriters. Besides being visually disruptive to smooth blocks of text, it is now unnecessary with the richer character sets that are available to typographers.

The en dash is also used to indicate ranges of numbers (such as “7&ndash;10 days”), although it isn’t flanked by spaces in this case.

## Use Smart Quotes, Dummy

The quotation mark that is produced when you type ” on your computer is not a true quotation mark (unless your word processing or page layout program has automatic formatting). True quotes are sometimes called “smart quotes,” and the right one must be used according to whether you are opening or closing a quotation. To open a quotation, use “ (<code>&amp;ldquo;</code>), and to close a quotation, use ” (<code>&amp;rdquo;</code>). For opening single quotes, use ‘ (<code>&amp;lsquo;</code>), and for closing single quotes and apostrophes, use ’ (<code>&amp;rsquo;</code>). CMS’ such as WordPress usually either convert dumb quotes to smart quotes automatically or have plug-ins for the job.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b82f23a4-7f6a-4454-9162-d23dcc556080/smart-quotes.png" alt="Smart quotes vs. dumb quotes" /></figure>

{{% ad-panel-leaderboard %}}

### Smart Quotes in Action

CNN uses dumb quotes, which look clunky and lifeless, while The New York Times uses smart quotes, which look clean and sophisticated:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c57f9dd3-bf2a-4ce7-8e8f-401faf896f4c/smart-quotes-cnn-nyt.jpg" alt="CNN vs. NYT" /></figure>

Smart quotes are so sexy that their sinuous forms can be used as ornamentation, such as in this pull quote on <a href="https://jasonsantamaria.com/articles/on-good/">Jason Santa Maria’s blog</a>, which features smart quotes only in shadow form:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/badd3167-1c0d-4e7f-9848-cff4db947a05/smart-quotes-santamaria.jpg" alt="smart quotes on jasonsantamaria.com" /></figure>

## Quotation Marks Don’t Measure Up

The “ and ’ on your keyboard are also often used to designate feet and inches (Steve Jobs is 6’ 2”). This, too, is technically incorrect. For feet, you should use ′ (<code>&amp;prime;</code>), and for inches, ″ (<code>&amp;Prime;</code>). (Steve Jobs is, in fact, 6′ 2″.)

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e3bbfa6-8b45-4378-98e7-588bac0feba4/prime.png" alt="prime vs. dumb quotes" /></figure>

Note that many desktop publishing programs are so advanced that they automatically (and incorrectly) insert “smart” apostrophes and quotation marks in all of these situations. This can be changed in the program’s settings, but the quickest way around this is simply to copy and paste the correct mark from a “less sophisticated” text editor.

## +1 For Proper Math Symbols

Sometimes in our haste, we use the wrong marks for math symbols. For example, as we learned above, a hyphen is not a minus sign (−, <code>&amp;minus;</code>). Additionally (no pun intended), neither an x nor an asterisk (\*) is a multiplication symbol (×, <code>&amp;times;</code>).

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e9fe690-fbcc-4475-8a4b-4d4994ddb207/math-symbols.png" alt="math symbols" /></figure>

Proper fractions not only add elegance to typography, but are more readily recognizable. Using a slash in your fractions (1/3) is not ½ (<code>&amp;frac12;</code>) as cool as using the proper vulgar fraction (as it’s called).

Certain other symbols are harder to substitute with common characters, such as when you write 98¢ (<code>&amp;cent;</code>) and 104° F (<code>&amp;deg;</code>). You might be tempted to just type these out as “cents” and “degrees.”

## There’s Always More With Ellipses

Sometimes, there’s more than meets the eye. Most of us type the ellipsis as three periods (...), but most fonts come equipped with their own character (…, <code>&amp;hellip;</code>) that is slightly more spaced out. *The Chicago Manual of Style* would have you think that the proper ellipsis consists of periods separated by spaces (. . .), but any typographer knows that is too disruptive to body text. Some typographers prefer to set their own ellipses by using thin spaces (<code>&amp;thinsp;</code>) between periods (...). But your judgment is best; pick the ellipsis treatment that makes your text block look most consistent (which will never be with full spaces between periods.)

## Accent Marks And Other Diacritics Aren’t Passé

Sure, in the US you can work on your resume while sitting in a cafe, and it wouldn’t be much different than if you were working on your résumé in a café in France. No matter how naïve you are, sometimes using the proper diacritical mark is… critical. A diacritic is a mark placed near (usually above or below) a letter to change its sound. The most common diacritic in English is the acute (´) accent, which is used in a number of words borrowed from other languages and which is sometimes very important, such as for the sake of declaring your passion for saké.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee18bdd8-9c59-44e2-a32d-76dd9059ec8f/diacritics.png" alt="acute vs. grave accent" /></figure>

The acute accent is often confused with the grave accent (\`), which leans to the left and is readily available on US keyboards below the tilde (\~). The grave accent is actually much less common in English than the acute accent. If you ever see one again, you might think you were having a déjà vu.

To insert an acute accent on Mac OS X, hold down Option while typing “e,” and then type the letter that you want to appear below the accent (so, if you want “é,” you’d be typing “e” twice). Play around with Option + u, i and \~, and a whole world of diacritics will open for you.

## Ligatures Bring Letters Together

In the early days of printing, when type was set in lead, the lead slugs on which characters were set made it difficult to set certain character pairs close enough. For example, in the letter combination “fi,” the top terminal of the “f” stuck out so far that the letter couldn’t be set close enough to the “i” because of the dot on the “i.” Thus, many fonts (usually the classic ones, such as Adobe Garamond) have ligatures for certain pairings that actually meld the letterforms together. Some modern fonts, such as Helvetica, also have ligatures, but their effect is negligible.

Below, you can see that ligatures are needed in some fonts more than others. Notice how an “fi” ligature is more critical to clean typography in Adobe Garamond than it is in Helvetica. Because of this, different fonts come with different ligatures.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/398ea0c7-82f6-43d6-9c84-0ae19e6b5c02/ligatures.png" alt="ligature vs. no ligature in Adobe Garamond vs. Helvetica" /></figure>

In addition to “fi,” ligatures are most commonly needed for the groupings “fl,” “ff,” “ffi” and “ffl.” Below you can see that Apple makes beautiful use of the “ffl” ligature in the type treatment of “iPod shuffle.”

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15b26509-14d1-491e-8d07-e6b2daf232ae/shuffle-ligature.jpg" alt="iPod Shuffle ligature on Apple.com" /></figure>

### Using Ligatures Practically

Obviously, typing in ligatures every time you need them is impractical. Even if you did, your content might not ultimately be displayed in a font that is equipped with the appropriate characters. Fortunately, plug-ins such as jQuery’s Ligature.js will automatically insert the most commonly supported ligatures where appropriate.

But, be careful: even if the proper characters are available, you might make it difficult for users to search for text on the page. Currently, Internet Explorer and WebKit-based browsers such as Chrome and Safari match ligatures to their corresponding letter pairs when the search command is used (for example, when a user searches for “fig” on the page), whereas Firefox does not.

### CSS3′s font-variant-ligatures Property

CSS3’s <code>font-variant-ligatures</code> property displays the proper ligatures without interfering with the actual HTML code of the page, thus preserving full functionality of the search command in all browsers. In this case, while Internet Explorer, Chrome and Safari do not currently support this property, Firefox does.

So, if you apply ligatures at the content level, then your Firefox users won’t be able to use the search command for them. And if you use <code>font-variant-ligatures</code>, only your Firefox users will see the ligatures. Because of the spotty browser support for ligatures, ignoring ligatures altogether in the body copy would not be unreasonable. A lack of ligatures in big headlines and headings might be more obvious, though, so picking your preferred method of support there might be worthwhile.

## Being Reasonable

Obviously, keeping track of and implementing some of these typographic details might seem pretty tedious. Fortunately, most Web frameworks and CMS’ have plug-ins that take care of them for you, and some of CSS3’s typography controls are at least beginning to be supported in browsers.

But as with all matters of design and production, economy comes into play. You may decide that implementing some of these details just isn’t worth the trouble. What’s important is at least *knowing* typographic etiquette, so that you can rely on it when it matters and make wise decisions that are appropriate for your project.

## Other Resources

You may be interested in the following articles and related resources:

*   [How to Type](https://www.howtotype.net/) Learn how to actually type these characters on your computer.
*   [*The Elements of Typographic Style*](https://www.amazon.com/Elements-Typographic-Style-Robert-Bringhurst/dp/0881791326), Robert Bringhurst The Amazon ordering page for the unofficial bible of modern typographers. This book is full of great advice on any typographic detail you can imagine.
*   [The Elements of Typographic Style Applied to the Web](http://webtypography.net/) An adaptation of Robert Bringhurst’s classic book for the Web.

*This post is based upon a chapter from David’s upcoming book, <a href="https://www.amazon.com/gp/product/1119998956">Design for Hackers: Reverse-Engineering Beauty</a>, which will be published in September 2011.*

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Macrotypography For A More Readable Web Page](https://www.smashingmagazine.com/2012/05/applying-macrotypography-for-readable-web-page/)
*   [How To Choose A Typeface &mdash; A Step-By-Step Guide!](https://www.smashingmagazine.com/2011/03/how-to-choose-a-typeface/)
*   [Respect Thy Typography](https://www.smashingmagazine.com/2012/03/respect-thy-typography/)
*   [Typography Keyboard Layout [Free Download]](https://www.smashingmagazine.com/2009/04/typography-keyboard-layout/)

{{< signature "al, mrn" >}}

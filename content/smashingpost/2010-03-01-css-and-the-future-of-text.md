---
title: The Future Of CSS Typography
slug: css-and-the-future-of-text
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2e3eac8-7f5d-4222-8c7b-7c9a5862277b/typography4.jpg
date: 2010-03-01T10:20:05.000Z
author: inayaili-de-leon
description: >-
  There has been an increasing and sincere **interest in typography** on the web
  over the last few years. Most websites rely on text to convey their messages,
  so it's not a surprise that text is treated with utmost care. In this article,
  we'll look at some useful techniques and clever effects that use the power of
  style sheets and some features of the upcoming CSS Text Level 3 specification,
  which should give Web designers finer control over text.
categories:
  - Coding
  - Typography
  - CSS
---
There has been an increasing and sincere <strong>interest in typography</strong> on the web over the last few years. Most websites rely on text to convey their messages, so it's not a surprise that text is treated with utmost care. In this article, we'll look at some useful techniques and clever effects that use the power of style sheets and some features of the upcoming CSS Text Level 3 specification, which should give Web designers finer control over text.

Keep in mind that these <strong>new properties and techniques are either new</strong> or still in the works, and some of the most popular browsers do not yet support them. But we feel it's important that you, as an informed and curious Web designer, know what's around the corner and be able to experiment in your projects.

Be sure to check out the following articles:

*   [8 Simple Ways to Improve Typography In Your Designs](https://www.smashingmagazine.com/2009/04/8-simple-ways-to-improve-typography-in-your-designs/)
*   [CSS Baseline: The Good, The Bad And The Ugly](https://www.smashingmagazine.com/2012/12/css-baseline-the-good-the-bad-and-the-ugly/)
*   [The Perfect Paragraph](https://www.smashingmagazine.com/2011/11/the-perfect-paragraph/)
*   [Applying Macrotypography For A More Readable Web Page](https://www.smashingmagazine.com/2012/05/applying-macrotypography-for-readable-web-page/)

## A Glance At The Basics

One of the most common CSS-related mistakes made by budding Web designers is creating inflexible style sheets that have <strong>too many classes and IDs</strong> and that are difficult to maintain.

{{% feature-panel %}}

Let’s say you want to change the color of the headings in your posts, keeping the other headings on your website in the default color. Rather than add the class <code>big-red</code> to each heading, the sensible approach would be to take advantage of the <code>DIV</code> class that wraps your posts (probably <code>post</code>) and create a selector that targets the heading you wish to modify, like so:

<pre><code class="language-css">.post h2 {
	font-weight: bold;
	color: red;
}</code></pre>

This is just a quick reminder that there is no need to add classes to everything you want to style with CSS, especially text. <strong>Think simple.</strong>

## The Font Property

Instead of specifying each property separately, you can do it all in one go using the font shorthand property. The order of the properties should be as follows: <code>font-style</code>, <code>font-variant</code>, <code>font-weight</code>, <code>font-size</code>, <code>line-height</code>, <code>font-family</code>.

When using the font shorthand, any values not specified <strong>will be replaced by their parent value</strong>. For example, if you define only <code>12px Helvetica, Arial, sans-serif</code>, then the values for <code>font-style</code>, <code>font-variant</code> and <code>font-weight</code> will be set as <code>normal</code>.

The font property can also be used to <strong>specify system fonts</strong>: <code>caption</code>, <code>icon</code>, <code>menu</code>, <code>message-box</code>, <code>small-caption</code>, <code>status-bar</code>. These values will be based on the system in use, and so will vary according to the user’s preferences.</p>

### Other Font Properties

A few font-related properties and values are not as commonly used. For example, instead of using <code>text-transform</code> to turn your text into all caps, you could use <code>font-variant: small-caps</code> for a more elegant effect.

You could also be very specific about the <a href="https://www.w3.org/TR/css3-fonts/#font-weight-the-font-weight-property">weight of your fonts</a>, instead of using the common <code>regular</code> and <code>bold</code> properties. CSS allows you to specify font weight with values from <code>100</code> to <code>900</code> (i.e. <code>100</code>, <code>200</code>, <code>300</code>, etc.). If you decide to use these, know that the <code>400</code> value represents the <code>normal</code> weight, while <code>700</code> represents <code>bold</code>. If a font isn’t given a weight, it will default to its parent weight.

Another useful property, sadly supported only in Firefox for now, is <code>font-size-adjust</code>, which allows you to specify an aspect ratio for when a fall-back font is called. This way, if the substitute font is smaller than the preferred one, the text's x-height will be preserved. A good explanation of how <code>font-size-adjust</code> works can be found on <a href="https://www.w3.org/TR/css3-fonts/#font-size-adjust">the W3C website</a>.</p>

## Dealing With White Space, Line Breaks And Text Wrapping

Several CSS properties deal with these issues, but the specs are still in the works (at the "Working Draft" stage).</p>

### White Space

The <code>white-space</code> property lets you specify a combination of properties for which it serves as a shorthand: <code><a href="https://dev.w3.org/csswg/css3-text/#white-space-collapsing">white-space-collapsing</a></code> and <code><a href="https://dev.w3.org/csswg/css3-text/#text-wrap">text-wrap</a></code>. Here's a breakdown of what each property stands for:

*   `normal` white-space-collapsing: collapse/text-wrap: normal
*   `pre` white-space-collapsing: preserve/text-wrap: none
*   `nowrap` white-space-collapsing: collapse/text-wrap: none
*   `pre-wrap` white-space-collapsing: preserve/text-wrap: normal
*   `pre-line` white-space-collapsing: preserve-breaks/text-wrap: normal

This property can be useful if you want to, for example, <strong>display snippets of code</strong> on your website and preserve line breaks and spaces. Setting the container to <code>white-space: pre</code> will preserve the formatting.

<a href="https://wordpress.org/"><img loading="lazy" decoding="async" class="32223" title="Wordpress" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69a24da1-9342-4d69-b92a-8790310e7cd1/wordpress.jpg" alt="Wordpress" width="500" height="200" /></a><br>
<em>WordPress uses <code>white-space: nowrap</code> on its dashboard so that the numbers indicating posts and comments don't wrap if the table cell is too small.</em>

### Word Wrap

One property that is already well used is <code>word-wrap</code>. It supports one of two values: <code>normal</code> and <code>break-word</code>. If you set <code>word-wrap</code> to <code>break-word</code> and a word is so long that it would overflow the container, it is broken at a random point so that it wraps within the container.

<a href="https://www.igcp.org/"><img loading="lazy" decoding="async" class="32220" title="International Gorilla Conservation Programme" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aab85bec-2658-4292-9b37-b49172129dfa/international-gorilla.jpg" alt="International Gorilla Conservation Programme" width="400" height="203" /></a><br>
<em>The International Gorilla Conservation Programme website uses <code>word-wrap</code> for its commenters' names.</em>

In theory, <code>word-wrap: break-word</code> should only be allowed when <code>text-wrap</code> is set to either <code>normal</code> or <code>suppress</code> (which suppresses line breaking). But in practice and for now, it works even when <code>text-wrap</code> is set to something else.

Bear in mind that according to the specification, the <code>break-strict</code> value for the <code>word-break</code> property is at risk of being dropped.</p>

### Word And Letter Spacing

Two other properties that are often used are <code>word-spacing</code> and <code>letter-spacing</code>. You can use them to control—you guessed it—the spacing between words and letters, respectively. Both properties support three different values that represent optimal, minimum and maximum spacing.

<a href="https://www.showandtellsale.com/"><img loading="lazy" decoding="async" class="32218" title="Show &amp; Tell" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/559e6b98-93fd-4b33-8c7d-0b89bd3573a3/show-and-tell.jpg" alt="Show &amp; Tell" width="600" height="200" /></a><br>
<em>Show &amp; Tell uses <code>letter-spacing</code> on its navigation links.</em>

For <code>word-spacing</code>, setting only one value corresponds to the optimal spacing (and the other two are set to <code>normal</code>). When setting two values, the first one corresponds to the optimal and minimum spacing, and the second to the maximum. Finally, if you set all three values, they correspond to all three mentioned above. With no justification, optimal spacing is used.

It works slightly different for <code>letter-spacing</code>. One value only corresponds to all three values. The others work as they do for <code>word-spacing</code>.

The specifications contain a few <strong>requests for more information and examples</strong> on how <a href="https://dev.w3.org/csswg/css3-text/#white-space-processing">white-space processing</a> will work and how it can be used and be useful for languages such as Japanese, Chinese, Thai, Korean, etc. So, if you'd like help out, why not give it a read (it's not <em>that</em> long), and see how you can contribute?

## Indentation And Hanging Punctuation

Text indentation and hanging punctuation are two typographical features that are <strong>often forgotten</strong> on the Web. This is probably due to one of three factors:

1.  Setting them is not as straightforward as it could be;
2.  There has been a conscious decision not to apply them;
3.  Designers simply aren’t aware of them or don't know how to properly use them.

<img loading="lazy" decoding="async" class="32129" title="Sushi &amp; Robots Journal" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c57338d3-af1e-4c81-bdbc-2848a8cbdd4b/sushi-robots.jpg" alt="Sushi &amp; Robots Journal" width="500" height="364" /><br>
<em>The Sushi &amp; Robots website has hanging punctuation on bulleted lists.</em>

Mark Boulton has a good brief explanation of hanging punctuation in his "Five Simple Steps to Better Typography" series, and Richard Rutter mentions indentation on his website, <a href="https://webtypography.net/">The Elements of Typographic Style Applied to the Web</a>. These are two very good reads for any Web designer.

So, <strong>the theory</strong> is that you should apply a small indentation to every text paragraph after the first one. You can easily do this with an adjacent sibling combinator:

<pre><code class="language-css">p + p {
	text-indent: 1em;
}</code></pre>

This selector targets every paragraph (i.e. <code>p</code>) that follows another paragraph; so the first paragraph is not targeted.

Another typographic rule of thumb is that <strong>bulleted lists and quotes</strong> should be “hung.” This is so that the flow of the text is not disrupted by these visual distractions.

The CSS Text Level 3 specification has an (incomplete) reference to an <a href="https://www.w3.org/TR/css3-text/#hanging-punctuation">upcoming hanging-punctuation property</a>.

For now, though, you can use the <code>text-indent</code> property with negative margins to achieve the desired effect:

<pre><code class="language-css">blockquote {
	text-indent: -0.2em;
}</code></pre>

For bulleted lists, just make sure that the position of the bullet is set to <code>outside</code> and that the container <code>div</code> is not set to <code>overflow: hidden</code>; otherwise, the bullets will not be visible.</p>

## Web Fonts And Font Decoration

### font-face

Much talk has been made on the Web about <code>font-face</code> and whether it’s a good thing—especially after the appearance of <a href="https://typekit.com/">Typekit</a> (and the still-in-private-beta <a href="https://fontdeck.com/">Fontdeck</a>). The debate is mainly about how much visual clutter this could bring to Web designs. Some people (the argument goes) aren't sufficiently font-savvy to be able to pull off a design in which they are free to use basically any font they wish. Wouldn’t our sensitive designer eyes be safer if only tested, approved Web-safe fonts were used?

On whatever side of the argument you fall, the truth is that the examples of websites that use <code>font-face</code> beautifully are numerous.

<a href="https://snook.ca/"><img loading="lazy" decoding="async" class="32131" title="Snook.ca" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1084797e-01ab-465d-ba09-af007f5e35c2/snook.jpg" alt="Snook.ca" width="600" height="437" /></a><br>
<em>Jonathan Snook’s recently redesigned website uses the <code>font-face</code> property.</em>

The <code>font-face</code> property is fairly straightforward to grasp and use. Upload the font you want to use to your website (make sure the licence permits it), give it a name and set the location of the file.

In its basic form, this is what the <code>font-face</code> property looks like:

<pre><code class="language-css">@font-face {
	font-family: Museo Sans;
	src: local(“Museo Sans”), url(MuseoSans.ttf) format(“opentype”);
}</code></pre>

The two required <code>font-face</code> descriptors are <code>font-family</code> and <code>src</code>. In the first, you indicate how the font will be referenced throughout your CSS file. So, if you want to use the font for <code>h2</code> headings, you could have:

<pre><code class="language-css">h2 {
	font-family: Museo Sans, sans-serif;
}</code></pre>

With the second property (<code>src</code>), we are doing two things:

1.  If the font is already installed on the user's system, then the CSS uses the local copy instead of downloading the specified font. We could have skipped this step, but using the local copy saves on bandwidth.
2.  If no local copy is available, then the CSS downloads the file linked to in the URI. We also indicate the format of the font, but we could have skipped that step, too.

For this property <strong>to work in IE</strong>, we would also need the EOT version of the font. Some font shops offer multiple font formats, including EOT, but in many cases we will need to convert the TrueType font using Microsoft’s own <a href="https://www.microsoft.com/typography/WEFT.mspx">WEFT</a>, or another tool such as <a href="https://code.google.com/p/ttf2eot/">ttf2eot</a>.

Some <strong>good resources</strong> for finding great fonts that can be used with <code>font-face</code> are <a href="https://www.fontsquirrel.com/">Font Squirrel</a> and <a href="https://www.fontspring.com/">Fontspring</a>.</p>

### text-shadow

The <code>text-shadow</code> property allows you to <strong>add a shadow to text easily</strong> and purely via CSS. The shadow is applied to both the text and text decoration if it is present. Also, if the text has <code>text-outline</code> applied to it, then the shadow is created from the outline rather than from the text.

<a href="https://neutroncreations.com/"><img loading="lazy" decoding="async" class="32133" title="Neutron Creations" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9f1b44d-dedb-46df-88ed-5434923a564d/neutron.jpg" alt="Neutron Creations" width="600" height="264" /></a><br>
<em>Neutron Creations website uses <code>text-shadow</code>.</em>

With this property you can set the horizontal and vertical position of the shadow (relative to the text), the color of the shadow and the blur radius. Here is a complete <code>text-shadow</code> property:

<pre><code class="language-css">p {
	text-shadow: #000000 1px 1px 1px;
}</code></pre>

Both the color and blur radius (the last value) are optional. You could also use an RGBa color for the shadow, making it transparent:

<pre><code class="language-css">p {
	text-shadow: rgba(0, 0, 0, 0.5) 1px 1px 1px;
}</code></pre>

Here we define the R, G and B values of the color, plus an additional alpha transparency value (hence the <code>a</code>, whose value here is <code>0.5</code>).

The specification still has some open questions about <code>text-shadow</code>, like how should the browser behave when the shadow of an element overlaps the text of an adjoining element? Also, be aware that multiple text shadows and the <code>text-outline</code> property may be dropped from the specification.</p>

### New Text-Decoration Properties

One problem with the <code>text-underline</code> property is that it gives us little control. The <a href="https://dev.w3.org/csswg/css3-text/#decoration">latest draft of the specification</a>, however, <strong>suggests new and improved properties</strong> that may give us fine-grained control. You can't use them yet, but we'll give you a condensed sneak peek at what may come.

*   `**text-decoration-line**` Takes the same values as `text-decoration`: `none`, `underline`, `overline` and `line-through`.
*   `**text-decoration-color**` Specifies the color of the line of the previous property.
*   `**text-decoration-style**` Takes the values of `solid`, `double`, `dotted`, `dashed` and `wave`
*   `**text-decoration**` The shorthand for the three preceding properties. If you specify a value of only one of `none`, `underline`, `overline` or `line-through`, then the property will be backwards-compatible with CSS Level 1 and 2\. But if you specify all three values, as in `text-decoration: red dashed underline`, then it is ignored in browsers that don't support them.
*   `**text-decoration-skip**` Specifies whether the text decoration should skip certain types of elements. The proposed values are `none`, `images`, `spaces`, `ink` and `all`.
*   `**text-underline-position**` With this property, you can control, for example, whether the underline should cross the text's descenders or not: `auto`, `before-edge`, `alphabetic` and `after-edge`.</p>

## Controlling Overflow

The <code>text-overflow</code> property lets you control what is shown when <strong>text overflows its container</strong>. For example, if you want all of the items in a list of news to have the same height, regardless of the amount of text, you can use CSS to add ellipses (…) to the overflow to indicate more text. This technique is commonly seen in iPhone apps and websites.

<a href="https://www.nytimes.com/ref/membercenter/iphonefaq.html"><img loading="lazy" decoding="async" class="32135" title="The New York Times iPhone App" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3242bd4-8c21-4281-8b98-43fc0fcd854d/nyt-app.jpg" alt="The New York Times iPhone App" width="320" height="480" /></a><br>
<em>The New York Times iPhone app uses an ellipsis for overflowing text.</em>

This property works in the latest versions of Safari and Opera and in IE6 (where the overflowing element should have a set width, such as <code>100%</code>) and IE7. To be able to apply the property to an element, the element has to have <code>overflow</code> set to something other than <code>visible</code> and <code>white-space: nowrap</code>. To make it work in Opera, you need to add the vendor-specific property:

<pre><code class="language-css">li {
	white-space: nowrap;
	width: 100%;
	overflow: hidden;
	-o-text-overflow: ellipsis;
	text-overflow: ellipsis;
}</code></pre>

In the <a href="https://dev.w3.org/csswg/css3-text/#text-overflow">Editor's draft of the specification</a>, you can see that other properties related to <code>text-overflow</code> are being considered, such as <code>text-overflow-mode</code> and <code>text-overflow-ellipsis</code>, for which <code>text-overflow</code> would be the shorthand.</p>

## Alignment And Hyphenation

Controlling hyphenation online is tricky. <strong>Many factors need to be considered</strong> when setting automatic hyphenation, such as the fact that different rules apply to different languages. Take Portuguese, in which you can hyphenate a word only at the end of a syllable; for double consonants, the hyphen must be located right in the middle.

The specification is still being developed, but the proposed properties are:

*   `hyphenate-dictionary`;
*   `hyphenate-before` and `hyphenate-after`;
*   `hyphenate-lines`;
*   `hyphenate-character`.

<a href="https://www.w3.org/TR/2007/WD-css3-gcpm-20070205/#hyphenation"><img loading="lazy" decoding="async" class="32221" title="Hyphenation draf spec" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddea0686-cea1-4179-a6b1-8bb91e23464b/hyphenation.jpg" alt="Hyphenation draf spec" width="600" height="318" /></a><br>
<em>Proposed specification for hyphenation on the W3C website.</em>

This is a good example of how the <strong>input of interested Web designers</strong> is vital. Thinking about and testing these properties before they are finalized has nothing to do with being "edgy" or with showing off. By <strong>proposing changes to the specification</strong> and illustrating our comments with examples, we are contributing to a better and stronger spec.

Another CSS3 property that hasn't been implemented in most browsers (only IE supports it, and only partially) is <code>text-align-last</code>. If your text is set to <code>justify</code>, you can define how to align the last line of a paragraph or the line right before a forced break. This property takes the following values: <code>start</code>, <code>end</code>, <code>left</code>, <code>right</code>, <code>center</code> and <code>justify</code>.</p>

## Unicode Range And Language

### Unicode Range

The <code>unicode-range</code> property lets you define the <strong>range of Unicode characters supported</strong> by a given font, rather than providing the complete range. This can be useful to restrict support for a wide variety of languages or mathematical symbols, and thus reduce bandwidth usage.

Imagine that you want to include some Japanese characters on your page. Using the <code>font-face</code> rule, you can have multiple declarations for the same <code>font-family</code>, each providing a different font file to download and a different Unicode range (or even overlapping ranges). The browser should only download the ranges needed to render that specific page.

To see examples of how <code>unicode-range</code> could work, head over to the <a href="https://www.w3.org/TR/css3-fonts/#character-range-the-unicode-range-descri">spec's draft page</a>.</p>

### Language

Use the <code>:lang</code> pseudo-class to create <strong>language-sensitive typography</strong>. So, you could have one background color for text set in French (<code>fr</code>) and another for text set in German (<code>de</code>):

<pre><code class="language-css">div:lang(fr) {
	background-color: blue;
}

div:lang(de) {
	background-color: yellow;
}</code></pre>

You might be wondering why we couldn't simply use an attribute selector and have something like the following:

<pre><code class="language-css">div[lang|=fr] {
	background-color: blue;
}</code></pre>

Here, we are targeting all <code>div</code> elements whose <code>lang</code> attribute is or starts with <code>fr</code>, followed by an <code>-</code>. But if we had elements inside that <code>div</code>, they wouldn't be targeted by this selector because their <code>lang</code> attribute isn't specified. By using the <code>:lang</code> pseudo-class, the <code>lang</code> attribute is <strong>inherited to all children of the elements</strong> (the whole <code>body</code> element could even be holding the attribute).

The good news is that all latest versions of the major browsers support this pseudo-class.</p>

## Conclusion

In surveying the examples in this article, you may be <strong>wondering why to bother</strong> with most of them.

True, the specification is far from being approved, and it could change over time, but now is the time for <strong>experimentation and to contribute</strong> to the final spec.

Try out these new properties, and think of how they could be improved or how you could implement them to make your life easier in future. <strong>Having examples of implementations</strong> is important to the process of adding a property to the spec and, moreover, of implementing it in browsers.

You can start with the simple step of subscribing to the <a href="https://www.w3.org/blog/CSS">CSS Working Group blog</a> to keep up to date on the latest developments.

So, do your bit to improve the lot of future generations of Web designers… and your own!

### Resources and Interesting Links

*   [CSS3 Text (Editor's Draft)](https://dev.w3.org/csswg/css3-text/), W3C
*   [Hyphenation](https://www.w3.org/TR/2007/WD-css3-gcpm-20070205/#hyphenation), W3C
*   [CSS3 Fonts](https://www.w3.org/TR/css3-fonts/), W3C
*   [The Elements of Typographic Style Applied to the Web](https://webtypography.net/)
*   [Type Experiments with HTML](https://www.everydayworks.com/?cat=52)
*   [Styling a Poem With Advanced CSS Selectors](https://webdesignernotebook.com/css/styling-a-poem-with-advanced-css-selectors/)
*   [CSS3: Examples and Best Practices](https://www.webdesignerwall.com/trends/css3-examples-and-best-practices/)

{{< signature "al" >}}


---
title: Avoiding Faux Weights And Styles With Google Web Fonts
slug: avoiding-faux-weights-styles-google-web-fonts
image: null
date: 2012-07-11T19:14:02.000Z
author: laura-franz
description: >-
  If you’re using Google Web Fonts on your websites, then there’s a very good
  chance that 1 in 5 visitors are seeing faux bold and italic versions of your
  fonts — even if you correctly selected and used all of the weights and styles.
  That’s because the implementation method recommended by Google Web Fonts
  doesn’t work with Internet Explorer 7 or 8.
categories:
  - Typography
  - Fonts
---
If you’re using Google Web Fonts on your websites, then there’s a very good chance that 1 in 5 visitors are seeing faux bold and italic versions of your fonts — even if you correctly selected and used all of the weights and styles. That’s because the implementation method recommended by Google Web Fonts doesn’t work with Internet Explorer 7 or 8.

As an experienced print and Web typographer, I embrace and use the term “font” when talking about Web fonts; it’s the term used in CSS syntax and by a myriad of Web font providers.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Setting Weights And Styles With The @font-face Declaration](https://www.smashingmagazine.com/2013/02/setting-weights-and-styles-at-font-face-declaration/)
*   [Taking A Second Look At Free Fonts](https://www.smashingmagazine.com/2014/03/taking-a-second-look-at-free-fonts/)
*   [The Good, The Bad And The Great Examples Of Web Typography](https://www.smashingmagazine.com/2014/12/the-good-the-bad-and-the-great-examples-of-web-typography/)
*   [Responsive Typography With Sass Maps](https://www.smashingmagazine.com/2015/06/responsive-typography-with-sass-maps/)

## Faux Bold And Italic Fonts Are Stretched And Slanted

Any designer who loves type will tell you that faux bold and italic aren’t beautiful. When a browser can’t find the true bold or italic version of a font, it will often “fake it” — creating faux bold and italic by stretching and slanting the original font.

{{% feature-panel %}}

### Faux Bold

Faux bold is made by slightly stretching the vertical strokes of the original font. In the image below, I’ve used Droid Sans Bold, which has consistent strokes. Yet in the faux bold, the vertical strokes are a little thicker than the horizontal strokes. This is most noticeable in the letter “e”; the top of the letter, where the stroke is thinnest, looks pointy.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32053258-2ef5-4271-b0b1-c7f6b23b1f9c/1-big-bold.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134558" title="1_big_bold" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32053258-2ef5-4271-b0b1-c7f6b23b1f9c/1-big-bold.jpg" alt="" width="500" height="250" /></a><br>
<em>A faux bold (top) slightly stretches the vertical strokes of the original font. This creates odd shapes, like the pointy top of the letter “e.” A true bold (bottom) is more consistent between horizontal and vertical strokes.</em>

### Faux Italic

Faux italic is made by slanting the original font at an angle. In the image below, I’ve used Droid Serif italic. The faux italic is missing the tail on the lowercase “f,” while the lowercase “a” continues to have the double-story shape. In a true italic font, the “f” and “a” look more calligraphic — or handwritten — especially in serif fonts. If you’ve chosen a serif font for an older, more traditional feel, then you’ll probably want to preserve these true characteristics of italic.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/727263b0-551f-40f9-93bc-12324d6b39b5/2-big-italic.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134561" title="2_big_italic" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/727263b0-551f-40f9-93bc-12324d6b39b5/2-big-italic.jpg" alt="" width="500" height="250" /></a><br>
<em>Faux italic (top) is made by slanting the original font. True italic (bottom) often has traditional calligraphic characteristics, such as the extended stroke on the “f,” the single-story “a” and the rounded “e.” </em>

### Faux Bold Italic

Faux bold italic both stretches the vertical strokes and slants the letters at an angle. The resulting letters are clunky compared to the rhythm and texture of a true bold italic.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e9253b7-45f7-4d5b-9d7c-729756a80c66/3-big-bolditalic.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134564" title="3_big_bolditalic" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e9253b7-45f7-4d5b-9d7c-729756a80c66/3-big-bolditalic.jpg" alt="" width="500" height="250" /></a><br>
<em>Faux bold italic (top) is both stretched and slanted. True bold italic (bottom) has a thoughtful rhythm and texture. </em>

Faux bold and italic are not as beautiful as the real thing. But when it comes to text, even more important than beauty is readability.</p>

## Faux Bold And Italic Undermine Reading

Faux bold and italic are often less legible, which in turn undermines the readability of text. When letters are stretched and slanted, the strokes and spaces are no longer well balanced.

### Well-Balanced Strokes and Spaces Improve Readability

If you’ve ever had to read a bad photocopy (or scan) for a class, conference or meeting, then you already appreciate how important strokes and spaces are for reading complex text.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af00f694-7833-4580-ae90-709ba1985d7c/4-photcopies.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134566" title="4_photcopies" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af00f694-7833-4580-ae90-709ba1985d7c/4-photcopies.png" alt="" width="500" height="300" /></a><br>
<em>Reproductions that are too dark or too light are hard to read. Too dark and we lose the spaces in the letters (left); too light and we lose the strokes in the letters (right).</em>

If a photocopy or scan is too dark, we lose the spaces in and around the letterforms. If a photocopy or scan is too light, we lose some of the strokes in the letterforms. In both cases, text is less legible. Reading speed slows as we try to identify the letters and words. We experience brain fatigue as we find ourselves rereading phrases to make out the words, leaving less energy for comprehension.

A good balance between strokes and spaces improves legibility and helps us read more quickly and easily.</p>

### Faux Bold, Strokes and Spaces

Because faux bold is created by stretching the vertical strokes of letters, the top and bottom strokes on rounded forms are often too thin. This makes letters like “e,” “c” and “s” start to break on the top and bottom curves. Meanwhile, letters with a diagonal stroke, such as ”w” and “N,” get too heavy and start to pop out of the rhythm of the text.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4269aab3-a890-4321-8c72-aaadf118a470/5-bold-text.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134567" title="5_bold_text" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4269aab3-a890-4321-8c72-aaadf118a470/5-bold-text.jpg" alt="" width="500" height="404" /></a><br>
<em>Droid Sans bold. The faux bold (top) is slightly less legible. The tops and bottoms of the rounded letters — like “e,” “c” and “s” — tend to disappear. Diagonal letters, like “w” and “N,” are too bold. True bold text (bottom) is more consistent.</em>

### Faux Italic, Strokes and Spaces

Because faux italic is created by slanting the original font at an angle, the spaces in the letters get condensed. This is a particular problem in the lowercase “a,” which continues to have two counterforms. Ironically, while faux italic letters feel more squished and are more difficult to read, they often take up more room, and fewer characters fit on a line.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33703b99-dd1c-4705-863a-36d74cab6a2b/6-italic-text.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134568" title="6_italic_text" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33703b99-dd1c-4705-863a-36d74cab6a2b/6-italic-text.jpg" alt="" width="500" height="368" /></a><br>
<em>Droid Serif italic. The faux italic (top) is less legible. Spaces within the letters are more condensed. The text itself feels smaller, even though fewer characters fit on each line. True italic (bottom) is not just more visually pleasing, but more legible and, thus, easier to read.</em>

## Fixing Google Web Fonts Bold And Italic In IE 7 And 8

Because real bold and italic fonts are usually more beautiful and more readable than their faux counterparts, we should make them work on as many browsers as possible.

As is usually the case, figuring out how to fix the problem starts by understanding why the proper bold and italic fonts don’t work in the first place.

In “<a href="https://www.alistapart.com/articles/say-no-to-faux-bold/">Say No to Faux Bold</a>,” recently published on A List Apart, Alan Stearns reminds us that a good start is to use fonts for which bold and italic styles are available — and to actually include the bold and italic styles that you need when choosing the fonts in the Google Web Fonts interface.

But choosing and using bold and italic styles aren’t enough.</p>

### Multiple Weights and Styles Don’t Work in IE 7 and 8

Google Web Fonts instructs us to implement its fonts by checking off all of the font weights and styles that we want to use, then copying the link it provides, and pasting it into the head of our HTML document.

For example, to use Droid Serif regular, italic, bold and bold italic, we would select all four weights and styles, like so:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55de7553-a9cf-4c9c-ab1f-45bade6fc909/7-google-webfont-fixed.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134569" title="7_google_webfont_fixed" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55de7553-a9cf-4c9c-ab1f-45bade6fc909/7-google-webfont-fixed.png" alt="" width="500" height="300" /></a><br>
<em>Droid Serif on Google Web Fonts</em>

In response, Google Web Fonts will create a link to all four styles:

<pre><code class="language-markup tmp-html">&lt;link href="https://fonts.googleapis.com/css?family=Droid+Serif:400,400italic,700,700italic" rel="stylesheet" type="text/css"&gt;</code></pre>

This link points each browser to its own browser-specific source. For example, Firefox is taken to a document that returns the @font-face declarations below. Note that the declarations use the <strong>same font-family name</strong> each time. This would cause a problem in IE 7 and 8, which don’t recognize multiple styles and weights that use the same font-family name.

<pre><code class="language-css">@font-face {
font-family: 'Droid Serif';
font-style: normal;
font-weight: bold;
src: local('Droid Serif Bold'), local('DroidSerif-Bold'), url('https://themes.googleusercontent.com/static/fonts/droidserif/v3/QQt14e8dY39u-eYBZmppwTqR_3kx9_hJXbbyU8S6IN0.woff') format('woff');
}

@font-face {
font-family: 'Droid Serif';
font-style: italic;
font-weight: normal;
src: local('Droid Serif Italic'), local('DroidSerif-Italic'), url('https://themes.googleusercontent.com/static/fonts/droidserif/v3/cj2hUnSRBhwmSPr9kS5899kZXW4sYc4BjuAIFc1SXII.woff') format('woff');
}

@font-face {
font-family: 'Droid Serif';
font-style: italic;
font-weight: bold;
src: local('Droid Serif Bold Italic'), local('DroidSerif-BoldItalic'), url('https://themes.googleusercontent.com/static/fonts/droidserif/v3/c92rD_x0V1LslSFt3-QEpgRV2F9RPTaqyJ4QibDfkzM.woff') format('woff');
}

@font-face {
font-family: 'Droid Serif';
font-style: normal;
font-weight: normal;
src: local('Droid Serif'), local('DroidSerif'), url('https://themes.googleusercontent.com/static/fonts/droidserif/v3/0AKsP294HTD-nvJgucYTaIbN6UDyHWBl620a-IRfuBk.woff') format('woff');
}</code></pre>

One way around the “single font-family, multiple weights and styles” problem is to send IE 7 and 8 to a different source. Google Web Fonts does this, but unfortunately the @font-face declaration looks like this:

<pre><code class="language-css">@font-face {
font-family: 'Droid Serif';
font-style: normal;
font-weight: normal;
src: url('https://themes.googleusercontent.com/static/fonts/droidserif/v3/0AKsP294HTD-nvJgucYTaGfQcKutQXcIrRfyR5jdjY8.eot');
src: local('Droid Serif'), local('DroidSerif'), url('https://themes.googleusercontent.com/static/fonts/droidserif/v3/0AKsP294HTD-nvJgucYTaGfQcKutQXcIrRfyR5jdjY8.eot') format('embedded-opentype'), url('https://themes.googleusercontent.com/static/fonts/droidserif/v3/0AKsP294HTD-nvJgucYTaIbN6UDyHWBl620a-IRfuBk.woff') format('woff');
}</code></pre>

This doesn’t help us. The single declaration <strong>sets the <code>font-weight</code> to <code>normal</code> and <code>font-style</code> to <code>normal</code></strong>, thus forcing IE 7 and 8 to “fake it” when requested to render bold and italic versions of the font.

The result? Faux bold and italic — even if we had carefully selected a font with bold and italic styles, and even if we had implemented all of the weights and styles as instructed.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32e5124a-14aa-4aca-83f2-c69b7e9d68b5/8-ie8and9.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134570" title="8_IE8and9" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32e5124a-14aa-4aca-83f2-c69b7e9d68b5/8-ie8and9.jpg" alt="" width="500" height="475" /></a><br>
<em>Droid Serif. IE 8 delivers faux bold and italic (top) because it works only with a single @font-face declaration and a single font-family name. Firefox delivers true bold and italic (bottom) because it can handle multiple weights and styles that are assigned to a single font-family.</em>

### A Common Fix Causes Problems in Opera (and Android)

A common “fix” for this problem is to insert separate links — one for each of the styles and weights used — into the head of the HTML document. That is, we select each weight and style of the font separately, taking the time to copy and paste each unique link into the head of the HTML document. The syntax for Droid Serif would look like this:

<pre><code class="language-markup tmp-html">&lt;link href="https://fonts.googleapis.com/css?family=Droid+Serif" rel="stylesheet" type="text/css"&gt;
&lt;link href="https://fonts.googleapis.com/css?family=Droid+Serif:400italic" rel="stylesheet" type="text/css"&gt;
&lt;link href="https://fonts.googleapis.com/css?family=Droid+Serif:700" rel="stylesheet" type="text/css"&gt;
&lt;link href="https://fonts.googleapis.com/css?family=Droid+Serif:700italic" rel="stylesheet" type="text/css"&gt;</code></pre>

While this solves the problem in IE 7 and 8, referencing four CSS files for a single font family increases the number of requests that the client makes to the server and <a href="https://developers.google.com/speed/docs/best-practices/rtt">contributes to latency</a>. The fix also creates a new typographic problem in Opera (including Opera Mobile on Android). Opera renders text using the last weight and style served; so, if the last weight and style served is bold italic, then the font will come in as bold italic over the entire page.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d89c22d3-a821-4d61-afed-a979781ad125/9-ie8andopera.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134571" title="9_IE8andopera" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d89c22d3-a821-4d61-afed-a979781ad125/9-ie8andopera.jpg" alt="" width="500" height="475" /></a><br>
<em>Droid Serif. Using separate links to each weight and style fixes the problem in IE 7 and 8 (top), but it causes problems in Opera (bottom). Opera renders text using the last weight and style served.</em>

### Using a Conditional Comment Works Across Browsers

There’s a better solution: adding a conditional comment. IE 7 and 8 are the only browsers that need the fonts to be served separately. And because conditional comments work only in IE, the solution is solid. The new syntax looks like this:

<pre><code class="language-markup tmp-html">&lt;link href="https://fonts.googleapis.com/css?family=Droid+Serif:400,400italic,700,700italic" rel="stylesheet" type="text/css"&gt;
&lt;!--[if IE]&gt;
&lt;link href="https://fonts.googleapis.com/css?family=Droid+Serif" rel="stylesheet" type="text/css"&gt;
&lt;link href="https://fonts.googleapis.com/css?family=Droid+Serif:400italic" rel="stylesheet" type="text/css"&gt;
&lt;link href="https://fonts.googleapis.com/css?family=Droid+Serif:700" rel="stylesheet" type="text/css"&gt;
&lt;link href="https://fonts.googleapis.com/css?family=Droid+Serif:700italic" rel="stylesheet" type="text/css"&gt;
&lt;![endif]--&gt;</code></pre>

Notice how all browsers except IE are instructed to use the usual method for accessing Google Web Fonts. This keeps bold and italic fonts loading correctly (and more quickly) in Firefox, Opera, Chrome and Safari. Meanwhile, IE is instructed to access each weight and style separately. This fixes the faux bold and italic problem in IE 7 and 8, and it doesn’t create any new problems in more recent versions of the browser.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58465517-e723-48b5-990f-35aee1f07793/10-all-work.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134572" title="10_all_work" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58465517-e723-48b5-990f-35aee1f07793/10-all-work.jpg" alt="" width="500" height="785" /></a><br>
<em>Using a conditional comment, we get true bold and italic to load correctly across browsers. Top to bottom: IE 8, IE 9, Firefox 11, Google Chrome 18, Safari 5, Opera 11.62.</em>

## Help Visitors Enjoy Their Reading Experience

If people are on your website, they’re probably either skimming quickly looking for something or they’ve found what they’re looking for and want to read it as easily as possible. Either way, keeping the text readable will help them achieve their goal.</p>

### Bold and Italic Help Organize Content

From a macro perspective, bold and italic forms of a font are important for people skimming your website. Bold and italic forms add emphasis — both <strong>strong</strong> and <em>subtle</em> — to text. They can help visitors understand the organization of content before they even start to read it.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ae348c0-36ac-4921-9bfa-b1da694c5325/11-organize-text.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134573" title="11_organize_text" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ae348c0-36ac-4921-9bfa-b1da694c5325/11-organize-text.png" alt="" width="500" height="360" /></a><br>
<em>Bold and italic create levels of emphasis, which helps to visually organize text (left). The same text without bold or italic (right) would feel more like a narrative.</em>

### True Bold and Italic Are Easier to Read

From a micro perspective, true bold and italic forms are important for people engaged in more sustained reading on your website. A proper balance between strokes and spaces improves legibility and makes text easier to read, thus minimizing brain fatigue and giving visitors a more pleasurable experience of the website. Type designers use their time and talent to create Web font families that are both legible and beautiful; for us, it’s just a matter of getting the true weights and styles to load properly.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4521f7ef-7d6c-489f-ba5a-d7c41e6a4c87/12-final-bold-italic.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="134574" title="12_final_bold_italic" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4521f7ef-7d6c-489f-ba5a-d7c41e6a4c87/12-final-bold-italic.png" alt="" width="500" height="181" /></a><br>
<em>True bold and italic text is not just more visually pleasing, but also easier to read.</em>

Waiting until Google fixes this problem might be tempting, but it’s been on Google’s radar since June 2010. Making sure that the bold and italic fonts served up by Google Web Fonts work across browsers is up to us. And it takes only a minute. Don’t let 1 in 5 visitors to your website down.</p>

### Further Resources

*   “[Say No to Faux Bold](https://www.alistapart.com/articles/say-no-to-faux-bold/)” Alan Stearns
*   “[It’s About Legibility](https://new.fonts.com/content/learning/fontology/level-4/fine-typography/legibility)” Allan Haley
*   “[Is the Font Easy to Read? Anatomy and Legibility](https://goodwebfonts.com/legibility_twd.pdf)” (PDF), Laura Franz This excerpt from the book _Typographic Web Design_ is in PDF format. View it in Adobe Acrobat to compare fonts via rollovers.

<em>(al) (il)</em>


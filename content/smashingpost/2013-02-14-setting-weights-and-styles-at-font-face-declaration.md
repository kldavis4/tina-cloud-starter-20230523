---
title: How To Set Weights And Styles With The @font-face Declaration
slug: setting-weights-and-styles-at-font-face-declaration
image: null
date: 2013-02-14T15:14:41.000Z
author: laura-franz
description: >-
  If people are on your website, they’re probably either skimming quickly,
  looking for something, or they’ve found what they’re looking for and want to
  read it as easily as possible. Either way, **keeping text readable** will help
  them achieve their goal.
categories:
  - Coding
  - Typography
  - Techniques
  - Essentials
---
If people are on your website, they’re probably either skimming quickly, looking for something, or they’ve found what they’re looking for and want to read it as easily as possible. Either way, <strong>keeping text readable</strong> will help them achieve their goal.

### Bold and Italic Help to Organize Content

A few months ago, I wrote an article on “<a title="Avoiding Faux Weights and Styles with Google Web Fonts" href="https://www.smashingmagazine.com/2012/07/11/avoiding-faux-weights-styles-google-web-fonts/">Avoiding Faux Weights and Styles with Google Web Fonts</a>.” I ended the article by showing that weights and styles are an important UX element when setting text. Bold and italic forms of a font help people to skim your website. They add emphasis — both <strong>strong</strong> and <em>subtle</em> — that can help visitors understand the organization of content before even starting to read it.

<img loading="lazy" decoding="async" class="154207" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/733a84d9-347c-498b-8d70-72334e9d7b27/1-organize-text.png" alt="1_organize_text" width="500" height="360" /><br>
<em>Weights and styles are an important UX element. Bold and italic help readers to see structure and to skim the text more efficiently (left). The same text without bold or italic (right) feels more like a narrative.</em>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The @Font-Face Rule And Useful Web Font Tricks](https://www.smashingmagazine.com/2011/03/the-font-face-rule-revisited-and-useful-tricks/)
*   [80 Beautiful Typefaces For Professional Design](https://www.smashingmagazine.com/2007/08/80-beautiful-fonts-typefaces-for-professional-design/)
*   [How To Choose The Right Face For A Beautiful Body](https://www.smashingmagazine.com/2012/05/how-to-choose-the-right-face-for-a-beautiful-body/)
*   [How To Choose A Typeface — A Step-By-Step Guide!](https://www.smashingmagazine.com/2011/03/how-to-choose-a-typeface/)

{{% feature-panel %}}

In this article, we’ll start where we left off. Because weights and styles help our visitors to read our content, we should make sure they work! And getting weights and styles to work correctly using the @font-face declaration can be a bit crazy-making. Let’s look at two popular approaches to setting weights and styles with the @font-face declaration. I’ll show you why they are not the best solutions, and show you a third more effective approach to follow.</p>

## Unique Font-Family Names, Normal Weights And Styles

If you’ve used one of <a href="https://www.fontsquirrel.com">FontSquirrel</a>’s amazing @font-face kits, then you’re familiar with this approach to setting weights and styles. The CSS provided in every kit uses a <em>unique</em> font-family name for each weight and style, and sets the weight and style in the @font-face declaration to <code>normal</code>.

For example, the syntax for Ubuntu Italic and Ubuntu Bold looks like this:

<pre><code class="language-css">@font-face {
   font-family: 'UbuntuItalic';
      src: url('Ubuntu-RI-webfont.eot');
      src: url('Ubuntu-RI-webfont.eot?#iefix') format('embedded-opentype'),
           url('Ubuntu-RI-webfont.woff') format('woff'),
           url('Ubuntu-RI-webfont.ttf') format('truetype'),
           url('Ubuntu-RI-webfont.svg#UbuntuItalic') format('svg');
   font-weight: normal;
   font-style: normal;
}

@font-face {
   font-family: 'UbuntuBold';
      src: url('Ubuntu-B-webfont.eot');
      src: url('Ubuntu-B-webfont.eot?#iefix') format('embedded-opentype'),
           url('Ubuntu-B-webfont.woff') format('woff'),
           url('Ubuntu-B-webfont.ttf') format('truetype'),
           url('Ubuntu-B-webfont.svg#UbuntuBold') format('svg');
   font-weight: normal;
   font-style: normal;
}</code></pre>

Notice that the font-family names are unique, with each font-family name accessing the appropriate Web font files. For example, <code>UbuntuItalic</code> accesses <code>Ubuntu-RI-webfont.woff</code>, while <code>UbuntuBold</code> accesses <code>Ubuntu-B-webfont.woff</code>.

Also, notice that the <code>font-weight</code> and <code>font-style</code> for both @font-face declarations are set to <code>normal</code>.</p>

### Styling Text Using This Method

To style text using this method, use the appropriate font-family name, and keep all weights and styles set to <code>normal</code>. For example, the Regular, Regular Italic, Bold and Bold Italic headings below are set with classes. The classes are styled like so:

<pre><code class="language-css">.u400 {
   font-family: 'UbuntuRegular', arial, sans-serif;
   font-weight: normal;
   font-style: normal;
}

.u400i {
   font-family: 'UbuntuRegularItalic', arial, sans-serif;
   font-weight: normal;
   font-style: normal;
}

.u700 {
   font-family: 'UbuntuBold', arial, sans-serif;
   font-weight: normal;
   font-style: normal;
}

.u700i {
   font-family: 'UbuntuBoldItalic', arial, sans-serif;
   font-weight: normal;
   font-style: normal;
}</code></pre>

<img loading="lazy" decoding="async" class="154208" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee459fce-3d06-43e1-88f3-007103c37ace/2-unique-font-families.png" alt="2_unique_font-families" width="500" height="600" /><br>
<em>Ubuntu Regular, Italic, Bold and Bold Italic on Windows 7 in Internet Explorer 8 (top) and on Mac OS X in Chrome 23 (bottom). Unique font-family names with normal weights and styles (á la FontSquirrel) work fine.</em>

### Make Sure the Weights and Styles Match!

Because the weights and styles are set to <code>normal</code> in the @font-face declarations, keeping the weights and styles set to <code>normal</code> when styling the text is important. Otherwise, the bolds may double-bold (some browsers will add a bold weight to the already bold Web font), and the italics may double-italic (some browsers will add an italic style to the already italic Web font).

For example, let’s say we <em>incorrectly</em> set the <code>font-style</code> to <code>italic</code> and the <code>font-weight</code> to <code>700</code> (bold) in our corresponding classes:

<div class="break-out">

<pre><code class="language-css">.u400 {
   font-family: 'UbuntuRegular', arial, sans-serif;
   font-weight: normal;
   font-style: normal;
}

.u400i {
   font-family: 'UbuntuRegularItalic', arial, sans-serif;
   font-weight: normal;
   font-style: italic;
}

.u700 {
   font-family: 'UbuntuBold', arial, sans-serif;
   font-weight: 700;
   font-style: normal;
}

.u700i {
   font-family: 'UbuntuBoldItalic', arial, sans-serif;
   font-weight: 700;
   font-style: italic;
}</code></pre></div>

The fonts will render incorrectly in Mac OS X browsers and on iPad Safari browsers.

<img loading="lazy" decoding="async" class="154209" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/826d130d-e233-4838-9876-26e5b9e2579f/3-unique-double-bold.png" alt="3_unique_double-bold" width="500" height="600" /><br>
<em>When using normal weights and styles in the @font-face declaration, give text elements normal weights and styles, too. Otherwise, your text may end up with a double-bold and double-italic. If you set text elements as bold or italic, then Ubuntu Italic, Bold and Bold Italic won’t double-bold or double-italic on Windows 7 in Internet Explorer 8 (top). But look at what happens on Mac OS X in Firefox 17 and on iPad 3 with iOS 5.1 in Safari (bottom) — yikes!</em>

### Using &lt;em&gt; and &lt;strong&gt; Elements

While <code>&lt;em&gt;</code> and <code>&lt;strong&gt;</code> can be styled to communicate emphasis and importance in a variety of ways, they are often used in their default forms: with <code>&lt;em&gt;</code> set to italic text and <code>&lt;strong&gt;</code> set to bold text.

For example, the paragraph below is styled like so:

<div class="break-out">

<pre><code class="language-css">p {
   font-family: 'UbuntuRegular', arial, sans-serif;
   font-weight: normal;
   font-style: normal;
}</code></pre></div>

And the <code>&lt;em&gt;</code> and <code>&lt;strong&gt;</code> elements are left in their default states:

<div class="break-out">

<pre><code class="language-css">em {
   font-style: italic;
}

strong {
   font-weight: bold;
}</code></pre></div>

<img loading="lazy" decoding="async" class="154210" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1d992c2-53bf-41fc-8458-47e33c0a5184/4-unique-em-strong-faux.png" alt="4_unique_em_strong_faux" width="498" height="201" /><br>
<em>Applying <code>&lt;em&gt;</code> and <code>&lt;strong&gt;</code> in their default states results in faux italic and faux bold.</em>

The result is a faux italic and a faux bold. Why? Because the paragraph is set to Ubuntu Regular, with the weight and style set to <code>normal</code>. When the <code>&lt;em&gt;</code> element is applied, the text remains Ubuntu Regular but is slanted to look like it’s italic. Notice the angular “e” and the double-story “a.” When the <code>&lt;strong&gt;</code> element is applied, the text remains Ubuntu Regular but is stretched to look like it’s bold. Notice the letter “e” is no longer monoline — the sides of the letter look thicker than the top and bottom of the letter.

We can fix this problem by making sure the <code>&lt;em&gt;</code> and <code>&lt;strong&gt;</code> elements use the correct font-family name. For example, the paragraph below continues to be styled like so:

<div class="break-out">

<pre><code class="language-css">p {
   font-family: 'UbuntuRegular', arial, sans-serif;
   font-weight: normal;
   font-style: normal;
}</code></pre></div>

And the <code>&lt;em&gt;</code> and <code>&lt;strong&gt;</code> elements are styled to use the correct corresponding font-family names:

<div class="break-out">

<pre><code class="language-css">em {
   font-family: 'UbuntuRegularItalic', arial, sans-serif;
   font-weight: normal;
   font-style: normal;
}

strong {
   font-family: 'UbuntuBold', arial, sans-serif;
   font-weight: normal;
   font-style: normal;
}</code></pre></div>

Notice that the <code>font-weight</code> and <code>font-style</code> for both <code>&lt;em&gt;</code> and <code>&lt;strong&gt;</code> are set to <code>normal</code>. This is counterintuitive, but necessary so that the text doesn’t end up with a double-italic or a double-bold.

<img loading="lazy" decoding="async" class="154211" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1b90790-82f0-4b63-a930-4c7be3e1b8cc/5-unique-em-strong-fixed.png" alt="5_unique_em_strong_fixed" width="498" height="169" /><br>
<em>Using the correct font-family names — and setting weights and styles to <code>normal</code> — results in true italic and true bold.</em>

The result is a true italic and true bold. Why? Because while the paragraph is set to Ubuntu Regular, the <code>&lt;em&gt;</code> element is set to Ubuntu Italic and the <code>&lt;strong&gt;</code> element is set to Ubuntu Bold — and all weights and styles are set to <code>normal</code>.</p>

### Problem: If the Fallback Font Loads, Weights and Styles Will Be Lost

While purposely stripping out weights and styles is counterintuitive, using a unique font-family name and normal weights and styles does work — as long as the Web font loads.

If the fallback font loads, then all bolds and italics will be lost — because we had set all weights and styles to <code>normal</code> — thus making it harder for readers to see the structure of your website’s content and making it harder for them to skim the text.

<img loading="lazy" decoding="async" class="154212" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db2c814f-9979-43f9-ac19-f531eff00db8/6-unique-fontfail.png" alt="6_unique_fontfail" width="496" height="422" /><br>
<em>If the Web font doesn’t load, then the fallback font (here, Times New Roman) will load with a normal weight and style — undermining hierarchy and readability. Remember, we had set all weights and styles to <code>normal</code> when we styled the elements!</em>

### The Short Version

Using unique font-family names combined with setting <code>font-weight</code> and <code>font-style</code> to <code>normal</code> is unforgiving. Mismatching weights and styles could easily result in either faux italic and faux bold or double-italic and double-bold. If the Web font doesn’t load, then the result will be <em>no</em> italic or bold! So, this approach to setting weights and styles using the @font-face declaration isn’t the best solution.</p>

## Style Linking

Another way to set weights and styles is to use the <strong>same font-family name multiple times</strong>, setting the weights and styles in each @font-face declaration to match the weight and style of the Web font file being accessed. This approach is called style linking.

For example, using style linking, the syntax for Ubuntu Italic and Ubuntu Bold would look like this:

<div class="break-out">

<pre><code class="language-css">@font-face {
   font-family: 'Ubuntu';
      src: url('Ubuntu-RI-webfont.eot');
      src: url('Ubuntu-RI-webfont.eot?#iefix') format('embedded-opentype'),
           url('Ubuntu-RI-webfont.woff') format('woff'),
           url('Ubuntu-RI-webfont.ttf') format('truetype'),
           url('Ubuntu-RI-webfont.svg#UbuntuItalic') format('svg');
   font-weight: 400;
   font-style: italic;
}

@font-face {
   font-family: 'Ubuntu';
      src: url('Ubuntu-B-webfont.eot');
      src: url('Ubuntu-B-webfont.eot?#iefix') format('embedded-opentype'),
           url('Ubuntu-B-webfont.woff') format('woff'),
           url('Ubuntu-B-webfont.ttf') format('truetype'),
           url('Ubuntu-B-webfont.svg#UbuntuBold') format('svg');
   font-weight: 700;
   font-style: normal;
}</code></pre></div>

Notice that the font-family names are the same, regardless of what Web font file is being accessed. For example, <code>Ubuntu</code> accesses <code>Ubuntu-RI-webfont.woff</code>, and <code>Ubuntu</code> also accesses <code>Ubuntu-B-webfont.woff</code>. How does that work?

Notice that the <code>font-weight</code> and <code>font-style</code> for each @font-face declaration is set to match the weight and style of the Web font file being accessed. The <code>Ubuntu</code> that accesses the <em>italic</em> Web font file has <code>font-style: italic</code>. The <code>Ubuntu</code> that accesses the <em>bold</em> Web font file has <code>font-weight: 700</code>.

In this method, the weights and styles in the @font-face declarations act as “markers.” When a browser encounters those weights and styles elsewhere in the CSS, it knows which @font-family declaration to use and which Web font files to access.</p>

### Styling Text Using Style Linking

To style text with this method, use the same font family for all versions of the font. Set weights and styles to trigger the correct Web font files that the browser should access. If you want the italic version of the font, make sure to set <code>font-style: italic</code>. For example, the Regular, Regular Italic, Bold and Bold Italic headings below are set with classes. The classes are styled like so:

<div class="break-out">

<pre><code class="language-css">.u400 {
   font-family: 'Ubuntu', arial, sans-serif;
   font-weight: 400;
   font-style: normal;
}

.u400i {
   font-family: 'Ubuntu', arial, sans-serif;
   font-weight: 400;
   font-style: italic;
}

.u700 {
   font-family: 'Ubuntu', arial, sans-serif;
   font-weight: 700;
   font-style: normal;
}

.u700i {
   font-family: 'Ubuntu', arial, sans-serif;
   font-weight: 700;
   font-style: italic;
}</code></pre></div>

<img loading="lazy" decoding="async" class="154213" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28c66bbe-9bb4-4dce-8bd5-1f3ba1fff4bb/7-style-linking.png" alt="7_style-linking" width="500" height="600" /><br>
<em>Ubuntu Regular, Italic, Bold and Bold Italic on Windows 7 in Internet Explorer 8 (top) and on Mac OS X in Chrome 23 (bottom). Using style linking to set weight and style appears to work fine.</em>

### Again, Make Sure the Weights and Styles Match!

Because weight and style are used to “trigger” the correct @font-face declaration, setting weights and styles to match those used in the @font-face declarations is important. As a bonus, when <strong>default rules</strong> for weights and styles are applied by browsers — like italic for <code>&lt;em&gt;</code> and bold for <code>&lt;strong&gt;</code> — then the correct fonts will automatically load (as long as your font has a bold and italic version), because the default rules will also trigger the correct @font-face declaration.

<img loading="lazy" decoding="async" class="154214" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3efd523d-a7d3-4485-8110-0d925c496473/8-style-linking-em-strong.png" alt="8_style-linking_em_strong" width="499" height="172" /><br>
<em>When default rules for weights and styles are applied by browsers — like italic for <code>&lt;em&gt;</code> and bold for <code>&lt;strong&gt;</code> — then the correct fonts will automatically load (as long as your font has a bold and italic version). Again, using style linking to set weight and style appears to work fine.</em>

### Bonus: If the Fallback Font Loads, Weights and Styles Will Be Retained

Unlike the first approach, setting weights and styles with style linking means that weights and styles will be retained even when the Web font fails to load. Why? Because all weights and styles were set correctly (for example, not <code>normal</code>) when styling the text.

<strong>Note:</strong> If the Web font doesn’t load, then the fallback font (here, Times New Roman) will still provide hierarchy — bolds and italics will remain intact. Remember, we set all weights and styles to match the Web fonts when we styled the elements!

But style linking has its own problems…

### Problem: Internet Explorer 7 and 8 Can Only Apply Up to Four Weights and Styles to a Single Font-Family Name

Style linking works — as long as you’re not using more than four weights and styles (and as long as the person reading your Web page isn’t the one of the one in eight people who still use Internet Explorer (IE) 7 or 8). If you use more than four weights and styles on the website, then IE 7 and 8 will convert all <code>light</code> and <code>medium</code> weights to normal, and all <code>black</code> and <code>heavy</code> weights to bold — so, you’ll lose some of your carefully set text.

<img loading="lazy" decoding="async" class="154216" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0511a57-f69e-4f6d-ba03-f58ce9450dea/10-style-linking-fail.png" alt="10_style-linking_fail" width="500" height="545" /><br>
<em>IE 7 and 8 can’t apply more than four weights and styles to a single font-family name. Ubuntu has eight weights and styles. If you used all eight with the font-family name <code>Ubuntu</code>, then the Light, Light Italic, Medium and Medium Italic would convert to Regular and Regular Italic.</em>

### Problem: Crashes Browsers on BlackBerry and iPad 1

No matter how well your fonts load, if the page crashes the browser, people won’t be able to see your content! And as of this writing, Web pages that use style linking crash BlackBerry 9900 browsers on a regular basis. They also crash iPad 1 browsers 100% of the time.</p>

### The Short Version

Using style linking appears to be more forgiving. It greatly reduces the potential for setting text that is faux italic and faux bold, or double-italic and double-bold. In addition, if the Web font doesn’t load, the text will retain both style and weight. But if you’re using more than four weights and styles, then text won’t render properly in IE 7 and 8. In addition, style linking crashes the browsers on BlackBerry and iPad 1 devices. So, this approach to setting weights and styles using the @font-face declaration isn’t the best solution at this time (although the future — when IE 7 and 8, BlackBerry 9900 and iPad 1 are all defunct — looks bright!).</p>

## Unique Font-Family Names, Matching Weights And Styles

A third — and currently the most effective — way to set weights and styles is to merge the first two methods. If you’ve used <del>FontDeck</del> (service closed dec/16) for Web fonts, then you’ll be familiar with this approach.

Use the <em>unique</em> font-family names — which allows IE to show all of the weights and styles you need. Also, use <strong>matching weights and styles</strong> (for example, do <em>not</em> set weights and styles to <code>normal</code>), which will keep the weights and styles intact should the Web font fail.

For example, the syntax for Ubuntu Italic and Ubuntu Bold would like this:

<div class="break-out">

<pre><code class="language-css">@font-face {
   font-family: 'UbuntuItalic';
      src: url('Ubuntu-RI-webfont.eot');
      src: url('Ubuntu-RI-webfont.eot?#iefix') format('embedded-opentype'),
           url('Ubuntu-RI-webfont.woff') format('woff'),
           url('Ubuntu-RI-webfont.ttf') format('truetype'),
           url('Ubuntu-RI-webfont.svg#UbuntuItalic') format('svg');
   font-weight: 400;
   font-style: italic;
}

@font-face {
   font-family: 'UbuntuBold';
      src: url('Ubuntu-B-webfont.eot');
      src: url('Ubuntu-B-webfont.eot?#iefix') format('embedded-opentype'),
           url('Ubuntu-B-webfont.woff') format('woff'),
           url('Ubuntu-B-webfont.ttf') format('truetype'),
           url('Ubuntu-B-webfont.svg#UbuntuBold') format('svg');
   font-weight: 700;
   font-style: normal;
}</code></pre></div>

Notice that the font-family names are unique, with each font-family name accessing the appropriate Web font files. For example, <code>UbuntuItalic</code> accesses <code>Ubuntu-RI-webfont.woff</code>, while <code>UbuntuBold</code> accesses <code>Ubuntu-B-webfont.woff</code>.

Also, notice the weight and style: The <code>font-weight</code> and <code>font-style</code> for each @font-face declaration is set to <strong>match the weight and style</strong> of the Web font file being accessed. The <code>UbuntuItalic</code> that accesses the italic Web font file has <code>font-style: italic</code>. The <code>UbuntuBold</code> that accesses the bold Web font file has <code>font-weight: 700</code>.</p>

### Styling Text Using the Combined Method

To style text with this method, use the unique font-family names, and set weights and styles to match those used in the @font-face declarations. For example, the Light, Light Italic, Regular, Regular Italic, Medium, Medium Italic, Bold and Bold Italic headings below are set with classes. The classes are styled like so:

<div class="break-out">

<pre><code class="language-css">.u300 {
   font-family: 'UbuntuLight', arial, sans-serif;
   font-weight: 300;
   font-style: normal;
}

.u300i {
   font-family: 'UbuntuLightItalic', arial, sans-serif;
   font-weight: 300;
   font-style: italic;
}

.u400 {
   font-family: 'UbuntuRegular', arial, sans-serif;
   font-weight: 400;
   font-style: normal;
}

.u400i {
   font-family: 'UbuntuRegularItalic', arial, sans-serif;
   font-weight: 400;
   font-style: italic;
}

.u700 {
   font-family: 'UbuntuMedium', arial, sans-serif;
   font-weight: 500;
   font-style: normal;
}

.u700i {
   font-family: 'UbuntuMediumItalic', arial, sans-serif;
   font-weight: 500;
   font-style: italic;
}

.u900 {
   font-family: 'UbuntuBold', arial, sans-serif;
   font-weight: 700;
   font-style: normal;
}

.u900i {
   font-family: 'UbuntuBoldItalic', arial, sans-serif;
   font-weight: 700;
   font-style: italic;
}</code></pre></div>

<img loading="lazy" decoding="async" class="154217" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4839d705-fcd2-43c3-ad1a-9e585ed9a135/11-unique-style-linking.png" alt="11_unique_style-linking" width="500" height="545" /><br>
<em>By combining unique font-family names with matching weights and styles, all eight weights and styles of Ubuntu will work — even on Windows 7 in IE 8. And BlackBerry and iPad 1 browsers won’t crash.</em>

### Again, Make Sure the Weights and Styles Match!

Although using unique font-family names means we no longer need the weights and styles to “trigger” the correct @font-face declaration, setting all weights and styles to match is important. Applying weights and styles to text elements will keep them intact in case the Web font fails. Also, because the weights and styles match, the text won’t end up with either a double-bold or double-italic, or a faux bold or faux italic.</p>

### Problem: Using &lt;em&gt; and &lt;strong&gt; Elements

Using unique font-family names brings back an earlier problem: getting <code>&lt;em&gt;</code> and <code>&lt;strong&gt;</code> elements to work properly. Default styling on these elements will result in faux italic and faux bold text.

For example, the three paragraphs below are styled like so:

<div class="break-out">

<pre><code class="language-css">p.light {
   font-family: 'UbuntuLight', arial, sans-serif;
   font-weight: 300;
   font-style: normal;
}

p {
   font-family: 'UbuntuRegular', arial, sans-serif;
   font-weight: normal;
   font-style: normal;
}

p.medium {
   font-family: 'UbuntuMedium', arial, sans-serif;
   font-weight: 500;
   font-style: normal;
}</code></pre></div>

And the <code>&lt;em&gt;</code> and <code>&lt;strong&gt;</code> elements are left in their default states:

<div class="break-out">

<pre><code class="language-css">em {
   font-style: italic;
}

strong {
   font-weight: bold;
}</code></pre></div>

<img loading="lazy" decoding="async" class="154218" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c21aee5d-2160-4407-a84a-ddc6c0e86418/12-unique-style-linking-emstrong-default.png" alt="12_unique_style-linking_EmStrong_default" width="498" height="529" /><br>
<em>Applying <code>&lt;em&gt;</code> and <code>&lt;strong&gt;</code> in their default states will result in faux italic and (usually) faux bold.</em>

The result is a faux italic and a faux bold (when it’s applied). Why? Because we’re using unique font-family names. Let’s look at the middle paragraph. It’s set to Ubuntu Regular, with weight and style set to match (<code>weight: normal</code> and <code>style: normal</code>). When the <code>&lt;em&gt;</code> element is applied, the text remains Ubuntu Regular but is slanted to look like it’s italic. When the <code>&lt;strong&gt;</code> element is applied, the text remains Ubuntu Regular but is stretched to look like it’s bold.

We can fix the bold text by making sure the <code>&lt;strong&gt;</code> element uses the correct font-family name, weight and style:

<div class="break-out">

<pre><code class="language-css">strong {
   font-family: 'UbuntuBold', arial, sans-serif;
   font-weight: 700;
   font-style: normal;
}</code></pre></div>

The <code>&lt;em&gt;</code> is a bit more difficult to fix. We can set it to Ubuntu Regular Italic and use the matching weight and style:

<div class="break-out">

<pre><code class="language-css">em {
   font-family: 'UbuntuRegularItalic', arial, sans-serif;
   font-weight: 400;
   font-style: italic;
}</code></pre></div>

<img loading="lazy" decoding="async" class="154219" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7d8a767-f93b-41a6-9019-319c61df4466/13-unique-style-linking-emstrong-set.png" alt="13_unique_style-linking_EmStrong_set" width="497" height="498" /><br>
<em>Setting <code>&lt;em&gt;</code> to <code>UbuntuRegularItalic</code> and <code>&lt;strong&gt;</code> to <code>UbuntuBold</code> will result in an italic that’s too heavy for light text and too light for medium text.</em>

The result is a bold and italic that are consistent throughout, regardless of the weight of the paragraph text. This may be fine for the <code>&lt;strong&gt;</code> element, but the <code>&lt;em&gt;</code> element looks a bit out of place on both the light and medium text.

The only way to fix this is to create a variety of classes for the <code>&lt;em&gt;</code> element, like so:

<div class="break-out">

<pre><code class="language-css">em {
   font-family: 'UbuntuRegularItalic', arial, sans-serif;
   font-weight: 400;
   font-style: italic;
}

em.light {
   font-family: 'UbuntuLightItalic', arial, sans-serif;
   font-weight: 300;
   font-style: italic;
}

em.medium {
   font-family: 'UbuntuMediumItalic', arial, sans-serif;
   font-weight: 500;
   font-style: italic;
}</code></pre></div>

<img loading="lazy" decoding="async" class="154220" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9aa3b835-6492-4565-bec3-f916f5226874/14-unique-style-linking-em3strong-set.png" alt="14_unique_style-linking_Em3Strong_set" width="496" height="489" /><br>
<em>Creating three versions of the <code>&lt;em&gt;</code> element (<code>em</code>, <code>em.light</code>, <code>em.medium</code>) will result in italics that “match” the weight of the text.</em>

This will result in italics that match the weight of the text in each paragraph. This creates much better hierarchy, but it undermines the beauty of cascading style sheets and the simplicity of using a single <code>&lt;em&gt;</code> element.</p>

### Bonus: If the Fallback Font Loads, Weights and Styles Will Be Retained

Setting all weights and styles correctly (for example, not <code>normal</code>) when styling the text means that basic weights and styles will be retained even if the Web font doesn’t load.

<img loading="lazy" decoding="async" class="154221" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f81d32b9-7deb-4ff9-85ad-07c9c693383f/15-unique-style-linking-fontfail.png" alt="15_unique_style-linking_fontfail" width="498" height="947" /><br>
<em>If the Web font doesn’t load, then the fallback font (here, Times New Roman) will still provide hierarchy — bolds and italics will remain intact. But because fallback fonts don’t usually have “extra” weights (such as Light, Medium and Black), some weights will revert to Normal and Bold.</em>

### The Short Version

Using unique font-family names <em>and</em> setting weights and styles to match (for example, not setting them to <code>normal</code>) is the most effective method of getting weights and styles to work with the @font-face declaration. An extra step is required (i.e. setting and using unique font-family names — even with elements such as <code>&lt;em&gt;</code> and <code>&lt;strong&gt;</code>) to avoid faux italic and faux bold, but the solution does reduce the potential for double-italic and double-bold text. In addition, if the Web font doesn’t load, then the text will retain both style and weight. Finally, text will render properly in IE 7 and 8 (even if you’re using more than four weights and styles), and your pages won’t crash the browsers on BlackBerry 9900 and iPad 1 devices.

## Make Sure Your Weights And Styles Work

Weights and styles help visitors read the content on your website. So, make sure your weights and styles load correctly — whether for IE 8, Chrome, Mac OS X Firefox or an iPad and whether or not the Web font loads correctly (or visitors see a fallback font).

When choosing which method to use for your website, ask yourself two questions:

<ol>
  <li>Will I be using more than four weights and styles on the website?</li>
  <li>Are BlackBerry and iPad 1 users part of my target audience?</li>
</ol>

If the answer to both questions is “no,” then go ahead and use style linking. It’s elegant and forgiving.

If the answer to either question is “yes,” then use the combined method. Currently, the only way to make sure your weights and styles work cross-browser is to use unique font-family names in conjunction with matching weights and styles (and, of course, to make sure your font has a bold and italic version). This might sound like a chore, requiring extra care and typing (<code>UbuntuRegularItalic</code> is longer to type than <code>Ubuntu</code>, after all), but as with most typographic details, <strong>the best results take time and effort</strong>. Even <a href="https://typekit.com">Typekit</a>, which uses JavaScript to handle the intricacies of Web fonts, requires variation-specific font-family names to support older versions of IE.

Once IE 7 and 8, BlackBerry 9900 browsers and the iPad 1 are defunct, using style linking alone <em>should</em> be enough to get the job done. But as of 28 January 2013, <a href="https://gs.statcounter.com">StatCounter</a> reports that IE 7 and 8 alone were used for 12.3% of the 45 billion page views collected from November 2012 to January 2013. Information on mobile browsers is not clear, but a minimum of 1 in 8 visitors still need us to go the extra mile. So, for now, we’ve got some extra typing to do.</p>

### Further Resources

*   [Say No to Faux Bold](https://www.alistapart.com/articles/say-no-to-faux-bold/), Alan Stearns, A List Apart
*   [New From Typekit: Variation-Specific Font-Family Names in IE 6–8](https://blog.typekit.com/2011/06/27/new-from-typekit-variation-specific-font-family-names-in-ie-6-8/ "Permanent Link to New from Typekit: Variation-specific font-family names in IE 6-8"), Typekit blog

{{< signature "al" >}}


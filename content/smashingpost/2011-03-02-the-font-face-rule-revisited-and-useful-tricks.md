---
title: The @Font-Face Rule And Useful Web Font Tricks
slug: the-font-face-rule-revisited-and-useful-tricks
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce52b0f0-faa0-4de5-a3c9-edf605e280cc/webfonts.jpg
date: 2011-03-02T17:26:24.000Z
author: ralf-hermann
description: >-
  The possibility of embedding any font you like into websites via `@font-face`
  is an additional stylistic device which promises to abolish the monotony of
  the usual system fonts. It surely would be all too easy if there was only one
  Web font format out there. Instead, there's quite a variety, as you will get
  to know in this article.
  "OpenType
  Features")](https://www.smashingmagazine.com/2011/03/02/the-font-face-rule-revisited-and-useful-tricks/)

  This quick introduction to `@font-face` will lead you towards a guide through
  the `@font-face` kit generator. If you want to make Web use of your already
  licensed desktop fonts, read up on how to embed them from your own server.
  Topped up with some helpful tips, tricks and workarounds, this article will
  hopefully provide some useful insights.
categories:
  - Typography
  - Fonts
---
The possibility of embedding any font you like into websites via <code>@font-face</code> is an additional stylistic device which promises to abolish the monotony of the usual system fonts. It surely would be all too easy if there was only one Web font format out there. Instead, there's quite a variety, as you will get to know in this article.

This quick introduction to <code>@font-face</code> will lead you towards a guide through the <code>@font-face</code> kit generator. If you want to make Web use of your already licensed desktop fonts, read up on how to embed them from your own server. Topped up with some helpful tips, tricks and workarounds, this article will hopefully provide some useful insights.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Setting Weights And Styles With The @font-face Declaration</span>](https://www.smashingmagazine.com/2013/02/setting-weights-and-styles-at-font-face-declaration/)
*   [What Font Should I Use?](https://www.smashingmagazine.com/2010/12/what-font-should-i-use-five-principles-for-choosing-and-using-typefaces/)
*   [How To Choose The Right Face For A Beautiful Body](https://www.smashingmagazine.com/2012/05/how-to-choose-the-right-face-for-a-beautiful-body/)
*   [Review of Popular Web Font Embedding Services](https://www.smashingmagazine.com/2010/10/review-of-popular-web-font-embedding-services/)

## Web Font Formats

EOT, TTF, OTF, CFF, AFM, LWFN, FFIL, FON, PFM, PFB, WOFF, SVG, STD, PRO, XSF, and the list goes on. To find one's way through in this veritable jungle of font formats is not exactly easy. Let's have a closer look at the pros and cons of font formats that are particularly relevant for their use on websites.

{{% feature-panel %}}

### TrueType

This format was developed in the late 1980s as a competitor to Adobe's Type 1 fonts used in PostScript. As a scalable outline format, it replaced the common bitmap fonts that were used for screen display at that time. Microsoft took up the TrueType format as well and it soon evolved into the standard format for system fonts due to the fact that it offered fine-tuned control for a precise display of font in particular sizes.</p>

### OpenType

Microsoft and Adobe teamed up in developing this font format. Based on the TrueType format, OpenType offers additional typographical features such as ligatures, fractions or context sensitive glyphs and the like. However, browser support of these features which are common in sophisticated layout and illustration programs is still unsatisfactory. There are two different versions of OpenType fonts, depending on the outline technology used. There are:

*   OpenType fonts with TrueType Outlines (OpenType TT) and
*   OpenType fonts with PostScript Outlines (OpenType PS)

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ba33a71-eb1e-4a75-8940-643e2358d0f4/wfs-opentypeflavours.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="86928" title="wfs-opentypeflavours" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ba33a71-eb1e-4a75-8940-643e2358d0f4/wfs-opentypeflavours.jpg" alt="Screenshot" width="540" height="271" /></a><br>
<em>OpenType comes in two different versions.</em>

OpenType PS is a so-called <em>CFF based file format</em> (CFF = compact file format). This is relevant when using OpenType PS fonts as Web fonts, because PostScript based formats are displayed without subpixel rendering on Windows platforms which affects the rendering quality considerably. That's why TrueType based fonts are the better choice as Web fonts, even though Microsoft will solve this rendering issue in the future. The structures of TrueType and OpenType fonts are very similar and browser support is available in Safari 3.1 and higher, Firefox 3.5 and Opera 10 (and of course newer versions).</p>

### EOT

Internet Explorer has supported the proprietary Embedded OpenType (EOT) standard from the late 1990s. It's a variation of the TrueType and OpenType formats that provide the following particularities:

*   EOT fonts are a compact form of OpenType optimized for quick delivery on the Web due to data compression.
*   By means of URL-binding, EOT fonts can be tied to a specific domain. The fonts can then only be delivered to and used on those Web pages. This technique helps prevent fonts from being copied and used without a licence.

EOT is exclusively supported by Internet Explorer. Even though it might not succeed as a Web font format in the future, it still makes sense to use this format today in order to supply the users of various IE versions with Web fonts. Current IE versions (&lt; 9) do not use any other format.

If you want to convert TTF fonts to natively compressed EOT files, you can use <a href="https://eotfast.com/" rel="nofollow">EOTFast</a> (a free application) currently available only for Windows.

### WOFF

Unlike EOT, the Web Open Font Format (WOFF) is in the process of being standardized as a recommendation by the W3C which published WOFF as a working draft back in July 2010.

WOFF came into existence as a kind of a compromise between font foundries and browser companies, so it's no wonder that WOFF has been developed by two font designers (Erik van Blokland and Tal Leming) in cooperation with Mozilla developer Jonathan Kew. Essentially, WOFF is a wrapper that contains TrueType and OpenType fonts, and it's not really a new format of its own.

WOFF uses an integrated compression algorithm named <em>zlib</em>, which offers file size reduction for TrueType fonts exceeding 40%. Furthermore, meta data can be added, e.g. a user's licence. However, this data presents only meta information and is not validated by browsers.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd23b7db-6b44-402b-8e76-d0518db0efc8/wfs-ff36woff.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="86929" title="wfs-ff36woff" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd23b7db-6b44-402b-8e76-d0518db0efc8/wfs-ff36woff.jpg" alt="Screenshot" width="500" height="300" /></a><br>
<em>Thanks to WOFF, Mozilla can use its corporate typeface FF Meta.</em>

The format has been supported by Firefox since version 3.6, and by Google Chrome since version 5.0. All other browser manufacturers are working on adding full support in future releases. Fonts can be converted into the WOFF format by the online service <a href="https://www.fontsquirrel.com/fontface/generator" rel="nofollow">Font Squirrel</a> free of charge.</p>

### SVG

SVG fonts are text files that contain the glyph outlines represented as standard SVG elements and attributes, as if they were single vector objects in the SVG image. But this is also one of the biggest disadvantages of SVG fonts. While EOT, WOFF and PostScript-flavoured OpenType have compression built into the font format — SVG fonts are always uncompressed and usually pretty large.

SVG fonts are not really an alternative to the other Web font formats, and iOS 4.2 is the first version of Mobile Safari to <a href="https://www.zeldman.com/2010/11/26/web-type-news-iphone-and-ipad-now-support-truetype-font-embedding-this-is-huge/" rel="nofollow">support native Web fonts</a> (in TrueType format) instead of SVG. However, SVG is the only format that can be used for the iPhone and iPad prior to iOS 4.2.

Tools, such as <a href="https://www.fontsquirrel.com/fontface/generator" rel="nofollow">Font Squirrel</a>, can be used to convert fonts into this format. Another possibility to obtain SVG fonts is to rent them from one of the numerous Web font providers.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/691356a5-4d0a-4f2d-af20-f73b409d51c5/wfs-typkit-ipad.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="86930" title="wfs-typkit-ipad" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/691356a5-4d0a-4f2d-af20-f73b409d51c5/wfs-typkit-ipad.jpg" alt="Screenshot" width="500" height="384" /></a><br>
<em><del>Typekit also serves its fonts as SVG files for the iPhone and iPad</del>. <a href="https://blog.typekit.com/2011/01/10/now-serving-truetype-fonts-to-ios-4-2-devices/" rel="nofollow">Typekit no longer servers SVG fonts to iOS devices</a>. The service serves TrueType fonts to iOS 4.2 devices and higher.</em>

## @font-face Revolution

The CSS3 property <code>@font-face</code> presents so many new possibilities that a veritable gold-digging mentality is taking hold of Web designers. There’s hope that regular system fonts will soon be abolished by Web font embedding, which enables us to choose practically any typeface and font style they want — just like in print design.

With regard to typography, the Web is <em>way </em>behind print. Take headlines: in print, condensed typefaces come in handy because they allow more words to fit on one line. System font collections, however, usually have no condensed fonts. Also, companies cannot use their proprietary fonts on their own websites. Instead, they have to replace them with standard fonts, such as Arial, which makes establishing a consistent corporate identity across all media impossible.</p>

### @font-face in the Late 1990s

The ability to embed any font into a website has been around for a while. Netscape 4 and Internet Explorer 4 supported <code>@font-face</code> by the end of the 1990s. The rule allowed us to deposit a font on a server and deliver it through a Web page.

<pre><code class="language-css">@font-face {
font-family: Gentium;
src: url(fonts/gentium.eot);
}</code></pre>

This technique was ahead of its time. At that point it was used for simple grayscale anti-aliasing. This was no problem for system fonts, which were laboriously optimized for rendering on screen, but other fonts were not rendered properly; they lacked the benefits of manual on-screen optimization. Instead of improving Web typography, the non-system fonts made websites look worse.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/462d7630-cee3-495e-8457-eb6b27872a7b/wfs-alias-compare-300x60.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="size-medium wp-image-86923" title="wfs-alias-compare" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/462d7630-cee3-495e-8457-eb6b27872a7b/wfs-alias-compare-300x60.jpg" alt="Screenshot" width="300" height="60" /></a>

It’s no wonder that the <code>@font-face</code> rule was removed in the CSS 2.1 specification. Using system fonts was the general practice in Web design, especially for copy. For headlines, several workarounds have been established. Some designers replaced text with a bitmap file or a Flash movie that displayed the headline in a particular font.

Another approach that has emerged in the past few years is to replace headlines with vector graphics, with the help of JavaScript. Typeface.js and <a href="https://cufon.shoqolate.com/generate/" rel="nofollow">Cufón</a> offer this functionality. Each of these techniques, though, has one problem or the other, be it incompatibility with search engines or issues with zooming.</p>

### Successful Second Run, Thanks to Subpixel Rendering

The introduction of Safari 3.1 by Apple marked a turning point in the use of Web fonts. The browser update brought the old <code>@font-face</code> rule back. A significant improvement came with the introduction of flat-panel LCD displays, which have high screen resolutions and anti-aliasing via subpixel rendering. Subpixel rendering takes advantage of the fact that each pixel on a color LCD is composed of individual red, green and blue subpixels. It uses these subpixels to anti-alias text, which increases the apparent resolution of an LCD display and thus improves the rendering of text — even text set at very small sizes.

On Mac OS X platforms, this function is activated by default. Windows uses its own trademark, ClearType, which is activated by default on Windows Vista and Windows 7 but turned off on Windows XP. In Microsoft Office 2007 and 2010, Internet Explorer 7+ and Windows Live Messenger, ClearType is turned on by default, even if it’s not enabled throughout the operating system.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4700f7c5-33a6-4640-94e8-691ea2554ad5/wfs-safari2008.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="86919" title="wfs-safari2008" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19e1a8dc-026e-4133-9323-05f14f0cd277/webkit-2.jpg" alt="Screenshot" width="545" height="341" /></a><br>
<em>Safari 3.1 offered support for standard font formats for the first time (<a href="https://www.fonts.info/info/press/font-face-embedding-demo.htm" rel="nofollow">demo</a>).</em>

Subpixel rendering is displayed in Safari on Mac OS X. What’s remarkable about Safari’s <code>@font-face</code> support is that, for the first time, embedding standard formats — namely, TrueType (TTF) and OpenType (TTF/OTF) — is possible without any prior conversion, as the following CSS shows:

<pre><code class="language-css">@font-face {
font-family: Gentium;
src: url(fonts/gentium.otf);
}</code></pre>

### The Font Foundries’ Concerns

Suppliers of commercial fonts, however, were not exactly happy about the new functionality. Anyone could now download and embed fonts without paying the licensing fee. A lively debate between browser makers and font foundries began… and continues. The foundries want commercial fonts to be protected from bootlegging and unlawful use, while the browser makers do not feel obligated to claim the foundries’ copyrights; they instead argue that content providers are responsible for declaring any copyright-protected fonts on their websites, just as they are obliged to do with images, video, text and other assets.</p>

## Using the @font face Kit Generator

For a practical test you might want to download the font package at <a href="https://www.fonts.info/info/downloads.php" rel="nofollow">Graublau Sans Web</a>. This font package offers a PostScript-based OpenType font that can actually be used on Safari 3.1+, Firefox 3.5+ and Opera 10+ without any changes. In order to provide browser support for Internet Explorer and improve the screen display, you can use the <a href="https://www.fontsquirrel.com/fontface/generator" rel="nofollow">@font-face Kit Generator</a>. Click the "Add Fonts" button and upload the respective font with all its weights. Then choose the "Expert" radio button and check all the necessary options, which we'll go through in more detail now:

### Font Formats

The main problem is that you have to activate EOT in order to obtain <code>@font-face</code> support on Internet Explorer IE4 to IE8 (in IE9 RC, WOFF is supported as well). SVG fonts will mainly be needed for Mobile Safari on the iPhone and iPad prior to iOS 4.2, although Chrome and Opera can handle this format as well. Alternatively or rather in addition to SVG, there's the compressed version SVGZ, which offers a much smaller file size. Unfortunately, it doesn't run on the iPhone so you'll need the SVG font anyway.

Creating a TrueType font format will allow for support in Safari (since 3.1), Firefox (since 3.5) and Opera (since 10). Checking the WOFF option won't increase browser support these days, but it sure will in the near future, when WOFF has become the standard Web font format.</p>

### Rendering and Miscellaneous Options

*   _Add Hinting_: This option offers improved font display in Windows. You should only uncheck it if you are absolutely positive that the respective fonts are screen-optimized already.
*   _WebOnly™_ adds specific modifications which allow browsers to use the modified fonts but avoid installation of these fonts on common operating systems. Checking this option helps to avoid unintended illegal copies.
*   _Keep OT Features_: Desktop fonts may have a number of OpenType functions. As there is little browser support for these functions today, you might want to remove them with this option (rendering and miscellaneous options). In order to keep some of the standard, i.e. already supported OpenType functions such as ligatures, you can activate this option.
*   _Remove Kerning_: Another possibility to reduce the file size is by checking this option which will erase all kerning values that are contained for specific letter combinations. In case you are going to use the font for body text, this option is highly recommended. For headlines it should be handled with care or not be done at all as the missing kerning values might lead to the unpleasant effect of the shape of words looking like a Swiss cheese.
*   _Simplify Outlines_ does exactly that: it tries to simplify the outline of characters. As this option reduces the quality of screen display, it is not advisable to use it.
*   _Build Cufón File_ isn't directly part of the options for @font-face embedding. For further details on building a file you can also check the [Cufón](https://cufon.shoqolate.com/generate/) website.</p>

### Subsetting

Subsetting means that all superfluous characters are removed. Whether or not this is actually necessary depends on the respective font. Some fonts can easily contain thousands of characters of various writing systems which bloats the font file considerably. Without subsetting such fonts, they are not suitable for use as Web fonts.

The option <em>Basic Subsetting</em> is set as default and offers the usual Western European glyph allocation based on the character set <a href="https://de.wikipedia.org/wiki/Macintosh_Roman" rel="nofollow">MacRoman</a>. <em>Custom Subsetting</em> allows for a custom defined scope of contained characters and glyphs. Whereas, the option <em>No Subsetting</em> deactivates subsetting completely and converts the font with all contained characters and glyphs.</p>

### CSS-Formats

The @font-face Kit Generator creates both the converted fonts and the matching CSS files which is helpful as the CSS code can be huge, especially when several fonts with various font formats are involved.

You can choose three different versions:

*   [Fontspring Syntax](https://www.fontspring.com/blog/the-new-bulletproof-font-face-syntax)
*   [Further Hardening of the Bulletproof Syntax](https://www.fontspring.com/blog/further-hardening-of-the-bulletproof-syntax)
*   Mo' Bulletproofer
*   [Smiley](https://www.fontspring.com/blog/the-new-bulletproof-font-face-syntax)

The Fontspring syntax is currently the most simple and compatible one. It can deliver the WOFF file to IE9 and EOT to IE prior version 9 and it also works on mobile operating systems like iOS and Android.</p>

### CSS Options

The option <em>Style Linking</em> groups styles by family. This allows for addressing the fonts later through the CSS properties <code>font weight</code> and <code>font-style</code>.

This option will only work properly if the font family doesn't contain more than the common four styles, i.e. regular, italic, bold and bold italic. Otherwise, you should leave the option unchecked so that fonts can be addressed by independent family names.

Last but not least, the option <em>Base64 Encode</em> embeds Web fonts with a base64 encoding into the CSS code instead of creating a separate font file. As a result, the fonts don't appear as font files in the browser's cache.</p>

## Code Sample

The following example illustrates what your CSS code for @font-face embedding might look like:

<pre><code class="language-css">@font-face {
font-family: Graublauweb;
src: url('Graublauweb.eot'); /* IE9 Compatibility Modes */
src: url('Graublauweb.eot?') format('eot'),  /* IE6-IE8 */
url('Graublauweb.woff') format('woff'), /* Modern Browsers */
url('Graublauweb.ttf')  format('truetype'), /* Safari, Android, iOS */
url('Graublauweb.svg#svgGraublauweb') format('svg'); /* Legacy iOS */
}</code></pre>

The first statement is for IE9 in IE7 &amp; IE8 render modes. In the second source declaration, the EOT file for Internet Explorer is declared first in this comma-separated list and the name is followed by a question mark. This fools IE into thinking the rest of the string is a query string and loads just the EOT file.

The other browsers follow the spec and select the format they need based on the <code>src</code> cascade and the format hint. The SVG specification contains an additional hash tag as a unique identification number. This is necessary as SVG files may contain several fonts. However, the Fontsquirrel @font-face generator takes care of the identification number and its embedding into the CSS code automatically.

Please notice that the syntax suggested by Ethan Dunham in his article <a href="https://www.fontspring.com/blog/the-new-bulletproof-font-face-syntax" rel="nofollow">The New Bulletproof @Font-Face Syntax</a> and revised by Richard Fink in an article on New @Font-Face Syntax: Simpler, Easier no longer works in Internet Explorer 9. Also, take a look at Ethan's follow-up <a href="https://www.fontspring.com/blog/further-hardening-of-the-bulletproof-syntax" rel="nofollow">Further Hardening of the Bulletproof Syntax</a>.</p>

### Loading Time Increases With Amount of Fonts

By means of the above-mentioned options, file sizes of Web fonts can be reduced to approximately 30 to 60 kilobytes. Larger font files or too many fonts on one web page can slow down loading of the page, especially on mobile devices.</p>

### Weird Interim Solution in Firefox

Most browsers won't show any text before all Web fonts are imported. Firefox, however, displays the text using a system font and renders the text again, when the embedded Web fonts are completely loaded. This technique results in a "flash of unstyled text" that sometimes leads to side-effects. Web designers can control this behaviour by using <a href="https://code.google.com/apis/webfonts/docs/webfont_loader.html" rel="nofollow">Google’s Webfont Loader</a>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d58b258b-34ef-4e9d-92ff-606f726d74d5/wfs-graublau.gif" rel="nofollow"><img loading="lazy" decoding="async" class="86981" title="wfs-graublau" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d58b258b-34ef-4e9d-92ff-606f726d74d5/wfs-graublau.gif" alt="Screenshot" width="600" height="736" /></a>

<em>The result of the above process looks like this in Safari on Mac OS X.</em>

## Embedding Web Fonts From Your Server

You don't necessarily always have to rent or licence fonts for use on Web pages. You can also pimp your already licenced desktop fonts for cross-browser Web font embedding and upload the fonts to your own Web server.</p>

### Fonts to Choose and Fonts to Avoid

Before you start converting your desktop fonts into Web fonts, make sure that the licence with the respective font entitles you to do so. Generally, commercial licence agreements do not permit the storing of font software on a publicly accessible Web server. This, however, is a prerequisite when using the <code>@font-face</code> rule.

Currently, commercial font providers count on Web font embedding services. Only a few suppliers deliver special Web font packages for storage on the customer's own Web server, among them <a href="https://www.fontshop.de/Schaufenster/Bereich/Schriften/Webfonts/" rel="nofollow">FSI FontShop International</a> and <a href="https://www.fontspring.com/" rel="nofollow">Fontspring</a>. A growing number of webfont packages can also be licensed via <a href="https://new.myfonts.com/info/webfonts/" rel="nofollow">MyFonts.com</a>.

Once the Web Open Font Format (WOFF) is accepted as a standard, more font vendors might offer this service.</p>

### Embedding Free and Open-Source Fonts

Besides commercial fonts, there's a wide variety of freeware and open source fonts which you can embed into your Web pages.

Another huge collection of such fonts is offered by <a href="https://www.fontsquirrel.com/" rel="nofollow">Font Squirrel</a>. It is a useful tool when it comes to converting desktop fonts into Web font formats as it offers a powerful tool, the <a href="https://www.fontsquirrel.com/fontface/generator" rel="nofollow">@font-face Kit Generator</a>.

Please note that the fonts you want to convert have to be legally eligible for Web font embedding!

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24f3635d-4063-4d8c-ad6a-de36b5a807f1/wfs-fontsquirrel.gif" rel="nofollow"><img loading="lazy" decoding="async" class="86978" title="wfs-fontsquirrel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08d28ada-d5d0-409b-ac5e-678670bbb1a9/ffgenerator.jpg" alt="Screenshot" width="553" height="340" /></a><br>
<em>Creating web fonts made easy by Font Squirrel's generator.</em>

## Tips, Tricks and Workarounds

The possibilities for using custom fonts on Web pages have developed more quickly over the past two years than anyone had expected. But Web designers still have to struggle with a clutter of formats in order to provide cross-browser support for a given font. This problem will subside as soon as the Web Open Font Format (WOFF) is established as the standard Web font format.

<a href="https://www.trevorhutchison.com/" rel="nofollow"><img loading="lazy" decoding="async" class="86989" title="wfs-trevor" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adedd80b-3daa-4600-bd26-fa9a968d0a14/wfs-trevor1.jpg" alt="Screenshot" width="500" height="424" /></a><br>
<em><a href="https://www.trevorhutchison.com/" rel="nofollow">Typographic variety</a> beyond the monotony of system fonts.</em>

Another obstacle, mentioned earlier, is the prevalence of Windows computers on which subpixel rendering is deactivated (either by default on Windows XP or by preference on the part of users). Compared to system fonts, most Web fonts are displayed at low quality on screen displays that lack subpixel rendering. Time will solve this problem, as users replace old hardware and operating systems. In the meantime, Internet Explorer 9 works with a text engine called <em>DirectWrite </em>that delivers significantly improved rendering.

Using Web fonts in your design <strong>requires thorough testing on as many different browsers</strong> and platforms as possible, with a close look at various options for rendering text. If the screen display is of poor quality and lacks subpixel rendering, then opt for graceful degradation by serving system fonts to older browsers and OS. Conditional comments are the easiest way to exclude older browsers and operating systems from style sheets with Web fonts. Of course, JavaScript is a more <a href="https://www.useragentman.com/blog/2009/11/29/how-to-detect-font-smoothing-using-javascript/" rel="nofollow">elegant</a> way to detect whether a client’s subpixel rendering is turned on.</p>

### Text Layout

Even though some Web layouts are drawing nearer in sophistication to print layouts (thanks to rich typography and Web font embedding), there’s still a big difference: <strong>browsers do not automatically hyphenate text</strong>. Especially in languages with many long words (such as German), justifying text is not possible without creating spacious gaps, and thus reducing the readability of the body text.

With JavaScript, you can provide language-based <a href="https://code.google.com/p/hyphenator/" rel="nofollow">client-side hyphenation</a>. A server-side solution is offered by phpHyphenator. Still, these are band-aid solutions for a function that should be integral to every browser — hopefully in the near future.</p>

### OpenType Typography Features

Another text-layout shortcoming shared by common browsers has come into focus as Web fonts spread: high-end desktop publishing programs, such as InDesign and QuarkXPress 7+, do not support OpenType typographic features.

OpenType functions add several smart options that enhance a font’s typographic and language-support capabilities. If an application supports these options, then characters can be replaced by additional features automatically. For Roman scripts, these mainly concern ligatures, fractions and small capitals.

&lt;<img loading="lazy" decoding="async" class="size-medium wp-image-86995" title="wfs-ffot-sc" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5200a513-6964-48c9-925b-df80dbd13a44/small-caps.jpg" alt="Screenshot" width="500" height="131" /><br>
<em>Computer-generated small caps (gray above) and true small caps (blue below) in Firefox 4 beta.</em>

Some fonts can be put to use only through OpenType functions in the first place. Take joined Roman lettering or Arabic writing, in which the shape of a character depends on its position in the word and on adjacent characters. Comprehensive OpenType fonts might, therefore, contain alternative glyphs for a given character. By means of OpenType functions, the basic version of a character would be replaced by a version with matching connections, based on context. The current beta version of Firefox 4 offers access to this OpenType feature for the first time. You can define with this browser-specific attribute:

<pre><code class="language-css">h1 {
-moz-font-feature-settings: 'smcp=1';
}</code></pre>

This would display the headline in true small caps, provided that the font has a small caps case.

Microsoft has a <a href="https://www.microsoft.com/typography/otspec/featurelist.htm" rel="nofollow">list</a> of common OpenType features. So far, there are no standards to address these features in your CSS style sheets, but the CSS Fonts <a href="https://dev.w3.org/csswg/css3-fonts/" rel="nofollow">Module </a>Level 3 draft mentions the possibility. Other browser companies will likely follow this example sooner or later.

Browser developers still have a long way to go before the Web catches up to the text layout in print design, let alone overtakes it. It’s good to know, though, that there’s a growing awareness of typographic subtleties among browser manufacturers. No doubt, further progress can be expected soon!

<em>(al) (sp) (ik)</em>


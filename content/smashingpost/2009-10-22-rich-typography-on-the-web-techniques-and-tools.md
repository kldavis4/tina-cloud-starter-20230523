---
title: 'Rich Typography On The Web: Techniques and Tools'
slug: rich-typography-on-the-web-techniques-and-tools
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99eb2ab2-3270-49b8-9eb0-1e7fbb0503d6/typekit2.png
date: 2009-10-22T13:57:54.000Z
author: cameron-chapman
description: >-
  In addition to font stacks, we can replace the heading text with an image, embedded font, or bit of Flash? The
  methods described below are easier than they sound. And the end result is that
  the vast majority of users will see the beautiful typography you want them to
  see.
categories:
  - Typography
  - Fonts
  - Design
  - Web Design
  - Techniques
---
Let's face it: Web-safe fonts are very limiting. Maybe a dozen fonts are out there that are widely enough adopted to be considered "Web safe," and those ones aren't exactly spectacular for much other than body type. Sure, Georgia, Arial or Times New Roman work just fine for the bulk of the text on your website, but what if you want something different for, let's say, headings? Or pull quotes? What then?

You have a few options. Many people just opt for more elaborate <a href="https://www.smashingmagazine.com/2009/09/22/complete-guide-to-css-font-stacks/">CSS font stacks</a>, with their preferred fonts up front. But that still leaves a big chunk of your visitors seeing the same old Web-safe fonts.

Enter <strong>dynamic text replacement</strong>. In addition to font stacks, why not replace the heading text with an image, embedded font, or bit of Flash? The methods described below are easier than they sound. And the end result is that the vast majority of users will see the beautiful typography you want them to see. A word of warning, though: <strong>don't use dynamic text replacement for all of the text on your page</strong>. All that would do is slow it down and frustrate your visitors. Instead, save it for headings, menu items, pull quotes and other small bits of text.</p>

## 1\. sIFR 2.0

<a href="https://www.mikeindustries.com/blog/sifr/">sIFR</a> (Scalable Inman Flash Replacement) was one of the first dynamic text replacement methods, developed in the spring of 2005. It uses JavaScript and Flash to convert any text you designate on a page to any typeface you choose and has been released as open source under the <a href="https://creativecommons.org/choose/cc-lgpl">CC-GNU LGPL license</a>, so it's free for anyone to use.

{{% feature-panel %}}

<a href="https://www.mikeindustries.com/blog/sifr/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d1ebd4a-31d9-4273-a9bc-f54c69915e64/sifr2pic.jpg" alt="sIFR 2.0" width="480" height="400" /></a>

sIFR is fully accessible to screen readers, because it simply displays the original text if JavaScript or Flash isn't enabled. And because of the way text is rendered, if your visitors zoom in using a browser's text-zoom option, the replaced text will also zoom in (only when the page loads, though, not if they zoom in afterward).</p>

### How sIFR Works

While sIFR is a rather complex system, its basic concept is simple: JavaScript checks to see whether Flash is installed in your browser. If it isn't (or if JavaScript isn't installed), it stops there and the visitor sees your text in whatever font you've specified in your style sheet. If Flash is installed, then the JavaScript measures each element on the page that you've designated to be converted.

Once JavaScript has measured all the elements, it replaces each with a Flash movie that is the same size as the original element. The original text is passed into the Flash movie as a variable, then some ActionScript code in the Flash file draws the text in the typeface you've chosen and scales it to fill the area occupied by the Flash movie.</p>

### Benefits of sIFR

*   Works with virtually any font
*   Degrades gracefully in most instances to the original HTML or (X)HTML file if the person doesn't have Flash or JavaScript installed
*   Cross-browser and cross-platform compatible
*   Because the original (X)HTML document remains unchanged, the SEO, accessibility and other concerns people usually have with Flash aren't really issues

### Drawbacks/Disadvantages of sIFR

*   Requires both JavaScript and Flash to be installed
*   Will not be visible if a Flash ad blocker is used
*   Firefox does not easily deselect sIFR text

## 2\. P+C DTR (With Word-Wrapping and Inner Tags)

<a href="https://www.joaomak.net/util/dtr/">P+C DTR (with word-wrapping and inner tags)</a> (the "P" and "C" standing for PHP and CSS) is a text replacement method that works with PHP and CSS rather than Flash or JavaScript. Considering that PHP is a server-side language, and every modern browser automatically supports CSS, this method has some advantages over those that use Flash or JavaScript. This version of P+C DTR is based on the <a href="https://artypapers.com/csshelppile/pcdtr/">original P+C DTR method</a>, but with the addition of word-wrapping and inner tags.

<a href="https://www.joaomak.net/util/dtr/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1c79162-5e28-40e5-ad0a-6e56dff7e55a/pcdtrpic.jpg" alt="P+C DTR" width="480" height="400" /></a>

### How P+C DTR Works

P+C DTR uses PHP's output buffering functions to extract the heading text and give it an inline style that points to the script that replaces the text with an image. Therefore, the only requirement on the back end is that the host server supports <a href="https://br.php.net/manual/en/ref.image.php">PHP image generation</a>.

The CSS comes into play in designating the heading's font color, size and background color. The styling for the heading is kept in a separate CSS file, but the file is called only once per browser session, so it doesn't have a noticeable impact on page load time.</p>

### Benefits of P+C DTR

*   Doesn't require Flash or JavaScript
*   Not affected by ad blockers
*   Output is valid XHTML and CSS

### Drawbacks/Disadvantages of P+C DTR

*   Will not work if images are disabled in the browser
*   headings have to be uniform throughout the website; you can't have one style of heading on one page and another on a different page (unless you use a different style sheet for each page)
*   Although it does seem possible to select the text in the headings, it is difficult to do so

## 3\. Cufón

Cufón was created as an sIFR alternative. It uses JavaScript to replace text, without Flash, making it more widely compatible than sIFR.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85cda506-5309-49e7-a6ed-abeb4ab41c11/cufonpic.jpg" alt="Cufon" width="480" height="400" />

### How Cufón Works

Using Cufón is a bit more involved than a lot of other DTR methods. You have to go through an extra step: converting whatever fonts you want to use to a format that Cufón can work with. An <a href="https://cufon.shoqolate.com/generate/">automated tool</a> can do this, though, so technically it is not more complicated than the other methods.

Once you've converted the fonts, Cufón simply replaces the text in your browser with the font you've designated via the JavaScript. Activating Cufón is as simple as uploading the script and putting a couple of lines of code in the head of your document.</p>

### Benefits of Cufón

*   Doesn't require Flash
*   Technically, it's quite easy to use — even with the extra step of converting fonts
*   In general, the embedded text can be copied and pasted in any application, but it doesn't always work – e.g. there are problems in Chrome 3 and Firefox 3.5.2
*   Because text is rendered using only JavaScript, it's **quicker than many other methods**
*   Degrades gracefully if JavaScript isn't supported

### Drawbacks/Disadvantages of Cufón

*   Converts your text to image files, which means it's not as accessible as plain (X)HTML
*   <del>Does not seem to work in IE8 unless the page is viewed in compatibility mode</del> It _does_ work in IE 8.
*   Requires JavaScript
*   Accessibility issues: Cufón wraps the text inside canvases and spans and so Because. Each. Word. Is. In. Its. Own. Span. Some. Screen. Readers. Will. Read. The. Text. Like. This.
*   In Firefox, if CSS is disabled, a bizarre text duplication occurs
*   Sometimes has problems with text selection

## 4\. Typeface.js

Typeface.js is a JavaScript-based dynamic text replacement method that embeds fonts on your page rather than converting them to images. This means that visitors are presented with a page that acts (and really is) like a regular HTML and CSS page.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/055899cd-b9ff-4c8a-b832-fba4bf8eaceb/typefacejspic.jpg" alt="Typeface.js" width="480" height="400" />

### How Typeface.js Works

Whereas most of the methods mentioned so far either replace the text with Flash or turn the text into an image, Typeface.js styles text with an embedded font using JavaScript. So, your text stays as accessible as it was before, without the need for Flash.

Typeface.js uses the browser's <strong>vector drawing capabilities</strong> to draw the text in your HTML documents. All modern browsers support this (Firefox, Opera and Safari use the &lt;canvas&gt; element and SVG, and Internet Explorer supports VML).</p>

### Benefits of Typeface.js

*   Leaves the text on your page as text, making it more accessible
*   Flash is not required
*   Not affected by ad blockers

### Drawbacks/Disadvantages of Typeface.js

*   Copyright issues prevent many fonts from being embedded in this manner, so only free and open source fonts can be used
*   Requires JavaScript
*   A tool is available to convert OpenType and TrueType fonts to Typeface.js's required format
*   Font embedding causes larger page size and more HTTP requests
*   Doesn't work in Internet Explorer when images are disabled

## 5\. Facelift v1.2 (FLIR)

Facelift Image Replacement (FLIR) is another DTR alternative that uses PHP and JavaScript. Flir lets you replace any element (h1, h2, spans, etc.) with dynamically generated text and has extensive documentation available as well as a forum for getting help.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a0d5fb0-573f-401f-8c85-f560acc54e76/flirpic.jpg" alt="FLIR" width="480" height="400" />

### How FLIR Works

FLIR is relatively straightforward. JavaScript finds the parts of your page that need to be replaced. It then sends the text for each of those parts to a PHP script that generates an image with the desired fonts, and then it plugs them back in where they belong on the page.</p>

### Benefits of FLIR

*   Doesn't require Flash
*   Supports word wrapping, so long headers aren't a problem
*   Works with almost any font you choose
*   Degrades gracefully if JavaScript is not available

### Drawbacks/Disadvantages of FLIR

*   Requires JavaScript
*   Text selection in Internet Explorer is virtually impossible
*   Will not work if images are disabled

## 6\. sIFR 3

<a href="https://novemberborn.net/sifr3">sIFR 3</a> is the newest version of sIFR. It's currently in development, so bugs still need to be worked out. A number of new features have been added, and using sIFR is now easier.

<a href="https://novemberborn.net/sifr3"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af98c856-a1b5-4db5-bed0-757ebc777888/sifr3pic.jpg" alt="sIFR 3" width="480" height="400" /></a>

### How sIFR 3 Works

sIFR 3 works much like sIFR 2.0. It uses Flash and JavaScript to replace text on the page with a Flash movie, while retaining accessibility features.</p>

### Benefits of sIFR 3

*   Same benefits as sIFR 2, mentioned above
*   Allows control of kerning, leading and line-height properties
*   Has the ability to ignore specific elements during replacement
*   Supports pixel fonts
*   Allows the use of background images within the Flash file

### Drawbacks/Disadvantages of sIFR 3

*   Same drawbacks as sIFR 2, mentioned above

## 7\. SIIR (Scalable Inline Image Replacement)

<a href="https://www.whaleofadive.com/misc/siir/about.php">SIIR</a> is another technique that replaces your original text with an image file in whatever font you choose. It includes a caching program to reduce the load on your server from all of the dynamically generated content, and it also includes some accessibility features. SIIR works with virtually any TrueType font.

<a href="https://www.whaleofadive.com/misc/siir/about.php"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/682e9575-b674-4e16-a19f-9f59dc59e7bb/siirpic.jpg" alt="SIIR" width="480" height="400" /></a>

### How SIIR Works

SIIR works like most other dynamic text replacement techniques that use images to replace the original text. A mixture of JavaScript and PHP code finds the individual elements that need to be replaced; it pulls text from the website to generate dynamic images in the desired font, and then inserts those images in place of the text.</p>

### Benefits of SIIR

*   Can be used to generate text with any TrueType font
*   Documentation is very thorough and easy to understand and includes explanations of modifications you can make
*   Uses the `alt` attribute in images to display the original text if the browser has images turned off
*   Does not require Flash
*   Doesn't detract from SEO, because the original text is still displayed in your code

### Drawbacks/Disadvantages of SIIR

*   Replaced text does not change when a user increases text size in their browser (but most browsers now use "zoom", so this is less of a concern)
*   Can be processor-intensive, though the caching does help
*   Copying and pasting the text in Internet Explorer is not possible

## 8\. sIFR Lite

Based on the original sIFR technique, <a href="https://www.allcrunchy.com/Web_Stuff/sIFR_lite/">sIFR Lite</a> is a simpler, more user-friendly technique. The result is much more light-weight than the original and entirely object-oriented. It has been tested on Safari, Firefox, Camino, IE and Opera.

<a href="https://www.allcrunchy.com/Web_Stuff/sIFR_lite/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1328bc00-f9e8-47da-aa25-48213bf293db/sifrlitepic.jpg" alt="sIFR Lite" width="480" height="400" /></a>

### How sIFR Lite Works

Like sIFR, sIFR Lite uses a combination of Flash and JavaScript to replace the original text with a Flash file. JavaScript searches the page for elements that need to be replaced, then Flash scripts create the dynamic images, and JavaScript replaces the original text with the new Flash files.</p>

### Benefits of sIFR Lite

*   Same as sIFR 2, mentioned above
*   Much smaller file size than original sIFR (3.7 KB vs. 22 KB)
*   Will automatically detect text color in your original file, which is an improvement over the original method that requires the developer to enter the color manually

### Drawbacks/Disadvantages of sIFR Lite

*   Same drawbacks as sIFR 2, mentioned above
*   Uses tag names and classes instead of CSS selectors, which does affect usability (although it does make it faster and more maintainable)

## 9\. Dynamic Text Replacement (DTR)

This is the original <a href="https://www.alistapart.com/articles/dynatext/">Dynamic Text Replacement</a> technique that appeared on A List Apart in June of 2004. It uses a combination of JavaScript and PHP to replace plain text on your page with a dynamically generated image. It is the precursor to all of the techniques discussed above. If it weren't for this technique, many of the other ones may not have been developed. It should also be noted that the demo page for this method now redirects to the P+C DTR method mentioned above, so it seems that the original method is viewed as obsolete.

<a href="https://www.alistapart.com/articles/dynatext/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2b9e5d5-f766-4ff5-88d9-7cdf0996ff06/dtrpic.jpg" alt="Dynamic Text Replacement" width="480" height="400" /></a>

### How DTR Works

A small PHP script generates and renders a PNG image whenever it's requested by a JavaScript file. The JavaScript file is largely based on Peter-Paul Koch's <a href="https://www.quirksmode.org/dom/fir.html">JavaScript Image Replacement</a> method. Basically, once the HTML on a page has finished loading, a JavaScript file tests for image support, and if images are supported, it finds the elements that need to be replaced and sends them to the PHP script. Using it is fairly straightforward, and only a couple of lines of code need to be configured.</p>

### Benefits of DTR

*   Doesn't require Flash
*   If the font you're replacing supports foreign characters, this method will work, even if the page is translated (e.g. through Google or another service)

### Drawbacks/Disadvantages of DTR

*   Requires images and JavaScript
*   Text selection is difficult
*   Method is obsolete, and so is not supported

## 10\. PHP Image Replacement

<a href="https://www.xanthir.com/pir/">PHP Image Replacement</a> (also known as PIR) is based at least in part on the method originally outlined by A List Apart but modified to be used with jQuery for better control over the end images produced.

<a href="https://www.xanthir.com/pir/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a3e138d-24b0-4537-aef1-c0f1a8015c28/pir.jpg" alt="PHP Image Replacement" width="500" height="450" /></a>

### How PIR Works

PHP Image Replacement uses a modified version of the PHP script from A List Apart to dynamically create the replacement images and then uses jQuery to dynamically replace pieces of the page text with images generated by the PHP script.</p>

### Benefits of PIR

*   Claims to be the simplest script of this type currently available.
*   Takes relevant information about background, size, color, etc. from the document itself.
*   Very lightweight.
*   Maintains accessibility and degrades gracefully.</p>

### Drawbacks/Disadvantages of PIR

*   Requires JavaScript.
*   Setup requires some basic PHP and JavaScript knowledge.</p>

## 11\. FontJazz

<a href="https://fontjazz.com/">FontJazz</a> is a JavaScript typography engine that works entirely on the client-side and requires no server-side processes. It works with any typeface.

<a href="https://fontjazz.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8755f13c-6a09-4e10-81c1-ef62cbbf2598/fontjazz.jpg" alt="FontJazz" width="500" height="450" /></a>

### How FontJazz Works

FontJazz uses JavaScript to render headlines in the user's browser, rather than as images on your site's server.</p>

### Benefits of FontJazz

*   Compatible with a wide variety of browsers, including IE5+, Firefox 2+ and Google Chrome.
*   Uses only client-side scripting.
*   Degrades gracefully, showing the original type if FontJazz isn't supported.
*   Works with any typeface.
*   SEO friendly.</p>

### Drawbacks/Disadvantages of FontJazz

*   Requires JavaScript.
*   Doesn't support kerning.</p>

## 12\. WordPress Plug-Ins For Dynamic Text Replacement

A few WordPress plug-ins are available for some of the dynamic text replacement methods mentioned above, as well as two that are unique to WordPress. The biggest advantage of plug-ins is that less coding is usually required, and you're less likely to run into bugs from conflicting scripts.</p>

### Facelift Image Replacement (FLIR) for WordPress

<a href="https://www.23systems.net/plugins/facelift-image-replacement-flir/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64fa6a8b-b431-444b-a2b7-96caf4888f35/wpflirpic.jpg" alt="WP FLIR" width="480" height="400" /></a>

<a href="https://www.23systems.net/plugins/facelift-image-replacement-flir/">FLIR</a> for WordPress is still in development but is close to being completed. It works just like the FLIR method mentioned above. The main bug currently present is that automatic updates don't always work. Almost all of the configuration for FLIR can be done from the admin panel, though you'll still need to do some things manually (such as upload and configure fonts).</p>

### WP sIFR

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29f51e37-9908-41e4-adf2-0393378febb7/wpsifrpic.jpg" alt="WP sIFR" width="480" height="400" />

WP sIFR works like sIFR 2.0. The only configuration you have to do is upload your SWF font file to the plug-in directory and activate the plug-in. All of the other configuration is done from within the WordPress admin panel.</p>

### Benefits of sIFR Lite

*   Same as sIFR 2, mentioned above
*   Much smaller file size than original sIFR (3.7 KB vs. 22 KB)
*   Will automatically detect text color in your original file, which is an improvement over the original method that requires the developer to enter the color manually

### Drawbacks/Disadvantages of sIFR Lite

*   Same drawbacks as sIFR 2, mentioned above
*   Uses tag names and classes instead of CSS selectors, which does affect usability (although it does make it faster and more maintainable)

## 9\. Dynamic Text Replacement (DTR)

This is the original <a href="https://www.alistapart.com/articles/dynatext/">Dynamic Text Replacement</a> technique that appeared on A List Apart in June of 2004. It uses a combination of JavaScript and PHP to replace plain text on your page with a dynamically generated image. It is the precursor to all of the techniques discussed above. If it weren't for this technique, many of the other ones may not have been developed. It should also be noted that the demo page for this method now redirects to the P+C DTR method mentioned above, so it seems that the original method is viewed as obsolete.

<a href="https://www.alistapart.com/articles/dynatext/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2b9e5d5-f766-4ff5-88d9-7cdf0996ff06/dtrpic.jpg" alt="Dynamic Text Replacement" width="480" height="400" /></a>

### How DTR Works

A small PHP script generates and renders a PNG image whenever it's requested by a JavaScript file. The JavaScript file is largely based on Peter-Paul Koch's <a href="https://www.quirksmode.org/dom/fir.html">JavaScript Image Replacement</a> method. Basically, once the HTML on a page has finished loading, a JavaScript file tests for image support, and if images are supported, it finds the elements that need to be replaced and sends them to the PHP script. Using it is fairly straightforward, and only a couple of lines of code need to be configured.</p>

### Benefits of DTR

*   Doesn't require Flash
*   If the font you're replacing supports foreign characters, this method will work, even if the page is translated (e.g. through Google or another service)

### Drawbacks/Disadvantages of DTR

*   Requires images and JavaScript
*   Text selection is difficult
*   Method is obsolete, and so is not supported

## 10\. PHP Image Replacement

<a href="https://www.xanthir.com/pir/">PHP Image Replacement</a> (also known as PIR) is based at least in part on the method originally outlined by A List Apart but modified to be used with jQuery for better control over the end images produced.

<a href="https://www.xanthir.com/pir/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a3e138d-24b0-4537-aef1-c0f1a8015c28/pir.jpg" alt="PHP Image Replacement" width="500" height="450" /></a>

### How PIR Works

PHP Image Replacement uses a modified version of the PHP script from A List Apart to dynamically create the replacement images and then uses jQuery to dynamically replace pieces of the page text with images generated by the PHP script.</p>

### Benefits of PIR

*   Claims to be the simplest script of this type currently available.
*   Takes relevant information about background, size, color, etc. from the document itself.
*   Very lightweight.
*   Maintains accessibility and degrades gracefully.</p>

### Drawbacks/Disadvantages of PIR

*   Requires JavaScript.
*   Setup requires some basic PHP and JavaScript knowledge.</p>

## 11\. FontJazz

<a href="https://fontjazz.com/">FontJazz</a> is a JavaScript typography engine that works entirely on the client-side and requires no server-side processes. It works with any typeface.

<a href="https://fontjazz.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8755f13c-6a09-4e10-81c1-ef62cbbf2598/fontjazz.jpg" alt="FontJazz" width="500" height="450" /></a>

### How FontJazz Works

FontJazz uses JavaScript to render headlines in the user's browser, rather than as images on your site's server.</p>

### Benefits of FontJazz

*   Compatible with a wide variety of browsers, including IE5+, Firefox 2+ and Google Chrome.
*   Uses only client-side scripting.
*   Degrades gracefully, showing the original type if FontJazz isn't supported.
*   Works with any typeface.
*   SEO friendly.</p>

### Drawbacks/Disadvantages of FontJazz

*   Requires JavaScript.
*   Doesn't support kerning.</p>

## 12\. WordPress Plug-Ins For Dynamic Text Replacement

A few WordPress plug-ins are available for some of the dynamic text replacement methods mentioned above, as well as two that are unique to WordPress. The biggest advantage of plug-ins is that less coding is usually required, and you're less likely to run into bugs from conflicting scripts.</p>

### Facelift Image Replacement (FLIR) for WordPress

<a href="https://www.23systems.net/plugins/facelift-image-replacement-flir/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64fa6a8b-b431-444b-a2b7-96caf4888f35/wpflirpic.jpg" alt="WP FLIR" width="480" height="400" /></a>

<a href="https://www.23systems.net/plugins/facelift-image-replacement-flir/">FLIR</a> for WordPress is still in development but is close to being completed. It works just like the FLIR method mentioned above. The main bug currently present is that automatic updates don't always work. Almost all of the configuration for FLIR can be done from the admin panel, though you'll still need to do some things manually (such as upload and configure fonts).</p>

### WP sIFR

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29f51e37-9908-41e4-adf2-0393378febb7/wpsifrpic.jpg" alt="WP sIFR" width="480" height="400" />

WP sIFR works like sIFR 2.0. The only configuration you have to do is upload your SWF font file to the plug-in directory and activate the plug-in. All of the other configuration is done from within the WordPress admin panel.</p>

### WP-Cufon

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48305ddf-26c5-45bd-ae73-47aaf09e3dd3/wpcufonpic.jpg" alt="WP-Cufon" width="480" height="400" />

WP-Cufon lets you easily use Cufón on your WordPress website and it includes good documentation and regular updates. It also works just like Cufón, so you'll still need to convert your fonts beforehand. Configuration is done directly in the admin panel in WordPress.</p>

### AnyFont

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/879c0380-5e4d-49ff-9e0f-f1a3684323e0/anyfontpic.jpg" alt="AnyFont" width="480" height="400" />

AnyFont uses custom fonts (TrueType or OpenType) to replace text in post titles, menu items, and pretty much anything else in your WordPress theme. It has a font manager that you use to easily upload new fonts from within WordPress; it has built-in style management; you can add shadows to your text; it includes cache management; and it uses SEO-compatible image replacements.</p>

### Font Burner Control Panel

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/960621a7-97f3-4f70-a716-aa8825622fae/fontburnerpic.jpg" alt="Font Burner Control Panel" width="480" height="400" />

The Font Burner Control Panel is a different technique for adding fonts to your website. Basically, it allows you to use any of the more than 1000 fonts available on Font Burner on your WordPress blog. All you have to do is upload the plug-in to your plug-ins folder, activate it and then configure it through the admin panel.</p>

## 13\. Font Embedding Options

Embedding fonts is another option if you don't want to use an image replacement technique. While you can upload fonts to your own server and use @font-face that way, it uses a lot more bandwidth and there can be intellectual property issues to deal with. The services below offer a great alternative by hosting fonts for you and serving them remotely. The advantage is, obviously, that you can have a rich embedding of commercial fonts in your designs; the drawback is that these services usually require membership and a monthly fee.</p>

### Typotheque

<a href="https://www.typotheque.com/webfonts"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/183b0df5-2683-4429-b583-944400bf6e24/typotheque.jpg" alt="typotheque" width="500" height="450" /></a>

<a href="https://www.typotheque.com/webfonts">Typotheque</a> is a service that lets you use the @font-face rule in CSS. It works with fonts within the Typotheque collection, which currently consists of more than 25 typefaces. They have a free trial license available, as well as a variety of paid options.</p>

### Kernest

<a href="https://www.kernest.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e611f33d-95a0-4c59-bf1a-d0ff0a7f302f/kernest.jpg" alt="Kernest" /></a>

<a href="https://www.kernest.com/">Kernest.com</a> is another web service that takes advantage of the @font-face attribute in your CSS and serves fonts for you, saving bandwidth. They serve both free and commercial fonts. Pricing is based on the font(s) you choose.</p>

### Typekit

<a href="https://www.typekit.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f11d321c-c34d-4600-9df0-da32e444cd18/typekit.jpg" alt="Typekit" width="480" height="393" /></a>

Together with various typographic foundries, <a href="https://www.typekit.com/">Typekit.com</a> has developed a web-only font linking license that allows for rich font embedding in web design and also protects interests of type designers. Typekit uses jQuery and a subscription service to allow designers to embed non-standard, non-system-specific fonts into HTML-pages.

As other services, it uses the @font-face CSS property. The configuration takes place via the Typekit's plattform; to use the fonts, designers just need to insert two JavaScript-snippets into their pages. The service offers a platform that hosts both free and commercial fonts and has various plans ranging from $24.99 per month to $49.99 per month. The service is in closed beta (October 2009). Developed by Jeffrey Veen.</p>

## Dynamic Text Replacement Methods Compared

Here's a handy table that shows the features of each technique mentioned above:

<table class="shortcuts" border="0" cellspacing="0" cellpadding="0" width="500"><br>
<tbody>
<tr class="main">
<th scope="col">Method</th>
<th scope="col">Technology Used</th>
<th scope="col">Font Types Supported</th>
<th scope="col">Images?</th>
</tr>
<tr>
<th scope="row">sIFR 2.0</th>
<td>Flash, JavaScript</td>
<td>Not specified</td>
<td>No, Flash</td>
</tr>
<tr>
<th scope="row">P+C DTR</th>
<td>PHP, CSS</td>
<td>Not specified</td>
<td>Yes</td>
</tr>
<tr>
<th scope="row">Cufon</th>
<td>JavaScript</td>
<td>Must be converted:  TTF, OTF, PFB, PostScript</td>
<td>Yes</td>
</tr>
<tr>
<th scope="row">Typeface.js</th>
<td>JavaScript</td>
<td>Must be converted: TrueType, OpenType</td>
<td>Yes</td>
</tr>
<tr>
<th scope="row">FLIR</th>
<td>JavaScript, PHP</td>
<td>Not specified</td>
<td>Yes</td>
</tr>
<tr>
<th scope="row">sIFR 3</th>
<td>Flash, JavaScript</td>
<td>Not specified</td>
<td>No, Flash</td>
</tr>
<tr>
<th scope="row">SIIR</th>
<td>JavaScript, PHP</td>
<td>TrueType</td>
<td>Yes</td>
</tr>
<tr>
<th scope="row">sIFR Lite</th>
<td>Flash, JavaScript</td>
<td>Not specified</td>
<td>No, Flash</td>
</tr>
<tr>
<th scope="row">DTR</th>
<td>JavaScript, PHP</td>
<td>OpenType, TrueType</td>
<td>Yes</td>
</tr>
<tr>
<th scope="row">PHP Image Replacement</th>
<td>JavaScript, PHP, jQuery</td>
<td>Any</td>
<td>Yes</td>
</tr>
<tr>
<th scope="row">FontJazz</th>
<td>JavaScript</td>
<td>Any</td>
<td>Yes (background)</td>
</tr>
<tr>
<th scope="row">AnyFont</th>
<td>WordPress-Only</td>
<td>TrueType, OpenType</td>
<td>Yes</td>
</tr>
<tr>
<th scope="row">Font Burner Control Panel</th>
<td>WordPress-Only</td>
<td>Font Burner Fonts Only</td>
<td>Yes</td>
</tr>
<tr>
<th scope="row">Typotheque</th>
<td>@font-face</td>
<td>Typotheque Fonts Only</td>
<td>No</td>
</tr>
<tr>
<th scope="row">Kernest.com</th>
<td>@font-face</td>
<td>Kernest.com Fonts Only</td>
<td>No</td>
</tr>
<tr>
<th scope="row">Typekit</th>
<td>@font-face</td>
<td>Typekit Fonts Only</td>
<td>No</td>
</tr>
</tbody></table>

### Further Resources:

*   Simplified Dynamic Text Replacement This article from CSS Tinderbox discusses Cufon and how to use it effectively.
*   [Dynamic Image Replacement: Practical Techniques and Tools](https://www.hongkiat.com/blog/dynamic-image-replacement-practical-techniques-and-tools/) This article from HongKiat offers an overview of multiple methods of dynamically replacing text on your website.
*   [Dynamic Text Replacement](https://www.netmag.co.uk/zine/javascript/dynamic-text-replacement) This article from .net magazine covers usage of sIFR.
*   [Roundup of Font Embedding and Replacement Techniques](https://zomigi.com/blog/roundup-of-font-embedding-and-replacement-techniques/) An excellent roundup with information on a variety of techniques and scripts.</p>

### About the Author

<em>Cameron Chapman is a professional Web and graphic designer with over 6 years of experience. She also writes for a number of blogs, including her own, <a href="https://cameronchapman.com">Cameron Chapman On Writing</a>. She's also the author of <a href="https://internetfamousbook.com">Internet Famous: A Practical Guide to Becoming an Online Celebrity</a>.</em>

<em>(al) (ll) (vf)</em>


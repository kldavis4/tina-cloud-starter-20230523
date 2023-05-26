---
title: 'Guide to CSS Font Stacks: Techniques and Resources'
slug: complete-guide-to-css-font-stacks
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/728567e2-c6b4-4515-94f0-4d7586189ab2/illutypo.jpg
date: 2009-09-22T10:20:31.000Z
author: cameron-chapman
description: >-
  CSS Font stacks are one of those things that elude a lot of designers.
  Many stick to the basic stacks tools auto-recommend or go even more
  basic by just specifying a single web-safe font. But doing either of those
  things means you're missing out on some great typography options. Font stacks
  can make it possible to show at least some of your visitors your site's
  typography exactly the way you intend without showing everyone else a default
  font.
categories:
  - Coding
  - Typography
  - CSS
  - Essentials
---
<strong>CSS Font stacks</strong> are one of those things that elude a lot of designers. Many stick to the basic stacks Dreamweaver auto-recommends or go even more basic by just specifying a single web-safe font.

But doing either of those things means you're missing out on some great typography options. Font stacks can make it possible to show at least some of your visitors your site's typography exactly the way you intend without showing everyone else a default font. Read on for more information on using and creating effective font stacks with CSS.

You might be interested in the following related posts:

*   [16 Pixels: For Body Copy. Anything Less Is A Costly Mistake](https://www.smashingmagazine.com/2011/10/16-pixels-body-copy-anything-less-costly-mistake/)
*   [The @Font-Face Rule And Useful Web Font Tricks](https://www.smashingmagazine.com/2011/03/the-font-face-rule-revisited-and-useful-tricks/)
*   [Avoiding Faux Weights And Styles With Google Web Fonts](https://www.smashingmagazine.com/2012/07/avoiding-faux-weights-styles-google-web-fonts/)
*   [Review of Popular Web Font Embedding Services](https://www.smashingmagazine.com/2010/10/review-of-popular-web-font-embedding-services/)

## Creating Your Own Font Stacks

There are a huge variety of font stacks recommended. It seems every designer has their own favorites, what they consider to be the "ultimate" font stack. While there is no definitive font stack out there, there are a few things to keep in mind when using or creating your own stacks.

{{% feature-panel %}}

First of all, make sure you <strong>always include a generic font family at the end</strong> of your font stacks. This way, if for some strange reason the person visiting your site has virtually no fonts installed, at least they won't end up looking at everything in Courier New. Second, there's a basic formula to creating a good font stack: <em>'Preferred Font', 'Next best thing', 'Something common and sorta close', 'Similar Web-safe', 'Generic font'.</em> There's nothing wrong with having more than one font for any of those, but try to keep your font stack reasonably short (six to ten fonts is a pretty good maximum number).

Third, make sure you <strong>pay attention to the scale of the fonts</strong> in your stack. One common thing I see in font stacks is the inclusion of Verdana and Arial or Helvetica in the same stack. Verdana is a very wide font; Arial is relatively narrow. In effect, this can make your site's typography appear very differently to different visitors. The same goes for Times New Roman (narrow) and Georgia (wide). Considering both Arial/Helvetica and Verdana are considered web-safe (same goes for Times/Times New Roman and Georgia), it doesn't make much sense to include both.</p>

## Common Font Stacks

A lot of designers out there have taken a crack at creating ideal font stacks. While I have yet to see an "ultimate" font stack, there are plenty of really great ones out there to choose from if you don't want to take the time create your own custom stacks. Here are some of the good ones we've seen.</p>

### Better CSS Font Stacks

Unit Interactive published an article last summer with a collection of "better" CSS font stacks. The list is extensive, with font stacks that should satisfy just about anyone. Fonts are listed out according to whether they're appropriate for headlines or body content.

Here are some listed for body text:

*   Baskerville, 'Times New Roman', Times, serif
*   Garamond, 'Hoefler Text', 'Times New Roman', Times, serif
*   Geneva, 'Lucida Sans', 'Lucida Grande', 'Lucida Sans Unicode', Verdana, sans-serif
*   GillSans, Calibri, Trebuchet, sans-serif

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1c9d447-f3f8-4a2b-8554-e7795080b9c4/garamondhoeflertext1.jpg)

For headlines:

*   Georgia, Times, 'Times New Roman', serif
*   Palatino, 'Palatino Linotype', 'Hoefler Text', Times, 'Times New Roman', serif
*   Tahoma, Verdana, Geneva
*   Trebuchet, Tahoma, Arial, sans-serif

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7184276c-70c7-4e6d-a5d3-4b16d25b04b1/trebuchettahoma1.jpg)

And a few that are balanced for either body or headline text:

*   Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif
*   Cambria, Georgia, Times, 'Times New Roman', serif
*   'Copperplate Light', 'Copperplate Gothic Light', serif
*   Futura, 'Century Gothic', AppleGothic, sans-serif

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed7a2164-79fe-4dcd-80e0-96053acf828b/futuracenturygothic1.jpg)

### 8 Definitive Web Font Stacks

<a href="https://www.sitepoint.com/article/eight-definitive-font-stacks/">This article from Sitepoint</a> written by Michael Tuck lists eight font stacks that are supposed to be the ultimate stacks for any application. It's based on a basic formula of: 'exact font', 'nearest alternative', 'platform-wide alternative(s)', 'universal (cross-platform) choice(s)', generic. My biggest issues with some of these font stacks is their length; is it really necessary to include 17 different fonts in a single font stack? I don't think so...

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/301cceca-17d9-4e81-a3ac-c151905c02ed/trebuchetstack1.jpg)](https://www.sitepoint.com/article/eight-definitive-font-stacks/)

The font stacks:

*   The Times New Roman-based serif stack: Cambria, 'Hoefler Text', Utopia, 'Liberation Serif', 'Nimbus Roman No9 L Regular', Times, 'Times New Roman', serif
*   A Modern Georgia-based serif stack: Constantia, 'Lucida Bright', Lucidabright, 'Lucida Serif', Lucida, 'DejaVu Serif', 'Bitstream Vera Serif', 'Liberation Serif', Georgia, serif
*   A more traditional Garamond-based serif stack: 'Palatino Linotype', Palatino, Palladio, 'URW Palladio L', 'Book Antiqua', Baskerville, 'Bookman Old Style', 'Bitstream Charter', 'Nimbus Roman No9 L', Garamond, 'Apple Garamond', 'ITC Garamond Narrow', 'New Century Schoolbook', 'Century Schoolbook', 'Century Schoolbook L', Georgia, serif
*   The Helvetica/Arial-based sans serif stack: Frutiger, 'Frutiger Linotype', Univers, Calibri, 'Gill Sans', 'Gill Sans MT', 'Myriad Pro', Myriad, 'DejaVu Sans Condensed', 'Liberation Sans', 'Nimbus Sans L', Tahoma, Geneva, 'Helvetica Neue', Helvetica, Arial, sans-serif
*   The Verdana-based sans serif stack: Corbel, 'Lucida Grande', 'Lucida Sans Unicode', 'DejaVu Sans', 'Bitstream Vera Sans', 'Liberation Sans', Verdana, 'Verdana Ref', sans-serif
*   The Trebuchet-based sans serif stack: 'Segoe UI', Candara, 'Bitstream Vera Sans', 'DejaVu Sans', 'Bitsream Vera Sans', 'Trebuchet MS', Verdana, 'Verdana Ref', sans-serif
*   The heavier "Impact" sans serif stack: Impact, Haettenschweiler, 'Franklin Gothic Bold', Charcoal, 'Helvetica Inserat', 'Bitstream Vera Sans Bold', 'Arial Black', sans-serif
*   The Monospace stack: Consolas, 'Andale Mono WT', 'Andale Mono', 'Lucida Console', 'Lucida Sans Typewriter', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Liberation Mono', 'Nimbus Mono L', Monaco, 'Courier New', Courier, monospace

### The Myth of 'Web-Safe' Fonts

<a href="https://safalra.com/web-design/typography/web-safe-fonts-myth/">The Myth of 'Web-Safe' Fonts</a> from Safalra.com offers up five simple, straightforward font stacks for web typography. These stacks are pretty bare-bones as far as most recommended font stacks go, but they're perfectly adequate for many applications, as well as being a good starting point for building your own stacks.

*   The 'wide' sans serif stack: Verdana, Geneva, sans-serif
*   The 'narrow' sans serif stack: Tahoma, Arial, Helvetica, sans-serif
*   The 'wide" serif stack: Georgia, Utopia, Palatino, 'Palatino Linotype', serif
*   The 'narrow' serif stack: 'Times New Roman', Times, serif
*   The monospace stack: 'Courier New', Courier, monospace

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc36342e-dd3d-49cc-ad9c-de90d3628ebc/tahomaarial1.jpg)](https://safalra.com/web-design/typography/web-safe-fonts-myth/)

## Tools

### Font Matrix

<a href="https://media.24ways.org/2007/17/fontmatrix.html">Font Matrix</a> is a font comparison tool that lists fonts bundled with Windows XP, Windows Vista, Mac OS X Tiger, Mac OS X Leopard, Microsoft Office (2003, 2007 and 2004 for Mac) and the Adobe Creative Suite. The chart shows which software bundles and operating systems come with which fonts, so you can get a good idea of how common a particular font might be. This is an incredibly valuable tool for those looking to create their own custom font stacks.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03df8b69-6d0b-483b-b460-7c006d93ed9a/fontmatrix1.jpg)](https://media.24ways.org/2007/17/fontmatrix.html)

### Complete Guide to Pre-Installed Fonts in Linux, Mac and Windows

Here's another <a href="https://www.apaddedcell.com/web-fonts">chart</a> that shows the fonts commonly installed on Linux, Mac and Windows machines, grouped together by family and similarity. It's another really valuable tool for font stack creators.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/976d2103-7ffa-490e-86a1-85b786018001/completefontguide1.jpg)](https://www.apaddedcell.com/web-fonts)

### Typechart

<a href="https://www.typechart.com/">Typechart</a> shows you web-safe and common fonts and suggests different sizes and styles for headings, paragraphs, and other typographic elements. There are a ton of different browsing options, and you can preview the way fonts will look on both Windows and Mac machines before downloading the CSS. The only drawback to Typechart is that it only includes a handful of fonts: Arial/Helvetica, Cambria, Georgia, Lucida Grande, Lucida Sans Unicode, Trebuchet MS, and Verdana.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6448a2ea-161f-472b-84d8-ca8c82355fdd/typechart1.jpg)](https://www.typechart.com/)

### Typetester

<a href="https://www.typetester.org/">Typetester</a> lets you try out up to three fonts side-by-side. This can be a great way to test font stacks to see what the differences will be as the stacks degrade. You can use any font on your system, though it does categorize fonts by web safe, Windows default, and Mac default, making it easier to create stacks without other reference materials.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62b6d9b6-9faa-4d3e-a042-c12cfece782a/typetester1.jpg)](https://www.typetester.org/)

### Font Stack Builder

Code Style offers the Font Stack Builder for creating font stacks based on font family, and whether the fonts are generally installed on Windows, Mac or Linux machines. You can add as many fonts as you want and it will show you a grid with how common those fonts are on different kinds of machines.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a30298d-bebf-44c4-8771-98e35c91cd9f/fontstackbuilder1.jpg)

## Articles

There are hundreds of articles out there about font stacks. Some have been mentioned above, but there are plenty of others that deserve some recognition. Here are a few:

<strong><a href="https://www.inspirationbit.com/striking-web-sites-with-font-stacks-that-inspire/">Striking Web Sites with Font Stacks that Inspire</a></strong>
This article covers twenty different websites with excellent font stacks. Basic web-safe and common fonts are covered along with more creative font stacks. It's a great resource for getting some inspiration before creating your own stacks.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3bbbe23-420f-4b85-920d-f44a735a52e1/strikingwebsites1.jpg)](https://www.inspirationbit.com/striking-web-sites-with-font-stacks-that-inspire/)

<strong><a href="https://www.devlounge.net/design/better-font-families-in-css">Better Font Families in CSS</a></strong>
This article from Devlounge gives a very brief overview of the author's favored font stacks, as well as a few tips for creating your own stacks.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1537a84-47cf-4189-95ee-e3bf37b29c77/betterfontfamilies1.jpg)](https://www.devlounge.net/design/better-font-families-in-css)

<strong><a href="https://www.clagnut.com/blog/266/">The New Typography</a></strong>
This article gives a great overview of creating font stacks and good web typography. There are plenty of tips mentioned, including which fonts to avoid using in the same font stacks and why.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11ace9b1-f5f7-4fee-84af-6a1da76b1034/newtypography1.jpg)](https://www.clagnut.com/blog/266/)

<strong><a href="https://nicewebtype.com/notes/2009/04/23/css-font-stacks/">Roundup: CSS Font Stacks</a></strong>
This article is a great introduction to CSS font stacks and how to use them effectively. It includes some tools, tips, and other information about creating your own font stacks or choosing which ones to use.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a58b331-469b-4d8c-8ea4-4c3321a2f69a/roundupcssfontstacks1.jpg)](https://nicewebtype.com/notes/2009/04/23/css-font-stacks/)

## Excellent Font Stack Examples

Here's a handful of sites that have excellent font stacks and great typography in general. You can find more examples at <a href="https://typesites.com/archives/">Typesites</a>.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37a6e2fc-f9ed-43f9-b5de-a5229ea18421/wilsonminer1.jpg)](https://www.wilsonminer.com/)

<strong>Font stack:</strong> "Helvetica Neue", Helvetica, Arial, sans-serif

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b8eef90-fbc5-4f18-b165-a3f9592620f7/typesites1.jpg)](https://typesites.com/projects/typetweets/)

<strong>Font stack:</strong> "Lucida Fax", Georgia, Helvetica, Arial, sans-serif

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c78bf08e-e6fd-483f-a5b2-fdef39c2bf35/jontangerine1.jpg)](https://jontangerine.com/)

<strong>Font stack:</strong> Baskerville, Palatino, 'Palatino Linotype', Georgia, Serif

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f161f7d0-8b6a-4143-a4ca-a68b49c1b677/ilovetypography1.jpg)](https://ilovetypography.com/)

<strong>Font stack:</strong> "Lucida Grande", Geneva, Helvetica, sans-serif (used for some of the headings and meta information)

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af0b1587-3fb8-4406-b196-d915bd7d40b9/twistedintellect1.jpg)](https://twistedintellect.com)

<strong>Font stack:</strong> "Adobe Caslon Pro", "Hoefler Text", Georgia, Garamond, Times, serif (pretty nice stack for what is primarily a holding page!)

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52cb3765-bde6-4467-9abd-6cb52a7544b3/aestheticallyloyal1.jpg)](https://www.aestheticallyloyal.com/)

<strong>Font stack:</strong> "Courier new", Courier, "Andale Mono"

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06761b28-0c5c-422c-bc08-90ab75847695/astheria.jpg)](https://astheria.com/)

<strong>Font stack:</strong> Gotham, "Helvetica Neue", Helvetica, Arial, sans-serif;

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c65e9fad-ac6c-4a2c-8771-26d745999a57/arstechnica1.jpg)](https://arstechnica.com)

<strong>Font stack:</strong> Arial, sans-serif

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dae80cfe-0299-440d-aa2e-7cfe25c02a50/digitalweb1.jpg)](https://www.digital-web.com)

<strong>Font stack:</strong> "Lucida Grande", Tahoma, Verdana, sans-serif

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/724efe77-8274-4c8c-ac35-832090060d43/netmag1.jpg)](https://www.netmag.co.uk/)

<strong>Font stack:</strong> Helvetica, Arial, sans-serif

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b23873a-2f4f-4baf-817c-e584aaf52500/time1.jpg)](https://www.time.com/time/)

<strong>Font stack:</strong>"Arial black", arial, sans-serif

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00b86d03-7e45-4ff9-8602-a7ad08fc54d2/psdtutsplus1.jpg)](https://psd.tutsplus.com)

<strong>Font stack:</strong>Arial, Helvetica, sans-serif

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/045cf285-3071-48bd-8855-56efae8c6c40/huffpo1.jpg)](https://www.huffingtonpost.com)

<strong>Font stack:</strong> Arial, "Helvetica Neue", Helvetica, sans-serif

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bba9603-d007-41f2-acd6-22db208ac1bd/mac.jpg)](https://mac.appstorm.net/)

<strong>Font stack:</strong>"Myriad Pro", Helvetica, Arial, sans-serif

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd856d9b-80a5-4aef-8247-52895eb55c0a/newsvine1.jpg)](https://www.newsvine.com/)

<strong>Font stack:</strong> "Lucida Grande", Arial, Verdana, Helvetica, sans-serif

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/726724f6-98e7-41a5-a7ad-04515efd26c0/markboulton1.jpg)](https://www.markboulton.co.uk/)

<strong>Font stack:</strong> Georgia, "Times New Roman", Times, serif


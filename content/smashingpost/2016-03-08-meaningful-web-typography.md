---
title: Tools And Resources For A More Meaningful Web Typography
slug: meaningful-web-typography
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96747906-4e90-41c1-b3ef-664afe3f6470/typography-resources-opt.png
date: 2016-03-08T23:26:48.000Z
author: cosima-mielke
description: >-
  It’s the small details that make a project shine. **Solid typography,
  well-crafted with attention and care** is one of them. A harmonious visual
  rhythm, typographic subtleties like soft caps, margin outdents or the correct
  use of hyphens and dashes — there are a lot of things that add up to it.

  In practice, however, publishing on the web is supposed to be fast, and the
  little details are often overlooked, which is a pity, because they are not
  only pleasing to the eye but also **improve the reading experience**.
categories:
  - Typography
  - Fonts
  - Resources
---
It’s the small details that make a project shine. **Solid typography, well-crafted with attention and care** is one of them. A harmonious visual rhythm, typographic subtleties like soft caps, margin outdents or the correct use of hyphens and dashes — there are a lot of things that add up to it.</p>

## <span class="rh">Further reading</span> on Smashing:

*   [Balancing Line Length And Font Size In RWD](https://www.smashingmagazine.com/2014/09/balancing-line-length-font-size-responsive-web-design/)
*   [Responsive Typography With Sass Maps](https://www.smashingmagazine.com/2015/06/responsive-typography-with-sass-maps/)
*   [Using System UI Fonts In Web Design](https://www.smashingmagazine.com/2015/11/using-system-ui-fonts-practical-guide/)
*   [Whitespace Characters in Unicode & HTML](https://www.smashingmagazine.com/2015/10/space-yourself/#all-together-now)
*   [The Good, The Bad and The Great Examples of Web Typography](https://www.smashingmagazine.com/2014/12/the-good-the-bad-and-the-great-examples-of-web-typography/)
*   [Freebie: Freebie: Exo 2.0, a Sans Serif Font](https://www.smashingmagazine.com/2013/12/freebie-exo-2-0-geometric-sans-serif-font/)

In practice, however, publishing on the web is supposed to be fast, and the little details are often overlooked, which is a pity, because they are not only pleasing to the eye but also **improve the reading experience**.

The tools and resources compiled in this article will help you bring some of that meaning that typography has always benefited from in print to your web projects. They simplify the process of establishing a solid foundation and modular scale to build upon, take care of the little details, so they don’t get lost along the way, and offer solutions to common pitfalls. Are you ready to do some catching up on that type game?

{{% feature-panel %}}

## Establishing Visual Rhythm

### Setting the Baseline Grid

Web typography often lacks that sense of craftsmanship that typography in print has benefited from since Johannes Gutenberg invented the printing press more than 500 years ago. To bring back a more meaningful typography, the [Gutenberg Web Typography Starter Kit](https://matejlatin.github.io/Gutenberg/) sets the baseline grid to establish a proper vertical rhythm which makes sure all elements fit into it harmoniously. The kit is based on Sass and comes with two predefined themes based on the Google Fonts Merriweather and Open Sans, but custom options allow you to load custom typefaces as well. The backbone of your typography.</p>

### Calculating a Modular Scale

A modular scale sets the visual harmony of your design. You use it like a ruler to set type sizes or to measure and set the size of any element or negative space in your composition. Body text size is a good base to establish your scale, also fixed-width images, for example. The [modular scale calculator](https://www.modularscale.com/) by Scott Kellum and Tim Brown provides valuable tips to choose a base and ratio for your design and uses these values to calculate your scale. Once set, you can get your scale as a Sass or JavaScript plugin, or you can reference your calculated results right on the site. A great tool to achieve responsive typography.</p>

<figure><a href="https://www.modularscale.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34b98843-b404-4ca2-86bb-cf001798f33c/modular-scale-small-opt.png" alt="Modular scale" width="500" height="267" /></a><figcaption>The <a href="https://www.modularscale.com/">Modular Scale calculator</a> multiplies your scale’s base (for example the size of your body text) with a ratio to produce a scale of numbers that are proportionally related. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6a32dd8-6017-43f3-9eb7-199c0f3ab496/modular-scale-opt.png">View large version</a>)</figcaption></figure>

### A Framework to Build Upon

To start your typography endeavour off right, you might also want to take a look at the [Typeplate starter kit](https://typeplate.com/). It offers solid, modular and flexible base styles, proper markup that you can extend to your liking. The library is not concerned with aesthetic design choices but gives you the building blocks to establish your own typographic framework. The CSS file weighs in at only 10KB, Sass at 18KB, and a Bower package is also available.</p>

## Taking Care Of The Details

### Small Caps, Ligatures and Other Finesses Made Easy

Caring for fine typographic details often comes with a downside: there’s usually no getting around a convoluted CSS. Kenneth Ormandy’s [Utility Open Type](https://utility-opentype.kennethormandy.com/) puts an end to this. Its 1.75KB small CSS file provides CSS utility classes for advanced typographic features such as ligatures, small caps, number variants and other finesses, making them as easy to apply to your elements and `<span>`s as using bold and italics. To spare you a lot of maintenance work, Utility Open Type cascades predictably. It supports Chrome, Firefox and IE 10+ and falls back gracefully elsewhere.</p>

### An HTML Preprocessor for Better Readability

Real hanging punctuation, optical margin outdents, punctuation and space substitution, soft hyphens — it’s the small details that improve a reading experience significantly. But, unfortunately, we often don’t pay as much attention to them as they’d deserve it. That’s where the HTML preprocessor [Typeset.js](https://blot.im/typeset/) comes in. It takes care of all these typographic subtleties, so they don’t get lost along the way.</p>

<figure><a href="https://blot.im/typeset/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad880690-1bbe-458b-b491-952ec56af398/with-typesetjs-small-opt.png" alt="Text with Typeset.js enabled." width="500" height="255" /></a><figcaption>Text with <a href="https://blot.im/typeset/">Typeset.js</a> enabled. Notice how details such as hanging punctuation, small-caps conversion and space substitution improve readability compared to the image below that doesn’t have Typeset.js enabled. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5245e00-bbfb-45b4-b7ba-40f0843526d4/with-typesetjs-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://blot.im/typeset/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44bdcbe0-f207-4abb-b99e-46d0f9058cec/without-typesetjs-small-opt.png" alt="Text without Typeset.js enabled." width="500" height="255" /></a><figcaption>The same text without Typeset.js. It feels more cramped and provides the reader with less visual anchors to guide them through the text. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a6b7da1-7b41-4819-a85a-3be5d03ba337/without-typesetjs-opt.png">View large version</a>)</figcaption></figure>

### Dealing With Long Words in CSS

It might not be too much of a problem for English-speaking websites, but some languages, German, for example, have words that are very, very long. So how to deal with them in responsive web design without breaking layouts and causing cropped words? [Michael Scharnagl has found a solution](https://justmarkup.com/log/2015/07/dealing-with-long-words-in-css/): combine `overflow-wrap` with `word-wrap` and `hyphens` that will show in browsers supporting it and will break lines in other browsers. Good to know.</p>

### Making Footnotes More User-Friendly

Long reads often call for footnotes and sidenotes. The common solution to provide them on the web, however, is quite distracting to the reading flow: you click a tiny number and jump to the bottom of the page. Chris Sauvé found a less interruptive way to enrich a text with additional information. His jQuery plugin [Bigfoot.js](https://www.bigfootjs.com/) detects the footnote link and content, turns the link into an unobtrusive button and opens a pop-over when the reader clicks on the button.</p>

<figure><a href="https://www.bigfootjs.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5f1529f-5190-4ec7-8c8b-316197b21a1a/bigfootjs-small-opt.png" alt="Footnotes as pop-overs" width="500" height="356" /></a><figcaption><a href="https://www.bigfootjs.com/">Bigfoot.js</a> provides footnotes that integrate well into the natural reading flow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5171c6c3-0e17-4a49-8b13-5e21950603ca/bigfootjs-opt.png">View large version</a>)</figcaption></figure>

## Guides And Cheatsheets

### A Practical Typography Guide

If you’re looking for one comprehensive guide that covers all the essentials of professional typography, check out [Donny Truong’s free eBook](https://prowebtype.com/). It leads you step by step through the craft of making informed typographic choices, shaping your attention for detail and providing you with the technical background you need to gain full control of your typography. The eBook is free, but if you find it useful, be fair and consider paying for it. The price is up to you.</p>

### Typography Cheatsheet

Smart quotes, dumb quotes, dashes, hyphens — do you have a hard time telling them apart? Then Typewolf’s [Typography cheatsheet](https://www.typewolf.com/cheatsheet#useful-typographic-characters) is one for your bookmarks. It answers all your questions about their proper usage and recalls their Mac and Windows shortcuts and HTML entities as well as those for some other useful characters such as mathematical and non-English ones. Handy.</p>

## Choosing The Right Font

### Try A Typeface Before You Purchase It

Usually, the only impression you get of a typeface before purchasing it is the specimen on the type foundry’s website. It needs a lot of imagination to asses from that little piece of default text what the typeface will look like in your own design. So if previewing is not enough for you, [Font Stand](https://fontstand.com/) has a licensing model which might be more to your liking. It gives you the chance to try any font for free in any of your applications for one hour — perfect for some quick prototyping. You can also rent a font on a monthly basis and after 12 months it automatically becomes yours. There are currently 635 families from 32 foundries to choose from. One little downside: the service is only available for Mac users.</p>

### Inspiring Font Combinations

Combining two fonts can be a challenge. What works, what doesn’t? Do-Hee Kim’s [100 Days Of Fonts](https://100daysoffonts.com/) project is a great source for some fresh inspiration. She designed and coded another combination of two Google fonts every day for 100 days. Impressive.</p>

<figure><a href="https://100daysoffonts.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/585789a2-1907-437f-af64-fdc40b2261ca/abril-sans-narrow-opt.png" alt="A combination of Abril Fatface and Sans Narrow" width="500" height="322" /></a><figcaption>Abril Fatface and Sans Narrow combined. One of Doo-Hee Kim’s inspiring <a href="https://100daysoffonts.com/">Google Fonts combinations</a>.</figcaption></figure>

### How Widespread Is Your Font?

Arial, Helvetica Neue, Verdana — these are still the three most-used typefaces on the web (at least if you take into account the top million websites). If you want to know how widespread a font is before you use it in your project, well, [Font Reach](https://www.fontreach.com/#) will tell you. The site scans the font stacks of the top million websites to rank them by popularity. You can also search for a specific font to see which websites use it. A nice tool no matter if you want to make a unique choice or plan to go with the current trend.</p>

## Web Font Loading And Performance

Web font loading has gone through a lot of iterations in the past: from data URIs to using scoped classes. The next iteration: Critical FOFT. The method builds on the Flash of Faux Text (FOFT) using a two stages loading process. Instead of loading the full Roman web font in the first stage, it loads a small subset of it (only upper and lower case characters, for example), and, thus, shrinks the first stage significantly. Zach Leatherman has done a comprehensive [write-up describing the technique in detail](https://www.zachleat.com/web/critical-webfonts/) and comparing its performance with other font loading techniques.

You have something to add to this collection? Feel free to share your favorite typography helpers in the comments section below.


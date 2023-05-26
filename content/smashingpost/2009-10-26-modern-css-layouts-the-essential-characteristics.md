---
title: 'Modern CSS Layouts: The Essential Characteristics'
slug: modern-css-layouts-the-essential-characteristics
image: null
date: 2009-10-26T14:41:53.000Z
author: zoe-mickley-gillenwater
description: >-
  Now is an exciting time to be creating **CSS layouts**. After years of what
  felt like the same old techniques for the same old browsers, we're finally
  seeing browsers implement CSS 3, HTML 5 and other technologies that give us
  cool new tools and tricks for our designs.

  But all of this change can be stressful, too. How do you keep up with all of
  the new techniques and make sure your Web pages look great on the increasing
  number of browsers and devices out there? First you'll learn the five
  essential characteristics of successful modern CSS websites. In the second
  part of this article, you'll learn about the techniques and tools that you
  need to achieve these characteristics.

  We won't talk about design trends and styles that characterize modern
  CSS-based layouts. These styles are always changing. Instead, we'll **focus on
  the broad underlying concepts that you need to know to create the most
  successful CSS layouts** using the latest techniques. For instance, separating
  content and presentation is still a fundamental concept of CSS Web pages. But
  other characteristics of modern CSS Web pages are new or more important than
  ever. A modern CSS-based website is: progressively enhanced, adaptive to
  diverse users, modular, efficient and typographically rich.
categories:
  - Coding
  - Layouts
  - CSS
  - Essentials
---
Now is an exciting time to be creating <strong>CSS layouts</strong>. After years of what felt like the same old techniques for the same old browsers, we're finally seeing browsers implement CSS 3, HTML 5 and other technologies that give us cool new tools and tricks for our designs.

But all of this change can be stressful, too. How do you keep up with all of the new techniques and make sure your Web pages look great on the increasing number of browsers and devices out there? In part 1 of this article, you'll learn the five essential characteristics of successful modern CSS websites. In part 2 of this article, you'll learn about the techniques and tools that you need to achieve these characteristics.

Be sure to check out the following articles:

*   [Modern CSS Layouts, Part 2: The Essential Techniques](https://www.smashingmagazine.com/2010/05/modern-css-layouts-part-2-the-essential-techniques/)
*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [Flexbox Is As Easy As Pie – Designing CSS Layouts](https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/)
*   [Mastering CSS Principles: A Comprehensive Guide](https://www.smashingmagazine.com/mastering-css-principles-comprehensive-reference-guide/)

We won't talk about design trends and styles that characterize modern CSS-based layouts. These styles are always changing. Instead, we'll <strong>focus on the broad underlying concepts that you need to know to create the most successful CSS layouts</strong> using the latest techniques. For instance, separating content and presentation is still a fundamental concept of CSS Web pages. But other characteristics of modern CSS Web pages are new or more important than ever. A modern CSS-based website is: progressively enhanced, adaptive to diverse users, modular, efficient and typographically rich.

{{% feature-panel %}}

*   Progressively enhanced,
*   Adaptive to diverse users,
*   Modular,
*   Efficient,
*   Typographically rich.</p>

## Progressive Enhancement

Progressive enhancement means creating a solid page with appropriate markup for content and adding advanced styling (and perhaps scripting) to the page for browsers that can handle it. It results in web pages that are usable by all browsers but that do not look identical in all browsers. Users of newer, more advanced browsers get to see more cool visual effects and nice usability enhancements.

The idea of allowing a design to look different in different browsers is not new. CSS gurus have been <a href="https://dowebsitesneedtolookexactlythesameineverybrowser.com/">preaching</a> this for years because font availability and rendering, color tone, pixel calculations and other technical factors have always varied between browsers and platforms. Most Web designers avoid “pixel perfection” and have accepted the idea of their designs looking slightly different in different browsers. But progressive enhancement, which has grown in popularity over the past few years, takes it a step further. Designs that are progressively enhanced may look more than slightly different in different browsers; they might look <em>very</em> different.

For example, the tweetCC website has a number of CSS 3 properties that add attractive visual touches, like drop-shadows behind text, multiple columns of text and different-colored background “images” (without there having to be actually different images). These effects are seen to various extents in different browsers, with old browsers like IE 6 looking the “plainest.” However, even in IE 6, the text is perfectly readable, and the design is perfectly usable.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51305b29-ffd7-4ed8-b56d-25325333713f/tweetcc-safari.jpg" alt="Screenshot" width="500" height="346" /><br>
<em>tweetCC in Safari.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef4fdd25-3cdd-48c2-b56e-cba66469b372/tweetcc-ie.jpg" alt="Screenshot" width="500" height="366" /><br>
<em>tweetCC in IE 6.</em>

In CSS 3-capable browsers like Safari (top), the tweetCC website shows a number of visual effects that you can't see in IE 6 (bottom).

These significant differences between browsers are perfectly okay, not only because that is the built-in nature of the Web, but because progressive enhancement brings the following benefits:

*   **More robust pages**.  Rather than use the graceful degradation method to create a fully functional page and then work backwards to make it function in less-capable browsers, you focus first on creating a solid “base” page that works everywhere.
*   **Happier users**.  You start building the page making sure the basic functionality and styling is the same for everyone. People with old browsers, mobile devices and assistive technology are happy because the pages are clean and reliable and work well. People with the latest and greatest browsers are happy because they get a rich, polished experience.
*   **Reduced development time**.  You don't have to spend hours trying to get everything to look perfect and identical in all browsers. Nor do you have to spend much time reverse-engineering your pages to work in older browsers after you have completed the fully functional and styled versions (as is the case with the graceful degradation method).
*   **Reduced maintenance time**.  If a new browser or new technology comes out, you can add new features to what you already have, without altering and possibly breaking your existing features. You have only one base version of the page or code to update, rather than multiple versions (which is the case with graceful degradation).
*   **More fun**.  It's just plain fun to be able to use cool and creative new techniques on your Web pages, and not have to wait years for old browsers to die off.

Learn more about progressive enhancement:

*   [Progressive Enhancement: What It Is, And How To Use It?](https://www.smashingmagazine.com/2009/04/22/progressive-enhancement-what-it-is-and-how-to-use-it/)
*   [Progressive Enhancement on Wikipedia](https://en.wikipedia.org/wiki/Progressive_enhancement)
*   [Progressive Enhancement: Paving the Way for Future Web Design](https://www.hesketh.com/publications/articles/progressive-enhancement-paving-the-way-for/)

## Adaptive to Diverse Users

Modern CSS-based Web pages have to accommodate the diverse range of browsers, devices, screen resolutions, font sizes, assistive technologies and other factors that users bring to the table. This concept is also not new but is growing in importance as Web users become increasingly diverse. For instance, a few years ago, you could count on almost all of your users having one of three screen resolutions. Now, users could be viewing your pages on 10-inch netbooks, 30-inch widescreen monitors or anything in between, not to mention tiny mobile devices.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d8b495e-f025-4533-b063-cb00efbb04c4/smartcolumnssample.gif" alt="Screenshot" width="520" height="300" /><br>
<em>In his article "Smart columns with CSS and jQuery" Soh Tanaka describes his techniques that adapts the layout depending on the current browser window size.</em>

Creating Web designs that work for all users in all scenarios will never possible. But the more users you can please, the better: for them, for your clients and for you. Successful CSS layouts now have to be more flexible and adaptable than ever before to the increasing variety of ways in which users browse the Web.

Consider factors such as these when creating CSS layouts:

*   **Browser**.  Is the design attractive and usable with the most current and popular browsers? Is it at least usable with old browsers?
*   **Platform**.  Does the design work on PC, Mac and Linux machines?
*   **Device**.  Does the design adapt to low-resolution mobile devices? How does it look on mobile devices that have full resolution (e.g. iPhones)?
*   **Screen resolution**.  Does the design stay together at multiple viewport (i.e. window) widths? Is it attractive and easy to read at different widths? If the design does adapt to different viewport widths, does it correct for extremely narrow or wide viewports (e.g. by using the `min-width` and `max-width` properties)?
*   **Font sizes**.  Does the design accommodate different default font sizes? Does the design hold together when the font size is changed on the fly? Is it attractive and easy to read at different font sizes?
*   **Color**.  Does the design make sense and is the content readable in black and white? Would it work if you are color blind or have poor vision or cannot detect color contrast?
*   **JavaScript presence**.  Does the page work without JavaScript?
*   **Image presence**.  Does the content make sense and is it readable without images (either background or foreground)?
*   **Assistive technology/disability** Does the page work well in screen readers? Does the page work well without a mouse?

This is not a comprehensive list; and even so, you would not be able to accommodate every one of these variations in your design. But the more you can account for, the more user-friendly, robust and successful your website will be.

See these resources on user diversity and Web page adaptability:

*   [Market Share by Net Applications](https://marketshare.hitslink.com/)
*   [Actual Browser Sizes](https://www.baekdal.com/reports/actual-browser-sizes/)
*   <span class="removed_link" title="https://www.smashingmagazine.com/2007/11/23/screen-resolutions-and-better-user-experience/">Screen Resolutions and Better User Experience</span>
*   [Fixed vs. Fluid vs. Elastic Layout: What's the Right One for You?](https://www.smashingmagazine.com/2009/06/02/fixed-vs-fluid-vs-elastic-layout-whats-the-right-one-for-you/)
*   [Mobile Web Design Trends for 2009](https://www.smashingmagazine.com/2009/01/13/mobile-web-design-trends-2009/)

## Modular

Modern websites are no longer collections of static pages. Pieces of content and design components are reused throughout a website and even shared between websites, as content management systems (CMS), RSS aggregation and user-generated content increase in popularity. Modern design components have to be able to adapt to all of the different places they will be used and the different types and amount of content they will contain.

<a href="https://wiki.github.com/stubbornella/oocss"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70fbffc7-b1af-43fb-b867-47a7aec0e1cc/oocss.jpg" alt="Screenshot" width="500" height="375" /></a><br>
<em><a href="https://wiki.github.com/stubbornella/oocss">Object Oriented CSS</a> is Nicole Sulivan's attempt to create a framework that would allow developers to write fast, maintainable, standards-based, modular front end code.</em>

Modular CSS, in a broad sense, is CSS that can be broken down into chunks that work independently to create design components that can themselves be reused independently. This might mean separating your style into multiple sheets, such as <em>layout.css</em>, <em>type.css</em>, and <em>color.css</em>. Or it might mean creating a collection of universal CSS classes for form layout that you can apply to any form on your website, rather than have to style each form individually. CMS', frameworks, layout grids and other tools all help you create more modular Web pages.

Modular CSS offers these benefits (depending on which techniques and tools you use):

*   **Smaller file sizes**.  When all of the content across your website is styled with only a handful of CSS classes, rather than an array of CSS IDs that only work on particular pieces of content on particular pages, your style sheets will have many fewer redundant lines of code.
*   **Reduced development time**.  Using frameworks, standard classes and other modular CSS tools keeps you from having to re-invent the wheel every time you start a new website. By using your own or other developers' tried and true CSS classes, you spend less time testing and tweaking in different browsers.
*   **Reduced maintenance time**.  When your style sheets include broad, reusable classes that work anywhere on your website, you don't have to come up with new styles when you add new content. Also, when your CSS is lean and well organized, you spend less time tracking down problems in your style sheets when browser bugs pop up.
*   **Easier maintenance for others**.  In addition to making maintenance less time-consuming for you, well-organized CSS and smartly named classes also make maintenance easier for developers who weren't involved in the initial development of the style sheets. They'll be able to find what they need and use it more easily. CMS' and frameworks also allow people who are not as familiar with your website to update it easily, without screwing anything up.
*   **More design flexibility**.  Frameworks and layout grids make it easy, for instance, to switch between different types of layout on different pages or to [plug in different types of content](https://24ways.org/2008/making-modular-layout-systems) on a single page.
*   **More consistent design**.  By reusing the same classes and avoiding location-specific styling, you ensure that all elements of the same type look the same throughout the website. CMS' and frameworks provide even more insurance against design inconsistency.

Learn more about modular CSS techniques:

*   [Object-Oriented CSS](https://www.stubbornella.org/content/2009/02/28/object-oriented-css-grids-on-github/)
*   [Making Modular Layout Systems](https://24ways.org/2008/making-modular-layout-systems)
*   <span class="removed_link" title="https://www.w3avenue.com/2009/04/29/definitive-list-of-css-frameworks-pick-your-style/">Definitive List of CSS Frameworks: Pick Your Style</span>

## Efficient

Modern CSS-based websites should be efficient in two ways:

*   Efficient for you to develop,
*   Efficient for the server and browser to display to users.

As Web developers, we can all agree that efficiency on the development side is a good thing. If you can save time while still producing high-quality work, then why wouldn't you adopt more efficient CSS development practices? But creating pages that perform efficiently for users is sometimes not given enough attention. Even though connection speeds are getting faster and faster, page load times are still very important to users. In fact, as connection speeds increase, users might expect all pages to load very quickly, so making sure your website can keep up is important. Shaving just a couple of seconds off the loading time can make a big difference.

We've already discussed how modular CSS reduces development and maintenance time and makes your workflow a lot faster and more efficient. A myriad of tools are out there to help you write CSS quickly, which we'll cover in part 2 of this article. You can also streamline your CSS development process by using many of the new effects offered by CSS 3, which cut down on your time spent creating graphics and coding usability enhancements.

Some CSS 3 techniques also improve performance and speed. For instance, traditional rounded-corner techniques require multiple images and DIVs for just one box. Using CSS 3 to create rounded corners requires no images, thus reducing the number of HTTP calls to the server and making the page load faster. No images also reduces the number of bytes the user has to download and speeds up page loading. CSS 3 rounded-corners also do not require multiple nested DIVs, which reduces page file size and speeds up page loading again. Simply switching to CSS 3 for rounded corners can give your website a tremendous performance boost, especially if you have many boxes with rounded corners on each page.

Writing clean CSS that takes advantage of shorthand properties, grouped selectors and other efficient syntax is of course just as important as ever for improving performance. Many of the more advanced tricks for making CSS-based pages load faster are also not new but are increasing in usage and importance. For instance, the <a href="https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/">CSS Sprites</a> technique, whereby a single file holds many small images that are each revealed using the CSS <code>background-position</code> property, was first described by <a href="https://www.alistapart.com/articles/sprites/">Dave Shea in 2004</a> but has been improved and added to a great deal since then. Many large enterprise websites now rely heavily on the technique to minimize HTTP requests. And it can improve efficiency for those of us working on smaller websites, too. CSS compression techniques are also increasingly common, and many automated tools make compressing and optimizing your CSS a breeze, as you'll also learn in part 2 of this article.

Learn more about CSS efficiency:

*   [7 Principles of Clean and Optimized CSS Code](https://www.smashingmagazine.com/2008/08/18/7-principles-of-clean-and-optimized-css-code/)
*   [Simplifying CSS Selectors](https://www.stevesouders.com/blog/2009/06/18/simplifying-css-selectors/)
*   [Best Practices for Speeding Up Your Website](https://developer.yahoo.com/performance/rules.html)
*   [The Mystery Of CSS Sprites: Techniques, Tools And Tutorials](https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/)
*   [35 CSS Lifesavers For Efficient Web Design](https://www.smashingmagazine.com/2009/06/25/35-css-lifesavers-for-efficient-web-design/)

## Rich Typography

Rich typography may seem out of place with the four concepts we have just covered. But we're not talking about any particular style of typography or fonts, but rather the broader concept of creating readable yet unique-looking text by applying tried and true typographic principles using the newest technologies. Typography is one of the most rapidly evolving areas of Web design right now. And boy, does it need to evolve! While Web designers have had few limits on what they could do graphically with their designs, their limits with typography have been glaring and frustrating.

Until recently, Web designers were limited to working with the fonts on their end users' machines. Image replacement tricks and clever technologies such as sIFR have opened new possibilities in the past few years, but none of these is terribly easy to work with. In the past year, we've finally made great strides in what is possible for type on the Web because of the growing support for CSS 3's <code>@font-face</code> property, as well as new easy-to-use technologies and services like <a href="https://cufon.shoqolate.com/generate/">Cufón</a> and <a href="https://blog.typekit.com/">Typekit</a>.

The <code>@font-face</code> rule allows you to link to a font on your server, called a “Web font,” just as you link to images. So you are no longer limited to working with the fonts that most people have installed on their machines. You can now take advantage of the beautiful, unique fonts that you have been dying to use.

@font-face in action: Teehanlax.com

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21ea8a57-6963-41ba-9591-9538080484df/fontface-teehanlax.gif)

Craigmod

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f52613fd-aa99-4894-8555-e73b6890f73f/fontface-craigmod.gif)](https://craigmod.com/journal/font-face/)

<a href="https://nicewebtype.com/fonts/museo-and-sans/">Nicewebtype</a>

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c05b34ca-7fe5-490a-baf4-c1c62542b3ef/fontface-nicewebtype-museo.gif)](https://nicewebtype.com/fonts/museo-and-sans/)

<em>The three screenshots above are all examples of what <code>@font-face</code> can do.</em>

The main problem with <code>@font-face</code>, aside from the ever-present issue of <a href="https://a.deveria.com/caniuse/#feat=fontface">browser compatibility</a>, is that most font licenses—even those of free fonts—do not allow you to serve the fonts over the Web. That's where <code>@font-face</code> services such as <a href="https://blog.typekit.com/">Typekit</a>, <a href="https://fontdeck.com/">Fontdeck</a> and <a href="https://www.kernest.com/">Kernest</a> are stepping in. They work with type foundries to license select fonts for Web design on a “rental” basis. These subscription-based services let you rent fonts for your website, giving you a much wider range of fonts to work with, while avoiding licensing issues.

<a href="https://forabeautifulweb.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f489b71-c211-4916-974a-da28e7d78d24/typekit-forabeautifulweb.jpg" alt="Screenshot" width="500" height="263" /></a><br>
<em><a href="https://forabeautifulweb.com/">For A Beautiful Web</a> uses the <a href="https://blog.typekit.com/">Typekit font embedding service</a> for the website name, introductory text and headings.</em>

<a href="https://ruleroftheinterwebs.blogspot.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d80f26c0-4ce5-4192-a74c-8d0138c817c4/kernest-ruleroftheinterwebs.gif" alt="Screenshot" width="500" height="268" /></a><br>
<em><a href="https://ruleroftheinterwebs.blogspot.com/">Ruler of the Interwebs</a> uses the <a href="https://www.kernest.com/">Kernest font embedding service</a> for the website name and headings.</em>

We still have a long way to go, but the new possibilities make typography more important to Web design than ever before. To make your design truly stand out, use these modern typographic techniques, which we'll cover in even greater detail in Part 2.

See these resources on current CSS typography techniques:

*   [Beautiful Fonts With @font-face](https://hacks.mozilla.org/2009/06/beautiful-fonts-with-font-face/)
*   Why Web Font Services Are the Future of Fonts on the Web
*   [The Direction Forward with Web Fonts](https://paulirish.com/2009/the-direction-forward-with-web-fonts/)
*   [Roundup of Font Embedding and Replacement Techniques](https://zomigi.com/blog/roundup-of-font-embedding-and-replacement-techniques/)

## Summary

We've looked at five characteristics of modern CSS websites:

*   Progressively enhanced,
*   Adaptive to diverse users,
*   Modular,
*   Efficient,
*   Typographically rich.

In part 2 of this article, coming soon, we'll go over the techniques and tools that will help you implement these important characteristics on your CSS-based Web pages.

{{< signature "al" >}}


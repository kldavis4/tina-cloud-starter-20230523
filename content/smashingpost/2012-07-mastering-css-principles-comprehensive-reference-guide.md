---
title: 'Mastering CSS Principles: A Comprehensive Guide'
slug: mastering-css-principles-comprehensive-reference-guide
image: null
date: 2012-07-02T12:29:21.000Z
author: vitaly-friedman
description: >-
  This overview features a hand-picked and organized selection of the most
  useful and popular Smashing Magazine’s articles related to CSS and published
  here over the years.
categories: []
---

This overview features a hand-picked and organized selection of the most useful and popular Smashing Magazine's articles related to CSS and published here over the years.

#### Quick Overview

*   [CSS Float Property](#a1)
*   [Negative Margins](#a2)
*   [Equal Height Column Layouts With Borders And Negative Margins In CSS](#a3)
*   [Z-Index CSS Property](#a4)
*   [CSS Specificity And Inheritance](#a5)
*   [!important CSS Declarations](#a6)
*   [Advanced CSS Selectors](#a7)
*   [Mastering CSS, Part 1: Styling Design Elements](#a8)
*   [Mastering CSS, Part 2: Advanced Techniques And Tools](#a9)
*   [The :before And :after Pseudo-Elements In CSS](#a10)
*   [CSS Font Stacks](#a11)
*   [Backgrounds In CSS](#a12)
*   [Designing CSS Buttons](#a13)
*   [The Future Of CSS: Embracing The Machine](#a14)
*   [The Guide To CSS Animation: Principles and Examples](#a15)
*   [Fixed vs. Fluid vs. Elastic Layout: What's The Right One For You?](#a16)
*   [Modern CSS Layouts: The Essential Characteristics](#a17)
*   [Modern CSS Layouts: The Essential Techniques](#a18)
*   [Styling Elements With Glyphs, Sprites And Pseudo-Elements](#a19)
*   [The Mystery Of CSS Sprites](#a20)
*   [CSS Sprites](#a21)
*   [CSS Sprites Revisited](#a22)
*   [CSS Differences In Internet Explorer 6, 7 & 8](#a23)
*   [Cross-Browser CSS Coding](#a24)
*   [Improving Code Readability With CSS Styleguides](#a25)
*   [Mastering CSS Coding: Getting Started](#a26)
*   [70 Expert Ideas For Better CSS Coding](#a27)
*   [An Introduction To Object Oriented CSS (OOCSS)](#a28)
*   [An Introduction To LESS, And Comparison To Sass](#a29)
*   [Writing CSS For Others](#a30)
*   [How To Set Up A Print Style Sheet](#a31)
*   [CSS Wishlist: New Ideas, Debates And Solutions](#a32)

### [The Mystery Of The CSS Float Property](https://www.smashingmagazine.com/2009/10/19/the-mystery-of-css-float-property/ "Permanent Link to The Mystery Of The CSS Float Property")

Years ago, when developers first started to make the transition to HTML layouts without tables, one **CSS** property that suddenly took on a very important role was the `float` property. The reason that the `float` property became so common was that, by default, block-level elements will not line up beside one another in a column-based format. Since columns are necessary in virtually every CSS layout, this property started to get used — and even overused — prolifically.

<figure><a href="https://www.smashingmagazine.com/2009/10/19/the-mystery-of-css-float-property/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5f2df07-a00c-4118-96cc-8826394b3bf8/float-fp.jpg" width="480" height="361" alt="No More Tables - Floats" /></a></figure>

The **CSS `float` property** allows a developer to incorporate table-like columns in an HTML layout without the use of tables. If it were not for the CSS `float` property, CSS layouts would not be possible except using absolute and relative positioning — which would be messy and would make the layout unmaintainable.

In this article, **we'll discuss exactly what the `float` property is and how it affects elements** in particular contexts. We'll also take a look at some of the differences that can occur in connection with this property in the most commonly-used browsers. Finally, we'll showcase a few practical uses for the CSS `float` property. This should provide a well-rounded and thorough discussion of this property and its impact on CSS development.

[Read more...](https://www.smashingmagazine.com/2009/10/19/the-mystery-of-css-float-property/)

### [The Definitive Guide To Using Negative Margins](https://www.smashingmagazine.com/2009/07/27/the-definitive-guide-to-using-negative-margins/ "Permanent Link to The Definitive Guide To Using Negative Margins")

Since the recommendation of CSS2 back in 1998, the use of tables has slowly faded into the background and into the history books. Because of this, CSS layouts have since then been synonymous with coding elegance.

<figure><a href="https://www.smashingmagazine.com/2009/07/27/the-definitive-guide-to-using-negative-margins/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbe79f7b-b5e0-4891-9322-aea13e2fe54e/margin-motion.gif" width="500" height="410" alt="Negative margins motion on static elements" /></a></figure>

Out of all the CSS concepts designers have ever used, an award probably needs to be given to the use of **Negative Margins** as being the most _least_ talked about method of positioning. It's like an online taboo  —  everyone's doing it, yet no one wants to talk about it.

[Read more...](https://www.smashingmagazine.com/2009/07/27/the-definitive-guide-to-using-negative-margins/)

### [Equal Height Column Layouts With Borders And Negative Margins In CSS](https://www.smashingmagazine.com/2010/11/08/equal-height-columns-using-borders-and-negative-margins-with-css/ "Permanent Link to Equal Height Column Layouts with Borders and Negative Margins in CSS")

_"What? Another "Equal Height Columns" article? Enough already!"_ If this is what you think, then think again because this solution is _different_. It does not rely on any of the usual tricks. It does not use images, nor extra markup, nor CSS3, nor pseudo-classes, nor Javascript, nor absolute positioning. All it uses is `border` and `negative margins`. Please note that this article will also demonstrate different construct techniques and will brush up on a few concepts.

<p><a title="Read full article" href="https://www.smashingmagazine.com/2010/11/08/equal-height-columns-using-borders-and-negative-margins-with-css/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a44ed70-d16b-4599-a5c6-67c0aba7dc59/2collayout.gif" alt="Two column layout" width="500" height="268" /></a></figure>

In this post we will build three layouts using CSS: a two column layout with no wrapper `div`, a two column layout with two vertical borders between the columns and a three column layout with a single wrapper. All layouts have coding examples and demos for your convenience.

[Read more...](https://www.smashingmagazine.com/2010/11/08/equal-height-columns-using-borders-and-negative-margins-with-css/)

### [The Z-Index CSS Property: A Comprehensive Look](https://www.smashingmagazine.com/2009/09/15/the-z-index-css-property-a-comprehensive-look/ "Permanent Link to The Z-Index CSS Property: A Comprehensive Look")

Most CSS properties are quite simple to deal with. Often, applying a CSS property to an element in your markup will have instant results — as soon as you refresh the page, the value set for the property takes effect, and you see the result immediately. Other CSS properties, however, are a little more complex and will only work under a given set of circumstances.

<figure><a href="https://www.smashingmagazine.com/2009/09/15/the-z-index-css-property-a-comprehensive-look/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74bec8ea-9624-4b65-837c-d032b500e9a7/24ways.jpg" alt="Usejquery.com's Unique Gallery" width="500" height="303" /></a></figure>

The `z-index` property belongs to the latter group. `z-index` has undoubtedly caused as much confusion and frustration as any other CSS property. Ironically, however, when `z-index` is fully understood, it is a very easy property to use, and offers **an effective method for overcoming many layout challenges.**

In this article, we'll explain exactly what `z-index` is, how it has been misunderstood, and we'll discuss some practical uses for it. We'll also describe some of the browser differences that can occur, particularly in previous versions of Internet Explorer and Firefox. This comprehensive look at `z-index` should provide developers with an excellent foundation to be able to use this property confidently and effectively.

[Read more...](https://www.smashingmagazine.com/2009/09/15/the-z-index-css-property-a-comprehensive-look/)

### [CSS Specificity And Inheritance](https://www.smashingmagazine.com/2010/04/07/css-specificity-and-inheritance/ "Permanent Link to CSS Specificity And Inheritance")

CSS' barrier to entry is extremely low, mainly due to the nature of its syntax. Being clear and easy to understand, the syntax makes sense even to the inexperienced Web designer. It's so simple, in fact, that you could style a simple CSS-based website within a few hours of learning it.

<figure><a href="https://www.smashingmagazine.com/2010/04/07/css-specificity-and-inheritance/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce864ef8-6f75-4bbf-8bcf-26b3ea3a6627/starwars.jpg" alt="CSS: Specificity Wars" width="500" height="300" loading="lazy" decoding="async" class="37633" /></a></figure>

But **this apparent simplicity is deceitful**. If after a few hours of work, your perfectly crafted website looks great in Safari, all hell might break loose if you haven't taken the necessary measures to make it work in Internet Explorer. In a panic, you add hacks and filters where only a few tweaks or a different approach might do. Knowing how to deal with these issues comes with experience, with trial and error and with failing massively and then learning the correct way.

Understanding a few often overlooked concepts is also important. The concepts may be hard to grasp and look boring at first, but understanding them and knowing how to take advantage of them is important.

[Read more...](https://www.smashingmagazine.com/2010/04/07/css-specificity-and-inheritance/)

### [!important CSS Declarations: How And When To Use Them](https://www.smashingmagazine.com/2010/11/02/the-important-css-declaration-how-and-when-to-use-it/ "Permanent Link to !important CSS Declarations: How and When to Use Them")

When the [CSS1 specification](https://www.w3.org/TR/REC-CSS1-961217) was drafted in the mid to late 90s, it introduced `!important` declarations that would help developers and users easily override normal specificity when making changes to their stylesheets. For the most part, `!important` declarations have remained the same, with only one change in CSS2.1 and nothing new added or altered in the CSS3 spec in connection with this unique declaration.

<figure><a href="https://www.smashingmagazine.com/2010/11/02/the-important-css-declaration-how-and-when-to-use-it/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ded14bd5-e033-48fd-88cd-89f6a7daed4c/css-not-important.gif" width="494" height="222" alt="Adding !important in Developer Tools" /></a></figure>

Let's take a look at **what exactly these kinds of declarations are all about**, and when, if ever, you should use them. But before we get into `!important` declarations and how exactly they work, let's give this discussion a bit of context. In the past, Smashing Magazine has covered [CSS specificity](https://www.smashingmagazine.com/2010/04/07/css-specificity-and-inheritance/) in-depth, so please take a look at that article if you want a detailed discussion on the CSS cascade and how specificity ties in.

[Read more...](https://www.smashingmagazine.com/2010/11/02/the-important-css-declaration-how-and-when-to-use-it/)

### [Taming Advanced CSS Selectors](https://www.smashingmagazine.com/2009/08/17/taming-advanced-css-selectors/ "Permanent Link to Taming Advanced CSS Selectors")

CSS is **one of the most powerful tools** that is available to web designers (if not the most powerful). With it we can completely transform the look of a website in just a couple of minutes, and without even having to touch the markup. But despite the fact that we are all well aware of its usefulness, CSS selectors are still not used to their full potential and we sometimes have the tendency to litter our HTML with excessive and unnecessary classes and ids, divs and spans.

<figure><a href="https://www.smashingmagazine.com/2009/08/17/taming-advanced-css-selectors/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efbd0baf-068f-489f-a282-4c0f71f4fb2d/firebug.jpg" width="535" height="256" /></a></figure>

The best way to avoid these plagues spreading in your markup and keep it clean and semantic, is by using more complex CSS selectors, ones that can target specific elements without the need of a class or an id, and by doing that **keep our code and our stylesheets flexible**.

[Read more...](https://www.smashingmagazine.com/2009/08/17/taming-advanced-css-selectors/)

### [Mastering CSS, Part 1: Styling Design Elements](https://www.smashingmagazine.com/2009/08/03/mastering-css-styling-design-elements/ "Permanent Link to Mastering CSS, Part 1: Styling Design Elements")

**CSS** is one of the most important building blocks of modern web design. Standards demand the use of CSS for formatting and styling pages, and with good reason. It's lighter-weight and capable of much more than older methods like tables.

<figure><a href="https://www.smashingmagazine.com/2009/08/03/mastering-css-styling-design-elements/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d635f71f-b503-4153-bbc0-2c251f0398da/66.jpg" width="480" height="300" alt=" Create an Image Rotator with Description (CSS/jQuery)" /></a></figure>

And CSS isn't nearly as tricky as some people tend to believe. Below are **fresh tips and techniques for creating and styling design elements with CSS**. They're a good place to start if you're new to CSS but are valuable even if you're a veteran designer. Not all the techniques are strictly CSS; some include integration with JavaScript or XHTML to extend the functionality of your site.

[Read more...](https://www.smashingmagazine.com/2009/08/03/mastering-css-styling-design-elements/)

### [Mastering CSS, Part 2: Advanced Techniques and Tools](https://www.smashingmagazine.com/2009/08/10/mastering-css-advanced-techniques-and-tools/ "Permanent Link to Mastering CSS, Part 2: Advanced Techniques and Tools")

**CSS** is one of the most basic building blocks of modern web design. It creates the structure and style that surrounds your content and is capable of making your site a joy to use or a pain in the neck. Mastering CSS is one of the most important things a web designer can do, and has really become an essential criteria for being a successful designer.

<figure><a href="https://www.smashingmagazine.com/2009/08/10/mastering-css-advanced-techniques-and-tools/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b941e9b3-c190-4ff1-9f2e-85f70d5a020e/steps2.gif" width="535" height="326" alt="Menu List with CSS" /></a></figure>

In [Part 1: Styling Design Elements](https://www.smashingmagazine.com/2009/08/03/mastering-css-styling-design-elements/) we covered the basics of web design with CSS. In Part 2 we're offering up some more advanced techniques and effects you can achieve with CSS. Everything from creating your own online apps (like calendars) to styling web pages for use with the iPhone to some basics of working with CSS3 is covered here.

[Read more...](https://www.smashingmagazine.com/2009/08/10/mastering-css-advanced-techniques-and-tools/)

### [Learning To Use The :before And :after Pseudo-Elements In CSS](https://www.smashingmagazine.com/2011/07/13/learning-to-use-the-before-and-after-pseudo-elements-in-css/ "Permanent Link to Learning To Use The :before And :after Pseudo-Elements In CSS")

If you've been keeping tabs on various Web design blogs, you've probably noticed that the `:before` and `:after` pseudo-elements have been getting quite a bit of attention in the front-end development scene — and for good reason. In particular, the experiments of one blogger — namely, London-based developer Nicolas Gallagher — have given pseudo-elements quite a bit of exposure of late.

<figure><a href="https://www.smashingmagazine.com/2011/07/13/learning-to-use-the-before-and-after-pseudo-elements-in-css/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1edde286-2f0d-4efa-a844-4973be86d135/styles-pseudo-elements.jpg" alt="screenshot" width="500" height="324" /></a></figure>

To complement this exposure (and take advantage of a growing trend), I've put together what I hope is a fairly comprehensive run-down of pseudo-elements. This article is aimed primarily at those of you who have seen some of the [cool things](https://nicolasgallagher.com/pure-css-gui-icons/) done with pseudo-elements but want to know what this CSS technique is all about before trying it yourself.

[Read more...](https://www.smashingmagazine.com/2011/07/13/learning-to-use-the-before-and-after-pseudo-elements-in-css/)

### [Guide To CSS Font Stacks: Techniques And Resources](https://www.smashingmagazine.com/2009/09/22/complete-guide-to-css-font-stacks/ "Permanent Link to Guide to CSS Font Stacks: Techniques and Resources")

**CSS Font stacks** are one of those things that elude a lot of designers. Many stick to the basic stacks Dreamweaver auto-recommends or go even more basic by just specifying a single web-safe font. But doing either of those things means you're missing out on some great typography options. Font stacks can make it possible to show at least some of your visitors your site's typography exactly the way you intend without showing everyone else a default font. Read on for more information on using and creating effective font stacks with CSS.

<figure><a href="https://www.smashingmagazine.com/2009/09/22/complete-guide-to-css-font-stacks/"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3bbbe23-420f-4b85-920d-f44a735a52e1/strikingwebsites1.jpg" height="354" width="480" /></a></figure>

There are a huge variety of font stacks recommended. It seems every designer has their own favorites, what they consider to be the "ultimate" font stack. While there is no definitive font stack out there, there are a few things to keep in mind when using or creating your own stacks.

First of all, make sure you **always include a generic font family at the end** of your font stacks. This way, if for some strange reason the person visiting your site has virtually no fonts installed, at least they won't end up looking at everything in Courier New. Second, there's a basic formula to creating a good font stack: 'Preferred Font', 'Next best thing', 'Something common and sorta close', 'Similar Web-safe', and 'Generic'. There's nothing wrong with having more than one font for any of those, but try to keep your font stack reasonably short (six to ten fonts is a pretty good maximum number).

[Read more...](https://www.smashingmagazine.com/2009/09/22/complete-guide-to-css-font-stacks/)

### [Backgrounds In CSS: Everything You Need To Know](https://www.smashingmagazine.com/2009/09/02/backgrounds-in-css-everything-you-need-to-know/ "Permanent Link to Backgrounds In CSS: Everything You Need To Know")

**Backgrounds** are a core part of CSS. They are one of the fundamentals that you simply need to know. In this article, we will cover the basics of using CSS backgrounds, including properties such as `background-attachment`. We'll show some common tricks that can be done with the background as well as what's in store for **backgrounds in CSS 3** (including four new background properties!).

<figure><a href="https://www.smashingmagazine.com/2009/09/02/backgrounds-in-css-everything-you-need-to-know/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebbeb757-92d2-4108-9bee-9f32d51209bd/css-background-position.jpg" width="406" height="548" alt="Screenshot" /></a></figure>

We have five main background properties to use in CSS 2\. They are as follows: background-color, background-image, background-position, background-repeat and background-attachment. These properties can all be merged into one **short-hand** property: `background`. One important thing to note is that the background accounts for the contents of the element, including the padding and border. It does not include an element's margin. This works as it should in Firefox, Safari and Opera, and now in IE8\. But in IE7 and IE6 the background does not include the border, as illustrated below.

[Read more...](https://www.smashingmagazine.com/2009/09/02/backgrounds-in-css-everything-you-need-to-know/)

### [Designing CSS Buttons: Techniques And Resources](https://www.smashingmagazine.com/2009/11/18/designing-css-buttons-techniques-and-resources/ "Permanent Link to Designing CSS Buttons: Techniques and Resources")

Buttons, whatever their purpose, are important design elements. They could be the end point of a Web form or a [call to action](https://www.smashingmagazine.com/2009/10/13/call-to-action-buttons-examples-and-best-practices/). Designers have many reasons to style buttons, including to make them more attractive and to enhance usability. One of the most important reasons, though, is that standard buttons can **easily be missed by users** because they often look similar to elements in their operating system. Here, we present you several techniques and tutorials to help you learn how to style buttons using CSS. We'll also address usability.

<figure><a href="https://www.smashingmagazine.com/?p=16087"><img alt="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91f7f9fb-d78e-410b-bbcb-9ed9292c233f/rounded-corners.png" width="500" height="190" /></a></figure>

Before we explain how to style buttons, let's clear up a common misconception: buttons are not links. The main purpose of a link is to navigate between pages and views, whereas buttons allow you to perform an action (such as submit a form).

[Read more...](https://www.smashingmagazine.com/2009/11/18/designing-css-buttons-techniques-and-resources/)

### [The Future Of CSS: Embracing The Machine](https://www.smashingmagazine.com/2011/11/07/the-future-of-css-embracing-the-machine/ "Permanent Link to The Future Of CSS: Embracing The Machine")

Designers hold CSS close to their hearts. It’s just code, but it is also what makes our carefully crafted designs come to life. Thoughtful CSS is CSS that respects our designs, that is handcrafted with precision. The common conception among Web designers is that a good style sheet is created by hand, each curly bracket meticulously placed, each vendor prefix typed in manually.

<figure><a href="https://www.smashingmagazine.com/2011/11/07/the-future-of-css-embracing-the-machine/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d22082f4-ea03-4680-9c2f-6f6a3c0557b2/02-passenger-train.jpg" alt="C. P. R. passenger train at Donald Station, BC, about 1887" loading="lazy" decoding="async" class="106193" /></a></figure>

But how does this tradition fit in a world where the websites and applications that we want to create are becoming increasingly complex?

[Read more...](https://www.smashingmagazine.com/2011/11/07/the-future-of-css-embracing-the-machine/)

### [The Guide To CSS Animation: Principles and Examples](https://www.smashingmagazine.com/2011/09/14/the-guide-to-css-animation-principles-and-examples/ "Permanent Link to The Guide To CSS Animation: Principles and Examples")

With **CSS animation** now supported in both Firefox and Webkit browsers, there is no better time to give it a try. Regardless of its technical form, whether traditional, computer-generated 3-D, Flash or CSS, animation always follows the same basic principles. In this article, we will take our first steps with CSS animation and consider the main guidelines for creating animation with CSS. We’ll be working through an example, building up the animation using the principles of traditional animation. Finally, we’ll see some real-world usages.

<figure><a href="https://www.smashingmagazine.com/2011/09/14/the-guide-to-css-animation-principles-and-examples/"><img title="Example illustration showing the different frames in traditional animation to make a bouncing ball" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ff5e581-ce80-4b23-b894-378c3d0da9f2/intro.jpg" alt="screenshot" /></a></figure>

[Read more...](https://www.smashingmagazine.com/2011/09/14/the-guide-to-css-animation-principles-and-examples/)

### [Fixed vs. Fluid vs. Elastic Layout: What's The Right One For You?](https://www.smashingmagazine.com/2009/06/02/fixed-vs-fluid-vs-elastic-layout-whats-the-right-one-for-you/ "Permanent Link to Fixed vs. Fluid vs. Elastic Layout: What's The Right One For You?")

The problem has boggled the minds of Web designers for years: fixed, fluid, elastic or a hybrid layout design? Each option has its benefits and disadvantages. But the final decision depends so much on usability that it is not one to be made lightly. So, with all the confusion, **is there a right decision?** By considering a few factors and properly setting up the final design, you can end up with a successful layout design that reaps all the benefits.

<figure><a href="https://www.smashingmagazine.com/2009/06/02/fixed-vs-fluid-vs-elastic-layout-whats-the-right-one-for-you/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9afc50bc-cec2-43fa-819a-a093b66bf603/fixed4.jpg" width="500" height="330" alt="Nine Lion Design" /></a></figure>

This article discusses the pros and cons of each type of layout. Either one can be used to make a successful website layout, as long as you keep usability in mind.

[Read more...](https://www.smashingmagazine.com/2009/06/02/fixed-vs-fluid-vs-elastic-layout-whats-the-right-one-for-you/)

### [Modern CSS Layouts: The Essential Characteristics](https://www.smashingmagazine.com/2009/10/26/modern-css-layouts-the-essential-characteristics/ "Permanent Link to Modern CSS Layouts: The Essential Characteristics")

Now is an exciting time to be creating **CSS layouts**. After years of what felt like the same old techniques for the same old browsers, we're finally seeing browsers implement CSS 3, HTML 5 and other technologies that give us cool new tools and tricks for our designs.

But all of this change can be stressful, too. How do you keep up with all of the new techniques and make sure your Web pages look great on the increasing number of browsers and devices out there? First you'll learn the five essential characteristics of successful modern CSS websites. In the second part of this article, you'll learn about the techniques and tools that you need to achieve these characteristics.

<figure><a href="https://www.smashingmagazine.com/2009/10/26/modern-css-layouts-the-essential-characteristics/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c05b34ca-7fe5-490a-baf4-c1c62542b3ef/fontface-nicewebtype-museo.gif" width="500" height="362" alt="Screenshot" /></a></figure>

We won't talk about design trends and styles that characterize modern CSS-based layouts. These styles are always changing. Instead, we'll **focus on the broad underlying concepts that you need to know to create the most successful CSS layouts** using the latest techniques. For instance, separating content and presentation is still a fundamental concept of CSS Web pages. But other characteristics of modern CSS Web pages are new or more important than ever. A modern CSS-based website is: progressively enhanced, adaptive to diverse users, modular, efficient and typographically rich.

[Read more...](https://www.smashingmagazine.com/2009/10/26/modern-css-layouts-the-essential-characteristics/)

### [Modern CSS Layouts, Part 2: The Essential Techniques](https://www.smashingmagazine.com/2010/05/06/modern-css-layouts-part-2-the-essential-techniques/ "Permanent Link to Modern CSS Layouts, Part 2: The Essential Techniques")

In [Modern CSS Layouts, Part 1: The Essential Characteristics](https://www.smashingmagazine.com/2009/10/26/modern-css-layouts-the-essential-characteristics/), you learned that modern, CSS-based web sites should be progressively enhanced, adaptive to diverse users, modular, efficient and typographically rich. Now that you know _what_ characterizes a modern CSS web site, _how_ do you build one? Here are dozens of essential techniques and tools to learn and use to achieve the characteristics of today's most successful CSS-based web pages.

<figure><a href="https://www.smashingmagazine.com/2010/05/06/modern-css-layouts-part-2-the-essential-techniques/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef6d988e-542b-4c0c-aa76-f1bcd8166c39/part2-grid.jpg" width="500" height="292" alt="Screenshot" /></a></figure>

Just as in the previous article, we're not going to be talking about design trends and styles; these styles are always changing. Instead, we're focusing on the specific techniques that you need to know to create modern CSS-based web pages of any style. For each technique or tool, we'll indicate which of the five characteristics it helps meet. To keep this shorter than an encyclopedia, we'll also just cover the basics of each technique, then point you to some useful, hand-picked resources to learn the full details.

[Read more...](https://www.smashingmagazine.com/2010/05/06/modern-css-layouts-part-2-the-essential-techniques/)

### [Styling Elements With Glyphs, Sprites And Pseudo-Elements](https://www.smashingmagazine.com/2011/03/19/styling-elements-with-glyphs-sprites-and-pseudo-elements/ "Permanent Link to Styling Elements With Glyphs, Sprites and Pseudo-Elements")

In 2002, Mark Newhouse published the article "[Taming Lists](https://www.alistapart.com/articles/taminglists/)", a very interesting piece in which he explained how to create custom list markers using pseudo-elements. Almost a decade later, Nicolas Gallagher came up with the technique [pseudo background-crop](https://nicolasgallagher.com/css-background-image-hacks/demo/crop.html "Emulating background-crop") which uses pseudo-elements with a sprite.

<figure><a href="https://www.smashingmagazine.com/2011/03/19/styling-elements-with-glyphs-sprites-and-pseudo-elements/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02aaa190-df5e-4b81-86b9-95708da9df16/figure-1.png" width="500" height="235" alt="Displaying icons in links and as custom list markers" /></a></figure>

Today, on the shoulders of giants, we'll try to push the envelope. We'll discuss how you can style elements with no extra markup and using a bidi-friendly [high-contrast proof CSS sprite](https://www.paciellogroup.com/blog/2010/01/high-contrast-proof-css-sprites/ "high contrast proof CSS sprites") technique (you'll find an example below). The technique will work in Internet Explorer 6/7 as well.

[Read more...](https://www.smashingmagazine.com/2011/03/19/styling-elements-with-glyphs-sprites-and-pseudo-elements/)

### [The Mystery Of CSS Sprites: Techniques, Tools And Tutorials](https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/ "Permanent Link to The Mystery Of CSS Sprites: Techniques, Tools And Tutorials")

**CSS Sprites** are not new. In fact, they are a rather well-established technique and have managed to become common practice in Web development. Of course, CSS sprites are not always necessary, but in some situation they can bring significant advantages and improvements – particularly if you want to reduce your server load. And if you haven't heard of CSS sprites before, now is probably a good time to learn what they are, how they work and what tools can help you create and use the technique in your projects.

<figure><a href="https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a9308ed-b43a-41a4-8397-13dac745c2db/sprites2.gif" width="401" height="195" alt="CSS Sprites Screenshot" /></a></figure>

The term "sprite" (similar to "spirit," "goblin," or "elf") has its origins in computer graphics, in which it described a graphic object blended with a 2-D or 3-D scene through graphics hardware. Because the complexity of video games has continually increased, there was a need for smart techniques that could deal with detailed graphic objects while keeping game-play flowing. One of the techniques developed saw sprites being plugged into a master grid (see the image below), then later pulled out as needed by code that mapped the position of each individual graphic and selectively painted it on the screen.

[Read more...](https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/)

### [CSS Sprites: Useful Technique Or Potential Nuisance?](https://www.smashingmagazine.com/2010/03/26/css-sprites-useful-technique-or-potential-nuisance/ "Permanent Link to CSS Sprites: Useful Technique, or Potential Nuisance?")

Ah, the ubiquitous CSS sprites — one of the few web design techniques that was able to bypass "trend" status almost instantly, planting itself firmly into the category of best practice CSS. Although it didn't really take off until well after A List Apart [explained and endorsed it](https://www.alistapart.com/articles/sprites/), it was discussed as a CSS solution as early as [July, 2003 by Petr StanÃ­cek](https://wellstyled.com/css-nopreload-rollovers.html).

<figure><a href="https://www.smashingmagazine.com/2010/03/26/css-sprites-useful-technique-or-potential-nuisance/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/384bf01a-70d5-42a4-ab22-59f50ff43187/firebug-http.jpg" alt="YSlow" width="500" height="290" /></a></figure>

Most web developers today have a fairly strong grasp of this technique, and there have been countless tutorials and articles written on it. In almost every one of those tutorials, the claim is made that designers and developers should be implementing CSS sprites in order **to minimize HTTP requests** and save valuable kilobytes. This technique has been taken so far that many sites, [including Amazon](https://g-ecx.images-amazon.com/images/G/01/gno/images/orangeBlue/navPackedSprites-US-15._V202471683_.png), now use mega sprites.

Is this much-discussed benefit really worthwhile? Are designers jumping on the CSS sprite bandwagon without a careful consideration of all the factors? In this article, I'm going to discuss some of the **pros and cons of using CSS sprites**, focusing particularly on the use of "mega" sprites, and why such use of sprites could in many cases be a waste of time.

[Read more...](https://www.smashingmagazine.com/2010/03/26/css-sprites-useful-technique-or-potential-nuisance/)

### [CSS Sprites Revisited](https://www.smashingmagazine.com/2012/04/11/css-sprites-revisited/ "Permanent Link to CSS Sprites Revisited")

I’m pretty confident that I won’t surprise anyone here by saying that CSS sprites have been around for quite a while now, rearing their somewhat controversial heads in the Web development sphere as early as 2003.

Still, the CSS sprite hasn’t truly found its way into the everyday toolkit of the common Web developer. While the theory behind CSS sprites is easy enough and its advantages are clear, they still prove to be too bothersome to implement, especially when time is short and deadlines are looming. Barriers exist to be breached, though, and we’re not going to let a couple of tiny bumps in the road spoil the greater perks of the CSS sprite.

<figure><a href="https://www.smashingmagazine.com/2012/04/11/css-sprites-revisited/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72e3088d-d434-4acc-9e03-f419b9bcd928/sprite-ref.jpg" alt="Example of a reference image." title="Example of a reference image." /></a></figure>

If you want more background information on best practices and practical use cases, definitely read “[The Mystery of CSS Sprites: Techniques, Tools and Resources](https://www.smashingmagazine.com/2009/04/27/the-mystery-of-CSS-sprites-techniques-tools-and-tutorials/).” If you’re the defensive type, I would recommend “[CSS Sprites: Useful Technique, or Potential Nuisance?](https://www.smashingmagazine.com/2010/03/26/CSS-sprites-useful-technique-or-potential-nuisance/),” which discusses possible caveats.

I won’t take a stance on the validity of CSS sprites. The aim of this article is to find out why people still find it difficult to use CSS sprites. Also, we’ll come up with a couple of substantial improvements to current techniques. So, start up Photoshop (or your CSS sprite tool of choice), put on your LESS and Sass hats, and brush up your CSS pseudo-element skills, because we’ll be mixing and matching our way to easier CSS sprite implementation.

[Read more...](https://www.smashingmagazine.com/2012/04/11/css-sprites-revisited/)

### [CSS Differences In Internet Explorer 6, 7 and 8](https://www.smashingmagazine.com/2009/10/14/css-differences-in-internet-explorer-6-7-and-8/ "Permanent Link to CSS Differences In Internet Explorer 6, 7 and 8")

One of the most bizarre statistical facts in relation to browser use has to be the virtual widespread numbers that currently exist in the use of **Internet Explorer** versions 6, 7 and 8\. As of this writing, Internet Explorer holds about a 65% market share combined across all their currently used browsers. In the web development community, this number is much lower, showing about a 40% share.

<figure><a href="https://www.smashingmagazine.com/2009/10/14/css-differences-in-internet-explorer-6-7-and-8/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e4d9b44-1c32-4f35-aeb7-53883dc973c6/ie.jpg" width="500" height="441" alt="Screenshot" /></a></figure>

The interesting part of those statistics is that the numbers across IE6, IE7, and IE8 are very close, preventing a single Microsoft browser from dominating browser stats — contrary to what has been the trend in the past. Due to these unfortunate statistics, it is imperative that developers do thorough testing in all currently-used Internet Explorer browsers when working on websites for clients, and on personal projects that target a broader audience.

This article will attempt to provide an **exhaustive, easy-to-use reference for developers desiring to know the differences in CSS support for IE6, IE7 and IE8**.

[Read more...](https://www.smashingmagazine.com/2009/10/14/css-differences-in-internet-explorer-6-7-and-8/)

### [The Principles Of Cross-Browser CSS Coding](https://www.smashingmagazine.com/2010/06/07/the-principles-of-cross-browser-css-coding/ "Permanent Link to The Principles Of Cross-Browser CSS Coding")

It is arguable that there is no goal in web design more satisfying than getting a beautiful and intuitive design to look exactly the same in every currently-used browser. Unfortunately, that goal is generally agreed to be almost impossible to attain. Some have even [gone on record](https://dowebsitesneedtolookexactlythesameineverybrowser.com/) as stating that perfect, cross-browser compatibility is not necessary.

<figure><a href="https://www.smashingmagazine.com/2010/06/07/the-principles-of-cross-browser-css-coding/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66bb043c-03eb-4338-835a-36b07f186997/browsers-css2.jpg" alt="Cross-Browser CSS" width="450" height="450" /></a></figure>

While I agree that creating a consistent experience for every user in every browser (putting aside mobile platforms for the moment) is never going to happen for every project, I believe **a near-exact cross-browser experience is attainable** in many cases. As developers, our goal should not just be to get it working in every browser; our goal should be to get it working in every browser with a minimal amount of code, allowing future website maintenance to run smoothly.

In this article, I'll be describing what I believe are some of **the most important CSS principles and tips** that can help both new and experienced front-end developers achieve as close to a consistent cross-browser experience as possible, with as little CSS code as possible.

[Read more...](https://www.smashingmagazine.com/2010/06/07/the-principles-of-cross-browser-css-coding/)

### [Improving Code Readability With CSS Styleguides](https://www.smashingmagazine.com/2008/05/02/improving-code-readability-with-css-styleguides/ "Permanent Link to Improving Code Readability With CSS Styleguides")

Once your latest project is finished, you are very likely to forget the structure of the project's layout, with all its numerous classes, color schemes and type setting. To understand your code years after you've written it you need to make use of sensible code structuring. The latter can dramatically reduce complexity, improve code management and consequently simplify maintainability. However, how can you achieve **sensible structuring**? Well, there are a number of options. For instance, you can make use of comments — after all, there is always some area for useful hints, notes and, well, comments you can use afterwards, after the project has been deployed.

<figure><a href="https://www.smashingmagazine.com/2008/05/02/improving-code-readability-with-css-styleguides/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91341423-5a76-457e-8209-fa87e2842434/styleguide.png" width="498" height="325" alt="CSS Styleguides" /></a></figure>

Indeed, developers came up with quite creative ways to use comments and text formatting to improve the maintainability of CSS-code. Such creative ways are usually combined into _CSS styleguides_ — pieces of CSS-code which are supposed to provide developers with useful insights into the structure of the code and background information related to it.

This article presents **5 coding techniques which can dramatically improve management and simplify maintainability of your code**. You can apply them to CSS, but also to any other stylesheet or programming language you are using. You can browse through the references listed under the article — they containt further information about how you can achieve a well-organized and well-structured code.

[Read more...](https://www.smashingmagazine.com/2008/05/02/improving-code-readability-with-css-styleguides/)

### [Mastering CSS Coding: Getting Started](https://www.smashingmagazine.com/2009/10/05/mastering-css-coding-getting-started/ "Permanent Link to Mastering CSS Coding: Getting Started")

**CSS** has become the standard for building websites in today's industry. Whether you are a hardcore developer or designer, you should be familiar with it. CSS is the bridge between programming and design, and any Web professional must have some general knowledge of it. If you are getting your feet wet with CSS, this is the perfect time to fire up your favorite text editor and follow along in this tutorial as we cover the most common and practical uses of CSS.

<figure><a href="https://www.smashingmagazine.com/2009/10/05/mastering-css-coding-getting-started/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fac5bc9a-a572-437d-ab7b-0cbc0298f340/upd3-b.gif" alt="Absolute Position" /></a></figure>

We'll start with what you could call **the fundamental properties and capabilities of CSS**, ones that we commonly use to build CSS-based websites: Padding vs. margin, Floats, Center alignment, Ordered vs. unordered lists, Styling headings, Overflow and Position. Once you are comfortable with the basics, we will kick it up a notch with some neat tricks to build your CSS website from scratch and make some enhancements to it: Background images, Image enhancement, PSD to XHTML conversion.

[Read more...](https://www.smashingmagazine.com/2009/10/05/mastering-css-coding-getting-started/)

### [70 Expert Ideas For Better CSS Coding](https://www.smashingmagazine.com/2007/05/10/70-expert-ideas-for-better-css-coding/ "Permanent Link to 70 Expert Ideas For Better CSS Coding")

**CSS isn't always easy to deal with.** Depending on your skills and your experience, CSS coding can sometimes become a nightmare, particularly if you aren't sure which selectors are actually being applied to document elements. An easy way to minimize the complexity of the code is as useful as not-so-well-known CSS attributes and properties you can use to create a semantically correct markup.

We've taken a close look at some of the **most interesting and useful CSS tricks, tips, ideas, methods, techniques and coding solutions** and listed them below. We also included some basic techniques you can probably use in every project you are developing, but which are hard to find once you need them.

And what has come out of it is an overview of **over 70 expert tips, which can improve your efficiency of CSS coding**. You might be willing to check out the list of references and related articles in the end of this post.

We'd like to **express sincere thank to all designers** who shared their ideas, techniques, methods, knowledge and experience with their readers. Thank you, we, coders, designers, developers, information architects - you name it - really appreciate it.

[Read more...](https://www.smashingmagazine.com/2007/05/10/70-expert-ideas-for-better-css-coding/)

### [An Introduction To Object Oriented CSS (OOCSS)](https://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/ "Permanent Link to An Introduction To Object Oriented CSS (OOCSS)")

Have you ever heard the phrase “Content is King”? Being a Web developer, and therefore having a job that’s often linked to content creation, it’s likely you have. It’s a fairly overused but true statement about what draws visitors to a site.

From a Web developer’s perspective, however, some may argue that [speed is king](https://www.stevesouders.com/blog/2009/10/06/business-impact-of-high-performance/). More and more, I’m starting to favour that stance. In recent years many experienced front-end engineers have [offered their suggestions](https://www.stevesouders.com/blog/) on how we can improve the user experience by means of some performance [best](https://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) [practices](https://www.amazon.com/Even-Faster-Web-Sites-Performance/dp/0596522304/).

<figure><a href="https://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b58f9ca8-f975-4a2d-85d4-0497e395c21c/oocss-splash1.jpg" alt="OOCSS" /></a></figure>

Unfortunately, CSS seems to get somewhat overlooked in this area while many developers (for good reason) focus largely on JavaScript performance and [other areas](https://developer.yahoo.com/performance/rules.html).

In this post, I’ll deal with this often overlooked area by introducing you to the concept of **object oriented CSS** and how it can help improve both the performance and maintainability of your Web pages.

[Read more...](https://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)

### [An Introduction To LESS, And Comparison To Sass](https://www.smashingmagazine.com/2011/09/09/an-introduction-to-less-and-comparison-to-sass/ "Permanent Link to An Introduction To LESS, And Comparison To Sass")

I’ve been using [LESS](https://lesscss.org/ "LESS « The Dynamic Stylesheet language") religiously ever since I stumbled upon it months ago. CSS was never really a problem for me, in and of itself, but I was intrigued by the idea of using variables to create something along the lines of a color palette for my websites and themes. Having a color palette with a fixed number of options to choose from helps prevent me from going color crazy and deviating from a chosen style.

<figure><a href="https://www.smashingmagazine.com/2011/09/09/an-introduction-to-less-and-comparison-to-sass/"><img loading="lazy" decoding="async" class="106038" title="less-sass" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ce8bff6-bb89-4eb8-9dac-992835184fc4/less-sass1.jpg" alt="LESS and SASS" /></a></figure>

[Read more...](https://www.smashingmagazine.com/2011/09/09/an-introduction-to-less-and-comparison-to-sass/)

### <a title="Permanent Link to Writing CSS For Others" rel="bookmark" href="">Writing CSS For Others</a>

I think a lot of us CSS authors are doing it wrong. We are selfish by nature; we get into our little bubbles, writing CSS (as amazing as it may be) with only ourselves in mind. How many times have you inherited a CSS file that’s made you say “WTF” at least a dozen times?

<figure><a href="https://www.flickr.com/photos/tocaboca/5630744267/in/photostream/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af0dead2-40ac-4e4f-acba-c7d32ea9668d/labyrinth-comic.jpg" alt="Labyrinth Comic" /></a></figure>

HTML has a standard format and syntax that everyone understands. For years, programmers have widely agreed on standards for their respective languages. CSS doesn’t seem to be there yet: everyone has their own favorite format, their own preference between single-line and multi-line, their own ideas on organization, and so on.

[Read more...](https://www.smashingmagazine.com/2011/08/26/writing-css-for-others/)

### [How To Set Up A Print Style Sheet](https://www.smashingmagazine.com/2011/11/24/how-to-set-up-a-print-style-sheet/ "Permanent Link to How To Set Up A Print Style Sheet")

In a time when everyone seems to have a tablet, which makes it possible to consume everything digitally, and the only real paper we use is bathroom tissue, it might seem odd to write about the long-forgotten habit of printing a Web page. Nevertheless, as odd as it might seem to visionaries and tablet manufacturers, we’re still far from the reality of a paperless world.

In fact, tons of paper float out of printers worldwide every day, because not everyone has a tablet yet and a computer isn’t always in reach. Moreover, many of us feel that written text is just better consumed offline. Because I love to cook, sometimes I print recipes at home, or emails and screenshots at work, even though I do so as rarely as possible out of consideration for the environment.

<figure><a href="https://www.smashingmagazine.com/2011/11/24/how-to-set-up-a-print-style-sheet/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/098e587f-bb2f-4603-8c9c-2c669402c465/1.jpg" alt="screenshot"></a></figure>

Print style sheets are useful and sometimes even necessary. Some readers might want to store your information locally as a well-formatted PDF to refer to the information later on, when they don’t have an Internet connection. However, [print styles are often forgotten](https://evolt.org/ResponsiveWebAndPrint) in the age of responsive Web design. The good news is that a print style sheet is actually very easy to craft: you can follow a couple of simple CSS techniques to create a good experience for readers and show them that you’ve gone the extra mile to deliver just a slightly better user experience. So, how do we start?

[Read more...](https://www.smashingmagazine.com/2011/11/24/how-to-set-up-a-print-style-sheet/)

### [CSS Wishlist: New Ideas, Debates And Solutions](https://www.smashingmagazine.com/2009/09/10/css-wishlist-new-ideas-debates-and-solutions/ "Permanent Link to CSS Wishlist: New Ideas, Debates and Solutions")

The future of CSS is arriving fast, and many tools, languages, and solutions have been developed that make CSS a job not just for Web designers but developers, too. In many ways, the job could become more complex and confusing, but in many other ways, the new changes will provide more opportunity and better technology for the future of the Web.

<figure><a href="https://www.smashingmagazine.com/2009/09/10/css-wishlist-new-ideas-debates-and-solutions/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f8c0247-e8ea-4c6e-8863-711afb2fdf42/lesscss.jpg" width="500" height="359" alt="Less CSS" /></a></figure>

CSS will get a number of new changes. Among them are **alternative syntaxes, CSS programming concepts** and the ability to allow more common design techniques without using images. In this article, we'll go over some current solutions, what we'd like to see in the future and the pros and cons of them all.

[Read more...](https://www.smashingmagazine.com/2009/09/10/css-wishlist-new-ideas-debates-and-solutions/)
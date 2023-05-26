---
title: 'Start Using CSS3 Today: Techniques and Tutorials'
slug: start-using-css3-today-techniques-and-tutorials
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e58ab639-5820-42a6-82b7-f07802a99a48/experiment.jpg
date: 2010-06-17T11:36:13.000Z
author: vitaly-friedman
description: >-
  We have been publishing articles about CSS3 for a while now, and we keep receiving angry e-mails from some developers who complain that it doesn't make sense to use CSS3 today. Yes, Internet Explorer doesn't support most CSS3 properties. And yes, CSS3 vendor prefixes are bad for maintainability (and this is why we recommend extracting vendor prefixes in a separate CSS3 file).
categories:
  - Coding
  - CSS
  - Tutorials
  - Techniques
  - Resources
---
But it's OK to accept that Web is a dynamic medium, and it's OK to create rich, interactive, beautiful designs for those who are already using a modern browser or will be using one soon. It just doesn't make sense to keep looking back, beiDang afraid of looking forward and therefore avoid experimenting and learning about new CSS3 properties today. And this is why we keep publishing articles about CSS3.

In this post we present an **extensive round-up of CSS3 techniques, tools and resources** that will help you learn how to use CSS3 in your designs right away. We have grouped most useful articles by the corresponding properties, described what browsers support what properties, presented alternative JavaScript-based approaches and workarounds for Internet Explorer and added a couple of links to useful CSS3 generators and tools in the end of the post.

You may be interested in the following related articles:

*   [50 Brilliant CSS3/JavaScript Coding Techniques](https://www.smashingmagazine.com/2010/02/01/50-brilliant-css3-javascript-coding-techniques/)  
    In this post we present 50 useful and powerful CSS3/jQuery-techniques that can strongly improve user experience, improve designer’s workflow and replace dirty old workarounds that we used in Internet Explorer 6 and Co.
*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/15/take-your-design-to-the-next-level-with-css3/)  
    This article covers the essential of what you need to know about CSS3 with examples and useful links.
*   [CSS3 Solutions for Internet Explorer](https://www.smashingmagazine.com/2010/04/28/css3-solutions-for-internet-explorer/)  
    This articles shows a number of options that developers can consider for those circumstances where support for a CSS3 feature is required for all versions of Internet Explorer (IE6, IE7, & IE8 — all of which are still currently in significant use).

{{% feature-panel %}}

## What's Possible With CSS3?

Let's start with a review of some truly remarkable design techniques and experiments that show what can be done with a bit of coding, patience and creativity by using simple CSS3 properties.

[Pure CSS3 Page Flip Effect](https://www.romancortes.com/blog/pure-css3-page-flip-effect/)  
By using CSS3 gradients, transitions, 2d transforms and clipping, Roman Cortes achieved this pure CSS3 page flipping effect (no JavaScript is used). However, it works in Webkit browsers only (Safari and Chrome).

[![ Pure CSS3 Page Flip Effect](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97006f6d-9cbc-4cda-93ce-2e07b50b2c10/css3-168.jpg)](https://www.romancortes.com/blog/pure-css3-page-flip-effect/)

[Create a Vibrant Digital Poster Design with CSS3](https://line25.com/tutorials/create-a-vibrant-digital-poster-design-with-css3)  
CSS has come a long way in recent years, and with new browser support for a hand full of CSS3 properties we can begin to replicate design styles directly in the browser that beforehand were recently only possible in our design applications. Follow this walkthrough of the making of Circlicious, a vibrant and abstract digital poster design made purely of HTML and CSS.

[![How To Create Depth And Nice 3D Ribbons Only Using CSS3](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffb416a5-5baf-4985-a18c-498de4c0ccfa/css3-22.jpg)](https://line25.com/tutorials/create-a-vibrant-digital-poster-design-with-css3)

CSS3 Leopard-style Stacks  
Pure CSS3 (and experimental CSS). No JavaScript. An experiment by Gordon Brander.

![CSS3 Leopard-style Stacks](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed0a2cc3-8d0d-4f89-b6b5-06f1fc1651e5/css3-15.jpg)

[Wicked CSS3 3D Bar Chart](https://www.marcofolio.net/css/wicked_css3_3d_bar_chart.html)  
An attempt to create a 3D bar chart using CSS3\. This example only works in the latest versions of Firefox, Chrome, Safari and Opera.

[![Wicked CSS3 3d bar chart](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/471866e6-bad3-4f7c-a8b8-5d508856ae54/css3-techniques-16.jpg)](https://www.marcofolio.net/css/wicked_css3_3d_bar_chart.html)

[Selectable Headlines with Color Transition (CSS3)](https://trentwalton.com/2010/03/24/css3-background-clip-text/)  
A CSS3 color transition applied to a selectable text with CSS3\. Works only in Safari and Google Chrome.

[![Wicked CSS3 Color Transition](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23d17487-8fa2-4a30-9691-ad787882e624/css3-techniques-24.jpg)](https://trentwalton.com/2010/03/24/css3-background-clip-text/)

[Our Solar System in CSS3](https://neography.com/journal/our-solar-system-in-css3/)  
This is an attempt to recreate our solar system using CSS3 features such as border-radius, trans forms and animations. The result is surprising and quite interesting.

[![Our Solar System in CSS3  ](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b831729d-457b-4b72-85b0-81d9238a85ef/css3-techniques-14.jpg)](https://neography.com/journal/our-solar-system-in-css3/)

[Fun With CSS Gradients](https://www.martinilab.com/blog/104/fun-with-webkit-css-gradients/)  
This similar looking display to that of the iPhone album display uses a radial gradient (opposed to a linear) as the background for the track names. The overall effect is a dim light. The odd numbered tracks also use a gradient to take advantage of -webkit-gradient’s support of alpha values.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0eac32f5-9ca7-462c-8a83-2557e601015b/css3-techniques-36.jpg)](https://www.martinilab.com/blog/104/fun-with-webkit-css-gradients/)

[CSS3 Bookshelf](https://www.steveworkman.com/web-design/css3-web-design/2010/css3-bookshelf/)  
A very interesting idea that doesn't look very nice because of rotation rendering, but is worth experimenting nevertheless.

[![CSS3 Bookshelf](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c122728-3fba-49bf-ace3-4ee02477179b/css3-techniques-02.jpg)](https://www.steveworkman.com/web-design/css3-web-design/2010/css3-bookshelf/)

   [Pure CSS Twitter Fail Whale](https://www.subcide.com/articles/pure-css-twitter-fail-whale/)  
Curves are done using various uneven border-radius properties, stranger angles (such as the strings) are masked using containers with overflow: hidden; set on them.

[![Pure CSS Twitter Fail Whale](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e06a678-caf5-42c9-b554-c4b4c0b82abc/css3-techniques-10.jpg)](https://www.subcide.com/articles/pure-css-twitter-fail-whale/)

[CSS World Clocks](https://lensco.be/2010/04/04/css-world-clocks/)  
Another interesting experiment that uses CSS3 and a bit of PHP to create an interactive clock.

[![ CSS World Clocks](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/101ae2a7-80ad-49fa-9cec-db409d3e6fe4/css3-117.jpg)](https://lensco.be/2010/04/04/css-world-clocks/)

[3D Text Tower](https://css-tricks.com/3d-text-tower/)  
What happens if you lay a couple of text shadows over and over again? Interesting hover-effect.

[![3D Text Tower](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51095cbd-e7d2-46b5-9690-7f3c6f7a30ab/css3-techniques-17.jpg)](https://css-tricks.com/3d-text-tower/)

Creating a Realistic Looking Button with CSS3  
"I had previously created the Cadmus "post" button in Photoshop and it was essentially three images for the different states. I wanted to use this style for all our buttons, but doing it with single images is not a good idea. So I set about creating the same style of the buttons with CSS3."

![Creating a Realistic Looking Button with CSS3](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3b371e4-c5c7-4eae-b616-ef62ec327845/css3-03.jpg)

CSS3 Spotlight  
Turn on the light! Works with Webkit and Firefox.

![CSS3 Spotlight](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ed97e26-dab1-4bde-a387-dbf209ea3632/css3-techniques-15.jpg)

Pure CSS3 Animated AT-AT Walker from Star Wars  
In this article you;kk walk-through the process of creating a CSS3 animation of an AT-AT Walker from The Empire Strikes Back. The author starts off by reviewing some CSS3 properties that made this animation possible. Then, he follows up with a list of the sections required to construct the AT-AT and the CSS3 code to move each section.

![Pure CSS3 Animated AT-AT Walker from Star Wars  ](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b197081-bda7-466e-ae4f-63e9d28d9a18/css3-101.jpg)

Pure CSS Icons  
An experiment by Zander Martineau. with a large scoop of border-radius, Zander created various 'common' icons that could be used in your web apps.

![ Pure CSS Icons](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f182c9d0-3880-46f7-ad4d-aada9816fc15/css3-techniques-01.jpg)

     [Create a Content Slider Using Pure CSS](https://www.nealgrosskopf.com/tech/thread.php?pid=45)  
The idea was to create a working example without the aid of JavaScript, using layers in CSS and using CSS3 transitions to give the slider the necessary animation.

[![Create a JQuery Content Slider Using Pure CSS](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b917384-bdff-48fa-90f6-6ac052542e40/css3-techniques-03.jpg)](https://www.nealgrosskopf.com/tech/thread.php?pid=45)

      [Sexy Tooltips with Just CSS](https://sixrevisions.com/css/css-only-tooltips/)  
While many innovative solutions exist using CSS and JavaScript (with and without JavaScript frameworks like jQuery), it's sometimes useful to look towards new technologies to examine the impact they may have on our current techniques. This tutorial looks at how using the evolving CSS standard can enhance some lovely cross-browser tooltips.

[![Sexy Tooltips with Just CSS](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9413856-469d-4dd8-8320-42ebcdd43d26/08-04-five-tooltips.png)](https://sixrevisions.com/css/css-only-tooltips/)

[Creating a Polaroid photo viewer with CSS3 and jQuery](https://www.marcofolio.net/webdesign/creating_a_polaroid_photo_viewer_with_css3_and_jquery.html)  
This example is making use of CSS3 and jQuery, just to show the effect when combining two powerful techniques. The CSS3 is injected by jQuery, keeping the CSS file clean.

[![Creating a Polaroid photo viewer with CSS3 and jQuery](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1257e7ab-85de-48ae-a845-84e7fc65da75/css3-152.jpg)](https://www.marcofolio.net/webdesign/creating_a_polaroid_photo_viewer_with_css3_and_jquery.html)

   [Animated Photoshop selection using CSS3](https://matthewjamestaylor.com/blog/animated-photoshop-selection-on-a-web-page#)  
When part of an image is selected in Photoshop, the area is highlighted by an animated dashed line. Matthew James Taylor figured out a way to get exactly the same effect using CSS3.

[![Animated Photoshop selection using CSS3](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a1f5de5-0965-4b85-8b3e-3c0d8d6e8ba7/css3-techniques-12.jpg)](https://matthewjamestaylor.com/blog/animated-photoshop-selection-on-a-web-page#)

[Sexy Image Hover Effects using CSS3](https://www.nikesh.me/blog/2010/05/sexy-image-hover-effects-using-css3/)  
This post shows how to create a sexy CSS effect on image hover.

[![Sexy Image Hover Effects using CSS3 ](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06099d5f-d6f5-473c-aebc-45e95b35ede9/css3-160.jpg)](https://www.nikesh.me/blog/2010/05/sexy-image-hover-effects-using-css3/)

   [CSS3 Dropdown Menu](https://www.webdesignerwall.com/tutorials/css3-dropdown-menu/)  
A multi-level dropdown menu that was created using `border-radius`, `box-shadow`, and `text-shadow`. It renders perfect on Firefox, Safari and Chrome. The dropdown also works on non-CSS3 compatible browsers such as IE7+, but the rounded corners and shadow will not be rendered.

[![CSS3 Dropdown Menu](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d187abb5-6246-47ec-9257-30bfdcb15912/css-gradient-dropdown-menu.gif)](https://www.webdesignerwall.com/tutorials/css3-dropdown-menu/)

[Middle Box Links](https://css-tricks.com/middle-box-links/)  
What we have here is some boxes of content. The goal is that when you mouse over them, they darken and a link appears in the exact center of them.

[![Middle Box Links ](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ed6c5b8-eac1-4345-a5b8-fcee07d1f8d2/css3-221.jpg)](https://css-tricks.com/middle-box-links/)

[Contextual Slideout Tips With jQuery and CSS3](https://tutorialzine.com/2010/04/slideout-context-tips-jquery-css3/)  
By now, you've probably heard about Adobe's new CS5 software pack. Also, you've probably seen their product pages, where they present the new features of the suite. Apart from the great design, they've also implemented an interesting solution for showcasing the new features their products are capable of – using contextual slideout tips.

[![Contextual Slideout Tips With jQuery and CSS3](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce8fd85a-6c8e-446a-816b-1aa3419703cb/css3-134.jpg)](https://tutorialzine.com/2010/04/slideout-context-tips-jquery-css3/)

[Beautiful UI styling with CSS3 text-shadow, box-shadow, and border-radius](https://dev.opera.com/articles/view/beautiful-ui-styling-with-css3-text-shadow-box-shadow-and-border-radius/)  
This article takes things further, showing how to use the properties to create beautiful UI elements without the use of any images, JavaScript or Flash. This last line highlights the real beauty of CSS3 — many of its features are designed to save you time otherwise spent creating and updating graphics in Photoshop. It makes techniques such as drop shadows and animated UI elements accessible to web developers and designers without scripting smarts or mad Photoshop skills.

[![Beautiful UI styling with CSS3 text-shadow, box-shadow, and border-radius ](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ea3c340-aaa0-4864-aa83-d7a3736d6ea6/css3-105.jpg)](https://dev.opera.com/articles/view/beautiful-ui-styling-with-css3-text-shadow-box-shadow-and-border-radius/)

## Learning CSS3 Properties

This section provides you with a general overview of the introductory articles about CSS3\. This is a nice starting point to learn what CSS3 is, which properties it has and how designers apply them to web designs.

[The Basics of CSS3](https://www.webdesignerwall.com/tutorials/the-basics-of-css3/)  
Here is a post on the basics of the new properties: text-shadow, box-shadow, and border-radius. These CSS3 properties are commonly used to enhance layout and good to know.

[![  The Basics of CSS3](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e31b37b4-1124-4ead-a10e-c195c5c02f18/css3-200.jpg)](https://www.webdesignerwall.com/tutorials/the-basics-of-css3/)

[Introduction to CSS3](https://designshack.co.uk/tutorials/introduction-to-css3-part-1-what-is-it)  
A great series of articles by David Appleyard which covers most new features of CSS3 including borders, text effects, user interface features, multiple columns and backgrounds. The series also contains many examples and code snippets. Very useful.

[![  The Basics of CSS3](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d75fb457-f688-414d-b0d8-f42a8a322730/css3-techniques-23.jpg)](https://designshack.co.uk/tutorials/introduction-to-css3-part-1-what-is-it)

[CSS3 Examples and Best Practices](https://www.webdesignerwall.com/trends/css3-examples-and-best-practices/)  
The CSS3 trend is getting more and more popular. In fact CSS3 new features open a lot of new possibilities. Check out my previous post on "CSS3 Animation Demos" to see the things that you can do with it. However, don't get too excited so soon because it is not fully supported by all browsers yet. But this doesn't mean you shouldn't use it at all. So, when should you use CSS3 new features? Well, continue on this post to see some excellent examples.

[![  CSS3 Examples and Best Practices](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1319b67-204d-4d42-86e3-c4e97a0f87ab/css3-175.jpg)](https://www.webdesignerwall.com/trends/css3-examples-and-best-practices/)

[CSS of the Future: How CSS3 can Optimize Design](https://www.seo.com/blog/css-future-css3-optimize-design/)  
The design blogosphere has been buzzing about the improvements level 3 of Cascading Style Sheets will bring. Although still a ways off from official recommendation status by the W3C, some browsers are already supporting pending features. I want to highlight a few of the CSS3 features I'm excited about that will not only add flexibility to the design process, but that will aid with search and conversion optimization as well.

[![CSS of the Future: How CSS3 can Optimize Design ](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3be0effa-159c-4617-bae5-b01b6b10d110/css3-108.jpg)](https://www.seo.com/blog/css-future-css3-optimize-design/)

[Practical Uses of CSS3](https://www.viget.com/inspire/practical-uses-of-css3/)  
A user is not going to pull up your site in two different browsers to compare the experience, so they won't even know what they are missing. Just because something is not fully supported, that does not mean that we can't use it to an extent. In this article I'll show you some practical uses for CSS3.

[![Practical Uses of CSS3](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2ce26fc-6d15-4ada-88d5-32ff341afb75/css3-172.jpg)](https://www.viget.com/inspire/practical-uses-of-css3/)

<span class="removed_link" title="https://www.smashingmagazine.com/2010/02/use-css3-now/">You Can Use CSS3 Right Now</span>  
CSS3 makes a designer's work easier because they're able to spend less time hacking their CSS and HTML code to work in IE and more time crafting their design. It is the future of web design and can be used today. This article will hopefully show you to care a little less about making everything pixel perfect in IE. It will inspire you to spend more time making your designs exquisite in the rest of the browsers while serving up a working and perfectly accessible website for IE.

[CSS3 + Progressive Enhancement = Smart Design](https://perishablepress.com/press/2010/01/11/css3-progressive-enhancement-smart-design/)  
Progressive enhancement is a good thing, and CSS3 is even better. Combined, they enable designers to create lighter, cleaner websites faster and easier than ever before.

[![CSS3 + Progressive Enhancement = Smart Design ](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f2d1da1-280e-426b-aefd-be989d1a3288/css3-232.jpg)](https://perishablepress.com/press/2010/01/11/css3-progressive-enhancement-smart-design/)

## CSS3 Selectors

The advanced CSS selectors in CSS3 make it much easier for developers to apply style to specific design elements without using unnecessary CSS classes or <div>-containers. Unfortunately, Internet Explorer will support most of CSS3 selectors only in IE 9 ([detailed support table](https://www.quirksmode.org/css/contents.html)), so we would need to use JavaScript-solutions for older versions. Supported by Firefox 3.5+, Safari 3.2+ and many selectors are supported by Chrome and Opera, too (use the link above).

[Taming Advanced CSS Selectors](https://www.smashingmagazine.com/2009/08/17/taming-advanced-css-selectors/)  
The best way to avoid these plagues spreading in your markup and keep it clean and semantic, is by using more complex CSS selectors, ones that can target specific elements without the need of a class or an id, and by doing that keep our code and our stylesheets flexible.

[The Skinny on CSS Attribute Selectors](https://css-tricks.com/attribute-selectors/)  
Every single CSS element has three attributes: ID, class, and rel. To select the element in CSS, you could use and ID selector (#first-title) or a class selector (.magical). But did you know you can select it based on that rel attribute as well? That is what is known as an attribute selector.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4e92b2a-1e9c-42e9-8cad-b550fa6184ab/css3-techniques-18.jpg)](https://css-tricks.com/attribute-selectors/)

<p><a href="https://css-tricks.com/pseudo-class-selectors/">Meet the Pseudo Class Selectors</a><br />Pseudo class selectors are immensely useful in a variety of situations. Some of them are CSS3, some CSS2… it depends on each particular one. Outside of IE, they have great browser support. In IE land, even IE8, support is pretty barren. However, the IE9 preview has full support of them. 
<p>A Look at Some of the New Selectors Introduced in CSS3<br />A very practical article, introducing concrete examples and code snippets for using CSS3 in your design (e.g. alternate row styling, specific row styling, first and last element styling as well as styling enabled and disabled input fields).</p>

<p><a href="https://kimblim.dk/css-tests/selectors/">CSS3 Selectors Browser Support</a><br />The following is a range of CSS tests of the most common browsers' support for selectors and pseudo selectors. The tests includes basic stuff from the good old days of CSS1 and funky stuff from the future (CSS3).</p>
<p class="showcase"><a href="https://kimblim.dk/css-tests/selectors/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c3883cc-e0f9-402a-8898-25ada76b1c3c/css3-techniques-20.jpg" width="480" height="300" alt="Screenshot" /></a></p>

### JavaScript Solutions

<p>IE-CSS3.js: CSS3 pseudo-class selector emulation for IE<br />This library allows Internet Explorer to identify CSS3 pseudo-class selectors and render any style rules defined with them.</p>
<p class="showcase"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77375d18-3bcb-454a-bcf9-2fed05ab357c/css3-techniques-45.jpg" width="480" height="300" alt="Screenshot" /></p>

<p><a href="https://sizzlejs.com/">Sizzle – JavaScript Selector Library</a><br />A pure JavaScript CSS selector engine which supports all CSS3 selectors, including advanced ones such as escaped selector support (#id:value), :contains(text), has selector (:has(div)), position selectors (:first, :last, :even, :odd, :gt, :lt, :eq), form selectors and header selectors. The tools also provides meaningful error messages for syntax problems.</p>

<p><a href="https://digitarald.de/journal/89737433/rolling-out-sly-the-javascript-selector-engine/">Sly &mdash; The JavaScript Selector Engine</a><br />A quick, cross-browser JavaScript class for querying DOM documents using CSS3 selectors. It allows for customizable pseudo-classes, attribute operators and combinators and contains extra optimizations for frequently used selectors and latest browser features.</p>
<p class="showcase"><a href="https://digitarald.de/journal/89737433/rolling-out-sly-the-javascript-selector-engine/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8f82a62-d3e7-464f-a2cc-b8a40f42dcf0/css3-techniques-47.jpg" width="480" height="300" alt="Screenshot" /></a></p>

<p><a href="https://www.alistapart.com/articles/keepelementskidsinlinewithoffspring/">Offspring.js</a><br />Offspring is a JavaScript library that applies CSS classes corresponding to some advanced CSS selectors, opening the door for more precise selectors in previously-incapable browsers. A lightweight library which in full mode supports only <code>first-child</code>, <code>last-child</code>, <code>only-child</code>, <code>nth-child-odd</code>, <code>nth-child-even</code>, and <code>nth-child-##</code>.</p>

<p><a href="https://developer.yahoo.com/yui/selector/">YUI Selector Utility</a><br />The YUI CSS3 Selector Utility, providing a compact shorthand for collecting, filtering, and testing HTMLElements.</p> 
<p><a href="https://www.impressivewebs.com/buggy-css-selectors-cross-browser-jquery/">Getting Buggy CSS Selectors to Work Cross-Browser via jQuery</a><br />A simple table that describes a number of CSS selectors that are not cross-browser compatible, along with the jQuery syntax for each.</p>

## CSS3 Borders and Backgrounds

<p>CSS3's <code>border-radius</code> is most certainly a godsend for developers. Implementing rounded corners with 4 images of fixed size, using them with CSS background image property and adding a couple of unnecessary <code>div</code>'s just to make it all work sounds like a nightmare, and indeed it was a nightmare. CSS3 makes it possible to use a standard CSS property to achieve the same effect. Besides, we can use some nifty advanced background features to add border-image or multiple backgrounds to our designs. Advanced border and background features do not work in IE, so we will need workarounds again.</p>
<p><a href="https://webdesignernotebook.com/css/an-ode-to-border-radius/">An Ode To Border-radius</a><br />Border-radius: web designer’s sweetheart and (sadly) the one that IE8 forgot, destroying many a web designer’s dreams. This post explains how it works, what are some of the cross-browser alternatives, and showcases some websites that took a step ahead and implemented it.</p>
<p class="showcase"><a href="https://webdesignernotebook.com/css/an-ode-to-border-radius/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9aff238-12ab-40cc-95b5-6e7cdf0c4914/css3-techniques-51.jpg" width="480" height="300" alt="CSS3 Border Radius" /></a></p>

<p><a href="https://dev.opera.com/articles/view/css3-border-background-boxshadow/">CSS3 borders, backgrounds and box-shadows</a><br />This general article showcases some examples made using the new properties in the W3C's CSS3 Backgrounds and Borders specification. It explains the properties background-clip, background-origin, border-radius, Multiple background images, background-attachment, box-shadow and border-image.</p>
<p class="showcase"><a href="https://dev.opera.com/articles/view/css3-border-background-boxshadow/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7eca9c12-1a14-474b-bbcd-352b3047a7fc/css3-techniques-22.jpg" width="480" height="300" alt="CSS3 Background-Clip and @Font-Face " /></a></p>

<p><a href="https://dev.opera.com/articles/view/css3-border-background-boxshadow/">CSS3 border-image</a><br />CSS3 draft introduces one that could be terribly powerful: border-image. This article explains what it can do today, how you can use it and how to make it work in Internet Explorer 7+ (JavaScript library).</p>

<p><a href="https://snook.ca/archives/html_and_css/multiple-bg-css-gradients">Multiple Backgrounds and CSS Gradients</a><br />Among CSS designers, there are those who are venturing ahead with CSS3 and are likely to run into a world of interesting quirks across the various platforms. Multiple backgrounds by itself is simple enough, as are CSS gradients, but combining the two is where things get interesting.</p>
<p class="showcase"><a href="https://snook.ca/archives/html_and_css/multiple-bg-css-gradients"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d92ef8a-f40e-4099-adb3-0148b331f043/css3-techniques-21.jpg" width="480" height="300" alt="CSS3 Background-Clip and @Font-Face " /></a></p>

<p><a href="https://www.smashingmagazine.com/2010/05/27/css-three-connecting-the-dots/">CSS Three &mdash; Connecting The Dots</a><br />This article describes how you can use <code>background-clip</code> property together with other CSS3 properties to create an experimental design.</p>

<p><a href="https://trentwalton.com/2010/04/06/css3-background-clip-font-face/">CSS3 Background-Clip and @Font-Face </a><br />An experiment with background-clip: text and @font-face via Typekit. When I finished Volume 2 in my Quoting Lebowski series the first thing that came to mind was that I bet I could CSS this.</p>
<p class="showcase"><a href="https://trentwalton.com/2010/04/06/css3-background-clip-font-face/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47de86c4-b737-4b11-b8ba-8adf0e8dd055/css3-120.jpg" width="480" height="300" alt="CSS3 Background-Clip and @Font-Face " /></a></p>

<p><a href="https://www.smashingmagazine.com/2009/09/02/backgrounds-in-css-everything-you-need-to-know/">Backgrounds In CSS: Everything You Need To Know</a><br />This article shows some common tricks that can be done with the background as well as what’s in store for backgrounds in CSS 3 (including four new background properties).</p>

### JavaScript Solutions
<p><a href="https://www.hanspinckaers.com/multiple-backgrounds-with-canvas-drawing">Cross-Browser Multi-background images, including IE</a><br />One of the biggest problems with using the CSS3 Multi-backgrounds is that it is not usable in Internet Explorer, however by using the: 'AlphaImageLoader IEFilter', it is possible to place two background images in an element.</p>

<p><a href="https://www.hanspinckaers.com/multiple-backgrounds-with-canvas-drawing">Multiple backgrounds with canvas drawing</a><br />All modern browsers are compatible with the canvas-tag, beside of Internet Explorer, but Google created a superb piece of javascript that ported the canvas to IE. This little piece of JavaScript draws multiple backgrounds in a canvas element behind HTML elements.</p>
<p class="showcase"><a href="https://www.hanspinckaers.com/multiple-backgrounds-with-canvas-drawing"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d7e30df-2c7f-4993-a543-e12aa3d54c8c/css3-techniques-48.jpg" width="480" height="300" alt="Canvas" /></a></p>

<p><a href="https://cubiq.org/dropbox/cssgrad.html">cssSandpaper – a CSS3 JavaScript Library</a><br />The cssSandpaper JavaScript library looks at the stylesheets in an HTML document and, where possible, smooths out the browser differences between CSS3 properties like <code>transform</code>, <code>opacity</code>, <code>box-shadow</code> and others.  This script is not only useful for developers who want to support CSS3 in IE.</p>
<p class="showcase"><a href="https://cubiq.org/dropbox/cssgrad.html"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b29c6ca9-5d23-46a1-9149-4877c5d259c9/css3-techniques-50.jpg" width="480" height="300" alt="Canvas" /></a></p>

<p><a href="https://stackoverflow.com/questions/2687804/emulating-css3-border-radius-and-box-shadow-in-ie7-8">Emulating CSS3 border-radius and box-shadow in IE7/8</a><br />A thread on StackOverflow that explains how to emulate <code>border-radius</code> and <code>box-shadow</code> on IE7/8.</p>
<p><a href="https://www.smashingmagazine.com/2010/04/28/css3-solutions-for-internet-explorer/">CSS3 Solutions for Internet Explorer </a><br />Smashing Magazine's article explaining how to make <code>border-radius</code>, <code>box-shadow</code>, multiple backgrounds, <code>gradients</code> and CSS Transformations work in Internet Explorer.</p>

## CSS3 Media Queries

<p>Web design community has been experimenting with adaptive layouts <a href="https://www.alistapart.com/articles/switchymclayout/">for a while</a> now, and with CSS media queries we now finally have a very simple and powerful tool to implement adaptive layouts without the use of JavaScript. Support: Firefox 3.5+, Safari 4.0+, Chrome 3.0+, Opera 9.6+, Internet Explorer 9.0. Again: we will need a JavaScript-solution for Internet Explorer.</p>
<p><a href="https://www.slideshare.net/maxdesign/css3-media-queries">CSS3 Media Queries</a><br />A detailed slideshow presentation by Russ Weakley.</p>
<p class="showcase"><a href="https://www.slideshare.net/maxdesign/css3-media-queries"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ff800f1-a2b8-4ee8-825e-5c787d2ec831/css3-207.jpg" width="480" height="300" alt="CSS3 Media Queries" /></a></p>

<p><a href="https://www.1stwebdesigner.com/tutorials/how-to-use-css3-orientation-media-queries/">How to use CSS3 Orientation Media Queries </a><br />For a long time we have been able to specify styles for different media types using CSS, print and screen being the most recognizable. With CSS3 these media types have been extended to allow additional expressions, aka media queries, which gives us greater control on when specific styles should be applied. In this article I will focus on the orientation media query and have a fun demonstration showing how to use it.</p>

<p><a href="https://mislav.uniqpath.com/2010/04/targeted-css/">Detecting device size and orientation in CSS</a><br />Gone are the days when we could safely assume that most our site visitors would have at least a 1024px-wide screen resolution. With smartphones and tablet computers on the rise, you visitors could also be browsing the web with screen widths ranging from 320px upwards. Does your site look good on a 768px-wide canvas? That's how people will see it using a portrait-oriented iPad.</p>
<p class="showcase"><a href="https://mislav.uniqpath.com/2010/04/targeted-css/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cde5dbf-bf00-4dc6-8460-1430b264c82e/css3-223.jpg" width="480" height="300" alt="Detecting device size and orientation in CSS" /></a></p>

<p><a href="https://addyosmani.com/links/2010/04/27/how-to-use-css3-orientation-media-queries/">How to use CSS3 Orientation Media Queries</a><br />For a long time we have been able to specify styles for different media types using CSS, print and screen being the most recognizable. With CSS3 these media types have been extended to allow additional expressions, aka media queries, which gives us greater control on when specific styles should be applied.</p>

<p><a href="https://css-tricks.com/resolution-specific-stylesheets/">Different Stylesheets for Differently Sized Browser Windows</a><br />This article explains how to implement resolution-dependent layouts using CSS3 media queries and JavaScript for Internet Explorer. Single website, different CSS files for rearranging a website to take advantage of the size available.</p>
<p class="showcase"><a href="https://css-tricks.com/resolution-specific-stylesheets/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c825974-1e09-4a74-8b94-89d451157afb/css3-techniques-52.jpg" width="480" height="300" alt="Different Stylesheets for Differently Sized Browser Windows" /></a></p>

### JavaScript Solutions

<p>Media Query JavaScript library<br />Media queries and device capabilities are currently not exposed to JavaScript directly. You can use this library to detect the capabilities of the browser and adapt your web page or widget accordingly.</p>

<p><a href="https://www.protofunc.com/scripts/jquery/mediaqueries/">CSS 3 Media Queries for all Browsers (jQuery Plugin)</a><br />The script adds basic Media-Query-Support (min-width and max-width in px units ) to the browsers. It helps you to create a dynamic resolution dependent layout with Web standards in mind.</p>

<p><a href="https://code.google.com/p/css3-mediaqueries-js/">css3-mediaqueries.js: make CSS3 Media Queries work in all browsers (JavaScript library)</a><br />A JavaScript library to make IE 5+, Firefox 1+ and Safari 2 transparently parse, test and apply CSS3 Media Queries. Firefox 3.5+, Opera 7+ and Safari 3+ already offer native support.</p>

## CSS3 Multi-Column Layout
<p>CSS3 Multi-Column layout module proposes a new technique for web layouts. As an alternative to relative/absolute positioning and floats, you can also use multi-column properties for cross-browser multi-column layouts. Obviously, this feature is great for magazine layouts and designers using grids or horizontal layouts. Support: Firefox 3.0+, Safari 3.2+, Chrome 3.0+. Neither Opera nor Internet Explorer support these features, and it's not clear if Opera will include multi-column layout support in the upcoming version. Again, a workaround is necessary here.</p>

<p><a href="https://webdesignernotebook.com/css/remembering-the-css3-multi-column-layout-module/">Remembering: The CSS3 Multi-Column Layout Module</a><br />Multi-column layout module allows you to layout the content of an element in multiple columns, like flowing text on a newspaper-type layout. Some of these Modules are at a more advanced stage of development and closer to being final than others. You can take a look at the <a href="https://www.w3.org/Style/CSS/current-work.html">Current Work table here</a>.</p>
<p class="showcase"><a href="https://webdesignernotebook.com/css/remembering-the-css3-multi-column-layout-module/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec3e1fdd-cd5f-4145-9822-3c906b28c3a4/css3-techniques-25.jpg" width="480" height="300" alt="CSS3 Screenshot" /></a></p>

<p>Using CSS3 media queries to achieve multiple columns on browser resize<br />This article explains how to combine CSS3 media queries and Multi-column layout module in CSS3 to create an adaptive CSS layout.</p>

<p><a href="https://www.quirksmode.org/css/multicolumn.html">Multi-column layout Module</a><br />The ever more delayed CSS 3 specification has a Multi-column layout module. Unsurprisingly, this module specifies ways and means of creating multi-column texts. This article contains a few tests of the column declarations.</p>
<p class="showcase"><a href="https://www.quirksmode.org/css/multicolumn.html"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7658d4e9-dfcb-4246-85b0-4bafedb855cd/css3-techniques-27.jpg" width="480" height="300" alt="CSS3 Screenshot" /></a></p>

<p><a href="https://www.stuffandnonsense.co.uk/archives/css3_multi-column_thriller.html">CSS3 Multi-Column Thriller</a><br />A detailed article about the CSS3 Multi-column Layout module, its features and possibilities. By Andy Clarke.</p>
<p class="showcase"><a href="https://www.stuffandnonsense.co.uk/archives/css3_multi-column_thriller.html"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43cf355e-cd39-4e64-b516-c41a25438e4c/css3-techniques-28.jpg" width="480" height="300" alt="CSS3 Screenshot" /></a></p>

### JavaScript-Solutions
<p><a href="https://welcome.totheinter.net/columnizer-jquery-plugin/">Columnizer jQuery Plugin</a><br />The primary problem with static column layouts, is that they break down when viewed on a variety of widths. There’s no good way to have multiple dynamic columns for your content. What’s needed is to adapt to the user’s screen width, and allow content to easily be resized and refit to as many columns as needed. What’s needed is the JQuery Columnizer Plugin. And, obviously, it works in Internet Explorer, too.</p>
<p>CSS3 - Multi Column Layout JS Library<br />A javascript implementation of the CSS3 multi-column module.</p>
<p class="showcase"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64e50216-30ec-4956-af52-64ad2b286722/css3-techniques-44.jpg" width="480" height="300" alt="CSS3 Screenshot" /></p>

<p><a href="https://codeasily.com/jquery/multi-column-list-with-jquery">Multi Column List with jQuery</a><br />"Instead of relying on consistent line heights, and applying different margin settings to list elements, I decided to decompose the large source list into several smaller lists (one for each column) and then use a CSS float parameter to make them all appear side-by-side."</p>

## CSS3 Color: Opacity, RGBa, HSLa
<p>With CSS3, web designs will be gaining more depth in the future. We can easily define the alpha transparency level of design elements in CSS, without extra images and extra markup. Support: Firefox 3.0+, Safari 3.2+, Chrome 3.0+, Opera 10.1+. Until yet, Internet Explorer does not support RGBa and HSLa, and Internet Explorer 9.0 will be supporting RGBa.</p>

<p><a href="https://24ways.org/2009/working-with-rgba-colour">Working With RGBa Colour</a><br />CSS3 introduces a couple of new ways to specify colours, and one of those is RGBa. The A stands for Alpha, which refers to the level of opacity of the colour, or to put it another way, the amount of transparency. This means that we can set not only the red, green and blue values, but also control how much of what’s behind the colour shows through. Like with layers in Photoshop.</p>
<p class="showcase"><a href="https://24ways.org/2009/working-with-rgba-colour"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cf2f487-e685-4d77-9763-b8387dd443f5/css3-techniques-29.jpg" width="480" height="300" alt="Working with RGBa" /></a></p>

<p><a href="https://css-tricks.com/yay-for-hsla/">Yay for HSLa</a><br />An introduction to HSLa (Hue Saturation Lightness(and alpha) and it's a way of declaring color in CSS. Basically, every browser that supports RGBa, supports HSLa too.</p>
<p class="showcase"><a href="https://css-tricks.com/yay-for-hsla/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c13b346-1fe6-4cd9-8b55-7c7562d50f35/css3-techniques-05.jpg" width="480" height="300" alt="Yay for HSLa" /></a></p>

<p><a href="https://kimili.com/journal/rgba-css-generator-for-internet-explorer">RGBa CSS Generator for Internet Explorer</a><br />If you’ve been keeping up with how recent browsers have been implementing parts of the CSS3 spec, you may already be using RGBa to define semi-transparent background colors. You’d also know that this works in recent versions of Firefox and Safari, but not in any version of Internet Explorer. This generator should solve your headache when you want to apply RGBa to your next project.</p>
<p class="showcase"><a href="https://kimili.com/journal/rgba-css-generator-for-internet-explorer"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab831656-fed9-45ef-9b39-e833bb0c4f9a/css3-techniques-30.jpg" width="480" height="300" alt="Screenshot" /></a></p>

<p>CSS3 Opacity<br />This article explains how you can apply opacity to change the transparency of an element and offers a cross-browser solution for that.</p>

<p><a href="https://deepubalan.com/blog/2010/03/29/rgba-vs-opacity-the-difference-explained/">RGBa vs Opacity: The Difference Explained</a><br />When we apply an opacity value to an element, the opacity value is inherited by all its child elements. RGBa sets the opacity of the color value of that particular element and the transparency is not inherited by its child elements. In other words, RGBA sets the opacity value only for a single declaration.</p>
<p><a href="https://forabeautifulweb.com/blog/about/is_css3_rgba_ready_to_rock/">Is CSS3 RGBa ready to rock?</a><br />A detailed article explaining why we can start using RGBa in our designs today.</p>
<p><a href="https://dev.opera.com/articles/view/color-in-opera-10-hsl-rgb-and-alpha-transparency/">HSL, RGB and Alpha Transparency</a><br />This article explains how the HSL (Hue, Saturation, Lightness) and RGB (Red, Green, Blue) color models work (and the alpha transparency options in both color models).</p>

<p><a href="https://css-tricks.com/examples/HSLaExplorer/">HSLa and RGBa Explorer</a><br />This little tool helps you to pick RGBa and HSLa color values for your designs. By Chris Coyier.</p>
<p class="showcase"><a href="https://css-tricks.com/examples/HSLaExplorer/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9b16d5e-57ac-4c2a-b4d6-ae1d0e068804/css3-techniques-31.jpg" width="480" height="300" alt="Screenshot" /></a></p>

<p><a href="https://www.slideshare.net/LeaVerou/colors-in-css3?src=embed">Colors In CSS3 (Slideshow)</a><br />A presentation by Lea Verou.</p>
<p class="showcase"><a href="https://www.slideshare.net/LeaVerou/colors-in-css3?src=embed"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7a567f8-1500-4b65-b276-458b15db2d59/css3-techniques-32.jpg" width="480" height="300" alt="Screenshot" /></a></p>

<p><a href="https://css-tricks.com/rgba-browser-support/">RGBa Browser Support</a><br />The article describes how browsers handle RGBa and what options developers have to guarantee the cross-browser RGBa support.</p>

## CSS3 Gradients
<p>Many regular tasks that we are performing using Photoshop today, will be easy to implement with simple CSS3 styles. One of such task is adding gradients to our design elements. The advantage is clear: we are creating scalable vector graphics in the browser and we save HTTP requests. CSS3 gradients fall into the camp where you can specify fallbacks (i.e. images), so that browsers that don’t support them just use the image instead. Good news: <a href="https://css-tricks.com/css3-gradients/">using different syntax for different rendering engines</a>, we can use gradients in all browsers.</p>
<p><a href="https://cubiq.org/playing-with-css3-gradients">Playing with CSS3 gradients</a><br />CSS3 gradients and masks are so powerful together that the average web application would never need an image for layout anymore. And it's not about making simple buttons. Mixing multiple gradients, masks, box-shadow and text-shadow you can achieve extremely complex results.</p>
<p class="showcase"><a href="https://cubiq.org/playing-with-css3-gradients"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a125161a-cc47-4a8b-b7dc-a8f1ef464e03/css3-techniques-49.jpg" width="480" height="300" alt="CSS3 Gradients " /></a></p>

<p><a href="https://css-tricks.com/css3-gradients/">Speed Up with CSS3 Gradients</a><br />WebKit browsers paved the way with CSS based gradients. Now Firefox 3.6 is out and is supporting them as well, which makes using them for progressive enhancement all the more appealing. More good news, CSS3 gradients fall into the camp where you can specify fallbacks (i.e. images) so that browsers that don't support them just use the image instead.  But what if you need to use an image anyway, why bother with declaring the gradient with CSS? That is kind of how I felt for a long time, but there is one important aspect that makes it worth it: browsers that support them don't load the image fallback. One less HTTP Request = all the faster your site will load.</p>
<p class="showcase"><a href="https://css-tricks.com/css3-gradients/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91618985-0219-4d52-82ae-82e8cae533c8/css3-106.jpg" width="480" height="300" alt="Speed Up with CSS3 Gradients" /></a></p>

<p><a href="https://www.webdesignerwall.com/tutorials/cross-browser-css-gradient/">Cross-Browser CSS Gradient</a><br />This post will show you how to code for the CSS gradient to be supported by the major browsers: IE, Firefox 3.6+, Safari, and Chrome.</p>
<p><a href="https://www.the-art-of-web.com/css/radial-gradients/">CSS: Radial gradients syntax</a><br />In this article you'll explore the various properties of radial gradient backgrounds as implemented by the WebKit and Gecko rendering engines. Gradients can used as backgrounds, pseudo-images and image masks among other things.</p>

<p><a href="https://www.webdesignerwall.com/tutorials/css3-gradient-buttons/">  CSS3 Gradient Buttons</a><br /> Today I'm going to show you how to put the CSS gradient feature in a good practical use. Check out my demo to see a set of gradient buttons that I have created with just CSS (no image or Javascript). The buttons are scalable based on the font-size. The button size can be easily adjusted by changing the padding and font-size values. The best part about this method is it can be applied to any HTML element such as div, span, p, a, button, input, etc.</p>
<p class="showcase"><a href="https://www.webdesignerwall.com/tutorials/css3-gradient-buttons/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10ea30f7-6ec7-4152-a434-74ccc5108ba2/css3-132.jpg" width="480" height="300" alt="  CSS3 Gradient Buttons" /></a></p>

<p><a href="https://gradients.glrzad.com/">CSS3 Gradient Generator</a><br />This tools generates CSS3 snippet for Webkit and Mozilla that can be used everywhere, be it a background-image, mask, border, or list item bullet. Another CSS3 linear gradient generator and <a href="https://www.display-inline.fr/projects/css-gradient/#startType=hex&amp;startValue=aaeeff&amp;endType=hex&amp;endValue=3399cc">yet another one</a>.</p>
<p class="showcase"><a href="https://gradients.glrzad.com/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f78c8e15-9857-42b8-9de5-009ad97be3d9/css3-techniques-35.jpg" width="480" height="300" alt="  CSS3 Gradient Buttons" /></a></p>

<p><a href="https://robertnyman.com/2010/02/15/css-gradients-for-all-web-browsers-without-using-images/">CSS Gradients For All Web Browsers, Without Using Images</a><br />Robert Nyman explains how to code cross-browser CSS gradients that work even in Internet Explorer.</p>

<p><a href="https://net.tutsplus.com/tutorials/html-css-techniques/quick-tip-understanding-css3-gradients/">Quick Tip: Understanding CSS3 Gradients</a><br />We can now create powerful gradients with minimal effort. In this video quick tip, we’ll examine some of the differences in syntax when working with the -moz and -webkit vendor prefixes.</p>

<p><a href="https://weston.ruter.net/projects/css-gradients-via-canvas/">(Kind of) Cross-Browser CSS Gradients via Canvas</a><br />CSS Gradients via Canvas provides a subset of WebKit's CSS Gradients proposal for browsers that implement the HTML5 canvas element. Unlike WebKit, this implementation does not currently allow gradients to be used for border images, list bullets, or generated content. Rudimentary gradients may be achieved in IE by means of its non-standard <a href="https://msdn.microsoft.com/en-us/library/ms532997%28VS.85%29.aspx">gradient filter</a>.</p>

## CSS3 Typography (incl. CSS 2.1 @font-face)
<p>Technically, @font-face attribute is not a CSS3 features, as it was proposed already in CSS 2.1. However, it is now being heavily used and provides designers with more freedom in their choice of typography in web design. @font-face is supported by all major browsers (Firefox 3.5+, Safari 3.2+, Chrome 4.0+, Opera 10.1+, Internet Explorer 6.0+). However, Trident (Internet Explorer) only supports EOT fonts. Opera does not support the font when 'format("opentype")' is used, although it does otherwise appear to support OTF fonts. For Internet Explorer, we need to use EOT-Kits such as <a href="https://www.fontsquirrel.com/fontface/generator">FontSquirrel's one</a> to make IE play nicely. Another option is to use commercial and/or open source font embedding services such as <a href="https://typekit.com/">TypeKit</a> or <a href="https://code.google.com/apis/webfonts/">Google Fonts API</a>.</p>
<p><a href="https://www.smashingmagazine.com/2010/03/01/css-and-the-future-of-text/">The Future Of CSS Typography</a><br />In this article, we’ll look at some useful techniques and clever effects that use the power of style sheets and some features of the upcoming CSS Text Level 3 specification, which should give Web designers finer control over text.</p>
<p class="showcase"><a href="https://www.smashingmagazine.com/2010/03/01/css-and-the-future-of-text/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb97efa4-1ea8-4f0a-828c-1af793140731/css3-techniques-42.jpg" width="480" height="300" alt="Beautiful UI styling with CSS3 text-shadow, box-shadow, and border-radius " /></a></p>

<p><a href="https://www.kremalicious.com/2008/04/make-cool-and-clever-text-effects-with-css-text-shadow/">Text-Shadow Exposed</a><br />An older, yet still useful article that provides a detailed
introduction to the CSS property <code>text-shadow</code>. Browser support table is provided as well. Text-shadow is support in Firefox 3.5+, Safari 4.0+, Chrome 3.0+, Opera 9.6+, and not supported by the whole Internet Explorer family.</p>

<p><a href="https://sixrevisions.com/css/font-face-guide/">The Essential Guide to @font-face</a><br />This guide will teach you how to implement @font-face with cross-browser compatibility and will also look at a number of the supporting services that have arisen, making it even easier to use custom fonts in your web designs.</p>
<p class="showcase"><a href="https://sixrevisions.com/css/font-face-guide/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5efa6204-b4d8-4bca-90b7-b175aa69552f/css3-techniques-39.jpg" width="480" height="300" alt="Screenshot" /></a></p>

<p><a href="https://www.fontsquirrel.com/fontface/generator">@font-face generator</a><br />An advanced generator of ready-to-use @font-face kits for various font formats, CSS styling and options. Also, check <a href="https://www.fontsquirrel.com/fontface">FontSquirrel</a> for dozens of useful, freely available @font-face font kits.</p>
<p class="showcase"><a href="https://www.fontsquirrel.com/fontface/generator"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf985b8e-3c78-4708-86de-fac5e3f2e119/css3-techniques-37.jpg" width="480" height="300" alt="Screenshot" /></a></p>

<p>The New Lens Flare <br />"By abusing the <code>text-shadow</code> property, you can turn any ho-hum bit of text into a magnificent, radiant beacon of allure and awe. But getting your bling-bling on has never been for the cheapskates. Expect to pay a boatload in refresh rates, as your browser buckles under the weight of rendering that glorious halo."</p>
<p class="showcase"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91695c0b-e720-4580-b985-9eda3ea69d54/css3-210.jpg" width="480" height="300" alt="The New Lens Flare " /></p>

### JavaScript Solutions

<p><a href="https://kilianvalkhof.com/2008/javascript/text-shadow-in-ie-with-jquery/">Text-Shadow In IE With JQuery</a><br />One handy little thing of Internet Explorer is that it also gives you access to CSS declarations it does not understand, so we can simply request the text-shadow value of a given element and process that. Works in Internet Explorer 5.5+.</p>
<p>CSS-3 Text-Shadow<br />CSS3 Text Shadow is not supported by Internet Explorer, but it is however possible to create an equivialant effect with the IE proprietary <a href="https://msdn.microsoft.com/en-us/library/ms532979(VS.85).aspx">CSS Filter Blur</a> and served with the jQuery plugin jquery.textshadow.js.</p>
<p><a href="https://www.nealgrosskopf.com/tech/thread.php?pid=61">jQuery Plugin To Create CSS3 Text-Shadows In Internet Explorer</a><br />Another approach that uses IE's shadow filter instead of blur filter. IE6, IE7 and IE8 do not support the CSS3 text-shadow property, and one form of shadowing they support is the proprietary <a href="https://msdn.microsoft.com/en-us/library/ms673539%28VS.85%29.aspx">shadow filter</a>.</p>

## CSS3 Flexible Box Model, Box Sizing and Box Shadow
<p>Another nice feature is the flexible box model which makes it much easier to create fluid layouts which adapt themselves to the size of the browser window or elastic layouts which adapt themselves to the font size. Also, you can specify a border/padding value in relation to a fluid length element with the new ‘box-sizing’ property (supported by IE8+ and all major browsers). Finally, you can also define box shadow to add more depth to your design elements (unavailable in IE 9, available in all major browsers).</p>

<p><a href="https://helephant.com/2008/10/css3-box-sizing-attribute/">CSS3 box-sizing attribute</a><br />CSS3 is going to include a new attribute called box-sizing so we can choose whether the width set on an element will include borders and padding or whether borders and paddings will be added to the width. Further details.</p>
<p class="showcase"><a href="https://helephant.com/2008/10/css3-box-sizing-attribute/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa0a2773-a3a5-48fa-8d1f-4d4db99f79c2/css3-techniques-40.jpg" width="480" height="300" alt="Screenshot" /></a></p>

<p><a href="https://hacks.mozilla.org/2010/04/the-css-3-flexible-box-model/">The CSS 3 Flexible Box Model</a><br />CSS 3 introduces a brand new box model in addition of the traditional box model from CSS 1 and 2. The flexible box model determines the way boxes are distributed inside other boxes and the way they share the available space. Take a look at the <a href="https://webtint.net/tutorials/future-of-css-the-flexible-box-model/">support table and tutorial</a>, too.</p>

<p><a href="https://designshack.co.uk/tutorials/introduction-to-css3-part-4-user-interface">Resizing, Box Sizing, Outline</a><br />CSS3 brings some great new properties relating to resizing elements, cursors, outlining, box layout and more. This article focuses on three of the most significant user interface enhancements.</p>

<p><a href="https://www.westciv.com/tools/boxshadows/index.html">Box Shadow Online Generator</a><br />CSS Shadows take three length values, and a color. The length values are a horizontal offset, a vertical offset and a blur. offsets may be negative or positive.</p>

<p><a href="https://markusstange.wordpress.com/2009/02/15/fun-with-box-shadows/">Fun With Box Shadows</a><br />This articles illustrates dozens of nice examples of how box-shadow can be used to achieve various visual effects.</p>
<p class="showcase"><a href="https://markusstange.wordpress.com/2009/02/15/fun-with-box-shadows/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d8c70cd-3919-4f18-b7b0-1b3e34f1b666/css3-techniques-43.jpg" width="480" height="300" alt="Screenshot" /></a></p>

<p><a href="https://dimox.net/cross-browser-css3-box-shadow/">Cross-browser CSS3 box-shadow</a><br />There is a simple way for creating cross-browser box-shadow in all modern and popular browsers including Internet Explorer (Opera only since 10.50 pre-alpha version). The solution uses VML and behaviour.</p>
<p class="showcase"><a href="https://dimox.net/cross-browser-css3-box-shadow/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1b2f417-d00f-434b-a7a5-dc0e811f04c5/css3-techniques-53.jpg" width="480" height="300" alt="Screenshot" /></a></p>

<p><a href="https://dimox.net/cross-browser-css3-box-shadow/">CSS3 box-shadow for IE 6-8</a><br />This article presents a very dirty way of making CSS3 Box Shadow work in Internet Explorer. The idea is to use <a href="https://msdn.microsoft.com/en-us/library/ms533086%28VS.85%29.aspx">Microsoft Shadow Filters</a> and <code>zoom</code>-property. In German, but the code should be self-explanatory.</p>

## CSS3 Transitions, Transforms, Animations
<p>CSS designers with sympathy for eye candy will find many intriguing features in CSS3 Transitions, Transforms and Animations. These are most useful when used in a subtle way, for visual feedback and smoothing user interaction. Until yet, transitions and animations are supported only in Webkit-browsers, transformations are supported only in Safari 5.0+. Unfortunately, there are no real alternatives or workarounds. So using these features makes sense only with progressive enhancement in mind.</p>
<p><a href="https://24ways.org/2009/going-nuts-with-css-transitions">Going Nuts with CSS Transitions</a><br />This post shows you how CSS 3 transforms and WebKit transitions can add zing to the way you present images on your site.</p>
<p class="showcase"><a href="https://24ways.org/2009/going-nuts-with-css-transitions"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dbe74f7-e059-42c7-b19a-d35b884c33ef/css3-techniques-54.jpg" width="480" height="300" alt="Using CSS3 Transitions, Transforms and Animation" /></a></p>

<p><a href="https://samuli.hakoniemi.net/css3-transitions-are-we-there-yet/">CSS3 Transitions - Are We There Yet? </a><br /> The whole topic has been split in two parts. The first part is offering a general overview in current status of CSS3 Transitions. Second part is called "CSS3 Transitions &mdash; Problems and Solutions", which will explain in details how CSS3 Transitions behave in different browsers.</p>
<p class="showcase"><a href="https://samuli.hakoniemi.net/css3-transitions-are-we-there-yet/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/371e6e49-4e43-4a43-9035-9d13a7592960/css3-techniques-55.jpg" width="480" height="300" alt="CSS3 Transitions - Are We There Yet? " /></a></p>

<p>Sexy Interactions with CSS Transitions <br />While Webkit-based browsers have had CSS Transitions since Safari 3.1.2, other browsers are only just now coming out with nightly builds supporting this exciting new part of the CSS3 specification.  With all browsers except for IE being slated to have Transitions support in the coming months, more and more web designers are turning to this powerful technique as a means to enhance their website's user experience.</p>
<p class="showcase"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc6226d7-70e3-4471-9f96-ad4b06588db1/css3-157.jpg" width="480" height="300" alt="Sexy Interactions with CSS Transitions " /></p>

<p><a href="https://css3.bradshawenterprises.com/">Using CSS3 Transitions, Transforms and Animation</a><br />Currently transitions and 2D transforms are available in all current browsers (at least in a dev build) apart from Internet Explorer. 3D transforms and animations are only in Safari. Most examples degrade nicely, so if you are using a legacy browser you can still use a site using these, you just won't get animation.</p>
<p class="showcase"><a href="https://css3.bradshawenterprises.com/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2593bfe9-9f8b-4806-8a65-d939eeb63698/css3-208.jpg" width="480" height="300" alt="Using CSS3 Transitions, Transforms and Animation" /></a></p>

<p><a href="https://www.webdesignerdepot.com/2010/01/css-transitions-101/">CSS Transitions 101 </a><br />Despite people's expectation of change and movement on the screen, CSS and HTML have few controls that allow you to design interactivity, and those that exist are binary.  What we need is a quick and easy way to add simple transitions to the page and in this article you'll find useful information about CSS transitions and how to use them.</p>
<p class="showcase"><a href="https://www.webdesignerdepot.com/2010/01/css-transitions-101/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5457e465-1a47-495f-942c-497042aa8bcc/css3-238.jpg" width="480" height="300" alt="CSS Transitions 101 " /></a></p>

<p>CSS Fundamentals: CSS 3 Transitions<br />This article explains the basics of using CSS3 transitions and animations to add an extra layer of polish.</p>

<p><a href="https://kilianvalkhof.com/2010/css-xhtml/css3-loading-spinners-without-images/">CSS3 loading spinners without images</a><br />While playing around with css-transform to make various shapes, I saw a way to create animated image-less loading spinners such as used in a lot of web-apps and of course on the iPhone.</p>
<p class="showcase"><a href="https://kilianvalkhof.com/2010/css-xhtml/css3-loading-spinners-without-images/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55ce5873-8813-4164-8f0a-6446f0451caa/css3-199.jpg" width="480" height="300" alt="CSS3 loading spinners without images" /></a></p>

<p><a href="https://www.marcofolio.net/css/3d_animation_using_pure_css3.html">3D animation using pure CSS3</a><br />The perspective property in Safari CSS Visual Guide is what we need to create the 3D effect. Using transform and transition, we can create 3D animation using pure CSS3.</p>
<p class="showcase"><a href="https://www.marcofolio.net/css/3d_animation_using_pure_css3.html"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf6bcedf-fb3f-4c9a-91b8-3b5ada827af8/css3-141.jpg" width="480" height="300" alt="3d animation using pure CSS3" /></a></p>

<p><a href="https://legendthemes.com/2010/05/14/3d-css-wordpress-theme/">First Ever 3D CSS WordPress Theme</a><br />CSS3 offers great opportunities for 3D transforms, perspective, and animation. Currently Safari is the only browser that fully supports it, but Firefox and Chrome will add support soon. With that we can take regular objects (WordPress posts in this case) and animate them.</p>
<p class="showcase"><a href="https://legendthemes.com/2010/05/14/3d-css-wordpress-theme/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1f8fb02-3b5a-4402-bc97-f6ed136bba8e/css3-techniques-06.jpg" width="480" height="300" alt="First Ever 3D CSS WordPress Theme" /></a></p>

## CSS3 Generators 

<ul> 
<li><a href="https://border-radius.com/">CSS3 Border Radius Generator</a><br />A simple generator that produces code for rounded corners using <code>border-radius</code>-property.</li>
<li><a href="https://csscorners.com/">CSS Corners</a><br />Yet another generator that produces the code for rounded elements with a linear gradient.</li>
<li><a href="https://css3generator.com/">CSS3 Generator</a><br />Generator of code snippets for <code>border-radius</code>, <code>box-shadow</code>, <code>text-shadow</code>, <code>RGBa</code>, <code>@font-face</code>, multiple columns, <code>box-resize</code>, <code>box-sizing</code> and <code>outline</code>.</li> 
<li><a href="https://css3please.com/">CSS3 Please!</a><br />Another generator and tester of CSS3 rules on the fly. Supports <code>border-radius</code>, <code>box-shadow</code>, <code>linear gradient</code>, <code>RGBa</code>, <code>transform</code>, <code>transition</code> and <code>@font-face</code>.</li> 
<li><a href="https://westciv.com/tools/index.html">CSS3 Sandbox</a><br />Westciv's set of tools generates <a href="https://westciv.com/tools/gradients/">linear gradients</a>, <a href="https://westciv.com/tools/radialgradients/">radial gradients</a>, <a href="https://westciv.com/tools/shadows/">text shadows</a>, <a href="https://westciv.com/tools/boxshadows/">box shadows</a>, <a href="https://westciv.com/tools/transforms/">transforms</a> as well as <a href="https://westciv.com/tools/textStroke/">text stroke</a>. Produces the code for Gecko and Webkit.</li> 
<li><a href="https://gradients.glrzad.com/">CSS3 Gradient Generator</a><br />Generates the code for linear gradients for Mozilla and WebKit browsers.</li> 
<li><a href="https://border-image.com/#%7B%22src%22%3A%22http%3A%2F%2Fwww.w3.org%2FTR%2Fcss3-background%2Fborder.png%22%2C%22linkBorder%22%3Atrue%2C%22borderWidth%22%3A%5B0%2C0%2C0%2C0%5D%2C%22imageOffset%22%3A%5B34%2C27%2C27%2C27%5D%2C%22setRepat%22%3Afalse%2C%22repeat%22%3A%5B%22repeat%22%2C%22repeat%22%5D%2C%22scaleFactor%22%3A3%2C%22setRepeat%22%3Atrue%7D">CSS Border-Image Generator</a><br />Generates the code for various border sizes, allows for border offsets and allows you to select vertical or/and horizontal repeat.</li>
<li><a href="https://www.fontsquirrel.com/fontface/generator">@font-face Generator</a><br />CSS3 @font-face kit generator.</li> 
</ul> 

## Useful References
<ul> 
<li><a href="https://www.impressivewebs.com/css3-click-chart/">CSS3 Click Chart</a><br />A detailed overview of CSS3 features, with descriptions, syntax, examples and browser support details for each CSS3 property.</li>
<li><a href="https://gallery.theopalgroup.com/selectoracle/">SelectORacle</a><br />This tools explains CSS2 and CSS3 selectors in plain English (or Spanish). Once you submitted a CSS code, it provides the description of what the style will apply to.</li> 
<li><a href="https://www.smashingmagazine.com/2009/07/13/css-3-cheat-sheet-pdf/">Printable CSS 3 Cheat Sheet (PDF)</a><br />This cheat sheet provides a complete listing of all the properties, selectors types and allowed values in the current CSS 3 specification from the W3C.</li>
<li><a href="https://www.smashingmagazine.com/2010/05/13/css-2-1-and-css-3-help-cheat-sheets-pdf/">CSS 2.1 and CSS 3 Help Cheat Sheets (PDF)</a><br />These cheat sheets contain most important properties, explanations and keywords for each CSS 2.1 and CSS 3 property.</li>
</ul> 

   <h3>Last Click</h3>
   <p><a href="https://www.modernizr.com/">Modernizr</a><br />A small and simple JavaScript library that allows you to use if-statements to check if a certain feature is available in the browser and gives you a fine level of control over older browsers that may not yet support these new technologies.</p>
<p class="showcase"><a href="https://www.modernizr.com/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbc78516-78b6-4ced-8944-10abcd9c5284/css3-techniques-13.jpg" width="480" height="300" alt="Modernizr" /></a></p>

   <h3>Will You Use CSS3 In Your Next Designs?</h3>

  <a href="https://polldaddy.com/poll/3358100/">Will you use CSS3 in your next designs?</a><span style="font-size:9px"><a href="https://polldaddy.com/features-surveys/">customer surveys</a></span>


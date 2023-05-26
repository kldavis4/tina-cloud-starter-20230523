---
title: The Principles Of Cross-Browser CSS Coding
slug: the-principles-of-cross-browser-css-coding
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c702df16-13da-4fb1-9d26-c37c3c5fa476/css-21.png
date: 2010-06-07T10:44:57.000Z
author: louis-lazaris
description: >-
  It is arguable that there is no goal in web design more satisfying than getting a beautiful and intuitive design to look exactly the same in every currently-used browser. Unfortunately, that goal is generally agreed to be almost impossible to attain. Some have even [gone on record](https://dowebsitesneedtolookexactlythesameineverybrowser.com/) as stating that perfect, cross-browser compatibility is not necessary. [Links checked & repaired March/06/2017]
categories:
  - Coding
  - CSS
  - Testing
  - Essentials
---

While I agree that creating a consistent experience for every user in every browser (putting aside mobile platforms for the moment) is never going to happen for every project, I believe <strong>a near-exact cross-browser experience is attainable</strong> in many cases. 

As developers, our goal should not just be to get it working in every browser; our goal should be to get it working in every browser with a minimal amount of code, allowing future website maintenance to run smoothly.</p>

In this article, I'll be describing what I believe are some of <strong>the most important CSS principles and tips</strong> that can help both new and experienced front-end developers achieve as close to a consistent cross-browser experience as possible, with as little CSS code as possible.

{{% feature-panel %}}

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/054da638-ce7e-4dff-99ae-5d7cd86fcf60/browsers-css.jpg" alt="Cross-Browser CSS" width="500" height="500" />

## Understand the CSS Box Model

This is one of the first things you should be thoroughly familiar with if you want to be able to achieve <strong>cross-browser layouts with very few hacks and workarounds</strong>. Fortunately, the box model is not a difficult thing to grasp, and generally works the same in all browsers, except in circumstances related to certain versions of Internet Explorer (more on this later).

The CSS box model is responsible for calculating:

*   How much space a block-level element takes up
*   Whether or not borders and/or margins overlap, or collapse
*   A box's dimensions
*   To some extent, a box's position relative to other content on the page

The CSS box model has the following basic rules:

*   Block-level elements are essentially rectangular (as are all elements, really)
*   The dimensions of a block element are calculated by width, height, padding, borders, and margins
*   If no height is specified, a block element will be as high as the content it contains, plus padding (unless there are floats, for which see below)
*   If no width is specified, a non-floated box will expand to fit the width of its parent minus padding (more on this later)

Some important things to keep in mind for dealing with block-level elements:

*   If a box has its width set to "100%", it shouldn't have any margins, padding, or borders, otherwise it will overflow its parent
*   Vertically-adjacent margins can cause some [complex collapsing issues](https://reference.sitepoint.com/css/collapsingmargins) that may cause layout problems
*   Elements positioned relatively or absolutely will behave differently, the details of which are extensive and beyond the scope of this article
*   The rules and principles above are stated under the assumption that the page holding the block-level elements is rendered in standards mode (this point was added later after review of the [comments posted](#comments))

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0f54309-26b4-4552-ab1d-d9d4ebc65d72/css-box-model.gif" alt="The Box Model as shown in Firebug" width="500" height="270" /><br>
<em>The box model as its displayed using Firebug in Firefox</em>

## Understand the Difference Between Block and Inline

For experienced developers, this is another no-brainer. It is, however, another crucial area that, when fully understood, will cause <a href="https://css-tricks.com/the-css-ah-ha-moment/">the light bulb to appear</a>, <strong>many headaches will be avoided</strong>, and you'll feel much more confident in creating cross-browser layouts.

The image below illustrates the difference between block and inline elements:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/027e0ec2-163e-4a04-9a4e-e08a5ea10f68/block-inline.jpg" alt="Block and Inline Elements" width="500" height="500" />

Here are some basic rules that differentiate block elements from inline:

*   Block elements will, by default, naturally expand horizontally to fill their parent container, so there's no need to set a width of "100%"
*   Block elements will, by default, begin at the leftmost edge of the parent box, below any previous block elements (unless floats or positioned elements are utilized; see below)
*   Inline elements will ignore width and height settings
*   Inline elements flow with text, and are subject to typographical properties such as `white-space`, `font-size`, and `letter-spacing`
*   Inline elements can be aligned using the `vertical-align` property, but block elements cannot
*   Inline elements will have some natural space below them in order to accommodate text elements that drop below the line (like the letter "g")
*   An inline element will become a block element if it is floated

## Understand Floating and Clearing

For multi-column layouts that are relatively easy to maintain, the best method is to use <a href="https://www.smashingmagazine.com/2009/10/19/the-mystery-of-css-float-property/">floats</a>. Having a <strong>solid understanding of how floats work</strong> is, therefore, another important factor in achieving a cross-browser experience.

A floated element can be floated either left or right, with the result that the floated element will shift in the specified direction until it reaches the edge of its parent container, or the edge of another floated element. All non-floated, inline content that appears below the floated element will flow along the side of the element that is opposite to the float direction.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1be04abe-ce76-49a2-8ab8-53d964ba8144/float-css.jpg" alt="A Floated Element" width="500" height="439" />

Here are some important things to keep in mind when floating and clearing elements:

*   Floated elements are removed from the flow of other block-level, non-floated elements; so in other words, if you float a box left, a trailing paragraph (block level) that's not floated will appear behind the float in the stack, and any text inside the paragraph (inline level) will flow around the float
*   To get content to flow around a floated element, it must be either inline or else floated in the same direction
*   A floated element without a declared width will shrink to the width of its content, so it's generally best to have a set width on a float
*   If a block element contains floated children, it will "collapse", [requiring a fix](https://www.sitepoint.com/blogs/2005/02/26/simple-clearing-of-floats/)
*   An element that's "cleared" will avoid flowing around floated elements above them in the document
*   An element that's both cleared and floated will only clear itself of elements that come before, not after

## Use Internet Explorer First (Or Don't)

<strong>Please note that Smashing Magazine's team strongly advises against developing websites in Internet Explorer first. In our opinion, sites should be developed in "modern" web-browsers, with standards first and then be tweaked for buggy versions of Internet Explorer. The advice below does not reflect the opinion of the Smashing Editorial team. Agree or disagree? Comment on this article!</strong>

Most of what I've discussed so far has to do with CSS coding and layout principles. This principle is more related to habits and preferences of most designers. Although we might hate to use IE6 and IE7 in our everyday internet activities, when it comes time to build a client project from scratch, one of the best things you can do is <strong>test your layout in those browsers early</strong> in development. You might even want to open up a <a href="https://www.my-debugbar.com/wiki/IETester/HomePage">standalone version of IE6 or IE7</a> and just start your development in that browser.

Of course, you won't have access to tools like Firebug, but generally for CSS (especially early in development) you won't need Firebug. It's much easier to get a layout working first in IE6 and IE7, then fix for other browsers, than to do it the other way around. Waiting until late in the development process to open up IE6 and/or IE7 will likely cause some, if not all, of the following problems:

*   Multiple hacks will be required, needing separate stylesheets for different versions of IE, making the code bloated and less maintainable and making the website slower
*   The layout in some spots may have to be reworked, multiplying development time
*   Testing time will increase, sometimes exponentially, leaving less time for more important tasks
*   The layout in other browsers will not be the same as in IE6 and IE7

I wouldn't expect developers to use Internet Explorer this aggressively for personal projects, web apps, or other non-client work. But <strong>for corporate clients</strong> whose user base is primarily on Internet Explorer, this tip could prevent a lot of headaches while getting things to work properly, and will definitely make a <strong>cross-browser experience much more likely</strong>.

Sometimes viewing IE's problems as "annoying bugs" can create unnecessary negativity, and can hinder development time and future maintenance. Dealing with IE is a fact of life for designers and developers, so just view its problems as you would any CSS issue — and build from there.

## Understand Internet Explorer's Most Common Problems

If you're going to start with IE in your development, or at the very least check your layout in IE early on, then you should understand what things Internet Explorer (usually versions 6 &amp; 7) has problems with, or what its limitations are.

A detailed discussion of every possible problem that can occur in Internet Explorer, and a list of <a href="https://www.smashingmagazine.com/2009/10/14/css-differences-in-internet-explorer-6-7-and-8/">all of its CSS compatibility issues</a> is certainly beyond this article. But there are some fairly significant inconsistencies and issues that come up in relation to IE that all CSS developers should be aware of. Here is a rundown of the most common problems you'll need to deal with:

*   IE6 will become problematic if floats are overused, causing (paradoxically) <span class="removed_link" title="https://haslayout.net/css/Disappearing-Content-Bug">disappearing content</span> or [duplicate text](https://www.impressivewebs.com/ie6-ghost-text-bug-with-multiple-solutions/)
*   IE6 will double the margin on floated elements on the side that is the same direction as the float; setting `display: inline` will often fix this
*   In IE6 and IE7, if an element [doesn't have layout](https://reference.sitepoint.com/css/haslayout), it can cause a number of problems, including backgrounds not showing up, margins collapsing improperly, [and more](https://www.satzansatz.de/cssd/onhavinglayout.html)
*   IE6 does not support min- and max-based CSS properties like `min-height`, or `max-width`
*   IE6 does not support fixed positioning of background images
*   IE6 and IE7 do not support many alternate values for the `display` property (e.g. `inline-table`, `table-cell`, `table-row`, etc.)
*   You cannot use the `:hover` pseudo-class on any element in IE6 except an anchor (`<a>`)
*   Certain versions of IE have [little support for certain CSS selectors](https://www.impressivewebs.com/buggy-css-selectors-cross-browser-jquery/) (e.g. attribute selectors, child selectors, etc.)
*   IE versions 6-8 have little support for CSS3, but there are [some workarounds](https://www.smashingmagazine.com/2010/04/28/css3-solutions-for-internet-explorer/)

There are many more bugs, issues, and inconsistencies that can arise in Internet Explorer, but these are probably the most common and most important ones to keep in mind when trying to create a cross-browser experience. I encourage all developers to <strong>do further research on many of the issues</strong> I've mentioned above in order to have a more accurate understanding of what problems these issues can cause, and how to handle them.</p>

## Some Things Will Never Look the Same

As already mentioned, creating the exact same experience visually and functionally in every browser is possible, but unlikely. You can get the layout and positioning of elements close to pixel-perfect, but there are <strong>some things that are out of the developer's control</strong>.</p>

### Forms Will Often Look Different

Discussing all the differences and quirks that occur with form elements across the different browsers and platforms could be an article in itself, so I won't go into extensive details here. A simple visual demonstration, however, should suffice to get the point across.

Take a look at the image below, which displays the <code>&lt;select&gt;</code> elements on the Facebook home page, as shown in 5 different browser versions (screenshots taken from Adobe's Browserlab):

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/344a2cb2-5696-4b83-97ad-97f71900d03b/forms-browsers.jpg" alt="The Facebook sign-up form in different browsers" width="500" height="331" /><br>
<em><code>&lt;select&gt;</code> elements appear differently in different browsers</em>

Some form elements can be controlled visually. For example, if the client requires that the submit button looks the same in every browser, that's no problem, you can just use an image, instead of the default <code>&lt;input type="submit"&gt;</code>, which, similar to <code>&lt;select&gt;</code> elements, will look different in different browsers.

But other form elements, like radio buttons, textarea fields, and the aforementioned <code>&lt;select&gt;</code> elements, are impossible to style in a cross-browser fashion without complicating matters using <span class="removed_link" title="https://widowmaker.kiev.ua/checkbox/">JavaScript plugins</span> (which some developers feel harm the user experience).</p>

### Typography Will Always Look Different

Another area in which we can't expect pixel-perfect designs is with regards to fonts, particularly fonts on body copy. <a href="https://www.smashingmagazine.com/2009/10/22/rich-typography-on-the-web-techniques-and-tools/">Different methods</a> have sprung up to help with custom fonts in headers, and the recently launched <a href="https://code.google.com/apis/webfonts/">Google Font API</a> will contribute to this. But body copy will probably always look different in different browsers.

With typography, we not only face the problem of font availability on different machines, but in some cases even when the font is available on two different machines, the type will look different. <a href="https://www.microsoft.com/typography/cleartype/tuner/step1.aspx">Windows ClearType</a>, for example, is available on IE7, but not on IE6, causing the same font to look different on two different versions of IE.

The graphic below displays screenshots from <a href="https://www.alistapart.com/">A List Apart</a> on IE6 and IE7. The grainy text in IE6 is more evident on the heading than in the body copy, but all text displays a marked difference between the two browsers (unless of course the text is an image):

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/769020c8-e762-4613-a81a-e071f3cb6b5c/cleartype-ie.jpg" alt="A List Apart's typography compared in IE6 and IE7" width="500" height="381" /><br>
<em>A List Apart's typography compared in IE6 and IE7</em>

## Use a CSS Reset

Ever since I started using a CSS reset for my projects, my <strong>ability to create a cross-browser experience has greatly increased</strong>. It's true that most resets will add unnecessary code to your CSS, but you can always go through and remove any selectors that you know will not be a factor (for example, if you don't plan to use the <code>&lt;blockquote&gt;</code> tag, then you can remove reference to it, and repeat this for any other unused tags).

Many of the margin- and padding-related differences that occur across different browsers become more normalized (even in troublesome HTML forms) when a CSS reset is implemented. Because the reset causes all elements to start from a zero base, you gain more control over the spacing and alignment of elements because all browsers will begin from the same basic settings.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f21ad7ef-6536-44d5-a38b-eeff97142799/reset-wd.jpg" alt="CSS Reset" width="500" height="319" /><br>
<em>A CSS reset as shown in Firefox's developer toolbar</em>

Besides the benefits of producing a cross-browser experience, a reset will also be beneficial because you won't use as many hacks, your code will be less bloated, and you'll be much more likely to create maintainable code. I recommend <a href="https://meyerweb.com/eric/tools/css/reset/">Eric Meyer's CSS reset</a>, which I've been using for quite some time now.</p>

## Use SitePoint's CSS Reference

If you're having trouble getting a particular CSS property to display correctly across all browsers, look up the property in the <a href="https://reference.sitepoint.com/css">SitePoint CSS Reference</a> to see if it has any compatibility limitations. SitePoint's reference (which is also available <a href="https://www.sitepoint.com/books/cssref1/">as a hard copy</a>, though not as up to date), includes a useful compatibility chart that displays browser support for every standard CSS property.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bec572b-0c5e-4a84-92e2-4700460c9b92/sitepoint-chart.jpg" alt="SitePoint's Compatibility Charts for CSS Properties" width="500" height="127" /><br>
<em>SitePoint's Compatibility Charts for CSS Properties</em>

Each compatibility chart is accompanied by a fairly detailed description of the bugs that occur in different browsers, and users are permitted to add comments to document new bugs that come up and to provide further explanations on complex CSS issues.

Using this as a guide, you can narrow down the possibilities, and can usually determine whether or not a CSS issue is due to a browser bug, or due to your own misapplication or misunderstanding of the CSS property in question.</p>

## Conclusion

While there is so much more that could be discussed on the topic of cross-browser CSS, the principles and guidelines I've introduced here should provide a foundation to assist CSS developers in creating as close to a consistent cross-browser experience as is currently possible. Cross-browser CSS is an attainable goal, within reasonable limits.

But, as an epilogue to this article, I also would like to concur with <a href="https://perishablepress.com/press/2010/01/11/css3-progressive-enhancement-smart-design/">those promoting the use of CSS3 with progressive enhancement</a>, and encourage developers to push new CSS techniques to the limits, even doing so, where possible, on client projects.

## Further Reading

*   [CSS Differences in Internet Explorer 6, 7 and 8](https://www.smashingmagazine.com/2009/10/css-differences-in-internet-explorer-6-7-and-8/)
*   [Using CSS3: Older Browsers And Common Considerations](https://www.smashingmagazine.com/2011/05/using-css3-older-browsers-and-common-considerations/)
*   [How To Support Internet Explorer and Still Be Cutting Edge](https://www.smashingmagazine.com/2009/12/how-to-support-internet-explorer-and-still-be-cutting-edge/)

The principles I've introduced here should help developers create a beautiful and intuitive experience in IE, while providing an <em>extra</em>-beautiful and <em>super</em>-intuitive experience in the more up-to-date browsers. That's a cross-browser goal that is definitely worth striving for.


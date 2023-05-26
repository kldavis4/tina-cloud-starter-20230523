---
title: 'Fixed vs. Fluid vs. Elastic Layout: What’s The Right One For You?'
slug: fixed-vs-fluid-vs-elastic-layout-whats-the-right-one-for-you
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdbc19a4-e876-47df-8f64-36257cd26669/illulayout41.gif
date: 2009-06-02T19:02:42.000Z
author: newsletter-team
description: >-
  The problem has boggled the minds of Web designers for years: fixed, fluid, elastic or a hybrid layout design? Each option has its benefits and disadvantages. But the final decision depends so much on usability that it is not one to be made lightly. So, with all the confusion, **is there a right decision?** By considering a few factors and properly setting up the final design, you can end up with a successful layout design that reaps all the benefits.
categories:
  - Coding
  - Layouts
  - CSS
---
This article discusses the pros and cons of each type of layout. Either one can be used to make a successful website layout, as long as you keep usability in mind.

Why all the debate? Web page design comes down to usability, and this can be difficult to balance because website users can account for many different variables among them.

{{% feature-panel %}}

When designing a website layout for a large audience, the designer must consider the <strong>following potential differences among visitors:</strong>

*   Screen resolution,
*   Browser choice,
*   Whether or not the browser is maximized,
*   Extra toolbars open in the browser (History, Bookmarks, etc.),
*   Even the operating system and hardware.

Without the benefit of a standardized website size to work with, Web designers encounter numerous problems when it's time to get to work.</p>

## 1\. Difference Between Fixed And Fluid Layouts

Although most designers and developers would consider defining fixed and fluid website layouts to be elementary, we'll go over it just to be clear.</p>

### Fixed Website Layouts

A fixed website layout has a wrapper that is a fixed width, and the components inside it have either percentage widths or fixed widths. The important thing is that the container (wrapper) element is set to not move. No matter what screen resolution the visitor has, he or she will see the same width as other visitors.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3ccabfb-1f1d-42f8-b3a6-f0dca9679655/fixed.jpg" alt="Fixed Website Layout" /></figure>

The image above shows the general outline of a fixed-width website layout. The components inside are fixed to 520, 200 and 200 pixels, respectively. A 960-pixel width has become the standard in modern Web design because most website users are assumed to browse in 1024x768 resolution or higher.</p>

### Fluid Website Layouts

In a fluid website layout, also referred to as a liquid layout, the majority of the components inside have percentage widths, and thus adjust to the user's screen resolution.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bfc16df-3bb6-42b2-9076-7a8f4daef4d2/fluid.jpg" alt="Fluid Website Layout" /></figure>

The image above shows a fluid (liquid) website layout. While some designers may give set widths to certain elements in fluid layouts, such as margins, the layout in general uses percentage widths so that the view is adjusted for each user.</p>

## 2\. Fixed Web Page Design

Many designers prefer fixed layouts to fluid ones because they're easier to make and provide more assurance that <strong>what the designer sees, the user sees.</strong> However, the pros and cons come out even with fluid-layout design.

### Pros

*   Fixed-width layouts are much easier to use and easier to customize in terms of design.
*   Widths are the same for every browser, so there is less hassle with images, forms, video and other content that are fixed-width.
*   There is no need for min-width or max-width, which isn't supported by every browser anyway.
*   Even if a website is designed to be compatible with the smallest screen resolution, 800x600, the content will still be wide enough at a larger resolution to be easily legible.</p>

### Cons

*   A fixed-width layout may create excessive white space for users with larger screen resolutions, thus upsetting "divine proportion," the "Rule of Thirds," overall balance and other design principles.
*   Smaller screen resolutions may require a horizontal scroll bar, depending the fixed layout's width.
*   Seamless textures, patterns and image continuation are needed to accommodate those with larger resolutions.
*   Fixed-width layouts generally have a lower overall score when it comes to usability.</p>

### Examples of Fixed-Page Design

Here are five examples from designers who get the most out of fixed-width layouts. These websites incorporate many design elements, a <strong>perfect scenario in which to use a fixed layout</strong>. The designers have more control over the placement of extra design elements around the content areas and can work with the content and navigation widths more precisely.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9db8aeef-9f6c-4259-85bb-c6e10fdb4ef8/fixed1.jpg" alt="Lebloe.Com" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b15d963-ddf6-4afc-a8c5-cff8404a992b/fixed2.jpg" alt="Corvus Art Design Studio" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6c44e82-36ef-4732-a1b9-b116bb9a8c47/fixed3.jpg" alt="Nathan-Sanders.Com" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9afc50bc-cec2-43fa-819a-a093b66bf603/fixed4.jpg" alt="Nine Lion Design" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4961e9e7-f33f-4174-b36b-c5edc51934eb/fixed5.jpg" alt="Colour Pixel" /></figure>

Notice how in all of these examples, the designers use continuous imagery to work with larger screen resolutions.</p>

## 3\. Getting Around The Cons Of Fixed Web Page Design

If you've decided on a fixed page design, you should know these few tricks to get around the cons of this layout and create a successful design.</p>

### Looking at the Statistics

Today, most designers assume that the majority of Internet users have a screen resolution of 1024x768 or higher. According to <a href="https://www.w3schools.com/browsers/browsers_display.asp">a poll published by W3Schools</a>, this is not the case (please notice that one should take the W3Schools statistics with a grain of salt, more details about it follow below):

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4bea9be-76e0-4c08-aebd-560d85c91406/piechart.jpg" alt="Screen Resolution Pie Chart" /></figure>

As you can see, 640x480 doesn't even register on the chart. W3Schools' analysis found a whopping 0% of users have this screen resolution. While, in fact, some users actually do have this screen resolution, the statistics show that they make up a small enough percentage that designers should be able to ignore the size and still offer wide usability.

Even for people who do use this resolution size, they probably use it mainly on smaller portable computers and wouldn't use it as their primary screen resolution normally.

However, these statistics are probably <strong>not as accurate</strong> as one might hope. Because W3Schools' visitors primarily belong to a certain demographic (designers and developers), the information is a little biased. Other research sources show different findings, but only slightly different. According to resolution statistics from individual companies in 2009, the 800x600 screen resolution showed up at somewhere under 10% of users.

This next interesting table comes from SohTanaka.com, whose blogger has done a bit of research comparing how some of the largest websites accommodated screen resolutions in February 2006 versus February 2008.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b1518c5-f3ab-4290-b363-709b215a0c49/topsiteaccomodations.jpg" alt="Screen Resolution Accommodations of some top websites." /></figure>

For all four major websites in the study, there was a complete turnaround. Even the biggest companies on the Web are now assuming that their audiences have larger screen resolutions.

For other research on screen resolution, have a look through the sources below:

*   [W3Counter](https://www.w3counter.com/globalstats.php),
*   [OneStat.com](https://www.onestat.com/html/aboutus_pressbox31.html).</p>

### 960px or 760px?

All this being said, <strong>most designers choose a fixed width of either 960 or 760 pixels</strong>. A layout 960 pixels wide looks good for users with a 1024x768 resolution or above, with a bit of room for margins. For designers who want to accommodate the approximately 10% of users with a 800x600 screen resolution, the 760-pixel-wide layout works well, and is still suitable for larger screens.</p>

### Always Center the Layout

When working with a fixed width design, be sure to at least center the wrapper div to maintain a sense of balance (<code>margin: 0 auto;</code> usually does the trick). Otherwise, for users with large screen resolutions, the entire layout will be tucked away in the corner.</p>

## 4\. Fluid Web Page Design

Designers may not use fluid page designs for various reasons, but the layout's benefits are often overlooked. Below are pros and cons to think about when considering fluid web page design.</p>

### Pros

*   Fluid web page design can be more user-friendly, because it adjusts to the user's set up.
*   The amount of extra white space is similar between all browsers and screen resolutions, which can be more visually appealing.
*   If designed well, a fluid layout can eliminate horizontal scroll bars in smaller screen resolutions.</p>

### Cons

*   The designer has less control over what the user sees and may overlook problems because the layout looks fine on their specific screen resolution.
*   Images, video and other types of content with set widths may need to be set at multiple widths to accommodate different screen resolutions.
*   With incredibly large screen resolutions, a lack of content may create excess white space that can diminish aesthetic appeal.</p>

### Examples of Fluid Page Design

Below are two designs that use percentage widths to accommodate different screen resolutions. The first example in each set alters the width of the content according to screen width, while the second screenshot uses varying widths for the white space.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72ddad3c-6950-4629-b9ec-f840a2abe692/fluid1-large.jpg" alt="Simple Bits" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39d7d131-543a-42f7-bc62-dc430e6bb5ff/fluid1-small.jpg" alt="Simple Bits" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e543afc-9071-4b8b-94c3-98feac3e0cba/fluid2-large.jpg" alt="Blossom Graphic and Web Design Boutique" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a14909d-6254-4301-809c-d78ee63370db/fluid2-small.jpg" alt="Blossom Graphic and Web Design Boutique" /></figure>

## 5\. Getting Fluid Web Page Design To Work

Even though fluid layouts can present a few problems, some of those problems can be overcome with a few tricks.</p>

### Use Simple Design

The less a fluid Web design depends on <strong>graphics and difficult techniques</strong>, the easier it will be to create and maintain. It will also be more compatible with alternate screen resolutions. With cleaner code and design, compatibility problems are more easily prevented, found and dealt with.

Smashing Magazine, for example, uses a fluid Web page layout, and to make it simple only the top black-and-orange navigation bar expands, depending on the user's situation. Otherwise, the content area expands and contracts as needed, and smart use of CSS covers situations in which the sidebar and internal content could clash.</p>

### Min-width and Max-width

Two CSS properties, min-width and max-width, can be used to create a fixed width if the user's screen is too small or too big for the layout to be usable. In this case, the layout gets a scroll bar and functions essentially as a fixed-width layout. Look over W3Schools' pages on the min-width and max-width CSS properties below for more details:

*   [W3Schools' page on the max-width CSS property](https://www.w3schools.com/cssref/pr_dim_max-width.asp),
*   [W3Schools' page on the min-width CSS property](https://www.w3schools.com/cssref/pr_dim_min-width.asp).

Unfortunately, most versions of Internet Explorer don't support min-width and max-width. Getting around this is simple, though, with an IE-specific expression. Read more about that in the article <a href="https://perishablepress.com/press/2007/01/16/maximum-and-minimum-height-and-width-in-internet-explorer/">Maximum and Minimum Height and Width in Internet Explorer</a>.</p>

## 6\. Elastic Design

There is a third option when working with Web page layouts. An elastic design is sometimes preferred by designers because it <strong>mixes the two other main layout types</strong>. It works by sizing all elements with <tt>em</tt>'s. The quote below explains exactly what an <tt>em</tt> is and why it can be beneficial.
<blockquote>"A pixel is an unscalable dot on a computer screen, whereas an em is a square of its font size. Because font sizes vary, the em is a relative unit that responds to users’ text-size preferences."
- <a href="https://www.alistapart.com/articles/elastic">Patrick Griffiths, A List Apart</a></blockquote>

While elastic design is supposed to offer more benefits, it still has its pros and cons like the other two layout styles.</p>

### Pros

*   If implemented correctly, this layout style can be very user-friendly. The goal is to have everything grow larger or smaller in proportion with the user's preference.
*   Elastic layouts are perfect for designers who love both fluid and fixed designs, because the pros of each are found in elastic layouts.</p>

### Cons

*   Even given the first pro above, this type of layout can create a huge problem with usability. It takes a lot of savvy and testing to get the layout right for all users.
*   This type of layout is much more difficult to create than the other two, and the extra bit of usability it brings may not always seem worth it.
*   Depending on the specifics of the layout, some elastic designs may require supplementary style sheets and cheats for IE6.</p>

### Examples of Elastic Page Design

Elastic and fluid layouts are incredibly similar in appearance, so much so that they are usually confused with each other. However, elastic designs use <tt>em</tt>'s instead of percentages and depend primarily on font size. These designs adjust to the text size that users set for their browser.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/502e4a76-14ab-41f3-9612-d9ee540fa87d/elastic1-large.jpg" alt="Clear Left" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef72fe48-aa26-4505-a6d3-41062a7c1139/elastic1-small.jpg" alt="Clear Left" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e40c68a-9d3e-45de-aa6c-eb21e61a2631/elastic2-large.jpg" alt="Mirella Furlan" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3616a232-f38a-4253-a2e0-487f15878d7e/elastic2-small.jpg" alt="Mirella Furlan" /></figure>

## 7\. Which Is Right For Your Website?

Choosing between a fixed and fluid website will depend a lot on the type of website itself. Weigh the pros and cons above to determine the right solution for your website.

A portfolio website, for example, would probably be best shown in a fixed-width layout, so that you have more control over the design. Not only will you be able to better control the layout of individual elements in the design, but the images in your portfolio showcase will be better handled with a fixed width. Many designers, not just those with portfolios, may prefer fixed-width layouts for the <strong>ease of use and assurance it gives them</strong>.

Any designer who seeks <strong>100% compatibility</strong> should take the time to set up a fluid layout. In such a case, the main challenge isn't the excess of white space in large screen resolutions, but rather the small percentage of users with a small screen resolution. For websites with large audiences, accommodating even the smallest percentage of users may be important. But even beyond that, websites with large audiences should have a simple and clean design anyway, which can be done effectively with a fluid layout.

Still can't decide? An elastic or partially elastic design is still an option. When used correctly, elastic layouts can bring the biggest benefits of both other types&lt;. Designers will often employ the elastic-layout principle in using <tt>em</tt>'s for fonts and containers, and then use a smart mix of percentages and pixel widths to set the rest of the layout elements.</p>

### What Other Designers Say

Comment by Heidi Cool on <a href="https://cuwebd.ning.com/forum/topic/show?id=1763934%3ATopic%3A22003">Fixed vs. Liquid vs. Elastic Layout</a>
This designer makes some great points about working with other people who will be using the layout and may not know as much about Web design:
<blockquote>"I go back and forth on this issue. We use a fixed width at case.edu because:
<ol>
 	<li>Liquid is more complicated, and <strong>we distribute templated designs to users of varying skills who might easily break a liquid layout</strong>. (They're actually regular HTML files rather than Dreamweaver templates.)</li>
 	<li>We want to ensure our maintainers don't build pages with line lengths that are too long and thus harder to read.</li>
 	<li>We try to limit the space available because <strong>people have a tendency of filling up whatever space is available</strong>. If they have large monitors they could really overcrowd a page not realize how messy it gets on smaller displays.</li>
</ol>
As you can see the bulk of these issues relate to the fact that our sites are distributed and built and maintained by people of varying skill levels. If I were working on one site alone and I was doing the coding, then I'd base the decision on goals, content, etc."</blockquote>

Comment by madr on <a href="https://www.sitepoint.com/blogs/2009/04/17/flexible-designs-dying-ou">Where Have All the Flexible Designs Gone?</a>
Two more good points are made here about using fixed-width layouts:
<blockquote>"<strong>Banners and ads are usually made with images and Flash movies</strong>, making it harder to do an elastic or flexible design. I have worked in the newspaper world for a year and a half, and the ads really are a holy cow in these areas. So are article images, for which an elastic layout would make the viewing area too big for the top image.

Every browser but Safari 3 and below (Safari 4 is coming), Firefox 2 and below and IE6 and below (which are to be viewed as obsolete/deprecated soon) <strong>have support for page zoom instead of text resizing</strong>, making the time to accomplish a flexible and elastic design hard to justify since the majority of the visitors won’t even notice it."</blockquote>

Comment by jphilapy on <a href="https://www.sitepoint.com/blogs/2009/04/17/flexible-designs-dying-ou">Where Have All the Flexible Designs Gone?</a>
Two good points in support of fluid-width layouts:
<blockquote>"Flexible sites can be made to work at many resolutions. There is no need for heated debates or research about user screen sizes. Besides, screen resolution statistics are a myth; <strong>few people run their browser full-screen and many have toolbars, sidebars, or other widgets</strong> that use valuable screen estate.

Mobile phones, such as the iPhone, and games consoles are becoming viable alternatives for web browsing. In general, these devices have smaller resolutions and can benefit from flexible web designs."</blockquote>

Comment by Calrion on <a href="https://www.456bereastreet.com/archive/200504/about_fluid_and_fixed_width_layouts">About Fluid- and Fixed-Width Layouts</a>
Clear case for using elastic designs:
<blockquote>"I think the ‘elastic’ layout is the best option. <strong>Fluid to a point</strong>, then fixed to ensure lines of text, etc., don’t become ridiculously long.

I’m a Windows user, and I maximize.

Mostly, I maximize because I can get the best look at whatever app I’m using, and because I generally have large amounts of detritus on my desktop. Additionally, maximizing my browser (Firefox) allows the maximum space for interface elements, specifically the links toolbar and tabbed area.

In terms of usability, <strong>fluid is probably best for savvy users</strong>, as their browser width is in control. <strong>For less experienced users, elastic is probably best</strong>, as it will automatically stop itself from becoming too wide."</blockquote>

Comment by Georg on <a href="https://www.456bereastreet.com/archive/200504/about_fluid_and_fixed_width_layouts">About Fluid- and Fixed-Width Layouts</a>
An explanation of how one designer uses a mix of all three to get the best results:
<blockquote><strong>"Fluid main part, fixed sidebars and (maybe) some elastic parts</strong> is my preferred layout method. I always keep text areas within 600px max-width though, and hack IE/win.

Using min/max for the whole page, so it’ll stay within 600 - 1200px and centers above. The same hacks for IE/win.

Testing everything on 600 to 2400 wide screens, and leave the rest to each visitor. Text lines will not get too wide (600px max), and the page doesn’t break too early under stress.

Most comments I get are that <strong>visitors don’t notice anything that really disturbs them</strong>, and that it makes easy read. Guess that means that it’s a <strong>working compromise</strong>.

Your site works fine for me, so I’ll call it a good compromise. My old eyes say the text is a bit too small, so I zoom it to 200% in Opera on a 1280 screen. No problems whatsoever."</blockquote>

## Further Resources

You may also be interested in these extra references:

- [Responsively Retrofitting An Existing Site With RWD Retrofit](https://www.smashingmagazine.com/2013/03/18/retrofit-a-website-to-be-responsive-with-rwd-retrofit/)
- [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
- [Responsive Web Design Techniques, Tools and Strategies](https://www.smashingmagazine.com/2011/07/responsive-web-design-techniques-tools-and-design-strategies/)
- [The State Of Responsive Web Design](https://www.smashingmagazine.com/2013/05/the-state-of-responsive-web-design/)
- [Design Process In The Responsive Age](https://www.smashingmagazine.com/2012/05/design-process-responsive-age/)

{{< signature "al" >}}


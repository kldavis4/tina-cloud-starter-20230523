---
title: Applying Divine Proportion To Your Web Designs
slug: applying-divine-proportion-to-web-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91c315f7-772f-4632-b029-86c667d20427/divine.png
date: 2008-05-29T15:51:05.000Z
author: vitaly-friedman
description: >-
  [Effective web
  design](https://www.smashingmagazine.com/2008/01/10-principles-of-effective-web-design/)
  doesn't have to be pretty and colorful — it has to be clear and intuitive; in
  fact, we have analyzed the [principles of effective
  design](https://www.smashingmagazine.com/2008/04/24/5-more-principles-of-effective-web-design/)
  in our previous posts. However, how can you achieve a clear and intuitive
  design solution? Well, there are a number of options — for instance, you can
  use grids, you can prefer the simplest solutions or you can focus on
  usability. However, in each of these cases you need to make sure your visitors
  have some natural sense of order, harmony, balance and comfort. And this is
  exactly where the so-called _Divine proportion_ becomes important.
categories:
  - Design
  - Web Design
  - Layouts
  - Mathematics
---
<a href="https://www.smashingmagazine.com/2008/01/10-principles-of-effective-web-design/">Effective web design</a> doesn't have to be pretty and colorful — it has to be clear and intuitive; in fact, we have analyzed the <a href="https://www.smashingmagazine.com/2008/04/24/5-more-principles-of-effective-web-design/">principles of effective design</a> in our previous posts. However, how can you achieve a clear and intuitive design solution? Well, there are a number of options — for instance, you can use grids, you can prefer the simplest solutions or you can focus on usability. However, in each of these cases you need to make sure your visitors have some natural sense of order, harmony, balance and comfort. And this is exactly where the so-called <em>Divine proportion</em> becomes important. 

This article <strong>explains what is the Divine proportion and what is the Rule of Thirds</strong> and describes how you can apply both of them effectively to your designs. Of course, there are many possibilities. Hopefully, this post will help you to find your way to more effective and beautiful web designs or at least provide some good starting points you can build upon or develop further.

You may want to take a look at the following related post:

*   [Applying Mathematics To Web Design](https://www.smashingmagazine.com/2010/02/applying-mathematics-to-web-design/)

## Divine Proportion

Since the Renaissance, many artists and architects have proportioned their works to approximate the golden ratio — especially in the form of the golden rectangle, in which the ratio of the longer side to the shorter is the golden ratio. The rationale behind it is the belief that this proportion is organic, universal, harmonic and aesthetically pleasing. Indeed, being evident everywhere in the universe (in fact, many things around us can be expressed in this ratio), divine proportion (which is also called Golden ratio, divine section, golden cut and mean of Phidias) is probably the most known law of proportion which can <strong>dramatically improve the communication of your design</strong>.

{{% feature-panel %}}

As Mark Boulton states in his article <em>Design and the Divine Proportion</em>, "one of the key components in the vehicle of communication is composition, and in design schooling it is something that is taught as something you should <em>feel</em> rather than create logically." Hence, to comfort your visitors with a pleasing and intuitive composition it is often worth considering the Golden ratio. So what exactly is Golden ratio? Basically, it is a proportion <strong>1.618033988749895 ≈ 1.618</strong> which holds between objects placed within some context.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0aabdf3-f03f-4139-a037-66d7e6274c6c/divine.gif" alt="Divine Proportions" width="500" height="486" />

Consider the example above. You would like to create a fixed width layout. The width of your layout is 960px. You would to have a large block for your content (<code>#content</code>) and a smaller block for your sidebar (<code>#sidebar</code>). How would you calculate the widths of your columns?

1.  First, calculate the width of your `#content`-block. You need to make sure that the ratio between this block and the overall layout width is 1.62\. Hence you divide 960px by 1.62 which results in approximately 593px.
2.  Subtract 593px from the overall layout width (which is 960px) and get 960px - 593px = 367px.
3.  Now if you calculate the ratio between the `#content`-block and the `#sidebar`-block (593px : 367px ≈ 1.615) and the ratio between the container-width and the width of the content-block (960px : 593px ≈ 1.618) you have achieved almost the same ratio.

This is the whole idea behind the "Golden" proportion. The same holds for fluid and elastic layouts, too.

Of course, a web design doesn't <em>need</em> to be organized according to the Divine proportion. However, in some cases it can improve not only the communication of your design, but also <strong>improve further details of your layouts</strong>. As an example consider The 404 Blog. The design itself is visually appealing, provides calm and supporting color scheme and has a nice composition.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7102fcdc-8849-4991-81b8-f0b1916ddfd9/404user1.jpg" width="500" height="439" />

However, the design does not correspond to the Divine proportion as you can see from the image below. Actually, users don't necessarily feel it, because they intuitively split the layout in two separate blocks of the width 583px (630px - 31px - 31px) and 299px (330px - 31px). The reason behind it is that white space of the main area is <em>passive</em> (three columns, each 31px wide), it clearly supports the content next to it rather than being the content itself.

The ratio between the layout blocks is 630 : 330 px ≈ 1.91 ≠ 1.62, and the ratio between the content blocks is 583 : 299px ≈ 1.92 ≠ 1.62. The reason why the layout looks almost perfect although it doesn't stick to the Divine proportion is the simple fact that it is <strong>balanced</strong> — both the layout blocks and the content blocks have the same proportion. Hence the design provides some sense of closure and structural harmony.

The interesting thing is, however, that due to a suboptimal layout length visitors are offered a suboptimal text length of over 90 symbols per line. However, an optimal number for comfortable reading lies between 60 and 80 symbols per line. The improvement of the layout would therefore lead to the improved readability of the content, too. That's a useful side-effect of getting things done according to the laws of nature.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcdf9575-9fc7-4ffb-aef5-18ae76153d0b/404user2.jpg" width="494" />

For some quick'n'dirty drafts you may use the ratio <em>5 : 3</em> which is not exactly the Divine proportion, but can turn out to be a useful <strong>rule of thumb</strong> in case you don't have a calculator near you. Divine proportion usually provides bulletproof values one can perfectly incorporate in almost every design. When working on your next project you may want to consider using the following tools to calculate the widths "on the fly":

*   [Phiculator](https://www.thismanslife.co.uk/phiculator) Phiculator is a simple tool which, given any number, will calculate the corresponding number according to the golden ratio. The free tool is available for both Win and Mac.
*   [Golden Section Ratio Design Tool](https://www.atrise.com/golden-section/) Atrise Golden Section is a program, which allows avoiding the routine operations, calculator compilations, planning of grouping and forms. You can see and change the harmonious forms and sizes, while being directly in the process of working on your project.</p>

## The Rule of Thirds

Basically, the Rule of Thirds is a simplified version of the Golden ratio and as such poses a compositional rule of thumb. Dividing a composition into thirds is an easy way to apply divine proportion without getting out your calculator.

It states that every composition can be divided into <strong>nine equal parts</strong> by two equally-spaced horizontal lines and two equally-spaced vertical lines. The four points formed by the intersections of these lines can be used to place the most important elements — the elements you'd like to give a prominent or dominant position in your designs. Aligning a composition according to Rule of thirds creates more tension, energy and interest in the composition than simply centering the feature would.

<a href="https://en.wikipedia.org/wiki/Rule_of_thirds"><img style="filter: url('#toggleGifsIndicatorFilter');" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db28632b-3b6e-4049-8b3b-beddbeb2a445/thirds.gif" alt="Rule of Thirds" width="307" height="307" /></a><br>
<em>This photograph demonstrates the principles of the rule of thirds. Source: <a href="https://en.wikipedia.org/wiki/Rule_of_thirds">Wikipedia</a></em>

In most cases it is neither possible nor useful to use all four points to highlight the most important functions or navigation options in a design. However, you can definitely use some of them (usually one or two) to properly place the most important message or functionality of the site. The <strong>left upper corner is usually the strongest one</strong>, since users scan web-sites according to the "F"-shape.

So how do you split a layout into 9 equal parts? Jason Beiard <a href="https://www.sitepoint.com/article/principles-beautiful-web-design/3">states</a> the following method for applying the Rule of Thirds to your layouts:

1.  To start the pencil-and-paper version of your layout, draw a rectangle. The vertical and horizontal dimensions don't really matter, but try to keep straight lines and 90-degree angles.
2.  Divide your rectangle horizontally and vertically by thirds.
3.  Divide the top third of your layout into thirds again.
4.  Divide each of your columns in half to create a little more of a grid.
5.  You should have a square on your paper that looks similar to the rule of thirds grid.

Let's consider the following situation. Assume you have a layout of fixed width 960px. Consider the area above the fold which is likely to have the height between 750 and 950px.

1.  Divide the width of your layout by 3\. In an example you get 960px / 3 = 320px.
2.  Divide the height of your layout by 3\. In an example you get ( (750 + 950 px) / 2 ) / 3 ≈ 285px.
3.  Each rectangle should have the size of 320px × 285px.
4.  Construct the grid of the rectangles described in step 4 by drawing lines going through the ends of rectangles.
5.  Place the most significant elements of your designs in the meeting points of horizontal and vertical lines.

Consider the design of demandware.com presented below. Although the design uses a number of vibrant colors, it is not noisy and seems to be both simple and clear. The navigation options are clearly visible and the structure of the site seems to be easy to scan.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22eb9dc8-cf56-46c5-a571-c2811ee9eac6/demand.jpg" alt="Rule of Thirds" width="495" height="420" />

However, if you consider the effectiveness of this design, you might find a perfect balance the design actually has. Indeed, it almost perfectly uses the Rule of Thirds as two out of four intersections of the lines (pink blocks in the picture below) <strong>contain exactly the information which the company wants its users to see</strong> — namely what the site is all about and an example of their work. Note also how perfectly the main sections are placed on the second horizontal axis. That is effective.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf53423d-85ce-4f30-a4fa-ffacc6c6b542/demandw.jpg" alt="Rule of Thirds" width="496" height="422" /><br>
<em>Rule of Thirds in use: two out of four intersections of the lines (pink blocks) contain exactly the information which the company wants its visitors to see.</em>

## Summary

In some cases, applying the Divine proportion and the Rule of Thirds may significantly improve the communication of your design to your visitors. Offering your users an almost natural balance in proportion 1 : 1.62 you literally <strong>impose the natural order</strong> on it and force your design layout to become more scannable and well-structured.

Using the Rule of Thirds you can also effectively highlight important functions of your site providing your visitors with a design they can easily work with and effectively delivering the message you want to deliver in the first place.


---
title: 'Typeplate: A Starter Kit For Beautiful Web Type'
slug: typeplate-for-beautiful-web-type
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d86145cd-86b4-472e-be0a-afd2cc9f411d/typo-2.jpg
date: 2013-02-28T02:14:06.000Z
author: zachary-kain
description: >-
  As of today we’re pleased to announce [Typeplate](https://typeplate.com), a free-range and open-source typographic starter kit that will hopefully help
  you build beautiful, text-rich websites. The word on the street is that the Web Is 95% Typography, so as we hurtle towards the future, we think there’s
  still a lot we can learn from five centuries of history
  "Typeplate: A Starter Kit For Beautiful Web
  Type")](https://www.smashingmagazine.com/2013/02/27/typeplate-for-beautiful-web-type/)
categories:
  - Freebies
  - Typography
  - Fonts
---
As of today we’re pleased to announce <a href="https://typeplate.com">Typeplate</a>, a free-range and open-source typographic starter kit that will hopefully help you build beautiful, text-rich websites. The word on the street is that the <a href="https://informationarchitects.net/blog/the-web-is-all-about-typography-period">Web Is 95% Typography</a>, so as we hurtle towards the future, we think there’s still a lot we can learn from five centuries of history. Typeplate is the result of this exploration of our typographic heritage.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02727de8-331f-4d7c-97a4-4917013c76e7/typeplate-t.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a469561d-5fc2-4e77-8d3b-8304f5ed5343/typeplate-logo-450px.png" alt="TypePlate" width="450" height="450" /></a>

## “Another Framework?”

We made Typeplate because we weren’t satisfied with existing Web frameworks. The problem with most frameworks is that they make <strong>too many assumptions</strong> about how you’re going to work. This can be helpful, but you’re often forced to code <em>their</em> way or find another framework — there’s a lot of 'framework fatigue' out there.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Mind Your En And Em Dashes: Typographic Etiquette](https://www.smashingmagazine.com/2011/08/mind-your-en-and-em-dashes-typographic-etiquette/)
*   [Macrotypography For A More Readable Web Page](https://www.smashingmagazine.com/2012/05/applying-macrotypography-for-readable-web-page/)
*   [How To Choose A Typeface — A Step-By-Step Guide!](https://www.smashingmagazine.com/2011/03/how-to-choose-a-typeface/)
*   [Respect Thy Typography](https://www.smashingmagazine.com/2012/03/respect-thy-typography/)

{{% feature-panel %}}

Pattern libraries are helpful but they rarely separate structure from aesthetics, which leads to projects looking generic unless you sink a lot of time into re-working all the patterns. We’re building websites in 2013! There is no reason we have to sacrifice customization and modularity in order to achieve beautiful, powerful results.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d754313-ed83-4791-943d-6016718143ff/typeplate-press.png"><img loading="lazy" decoding="async" class="156184" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49f4932c-d711-400b-a18e-b266b8620511/typeplate-press-500.png" alt="typeplate-press-500" width="500" height="295" /></a><br>
<em>With Typeplate, you can combine solid typographic conventions of the past with flexible styles of the presence. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d754313-ed83-4791-943d-6016718143ff/typeplate-press.png">Larger view</a>.</em>

## How It Works

So what does Typeplate do? As a <strong>“starter kit”</strong>, the library makes no assumptions about how you write code — <em>at all</em>. We went way back to basics, inspired by Harry Roberts’ <a href="https://inuitcss.com">inuit.css</a> and other OOCSS projects. Typeplate lets you set solid base styles and include conventional typographic features (e.g. block quotes and drop capitals) built with good markup and flexible styling.

Typeplate isn’t the next Bootstrap or Foundation; we're building a toolkit for Web type that’s meant to be extended and customized. There’s no reason we have to sacrifice customization and modularity in order to achieve beautiful, powerful results.

Typeplate is built with <a href="https://www.smashingmagazine.com/2011/09/an-introduction-to-less-and-comparison-to-sass/">Sass</a> and borrows heavily from <a href="https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/">Object-Oriented CSS</a> techniques. A key feature is that Typeplate is 100% à la carte: it takes just 3 Kb of CSS to integrate the entire project, but you can cherry-pick only the elements you need and just delete the rest. There is a plain CSS version of Typeplate available (and actively being improved), but if you want to take advantage of all the heavy lifting, you probably will want to work with Sass: Typeplate generates CSS with lots of variables and functions, letting you concentrate on implementing features, not typing them out. For example, our <a href="https://www.smashingmagazine.com/2016/05/fluid-typography/">Typographic Scale</a> loop generates 53 lines of code to create a full <a href="https://csswizardry.com/2012/02/pragmatic-practical-font-sizing-in-css/">double-stranded heading hierarchy</a> from just three variables and some font sizes.</p>

## Demo And Downloads

*   [Live demo page](https://typeplate.com/demo.html)
*   [Examples and Documentation](https://typeplate.com/)
*   [Download the source files](https://typeplate.com) (in both Sass and CSS flavors, 3 Kb compressed, 17 Kb raw)
*   [Github Repo](https://github.com/typeplate/typeplate.github.com)

## How To Use It

Easy. To use Typeplate, simply <code>@import "&#95;typeplate.scss"</code> in your project’s main Sass file, preferably after a reset like Normalize. By default, Typeplate sets base styles on the <code>html</code>, <code>body</code>, <code>h1</code>–<code>h6</code>, <code>pre</code>, <code>code</code>, and <code>abbr</code> elements — you’ll want to start tweaking the variables before adding new styles. Don’t forget that you can always delete those sections and use the mixins in your own stylesheet instead.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62acca0f-d641-4e34-a033-57db260a5ab6/typeplate-kit-450px.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62acca0f-d641-4e34-a033-57db260a5ab6/typeplate-kit-450px.png" alt="TypePlate" width="450" height="450" /></a>

As the project matures, we'll most certainly be updating the page and blogging about what we've learned during development as well as posting better demos and documentation. We would appreciate your help in making Typeplate better, so please fork, pull-request and <a href="https://github.com/typeplate/typeplate.github.com">submit issues on GitHub</a>.

<em>We sincerely thank <a href="https://twitter.com/tommycreenan">@TommyCreenan</a> (<a href="https://dribbble.com/tommycreenan">dribbble</a>) for designing the Typeplate logo.</em>


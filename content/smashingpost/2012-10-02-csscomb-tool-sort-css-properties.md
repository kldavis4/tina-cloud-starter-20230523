---
title: 'CSScomb: Sorting CSS Properties, The Better Way'
slug: csscomb-tool-sort-css-properties
image: null
date: 2012-10-02T08:30:23.000Z
author: vyacheslav-oliyanchuk
description: >-
  _This is our seventh article in a series that introduces the latest useful and
  freely available tools and techniques, developed and released by active
  members of the Web design community. The first article covered
  [PrefixFree](https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/);
  the second introduced
  [Foundation](https://www.smashingmagazine.com/2011/10/25/rapid-prototyping-for-any-device-with-foundation/),
  a responsive framework; the third presented
  [Sisyphus.js](https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/),
  a library for Gmail-like client-side drafts. The fourth shared a free plugin
  called
  [GuideGuide](https://www.smashingmagazine.com/2012/01/03/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/)
  with us, and later we've announced Erskine's responsive grid generator
  [Gridpak](https://www.smashingmagazine.com/2012/03/19/gridpak-the-responsive-grid-generator/)
  and [JS
  Bin](coding.smashingmagazine.com/2012/07/23/js-bin-built-for-sharing-education-and-real-time/).
  This time we present **CSScomb**, a tool to help you sort and categorize CSS
  properties in your code to improve maintenance._

  [![CSScomb](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9513cca-667d-4bc6-8fa1-8ee71a9c904f/csscomb-com-500.jpg)](https://www.smashingmagazine.com/2012/09/18/csscomb-tool-sort-css-properties/)

  As of this writing, Web browsers support about 200 different CSS properties.
  In all probability, you use pretty much every single one of them in your
  projects. So it’s about time to think of the consistency of the ordering of
  CSS properties inside selector declarations as seriously as you’d think about
  consistency in the formatting of code. So, if you want to pay attention to
  your code’s style, this article is for you. There’s a simple way to
  automatically sort CSS properties in your projects.
categories:
  - Coding
  - Tools
  - CSS
---
_This is our seventh article in a series that introduces the latest useful and freely available tools and techniques, developed and released by active members of the Web design community. The first article covered [PrefixFree](https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/); the second introduced [Foundation](https://www.smashingmagazine.com/2011/10/25/rapid-prototyping-for-any-device-with-foundation/), a responsive framework; the third presented [Sisyphus.js](https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/), a library for Gmail-like client-side drafts. The fourth shared a free plugin called [GuideGuide](https://www.smashingmagazine.com/2012/01/03/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/) with us, and later we've announced Erskine's responsive grid generator [Gridpak](https://www.smashingmagazine.com/2012/03/19/gridpak-the-responsive-grid-generator/) and [JS Bin](https://www.smashingmagazine.com/2012/07/23/js-bin-built-for-sharing-education-and-real-time/). This time we present **CSScomb**, a tool to help you sort and categorize CSS properties in your code to improve maintenance._

As of this writing, Web browsers support about 200 different CSS properties. In all probability, you use pretty much every single one of them in your projects. So it’s about time to think of the consistency of the ordering of CSS properties inside selector declarations as seriously as you’d think about consistency in the formatting of code. So, if you want to pay attention to your code’s style, this article is for you. There’s a simple way to automatically sort CSS properties in your projects.

[CSScomb](https://csscomb.com) is a utility to sort CSS properties within each selector declaration in a predefined order. The CSScomb algorithm is intended to be as close as possible to the choices a Web developer would make when working on CSS code. In order to re-sort, it is would usually be necessary to cut and paste lines, taking into consideration comments, multiline values, hacks — everything you would encounter in any serious project. This task is fairly dull to do by hand: you can trust CSScomb to do it for you.

[![CSScomb](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27775feb-117b-4ca9-b0f6-5f84048f02aa/csscomb.com-1)](https://CSScomb.com/)

The CSScomb algorithm is designed to “think” as a human editor, not as a dumb robot parsing CSS. This keeps the utility simple.

{{% feature-panel %}}

Here’s an example of how disarranged code can be fixed by CSScomb:

![Comb your code](https://res.cloudinary.com/indysigner/image/upload/v1549816672/csscomb_s9qkfp.jpg)  
_On the left, unsorted code. On the right, code after using CSScomb._

So, some details for the geeks and perfectionists who love tech small talk…

## Why Do You Need CSScomb?

I’ve worked on several teams, and each had a different CSS coding style. The naming system for CSS classes, line lengths, spaces, tabs and indents, and the order of CSS properties within selectors — everything was different. Maintaining the correct order by hand was tiresome. In addition, sometimes I had to work with legacy or third-party code that did not comply with our coding style. That was when I decided to create a very simple utility that would do just one thing but do it well: **sort the properties inside each selector**.

CSScomb has turned into a great utility that can really help with your professional work. Here are some reasons to use this little tool for CSS sorting:

1.  **CSScomb helps maintain your coding style.**  
    This is very important for long-term projects, in which code is constantly edited, rewritten or replaced. To maintain uniformity and make code independent of any one programmer’s style, you would have to watch over every character typed. In such situations, CSScomb would relieve the burden and free you to concentrate on more important things.
2.  **CSScomb helps you understand code.**  
    Code written by you, your colleagues or other programmers would be predictably sorted and, therefore, easier to understand.
3.  **CSScomb helps you find CSS properties faster.**  
    You would know exactly where a CSS property is, and looking through the list of declarations would require less effort.
4.  **CSScomb prevents accidental errors.**  
    Overriding properties in a CSS selector would be unlikely because identical properties would be sorted. Mutually exclusive properties would also be highly visible.</p>

## How Exactly Should CSS Properties Be Sorted?

I created CSScomb for another reason: no utility known to me could sort CSS properties well. Some online CSS beautifiers had a sorting option. But it was just an option and, more importantly, no real attention was paid to design. These utilities seemed to have been written by programmers driven to demonstrate their abilities to other programmers.

Especially astounding were the settings. Sorting CSS properties by length is obviously absurd. If you tried applying this kind of sorting to a real file, you would immediately see the disadvantages. For example, `top`, `right`, `bottom` and `left` would be scattered all over the selector declaration. It goes without saying that alphabetical arrangement would ensure that all prefixed properties would be grouped together.

Sorting CSS properties by alphabet just makes me smile. It’s a pity that advocates of it do not understand the difference between functional grouping and grouping for the sake of grouping. Sorting CSS selectors alphabetically is beyond repair.

**The only way to sort CSS properties usefully is to arrange them functionally.** This is the sort order included in CSScomb by default. All properties are divided into several groups and arranged in the most logical order within each group.

When I started developing CSScomb, I took the default sort order from the [Zen Coding](https://code.google.com/p/zen-coding/wiki/ZenCSSPropertiesEn "Zen CSS properties") project (perhaps you know of it). But the list of properties in CSScomb has become a bit bigger to account for the nuances of real-world CSS. You can read more about the default sort-order declaration on the [CSScomb page on GitHub](https://github.com/miripiruni/CSScomb/wiki/Sort-Order-CSS-Properties-(CSScomb-v2.11) "Sort Order CSS Properties (CSScomb v2.11)").

If using another sort order is necessary, there are two additional features:

*   You can change the sort order (because, say, you are already using another order in your project);
*   You can separate groups of properties by line breaks.

CSScomb sorts the properties in your CSS by using a JSON array with the names of all properties in order. Changing the sort order is possible, but you’d have to rearrange the 200 values in that JSON array. I hope you’re not motivated enough to do that. The default sorting algorithm seems to be the most rational one to me.

You can also split properties in groups, like this:

<pre id="p-r" class="brush: css">
#box {
  position: absolute;

  margin: 1em 0;
  border: 20px solid black;

  background: green;
  box-shadow: 0 2px 10px #666;
  color: red;

  letter-spacing: 3px;
  font-size: 72px;
  }
</pre>

In order to do this, you would rewrite the array with the CSS properties as an array of arrays, like this:

<pre><code class="language-javascript">[
  [
    "position",
    …
  ],
  [
    "margin",
    "padding",
    "border",
    …
  ],
  …
]</code></pre>

## What CSScomb Can Do?

Even if I personally like the “one line, one property” rule, CSScomb is completely agnostic about whether you use one-line or multiline syntax, or how your code is formatted at all. The utility’s purpose is just to reorder properties.

Duplicate properties will be sorted one after another in the same order they were in in the original selector declaration.

Unknown properties (i.e. those not specified in the sort order declaration) will be moved to the end of the list in the same order as they were in the original selector declaration.

I’ve paid particular attention to the peculiarities of real CSS code. CSScomb handles the following beautifully:

*   Sorting properties with multiline values;
*   CSS hacks (you use them responsibly, right?);
*   Overriding properties — sometimes accidental, sometimes intentional to support graceful degradation;
*   Missing semicolons before the closing brace (`}`);
*   `expression` syntax for Internet Explorer;
*   `datauri`, HTML entities, `@rules` and other lexical constructs of CSS;
*   Pretty much anything you might encounter in a complicated project.

CSScomb does not delete properties that are commented in your code. Instead it sorts the comments as it would had they not been commented out (in other words, the comments remains as comments — don’t worry). In doing that, **CSScomb knows the difference between declarations and comments**.

Here’s an example of several commented declarations before sorting:

<pre><code class="language-css">h1 {
  background: #faf0e6;
  /* border: 2px dashed #800000;
  color: #a0522d; */
  padding: 7px;
  }</code></pre>

The same code after sorting with CSScomb would look like this:

<pre><code class="language-css">h1 {
  padding: 7px;
  /* border: 2px dashed #800000; */
  background: #faf0e6;
  /* color: #a0522d; */
  }</code></pre>

As you can see, the properties are still commented out, but now they are separated and take their place according to the sort-order declaration.

I’ll be honest with you: it was a real pain developing the engine to correctly handle the comments, and this is perhaps the most complicated and error-prone feature. So, to speak frankly, if the comments are a three-level-nested byzantine labyrinth, please be forgiving of the sorting result.

Another pressing issue. Every good Web developer knows the principle of sorting prefixed properties. In the sort-order declaration, CSScomb by default follows the **principle of the inverted pyramid**: prefixes are sorted from longest to shortest, followed by the unprefixed property.

<pre><code class="language-css">-webkit-browser: cool;
-moz-browser: cool;
-ms-browser: cool;
-o-browser: cool;
browser: kewl;</code></pre>

Last but not least, you can feed CSScomb with a standalone property list, a whole CSS file or a `<style>` tag with CSS declarations. Being able to work with part of a file in your favorite code editor is extremely useful. And as for that…

## Real Product, Real Plans

CSSсomb does not have a built-in CSS parsing engine. The tool uses regular expressions to work with code. That decision keeps the utility compact (about 1000 lines of code). The project is written in **pure PHP, without any external libraries or dependencies**. I plan to switch to JavaScript in a future version, and to add support for CSS preprocessors after that.

As of now, CSScomb is not just an [online demo](https://CSScomb.com/online/ "Try CSScomb online") and a command-line utility, but also a great set of plug-ins for most popular editors:

*   Sublime Text 2 (can be installed via Package Control)
*   TextMate
*   Coda
*   Coda 2
*   Espresso 2
*   IntelliJ IDEA
*   WebStorm
*   PyCharm
*   Notepad++
*   Vim

Every stage in the process of planning and development is transparent and available on the [project page on GitHub](https://github.com/miripiruni/CSScomb/). As of this writing, CSScomb is at version 2.11, and the next version is already planned. You can follow news and updates about the project on the [Twitter stream](https://twitter.com/CSScomb).

If you can help to develop a CSScomb plugin for an editor that’s not on the list above (such as for Eclipse, Aptana Studio, UltraEdit, Komodo Edit, CSSEdit, Emacs or TopStyle), please contact me or open an issue on GitHub.</p>

## Conclusion

I hope CSScomb helps you make your code a little better, reduces bugs and makes you a bit happier. Find everything about the project (including the online demo and tests) on the [CSScomb website](https://CSScomb.com).

{{< signature "al" >}}


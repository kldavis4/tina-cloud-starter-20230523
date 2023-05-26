---
title: 'GuideGuide: Free Plugin For Dealing With Grids In Photoshop'
slug: guideguide-free-plugin-for-dealing-with-grids-in-photoshop
image: null
date: 2012-01-03T23:34:29.000Z
author: cameron-mcefee
description: >-
  This article is the fourth in our new series that introduces the latest, useful and freely available tools and techniques, developed and released by active members of the Web design community.
categories:
  - Graphics
  - Freebies
  - Tools
  - Photoshop
---
<p>The first article covered <a href="https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/">PrefixFree</a>; the second introduced <a href="https://www.smashingmagazine.com/2011/10/25/rapid-prototyping-for-any-device-with-foundation/">Foundation</a>, a responsive framework; the third presented <a href="https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/">Sisyphus.js</a>, a library for Gmail-like client-side drafts. Today we are happy to present Cameron McEfee's Photoshop extension <strong>GuideGuide</strong> which provides a tool to create pixel accurate columns, rows, midpoints and baselines.</p>

Take a moment and think about creating a multi-column grid in a Photoshop comp. Have your palms started to sweat? Yes, creating grids in Photoshop is a pain indeed. Some designers just estimate and drag guides arbitrarily onto the stage. Others draw vector shapes, duplicate them to represent columns, then stretch them to fit their design. The hardy few who don’t say things like, “I’m a designer, not a mathematician,” generally use a little math and logic to calculate their grid. If you were to boil that math down, it probably ends up looking something like this:

<pre><code class="language-css">
(siteWidth - (gutterWidth × (numberOfColumns - 1) ) ÷ numberOfColumns = columnWidth
</code></pre>

{{% feature-panel %}}

I was sitting at my desk one day doing this exact equation when I thought, "<em>Man, this looks just like code. I wish someone would make a plugin that would do this for me.</em>" Several months and many grids later, it occurred to me that I could probably build the plugin myself.</p>

## Enter: GuideGuide

I created GuideGuide for the sole purpose of making one of the most time consuming parts of Photoshop based design as easy as possible. Enter in a few numbers and GuideGuide will draw a grid on your document using Photoshop’s guides. You’ll become drunk with power the first time you watch it happen, I promise. Even better, GuideGuide’s real power is Photoshop’s marquee. If you have an active selection in your Photoshop document, GuideGuide creates the grid you specify within the selection’s boundaries. Anything GuideGuide can do, can be done using either the document or a selection.</p>

### Columns and Rows

Designing a site that needs multiple columns and gutters? GuideGuide has your back.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72847aae-2da9-4a42-ae16-211c4c85ad17/gg-cols-demo.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11e9b675-34d2-4d40-948e-3f7367adc5bb/gg-cols-demo-500.jpg" alt="Columns and Rows" width="500" height="254" /></a>

### Midpoints

GuideGuide makes finding the midpoint of items within your design a breeze. Simply draw a selection or <code>⌘</code> + <code>click</code> (<code>ctrl</code> + <code>click</code> on Windows) to create a selection around the item you want to find the midpoint of. To find its midpoint, click one of the midpoint buttons.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86436aef-2bfc-4874-8b1c-5041c47799f4/gg-midpoint-demo.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be81ff24-84d3-446d-ad70-3e18bab52cf4/gg-midpoint-demo-500.jpg" alt="Midpoints" width="500" height="327" /></a>

GuideGuide places a guide at the midpoint of the selection. Now you can easily center align elements under the original item.</p>

### Save It For Later

If you find yourself frequently using the same grid over and over, you can save it as a set for later use.</p>

## The Fun Part

Sure, GuideGuide has its basic rows, columns and midpoints, but with a little creativity it can do a whole lot more.</p>

### Measure Navigation

I <em>hate</em> figuring out how wide a navigation element needs to be to evenly fit across the width of a site. Instead, I let GuideGuide do the work for me.

1.  Make a selection the width of your site
2.  Enter your info, thinking of the _columns_ field as the number of navigation items and the _gutter_ field as the space you want between each item (if you want it).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0412645a-b9aa-4dea-8d01-957824510d84/gg-nav-demo.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/470a93a0-a7c6-41fd-b3b1-f2b733e31cd7/gg-nav-demo-500.jpg" alt="Measure Navigation" width="500" height="355" /></a>

### Element Padding

Want to draw a box around an item but don’t feel like measuring it out exactly?

1.  `⌘` + `click` (`ctrl` + `click` on Windows) the item to make a selection around it.
2.  Enter a negative margin in one of GuideGuide’s margin fields, and click the icon next to it. GuideGuide will fill that value into all the margin fields.
3.  Use the newly placed guides to draw your box.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34de3aa9-b20d-4e63-9690-a8a603636d8a/gg-neg-demo.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/951283fa-ed7c-409f-8a10-411a68edfd86/gg-neg-demo-500.jpg" alt="Element Padding" width="500" height="390" /></a>

### Baseline Grid

Using GuideGuide’s explicit row height, you can easily create a baseline grid for your design.

1.  Enter your desired line height in the row height field.
2.  Align your type and other elements to your new baseline grid.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b952b239-832d-4804-bec1-14b55588f72e/gg-baseline-demo.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/788a42b0-d685-433b-be58-ef5b206b6619/gg-baseline-demo-500.jpg" alt="Baseline Grid" width="500" height="385" /></a>

### Thoughts?

Do you have an unconventional use for GuideGuide? Post it in the comments of this post. I love hearing the clever and unusual ways people use GuideGuide. Found a bug or have a feature request? If you’d like to request a feature or have found something that is broken, please create an issue on GuideGuide’s support repo over on GitHub.

To download GuideGuide and learn more about some of its hidden features, head on over to <a href="https://www.guideguide.me">guideguide.me</a>. OS X Lion users with CS5 will need to <a href="https://blogs.adobe.com/cssdk/2011/12/fix-for-extension-signature-bug-on-mac-os-10-7-patch-posted.html">download a patch</a> for Adobe Extension Manager before they will be able to install GuideGuide.

{{< signature "il" >}}


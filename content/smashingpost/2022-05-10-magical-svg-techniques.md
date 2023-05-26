---
title: 'Magical SVG Techniques'
slug: magical-svg-techniques
author: cosima-mielke
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6be13a6e-5850-49e2-82b0-89d47212c66c/animated-debit-card-opt.png
date: 2022-05-10T10:00:00.000Z
summary: >-
  Smart SVG techniques, from generative SVG grids to SVG paths with masks, grainy SVG gradients, cut-out effects and fractional SVG stars. Let’s look at some magical SVG techniques that you can use right away.
description: >-
  Smart SVG techniques, from generative SVG grids to SVG paths with masks, grainy SVG gradients, cut-out effects and fractional SVG stars. Let’s look at some magical SVG techniques that you can use right away.
categories: 
  - SVG
  - Resources
  - Round-Ups
---

SVGs have become more and more popular in the past few years. For good reasons. They are scalable, flexible, and, most importantly, lightweight. And, well, they have even more to offer than you might think. We came across some magical SVG techniques recently that we’d love to share with you. From **SVG grids** and **fractional SVG stars** to SVG masks, fancy **grainy SVG gradients**, and handy SVG tools. We hope you’ll find something useful in here.

By the way, a while ago, we also looked at [SVG Generators](https://www.smashingmagazine.com/2021/03/svg-generators/) — for everything from shapes and backgrounds to SVG path visualizers, cropping tools, and SVG → JSX generators. If you’re tinkering with SVG, these might come in handy, too.

## Generative SVG Grids

Generative art is a wonderful opportunity for everyone who would love to create art but feels more at home in code. Let’s say you want to create **geometric patterns**, for example. Generative art will take away the difficult decisions from you: What shapes do I use? Where do I put them? And what colors should I use? If you want to give it a try, Alex Trost wrote a [tutorial on creating generative art with SVG grids](https://frontend.horse/articles/generative-grids/) that is bound to tickle your creativity &mdash; and teach you more about SVG.

{{< rimg breakout="true" href="https://frontend.horse/articles/generative-grids/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c3f5704-0a4c-483d-8a63-70601dc84305/generative-grids-opt.png" width="800" height="479" sizes="100vw" caption="Alex Trost shows <a href='https://frontend.horse/articles/generative-grids/'>how to create generative art with SVG grids</a>." alt="Creating Generative SVG Grids" >}}

The generative art that Alex creates is a grid of blocks with a random number of rows and columns. Each block has a randomly chosen design and colors from a shared color palette. Alex takes you step by step through the process of coding this piece: from setting up the grid and creating isolated **functions to draw SVGs** to working with color palettes, adding animations, and more. A fun little project &mdash; not only if you’re new to generative art and creative coding.

## Generative Landscape Rolls

An awe-inspiring project that bridges the gap between a century-old tradition and state-of-the-art coding is [*{Shan, Shui}*](https://github.com/LingDong-/shan-shui-inf). Created by Lingdong Huan and inspired by traditional Chinese landscape rolls, it creates procedurally generated, infinitely-scrolling **Chinese landscapes in SVG format**. The mountains and trees in the landscape are modeled from scratch using noise and mathematical functions. Fascinating!

{{< rimg breakout="true" href="https://github.com/LingDong-/shan-shui-inf" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99853108-7dd6-40c2-950b-47d41be709cc/shan-shui-opt.png" width="800" height="433" sizes="100vw" caption="The generative art project <em><a href='https://github.com/LingDong-/shan-shui-inf'>{Shan, Shui}</a></em> is inspired by traditional Chinese landscape paintings." alt="Shan, Shui" >}}

Now, if you’re asking yourself how something as complex might work, you’re not alone. Victor Shepelev wanted to get behind the secret of {Shan, Shui}* and made it his advent project to understand how it works. And, indeed, it took him 24 days to fully **dig into the code**. He summarized his findings in a [series of articles](https://zverok.github.io/blog/2021-12-28-grok-shan-shui.html).

## SVG Paths With Masks

SVGs have a lot of benefits compared to raster images. They are small in size, scalable, animatable, they can be edited with code, and a lot more. You can’t get the textured feel that raster graphics can provide, though. However, we can combine the **strengths of vector and raster** to create some charming effects. Like Tom Miller did in his [Silkscreen Squiggles](https://codepen.io/creativeocean/pen/abLGMwv) demo.

{{< rimg breakout="true" href="https://frontend.horse/articles/painting-svg-paths-with-masks/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fe06f6f-6d54-41fe-8d73-5c7ff06a2103/svg-paths-opt.png" width="800" height="477" sizes="100vw" caption="Adding a paintbrush effect to an SVG? A <a href='https://frontend.horse/articles/painting-svg-paths-with-masks/'>little trick</a> makes it possible." alt="Painting SVG Paths with Masks" >}}

Silkscreen Squiggles is an animation where squiggles fill a rectangular canvas. What makes the squiggles special is that they appear to have a **paintbrush texture**. The secret: a mask with an alpha layer that gives the simple squiggly paths their texture. Alex Trost [dissects how it works](https://frontend.horse/articles/painting-svg-paths-with-masks/). Inspiring!

## Grainy Gradients

Noise is a simple technique to **add texture** to an image and make otherwise solid colors or smooth gradients more realistic. But despite designer’s affinity for texture, noise is rarely used in web design. Jimmy Chion explores [how we can add texture to a gradient](https://css-tricks.com/grainy-gradients/) with only a small amount of CSS and SVG.

{{< rimg breakout="true" href="https://css-tricks.com/grainy-gradients/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7f7f36b-6f4c-43db-8dae-d49471554ce8/holographic-type-opt.png" width="800" height="499" sizes="100vw" caption="A fascinating <a href='https://css-tricks.com/grainy-gradients/'>holographic type effect</a> achieved with a grainy SVG gradient." alt="Grainy Gradients" >}}

The trick is to use an SVG filter to create the noise, then apply that noise as a background. Layer it underneath your gradient, boost the brightness and contrast, and that’s already it. Potential use cases could be light and shadows or **holographic foil effects**, for example. The core of this technique is supported by all modern browsers. A clever visual effect to add depth and texture to a design.

## Adding Texture And Depth

“Analog” materials like paint and paper naturally add depth to an artwork, but when working digitally, we often sacrifice the **organic depth** they provide for precision and speed. Let’s bring some texture back into our work! George Francis shares [three ways to do so](https://georgefrancis.dev/writing/texture-generative-snacks/).

{{< rimg breakout="true" href="https://georgefrancis.dev/writing/texture-generative-snacks/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9749a39-5afc-4b17-b091-de9f1cb162ac/texture-generative-snacks-opt.png" width="800" height="569" sizes="100vw" caption="George Francis explores <a href='https://georgefrancis.dev/writing/texture-generative-snacks/'>how to create texture and depth</a>." alt="Texture Generative Snacks" >}}

The techniques that George explores are quite simple but effective. Tiny **random shapes** added to a canvas at random points, solid shape fills with lines, and non-overlapping circles distributed evenly but randomly with an algorithm. Inspiring ideas to tinker with.

## Cut-Out Effects With CSS And SVG

In a recent front-end project that Ahmad Shadeed was working on, one of the components included a cut-out effect where an area is cut out of a shape. And because there are multiple ways to create such an effect in CSS or SVG, he decided to explore the **pros and cons** that each of the solutions brings along.

{{< rimg breakout="true" href="https://ishadeed.com/article/thinking-about-the-cut-out-effect/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e4319a1-8dcf-443b-b781-e659380aa800/cut-out-effect-opt.png" width="800" height="501" sizes="100vw" caption="If you want to create a <a href='https://ishadeed.com/article/thinking-about-the-cut-out-effect/'>cut-out effect</a>, Ahmad Shadeed helps you find the best technique for your use case." alt="Thinking About The Cut-Out Effect" >}}

In his blog post “[Thinking About The Cut-Out Effect](https://ishadeed.com/article/thinking-about-the-cut-out-effect/)”, Ahmad takes a look at three different use cases for a cutout effect: an avatar with a cut-out **status badge** that indicates that a user is currently online, a “seen avatar” that consists of overlapping circle avatars that are indicators that a message has been seen in a group chat, as well as a website header with a cut-out area behind a circular logo. Ahmad presents different solutions for each use case &mdash; SVG-only, CSS-only, and a mix of both &mdash; and explains the pros and cons of each one of them. A comprehensive overview.

{{% ad-panel-leaderboard %}}

## Fractional SVG Stars

Are you building a rating component and you want it to support fractional values like 4.2 or 3.7 stars but without using images? Good news, you can achieve **fractional ratings** with only CSS and inline SVG. Samuel Kraft [explains how it works](https://samuelkraft.com/blog/fractional-svg-stars-css).

{{< rimg breakout="true" href="https://samuelkraft.com/blog/fractional-svg-stars-css" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e4ace33-8648-4ec4-a5a9-68988ad459ce/fractional-stars-opt.png" width="800" height="348" sizes="100vw" caption="A clever trick to create <a href='https://samuelkraft.com/blog/fractional-svg-stars-css'>fractional rating stars</a> only with CSS and SVG comes from Samuel Kraft." alt="Fractional SVG Stars" >}}

The component basically consists of two parts: a list of star icons based on the max rating and an “overlay” `div` that will be responsible for **changing the colors** of the stars underneath. This is the magic that makes the fractional part work. The technique is supported in all modern browsers; for older browsers, you can fall back to opacity instead. Clever!

## Generative Mountain Ridge Dividers

When Alistair Shepherd built his personal website, he wanted to have section dividers that match the mountain theme of the site. But not any mountain dividers, but dividers with **unique ridges** for every divider.

{{< rimg breakout="true" href="https://alistairshepherd.uk/writing/svg-generative-ridges/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f16fdf7a-1bc9-4d41-acd1-805f897d5025/generative-mountain-divider-opt.png" width="800" height="269" sizes="100vw" caption="Alistair Shepherd created <a href='https://alistairshepherd.uk/writing/svg-generative-ridges/'>generative SVG mountain ridge dividers</a>." alt="SVG generative mountain ridge dividers" >}}

Instead of creating a variety of different dividers manually, Alistair decided to use a combination of SVG and terrain generation, a technique that is usually used in **game development**, to generate the dividers automatically. In a [blog post](https://alistairshepherd.uk/writing/svg-generative-ridges/), he explains how it works.

If you’re up for some more horizontal divider inspiration, also be sure to check out Sara Soueidan’s blog post “[Not Your Typical Horizontal Rules](https://www.sarasoueidan.com/blog/horizontal-rules/)” in which she shows how she turned a boring horizontal line into a cute “**birds on a wire**” divider with the help of some CSS and SVG.

## Flexible Repeating SVG Masks

Sometimes it’s a small idea, a little detail in a project that you tinker with and that you can’t let go off until you come up with a tailor-made solution to make it happen. Nothing that seems like a big deal at first glance, but that requires you to think outside the box. In Tyler Gaw’s case, this little detail was a **flexible header** with a little squiggle at the bottom instead of a straight line. The twist: to make the component future-proof, Tyler wanted to use a seamless, horizontal repeating pattern that he could color with CSS.

{{< rimg breakout="true" href="https://tylergaw.com/articles/css-repeating-svg-masks/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58c7f164-9648-4cb0-8e17-eeca66eee1ad/banner-squiggles-opt.png" width="800" height="447" sizes="100vw" caption="Tyler Gaw’s <a href='https://tylergaw.com/articles/css-repeating-svg-masks/'>banner squiggles</a> are a great base for some fun experiments." alt="Flexible Repeating SVG Masks" >}}

To get the job done, Tyler settled on [flexible repeating SVG masks](https://tylergaw.com/articles/css-repeating-svg-masks/). SVG **provides the shape**, CSS handles the color, and `mask-image` does the heavy lifting by hiding anything in the underlying `div` that doesn’t intersect with the shape. A clever approach that can be used as the base for some fun experiments.

## Swipey Image Grids

When you think of “SVG animation”, what comes to your mind? Illustrative animation? Well, SVG can be useful for much more than pretty graphics. As Cassie Evans points out, a whole new world of **UI styling** opens up once you stop looking at SVG purely as a format for illustrations and icons. One of her favorite use cases for SVG: [responsive animated image grids](https://www.cassie.codes/posts/swipey-image-grids/).

{{< rimg breakout="true" href="https://www.cassie.codes/posts/swipey-image-grids/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a60334e-e053-484c-9da7-6dde0a1f86d2/swipey-image-grids-opt.png" width="800" height="505" sizes="100vw" caption="Cassie Evans uses SVG’s internal coordinate system to create a <a href='https://www.cassie.codes/posts/swipey-image-grids/'>swipey image grid</a>." alt="Swipey Image Grids" >}}

Cassie doesn’t build her image grid on CSS Grid but uses SVG’s **internal coordinate system** (which is responsive by design) to design the grid layout. She then adds images to the grid and positions them with <code>preserveAspectRatio</code>. <code>clipPath</code> “swipes” the images in. The final animation relies on GreenSock to ensure that the transforms work consistently across browsers. If you want to dig deeper into the code, be sure to check out Cassie’s [blog post](https://www.cassie.codes/posts/swipey-image-grids/) in which she explains each step in detail.

## Animated SVG Debit Card Illustrations

What if you could animate a debit card design? Probably not on an actual physical card, but rather for a landing page where you’d like to drive interest towards the card’s **design or features**? Well that’s an unusual challenge to tackle, and Tom Miller decided to take it on.

{{< rimg breakout="true" href="https://codepen.io/collection/MgYZwW" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6be13a6e-5850-49e2-82b0-89d47212c66c/animated-debit-card-opt.png" width="800" height="459" sizes="100vw" caption="The <a href='https://codepen.io/collection/MgYZwW'>animated SVG illustrations</a> that Tom Miller created bring debit cards to life." alt="Animated SVG Debit Card Illustrations" >}}

In a series of [SVG debit card animations](https://codepen.io/collection/MgYZwW), Tom uses GreenSock to **animate SVG paths and shapes** smoothly, so every card literally comes to life on its own, transforming, rotating, and scaling beautifully, alongside just a few lines of JavaScript. A wonderful inspiration for your next landing page design!

{{% ad-panel-leaderboard %}}

## Raster Image To SVG Converter

You need to quickly convert a raster image into an SVG? Then [SVGcode](https://svgco.de/) is for you. The progressive web app converts image formats like JPG, PNG, GIF, WebP, and AVIF to vector graphics in SVG format.

{{< rimg breakout="true" href="https://svgco.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6434f1f-f711-472e-89a1-fea1a40edd78/svgcode-opt.png" width="800" height="518" sizes="100vw" caption="<a href='https://svgco.de/'>SVGcode</a> turns raster images into vector images." alt="SVGcode" >}}

To convert an image, drop your raster image into the SVGcode app, and the app will trace the image, color by color, until a vectorized version of the input appears. You can choose between color SVG and monochrome SVG and there also are a number of **customization settings** to improve the output further, by suppressing speckles and adjusting the color, for example. If you install the PWA, you can even use it as a default file handler on your machine. A real timesaver.

## Download SVGs From Any Site

A handy little tool to enhance your SVG workflow is [SVG Gobbler](https://www.svggobbler.com/). The browser extension finds the vector content on the page you’re viewing and gives you the option to download, optimize, copy, **view the code**, or export it as an image.

{{< rimg breakout="true" href="https://www.svggobbler.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6930c11-dd66-4b3e-b3d3-8c4a2f88fe1f/svg-gobbler-opt.png" width="800" height="485" sizes="100vw" caption="<a href='https://www.svggobbler.com/'>SVG Gobbler</a> makes it easy to download SVGs from any site." alt="SVG Gobbler" >}}

When you click the browser extension, it shows you all SVGs detected on the site. You can quickly download the ones you like or copy them to your clipboard. When you view the code, you can toggle **optimization options** from SVGO &mdash; to beautify the markup or clean up attributes or numeric values, for example. And if you need a PNG version of an SVG, you can export it in any size you want. A fantastic addition to any developer’s toolkit.

## Scaling SVGs Made Simple

Scaling `svg` elements can be a daunting task, since they act very differently than normal images. Amelia Wattenberger came up with an [ingenious comparison](https://wattenberger.com/guide/scaling-svg) to help us make sense of SVGs and their special features: “The `svg` element is a **telescope** into another world.”

{{< rimg breakout="true" href="https://wattenberger.com/guide/scaling-svg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53b477a1-4d91-4f1c-af48-5f2f781b716c/scaling-svg-opt.png" width="800" height="541" sizes="100vw" caption="Imagine the <code>svg</code> element as a <a href='https://wattenberger.com/guide/scaling-svg'>telescope into another world</a>, and scaling will become a lot easier." alt="SVG Gobbler" >}}

Based on the idea of the telescope, Amelia explains how to use the `viewBox` property to zoom in or out with your “telescope”, and, thus, change the size of your `<svg>`. A small tip that works wonders.

## Wrapping Up

We hope that these techniques will tickle your curiosity and inspire you to try some SVG magic yourself. If *you* came across an interesting SVG technique that left you in awe, please don’t hesitate to share it in the comments below. We’d love to hear about it. Happy creating!

### More On SVG

<ul>
    <li><a href="https://www.smashingmagazine.com/2021/03/svg-generators/">SVG Generators</a></li>
    <li><a href="https://www.smashingmagazine.com/2019/05/svg-design-tools-practical-guide/">A Practical Guide To SVG And Design Tools</a></li>
    <li><a href="https://www.smashingmagazine.com/2019/03/svg-circle-decomposition-paths/">SVG Circle Decomposition To Paths</a></li>
    <li><a href="https://www.smashingmagazine.com/2021/05/accessible-svg-patterns-comparison/">Accessible SVGs: Perfect Patterns For Screen Reader Users</a></li>
    <li>Also, <a href="/the-smashing-newsletter/">subscribe to our newsletter</a> to not miss the next ones.</li>
</ul>

{{% newsletter-panel %}}

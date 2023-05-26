---
title: 'CSS Generators'
slug: css-generators
author: iris-ljesnjanin
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af649c50-abf1-4214-9e6c-493c3c4ad872/4-css-generators.png
date: 2021-03-15T11:30:00.000Z
summary: >-
  In a new short series of posts, we highlight some of the useful tools and techniques for developers and designers. This time it’s all about CSS Generators: from CSS shadows to easing gradients to CSS overlays to CSS doodles.
description: >-
  In a new short series of posts, we highlight some of the useful tools and techniques for developers and designers. This time it’s all about CSS Generators: from CSS shadows to easing gradients to CSS overlays to CSS doodles.
categories:
  - CSS
  - Generators
  - Tools
  - Round-Ups
last_updated: 2021-06-24T11:00:00.000Z
---

Last week, we looked at [CSS Auditing tools](https://www.smashingmagazine.com/2021/03/css-auditing-tools/), and this week around we’ll be looking at useful generators for everything CSS: from gradients to drop-shadows and bezier curves to triangles and type scales. Just a few useful tools for your toolbelt, to keep close.


<div style="background-color: #f6f6f6;
border-radius:11px;padding: 15px 30px;margin-top: 1em">
    <h4 style="margin-top: 0.5em">More On CSS:</h4>
    <ul>
    <li><a href="https://www.smashingmagazine.com/2021/03/css-auditing-tools/">CSS Auditing Tools</a></li>
    <li><a href="https://www.smashingmagazine.com/2021/02/things-you-can-do-with-css-today/">Things You Can Do With CSS Today</a></li>
    <li><a href="https://www.smashingmagazine.com/2021/02/useful-chrome-firefox-devtools-tips-shortcuts/">Useful DevTools Tips and Shortcuts</a></li>
    <li>Also, <a href="/the-smashing-newsletter/">subscribe to our newsletter</a> to not miss the next ones.</li>
</ul>
</div>

## CSS Shadows Generator

Looking for a tool that’ll automatically generate CSS code for really **smooth, layered box-shadows**? Well, you’re going to love [SmoothShadow](https://brumm.af/shadows). Inspired by an article written by [Tobias Ahlin Bjerrome](https://tobiasahlin.com/blog/layered-smooth-box-shadows/), this nifty tool was created to help anyone generate the code they need on the spot.

{{< rimg href="https://brumm.af/shadows" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29c59032-7213-4d9a-b5d4-6653c2d7c456/1-css-generators.png" width="700" height="454" sizes="100vw" caption="SmoothShadow Figma plugin by Philipp Brumm (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29c59032-7213-4d9a-b5d4-6653c2d7c456/1-css-generators.png'>Large preview</a>)" alt="SmoothShadow Figma plugin by Philipp Brumm" >}}

Once you’ve given it a try, it will be difficult to not use it. The little tool allows you to visually design a layered smooth box-shadow, but also tweak alpha, offset and blur with individual easing curves. And it gets even better: The creator of the tool, [Philipp Brumm](https://twitter.com/funkensturm), has also released SmoothShadow as a [Figma plugin](https://www.figma.com/community/plugin/788830704169694737/SmoothShadow), so you can optimize your workflow just like you’ve always wanted to.

<style type="text/css">@media screen and (min-width:1100px){.c-garfield-the-cat .c-garfield-native-panel{grid-row:8/14}.c-garfield-native-panel__right{grid-row:8/11}.c-garfield-the-cat .c-garfield-native-panel__below {grid-row: 18/22;}}</style>

## CSS Border-Radius Generator

When we think about `border-radius`, we usually think about a few straightforward values &mdash; perhaps 8px or 11px, or maybe 16px. However, `border-radius` can be quite [fancy](https://9elements.com/blog/css-border-radius/), and [fancy-border-radius](https://9elements.github.io/fancy-border-radius/#30.30.30.33--.) generator allows you to generate them easily. The tool provides a visualization of not only plain round shapes, but also organic shapes, by using eight values combined. Essentially, what we are creating are overlapping ellipses that build the final shape. The tool is also available as [CLI tool](https://github.com/9elements/fancy-border-radius), so you can run it locally as well.

{{< rimg href="https://9elements.github.io/fancy-border-radius/#30.30.30.33--." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67998e7d-f168-4b4e-9b3c-aea3c7bffe2b/2-css-generators.png" width="800" height="629" sizes="100vw" caption="Border Radius organic cell (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67998e7d-f168-4b4e-9b3c-aea3c7bffe2b/2-css-generators.png'>Large preview</a>)" alt="Border Radius organic cell" >}}

## Cubic-Bezier Curves Generator

Sometimes an animation just doesn’t feel right, does it? Perhaps the duration is off, or the easing is quirky, and figuring it out might take quite some time. With Lea Verou’s [cubic-bezier](https://cubic-bezier.com/), you can **preview and compare animations**, slow them down and even adjust them visually. And then copy-paste the CSS snippet to plug into your project right away.

{{< rimg href="https://cubic-bezier.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b04b7c5-9cb5-4bb9-be2d-f9273e31871c/3-css-generators.png" width="700" height="492" sizes="100vw" caption="Perfect Cubic-Bezier Curves (<a href=''>Large preview</a>)" alt="Perfect Cubic-Bezier Curves" >}}

And if you need basic or complex CSS @keyframe animations, [Keyframes.app](https://keyframes.app/) provides a **visual timeline editor** similar to video-editing software. You can add steps, change sizing and position, apply transforms and color changes and get the CSS to copy-paste as well. Ah and not to forget the [Animation panel in Chrome](https://developers.google.com/web/tools/chrome-devtools/inspect-styles/animations) and [Firefox](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Work_with_animations) for debugging as well.

## Easing Gradients

With gradients, we often rely on linear gradients, transitioning from one color to another. However, linear gradients have hard edges where they start or end. There is a way to make the gradients slightly better, with easing functions. So Andreas Larsen has built a little editor, [Easing Gradients Editor](https://larsenwork.com/easing-gradients/), that allows us to create and preview easing gradients in CSS. The tool is also available as a [Sketch plugin](https://github.com/larsenwork/sketch-easing-gradient#readme) and a [PostCSS plugin](https://github.com/larsenwork/postcss-easing-gradients). You can use a color picker, but unfortunately can't add an actual HEX color value yet.

{{< rimg href="https://larsenwork.com/easing-gradients/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ae9e757-68f6-4ea4-a75f-a8f2d6533a72/c0zoib50.png" width="837" height="410" sizes="100vw" caption="Linear gradients have hard edges where they start or end, and we can fix it with easing functions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ae9e757-68f6-4ea4-a75f-a8f2d6533a72/c0zoib50.png'>Large preview</a>)" alt="LearnUI Data Color Picker" >}}

## Data Visualization Color Palettes

Sometimes you need very specific type of color for a very specific task. For example, if you are working on a data visualization project &mdash; e.g. pie charts, grouped bar charts, maps &mdash; you probably need a series of colors that are *visually equidistant*. That’s when [LearnUI Data Color Picker](https://learnui.design/tools/data-color-picker.html#palette) can become very useful. In such cases, it’s better to use a **range of hues,** so users can identify the differences faster. It’s indeed easier to distinguish *yellow from orange* than *blue from blue-but-15%-lighter*.

{{< rimg href="https://learnui.design/tools/data-color-picker.html#palette" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af649c50-abf1-4214-9e6c-493c3c4ad872/4-css-generators.png" width="800" height="541" sizes="100vw" caption="An accessible and vibrant color scheme, using a range of hues to identify differences faster. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af649c50-abf1-4214-9e6c-493c3c4ad872/4-css-generators.png'>Large preview</a>)" alt="LearnUI Data Color Picker" >}}

With the tool, you choose how many colors you need and whether you need a light or a dark background color, and choose whether you want a default palette, a single hue palette, or a divergent color scale. Once you have it, you can copy hex values and export them as SVG to use in Sketch, Figma or Adobe XD.

{{< rimg href="https://learnui.design/tools/accessible-color-generator.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b268276-9d44-4aa5-bc13-3d376cc1f60a/4b-css-generators.png" width="663" height="365" sizes="100vw" caption="An accessibility check for headings and body copy. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b268276-9d44-4aa5-bc13-3d376cc1f60a/4b-css-generators.png'>Large preview</a>)" alt="Accessible color generator" >}}

LearnUI also provides an [accessible color generator](https://learnui.design/tools/accessible-color-generator.html) and a quite [fancy gradient generator](https://learnui.design/tools/gradient-generator.html), with different gradient types, interpolation, angle, easing and how smooth you’d like the gradient to be.

{{% feature-panel %}}

## From CSS Color Shades To Triangles and Fake Data

Imagine that you just need to find CSS triangle styles for elements and pseudo-elements. Or perhaps refine the color palette a bit by exploring **tints and shades** of a given color. Or perhaps generate a linear and radial CSS gradient for a section of the page. There is no need to do it all manually or try to find those CSS snippets all over the web. You can always find them on [Omatsuri](https://omatsuri.app/).

{{< rimg href="https://omatsuri.app/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27d30187-536e-4944-882a-2651fa5f33a6/5-css-generators.jpg" width="800" height="427" sizes="100vw" caption="From CSS Gradients To Fake Data (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27d30187-536e-4944-882a-2651fa5f33a6/5-css-generators.jpg'>Large preview</a>)" alt="From CSS Gradients To Fake Data" >}}

Omatsuri means *festival* in Japanese, and the site is a lovely little festival of open-source browser tools for everyday use. On the site, you’ll find a [triangle generator,](https://omatsuri.app/triangle-generator) a color shades generator, a gradient generator, page dividers, SVG compressor, **SVG → JSX converter**, a fake data generator, CSS cursors, and keyboard event codes. Designed and built by Vitaly Rtishchev and Vlad Shilov. The [source code of the site](https://github.com/rtivital/omatsuri) is available as well.

## CSS Overlay With High Contrast Generator

If you want to make text better stand out against a background image, there’s a little trick: You can use a CSS `linear-gradient` overlay with a certain opacity on top of the image to improve color contrast. [Spotify](https://twitter.com/addyosmani/status/1365735686838493187), for example, uses the technique.

{{< rimg href="https://codepen.io/yaphi1/pen/oNbEqGV" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a813689-6e6e-4444-805a-8ae2830273f9/6-css-generators.png" width="700" height="393" sizes="100vw" caption="CSS linear gradient overlay (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a813689-6e6e-4444-805a-8ae2830273f9/6-css-generators.png'>Large preview</a>)" alt="CSS linear gradient overlay" >}}

While all of this only requires one line of code, there’s still one question left to be answered: How to determine the opacity to use for the overlay? The [Optimal Overlay Finder](https://codepen.io/yaphi1/pen/oNbEqGV) helps you find out. You upload an image, enter your text and choose your overlay and text colors, and the tool shows you a preview of what the overlay looks like when applied to your image, as well as the optimal overlay opacity. A small detail that goes a long way.

## CSS Color Palette Generator

There are plenty of fantastic tools to generate your color palette, but [Coolors.co](https://coolors.co/) is a little nifty tool that does just enough to generate palettes and explore different shades of a color. You can create a palette from the photo or a collage of photos, test for color blindness and quickly adjust hue, saturation, brightness and temperature. Obviously, it also features [trending color palettes](https://coolors.co/palettes/trending).

{{< rimg href="https://coolors.co/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae2e3c82-3484-4581-88cd-2ecc52282573/7-css-generators.png" width="800" height="314" sizes="100vw" caption="CSS Color Palette Generator for finding just the right gradients. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae2e3c82-3484-4581-88cd-2ecc52282573/7-css-generators.png'>Large preview</a>)" alt="Trending color palettes" >}}

You can also produce a [gradient palette](https://coolors.co/gradient-palette/) between two colors and [create and export your own gradient](https://coolors.co/gradient-maker/fcf3c4-f962a0-aa96f9) as CSS. The tool is available as an iOS app, Adobe add-on and Chrome extension.

{{< rimg href="https://cssgradient.io/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c142156-9777-4fdb-9902-5f918c3bc485/8-css-generators.png" width="700" height="393" sizes="100vw" caption="Another color generator, also available as iOS app, Adobe add-on and Chrome extension. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c142156-9777-4fdb-9902-5f918c3bc485/8-css-generators.png'>Large preview</a>)" alt="" >}}

And if you need something slightly more sophisticated for gradients in your toolbox, [CSSGradient.io](https://cssgradient.io/) is another tool for all your gradient needs &mdash; be it lineal or radial gradients, [color shades](https://cssgradient.io/color-shades/) or gradient backgrounds.

Also, [Gradient Generator](https://colordesigner.io/gradient-generator) generates 1 to 40 stepped gradients from two colors of your choice. Each gradient is automatically presented in HEX, HSL, and RGB formats &mdash; all you need to do is simply click on the value, and it will be copied to your clipboard right away.

## CSS Color Gradients Generator

Hand-picking colors to make a color gradient requires design experience and a good understanding of color harmony. If you need a gradient for a background or for UI elements but don’t feel confident enough to tackle the task yourself (or if you’re in a hurry), the [color gradient generator](https://mybrandnewlogo.com/color-gradient-generator) which the folks at My Brand New Logo have created has got your back.

{{< rimg href="https://mybrandnewlogo.com/color-gradient-generator" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f1e06d9-0162-4a6d-ae11-56a07295f12b/9-css-generators.png" width="700" height="464" sizes="100vw" caption="Color gradient generator (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f1e06d9-0162-4a6d-ae11-56a07295f12b/9-css-generators.png'>Large preview</a>)" alt="Color gradient generator" >}}

Powered by color gradient algorithms, the generator creates well-balanced gradients based on a color you select. There are four different styles of gradients that go from subtle to a mother-of-pearl effect and an intense, deep color gradient. You can adjust the gradient with sliders and, once you’re happy with the result, copy-paste the generated CSS code to use it in your project.

## CSS Type Scale Generator

So what if you want to create a reliable typographic system that works well both on mobile and on desktop? Usually you would rely on established typographic scales, that provide a typographic hierarchy for everything from paragraphs to captions and headings. [Type-Scale](https://type-scale.com/) by Jeremy Church is a fantastic little tool that helps you build a typographic scale and export it in CSS. Small scales are usually a good fit for mobile views, medium scales could work well for the desktop view, and large scales could work well for marketing sites.

{{< rimg href="https://type-scale.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0216afda-fc55-4d57-9928-885a89d01f7b/10-css-generators.png" width="800" height="572" sizes="100vw" caption="A a fantastic little tool that helps you build a typographic scale and export it in CSS. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0216afda-fc55-4d57-9928-885a89d01f7b/10-css-generators.png'>Large preview</a>)" alt="Type-Scale" >}}

The tool provides 8 pre-defined harmonious type scales (but you can define a custom one as well), from Major Third to Perfect Fifth and generate a sequence of font sizes with a particular geometric incrementation ratio. You can adjust the settings such as `line-height` and body weight, refine the preview text and get the generated CSS &mdash; or edit it with a type specimen on CodePen. Alternatively, you can check Tim Brown’s good ol’ [ModularScale.com](https://www.modularscale.com/) as well.

{{< rimg href="https://www.layoutgridcalculator.com/typographic-scale/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68f9f6c6-8ece-49a0-b283-efc4ad7332d6/11-css-generators.png" width="585" height="351" sizes="100vw" caption="Modular scale, using similar structures like the musical scale. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68f9f6c6-8ece-49a0-b283-efc4ad7332d6/11-css-generators.png'>Large preview</a>)" alt="Typographic Scale" >}}

Another lovely tool is a [Typographic Scale Calculator](https://www.layoutgridcalculator.com/typographic-scale/) by [Jean-Lou Desire](https://www.jeanlou.net/) which, unlike Tim’s and Jeremy’s tools, generates a [modular scale](https://alistapart.com/article/more-meaningful-typography) using three defining properties (the initial term, the increment ratio, and the number of sizes in the scale) similar to the musical scale. The result is a smoother sizing for designers, with a few more options to compose more values from &mdash; e.g. for smaller side notes or large blockquotes.

## Line Height Calculator

If you’re building a type scale based on a baseline grid, there’s a tricky question to be answered: What’s the right line height for every text size on your scale? Fran Pérez’s [Good Line-Height calculator](https://www.thegoodlineheight.com/) does the maths for you.

{{< rimg href="https://www.thegoodlineheight.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11e08b27-cf30-4f4e-bc03-5853edea2407/good-line-height-opt.png" width="800" height="450" sizes="100vw" caption="Calculate the perfect line height for your baseline grid. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11e08b27-cf30-4f4e-bc03-5853edea2407/good-line-height-opt.png'>Large preview</a>)" alt="Good Line Height calculator" >}}

To calculate the results, you only need to enter three parameters: font size, multiplier, and grid row height. Font size is the key to ensure your text sits nicely on the baseline grid, no matter the text size, the multiplier gives you control over the distance between lines, and grid row height defines the height of each row in your baseline grid. 

## Fluid Heading Generator

Thanks to `clamp()`, you can set a font size that grows with the viewport but doesn’t go below or above the minimum and maximum font size that you define. To help you find the perfect CSS values for your fluid heading and control how it scales across different viewports, Erik André Jakobsen built the [Fluid Typography](https://fluid-typography.netlify.app/) tool.

{{< rimg href="https://fluid-typography.netlify.app/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8181cf45-8438-4f48-abb4-66631a15dd81/fluid-typography-opt.png" width="800" height="510" sizes="100vw" caption="Calculate a <code>clamp()</code> rule to make your headings fluid. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8181cf45-8438-4f48-abb4-66631a15dd81/fluid-typography-opt.png'>Large preview</a>)" alt="Fluid Typography" >}}

You enter the minimum and maximum font size as well as the minimum and maximum viewport width, and the tool calculates not only the `clamp()` rule for you but also shows you a demo of what the specifications look like when applied to an actual heading. 

Another helpful [generator to help you figure out the `clamp()` rule](https://maximeroudier.com/typeScaleClampGenerator/) for your project comes from Maxime Roudier. It works similarly to Erik’s tool but also lets you select a font family and a range that you adjust with a slider instead of entering concrete minimum and maximum values.

## CSS Capsize Generator

To minimize disorienting and expensive layout shifts during loading, we need to match the fallback font against the web font. Monica Dinculescu’s [font-style-matcher](https://meowni.ca/font-style-matcher/) allows us to minimize the jarring shift by matching the fallback font and the intended webfont’s x-heights and widths and we could make use of [f-mods](https://simonhearne.com/2021/layout-shifts-webfonts/) to do the same thing with new CSS properties.

{{< rimg href="https://seek-oss.github.io/capsize/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b66dd29c-4998-47b4-a8fa-aa4c3a114ae6/12-css-generators.png" width="734" height="328" sizes="100vw" caption="A little tool that adjusts the font-size, so that the height of capital letters is a multiple of your grid. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b66dd29c-4998-47b4-a8fa-aa4c3a114ae6/12-css-generators.png'>Large preview</a>)" alt="Font style matcher" >}}

By default, many fonts come with pre-defined margins and leadings, so if a fallback font and a web font are different, the entire layout will change significantly. [Capsize](https://seek-oss.github.io/capsize/) adjusts the font-size, so that the height of capital letters is a multiple of your grid. It does so by trimming the space above capital letters and below the baseline. So by keeping the same line-height in a fallback font and a web font, the tool generates “magic numbers” to make sure that the switch is seamless.

## CSS Complex Selectors Generator

Imagine that you need to create a table of items. You might want to keep them on the same row if there are 3 or fewer items, but then spanning two full lines for 6 and 8 items, while being just a list of cards with 10 items and more. How would you build it? While many of these situations can be fixed with CSS Grid and Flexbox, sometimes you might end up with a quite complex situation which would need a quite complex CSS selector.

{{< rimg href="https://quantityqueries.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e94e9f0d-2808-4e40-ae62-50d4d23ee991/13-css-generators.png" width="800" height="378" sizes="100vw" caption="For building complex selectors that heavily rely on the exact number of children or siblings in a container. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e94e9f0d-2808-4e40-ae62-50d4d23ee991/13-css-generators.png'>Large preview</a>)" alt="Quantity Selectors" >}}

For this purpose, Drew Minns has built a generator for [Quantity Selectors](https://quantityqueries.com/) &mdash; complex CSS selectors that allow styles to be applied to elements based on the number of siblings. For example, when you want to apply styles to all elements when there are **at least** 5 items and siblings, or at most 10, or perhaps between 3 to 5 items.

The final selector might not be easy to understand though, so it’s worth making sure that you provide a proper explanation in the code of what it’s supposed to target.

## CSS `clip-path` Generator

Thanks to the `clip-path` property, we can create [complex shapes in CSS](https://twitter.com/mikaelainalem/status/1358492344602025985) by clipping an element to a basic shape, be it a simple circle, a fancy polygon, or even an SVG source. The CSS `clip-path` maker [Clippy](https://bennettfeely.com/clippy/) is a visual tool that helps you **create and customize clip-paths** right in your browser.

{{< rimg href="https://bennettfeely.com/clippy/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1eeb51d6-4a17-4774-ac1c-fbfe6def32cb/14-css-generators.png" width="700" height="480" sizes="100vw" caption="Clip-path generator for complex shapes in CSS. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1eeb51d6-4a17-4774-ac1c-fbfe6def32cb/14-css-generators.png'>Large preview</a>)" alt="Clippy" >}}

To start off, you select a shape and a demo background from Clippy’s menu. You can then drag the shape’s points to create any shape you like &mdash; the color-coded CSS will not only reflect your changes instantly but also highlight them to help you understand how your choices influence the code.

If the whole `clip-path` thing still feels a bit abstract to you or if you’re looking for a cool example of how to use it in an actual project, be sure to check out the [pop-out effect](https://codepen.io/ainalem/pen/QWGNzYm) that Mikael Ainalem created with `clip-path`.

## CSS Grid Layout Generator

CSS Grid Layout can be [quite](https://www.smashingmagazine.com/2020/01/understanding-css-grid-container/) [straightforward](https://www.smashingmagazine.com/2020/01/understanding-css-grid-lines/), but sometimes you might want to play with the Grid properties to figure out what just the right behavior would be for your layout. To get started, we can use Sarah Drasner’s [CSS Grid Generator](https://cssgrid-generator.netlify.app/), Drew Minns’ [Griddy](https://griddy.io/), Ali Alaa’s [CSS Grid Cheat Sheet Generator](https://alialaa.github.io/css-grid-cheat-sheet/) and LenioLabs’ [LayoutIt](https://grid.layoutit.com/) &mdash; they all allow you to define the grid and containers on the grid, as well as gaps, and it generates the CSS right away. If you need more guidance around Flexbox, [Flexbox Patterns](https://www.flexboxpatterns.com/) contains plenty of examples to play with.

{{< rimg href="https://cssgrid-generator.netlify.app/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c43d0fd-5a77-49db-a031-4f2f7cafe81d/15-css-generators.png" width="800" height="439" sizes="100vw" caption="CSS Grid Layout generator: a great little tool to experiment with your CSS Grid Layout. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c43d0fd-5a77-49db-a031-4f2f7cafe81d/15-css-generators.png'>Large preview</a>)" alt="Flexbox Patterns" >}}

Or you could use single line of CSS solutions. Una Kravets has built [1-Line Layouts](https://1linelayouts.glitch.me/), a collection of ten modern CSS layout and sizing techniques. Starting out with the biggest mystery of all (centering) and covering everything from the **classic Holy Grail Layout** and the “Deconstructed Pancake” to applying `clamp()` and respecting aspect ratio, Una’s collection is full of little tidbits that are bound to make your life as a developer easier.

Each technique comes with a demo, a CodePen to tinker with, and information on browser support. Una also recorded a **video** in which she explains every one-line wonder in greater detail. No matter if you’re a beginner or a pro, this resource will sure come in handy.

## CSS Compound Grids Generator

[Compound grids](https://www.smashingmagazine.com/2019/07/inspired-design-decisions-pressing-matters/) offer enormous flexibility and a lot of room for creativity. Made up of two or more grids of any type (column, modular, symmetrical, and asymmetrical) on one page, they can occupy separate areas or overlap.

{{< rimg href="https://codepen.io/michellebarker/full/zYOMYWv" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52c2464c-e8ed-4291-a06f-e9b95497b1b7/16-css-generators.png" width="700" height="410" sizes="100vw" caption="Compound Grid Generator (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52c2464c-e8ed-4291-a06f-e9b95497b1b7/16-css-generators.png'>Large preview</a>)" alt="Compound Grid Generator" >}}

A little tool to help you generate compound grids and save time drawing endless variations now comes from Michelle Barker: the [compound grid generator](https://codepen.io/michellebarker/full/zYOMYWv). All you need to do is enter the number of columns for each of your grids, and they’ll be merged into a compound grid. A great addition to your digital toolbox. And if you need to create a modular grid, multicolumn grid or manuscript grid for your print project, [Modular Grid Calculator](https://www.layoutgridcalculator.com/online/) provides a thorough explanation on achieve it in InDesign.

## CSS Filters and Blend Modes Generator

The CSS `drop-shadow` filter has excellent support but is rather underrated &mdash; a real shame given the fact that it could save you a lot of time hacking around with `box-shadow`.

{{< rimg href="https://css-irl.info/drop-shadow-the-underrated-css-filter/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfe67708-fdba-49a3-9ce2-ddb20c92d600/17-css-generators.png" width="700" height="390" sizes="100vw" caption="Box-shadow vs. drop-shadow (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfe67708-fdba-49a3-9ce2-ddb20c92d600/17-css-generators.png'>Large preview</a>)" alt="Box-shadow vs. drop-shadow" >}}

As Michelle Barker explains in a [blog post](https://css-irl.info/drop-shadow-the-underrated-css-filter/), `drop-shadow` lets you use values for x-offset, y-offset, blur radius, and color &mdash; just like its more prominent sibling `box-shadow`. However, there’s one big advantage: the shadow does not correspond to the bounding box of an element (which is often where the hacking begins when using `box-shadow`) but to the non-transparent parts of an image. Perfect if you want to apply a drop shadow to a transparent PNG or SVG logo, for example, or even a clipped shape.

There are [plenty of CSS filters](https://css-tricks.com/almanac/properties/f/filter/) out there, so if you need to find just the right set of filters for your project, Mads Stoumann’s [CSS Filter Editor](https://codepen.io/stoumann/pen/MWeNmyb) for testing out all **supported filters**, along with some presents that Mads has provided as well. Obviously, the CSS is generated on the fly as well.

Beyond filters, there are also plenty of options for [CSS blend modes](https://css-tricks.com/basics-css-blend-modes/). If you’d like to preview how some of the visual effects could work together, you can use Rick Metzger’s [CSS Duotone Generator](https://cssduotone.com/). The tool includes options for zooming, spacing, blur and image opacity, but also all blend modes for foreground and background images. Of course, the tool also generates HTML and CSS.

{{% feature-panel %}}

## Blurred Image Placeholders Generator

An image placeholder is an efficient way to improve a site’s perceived performance when an image is loading. On his quest to find the fastest and best-looking image placholders for the web, Joe Bell decided to come up with a solution himself. The result: [Plaiceholder](https://plaiceholder.co/).

{{< rimg href="https://plaiceholder.co/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f05aea7c-a0b2-4193-93f9-5dbde46ea3ff/18-css-generators.png" width="700" height="375" sizes="100vw" caption="A generator of blurred image placeholders. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f05aea7c-a0b2-4193-93f9-5dbde46ea3ff/18-css-generators.png'>Large preview</a>)" alt="Plaiceholder" >}}

Powered by a collection of Node.js helpers, Plaiceholder turns your images into lightweight, blurred placeholder images. There are several approaches to choose from: CSS (which is recommended), SVG, Base 64, [Blurhash](https://blurha.sh/), and the experimental [Blurhash to CSS](https://github.com/joe-bell/blurhash-to-css).

## Hero Generator

Are you tired of implementing the same hero over and over again? Sarah Drasner’s [Hero Generator](https://hero-generator.netlify.app/) is here to help. It lets you generate responsive heros with just a few clicks, based on your preferences.

{{< rimg href="https://hero-generator.netlify.app/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39a034f5-4c05-47d2-bf66-ba4a31bbe15d/hero-generator-opt.png" width="700" height="405" sizes="100vw" caption="Generate heros with ease. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39a034f5-4c05-47d2-bf66-ba4a31bbe15d/hero-generator-opt.png'>Large preview</a>)" alt="Hero Generator" >}}

You decide what kind of gradient you’d like to apply to your hero image, the gradient reduction, and title spacing. And if you wish to include a button, the generator has got you covered, too, with options to customize the button’s colors (including hover and gradient color) and button radius. Once you’re happy with the result, you can copy and paste the code and use it in your project right away. A real timesaver!

## Image Maps Generator

Image maps let you create clickable areas on an image. If you’d like to create an image map but don’t want to fiddle with coordinates to define the clickable regions, [imagemaps.net](https://www.imagemaps.net/) is here to help.

{{< rimg href="https://www.imagemaps.net/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fbc931e-c47f-4ccb-80cd-1905368e508f/imagemaps-opt.png" width="800" height="428" sizes="100vw" caption="Create annotated, interactive images. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fbc931e-c47f-4ccb-80cd-1905368e508f/imagemaps-opt.png'>Large preview</a>)" alt="Image map" >}}

The site features a graphical user interface to make the process more straightforward. Once you’ve uploaded your image, you can use the Pen, Rectangle, and Polygon tools to draw your clickable regions. To customize them and, most importantly, give them their functionality, you can then name each region, assign a link to it, and adjust its color, height and width. A click on the “Export” button provides you with the HTML map and React code that you can copy and paste into your project.

## CSS Animations Generator

It’s quite easy to tell a difference between an animation that seems to be a bit off, and an animation that is done just well. But adjusting the keyframes animations or transitions manually can be quite time-consuming. [Animista](https://animista.net/) provides a **library of animations and transitions** that you can use out of the box. There are plenty of presets for entrances and exits, text highlights, button actions and background effects. Once you’ve defined an animation you can copy-paste the CSS snippet of the animation, along with the code generated by Autoprefixer.

{{< rimg href="https://animista.net/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fe272ca-8cbc-41ec-9b35-9076f70a98ad/19-css-generators.png" width="800" height="641" sizes="100vw" caption="A comprehensive library of animations and transitions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fe272ca-8cbc-41ec-9b35-9076f70a98ad/19-css-generators.png'>Large preview</a>)" alt="Animista" >}}

[CSS Wand](https://www.csswand.dev/) provides **hover and loading animations**, but you can also use [Ladda animations](https://github.com/hakimel/Ladda) (buttons with built-in loading indicators) and [Eric Spinners](https://epic-spinners.epicmax.co/) (with Vue.js integration). And perhaps you’d like to add a whimsical twist on hover transitions with [Boop!](https://www.joshwcomeau.com/react/boop/) &mdash; just keep in mind to [scale with pseudo-elements](https://www.joshwcomeau.com/snippets/html/scale-with-pseudoelements/) and respect motion preferences for users who opt-in for reduced motion.

## 3D CSS Cuboid Generator

[Jhey Tompkins](https://twitter.com/jh3yy/) is known for his fun 3D CSS creations. Maybe you’ve already seen his [helicopter](https://codepen.io/jh3y/pen/WNRjxjP) that magically shifts as you move the mouse? The basis for the helicopter and other experiments like these are responsive CSS cuboids that are controllable with scoped CSS custom properties.

{{< rimg href="https://codepen.io/jh3y/pen/MWJdqBo" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b999788b-8fc5-4c63-be77-b5738b1b4175/3d-cuboid-generator-opt.png" width="800" height="510" sizes="100vw" caption="A generator to create animated 3D cuboids with ease. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b999788b-8fc5-4c63-be77-b5738b1b4175/3d-cuboid-generator-opt.png'>Large preview</a>)" alt="3D CSS Cuboid Generator" >}}

Now, if you want to bring your 3D ideas to life, too, Jhey’s [3D CSS Cuboid Generator](https://codepen.io/jh3y/pen/MWJdqBo) is here to help. Just adjust the sliders to determine height, width, depth, and hue of your cuboid, and you’ve already got the code you need to get things rolling, twisting, sliding, or whatever else you’re planning. Have fun!

## CSS Doodles Generator

We can bring the most sophisticated layouts to life with CSS, but we can also generate playful artworks and doodles. Yuan Chuan has built [<css-doodle/>](https://css-doodle.com/), a web component for **drawing patterns with CSS**. The component includes plenty of utility functions and shorthand properties to play with. As a result, the component generates a grid of `div`s along with the plain CSS. The source code is also [available on GitHub](https://github.com/css-doodle/css-doodle).

{{< rimg href="https://css-doodle.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c7c8607-7e04-4007-bd6b-6c1325492500/21-css-generators.png" width="800" height="411" sizes="100vw" caption="Drawing doodles with CSS? Sure thing, thanks to Yuan Chuan. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c7c8607-7e04-4007-bd6b-6c1325492500/21-css-generators.png'>Large preview</a>)" alt="CSS Doodles Generator" >}}


## Useful Little Web Dev Helpers

If you need a few more tools in your life, luckily, there are a lot of good ’ol web developers collecting their favorite **useful tools all in one place** named [Tiny Helpers](https://tiny-helpers.dev/). Maintained by Stefan Judis, you’re sure to find all sorts of tools: from APIs, accessibility and color, to fonts, performance, regular expressions, SVG, and Unicode.

{{< rimg href="https://tiny-helpers.dev/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a70059a2-74cd-4cf6-a8a5-701e777154b2/20-css-generators.png" width="800" height="458" sizes="100vw" caption="A growing repository of friendly and tiny helpers for web developers. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a70059a2-74cd-4cf6-a8a5-701e777154b2/20-css-generators.png'>Large preview</a>)" alt="Tiny Helpers" >}}

Of course, there are many more shared on other platforms, such as the very useful [Twitter thread by Josh W. Comeau](https://twitter.com/JoshWComeau/status/1212416797254832130) but also by [Stefan Judis](https://twitter.com/stefanjudis/status/1216788482972168193) himself. Whatever it is that you’ve been eager to find that will help you get work done better and faster, you’re bound to find it there!

## Wrapping Up

There are *literally* [hundreds](https://uitest.com/) of resources out there, and we hope that some of the ones listed here will prove to be useful in your day-to-day work &mdash; and most importantly help you avoid some time-consuming, routine tasks. Happy generating!

<div style="background-color: #f6f6f6;
border-radius:11px;padding: 15px 30px;margin-top: 1em">
    <h4 style="margin-top: 0.5em">More On CSS:</h4>
    <ul>
    <li><a href="https://www.smashingmagazine.com/2021/03/css-auditing-tools/">CSS Auditing Tools</a></li>
    <li><a href="https://www.smashingmagazine.com/2021/02/things-you-can-do-with-css-today/">Things You Can Do With CSS Today</a></li>
    <li><a href="https://www.smashingmagazine.com/2021/02/useful-chrome-firefox-devtools-tips-shortcuts/">Useful DevTools Tips and Shortcuts</a></li>
    <li>Also, <a href="/the-smashing-newsletter/">subscribe to our newsletter</a> to not miss the next ones.</li>
</ul>
</div>

{{< signature "cm, il, vf" >}}

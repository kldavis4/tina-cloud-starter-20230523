---
title: 'A Guide To Modern CSS Colors With RGB, HSL, HWB, LAB And LCH'
slug: guide-modern-css-colors
author: michelle-barker
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b424cd2e-1e44-4ca2-8506-4e45a5bdb570/guide-modern-css-colors.jpg
date: 2021-11-17T16:00:00.000Z
summary: >-
  Did you know that your chosen color palette can have an impact on how much energy your website uses? Even a more environmentally friendly choice of colors can reduce the impact on the battery life of mobile devices. In this article, Michelle Barker shares advice on the not-so-obvious things you have to keep in mind when handling colors in CSS today.
description: >-
  In this article, we’ll take a look at the best ways to handle colors in CSS today, some tips for using them in a design system, and what we can expect from our colors in the not-too-distant future.
categories:
  - CSS
  - Tools
  - Colors
  - Techniques
  - Design Systems
last_updated: 2021-11-18T08:30:00.000Z
updated_by: iris-ljesnjanin
---

There’s more to color on the web than meets the eye, and it’s about to get a lot more interesting! Today, we’ll take a look at the best ways to use colors in a design system, and what we can expect from our colors in the not-too-distant future.

## Well-Known Color Values

There are many different ways to define colors in CSS. [CSS named colors](https://css-tricks.com/snippets/css/named-colors-and-hex-equivalents/) are one of the simplest ways to color an element:

<pre><code class="language-css">.my-element {
  background-color: red;
}
</code></pre>

These are very limited, and rarely fit the designs we are building! We could also use color hex (hexadecimal) values. This code gives our element a red background color:

<pre><code class="language-css">.my-element {
  background-color: #ff0000;
}
</code></pre>

Unless you’re a color expert, hex values are very difficult to read. It’s unlikely you would be able to guess the color of an element by reading the hex value. When building a website we might be given a hex color value by a designer, but if they asked us to make it, say 20% darker, we would have a hard time doing that by adjusting the hex value, without a visual guide or color picker.

### RGB

RGB (red, green, blue) notation is an alternative way of writing colors, giving us access to the same range of colors as hex values, in a much more readable form. We have an `rgb()` function in CSS for this. Colors on the web are additive, meaning the higher the proportion of red, green and blue, the lighter the resulting color will be. If we only use the red channel, the result is red:

<pre><code class="language-css">.my-element {
  background-color: rgb(255, 0, 0);
}
</code></pre>

Setting the red, green and blue channels to the highest value will result in white:

<pre><code class="language-css">.my-element {
  background-color: rgb(255, 255, 255);
}
</code></pre>

We can also add an alpha channel (for transparency), by using the `rgba()` function:

<pre><code class="language-css">.my-element {
  background-color: rgba(255, 0, 0, 0.5); // transparency of 50%
}

.my-element {
  background-color: rgba(255, 0, 0, 1); // fully opaque
}
</code></pre>

`rgb()` and `rgba()` allow us to “mix” colors in our code to some extent, but the results can be somewhat unpredictable.

### HSL

More recently, we have been able to use HSL (hue, saturation, lightness) values, with the `hsl()` and `hsla()` color functions. As a developer, these are far more intuitive when it comes to adjusting color values. For example, we can get darker and lighter variants of the same color by adjusting the `lightness` parameter:

<pre><code class="language-css">.my-element {
  background-color: hsl(0deg, 100%, 20%); // dark red
}

.my-element {
  background-color: hsl(0deg, 100%, 50%); // medium red
}

.my-element {
  background-color: hsl(0deg, 100%, 80%); // light red
}
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6d3545f-7d8b-497a-99be-6f4bb8704b64/1-modern-css-color.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6d3545f-7d8b-497a-99be-6f4bb8704b64/1-modern-css-color.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6d3545f-7d8b-497a-99be-6f4bb8704b64/1-modern-css-color.png'>Large preview</a>)" alt="Three color swatches resulting from the previous code, ranging from dark to light red" >}}

The `hue` parameter represents the position on a color wheel, and can be any value between `0` and `360deg`. The function also accepts turn units (e.g. `0.5turn`), and unitless values.

The following are all valid:

<pre><code class="language-css">.my-element {
  background-color: hsl(180deg, 50%, 50%);
}

.my-element {
  background-color: hsl(0.5turn, 50%, 50%);
}

.my-element {
  background-color: hsl(180, 50%, 50%);
}
</code></pre>

**Tip**: Holding down <kbd>SHIFT</kbd> and clicking the color swatch in the inspector in Chrome and Firefox dev tools will toggle the color value between hex, RGB and HSL!

`hsl()` and `hsla()` lend themselves well to manipulation with custom properties, as we’ll see shortly.

### `currentColor`

The `currentColor` keyword is worth a mention as another way of setting a color on an element that’s been around for a while. It effectively allows us to use the current text color of an element as a variable. It’s pretty limited when compared with custom properties, but it’s often used for setting the fill color of SVG icons, to ensure they match the text color of their parent. [Read about it here](https://css-tricks.com/cascading-svg-fill-color/).

{{% feature-panel %}}

## Modern Color Syntax

The [CSS Color Module Level 4](https://www.w3.org/TR/css-color-4) provides us with a more convenient syntax for our color functions, which is [widely supported in browsers](https://caniuse.com/?search=space-separated). We no longer need the values to be comma-separated, and the `rgb()` and `hsl()` functions can take an optional alpha parameter, separated with a forward slash:

<pre><code class="language-css">.my-element {
  /* optional alpha value gives us 50% opacity */
  background-color: hsl(0 100% 50% / 0.5);
}

.my-element {
  /* With no alpha value the background is fully opaque*/
  background-color: hsl(0 100% 50%);
}
</code></pre>

## New CSS Color Functions

### HWB

HWB stands for hue, whiteness and blackness. Like HSL, the hue can be anywhere within a range of 0 to 360. The other two arguments control how much white or black is mixed into that hue, up to 100% (which would result in a totally white or totally black color). If equal amounts of white and black are mixed in, the color becomes increasingly gray. We can think of this as being similar to mixing paint. It could be especially useful for creating monochrome color palettes.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/536ab898-2bb4-4c42-a9f1-e46bf1da7f63/2-modern-css-color.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/536ab898-2bb4-4c42-a9f1-e46bf1da7f63/2-modern-css-color.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/536ab898-2bb4-4c42-a9f1-e46bf1da7f63/2-modern-css-color.png'>Large preview</a>)" alt="Five color swatches resulting from HWB colors with different amounts of white/black" >}}

Try it out with [this demo](https://codepen.io/smashingmag/pen/xxLmOgV) (works in Safari only):

{{< codepen height="480" theme_id="light" slug_hash="xxLmOgV" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [HWB color (Safari only)](https://codepen.io/smashingmag/pen/xxLmOgV) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

### LAB

LAB and LCH are defined in the [specification](https://www.w3.org/TR/css-color-4/#specifying-lab-lch) as **device-independent colors**. LAB is a color space that can be accessed in software like Photoshop and is recommended if you want a color to look the same on-screen as, say, printed on a t-shirt. It uses three axes: lightness, followed by the *a-axis* (green to red) and *b-axis* (blue to yellow).

Lightness is expressed as a percentage, much like HSL, but can in fact exceed 100% when used with the `lab()` color function. Extra-bright whites can use a percentage of up to 400%. Values for the *a* and *b* axes can range from positive to negative. Two negative values will result in a color towards the green/blue end of the spectrum, while two positive values can give a more orange/red hue.

<pre><code class="language-css">.my-element {
  background-color: lab(80% 100 50); // reddish pink
}

.my-element {
  background-color: lab(80% -80 -100); // blue/turquoise
}
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da33544f-aab5-4fc3-81d9-d3e5f75442d4/3-modern-css-color.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da33544f-aab5-4fc3-81d9-d3e5f75442d4/3-modern-css-color.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da33544f-aab5-4fc3-81d9-d3e5f75442d4/3-modern-css-color.png'>Large preview</a>)" alt="Red/pink color swatch with positive a/b values, blue/turquoise color swatch with negative a/b values" >}}

{{< codepen height="480" theme_id="light" slug_hash="JjywKNK" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [LAB Color (Safari only)](https://codepen.io/smashingmag/pen/JjywKNK) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

### LCH

LCH stands for lightness, chroma, and hue. As with LAB, *lightness* can be a percentage that exceeds 100%. Similar to HSL, *hue* can be a range between 0 and 360. Chroma represents the *amount* of color, and we can think of it as being similar to saturation in HSL. But chroma can exceed 100 — in fact, it’s theoretically unbounded. Example usage:

<pre><code class="language-css">.my-element {
  background-color: lch(80% 100 50);
}

.my-element {
  background-color: lch(80% 240 50); // this color would be outside of the displayable range of today’s browsers
}
</code></pre>

However, there is a limit on how many colors browsers and monitors today can display (more on that shortly), so values above 230 are unlikely to make a difference — the Chroma is reduced until it is within range.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71cf899c-c146-484e-bb1a-5a26e9e7c55d/4-modern-css-color.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71cf899c-c146-484e-bb1a-5a26e9e7c55d/4-modern-css-color.png" width="800" height="" sizes="100vw" caption="The final color on the right is outside the displayable range (gamut), so no difference is perceived. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71cf899c-c146-484e-bb1a-5a26e9e7c55d/4-modern-css-color.png'>Large preview</a>)" alt="Four LCH color swatches with red hue, varying chroma levels" >}}

Why do we need LAB and LCH when we have HSL? One reason is that using LAB or LCH, gives us access to a much larger range of colors. LCH and LAB are designed to give us access to the entire spectrum of human vision. Furthermore, HSL and RGB have a few shortcomings: they are not perceptually uniform and, in HSL, increasing or decreasing the lightness has quite a different effect depending on the hue.

In [this demo](https://codepen.io/smashingmag/pen/yLoGJXd), we can see a stark contrast between LCH and HSL by hitting the grayscale toggle. For the HSL hue and saturation strips, there are clear differences in the perceptual lightness of each square, even though the “lightness” component of the HSL function is the same! Meanwhile, the chroma and hue strips on the LCH side have an almost-uniform perceptual lightness.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4253d9b2-46d7-4b10-9e1a-b5f3ac6cea1c/5-modern-css-color.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4253d9b2-46d7-4b10-9e1a-b5f3ac6cea1c/5-modern-css-color.png" width="800" height="" sizes="100vw" caption="By applying a grayscale filter we can see that the LCH colors (left) have an almost-uniform lightness when we adjust the chroma and hue, compared to when we adjust the hue and saturation of the HSL colors (right), where there are visible differences in lightness. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4253d9b2-46d7-4b10-9e1a-b5f3ac6cea1c/5-modern-css-color.png'>Large preview</a>)" alt="LCH and HSL color swatches compared side-by-side" >}}

We can also see a big difference when using LCH color for gradients. Both these gradients start and end with the same color (with LCH values converted to the HSL equivalents using [this converter](http://colormine.org/convert/lch-to-hsl)). But the LCH gradient goes through vibrant shades of blue and purple in the middle, whereas the HSL gradient looks muddier and washed-out by comparison.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72ba74de-3574-4301-ab9c-03b37c52acf6/6-modern-css-color.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72ba74de-3574-4301-ab9c-03b37c52acf6/6-modern-css-color.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72ba74de-3574-4301-ab9c-03b37c52acf6/6-modern-css-color.png'>Large preview</a>)" alt="LCH and HSL blue to pink gradient strips" >}}

- [See the demo&nbsp;&rarr;](https://codepen.io/smashingmag/pen/VwzqjzW)

LAB and LCH, while perhaps being syntactically a little less intuitive, behave in a way that makes more sense to the human eye. In her article, [LCH color in CSS: what, why, and how?](https://lea.verou.me/2020/04/lch-colors-in-css-what-why-and-how/), Lea Verou explains in detail the advantages of LCH color. She also built this [LCH color picker](https://css.land/lch/).

As with other color functions, `hwb()`, `lab()` and `lch()` can also take an optional alpha parameter.

<pre><code class="language-css">.my-element {
  background-color: lch(80% 240 50 / 0.5); // Resulting color has 50% opacity
}
</code></pre>

{{% ad-panel-leaderboard %}}

## Browser Support And Color Spaces

`hwb()`, `lab()` and `lch()` are currently only supported in Safari. It’s possible to start using them straight away by providing a fallback for non-supporting browsers. Browsers that don’t support the color function will simple ignore the second rule:

<pre><code class="language-css">.my-element {
  background-color: lch(55% 102 360);

  /* LCH color converted to RGB using Lea Verou’s tool: https://css.land/lch/ */
  background-color: rgb(98.38% 0% 53.33%);
}
</code></pre>

If other styles depend on newer color functions being supported, we could use a feature query:

<pre><code class="language-css">.my-element {
  display: none;
}

/* Only display this element if the browser supports lch() */
@supports (background-color: lch(55% 102 360)) {
  .my-element {
    display: block;
    background-color: lch(55% 102 360);
  }
}
</code></pre>

It’s worth noting, as Lea explains in her article, that although modern screens are capable of displaying colors beyond RGB, most browsers currently only support colors within the sRGB color space. In the [LAB color demo](https://codepen.io/smashingmag/pen/KKvbMXY) you might notice that moving the sliders beyond a certain point doesn’t actually affect the color, even in Safari where `lab()` and `lch()` are supported. Using values outside of the sRGB range will only have an effect when hardware and browsers advance sufficiently.

Safari now supports the `color()` function, which enables us to display colors in the P3 space, but these are limited to RGB colors for now, and don’t yet give us all the advantages of LAB and LCH.

<pre><code class="language-css">.my-element {
  background: rgb(98.38% 0% 53.33%); // bright pink
  background: color(display-p3 0.947 0 0.5295); // equivalent in P3 color space
}
</code></pre>

**Recommended Reading**: *“[Wide Gamut Color in CSS with Display-P3](https://webkit.org/blog/10042/wide-gamut-color-in-css-with-display-p3/)” by Nikita Vasilyev*

## Accessibility

Once they are widely supported, perhaps LAB and LCH can help us choose more accessible color combinations. Foreground text should have the same contrast ratio with background colors with different hue or chroma values, as long as their lightness value remains the same. That’s certainly not the case at the moment with HSL colors.

## Color Management

A wider range of color functions means we have more options when it comes to managing colors in our application. Often we require several variants of a given color in our design system, ranging from dark to light.

### Custom Properties

CSS custom properties allow us to store values for reuse in our stylesheets. As they allow partial property values, they can be especially useful for managing and manipulating color values. HSL lends itself particularly well to custom properties, due to its intuitiveness. In the previous demo, I’m using them to adjust the hue for each segment of the color strip by calculating a `--hue` value based on the element’s index (defined in another custom property). 

<pre><code class="language-css">li {
  --hue: calc(var(--i) * (360 / 10));
  background: hsl(var(--hue, 0) 50% 45%);
}
</code></pre>

We can also do things like calculate complementary colors (colors from opposite sides of the color wheel). Plenty has been written about this, so I won’t cover old ground here, but if you’re curious then Sara Soueidan’s article on [color management with HSL](https://www.sarasoueidan.com/blog/hex-rgb-to-hsl/) is a great place to start. 

### Migrating From Hex/RGB To HSL

RGB colors might serve your needs up to a point, but if you need the flexibility to be able to derive new shades from your base color palette then you might be better off switching to HSL (or LCH, once supported). I would recommend embracing custom properties for this.

**Note**: *There are plenty of online resources for converting hex or RGB values to HSL (here’s [one example](https://www.w3docs.com/tools/color-rgb)).*

Perhaps you have colors stored as Sass variables:

<pre><code class="language-css">$primary: rgb(141 66 245);
</code></pre>

When converting to HSL, we can assign custom properties for the hue, saturation and lightness values. This makes it easy to create darker or lighter, more or less saturated variants of the original color.

<pre><code class="language-css">:root {
  --h: 265;
  --s: 70%;
  --l: 50%;
        
  --primary: hsl(var(--h) var(--s) var(--l));
  --primaryDark: hsl(var(--h) var(--s) 35%);
  --primaryLight: hsl(var(--h) var(--s) 75%);
}
</code></pre>

HSL can be incredibly useful for creating color schemes, as detailed in the article  [Building a Color Scheme](https://web.dev/building-a-color-scheme/) by Adam Argyle. In the article he creates light, dark and dim color schemes, using a brand color as a base. I like this approach because it allows for some fine-grained control over the color variant (for example, decreasing the saturation for colors in the “dark” scheme), but still retains the big advantage of custom properties: updating the brand color in just one place will be carried through to all the color schemes, so it could potentially save us a lot of work in the future.

### Sass Color Functions

When it comes to mixing and adjusting colors, Sass has provided [color functions](https://sass-lang.com/documentation/modules/color) to enable us to do just this for many years. We can saturate or desaturate, lighten or darken, even mix two colors together. These work great in some cases, but they have some limitations: firstly, we can only use them at compile-time, not for manipulating colors live in the browser. Secondly, they are limited to RGB and HSL, so they suffer from the same issues of perceptual uniformity, as we can see in [this demo](https://codepen.io/smashingmag/pen/abyPZVZ), where a color is increasingly desaturated yet appears increasingly lighter when converted to grayscale.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad752292-91a6-4289-b31b-784776b86a06/7-modern-css-color.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad752292-91a6-4289-b31b-784776b86a06/7-modern-css-color.png" width="800" height="" sizes="100vw" caption="The top strip has a grayscale filter applied. As we decrease the saturation of the main red color using Sass (bottom), we can see that the color actually becomes lighter. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad752292-91a6-4289-b31b-784776b86a06/7-modern-css-color.png'>Large preview</a>)" alt="Red color swatches increasingly desaturated, with grayscale filter applied to top half" >}}

To ensure that the lightness remains uniform, we could use custom properties with LCH in a similar way to HSL above.

<pre><code class="language-css">li {
  --hue: calc(var(--i) * (360 / 10));
  background: lch(50% 45 var(--hue, 0));
}
</code></pre>

## Color Mixing And Manipulation

### Color Mixing

One thing CSS doesn’t *yet* allow us to do is mix colors in the browser. That’s all about to change: the [Level 5 CSS Color Specification](https://www.w3.org/TR/css-color-5/#color-mix) (working draft) contains proposals for color mixing functions that sound rather promising. The first is the `color-mix()` function, which mixes two colors much like Sass’s `mix()` function. But `color-mix()` in CSS allows us to specify a color space, and uses the LCH by default, with superior mixing as a result.

**Update**: *`color-mix()` and `color-contrast()` are now available behind a flag in Safari 15! Check out [this article](https://appademic.tech/safari-hidden-features-debug-menu/) on how to enable experimental features in Safari.*

The colors don’t have to be LCH when passed in as arguments either, but the interpolation will use the specified color space. We can specify how much of each color to mix, similar to gradient stops:

<pre><code class="language-css">.my-element {
  /* equal amounts of red and blue */
  background-color: color-mix(in lch, red, blue);
}

.my-element {
  /* 30% red, 70% blue */
  background-color: color-mix(in lch, red 30%, blue);
}
</code></pre>

### Color Contrast And Accessibility

`color-contrast()` is another proposed function, which really does have huge implications for picking accessible colors. In fact, it’s designed with accessibility in mind first and foremost. It permits the browser to pick the most appropriate value from a list, by comparing it with another color. We can even specify the desired contrast ratio to ensure our color schemes meet WCAG guidelines. Colors are evaluated from left to right, and the browser picks the first color from the list that meets the desired ratio. If no colors meet the ratio, the chosen color will be the one with the highest contrast.

<pre><code class="language-css">.my-element {
  color: wheat;
  background-color: color-contrast(wheat vs bisque, darkgoldenrod, olive, sienna, darkgreen, maroon to AA);
}
</code></pre>

Because this isn’t supported in any browsers right now, I’ve borrowed this example directly from the spec. when the browser evaluates the expression the resulting color will be `darkgreen`, as it is the first one that meets the AA contrast ratio when compared to `wheat`, the color of the text.

### Browser Support

The Level 5 Color Specification is currently in Working Draft, meaning no browsers yet support the `color-contrast()` and `color-mix()` functions and their syntax is subject to change. But it certainly looks like a bright future for color on the web!

{{% ad-panel-leaderboard %}}

## Environmental Impact Of Colors

Did you know that your chosen color palette can have an impact on how much energy your website uses? On OLED screens (which account for most modern TVs and laptops), darker colors will use significantly less energy than light colors &mdash; with white using the most energy, and black the least. According to Tom Greenwood, author of [Sustainable Web Design](https://abookapart.com/products/sustainable-web-design), blue is also more energy-intensive than colors in the red and green areas of the spectrum. To reduce the environmental impact of your applications, consider a darker color scheme, using less blue, or enabling a dark-mode option for your users. As an added bonus, a more environmentally friendly choice of colors can also reduce the impact on the battery life of mobile devices.

## Tools

- [Hexplorer](https://codepen.io/robdimarzo/full/xxZgKOR), Rob DiMarzo  
*Learn to understand hex colors with this interactive visualization.*
- [LCH color picker](https://css.land/lch/), Lea Verou and Chris Lilley  
*Get LCH colors and their RGB counterparts.*
- [HWB color picker](https://www.w3docs.com/tools/color-hwb)  
*Visualize HWB colors and convert to HSL, RGB and hex.*
- [Ally Color Tokens](https://github.com/5t3ph/a11y-color-tokens), Stephanie Eckles  
*An accessible color token generator.*

## Resources

- “[A Nerd’s Guide To Color On The Web](https://css-tricks.com/nerds-guide-color-web/),” Sarah Drasner, CSS-Tricks
- “[LCH Colors In CSS: What, Why, And How?](https://lea.verou.me/2020/04/lch-colors-in-css-what-why-and-how/),” Lea Verou
- “[The Best Color Functions In CSS?](https://css-tricks.com/the-best-color-functions-in-css/),” Chris Coyier, CSS-Tricks
- “[Building A Color Scheme](https://web.dev/building-a-color-scheme/),” Adam Argyle, Web.dev
- “[Using HSL Colors In CSS](https://www.smashingmagazine.com/2021/07/hsl-colors-css/),” Ahmad Shaheed, Smashing Magazine
- “[On Switching From Hex And RGB To HSL](https://www.sarasoueidan.com/blog/hex-rgb-to-hsl/),” Sara Soueidan
- “[Improving Color On The Web](https://webkit.org/blog/6682/improving-color-on-the-web/),” Dean Jackson, Webkit Blog

{{< signature "vf, il" >}}

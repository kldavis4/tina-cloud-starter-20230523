---
title: 'Simplify Your Color Palette With CSS Color-Mix()'
slug: simplify-color-palette-css-color-mix
author: daniel-yuschick
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57b9844c-e3aa-48e2-9d72-3938dbf553d0/simplify-color-palette-css-color-mix-sharing-card.jpg
date: 2022-06-08T09:00:00.000Z
summary: >-
  Defining a color palette and theme can be a lot of work, especially when considering contextual colors for elements’ various states. While CSS `color-mix()` *only* blends two colors together, this little function may be the key to maximizing your colors without maximum effort.
description: >-
  CSS color-mix is an experimental function that blends two colors and can be used to simplify color palettes. You can define a color palette and theme without too much effort using CSS color-mix().
categories:
  - CSS
  - Design Systems
  - Techniques
  - Tools
---

There’s a reason for all the new, experimental color features CSS is introducing. And there’s a reason for all the excitement they’re stirring up.

Colors are hard. Defining a base color palette can be time-consuming and involve quite a few stakeholders. And that’s not even considering contextual colors, like hover, active and inactive states. Defining these values requires even more time and more attention to accessibility. This can result in a bloated palette and an even more bloated set of design tokens.

It can be a lot to juggle. 🤹 

While the CSS `color-mix()` function may *only* blend two colors together, could it be used to simplify color palettes and streamline contextual values across themes?

## The CSS Color-Mix() Function

The CSS `color-mix()` function is an experimental feature that is currently a part of the [Color Module 5](https://www.w3.org/TR/css-color-5/#colorcontrast). True to its name, the function will accept any two colors, mix them together and return a little *color Frankenstein*.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d689d10c-559f-4174-9ce1-01703fd73d84/1-simplify-color-palette-css-color-mix.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d689d10c-559f-4174-9ce1-01703fd73d84/1-simplify-color-palette-css-color-mix.jpg" width="800" height="332" sizes="100vw" caption="CSS Color-Mix() required syntax (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d689d10c-559f-4174-9ce1-01703fd73d84/1-simplify-color-palette-css-color-mix.jpg'>Large preview</a>)" alt="color-mix funcion parts explained. For a line color-mix( in HSL, red 50%, white ); HSL is to set the resulting color space. Red is a base color and 50% is a percentage of the base color. White is the blend color." >}}

For the sake of this article, let’s define how these arguments will be called while using this example.

- **Color Space** would refer to `HSL`;
- **Base Color** would refer to `red`;
- **Base Percent** would refer to `50%`;
- **Blend Color** would refer to `white`;
- **Blend Percent**, not shown in this example, will refer to a value covered later.

There are quite a few moving pieces here, so let’s have a quick interactive visual to simulate the base color, base percent, and blend color.

{{< codepen height="300" theme_id="light" slug_hash="jOZvVqM" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [CSS Color-Mix – Base Color Percentage Demo](https://codepen.io/smashingmag/pen/jOZvVqM) by <a href="https://codepen.io/DanielYuschick">Daniel Yuschick</a>.{{< /codepen >}}

{{< vimeo id="717996422" caption="Results of color-mix blending two colors with different percentages" breakout="true" >}}

Like with any experimental feature, the syntax or features could change before widespread browser adoption. However, the features in Color Module 5 seem stable enough to, at the very least, begin tinkering ourselves.

At the time of writing this article, browser support is very limited (as in, all but non-existent). The feature can be toggled behind development flags in both Firefox and [Safari Technology Preview](https://developer.apple.com/safari/technology-preview). But the web moves fast, and it’s probably worth visiting [Color-Mix() On Caniuse](https://caniuse.com/?search=color-mix) to see the latest (and hopefully greatest) support.

Now, with the formalities out of the way, grab some dark rum, ginger beer, and lime juice, and let’s get mixing.

## Throwback Art Class 🎨 

Do you remember learning about the color wheel in art class?

The primary colors anchored the wheel, and when blended, they formed the secondary layer. Lastly, by blending the secondary layer, the tertiary colors were formed. The wheel was complete.

Disregarding the lack of a visual wheel here, CSS `color-mix()` can be used to create the same effect.

{{< codepen height="300" theme_id="light" slug_hash="GRQXNZb" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [CSS Color-Mix – Art Class Demo](https://codepen.io/smashingmag/pen/GRQXNZb) by <a href="https://codepen.io/DanielYuschick">Daniel Yuschick</a>.{{< /codepen >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8c91d82-c781-4f5b-9e12-dd2b0bfe59dd/3-simplify-color-palette-css-color-mix.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8c91d82-c781-4f5b-9e12-dd2b0bfe59dd/3-simplify-color-palette-css-color-mix.jpg" width="800" height="275" sizes="100vw" caption="Result of using color-mix to recreate the a linear color wheel (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8c91d82-c781-4f5b-9e12-dd2b0bfe59dd/3-simplify-color-palette-css-color-mix.jpg'>Large preview</a>)" alt="display of colors to show the mixing of primary and secondary colors." >}}

Building the linear color wheel was a lot of fun and a great dive into using `color-mix()`. It often helps when experimenting with a new feature to already know what the visual outcome should be. 

So how does this work?

First: Define the base primary colors.

<pre><code class="language-css">--primary-1: #ff0;
--primary-2: #f00;
--primary-3: #00f;
</code></pre>

Next: Mix the primary colors to create the secondary colors.

<pre><code class="language-javascript">--secondary-1: color-mix(in srgb, var(--primary-1) 50%, var(--primary-2));
--secondary-2: color-mix(in srgb, var(--primary-2) 50%, var(--primary-3));
--secondary-3: color-mix(in srgb, var(--primary-3) 50%, var(--primary-1));
</code></pre>

Last: Mix the primary and secondary colors to create the tertiary colors.

<pre><code class="language-javascript">--tertiary-1: color-mix(in srgb, var(--primary-1) 50%, var(--secondary-1));
--tertiary-2: color-mix(in srgb, var(--secondary-1) 50%, var(--primary-2));
--tertiary-3: color-mix(in srgb, var(--primary-2) 50%, var(--secondary-2));
--tertiary-4: color-mix(in srgb, var(--secondary-2) 50%, var(--primary-3));
--tertiary-5: color-mix(in srgb, var(--primary-3) 50%, var(--secondary-3));
--tertiary-6: color-mix(in srgb, var(--secondary-3) 50%, var(--primary-1));
</code></pre>

Of course, when I was in art class, there was only one set of paints. So if you wanted yellow, there was only one yellow. Red? There was only one red. Blue? Well, you get the idea. 

But the web and CSS offer a much wider selection of colors in the way of *‘color spaces.’* Some of these color spaces may already be familiar, but there were quite a few I hadn’t used before, including [four new CSS color features](https://css-tricks.com/new-css-color-features-preview/) which are gradually gaining support.

Color spaces can calculate their colors differently from one another. Newer color spaces provide wider palettes with more vivid shades to maximize the latest screen technologies &mdash; like ultra-high-definition retina displays. It means that a single color may appear differently across each color space.

Knowing the CSS `color-mix()` function supports using different color spaces, let’s experiment with color spaces by replacing the use of `srgb` from the previous example with a custom property to see how the color wheel changes.

{{< codepen height="300" theme_id="light" slug_hash="ZErMBOy" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [CSS Color-Mix – Color Space Demo](https://codepen.io/smashingmag/pen/ZErMBOy) by <a href="https://codepen.io/DanielYuschick">Daniel Yuschick</a>.{{< /codepen >}}

{{< vimeo id="717996445" caption="Using color-mix to toggle the mixture’s color space" breakout="true" >}}

The `color-mix()` function isn’t limited to only blending HEX codes either. In fact, it can mix multiple color types at once. The previous example can be modified to use different color types while returning the same results.

First: Define the base primary colors

<pre><code class="language-css">--primary-1: yellow;
--primary-2: rgb(255,0,0);
--primary-3: hsl(240,100%,50%);
</code></pre>

Next: Mix the primary colors to create the secondary colors

<pre><code class="language-javascript">--secondary-1: color-mix(in srgb, var(--primary-1) 50%, var(--primary-2));
--secondary-2: color-mix(in srgb, var(--primary-2) 50%, var(--primary-3));
--secondary-3: color-mix(in srgb, var(--primary-3) 50%, var(--primary-1));
</code></pre>

{{% feature-panel %}}

## Mixing N’ Matching

Recreating childhood art class is fun, but those concepts can be taken further and applied more practically to our adulthood hobbies and careers.

<blockquote>A lot of time can be spent defining every color variation and shade, but color-mix() can blend theme values together to fill in those variation gaps.</blockquote>

Let’s take a look at contextual UI colors, like button `:hover` and `:active` states. A lot of time can be spent defining these values to ensure they’re cohesive with the current theme and accessible. But when themes often include primary dark and light colors already, could these values be mixed to create contextual colors a bit more automatically?

{{< codepen height="300" theme_id="light" slug_hash="gOvdLMV" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [CSS Color-Mix() – Contextual Button Demo](https://codepen.io/smashingmag/pen/gOvdLMV) by <a href="https://codepen.io/DanielYuschick">Daniel Yuschick</a>.{{< /codepen >}}

{{< vimeo id="717996481" caption="Using color-mix to blend theme colors to create contextual shade" breakout="true" >}}

While a similar effect could be created with [the HWB color function](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/hwb) by increasing the button color’s blackness value, sometimes darkening a button isn’t just a matter of mixing in a splash of black. Just ask anybody who’s ever struggled finding the perfect dark mode theme. This is also where `color-mix()` stands out from Sass `darken()` and `lighten()` functions. The `color-mix()` function gives greater and granular control of how colors are adjusted, and it does so natively to CSS.

By mixing a specific theme value, like `--color-dark-primary` , the pseudo-states can be created while remaining visually cohesive with the rest of the theme.

Additionally, a `color-mix()` result can be used as the base color in another `color-mix()` function. This is done in the demo to define the buttons’ `:active` states relative to their `:hover` state.

<blockquote>When specifying a base percentage, the blend color is mixed with a percentage that would total 100%. If the base percentage is 75%, the blend percent will be 25%.</blockquote>

<pre><code class="language-css"> :root {
  --color-dark-primary: #dedbd2;
}

button {
  --btn-bg: #087e8b;
  --btn-bg-hover: color-mix(in srgb, var(--btn-bg) 75%, var(--color-dark-primary));
  --btn-bg-active: color-mix(in srgb, var(--btn-bg-hover) 80%, var(--color-dark-primary));

  background: var(--btn-bg);

  &:hover {
    background: var(--btn-bg-hover);
  }

  &:active {
    background: var(--btn-bg-active);
  }
}
</code></pre>

In this example, the `--btn-bg-hover` value is defined by mixing 75% of `--btn-bg` with `--color-dark-primary`. Then, `--btn-bg-active` is set by mixing 80% of `--btn-bg-hover` with `--color-dark-primary` again.

It’s important to note when specifying a base percentage that the blend color is mixed with a percentage that would total 100%. If the base is 75%, the blend percent will be 25%.

However, this becomes a bit complicated when introducing a separate blend percent.

## Mixing Mastery With Blend Percents

As an optional argument for `color-mix()`, the blend percent introduces an additional level of mix mastery. In the previous examples, without a blend percentage, the blend color would automatically use a value that, when added to the base percent, totaled 100.

If the base percent was 50, the blend percent would be 50. If the base percent was 99, the blend percent would be 1.

However, specifying a custom blend percent means the percentage total may not always round out so evenly.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58f26747-9e38-413a-96fd-cc6aab9ffd91/6-simplify-color-palette-css-color-mix.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58f26747-9e38-413a-96fd-cc6aab9ffd91/6-simplify-color-palette-css-color-mix.jpg" width="800" height="285" sizes="100vw" caption="Optionally define a blend color percentage (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58f26747-9e38-413a-96fd-cc6aab9ffd91/6-simplify-color-palette-css-color-mix.jpg'>Large preview</a>)" alt="color-mix funcion parts explained. For a line color-mix( in HSL, red 50%, white ); HSL is to set the resulting color space. Red is a base color and 50% is a percentage of the base color. White is the blend color." >}}

While the [W3 docs](https://www.w3.org/TR/css-color-5/#color-mix) explain the calculations behind this functionality quite well, the math is a tad beyond my abilities to explain clearly &mdash; this is art class, after all. But, as best as I can put it:

<pre><code class="language-javascript">--math-bg: color-mix(in srgb, red 20%, white 60%);
</code></pre>

In this example, the base percentage is `20` while the blend percent is `60` creating a total of `80`. This gives us, what’s called, an alpha multiplier of `0.8` where `1 = 100` and `0.8 = 80%`.

To fill in the gaps, the function will multiply the base and blend percentages by this alpha multiplier to scale them up to 100% while remaining relative to their original weights.

<pre><code class="language-javascript">20% * 100/80 = 25%
60% * 100/80 = 75%

--math-bg: color-mix(in srgb, red 25%, white 75%);
</code></pre>

If the base and blend percentages total more than 100, the inverse of this approach would be taken to round down to 100. Again, the math behind the scaling of these values, along with the general mixing calculations, is beyond my depth. For those interested in digging deeper into the technicalities of `color-mix()`, I would point to [the W3 docs](https://www.w3.org/TR/css-color-5/#color-mix-with-alpha).

However, that mathematical understanding isn’t required for the below demo, where both the base and blend percentages can be adjusted to view the result.

{{< codepen height="300" theme_id="light" slug_hash="rNJZWMY" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [CSS Color-Mix – Blend Color Percentage Demo](https://codepen.io/smashingmag/pen/rNJZWMY) by <a href="https://codepen.io/DanielYuschick">Daniel Yuschick</a>.{{< /codepen >}}

{{< vimeo id="717996501" caption="Using color-mix with base and blend percentages" breakout="true" >}}

{{% ad-panel-leaderboard %}}

## Actin’ Shady With Transparencies

Colors with transparency add another level to the `color-mix()` function. The concept seemed complicated, but after experimenting, opacities look to mix similar to the opaque mix percentages.

<pre><code class="language-css"> :root {
  --base-opacity: 50%;
  --blend-opacity: 50%;
  --base-color: rgba(255, 0, 0, var(--base-opacity));
  --blend-color: rgba(0, 0, 255, var(--blend-opacity));
}

#result {
  background: color-mix(in lch, var(--base-color) 50%, var(--blend-color));
}
</code></pre>

In this sample, the base color is red, and the blend color is blue. In normal circumstances, these colors would mix to create pink. However, each color is defined using `rgba` and a `50%` opacity.

The result is the expected pink shade but with an averaged opacity. If the base opacity is `100%` and the blending opacity is `0%`, the resulting opacity will be `50%`. But regardless of the resulting opacity, the 50/50 color mix keeps its consistent pink shade.

{{< codepen height="300" theme_id="light" slug_hash="mdXGOrZ" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [CSS Color-Mix – Opacities Demo](https://codepen.io/smashingmag/pen/mdXGOrZ) by <a href="https://codepen.io/DanielYuschick">Daniel Yuschick</a>.{{< /codepen >}}

{{< vimeo id="717996528" caption="The results of using color-mix with transparent colors" breakout="true" >}}

## A Dash Of Caution

There are inevitable drawbacks to consider, as with any experimental or new feature, and `color-mix()` is no different.

### Custom Properties And Fallbacks

Since CSS custom properties support fallback values for when the property is not defined, it seemed like a good approach to use `color-mix()` as a progressive enhancement.

<pre><code class="language-javascript">--background-color: color-mix(in srgb, red 50%, blue);
background: var(--background-color, var(--fallback-color));
</code></pre>

If `color-mix()` is not supported, the `--background-color` property would not be defined, and therefore the `--fallback-color` would be used. Unfortunately, that’s not how this works.

An interesting thing happens in unsupported browsers &mdash; the custom property would be defined with the function itself. Here’s an example of this from Chrome DevTools:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d4c97f9-9172-478c-8aa3-a63764bd42f0/9-simplify-color-palette-css-color-mix.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d4c97f9-9172-478c-8aa3-a63764bd42f0/9-simplify-color-palette-css-color-mix.jpg" width="800" height="64" sizes="100vw" caption="Unsupported browsers, like Chrome, will use color-mix() as a value (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d4c97f9-9172-478c-8aa3-a63764bd42f0/9-simplify-color-palette-css-color-mix.jpg'>Large preview</a>)" alt="Unsupported browsers, like Chrome, will use color-mix() as a value" >}}

Because the `--background-color` property is *technically* defined, the fallback won’t trigger.

However, that’s not to say `color-mix()` can’t be used progressively, though. It can be paired with the `@supports()` function, but be mindful if you decide to do so. As exciting as it may be, with such limited support and potential for syntax and/or functionality changes, it may be best to hold off on mixing this little gem into an entire codebase.

<pre><code class="language-css">@supports (background: color-mix(in srgb, red 50%, blue)) {
  --background-color: color-mix(in srgb, red 50%, blue);
}
</code></pre>

### CurrentColor Is Not Supported

A powerful little piece of CSS is being able to use `currentColor` as a value, keeping styles relative to their element. Unfortunately, this relative variable cannot be used with `color-mix()`.

<pre><code class="language-css">button {
  background: color-mix(in srgb, currentColor 50%, white);
}
</code></pre>

The hope was to have ever greater control over relative colors, but unfortunately, using `currentColor` in this way will not work. While `color-mix()` can’t achieve relative colors to this degree, the new relative color syntax is also coming to CSS. Read about CSS relative color syntax with [Stefan Judis](https://www.stefanjudis.com/notes/new-in-css-relative-colors/).

{{% ad-panel-leaderboard %}}

## Wrapping Up

While `color-mix()` may not be as powerful as something like `color-contrast()`, there is definitely a place for it in a CSS tool belt &mdash; or kitchen cabinet. Wherever.

The use cases for contextual colors are intriguing, while the integration into design systems and themes (to potentially simplify color palettes while retaining great flexibility) is where I want the most to experiment with in the feature. However, those experiments are likely still a ways off due to the current browser support. 

Personally, combining `color-mix()` with `color-contrast()` is an area that seems particularly exciting, but without proper browser support, it will still be difficult to fully explore.

Where would you first implement `color-mix()`? 🤔 

Maybe it could be used as a mixin to roughly replicate the `lighten()` and `darken()` SCSS functions. Could there be greater potential in the realm of user-generated themes? Or even web-based graphic editors and tools? Maybe it could be used as a simple color format converter based on device capabilities.

Nevertheless, CSS is providing the web with plenty of new and exciting ingredients. It’s only a matter of time before we start mixing up some incredible recipes.

### Further Reading On Smashing Magazine
- “[Manage Accessible Design System Themes With CSS Color-Contrast()](https://www.smashingmagazine.com/2022/05/accessible-design-system-themes-css-color-contrast/),” Daniel Yuschick 
- “[A Recipe For A Good Design System](https://www.smashingmagazine.com/2022/02/recipe-good-design-system/),” Átila Fassina
- “[A Guide To Modern CSS Colors With RGB, HSL, HWB, LAB And LCH](https://www.smashingmagazine.com/2021/11/guide-modern-css-colors/),” Michelle Barker
- “[Color Tools And Resources](https://www.smashingmagazine.com/2021/07/color-tools-resources/),” Cosima Mielke

{{< signature "nl, il" >}}

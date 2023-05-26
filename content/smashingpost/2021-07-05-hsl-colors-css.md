---
title: 'Using HSL Colors In CSS'
slug: hsl-colors-css
author: ahmad-shadeed
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73607a1e-fe7f-47ea-aada-df79342d823a/hsl-colors-css.jpg
date: 2021-07-05T10:30:00.000Z
summary: >-
  In this article, Ahmad Shadeed explains what HSL is, how to use it, and shares some of the useful use-cases and examples that you can use right away in your current projects.
description: >-
  In this article, Ahmad Shadeed explains what HSL is, how to use it, and shares some of the useful use-cases and examples that you can use right away in your current projects.
categories:
  - CSS
  - Colors
  - Tools
  - Techniques
---

From my experience, most of the colors I see people using in CSS are hex and RGB. Recently, I’ve started seeing more usage of HSL colors, however, I still think that the full potential of HSL is overlooked. With the help of this article, I’d like to show you how HSL can truly help us work better with colors in CSS.

## Introduction

Usually, we use hexadecimal color codes (hex colors) which are fine, but they have a couple of issues:

- They are limiting;
- They’re hard to understand from reading them.

By “limited”, I mean that it’s not easy to alter the color without opening a color wheel and picking a color yourself. Adding on that, it’s not easy to guess what color is from looking at the hex code.

Consider the following figure:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75579961-c7de-40d7-83d1-835c5d43b1f4/1-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75579961-c7de-40d7-83d1-835c5d43b1f4/1-hsl-colors-css.jpg" width="800" height="308" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75579961-c7de-40d7-83d1-835c5d43b1f4/1-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 1" >}}

I picked a hex color for a sky blue, and a darker one. Notice that the hex colors are not related to each other. It’s hard to tell that they are both blue but with different shades.

In a real-life scenario, you might need to create a lighter or darker shade of a color to quickly test or validate something. With hex colors, this isn’t possible until you open the color picker.

Thankfully, HSL colors can help us in solving this specific problem, and it opens a lot of possibilities for us.

## What Is HSL?

HSL stands for hue, saturation, and lightness. It’s based on the RGB color wheel. Each color has an angle and a percentage value for the saturation and lightness values.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a90c72b5-56f2-4147-94c7-e4245a5e3dfb/2-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a90c72b5-56f2-4147-94c7-e4245a5e3dfb/2-hsl-colors-css.jpg" width="800" height="484" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a90c72b5-56f2-4147-94c7-e4245a5e3dfb/2-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 2" >}}

Let’s take an example of the sky blue color that we discussed previously. First, we pick the color like we usually do from a color picker, and we make sure to get the HSL value for it.

**Note**: *I’m using Sketch app, but you use whatever design tool you want.*

Consider the following figure:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8aba4b2c-fb5e-4ab1-87d1-9b5e099e597a/3-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8aba4b2c-fb5e-4ab1-87d1-9b5e099e597a/3-hsl-colors-css.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8aba4b2c-fb5e-4ab1-87d1-9b5e099e597a/3-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 3" >}}

Notice that the HSL values in there. The first one is the angle, which represents the angle of the color we have. In this case, it’s sky blue. Once we have the angle, we can start tweaking the saturation and brightness as per our needs.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b65afa0-15a9-494b-aab6-9ecf5b2adede/4-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b65afa0-15a9-494b-aab6-9ecf5b2adede/4-hsl-colors-css.jpg" width="800" height="484" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b65afa0-15a9-494b-aab6-9ecf5b2adede/4-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 4" >}}

### Saturation

**Saturation** controls how saturated the color should be. `0%` is completely unsaturated, while `100%` is fully saturated.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a318a69f-beac-4eee-950a-45809577a787/5-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a318a69f-beac-4eee-950a-45809577a787/5-hsl-colors-css.jpg" width="800" height="265" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a318a69f-beac-4eee-950a-45809577a787/5-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 5" >}}

### Lightness

As for **lightness**, it controls how light or dark the color is. `0%` is is black, and `100%` is white.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec6dcc48-6d9a-40f6-920e-4cf8db57eec8/6-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec6dcc48-6d9a-40f6-920e-4cf8db57eec8/6-hsl-colors-css.jpg" width="800" height="265" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec6dcc48-6d9a-40f6-920e-4cf8db57eec8/6-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 6" >}}

Consider the following figure:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0227ec0a-78eb-4f0a-b1d0-8b87c0711e19/7-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0227ec0a-78eb-4f0a-b1d0-8b87c0711e19/7-hsl-colors-css.jpg" width="800" height="440" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0227ec0a-78eb-4f0a-b1d0-8b87c0711e19/7-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 7" >}}

With that, we have three values that are representing color, angle, saturation, and brightness. Here is how we can use the color in CSS:

<pre><code class="language-css">.element {
    background-color: hsl(196, 73%, 62%);
}
</code></pre>

By modifying the color **angle**, we can get colors that are similar in saturation and lightness to the base one. This is very useful when working on new brand colors as it can create a consistent set of secondary brand colors.

Consider the following figure:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26543b08-b7d6-435d-ac6e-a8a92fc56f61/8-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26543b08-b7d6-435d-ac6e-a8a92fc56f61/8-hsl-colors-css.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26543b08-b7d6-435d-ac6e-a8a92fc56f61/8-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 8" >}}

Do you feel that the three colors are related to each other in terms of how the color is saturated, and how it’s dark or light it is? That has been achieved by only changing the color angle. This is what great about HSL colors. It’s more human-friendly to read and edit than any other color type.

{{% feature-panel %}}

## Use Cases For HSL Colors

#### Changing Colors On Hover

When a color in a specific component needs to appear darker on hover, HSL colors can be perfect for this. It can be helpful for components like buttons and cards.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9413f42-9ed9-4d8b-baec-3c50d73be073/9-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9413f42-9ed9-4d8b-baec-3c50d73be073/9-hsl-colors-css.jpg" width="800" height="434" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9413f42-9ed9-4d8b-baec-3c50d73be073/9-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 9" >}}

<div class="break-out">

 <pre><code class="language-css">:root {
  --primary-h: 221;
  --primary-s: 72%;
  --primary-l: 62%;
}

.button {
  background-color: hsl(var(--primary-h), var(--primary-s), var(--primary-l));
}

.button:hover {
  --primary-l: 54%;
}
</code></pre>
</div>

Notice how I combined CSS variables with HSL colors. On hover, I only need to alter the lightness value. Remember, the higher the value, the lighter. For a darker shade, we need to reduce the value.

#### A Combination Of Tinted Colors

HSL can be handy when we have a design that uses the same color but with different shades. Consider the following design:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43eafd84-5139-4830-a5de-9821753578f7/10-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43eafd84-5139-4830-a5de-9821753578f7/10-hsl-colors-css.jpg" width="800" height="370" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43eafd84-5139-4830-a5de-9821753578f7/10-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 10" >}}

The main header navigation has the primary color, while the secondary navigation has a lighter shade. With HSL, we can get the lighter shade easily by altering **the lightness** value.

{{% ad-panel-leaderboard %}}

This can be extremely useful while having a UI with multiple themes. I created two themes and switching from one to another only requires me to edit the hue degree.

First theme:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98bde5c3-ccc2-4f5c-bf6c-8f2fb25c9c73/11-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98bde5c3-ccc2-4f5c-bf6c-8f2fb25c9c73/11-hsl-colors-css.jpg" width="800" height="415" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98bde5c3-ccc2-4f5c-bf6c-8f2fb25c9c73/11-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 11" >}}

Second theme:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94168ed9-c6ae-4068-a7d9-76511ac659ae/12-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94168ed9-c6ae-4068-a7d9-76511ac659ae/12-hsl-colors-css.jpg" width="800" height="414" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94168ed9-c6ae-4068-a7d9-76511ac659ae/12-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 12" >}}

#### Color Palettes

By altering the lightness, we can create a set of shades for a color that can be used throughout the UI where possible.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64d4a97f-17a0-48c8-9688-cd26aa3ba555/13-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64d4a97f-17a0-48c8-9688-cd26aa3ba555/13-hsl-colors-css.jpg" width="800" height="255" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64d4a97f-17a0-48c8-9688-cd26aa3ba555/13-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 13" >}}

This is useful for design systems where designers provide developers with the shades for each color of the brand.

Here is an interactive demo that shows that. The input slider only changes the hue value, and the rest of the shades change based on that.

{{< codepen height="480" theme_id="light" slug_hash="gOWawpX" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Testing HSL Colors (22 Jun 2021)](https://codepen.io/smashingmag/pen/gOWawpX) by <a href="https://codepen.io/shadeed">Ahmad Shadeed
</a>.{{< /codepen >}}

#### Custom White Color

Oftentimes, we need to color a text with white color to make the text stand out. This white color is boring, and we can replace it with a very light shade of the color we have.

Consider the following example:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05b6fe9a-9894-47da-a66b-b42c59377e1b/14-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05b6fe9a-9894-47da-a66b-b42c59377e1b/14-hsl-colors-css.jpg" width="800" height="340" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05b6fe9a-9894-47da-a66b-b42c59377e1b/14-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 14" >}}

Notice how the white on the right is too much. We can replace this with a custom white that is derived from a very light shade of the color we have. In my opinion, it’s much better.

{{% ad-panel-leaderboard %}}

#### Variations Of A Button

Another useful use case for HSL colors is when we have primary and secondary options that are from the same color but with different shades. In this example, the secondary button has a very light tint of the main color. HSL colors are perfect for that.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ef5df9f-c2ed-4630-a1aa-3f2e28926b77/15-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ef5df9f-c2ed-4630-a1aa-3f2e28926b77/15-hsl-colors-css.jpg" width="800" height="269" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ef5df9f-c2ed-4630-a1aa-3f2e28926b77/15-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 15" >}}

<div class="break-out">

 <pre><code class="language-css">:root {
  --primary-h: 221;
  --primary-s: 72%;
  --primary-l: 62%;
}

.button {
  background-color: hsl(var(--primary-h), var(--primary-s), var(--primary-l));
}

.button--secondary {
    --primary-l: 90%;
    color: #222;
}

.button--ghost {
    --primary-l: 90%;
    background-color: transparent;
    border: 3px solid hsl(var(--primary-h), var(--primary-s), var(--primary-l)); 
}
</code></pre>
</div>

Tweaking the primary button variations where fast and can be extended more for broader usage. Changing the `hue` value will change all the buttons’ themes.

#### Dynamic Washed-Out Effects

In some cases, we might need a gradient to have a very light shade of the other color stop. With HSL, we can use the same color but with a different lightness value for the second one.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d29ca549-5749-4383-aa02-68b95b878f55/16-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d29ca549-5749-4383-aa02-68b95b878f55/16-hsl-colors-css.jpg" width="800" height="338" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d29ca549-5749-4383-aa02-68b95b878f55/16-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 16" >}}

<div class="break-out">

 <pre><code class="language-css">.section {
  background: linear-gradient(to left, hsl(var(--primary-h), var(--primary-s), var(--primary-l)), hsl(var(--primary-h), var(--primary-s), 95%));
}

.section-2 {
  --primary-h: 167;
}
</code></pre>
</div>

The gradient starts from the right with a solid color and then fades out to the lighter shade. This can be used for a decorative hero section, for example.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b0cd8e2-617b-4f82-8d69-84c76fc8be71/17-hsl-colors-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b0cd8e2-617b-4f82-8d69-84c76fc8be71/17-hsl-colors-css.jpg" width="800" height="305" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b0cd8e2-617b-4f82-8d69-84c76fc8be71/17-hsl-colors-css.jpg'>Large preview</a>)" alt="Figure 17" >}}

That’s all with the use cases. I hope that you learned something new and useful.

## Conclusion

HSL colors are very powerful when we use them the right way. They can save us time and effort and even help us to explore options for how to apply color to design.

{{< signature "vf, il" >}}

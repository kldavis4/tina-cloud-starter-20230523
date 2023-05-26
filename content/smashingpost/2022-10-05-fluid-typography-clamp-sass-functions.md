---
title: 'Easy Fluid Typography With clamp() Using Sass Functions'
slug: fluid-typography-clamp-sass-functions
author: brecht-de-ruyte
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ced8e27-33ad-4e3d-9e45-970f5324c8d4/fluid-typography-clamp-sass-functions.jpg
date: 2022-10-05T12:00:00.000Z
summary: >-
  We can use the `clamp()` method today because of the great browser support. In this article, Brecht De Ruyte explains how it can be a beautiful addition to your upcoming project or as an upgrade to a previous one.
description: >-
  We can use the `clamp()` method today because of the great browser support. In this article, Brecht De Ruyte explains how it can be a beautiful addition to your upcoming project or as an upgrade to a previous one.
categories:
  - CSS
  - Sass
  - Typography
  - Techniques
---

Fluid typography is getting a lot more popular, especially since the [`clamp()` math function](https://developer.mozilla.org/en-US/docs/Web/CSS/clamp) is available in every evergreen browser. But if we’re honest, it’s still a lot of mathematics to achieve this. You can use tools such as [`utopia.fyi`](https://utopia.fyi), which are fantastic. But in large projects, it can get messy pretty fast. I’m a big fan of readable and maintainable code and always want to see what my code is doing at a glance. I’m sure there are many more of you like that, so instead of adding a full `clamp()` function inside of our code, maybe we can make this a bit more readable with Sass.

## Why Should We Use Fluid Typography?

Usually, when designing for different screen sizes, we use media queries to determine the font size of our typographic elements. Although this usually gives enough control for the more conventional devices, it doesn’t cover all of the screen sizes.

{{% pull-quote %}}
By using fluid typography, we can make the typography scale more logically between all sorts of different devices.
{{% /pull-quote %}}

This is now possible in all evergreen browsers because of the `clamp()` function in CSS. It is perfect for the job and reduces our media query writing, thus saving us a bit of file size along the way. 

## How Exactly Does This `clamp()` Function Work For Typography?

In short, the clamp function looks like this:

<pre><code class="language-css">clamp([min-bound], [value-preferred], [max-bound]);
</code></pre>

This takes into account three numbers: **a minimum bound**, **preferred value**, and **a maximum bound**. By using `rem` values, we can increase the accessibility a bit, but it’s still not 100% foolproof, especially for external browser tools.

If you want a more in-depth explanation of the math, I suggest you read this post from Adrian Bece “[Modern Fluid Typography Using CSS Clamp ](https://www.smashingmagazine.com/2022/01/modern-fluid-typography-css-clamp/)”.

However, there is a bit of a problem. When you read those `clamp` functions inside your CSS, it’s still hard to see exactly what is happening. Just imagine a file full of font sizes that look like this:

<pre><code class="language-css">clamp(1.44rem, 3.44vw + 0.75rem, 2.81rem)
</code></pre>

But with a little help from the `sass` function, we can make these font sizes much more readable.

## What Do We Want To Achieve With This Simple Sass Function?

In short, we want to do something like this: We have a **minimum font size**, from the moment our **breakpoint is larger than `400px`**, we want it to **scale it to our biggest font size** until the **maximum breakpoint is reached.**

The minimum and maximum font sizes are covered quite easily. If we want a minimum font size of `16px` (or `1rem`) and a maximum font size of `32px` (or `2rem`), we already have the two parts of our clamp function:

<pre><code class="language-css">clamp(1rem, [?], 2rem)
</code></pre>

{{% feature-panel %}}

## Creating A Basic Automated Fluid Function

This is where things get tricky, and I suggest you follow the article by Adrian Bece, who gives a great in-depth explanation of the math behind this.

In short, the equation is the following:

**(maximum font-size  - minimum font-size) / (maximum breakpoint - minimum breakpoint)**

Let’s get ready to do some mathematics for this to happen in Sass, so let’s create our **`fluid-typography.scss`** function file and start by adding `sass:math` and the function with the values we’ll need:

<div class="break-out">

<pre><code class="language-css">@use "sass:math";

@function fluid($min-size, $max-size, $min-breakpoint, $max-breakpoint, $unit: vw) {
 
}
</code></pre>
</div>

Now, let’s add the calculation for the slope inside of our function with some `sass:math`:

<div class="break-out">

<pre><code class="language-css">@function fluid($min-size, $max-size, $min-breakpoint, $max-breakpoint, $unit: vw) {
 $slope: math.div($max-size - $min-size, $max-breakpoint - $min-breakpoint);
}
</code></pre>
</div>

To get a value we can work with, we’ll need to multiply our slope by `100`:

<pre><code class="language-css">$slope-to-unit: $slope &#42; 100;
</code></pre>

All that is left is for us to find our intercept to build the equation. We can do this with the following function:

<pre><code class="language-css">$intercept: $min-size - $slope &#42; $min-breakpoint;
</code></pre>

And finally, return our function:

<div class="break-out">

<pre><code class="language-css">@return clamp(#{$min-size}, #{$slope-to-unit}#{$unit} + #{$intercept}, #{$max-size});
</code></pre>
</div>

If we call the created `sass` function in our scss, we should now get fluid typography:

<pre><code class="language-css">h1 {
   font-size: #{fluid(1rem, 2rem, 25rem, 62.5rem)}
}
</code></pre>

### A Note About Units

In most cases, we will be using a viewport width when it comes to fluid typography, so this makes a good default. However, there are some cases, especially when using the `clamp()` function for vertical spacing, where you want to use a viewport height instead of width. When this is desired, we can change the outputted unit and use a minimum and maximum breakpoint for the height:

<pre><code class="language-css">h1 {
   font-size: #{fluid(1rem, 2rem, 25rem, 62.5rem, vh)}
}
</code></pre>

{{% ad-panel-leaderboard %}}

## Updating The Function To Make The Calculations Feel More Natural

We got what we need, but let’s be honest, most of the time, we are implementing a design, and it doesn’t feel natural to pass our viewports as `rems`. So, let’s update this function to use pixels as a viewport measurement. While we’re at it, let’s update the font sizes so we can use pixel values for everything. We will still convert them to `rem` units since those are better for accessibility.

First, we’ll need an extra function to calculate our `rem` values based on a pixel input. 

**Note**: *This won’t work if you change your base `rem` value.*

<pre><code class="language-css">@function px-to-rem($px) {
    $rems: math.div($px, 16px) &#42; 1rem;
    @return $rems;
}
</code></pre>

Now we can update our fluid function to output `rem` values even though it gets pixels as input. This is the updated version:

<div class="break-out">

<pre><code class="language-css">@function fluid($min-size, $max-size, $min-breakpoint, $max-breakpoint, $unit: vw) {
    $slope: math.div($max-size - $min-size, $max-breakpoint - $min-breakpoint);
    $slope-to-unit: $slope &#42; 100;
    $intercept-rem: px-to-rem($min-size - $slope &#42; $min-breakpoint);
    $min-size-rem: px-to-rem($min-size);
    $max-size-rem: px-to-rem($max-size);
    @return clamp(#{$min-size-rem}, #{$slope-to-unit}#{$unit} + #{$intercept-rem}, #{$max-size-rem});
}
</code></pre>
</div>

Now we can use the following input:

<pre><code class="language-css">font-size: #{fluid(16px, 32px, 320px, 960px)}
</code></pre>

This will result in the following:

<pre><code class="language-css">font-size: clamp(1rem, 2.5vw + 0.5rem, 2rem);
</code></pre>

At first glance, this seems perfect, but mostly that’s because I’ve been using very simple values. For example, when clamping to a maximum value of `31px` instead of `32px`, our `rem` values won’t be so rounded, and our output will get a bit messy.

***Input:***

<pre><code class="language-css">font-size: #{fluid(16px, 31px, 320px, 960px)}
</code></pre>

***Output:***

<pre><code class="language-css">font-size: clamp(1rem, 2.34375vw + 0.53125rem, 1.9375rem);
</code></pre>

If you’re like me and find this a bit messy as well, we could round our values a little bit to increase readability and save some bytes in our final CSS file. Also, it might get a bit tedious if we always have to add the viewport, so why not add some defaults in our function?

{{% ad-panel-leaderboard %}}

## Rounding Our Values And Adding Some Defaults

Let’s start by adding a rounding function to our Sass file. This will take any input and round it to a specific amount of decimals:

<pre><code class="language-css">@function round($number, $decimals: 0) {
    $n: 1;
    @if $decimals &gt; 0 {
        @for $i from 1 through $decimals {
            $n: $n &#42; 10;
        }
    }
    @return math.div(math.round($number &#42; $n), $n);
}
</code></pre>

Now we can update our output values with rounded numbers. Update the function accordingly. I would suggest setting at least two decimals for the output values for the most consistent results:

<div class="break-out">

<pre><code class="language-css">@function fluid($min-size, $max-size, $min-breakpoint, $max-breakpoint, $unit: vw) {
    $slope: math.div($max-size - $min-size, $max-breakpoint - $min-breakpoint);
    $slope-to-unit: round($slope &#42; 100, 2);
    $intercept-rem: round(px-to-rem($min-size - $slope &#42; $min-breakpoint), 2);
    $min-size-rem: round(px-to-rem($min-size), 2);
    $max-size-rem: round(px-to-rem($max-size), 2);
    @return clamp(#{$min-size-rem}, #{$slope-to-unit}#{$unit} + #{$intercept-rem}, #{$max-size-rem});
}</code></pre>
</div>

Now the same example as before will give us a much cleaner result.

***Input:***

<pre><code class="language-css">font-size: #{fluid(16px, 31px, 320px, 960px)};
</code></pre>

***Output:***

<pre><code class="language-css">font-size: clamp(1rem, 2.34vw + 0.53rem, 1.94rem);
</code></pre>

### Adding A Default Breakpoint

If you don’t feel like repeating yourself, you can always set a default breakpoint to your function. Try updating the function like this:

<div class="break-out">

<pre><code class="language-css">$default-min-bp: 320px;
$default-max-bp: 960px;

@function fluid($min-size, $max-size, $min-breakpoint: $default-min-bp, $max-breakpoint: $default-max-bp, $unit: vw) {
	// ...
}
</code></pre>
</div>

Now, we don’t need to repeat these viewports all the time. We can still add a custom breakpoint but a simple input such as:

<pre><code class="language-css">font-size: #{fluid(16px, 31px)};
</code></pre>

Will still result in:

<pre><code class="language-css">font-size: clamp(1rem, 2.34vw + 0.53rem, 1.94rem);
</code></pre>

Here is the full function:

<div class="break-out">

<pre><code class="language-css">@use 'sass:math';

$default-min-bp: 320px;
$default-max-bp: 960px;

@function round($number, $decimals: 0) {
    $n: 1;
    @if $decimals &gt; 0 {
        @for $i from 1 through $decimals {
            $n: $n &#42; 10;
        }
    }
    @return math.div(math.round($number &#42; $n), $n);
}

@function px-to-rem($px) {
    $rems: math.div($px, 16px) &#42; 1rem;
    @return $rems;
}

@function fluid($min-size, $max-size, $min-breakpoint: $default-min-bp, $max-breakpoint: $default-max-bp, $unit: vw) {
    $slope: math.div($max-size - $min-size, $max-breakpoint - $min-breakpoint);
    $slope-to-unit: round($slope &#42; 100, 2);
    $intercept-rem: round(px-to-rem($min-size - $slope &#42; $min-breakpoint), 2);
    $min-size-rem: round(px-to-rem($min-size), 2);
    $max-size-rem: round(px-to-rem($max-size), 2);
    @return clamp(#{$min-size-rem}, #{$slope-to-unit}#{$unit} + #{$intercept-rem}, #{$max-size-rem});
}
</code></pre>
</div>

## A Final Note: Be A Happy Clamper For All users Out There

If you followed this little tutorial and were amazed by it, you might want to add this `clamp()` method for everything, but there is an important side note when it comes to accessibility.

**Note**: *When you use `vw` units or limit how large text can get with `clamp()`, there is a chance a user may be unable to scale the text to 200% of its original size.*

If that happens, it is WCAG failure. As Adrian Bece mentioned, it’s not 100% foolproof. [Adrian Roselli has written some examples on this](https://adrianroselli.com/2019/12/responsive-type-and-zoom.html), which you might find interesting.

We can use this method today because of the great browser support. By being smart on the usage, I’m sure it can be a beautiful addition to your upcoming project or as an upgrade to a previous one.

{{< signature "vf, yk, il" >}}

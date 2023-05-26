---
title: 'FabUnit: A Smart Way To Control And Synchronize Typo And Space'
slug: fabunit-smart-way-control-synchronize-typo-space
author: fabienne-bielmann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b3ae408-a861-423b-a18c-bbe6151bbe83/fabunit-smart-way-control-synchronize-typo-space.jpg
date: 2022-12-01T09:00:00.000Z
summary: >-
  Today, we’ll take a look at the Sass function that does all the work for you &mdash; with no media queries, no breakpoints, and no design jumps. In this article, Fabienne Bielmann explains what FabUnit stands for and why she decided to create her very own responsive magic formula.
description: >-
  Today, we’ll take a look at the Sass function that does all the work for you &mdash; with no media queries, no breakpoints, and no design jumps. In this article, Fabienne Bielmann explains what FabUnit stands for and why she decided to create her very own responsive magic formula.
categories:
  - CSS
  - Tools
  - Techniques
  - Responsive Design
---

What if we were able to implement the sizes of designer’s contribution without hassle? What if we could set custom anchor points to generate a perfectly responsive value, giving us more options as the fluid size approach? What if we had a magic formula that controlled and synchronized the whole project?

It is often the case that I receive two templates from the designer: One for mobile and one for desktop. Lately, I have been asking myself how I could automate the process and optimize the result. How do I implement the specified sizes most effectively? How do I ensure a comfortable tablet view? How can I optimize the output for large screens? How can I react to extreme aspect ratios?

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86bb41d6-5327-4217-b786-67339636c5e7/16-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86bb41d6-5327-4217-b786-67339636c5e7/16-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="447" sizes="100vw" caption="Desktop and mobile template from the designer. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86bb41d6-5327-4217-b786-67339636c5e7/16-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Desktop and mobile template from the designer" >}}

I would like to be able to read the two values of the different sizes (font, spaces, etc.) in pixel and enter them as arguments into a function that does all the work for me. I want to create my own responsive magic formula, my FabUnit.

When I started working on this topic in the spring and launched the FabUnit, I came across this interesting article by [Adrian](https://www.smashingmagazine.com/2022/01/modern-fluid-typography-css-clamp/). In the meantime, [Ruslan](https://www.smashingmagazine.com/2022/08/fluid-sizing-multiple-media-queries/) and [Brecht](https://www.smashingmagazine.com/2022/10/fluid-typography-clamp-sass-functions/) have also researched in this direction and presented interesting thoughts.

## How Can I Implement The Design Templates Most Effectively?

I am tired of writing media queries for every value, and I want to avoid design jumps. The maintenance and the result are not satisfying. So what is the best way to implement the designer’s contribution? 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b15c1531-d785-4774-bfa3-b1413d8de60c/11-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b15c1531-d785-4774-bfa3-b1413d8de60c/11-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="295" sizes="100vw" caption="Media queries with breakpoints. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b15c1531-d785-4774-bfa3-b1413d8de60c/11-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Media queries with breakpoints" >}}

What about fluid sizes? There are handy calculators like [Utopia](https://utopia.fyi/) or [Min-Max-Calculator](https://min-max-calculator.9elements.com/).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c05259d8-7e0e-4a94-93fe-bfb983fd2864/5-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c05259d8-7e0e-4a94-93fe-bfb983fd2864/5-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="295" sizes="100vw" caption="Fluid size with minimum and maximum. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c05259d8-7e0e-4a94-93fe-bfb983fd2864/5-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Fluid size with minimum and maximum" >}}

But for my projects, I usually need more setting options. The tablet view often turns out too small, and I can neither react to larger viewports nor to the aspect ratio. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71c08ab8-5539-4799-845c-723a54f008a9/7-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71c08ab8-5539-4799-845c-723a54f008a9/7-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="583" sizes="100vw" caption="Disadvantages of the fluid-size approach with fixed minimum and maximum: font size and spacings are too small for tablet views and no responsiveness for larger screens or extreme aspect ratios. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71c08ab8-5539-4799-845c-723a54f008a9/7-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Visualization of the disadvantages of the fluid size approach with fixed minimum and maximum. A tick in a box for mobile and desktop, and a red cross for a tablet, larger screens, and extreme aspect ratios" >}}

And it would be nice to have a proportional synchronization across the whole project. I can define global variables with the calculated values, but I also want to be able to generate an interpolated value locally in the components without any effort. I would like to draw my own responsive line. So I need a tool that spits out the perfect value based on several anchor points (screen definitions) and automates the processes for most of my projects. My tool must be fast and easy to use, and the code must be readable and maintainable. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56ae9070-074a-47c7-b038-0b15e0cb8ecf/9-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56ae9070-074a-47c7-b038-0b15e0cb8ecf/9-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="319" sizes="100vw" caption="Custom responsive line based on anchor points. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56ae9070-074a-47c7-b038-0b15e0cb8ecf/9-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Custom responsive line based on anchor points" >}}

## What Constants From The Design Specifications Should Our Calculations Be Based On?

Let’s take a closer look at our previous example:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d08dd642-370c-4b1e-aea1-17fe0a00c57b/15-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d08dd642-370c-4b1e-aea1-17fe0a00c57b/15-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="461" sizes="100vw" caption="Input from a designer with size and screen specifications. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d08dd642-370c-4b1e-aea1-17fe0a00c57b/15-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Input from a designer with size and screen specifications" >}}

The body font size should be `16px` on mobile and `22px` on desktop (we will deal with the complete style guide later on). The mobile sizes should start at `375px` and continuously adjust to `1024px`. Up to `1440px`, the sizes are to remain statically at the optimum. After that, the values should scale linearly up to `2000px`, after which the max-wrapper takes effect.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6c5408b-ba9c-41f7-8d4b-a3996f47c29f/10-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6c5408b-ba9c-41f7-8d4b-a3996f47c29f/10-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="522" sizes="100vw" caption="Screen behavior for the design on mobile (min), desktop (opt) and larger screens (with wrapper). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6c5408b-ba9c-41f7-8d4b-a3996f47c29f/10-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Responsive design for the design on mobile (min), desktop (opt) and larger screens (with wrapper)" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc16d045-6132-43ee-8dd4-b31688d2b81d/2-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc16d045-6132-43ee-8dd4-b31688d2b81d/2-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="445" sizes="100vw" caption="Screen behavior of the design templates as a responsive line based on anchor points. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc16d045-6132-43ee-8dd4-b31688d2b81d/2-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Screen behavior of the design templates as a responsive line based on anchor points" >}}

This gives us the following constants that apply to the whole project:

<pre><code class="language-css">Xf	375px		global		screen-min		
Xa	1024px		global		screen-opt-start
Xb	1440px		global		screen-opt-end
Xu	2000px		global		screen-max
</code></pre>

The body font size should be at least `16px`, ideally `22px`. The maximum font size at `2000px` should be calculated automatically: 

<pre><code class="language-css">Yf	16px		local		size-min		
Ya	22px
Yb	22px		local		size-opt
Yu	auto
</code></pre>

So, at the end of the day, my function should be able to take two arguments &mdash; in this case, `16` and `22`.

<pre><code class="language-css">fab-unit(16, 22);
</code></pre>

## The Calculation

If you are not interested in the mathematical derivation of the formula, feel free to jump directly to the section “[How To Use The FabUnit?](#how-to-use-the-fabunit)”.

So, let’s get started!

{{% feature-panel %}}

### Define Main Clamps

First, we need to figure out which main clamps we want to set.

<pre><code class="language-css">clamp1: clamp(Yf, slope1, Ya)
clamp2: clamp(Yb, slope2, Yu)
</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/771ce050-158a-4868-affc-356e838f3cdb/14-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/771ce050-158a-4868-affc-356e838f3cdb/14-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="395" sizes="100vw" caption="Definition of the main clamps based on the specified anchor points. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/771ce050-158a-4868-affc-356e838f3cdb/14-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Definition of the main clamps based on the specified anchor points" >}}

### Combine And Nest The Clamps

Now we have to combine the two clamps. This might get a little tricky. We have to consider that the two lines, `slope1` and `slope2`, can overwrite each other, depending on how steep they are. Since we know that `slope2` should be 45 degrees or 100% (m = 1), we can query whether `slope1` is above 1. This way, we can set a different clamp depending on how the lines intersect.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0a0a0b5-bff6-45c9-b00f-a44dfcfff7f7/3-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0a0a0b5-bff6-45c9-b00f-a44dfcfff7f7/3-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="445" sizes="100vw" caption="Depending on the difference between the two sizes, the slope lines can intersect &mdash; the two clamps can come into conflict. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0a0a0b5-bff6-45c9-b00f-a44dfcfff7f7/3-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Visualization of two intersected lines" >}}

If `slope1` is steeper than `slope2`, we combine the clamps like this:

<pre><code class="language-css">clamp(Yf, slope1, clamp(Yb, slope2, Yu))
</code></pre>

If `slope1` is flatter than `slope2`, we do this calculation:

<pre><code class="language-css">clamp(clamp(Yf, slope1, Ya), slope2, Yu)
</code></pre>

Combined:

<pre><code class="language-css">steep-slope
  ? clamp(Yf, slope1, clamp(Yb, slope2, Yu))
  : clamp(clamp(Yf, slope1, Ya), slope2, Yu)
</code></pre>

### Set The Maximum Wrapper Optionally

What if we don’t have a maximum wrapper that freezes the design above a certain width?

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddc076a2-74e2-46a6-8c2f-c8847d187776/12-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddc076a2-74e2-46a6-8c2f-c8847d187776/12-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="395" sizes="100vw" caption="Adjustment of the operations if no maximum value is to be set. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddc076a2-74e2-46a6-8c2f-c8847d187776/12-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Adjustment of the operations if no maximum value is to be set" >}}

First, we need to figure out which main clamps we want to set.

<pre><code class="language-css">clamp1: clamp(Yf, slope1, Ya)
max: max(Yb, slope2)
</code></pre>

If `slope1` is steeper than `slope2`:

<pre><code class="language-css">clamp(Yf, slope1, max(Yb, slope2))
</code></pre>

If `slope1` is flatter than `slope2`:

<pre><code class="language-css">max(clamp(Yf, slope1, Ya), slope2)
</code></pre>

The calculation without wrapper &mdash; elastic upwards:

<pre><code class="language-css">steep-slope
  ? clamp(Yf, slope1, max(Yb, slope2))
  : max(clamp(Yf, slope1, Ya), slope2)
</code></pre>

Combined, with optional max wrapper (if screen-max `Xu` is set):

<pre><code class="language-css">Xu
  ? steep-slope
    ? clamp(Yf, slope1, clamp(Yb, slope2, Yu))
    : max(clamp(Yf, slope1, Ya), Yu)
  : steep-slope
    ? clamp(Yf, slope1, max(Yb, slope2))
    : max(clamp(Yf, slope1, Ya), slope2)
</code></pre>

Thus we have built the basic structure of the formula. Now we dive a little deeper. 

### Calculate The Missing Values

Let’s see which values we get in as an argument and which we have to calculate now:

<code><strong>steep-slope</strong><br /> 
&nbsp;&nbsp;? clamp(Yf, <strong>slope1</strong>, clamp(Yb, <strong>slope2</strong>, <strong>Yu</strong>))<br />
&nbsp;&nbsp;: max(clamp(Yf, slope1, Ya), Yu)<br />
<br />
<strong>steep-slope</strong><br />
Ya = Yb = 22px<br />
Yf = 16px<br />
slope1 = <strong>Mfa</strong><br />
slope2 = <strong>Mbu</strong><br />
<strong>Yu</strong>
</code>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a667ba8-8361-48d8-8bbc-05277ad0eda5/4-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a667ba8-8361-48d8-8bbc-05277ad0eda5/4-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="343" sizes="100vw" caption="To complete the responsive line, two slopes and one anchor point must be calculated automatically. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a667ba8-8361-48d8-8bbc-05277ad0eda5/4-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="To complete the responsive line, two slopes and one anchor point must be calculated automatically" >}}

- `steep-slope`  
Check whether the slope `Yf → Ya` is above the slope `Yb → Yu` (m = 1) :

<pre><code class="language-css">((Ya - Yf) / (Xa - Xf)) &#42; 100 > 1
</code></pre>

- `Mfa`  
Linear interpolation, including the calculation of the slope `Yf → Ya`:

<pre><code class="language-css">Yf + (Ya - Yf) &#42; (100vw - Xf) / (Xa - Xf)
</code></pre>
    
- `Mbu`  
Linear interpolation between `Yb` and `Yu` (slope m = 1):

<pre><code class="language-css">100vw / Xb &#42; Yb
</code></pre>

- `Yu`  
Calculating the position of `Yu`:

<pre><code class="language-css">(Xu / Xb) &#42; Yb
</code></pre>

### Put All Together

<div class="break-out">

<pre><code class="language-css">Xu
  ? ((Ya - Yf) / (Xa - Xf)) &#42; 100 &gt; 1
    ? clamp(Yf, Yf + (Ya - Yf) &#42; (100vw - Xf) / (Xa - Xf), clamp(Yb, 100vw / Xb &#42; Yb, (Xu / Xb) &#42; Yb))
    : max(clamp(Yf, Yf + (Ya - Yf) &#42; (100vw - Xf) / (Xa - Xf), Ya), (Xu / Xb) &#42; Yb)
  : ((Ya - Yf) / (Xa - Xf)) &#42; 100 &gt; 1
    ? clamp(Yf, Yf + (Ya - Yf) &#42; (100vw - Xf) / (Xa - Xf), max(Yb, 100vw / Xb &#42; Yb))
    : max(clamp(Yf, Yf + (Ya - Yf) &#42; (100vw - Xf) / (Xa - Xf), Ya), 100vw / Xb &#42; Yb)
</code></pre>
</div>

We’d better store some calculations in variables:

<pre><code class="language-css">steep-slope = ((Ya - Yf) / (Xa - Xf)) &#42; 100 &gt; 1
slope1 = Yf + (Ya - Yf) &#42; (100vw - Xf) / (Xa - Xf)
slope2 = 100vw / Xb &#42; Yb
Yu = (Xu / Xb) &#42; Yb

Xu
  ? steep-slope
    ? clamp(Yf, slope1, clamp(Yb, slope2, Yu))
    : max(clamp(Yf, slope1, Ya), Yu)
  : steep-slope
    ? clamp(Yf, slope1, max(Yb, slope2))
    : max(clamp(Yf, slope1, Ya), slope2)
</code></pre>

## Include Aspect Ratio

Because we now see how the cat jumps, we treat ourselves to another cookie. In the case of an extremely wide format, e.g. mobile device landscape, we want to scale down the sizes again. It’s more pleasant and readable this way.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1c15e73-f551-436b-9d1c-dea7614624ae/1-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1c15e73-f551-436b-9d1c-dea7614624ae/1-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="433" sizes="100vw" caption="Extreme aspect ratios can have a negative effect on the rendered design. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1c15e73-f551-436b-9d1c-dea7614624ae/1-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Visualization of the negative effect of the extreme aspect ratios on the rendered design pictured with a cross in a red box" >}}

So what if we could include the aspect ratio in our calculations? In this example, we want to shrink the sizes when the screen is wider than the aspect ratio of 16:9.

<pre><code class="language-css">aspect-ratio = 16 / 9
screen-factor = min(100vw, 100vh &#42; aspect-ratio)
</code></pre>

In both slope interpolations, we simply replace `100vw` with the new screen factor.

<pre><code class="language-css">slope1 = Yf + (Ya - Yf) &#42; (screen-factor - Xf) / (Xa - Xf)
slope2 = screen-factor / Xb &#42; Yb
</code></pre>

So, finally, that’s it. Let’s look at the whole magic formula now. 

{{% ad-panel-leaderboard %}}

## Formula

<pre><code class="language-css">screen-factor = min(100vw, 100vh &#42; aspect-ratio)
steep-slope = ((Ya - Yf) / (Xa - Xf)) &#42; 100 &gt; 1
slope1 = Yf + (Ya - Yf) &#42; (screen-factor - Xf) / (Xa - Xf)
slope2 = screen-factor / Xb &#42; Yb
Yu = (Xu / Xb) &#42; Yb

Xu
  ? steep-slope
    ? clamp(Yf, slope1, clamp(Yb, slope2, Yu))
    : max(clamp(Yf, slope1, Ya), Yu)
  : steep-slope
    ? clamp(Yf, slope1, max(Yb, slope2))
    : max(clamp(Yf, slope1, Ya), slope2)
</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ff710f6-e9ec-41e4-84cf-be71806b1980/6-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ff710f6-e9ec-41e4-84cf-be71806b1980/6-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="523" sizes="100vw" caption="A handy <a href='https://codepen.io/Faboolea/live/yLvGMqZ/ed43660a7931e55b2fb2ec35d18e7f8c'>FabUnit Visualizer</a> that accepts user-defined values, displays the automatically calculated maximum size and draws the corresponding responsive line. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ff710f6-e9ec-41e4-84cf-be71806b1980/6-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="FabUnit Visualizer that accepts user-defined values, displays the automatically calculated maximum size and draws the corresponding responsive line" >}}

## Function

Now we can integrate the formula into our setup. In this article, we’ll look at how to implement it in Sass. The two helper functions ensure that we output the rem values correctly (I will not go into it in detail). Then we set the anchor points and the aspect ratio as constants (respectively, Sass variables). Finally, we replace the coordinate points of our formula with variable names, and the FabUnit is ready for use.

*&#95;fab-unit.scss*

<div class="break-out">

<pre><code class="language-css">@use "sass:math";


/&#42; Helper functions &#42;/

$rem-base: 10px;

@function strip-units($number) {
  @if (math.is-unitless($number)) {
      @return $number;
    } @else {
      @return math.div($number, $number &#42; 0 + 1);
  }
}

@function rem($size){
  @if (math.compatible($size, 1rem) and not math.is-unitless($size)) {
    @return $size;
  } @else {
    @return math.div(strip-units($size), strip-units($rem-base)) &#42; 1rem;
  }
}


/&#42; Default values fab-unit 🪄 &#42;/

$screen-min: 375;
$screen-opt-start: 1024;
$screen-opt-end: 1440;
$screen-max: 2000;  // $screen-opt-end | int &gt; $screen-opt-end | false
$aspect-ratio: math.div(16, 9);  // smaller values for larger aspect ratios


/&#42; Magic function fab-unit 🪄 &#42;/

@function fab-unit(
    $size-min, 
    $size-opt, 
    $screen-min: $screen-min, 
    $screen-opt-start: $screen-opt-start, 
    $screen-opt-end: $screen-opt-end, 
    $screen-max: $screen-max,
    $aspect-ratio: $aspect-ratio
  ) {
  $screen-factor: min(100vw, 100vh * $aspect-ratio);
  $steep-slope: math.div(($size-opt - $size-min), ($screen-opt-start - $screen-min)) * 100 &gt; 1;
  $slope1: calc(rem($size-min) + ($size-opt - $size-min) * ($screen-factor - rem($screen-min)) / ($screen-opt-start - $screen-min));
  $slope2: calc($screen-factor / $screen-opt-end * $size-opt);
  @if $screen-max {
    $size-max: math.div(rem($screen-max), $screen-opt-end) * $size-opt;
    @if $steep-slope {
      @return clamp(rem($size-min), $slope1, clamp(rem($size-opt), $slope2, $size-max));
    } @else {
      @return clamp(clamp(rem($size-min), $slope1, rem($size-opt)), $slope2, $size-max);
    }
  } @else {
    @if $steep-slope {
      @return clamp(rem($size-min), $slope1, max(rem($size-opt), $slope2));
    } @else {
      @return max(clamp(rem($size-min), $slope1, rem($size-opt)), $slope2);
    }
  }
}
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## How To Use The FabUnit?

The work is done, now it’s simple. The style guide from our example can be implemented in no time:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb7c0475-2d3f-4855-b4ee-43d8167c6406/13-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb7c0475-2d3f-4855-b4ee-43d8167c6406/13-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="449" sizes="100vw" caption="Style guide from a designer with all size specifications for mobile and desktop. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb7c0475-2d3f-4855-b4ee-43d8167c6406/13-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Style guide from a designer with all size specifications for mobile and desktop" >}}

We read the related values from the style guide and pass them to the FabUnit as arguments: `fab-unit(16, 22)`.

*style.scss*

<div class="break-out">

<pre><code class="language-css">@import "fab-unit";


/&#42; overwrite default values 🪄 &#42;/
$screen-max: 1800;


/&#42; Style guide variables fab-unit 🪄 &#42;/

$fab-font-size-body: fab-unit(16, 22);
$fab-font-size-body-small: fab-unit(14, 16);

$fab-font-size-h1: fab-unit(60, 160);
$fab-font-size-h2: fab-unit(42, 110);
$fab-font-size-h3: fab-unit(28, 60);

$fab-space-s: fab-unit(20, 30);
$fab-space-m: fab-unit(40, 80);
$fab-space-l: fab-unit(60, 120);
$fab-space-xl: fab-unit(80, 180);


/&#42; fab-unit in action 🪄 &#42;/

html {
  font-size: 100% &#42; math.div(strip-units($rem-base), 16);
}

body {
  font-size: $fab-font-size-body;
}

.wrapper {
  max-width: rem($screen-max);
  margin-inline: auto;
  padding: $fab-space-m;
}

h1 {
  font-size: $fab-font-size-h1;
  border-block-end: fab-unit(2, 10) solid plum;
}

…

p {
  margin-block: $fab-space-s;
}

…
</code></pre>
</div>

<div class="break-out">

<pre><code class="language-css">/&#42; other use cases for calling fab-unit 🪄 &#42;/

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(fab-unit(200, 500), 1fr));
  gap: $fab-space-m;
}

.thing {
  flex: 0 0 fab-unit(20, 30);
  height: fab-unit(20, 36, 660, 800, 1600, 1800);  /&#42; min, opt, … custom anchor points &#42;/
}
</code></pre>
</div>

We are now able to draw the responsive line by calling `fab-unit()` and specifying just two sizes, the minimum and the optimum. We can control the font sizes, paddings, margins and gaps, heights and widths, and even &mdash; if we want to &mdash; define grid columns and flex layouts with it. We are also able to move the predefined anchor points locally. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5078694b-caeb-4198-b2ef-ef5e4cece5cc/8-fabunit-smart-way-control-synchronise-typo-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5078694b-caeb-4198-b2ef-ef5e4cece5cc/8-fabunit-smart-way-control-synchronise-typo-space.png" width="800" height="593" sizes="100vw" caption="Optimal adaptation to different viewports sizes and aspect ratios with the FabUnit. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5078694b-caeb-4198-b2ef-ef5e4cece5cc/8-fabunit-smart-way-control-synchronise-typo-space.png'>Large preview</a>)" alt="Optimal adaptation to different viewports sizes and aspect ratios with the FabUnit" >}}

Let’s have a look at the compiled output:

<div class="break-out">

<pre><code class="language-css">…
font-size: clamp(clamp(1.3rem, 1.3rem + 2 &#42; (min(100vw, 177.7777777778vh) - 37.5rem) / 649, 1.5rem), min(100vw, 177.7777777778vh) / 1440 &#42; 15, 2.0833333333rem);
…
</code></pre>
</div>

And the computed output:

<pre><code class="language-css">font-size: 17.3542px
</code></pre>

### Accessibility Concerns

To ensure good accessibility, I recommend testing in each case whether all sizes are sufficiently zoomable. Arguments with a large difference might not behave as desired. For more information on this topic, you can check the article “[Responsive Type and Zoom](https://adrianroselli.com/2019/12/responsive-type-and-zoom.html)” by Adrian Roselli. 

## Conclusion

Now we have created a function that does all the work for us. It takes a minimum and an optimum value and spits out a calculation to our CSS property, considering the screen width, aspect ratio, and the specified anchor points &mdash; a single formula that drives the entire project. No media queries, no breakpoints, no design jumps.

The FabUnit presented here is based on my own experience and is optimized for most of my projects. I save a lot of time and am satisfied with the result. It may be that you and your team have another approach and therefore have other requirements for a FabUnit. It would be nice if you were now able to create your own FabUnit according to your needs. 

I would be happy if my approach inspired you with new ideas. I would be honored if you directly use the [npm package ](https://www.npmjs.com/package/fab-unit) of the FabUnit from this article for your projects.

Thank you! 🙏🏻

### FAB-UNIT LINKS

- [FabUnit CodeSandbox Example](https://codesandbox.io/s/fabunit-ow8wjr)
- [FabUnit Github](https://github.com/Faboolea/fab-unit)
- [FabUnit Npm Package](https://www.npmjs.com/package/fab-unit)
- [FabUnit Visualiser](https://codepen.io/Faboolea/live/yLvGMqZ/ed43660a7931e55b2fb2ec35d18e7f8c)

*Merci Eli, Roman, Patrik, Fidi.*

{{< signature "yk, il" >}}

---
title: 'There Is No Such Thing As A CSS Absolute Unit'
slug: css-absolute-units
author: elad-shechter
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ee35630-bbe1-486c-8877-dacdd4b12869/css-absolute-units.jpg
date: 2021-07-29T10:30:00.000Z
summary: >-
  What are absolute units? What are the differences between relative and absolute units, and how do we create accurate sizes on the web? In this article, Elad Shechter explains why CSS absolute units aren’t so absolute.
description: >-
  What are absolute units? What are the differences between relative and absolute units, and how do we create accurate sizes on the web? In this article, Elad Shechter explains why CSS absolute units aren’t so absolute.
categories:
  - CSS
  - Coding
  - Browsers
  - Responsive Design
---

When we start learning CSS, we find that CSS units of measurement are categorized as relative or absolute. Absolute units are rooted in physical units, such as pixels, centimeters, and inches. But over the years, all absolute units in CSS have lost their connection to the physical world and have become different kinds of relative units, at least from the perspective of the web.

It’s important to note that there are still significant **differences between relative and absolute units**. CSS relative units are sized according to other style definitions defined by parent elements or are affected by the size of a parent container. As for absolute units, we will dive in and see how they are affected by other things, such as the screen and the device’s operating system.

Relative units include units such as `%`, `em`, `rem`, viewport units (`vw` and `vh`), and more. The most common absolute unit is the pixel (`px`). Besides that, we have the centimeter unit (`cm`) and the inches unit (`in`).

Now, let’s explore why CSS absolute units aren’t so absolute.

## CSS Pixels

Pixels have been the most common unit of CSS, dating to the beginning of the web. In the old world of desktop screens, before we had any smartphones, the screen’s pixels were always equivalent to CSS pixels.

In 2007, for example, the most common desktop resolution was `1024`&times;`768` pixels. Back then, we would normally give our web pages a fixed width of `1000` pixels to fit the entire page, and the leftover pixels would be saved for the browser’s scrollbar.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77e9ff8f-fe01-4bea-9ee1-f5007d7e69a1/8-css-absolute-units.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77e9ff8f-fe01-4bea-9ee1-f5007d7e69a1/8-css-absolute-units.jpg" width="800" height="322" sizes="100vw" caption="Monitors used to look quite different back in the day! (Image credit: <a href='https://www.shutterstock.com/de/image-photo/side-view-old-obsolete-computer-on-1340046218'>Shutterstock</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77e9ff8f-fe01-4bea-9ee1-f5007d7e69a1/8-css-absolute-units.jpg'>Large preview</a>)" alt="Old desktop screen" >}}

### Smartphone Screens

Smartphones brought another quiet evolution, starting the era of high-density screens. If we consider an iPhone 12 Pro, whose screen is `1170` pixels wide, we would count every `3` pixels on the device as `1` pixel in the CSS.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f130759d-ceb4-4a8e-806c-74c02feafbdc/10-css-units.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f130759d-ceb4-4a8e-806c-74c02feafbdc/10-css-units.png" width="800" height="304" sizes="100vw" caption="High-density screens caused the first separation between device pixels and CSS pixels. (Image credit: <a href='https://en.wikipedia.org/wiki/IPhone_(1st_generation)'>Wikipedia</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f130759d-ceb4-4a8e-806c-74c02feafbdc/10-css-units.png'>Large preview</a>)" alt="The density of iPhone screens over the years" >}}

When we size in mobile, we measure according to CSS pixels, not according to device pixels. To sum up:

- CSS pixel are **logical pixels**.
- Device pixels are real **physical pixels**.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da555c07-8491-4e32-9636-0a88fddc37c7/13-css-absolute-units.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da555c07-8491-4e32-9636-0a88fddc37c7/13-css-absolute-units.png" width="800" height="346" sizes="100vw" caption="1 CSS pixel could be more than 1 device pixel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da555c07-8491-4e32-9636-0a88fddc37c7/13-css-absolute-units.png'>Large preview</a>)" alt="High density screens comparison" >}}

Okay, but what about desktop devices? Do they still work with the same old pixel calculation? Let’s talk about that.

### Desktop Screens In 2021

High-density screens came to laptops several years later. The 2014 MacBooks got the first “retina” screens (retina being synonymous with high density).

These days, most laptops have a high-density screen.

Let’s consider **MacBooks**:

- The **13.3-inch MacBook Pro** has a screen that is `2560` pixels wide but that behaves like `1440` pixels. This means that every `1.778` physical pixels act like `1` logical pixel.
- The **16-inch MacBook Pro** has a screen that is `3072` pixels wide but that behaves like `1792` pixels. This means that every `1.714` physical pixels act like `1` logical pixel.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92725e4c-1d61-4206-b5d5-dcb8d0657237/5-css-absolute-units.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92725e4c-1d61-4206-b5d5-dcb8d0657237/5-css-absolute-units.png" width="800" height="352" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92725e4c-1d61-4206-b5d5-dcb8d0657237/5-css-absolute-units.png'>Large preview</a>)" alt="Built-in retina display showing 16-inch with 3072 times 1920 pixels" >}}

Among **PC laptops**, I tested two 15.6-inch screens, one with full HD resolution and the other with 4K resolution. The results were interesting:

- The **15.6-inch full-HD screen** is `1920` pixels wide but behaves like `1536` pixels. This means that every `1.25` physical pixels act like `1` logical pixel.
- The **15.6-inch 4K screen** is `3840` pixels wide but behaves, again, like `1536` pixels. This means that every `2.5` physical pixels act like `1` logical pixel.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9059155-7acf-437d-a846-83ead674e487/15-css-absolute-units.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9059155-7acf-437d-a846-83ead674e487/15-css-absolute-units.png" width="800" height="401" sizes="100vw" caption="These PC devices have different resolutions but act the same for CSS resolution. (Image credit: Elad Shechter) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9059155-7acf-437d-a846-83ead674e487/15-css-absolute-units.png'>Large preview</a>)" alt="Two 15.6-inch screens compared with full HD on the left and 4K on the right with both having a CSS resolution of 1536 times 864 pixels" >}}

As you can see, the connection between the real physical (i.e. device) pixels and the CSS (i.e. logical) pixels has almost vanished.

### Screens Have Become Denser Over The Years

In the past, if you looked closely at a screen, you could actually see its pixels. When the technology of screens improved, manufacturers started to create higher-density screens.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a04de8c-0c0b-42d0-a631-7aa477cd7581/example-device-pixels.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a04de8c-0c0b-42d0-a631-7aa477cd7581/example-device-pixels.png" width="800" height="526" sizes="100vw" caption="In the past, if you got close enough to your screen, you could see the device pixels. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a04de8c-0c0b-42d0-a631-7aa477cd7581/example-device-pixels.png'>Large preview</a>)" alt="A close-up of an image on a screen showing device pixels" >}}

**Recommended reading**: [*What Does A Foldable Web Actually Mean?*](https://www.smashingmagazine.com/2020/02/foldable-web-meaning/)

### Why Do We Calculate Logical Pixels Differently?

Over the years, as screens became denser, we couldn’t fit more content in the same screen size merely because the screen has more pixels.

Think about it for a moment. Consider the **Samsung Galaxy S21 Ultra**. Its narrower dimension is `1440` physical pixels. We could easily fit it in a regular desktop screen. But if we did, the text would be small to the point of being unreadable. Because of this, we separate physical pixels from logical pixels.

Sizes in CSS (i.e. width and height), then, are calculated according to CSS logical pixels. Of course, we can **use physical pixels to load high-density content**, such as images and videos, like so:

<pre><code class="language-markup">&lt;img src="image-size-1200px.jpg" width="300" &gt;
</code></pre>

OK, CSS pixels aren’t equal to a device’s physical pixels. But we have centimeters and inches. Those are physical units connected to the physical world, right? Let’s check them out.

{{% feature-panel %}}

## CSS Inches And CSS Centimeters

Wherever we use physical units like inches and centimeters, we know these are absolute units.

I had a thought that if CSS pixels aren’t equal to device pixels, then maybe it would be a good idea to use physical units such as inches and centimeters on the web. They are absolute units, right?

To be sure, I tested it. I created a box with a width and height of 1 centimeter and gave it a background color of red. I grabbed a real tape measure and got a surprise:

<blockquote>A CSS centimeter isn’t equal to a physical centimeter.</blockquote>

Here I am testing a CSS centimeter unit with a tape measure on a mid-2019 13-inch MacBook:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d78d3e39-e832-4ce5-8ce7-b440f646e478/6-css-absolute-units.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d78d3e39-e832-4ce5-8ce7-b440f646e478/6-css-absolute-units.jpg" width="800" height="450" sizes="100vw" caption="As you can see, a CSS centimeter is obviously not equal to a physical one. (Image credit: Elad Shechter) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d78d3e39-e832-4ce5-8ce7-b440f646e478/6-css-absolute-units.jpg'>Large preview</a>)" alt="Comparing a CSS centimeter with a physical centimeter using a tape on a 13-inch MacBook screen" >}}

The result is the same for CSS inches:

<blockquote>A CSS inch isn’t equal to a physical inch.</blockquote>

The same holds true for pica (`pc`) and millimeter (`mm`) units. These correspond to a part of either a CSS inch or a CSS centimeter, neither of which is connected to a real inch or a real centimeter.

### Why CSS Inches And Centimeters Aren’t Real Inches And Centimeters

Since the 1980s, the PC market has determined a CSS inch to be equivalent to `96` pixels. This calculation of pixels was directly tied to the DPI/PPI (pixels per inch) standard of Microsoft’s Windows operating system for monitors at the time, the most common of which had a standard of `96` DPI.

This meant that `1` CSS inch would always be equivalent to `96` CSS pixels.

As for CSS centimeters, every centimeter is directly calculated from inches, which means that `1` inch is equivalent to `2.54` centimeters. This means that every `1` CSS centimeter will always be equal to `37.7952756` CSS pixels.

In other words: `1cm = 37.7952756px (96px / 2.54)`.

{{< codepen height="480" theme_id="light" slug_hash="BaRJvWj" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [CSS Real Dimensions!](https://codepen.io/smashingmag/pen/BaRJvWj) by <a href="https://codepen.io/elad2412">Elad Shechter</a>.{{< /codepen >}}

That decision, which seemed like a good idea at the beginning of the PC industry (which had kind of one standard), turned out to be a poor decision that would make the CSS inch and centimeter obsolete and useless (at least from the perspective of the web).

Note that in the 1980s, Apple had a different standard of `72` DPI for screens.

### Screen Pixels Get Denser

As I mentioned, the DPI of screens got denser over the years, and we saw screens of `120` to `160` DPI. And because `1` CSS inch always equals `96` CSS pixels, it means now that a CSS inch isn’t equal to a real physical inch.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46791e27-5a92-4081-b9ee-512aa3a23d70/2-css-absolute-units.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46791e27-5a92-4081-b9ee-512aa3a23d70/2-css-absolute-units.png" width="800" height="429" sizes="100vw" caption="(Image credit: “<a href='https://hacks.mozilla.org/2013/09/css-length-explained/'>CSS Length Explained”, Mozilla Hacks</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46791e27-5a92-4081-b9ee-512aa3a23d70/2-css-absolute-units.png'>Large preview</a>)" alt="A table comparing baseline pixel density in three categories of devices: a twentieth century PC with CRT display, modern laptop with LCD, and smartphones and tablets" >}}

Because a CSS inch and a CSS centimeter are directly converted from CSS pixels, and because screens have gotten more DPIs over the years, we’ve gotten to the point where **these units don’t represent what they’re supposed to represent on screens**.

## CSS Point Unit

The point (`pt`) unit is one of the less-recognized units of CSS. As [Wikipedia states](https://en.wikipedia.org/wiki/Point_%28typography%29):

<blockquote>“In typography, the point is the smallest unit of measure. It is used for measuring font size, leading, and other items on a printed page.”</blockquote>

The Wikipedia page shows a ruler with the point scale on the bottom and the inch scale on the top:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffc7b6ca-e822-418d-90f8-b5d131f132b6/11-css-absolute-units.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffc7b6ca-e822-418d-90f8-b5d131f132b6/11-css-absolute-units.jpg" width="800" height="275" sizes="100vw" caption="(Image credit: <a href='https://en.wikipedia.org/wiki/Point_%28typography%29'>Wikipedia</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffc7b6ca-e822-418d-90f8-b5d131f132b6/11-css-absolute-units.jpg'>Large preview</a>)" alt="Ruler shown on the Wikipedia page" >}}

Before we get into why this unit isn’t really an absolute unit for the web, let’s go over the basic units of screens and printers.

### PPI And DPI

We’ve already mentioned DPI, and you might have heard those terms in the past, but if you’ve never understood what exactly they’re all about, here is quick primer:

- **PPI**  
Screens are built from a lot of small light dots, called pixels. To measure the density of pixels, we count the number of pixels that fit 1 inch, called pixels per inch (PPI).
- **DPI**  
Printers print color dots. To represent the density of printer dots, we count the number of dots that fit 1 inch of paper, called dots per inch (DPI).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ac03533-30f7-4e8a-8fa1-8ad843a29bcd/7-css-absolute-units.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ac03533-30f7-4e8a-8fa1-8ad843a29bcd/7-css-absolute-units.png" width="800" height="469" sizes="100vw" caption="(Image credit: <a href='https://www.shutterstock.com/de/image-vector/graphic-design-188149937'>Shutterstock</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ac03533-30f7-4e8a-8fa1-8ad843a29bcd/7-css-absolute-units.png'>Large preview</a>)" alt="PPI vs DPI: PPI refers to display resolution while DPI refers to printer resolution" >}}

In short, these are two ways to measure the density of visual information that we can fit in 1 inch.

- **PPI**: pixels per inch (for screens)
- **DPI**: dots per inch (for printers)

It is important to mention that the count of CSS pixels and dots in `1` inch are for both the width and the height. This means that on a screen of `96` PPI, a box with a height and width of `1` inch will have a total size of `9216` pixels (`96`&times;`96` px = `9216` px).

Here is a visual demonstration of `1` inch with a screen of `10` PPI:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bc351c3-f61d-4f40-999f-894cd485f0ea/3-css-absolute-units.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bc351c3-f61d-4f40-999f-894cd485f0ea/3-css-absolute-units.png" width="800" height="414" sizes="100vw" caption="(Image credit: <a href='https://www.shutterstock.com/de/image-vector/seamless-vector-background-similar-paper-676523518'>Shutterstock</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bc351c3-f61d-4f40-999f-894cd485f0ea/3-css-absolute-units.png'>Large preview</a>)" alt="A demonstration of 1 inch with a screen of 10 PPI" >}}

Here are some examples of real calculations of CSS PPI:

<table class="tablesaw">
  <thead>
    <tr>
      <th>CSS Resolution<br />(Pixels)</th>
      <th>CSS PPI</th>
      <th>CSS Inches<br />(width and height)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>96x96</td>
      <td>96</td>
      <td>1&times;1</td>
    </tr>
    <tr>
      <td>141&times;141</td>
      <td>141</td>
      <td>1&times;1</td>
    </tr>
  </tbody>
</table>

### “DPI” For Screens

Manufacturers of mobile and desktop devices prefer to express their screen measurements in DPI, not PPI. But don’t let that confuse you: **It is always PPI for screens and DPI for printers**.

### DPI/PPI Standards

To represent all those dots and pixels, we have the point (`pt`) unit.

But the point unit of CSS derives from the default printer DPI, which, again, was decided in the 1980s and is equal to `72` DPI. This means that `1` inch of CSS always equals `72` points.

- `1` inch = `72` points
- `1` point = `1/72`<sup>nd</sup> of `1` inch

### Pixels For Web, Dots For Printers

For the web, the DPI unit has no meaning. The web DPI is defined according to a different standard (`96` DPI), which we already talked about when we calculated a CSS inch and CSS centimeter. Because of this, there is no reason to use the point unit on the web.

**Note**: *`1` point isn’t equal to (CSS) pixels.*

- `1` point = `1.333` pixels
- `72` points = `1` inch
- `72` points = `96` pixels

{{% ad-panel-leaderboard %}}

## Printers

In this article, I mainly wanted to demonstrate why there aren’t any absolute units for the web. But what about using them for printers? Is there a reason to use CSS inches or centimeters or point units for printers?

### My Printing Test

I ran a small test to check whether the 1980s standard of DPI works correctly on printers. I created two boxes: one with a width and height of `72` points, and the second one with a width and height of `1` inch.

I printed these two boxes on a laser printer that I have in my office. Here is my Codepen for testing points and inches for printers:

{{< codepen height="480" theme_id="light" slug_hash="ZEKxMMy" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [1 inch](https://codepen.io/smashingmag/pen/ZEKxMMy) by <a href="https://codepen.io/elad2412">Elad Shechter</a>.{{< /codepen >}}

### Result

I printed this demo on a laser printer. To my surprise, if I use `72` points (or `1` inch), I get exactly `1` inch. This means that, for printers, there is still, maybe, a good reason to use CSS units such as points, inches, and centimeters.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/259bc61e-861f-4cea-8646-9517a29a3cab/4-css-absolute-units.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/259bc61e-861f-4cea-8646-9517a29a3cab/4-css-absolute-units.jpg" width="800" height="345" sizes="100vw" caption="(Image credit: Elad Shechter) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/259bc61e-861f-4cea-8646-9517a29a3cab/4-css-absolute-units.jpg'>Large preview</a>)" alt="On the left, the printer. On the right, the printed test." >}}

Printers are able to print more DPIs, but if we are working at `100%` zoom on the printer, then `72` points (or `1` inch) of CSS will equal a real physical inch.

**Reminder**: *This article is more about the connection of absolute units to the web rather than to printers. Of course, the results might change on different types of printers.*

**Recommended reading**: [*Using HSL Colors In CSS*](https://www.smashingmagazine.com/2021/07/hsl-colors-css/)

## Trying To Create Accurate Sizes On The Web

If we look at the 16-inch MacBook Pro, which has a ratio of `1.714` physical pixels to every `1` CSS pixel, we can’t accurately predict sizes on the web.

If we try to guess the real device pixel ratio on the 16-inch MacBook Pro using JavaScript’s `window.devicePixelRatio`, it will return an incorrect ratio of `2`, instead of `1.714`. (And this is without taking into account the zoom state of the web browser and operating system.)

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d2187ff-05d2-4721-941a-8aee1f433333/9-css-absolute-units.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d2187ff-05d2-4721-941a-8aee1f433333/9-css-absolute-units.jpg" width="800" height="375" sizes="100vw" caption="(Image credit: <a href='https://www.shutterstock.com/de/image-vector/measuring-tape-hands-person-making-measurements-1698787015'>Shutterstock</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d2187ff-05d2-4721-941a-8aee1f433333/9-css-absolute-units.jpg'>Large preview</a>)" alt="An illustration of a measuring tape" >}}

## Why We Need Real Absolute CSS Units

When we want to define a fixed size for a sidebar element, we would use CSS pixels. But if you think about it, CSS pixels have no meaning these days. As we saw above, on most smartphones and desktops, CSS pixels don’t describe device pixels anymore.

Based on this, I believe **we need actual physical units for CSS** (like a real centimeter or inch unit) because CSS pixels no longer have any true meaning on the web.

It’s worth mentioning that Firefox had implemented an actual physical millimeter unit (`mozmm`), but removed it in version 59. I don’t know why they removed it. Perhaps it’s because so many things already depend on CSS pixels, such as responsive images and the `em` and `rem` units. If we tried to add a new physical measurement, maybe it would cause more problems than it solves.

It seems that web folk have gotten so used to thinking in pixels that, even though the CSS pixel unit has lost its connection to device pixels, we’ll keep using the unit.

And in case you still think that CSS pixels are an excellent unit of measurement, try to explain to a new web developer what this unit is actually measuring.

For now, we don’t have any real way to describe physical sizes in CSS.

So, the **CSS pixel is the worst kind of absolute unit &mdash; except for all the others.**

{{% ad-panel-leaderboard %}}

## To Summarize

At the beginning of this article, I said that the absolute CSS units have become like new kinds of relative units. We started with CSS pixels, and we saw the difference between CSS pixels and device pixels.

Then, we found that CSS inches and CSS centimeters are directly converted from CSS pixels and aren’t connected to real inches and centimeters. In the end, we talked about the point unit and, again, about how this unit has no absolute meaning for the web.

### Final Words

That’s all. I hope you’ve enjoyed this article and learned from my experience. If you like this post, I would appreciate hearing about it and sharing it.

### References

* “[CSS Length Explained](https://hacks.mozilla.org/2013/09/css-length-explained/)”, Tim Chien, Robert Nyman, Mozilla Hacks
* “[Dots Per Inch](https://en.wikipedia.org/wiki/Dots_per_inch)”, Wikipedia
* “[Point (Typography)](https://en.wikipedia.org/wiki/Point_%28typography%29)”, Wikipedia
* “[CSS Values and Units](https://www.w3.org/TR/css-values-3/)”, W3C

{{< signature "vf, il, al" >}}

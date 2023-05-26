---
title: 'Fluid Typography: Predicting A Problem With Your User’s Zoom-In'
slug: fluid-typography-predict-problem-users-zoom-in
author: ruslan-yevych
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e896f9f1-7437-48c5-9481-483ae087a622/fluid-typography-predict-problem-users-zoom-in.jpg
date: 2022-12-30T15:00:00.000Z
summary: >-
  In this article, Ruslan Yevych will show you an easy way how to predict the appearance of a problem known as WCAG Failure Under 1.4.4 Resize Text (AA) while zooming the page. You will have a clear understanding of the possible risks of using responsive typography at the stage of development.
description: >-
  In this article, Ruslan Yevych will show you an easy way how to predict the appearance of a problem known as WCAG Failure Under 1.4.4 Resize Text (AA) while zooming the page. You will have a clear understanding of the possible risks of using responsive typography at the stage of development.
categories:
  - Typography
  - CSS
  - Techniques
---

When I wrote [my previous tutorial](https://www.smashingmagazine.com/2022/08/fluid-sizing-multiple-media-queries/) about the extended use of the CSS `clamp` function, I was surprised by the drawback of zooming of text in fluid typography.Thanks to [Adrian Bece](https://www.smashingmagazine.com/2022/01/modern-fluid-typography-css-clamp/) and [Adrian Roselli](https://adrianroselli.com/2019/12/responsive-type-and-zoom.html), I now know that this problem is known as a WCAG Failure Under 1.4.4 Resize Text (AA).

But what does this exactly mean?

<blockquote>“When people zoom a page, it is typically because they want the text to be bigger. When we anchor the text to the viewport size, even with a (fractional) multiplier, we can take away their ability to do that. It can be as much a barrier as disabling zoom. If a user cannot get the text to 200% of the original size, you may also be looking at a WCAG 1.4.4 Resize text (AA) problem &mdash; check out Failure of Success Criterion 1.4.4 due to incorrect use of viewport units to resize text.”<br /><br />&mdash; Adrian Roselli</blockquote>

The prominent example that demonstrates the problem is a [simple demo](https://codepen.io/pprg1996/pen/yLONLPv) from Adrian Roselli’s article, “[Responsive Type and Zoom](https://adrianroselli.com/2019/12/responsive-type-and-zoom.html).” Make the viewport width to 800px and see how text gets smaller while zooming to 220%. If you continue zooming, the text will begin to increase again, but will never reach its 2&times; increase in size (browsers currently have a zoom limit of 500%). 

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cfae04a-ad38-44c5-9982-f38a1dd6dce1/1-fluid-typography-predict-problem-users-zoom-in.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4837b218-b651-48b1-89b2-3b12ddf0ddf4/6-fluid-typography-predict-problem-users-zoom-in.gif" width="500" height="448" alt="Decreasing of text while zooming" /></a><figcaption>The text becomes smaller as the zoom increases. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cfae04a-ad38-44c5-9982-f38a1dd6dce1/1-fluid-typography-predict-problem-users-zoom-in.gif">Large preview</a>)</figcaption></figure>

When I started to study this question intently, I found out that there is no solution at the time as well as detailed explanation. The great recommendation is: 

<blockquote>“If you are going to use responsive typography techniques anyway, you must test it by zooming. Zoom across devices, across browsers, across viewport sizes (not everyone surfs full-screen), and across viewport orientations.”<br /><br />&mdash; Adrian Roselli</blockquote>

So, if you want to be sure that the user will be able to zoom in the text to at least 200% of original size, you should make a huge amount of tests. In this article I propose the solution **how to predict** the mentioned WCAG Failure at the stage of development. And I am not sure that my findings will guarantee the 100% absence of the problem, but I am sure that it will be helpful to avoid developers from rough errors in the real use cases.

## Not Responsive Typography

So, what is really going on when users try to zoom the web page? The answer to this question is very simple: **All modern browsers assume that pixel is stretchable**. Therefore, the screen size “effectively” decreases on zooming.

<blockquote><strong>Note</strong>: This article was written a few months ago, and OMG, Firefox now zooms pages correctly. The screen size doesn’t “effectively” decrease as you zoom in, but it is constant. Thus, the problem described in the article is still relevant for Chrome, Opera, but not for Firefox. So, while reading, you may find different behavior of the examples depending on the browser.</blockquote>

When we try to zoom the page to 200% of its original size, the pixel becomes twice as large in height and width. So, look at the code below:

<pre><code class="language-css">p {
  font-size: 16px;
}
</code></pre>

Without zooming, we will see a text of this paragraph as text of some *“visual-size”*. Due to different physical size of pixels for different devices, this *“visual-size”* will change from one device to another. Really, if your 42-inch TV has a resolution of 1920&times;1080 pixels, then it contains 2073600 pixels, and your 6.1-inch iPhone 13, for example, has a resolution of 2532&times;1170 pixels and contains a whopping 2962440 pixels. Let introduce some coefficient *k* that is proportional coefficient between *“visual-size”* (what we see on screen) and *“font-size”* (what we set in CSS):

$$(1)\\quad visual\\_size=k * font\\_size$$

{{< rimg class="MathJaxPlaceholder" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f35cc1-2cf7-41f9-9944-6623a9563258/1-formula-fluid-typography.png" width="800" height="176" sizes="100vw" caption="" alt="Formula 1" >}}

This coefficient depends on type of screen. But as we will see below, it does not effect on a final result. 

Now let’s try zoom in and see what happens. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d56d77eb-f7f6-44ec-aa9a-eb0f9513d875/2-fluid-typography-predict-problem-users-zoom-in.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d56d77eb-f7f6-44ec-aa9a-eb0f9513d875/2-fluid-typography-predict-problem-users-zoom-in.png" width="800" height="134" sizes="100vw" caption="Fig.2. Increasing of “visual-size” of text while zooming. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d56d77eb-f7f6-44ec-aa9a-eb0f9513d875/2-fluid-typography-predict-problem-users-zoom-in.png'>Large preview</a>)" alt="Increasing of text while zooming" >}}

As we can see, the `"visual-siz"e` of the text monotonically increases while zooming, and we can describe this by introducing the `"zoom-coefficient"` (browser zoom) as the following:

$$(2)\\quad visual\\_size=k * zoom\\_coefficient * font\\_size$$

{{< rimg  class="MathJaxPlaceholder" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04ac74ba-d8d4-490b-ba93-72765442e410/2-formula-fluid-typography.png" width="800" height="90" sizes="100vw" caption="" alt="Formula 2" >}}

The `"zoom-coefficient"` is equal to 1 for the original size (without zoom in), 2 &mdash; for 200% of browser zoom, 3 &mdash; for 300%, and so on, and `"zoom-coefficient"` &lt; 1 when we zoom out. Now we can introduce and calculate a `"visible-zoom"` coefficient, which is a measure of the real visible increasing (decreasing) of a size of the text, as ratio:

$$\begin{eqnarray}
(3)\quad visible\\_zoom&=&\frac{\textrm{size what we see while zooming}\,(zoom\\_coefficient\ne 1)}{\textrm{size what we see without zooming}\,(zoom\\_coefficient=1)}=\nonumber \\\\ \\\\ 
     &=&\frac{(k * zoom\\_coefficient * font\\_size)}{(k * font\\_size)}=zoom\\_coefficient \nonumber
\end{eqnarray}$$

{{< rimg class="MathJaxPlaceholder" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/587451d9-480b-434a-ab27-61587c64ac09/3-formula-fluid-typography.png" width="800" height="181" sizes="100vw" caption="" alt="Formula 3" >}}

As we can see from equation (3), the `"visible-zoom"` is equal to browser `"zoom-coefficient"`. That is, to double the text size (`"visible-size"` of text), we need to simple apply browser 200% zoom in. So, the mentioned WCAG Failure Under 1.4.4 Resize Text (AA) will never be observed in the case of not responsive typography (constant font size).

{{% feature-panel %}}

## Fluid Typography

So, what happens in the case of responsive typography? In the mentioned [simple demo](https://codepen.io/pprg1996/pen/yLONLPv) one can find the following record in CSS stylesheet:

<pre><code class="language-css">h1{
   font-size: clamp(1rem, -0.875rem + 8.333333vw, 3.5rem);
(&#42;)
}
</code></pre>

It is an example of fluid (responsive) typography. Fluid typography give us the possibility to change text smoothly with viewport width. The widespread implementation of such concept in CSS stylesheet is to use a `clamp` function. Using `clamp` you can smoothly change `"font-size"` between `"min-value"` and `"max-value"` in the given range of viewport width (from `"start-width"` to `"end-width"`).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d0130d1-26b3-47df-b7de-e70c0ffb6268/3-fluid-typography-predict-problem-users-zoom-in.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d0130d1-26b3-47df-b7de-e70c0ffb6268/3-fluid-typography-predict-problem-users-zoom-in.png" width="800" height="612" sizes="100vw" caption="Fig.3. Behavior of font size with viewport width defined by <code>clamp</code> function. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d0130d1-26b3-47df-b7de-e70c0ffb6268/3-fluid-typography-predict-problem-users-zoom-in.png'>Large preview</a>)" alt="Visualization of CSS clamp function" >}}

In such the case, when font-size value depends on viewport width, equations (2) and (3) can be easily modified. In these equations we should take into account two facts:

1. `"font-size"` depends on (function of) `"viewport-width"`, so `"font-size"` = `"font-size"("viewport-width")`;
2. The value of viewport width depends on `"zoom-coefficient"`.

The second fact is not so obvious like the first one. But we should remember that under zooming the viewport width “effectively” decreases. So, we will have the following transformation when zooming:

$$(4)\quad viewport\\_width\rightarrow\frac{viewport\\_width}{zoom\\_coefficient}$$

{{< rimg class="MathJaxPlaceholder" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3f9f8bb-575a-4d0a-95b1-75df36e99692/4-formula-fluid-typography.png" width="800" height="176" sizes="100vw" caption="" alt="Formula 4" >}}

Using relation (4), equation (3) take the following form:
 
$$\begin{eqnarray}
(5)\quad visible\\_zoom&=&\frac{k * zoom\\_coefficient * font\\_size\left(\frac{viewport\\_width}{zoom\\_coefficient}\right)}{k * font\\_size\left(\frac{viewport\\_width}{zoom\\_coefficient=1}\right)}=\nonumber \\\\ \\\\ \\\\
     &=&\frac{zoom\\_coefficient * font\\_size\left(\frac{viewport\\_width}{zoom\\_coefficient}\right)}{font\\_size\left(viewport\\_width\right)} \nonumber
\end{eqnarray}$$

{{< rimg class="MathJaxPlaceholder" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbd12499-28aa-4105-92ae-15fafd55106e/5-formula-fluid-typography.png" width="800" height="254" sizes="100vw" caption="" alt="Formula 5" >}}

Equation (5) and a simple criterion (“minimum 200% zoom requirement”):

$$(6)\quad visible\_zoom\ge 2$$

{{< rimg class="MathJaxPlaceholder" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26401600-76ff-4620-a59f-01c75aef2e27/6-formula-fluid-typography.png" width="550" height="176" sizes="100vw" caption="" alt="Formula 6" >}}

can be used to check whatever users can get text to 200% of its original size for the available range of browser zoom (up to 5 or 500% nowadays) for the any value of viewport width. On a practice, it is better to create some 3D plot in coordinates `"visible-zoom"` &mdash; `"viewport-width"` &mdash; `"zoom-coefficient"` or corresponding contour map. Such visualization is an easy way to estimate the extent of the problem if it exists.

**Example**: Let’s apply equation (5) to analyze the [simple demo](https://codepen.io/pprg1996/pen/yLONLPv) from Introduction. At first, we can reassemble the `(*)` record for better understanding of the parent behavior (what developer specified in). Here we will assume that browser’s default font size is `16px`. The influence of browser default font size on our conclusion will be discussed latter. Keeping in the mind `clamp("min-value", "responsive-value", "max-value")` function record form, we have from `(*)"min-value" = 1rem = 16px`, `"max-value" = 3.5rem = 56px`. Taken into account that viewport width is equal to `100vw`, we can write two equations to determine `"start-width"` and `"end-width"`:

<div class="break-out">

 <pre><code class="language-markup">-0.875rem + 0.08333333 \* "start-width" = 1rem;  
-0.875rem + 0.08333333 \* "end-width" = 3.5rem.
</code></pre>
</div>

From these equations one can find that `"start-width"= 22.5rem= 360px`, and `"end-width" = 52.5rem=840px`, or represent the result graphically:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b95b206-9327-4b56-b6e7-661b1bffcc99/4-fluid-typography-predict-problem-users-zoom-in.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b95b206-9327-4b56-b6e7-661b1bffcc99/4-fluid-typography-predict-problem-users-zoom-in.png" width="800" height="612" sizes="100vw" caption="Behavior of font size with viewport width defined by <code>clamp(16px, -14px + 8.333333vw, 56px)</code> function from <a href='https://codepen.io/pprg1996/pen/yLONLPv'>simple demo</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b95b206-9327-4b56-b6e7-661b1bffcc99/4-fluid-typography-predict-problem-users-zoom-in.png'>Large preview</a>)" alt="Visualization of CSS clamp function with certain parameters" >}}

To obtain the calculated dependency of `"visible-zoom"` on `"zoom-coefficient"` at 800px of viewport width where anomalous behavior is observed, we can use equation (5) with fixed value of *“viewport-width”* = 800px and plot the corresponding curve (by [Plotly JavaScript Open Source Graphing Library](https://plotly.com/javascript/)). Here you can see the result:

{{< codepen height="480" theme_id="light" slug_hash="ZEoMrjB" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [zoom(ex-2) [forked]](https://codepen.io/smashingmag/pen/ZEoMrjB) by <a href="https://codepen.io/ryevych">Ruslan</a>.{{< /codepen >}}  

The `"visible-zoom"` and `"zoom-coefficient"` are represented on graphics by percentage. So the 100% value mean the original size. As you can see, the observed anomalous behavior, when text becomes smaller as the zoom increases, is well reproduced. Moreover, it is shown that `"visible-zoom"` coefficient will never reach the value of 200%. Its maximum value is about 150% by applying the maximum possible 500% browser zoom. 

But what happens at other values of the viewport width? To explore this question one can create a 3D plot or corresponding projected contours:

{{< codepen height="480" theme_id="light" slug_hash="GRdXQBz" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [zoom(ex-3) [forked]](https://codepen.io/smashingmag/pen/GRdXQBz) by <a href="https://codepen.io/ryevych">Ruslan</a>.{{< /codepen >}}

As you can see, when the font size of the text is determined by the `(*)` record, `"visible-zoom"` is less than 200% (grey color) when zooming for the wide range of the viewport values &mdash; from about 650 to 1680px. According to the [data](https://www.w3schools.com/browsers/browsers_display.asp), this range for screen resolution is still very popular. Given the above, it is very likely that users will have a problem while zooming. `MinValue`, `maxValue`, `startWidth`, `endWidth` constants in Codepen define the behavior of font size shown in Fig.4. You can change it to test your own cases.

So, using the equation (5) and the graphs built with it, we were able to easily explain the observed anomalous behavior of the font size while zooming. 

{{% ad-panel-leaderboard %}}

## Browser Default Font Size

Let’s analyze the influence of browser default font size on the fulfillment of *“minimum 200% zoom requirement”* on the example of [simple demo](https://codepen.io/pprg1996/pen/yLONLPv). [Here](https://codepen.io/ryevych/pen/YzYbjBq) one can change a value for `browserDefaultFontSize` variable from 16 to another values and see the changes. Figure 5 shows the result for `browserDefaultFontSize = 16, …, 28 (px)`.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c925362-38dd-4af6-81c8-678fcc520924/5-fluid-typography-predict-problem-users-zoom-in.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c925362-38dd-4af6-81c8-678fcc520924/5-fluid-typography-predict-problem-users-zoom-in.gif" width="800" height="500" alt="Fig.5. Fulfillment of “minimum 200% zoom requirement” when browser default font size changes" /></a><figcaption>Influence of browser default font size on the fulfillment of “minimum 200% zoom requirement”.</figcaption></figure>

As you can see there is nothing but a “stretching” along *“viewport-width”*-axis only. By increasing of browser default font size, we just move the area of viewport widths where *“minimum 200% zoom requirement”* is failed. The main peculiarities of the text font size changing when zooming remain the same.

## Media Queries

Above we considered the case where there no media queries influent on text font size. It is time to analyze what will change in the opposite case? It is strongly recommended to use relative units in media query condition (read [this article by Zell](https://zellwk.com/blog/media-query-units/), for example). In such the cases, there will no difference how to define the fluid typography &mdash; using media queries or not. (You can find the algorithm how to specify an any complicated behavior of responsive font size without media queries in [my previous tutorial](https://www.smashingmagazine.com/2022/08/fluid-sizing-multiple-media-queries/).)

Now we can describe a usage of equation (5) for different cases:

1. Without media queries &mdash; one can directly apply the equation (5).
2. With media query/queries (features are in *em*, recommended), *“font-size”* depends on viewport width as:

{{< rimg class="MathJaxPlaceholder" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/214d0a13-7cc5-43fe-86ca-5ebd8a3e0bad/7-formula-fluid-typography.png" width="800" height="150" sizes="100vw" caption="" alt="Formula 7a" >}}

$$\begin{eqnarray}
(7)\&\quad\& font\\_size(viewport\\_width)=\nonumber\\\\[5pt]
\&=\&\\left\\{\\begin{array}{cc}
    function_1 (viewport\\_width),\\,viewport\\_width>breakPoint_1,\nonumber\\\\[3pt]
    function_2 (viewport\\_width),\\,breakPoint_1>viewport\\_width>breakPoint_2,\nonumber
  \\end{array}\\right.
\end{eqnarray}$$

- You can exclude it by using the algorithm proposed in [my previous article](https://www.smashingmagazine.com/2022/08/fluid-sizing-multiple-media-queries/) and return to pt. 1;
- For given `"viewport-width"` and `"zoom-coefficient"`, we should transform the equation (7) to use as numerator in equation (5) like:

$$\begin{eqnarray}
\&\quad& font\\_size\left(\frac{viewport\\_width}{zoom\\_coefficient}\right)=\nonumber\\\\[5pt]
\&=\&\\left\\{\\begin{array}{cc}
    function_1\left(\frac{viewport\\_width}{zoom\\_coefficient}\right),\\,\frac{viewport\\_width}{zoom\\_coefficient}>breakPoint_1,\nonumber\\\\[3pt]
    function_2\left(\frac{viewport\\_width}{zoom\\_coefficient}\right),\\,breakPoint_1>\frac{viewport\\_width}{zoom\\_coefficient}>breakPoint_2,\nonumber
  \\end{array}\\right.
\end{eqnarray}$$

{{< rimg class="MathJaxPlaceholder" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/600d6e2f-933e-4de5-92e7-1ed0637504ed/8-formula-fluid-typography.png" width="800" height="215" sizes="100vw" caption="" alt="Formula 7b" >}}

It is your choice how to use equation (5), but I recommend to reduce the task to pt. 1/2(i).

It should be noted that we did not consider operating system zoom here. When user applied it this will also affect on “effective” screen size. As a result, the `"zoom-coefficient"` should be represented as a product of browser and operating system zoom. Such influence on final prediction will be similar to the case of changing browser default font size.

{{% ad-panel-leaderboard %}}

## Conclusion

Now we are able to predict the behavior of text size changing while zooming to avoid the WCAG Failure Under 1.4.4 Resize Text (AA). Equation (5) and *“minimum 200% zoom requirement”* (6) give us an easy way to anticipate a problem on the stage of development and analyze it. Due to a variety of possible dependencies for a text font size on viewport width that developer can implement, there is no general solution of a problem. But you can slightly change the input parameters and view the predictions. In most cases, such corrections will give the desired result. We should make a choice in favor of completely eliminating possible problems with text scaling.

{{< signature "vf, yk, il" >}}

<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<style type="text/css">
@media (prefers-color-scheme: dark) {
  mjx-mi, mjx-mo, mjx-c {
    color: white !important;
  }
}
.MathJaxPlaceholder {
  display: block;
}
.MathJax {
  display: none !important;
}
@media all and (min-width: 768px) {
  .MathJaxPlaceholder {
    display: none !important;
  }
  .MathJax {
    display: block !important;
  }
}
</style>

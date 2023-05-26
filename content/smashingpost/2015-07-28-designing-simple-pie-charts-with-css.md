---
title: 'Designing A Flexible, Maintainable CSS Pie Chart With SVG'
slug: designing-simple-pie-charts-with-css
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/550931a3-57b7-4a7d-a9a1-af472ba2a0f0/pie-charts.png'
date: 2015-07-28T21:12:34.000Z
author: lea-verou
description: >-
  Pie charts have traditionally been anything but simple to create with web technologies, despite being incredibly common for information ranging from simple stats to progress indicators and timers.
summary: >-
  Pie charts have traditionally been anything but simple to create with web technologies, despite being incredibly common for information ranging from simple stats to progress indicators and timers.
categories:
  - Coding
  - CSS
  - Techniques
  - SVG
---

Pie charts, even in their simplest two-color form, have traditionally been anything but simple to create with web technologies, despite being incredibly common for information ranging from simple stats to progress indicators and timers. Implementations usually involved either using an external image editor to create **multiple images for multiple values** of the pie chart, or large JavaScript frameworks designed for much more complex charts.

Although the feat is not as impossible as it once was, there’s still no simple one-liner for it. However, there are many better, more **maintainable ways to achieve it today**.

<div class="c-felix-the-cat">
<h4 class="h3">Creating Cel Animations With SVG</h4>
<p>What if there was an image format like GIF, but it worked with vectors? The image format, SVG, already exists. Let’s  take a somewhat primitive art and breath new life into it.</p><p><a href="https://www.smashingmagazine.com/2015/09/creating-cel-animations-with-svg/" class="btn btn--small btn--green">Jump to a related article&nbsp;↬</a></p>
</div>

## Transform-Based Solution

This solution is the best in terms of markup: it only needs one element and the rest is done with pseudo-elements, transforms and CSS gradients. Let‘s start with a simple element:

<pre><code class="language-markup">&lt;div class="pie"&gt;&lt;/div&gt;
</code></pre>

For now, let’s assume we want a pie chart that displays the hardcoded percentage **20%**. We will work on making it flexible later. Let’s first style the element as a circle, which will be our background (Figure 1):

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ababdce-3803-4c9c-bb34-b7390316a1e2/pie-chart-01.png"><figcaption>Figure 1: Our starting point (or, a pie chart showing 0%)</figcaption>
</figure>

<pre><code class="language-css">.pie {
  width: 100px; height: 100px;
  border-radius: 50%;
  background: yellowgreen;
}
</code></pre>

Our pie chart will be green (specifically `yellowgreen`) with brown (`#655`) showing the percentage. We might be tempted to use skew transforms for the percentage part, but as a little experimentation shows, they prove to be a very messy solution. Instead, we will color the left and right parts of our circle in our **two colors**, and use a **rotating pseudo-element to uncover only the percentage we need**.

{{% feature-panel %}}

To color the right part of our circle brown, we will use a simple linear gradient:

<pre><code class="language-css">background-image:
  linear-gradient(to right, transparent 50%, #655 0);
</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86b4f1a7-9592-4f8f-8dbb-5990670c1f13/pie-chart-02.png"></figure>
  <figcaption>Figure 2: Coloring the right part of our circle brown, with a simple linear gradient</figcaption>
</figure>

As you can see in Figure 2, this is all that’s needed. Now, we can proceed to styling the pseudo-element that will act as a mask:

<pre><code class="language-css">.pie::before {
  content: ’;
  display: block;
  margin-left: 50%;
  height: 100%;
}
</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44f22a8-cd71-4a5b-b2e4-8994d5570067/pie-chart-03.png"></figure>
  <figcaption>Figure 3: The pseudo-element that will act as a mask is shown here with dashed lines</figcaption>
</figure>

You can see in Figure 3 where our pseudo-element currently lies relative to the pie element. Currently, it’s not styled and it doesn’t cover anything. It’s merely an invisible rectangle. To start styling it, let’s make a few observations:

- Because we want it to **cover the brown part of our circle**, we need to apply a green background to it, using `background-color: inherit` to avoid duplication, as we want it to have the same background color as its parent.
- We want it to **rotate around the circle’s center**, which is on the middle of the pseudo-element’s left side, so we should apply a `transform-origin` of `0 50%` to it, or just `left`.
- We don’t want it to be a rectangle, as it makes it bleed past the edges of the pie chart, so we need to either apply `overflow: hidden` to the `.pie`, or an appropriate `border-radius` to make it a semicircle.

Putting it all together, our pseudo-element’s CSS will look like this:

<pre><code class="language-css">.pie::before {
  content: ’;
  display: block;
  margin-left: 50%;
  height: 100%;
  border-radius: 0 100% 100% 0 / 50%;
  background-color: inherit;
  transform-origin: left;
}
</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a350921d-cb1f-4a85-853b-0dca1b787b8d/pie-chart-04.png"></figure>
  <figcaption>Figure 4: Our pseudo-element (shown here with a dashed outline) after we finished styling it</figcaption>
</figure>

<blockquote>Note: Take care not to use <code>background: inherit;</code>, instead of the <code>background-color: inherit;</code>, otherwise the gradient will be inherited too!</blockquote>

Our pie chart currently looks like Figure 4\. This is where the fun begins! We can start **rotating the pseudo-element**, by applying a `rotate()` transform. For the **20%** we were trying to achieve, we can use a value of `72deg` (0.2 × 360 = 72), or `.2turn`, which is much more readable. You can see how it looks for a few other values as well, in Figure 5.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66a91ddb-a723-438d-8a7e-51328ab53ca4/pie-chart-05.png">
  <figcaption>Figure 5: Our simple pie chart showing different percentages; from top to bottom: 10% (<code>36deg</code> or <code>.1turn</code>), 20% (<code>72deg</code> or <code>.2turn</code>), 40% (<code>144deg</code> or <code>.4turn</code>)</figcaption>
</figure>

We might be tempted to think we’re done, but unfortunately it’s not that simple. Our pie chart works great for displaying percentages from 0 to 50%, but if we try to depict a 60% rotation (by applying `.6turn`), Figure 6 happens. Don’t lose hope yet, though, as we can — and we will — fix this!

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e863910-c49b-4a32-9297-863b0304189d/pie-chart-06.png">
  <figcaption>Figure 6: Our pie chart breaks for percentages <strong>greater than 50%</strong> (shown here: <strong>60%</strong>)</figcaption>
</figure>

If we think about 50%–100% percentages as a separate problem, we might notice that we can use **an inverted version of the previous solution** for them: a brown pseudo-element, rotating from `0` to `.5turn`, respectively. So, for a 60% pie, the pseudo-element code would look like this:

<pre><code class="language-css">.pie::before {
  content: ’;
  display: block;
  margin-left: 50%;
  height: 100%;
  border-radius: 0 100% 100% 0 / 50%;
  background: #655;
  transform-origin: left;
  transform: rotate(.1turn);
}
</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71f16ab4-108e-4b41-af8f-b769d747d99c/pie-chart-07.png"></figure>
  <figcaption>Figure 7: Our now correct 60% pie</figcaption>
</figure>

You can see this in action in Figure 7\. Because we’ve now worked out a way to depict any percentage, we could even **animate the pie chart from 0% to 100% with CSS animations**, creating a fancy progress indicator:

<pre><code class="language-css">@keyframes spin {
  to { transform: rotate(.5turn); }
}

@keyframes bg {
  50% { background: #655; }
}

.pie::before {
  content: ’;
  display: block;
  margin-left: 50%;
  height: 100%;
  border-radius: 0 100% 100% 0 / 50%;
  background-color: inherit;
  transform-origin: left;
  animation: spin 3s linear infinite,
             bg 6s step-end infinite;
}
</code></pre>

{{% feature-panel %}}

## Animated Pie

All this is good, but how do we style multiple static pie charts with different percentages, which is the most common use case? Ideally, we want to be able to type something like this:

<pre><code class="language-markup">&lt;div class="pie"&gt;20%&lt;/div&gt;
&lt;div class="pie"&gt;60%&lt;/div&gt;
</code></pre>

…and get two pie charts, one showing 20%, and the other one showing 60%. First, we will explore how we can do it with inline styles, and then we could always write a short script to parse the text content and add said inline styles, for code elegance, encapsulation, maintainability, and perhaps most importantly, accessibility.

The challenge to controlling the pie chart percentage with inline styles is that the CSS code that is responsible for setting the percentage is set on the pseudo-element. As you already know, **we cannot set inline styles on pseudo-elements**, so **we need to be inventive**.

<blockquote>Note: You can use the same technique for other cases where you want to use <strong>values from a spectrum</strong> without repetition and complex calculations, as well as for <strong>debugging animations</strong> by stepping through them. View a simpler, isolated example of the technique.</blockquote>

The solution comes from one of the most unlikely places. We are going to use the animation we already presented, but it will be **paused**. Instead of running it like a normal animation, we are going to use negative animation delays to **step through to any point in the animation** statically and stay there. Confused? Yes, a negative `animation-delay` is not only allowed by the specification, but is very useful for cases like this:

<blockquote>
A negative delay is <strong>valid</strong>. Similar to a delay of ‘<code>0s</code>’, it means that the animation executes immediately, but is automatically progressed by the absolute value of the delay, as if the animation had started the specified time in the past, and so it appears to start partway through its active duration.
&mdash;<a href="https://drafts.csswg.org/css-animations-1/#animation-delay">CSS Animations Level 1</a>
</blockquote>

Because our animation is paused, the first frame of it (defined by our negative `animation-delay`), will be the only one displayed. The percentage shown on the pie chart will be the percentage of the total duration our `animation-delay` is. For example, with the current duration of `6s`, we would need an `animation-delay` of `-1.2s` to display a 20% percentage. To simplify the math, we will set a duration of `100s`. Keep in mind that because the animation is paused forever, the duration we specify has no other effect.

There is one last issue: the **animation is on the pseudo-element, but we want to set an inline style on the `.pie` element**. However, because there is no animation on the `<div>`, we can set the `animation-delay` on that as an inline style, and then use `animation-delay: inherit;` on the pseudo-element. To put it together, our markup for the 20% and 60% pie charts will look like this:

<pre><code class="language-markup">&lt;div class="pie"
     style="animation-delay: -20s"&gt;&lt;/div&gt;
&lt;div class="pie"
     style="animation-delay: -60s"&gt;&lt;/div&gt;
</code></pre>

And the CSS code we just presented for this animation would now become (not including the `.pie` rule, as that stays the same):

<pre><code class="language-css">@keyframes spin {
  to { transform: rotate(.5turn); }
}

@keyframes bg {
  50% { background: #655; }
}

.pie::before {
  /* [Rest of styling stays the same] */
  animation: spin 50s linear infinite,
             bg 100s step-end infinite;
  animation-play-state: paused;
  animation-delay: inherit;
}
</code></pre>

At this point, we can convert the markup to use percentages as content, as we originally aimed for, and add the `animation-delay` inline styles via a simple script:

<pre><code class="language-javascript">$$('.pie').forEach(function(pie) {
  var p = parseFloat(pie.textContent);
  pie.style.animationDelay = '-' + p + 's';
});
</code></pre>

Note that we left the text intact, because we need it for accessibility and usability reasons. Currently, our pie charts look like Figure 8\. We need to hide the text, which we can do accessibly via `color: transparent`, so that it remains **selectable and printable**. As extra polish, we can **center the percentage in the pie chart**, so that it’s not in a random place when the user selects it. To do that, we need to:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24ff6c2c-378e-4880-9653-3fc9351cbf4d/pie-chart-08.png">
  <figcaption>Figure 8: Our text, before we hide it</figcaption>
</figure>

- Convert the pie’s `height` to `line-height` (or add a `line-height` equal to the `height`, but that’s pointless code duplication, because `line-height` would set the computed height to that as well).
- Size and position the pseudo-element via **absolute positioning**, so that it doesn’t push the text down
- Add `text-align: center;` to horizontally center the text.

The final code looks like this:

<pre><code class="language-css">.pie {
  position: relative;
  width: 100px;
  line-height: 100px;
  border-radius: 50%;
  background: yellowgreen;
  background-image:
    linear-gradient(to right, transparent 50%, #655 0);
  color: transparent;
  text-align: center;
}

@keyframes spin {
  to { transform: rotate(.5turn); }
}
@keyframes bg {
  50% { background: #655; }
}

.pie::before {
  content: ’;
  position: absolute;
  top: 0; left: 50%;
  width: 50%; height: 100%;
  border-radius: 0 100% 100% 0 / 50%;
  background-color: inherit;
  transform-origin: left;
  animation: spin 50s linear infinite,
             bg 100s step-end infinite;
  animation-play-state: paused;
  animation-delay: inherit;
}
</code></pre>

### SVG Solution

SVG makes a lot of graphical tasks easier and pie charts are no exception. However, instead of creating a pie chart with paths, which would require complex math, we are going to use a little trick instead.

Let’s start with a circle:

<pre><code class="language-markup">&lt;svg width="100" height="100"&gt;
&lt;circle r="30" cx="50" cy="50" /&gt;
&lt;/svg&gt;
</code></pre>

Now, let’s apply some basic styling to it:

<pre><code class="language-css">circle {
  fill: yellowgreen;
  stroke: #655;
  stroke-width: 30;
}
</code></pre>

<blockquote>Note: As you might know, these <strong>CSS properties are also available as attributes</strong> on the SVG element, which might be convenient if portability is a concern.</blockquote>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01cdbddb-05fe-4d9a-a4cc-cdc4f75975e4/pie-chart-09.png">
  <figcaption>Figure 9: Our starting point: a green SVG circle with a fat <code>#655</code> stroke</figcaption>
</figure>

You can see our stroked circle in Figure 9\. SVG strokes don’t just consist of the `stroke` and `stroke-width` properties. There are many other less popular stroke-related properties to fine-tune strokes. One of them is `stroke-dasharray`, intended for creating dashed strokes. For example, we could use it like this:

<pre><code class="language-css">stroke-dasharray: 20 10;
</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ab6a735-462c-4d54-851d-64be4e53a9b4/pie-chart-10.png"></figure>
  <figcaption>Figure 10: A simple dashed stroke, created with <code>stroke-dasharray</code></figcaption>
</figure>

This means we want dashes of length `20` with gaps of length `10`, like the ones in Figure 10\. At this point, you might be wondering what on earth this SVG stroke primer has to do with pie charts. It starts getting clearer when we apply a stroke with a dash width of `0` and a gap width greater than or equal to the circumference of our circle (C = 2πr, so in our case C = 2π × 30 ≈ 189):

<pre><code class="language-css">stroke-dasharray: 0 189;
</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/463cc404-ee8e-4e89-ba13-46b45189aea2/pie-chart-11.png"></figure>
  <figcaption>Figure 11: Multiple <code>stroke-dasharray</code> values and their effect; from left to right:<code>0 189</code>; <code>40 189</code>; <code>95 189</code>; <code>150 189</code></figcaption>
</figure>

As you can see in the first circle in Figure 11, this completely removes any stroke, and we’re left with just a green circle. However, the fun begins when we start increasing the first value (Figure 11): because the gap is so long, we no longer get a dashed stroke, just a stroke that covers the percentage of the circle’s circumference that we specify.

You might have started to figure out where this is going: if we reduce the radius of our circle enough that it’s completely covered by its stroke, we end up with something that resembles a pie chart quite closely. For example, you can see in Figure 12 how that looks when applied to a circle with a radius of `25` and a `stroke-width` of `50`, like what’s produced by the following code:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37cb104a-0eef-49e7-a8c2-e5527575024f/pie-chart-12.png">
  <figcaption>Figure 12: Our SVG graphic is starting to resemble a pie chart</figcaption>
</figure>

<aside id="note-remember">Remember: SVG strokes are always half inside and half outside the element they’re applied to. In the future, we will be able to control this behavior.</aside>

<pre><code class="language-markup">&lt;svg width="100" height="100"&gt;
  &lt;circle r="25" cx="50" cy="50" /&gt;
&lt;/svg&gt;
</code></pre>

<pre><code class="language-css">circle {
  fill: yellowgreen;
  stroke: #655;
  stroke-width: 50;
  stroke-dasharray: 60 158; /* 2π × 25 ≈ 158 */
}
</code></pre>

Now, turning it into a pie chart like the ones we made in the previous solution is rather easy: we just need to add **a larger green circle underneath the stroke**, and **rotate it 90° counterclockwise** so that it starts from the top-middle. Because the `&lt;svg&gt;` element is also an HTML element, we can just style that:

<pre><code class="language-css">svg {
  transform: rotate(-90deg);
  background: yellowgreen;
  border-radius: 50%;
}
</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69331269-a4b2-4adf-8817-baa79c58908d/pie-chart-13.png"></figure>
  <figcaption>Figure 13: The final SVG pie chart</figcaption>
</figure>

You can see the final result in Figure 13\. This technique makes it even easier to animate the pie chart from `0%` to `100%`. We just need to create a CSS animation that animates `stroke-dasharray` from `0 158` to `158 158`:

<pre><code class="language-css">@keyframes fillup {
  to { stroke-dasharray: 158 158; }
}

circle {
  fill: yellowgreen;
  stroke: #655;
  stroke-width: 50;
  stroke-dasharray: 0 158;
  animation: fillup 5s linear infinite;
}
</code></pre>

As an additional improvement, we can specify a certain radius on the circle so that the length of its circumference is (infinitesimally close to) 100, so that we can **specify the `stroke-dasharray` lengths as percentages**, without having to make calculations. Because the circumference is 2πr, our radius needs to be 100 ÷ 2π ≈ 15.915494309, which for our needs could be rounded up to 16\. We will also specify the SVG’s dimensions in the `viewBox` attribute instead of the `width` and `height` attributes, to make it adjust to the size of its container.

After these modifications, the markup for the pie chart of Figure 13 would now become:

<pre><code class="language-markup">&lt;svg viewBox="0 0 32 32"&gt;
  &lt;circle r="16" cx="16" cy="16" /&gt;
&lt;/svg&gt;
</code></pre>

And the CSS would become:

<pre><code class="language-css">svg {
  width: 100px; height: 100px;
  transform: rotate(-90deg);
  background: yellowgreen;
  border-radius: 50%;
}

circle {
  fill: yellowgreen;
  stroke: #655;
  stroke-width: 32;
  stroke-dasharray: 38 100; /* for 38% */
}
</code></pre>

Note **how easy it now is to change the percentage**. Of course, even with this simplification, we don’t want to have to repeat all this SVG markup for every pie chart. It’s time for JavaScript to lend us its helping hand for a little bit of automation. We will write a small script to take simple HTML markup like the following…

<pre><code class="language-markup">&lt;div class="pie"&gt;20%&lt;/div&gt;
&lt;div class="pie"&gt;60%&lt;/div&gt;
</code></pre>

…and add an inline SVG inside every `.pie` element, with all necessary elements and attributes. It will also add a `<title>` element, for accessibility, so that screen reader users can also know what percentage is displayed. The final script will look like this:</title>p>

<pre><code class="language-javascript">$$('.pie').forEach(function(pie) {
  var p = parseFloat(pie.textContent);
  var NS = "https://www.w3.org/2000/svg";
  var svg = document.createElementNS(NS, "svg");
  var circle = document.createElementNS(NS, "circle");
  var title = document.createElementNS(NS, "title");
  circle.setAttribute("r", 16);
  circle.setAttribute("cx", 16);
  circle.setAttribute("cy", 16);
  circle.setAttribute("stroke-dasharray", p + " 100");
  svg.setAttribute("viewBox", "0 0 32 32");
  title.textContent = pie.textContent;
  pie.textContent = ’;
  svg.appendChild(title);
  svg.appendChild(circle);
  pie.appendChild(svg);
});
</code></pre>

That’s it! You might be thinking that the CSS method is better, because its code is simpler and less alien. However, the SVG method has certain benefits over the pure CSS solution:

- It’s **very easy to add a third color**: just add another stroked circle and shift its stroke with `stroke-dashoffset`. Alternatively, add its stroke length to the stroke length of the circle before (underneath) it. How exactly do you picture adding a third color to pie charts made with the first solution?
- We **don’t have to take any extra care for printing**, as SVG elements are considered content and are printed, just like `<img>` elements. The first solution depends on backgrounds, and thus, will not print.
- We can **change the colors with inline styles**, which means we can easily change them via **scripting** (e.g., depending on **user input**). The first solution relies on pseudo-elements, which cannot take inline styles except via inheritance, which is not always convenient.

<pre><code class="language-css">circle {
  fill: yellowgreen;
  stroke: #655;
  stroke-width: 32;
  stroke-dasharray: 38 100; /* for 38% */
}
</code></pre>

Note **how easy it now is to change the percentage**. Of course, even with this simplification, we don’t want to have to repeat all this SVG markup for every pie chart. It’s time for JavaScript to lend us its helping hand for a little bit of automation. We will write a small script to take simple HTML markup like the following…

<pre><code class="language-markup">&lt;div class="pie"&gt;20%&lt;/div&gt;
&lt;div class="pie"&gt;60%&lt;/div&gt;
</code></pre>

…and add an inline SVG inside every `.pie` element, with all necessary elements and attributes. It will also add a `<title>` element, for accessibility, so that screen reader users can also know what percentage is displayed. The final script will look like this:</title>p>

<pre><code class="language-javascript">$$('.pie').forEach(function(pie) {
  var p = parseFloat(pie.textContent);
  var NS = "https://www.w3.org/2000/svg";
  var svg = document.createElementNS(NS, "svg");
  var circle = document.createElementNS(NS, "circle");
  var title = document.createElementNS(NS, "title");
  circle.setAttribute("r", 16);
  circle.setAttribute("cx", 16);
  circle.setAttribute("cy", 16);
  circle.setAttribute("stroke-dasharray", p + " 100");
  svg.setAttribute("viewBox", "0 0 32 32");
  title.textContent = pie.textContent;
  pie.textContent = ’;
  svg.appendChild(title);
  svg.appendChild(circle);
  pie.appendChild(svg);
});
</code></pre>

That’s it! You might be thinking that the CSS method is better, because its code is simpler and less alien. However, the SVG method has certain benefits over the pure CSS solution:

- It’s **very easy to add a third color**: just add another stroked circle and shift its stroke with `stroke-dashoffset`. Alternatively, add its stroke length to the stroke length of the circle before (underneath) it. How exactly do you picture adding a third color to pie charts made with the first solution?
- We **don’t have to take any extra care for printing**, as SVG elements are considered content and are printed, just like `<img>` elements. The first solution depends on backgrounds, and thus, will not print.
- We can **change the colors with inline styles**, which means we can easily change them via **scripting** (e.g., depending on **user input**). The first solution relies on pseudo-elements, which cannot take inline styles except via inheritance, which is not always convenient.

## Future Pie Charts

Conical gradients would be immensely helpful here too. All it would take for a pie chart would be a circular element, with a conical gradient of two color stops. For example, the **40% pie chart** in Figure 5 would be as simple as:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95ef3e41-ffed-45b8-a063-9f9ae778d828/pie-chart-14.png"></figure>

<pre><code class="language-css">.pie {
  width: 100px; height: 100px;
  border-radius: 50%;
  background: conic-gradient(#655 40%, yellowgreen 0);
}
</code></pre>

Furthermore, once the updated `attr()` function defined in [CSS Values Level 3](https://w3.org/TR/css3-values/#attr-notation) is widely implemented, you will be able to control the percentage with a simple HTML attribute:

<pre><code class="language-css">background: conic-gradient(#655 attr(data-value %), yellowgreen 0);
</code></pre>

This also makes it incredibly easy to add a third color. For example, for a pie chart like the one shown on the pie chart above, we would just add two more color stops:

<pre><code class="language-css">background: conic-gradient(deeppink 20%, #fb3 0, #fb3 30%, yellowgreen 0);
</code></pre>

_Editor’s note_: You can use conic gradients today thanks to [Lea’s Conic Gradient polyfill]( https://leaverou.github.io/conic-gradient/), published shortly after her SmashingConf talk. And this is how you would design a simple pie chart with CSS! What method would you use and why? Or perhaps you've come up with an entirely different solution? Let us know in the comments to this post!

{{< signature "vf, ml, mh, og, il" >}}

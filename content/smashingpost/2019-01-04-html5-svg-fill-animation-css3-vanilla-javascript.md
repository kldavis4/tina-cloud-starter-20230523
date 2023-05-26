---
title: 'HTML5 SVG Fill Animation With CSS3 And Vanilla JavaScript'
slug: html5-svg-fill-animation-css3-vanilla-javascript
author: marina-ferreira
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5538b933-8d87-4609-bd37-9fa9fb4321a9/note-display-template.jpg
date: 2019-01-04T13:00:19+01:00
summary: >-
  In this article, you can learn how to build the animated note display from the <a href="https://www.awwwards.com/">Awwwards</a> website. It discusses the HTML5 SVG circle element, its stroke properties, and how to animate them with CSS variables and Vanilla JavaScript.
description: >-
  In this article, you can learn how to build the animated note display from the <a href="https://www.awwwards.com/">Awwwards</a> website. It discusses the HTML5 SVG circle element, its stroke properties, and how to animate them with CSS variables and Vanilla JavaScript.
categories:
  - JavaScript
  - CSS
  - HTML
  - SVG
  - Animation
---
SVG stands for **S**calable **V**ector **G**raphics and it is a standard XML-based markup language for vector graphics. It allows you to draw paths, curves, and shapes by determining a set of points in the 2D plane. Moreover, you can add twitch properties on those paths (such as stroke, color, thickness, fill, and more) in order to produce animations.

Since April 2017, [CSS Level 3 Fill and Stroke Module](https://www.w3.org/TR/fill-stroke-3/) allow SVG colors and fill patterns to be set from an external stylesheet, instead of setting attributes on each element. In this tutorial, we will use a simple plain hex color, but both fill and stroke properties also accept patterns, gradients and images as values.

**Note**: *When visiting the <a href="https://www.awwwards.com/">Awwwards</a> website, the animated note display can only be viewed with browser width set to 1024px or more.*

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5635753-ba37-4816-95ba-d08c8bd48473/demo.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5635753-ba37-4816-95ba-d08c8bd48473/demo.gif" width="800" alt="Note Display Project Demo" /></a><figcaption>A demo of the final result (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5635753-ba37-4816-95ba-d08c8bd48473/demo.gif">Large preview</a>)</figcaption></figure>

- 🕹 Demo: <a href="https://marina-ferreira.github.io/smashing-magazine-note-display-demo/">Note Display Project</a>
- 📂 Repo: <a href="https://github.com/marina-ferreira/smashing-magazine-note-display-demo">Note Display Repo</a>

{{% feature-panel %}}

## File Structure

Let’s start by creating the files in the terminal:

<pre><code class="language-bash">🌹  mkdir note-display
🌹  cd note-display
🌹  touch index.html styles.css scripts.js
</code></pre>

## HTML

Here is the initial template that links both `css` and `js` files:

<pre><code class="language-html">&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;

  &lt;title&gt;Note Display&lt;/title&gt;

  &lt;link rel="stylesheet" href="./styles.css"&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;script src="./scripts.js"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>

Each note element consists of a list item: `li` that holds the `circle`, the `note` value, and its `label`.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40ce656b-7171-4573-998f-c3f545842ffa/direct-children.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40ce656b-7171-4573-998f-c3f545842ffa/direct-children.jpg" sizes="100vw" caption="List item element and its direct children: <code>.circle</code>, <code>.percent</code> and <code>.label</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40ce656b-7171-4573-998f-c3f545842ffa/direct-children.jpg'>Large preview</a>)" alt="List item element and direct children" >}}

<p>The <code>.circle_svg</code> is an <a href="https://developer.mozilla.org/en-US/docs/Web/SVG">SVG</a> element, that wraps two <a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Element/circle">&lt;circle&gt;</a> elements. The first is the path to be filled while the second is the fill that will be animated.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa5b4850-91cb-498b-a32a-6d107eae2dac/svg-elements.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa5b4850-91cb-498b-a32a-6d107eae2dac/svg-elements.jpg" sizes="100vw" caption="SVG elements. SVG wrapper and circle tags. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa5b4850-91cb-498b-a32a-6d107eae2dac/svg-elements.jpg'>Large preview</a>)" alt="SVG elements" >}}

The `note` is separated into integer and decimals so different font sizes can be applied to them. The `label` is a simple `<span>`. So, putting all of this together looks like this:

<div class="break-out">

<pre><code class="language-html">&lt;li class="note-display"&gt;
  &lt;div class="circle"&gt;
    &lt;svg width="84" height="84" class="circle__svg"&gt;
      &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--path"&gt;&lt;/circle&gt;
      &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--fill"&gt;&lt;/circle&gt;
    &lt;/svg&gt;

    &lt;div class="percent"&gt;
      &lt;span class="percent__int"&gt;0.&lt;/span&gt;
      &lt;span class="percent__dec"&gt;00&lt;/span&gt;
    &lt;/div&gt;
  &lt;/div&gt;

  &lt;span class="label"&gt;Transparent&lt;/span&gt;
&lt;/li&gt;
</code></pre></div>

The `cx` and `cy` attributes define the circle’s x-axis and y-axis center point. The `r` attribute defines its radius.

You have probably noticed the underscore/dash pattern in classes names. That’s <a href="https://getbem.com/naming/">BEM</a>, which stands for `block`, `element` and `modifier`. It is a methodology that makes your element naming more structured, organized and semantic.

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2018/06/bem-for-beginners/">An Explanation Of BEM And Why You Need It</a></em></p>

To finish the template structures, let’s wrap the four list items in an unordered list element:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0010cf6e-569f-4ea4-9b96-5e9fc6f836f8/note-display-ul.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0010cf6e-569f-4ea4-9b96-5e9fc6f836f8/note-display-ul.jpg" sizes="100vw" caption="Unordered list wrapper holds four <code>li</code> children (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0010cf6e-569f-4ea4-9b96-5e9fc6f836f8/note-display-ul.jpg'>Large preview</a>)" alt="Unordered list wrapper" >}}

<div class="break-out">

<pre><code class="language-html">&lt;ul class="display-container"&gt;
  &lt;li class="note-display"&gt;
    &lt;div class="circle"&gt;
      &lt;svg width="84" height="84" class="circle__svg"&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--path"&gt;&lt;/circle&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--fill"&gt;&lt;/circle&gt;
      &lt;/svg&gt;

      &lt;div class="percent"&gt;
        &lt;span class="percent__int"&gt;0.&lt;/span&gt;
        &lt;span class="percent__dec"&gt;00&lt;/span&gt;
      &lt;/div&gt;
    &lt;/div&gt;

    &lt;span class="label"&gt;Transparent&lt;/span&gt;
  &lt;/li&gt;

  &lt;li class="note-display"&gt;
    &lt;div class="circle"&gt;
      &lt;svg width="84" height="84" class="circle__svg"&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--path"&gt;&lt;/circle&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--fill"&gt;&lt;/circle&gt;
      &lt;/svg&gt;

      &lt;div class="percent"&gt;
        &lt;span class="percent__int"&gt;0.&lt;/span&gt;
        &lt;span class="percent__dec"&gt;00&lt;/span&gt;
      &lt;/div&gt;
    &lt;/div&gt;

    &lt;span class="label"&gt;Reasonable&lt;/span&gt;
  &lt;/li&gt;

  &lt;li class="note-display"&gt;
    &lt;div class="circle"&gt;
      &lt;svg width="84" height="84" class="circle__svg"&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--path"&gt;&lt;/circle&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--fill"&gt;&lt;/circle&gt;
      &lt;/svg&gt;

      &lt;div class="percent"&gt;
        &lt;span class="percent__int"&gt;0.&lt;/span&gt;
        &lt;span class="percent__dec"&gt;00&lt;/span&gt;
      &lt;/div&gt;
    &lt;/div&gt;

    &lt;span class="label"&gt;Usable&lt;/span&gt;
  &lt;/li&gt;

  &lt;li class="note-display"&gt;
    &lt;div class="circle"&gt;
      &lt;svg width="84" height="84" class="circle__svg"&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--path"&gt;&lt;/circle&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--fill"&gt;&lt;/circle&gt;
      &lt;/svg&gt;

      &lt;div class="percent"&gt;
        &lt;span class="percent__int"&gt;0.&lt;/span&gt;
        &lt;span class="percent__dec"&gt;00&lt;/span&gt;
      &lt;/div&gt;
    &lt;/div&gt;

    &lt;span class="label"&gt;Exemplary&lt;/span&gt;
  &lt;/li&gt;
&lt;/ul&gt;
</code></pre></div>

You must be asking yourself what the labels `Transparent`, `Reasonable`, `Usable` and `Exemplary` mean. The more acquainted you get with programming, you will realize that writing code is not only about making the application functional, but also assuring that it will be long-term maintainable and scalable. That is only achieved if your code is easy to change.

<blockquote>“The acronym <code>TRUE</code> should help decide if the code you write will be able to accommodate change in the future or not.”</blockquote>

So, next time, ask yourself:

- `Transparent`:  Are code changes consequences clear?
- `Reasonable`: Is cost benefit worth it?
- `Usable`: Will I be able to reuse it in unexpected scenarios?
- `Exemplary`: Does it present high quality as an example for future code?

**Note**: *“[Practical Object-Oriented Design in Ruby](https://g.co/kgs/TnBTNp)” by Sandi Metz explains `TRUE` along with other principles and how to achieve those through design patterns. If you haven’t taken some time to study design patterns yet, consider adding this book to your bedtime reading.*

{{% ad-panel-leaderboard %}}

## CSS

Let’s import the fonts and apply a reset to all items:

<div class="break-out">

<pre><code class="language-css">
@import url('https://fonts.googleapis.com/css?family=Nixie+One|Raleway:200');

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
</code></pre></div>

The `box-sizing: border-box` property includes padding and border values into an element’s total width and height, so it’s easier to calculate its dimensions.

**Note**: *For a visual explanation on `box-sizing`, please read “<a href="https://medium.com/swlh/make-your-life-easier-with-css-box-sizing-3b6b2578bccd">Make Your Life Easier With CSS Box Sizing</a>.”*

<pre><code class="language-css">body {
  height: 100vh;
  color: #fff;
  display: flex;
  background: #3E423A;
  font-family: 'Nixie One', cursive;
}

.display-container {
  margin: auto;
  display: flex;
}
</code></pre>

By combining the rules `display: flex` in the `body` and `margin-auto` in the `.display-container`, it’s possible to center the child element both vertically and horizontally. The `.display-container` element will also be a `flex-container`; that way, its children will be placed in the same row along the main axis.

The `.note-display` list item will also be a `flex-container`. Since there are many children for centering, let’s do it through the `justify-content` and `align-items` properties. All `flex-items` will be centered along the `cross` and `main` axis. If you’re not sure what those are, check out the alignment section at “<a href="https://medium.com/swlh/css-flexbox-fundamentals-visual-guide-1c467f480dac">CSS Flexbox Fundamentals Visual Guide</a>.”

<pre><code class="language-css">.note-display {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0 25px;
}
</code></pre>

Let’s apply a <a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/stroke">stroke</a> to the circles by setting the rules `stroke-width`, `stroke-opacity` and `stroke-linecap` that altogether style the stroke live ends. Next, let’s add a color to each circle:

<div class="break-out">

<pre><code class="language-css">.circle__progress {
  fill: none;
  stroke-width: 3;
  stroke-opacity: 0.3;
  stroke-linecap: round;
}

.note-display:nth-child(1) .circle__progress { stroke: #AAFF00; }
.note-display:nth-child(2) .circle__progress { stroke: #FF00AA; }
.note-display:nth-child(3) .circle__progress { stroke: #AA00FF; }
.note-display:nth-child(4) .circle__progress { stroke: #00AAFF; }
</code></pre></div>

In order to position the `percent` element absolutely, it’s necessary to know absolutely to what. The `.circle` element should be the reference, so let’s add `position: relative` to it.

**Note**: *For a deeper, visual explanation on absolute positioning, please read “[How To Understand CSS Position Absolute Once And For All](https://medium.freecodecamp.org/how-to-understand-css-position-absolute-once-and-for-all-b71ca10cd3fd).”*

Another way of centering elements is to combine `top: 50%`, `left: 50%` and `transform: translate(-50%, -50%);` which position the element’s center at its parent’s center.

<pre><code class="language-css">.circle {
  position: relative;
}

.percent {
  width: 100%;
  top: 50%;
  left: 50%;
  position: absolute;
  font-weight: bold;
  text-align: center;
  line-height: 28px;
  transform: translate(-50%, -50%);
}

.percent__int { font-size: 28px; }
.percent__dec { font-size: 12px; }

.label {
  font-family: 'Raleway', serif;
  font-size: 14px;
  text-transform: uppercase;
  margin-top: 15px;
}
</code></pre>

By now, the template should be looking like this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5538b933-8d87-4609-bd37-9fa9fb4321a9/note-display-template.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5538b933-8d87-4609-bd37-9fa9fb4321a9/note-display-template.jpg" sizes="100vw" caption="Finished template elements and styles (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5538b933-8d87-4609-bd37-9fa9fb4321a9/note-display-template.jpg'>Large preview</a>)" alt="Finished initial template" >}}

## Fill Transition

The circle animation can be created with the help of two circle SVG properties: [`stroke-dasharray`](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/stroke-dasharray) and [`stroke-dashoffset`](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/stroke-dashoffset).

<blockquote>“<code>stroke-dasharray</code> defines the dash-gap pattern in a stroke.”</blockquote>

It can take up to four values:

- When it’s set to an only integer (`stroke-dasharray: 10`), dashes and gaps have the same size;
- For two values (`stroke-dasharray: 10 5`), the first is applied to dashes, second to gaps;
- The third and forth forms (`stroke-dasharray: 10 5 2` and `stroke-dasharray: 10 5 2 3`) will generate dashes and gaps in various sizes.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87b50f18-b9b2-47bb-b88b-519662900d51/dasharray-animation.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87b50f18-b9b2-47bb-b88b-519662900d51/dasharray-animation.gif" width="800" alt="Stroke dasharray property values" /></a><figcaption><code>stroke-dasharray</code> property values (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87b50f18-b9b2-47bb-b88b-519662900d51/dasharray-animation.gif">Large preview</a>)</figcaption></figure>

The image to the left shows the property `stroke-dasharray` being set from 0 to 238px, which is the circle circumference length.

The second image represents the `stroke-dashoffset` property that offsets the beginning of the dash array. It is also set from 0 to the circle circumference length.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e2ad1cc-d1f8-4143-97d3-5e401208d750/stroke-properties.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e2ad1cc-d1f8-4143-97d3-5e401208d750/stroke-properties.gif" width="800" alt="Stroke dasharray and dashoffset properties" /></a><figcaption><code>stroke-dasharray</code> and <cod>stroke-dashoffset</cod> properties (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e2ad1cc-d1f8-4143-97d3-5e401208d750/stroke-properties.gif">Large preview</a>)</figcaption></figure>

To produce the filling effect, we will set the `stroke-dasharray` to the circumference length, so that all of its length gets filled with a big dash and no gap. We’ll also offset it by the same value, so it gets “hidden”. Then the `stroke-dashoffset` will be updated to the corresponding note value, filling the stroke accordingly to the transition duration.

{{% ad-panel-leaderboard %}}

The properties updating will be done in the scripts through [CSS Variables](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables). Let’s declare the variables and set the properties:

<div class="break-out">

<pre><code class="language-css">.circle__progress--fill {
  --initialStroke: 0;
  --transitionDuration: 0;
  stroke-opacity: 1;
  stroke-dasharray: var(--initialStroke);
  stroke-dashoffset: var(--initialStroke);
  transition: stroke-dashoffset var(--transitionDuration) ease;
}
</code></pre></div>

In order to set the initial value and update the variables, let’s start by selecting all `.note-display` elements with [`document.querySelectorAll`](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll). The `transitionDuration` will be set to `900` milliseconds.

Then, we iterate through the displays array, select its `.circle__progress.circle__progress--fill` and extract the `r` attribute set in the HTML to calculate the circumference length. With that, we can set the initial `--dasharray` and `--dashoffset` values.

The animation will occur when the `--dashoffset` variable gets updated by a 100ms setTimeout:

<div class="break-out">

<pre><code class="language-javascript">const displays = document.querySelectorAll('.note-display');
const transitionDuration = 900;

displays.forEach(display => {
  let progress = display.querySelector('.circle__progress--fill');
  let radius = progress.r.baseVal.value;
  let circumference = 2 * Math.PI * radius;

  progress.style.setProperty('--transitionDuration', `${transitionDuration}ms`);
  progress.style.setProperty('--initialStroke', circumference);

  setTimeout(() => progress.style.strokeDashoffset = 50, 100);
});
</code></pre></div>

To get the transition starting from the top, the  `.circle__svg` element has to be rotated:

<pre><code class="language-css">.circle__svg {
  transform: rotate(-90deg);
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9823b0f4-4e9e-4476-a75c-b12a6c235d7c/fill-animation.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9823b0f4-4e9e-4476-a75c-b12a6c235d7c/fill-animation.gif" width="800" alt="Stroke properties transition" /></a><figcaption>Stroke properties transition (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9823b0f4-4e9e-4476-a75c-b12a6c235d7c/fill-animation.gif">Large preview</a>)</figcaption></figure>

<p>Now, let’s calculate the <code>dashoffset</code> value &mdash; relative to the note. The note value will be inserted to each <code>li</code> item through the <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/data-*">data-&#42;</a> attribute. The <code>&#42;</code> can be switched for any name that suits your needs and it can then, be retrieved in JavaScript through the element’s dataset: <code>element.dataset.*</code>.</p>

<p><strong>Note</strong>: <em> You can read more about the data-&#42; attribute on <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/data-*">MDN Web Docs</a>.</em></p>

<p>Our attribute will be called “<code>data-note</code>”:</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;ul class="display-container"&gt;
+ &lt;li class="note-display" data-note="7.50"&gt;
    &lt;div class="circle"&gt;
      &lt;svg width="84" height="84" class="circle__svg"&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--path"&gt;&lt;/circle&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--fill"&gt;&lt;/circle&gt;
      &lt;/svg&gt;

      &lt;div class="percent"&gt;
        &lt;span class="percent__int"&gt;0.&lt;/span&gt;
        &lt;span class="percent__dec"&gt;00&lt;/span&gt;
      &lt;/div&gt;
    &lt;/div&gt;

    &lt;span class="label"&gt;Transparent&lt;/span&gt;
  &lt;/li&gt;

+ &lt;li class="note-display" data-note="9.27"&gt;
    &lt;div class="circle"&gt;
      &lt;svg width="84" height="84" class="circle__svg"&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--path"&gt;&lt;/circle&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--fill"&gt;&lt;/circle&gt;
      &lt;/svg&gt;

      &lt;div class="percent"&gt;
        &lt;span class="percent__int"&gt;0.&lt;/span&gt;
        &lt;span class="percent__dec"&gt;00&lt;/span&gt;
      &lt;/div&gt;
    &lt;/div&gt;

    &lt;span class="label"&gt;Reasonable&lt;/span&gt;
  &lt;/li&gt;

+ &lt;li class="note-display" data-note="6.93"&gt;
    &lt;div class="circle"&gt;
      &lt;svg width="84" height="84" class="circle__svg"&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--path"&gt;&lt;/circle&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--fill"&gt;&lt;/circle&gt;
      &lt;/svg&gt;

      &lt;div class="percent"&gt;
        &lt;span class="percent__int"&gt;0.&lt;/span&gt;
        &lt;span class="percent__dec"&gt;00&lt;/span&gt;
      &lt;/div&gt;
    &lt;/div&gt;

    &lt;span class="label"&gt;Usable&lt;/span&gt;
  &lt;/li&gt;

+ &lt;li class="note-display" data-note="8.72"&gt;
    &lt;div class="circle"&gt;
      &lt;svg width="84" height="84" class="circle__svg"&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--path"&gt;&lt;/circle&gt;
        &lt;circle cx="41" cy="41" r="38" class="circle__progress circle__progress--fill"&gt;&lt;/circle&gt;
      &lt;/svg&gt;

      &lt;div class="percent"&gt;
        &lt;span class="percent__int"&gt;0.&lt;/span&gt;
        &lt;span class="percent__dec"&gt;00&lt;/span&gt;
      &lt;/div&gt;
    &lt;/div&gt;

    &lt;span class="label"&gt;Exemplary&lt;/span&gt;
  &lt;/li&gt;
&lt;/ul&gt;
</code></pre></div> 

The [`parseFloat`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseFloat) method will convert the string returned by `display.dataset.note` into a floating point number. The `offset` represents the percentage missing to reach the maximum score. So, for a `7.50` note, we would have `(10 - 7.50) / 10 = 0.25`, which means the `circumference` length should be offset by `25%` of its value:

<pre><code class="language-javascript">let note = parseFloat(display.dataset.note);
let offset = circumference * (10 - note) / 10;
</code></pre>

Updating the `scripts.js`:

<div class="break-out">

<pre><code class="language-javascript">const displays = document.querySelectorAll('.note-display');
const transitionDuration = 900;

displays.forEach(display => {
  let progress = display.querySelector('.circle__progress--fill');
  let radius = progress.r.baseVal.value;
  let circumference = 2 * Math.PI * radius;
+ let note = parseFloat(display.dataset.note);
+ let offset = circumference * (10 - note) / 10;

  progress.style.setProperty('--initialStroke', circumference);
  progress.style.setProperty('--transitionDuration', `${transitionDuration}ms`);

+ setTimeout(() => progress.style.strokeDashoffset = offset, 100);
});
</code></pre></div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/894e4046-1c16-4168-8989-9f4bd1fedaaa/fill-to-percent-animation.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/894e4046-1c16-4168-8989-9f4bd1fedaaa/fill-to-percent-animation.gif" width="800" alt="Stroke properties transition up to note value" /></a><figcaption>Stroke properties transition up to note value (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/894e4046-1c16-4168-8989-9f4bd1fedaaa/fill-to-percent-animation.gif">Large preview</a>)</figcaption></figure>

Before we move on, let’s extract the stoke transition to its own method:

<div class="break-out">

<pre><code class="language-javascript">const displays = document.querySelectorAll('.note-display');
const transitionDuration = 900;

displays.forEach(display => {
- let progress = display.querySelector('.circle__progress--fill');
- let radius = progress.r.baseVal.value;
- let circumference = 2 * Math.PI * radius;
  let note = parseFloat(display.dataset.note);
- let offset = circumference * (10 - note) / 10;

- progress.style.setProperty('--initialStroke', circumference);
- progress.style.setProperty('--transitionDuration', `${transitionDuration}ms`);

- setTimeout(() => progress.style.strokeDashoffset = offset, 100);

+ strokeTransition(display, note);
});

+ function strokeTransition(display, note) {
+   let progress = display.querySelector('.circle__progress--fill');
+   let radius = progress.r.baseVal.value;
+   let circumference = 2 * Math.PI * radius;
+   let offset = circumference * (10 - note) / 10;

+   progress.style.setProperty('--initialStroke', circumference);
+   progress.style.setProperty('--transitionDuration', `${transitionDuration}ms`);

+   setTimeout(() => progress.style.strokeDashoffset = offset, 100);
+ }
</code></pre></div>

## Note Value Increase

There is still the note transition from `0.00` to the note value to be built. The first thing to do is to separate the integer and decimal values. We will use the string method [`split()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) (it takes an argument that determines where the string will be broken and returns an array containing both broken strings). Those will be converted to numbers and passed as arguments to the `increaseNumber()` function, along with the `display` element and a flag indicating if its an integer or a decimal.

<div class="break-out">

<pre><code class="language-javascript">const displays = document.querySelectorAll('.note-display');
const transitionDuration = 900;

displays.forEach(display => {
  let note = parseFloat(display.dataset.note);
+ let [int, dec] = display.dataset.note.split('.');
+ [int, dec] = [Number(int), Number(dec)];

  strokeTransition(display, note);

+ increaseNumber(display, int, 'int');
+ increaseNumber(display, dec, 'dec');
});
</code></pre></div>

In the `increaseNumber()` function, we select either the `.percent__int` or `.percent__dec` element, depending on the `className`, and also in case the output should contain a decimal point or not. We’ve set our `transitionDuration` to `900ms`. Now, to animate a number from 0 to 7, for example, the duration has to be divided by the note `900 / 7 = 128.57ms`. The result represents how long each increase iteration will take. This means our `setInterval` will fire every `128.57ms`.

With those variables set, let’s define the [`setInterval`](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setInterval). The `counter` variable will be appended to the element as text and increased on each iteration:

<div class="break-out">

<pre><code class="language-javascript">function increaseNumber(display, number, className) {
  let element = display.querySelector(`.percent__${className}`),
      decPoint = className === 'int' ? '.' : '',
      interval = transitionDuration / number,
      counter = 0;

  let increaseInterval = setInterval(() => {
    element.textContent = counter + decPoint;
    counter++;
  }, interval);
}
</code></pre></div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c625f9f1-6d5c-4645-93cc-bb09d95905b3/infinite-counter-animation.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c625f9f1-6d5c-4645-93cc-bb09d95905b3/infinite-counter-animation.gif" width="800" alt="Infinite counter increase" /></a><figcaption>Infinite counter increase (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c625f9f1-6d5c-4645-93cc-bb09d95905b3/infinite-counter-animation.gif">Large preview</a>)</figcaption></figure>

Cool! It does increase the values, but it kind of does it forever. We need to clear the `setInterval` when the notes achieve the value we want. That is done with [`clearInterval`](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/clearInterval) function:

<div class="break-out">

<pre><code class="language-javascript">function increaseNumber(display, number, className) {
  let element = display.querySelector(`.percent__${className}`),
      decPoint = className === 'int' ? '.' : '',
      interval = transitionDuration / number,
      counter = 0;

  let increaseInterval = setInterval(() => {
+   if (counter === number) { window.clearInterval(increaseInterval); }

    element.textContent = counter + decPoint;
    counter++;
  }, interval);
}
</code></pre></div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6445706-49ad-4f26-b99e-ad2a9bf030d9/finished-project.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6445706-49ad-4f26-b99e-ad2a9bf030d9/finished-project.gif" width="800" alt="Finished note display project" /></a><figcaption>Finished project (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6445706-49ad-4f26-b99e-ad2a9bf030d9/finished-project.gif">Large preview</a>)</figcaption></figure>

Now the number is updated up to the note value and cleared with `clearInterval()` function.

That’s pretty much it for this tutorial. I hope you enjoyed it!

If you feel like building something a bit more interactive, check out my [Memory Game Tutorial](https://medium.freecodecamp.org/vanilla-javascript-tutorial-build-a-memory-game-in-30-minutes-e542c4447eae) created with Vanilla JavaScript. It covers basic HTML5, CSS3 and JavaScript concepts such as positioning, perspective, transitions, Flexbox, event handling, timeouts and ternaries.

Happy coding! 🌹

{{< signature "dm, ra, il" >}}

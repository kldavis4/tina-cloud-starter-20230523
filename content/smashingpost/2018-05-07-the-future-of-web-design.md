---
title: 'New CSS Features That Are Changing Web Design'
slug: future-of-web-design
author: zellliew
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2b60894-b7dd-41ac-94dd-b87a6bdf3cbc/future-web-design-beyonce.png
date: 2018-05-07T12:30:10+02:00
summary: >-
  Today, the design landscape has changed completely. We’re equipped with new and powerful tools — CSS Grid, CSS custom properties, CSS shapes and CSS writing-mode, to name a few — that we can use to exercise our creativity. Zell Liew explains how.
description: >-
  Today, the design landscape has changed completely. We’re equipped with new and powerful tools — CSS Grid, CSS custom properties, CSS shapes and CSS writing-mode, to name a few — that we can use to exercise our creativity. Zell Liew explains how.
categories:
  - CSS
  - JavaScript
  - Responsive Design
---
There was a time when web design got monotonous. Designers and developers built the same kinds of websites over and over again, so much so that we were mocked by people in our own industry for creating only two kinds of websites:

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">which one of the two possible websites are you currently designing? <a href="https://t.co/ZD0uRGTqqm">pic.twitter.com/ZD0uRGTqqm</a></p>&mdash; Jon Gold (@jongold) <a href="https://twitter.com/jongold/status/694591217523363840?ref_src=twsrc%5Etfw">February 2, 2016</a></blockquote>
<script defer  src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Is this the limit of what our “creative” minds can achieve? This thought sent an incontrollable pang of sadness into my heart.

I don't want to admit it, but maybe that was the best we could accomplish back then. Maybe we didn't have suitable tools to make creative designs. The demands of the web were evolving quickly, but we were stuck with ancient techniques like floats and tables.

Today, the design landscape has changed completely. We're equipped with new and powerful tools &mdash; CSS Grid, CSS custom properties, CSS shapes and CSS `writing-mode`, to name a few &mdash; that we can use to exercise our creativity.

{{% feature-panel %}}

## How CSS Grid Changed Everything

Grids are essential for web design; you already knew that. But have you stopped to asked yourself how you designed the grid you mainly use?

Most of us haven't. We use the 12-column grid that has became a standard in our industry.

- But why do we use the same grid?
- Why are grids made of 12 columns?
- Why are our grids sized equally?

Here's one possible answer to why we use the same grid: **We don't want to do the math**.

In the past, with float-based grids, to create a three-column grid, you needed to calculate the width of each column, the size of each gutter, and how to position each grid item. Then, you needed to create classes in the HTML to style them appropriately. It was [quite complicated](https://zellwk.com/blog/responsive-grid-system/).

To make things easier, we adopted grid frameworks. In the beginning, frameworks such as [960gs](https://960.gs) and [1440px](https://1440px.com) allowed us to choose between 8-, 9-, 12- and even 16-column grids. Later, Bootstrap won the frameworks war. Because Bootstrap allowed only 12 columns, and changing that was a pain, we eventually settled on 12 columns as the standard.

But we shouldn't blame Bootstrap. It was the best approach back then. Who wouldn't want a good solution that works with minimal effort? With the grid problem settled, we turned our attention to other aspects of design, such as typography, color and accessibility.

Now, with the **advent of CSS Grid, grids have become much simpler**. We no longer have to fear grid math. It’s become so simple that I would argue that creating a grid is easier with CSS than in a design tool such as Sketch!

Why?

Let's say you want to make a 4-column grid, each column sized at 100 pixels. With CSS Grid, you can write `100px` four times in the `grid-template-columns` declaration, and a 4-column grid will be created.

<pre><code class="language-css">.grid {
  display: grid;
  grid-template-columns: 100px 100px 100px 100px;
  grid-column-gap: 20px;
}
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9287f25c-75f8-456b-9f22-b3190802d543/future-web-design-grid-four.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9287f25c-75f8-456b-9f22-b3190802d543/future-web-design-grid-four.png" sizes="100vw" caption="You can create four grid columns by specifying a column-width four times in <code>grid-template-columns</code>" alt="Screenshot of Firefox's grid inspector that shows four columns." >}}

If you want a 12-column grid, you just have to repeat `100px` 12 times.

<div class="break-out">

<pre><code class="language-css">.grid {
  display: grid;
  grid-template-columns: 100px 100px 100px 100px 100px 100px 100px 100px 100px 100px 100px 100px;
  grid-column-gap: 20px;
}
</code></pre></div>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61ab598a-9c0d-4d81-a624-3fbca4dfb6b2/future-web-design-grid-twelve.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61ab598a-9c0d-4d81-a624-3fbca4dfb6b2/future-web-design-grid-twelve.png" sizes="100vw" caption="Creating 12 columns with CSS Grid" alt="Screenshot of Firefox's grid inspector that shows twelve columns." >}}

Yes, the code isn't beautiful, but we're not concerned with optimizing for code quality (yet) &mdash; we're still thinking about design. CSS Grid makes it so easy for anyone &mdash; even a designer without coding knowledge &mdash; to create a grid on the web.

If you want to create grid columns with different widths, you just have to specify the desired width in your `grid-template-columns` declaration, and you're set.

<pre><code class="language-css">.grid {
  display: grid;
  grid-template-columns: 100px 162px 262px;
  grid-column-gap: 20px;
}
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6be83c78-9646-4c17-8d74-a3ffa55c13e1/future-web-design-grid-asym.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6be83c78-9646-4c17-8d74-a3ffa55c13e1/future-web-design-grid-asym.png" sizes="100vw" caption="Creating columns of different widths is easy as pie." alt="Screenshot of Firefox's grid inspector that shows three colums of different width." >}}

### Making Grids Responsive

No discussion about CSS Grid is complete without talking about the responsive aspect. There are several ways to make CSS Grid responsive. One way (probably the most popular way) is to use the `fr` unit. Another way is to change the number of columns with media queries.

`fr` is a flexible length that represents a fraction. When you use the `fr` unit, browsers divide up the open space and allocate the areas to columns based on the `fr` multiple. This means that to create four columns of equal size, you would write `1fr` four times.

<pre><code class="language-css">.grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-column-gap: 20px;
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f12ee9f9-e577-4e2a-8173-f8c6fddff213/future-web-design-grid-fr.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f12ee9f9-e577-4e2a-8173-f8c6fddff213/future-web-design-grid-fr.gif" width="1000" height="165" alt="GIF shows four columns created with the fr unit. These columns resize according to the available white space" /></a><figcaption>Grids created with the <code>fr</code> unit respect the maximum width of the grid. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f12ee9f9-e577-4e2a-8173-f8c6fddff213/future-web-design-grid-fr.gif">Large preview</a>)</figcaption></figure>

**Let's do some calculations to understand why four equal-sized columns are created**.

First, let's assume the total space available for the grid is `1260px`.

Before allocating width to each column, CSS Grid needs to know how much space is available (or leftover). Here, it subtracts `grip-gap` declarations from `1260px`. Since each gap `20px`, we're left with `1200px` for the available space. `(1260 - (20 * 3) = 1200)`.

Next, it adds up the `fr` multiples. In this case, we have four `1fr` multiples, so browsers divide `1200px` by four. Each column is thus `300px`. This is why we get four equal columns.

**However, grids created with the `fr` unit aren't always equal**!

When you use `fr`, you need to be aware that each `fr` unit is a fraction of the available (or leftover) space.

If you have an element that is wider than any of the columns created with the `fr` unit, the calculation needs to be done differently.

For example, the grid below has one large column and three small (but equal) columns even though it's created with `grid-template-columns: 1fr 1fr 1fr 1fr`.

{{< codepen height="480" theme_id="light" slug_hash="vjWQep" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/zellwk/pen/vjWQep/">CSS Grid `fr` unit demo 1</a> by Zell Liew (<a href="https://codepen.io/zellwk">@zellwk</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

After splitting `1200px` into four and allocating `300px` to each of the `1fr` columns, browsers realize that the first grid item contains an image that is `1000px`. Since `1000px` is larger than `300px`, browsers choose to allocate `1000px` to the first column instead.

That means, we need to recalculate leftover space.

The new leftover space is `1260px - 1000px - 20px * 3 = 200px`; this `200px` is then divided by three according to the amount of leftover fractions. Each fraction is then `66px`. Hopefully that explains why `fr` units do not always create equal-width columns.

If you want the `fr` unit to create equal-width columns everytime, you need to force it with `minmax(0, 1fr)`. For this specific example, you’ll also want to set the image’s `max-width` property to 100%.

{{< codepen height="480" theme_id="light" slug_hash="NMwEvo" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/zellwk/pen/mxyXOm/">CSS Grid `fr` unit demo 2</a> by Zell Liew (<a href="https://codepen.io/zellwk">@zellwk</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

**Note**: *Rachel Andrew has written an amazing [article](https://www.smashingmagazine.com/2018/01/understanding-sizing-css-layout/) on how different CSS values (min-content, max-content, fr, etc.) affect content sizes. It’s worth a read!*

### Unequal-Width Grids

To create grids with unequal widths, you simply vary the fr multiple. Below is a grid that follows the golden ratio, where the second column is 1.618 times of the first column, and the third column is 1.618 times of the second column.

<pre><code class="language-css">.grid {
  display: grid;
  grid-template-columns: 1fr 1.618fr 2.618fr;
  grid-column-gap: 1em;
}
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18f3c1ee-74f1-4bdc-b747-1019285f671b/future-web-design-grid-fr-asym.gif" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18f3c1ee-74f1-4bdc-b747-1019285f671b/future-web-design-grid-fr-asym.gif" sizes="100vw" caption="A three-column grid created with the golden ratio" alt="GIF shows a three-column grid created with the golden ratio. When the browser is resized, the columns resize accordingly." >}}

### Changing Grids At Different Breakpoints

If you want to change the grid at different breakpoints, you can declare a new grid within a media query.

<pre><code class="language-css">.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-column-gap: 1em;
}

@media (min-width: 30em) {
  .grid {
    grid-template-columns: 1fr 1fr 1fr 1fr;
  }
}
</code></pre>

Isn't it easy to create grids with CSS Grid? Earlier designers and developers would have killed for such a possibility.

### Height-Based Grids

It was impossible to make grids based on the height of a website previously because there wasn't a way for us to tell how tall the viewport was. Now, with viewport units, CSS Calc, and CSS Grid, we can even make grids based on viewport height.

In the demo below, I created grid squares based on the height of the browser.

{{< codepen height="480" theme_id="light" slug_hash="qoEYaL" default_tab="result" user="zellwk" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/zellwk/pen/qoEYaL/">Height based grid example</a> by Zell Liew (<a href="https://codepen.io/zellwk">@zellwk</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Jen Simmons has a great video that talks about [desgining for the fourth edge](https://www.youtube.com/watch?v=dQHtT47eH0M&feature=youtu.be) &mdash; with CSS Grid. I highly recommend you watch it.

### Grid Item Placement

Positioning grid items was a big pain in the past because you had to calculate the `margin-left` property.

Now, with CSS Grid, you can place grid items directly with CSS without the extra calculations.

<pre><code class="language-css">.grid-item {
  grid-column: 2; /* Put on the second column */
}
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf790516-2d0d-4078-aac0-6a1d9357a74b/future-web-design-grid-placement.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf790516-2d0d-4078-aac0-6a1d9357a74b/future-web-design-grid-placement.png" sizes="100vw" caption="Placing an item on the second column." alt="Screenshot of a grid item placed on the second column" >}}

You can even tell a grid item how many columns it should take up with the `span` keyword.

<pre><code class="language-css">.grid-item {
  /* Put in the second column, span 2 columns */
  grid-column: 2 / span 2;
}
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a66e3449-3bd9-40ff-8fe2-6116c0939d77/future-web-design-grid-placement-span.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a66e3449-3bd9-40ff-8fe2-6116c0939d77/future-web-design-grid-placement-span.png" sizes="100vw" caption="You can tell grid items the number of columns (or even rows) they should occupy with the <code>span</code> keyword" alt="Screenshot of a grid item that's placed on the second column. It spans two columns" >}}

### Inspirations

CSS Grid enables you to lay things out so easily that you can create a lot of variations of the same website quickly. One prime example is [Lynn Fisher's personal home page](https://lynnandtonic.com).

{{< vimeo id="267241410" >}}

If you'd like to find out more about what CSS Grid can do, check out [Jen Simmon's lab](https://labs.jensimmons.com), where she explores how to create different kinds of layouts with CSS Grid and other tools.

To learn more about CSS Grid, check out the following resources:

- [Master CSS Grid](https://mastercssgrid.com), Rachel Andrew and Jen Simmons
Video tutorials
- [Layout Land](https://www.youtube.com/channel/UC7TizprGknbDalbHplROtag), Jen Simmons
A series of videos about layout
- [CSS layout workshop](https://thecssworkshop.com), Rachel Andrew
A CSS layout course
- [Learn CSS Grid](https://learncssgrid.com), Jonathan Suh
A free course on CSS Grid.
- [Grid critters](https://geddski.teachable.com/p/gridcritters), Dave Geddes
A fun way to learn CSS Grid

## Designing With Irregular Shapes

We are used to creating rectangular layouts on the web because the CSS box model is a rectangle. Besides rectangles, we’ve also found ways to create simple shapes, such as triangles and circles.

Today, we don't need to stop there. With CSS shapes and `clip-path` at our disposal, we can create irregular shapes without much effort.

For example, [Aysha Anggraini](https://twitter.com/RenettaRenula) experimented with a comic-strip-inspired layout with CSS Grid and `clip path`.

{{< codepen height="480" theme_id="light" slug_hash="LzLXYJ" default_tab="result" user="rrenula" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rrenula/pen/LzLXYJ/">Comic-book-style layout with CSS Grid</a> by Aysha Anggraini (<a href="https://codepen.io/rrenula">@rrenula</a>) on <a href="https://codepen.io">CodePen</a>. {{< /codepen >}}

[Hui Jing](https://twitter.com/hj_chen) explains how to use CSS shapes in a way that [allows text to flow](https://www.chenhuijing.com/blog/why-you-should-be-excited-about-css-shapes/) along the Beyoncé curve.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2b60894-b7dd-41ac-94dd-b87a6bdf3cbc/future-web-design-beyonce.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2b60894-b7dd-41ac-94dd-b87a6bdf3cbc/future-web-design-beyonce.png" sizes="100vw" caption="Text can flow around Beyoncé if you wanted it to!" alt="An image of Huijing's article, where text flows around Beyoncé." >}}

If you'd like to dig deeper, [Sara Soueidan](https://twitter.com/SaraSoueidan) has an article to help you [create non-rectangular layouts](https://www.sarasoueidan.com/blog/css-shapes/).

CSS shapes and `clip-path` give you infinite possibilities to create custom shapes unique to your designs. Unfortunately, syntax-wise, CSS shapes and `clip-path` aren't as intuitive as CSS Grid. Luckily, we have tools such as [Clippy](https://bennettfeely.com/clippy/) and [Firefox's Shape Path Editor](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Edit_CSS_shapes) to help us create the shapes we want.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c101607-4aac-4fa9-a968-62a33133331c/future-web-design-clippy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c101607-4aac-4fa9-a968-62a33133331c/future-web-design-clippy.png" sizes="100vw" caption="Clippy helps you create custom shapes easily with <code>clip-path</code>." alt="Image of Clippy, a tool to help you create custom CSS shapes" >}}

## Switching Text Flow With CSS’ `writing-mode`

We're used to seeing words flow from left to right on the web because the web is predominantly made for English-speaking folks (at least that's how it started).

But some languages don't flow in that direction. For example, Chinese words can read top down and right to left.

CSS’ `writing-mode` makes text flow in the direction native to each language. Hui Jing experimented with a Chinese-based layout that flows top down and right to left on a website called [Penang Hokkien](https://penang-hokkien.gitlab.io). You can read more about her experiment in her article, “[The One About Home](https://www.chenhuijing.com/blog/the-one-about-home/#🏀)”.

Besides articles, Hui Jing has a great talk on typography and `writing-mode`, “[When East Meets West: Web Typography and How It Can Inspire Modern Layouts](https://www.youtube.com/watch?v=Tqxo269aORM)”. I highly encourage you to watch it.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f69df2b-18d2-4da4-8e44-22226ef0becd/future-web-design-penang-hokkien.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f69df2b-18d2-4da4-8e44-22226ef0becd/future-web-design-penang-hokkien.png" sizes="100vw" caption="Penang Hokkien shows that Chinese text can be written from top to bottom, right to left." alt="An image of the Penang Hokken, showcasing text that reads from top to bottom and right to left." >}}

Even if you don't design for languages like Chinese, it doesn't mean you can't apply CSS’ `writing-mode` to English. Back in 2016, when I created [Devfest.asia](https://2016.devfest.asia/community/), I flexed a small creative muscle and opted to rotate text with `writing-mode`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70acafa4-5454-4257-bbdd-3f5fe18d3696/future-web-design-devfest.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70acafa4-5454-4257-bbdd-3f5fe18d3696/future-web-design-devfest.png" sizes="100vw" caption="Tags were created by using writing mode and transforms." alt="An image that shows how I rotated text in a design I created for Devfest.asia" >}}

[Jen Simmons's lab](https://labs.jensimmons.com) contains many experiments with `writing-mode`, too. I highly recommend checking it out, too.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f024681-c86e-4009-89aa-1ff379e71e8a/future-web-design-lab.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f024681-c86e-4009-89aa-1ff379e71e8a/future-web-design-lab.png" sizes="100vw" caption="An image from Jen Simmon's lab that shows Jan Tschichold" alt="An image from Jen Simmon's lab that shows a design from Jan Tschichold." >}}

## Effort And Ingenuity Go A Long Way

Even though the new CSS tools are helpful, you don't need any of them to create unique websites. A little ingenuity and some effort go a long way.

For example, in [Super Silly Hackathon](https://supersillyhackathon.sg), [Cheeaun](https://twitter.com/cheeaun) rotates the entire website by -15 degrees and makes you look silly when reading the website.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e308a830-ba6a-431c-8e5d-c4128cad965a/future-web-design-supersilly.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e308a830-ba6a-431c-8e5d-c4128cad965a/future-web-design-supersilly.png" sizes="100vw" caption="Cheeaun makes sure you look silly if you want to enter Super Silly Hackathon." alt="A screenshot from Super Silly Hackthon, with text slightly rotated to the left" >}}

[Darin Senneff](https://twitter.com/dsenneff) made an [animated login avatar](https://codepen.io/dsenneff/full/2c3e5bc86b372d5424b00edaf4990173/) with some trigonometry and GSAP. Look at how cute the ape is and how it covers its eyes when you focus on the password field. Similar to the interactive login form, there’s also a really nice and [interactive calculator](https://appinstitute.com/just-eat-commission/) that helps estimating the amount of lost revenues when using external services such as JustEat!

{{< vimeo id="267239924" >}}

When I created the sales page for my course, [Learn JavaScript](https://learnjavascript.today), I added elements that make the JavaScript learner feel at home.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b66f918-dc6f-4da1-870e-aa6b5ea8029c/future-web-design-learnjavascript.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b66f918-dc6f-4da1-870e-aa6b5ea8029c/future-web-design-learnjavascript.png" sizes="100vw" caption="I used the <code>function</code> syntax to create course packages instead of writing about course packages" alt="Image where I used JavaScript elements in the design for Learn JavaScript." >}}

## Wrapping Up

A unique web design isn't just about layout. It's about how the design integrates with the content. With a little effort and ingenuity, all of us can create unique designs that speak to our audiences. The tools at our disposal today make our jobs easier.

The question is, do you care enough to make a unique design? I hope you do.

{{< signature "ra, il, al" >}}


---
title: 'The New Layout Standard For The Web: CSS Grid, Flexbox And Box Alignment'
slug: css-grids-flexbox-box-alignment-new-layout-standard
author: rachel-andrew
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ef65019-11a6-4199-9f36-ba30420df25a/flexbox-equal-height-columns-codepen-screenshot-opt.png
date: 2016-11-08T21:12:40.000Z
description: >-
  Editor’s note: Please note that this article is quite lengthy, and contains
  dozens of CodePen embeds for an interactive view. The page might take a little
  while to load, so please be patient.

  This article explains how Flexbox and CSS Grid fit together, and how we can
  build resilient and flexible layouts today while providing a decent fallback
  for older browsers.
categories:
  - CSS
  - Flexbox
  - CSS Grid
---
**Layout on the web is hard.** The reason it is so hard is that the layout methods we've relied on ever since using CSS for layout became possible were not really designed for complex layout. While we were able to achieve quite a lot in a fixed-width world with hacks such as faux columns, these methods fell apart with responsive design.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ef3d417-c5db-43dd-a988-b2713ce17ee6/01-susy-grid-opt.jpg" alt="01-susy-grid-opt" width="923" height="662" alt="css grid" title="CSS Grid – Flexbox And Box Alignment For Web Layout" loading="lazy" decoding="async" class="222550"  /></figure>

Thankfully, we have hope, in the form of flexbox — which many readers will already be using — CSS Grid Layout and the box alignment module.

In this article, I'm going to explain how these fit together, and you'll discover that by understanding flexbox you are very close to understanding much of grid layout.</p>

## New Values For Display

Both `grid` and `flexbox` are new values for the `display` property. To make an element a flex container, we use `display: flex`; to make it a grid container, we use `display: grid`.

{{% feature-panel %}}

As soon as we do so, the immediate children of our flex or grid container become flex or grid items. Those immediate children take on the initial values of flex or grid items.</p>

### display: flex

In the first example, we have three elements in a wrapper element set to `display: flex`. That's all we need to do to start using flexbox.

Unless we add the following properties with different values, the initial values for the flex container are:

*   `flex-direction: row`
*   `flex-wrap: no-wrap`
*   `align-items: stretch`
*   `justify-content: flex-start`

The initial values for our flex items are:

*   `flex-grow: 0`
*   `flex-shrink: 1`
*   `flex-basis: auto`

We'll look at how these properties and values work later in this article. For now, all you need to do is set `display: flex` on a parent, and flexbox will begin to work.</p>

<figure>{{< codepen  theme_id="0" slug_hash="ZOpOqB" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/ZOpOqB/'>Flexbox defaults</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

### display: grid

To lay out items on a grid, we use `display: grid`. In order that we can see the grid's behavior, this example has five cards to lay out.

Adding `display: grid` won't make a dramatic change; however, our child items are all now grid items. They have fallen into a single-column track grid, displaying one below the other, the grid creating implicit row tracks to hold each item.</p>

<figure>{{< codepen  theme_id="0" slug_hash="QEKGNm" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/QEKGNm/'>Grid defaults</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

We can take our grid a step further and make it more grid-like by creating some columns. We use the `grid-template-rows` property to do this.

In this next example, I've created three equal-width column tracks using a new unit that has been created for `grid`. The `fr` unit is a fraction unit signifying the fraction of available space this column should take up. You can see how our grid items have immediately laid themselves out on the grid, one in each created cell of our explicitly defined columns. The grid is still creating _implicit_ rows; as we fill up the available cells created by our columns, new rows are created to hold more items.</p>

<figure>{{< codepen  theme_id="0" slug_hash="LZRbRV" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/LZRbRV/'>Grid columns</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

Once again, we have some default behavior in evidence. We haven't positioned any of these grid items, but they are placing themselves onto our grid, one per cell of the grid. The initial values of the grid container are:

*   `grid-auto-flow: row`
*   `grid-auto-rows: auto`
*   `align-items: stretch`
*   `justify-items: stretch`
*   `grid-gap: 0`

These initial values mean that our grid items are placed one into each cell of the grid, working across the rows. Because we have a three-column track grid, after filling the grid cell of the third column, a new row is created for the rest of the items. This row is auto-sized, so will expand to fit the content. Items stretch in both directions, horizontal and vertical, filling the grid area.</p>

## Box Alignment

In both of these simple examples, we are already seeing values defined in the box alignment module in use. "Box Alignment Module Level 3" essentially takes all of the alignment and space distribution defined in flexbox and makes it available to other modules. So, if you already use flexbox, then you are already using box alignment.

Let's look at how box alignment works in flexbox and grid, and the problems that it helps us solve.</p>

### Equal-Height Columns

Something that was very easy to create with old-school table-based layouts, yet fiendishly difficult using positioning and floats, is equal-height columns. In the floated example below, our cards contain unequal amounts of content. We have no way of indicating to the other cards that they should visually take on the same height as the first card — they have no relationship to each other.</p>

<figure>{{< codepen  theme_id="0" slug_hash="YWGrPy" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/YWGrPy/'>Floated columns</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

As soon as we set the `display` property to `grid` or `flex` on a parent, we give the children a relationship to each other. That relationship enables the box-alignment properties to work, making equal-height columns simple.

In the flex example below, our items have unequal amounts of content. While the background on each lines up, it doesn't sit behind the content as it would for floated elements. Because these items are displayed in a row, the property that controls this behavior is `align-items`. Creating equal-height columns requires that the value be `stretch` — the initial value for this property.</p>

<figure>{{< codepen  theme_id="0" slug_hash="ZOpXEM" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/ZOpXEM/'>Flexbox equal-height columns</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

We see the same with grid layouts. Below is the simplest of grid layouts, two columns with a sidebar and main content. I'm using those fraction units again; the sidebar has 1 fraction of the available space, and the main content 3 fractions. The background color on the sidebar runs to the bottom of the content. Once again, the default value of `align-items` is `stretch`.</p>

<figure>{{< codepen  theme_id="0" slug_hash="GqjMJj" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/GqjMJj/'>Grid equal-height columns</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

### Alignment in Flexbox

We've seen how the default value of `align-items` for both `grid` and `flexbox` is `stretch`.

For flexbox, when we use `align-items`, we are aligning them inside the flex container, on the cross axis. The main axis is the one defined by the `flex-direction` property. In this first example, the main axis is the row; we are then stretching the items on the cross axis to the height of the flex container. The height of the flex container is, in this case, determined by the item with the most content.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93877106-6b52-4d83-a395-6a04fd6af1dd/01-flex-row-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddb7096e-5e8a-4db3-a079-5feff041fe38/01-flex-row-preview-650px-opt.png" alt="01-flex-row-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93877106-6b52-4d83-a395-6a04fd6af1dd/01-flex-row-opt.png">View large version</a>)</figcaption></figure>

I could give the wrapper a height, and in this case the height of the flex container would be defined by that height.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f987ed76-88ae-4b73-a9ab-4ccbe2e9fef9/02-flex-row-height-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b90748e0-65e1-40ad-81bf-579825da405c/02-flex-row-height-preview-650px-opt.png" alt="02-flex-row-height-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f987ed76-88ae-4b73-a9ab-4ccbe2e9fef9/02-flex-row-height-opt.png">View large version</a>)</figcaption></figure>

We can use other values, instead of the default `stretch`:

*   `flex-start`
*   `flex-end`
*   `baseline`
*   `stretch`

To control the alignment on the main axis, use the `justify-content` property. The default value is `flex-start`, which is why our items are all aligned against the left margin. We could instead use any of the following values:

*   `flex-start`
*   `flex-end`
*   `center`
*   `space-around`
*   `space-between`

The `space-between` and `space-around` keywords are especially interesting. With `space-between`, the space left over after the flex items have been displayed is distributed evenly between the items.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b52bdd9-1abd-4908-8077-95c7757f8da8/03-flex-space-between-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dbe3c19-0ee6-4f53-afd6-da2b5e3ec8a5/03-flex-space-between-preview-650px-opt.png" alt="03-flex-space-between-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b52bdd9-1abd-4908-8077-95c7757f8da8/03-flex-space-between-opt.png">View large version</a>)</figcaption></figure>

Using `space-around` is similar except that the space left over is distributed on both sides of the items. You get a half-sized gap on each end.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af341f9b-e1cb-4a19-ad57-002960f7d578/04-flex-space-around-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1089f9b8-b099-49d3-955f-771403c2c5b2/04-flex-space-around-preview-650px-opt.png" alt="04-flex-space-around-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af341f9b-e1cb-4a19-ad57-002960f7d578/04-flex-space-around-opt.png">View large version</a>)</figcaption></figure>

You can see these properties and values in the CodePen below.</p>

<figure>{{< codepen  theme_id="8287" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/32a53959ea2287ba69c130ff9872790b/'>Flexbox align and justify on a row</a> by Rachel (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

<figure>{{< codepen  theme_id="0" slug_hash="PzGJzm" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/PzGJzm/'>Flexbox alignment flex-direction: row</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

We can display flex items as a column rather than a row. If we change the value of `flex-direction` to `column`, then the main axis becomes the column, and the cross axis is along the row — `align-items` is still `stretch` by default, and so stretches the items across row-wise.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a57ed32f-36ea-440d-abd1-893ac27dc9dd/05-flex-column-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1c884e9-2ced-4030-bc2e-9c3b42061e34/05-flex-column-preview-650px-opt.png" alt="05-flex-column-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a57ed32f-36ea-440d-abd1-893ac27dc9dd/05-flex-column-opt.png">View large version</a>)</figcaption></figure>

If instead we want them to align to the start of the flex container, we use `flex-start`.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a7c0741-a6b2-4de1-a8a9-86c02c53b91c/06-flex-column-start-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dcad186-36f7-4681-94b9-443e2f907c75/06-flex-column-start-preview-650px-opt.png" alt="06-flex-column-start-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a7c0741-a6b2-4de1-a8a9-86c02c53b91c/06-flex-column-start-opt.png">View large version</a>)</figcaption></figure>

We can use `justify-items`, too, including `space-between` and `space-around`. The container needs to have enough height for you to see each in action, though!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bad794ea-7deb-47ae-9cd9-2a5894508c93/07-flex-column-space-between-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a09ee44b-8d46-4253-be0c-3113bb8ce764/07-flex-column-space-between-preview-650px-opt.png" alt="07-flex-column-space-between-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bad794ea-7deb-47ae-9cd9-2a5894508c93/07-flex-column-space-between-opt.png">View large version</a>)</figcaption></figure>

<figure>{{< codepen  theme_id="0" slug_hash="JKRrvY" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/JKRrvY/'>Flexbox alignment flex-direction: column</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

### Alignment in Grid Layout

In a grid layout, the behavior is similar, except that we are aligning items within the defined grid area. In flexbox, we talk about the main and cross axis; with grids, we use the terms "block" or "column axis" to describe the axis defining our columns, and "inline" or "row axis" to describe the axis defining our rows.

We can align content inside a grid area using the properties and values described in the box alignment specification.

A grid area is one or more grid cells. In the example below, we have a four-column and four-row track grid. The tracks are separated by a grid gap of 10 pixels, and I have created three grid areas using line-based positioning. We'll look at this positioning properly later in this guide, but the value before the `/` is the line that the content starts on, and the value after where it ends.</p>

<figure>{{< codepen  theme_id="0" slug_hash="EygpMv" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/EygpMv/'>Grid alignment: align-items and justify-items</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

The dotted border is on a background image, to help us see the defined areas. So, in the first example, each area uses the defaults of `stretch` for both `align-items` on the column axis and `justify-items` on the row axis. This means that the content stretches to completely fill the defined area.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a1a6d57-525e-40bf-8248-b59fa7485926/08-grid-default-align-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d324a09c-179e-43c6-83fa-a1a1ac17c25a/08-grid-default-align-preview-650px-opt.png" alt="08-grid-default-align-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a1a6d57-525e-40bf-8248-b59fa7485926/08-grid-default-align-opt.png">View large version</a>)</figcaption></figure>

In the second example, I have changed the value of `align-items` on the grid container to `center`. We can also change this value on an individual grid item using the `align-self` property. In this case, I have set all items to `center`, but item two to `stretch`.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab746eb9-e569-4286-b59a-9fc95b0938d2/09-grid-align-items-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a18cd5d-5c17-48d7-af02-4ec92512744f/09-grid-align-items-preview-650px-opt.png" alt="09-grid-align-items-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab746eb9-e569-4286-b59a-9fc95b0938d2/09-grid-align-items-opt.png">View large version</a>)</figcaption></figure>

In the third example, I have changed the value of `justify-items` and `justify-self` again, setting these to `center` and `stretch`.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75f7d0c0-3777-4f1d-8765-1e9e6cac9394/10-grid-justify-items-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b4a07d5-fb2d-43eb-9fe3-e758ace13ffa/10-grid-justify-items-preview-650px-opt.png" alt="10-grid-justify-items-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75f7d0c0-3777-4f1d-8765-1e9e6cac9394/10-grid-justify-items-opt.png">View large version</a>)</figcaption></figure>

In all of the examples above, I have aligned the content of the grid areas, the areas defined by the start and end grid lines.

We can also align the entire grid inside the container, if our grid tracks are sized so that they take up less space than the container that has been set to `display: grid`. In this case, we use the `align-content` and `justify-content` properties, as with flexbox.</p>

<figure>{{< codepen  theme_id="0" slug_hash="aZBozX" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/aZBozX/'>Grid alignment: aligning the grid</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

In the first example, we see the default alignment of a grid where the columns and rows have been defined in absolute units and take up less space than the fixed-sized wrapper allows for. The default values for both are `start`.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e92f32c4-0b80-4180-a163-86cff57407a4/11-grid-align-start-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f64b35ee-360b-4bd5-ad4b-1e5a3219da15/11-grid-align-start-preview-650px-opt.png" alt="11-grid-align-start-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e92f32c4-0b80-4180-a163-86cff57407a4/11-grid-align-start-opt.png">View large version</a>)</figcaption></figure>

To move the tracks to the bottom right, we change the values to `end`.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7cf15d6-154d-4014-8c87-aabe157b4329/12-grid-align-end-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad8460a1-b3ed-4f59-a8d2-de11e352006c/12-grid-align-end-preview-650px-opt.png" alt="12-grid-align-end-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7cf15d6-154d-4014-8c87-aabe157b4329/12-grid-align-end-opt.png">View large version</a>)</figcaption></figure>

Just as with flexbox, we can use `space-around` and `space-between`. This might cause some behavior that we don't want as the grid gaps essentially become wider. However, as you can see from the image below and in the third example in the CodePen, we get the same space between or around the tracks as we see with flexbox.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/468525a7-63b2-4e9c-a6ca-059cca50a42a/13-grid-align-space-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52a1692e-df2f-41c8-84b5-8cb15704c231/13-grid-align-space-preview-650px-opt.png" alt="13-grid-align-space-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/468525a7-63b2-4e9c-a6ca-059cca50a42a/13-grid-align-space-opt.png">View large version</a>)</figcaption></figure>

The fixed-sized tracks will gain additional space if they span more than one track. Element two and four in our example are wider and three is taller because they are given the extra space assigned to the gap they span over.

We can completely center the grid by setting both values to `center`, as shown in the last example.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b7be767-aa1d-4657-bfcf-518e52a65123/14-grid-align-center-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dea112c-8821-4360-be7a-2712e0f7622d/14-grid-align-center-preview-650px-opt.png" alt="14-grid-align-center-preview-650px-opt" width="6520" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b7be767-aa1d-4657-bfcf-518e52a65123/14-grid-align-center-opt.png">View large version</a>)</figcaption></figure>

We have very nice alignment abilities in both flexbox and grid, and they work in a generally consistent way. We can align individual items and groups of items in a way that is responsive and prevents overlap — something the web has lacked until now!

## Responsive By Default

In the last section, we looked at alignment. The box-alignment properties as used in grid and flexbox layouts are one area where we see how these specifications have emerged in a world where responsive design is just how things are done. Values such as `space-between`, `space-around` and `stretch` allow for responsiveness, distributing content equally among or between items.

There is more, however. Responsive design is often about maintaining proportion. When we calculate columns for a responsive design using the `target ÷ context` approach, we maintain the proportions of the original absolute-width design. Flexbox and grid layouts give us far simpler ways to deal with proportions in our designs.

Flexbox gives us a **content-out** approach to flexibility. We see this when we use a keyword value of `space-between` to space our items evenly. First, the amount of space taken up by our items is calculated, and then the remaining space in the container is divided up and used evenly to space out the items. We can get more control of content distribution by way of properties that we apply to the flex items themselves:

*   `flex-grow`
*   `flex-shrink`
*   `flex-basis`

These three properties are more usually described by the shorthand `flex` property. If we add `flex: 1 1 300px` to an item, we are stating that `flex-grow` should be `1` so that items can grow, `flex-shrink` should be `1` so that items can shrink, and the `flex-basis` should be 300 pixels. Applying this to our cards layout gives us the example below.</p>

<figure>{{< codepen  theme_id="0" slug_hash="gMLrEG" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/gMLrEG/'>Flexbox: flex properties</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

Our `flex-basis` here is 300 pixels, and we have three cards in a row. If the flex container is wider than 900 pixels, then the remaining space is divided into three and distributed between the items equally. This is because we have set `flex-grow` to `1` so that our items can grow from the `flex-basis`. We have also set `flex-shrink` to `1`, which means that, where we don't have space for three 300-pixel columns, space will be removed equally.

If we want these items to grow in different proportions, then we can change the `flex-grow` value on one or more items. If we would like the first item to get three times the available space distributed to it, we would set `flex-grow` to `3`.</p>

<figure>{{< codepen  theme_id="0" slug_hash="NrbNmz" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/NrbNmz/'>Flexbox: flex properties</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

The available space is distributed _after_ the amount needed for `flex-basis` has been taken into account. This is why our first item is not three times the size of our other items, but instead gets a share of three parts of the remaining space. You will see a bigger change by setting the value for `flex-basis` to `0`, in which case we wouldn't have a starting value to remove from the overall container. Then, the entire width of the container could be distributed in proportion to our items.</p>

<figure>{{< codepen  theme_id="0" slug_hash="jrVqoQ" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/jrVqoQ/'>Flexbox: flex properties</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

A very useful tool to help you understand these values is [Flexbox Tester](https://madebymike.com.au/demos/flexbox-tester/). Pop the different values into the tester, and it calculates the actual sizes at which your items will end up, and explains why they end up at that size.

If you use `auto` as your `flex-basis` value, it will use any size set on the flex item as the `flex-basis` value. If there is no size, then it defaults to be the same as the value of `content`, which is the content's width. Using `auto` is, therefore, very useful for reusable components that might need to have a set size on an item. You can use `auto` and be sure that if the item needs to be around a size defined on it, flexbox will respect it.

In the next example, I have set the `flex-basis` on all cards to `auto`. I then gave the first card a width of 350 pixels. So, the `flex-basis` of that first card is now 350 pixels, which is used to work out how to distribute space. The other two cards have a `flex-basis` based on their content's width.</p>

<figure>{{< codepen  theme_id="0" slug_hash="mEOPZM" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/mEOPZM/'>Flexbox: flex properties</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

If we go back to our original `flex: 1 1 300px`, add more items to our example and set `flex-wrap: wrap` on the container, the items will wrap in order to maintain as near as possible the `flex-basis` value. If we have five images and three fit onto one row, then the next two will wrap onto a new row. As the items are allowed to grow, they both grow equally, and so we get two equal-sized items on the bottom row and three in the row above.</p>

<figure>{{< codepen  theme_id="0" slug_hash="QEGNeZ" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/QEGNeZ/'>Flexbox: wrapping</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

The question then asked is often, "How can I get the items on the bottom row to line up with the ones on the top, leaving a gap at the end?" The answer is that you don't, not with flexbox. For that kind of behavior you need a grid layout.</p>

### Keeping Things in Proportion With Grid Layout

Grid layouts, as we have already seen, have a concept of creating column and row **tracks** into which items can be positioned. When we create a flexible grid layout, we set the proportions when defining the tracks on the grid container — rather than on the items, as with flexbox. We encountered the `fr` unit when we created our grids earlier. This unit works in a similar way to `flex-grow` when you have a `flex-basis` of `0`. It assigns a fraction of the available space in the grid container.

In this code example, the first column track has been given `2fr`, the other two `1fr`. So, we divide the space into four and assign two parts to the first track and one part each to the remaining two.</p>

<figure>{{< codepen  theme_id="0" slug_hash="xOROVO" default_tab="html,result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/xOROVO/'>Simple grid showing fraction units</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

Mixing absolute units and `fr` units is valid. In this next example, we have a `2fr` track, a `1fr` track and a 300-pixel track. First, the absolute width is taken away, and then the remaining space is divided into three and assigned three parts to track 1 and one part to track 2.</p>

<figure>{{< codepen  theme_id="0" slug_hash="rLWLLa" default_tab="html,result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/rLWLLa/'>Grid: Mixing absolute and  fraction units</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

What you can also see from this example is that our items fit into the defined tracks — they don't distribute across the row, as they do in the flexbox example. This is because, with grid layouts, we are creating a two-dimensional layout, then putting items into it. With flexbox, we get our content and work out how much will fit in a single dimension in a row or column, treating additional rows or columns as entirely new flex containers.

What would be nice, however, is to still have a way to create **as many columns of a certain size as will fit into the container**. We can do this with `grid` and the `repeat` syntax.

In the next example, I will use the `repeat` syntax to create as many 200-pixel columns as will fit in our container. I am using the `repeat` syntax for the track listing, with a keyword value of `auto-fill` and then the size that I want the repeated tracks to be.

(At the time of writing, this was not implemented in Chrome, but works in Firefox Developer Edition.)

<figure>{{< codepen  theme_id="0" slug_hash="Pzbzze" default_tab="html,result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/Pzbzze/'>Grid: As many 200-pixel tracks as will fit</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

We can go a step further than that and combine fraction units and an absolute width to tell the grid to create as many 200-pixel tracks as will fit in the container and to distribute the remainder equally.</p>

<figure>{{< codepen  theme_id="0" slug_hash="EyNyNK" default_tab="html,result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/EyNyNK/'>Grid: As many 200-pixel tracks as will fit, distributing remaining space evenly</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

In this way, we get the benefits of a two-dimensional layout but still have flexible quantities of tracks — all without using any media queries. What we also see here is the grid and flexbox specifications diverging. Where flexbox ends with distributing items in one dimension, grid is just getting started.</p>

### A Separation of Source Order and Visual Display

With flexbox, we can't do a lot in terms of positioning our flex items. We can choose the direction in which they flow, by setting `flex-direction` to `row`, `row-reverse` or `column`, `column-reverse`, and we can set an order, which controls the visual order in which the items display.</p>

<figure>{{< codepen  theme_id="0" slug_hash="YWpWVE" default_tab="result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/YWpWVE/'>Flexbox: order</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

With grid layouts, we get to properly position child items onto the grid we have defined. In most of the examples above, we have been relying on grid auto-placement, the rules that define how items we have not positioned are laid out. In the example below, I am using line-based positioning to position the items on the grid.

The `grid-column` and `grid-row` properties are a shorthand for `grid-column-start`, `grid-row-start`, `grid-column-end` and `grid-row-end`. The value before the `/` is the line that the content starts on, while the value after is the line it ends on.</p>

<figure>{{< codepen  theme_id="0" slug_hash="rLWLwO" default_tab="html,result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/rLWLwO/'>Grid: line-based positioning</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

You can also name your lines. This happens when you create your grid on the grid container. Name the lines in brackets, and then position the items as before but using the names instead of the line index.</p>

<figure>{{< codepen  theme_id="0" slug_hash="aZBZEB" default_tab="html,result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/aZBZEB/'>Grid: line-based positioning, named lines</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

You can have multiple lines with the same name, and then target them by line name and index.</p>

<figure></figure>

You can use a `span` keyword, spanning a number of lines or, for example, to the third line named `col`. This type of positioning is useful for creating components that sit in various places in the layout. In the example below, I want some elements to span six column tracks and others to span three. I am using auto-placement to lay out the items, but when the grid encounters an item with a class of `wide`, the start value will be `auto` and the end value will be `span 2`; so, it will start on the line it would normally start on based on the auto-placement rules, but span two lines.</p>

<figure>{{< codepen  theme_id="0" slug_hash="LZbZdj" default_tab="html,result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/LZbZdj/'>Grid: multiple lines with the same name</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

Using auto-placement with some rules in this way will likely leave some gaps in our grid as the grid encounters items that need two tracks and has space for only one. By default, the grid progresses forward; so, once it leaves a gap, it doesn't go back to place things in it — unless we set `grid-auto-flow` to a value of `dense`, in which case, the grid will actually backfill the gaps left, taking the content out of DOM order.</p>

<figure>{{< codepen  theme_id="0" slug_hash="beBeKJ" default_tab="html,result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/beBeKJ/'>Grid: grid-auto-flow: dense</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

There is also a whole different method of positioning items using the grid layout — by creating a visual representation of our layout right in the value of the `grid-template-areas` property. To do this, you first need to name each direct child of the grid container that you want to position.

We then lay the items out in this ASCII art manner as the value of `grid-template-areas`. If you wanted to entirely redefine the layout based on media queries, you could do so just by changing the value of this one property!

<figure>{{< codepen  theme_id="0" slug_hash="oLYLMo" default_tab="html,result" user="rachelandrew" >}}See the Pen <a href='https://codepen.io/rachelandrew/pen/oLYLMo/'>Grid: template areas</a> by rachelandrew (<a href='https://codepen.io/rachelandrew'>@rachelandrew</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

As you can see from the example, to leave a cell empty, we use a full stop or a series of full stops with no white space between them. To cause an element to span a number of tracks, we repeat the name.</p>

### Accessibility Implications of Reordering

For flexbox and even more so for grid layouts, we need to take great care when using these methods to reorder content. The specification for flexbox states:

<blockquote>
<p>Authors must use order only for visual, not logical, reordering of content. Style sheets that use order to perform logical reordering are non-conforming.</p>
</blockquote>

For grids, we are warned:

<blockquote>
<p>Grid layout gives authors great powers of rearrangement over the document. However, these are not a substitute for correct ordering of the document source. The order property and grid placement do not affect ordering in non-visual media (such as speech). Likewise, rearranging grid items visually does not affect the default traversal order of sequential navigation modes (such as cycling through links).</p>
</blockquote>

In both cases, as currently defined, the reordering is only visual. It does not change the logical order of the document. In addition, we need to take great care in considering sighted keyboard users. It would be incredibly simple to cause someone tabbing through the document to tab along the navigation at the top and then suddenly be taken to the bottom of the document due to a grid item that appears early in the source being positioned there.</p>

## A New System For CSS Grid Layout

I've not covered every aspect of Grid and Flexbox in this guide - my aim being to show the similarities and differences between the specifications, and to throw Box Alignment into the mix. To demonstrate that what these specifications are bringing us is a new layout system, one that understands the kind of sites and applications we are building today.

Do play with the examples in the article, and there is a whole host of other stuff detailed in the resources below. I would be especially interested in use cases that you can't achieve with these layout methods. If you find one let me know, I'm interested in finding the edges of the specifications we have so welcome a challenge.</p>

## Watch My Talk

{{< vimeo id="215091807" >}}

### Resources

Here are some resources to help you explore these specifications further.

*   [Grid by Example](https://gridbyexample.com), Rachel Andrew
*   "[Laying Out The Future With Grid And Flexbox](https://www.youtube.com/watch?v=ibeF6rbzD70)" (video), Rachel Andrew, Mozilla Hacks

{{< signature "ms, vf, ml, rb, al, il" >}}


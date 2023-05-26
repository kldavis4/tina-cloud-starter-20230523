---
title: 'Understanding CSS Grid: Grid Template Areas'
slug: understanding-css-grid-template-areas
author: rachel-andrew
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f7e40b8-3925-4241-8b3e-e9624e5c8a86/understanding-css-grid-template-areas.png
date: 2020-02-12T11:30:00.000Z
evergreen: true
last_updated: 2020-02-20T11:30:00.000Z
updated_by: rachel-andrew
summary: >-
  In a new series, Rachel Andrew breaks down the CSS Grid Layout specification. This time, we take a look at how to use <code>grid-template-areas</code> to place items.
description: >-
  In a new series, Rachel Andrew breaks down the CSS Grid Layout specification. This time, we take a look at how to use <code>grid-template-areas</code> to place items.
categories:
  - CSS
  - CSS Grid
  - Browsers
---

When using CSS Grid Layout, you can always place items from one grid line to another. However, there is an alternate way of describing your layout, one that is visual in nature. In this article, we will learn how to use the `grid-template-areas` property to define placement on the grid and find out how the property really works.

*In case you missed the previous articles in this series, you can find them over here:*

- Part 1: [Creating A Grid Container](https://www.smashingmagazine.com/2020/01/understanding-css-grid-container/)
- Part 2: [Grid Lines](https://www.smashingmagazine.com/2020/01/understanding-css-grid-lines/)
- **Part 3: Grid Template Areas**

## Describing Layout With `grid-template-areas`

The `grid-template-areas` property accepts one or more strings as a value. Each string (enclosed in quotes) represents a row of your grid. You can use the property on a grid that you have defined using `grid-template-rows` and `grid-template-columns`, or you can create your layout in which case all rows will be auto-sized.

The following property and value describe a grid with four areas &mdash; each spanning two column tracks and two row tracks. An area is caused to span multiple tracks by repeating the name in all of the cells that you would like it to cover:

<pre><code class="language-css">grid-template-areas: "one one two two"
                     "one one two two"
                     "three three four four"
                     "three three four four";
</code></pre>

Items are placed into the layout by being named with an ident using the `grid-area` property. Therefore, if I want to place an element with a class of `test` into the area of the grid named `one`, I use the following CSS:

<pre><code class="language-css">.test {
  grid-area: one;
}
</code></pre>

You can see this in action in the CodePen example shown below. I have four items (with classes one to four); these are assigned to the relevant grid area using the `grid-area` property and therefore display on the grid in the correct boxes.

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="VwLLRKE" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/VwLLRKE">Simple grid-template-areas example</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

If you use the Firefox Grid Inspector, then you can see the area names and the grid lines demonstrating that each item does indeed span two row and two column tracks &mdash; all without doing any line-based positioning on the item itself.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96e561de-d1a7-4747-bfca-ede682b93b1e/smashing-grid-area1.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96e561de-d1a7-4747-bfca-ede682b93b1e/smashing-grid-area1.jpg" sizes="100vw" caption="Each items spans two rows and two columns" alt="A grid of four items with the Firefox Grid Inspector highlighting the lines" >}}

### Rules For Using `grid-template-areas`

There are a few rules when creating a layout in this way. Breaking the rules will make the value invalid and therefore your layout will not happen. The first rule is that **you must describe a complete grid**, i.e. every cell on your grid must be filled.

If you do want to leave a cell (or cells) as empty space, you do this by inserting a `.` or series such as `...` with no space between them.

Therefore, if I change the value of `grid-template-areas` as follows:

<pre><code class="language-css">grid-template-areas: "one one two two"
                     "one one two two"
                     ". . four four"
                     "three three four four";
</code></pre>

I now have two cells with no content in them. Item three only displays in the last row of the grid.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0036d067-1a36-4520-aeeb-5782dd1e32f8/smashing-grid-area2.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0036d067-1a36-4520-aeeb-5782dd1e32f8/smashing-grid-area2.jpg" sizes="100vw" caption="There is now whitespace in the grid" alt="One item now only spans one row with the Firefox Grid Inspector highlighting the lines" >}}

**You can only define each area once**, meaning that you can’t use this property to copy content into two places on the grid! So the following value would be invalid and cause the entire property to be ignored as we have duplicated the area `three`:

<pre><code class="language-css">grid-template-areas: "one one three three"
                     "one one two two"
                     "three three four four"
                     "three three four four";
</code></pre>

You can’t create a non-rectangular area, so the property can’t be used to create an ‘L’ or ‘T’ shaped area &mdash; making the following value also invalid:

<pre><code class="language-css">grid-template-areas: "one one two two"
                     "one one one one"
                     "three three four four"
                     "three three four four";
</code></pre>

### Formatting The Strings

I like to display the value of `grid-template-areas` as I have above (with each string representing a row below the row before). This gives me a visual representation of what the layout will be.

To help with this, it is valuable to add additional whitespace characters between each cell, and also to use multiple `.` characters denoting empty cells.

In the value below, I have used multiple whitespace characters between smaller words, and also multiple `.` characters so the empty cells line up:

<pre><code class="language-css">grid-template-areas: "one   one   two  two"
                     "one   one   two  two"
                     "..... ..... four four"
                     "three three four four";
</code></pre>

That said, it is also completely valid to have all of the strings on one line, so we could write our example as follows:

<pre><code class="language-css">grid-template-areas: "one one two two" "one one two two" "three three four four" "three three four four";
</code></pre>

{{% feature-panel %}}

## Explaining `grid-template-areas` And `grid-area`

The reason that each area needs to be a complete rectangle is that it needs to be the same shape that you could create by using line-based placement. If we stick with our example above, we could make this layout with grid lines as in the next CodePen. Here I have created my grid as before. This time, however, I used grid lines to create the positioning using the longhand `grid-column-start`, `grid-column-end`, `grid-row-start` and `grid-row-end` properties.

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="LYEdOdB" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/LYEdOdB">Grid Line placement</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

**Note**: *If you read my previous article "[Understanding CSS Grid: Grid Lines](https://www.smashingmagazine.com/2020/01/understanding-css-grid-lines/)" you will know that it is possible to use `grid-area` as a shorthand for declaring all four lines at once.*

This means that we could also create our layout with the following order of lines:

- `grid-row-start`
- `grid-column-start`
- `grid-row-end`
- `grid-column-end`

<pre><code class="language-css">.one {
  grid-area: 1 / 1 / 3 / 3;
}

.two {
  grid-area: 1 / 3 / 3 / 5;
}

.three {
  grid-area: 3 / 1 / 5 / 3;
}

.four {
  grid-area: 3 / 3 / 5 / 5;
}
</code></pre>

The `grid-area` property is interesting as it can take line numbers and line names. It is also important to understand the different way it behaves when in each mode.

### Using `grid-area` With Line Numbers

If you use the `grid-area` property with line numbers, then the lines are assigned in the order described above.

If you miss off any values &mdash; therefore providing 1, 2 or 3 line numbers &mdash; missing values are set to `auto` which means that the area will span 1 track (that being the default). So the following CSS would place an item `grid-row-start: 3` with all other values set to auto, therefore, the item would be auto-placed in the first available column track, and span one row track and one column track.

<pre><code class="language-css">grid-area: 3;
</code></pre>

### Using `grid-area` With Idents

If you use an ident (which is what a named area is called in Grid Layout), then the `grid-area` property also takes four lines. If you have named lines on your grid as described in “[Understanding CSS Grid: Creating A Grid Container](https://www.smashingmagazine.com/2020/01/understanding-css-grid-container/)”, then you can use these named lines in the same way as numbered lines.

However, what happens when you miss off some lines is different to when you use idents and not numbers.

Below, I have created a grid with named lines and used `grid-area` to place an item (missing off the final value):

<div class="break-out">

 <pre><code class="language-css">.grid {
  display: grid;
  grid-template-columns:
      [one-start three-start] 1fr 1fr
      [one-end three-end two-start four-start] 1fr 1fr [two-end four-end];
  grid-template-rows:
    [one-start two-start] 100px 100px
    [one-end two-end three-start four-start] 100px 100px [three-end four-end];;
}

.two {
  grid-area: two-start / two-start / two-end;
}
</code></pre>
</div>

This means that we are missing the line name for `grid-column-end`. The spec says that in this situation, `grid-column-end` should use a copy of `grid-column-start`. If `grid-column-end` and `grid-column-start` are identical, then the end line is thrown away, and essentially the value is set to auto so we span one track as in the numbered version.

The same thing happens if we miss off the third value `grid-row-end`; it becomes the same as `grid-row-start` and therefore becomes `auto`.

Take a look at the next CodePen example of how each `grid-area` is used and how this then changes the layout of the item:

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="oNXXOvR" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/oNXXOvR">Missing idents in grid-area</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

This then explains why `grid-area` works with a single value ident representing an area name.

When we create a named area with the `grid-template-areas` property, the edge of each area can be referenced by a line name which is the same as the area name you used. In our case, we could take our area named `one` and place our item using named lines as follows:

<pre><code class="language-css">.one {
  grid-row-start: one;
  grid-row-end: one;
  grid-column-start: one;
  grid-row-end: one;
}
</code></pre>

If the line is a `-start` line, then `one` resolves to the start end of the column or row. If it is an `-end` line, then `one` resolves to the end line of the column or row.

This means that when we say `grid-area: one`, we have omitted the last three values for the `grid-area` shorthand; they all end up being copies of the first value &mdash; all in our case become `one` and the item is placed just as with our longhand usage.

The way that naming works in Grid Layout is clever and enables some interesting things, which I have written about in my previous articles “[Naming Things In CSS Grid Layout](https://www.smashingmagazine.com/2017/10/naming-things-css-grid-layout/)” and “[Editorial Design Patterns With CSS Grid And Named Columns](https://www.smashingmagazine.com/2019/10/editorial-design-patterns-css-grid-subgrid-naming/)”.

{{% ad-panel-leaderboard %}}

### Layering Items When Using `grid-template-areas`

Only one name can occupy each cell when using `grid-template-areas`, however, you can still add additional items to the grid after doing your main layout in this way. You can use the line numbers as usual.

In the below CodePen example, I have added an additional item and positioned it using line-based positioning over the items already positioned:

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="bGddJRr" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/bGddJRr">Placing an item with line numbers</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

You can also use lines names defined when creating your usual columns or rows. Even better, you’ll have some line names created by the formation of the areas. We’ve already seen how you can get four line names with the name of the area. You also get a line on the start edge of each area with `-start` appended to the name of the area, and a line at the end edge of each area with `-end` appended.

Therefore, the area named `one` has start edge lines named `one-start` and end edge lines named `one-end`.

You can then use these implicit line names to place an item on the grid. This can be useful if you are redefining the grid at different breakpoints as long as you always want the placed item to come after a certain line name.

{{< codepen breakout="true" height="480" theme_id="light" slug_hash="QWbbPMQ" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/QWbbPMQ">Placing an item with implicit line names</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## Using Grid Template Areas In Responsive Design

I often work with building up components in a component library and I find that using `grid-template-areas` can be helpful in terms of being able to see exactly what a component will look like from the CSS. It is also very straightforward to redefine the component at different breakpoints by redefining the value of `grid-template-areas` sometimes in addition to changing the number of available column tracks.

In the CSS below, I have defined a single column layout for my component. Next, at a minimum width of 600px, I redefine the number of columns and also the value of `grid-template-areas` in order to create a layout with two columns. The nice thing about this approach is that anyone looking at this CSS can see how the layout works!

<pre><code class="language-css">.wrapper {
  background-color: #fff;
  padding: 1em;
  display: grid;
  gap: 20px;
  grid-template-areas:
    "hd"
    "bd"
    "sd"
    "ft";

}

@media (min-width: 600px) {
  .wrapper {
    grid-template-columns: 3fr 1fr;
    grid-template-areas:
      "hd hd"
      "bd sd"
      "ft ft";
  }
}

header { grid-area: hd; }
article {grid-area: bd; }
aside { grid-area: sd; }
footer { grid-area: ft; }
</code></pre>

{{% ad-panel-leaderboard %}}

## Accessibility

You need to be aware when using this method that it is very easy to move things around and cause the problem of [disconnecting the visual display from the underlying source order](https://rachelandrew.co.uk/archives/2019/06/04/grid-content-re-ordering-and-accessibility/). Anyone tabbing around the site, or who is watching the screen while having the content spoken, will be using the order that things are in the source. By moving the display from that order, you could create a very confusing, disconnected experience. Don’t use this method to move things around without also ensuring that the source is in a sensible order and matching the visual experience.

## Summary

That’s the lowdown on using the `grid-template-area` and `grid-area` properties to create layouts. If you haven’t used this layout method before, give it a try. I find that it is a lovely way to experiment with layouts and often use it when prototyping a layout &mdash; even if for one reason or another we will ultimately use a different method for the production version.

<div class="c-felix-the-cat">
<h4 class="h3">Overflow And Data Loss In CSS</h4>
<p>CSS is designed to keep your content readable. Let’s explore situations in which you might encounter overflow in your web designs and how CSS has evolved to create better ways to manage and design around unknown amounts of content. <a href="https://www.smashingmagazine.com/2019/09/overflow-data-loss-css/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

{{< signature "il" >}}

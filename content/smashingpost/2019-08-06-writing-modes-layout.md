---
title: Writing Modes And CSS Layout
slug: writing-modes-layout
author: rachel-andrew
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04742356-da07-4832-bd65-8d3d2c56e6b8/writing-modes-sharing-card.png
date: 2019-08-06T12:00:00.000Z
summary: >-
  An understanding of CSS Writing Modes is useful if you want to work with
  vertical scripts, or change writing mode for creative reasons. However, they
  also underpin our new layout methods, and those ideas are increasingly being
  applied across all of CSS. In this article, find out why Rachel Andrew
  believes understanding writing modes is so important.
description: >-
  An understanding of CSS Writing Modes is useful if you want to work with
  vertical scripts, or change writing mode for creative reasons. However, they
  also underpin our new layout methods, and those ideas are increasingly being
  applied across all of CSS. In this article, find out why Rachel Andrew
  believes understanding writing modes is so important.
categories:
  - CSS
  - Browsers
---
This is not an article about the practical or creative application of this property. Instead, I want to demonstrate why understanding writing modes is so important &mdash; even to those of us who rarely need to change the writing mode of a page or component. The support of multiple writing modes is key to the way that our new layout methods of Flexbox and Grid Layout have been designed. Understanding this can unlock a better understanding of how these layout methods work.

### What Are Writing Modes?

The writing mode of a document or a component refers to the direction that text flows. In CSS, to work with writing modes we use the `writing-mode` property. This property can take the following values:

* `horizontal-tb`
* `vertical-rl`
* `vertical-lr`
* `sideways-rl`
* `sideways-lr`

If you are reading this article on Smashing Magazine in English, then the writing mode of this document is `horizontal-tb`, or **Horizontal Top To Bottom**. In English, sentences are written horizontally &mdash; the first letter of each line starting on the left.

A language such as Arabic also has a `horizontal-tb` writing mode. It is written horizontally, top to bottom, however Arabic script is written right to left, and so sentences in Arabic start on the right.

Chinese, Japanese and Korean are written vertically, with the first character of the first sentence being top right. Following sentences being added to the left. Therefore, the writing mode used is `vertical-rl`. A vertical writing mode running from right to left.

Mongolian is also written vertically, but from left to right. Therefore, should you want to typeset Mongolian script you would use the writing mode `vertical-lr`.

{{% feature-panel %}}

The other two values of `writing-mode` are designed more for creative purposes than for typesetting vertical scripts. Using `sideways-lr` and `sideways-rl` turns text sideways &mdash; even characters normally written vertically and upright. The values, unfortunately, are only supported in Firefox at the moment. The following CodePen shows all of the different values of `writing-mode`, you will need to use Firefox if you want to see the `sideways-*` ones in action.

{{< codepen height="480" theme_id="light" slug_hash="dxVVRj" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Writing Mode demo](https://codepen.io/rachelandrew/pen/dxVVRj) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

Writing Modes can be used when creating a document that uses a language written using that writing mode. They can also be used creatively, for example, to set a heading vertically down the side of some content. In this article, however, I want to take a look at the impact that supporting vertical languages, and the possibility of vertical text, has on CSS layout, and across CSS in general.

Before I do so &mdash; if you are interested in the use of writing modes for vertical text &mdash; here are some useful resources:

* The W3C Internationalization site has a wealth of useful information. Read about [RTL scripts](https://www.w3.org/International/questions/qa-scripts#which) and [vertical text](https://www.w3.org/International/articles/vertical-text/).
* Jen Simmons wrote an excellent article about [CSS Writing Modes](https://24ways.org/2016/css-writing-modes/) which also includes several examples from print of these modes in use.
* [Thoughts on the world and our writing systems](https://www.chenhuijing.com/blog/thoughts-on-the-world-and-our-writing-systems/) - Chen Hui Jing
* [Vertical Typesetting With Writing Mode revisited](https://www.chenhuijing.com/blog/vertical-typesetting-revisited/) - Chen Hui Jing
* The [writing-mode](https://developer.mozilla.org/en-US/docs/Web/CSS/writing-mode) property on MDN

## The Block And Inline Dimensions

When we change the writing mode of a document, what we are doing is switching the direction of the **block flow**. Therefore, it quickly becomes very useful for us to understand what is meant by block and inline.

One of the first things we learn about CSS is that some elements are block elements, for example, a paragraph. These elements display one after the other in the block direction. Inline elements, such as a word in a sentence display one after the other in the inline direction. Working in a horizontal writing mode, we become used to the fact that the block dimension runs top to bottom vertically, and the inline dimension left to right horizontally.

As block and inline elements relate to the writing mode of our document, however, the inline dimension is horizontal only if we are in a horizontal writing mode. It doesn't relate to width, but instead to inline size. The block dimension is only vertical when in a horizontal writing mode. Therefore it doesn't relate to height, but to block size.

### Logical, Flow-Relative Properties

These terms, inline size and block size are also used as the names of new CSS properties designed to reflect our new writing mode aware world. If, in a horizontal writing mode you use the property `inline-size` instead of `width`, it will act in exactly the same way as width - until you switch the writing mode of your component. If you use `width` that will always be a physical dimension, it will always be the size of the component horizontally. If you use `inline-size`, that will be the size in the inline dimension, as the below example shows.

{{< codepen height="480" theme_id="light" slug_hash="RXLLyd" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [width vs. inline-size](https://codepen.io/rachelandrew/pen/RXLLyd) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

The same is true for `height`. The `height` property will always be the size vertically. It relates to how tall the item is. The `block-size` property, however, gives the size _in the block dimension_, vertically if we are in a horizontal writing mode and horizontal in a vertical one.

As I described in my article "[Understanding Logical Properties And Values](https://www.smashingmagazine.com/2018/03/understanding-logical-properties-values/)", there are mappings for all of the physical properties, those which are tied to the dimensions of the screen. Once you start to think about it, so much of CSS is specified in relation to the physical layout of a screen. We set positioning, margins, padding and borders using top, right, bottom, and left. We float things left and right. Sometimes tying things to the physical dimension will be what we want, however increasingly we are thinking about our layouts without reference to physical location. The Logical Properties and Values specification rolls out this writing mode agnostic way of working right across CSS.

## Writing Modes, Grid And Flexbox

When our new layout methods landed on the scene, they brought with them an agnostic way of looking at the writing mode of the component being laid out as a flex or grid layout. For the first time people were being asked to think about start and end, rather than left and right, top and bottom.

When I first started to present on the subject of CSS Grid, my early presentations were a rundown of all of the properties in the specification. I mentioned that the `grid-area` property could be used to set all four lines to place a grid item. The order of those lines was not, however, the familiar top, right, bottom and left we use to set all four margins. Instead, we need to use top, left, bottom, right - the reverse of that order! Until I understood the connection between grid and writing modes, this seemed a very odd decision. I came to realize that what we are doing is setting both start lines, then both end lines. Using top, right, bottom and left would work fine if we were in a horizontal writing mode, turn the grid on its side however and that makes no sense. If we use `grid-area: 1 / 2 / 3 / 5;` as in the pen below the lines are set as follows:

* `grid-row-start: 1;` - block start
* `grid-column-start: 2` - inline start
* `grid-row-end: 3` - block end
* `grid-column-end: 5` - inline end

{{< codepen height="480" theme_id="light" slug_hash="zgEEQW" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [grid-area](https://codepen.io/rachelandrew/pen/zgEEQW) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

### Flexbox Rows And Columns

If you use Flexbox and add `display: flex` to a container, your items will display as a row as the initial value of the `flex-direction` property is `row`. A row will follow the inline dimension of the writing mode in use. Therefore if your writing mode is `horizontal-tb` a row runs horizontally. If the text direction of the current script is left to right then items will line up starting from the left, if it is right to left they will line up starting on the right.

Use a vertical writing mode however, such as `vertical-rl` and `flex-direction: row` will cause the items to lay out vertically, as the inline direction is vertical. In this next CodePen all of the examples have `flex-direction: row`, only the writing mode or direction has changed.

{{< codepen height="480" theme_id="light" slug_hash="XvezrE" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [flex-direction: row](https://codepen.io/rachelandrew/pen/XvezrE) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

Add `flex-direction: column`, and the items layout in the block dimension of your writing mode. In a horizontal writing mode the block dimension is top to bottom, so a column is vertical. With a writing mode of `vertical-rl` a column is horizontal. As with the previous example, the only difference between the below flex layouts is the writing mode being used.

{{< codepen height="480" theme_id="light" slug_hash="RXLjbX" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [flex-direction: column](https://codepen.io/rachelandrew/pen/RXLjbX) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

### Grid Auto-Placement

When using auto-placement in grid, you will see similar behavior to that in flex layout. Grid items auto-place according to the writing mode of the document. The default is to place items in rows, which will be the inline direction - horizontally in a horizontal writing mode and vertically in a vertical one.

{{< codepen height="480" theme_id="light" slug_hash="eqGeYV" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Grid auto-placement row](https://codepen.io/rachelandrew/pen/eqGeYV) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

Try changing the flow of items to `column` as in the example below. The items will now flow in the block dimension - vertically in a horizontal writing mode and horizontally in a vertical one.

{{< codepen height="480" theme_id="light" slug_hash="xvXPby" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Grid auto-placement column](https://codepen.io/rachelandrew/pen/xvXPby) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

### Grid Line-Placed Placement

Line-based placement also respects writing mode. The lines of our grid start at 1, both for rows and columns. If we position an item from column line 1 to column line 3, and are in a horizontal writing mode with a left to right direction, that item will stretch from the left-most column line across two grid tracks horizontally. Thus spanning two columns.

Change the writing mode to `vertical-rl` and column line 1 will be at the top of the grid, the item spanning two tracks vertically. Still spanning two columns, but the columns are now running horizontally.

{{< codepen height="480" theme_id="light" slug_hash="mNBqEy" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Margins: adjacent siblings](https://codepen.io/rachelandrew/pen/mNBqEy) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

### Alignment In Grid And Flexbox

One of the first places many people will have come into contact with the way Flexbox dealt with writing modes, would be when aligning items in a flex layout. If we take the `flex-direction: row` example above, and use the `justify-content` property to align all of the items to `flex-end` the items move to the end of their row. This means that in a horizontal writing mode with left to right direct the items all move to the right, as the end of that row is on the right. If the direction is right to left, then they all move to the left.

In the vertical writing mode, they move to the bottom, assuming there is space for them to do so. I have set an `inline-size` on the components in this example to ensure that we have spare space in our flex containers to see the alignment in action.

Alignment is a little easier to understand in grid layout, as we always have the two axes to play with. Grid is two-dimensional, those two dimensions are block and inline. Therefore, you can remember one rule if you want to know whether to use the properties that begin with `align-` or those which begin with `justify-`. In grid layout the `align-` properties:- `align-content`, `align-items`, `align-self` are used to do block axis alignment. In a horizontal writing mode that means vertically, and in a vertical writing mode horizontally.

Once again, we don't use left and right or top and bottom, as we want our grid layout to work in exactly the same way no matter what the writing mode. So we align using `start` and `end`. If we align to `start` on the block dimension, that will be `top` when in `horizontal-tb`, but will be `right` when in `vertical-rl`. Take a look in the example below, the alignment values are identical in both grids, the only difference is the writing mode used.

{{< codepen height="480" theme_id="light" slug_hash="jgGaML" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Margins: adjacent siblings](https://codepen.io/rachelandrew/pen/jgGaML) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

The properties `justify-content`, `justify-items`, `justify-self` are always used for inline alignment in grid layout. That will be horizontal in a horizontal writing mode and vertical in a vertical writing mode.

{{< codepen height="480" theme_id="light" slug_hash="RXLjpP" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Margins: adjacent siblings](https://codepen.io/rachelandrew/pen/RXLjpP) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

Flexbox alignment is complicated somewhat by the fact that the main axis can be switched from row to column. Therefore, in Flexbox, we need to think about the alignment method as the main axis versus cross axis. The `align-` properties are used on the cross axis. On the main axis, all you have is `justify-content` because we deal with items as a group in Flexbox. On the cross axis, you can use `align-content` in cases where you have multiple flex lines _and_ space in the flex container to space them out. You can also use `align-items` and `align-self` to move the flex items on the cross axis in relationship to each other and their flex line.

{{< codepen height="480" theme_id="light" slug_hash="YmrExP" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Flexbox alignment](https://codepen.io/rachelandrew/pen/YmrExP) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

For more on alignment in CSS layout see my previous Smashing Magazine articles:

* [How To Align Things In CSS](https://www.smashingmagazine.com/2019/03/css-alignment/)
* [Everything You Need To Know About Alignment In Flexbox](https://www.smashingmagazine.com/2018/08/flexbox-alignment/)

{{% ad-panel-leaderboard %}}

## Writing Mode Awareness And Older CSS

Not all of CSS has fully caught up with this flow-relative, writing mode agnostic way of working. The places where it has not start to stand out as unusual the more you think of things in terms of block and inline, start and end. For example, in a multi-column layout, we specify `column-width`, which really means column inline-size, as it isn't mapped to the physical width when working in a vertical writing mode.

{{< codepen height="480" theme_id="light" slug_hash="pMWdLL" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Multicol and writing-mode](https://codepen.io/rachelandrew/pen/pMWdLL) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

As you can see, writing modes underpin much of what we do in CSS, even if we never use a writing mode other than `horizontal-tb`.

I find it incredibly helpful to think about CSS layout in this writing mode agnostic way. While it is perhaps a little early to be switching all of our properties and values to logical ones, we are already in a flow-relative world when dealing with new layout methods. Having your mental model be one of block and inline, start and end, rather than tied to the four corners of your screen, clarifies many of the things we come across when using FlexBox and grid.

{{< signature "il" >}}

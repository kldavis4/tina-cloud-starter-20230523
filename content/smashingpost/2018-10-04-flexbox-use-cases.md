---
title: 'Use Cases For Flexbox'
slug: flexbox-use-cases
author: rachel-andrew
image: >-
  https://res.cloudinary.com/indysigner/image/upload/v1538638101/use-cases-for-flexbox-rachel-andrew_fyhovj.png
date: 2018-10-04T13:50:30+02:00
summary: >-
  In this final article of the series, we wrap up by taking a look at some of the common uses for Flexbox. What should we use Flexbox for, and what it is not so good at?
description: >-
  In this final article of the series, we wrap up by taking a look at some of the common uses for Flexbox. What should we use Flexbox for, and what it is not so good at?
categories:
  - CSS
  - Flexbox
---
We come to the final part in my Flexbox series here at Smashing Magazine. In this post, I am going to spend some time thinking about what the use cases for Flexbox really are, given that we now have CSS Grid Layout, giving some suggestions for what you might use when and a way to decide.

## Earlier In This Series

If you haven’t picked up the other articles yet, this is essentially a concluding post so check those out first. I began by describing [exactly what happens when you create a flex container](https://www.smashingmagazine.com/2018/08/flexbox-display-flex-container/). In the second article in the series, I took a look at [alignment](https://www.smashingmagazine.com/2018/08/flexbox-alignment/), and how we align items on the main and cross axis in flexbox. In the third article, I unpack [how sizing works in Flexbox](https://www.smashingmagazine.com/2018/09/flexbox-sizing-flexible-box/), and how the browser figures out how big a flex item should be. Now that we know exactly how Flexbox works, we can wrap up by thinking about the use cases it is best for.

## Should I Use Grid Or Flexbox?

This is still the top question that I’m asked when teaching layout, and in general, I find that as people become more used to working with newer layout methods, it becomes a question you need to ask yourself less. As you build more components you will get a feel for which layout method to use.

If you are just getting to grips with the idea, however, the thing to remember is that **both CSS Grid Layout and Flexbox are both CSS**. Whether you have specified `display: grid` or `display: flex`, you often use more that is common than is different. Both Grid and Flexbox use the properties which are part of the Box Alignment specification; they both draw on concepts detailed in CSS Intrinsic and Extrinsic Sizing.

Asking whether your design should use Grid _or_ Flexbox is a bit like asking if your design should use font-size _or_ color. You should probably use both, as required. And, no-one is going to come to chase you if you use the _wrong_ one.

{{% feature-panel %}}

So, we are not picking between Vue.js and React, Bootstrap or Foundation. We are using CSS to do layout, and we need to use the bits of CSS which make most sense for the particular bit of our design that we are working on. Consider each component, and decide what is best for it, or what combination of things are best for it.

That might be Grid, or it might be Flexbox. It might be a grid outer container with some of your grid items becoming flex items or the reverse. There is no issue in nesting a grid inside a flex item if that is what your design calls for.

## What Is Flexbox Really For?

The Flexbox specification describes the layout method like this,

<blockquote>“Flex layout is superficially similar to block layout. It lacks many of the more complex text- or document-centric properties that can be used in block layout, such as floats and columns. In return, it gains simple and powerful tools for distributing space and aligning content in ways that web apps and complex web pages often need.”</blockquote>

I think the key phrase here is “distributing space and aligning content”. Flexbox is all about taking a bunch of things (which have varying sizes) and fitting them into a container (which itself has a varying size). Flexbox is squishy. Flexbox tries to create the best possible layout for our items, giving bigger items more space and smaller items less space, thus preserving readability of content. 

When people find Flexbox hard and weird, it is often because they are trying to use Flexbox as a grid system &mdash; trying to take back control over sizing and space distribution. When you do this, Flexbox can seem weird and hard as you are fighting against the very thing that makes it Flexbox, i.e. that inherent flexibility.

Therefore, patterns which suit flex layout very well are those where we are not so interested in having a pixel-perfect size for each item. We just want those items to display well alongside each other.

{{< codepen height="480" theme_id="light" slug_hash="EdPjgE" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/EdPjgE">Smashing Flexbox Series 4: Items Sharing Space</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

There are also patterns where you want to have wrapped lines, however, you do not want a strict grid. If we take the seminal grid versus the Flexbox example where we use the repeat auto-fill syntax in grid, and then a flex container with wrapped flex lines. Here we immediately see the difference between the two methods.

{{% ad-panel-leaderboard %}}

In the grid example, the grid items line up in rows and columns. While the number of column tracks changes (depending on space), the items always go into the next grid cell that is available. In fact, there is no way to ask a grid item to span tracks if there are some empty cells to fill in that auto-flow scenario.

{{< codepen height="480" theme_id="light" slug_hash="LgGVyX" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/LgGVyX">Smashing Flexbox Series 4: Grid Example</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

In the flex example, the final items share any space left over between them; this way, we do not have alignment horizontally and vertically. 

{{< codepen height="480" theme_id="light" slug_hash="vVLOZq" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/vVLOZq">Smashing Flexbox Series 4: Wrapped Items flex-basis: auto</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

If we have a flex-basis of auto and any of the flex items are larger, they will also be given more space so that the alignment could be quite different line by line.

{{< codepen height="480" theme_id="light" slug_hash="JmGdEa" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/JmGdEa">Smashing Flexbox Series 4: Wrapped Items</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

This then is a very clear example of where we would want to use Flexbox over Grid Layout. If we want the items to wrap but to take up the space they need on a line-by-line basis. That is a very different kind of layout to a grid. Patterns like this might be a set of tags (one or two-word elements that you wish to display nicely as a set of items), taking up the space they need and not rigidly being forced into a strict grid.

{{< codepen height="480" theme_id="light" slug_hash="EdPVNz" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/EdPVNz">Smashing Flexbox Series 4: Tags example</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

At the present time, Flexbox is also the best way to perform vertical and horizontal centering of an item inside a container. 

{{< codepen height="480" theme_id="light" slug_hash="BqjoxY" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/BqjoxY">Smashing Flexbox Series 4: Center an Item</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

In the future (when there is browser support for the Box Alignment properties outside of flex layout), we may be able to do this without needing to add `display: flex` to the container. For now, however, that is what you need to do &mdash; that extra line of CSS is really not an issue.

Flexbox is very good at dealing with small, one-dimensional components. Sets of form fields, icons, or other information can be easily laid out and allowed to be flexible without needing to carefully set the sizing on each item.

{{< codepen height="480" theme_id="light" slug_hash="vVLNbZ" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/vVLNbZ">Smashing Flexbox Series 4: Simple Row of Form Elements</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

You might also choose Flexbox in a scenario where all you need to do is cause content at the bottom of a layout to stick to the bottom of a container rather than popping up. In this example, I make the container a flex container by displaying the contents as a column, then allowing the middle to grow by pushing the footer to the bottom of the component.

{{< codepen height="480" theme_id="light" slug_hash="xyZYwY" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/xyZYwY">Smashing Flexbox Series 4: Sticky Footer Card</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

In production, I am finding that Flexbox is useful for lots of little jobs, making sure that things align properly, that space is shared out nicely between items. You could absolutely use a one-dimensional grid container for some of those things, and don’t worry about it if that is what you decide to do.

What I think Flexbox does very well, however, is to cope with the situation where extra items might need to be added that I didn’t expect in my design. For example, if I have a navigation component using Grid I would be creating enough tracks for all items, as I wouldn’t want a new row to be created if I had "too many" items. With flexbox, as long as I was allowing the items to be flexible from a flex-basis of 0 (or auto) then the items would allow their new companion into the row and make space for it.

{{% ad-panel-leaderboard %}}

## When Should I _Not_ Use Flexbox?

We have looked at some of the reasons that I think you should choose Flexbox over Grid Layout, so we can now look at some of the places where Flexbox might not be the best choice. We have already looked at our Flexbox versus grid example with items aligned horizontally and vertically versus items which take up space line by line. And, that distinction is the first thing to consider.

The grid example is of two-dimensional layout. Layout in rows and columns at the same time. The Flexbox example is one-dimensional layout. We have wrapped flex lines but space distribution is happening on a line by line basis. Each line is essentially acting as a new flex container in the flex-direction.

Therefore, if your component needs two-dimensional layout, you would be better placed to use Grid over Flexbox. It doesn’t matter whether your component is large or small. If you take one thing from this article, it is to remove the idea from your brain that Grid is somehow only meant for main page layout, and Flexbox for components. You can have a tiny component that requires two-dimensional layout, and main page structures which better suit one-dimensional layout.

Another good point at which Grid may be considered the better solution is if you are applying a width, or a flex-basis set as a length unit to your flex items in order to line them up with another row of flex items, or just to restrict the flexibility in some way. Quite often that indicates either than you really need a two-dimensional layout method or that the control from the container of grid would suit your layout better.

For example, we could make our flex layout display more like a grid, by restricting the flexibility of our items. Setting flex-grow to 0 and sizing the items with percentages, in a similar way to the way we would size items in a floated “grid”. If you find that you are doing that, I would suggest that Grid Layout is a much better approach as it is designed for this type of layout.

{{< codepen height="480" theme_id="light" slug_hash="jeWZyM" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/jeWZyM">Smashing Flexbox Series 4: Wrapped Flex Items with Percentage Widths</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

With all that said, remember that there is very often not a clear right _or_ wrong answer. Sometimes the only thing you can do is to try different ways and see what suits the component best. Remember that you can also switch layout methods, using Flexbox at one breakpoint and Grid at another. 

## And That’s A (Flex) Wrap!

I hope this series on Flexbox has been helpful and demonstrated how understanding some of the logic behind alignment and sizing of flex items, makes life easier when working with it. If you are left with any outstanding questions or have a pattern which seems not to have an obvious answer in terms of the layout method to use, post a comment.

{{< signature "il" >}}
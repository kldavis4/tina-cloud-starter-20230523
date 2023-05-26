---
title: 'When And How To Use CSS Multi-Column Layout'
slug: css-multiple-column-layout-multicol
author: rachel-andrew
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58c87a1e-ec68-4dc7-9ca1-a4a439ff3c4d/multicol-article-sharing-card.png
date: 2019-01-11T15:00:30+02:00
summary: >-
  The Multi-column Layout spec is often overlooked as we use Grid and Flexbox. In this article Rachel Andrew explains why it is different to other layout methods, and shows some useful patterns and sites which showcase it well.
description: >-
  The Multi-column Layout spec is often overlooked as we use Grid and Flexbox. In this article Rachel Andrew explains why it is different to other layout methods, and shows some useful patterns and sites which showcase it well.
categories:
  - CSS
  - Layouts
  - Responsive Design
---
In all of the excitement about CSS Grid Layout and Flexbox, another layout method is often overlooked. In this article I’m going to take a look at Multi-column Layout &mdash; often referred to as multicol or sometimes "CSS Columns". You’ll find out which tasks it is suited for, and some of the things to watch out for when making columns.

## What Is Multicol?

The basic idea of multicol, is that you can take a chunk of content and flow it into multiple columns, as in a newspaper. You do this by using one of two properties. The `column-count` property specifies the number of columns that you would like the content to break into. The `column-width` property specifies the ideal width, leaving the browser to figure out how many columns will fit.

It doesn’t matter which elements are inside the content that you turn into a multicol container, everything remains in normal flow, but broken into columns. This makes multicol unlike other layout methods that we have in browsers today. Flexbox and Grid for example, take the child elements of the container and those items then participate in a flex or grid layout. With multicol, you still have normal flow, except inside a column.

In the below example I am using `column-width`, to display columns of at least `14em`. Multicol assigns as many `14em` columns as will fit and then shares out the remaining space between the columns. Columns will be at least `14em`, unless we can only display one column in which case it may be smaller. Multicol was the first time that we saw this kind of behavior in CSS, columns being created which were essentialy responsive by default. You do not need to add Media Queries and change the number of columns for various breakpoints, instead we specify an optimal width and the browser will work it out.

{{< codepen height="480" theme_id="light" slug_hash="xmyzad" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/xmyzad">Smashing Multicol: column-width</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

{{% feature-panel %}}

## Styling Columns

The column boxes created when you use one of the column properties can’t be targeted. You can’t address them with JavaScript, nor can you style an individual box to give it a background color or adjust the padding and margins. All of the column boxes will be the same size. The only thing you can do is add a rule between columns, using the column-rule property, which acts like border. You can also control the gap between columns using the `column-gap` property, which has a default value of `1em` however you can change it to any valid length unit.

{{< codepen height="480" theme_id="light" slug_hash="OrBErd" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/OrBErd">Smashing Multicol: column styling</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

That is the basic functionality of multicol. You can take a chunk of content and split it into columns. Content will fill the columns in turn, creating columns in the inline direction. You can control the gaps between columns and add a rule, with the same possible values as border. So far so good, and all of the above is very well supported in browsers and has been for a long time, making this spec very safe to use in terms of backwards compatibility.

There are some further things you might want to consider with your columns, and some potential issues to be aware of when using columns on the web.

## Spanning Columns

Sometimes you might like to break some content into columns, but then cause one element to span across the column boxes. Applying the `column-span` property to a descendent of the multicol container achieves this.

<p class="c-pre-sidenote--left">In the example below, I have caused a <code>&lt;blockquote&gt;</code> element to span across my columns. Note that when you do this, the content breaks into a set of boxes above the span, then starts a new set of column boxes below. The content doesn’t jump across the spanned element.</p><p class="c-sidenote c-sidenote--right"> The <code>column-span</code> property is currently being implemented in Firefox and is behind a feature flag.</p>

{{< codepen height="480" theme_id="light" slug_hash="YdJvgv" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/YdJvgv">Smashing Multicol: column-span</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Be aware that in the current spec, the values for `column-span` are either `all` or `none`. You can’t span just some of the columns, but you can get the kind of layout you might see in a newspaper by combining multicol with other layout methods. In this next example, I have a grid container with two column tracks. The left-hand track is `2fr`, the right-hand track `1fr`. The article in the left-hand track I have turned into a multicol container with two tracks, it also has a spanning element.

On the right, we have an aside which goes into the second Grid column track. By playing around with the various layout methods available to us, we can figure out exactly which layout method suits the job at hand &mdash; don’t be afraid to mix and match!

{{< codepen height="480" theme_id="light" slug_hash="aPRjzL" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/aPRjzL">Smashing Multicol: mixing layout methods</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## Controlling Content Breaks

If you have content containing headings, then you probably want to avoid the situation where a heading ends up as the last thing in a column with the content going into the next column. If you have images with captions then the ideal situation would be for the image and caption to stay as one unit, not becoming split across columns. To deal with these problems CSS has properties to control where the content breaks.

When you split your content into columns, you perform what is known as fragmentation. The same is true if you split your content between pages, such as when you create a stylesheet for a print context. Therefore, multicol is closest to Paged Media than it is to other layout methods on the web. Because of this, for several years the way to control breaks in the content has been to use the `page-break-` properties which were part of CSS2.1.

- `page-break-before`
- `page-break-after`
- `page-break-inside`

More recently the CSS Fragmentation specification has defined properties for fragmentation which are designed for any fragmented context, the spec includes details for Paged Media, multicol and the stalled Regions spec; Regions also fragments a continuous piece of content. By making these properties generic they can apply to any future fragmented context to, in the same way that the alignment properties from Flexbox were moved into the Box Alignment spec in order that they could be used in Grid and Block layout.

- `break-before`
- `break-after`
- `break-inside`

As an example, I have used `break-inside avoid` on the `<figure>` element, to prevent the caption being detached from the image. A supporting browser should keep the figure together even if that causes the columns to look unbalanced.

{{< codepen height="480" theme_id="light" slug_hash="PXyBrN" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/PXyBrN">Smashing Multicol: break-inside</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Unfortunately, support for these properties in multicol is pretty patchy. Even where supported they should be seen as a suggestion due to the fact that it would be possible to make so many requests while trying to control breaking, that essentially the browser can’t really break anywhere. The spec does define priorities in this case, however it is probably more useful for you to control only the most important cases.

{{% ad-panel-leaderboard %}}

## The Problem Of Columns On the Web

One reason why we don’t see multicol used much on the web is the fact that it would be very easy to end up with a reading experience which made the reader scroll in the block dimension. That would mean scrolling up and down vertically for those of us using English or another vertical writing mode. This is not a good reading experience!

If you fix the height of the container, for example by using the viewport unit `vh`, and there is too much content, then overflow will happen in the inline direction and so you get a horizontal scrollbar instead.

{{< codepen height="480" theme_id="light" slug_hash="mazQda" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/mazQda">Smashing Multicol: overflow columns</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Neither of these things are ideal, and making use of multicol on the web is something we need to think about very carefully in terms of the amount of content we might be aiming to flow into our columns.

### Block Overflow Columns

For Level 2 of the specification, we are considering how to enable a method by which overflow columns, those which currently end up causing the horizontal scrollbar, could instead be created in the block direction. This would mean that you could have a multicol container with a height, and once the content had made columns which filled that container, a new set of columns would be created below. This would look a little like our spanning example above, however, instead of having a spanner causing the new column boxes to start, it would be the overflow caused by a container with a restriction in the block dimension.

This feature would make multicol far more useful for the web. While we are a little way off right now, you can keep an eye on [the issue in the CSS Working Group repo](https://github.com/w3c/csswg-drafts/issues/2923). If you have additional use cases for this feature do post them, it can really help when designing the new feature.

{{% ad-panel-leaderboard %}}

## What Is Multicol Useful For Today?

With the current specification, splitting all of your content into columns without consideration for the problems of scrolling isn’t advised. However, there are some cases where multicol is ideal on the web. There are enough uses cases to make it something you should consider when looking at design patterns.

### Collapsing Small UI Or Text Elements

Multicol can be useful in any place where you have a small list of items that you want to take up less space. For example a simple listing of checkboxes, or a list of names. Often in these scenarios, the visitor is not reading down one column and then going back to the top of the next, but scanning the content for a checkbox to click or an item to select. Even if you do create a scrolled experience, it may not be an issue.

You can see an example of multicol used in this way by [Sander de Jong](https://twitter.com/Spinal83) on the [DonarMuseum
](https://www.donarmuseum.nl/spelers/) website.

{{< rimg breakout="true" href="https://www.donarmuseum.nl/spelers/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85624645-e42a-4ed4-93cf-6e5084a21e50/donarmuseum.png" sizes="100vw" caption="On <a href='https://www.donarmuseum.nl/'>DonarMuseum</a>, we can see multicol used to display lists of names. (<a href='https://www.donarmuseum.nl/spelers/'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85624645-e42a-4ed4-93cf-6e5084a21e50/donarmuseum.png'>Large preview</a>)" alt="Names are arranged into multiple columns on the DonarMuseum website" >}}

### Known Small Amounts Of Content

There are times when we design a site where we know that some piece of content is relatively small, and will fit on the majority of screens without causing unwanted scrolling. I’ve used multicol on [Notist presentation pages](https://noti.st/rachelandrew/Au3wK3/making-things-better-redefining-the-technical-possibilities-of-css), for the introduction to a talk.

[Andy Clarke](https://twitter.com/Malarkey) designed a lovely example for the [Equfund website](https://equfund.com/housing-in-crisis).

{{< rimg breakout="true" href="https://equfund.com/housing-in-crisis" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b5c64ee-f7c8-4163-814a-c0f279751358/equfund.png" sizes="100vw" caption="On the Equfund website, you can see how different HTML elements remain in normal flow while displayed inside columns. (<a href='https://equfund.com/housing-in-crisis'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b5c64ee-f7c8-4163-814a-c0f279751358/equfund.png'>Large preview</a>)" alt="A two-column layout including various content" >}} 

To avoid the possibility of very small screens causing scrolling, remember that you can use media queries to check for height as well as width (or in a logical world, block as well as inline). If you only enable columns at a breakpoint which has a `min-height` large enough for their content, this can save users of very small devices having a poor scrolling experience.

### Masonry-Like Display Of Content

Another place where Multiple-column Layout works beautifully is if you want to create a Masonry type of display of content. Multicol is the only layout method that will currently create this kind of layout with unequal height items. Grid would either leave a gap, or stretch the items to make a strict two-dimensional grid.

[Veerle Pieters](https://twitter.com/vpieters) has a beautiful example of using multicol in this way on her [inspiration](https://veerle.duoh.com/inspiration) page.

{{< rimg breakout="true" href="https://veerle.duoh.com/inspiration" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61458bee-ab40-49a9-b16e-73c75c1817e4/duoh.png" sizes="100vw" caption="In this design by Veerle Pieters, multicol is used to layout multiple boxes or cards as columns. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61458bee-ab40-49a9-b16e-73c75c1817e4/duoh.png'>Large preview</a>)" alt="An arrangement of multiple boxes in columns designed by Veerle Pieters" >}}

### Grid And Flexbox Fallbacks

The `column-` properties can also be used as a fallback for Grid and Flex layout. If you specify one of the properties on a container, then turn that container into a Flex or Grid layout by using `display: flex` or `display: grid` any column behavior will be removed. If you have, for example, a cards layout that uses Grid Layout, and the layout would be readable if it ran in columns rather than across the page, you could use multicol as a simple fallback. Browsers that do not support Grid will get the multicol display, those which support Grid will get the Grid Layout.

## Don’t Forget Multicol!

Fairly frequently I answer Grid and Flexbox questions where the answer is to not use Grid or Flexbox, but instead to look at Multicol. You probably won’t use it on every site, but when you come across a use case it can be really helpful. Over at MDN there are useful resources for [multicol](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Columns) and the related [fragmentation properties](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Fragmentation).

If you have used multicol on a project, perhaps drop a note in the comments, to share other ways in which we can use the feature.

{{< signature "il" >}}
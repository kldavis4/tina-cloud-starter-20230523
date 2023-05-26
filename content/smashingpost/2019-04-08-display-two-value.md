---
title: 'Digging Into The Display Property: The Two Values Of Display'
slug: display-two-value
author: rachel-andrew
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df4d7ab7-0e02-420b-8f2a-b89282547ecb/display-property-sharing-card-rachel-andrew.png
date: 2019-04-08T13:00:59+02:00
summary: >-
  We talk a lot about Flexbox and CSS Grid Layout, but these layout methods are essentially values of the CSS `display` property, a workhorse of a property that doesn’t get a lot of attention. Rachel Andrew takes a better look in a short series.
description: >-
  We talk a lot about Flexbox and CSS Grid Layout, but these layout methods are essentially values of the CSS `display` property, a workhorse of a property that doesn’t get a lot of attention. Rachel Andrew takes a better look in a short series.
categories:
  - CSS
  - Browsers
---
A flex or grid layout starts out with you declaring `display: flex` or `display: grid`. These layout methods are values of the CSS `display` property. We tend not to talk about this property on its own very much, instead concentrating on the values of `flex` or `grid`, however, there are some interesting things to understand about `display` and how it is defined that will make your life much easier as you use CSS for layout.

In this article, the first in a short series, I’m going to take a look at the way that the values of `display` are defined in the Level 3 specification. This is a change to how we defined `display` in earlier versions of CSS. While it may seem unusual at first for those of us who have been doing CSS for many years, I think these changes really help to explain what is going on when we change the value of `display` on an element.

## Block And Inline Elements

One of the first things we teach people who are new to CSS are the concepts of block and inline elements. We will explain that some elements on the page are `display: block` and they have certain features because of this. They stretch out in the inline direction, taking up as much space as is available to them. They break onto a new line; we can give them width, height, margin as well as padding, and these properties will push other elements on the page away from them.

We also know that some elements are `display: inline`. Inline elements are like words in a sentence; they don’t break onto a new line, but instead reserve a character of white space between them. If you add margins and padding, this will display but it won’t push other elements away.

The behavior of block and inline elements is fundamental to CSS and the fact that a properly marked up HTML document will be readable by default. This layout is referred to as “Block and Inline Layout” or “Normal Flow” because this is the way that elements lay themselves out if we don’t do anything else to them.

{{% feature-panel %}}

## Inner And Outer Values Of `display`

We understand block and inline elements, but what happens if we make an item `display: grid`? Is this something completely different? If we look at a component on which we have specified `display: grid`, in terms of the parent element in the layout it behaves like a `block level` element. The element will stretch out and take up as much space in the inline dimension as is available, it will start on a new line. It behaves just like a `block` element in terms of how it behaves alongside the rest of the layout. We haven’t said `display: block` though, or have we?

It turns out that we have. In [Level 3 of the Display specification](https://www.w3.org/TR/css-display-3), the value of `display` is defined as two keywords. These keywords define the outer value of display, which will be `inline` or `block` and therefore define how the element behaves in the layout alongside other elements. They also define the inner value of the element &mdash; or how the direct children of that element behave.

This means that when you say `display: grid`, what you are really saying is `display: block grid`. You are asking for a block level grid container. An element that will have all of the block attributes &mdash; you can give it height and width, margin and padding, and it will stretch to fill the container. The children of that container, however, have been given the inner value of `grid` so they become grid items. How those grid items behave is defined in the CSS Grid Specification: the `display` spec gives us a way to tell the browser that this is the layout method we want to use.

I think that this way of thinking about `display` is incredibly helpful; it directly explains what we are doing with various layout methods. If you were to specify `display: inline flex`, what would you expect? Hopefully, a box that behaves as an inline element, with children that are flex items.

There are a few other things neatly explained by thinking about `display` in this new way, and I’ll take a look at some of these in the rest of this article.

## We Are Always Going Back To Normal Flow

When thinking about these inner and outer display properties, it can be helpful to consider what happens if we don’t mess around with the value of display at all. If you write some HTML and view it in a browser, what you get is Block and Inline Layout, or Normal Flow. The elements display as `block` or `inline` elements.

{{< codepen height="480" theme_id="light" slug_hash="ZZzPQE" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="[https://codepen.io/rachelandrew/pen/ZZzPQE/](https://codepen.io/rachelandrew/pen/ZZzPQE)">Block and Inline Layout</a> by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

The example below contains some markup that I have turned into a media object, by making the `div` `display: flex` (the two direct children) now become flex items, so the image is now in a row with the content. If you see in the content, however, there is a heading and a paragraph which are displaying in normal flow again. The direct children of the media object became flex items; _their_ children return to normal flow unless we change the value of display on the flex item. The flex container itself is a block box, as you can see by the fact the border extends to the edge of its parent.

{{< codepen height="480" theme_id="light" slug_hash="gyYEPz" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="[https://codepen.io/rachelandrew/pen/gyYEPz](https://codepen.io/rachelandrew/pen/gyYEPz)">Block and Inline Layout With Flex Component</a> by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

If you work with this process, the fact that elements on your page will lay themselves out with this nice readable normal flow layout, rather than fighting against it and trying to place everything, CSS is much easier. You are also less likely to fall into accessibility issues, as you are working with the document order, which is exactly what a screen reader or a person tabbing through the document is doing.

{{% ad-panel-leaderboard %}}

### Explaining `flow-root` And `inline-block`

The value of `inline-block` is also likely to be familiar to many of us who have been doing CSS for a while. This value is a way to get some of the block behavior on an `inline` element. For example, an `inline-block` element can have a width and a height. An element with `display: inline-block` also behaves in an interesting way in that it creates a **B**lock **F**ormatting **C**ontent (BFC).

A BFC does some useful things in terms of layout, for example, it contains floats. To read about Block Formatting Contexts in more detail see my previous article “[Understanding CSS Layout And The Block Formatting Context](https://www.smashingmagazine.com/2017/12/understanding-css-layout-block-formatting-context/).” Therefore saying `display: inline-block` gives you an inline box which also establishes a BFC.

As you will discover (if you read the above-mentioned article about the Block Formatting Context), there is a newer value of display which also explicitly creates a BFC. This is the value of `flow-root`. This value creates a BFC on a block, rather than an inline element.

* `display: inline-block` gives you a BFC on an inline box.
* `display: flow-root` gives you a BFC on a block box.

You are now probably thinking that is all a bit confusing: why do we have two completely different keywords here, and what happened to the two-value syntax we were talking about before? This leads neatly into the next thing I need to explain about `display`, i.e. the fact that CSS has a history we need to deal with in terms of the `display` property.

## Legacy Values Of Display

The CSS2 Specification detailed the following values for the `display` property:

* `inline`
* `block`
* `inline-block`
* `list-item`
* `none`
* `table`
* `inline-table`

Also defined were the various table internal properties such as `table-cell` which we are not dealing with in this article.

We then added to these some values for display, to support flex and grid layout:

* `grid`
* `inline-grid`
* `flex`
* `inline-flex`

**Note**: *The specification also defines `ruby` and `inline-ruby` to support Ruby Text which you can read about in the [Ruby specification](https://drafts.csswg.org/css-ruby-1/#ruby-def).*

{{% ad-panel-leaderboard %}}

These are all single values for the `display` property, defined before the specification was updated to explain CSS Layout in this way. Something very important about CSS is the fact that we don’t go around breaking the web; **we can’t simply change things**. We can’t suddenly decide that everyone should use this new two-value syntax and therefore every website ever built that used the single value syntax will break unless a developer goes back and fixes it!

While thinking about this problem, you may enjoy this [list of mistakes in the design of CSS](https://wiki.csswg.org/ideas/mistakes) which are less mistakes in many cases as things that were designed without a crystal ball to see into the future! However, the fact is that we can’t break the web, which is why we have this situation where right now browsers support a set of single values for display, and the specification is moving to two values for display.

The way we get around this is to specify legacy and short values for display, which includes all of these single values. This means that a mapping can be defined between single values and new two keyword values. Which gives us the following table of values:

<table>
    <thead>
        <tr>
            <th>Single Value</th>
            <th>Two-Keyword Values</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>block</code></td>
            <td><code>block flow</code></td>
            <td>Block box with normal flow inner</td>
        </tr>
        <tr>
            <td><code>flow-root</code></td>
            <td><code>block flow-root</code></td>
            <td>Block box defining a BFC</td>
        </tr>
        <tr>
            <td><code>inline</code></td>
            <td><code>inline flow</code></td>
            <td>Inline box with normal flow inner</td>
        </tr>
        <tr>
            <td><code>inline-block</code></td>
            <td><code>inline flow-root</code></td>
            <td>Inline box defining a BFC</td>
        </tr>
        <tr>
            <td><code>list-item</code></td>
            <td><code>block flow list-item</code></td>
            <td>Block box with normal flow inner and additional marker box</td>
        </tr>
        <tr>
            <td><code>flex</code></td>
            <td><code>block flex</code></td>
            <td>Block box with inner flex layout</td>
        </tr>
        <tr>
            <td><code>inline-flex</code></td>
            <td><code>inline flex</code></td>
            <td>Inline box with inner flex layout</td>
        </tr>
        <tr>
            <td><code>grid</code></td>
            <td><code>block grid</code></td>
            <td>Block box with inner grid layout</td>
        </tr>
        <tr>
            <td><code>inline-grid</code></td>
            <td><code>inline grid</code></td>
            <td>Inline box with inner grid layout</td>
        </tr>
        <tr>
            <td><code>table</code></td>
            <td><code>block table</code></td>
            <td>Block box with inner table layout</td>
        </tr>
        <tr>
            <td><code>inline-table</code></td>
            <td><code>inline table</code></td>
            <td>Inline box with inner table layout</td>
        </tr>
    </tbody>
</table>

To explain how this works, we can think about a grid container. In the two-value world, we would create a block level grid container with:

<pre><code class="language-css">.container {
    display: block grid;
}
</code></pre>

However, the legacy keyword means that the following does the same thing:

<pre><code class="language-css">.container {
    display: grid;
}
</code></pre>

If, instead, we wanted an inline grid container, in the two-value world we would use:

<pre><code class="language-css">.container {
    display: inline grid;
}
</code></pre>

And if using the legacy values:

<pre><code class="language-css">.container {
    display: inline-grid;
}
</code></pre>

We can now go back to where this conversation began and look at `display: inline-block`. Looking at the table, you can see that this is defined in the two-value world as `display: inline flow-root`. It now matches `display: flow-root` which in a two-value world would be `display: block flow-root`. A little bit of tidying up and clarification of how these things are defined. A refactoring of CSS, if you like.

## Browser Support For The Two-Value Syntax

As yet, browsers do not support the two-value syntax for the `display` property. The implementation bug for Firefox can be found [here](https://bugzilla.mozilla.org/show_bug.cgi?id=1038294). Implementation &mdash; when it happens &mdash; would essentially involve aliasing the legacy values to the two-value versions. It’s likely to be a good while, therefore, before you can actually use these two-value versions in your code. However, that really isn’t the point of this article. Instead, I think that looking at the values of display in the light of the two-value model helps explain much of what is going on.

When you define layout on a box in CSS, you are defining what happens to this box in terms of **how it behaves in relation to all of the other boxes in the layout**. You are also defining how the *children* of that box behave. You can think in this way long before you can explicitly declare the values as two separate things, as the legacy keywords map to those values, and it will help you understand what happens when you change the value of `display`.

{{< signature "il" >}}
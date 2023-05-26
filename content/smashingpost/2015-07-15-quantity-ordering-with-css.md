---
title: Quantity Ordering With CSS
slug: quantity-ordering-with-css
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b2721f5-6f5f-4d5a-ac91-870c62b7b82e/css.jpg'
date: 2015-07-15T00:20:54.000Z
author: drewminns
description: >-
  Here is your mission, should you choose to accept it: **create a table of
  items**. Each item should span a third of the content area, with the fourth
  item starting on a new row, much like floats. However, a particular item must
  always display the price at the end of the first row.

  So if there are only two elements, the price element would be second. But if
  there are more than three items, the price would be the last element in the
  first row. You might assume that JavaScript would be the best solution — just
  loop over the items, and if there are more than three, update the styling. But
  what if I told you could do it with CSS alone?
categories:
  - Coding
  - CSS
  - Techniques
  - Flexbox
---
Here is your mission, should you choose to accept it: **create a table of items**. Each item should span a third of the content area, with the fourth item starting on a new row, much like floats. However, a particular item must always display the price at the end of the first row.

So if there are only two elements, the price element would be second. But if there are more than three items, the price would be the last element in the first row.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [It’s Time To Start Using CSS Custom Properties](https://www.smashingmagazine.com/2017/04/start-using-css-custom-properties/)
*   [Houdini: Maybe The Most Exciting Development In CSS](https://www.smashingmagazine.com/2016/03/houdini-maybe-the-most-exciting-development-in-css-youve-never-heard-of/)
*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [Truly Fluid Typography With vh And vw Units](https://www.smashingmagazine.com/2016/05/fluid-typography/)

You might assume that JavaScript would be the best solution — just loop over the items, and if there are more than three, update the styling. But what if I told you could do it with CSS alone?

{{% feature-panel %}}

## Pure CSS Counting

I’ve gone all in on flexbox lately, teaching it right alongside floats as a layout method at our little project called _HackerYou_, and I have found that students take to it well. The flexbox specification contains properties that enable us to modify markup in new ways. One of these is `order`, which allows us to modify the presentational order of content without touching the markup or structure.

Used with media queries, `order` is extremely useful, enabling us to change the content’s order with the viewport size. That got me thinking: Why can’t we change the order of elements according to the amount of content?

## Quantity Queries

An idea [explored by Lea Verou](https://lea.verou.me/2011/01/styling-children-based-on-their-number-with-css3/), [André Luis](https://andr3.net/blog/post/142) and [Heydon Pickering](https://alistapart.com/article/quantity-queries-for-css), quantity queries count the number of sibling elements and apply styles if a certain number are present.

What if we combined quantity queries and the `order` property to change how content is read according to how much of it there is?

## Using Flexbox

Flexbox, or the “[Flexible Box Layout Module](https://www.w3.org/TR/2015/WD-css-flexbox-1-20150514/),” is a CSS specification that allows for content to be laid out in any direction and for children to be sized to their parent easily. Originally introduced in 2009, flexbox has gone through many changes over the years. However, [it is supported](https://caniuse.com/#search=flex) in all current browsers, with the exception of Internet Explorer 9+.

One of the most significant changes within flexbox is the naming syntax of associated properties and values. Because the specification evolved over years, browser vendors would use the syntax that was being developed at the time. So, using vendor prefixes is recommended to ensure support across legacy browsers.

One recommended tool for managing cross-browser support in CSS is [Autoprefixer](https://github.com/postcss/autoprefixer), which is typically included in preprocessors and Gulp and Grunt files.</p>

### Understanding Order

Before we dig into quantity queries and how they work, we should understand how to use the `order` property. First, we need to wrap the content with a parent element and apply `display: flex` to it.

Here’s the HTML:

<pre><code class="language-markup">&lt;div class=&quot;container&quot;&gt;
  &lt;p class=&quot;itemOne&quot;&gt;Hello&lt;/p&gt;
  &lt;p class=&quot;itemTwo&quot;&gt;World!&lt;/p&gt;
&lt;/div&gt;</code></pre>

And here’s the CSS:

<pre><code class="language-scss">.container {
  display: flex;
}</code></pre>

See the Pen [LVVXxz](https://codepen.io/drewminns/pen/LVVXxz/) by Drew Minns ([@drewminns](https://codepen.io/drewminns)) on [CodePen](https://codepen.io).

By default, elements will appear in their order in the markup. All child elements of a flexbox parent share an `order` value of `1`.

This value is unitless and simply refers to the order of the element relative to the other elements around it. However, we can change the value of an individual element using the `order` property.

<pre><code class="language-css">p.itemOne {
  order: 2;
}</code></pre>

See the Pen [Really Good Work Article](https://codepen.io/drewminns/pen/oXXQBo/) by Drew Minns ([@drewminns](https://codepen.io/drewminns)) on [CodePen](https://codepen.io).

In the example above, we’ve changed the order of `p.itemOne` to a value of `2`, making it fall after `p.itemTwo` and thereby changing the presentational order for the user. Note that the markup remains the same, however.</p>

## Counting With CSS

Media queries, eh? Such an awesome tool for applying CSS when certain conditions are met. Those conditions could be device type, size, color and more — pretty powerful stuff. But the query applies **only to the device that the viewer is using**; there is no defined CSS method for querying the _amount_ of content in an element.

If we get creative with existing CSS pseudo-selectors, however, we can build tools that count the number of children in an element and then apply styles accordingly. For this example, let’s use a simple ordered list:

<pre><code class="language-markup">&lt;ul class=&quot;ellist&quot;&gt;
  &lt;li&gt;1&lt;/li&gt;
  &lt;li&gt;2&lt;/li&gt;
  &lt;li&gt;3&lt;/li&gt;
  &lt;li&gt;4&lt;/li&gt;
  &lt;li&gt;5&lt;/li&gt;
  &lt;li class=&quot;target&quot;&gt;6&lt;/li&gt;
&lt;/ul&gt;</code></pre>

The magic of counting sibling elements is in the selector below. This example applies styles to elements when four or more are available.

<pre><code class="language-scss">ul.ellist li:nth-last-child(n+4) ~ li,
ul.ellist li:nth-last-child(n+4):first-child {
  // styles go here
}</code></pre>

See the Pen [WvvYyN](https://codepen.io/drewminns/pen/WvvYyN/) by Drew Minns ([@drewminns](https://codepen.io/drewminns)) on [CodePen](https://codepen.io).</p>

### Wait, No. That’s Insane!

Yep, that’s the selector. In English, it could be translated as this: “When there are four or more child elements, get the other list items and the first child.”

Let’s break this down. First, the counting:

<pre><code class="language-scss">ul.ellist li:nth-last-child(n+4) {
  // Styles!
}</code></pre>

This translates as, “Go to the last child and count back four children.” Apply the styles to the fourth element and all elements before it.

Go ahead and experiment by editing the Codepen and changing the selector to a different number.

See the Pen [Pqqvqp](https://codepen.io/drewminns/pen/Pqqvqp/) by Drew Minns ([@drewminns](https://codepen.io/drewminns)) on [CodePen](https://codepen.io).

So, there it is, counting. If fewer than four siblings are counted, nothing is selected and no styles are applied. We can now modify this selector to select all `li` elements using the [general sibling combinator](https://www.w3.org/TR/selectors/#general-sibling-combinators).

<pre><code class="language-scss">ul.ellist li:nth-last-child(n+4) ~ li {
  // Styles!
}</code></pre>

The problem is that this doesn’t select the first child element. We can append another selector to do that:

<pre><code class="language-scss">ul.ellist li:nth-last-child(n+4) ~ li,
ul.ellist li:nth-last-child(n+4):first-child {
  // Styles!
}</code></pre>

Of course, we can make the selector more agnostic simply by supplying the parent element and letting it choose all of the children. We do this with the `*` selector.

<pre><code class="language-scss">element &gt; *:nth-last-child(n+4) ~ *,
element *:nth-last-child(n+4):first-child {
  // Styles!
}</code></pre>

## Ordering Based On Quantity

Now that we have explored how to count with CSS selectors and how to use flexbox to order content, let’s mix them together to build a tool that orders elements based on the number of siblings.

Again, we’re trying to make our last element be the third element (i.e. appear as the last element in the first row) when there are more than three siblings.

Let’s apply some CSS for some presentational styling. We’ll apply `display: flex` to the parent container, which allows us to apply the `order` property on the child elements. As well, we’ll apply some default styling to the `.target` element to differentiate it.

<pre><code class="language-scss">ul.ellist {
  margin: 20px 0;
  padding: 0;
  list-style: none;
  display: flex;
  flex-flow: row wrap;
}
ul.ellist &gt; * {
  border: 10px solid #27ae60;
  text-align: center;
  flex: 1 0 calc(33.33% - 20px);
  padding: 20px;
  margin: 10px;
}
.target {
  color: white;
  background: #2980b9;
  border: 10px solid #3498db;
}
ul.ellist, ul.ellist &gt; * {
  box-sizing: border-box;
}
ul.ellist {
  margin: 20px 0;
  padding: 0;
  list-style: none;
  display: flex;
  flex-flow: row wrap;
}
ul.ellist &gt; * {
  border: 10px solid #27ae60;
  text-align: center;
  flex: 1 0 calc(33.33% - 20px);
  padding: 20px;
  margin: 10px;
}
ul.ellist .target {
  color: white;
  background: #2980b9;
  border: 10px solid #3498db;
}</code></pre>

Now that we have a base style to work with, we can create some logic to order our items accordingly. Again, by default, all elements have an `order` value of `1` and are displayed according to the order in which they appear in the markup.

Using a quantity query, we can count whether there are more than three items.

<pre><code class="language-scss">ul.ellist &gt; *:nth-last-child(n+3) {
  // Styles!
}</code></pre>

We can then modify our query to select the `.target` element only if the number of items is met. For now, we’ll apply an `order` of `-1`, so that it appears at the beginning of our list.

<pre><code class="language-scss">ul.ellist &gt; *:nth-last-child(n+3) ~ .target {
  order: -1;
}</code></pre>

Voilà! We’ve just styled an element based on the numbers of siblings it has. Using this code, we can put one element in front of another.

But what if it needs to go between items?

### Some Logical Thinking

Here is the problem, in three arguments:

*   By default, all items have an `order` set to `1`. We need the items at the beginning of the list to keep that `order` value.
*   Our target will be presented at the end of the first row. So, we need the target’s `order` value to be higher than the ones in the beginning — i.e. `2`.
*   We need all items from three onward to have a higher `order` than our target and lead elements. So, they will have an `order` value of `3`.

How about this?

Because all items have a default value of `1`, we don’t need to declare that. Let’s allow our target element to have an `order` value of `2` via our quantity query, effectively placing it higher than the others.

<pre><code class="language-scss">ul.ellist &gt; *:nth-last-child(n+3) ~ .target {
  order: 2;
}</code></pre>

Then, using another quantity query that utilizes `nth-child()`, we will **count from the beginning of the list**, rather than from the end. Because our `.target` quantity query is more specific, the last element will be ignored, but all others three and higher will have their order changed.

<pre><code class="language-scss">ul.ellist &gt; *:nth-last-child(n+3) ~ .target {
  order: 2;
}
ul.ellist &gt; *:nth-child(n+3) {
  order: 3;
}</code></pre>

## Whoa! Let’s Go Over That Again

We counted from the end of a parent element if there were a number of child elements. If there were, we applied some styles to an element of our choice. We then counted from the beginning and applied styles to all elements past that point.

The beautiful part is that if we were to remove elements, the target element would still appear in the correct position.

<pre><code class="language-markup">&lt;ul class=&quot;ellist&quot;&gt;
  &lt;li&gt;1&lt;/li&gt;
  &lt;li&gt;2&lt;/li&gt;
  &lt;li&gt;3&lt;/li&gt;
  &lt;li class=&quot;target&quot;&gt;4&lt;/li&gt;
&lt;/ul&gt;</code></pre>

## The Resulting Task

My first thought when given this task was to use a programming language. Because the website was built on WordPress, I could modify “the loop” to count and inject the element where needed.

However, because I’m building the website for a front-end development school, I wanted to do it with pure CSS and explore the possibilities that flexbox’s `order` allows.

Below is an example of the resulting page, done entirely with CSS.

See the Pen [Quantity Ordering](https://codepen.io/drewminns/pen/waarLQ/) by Drew Minns ([@drewminns](https://codepen.io/drewminns)) on [CodePen](https://codepen.io).</p>

## Using It In The Real World

### Sass

Quantity queries are a fairly new concept, and writing the selectors can be a bit of a challenge. Nevertheless, the community is embracing the concept and is building tools and writing Sass mixins that can help us write queries effectively. Libraries such as the one by [Daniel Guillan](https://www.danielguillan.com/), called a [Quantity Queries Mixin](https://github.com/danielguillan/quantity-queries), enable us to write media queries as simple includes.

<pre><code class="language-scss">@include at-least($count) { … }</code></pre>

<pre><code class="language-scss">@include between($first, $last) { … }</code></pre>

A plethora of articles also explain the concept and power behind this. [James Steinbach](https://jamessteinbach.com/) wrote a great article on “[Using Sass for Quantity Queries](https://www.sitepoint.com/using-sass-quantity-queries/).”

### PostCSS

PostCSS is a new tool that allows CSS to be transformed with JavaScript. The current PostCSS ecosystem includes many community-developed plugins, including a [Quantity Query](https://github.com/pascalduez/postcss-quantity-queries) plugin.

The plugin allows for custom pseudo-selectors to target values within a certain range, at least, or at most.

<pre><code class="language-scss">
p:at-least(4) { … }

p:between(4,6) { … }
</code></pre>

### Browser Support

Currently, support for both CSS pseudo-selectors and [flexbox](https://caniuse.com/#search=flexbox) is great in modern browsers. If your project targets users on IE 10 and above, **you can use quantity queries and flexbox ordering together**.</p>

### Where to Use It

When building websites, we often use programming languages that allow us to count and modify our content as needed. However, as CSS has improved, we’ve moved away from programming languages into advanced CSS properties.

One example is CSS animations. What was previously possible only through Flash or JavaScript is now achievable with pure CSS, a language for defining the presentation of our content.

Quantity ordering enables us to **remove modified loops** that count and insert content accordingly, allowing our content to be read semantically.

A great example of the usefulness of quantity ordering would be a news website with advertising. In the markup, all articles are organized together, and the ads are placed at the end. In terms of accessibility, this allows for an uninterrupted flow of content. The ads can then be placed throughout the content, using quantity ordering only on a presentational layer.

See the Pen [vOLGPg](https://codepen.io/drewminns/pen/vOLGPg/) by Drew Minns ([@drewminns](https://codepen.io/drewminns)) on [CodePen](https://codepen.io).

While ordering can be used to change the presentational display of elements, for accessibility, it can damage the experience. Be aware of how content flows and how it will be read on accessibility devices.</p>

## Conclusion

Quantity queries and quantity ordering are advanced concepts and might be scary for beginners. However, as we move presentational styling away from programming languages and into CSS, we should use these tools more and more.

Even as many members of our industry explore [content queries](https://github.com/marcj/css-element-queries), we can now use quantity queries to modify the order of content simply by counting.

_Excerpt image: [Markus Spiske](https://www.flickr.com/photos/markusspiske/18544440564/in/album-72157644611527928/)_

{{< signature "ds, ml, al" >}}


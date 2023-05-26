---
title: Constructing CSS Quantity Queries On The Fly
slug: constructing-css-quantity-queries-on-the-fly
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fd1ff7e-c481-43ed-a950-df649550d1a2/fig2-squid.png'
date: 2015-07-29T22:16:01.000Z
author: drewminns
description: >-
  Often within a project, the presentation of our content changes based on
  certain needs. We see this when we use media queries to change our styles
  based on the user device. [CSS quantity
  queries](https://www.smashingmagazine.com/2015/07/quantity-ordering-with-css/)
  follow the same concept of changing the styles based on a condition: the
  condition within a quantity query being the number of sibling elements.

  An example would be navigation where items are 25% wide when four items are
  available; yet when there are five items available, the width of the
  navigation items changes to 20%. This is a common problem with dynamic site
  frameworks like WordPress or Ghost. A client might not realize the
  complications that could arise, for example, by adding one more menu item when
  the CSS is not set up to fit it in.
categories:
  - Tools
  - CSS
  - Techniques
---
Often within a project, the presentation of our content changes based on certain needs. We see this when we use media queries to change our styles based on the user device. <a href="https://www.smashingmagazine.com/2015/07/quantity-ordering-with-css/">CSS quantity queries</a> follow the same concept of changing the styles based on a condition: the condition within a quantity query being the number of sibling elements.

An example would be navigation where items are 25% wide when four items are available; yet when there are five items available, the width of the navigation items changes to 20%. This is a common problem with dynamic site frameworks like WordPress or Ghost.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [It’s Time To Start Using CSS Custom Properties](https://www.smashingmagazine.com/2017/04/start-using-css-custom-properties/)
*   [Quantity Ordering With CSS](https://www.smashingmagazine.com/2015/07/quantity-ordering-with-css/)
*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [Truly Fluid Typography With vh And vw Units](https://www.smashingmagazine.com/2016/05/fluid-typography/)

A client might not realize the complications that could arise, for example, by adding one more menu item when the CSS is not set up to fit it in. Now, <a href="https://www.smashingmagazine.com/2015/03/harnessing-flexbox-for-todays-web-apps/">you could easily solve this problem with Flexbox</a> (and <a href="https://flexbox.io/">many other problems</a>), but what about a smart fallback for browsers not supporting Flexbox — preferably with CSS alone, without JavaScript altogether? Ideally, we could use <a href="https://caniuse.com/#search=supports">@supports</a> — but you can probably guess which browsers don't support the property.

{{% feature-panel %}}

<figure><a href="https://alistapart.com/article/quantity-queries-for-css"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fd1ff7e-c481-43ed-a950-df649550d1a2/fig2-squid.png" /></a><figcaption>You must have run into this problem in the past: you have a dynamic number of siblings, and you need to style them differently, based on the total count of siblings. It can be solved, easily, with CSS quantity queries. Image source: <a href="https://alistapart.com/article/quantity-queries-for-css">Quantity Queries on ALA</a>.</figcaption></figure>

Sometimes Flexbox won't cut it though. What if you are designing a gallery with an uneven number of items and you'd like to highlight the image in the center without tracking with JavaScript how many items fit the screen? Or what about a table in which some columns might need different styling based on how many items can be displayed at a given resolution — e.g. in an airline flight selection, or cinema tickets reservation?

The same goes for pretty much every module that could suffer from some dynamic addition or subtraction of elements. Can you <strong>avoid too many media queries and JavaScript workarounds</strong>?

Yes, you can. This is where quantity queries are best used. By being creative with CSS selectors, we can <strong>count the number of sibling items</strong> and apply styles if they meet the conditions. Using these queries, we can future-proof our designs and projects, and allow them to scale gracefully.</p>

## An Example Of A Quantity Query

Using CSS selectors like <code>nth-last-child()</code>, <code>last-child</code> and <code>~</code>, we can craft selectors that match our requirements. If you’re interested in reading more about how they work, Lea Verou, Heydon Pickering and myself <a href="https://lea.verou.me/2011/01/styling-children-based-on-their-number-with-css3/">have</a> <a href="https://alistapart.com/article/quantity-queries-for-css">written</a> <a href="https://www.smashingmagazine.com/2015/07/quantity-ordering-with-css/">articles</a> on the subject.

Here's an example of a quantity query that will apply styles if there are <strong>at least</strong> five sibling elements:

<pre><code class="language-scss">
ul li:nth-last-child(n+5), ul li:nth-last-child(n+5) ~ li {
  // styles go here
}
</code></pre>

We can take this further and change the query to select all sibling elements <strong>up to</strong> a certain amount:

<pre><code class="language-scss">
ul li:nth-last-child(-n+5):first-child, ul li:nth-last-child(-n+5):first-child ~ li {
  // styles go here 
}
</code></pre>

Extending further still, we can set boundaries and apply styles if the sibling items are within a certain range.</p>

<pre><code class="language-scss">
ul li:nth-last-child(n+5):nth-last-child(-n+10):first-child, ul li:nth-last-child(-n+5):nth-last-child(-n+10):first-child ~ li {
  // styles go here
}
</code></pre>

## A Solution To Writing Quantity Queries

As you can see, these queries can be a bit verbose and difficult to write. This is why I created <a href="https://quantityqueries.com">QuantityQueries.com</a>: a tool I needed to help construct and demonstrate quantity queries for my own projects.

<figure><a href="https://quantityqueries.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a77b3889-e9e9-445e-a893-90a9eed31d56/qq-tool-opt.png" alt="QuantityQueries.com" /></a><figcaption>Building quantity queries at <a href="https://quantityqueries.com">QuantityQueries.com</a> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac2e7dcf-f00d-4f8b-baf4-431eccd1e795/qq-largeimage-opt.jpg">View larger screenshot</a>)</figcaption></figure>

Written as an experiment with <a href="https://facebook.github.io/react/">React</a>, the project evolved into a dynamic tool for our web design community to use and understand how best to apply these quantity queries.

The app allows a query to be built through three questions: the elements to be counted, the type of query, and the amount of items to count. Based on the questions, a CSS selector is created that can be used within your project, as well as a small demo that will react to your query.

Within the demo, as items are added or removed, the colour of the items will change to pink to reflect the query being applied to the demo.</p>

<figure><a href="https://quantityqueries.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7044e9bb-9000-46da-b55b-5c5193d8008e/qq-demoimage-opt-small.jpg" alt="qq_demoImage-opt-small" /></a><figcaption>A demo in action. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dda79dd1-576a-4faa-88d2-43d4f00c2e71/qq-demoimage-opt.jpg">View large version</a>)</figcaption></figure>

## "But I Have To Support Browser X…"

Quantity queries are constructed using modern CSS properties to perform the selection. They will work in all modern browsers (both desktop and mobile, including Opera Mini 8), back to IE9. Selectors such as <code>nth-last-child()</code>, <code>~</code> and <code>last-child</code> were introduced in CSS3, and <code>first-child</code> was introduced by CSS2.1. Obviously you can treat them as progressive enhancement, but if you absolutely have to support legacy browsers, you can use <a href="https://selectivizr.com/">Selectivizr</a> and <a href="https://modernizr.com/">Modernizr</a>.</p>

## Using It Today

Feel free to bookmark the site and keep it handy in your toolbelt. Each project has different requirements and will need to be tailored to client needs, but the tool might come in handy when you need a quite complex selector and don't want to spend hours figuring out the math. You can also use Lea Verou's <a href="https://lea.verou.me/demos/nth.html">CSS3 structural pseudo-class selector tester</a>, CSS Tricks' <a href="https://css-tricks.com/examples/nth-child-tester/">:nth tester</a> and <a href="https://nth-test.com/">nth-test</a> for testing.

If you would like to help improve the tool or you discover any bugs, you can <a href="https://github.com/drewminns/qqui">help improve</a> the app, or report any <a href="https://github.com/drewminns/qqui/issues">issues</a>. I hope that the project will be helpful for your projects!

{{< signature "og" >}}


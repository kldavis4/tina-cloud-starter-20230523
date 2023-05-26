---
title: 'Helping Browsers Optimize With The CSS Contain Property'
slug: browsers-containment-css-contain-property
author: rachel-andrew
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46f0a462-6a6f-4620-a7fc-e02cbf97f4d6/browsers-containment-css-contain-property.png
date: 2019-12-27T12:00:00.000Z
summary: >-
  The CSS <code>contain</code> property gives you a way to explain your layout to the browser, so performance optimizations can be made. However, it does come with some side effects in terms of your layout.
description: >-
  The CSS <code>contain</code> property gives you a way to explain your layout to the browser, so performance optimizations can be made. However, it does come with some side effects in terms of your layout.
categories:
  - CSS
  - Browsers
---

In this article, I’m going to introduce a CSS Specification that has just become a W3C Recommendation. The CSS Containment Specification defines a single property, `contain`, and it can help you to explain to the browser which parts of your layout are independent and will not need recalculating if some other part of the layout changes.

While this property exists for performance optimization reasons, it can also affect the layout of your page. Therefore, in this article, I’ll explain the different types of containment you can benefit from, but also the things you need to watch out for if applying `contain` to elements in your site.

## The Problem Of Layout Recalculation

If you are building straightforward web pages that do not dynamically add or change elements after they have loaded using JavaScript, you don’t need to worry about the problem that CSS Containment solves. The browser only needs to calculate your layout once, as the page is loaded.

Where Containment becomes useful is when you want to add elements to your page without the user needing to reload it. In my example, I created a big list of events. If you click the button, the first event is modified, a floated element is added, and the text is changed:

{{< rimg href="https://codepen.io/rachelandrew/pen/ExxzNNo" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/637f90a5-4a8f-4d1f-b70b-3be602eef26a/listing.png" sizes="100vw" caption="(<a href='https://codepen.io/rachelandrew/pen/ExxzNNo'>See the initial example on CodePen</a>)" alt="A listing of items with a button to change some of the content in the first item" >}}

When the content of our box is changed, the browser has to consider that any of the elements may have changed. Browsers are in general pretty good at dealing with this, as it’s a common thing to happen. That said, as the developer, you will know if each of the components is independent, and that a change to one doesn’t affect the others, so it would be nice if you could let the browser know this via your CSS. This is what containment and the CSS `contain` property gives you.

{{% feature-panel %}}

## How Does Containment Help?

An HTML document is a tree structure which you can see when inspecting any element with DevTools. In my example above, I identify one item that I want to change by using JavaScript, and then make some changes to the internals. (This means that I’m only changing things inside the subtree for that list item.)

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40815082-053d-4e77-abfc-539ce7707bde/tree.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e984684-cc33-45bd-8669-d9f5c98288d7/example-contain-css-tree-code.png" sizes="100vw" caption="Inspecting a list item in DevTools" alt="DevTools with the list item of the featured item expanded to see the elements inside" >}}

Applying the `contain` property to an element tells the browser that changes are scoped to the subtree of that element, so that the browser can do any possible optimizations &mdash; safe in the knowledge that nothing else outside of that element will change. Exactly what a particular browser might do is down to the engine. The CSS property simply gives you &mdash; as the developer and expert on this layout &mdash; the chance to let it know.

In many cases, you will be safe to go right ahead and start using the `contain` property, however, the different values come with some potential side effects which are worth understanding before adding the property to elements in your site.

## Using Containment

The `contain` property can set three different types of containment:

- `layout`
- `paint`
- `size`

**Note**: *There is a `style` value in the Level 2 Specification. It was removed from Level 1, so does not appear in the Recommendation, and is not implemented in Firefox.*

### Layout

Layout containment brings the biggest benefits. To turn on layout containment, use the following snippet:

<pre><code class="language-css">.item {
  contain: layout;
}
</code></pre>

With layout containment enabled, the browser knows that nothing outside the element can affect the internal layout, and nothing from inside the element can change anything about the layout of things outside it. This means that it can make any possible optimizations for this scenario.

A few additional things happen when layout containment is enabled. These are all things which ensure that this box and contents are independent of the rest of the tree.

The box establishes an *independent formatting context*. This ensures that the content of the box stays in the box &mdash; in particular floats will be contained and margins will not collapse through the box. This is the same behavior that we switch on when we use `display: flow-root` as in explained in my article “[Understanding CSS Layout And The Block Formatting Context](https://www.smashingmagazine.com/2017/12/understanding-css-layout-block-formatting-context/)”. If a float could poke out of your box, causing following text to flow around the float, that would be a situation where the element _was_ changing the layout of things outside it, making it a poor candidate for containment.

{{% ad-panel-leaderboard %}}

The containing box acts as the containing block for any absolutely or fixed position descendants. This means it will act as if you had used `position: relative` on the box you have applied `contain: layout`.

The box also creates a *stacking context*. Therefore `z-index` will work on this element, it’s children will be stacked based on this new context.

If we look at the example, this time with `contain: layout`, you can see that when the floated element is introduced it no longer pokes out the bottom of the box. This is our new Block Formatting Context in action, containing the float.

{{< rimg breakout="true" href="https://codepen.io/rachelandrew/pen/abzwRmR" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a346dd96-1d43-4d53-ad5b-97315973242c/layout-containment.png" sizes="100vw" caption="Using contain: layout the float is contained (<a href='https://codepen.io/rachelandrew/pen/abzwRmR'>See the layout containment example on CodePen</a>)" alt="A listing of items, a floated element is contained inside the bounds of the parent box" >}}

### Paint

To turn on paint containment, use the following:

<pre><code class="language-css">.item {
  contain: paint;
}
</code></pre>

With paint containment enabled, the same side effects as seen with layout containment occur: The containing box becoming an independent formatting context, a containing block for positioned elements, and establishing a stacking context.

What paint containment does is indicate to the browser that elements inside the containing block will not be visible outside of the bounds of that box. The content will essentially be clipped to the box.

We can see this happen with a simple example. Even if we give our card a height, the floated item still pokes out the bottom of the box, due to the fact that the float is taken out of flow.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdefa989-1011-40e9-a35c-d05c2227a92d/paint-containment-off.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdefa989-1011-40e9-a35c-d05c2227a92d/paint-containment-off.png" sizes="100vw" caption="The float is not contained by the list item" alt="A floated box poking out the bottom of a containing box" >}}

With paint containment turned on the floated item is now clipped to the size of the box. Nothing can be painted outside of the bounds of the element with `contain: paint` applied.

{{< rimg breakout="true" href="https://codepen.io/rachelandrew/pen/ZEYyqBr" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fc4aece-1f8e-47c2-a30f-0a821a000b5d/paint-containment.png" sizes="100vw" caption="The content of the box is clipped to the height of the box (<a href='https://codepen.io/rachelandrew/pen/ZEYyqBr'>See the paint example on CodePen</a>)" alt="A box with a floated box inside which has been cut off where it escapes the box" >}}

## Size

Size containment is the value that is most likely to cause you a problem if you aren’t fully aware of how it works. To apply size containment, use:

<pre><code class="language-css">.item {
  contain: size;
}
</code></pre>

If you use size containment then you are telling the browser that you know the size of the box and it is not going to change. This does mean that if you have a box which is auto-sized in the block dimension, it will be treated as if the content has no size, therefore the box will collapse down as if it had no contents.

In the example below, I have not given the `li` a height; they also have `contain: size` applied. You can see that all of the items have collapsed as if they had no content at all, making for a very peculiar looking listing!

{{< rimg breakout="true" href="https://codepen.io/rachelandrew/pen/oNgwaBR" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3686d32-ae9a-4ebb-ae12-35db37fd82a8/size-containment.png" sizes="100vw" caption="(<a href='https://codepen.io/rachelandrew/pen/oNgwaBR'>See the size example on CodePen</a>)" alt="A listing of items with a button to change some of the content in the first item" >}}

If you give the boxes a height then the height will be respected when `contain: size` is used. Alone, size containment will not create a new formatting context and therefore does not contain floats and margins as layout and paint containment will do. It’s less likely that you would use it alone; instead, it is most likely you would apply it along with other values of `contain` to be able to get the most possible containment.

{{% ad-panel-leaderboard %}}

## Shorthand Values

In most cases, you can use one of two shorthand values to get the best out of containment. To turn on layout and paint containment, use `contain: content;`, and to turn on all possible containment (keeping in mind that items which do not have a size will then collapse), use `contain: strict`.

[The Specification says](https://www.w3.org/TR/css-contain-1/#valdef-contain-content):

<blockquote>“<code>contain: content</code> is reasonably "safe" to apply widely; its effects are fairly minor in practice, and most content won’t run afoul of its restrictions. However, because it doesn’t apply size containment, the element can still respond to the size of its contents, which can cause layout-invalidation to percolate further up the tree than desired. Use <code>contain: strict</code> when possible, to gain as much containment as you can.”</blockquote>

Therefore, if you do not know the size of the items in advance, and understand the fact that floats and margins will be contained,  use `contain: content`. If you do know the size of items in addition to being happy about the other side effects of containment, use `contain: strict`. The rest is down to the browser, you have done your bit by explaining how your layout works.

## Can I Use Containment Now?

The CSS Containment specification is now a W3C Recommendation which is what we sometimes refer to as a *web standard*. In order for the spec to get to this stage, there needed to be two implementations of the feature which we can see in both Firefox and Chrome:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2c98278-ffea-4a72-80bd-8b41b6a913d7/can-i-use-contain.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2c98278-ffea-4a72-80bd-8b41b6a913d7/can-i-use-contain.png" sizes="100vw" caption="Browser support for containment (Source: <a href='https://caniuse.com/#feat=css-containment'>Can I Use</a>)" alt="Screenshot of the browser support information on Containment on Can I Use" >}}

As this property is transparent to the user, it is completely safe to add to any site even if you have lots of visitors in browsers that do not support it. If the browser doesn’t support containment then the visitor gets the experience they usually get, those in supporting browsers get the enhanced performance.

I would suggest that this is a great thing to add to any components you create in a component or pattern library, if you are working in this way it is likely each component is designed to be an independent thing that does not affect other elements on the page, making `contain: content` a useful addition.

Therefore, if you have a page which is adding content to the DOM after load, I would recommend giving it a try &mdash; if you get any interesting results let me know in the comments!

### Related Resources

The following resources will give you some more detail about the implementation of containment and potential performance benefits:

- “[The `contain` CSS Property](https://developer.mozilla.org/en-US/docs/Web/CSS/contain),” *MDN web docs*
- “[CSS Containment In Chrome 52](https://developers.google.com/web/updates/2016/06/css-containment),” *Google Developers*
- “[CSS Containment Module Level 1](https://www.w3.org/TR/css-contain-1/),” *W3C Recommendation*
- “[An Introduction To CSS Containment](https://blogs.igalia.com/mrego/2019/01/11/an-introduction-to-css-containment/),” *Manuel Rego Casasnovas*

{{< signature "il" >}}

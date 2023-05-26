---
title: 'Managing SVG Interaction With The Pointer Events Property'
slug: svg-interaction-pointer-events-property
author: tiffany-brown
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c6ca644-9b42-4548-9180-c9f3a5c0170a/pointer-events-property-featured-image.png
date: 2018-05-16T14:15:25+02:00
summary: >
  Let’s take a look at how to shape the interactivity of SVG images &mdash; that is, control which parts of the document can receive clicks, touches, or taps &mdash; using the `pointer-events` property.
description: >
  Let’s take a look at how to shape the interactivity of SVG images &mdash; that is, control which parts of the document can receive clicks, touches, or taps &mdash; using the `pointer-events` property.
categories:
  - CSS
  - SVG
  - User Interaction
---
<p>Try clicking or tapping the SVG image below. If you put your pointer in the right place (the shaded path) then you should have Smashing Magazine’s homepage open in a new browser tab. If you tried to click on some white space, you might be really confused instead.</p>

{{< codepen height="480" theme_id="light" slug_hash="XEeMKd" default_tab="result" user="Yakudoo" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/webinista/pen/XEeMKd/">Amethyst</a> by Tiffany Brown (<a href="https://codepen.io/webinista">@webinista</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

This is the dilemma I faced during a recent project that included links within SVG images. Sometimes when I clicked the image, the link worked. Other times it didn't. Confusing, right?

I turned to the SVG [specification](https://www.w3.org/TR/SVG2/) to learn more about what might be happening and whether SVG offers a fix. The answer: `pointer-events`.

{{% feature-panel %}}

<p>Not to be confused with DOM (<strong>D</strong>ocument <strong>O</strong>bject <strong>M</strong>odel) <a href="https://w3c.github.io/pointerevents/">pointer events</a>, <code>pointer-events</code> is both a CSS property and an SVG element attribute. With it, we can manage which parts of an SVG document or element can receive events from a pointing device such as a mouse, trackpad, or finger.</p>

<p>A note about terminology: "pointer events" is also the name of a <a href="https://www.w3.org/TR/2015/REC-pointerevents-20150224/">device-agnostic</a>, web platform feature for user input. However, in this article &mdash; and for the purposes of the <code>pointer-events</code> property  &mdash; the phrase "pointer events" also includes mouse and touch events.</p>

## Outside Of The Box: SVG’s "Shape Model"

Using CSS with HTML imposes a [box layout model](https://developer.mozilla.org/en-US/docs/Web/CSS/Visual_formatting_model) on HTML. In the box layout model, every element generates a rectangle around its contents. That rectangle may be inline, inline-level, atomic inline-level, or block, but it’s still a rectangle with four right angles and four edges. When we add a link or an event listener to an element, the interactive area matches the  dimensions of the rectangle.

**Note**: *Adding a `clip-path` to an interactive element alters its interactive bounds. In other words, if you add a hexagonal `clip-path` path to an `a` element, only the points within the clipping path will be clickable. Similarly, adding a skew transformation will turn rectangles into rhomboids.*

SVG does not have a box layout model. You see, when an SVG document is contained by an HTML document, within a CSS layout, the root SVG element adheres to the box layout model. Its child elements do not. As a result, most CSS layout-related properties don’t apply to SVG.

So instead, SVG has what I’ll call a ‘shape model’. When we add a link or an event listener to an SVG document or element, the interactive area will not necessarily be a rectangle. SVG elements _do_ have a [bounding box](https://svgwg.org/svg2-draft/coords.html#BoundingBoxes). The bounding box is defined as: <q>the tightest fitting rectangle aligned with the axes of that element’s user coordinate system that entirely encloses it and its descendants.</q> But initially, which parts of an SVG document are interactive depends on which parts are _visible_ and/or _painted_.

## Painted vs. Visible Elements

SVG elements can be “filled” but they can also be “stroked”. _Fill_ refers to the interior of a shape. _Stroke_ refers to its outline.

Together, “fill” and “stroke” are _painting operations_ that render elements to the screen or page (also known as the _canvas_). When we talk about _painted elements_, we mean that the element has a fill and/or a stroke. Usually, this means the element is also visible.

However, an SVG element can be painted without being visible. This can happen if the ` visible ` attribute value or CSS property is ` hidden ` or when `display` is `none`. The element is there and occupies theoretical space. We just can’t see it (and assistive technology may not detect it). 

Perhaps more confusingly, an element can also be visible &mdash; that is, have a computed `visibility` value of `visible` &mdash; without being painted. This happens when elements lack both a stroke and a fill.

**Note**: *Color values with alpha transparency (e.g. `rgba(0,0,0,0)`) do not affect whether an element is painted or visible. In other words, if an element has an alpha transparent fill or stroke, it’s painted even if it can’t be seen.*

Knowing when an element is painted, visible, or neither is crucial to understanding the impact of each ` pointer-events ` value. 

## All Or None Or Something In Between: The Values

` pointer-events ` is both a CSS property and an SVG element attribute. Its initial value is `auto`, which means that only the painted and visible portions will receive pointer events. Most other values can be split into two groups: 

1. Values that require an element to be visible; and
2. Values that do not.

`painted`, `fill`, `stroke`, and `all` fall into the latter category. Their visibility-dependent counterparts &mdash; `visiblePainted`, `visibleFill`, `visibleStroke` and `visible` &mdash; fall into the former. 

The [SVG 2.0 specification](https://svgwg.org/svg2-draft/interact.html#PointerEventsProp) also defines a `bounding-box` value. When the value of `pointer-events` is `bounding-box`, the rectangular area around the element can also receive pointer events. As of this writing, only Chrome 65+ supports the `bounding-box` value. 

`none` is also a valid value. It prevents the element and its children from receiving any pointer events. The `pointer-events` CSS property can be used with HTML elements too. But when used with HTML, only `auto` and `none` are valid values.

Since `pointer-events` values are better demonstrated than explained, let’s look at some demos. 

Here we have a circle with a fill and a stroke applied. It’s both _painted_ and _visible_. The entire circle can receive pointer events, but the area outside of the circle cannot.

{{< codepen height="480" theme_id="light" slug_hash="xWXqrd" default_tab="result" user="webinista" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/webinista/pen/xWXqrd/">Visible vs painted in SVG</a> by Tiffany Brown (<a href="https://codepen.io/webinista">@webinista</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Disable the fill, so that its value is `none`. Now if you try to hover, click, or tap the interior of the circle, nothing happens. But if you do the same for the stroke area, pointer events are still dispatched. Changing the `fill` value to `none` means that this area _visible_, but not _painted_.

Let’s make a small change to our markup. We'll add `pointer-events="visible"` to our `circle` element, while keeping `fill=none`.

{{< codepen height="480" theme_id="light" slug_hash="dmVWoQ" default_tab="result" user="webinista" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/webinista/pen/dmVWoQ/">How adding pointer-events: all affects interactivity</a> by Tiffany Brown (<a href="https://codepen.io/webinista">@webinista</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Now the unpainted area encircled by the stroke can receive pointer events.

## Augmenting The Clickable Area Of An SVG Image

Let’s return to the image from the beginning of this article. Our "amethyst"  is a `path` element, as opposed to a group of polygons each with a `stroke` and `fill`. That means we can’t just add `pointer-events="all"` and call it a day.

Instead, we need to augment the click area. Let’s use what we know about painted and visible elements. In the example below, I’ve added a rectangle to our image markup.

{{< codepen height="480" theme_id="light" slug_hash="BrwWQv" default_tab="result" user="webinista" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/webinista/pen/BrwWQv/">Augmenting the click area of an SVG image</a> by Tiffany Brown (<a href="https://codepen.io/webinista">@webinista</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Even though this rectangle is unseen, it’s still _technically_ visible (i.e. `visibility: visible`).  Its lack of a fill, however, means that it is not _painted_. Our image looks the same. Indeed it still works the same &mdash; clicking white space still doesn’t trigger a navigation operation. We still need to add a `pointer-events` attribute to our `a` element. Using the `visible` or `all` values will work here.

{{< codepen height="480" theme_id="light" slug_hash="RMLpGy" default_tab="result" user="webinista" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/webinista/pen/RMLpGy/">Augmenting the click area of an SVG image</a> by Tiffany Brown (<a href="https://codepen.io/webinista">@webinista</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Now the entire image can receive pointer events.

Using `bounding-box` would eliminate the need for a phantom element. All points within the bounding box would receive pointer events, including the white space enclosed by the path. But again: `pointer-events="bounding-box"` isn’t widely supported. Until it is, we can use unpainted elements.

## Using `pointer-events` When Mixing SVG And HTML

Another case where `pointer-events` may be helpful: using SVG inside of an HTML button.

{{< codepen height="480" theme_id="light" slug_hash="Ovxmmy" default_tab="result" user="webinista" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/webinista/pen/Ovxmmy/">Ovxmmy</a> by Tiffany Brown (<a href="https://codepen.io/webinista">@webinista</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

In most browsers &mdash; Firefox and Internet Explorer 11 are exceptions here &mdash; the value of `event.target` will be an SVG element instead of our HTML button. Let’s add `pointer-events="none"` to our opening SVG tag. 

{{< codepen height="480" theme_id="light" slug_hash="KoXmqm" default_tab="result" user="webinista" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/webinista/pen/KoXmqm/">How pointer-events: none can be used with SVG and HTML</a> by Tiffany Brown (<a href="https://codepen.io/webinista">@webinista</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Now when users click or tap our button, the `event.target`  will refer to our `button`.

Those well-versed in the DOM and JavaScript will note that using the `function` keyword instead of an arrow function and `this` instead of `event.target` fixes this problem. Using `pointer-events="none"` (or `pointer-events: none;` in your CSS), however, means that you don’t have to commit that particular JavaScript quirk to memory.

## Conclusion

SVG supports the same kind of interactivity we're used to with HTML. We can use it to create charts that respond to clicks or taps. We can create linked areas that don’t adhere to the CSS and HTML box model. And with the addition of `pointer-events`, we can improve the way our SVG documents behave in response to user interaction. 

Browser support for SVG `pointer-events` is robust. Every browser that supports SVG supports the property for SVG documents and elements. When used with [HTML elements](https://caniuse.com/#search=pointer-events), support is slightly less robust.  It isn’t available in Internet Explorer 10 or its predecessors, or any version of Opera Mini.

We’ve just scratched the surface of `pointer-events ` in this piece. For a more in-depth,  technical treatment, read through the [SVG Specification](https://www.w3.org/TR/SVG2/interact.html#PointerEventsProp). MDN (Mozilla Developer Network) Web Docs offers more web developer-friendly documentation for [`pointer-events`](https://developer.mozilla.org/en-US/docs/Web/CSS/pointer-events), complete with examples.

{{< signature "rb, ra, yk, il" >}}


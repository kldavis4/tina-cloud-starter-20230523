---
title: 'Take A New Look At CSS Shapes'
slug: css-shapes
author: rachel-andrew
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90f7d3f4-6b28-46ad-bae7-b9d4ad6172e8/rachel-css-shapes.png
date: 2018-09-04T13:30:57+02:00
summary: >
   In this article, we take a look at CSS Shapes and how to create non-rectangular shapes using images, gradients, and basic shapes. We also discover how the new tools in Firefox make editing shapes easier.
description: >
   In this article, we take a look at CSS Shapes and how to create non-rectangular shapes using images, gradients, and basic shapes. We also discover how the new tools in Firefox make editing shapes easier.
categories:
  - CSS
---
CSS Shapes Level 1 has been available in Chrome and Safari for a number of years, however, this week it ships in a production version of Firefox with the release of Firefox 62 &mdash; along with a very nice addition to the Firefox DevTools to help us work with Shapes. In this article, I'll take a look at some of the things you can do with CSS Shapes. Perhaps it's time to consider adding some curves to your designs?

## What Are CSS Shapes?

The CSS Shapes specification Level 1 defines three new properties:

- `shape-outside`
- `shape-image-threshold`
- `shape-margin`

The purpose of this specification is to allow content to flow around a non-rectangular shape, something which is quite unusual on our boxy web. There are a few different ways to create shapes, which we will have a look at in this tutorial. We will also have a look at the Shape Path Editor, available in Firefox, as it can help you to easily understand the shapes on your page and work with them.

In the current specification, shapes can only be applied to a float, so any shapes example needs to start with a floated element. In the example below, I have a PNG image with a transparent background in which I have floated the image left. The text that follows the image now flows around the right and bottom of my image.

What I would like to happen is for my content to follow the shape of the opaque part of the image, rather than follow the line of the physical image file. To do this, I use the `shape-outside` property, with the value being the URL of my image. I'm using the actual image file to create a path for the content to flow around.

{{< codepen height="480" theme_id="light" slug_hash="KxaZXw" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/KxaZXw">Smashing Shapes: image</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Note that your image needs to be CORS compatible, so hosted on the same server as the rest of your content or sending the correct headers if hosted on a CDN. Browser DevTools will usually tell you if your image is being blocked due to CORS.

This method of creating shapes uses the alpha channel of the image to create the shape, as we have a shape with a fully transparent area, then all we need do is pass the URL of the image to `shape-outside` and the shape path follows the line of the fully opaque area.

{{% feature-panel %}}

## Creating A Margin

To push the line of the text away from the image we can use the `shape-margin` property. This creates a margin between the line of the shape and the content running alongside it.

{{< codepen height="480" theme_id="light" slug_hash="vzgdXw" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/vzgdXw">Smashing Shapes: shape-margin</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## Using Generated Content For Our Shape

In the case above, we have the image displayed on the page and then the text curved around it. However, you could also use an image as the path for the shape in order to create a curved text effect without also including the image on the page. You still need something to float, however, and so for this, we can use Generated Content.

{{< codepen height="480" theme_id="light" slug_hash="bxgLBp" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/bxgLBp">Smashing Shapes: generated content</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

In this example, we have inserted some generated content, floated it left, given it a width and a height and then used `shape-outside` with our image just as before. We then get a curved line against the whitespace, but no visible image.

## Using A Gradient For Our Shape

A CSS gradient is just like an image, which means we can use a gradient to create a shape, which can make for some interesting effects. In this next example, I have created a gradient which goes from blue to transparent; your gradient will need to have a transparent or semi-transparent area in order to use shapes. Once again, I have used generated content to add the gradient and am then using the gradient in the value for `shape-outside`.

Once the gradient becomes fully transparent, then the shape comes into play, and the content runs along the edge of the gradient.

{{< codepen height="480" theme_id="light" slug_hash="zJNRpL" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/zJNRpL">Smashing Shapes: gradients</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## Using `shape-image-threshold` To Position Text Over A Semi-Opaque Image

So far we have looked at using a completely transparent part of an image or of a gradient in order to create our shape, however, the third property defined in the CSS Shapes specification means that we can use images or gradients with semi-opaque areas by setting a threshold. A value for `shape-image-threshold` of `1` means fully opaque while `0` means fully transparent.

A gradient like our example above is a great way to see this in action as we can change the `shape-image-threshold` value and move the line along which the text falls to more opaque areas or more transparent areas. This property works in exactly the same way with an image that has an alpha channel yet is not fully transparent.

{{< codepen height="480" theme_id="light" slug_hash="JaEpMw" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/JaEpMw">Smashing Shapes: shape-image-threshold</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

This method of creating shapes from images and gradients is &mdash; I think &mdash; the most straightforward way of creating a shape. You can create a shape as complex as you need it to be, in the comfort of a graphics application and then use that to define the shape on your page. That said, there is another way to create our shapes, and that's by using _Basic Shapes_.

{{% ad-panel-leaderboard %}}

## CSS Shapes With Basic Shapes

The Basic Shapes are a set of predefined shapes which cover a lot of different types of shapes you might want to create. To use a basic shape, you use the basic shape _type_ as a value for `shape-outside`. This type uses functional notation, so we have the name of the shape followed by brackets (inside which are some values for our shape).

The options that you have are the following:

- `inset()`
- `circle()`
- `ellipse()`
- `polygon()`

We will take a look at the `circle()` type first as we can use this to understand some useful things which apply to all shapes which use the basic shape type. We will also have a look at the new tools in Firefox for inspecting these shapes.

In the example below, I am creating the most simple of shapes: a circle using `shape-outside: circle(50%)`. I'm using generated content again, and I have given the box a background color, and also added a margin, border, and padding to help highlight some of the concepts of using CSS Shapes. You can see in the example that the circle is created centered on the box; this is because I have given the circle a value of 50%. That value is the `<shape-radius>` which can be a length or a percentage. I've used a percentage so that the radius is half of the size of my box.

{{< codepen height="480" theme_id="light" slug_hash="dqNmvM" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/dqNmvM">Smashing Shapes: shape-outside: circle()</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

This is a really good to time have a look at the shape that has been created using the Firefox Shape Path Editor. You can inspect the shape by clicking on the generated content and then clicking the little shape icon next to the property `shape-outside`; your shape will now highlight.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ada6850-25be-4c76-b403-4a0c7e367bc4/circle.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ada6850-25be-4c76-b403-4a0c7e367bc4/circle.png" sizes="100vw" caption="The Shape Path Editor highlights the circle shape (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ada6850-25be-4c76-b403-4a0c7e367bc4/circle.png'>Large preview</a>)" alt="The shape highlighted with a line" >}}

You can see how the circle extends to the edge of the margin on our box. This is because the initial _reference box_ used by our shape is `margin-box`. You already know something of reference boxes if you have ever added `box-sizing: border-box` to your CSS. When you do this, you are asking CSS to use the `border-box` and not the default `content-box` as the size of elements. In Shapes, we can also change which reference box is used. After any basic shape, add `border-box` to use the border to define the shape or `content-box` to use the edge of the content (inside the padding). For example:

<div class="break-out">

<pre><code class="language-css">.content::before {
    content: "";
    width: 150px;
    height: 150px;
    margin: 20px;
    padding: 20px;
    border: 10px solid #FC466B;
    background: linear-gradient(90deg, #FC466B 0%, #3F5EFB 100%);
    float: left;
    circle(50%) content-box;
}
</code></pre></div>

You will see the circle appear to become much smaller. It is now using the width of the content &mdash; in this case the width of the box at 150px &mdash; rather than the margin box which includes the padding, border, and margin.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cd0eefa-4cc2-4721-873b-6933a9643770/content-box.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cd0eefa-4cc2-4721-873b-6933a9643770/content-box.png" sizes="100vw" caption="The content-box is the edge of the content of the square we created with our generated content (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cd0eefa-4cc2-4721-873b-6933a9643770/content-box.png'>Large preview</a>)" alt="A smaller circle is highlighted" >}}

Inspecting your element in Firefox DevTools will also show you the reference boxes so you can choose which might give you the best result with your particular shape.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89137819-2571-4164-8133-48e42f55f153/reference-boxes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89137819-2571-4164-8133-48e42f55f153/reference-boxes.png" sizes="100vw" caption="Reference boxes highlighted in Firefox (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89137819-2571-4164-8133-48e42f55f153/reference-boxes.png'>Large preview</a>)" alt="Highlights showing the margin, border and padding" >}}

#### The Position Value

A second value can be passed to `circle()` which is a position; if you do not pass this value, it defaults to `center`. However, you can use this value to pull your circle around. In the next example, I have positioned the circle by using `shape-outside(50% at 30%)`; this changes where the center of the circle is positioned.

{{< codepen height="480" theme_id="light" slug_hash="rZjvJW" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/rZjvJW">Smashing Shapes: circle() with position</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

#### `clip-path`

Something useful to know is that the same `<basic-shape>` values can be used as a value for `clip-path`. This means that after creating a shape, you can clip away the image or background color that extends outside of the shape. In the example below, I am going to do this with our example gradient background, so that we end up with a circle that has text curved around from our square box.

{{< codepen height="480" theme_id="light" slug_hash="dqNeJm" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/dqNeJm">Smashing SHapes: circle() with clip-path</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

All of the above concepts can be applied to our other basic shapes. Now let's have a quick look at how they work.

{{% ad-panel-leaderboard %}}

### inset()

The `inset()` value defines a rectangle. This might not seem very useful as a float is a rectangle, however, this value means that you can inset the content wrapping your shape. It takes four values for top, right, bottom, and left plus a final value which defines a border radius.

In the example below, I am using the values to inset the content on the right and bottom of the floated image, plus adding a border radius around which my content will wrap using `shape-outside: inset(0 30px 100px 0 round 40px) `. You can see how the content is now over the background color of the box:

{{< codepen height="480" theme_id="light" slug_hash="PdWaPY" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/PdWaPY">Smashing Shapes: inset()</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### ellipse()

An ellipse is a squashed circle and as such needs two radii for x and y (in that order). You can then push the ellipse around just as with circle using the position value. In the example below, I am creating an ellipse and then using clip-path with the same values to remove the content outside of my shape.

{{< codepen height="480" theme_id="light" slug_hash="bxgKwE" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/bxgKwE">Smashing Shapes: ellipse()</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

In the above example, I also used `shape-margin` to demonstrate how we can use this property as with our image generated shapes to push the content away.

### polygon()

Creating polygon shapes gives us the most flexibility, as our shapes can be created with three or more points. The value passed to the polygon needs to be three or more pairs of values which represent coordinates. 

It is here where the Firefox tools become really useful as we can use them to help create our polygon. In the below example, I have created a polygon with four points. In the Firefox DevTools, you can double-click on any line to create a new point, and double-click again to remove it. Once you have created a polygon that you are happy with, you can then copy the value out of DevTools for your CSS.

{{< codepen height="480" theme_id="light" slug_hash="BOpVVL" default_tab="result" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/rachelandrew/pen/BOpVVL">Smashing Shapes: polygon()</a> by Rachel Andrew (<a href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### Fallbacks

As CSS Shapes are applied to a float, in many cases the fallback is that instead of seeing the content wrap around a shape, the content will wrap around a floated element (in the way that content has always wrapped around floats). Browsers ignore properties they do not understand, so if they don't understand Shapes, it doesn't matter that the `shape-outside` property is there.

Where you should take care would be in any situation where not having shapes could mean that content overlaid an area which made it difficult to read. Perhaps you are using Shapes to push content away from a busy area of a background image, for example. In that case, you should first make sure that your content is usable for the non-Shapes people, then use Feature Queries to check for support of `shape-outside` and overwrite that CSS and apply the shape. For example, you could use a margin to push the content away for non-Shapes visitors and remove the margin inside your feature query.

<pre><code class="language-css">.content {
    margin-left: 120px;
}

@supports (shape-outside: circle()) {
    .content {
        margin-left: 0;
        /* add the rest of your shapes CSS here */
    }

}
</code></pre>

With Firefox releasing their support we now only have one main browser without support for Shapes &mdash; Edge. If you want to see Shapes support across the board you could go and [vote for the feature here](https://wpdev.uservoice.com/forums/257854-microsoft-edge-developer/suggestions/6263716-shapes), and see if we can encourage the implementation of the feature in Edge.

### Find Out More About CSS Shapes

In this article, I've tried to give a quick overview of some of the interesting things that are possible with CSS Shapes. For a more in-depth look at each feature, check out the [Guides to CSS Shapes](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Shapes) over at MDN. You can also read a [guide to the Shape Path Editor in Firefox](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Edit_CSS_shapes).

{{< signature "il" >}}

---
title: 'Mastering Photoshop: Noise, Textures, Gradients and Rounded Rectangles'
slug: mastering-photoshop-noise-textures-gradients-and-rounded-rectangles
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5c8c992-2588-4187-89fd-95f1b4f0ec01/photoshop-techniques.jpg
date: 2011-02-07T12:51:56.000Z
author: marc-edwards
description: >-
  Often, it's the little details that turn a good layout into a great design;
  details such as subtle textures, shading and smooth shapes. Photoshop contains
  a vast array of tools for embellishing a design, but choosing the right one
  isn't always easy.
categories:
  - Graphics
  - Techniques
  - Photoshop
---
Often, it's the little details that turn a good layout into a great design; details such as subtle textures, shading and smooth shapes. Photoshop contains a vast array of tools for embellishing a design, but choosing the right one isn't always easy. Being the obsessive-compulsives that we are, we've conducted a huge range of experiments to determine the benefits and disadvantages of each technique. Here, then, is an obsessive-compulsive's guide to some frequently used tools and techniques for Web and UI design in Photoshop. 

You may want to take a look at the following related posts:

*   [Techniques For Creating Custom Textures In Photoshop](https://www.smashingmagazine.com/2014/07/creating-custom-textures-photoshop-techniques/)
*   [The Whys And The Hows Of Textures In Web Design](https://www.smashingmagazine.com/2011/10/whys-hows-textures-web-design/)
*   [Pixel Perfection When Rotating, Pasting And Nudging In Photoshop](https://www.smashingmagazine.com/2011/04/mastering-photoshop-pixel-perfection-when-rotating-pasting-and-nudging/)

## Noise and Textures

Subtle noise or texture on UI elements can look great, but what’s the best way to add it? Our goal is to find the best method that maintains quality when scaled but that is also easy to implement and edit. To find out which is best, we’ll judge each method using the following criteria:

{{% feature-panel %}}

*   Number of layers used: fewer is better.
*   Ability to scale: if the document is resized, will the effect maintain its quality?
*   Can the noise be on top of the Color and Gradient layer styles?
*   Can the method be used with any texture, not just noise?

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/044a6dcb-7577-48cc-af98-5bb1f0ac7c23/noise1.jpg" alt="noise1" width="500" height="192" />

### 1. Bitmap Layer With Noise

Probably the most obvious method for adding texture to a shape is to create a normal bitmap layer, fill it with a color, select <code>Filter</code> → <code>Noise</code> → <code>Add Noise</code>, then apply a mask or Vector Mask to match the element you’re adding noise to.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13b3146a-eb00-4195-b211-fc231b9b49e8/noise2.gif" alt="noise2" width="500" height="500" />

Using a high amount of noise, setting the layer blending mode to Luminosity and reducing the opacity will yield the most control over the noise with the least disturbance to the underlying layers. A noise setting of 48% gives a high dynamic range without clipping the noise. (Clipping results in higher contrast, which might not be desirable.)

*   Layers: _2_
*   Scales: _No, texture will have to be recreated if the document is scaled_
*   Works with Color and Gradient layer styles: _Yes_
*   Works with any texture: _Yes_

### 2. Inner Glow Layer Style

Adding an Inner Glow layer style with the source set to center and the size to 0 will let you use the noise slider to add texture to any layer. It’s a good solution, provided you’re not already using the Glow layer style for something else. The noise is added above the Color, Gradient and Pattern layer styles, which is great.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/750450cb-34c7-46c9-ab6a-4c0bd36d4ea2/noise3.jpg" alt="noise3" width="500" height="295" />

Unfortunately, the noise can only lighten or darken the underlying elements. The previous bitmap layer method can add highlights and shade at once while maintaining the average luminosity, and it looks far better in my opinion.

*   Layers: _1_
*   Scales: _Yes, texture will be remade automatically_
*   Works with Color and Gradient layer styles: _Yes_
*   Works with any texture: _No_

### 3. Smart Object with Filter

Create a Solid Color layer, convert it to a Smart Object, select <code>Filter</code> → <code>Noise</code> → <code>Add Noise</code>, apply a Vector Mask to match your element, set the layer blending mode to <em>Luminosity</em> and reduce the layer’s opacity.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d419f9f9-9eb4-430c-969c-ba70894d5200/noise4.gif" alt="noise4" width="500" height="562" />

It’s a fairly involved process, but it can accommodate a combination of effects that can be remade if the document gets scaled.

*   Layers: _2_
*   Scales: _Yes, texture will be remade automatically_
*   Works with Color and Gradient layer styles: _Yes_
*   Works with any texture: _No_

### 4. Pattern Overlay Layer Style

Start by creating a noise or repeating pattern in a new document, then choose <code>Edit</code> → <code>Define Pattern</code>. Once you’ve defined the pattern, it will be available in the Pattern Overlay layer style options. As with previous methods, using <em>Luminosity</em> as a blending mode and reducing the opacity to suit it yield great results.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c4ddf35-9158-4995-b37c-57de2440ebfb/noise5.gif" alt="noise5" width="500" height="464" />

The Pattern layer style is composited below the Color and Gradient styles, ruining an otherwise perfect noise and texture method. However, you can create a second layer that just holds the texture if you need to, or start with a Gradient Fill layer, sidestepping the limitation.

*   Layers: _1_
*   Scales: _Yes, but you’ll need to change the Layer style scale to 100% after scaling_
*   Works with Color and Gradient layer styles: _No, the pattern appears underneath_
*   Works with any texture: _Yes_

### Which Method Is Best?

Although a little cumbersome, creating a Gradient Fill layer, adding a Pattern layer style, then creating a Vector Mask seems to be the best method possible. This can be used to create flexible, scalable and editable single-layer UI elements with texture. As a bonus, Gradient Fill layers can be dithered and so also produces the highest quality results (Gradient layer styles cannot be dithered).

We’ve created some examples below and included the source document so that you can see how they were built.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce4d6ef2-7cc1-4a7b-b40d-e650d7e138a4/reset-kill-limit.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad40f3a0-4f39-40fd-af55-9ca9d97219ac/reset-kill-limit-small1.jpg" alt="Screenshot" width="500" height="90" /></a>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90f45197-1577-4905-bb75-e3d198e5371b/bjango-noise-examples.zip">Download the PSD</a> (.zip)

## Rounded Rectangles

Rounded rectangles, or “roundrects” as <a href="https://en.wikipedia.org/wiki/QuickDraw">QuickDraw</a> so fondly calls them, are standard fare on a Web and interface designer’s utility belt. They’re so common that it’s rare for Web pages or apps to <em>not</em> contain a roundrect or two. Unfortunately, pixel-locked rounded rectangles can actually be fairly difficult to draw in Photoshop. (By pixel-locked, I mean that every edge falls on an exact pixel boundary, creating the sharpest object possible.)

Experienced Photoshop users will probably already know one or two ways to draw a roundrect. Hopefully, after reading this article, they’ll also know a couple more, as well as which methods produce pixel-perfect results.</p>

### 1. Rounded Rectangle Vector Tool

Photoshop’s Rounded Rectangle vector tool is the ideal candidate for the task. The result is perfect roundrects, every time. And the corner radius can be altered during or after drawing the shape (Window &gt; Properties). On the positive side, keeping your objects as vectors means that you’ll be able to resize the document and the corners will take full advantage of any extra resolution. There is one small caveat though: if you resize, you’ll have to do it as an exact multiple, or risk fuzzy non-pixel–locked edges.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3864dd3-6587-41cd-a2bf-1f7a3ca200e1/noise6.gif" alt="noise6" width="500" height="248" />

### 2. Blur

The blur method is a bit of a hack that involves creating a selection, blurring it, then increasing the contrast so that you’re left with a sharp mask that’s antialiased nicely.

It’s seven steps in total and is prone to being inaccurate; plus, the radius of the corners can’t be changed on the fly. Applying levels can also be a bit fiddly. One advantage is that different levels settings can be used to obtain different degrees of antialiasing, from incredibly soft to completely aliased.

1.  Create a new layer.
2.  Draw a rectangular selection.
3.  Enter quick mask (`Q`).
4.  Gaussian blur by half the radius that you’d like for the rounded corners. (For example, a 10-pixel radius would need a 5-pixel blur.)
5.  Apply Levels (`Command + L`), and use about 118 for the black point and 137 for the white point on the input levels.
6.  Exit quick mask (`Q`).
7.  Fill selection.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfe35f1e-c925-45e2-b899-3a62b5048e9b/blur.png" alt="Screenshot" width="550" height="136" />

On the positive side, this blur method can be used to quickly create some interesting and organic shapes that would be difficult to draw by hand.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8caef98d-9b16-4188-a9b9-1bacaa5651b3/blur-examples.png" alt="Screenshot" width="550" height="136" />

### 3. Circles

The circles method is very accurate and easily reproducible, but has a whopping 13 steps. That’s a lot of clicking for just a single roundrect.

1.  Create a new layer.
2.  Make a circular selection that is twice as large as the radius you would like (for example, a 10-pixel radius would require a 20x20-pixel circle).
3.  Fill the selection.
4.  Move the selection right. This can be done quickly by holding down Shift and pressing the right-arrow key a few times.
5.  Fill the selection.
6.  Move the selection down.
7.  Fill the selection.
8.  Move the selection left.
9.  Fill the selection.
10.  Make a rectangular selection that covers the entire vertical span of the roundrect but that starts and ends halfway through the circles at the ends.
11.  Fill the selection.
12.  Make a rectangular selection that covers the entire horizontal span of the roundrect but that starts and ends halfway through the circles at the ends.
13.  Fill the selection.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73228cee-071d-409c-b05e-853ddc676cc9/fourcircles.png" alt="Screenshot" width="550" height="136" />

### 4. Stroke

The stroke method is very accurate, easily reproducible and has only about four steps, depending on the result you’re after. The corners are a bit sharper than those of the circle method, though. That may be a good thing or a bad thing, depending on your preference.

1.  Create a new layer.
2.  Draw a rectangular selection that is smaller than the area you require (smaller by double the radius, if you want to be exact).
3.  Fill the selection.
4.  Add a stroke as a layer style that is as thick as the corner radius you would like.

If you’d like to flatten the object to remove the stroke, keep following the steps below.

1.  Create a new layer.
2.  In the Layers palette, select the new layer and the previous layer.
3.  Merge layers (`Command + E`).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3868164b-3b9e-485c-8033-cb16b8fa3e25/strokeit.png" alt="Screenshot" width="550" height="136" />

It’s possible to automate the flattening with a Photoshop Action. This can also be set up as a function key to speed things up further.

A huge advantage of the stroke method is that it’s dynamic, so the radius can be edited in real time. It can also be used to easily create other rounded shapes, as seen below.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b6afe4e-26b5-427a-b67b-7312bbf9f701/strokeit-examples.png" alt="Screenshot" width="550" height="277" />

### Which Method Is Best?

In most cases, using the Rounded Rectangle tool will give great results and be the quickest method.</p>

## Gradients

Gradients are a great way to add life-like lighting and shading to surfaces. When built with gradient layers and layer styles, they also ensure that UI elements can be scaled and reused easily.</p>

### Linear Gradients

Linear gradients are gradients in their most basic form — a gradual blend of colors and following a straight line. I’m sure you knew that, so onto the more interesting stuff.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcaa1ab1-72e7-43ca-bb93-28736573b815/linear.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3869a27a-8415-4144-a078-bc0a6afea8aa/linear.jpg" alt="Screenshot" width="550" height="184" /></a>

### Reflected Gradients

Reflected gradients are like their linear friends, but they repeat the gradient twice, with the second repeat mirrored. This makes editing a little less tedious, provided it fits the result you’re after.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/372a0ea1-28fb-4937-a0e9-d0e95fdfd38f/reflected.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c9b307f-704e-4528-b6ad-01a8414514b8/reflected.jpg" alt="Screenshot" width="550" height="184" /></a>

### Radial Gradients

Radial gradients start from the center (or any chosen point) and grow outward in a circular pattern. They’re handy for creating spheres and applying effects to the edge of circular elements. The center point of the gradient can be moved by clicking and dragging on the canvas while the gradient window or layer styles window is open.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3b108f1-6f8d-4444-8afd-b09c8ff55a67/radial.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25fb2c18-1d85-4b44-b9a7-1d0cfe08a900/radial.jpg" alt="Screenshot" width="550" height="312" /></a>

### Angle Gradients

Angle gradients can be a great way to mimic environmental reflections found on highly polished metallic objects. The center point of the gradient can be moved by clicking and dragging on the canvas while the gradient window or layer styles window is open.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7851f75f-4604-4540-a8fa-a861e5bce7c9/angle.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e8264e7-1796-4fdf-a54e-b119133f2986/angle.jpg" alt="Screenshot" width="550" height="312" /></a>

### Gradients on Gradients

Anything worth doing is worth overdoing, right? Combining a gradient layer with a gradient layer style lets you overlay two different gradients, giving more complex and — here’s the good part — completely dynamic results. To combined the gradients, you’ll need to set a blending mode for the gradient layer style. For the examples below, I’ve used either Screen (good for lightening) or Multiply (good for darkening).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5183a226-ec58-48e4-9b6e-c5d9e01603e2/combined.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/580542ca-26e9-4d30-bfe8-731f88bd0d1c/gradients-on-gradients.jpg" alt="Screenshot" width="550" height="469" /></a>

### Dithering Is Everything

Adding dithering to a gradient produces smoother results. Non-dithered gradients often contain visible banding. Dithering is even more important if your artwork is being viewed on cheaper 6-bit per channel <a href="https://en.wikipedia.org/wiki/TFT_LCD">TN LCDs</a> and <a href="https://www.displaymate.com/Nexus_One_ShootOut.htm">certain display types</a> that tend to amplify <a href="https://en.wikipedia.org/wiki/Posterization">posterization</a> problems.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09ade903-12ea-4e28-b1d7-e92f52f15ea4/dithering.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e7ac809-aa97-44e0-8307-b015d291376c/dithered.jpg" alt="Screenshot" width="550" height="312" /></a>

If you’re not seeing the difference, here’s an extreme and completely unrealistic example of gradient dithering in action:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc519aef-8e22-402c-92b3-cb73a72b1b00/dithering-extreme.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0737eabd-7390-4e36-9bb0-7168fb4ac70a/dithered2.jpg" alt="Screenshot" width="550" height="238" /></a>

Ensuring that your gradients are dithered is easy: just check the appropriate box in Photoshop.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc91965f-6768-4310-ae3f-b6f7fb9293e5/check-dither.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e91a358b-b58a-4fbe-8219-67759d9b9db0/gradient-fill.jpg" alt="Screenshot" width="550" height="277" /></a>

Note that gradient layer styles can’t be dithered, and gradients in placed objects (such as stuff you’ve pasted from Illustrator) aren’t dithered.

If you use transparency in a gradient, that won’t be dithered either, which can be a huge issue at times. There is a solution for some specific cases: if you’re using a gradient with transparency to lighten an area with white, then using a non-transparent gradient with a Screen Layer blending mode will let you dither it. The same technique can be used for darkening with the Multiply blending mode.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3acd990c-8fc4-4fd6-879a-59add00d9cbe/transparency.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd646545-cec5-4fd8-bf02-d31e764ef3a1/transparency.jpg" alt="Screenshot" width="550" height="163" /></a>

A combination of the gradient techniques described above were used to create the Mac app icon below.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7b94267-f3d3-452d-880f-6e85a8895d92/istatmenus-icon.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e33a1018-391d-4d72-ab87-f9b486dec603/mac-app-icon.jpg" alt="Screenshot" width="578" height="348" /></a>

### Gradient Maps

Quite different to other types of gradients, gradient maps can be a great way to add color treatment, allowing for very precise control. Gradient maps use the brightness of each pixel to map to a corresponding color in a gradient.

If the gradient starts at red and ends at blue, then everything white in the image will turn red, and everything black will turn blue. Everything in the middle tonally will map to the gradient, depending on how bright it is.

The image below was used in a poster for Kingswim, a swimming school:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/895b8c4e-1d9f-40c1-8722-c5b35c10e62c/gradientmap.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86f2b3f7-be79-4e30-86b9-0b71d4cfac5e/kingswim.jpg" alt="Screenshot" width="500" height="546" /></a><br>
<em>With a gradient map. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/895b8c4e-1d9f-40c1-8722-c5b35c10e62c/gradientmap.jpg">Large view</a></em>

Without the gradient map, things look quite different. It’s a composite of about seven photos; the boy and background were shot on black and white film with intentionally low contrast so that the grain would be more prominent when the contrast was pushed by the gradient map. The gradient map also hides the color mismatches in the compositing.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5307866c-a5f2-4284-9a53-93503379c806/gradientmap-off.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcb23626-1b96-4589-9d55-923f1c3fe321/kingswim2.jpg" alt="Screenshot" width="500" height="486" /></a><br>
<em>Gradient map off. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5307866c-a5f2-4284-9a53-93503379c806/gradientmap-off.jpg">Large view</a></em>

## A Little Obsessed?

Absolutely. I conducted all of the tests above to learn more about some common techniques that I already use: that is, to reassess and fine tune, with the aim of improving my designs. Creating great artwork without intimately knowing your tools is certainly possible, but the more you know, the more likely you are to work faster and with greater confidence.

<em>(al), (dm)
</em>


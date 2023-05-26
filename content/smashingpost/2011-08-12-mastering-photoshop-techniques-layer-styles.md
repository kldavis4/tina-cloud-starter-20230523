---
title: 'Mastering Photoshop Techniques: Layer Styles'
slug: mastering-photoshop-techniques-layer-styles
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e597ecd-0df3-48d4-bdd9-0be6103596fc/photoshop-07.gif
date: 2011-08-12T11:47:52.000Z
author: thomas-giannattasio
summary: >-
  Despite the layer styles ubiquity, many designers do not yet realize the full potential of this handy menu. Thomas Giannattasio presents, step by step, several practical techniques to help you refine your designs, increase productivity and reduce layer clutter.
description: >-
  Thomas Giannattasio presents several practical techniques to help you refine your designs, increase productivity and reduce layer clutter.
categories:
  - Graphics
  - Tutorials
  - Photoshop
---

Layer Styles are nothing new. They’ve been used and abused again and again. Despite their ubiquity, or perhaps because of it, many designers do not yet realize the full potential of this handy menu.
Its beauty lies in our ability to create an effect and then copy, modify, export, hide or trash it, without degrading the content of the layer.

Below we present, step by step, several practical techniques to help you refine your designs, increase productivity and reduce layer clutter.

{{% feature-panel %}}

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/393d019e-a4f5-4a0e-83af-2beb5f99ec28/layer-styles-mastery.zip">Download the source files</a> (.zip, 1.6 Mb).

## The Bump Map Effect

“Wait, what?” you exclaim, “There’s no bump map effect in the Layer Styles menu!” That’s true, but by combining Pattern Overlay and Bevel and Emboss, we can achieve a textured, bump-mapped surface with a controllable light source.

This technique requires two images: one for texture and color, and the other to serve as a depth map. The depth map needn’t have any hue because it determines depth based on a composite value, black being the lowest, white the highest. In some cases, you may be able to use the same image for both, but in our example we’ll use completely different ones.

**Step by Step**

We’ll start by creating our bump map pattern. **Open the *diamond-plate.psd* file.**

Inside you’ll find a number of white shapes on a black background. **Create a pattern** from this document: Select All <code>(Cmd/Ctrl + A)</code>, then *“Edit” → “Define Pattern.”* Name it “diamond plate bump map” and click okay.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e160c667-95b8-409a-b9e4-cfd571f2c26a/mastering-layer1.gif" alt="mastering-layer1" width="500" height="125" /><figcaption>Creating the diamond plate pattern.</figcaption></figure>

Now, **open the *start.psd* file**.

**Repeat step 2** to create a pattern from the “patchy gray” layer. This will be used later to add texture to our background.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58037f63-f068-4740-9122-0e10c84c2338/mastering-layer2.gif" alt="mastering-layer2" width="500" height="178" /><figcaption>Defining the texture pattern.</figcaption></figure>

After creating the pattern, **delete the “patchy gray” layer**. It’s no longer needed.

Use the Rectangular Shape tool to create a shape layer about 20 pixels wider and 20 pixels higher than the canvas. Change the color of this layer to a dark, brownish, chromatic gray.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6edb5d2a-7811-4081-9e5b-c7afaa8f08cc/bump-step-06.gif" alt="" /><figcaption>Creating the shape layer for our background.</figcaption></figure>

Be sure that the shape layer doesn’t have any Layer Styles already applied to it (Photoshop will often apply the most recent Layer Style automatically). Then, **begin the new Layer Style by adding a Pattern Overlay**.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01a54cdf-c4ca-42ef-a416-6e55c2a477bc/mastering-layer3.gif" alt="mastering-layer3" width="500" height="373" /><figcaption>Adding a Pattern Overlay effect.</figcaption></figure>

**Choose the "patchy gray" pattern from the pattern picker, and change the Blend Mode to Soft Light**. This will add the texture to our background layer.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86481381-0c1e-4ca9-98f9-5b31be151ea6/bump-step-08b.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6eb22f53-03ab-4360-9d77-8211b559a06e/mastering-layer4b.gif" alt="mastering-layer4b" width="500" height="342" /><figcaption>Adding a pattern overlay effect.</figcaption></figure>

Next, add a Bevel and Emboss, along with the Texture effect. This time, change the Texture effect’s Pattern to the “diamond plate bump map” pattern created in step 2. We now have a grungy diamond plate background.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a60e0a4c-ada2-4768-a53b-29c834379fbf/bump-step-09b.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f54f2604-db75-4c0e-b7f5-b9388c22f111/mastering-layer5.gif" alt="mastering-layer5" width="500" height="422" /><figcaption>Applying the Bevel and Emboss texture effect.</figcaption></figure>

As with most Layer Style effects, the default values are rarely ideal. **By tweaking the Bevel Type and Size, Gloss Contour, Highlights, Shadows and Light settings** you can achieve some dramatic results.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e332d82-d324-4eb1-aa2c-20c933b64b3c/bump-step-10b.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/885d0eda-4fd1-4174-a931-bc2bfe74adfa/mastering-layer6.gif" alt="mastering-layer6" width="500" height="439" /><figcaption>Tweaking the Bevel and Emboss settings.</figcaption></figure>

With a few extra effects, you can shape the background layer even more. The example has a **Gradient Overlay** to simulate reflected light by darkening certain regions of the image.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a147c80-bab3-4d90-b044-f5c0e8e5713a/bump-step-11b.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd93b52e-875d-42f5-a1dd-7b95ef4a4316/mastering-layer7.gif" alt="mastering-layer7" width="500" height="439" /><figcaption>Using the Gradient Overlay to darken some regions.</figcaption></figure>

You may notice that the highlights from the Bevel and Emboss filter all seem to have the same value. This is because the Bevel and Emboss effects are very high on the Layer Style’s stacking order. To darken the highlights that lie outside our main light source, simply **paint a Layer Mask using the Brush tool**.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a03c18c0-41e2-4da1-a03b-f09838a2a6a5/mastering-layer8.jpg" alt="mastering-layer8" width="500" height="320" /><figcaption>Painting a mask to increase the appearance of light in the background.</figcaption></figure>

We now have a textured, bump-mapped background that is completely dynamic; everything about it can be modified easily from within the Layer Styles menu. Consolidating complex imagery into one dynamic layer like this can reduce layer clutter dramatically and allows you (and whoever else may be using the file) to easily find and modify things. Now, let’s move on to creating our icon.

## 3-D Modeling

By combining some interior effects, we can use the Layer Styles menu to create simulated 3-D objects: great for icons, buttons and other interface objects. We’ll now model the base of the round icon in the example image using a single layer.

**Step by Step**

**Begin by creating a circular shape layer with a rich red fill**.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b808af8-dbc7-4590-9a54-5901a94e3bd4/3d-step-01.jpg" alt="" /><figcaption>Creating the shape layer for the icon’s base.</figcaption></figure>

As is often the case when modeling a 3-D shape, **let’s begin by adding a Gradient Overlay to our Layer Style**. A white-to-black Radial-styled gradient set to Linear Burn works best for our implementation. Be sure the white area of the gradient is at the origin.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74639e12-1da6-4e84-bc8b-ca08115e54fc/3d-step-02.jpg" alt="" /><figcaption>Adding Gradient Overlay set to Linear Burn.</figcaption></figure>

We now have a dramatically shaded sphere with a head-on light source. By **decreasing the opacity of the gradient**, we can flatten the shape to a more concave button.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2194473-d5b7-4aa2-b783-56cd817d5e35/mastering-layer9.gif" alt="mastering-layer9" width="500" height="345" /><figcaption>Reducing the Opacity for a subtler effect.</figcaption></figure>

Let’s also move the direction of the light to the upper-left. While leaving the Layer Style menu open, move the mouse over the image itself (the Move Tool icon should appear). Simply **click and drag the epicenter of the gradient to the upper-left of the shape layer**.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a65bf791-d8b6-400a-a8fc-a7ebc39ac689/3d-step-04.jpg" alt="" /><figcaption>Repositioning the gradient within the Layer Styles menu.</figcaption></figure>

While Bevel and Emboss may seem like more logical tools, you can often get a cleaner, more customizable beveled look by using a combination of other effects. First, **add a black Inner Glow, set to Multiply**. Adjust the Choke, Size, Opacity and Contour until you have a softened edge inside the shape.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e03319d-1559-408b-96a5-dbb6b7fc653c/3d-step-05b.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d7eca50-1c60-49d1-87a8-812a41649780/mastering-layer10b.gif" alt="mastering-layer10b" width="500" height="411" /><figcaption>Adding a Glow to darken the edge of the base.</figcaption></figure>

Like for any well-rendered spherical surface, we have to add some reflected light in our shadow region. This is easily achieved with the **Inner Shadow effect**. Change the color to white and the Blend Mode to Linear Dodge. Adjust the angle so that it appears in the lower-right of our shape. Tweak the Contour, Distance, Size and Opacity to create a subtler effect.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b5db1bd-88c7-46eb-8da2-184037ff612b/3d-step-06b.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/768ca634-f144-4ed7-8ebe-f687c56b3d1a/mastering-layer11.gif" alt="mastering-layer11" width="500" height="363" /><figcaption>Adding subtle reflected light using Inner Shadow.</figcaption></figure>

To enhance the feeling that the shape is part of the document’s “environment,” we can add some effects to interact with the background. **Drop Shadow** is usually the easiest tool to use for this. Massage the settings until everything feels right.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/934a5dc7-f826-4ed9-87e6-c225af915131/3d-step-07b.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df5b139c-28b8-4628-9e54-5bd09bb2d6bc/mastering-layer12.gif" alt="mastering-layer12" width="500" height="363" /><figcaption>A simple Drop Shadow goes a long way.</figcaption></figure>

Using the **Outer Glow** effect, we can simulate the reflected red light that our background image would absorb if this were an actual setting. Change the glow’s color to a darker red, and change the Blend Mode to darken. Again, work with the Size and Opacity settings to create the desired effect. This is one of those effects that, when used correctly, no one should notice because it just looks natural.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96cef3a7-5cc6-4a4c-9112-f540ab89106e/3d-step-08b.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2d71997-1104-4d07-a541-e9a4905fd2f4/mastering-layer13.gif" alt="mastering-layer13" width="500" height="363" /><figcaption>A red Glow to add more "environment."</figcaption></figure>

Please notice that Layer Style gradients can’t be dithered, which can make them lower quality than their Gradient Layer and Gradient Tool counterparts (*&mdash; Marc Edwards*).

{{% ad-panel-leaderboard %}}

## Diffuse vs. Specular Light

Now, our icon reflects a simulated **diffuse light**, which gives it the look of a matte-finished surface. If you prefer a glossier appearance, you can easily create a **specular highlight** using (what else?) Layer Styles.

**Step by Step**

**Duplicate the current shape layer <code>(Cmd/Ctrl + J)</code>**.

**Clear the new layer’s Layer Styles**: right-click the layer in the Layers palette and select "Clear Layer Style."

We also need to modify the shape of the layer to give the reflected light a sharper edge. Using the Direct Selection Tool (A), select the shape path in the layer’s vector mask. Copy it <code>(Cmd/Ctrl + C)</code> and paste it <code>(Cmd/Ctrl + V)</code> above the current path. Change this path’s mode to Subtract from shape area *(-)*. Then move the shape down and to the right to create a crescent shape. You may also want to make the negative shape larger to create a more natural inside curve: simply Free Transform <code>(Cmd/Ctrl + T)</code> and then scale the shape up.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce446d72-3bfe-4508-8e78-956223699ae8/spec-step-03.jpg" alt="" /><figcaption>Modifying the shape of the specular highlight.</figcaption></figure>

Because we need this layer only for its Layer Styles, we can **set its Fill Opacity to 0%**. We also want this layer to inherit the Layer Styles of the underlying layer, so **create a Clipping Mask on the new layer <code>(Cmd/Ctrl + Option + G)</code>**.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d21335c-c4d2-4cb8-8c6c-0ca7b1db2a65/mastering-layer14.gif" alt="mastering-layer14" width="500" height="440" /><figcaption>Creating a Clipping Mask to inherit effects.</figcaption></figure>

Now, **begin the Layer Style with a Gradient Overlay**. Use the default black-to-white gradient, and set the Blend Mode to Screen. Knock the Opacity down to about 50%, and change the angle to about 115°. You may need to change the positioning of the gradient, which you can do by clicking and dragging inside the document window, just as you did in the 3-D modeling section.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/802473a3-5363-44b7-8503-f76715d297de/spec-step-06b.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e148-bef1-4b9d-9c88-bf3f2f5e9032/mastering-layer15.gif" alt="mastering-layer15" width="500" height="307" /><figcaption>Setting the Gradient Overlay to Screen.</figcaption></figure>

This is a good start for the highlight, but it still looks somewhat unnatural. Using a transparent inside stroke, we can shrink the perimeter of the interior effects. **Add a Stroke effect to the layer and drop its opacity to 0%**. Change the position to Inside, and work with the size slider until the highlight begins about where the darker inner glow ends on the underlying layer (the example image uses 5 pixels).

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1b857c8-ece4-4b2b-975a-8716c4ec9834/spec-step-07b.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/699eaee3-08d7-4b6e-8541-817aa90bfffd/mastering-layer16.gif" alt="mastering-layer16" width="500" height="307" /><figcaption>Using a 0% Inside Stroke to shrink the perimeter of interior effects.</figcaption></figure>

To add a more dynamic look to your highlight, you can **add a white Inner Shadow set to Screen** with a custom contour. Tweak the distance and size settings to finish off the effect.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d69f91cb-ee47-47ff-bbb7-d6793f1a52e9/spec-step-08b.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a7f99e4-b5e1-4101-9ab3-82ecf29586a6/mastering-layer17.gif" alt="mastering-layer17" width="500" height="307" /><figcaption>The Inner Shadow creates a more dynamic specular reflection.</figcaption></figure>

## X-Ray Vision

**Step by Step**

To create the die-cut type inside our icon, we could turn the text layer into a shape layer and use the paths to mask away areas from the base. However, this would result in degenerated content; we would no longer be able to modify the type. Instead, we’ll simulate a mask using the **Knockout Blending Option**. This will also allow us to apply custom effects to the cut-out area.

**Create a new Type Layer with the text “fx”**, and position it within the circular base. The example uses 120 point Garamond Bold Italic.

**Drop the Fill Opacity to 100%.**

**Begin your Layer Style by adding an Inner Shadow**. Increase the size, and increase the opacity to about 90%. You may also want to modify the distance and contour to your liking.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8658f36-a46a-4ec7-9c32-7d6ac604dc7b/xray-step-03.jpg" alt="" /><figcaption>The beginnings of the die-cut effect.</figcaption></figure>

We now have the beginnings of a die-cut effect, except that the text still shows the base below it. To fix this, **go to the Blending Options section in the Layer Styles menu. Change the Knockout from None to Shallow** (this setting samples pixels from the layer directly beneath the current layer’s group). Because our text layer doesn’t belong to a layer group, it samples instead from the Background layer. (Using a Deep Knockout would always sample from the Background layer, regardless of the layer’s group.)

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3461a958-05c3-475a-8b04-240b97f492b2/xray-step-04b.jpg" alt="" /><figcaption>Shallow Knockout samples pixels from the layer directly beneath the current layer’s group.</figcaption></figure>

To get the text layer to sample from our diamond plate layer, **start by clicking “Okay” to close the Layer Style menu. Select the text layer and both of the buttons that make up the base, and group the layers <code>(Cmd/Ctrl + G)</code>.** As you can see, the “fx” shapes are now drawing pixels from the textured layer directly below the new layer group.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92ecb060-447c-4b8b-ab0b-51dca3a650e8/mastering-layer19.jpg" alt="mastering-layer19" width="500" height="320" /><figcaption>Grouping the icon so that the Knockout samples from the diamond plate layer.</figcaption></figure>

The knockout effect is very convincing, but the type still feels detached from the base. Let’s add a beveled effect to simulate the surface quality of the base. **Start by adding an outside Stroke with a size of 2; then drop the opacity to 0%.** This doesn’t achieve anything but is necessary for the next step.

**Now add a Bevel and Emboss effect. Change the Style to Stroke Emboss and Technique to Chisel Hard.** This will apply the bevel’s lighting effects within the stroke area created in the step above. Modify the settings to achieve a subtle and smooth edge.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e42bc9ad-2246-4054-b275-c3a75d56f165/xray-step-07b.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e3e29bf-65e6-4882-bdb0-90492459e416/mastering-layer18.gif" alt="mastering-layer18" width="500" height="428" /><figcaption>Adding a Stroke Emboss.</figcaption></figure>

Let’s take the bevel one step further by adding a thin specular highlight to the bottom-right edges of the shape. **We can use a white Drop Shadow effect, set to Screen, to add a bright highlight just at the edge of the bevel.** You’ll want to modify the distance and size to give the highlight a sharp edge.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e962a8e-9132-4e22-a1f5-585425df42f7/xray-step-08b.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54d01745-0fe1-4c20-a3db-7cc51379f619/mastering-layer19.gif" alt="mastering-layer19" width="500" height="342" /><figcaption>Adding a thin specular highlight using a Drop Shadow.</figcaption></figure>

Finish off the Layer Style with more shading within the die-cut letters by **adding a simple black-to-white Gradient Overlay, set to Multiply**.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f33f14c-5747-4c54-88f5-bad2bf1f9b7b/xray-step-09.jpg" alt="" /><figcaption>Finishing off the die-cut.</figcaption></figure>

## Quick Tips

Despite frequent misuse, the Layer Styles menu really is a powerful tool that every designer should learn to work with. Not only does it provide a level of speed and control not easily found through other means, but it provides invaluable flexibility.

Our example shows how a multi-dimensional icon and a completely dynamic background can be consolidated within four simple Shape layers, allowing them to be easily modified, reused and repurposed throughout your designs. Below are a few extra tips to remember when working on your next project.

**Effects Stacking Order**

You may have noticed sometimes that an effect isn’t visible when another effect is being used. For example, a Color Overlay seems to override a Gradient Overlay. This is because of the Layer Styles Stacking Order. Just as with the Layer’s Palette, one layer will cover another that is lower down in the stacking order.

Unfortunately, the Layer Styles menu doesn’t allow you to rearrange the order of effects. One way around this (even if you sacrifice the ability to edit) is to use Create Layers, which turns all of your Layer Style effects into actual layers that you can move.

**Interior Effects Stacking Order:**

*   Stroke
*   Bevel and Emboss
*   Inner Shadow
*   Innger Glow
*   Satin
*   Color Overlay
*   Gradient Overlay
*   Pattern Overlay

**Exterior Effects Stacking Order:**

*   Stroke
*   Outer Glow
*   Drop Shadow
*   Non-Color-Specific Styles

Though not always possible, you may want to use black, white and grays for your effects. Using monochromatic colors in conjunction with the proper Blend Mode allows you to create styles that are non-color-specific, meaning you can modify the color of the actual layer, and your Layer Style will update appropriately.

**Scaling Effects**

There may be times when you’ve created a Layer Style that looks great at the original size, but when the shape is increased or decreased, your beautiful style is destroyed. Fortunately, Photoshop provides a method to adjust styles that are out of whack. Simply choose *Layer → Layer Style → Scale Effects*, and then input the percentage you need.

**Inconspicuous Menu Options**

A number of hidden commands are available to you from within the Layer Styles menu. Depending on the effect, you will have access to either the Hand tool or the Move tool by simply mousing over the document window. The Hand tool allows you to move the document around just as you would outside the Layer Styles menu, and the Move tool repositions the current effect and updates the settings automatically.

When using the Move tool, you can still access the Hand tool by holding the space bar. While using either of the tools, you can zoom in and out by holding <code>Space + Cmd</code> or <code>Space + Option</code> respectively. Don’t forget, as with most other menus in Photoshop, holding "Option" will change the "Cancel" button to a “Reset” button, allowing you to undo any changes.

*Thanks to Marc Edwards and Ricardo Gimenes for their assistance in editing the article.*

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Mastering Photoshop: Unknown Tricks and Time-Savers](https://www.smashingmagazine.com/2010/01/obscure-adobe-photoshop-time-savers/)
*   [Useful Adobe Photoshop Techniques, Tutorials and Tools](https://www.smashingmagazine.com/2010/09/round-up-of-useful-adobe-photoshop-techniques-tutorials-and-tools/)
*   [70 Beauty-Retouching Photoshop Tutorials](https://www.smashingmagazine.com/2008/07/70-beauty-retouching-photoshop-tutorials/)
*   [Photoshop Plugins and Filters A-Z](https://www.smashingmagazine.com/2009/08/a-z-of-free-photoshop-plugins-and-filters/)

{{< signature "al, mrn" >}}

---
title: 'How To Use Photoshop Masks [+Keyboard Shortcuts]'
slug: unveiling-photoshop-masks
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac9d3c3c-f3ea-48e8-830b-bdff629697aa/masks.png
date: 2009-12-17T16:06:38.000Z
author: thomas-giannattasio
summary: >-
  Design is a fluid and shifting process in which layers are constantly modified and tweaked. As complexity builds, so does the need for preserving data in a flexible way. Learning non-destructive editing techniques helps you produce documents that bend along with your creativity. Photoshop Masks are the cornerstone of this process. Not only do they preserve important pixel data, but they allow for the creation of flexible interface elements as well.
description: >-
  Photoshop Masks are the cornerstone of this process. Not only do they preserve important pixel data, but they allow for the creation of flexible interface elements as well.
categories:
  - Graphics
  - Photoshop
---
In this article, we'll explore the technical aspects and creative advantages of incorporating masks into your workflow. [Updated February/02/2017]

Photoshop offers five methods of masking: Pixel Masks, Vector Masks, Quick Masks, Clipping Masks and Clipping Paths, all of which define pixel opacities without affecting the original data. Each of them has its own pros and cons, and knowing which method to use is extremely important for creating clean, flexible and properly masked layers.

## Pixel Masks

Pixel masks determine opacity values based on <strong>a raster image with grayscale values that correspond pixel for pixel to the original layer.</strong> This makes them ideal for masking complex photographic imagery (e.g. the hair on a model or leaves on a tree). Pixel masks allow 100 shades of gray, which correspond directly to opacity percentages. The ability to vary opacities is unique to pixel masks, making them an invaluable tool.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/708d174c-f558-4bca-97ee-c02a274e6cec/maks2.jpg" alt="Pixel Masks are ideal for extracting complex photographic imagery." width="500" height="375" /><br>
<em>Pixel Masks are ideal for extracting complex photographic imagery.</em>

While pixel masks can be easily modified, they aren't ideal for every situation. Because of their raster format, scaling them can cause unwanted artifacts and interpolated bluriness. Smooth curves and perfect edges can also be tricky to create when painting a mask. Under such circumstances, vector masks would be preferable.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd0a13fb-e93a-42cd-ac36-4ad7def48354/mask3.jpg" alt="Pixel masks should not be used when rescaling is a possibility." width="500" height="364" /><br>
<em>Pixel masks should not be used when you might have to rescale.</em>

### Creation

Creating a pixel mask is as easy as selecting the layer or layer group and clicking the "Add Layer Mask" button at the bottom of the layer's palette. A second thumbnail will be added to the layer, giving you a preview of the mask. By default, this will be entirely white. However, if you happen to have a selection active when creating the mask, the selection will be used to define the grayscale values of the mask.

Once a mask is created, it can be edited as if it were any other pixel data by clicking on the mask's thumbnail. You can then paint in black to hide areas or white to show them. The mask can also be tweaked using adjustments and filters such as Curves, Threshold, Unsharp mask and Gaussian blur.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e65c6bd7-94f3-4769-873c-2599506b9e00/mask4.jpg" alt="Painting the mask black is much like using the eraser tool." width="500" height="346" /><br>
<em>Painting the mask black is much like using the eraser tool.</em>

### View Modes

While creating a mask, there are a number of ways to view the mask data. <em>Option + clicking</em> on the thumbnail will display only the mask on the canvas; this is great for fine-tuning areas but doesn't allow you to see the actual layer as you work. If you'd like to see both the mask and the layer at the same time, you can view the mask as a Ruby overlay. Simply press with the layer selected to toggle the overlay on and off. The color and opacity of the overlay can also be changed by double-clicking the mask's thumbnail. Additionally, if you'd like to temporarily remove the mask, you can toggle it on and off by <em>Shift + clicking</em> on the mask's thumbnail.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6864b865-73a9-4fef-ba0a-d64c269397c1/mask5.jpg" alt="Pixel Masks are ideal for extracting complex photographic imagery." width="500" height="421" /><br>
<em>Turning the mask off and the overlay on can help with fine-tuning.</em>

### Channels

Every time a layer with a mask is selected, the mask is shown as a <strong>temporary alpha channel in the Channels palette.</strong> From here, you can save the channel for later use by dragging the channel to the "Create new channel" button at the bottom of the palette or by selecting "New Channel" from the fly-out menu. You can also change the mask's Ruby overlay settings by double-clicking the channel's thumbnail. Because a temporary channel becomes available whenever a masked layer is selected, you can use some keyboard shortcuts to toggle between the actual layer and its mask. Pressing <em>Command + </em> will select the mask and <em>Command + 2</em> will bring you back to the layer data.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/237b66c7-4fbd-400d-842b-f6f332d15520/mask6.jpg" alt="A temporary channel is available whenever a layer with a mask is selected." width="500" height="641" /><br>
<em>A temporary channel is available whenever a layer with a mask is selected.</em>

{{% feature-panel %}}

## Vector Masks

Vector masks pick up where pixel masks fall short. By defining the mask's shape using paths, vector masks provide <strong>a superior level of finesse and flexibility</strong>. They're ideal for defining shapes with <strong>clean, crisp lines, such as interface elements.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79a0a8cb-c81c-40c6-85a5-0f0fee05ba3a/mask7.jpg" alt="Vector Masks are ideal for masking crisp-edged objects." width="500" height="707" /><br>
<em>Vector Masks are ideal for masking crisp-edged objects.</em>

The disadvantage of vector masks is that they are unable to vary pixel opacities; they are basically either 0 or 100. For this reason, many masking jobs require a hybrid implementation. By using a vector mask to define the solid edges and a pixel mask for the more complex areas or for varying opacities, you can effectively extract objects while maximizing flexibility.

### Creation

To add a vector mask to an existing layer, simply <em>Command + Click</em> the "Add Layer Mask" button at the bottom of the layer's palette. If a path is currently active, the mask will be created using it. Otherwise, the mask will be empty. Paths can then be added, subtracted or modified by clicking the mask's thumbnail.

Being able to create flexible interface elements is one of the best advantages of vector masks. Using the Shape Tool (U) set to Shape Layers allows you to quickly create a fill layer with a Vector Mask. These layers are far more flexible than a raster level and are perfect for creating buttons, rules and other elements that can be resized without interpolating data.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c48b20d6-2dd0-46a7-987c-66e0ba5b72a5/mask8.jpg" alt="Vector Masks are ideal for masking crisp-edged objects." width="500" height="318" /><br>
<em>The flexibility offered by Vector Masks make them perfect for interface elements such as buttons.</em>

### View Modes

By clicking on the Vector Mask's thumbnail in the the Layer's palette, you can show or hide the paths saved in the mask. These paths can also be accessed from the Path's palette, but only if the layer itself is selected. Toggling the mask on and off can be done by <em>Shift + clicking</em> the thumbnail.

### Paths

Much like how layer masks appear in the Channels palette, <strong>a temporary work path would be displayed in the Paths palette when a layer with a vector mask is selected.</strong> You can then save the mask by dragging it to the "Create new path" button at the bottom of the palette or selecting "Save Path" from the fly-out menu. This temporary path can be accessed at any time by first selecting the Path Selection tool (<em>A</em>) and then pressing <em>Enter</em>; it can be dismissed by pressing <em>Enter</em> again. You can also quickly create a selection from an active path by pressing <em>Command + Enter</em>.

### Applying

Before a vector mask can be applied to a layer it must first be rasterized by right-clicking the vector mask thumbnail and choosing Rasterize Vector Mask. If the layer already has a pixel mask, the two masks will be composited together to create a single pixel mask. It can then be applied like any other layer mask (right-clicking the thumbnail and choosing "Apply Layer Mask").

## Quick Masks

The Quick Mask mode allows you to <strong>create a selection using pixel editing tools as opposed to the primitive selection tools.</strong> This is a more logical approach to creating a complex mask with variable opacity. You can access this mode by clicking on the "Quick Mask" button in the Tools bar or by pressing <em>Q</em>.

Once in Quick Mask mode, you'll no longer be editing the current layer. Instead, you'll be editing a Ruby overlay that can be edited as if it were regular pixel data. By default, entering this mode will cover the entire canvas with a semi-transparent red color. You can then paint white to remove the overlay and black to add it back. The Quick Mask is essentially a more visual representation of a selection. Therefore, every area that you remove from the overlay is added to the selection.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec184497-2c90-442d-9214-8531835251dd/mask9.jpg" alt="Quick Mask mode allows you to quickly paint a selection." width="500" height="333" /><br>
<em>Quick Mask mode allows you to quickly paint a selection.</em>

### Options

You can <strong>modify how the Quick Mask mode is displayed</strong> by double-clicking the "Quick Mask" button in the Tools bar. Here you can change the color and opacity of the mask as well as whether the mask color indicates masked areas or selected areas. Personally, I find painting selected areas more intuitive than painting masked areas, which is the default.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89e6b591-dc8f-41c2-a588-cfc90dcdb1e7/mask10.jpg" alt="The Quick Mask Options menu allows you to change the color, opacity and target of the overlay." width="500" height="344" /><br>
<em>The Quick Mask Options menu allows you to change the color, opacity and target of the overlay.</em>

### Saving

After creating a quick mask, you can <strong>immediately apply it to a layer by creating a layer mask or save it for later use.</strong> By selecting <em>Selection → Save Selection</em>, you can save your selection as a new channel or apply it to an existing channel. This allows you to come back to the selection at any time by <em>Control + clicking</em> the channel in the Channel's palette or by selecting <em>Selection → Load Selection</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/513c04d1-086f-4c2e-a97a-9fcfd6ee28e9/mask11.jpg" alt="Saving a Quick Mask creates a new channel." width="500" height="333" /><br>
<em>Saving a Quick Mask creates a new channel.</em>

{{% ad-panel-leaderboard %}}

## Clipping Masks

You'll often run into situations in which multiple layers require the same mask. You could group the layers and mask the layer group, but that is not always ideal. Clipping masks allows for a layer simply to <strong>adopt the opacity of an underlying layer.</strong> This is extremely helpful when using adjustment layers; by clipping them to a layer, you can apply adjustments to a single layer without affecting those below it.

The easiest way to create a clipping mask is to <strong><em>Option + click</em> between the two layers in the Layer's palette when the clipping mask cursor appears.</strong> Alternatively, you could press <em>Command + Option + G</em> to clip a layer to the one below it. Any number of layers can be clipped to one master layer, but a clipped layer can't be used as a clipping mask itself.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68b514ee-d4d7-4b9f-b61f-4b331797ed33/mask12.jpg" alt="Clipping Masks are great for constraining Adjustment Layers." width="500" height="394" /><br>
<em>Clipping Masks are great for constraining Adjustment Layers. (<a href="https://www.sxc.hu/photo/1118481">Image Source</a>)</em>

## Clipping Paths

Clipping Paths are a lot like Vector Masks except that they <strong>apply to an entire document rather than a layer or layer group.</strong> They are primarily used by print designers to specify uniquely shaped objects that are imported into a page layout program. The path is imported along with the image to ensure a crisp clean edge.

To create a clipping path, first be sure that you have a path saved; having a temporary Work Path does not suffice. You must select "Save Path" from the fly-out menu in the Paths palette if your path is not saved. Then, from the fly-out menu, choose "Clipping Path." Your document's appearance will not change, but if you were to import the document into Illustrator using the Place command, it would be clipped to the path.

## Select and Mask

The Masks palette, introduced in CS4, adds some useful features to help with <strong>creating and refining both pixel and vector masks.</strong> For the first time, you can feather a mask and change its density without losing the original mask.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cfbe755-8335-4054-952b-21b5f03f534e/mask13.jpg" alt="Select and Mask was a great addition to Photoshop CC." width="500" height="270" /><br>
<em>Select and Mask was a great addition to Photoshop CC.</em>

### Create/View Buttons

At the top of the palette are two buttons that can be used to select the layer mask or vector mask or to create one if one doesn't exist.

### Density

The density slider basically controls how strong the mask is. At 100%, fully masked areas will be completely transparent. When density is set to 50%, those same areas would be only 50% transparent.

### Feather

Feathering the edges of a mask used to require applying a Gaussian Blur, which would destroy the original mask shape. With the Masks palette you can now <strong>change the amount of feathering at any time while maintaining the original mask data.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0caf5303-2da8-45fe-a212-168fd2cbaf2e/mask14.jpg" alt="With the Feather slider you can now change the mask's softness on the fly-" width="500" height="405" /><br>
<em>With the Feather slider, you can now change the mask's softness on the fly.</em>

### Mask Edge

The Mask Edge menu provides some long-desired features that aid in <strong>refining a mask's perimeter</strong>. They come in extremely handy when the extracted object is still picking up color from the masked background.

<strong>Radius</strong>
The Radius setting is similar to feathering, but it retains some of the edge's crispness. This can be helpful with reducing awkward or overly sharp edges on complex shapes.

<strong>Contrast</strong>
Contrast simply modifies the contrast of edge elements, which helps crispen any soft edges. Using this in conjunction with Radius can help remove unwanted artifacts in the mask.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adb1ba89-d667-470f-a655-4b4edb43c5a4/mask15.jpg" alt="Radius and Contrast can be used to remove unwanted artifacts." width="500" height="393" /><br>
<em>Radius and Contrast can be used to remove unwanted artifacts.</em>

<strong>Smooth</strong>
Smooth simplifies the complexity of the mask's edges. This can be useful if you've painted the mask by hand and need to quickly clean up some rough edges.

<strong>Feather</strong>
This feather command is nearly identical to the Mask palette's primary feather command, but it restricts the blur more to the edge of the mask. The difference is slight yet noticeable.

<strong>Contract/Expand</strong>
The Contract and Expand slider allows you to grow and shrink the edges of the mask. This is extremely useful for reducing unwanted color fringes.

<strong>Preview Mode</strong>
At the top of the palette are five different preview modes that allow you to view the mask as a selection with marching ants, quick mask ruby overlay, black matte, white matte or grayscale mask.

### Color Range

The Color Range menu is one of the most powerful ways to extract an image from an evenly colored background. With only a few clicks and adjustments, even the most complex object can be cleanly masked. For further details, see the "Techniques" section just below.

{{% ad-panel-leaderboard %}}

## Techniques

Each masking job is unique and requires a different method of creation and refinement. However, some common techniques can drastically improve the efficiency and maximize the flexibility of your masks.

### Color Range

When your masking task requires an object to be extracted from an evenly colored background (much like the video editing process of Chroma keying), <strong>the quickest means is often the Color Range command.</strong> First, use the Eyedropper Tool to select the primary color of the background. Then, you can use the "Add to sample" and "Remove from sample" tools to refine the color selection. The fuzziness slider lets you broaden the range of colors selected. If the color data is there to support it, this process makes short work of an otherwise tedious task.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/caf68d28-dbc9-46f1-a649-963498ad9778/mask16.jpg" alt="Using the Eyedropper tools allows you to easily select the sky in the photo." width="500" height="500" /><br>
<em>The Eyedropper tools allow you to easily select the sky in the photo.</em>

### Channels

<strong>A mask is often hiding in one of the layer's channels, just waiting to be unlocked.</strong> Depending on the image you're using, you may be able to find a channel with strong contrast between the target object and its surroundings. You may even want to try temporarily changing the color mode to Lab or CMYK to provide alternative channel options. Once you find a channel with a strong enough contrast, <em>Command + click</em> it to create a selection. Then, apply the selection as a layer mask. You'll then be able to tweak it as you would any other mask.

1.  The original image has strong vibrant colors, making it a great opportunity to create a mask using channels.
2.  The red channel has the foreground-to-background contrast, so we'll start there. We've copied and pasted it onto a new layer and then inverted it.
3.  The green cup is still very prominent, so we've converted the blue channel to a layer and will use it to negate the green and red cups.
4.  By setting the Blending Mode on the blue channel's layer to Multiply, we can effectively erase any extraneous white areas.
5.  The two layers are then flattened and applied as a layer mask to the original image. This leaves us with a cleanly masked blue mug.

### Pixel/Vector Hybrid

Objects will quite often have a combination of sharp edges and soft feathered edges. In instances like these, using both a pixel and a vector mask may be best. One common example of this is extracting a figure. You can use the pen tool to draw all of the smooth edges along the figure's body and then use a pixel mask to paint in the fine details such as hair.

### Multiple Masks

There may be times when you want to apply more than one mask to a layer. You could choose to apply the mask by right-clicking the layer and selecting Apply Layer Mask, after which you could apply a new mask. This, however, is not ideal because the data behind the mask will be lost.

A far better method is to <strong>create a Smart Object from the layer and mask the new layer.</strong> This allows you to apply two masks to one layer without losing data. In fact, if needed, you could repeat this process over and over.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99f7b092-f7bf-4071-9893-31b14079fc2a/mask17.jpg" alt="Converting a layer to a Smart Object allows you add multiple masks without losing data." width="500" height="842" /><br>
<em>Converting a layer to a Smart Object allows you to add multiple masks without losing data.</em>

### Layer Styles

If you have ever added a mask to a layer with layer styles, things may have gotten messy, especially if the mask had soft edges or varying opacities. This is because, by default, Photoshop uses a composite of the layer's opacity along with any masks on it to define the area used by the layer styles. This is desirable but can also be a nuisance. To counter the default behavior, open the Blending Options menu for the layer, and apply either "Layer Mask Hides Effects" or "Vector Mask Hides Effects."

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be722b59-b962-4beb-9035-4a66298141fa/mask18.jpg" alt="Messes can often be tidied by using the Layer Mask Hides Effects option." width="500" height="256" /><br>
<em>Messes can often be tidied by using the "Layer Mask Hides Effects" option.</em>

### Blend Clipped Layers as Group

By default, Photoshop assumes that all layers in a clipping stack should be blended with the base layer before the base layer is blended with the layers below it. This makes sense sometimes, but other times you may need the clipped layers to adopt the shape of the base layer but not the blend mode. To prevent this behavior, open the Blending Options menu for the base layer (right-click the layer and choose "Blending Options"), and uncheck the "Blend Clipped Layers as Group" option. Now, each of the clipped layers will blend with underlying layers as if they weren't clipped.

### Type Masks

Grouped with the Type tool in the Tools bar is the deceptively named Type Mask tool. It allows you to create type just like the regular type tool; but once committed, the type is converted to a selection. This selection can be converted to a layer mask but will no longer be editable. This is not ideal. If editability is important, you may want to create a regular type layer and use it as the base of a clipping mask. This is the only way to mask objects to the shape of type without losing the ability to edit the text. Perhaps someday Photoshop will let us create an editable Type Mask for a layer.

### Removing Edge Fringes

Even after using the "Refine Edge" command in the Masks palette, you may find <strong>random color fringes left along the edge of your mask.</strong> This is where some manual brushwork comes in handy. The Paintbrush tool can be used here, but I recommend the Healing Brush, Stamp Tool or Smudge Tool because they will blend better with the subject.

First, create a new layer and clip it to the masked layer. Then, set your tool of choice to sample all layers. You can now select your sample area and paint the fringes out; the original layer data will be preserved. Often, changing the brush's Blend Mode will help preserve the detail of the layer.

## Keyboard Shortcuts

*   View Layer Mask as an overlay
*   **Command +**  
Set layer focus to Layer Mask
*   **Command + 2**  
Set layer focus to layer data
*   **Command + Option +**  
Create selection from Layer Mask
*   **Command + Option + G**  
Make/Release Clipping Mask
*   **A, then Enter**  
Activate/Dismiss Vector Mask
*   **Command + Enter**  
Create selection from active vector mask
*   **Command + Click Mask Thumbnail**  
Create selection from mask
*   **Command + Option + Click Mask Thumbnail**  
Subtract mask from selection
*   **Command + Option + Shift + Click Mask Thumbnail**  
Intersect mask from selection
*   **Q**  
Toggle Quick Mask mode

### Inside the Color Range Menu

*   **Option**  
Toggle the Reset button and the "Subtract from Sample" tool
*   **Command**  
Toggle between the Selection view and Image view
*   **Shift**  
Toggle the "Add to Sample" tool

### Further Reading

*   [Mastering Photoshop With Paths](https://www.smashingmagazine.com/2009/08/18/mastering-photoshop-with-paths/)
You may want to take a look at related Photoshop articles:
*   [Top 10 Killer Combo Moves](https://www.smashingmagazine.com/professional-photoshop-techniques-tutorials/#a4)
*   [Unknown Tricks And Time Savers](https://www.smashingmagazine.com/professional-photoshop-techniques-tutorials/#a5)
*   [Mastering Layer Styles](https://www.smashingmagazine.com/professional-photoshop-techniques-tutorials/#c7)

{{< signature "al, il" >}}

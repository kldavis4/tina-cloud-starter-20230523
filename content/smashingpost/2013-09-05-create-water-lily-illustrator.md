---
title: How To Create A Water Lily In Illustrator
slug: create-water-lily-illustrator
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/319759c6-17dd-4c8f-9c19-3b05766fcfa6/water-lily-final2-1.jpg
date: 2013-09-05T01:42:11.000Z
author: veerle-pieters
summary: >-
  Water lilies are beautiful flowers and ideal tutorial material. To get to our result, we’ll be doing a lot of clever actions, mostly rotating and duplicating, and we’ll have a lot of room for experimentation as well. For instance, we can try out different ways to build the layers of petals, and we can play with different shades of pink gradients.
description: >-
  Water lilies are beautiful flowers and ideal tutorial material. To get to our result, we’ll be doing a lot of clever actions, mostly rotating and duplicating, and we’ll have a lot of room for experimentation as well.
categories:
  - Graphics
  - Design
  - Illustrator
  - Tutorials
---
This tutorial shows the basic steps I followed; but in creating this flower, I did way more than what is presented here. You see, every creation is never straightforward or perfect right away. It takes some trial and error, because I also needed to find the method that can be most easily explained.

## Load The Water Lily Swatches

To make it easy to apply colors and gradients repeatedly, I have saved the swatches I used in an <a href="https://cl.ly/1m0c2y1D0t0f">Illustrator swatch library file</a>. The easiest way to use a swatch library file is simply by opening it as a regular Illustrator file via <code>File → Open</code>. You may still modify the settings of the document, such as dimensions and color, via <code>File → Document Setup</code>.

If a document is already open and all set up, then you can load it into your Illustrator document by going to the swatches panel options menu, choosing <code>Open Swatch Library → Other Library…</code>, browsing to the <code>Water-lily-Swatches.ai</code> file, selecting it and clicking “Open”. Then, select the swatches and drag them into the main swatches panel of your document (<code>Window → Swatches</code>). Make sure the swatches are displayed in list view; go to the Swatches panel options menu again, and choose “Small List View.” This way, you will also see the names of the swatches.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39934ad7-9d6f-4820-8fbd-1f1786687a60/water-lily-howto30.jpg" alt="the water lily Swatches Library" width="500" />

We’ll start by building the various layers of petals, level by level. Then, we’ll create the inner part of the flower, which I’ll call the “core.” At the very end, I’ll briefly explain how I created the environment of the water and floating leaves. To help you with this part, I have added all of the colors and gradients to the <a href="https://cl.ly/1m0c2y1D0t0f">Illustrator swatch library file</a>.

## Creating The Petals

Looking at the typical shape of a water lily’s petal, I figured that using the Ellipse tool would not give us the exact result we’re after. The petal has a rather pointy tip, so I thought to use a tool that I hardly ever use, the Arc tool. This tool is hidden under the Line tool in the tools panel (hold down your mouse click to reveal the hidden tools). First, we’ll set the right options in the Arc options window.

{{% feature-panel %}}

### Create the First Petal

<strong>Define the Arc tool’s options.</strong>

To make sure you can preview things in the Arc options window, click “Fill swatch” in the tools panel, and select the “Light Pink” color swatch from the swatches panel. We’ll also need a vertical guide because we will create one fourth of a petal and then reflect this shape using the vertical guide as the axis. Drag a vertical guide from the rulers somewhere towards the center of your document. If rulers aren’t visible in your document, go to <code>View → Rulers → Show Rulers</code> or hit <code>Command/Control + R</code>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acc10275-8be5-4c46-af80-18d0e18aad10/water-lily-howto01.jpg" alt="" width="500" />

Now, double-click the Arc tool in the tools panel. In the Arc options window that appears, enter the value <code>40 px</code> for the x-axis’ length and <code>70 px</code> as the y-axis’ length. Also, for the “Type” option, choose <code>Closed</code>; for “Base Along,” choose <code>Y Axis</code>; for “Slope,” select a value of <code>40</code>; and enable the “Fill Arc” check box.

<strong>Create the arc.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1dec18c4-e7b6-4c05-a445-277e066a7809/water-lily-howto02.jpg" alt="" width="500" />

With the Arc tool still selected, click precisely on the vertical guide. The Arc window will appear showing the settings you’ve entered. Just click “OK” to create the arc object.

<strong>Copy-reflect the arc object around the vertical axis.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bb93ac9-d734-4ff3-bc4b-566178fcd033/water-lily-howto03.gif" alt="" width="500" />

With the arc object selected, select the Reflect tool from the tools panel (hidden under the Rotate tool), and click precisely on the vertical guide while holding down the <code>Alt/Option</code> key. In the Reflect options window that appears, select the vertical axis, and click “Copy.”

<strong>Copy-reflect the two arc objects around the horizontal axis.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb707fd9-bc06-42cf-a0ca-831e45cdf7e8/water-lily-howto04.gif" alt="" width="500" />

Make sure both arc objects are selected. Then select the Reflect tool again, and click precisely on the bottom line of the two objects while holding down the <code>Alt/Option</code> key to invoke the Reflect options window. This time, select the horizontal axis and click “Copy.”

<strong>Unite the four objects.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d608024-b56b-4b75-8f05-4f62096068a7/water-lily-howto05.gif" alt="" width="500" />

Select the four arc objects, go to the Pathfinder panel, and choose “Unite.” This will unite the four shapes into one. Now you have created one petal, which is the flower’s most important base element. We will use this object multiple times during this tutorial. It’s time to let those petals fly!

### Creating the Middle-Level Petals

<strong>Copy-rotate the petal.</strong>

First, drag a horizontal guide from the rulers somewhere to the bottom of the petal. The intersection of both guides will serve as the center of the flower. The position of this point is crucial, so make sure it is positioned as shown here:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47578924-724b-444a-bfa5-cb8c8f0fd5f6/water-lily-howto06.gif" alt="" width="500" />

Select the Rotate tool, and click precisely on the guides’ intersecting point while holding down <code>Alt/Option</code>. In the Rotate options window that appears, enter a value <code>90°</code> and hit “Copy” to duplicate the object. Repeat this transformation action twice by hitting <code>Command/Control + D</code> two times (or go to <code>Object → Transform Again</code> twice).

<strong>Apply a radial gradient.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72b45190-d316-445f-828e-0ecabe29ea32/water-lily-howto07.jpg" alt="" width="500" />

Select all objects and select the radial gradient swatch named “Darker Radial Gradient.” The gradient will now be applied to each petal separately, with the dark area at the center of the each petal. To change the position to the center of the flower, we need to reapply this gradient by selecting the Gradient tool and click-dragging the mouse from the center of the flower to the outside (i.e. the end of a petal). I usually do this in a straight horizontal movement, holding down the <code>Shift</code> key.

<strong>Copy rotate at 45°.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9eca2c98-57ac-4445-ba7c-a74e7738f39e/water-lily-howto08.jpg" alt="" width="500" />

With the object still selected, copy-rotate the object by copying the object (<code>Command/Control + C)</code> and pasting it in front (<code>Command/Control + F</code>, or in the menu, <code>Edit → Paste in Front</code>). With the Selection tool selected, mouse over a corner of the bounding box until the rotate cursor appears. Hold down the mouse and slowly rotate the object while holding down the <code>Shift</code> key so that the rotation jumps to 45°. When it reaches 45°, first release the mouse, then the <code>Shift</code> key.

<strong>Apply a new gradient.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dae4c04b-2873-4c0d-8fee-2bca77214bc9/water-lily-howto09.jpg" alt="" width="500" />

Select the “Light Radial Gradient 2” swatch from the swatches panel to apply this gradient to the new petals. If you like, you can tweak some of the color swatches in the gradient by double-clicking on the gradient stops (in the Gradient panel), or by sliding them to the left or right. While working on this project, I’ve tweaked them here and there, saving the gradients I like best. Feel free to play around by making them a bit more white or more pink, etc.

{{% ad-panel-leaderboard %}}

### Creating the Bottom-Level Petals

From now on, keep things as organized as possible, because we will be creating different levels of petals to build up the flower. Aside from the flower’s core and stamen, which are each on a separate layer, we’re working with five different levels, putting each level on a separate layer:

*   the top yellow petals (to be created in the last step),
*   the yellow petals (to be created in the last step),
*   the top petals (to be created in a later step),
*   the middle petals,
*   the bottom petals (to be created in this step).

<strong>Create the first bottom-level petals.</strong>

Name the layer with the middle-level petals that we’ve just created by double-clicking the layer. I’ve called it “middle petals.” Select the topmost vertical petal, copy it, and lock the “middle petals” layer by clicking in the column next to the eye icon of the layer in the Layers panel. A lock icon should appear. Create a new layer by clicking “Create New Layer” at the bottom of the Layers panel. Paste the petal in the exact same place by hitting <code>Command/Control + Shift + V</code>. Double-click the layer and name it “bottom petals.” With the layer still selected in the Layers panel, drag the layer to below the “middle petals” layer.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fca76911-85be-4a6f-8aeb-dc58e9463a2e/water-lily-howto10.jpg" alt="" width="500" />

First, we’ll resize the petal a bit, making it taller. Select the Scale tool, and click precisely at the intersecting point of the two guides (i.e. the center of the flower) while holding down <code>Option/Alt</code> to invoke the Scale window. Choose the “Non-uniform” option, and enter <code>85%</code> for “Horizontal” and <code>115%</code> for “Vertical.” Check the “Preview” option to see how this will look, and click “OK.”

<strong>Apply a gradient.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8f5d71a-2508-48b3-845d-9aa4e1e1bbdb/water-lily-howto11.jpg" alt="" width="500" />

Apply the “Light Radial Gradient 2” by selecting the swatch from the Swatches panel and then selecting the Gradient tool. Now, drag vertically straight towards the top of the petal, starting from the center of the flower, holding down the <code>Shift</code> key. To keep the petal light near the end, stop about one fourth from the end.

<strong>Copy rotate at 45°.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdbf9444-67f6-483b-96cb-c739204c15b2/water-lily-howto12.jpg" alt="" width="500" />

With the petal still selected, select the Rotate tool and click precisely at the guides’ intersecting point while holding down <code>Alt/Option</code>. In the Rotate options window that appears, enter a value of <code>45°</code> and hit “Copy” to duplicate the object. Repeat this transformation six times by hitting <code>Command/Control + D</code> six times.

<strong>Rotate at 27.5°.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/546b0f4c-8100-4b66-990c-cae363e85f97/water-lily-howto13.jpg" alt="" width="500" />

To create a bit of natural variation in the positions of the levels of petals, we’ll rotate them by 27.5°. You could, of course, choose another value — for instance, keeping the petals perfectly symmetrical and going for 22.5° instead, which is exactly half of 45°. It’s totally up to you. Make sure all petals of this level are selected. Click precisely at the guides’ intersecting point again while holding down <code>Alt/Option</code>. In the Rotate options window, enter a value of <code>27.5°</code> and hit “OK.”

<strong>Tweak the gradient where needed.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ece64563-b820-4d13-898a-a649d35d4de6/water-lily-howto14.jpg" alt="" width="500" />

While creating these different levels of petals, you can tweak the gradients of the petals at any time, making them a bit lighter or darker. Do this by sliding the gradient stops to the left or right or by changing the color of the gradient color stops (by double-clicking one of the stops of the gradient in the Gradient panel). You could, of course, leave this part till the very end, too.

<strong>Copy rotate at 27.5°.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63a2a900-6a94-4125-b745-31a940b0ba01/water-lily-howto15.jpg" alt="" width="500" />

Click precisely at the guides’ intersecting point again while holding down <code>Alt/Option</code>, and enter a value of <code>27.5°</code> in the Rotate options window. Hit “Copy” to copy this action. Choose another value here if you like. If you go for a fully symmetrical style, then try 22.5°. Apply a gradient that is light near the end of the petals. Select one of the light radial swatches and tweak if needed.

{{% ad-panel-leaderboard %}}

### Creating the Top Level of Petals

To finish off the petals, we need to add yet one more level of petals at the top. Select the four petals stacked at the top (first unlocking the “middle petals” layer by clicking the lock icon of the layer in the Layers panel), and put them in your copy memory by hitting <code>Command/Control + C</code>. Lock both the “middle petals” and “bottom petals” layers, and create a new layer by clicking the “Create New Layer” icon at the bottom of the Layers panel. Name the layer by double-clicking it; I’ve named mine “top petals.” Now, paste the petals in the exact same place by hitting <code>Command/Control + Shift + V</code>.

<strong>Rotate at 27.5°.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8e69fe6-1038-4cbd-add6-433a9eb1d11b/water-lily-howto31.jpg" alt="" width="500" />

With the petals still selected, select the Rotate tool and click precisely at the center of the flower while holding down <code>Option/Alt</code>. Enter a value of <code>27.5°</code> and hit “OK.” Again, choose whatever value you think fits best. Just check “Preview” to peek at the result.

<strong>Apply a radial gradient.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9957887-1347-4d74-9686-918ec60acd46/water-lily-howto32.jpg" alt="" width="500" />

Apply the radial gradient swatch named “Light Radial Gradient 3.” This gradient is almost the same as “Light Radial Gradient 2”, but the lighter color is a bit lighter and the color stop has been moved a little to the left to shorten the transition of the gradient, thus making the petal lighter from the middle to the end. Again, play around with the gradient color stops to create the effect you like best.

## Creating The Core And Stamen

In the next step, we’ll create the core of the flower. To get started, lock the three layers. Create a new layer, naming it “core” (or whatever you like).

### Creating the Core

<strong>Draw a circle and apply a gradient.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff525fb9-97dd-4764-8b86-c89cbeab990b/water-lily-howto16.jpg" alt="" width="500" />

Select the Ellipse tool and draw a circle from the center out, holding down <code>Alt/Option + Shift</code> while dragging. Apply the radial gradient named “Radial Core Gradient” from the Swatches panel.

### Creating the Stamen

<strong>Create a filament by drawing a rounded rectangle.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c0ae931-a4cc-4b60-a5c1-22945b287b67/water-lily-howto17.jpg" alt="" width="500" />

First, lock the “core” layer, and create a new layer, naming it “stamen.” Select the Rounded Rectangle tool, and draw a vertical rounded rectangle, as shown in the image above. Start at the top, to the left of the vertical guide, and drag diagonally to the bottom-right of the vertical guide. While dragging, you can modify the radius of the rounded corners using the up and down arrow keys.

<strong>Horizontally align the center.</strong>

To position the object perfectly in the center, select both the object and the “core” circle below it. Temporarily unlock the “core” layer to be able to select it. To select the second object in a row, hold down the <code>Shift</code> key and select the core circle again, but this time without holding <code>Shift</code>. You should see an extra-thick selection line; this means that this will be the target object to align with, and so this object will stay in its position, and only other objects will move as needed. Now, select the “Horizontal Align Center” option from the control bar at the top. If you don’t see this bar, go to <code>Window → Control</code>. After aligning the object, make sure to lock the “core” layer again.

<strong>Apply a linear gradient.</strong>

Apply a “Linear Gradient,” and enter <code>90°</code> in the “angle” field.

<strong>Scale down the bottom anchor points.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/375e60dc-8967-4fc4-a3a0-bfa26c60d007/water-lily-howto18.jpg" alt="" width="500" />

Now, we need to make the bottom part of the filament smaller. Select the Direct Selection tool (white arrow), and draw a selection over the three bottom anchor points. Select the Scale tool, and click precisely to the top anchor point of the object. Make sure you see the scale arrow cursor first somewhere near the bottom-right of the object. Now, start dragging from right to left to make the bottom part smaller (see the image for a reference). Turning on the smart guides might also help; go to <code>View → Smart Guides</code> (or hit <code>Command/Control + U</code> to toggle them on and off).

<strong>Cut a slice to create the anther.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91307f7f-60f2-4272-abfc-44627052f9a7/water-lily-howto19.jpg" alt="" width="500" />

Now we’ll create the anther. Select the Knife tool, which is hidden under the Eraser tool. Hold down both <code>Shift</code> and <code>Alt/Option</code>, and drag from left to right, crossing the object in a straight line at the very bottom (as shown in the image above). Now, the object will be cut in two parts, the filament and the anther. Select only the bottom part, and apply the “Soft Brown” color from the swatches panel.

<strong>Copy and paste in front and apply different colors.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8918e43a-4660-49b1-8abc-d413dc26fa21/water-lily-howto20.jpg" alt="" width="500" />

Copy the two objects and paste them in front by hitting <code>Command/Control + F</code>. Apply “Linear gradient 2” to the filament, making sure to enter <code>90°</code> in the “angle” field. Give the anther a “Brown” color.

<strong>Scale down and rotate manually.</strong>

In this step, we need to position the second stamen next to the first, but slightly rotated, with the rotation from the center of the flower, and also slightly smaller. We’ll first scale down the object and then rotate it into position. First, make sure the stamen is properly selected. Mouse over the top-left corner of the bounding box until you see the resizing arrows. Click and drag slightly towards the bottom right to make the object smaller. There is no need to keep the proportions exact; just make the object slightly smaller (see the image below).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5ea4711-63e5-40d3-814c-b9e125066134/water-lily-howto21.jpg" alt="" width="500" />

With the object still selected, mouse over the top-right corner of the bounding box until the rotate arrows cursor appear. Click and drag to rotate the object just slightly. An alternative here is to use the Rotate tool and rotate the object from the center of the flower. I don’t have exact measurements to give you because it all depends on the sizes of the two stamens. As you’ll see in the following steps (the second image that follows), this might require a bit of trial and error to get right.

<strong>Copy-rotate at 20°.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0291701-b74c-4e38-adbf-ab082427dea1/water-lily-howto22.jpg" alt="" width="500" />

When both stamens are aligned nicely, select them both and <code>Alt/Option</code>-click at the center of the flower. In the Rotate window that appears, make sure the <code>Preview</code> option is checked, and enter a value of <code>20°</code>. Click “Copy” to copy them.

<strong>Tweak to get it right.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f6ac184-451b-49fb-a5fc-a3ce0c0981b1/water-lily-howto23.jpg" alt="" width="500" />

If you end up with the result in the image above, then you’ll need to undo your action (using the shortcut <code>Command/Control + Z)</code> and reposition the second stamen. Make sure the stamens don’t overlap when you rotate the second one. You might need to make both stamen a bit thinner or smaller, adjust the rotation angle, or adjust the position of the second stamen; this step might require some trial and error to get right. Another option is to go with another rotation value (for example, 24°) to end up with fewer stamen (say, 15 instead of 18) — see the next step.

<strong>Transform again until you get a full circle of stamens.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d803770a-bdbf-4897-8166-061b3d2460c0/water-lily-howto24.jpg" alt="" width="500" />

When the rotations of all four stamens are right (after having hit the “Copy” button), repeat hitting <code>Command/Control + D</code> to apply the transformation again and again, until a full circle is drawn (as shown in the image above).

## Creating The Core Petals

### Creating the First Layer of Petals

<strong>Copy and paste a petal in place and resize it.</strong>

We need to do one final step to complete the flower, and that is create a layer of small yellow petals around the core of the flower. First, create a new layer, and name it (I’ve named it “yellow petals”).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f77b3bca-4160-4f24-8556-9a7eec13cbf3/water-lily-howto25.jpg" alt="" width="500" />

Unlock the “middle petals” layer, and select the vertical petal at the top. Copy the petal, re-lock “middle petals,” click the new “yellow petals” layer, and paste the petal in the exact same place by hitting <code>Command/Control + Shift + V</code>. Apple the color named “Soft Yellow for Petals.” Select the Scale tool, click the center of the flower, and manually scale down the petal, as shown in the image above.

<strong>Copy rotate at 60°.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ff23290-780e-4951-a4e8-a25c6e89a0e8/water-lily-howto26.jpg" alt="" width="500" />

Select the Rotate tool and <code>Alt/Option</code>-click in the center of the flower. In the rotate window, enter a value of <code>60°</code>, and click “Copy.” Hit <code>Command/Control + D</code> four times in a row to duplicate this transform action to complete the circle of petals.

### Creating the Second Layer of Petals

<strong>Duplicate the layer of petals.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35486014-7fca-4ac7-ad9e-b9f55d22b3c5/water-lily-howto27.jpg" alt="" width="500" />

We could do the same actions as before for this next step and copy and paste the layer of petals in place on a new layer. Instead, we’ll duplicate the petals directly onto a new layer, just to demonstrate another easy technique.

First, create the new layer on top of the current one, and name it something like “top yellow petals.” Select the layer of petals by going to the Layers panel and clicking in the area to the right of the circle icon, located on the right side of the current layer. This selects — or, more precisely, <em>targets</em> — all selectable objects of the layer. A small colored square will appear, indicating the selected art. This square wouldn’t appear if this layer was empty, which makes this a handy check whenever you want to remove unnecessary layers during or at the end of the process. We’ll duplicate the selection onto the new layer by holding down <code>Alt/Option</code> and click-dragging the colored square to the new layer above (see the image above).

<strong>Apply a gradient</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb4b2fc6-3017-4a11-ad09-81b94794792b/water-lily-howto28.jpg" alt="" width="500" />

Lock the “yellow petals” layer so that you don’t accidentally modify it. Select the newly duplicated petals, and apply the “Radial Petals Gradient” swatch.

<strong>Copy rotate at 30°.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/128718af-a6e6-4c08-9431-c4a07064708d/water-lily-howto29.jpg" alt="" width="500" />

Select the Rotate tool and click precisely at the center of the flower, holding down <code>Alt/Option</code>. In the Rotate window that appears, enter a value of <code>30°</code>, and click “Copy.”

## Create An Environment

That’s it! The flower is now finished. All that’s left is to add a layer of water and leaves below, give the flower a subtle shadow, etc. For the water, I used a radial gradient, making sure the lighter blue surrounds the flower. To help you create this environment, I’ve added all of the colors and gradients that I used to the <a href="https://cl.ly/1m0c2y1D0t0f">Illustrator swatches library</a>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a318c0f-c930-4371-be2a-c80f3b0ebf77/water-lily-final2.jpg" alt="The result of the water lily placed in a natural environment" width="500" />

For the shape of the leaves, I created a circle and a very sharp triangle at the top, which I then subtracted to create that characteristic sliver. I used the Minus Front Pathfinder option to do this, but you could easily use the Shapebuilder tool instead, holding down <code>Alt/Option</code> to remove the triangle shape. Then, it’s a matter of duplicating, rotating and scaling the leaves and applying different shades of green.

There you have it! I hope you’ve enjoyed this tutorial and maybe even learned a few things here and there. Keep experimenting, and keep it fun!

### <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Create A Dramatic Vector Illustration](https://www.smashingmagazine.com/2016/11/how-to-create-a-dramatic-vector-illustration/)
*   [The Process Behind Good Illustration (Part 1)](https://www.smashingmagazine.com/2010/06/the-process-behind-good-illustration-part-1/)
*   [Inspiring Illustrator Artworks By Artists Around The World](https://www.smashingmagazine.com/2010/03/100-beautiful-illustrator-artworks-by-artists-around-the-world/)
*   [40 Excellent Adobe Illustrator Tutorials](https://www.smashingmagazine.com/2009/09/back-to-school-with-40-excellent-adobe-illustrator-tutorials/)

{{< signature "al, il" >}}

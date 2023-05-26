---
title: Designing A Responsive Music Player In Sketch (Part 2)
slug: designing-responsive-music-player-sketch-part-2
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9800f877-3a65-4e32-8b33-b2f7097a49a8/intro-sketch-500w-opt.png
date: 2017-01-12T23:23:00.000Z
author: christian-krammer
description: >-
  Welcome to the second part of this tutorial, in which we will finish designing
  the music player that we started in [part
  one](https://www.smashingmagazine.com/2017/01/designing-responsive-music-player-sketch-part-1/).
  This includes creating the icons at the bottom, as well as making the music
  player responsive, so that all elements adapt to the width of the artboard
  and, thus, can be used for different device widths.

  Our premise in creating all of the icons is to use basic shapes as often as
  possible, instead of custom vector elements. **Shapes are much easier to set
  up and modify**, and we will still be able to combine them into more complex
  forms using Boolean operations.
categories:
  - Graphics
  - Tutorials
  - Sketch
  - Mobile
---
Our premise in creating all of the icons is to use basic shapes as often as possible, instead of custom vector elements. Shapes are much easier to set up and modify, and we will still be able to combine them into more complex forms using Boolean operations.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Using Sketch For Responsive Web Design](https://www.smashingmagazine.com/2015/04/using-sketch-for-responsive-web-design-case-study/)
*   [Sketch Vs. Figma: The Showdown](https://www.smashingmagazine.com/2017/03/sketch-figma-showdown/)
*   [Designing With Real Data In Sketch Using The Craft Plugin](https://www.smashingmagazine.com/2017/02/design-with-real-data-sketch-using-craft-plugin/)
*   [Sketch With Material Design](https://www.smashingmagazine.com/2015/05/sketch-with-material-design/)

The grid would hinder more than help in the creation of the icons, so you can hide it with `Ctrl + G`.

{{% feature-panel %}}

Let’s begin with the repeat icon in the bottom-left corner.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0410233f-9345-4d0b-99fb-35e49b35a14f/screenshot1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe0974e5-b831-4aaf-8a71-8dfb98f59d52/screenshot1-preview-opt.png" /></a><figcaption>This is the music player we started in part one of this tutorial. This second part is all about creating the icons at the bottom and making the player responsive. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0410233f-9345-4d0b-99fb-35e49b35a14f/screenshot1-large-opt.png">Large preview</a>)</figcaption></figure>

## Repeat After Me

The repeat icon is based on a simple rectangle, with dimensions of 22 × 12 pixels and fully rounded corners. Change from the fill to a border again, so that you can set the position to “center” and the thickness to “2.” For the color, choose white; the “Ends” need to be set to the middle icon in the border options. There’s also a chance we’ll want to use the same properties for the other icons, so set up a shared style: Click on the dropdown menu in the Inspector that says “No Shared Style,” select “Create New Shared Style,” and name it “Icons.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f1ccac4-9976-420c-b4fb-536ad306b5fc/screenshot15-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5fd994a-990b-4568-aa14-5d1c3e8187a0/screenshot15-preview-opt.png" /></a><figcaption>Create a shared style that combines all of the styles we will need for the icons. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f1ccac4-9976-420c-b4fb-536ad306b5fc/screenshot15-large-opt.png">Large preview</a>)</figcaption></figure>

After you have zoomed into the rectangle with `Cmd + 2`, enter vector point mode with `Enter`. Add a first point to the straight segment in the bottom left, where it meets with the curve. Copy its `X` position in the Inspector; add another point to the right, and paste this value but add “+5”. Do the same for the straight top segment, but on the right side: Add a point where it meets with the curve, copy the `X` position, add a point to the left, paste this value, and subtract “-5px”. Now, use the Scissors tool again to cut the segments between the points: first at the bottom left, then at the top right.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcb4e73d-beff-4987-b00a-9faa0cb6abd4/screenshot16-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ae3aca5-4203-4bdb-a9e1-d95f5c7a3227/screenshot16-preview-opt.png" /></a><figcaption>Add a point at the bottom-left (1), where the straight segment meets with the curve. Copy its X position in the Inspector, add another point to the right, paste this value there, and add “5px.” Do the same for the top segment, but in the inverse order (points 3 and 4). Finally, cut the segments in between with the Scissors tool. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcb4e73d-beff-4987-b00a-9faa0cb6abd4/screenshot16-large-opt.png">Large preview</a>)</figcaption></figure>

For the arrows, we can use the “Arrow” symbol again: Insert it, detach it, remove the group, set the border thickness to “2,” and resize it to a height of 3 pixels on the canvas while holding `Shift` (so that the ratio is maintained). Finally, align it to the bottom segment of the base shape.

**Note:** This might require you to change the `Y` position in `0.1` pixel increments. The easiest way is to focus this input field, hold the `Alt` key, and increase or decrease the value with the `up` or `down` arrow key.

Finally, duplicate the arrow, flip it horizontally, and align it to the top segment. Move all elements into a “Repeat” group to finish this first icon.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5ac09e1-f093-437c-be97-d18d56107cd6/screenshot17-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cce86dd5-c94a-49bc-96e6-cb069f4c80ed/screenshot17-preview-opt.png" /></a><figcaption>This is what the repeat icon looks like when it’s ready. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5ac09e1-f093-437c-be97-d18d56107cd6/screenshot17-large-opt.png">Large preview</a>)</figcaption></figure>

## At Random

Whereas we started with a rectangle for the repeat icon, the shuffle icon is based on a freeform vector shape.

Pan the canvas a bit to the right, away from the first icon, and press `V` for the Vector tool. But before you start drawing, set the “Round” dropdown menu (below the corners slider in the Inspector panel) to “Round to full pixel edges,” which will prevent points from being created with decimal numbers.

Now, click to add a point, then hold `Shift` (to constrain the movement to the horizontal axis), go slightly to the right, and make another click. Pressing `Escape` will stop the drawing process and let you focus the first point again with a click. As with the repeat icon, copy its `X` position in the Inspector, press `Escape` again, select the second point, focus its `X` field, and insert the value there, but add “+5”. Pressing `Enter` will move the point 5 pixels to the right of the other point.

Continue making the vector shape: Insert a third point at the top right with a click. Press `Escape`, focus the second point again, copy its “X” position, insert it at the third point, but add “+10.” Also copy the `Y` position — but in contrast, subtract 10 pixels here, to move the point up. For the last point, you need to constrain the movement to the horizontal axis again with `Shift` and a click to the right. Offset this one by 7 pixels on the `X` axis from the third point. Press `Escape` twice when you are finished.

You could also insert all of the points by instinct first and match their coordinates to each other later.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05235eea-7baf-47c8-b576-8016e15c147c/screenshot18-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12b28d90-b1db-47cf-ac81-a1b5a1ab0f63/screenshot18-preview-opt.png" /></a><figcaption>Create the points for the vector shape in this order. Copy the <code>X</code> (and <code>Y</code>) positions from one point to the other again for the correct placement. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05235eea-7baf-47c8-b576-8016e15c147c/screenshot18-large-opt.png">Large preview</a>)</figcaption></figure>

Give this line the same appearance as the repeat icon; the shared style we set up earlier makes this possible. Open the “No Shared Style” dropdown menu in the Inspector, and select “Icons.”

In addition to the round ends, the two points in the middle also need to be slightly rounded. Select all points with `Cmd + A` while still in vector point mode, and change the corners to “1.” Copy the right-pointing arrowhead from the repeat icon, and align it to the vector in the top right. Put them in a group, and duplicate and flip it vertically to create the second arrow. Be sure that the straight segments are at the same height.

We need to modify the second arrow slightly, so that it breaks where it meets the other one. For this, enter vector point mode for the line again, add a point before and after the intersection, and cut it with the Scissors. Trust your sense of proportion here. Finally, put these two groups into an overarching “Shuffle” group, and rejoice that you’ve finished the second icon.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94eb0838-2aec-4743-8984-e4e848e87684/screenshot19-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a11b059-24f2-432a-89bc-03c74e40b4b9/screenshot19-preview-opt.png" /></a><figcaption>Add a point before and after the intersection of the arrows, and cut it with the Scissors tool to create the final icon. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94eb0838-2aec-4743-8984-e4e848e87684/screenshot19-large-opt.png">Large preview</a>)</figcaption></figure>

## My Absolute Favorite

The third icon, which lets you favorite a song, is rather simple. You might not realize it, but it’s a heart made from a simple circle. We just need to adapt its points a bit and change the point types. Create it next to the shuffle icon with a diameter of 20 pixels, and give it the same shared style “Icons” as the previous icons.

Now, to the points: Go into vector point mode, and change the point type of the bottommost point (it should already be selected) to “Straight” with `1` on the keyboard or by selecting the relevant option in the Inspector. That’s it! Cycle to the top point by pressing `Tab` twice, move it about 7 pixels down with the arrow key, and change the point type to “Disconnected” with `3`, which lets you adapt the vector control points (the handles that stick out of the point) separately. Select the left one, move it up by 6 pixels, as well as 1 pixel to the right. Do the same for the right control point, but move it 1 pixel to the left instead.

The circle already resembles a heart; we just need to adjust the remaining points on the left and right slightly. Cycle to the left one with another press of `Tab`. This requires an “Asymmetric” point; press `4` to change to this type. With this adjustment, we are able to move the upper control point just a notch up, independent of its counterpart. This makes the heart a bit more curved at the top. Repeat the same for the vector point on the right (press `Tab` two more times to select it), and we are almost finished. All we need to do is to rename the shape to “Favorite.” That was a breeze!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7de97ae7-3bb5-47a5-b28e-9f027f11f30d/screenshot20-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/059db408-69eb-4299-800e-da8de32a3feb/screenshot20-preview-opt.png" /></a><figcaption>The adjustments to go from a circle to a heart shape. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7de97ae7-3bb5-47a5-b28e-9f027f11f30d/screenshot20-large-opt.png">Large preview</a>)</figcaption></figure>

## Turn Up The Volume

Good that we were able to relax a bit with the favorite icon, because the volume icon needs more attention. It consists of two rectangles for the speaker shape — one modified to a triangle — and some circles for the sound waves, which will be removed for the most part.

Create the first rectangle with dimensions of 12 × 10 pixels. Duplicate it, hold `Alt` (to resize it from the center), grab the middle handle of the bottom side on the canvas, and drag it down until it has a height of 16 pixels. Modify it to a left-pointing triangle, like we did for the back icon: Enter vector point mode, and insert a point in the middle of the left side while holding `Cmd`. Then, pick the points above and below, and delete them.

After you have left vector point mode of the triangle, select it together with the rectangle and apply a Union Boolean operation (with `Alt + Cmd + U`). This will create the speaker shape, which you can set to the well-known layer style “Icons.” Flattening it with “Layer” → “Paths” → “Flatten” from the menu bar will convert it to a single shape and allow you to change the corners of all points in vector point mode to “1.” However, this will remove the Boolean operation and, with it, the ability to modify the individual shapes, so create a backup first and hide it. While this is generally a good idea before flattening any shape, we will also need this backup later on for another purpose.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11be1b62-8808-4181-baff-148d24c72946/screenshot21-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4604f3b6-f712-4869-b37d-1b349401cb10/screenshot21-preview-opt.png" /></a><figcaption>Combine the rectangle and the triangle (which you created from a rectangle) to the speaker shape. To complete it, create a Union Boolean operation, set the “Icons” layer style, flatten it, and apply rounded corners of “1” for all points. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11be1b62-8808-4181-baff-148d24c72946/screenshot21-large-opt.png">Large preview</a>)</figcaption></figure>

Next, the sound waves: Add a first circle with a diameter of 18 pixels, and use the same layer style as for the speaker shape. Select it together with the speaker shape and center them on both axes, but move the circle 3 pixels to the right in succession. Duplicate it for the second sound wave, hold `Shift` and `Alt`, grab a corner handle, and drag it out from the center until the shape has a diameter of 28 pixels.

Now we need a stencil to add some points to the circles. It can be based on the triangle from the speaker shape, a copy of which we backed up earlier: Copy, paste and move it out of the hidden group to show it; also, place it at the top of the layers list with `Ctrl + Alt + Cmd + up arrow`. Before we move on, hide the flattened speaker shape with `Shift + Cmd + H`, because we need an undistracted view of the circles for the next steps. Now, change the width of the new triangle to `25px` in the Inspector panel; the height can be left as is. Setting the opacity to `50%` will make the circles shine through.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91465183-1aeb-4581-8389-e788dc226801/screenshot21a-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14d38543-515f-4f59-adf4-c7480d411449/screenshot21a-preview-opt.png" /></a><figcaption>The steps required to create the circles for the sound waves. Please note that I’ve reduced the opacity of the speaker shape to highlight the circles. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91465183-1aeb-4581-8389-e788dc226801/screenshot21a-large-opt.png">Large preview</a>)</figcaption></figure>

This allows us to enter vector point mode for both circles at the same time and to add points where they overlap with the triangle. Just make sure that it is left-aligned to the inner circle. The rest can be cut with the Scissors tool once you have left vector point mode. Unfortunately, you need to do that for each circle separately. You can remove the triangle after that, but show the speaker shape again. Finish the icon by putting all of its parts into a new “Volume” group.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ea9c8bd-922a-4661-a8d2-0c8abb7823c8/screenshot22-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c2bbf22-4aee-4c44-81d1-52cf8670144f/screenshot22-preview-opt.png" /></a><figcaption>Overlay the triangle on the circles, and add points where they overlap. Cut the rest (the red lines) with the Scissors tool. Please note that I’ve temporarily hidden the speaker shape. See the finished icon at the bottom right. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ea9c8bd-922a-4661-a8d2-0c8abb7823c8/screenshot22-large-opt.png">Large preview</a>)</figcaption></figure>

## Show Me More

After so much work, we deserve a break again. Luckily for us, the remaining “more” icon is made up of not more than three dots.

One way would be to create three circles with an offset, but we will take a slightly different approach and employ the border options instead. This has just a minor downside: The dots will not be 100% circular, but you will hardly notice that at the actual (zoomed-out) size of the icon.

Start with a horizontal line (press `L`) that is 23 pixels long and has a 6-pixel border applied to it. For the color, use white again. Open the border options, and bring your attention to the “Dash” and “Gap” fields. They allow you to create dashed or dotted lines, which we will take advantage of. For the dash, insert “1,” for the gap “8”. Voilà, this will give you three dots after you have set the ends to rounded! Just change the name to “More” and we have finished all five icons.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23cc5d2d-849b-417c-8147-f52715ca3d21/screenshot23-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a06a64d0-6b04-4bcd-adba-36edffaf72a8/screenshot23-preview-opt.png" border /></a><figcaption>Create the “more” icon from a simple line by using the “Dash” and “Gap” fields in the border options. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23cc5d2d-849b-417c-8147-f52715ca3d21/screenshot23-large-opt.png">Large preview</a>)</figcaption></figure>

Unfortunately, when you go back to full view with `Cmd + 1`, you’ll see that the icons are scattered around the bottom of the music player. Let’s bring some order to this mess.

Show the grid again (with `Ctrl + G`), and use it to align the “repeat” icon 3 grid units away from both the left and bottom edges. Lock it with `Shift + Cmd + L`. Proceed to the “more” icon and also give it a spacing of 3 units from the right artboard edge. The vertical alignment doesn’t matter at the moment. Now, select all icons (or their groups) in the layers list, including the locked one; select “Align Middle” from a right-click to align them all to the locked element, and click on “Distribute Horizontally” from the same menu to space them equally from each other. Be sure to keep the icons selected for the next step.

Things are looking much better with the distribution of the icons; however, they are still pretty prominent. To remedy this, put all of them into an “Icons” group (and move it to the bottom of the layers list), and set the opacity to `30%` with `3`. Nice! We have one last thing to do for the icons: The favorite icon should represent the selected state and, thus, have the same bright color as the progress indicator. Duplicate and move it out of the group, rename it to “Favorite highlight” and assign the corresponding color from the “Document Colors.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/055592d4-c765-44be-b84f-6c3801289cf3/screenshot24-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c07d4257-bab3-41c1-9e76-1e11283945e5/screenshot24-preview-opt.png" /></a><figcaption>The finished icons, including the full layer hierarchy and the proper alignment to the grid. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/055592d4-c765-44be-b84f-6c3801289cf3/screenshot24-large-opt.png">Large preview</a>)</figcaption></figure>

With this last action finished, the music player is complete. You have done a great job so far, but what if we want to use the player for different device sizes or widths?

Let me show you how to make the design responsive with the help of the “Group resizing” feature of Sketch.</p>

## From Fixed To Fluid

The requirement for this feature is to have a parent group that contains all of the elements created so far. Select them with `Cmd + A`, make an overarching group with `Cmd + G`, and rename it to “Container.”

If you try to resize this group now, the result will be far from pleasing, because all layers will simply stretch. With the default setting for the “Resizing” dropdown menu in the Inspector panel, both the size and spacing of an element will be relative to the parent group.

If we change this setting for some objects, we will start to see some initial results. Select the “Back button” group, for example, and set it to “Pin to corner”; this will stop the elements from being resized but will maintain the same distance from the closest edge of the parent group. Do the same for the “List button” group, and try to resize the “Container” group now. These two elements will show improved behavior.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f4ecf9c-7d4c-47dc-b29b-1c73e9da9c25/screenshot25-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a5bb093-4e4e-4093-b4c9-62fcc9807e34/screenshot25-preview-opt.png" /></a><figcaption>Default behavior, left: not good. Improved behavior, right: much better! (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f4ecf9c-7d4c-47dc-b29b-1c73e9da9c25/screenshot25-large-opt.png">Large preview</a>)</figcaption></figure>

Let’s continue with the cover. Because Sketch can’t resize a layer and keep its aspect ratio at the same time, we will simply center the element. There are two ways to achieve this:

*   The first is to “Float in place.” This maintains the size of the object, but sets the spacing relative to the parent group. This makes it also suitable to center an element.
*   The second way is the “Pin to corner” property, which we already know.

**Note:** There’s one caveat for both options of image layers. The element can’t be smaller than the container; otherwise, it will be squished. Luckily for us, there’s a way to fix this: Change to a pattern fill. To do so, copy the image layer with `Cmd + C`, add a fill to the layer, enter its options, go to the second-to-last fill type (“Pattern Fill”), click on the preview area at the left of the dialog, and paste the image with `Cmd + V`. Now, the image will clip when the container shrinks.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7a6be04-81d3-43f9-a94d-8de5378fd76f/screenshot26-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51af8766-5e11-49fb-ac13-6b02d149bba7/screenshot26-preview-opt.png" /></a><figcaption>Add a pattern fill to the image layer to improve its resizing behavior: Copy the image in the layers list and paste it into the preview area of the fill dialog. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7a6be04-81d3-43f9-a94d-8de5378fd76f/screenshot26-large-opt.png">Large preview</a>)</figcaption></figure>

The next big task is the progress indicator. It needs some more consideration; however, with a few cleverly placed subgroups, it won’t be a problem at all. In its current state, we can’t achieve what we have in mind — the bars should resize with the parent group but keep their original spacing from it. Also, the circular indicator and the current playtime need to follow the position of the colored bar. The total time, however, should be pinned to the right edge.

Before we start adding the required subgroups, we can set the “Progress indicator” group itself to “Resize object”; this will retain the spacing of the element but change the width relative to the parent group. Now, select the two bars (“Bar” and “Bar progress”), create a new “Bars” group from them, and set it to “Resize object.” It should also include the “Indicator” group (containing the circular indicator and the comet tail); change it to “Float in place” in turn. This setting makes sure that the indicator follows the colored bar. The same goes for the “Progress time” group. To conclude, pin the total time to the right edge with “Pin to corner.” Give it another try: Resize the container and see the magic unfold before your eyes.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/257a448e-f9fb-4742-9bc2-aa19e0fa6217/screenshot27-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed4da02d-73e2-4b10-9ad6-a32c6e551c8e/screenshot27-preview-opt.png" /></a><figcaption>The new layer hierarchy of the progress indicator. The colored bars below the layers and groups show the respective resizing properties. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/257a448e-f9fb-4742-9bc2-aa19e0fa6217/screenshot27-large-opt.png">Large preview</a>)</figcaption></figure>

## Over The Hill

In comparison, the adaptation of the following text layers is rather simple. The group of the song title, as well as the text layer contained within, can be set to the “Resize object” property. This will ensure that the spacing is retained and that more and more of the text will be revealed as you enlarge the parent, but the gradient will keep covering the right part. The second text layer can be centered with “Float in place” again.

This setting also plays a big role for the remaining elements, because both the controls and the icons at the bottom should keep their relative spacing from the edges of the container (respective to each other), but their size should be left untouched. Apply “Float in place” to all of the mentioned elements (or their symbols or groups). For the icons, we need to make some additional changes: We want to pin the outer two icons to the outer edges of the container. The easiest way is to set the “Icons” group to “Resize object.” This will keep the distance to the edges of the artboard but will resize the group relative to the artboard’s width.

The highlighted “Favorite” icon requires some special treatment. Currently, it isn’t tied to the “Icons” group; and moving it into this group would give it a 30% opacity. The solution is to create a new “Icon outer” group that contains both this highlighted icon and the “Icons” group. Set it to “Resize object.”

Now, we have a fully responsive music player!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66946196-8613-4ad9-ab58-1a651f25ebab/screenshot28-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/480d4d42-3645-4412-bdfe-c6fc01aa7851/screenshot28-preview-opt.png" /></a><figcaption>The required settings for the remaining elements. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66946196-8613-4ad9-ab58-1a651f25ebab/screenshot28-large-opt.png">Large preview</a>)</figcaption></figure>

In case you want to switch to a completely different device type — say, the iPhone SE — select the artboard, and select “Scale…” from “Edit” in the menu bar (or press `Cmd + K`): Entering “320px” for the “Width” will scale all elements proportionally. From there, the width of an iPhone 6 is just a simple step away: Set the artboard’s width to 375 pixels, select the “Container” group, and enter `100%` for the width in the Inspector panel. You’ll see all of the elements respond correctly.</p>

<figure><div class="aspect-ratio">{{< vimeo 196287534 >}}<figcaption>&gt;</div></figure>

## Conclusion

I hope you’ve enjoyed the second part of the tutorial and learned more about using Sketch effectively for mobile app design. In the comments below, feel free to post your questions or mention alternative approaches to making a certain part of the music player. You can also contact me on Twitter ([@SketchTips](https://twitter.com/sketchtips)) or visit my little side project, [SketchTips](https://sketchtips.info), where I provide more great tips on using Sketch.

**Editor’s note:** _Christian Krammer is a web designer and Sketch app pro who has written [_The Sketch Handbook_](https://www.smashingmagazine.com/sketch-handbook/), our brand new Smashing book. If you want to master all the tricky, advanced facets of Sketch, we recommend you get the book. It’s filled with practical examples and tutorials over 12 chapters and is available both in print and as an e-book._

{{< signature "mb, al" >}}


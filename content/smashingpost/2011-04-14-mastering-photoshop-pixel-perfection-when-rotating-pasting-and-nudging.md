---
title: 'Pixel Perfection When Rotating, Pasting And Nudging In Photoshop'
slug: mastering-photoshop-pixel-perfection-when-rotating-pasting-and-nudging
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b80cde-6347-44dd-96ff-606a9be3b9b8/pixelated-screw-illu.jpg
date: 2011-04-14T12:00:47.000Z
author: marc-edwards
summary: >-
  When creating Web and app interfaces, add this small changes to your workflow. Move, rotate and paste maintaining the highest-quality artwork from the start to the end of the project.  
description: >-
  When creating Web and app interfaces, add this small changes to your workflow. Move, rotate and paste maintaining the highest-quality artwork from the start to the end of the project. 
categories:
  - Graphics
  - Techniques
  - Photoshop
---

When creating Web and app interfaces, most designers slave over every single pixel, making sure it’s got exactly the right color, texture and position. If you’re not careful, though, some common functions like moving, rotating and pasting can undo your hard work, resulting in a blurry mess. But with some small changes to your workflow, you should be able to maintain the highest-quality artwork from the start to the end of the project.

{{% feature-panel %}}

## Pixel-Perfect Rotation

If you’re not careful, rotating layers in Photoshop can damage them in a very noticeable, pixel-mashing way.

When rotating layers with Free Transform (and some other tools) to exactly 90 or 270°, the quality of the outcome is determined by the layer’s size. If the layer is of an even width and even height, then you’ll be fine. If it’s of an odd width and odd height, you’ll also be okay. But if they’re of an odd width by even height or even width by odd height, then you’ll see something like the result below:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ea36c35-0225-4f85-880b-7c1554c8a620/pixel-rotation.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58d16aa2-f3d6-4905-9e82-4d23de21ab19/mastering1.gif" alt="" width="481" height="444" /></a><figcaption>Pixel perfect rotation &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ea36c35-0225-4f85-880b-7c1554c8a620/pixel-rotation.png">Large preview.</a></figcaption></figure>

In this case, the artwork is 20 &times; 9 pixels: even-by-odd dimensions. The results for bitmap layers and vector layers are different, but they both produce unusable results because the origin of rotation doesn’t fall on an exact pixel boundary.

### A Fix

Because even-by-odd or odd-by-even dimensions are the problem, we need a way to ensure that the contents of the layer are odd-by-odd or even-by-even. Probably any method you can think of will solve this problem, be it adding a square bitmap mask to a layer or adding more content to the layer that you’re rotating. You could also draw a square on another layer and rotate both at once.

As long as the dimensions for the layer or layers are even-by-even or odd-by-odd, it’ll be fine.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ac2e889-cb3e-4292-b2e0-5713513fecc7/square-selection.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c8ea227-d031-4380-a8ff-b377914a13ce/mastering2.gif" alt="" width="231" height="230" /></a><figcaption>Square selection &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ac2e889-cb3e-4292-b2e0-5713513fecc7/square-selection.png">Large preview.</a></figcaption></figure>

### An Easier Fix

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d1f4bea-4a0e-4a44-bfc9-60ceaef6d2a0/rotation-origin.png" alt="rotation-origin" width="191" height="55" /><figcaption>Changing the origin of rotation.</figcaption></figure>

Changing the origin of rotation to the top left (or any other corner) will ensure it is on a pixel boundary, guaranteeing perfect results every time. To do this, click on a corner origin after selecting the Free Transform tool, but before rotating. This works brilliantly and is the simplest solution yet.

Bitmap and vector masks are affected by this issue as well, so please take care. But the issue affects only rotated layers, either via “Free Transform” or “Transform” under the *Edit* menu. Rotating the entire canvas via *Image → Image Rotation* has no problem.

To make things even easier, I’ve created some <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8a37f65-936f-450b-baa8-993781aef6fc/photoshop-actions-and-workflows.zip">Photoshop Actions and Workflows</a> that take care of everything for you.

## Pixel-Perfect Vector Pasting

If you’ve drawn pixel-snapped artwork in Illustrator and pasted it into Photoshop as a shape layer, you may have noticed that the result is not quite what you expect (i.e. a perfectly sharp image), but rather a blurry mess. Here’s how to fix that.

Below is some artwork as it appears in Illustrator: perfectly formed, snapped to the pixel grid, and at the size we intend to use it in Photoshop.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1a63a47-c406-48b6-a9ae-7252da2f8066/illustrator-vector.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63884960-bc88-435d-8cfd-c75ec49571ba/mastering3.gif" alt="" width="546" height="290" /></a><figcaption>Artwork as it appears in Illustrator &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1a63a47-c406-48b6-a9ae-7252da2f8066/illustrator-vector.png">Large preview.</a></figcaption></figure>

Below are the same paths pasted into Photoshop a few times. Notice how only the top-left version is sharp, while the others are half a pixel out on the x axis, y axis or both.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b195034-daa4-414c-8a98-d871112e0165/paste.jpg" alt="" width="524" height="463" /><figcaption>Same paths pasted into Photoshop.</figcaption></figure>

{{% ad-panel-leaderboard %}}

### What Went Wrong?

Photoshop’s pasting behavior works in one of two ways. If you’ve made a selection, then the clipboard’s contents are pasted so that the center of the clipboard is aligned with the center of the selection. If a selection hasn’t been made, then the contents are pasted so that the center of the clipboard aligns with the center of your current view. The level you’re zoomed into and the portion of the document you’re viewing determines the result.

### A Fix

Our test artwork is 32 pixels wide by 12 pixels high. Drawing a 32 &times; 12 marquee selection in Photoshop forces the artwork to land exactly where we want it and to be pixel-aligned. This works every single time.

### An Easier Fix

The marquee doesn’t have to be the exact size of your artwork, though. In our case, a 2 &times; 2-pixel selection would work just as well, because the center of an even-width-and-height marquee selection and the center of even-width-and-height clipboard contents would fall exactly on a pixel boundary, which is what we want. If the artwork was an odd width and height, then a 1 &times; 1 selection would have been required.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/795e76f0-b6ff-4154-bcd1-dbdea76434e4/mastering5.gif" alt="" width="544" height="162" /><figcaption>The marquee doesn’t have to be the exact size of your artwork.</figcaption></figure>

If you couldn’t be bothered noting your artwork’s dimensions, then by drawing an appropriately sized marquee, you can draw a 2 &times; 2-pixel selection and paste. If the image is blurry on the x axis only, make the selection 1 &times; 2 and paste again. If the image is blurry on the y axis only, make the selection 2 &times; 1 and paste again. If the image is blurry on both axes, make the selection 1 &times; 1 and paste again.

It may sound complex, but in practice it’s very quick; you’ll only ever have to paste twice to get sharp vector paths from Illustrator.

### Smart Objects

Pasting elements as smart objects doesn’t come with the same issue (at least not in Photoshop CS5 anyway). I like to use Shape layers, though: they allow more control and editability and have better anti-aliasing.

## Pixel-Perfect Vector Nudging

When nudging vector points, Photoshop exhibits some strange behavior, related to how far you’re zoomed in. At 100%, nudging with the arrow keys will move your vector point exactly 1 pixel. At 200%, nudging moves the point by half a pixel. At 300%, it moves by a third of a pixel.

The behavior seems intentional, but it’s not usually what I’m after. Most of the time, I want to nudge in whole pixel increments. Here’s how you can do that, without zooming out to 100%.

Open your document, and then create a second window by going to *Window → Arrange → New Window*. You can then resize the new window and place it out of the way.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d9aa204-cedf-46cf-b768-ef58622213e6/nudging-menubar.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb58ca76-5766-4906-be0a-4b9ba06157bf/mastering6.jpg" alt="" width="500" height="351" /></a><figcaption>Pixel-Perfect Vector Nudging &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d9aa204-cedf-46cf-b768-ef58622213e6/nudging-menubar.jpg">Large preview.</a></figcaption></figure>

Edit in the other window as normal, zooming in as far as you’d like. You’ll now be able to press <kbd>Cmd</kbd> + <kbd>&#96;</kbd> to switch back to the window that’s zoomed to 100%, nudge using the arrow keys, and then press <kbd>Cmd</kbd> + <kbd>&#96;</kbd> to switch back again. Because the other window is zoomed to 100%, nudging will move the selected vector points exactly 1 pixel.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94482ecd-5414-445b-94ce-b6a50f7747f5/nudging-windows.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2decf7be-bdf4-4ee2-9873-a77e5b7a38fd/mastering7.jpg" alt="" width="550" height="720" /></a><figcaption>Nudging windows &ndash; <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94482ecd-5414-445b-94ce-b6a50f7747f5/nudging-windows.jpg">Large preview.</a></figcaption></figure>

Please note that holding <code>Shift</code> while using the arrow keys to nudge always moves by 10 pixels, no matter how far in you’re zoomed. Also, dragging points with the mouse will snap to pixels in most situations &mdash; most, but not all.

While not perfect, this technique does remove some of the frustration with editing detailed vector paths in Photoshop. Or maybe it’s just another reason why complex shapes should be drawn in Illustrator first, and then pasted as shape layers?

{{% ad-panel-leaderboard %}}

## Take Charge Of Your Pixels

Using the correct techniques, it should be easy to place pixels exactly where you want. Remember, you’re the one in charge. Demand that they fall in line. Accept nothing less than pixel perfection.

Would you like to know more about a particular technique or Photoshop feature? Please let us know in the comments.

### Further Reading

*   [Mastering Photoshop: Unknown Tricks and Time-Savers](https://www.smashingmagazine.com/2010/01/obscure-adobe-photoshop-time-savers/)
*   [The Ultimate Guide To Cloning In Photoshop](https://www.smashingmagazine.com/2010/03/the-ultimate-guide-to-cloning-in-photoshop/)
*   [Noise, Textures, Gradients and Rounded Rectangles](https://www.smashingmagazine.com/2011/02/mastering-photoshop-noise-textures-gradients-and-rounded-rectangles/)
*   [Useful Photoshop Tools and Techniques For Your Workflow](https://www.smashingmagazine.com/2011/05/useful-photoshop-tools-and-techniques-for-your-workflow/)

{{< signature "al, mrn, il" >}}

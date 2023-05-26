---
title: 'Illustrator’s Live Trace: Sketch To Vector'
slug: illustrator-s-live-trace-sketch-to-vector
image: null
date: 2010-11-15T12:52:25.000Z
author: sharon-hart
description: >-
  In this post we will take a drawn design, scan it and clean it up in Photoshop, then trace it using the Live Trace feature in Adobe Illustrator.
categories:
  - Graphics
  - Illustrator
  - Tutorials
  - Drawing
---
Live Trace was introduced in Adobe Illustrator CS2 but is still a powerful tool available in Illustrator CS5. This process really gives an artist the freedom to <strong>digitally experiment with drawings of any kind</strong>. The vector art it produces can be used in numerous ways and is easily customized.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Pen Tool Vs. Live Trace: The Big Comparison](https://www.smashingmagazine.com/2016/02/pen-tool-live-trace-comparison/)
*   [ Things You Didn’t Know Your Doodles Could Accomplish](https://www.smashingmagazine.com/2013/10/things-you-can-accomplish-with-hand-sketching-doodling/)
*   [I Draw Pictures All Day](https://www.smashingmagazine.com/2012/08/i-draw-pictures-all-day/)
*   [40 Excellent Adobe Illustrator Tutorials](https://www.smashingmagazine.com/2009/09/back-to-school-with-40-excellent-adobe-illustrator-tutorials/)

My motivation for trying this was originally to make a "growing vine"-type animation in Adobe After Effects. I will show a link to the resulting animation at the end of this tutorial, but for now, let's get started.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a99be4aa-536a-4f84-9c76-f45a86519f3a/1frame2.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a99be4aa-536a-4f84-9c76-f45a86519f3a/1frame2.jpg" alt="Screenshot" width="500" height="353" /></a></figure>

{{% feature-panel %}}

## Scan And Clean Up

Scan your sketch and bring the image into Adobe Photoshop. Make sure that the image is Grayscale (<strong>Image</strong> → <strong>Mode</strong> → <strong>Grayscale</strong>). Begin by adjusting the image using <strong>Image</strong> → <strong>Adjust</strong> → <strong>Brightness/Contrast</strong> → <strong>Levels</strong> (<code>Cmd/Ctrl + L</code>) and/or <strong>Curves</strong> (<code>Cmd/Ctrl + M</code>) to improve upon the sharpness and contrast if needed. Clean the image using the Eraser Tool (<code>E</code>), trying to get the white areas as clean as possible. Paint the black areas, and alter or redesign any shapes so you are happy with the overall design.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1391cae5-da59-4876-b4c8-49d586229f6d/2-copy.jpg"><img loading="lazy" decoding="async" class="72413" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1391cae5-da59-4876-b4c8-49d586229f6d/2-copy.jpg" alt="Screenshot" width="500" height="352" /></a></figure>

Cleaning up the image is important for getting a good trace in Illustrator. There are a number of techniques that help get rid of unwanted specks and imperfections, here's the method I used:

Go to <strong>Select</strong> → <strong>Color Range</strong>:

*   Sample Colors: Select from drop-down.
*   Localized Color Clusters: Leave this deselected in the beginning.
*   Fuzziness: Play with this setting to get the edges less, or more, sharp.
*   Selection Preview: Select None.
*   Invert: Choose this if you would rather preview selected pixels as black instead of white.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df0558c5-5f35-4aa8-984c-e342c4ceee2a/cleanup4-new-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df0558c5-5f35-4aa8-984c-e342c4ceee2a/cleanup4-new-opt.png" alt="Screenshot" width="522" height="529" /></a><figcaption>Color range preview</figcaption></figure>

Use the Eyedropper Tool to click on your image and to sample the colors you want included. Because we chose the Selection preview (and Invert is not selected), you will see the selected pixels as white, so white = selected. Using the Eyedropper Tool, zoom into your main drawing (<code>Cmd/Ctrl + Scroll</code>) so you can see the pixels you are selecting. View the results on the <strong>Color Range</strong> preview.

*   Add to Sample and Subtract from Sample: Use these Eyedropper Tools (to the right of the main Eyedropper Tool) to select or take away from the preview image.

If you have trouble areas, you can select the <strong>Localized Color Clusters</strong> box and this will help add or take away from localized areas (not the whole image). When you are happy with the selection, click OK; you should now see dancing ants. Make a new layer and click on that empty layer. Go to <strong>Edit</strong> → <strong>Fill</strong> (<code>Shift + F5</code>) and fill with black.

Turn off your previous layer. The result should be a much cleaner version of your image. It may take a few experimental tries, since every drawing is different. When you are done, save the image as a .PSD file (this is important for editing it later in Illustrator).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6799b6a-2ffc-4e05-9480-02e3b9023e22/3-copy.jpg"><img loading="lazy" decoding="async" class="72622" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6799b6a-2ffc-4e05-9480-02e3b9023e22/3-copy.jpg" alt="Screenshot" width="520" height="380" /></a></figure>

Lastly, take the Eraser Tool (<code>E</code>) and separate parts of the image that run together, isolating each component image or shape that you want separated. An alternative is to select small shapes with the Magic Wand Tool (<code>W</code>) and add a 2-4 pixel white stroke (Edit &gt; Stroke) to slightly separate shapes. This is to avoid having large groups of your drawing connected with anchor points when it is converted to vectors. There are methods to cut and separate these areas later (which will be explained), but it's a good idea to try to achieve this early-on.</p>

## Tracing In Illustrator

Open a document in Illustrator and place your clean PSD image. Click on the image to select. Click the small box to the right of the Live Trace button called Tracing Presets and Options and scroll down to Tracing Options.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d408e4c3-71da-483f-8410-d816c4d9928c/tracoptdialbox-new-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d408e4c3-71da-483f-8410-d816c4d9928c/tracoptdialbox-new-opt.png" alt="Screenshot" width="281" height="572" /></a><figcaption>Tracing options</figcaption></figure>

The <strong>Tracing Options</strong> dialogue box will open. There are many preset selections to choose from but we're going to use our own settings to get the best possible trace:

*   Check Preview: Now you can see the effects live as you change the settings.
*   Check **Ignore White**: Now the white background is not present.
*   Set the Mode: Select **Black and White**. Leave Raster set to **No Image** and Vector set to **Tracing Results**, and check Fills.

Since you can see the results live, it helps to play with the settings a bit to get used to what effect they have. The way to think of the settings is that the left side (Adjustments) resembles Photoshop, and is conditioning the raster image before it is traced; the right side (Trace Settings) resembles Illustrator, and is taking the conditioned rasterized image and converting it to paths. Let's look at what the most relevant settings do.

*   **Threshold:** This value determines which pixels are white and which are black. Any pixels lighter than the Threshold value are turned white and all pixels darker will become black. For instance, making the threshold higher means that more of the darker pixels will be included in the vector shape.
*   **Blur:** This blurs the original image before its traced, which helps smooth out jagged edges.
*   **Resample:** This may come as a surprise to some, but with Live Trace, a higher resolution doesn't necessarily translate to a better traced result. In many cases, a high-resolution file can add unwanted complexity to a traced file. So play with this feature to see if your image might do better using a lower resolution.
*   **Path Fitting:** The lower the number/setting, the tighter the image will be traced. If it's too low you could get a jaggy effect. The higher the number/setting, the smoother the effect, but you lose detail.
*   **Minimum Area:** Defines the minimum area that will be traced, which helps get rid of the imperfections or "dirty" areas you don't want to capture. This setting determines the pixel minimum area, so anything smaller won't be traced.
*   **Corner Angle:** Sets the sharpness of the corner angles. The lower the number/setting, the sharper the corners.

When you are happy with the settings, be sure to first <strong>Save Preset.</strong> This is on the right of the Tracing Options dialogue box and will come in very handy if you need to make some other changes before tracing again. Once you've saved, hit Trace. You will then need to hit the Expand button or <strong>Object → Live Trace → Expand</strong> to see the actual results.</p>

## Edit And Tweak The Results

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ceaf8cc-29de-4e26-ba75-51f81654380b/6-copy.jpg"><img loading="lazy" decoding="async" class="72417" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ceaf8cc-29de-4e26-ba75-51f81654380b/6-copy.jpg" alt="Screenshot" width="500" height="352" /></a></figure>

### Separate Grouped Vector Objects

Be sure to <strong>Ungroup</strong> (<code>Shift + Cmd/Ctrl + G</code>) (<strong>Object &gt; Ungroup</strong>) as many times as necessary to make sure everything is ungrouped.

In the above images you can see that I did some editing to my original trace. Some shapes were unwittingly grouped together, despite my efforts in Photoshop to keep them separate. Luckily, should this happen, there are a few easy solutions.</p>

<strong>Revise the Original Image:</strong>

It is easy to go back and quickly edit your image in Photoshop with a click of a button. The <strong>Undo</strong> (<code>Cmd/Ctrl + Z</code>) command will need to be applied until you return to the raster image (hence saving the preset, so we can use it again here):

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad9f3505-6bd7-4d10-97f1-b06696055b74/links-panel-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad9f3505-6bd7-4d10-97f1-b06696055b74/links-panel-opt.png" alt="Links Panel" width="337" height="990" /></a><figcaption>The Links panel</figcaption></figure>

Go to the <strong>Links</strong> panel (<strong>Window &gt; Links</strong>) and click on the little pencil icon in the lower right corner. It can now be instantly edited in Photoshop. When the editing is done, close the window and when prompted, choose to update/save the changes in Illustrator. You can now use your preset to re-apply the trace in Illustrator.</p>

<strong>Use the Knife Tool:</strong>

Another solution is to simply use the Knife Tool (pictured above, it is part of the Eraser group on the tool bar) to cut grouped anchor points apart. It helps to <strong>View Outlines</strong> (<code>Cmd/Ctrl+Y</code>). You can also hold down <code>Alt</code> to have the knife tool cut a straight line. Zoom in by scrolling while holding <code>Cmd/Ctrl</code>. The Delete Anchor Point Tool (Pen Tool + minus sign) is another tool for deleting anchor points and separating grouped objects.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c420e46-aace-4878-801b-6ca4b12c8ab4/knife-tool-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c420e46-aace-4878-801b-6ca4b12c8ab4/knife-tool-opt.png" alt="The Knife tool" width="42" height="577" /></a><figcaption>The "Knife" tool</figcaption></figure>

<strong>Live Paint (see "Inspirational Suggestions" section below):</strong>

This feature doesn't actually alter any of the vector groupings; instead it allows the coloring and texturing of any lines or shapes, regardless of how they are grouped.</p>

### Reduce the Number of Anchor Points

Live Trace tends to produce an extraneous amount of anchor points in some places. To get rid of some of these we can use the Smooth Tool (pictured in the above image). Click and drag to simplify and reduce the anchor points and to smooth curves.</p>

### Touch-Ups

If some shapes did not trace properly (as with the circles in the example below), they can quickly be redrawn. It's helpful to lock down the original raster art on the background at around 20% opacity.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22ffce82-e57d-4976-b45e-35c39b9e8611/main3.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7716dfad-1781-48ef-9429-342929d73a36/final-result.jpg" alt="The final result" width="500" height="373" /></a><figcaption>The final result</figcaption></figure>

Animated Illustration

## Design Techniques

At this point you can alter, delete or add to your vector design as you creatively see fit. I experimented with patterns, textures and backgrounds. The main thing is that you now have your art in vector form and can easily alter it in many creative ways. Here are a few brief suggestions for techniques that are useful:

### Adobe Kuler

An extension handy for anyone using Illustrator, <a href="https://kuler.adobe.com/">Adobe Kuler</a> puts a pallet of suggested and popular color combinations that can be added to the swatches panel. <a href="https://layersmagazine.com/kuler-color-illustrator.html">This tutorial</a> shows a way to create and load your own Kuler swatches from the Kuler website to your Illustrator library. Another great informational video tutorial: <a href="https://tv.adobe.com/watch/learn-photoshop-cs4/using-kuler-color-themes/">Learn CS4 Design Premium: Using Kuler Color Themes</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f89aa4-f10b-4169-abd8-e62a9688a3df/adobe-kuler-extension-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f89aa4-f10b-4169-abd8-e62a9688a3df/adobe-kuler-extension-opt.png" alt="Adobe Kuler screenshot" width="282" height="760" /></a><figcaption>Adobe's Kuler extension</figcaption></figure>

### Live Paint

Live Paint deserves a tutorial of its own, as there are many features; a quick mention is worth it here, because Live Paint can easily fill in shapes without having to alter the vector groupings:

Select your artwork and go to the <strong>Object</strong> menu. Select <strong>Live Paint &gt; Make</strong>. Select the <strong>Live Paint Bucket</strong> (K) and fill the cells with the desired colors.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6afec6f1-d925-4585-9129-b506487386bb/111.jpg"><img loading="lazy" decoding="async" class="72273" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6afec6f1-d925-4585-9129-b506487386bb/111.jpg" alt="Screenshot" width="500" height="359" /></a></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3f50d7a-be25-49e6-b862-e104440b133b/live-paint-bucket-tool-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3f50d7a-be25-49e6-b862-e104440b133b/live-paint-bucket-tool-opt.png" alt="Live Pain Bucket" width="319" height="373" /></a></figure>

### Recolor Artwork

Great for playing with color combinations. This feature takes the existing colors and provides complimentary color options which can be viewed instantly. To open the palette, select your artwork and click the little colorful circular button on the top menu, or choose <strong>Edit &gt; Edit Colors &gt; Recolor Artwork</strong>. This is pretty intuitive to use, but here is a great <a href="https://www.youtube.com/watch?v=2uVjDKxETUg">tutorial</a> from Mordy Golding if you're interested in an in-depth look.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b78fac0d-26bb-4aae-8c20-1cadd5bc0a8b/recolor-artwork-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b78fac0d-26bb-4aae-8c20-1cadd5bc0a8b/recolor-artwork-opt.png" alt="Recoloring artwork" width="520" height="434" /></a><figcaption>Recoloring artwork</figcaption></figure>

### Credits, Links And Resources

*   [Fridays with Mordy](https://fridays.mordy.com/) I've seen Mordy Golding pop up, over and over again, in video tutorials about Illustrator. He has a great deal of valuable information. This link takes you directly to his "Fridays with Mordy: Live Trace in Illustrator" podcast.
*   [Lynda.com](https://www.Lynda.com/freepass/mordy) This website has many useful video tutorials, including ones on the Live Trace feature. Access them by subscription, or by signing up for their 7-day free trial.
*   [Tweak to Get the Perfect Trace](https://www.adobe.com/designcenter/illustrator/articles/illcs2at_tweak_print.html) From the Adobe website, this gives an in-depth explanation of all the options in the Trace Settings feature.
*   [Live Trace Tricks in Adobe Illustrator](https://layersmagazine.com/live-trace-tricks.html) This video tutorial from Layers Magazine is more about using Live Trace for color photographs, but I thought I'd include it since it's a nice variation and describes the Live Paint Bucket feature very well.

This is a nice, simple tutorial for adding textures.

{{< signature "rk, ik, vf" >}}


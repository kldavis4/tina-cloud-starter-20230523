---
title: 'Ready For Retina HD: Create Pixel-Perfect Assets For Multiple Scale Factors'
slug: create-assets-for-multiple-scale-factors
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c59d6e8b-5ae0-4c38-a052-0e97c3c7ebe6/03-pathfinder-opt.png
date: 2014-10-15T17:00:55.000Z
author: karstenbruns
description: >-
  The 6 Plus is the first iPhone that sports a “Retina HD” display — the
  sharpest display Apple has ever made. It forces designers to provide an
  additional set of image resources to developers to match that sharpness.

  We needed only one set of assets for the original iPhone up to iPhone 3GS. And
  when iPhone 4 came out with the Retina display, we also needed 2x assets —
  images twice as detailed. Now, with the display of the 6 Plus being even more
  detailed than that of the iPhone 4, **we will also need to provide 3x
  assets**. The numbers 1x, 2x and 3x are also called “scale factors.”
categories:
  - Mobile
  - Graphics
  - Icons
  - Vectors
  - Tutorials
  - Photoshop
  - SVG
---
The 6 Plus is the first iPhone that sports a “Retina HD” display — the sharpest display Apple has ever made. It forces designers to provide an additional set of image resources to developers to match that sharpness.

We needed only one set of assets for the original iPhone up to iPhone 3GS. And when iPhone 4 came out with the Retina display, we also needed 2x assets — images twice as detailed. Now, with the display of the 6 Plus being even more detailed than that of the iPhone 4, <strong>we will also need to provide 3x assets</strong>. The numbers 1x, 2x and 3x are also called “scale factors.”

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Retina Asset Workflow You’ve Always Wanted For Photoshop](https://www.smashingmagazine.com/2016/03/the-retina-asset-workflow-youve-always-wanted-for-photoshop/)
*   [Photoshop Etiquette For Responsive Web Design](https://www.smashingmagazine.com/2016/08/photoshop-etiquette-for-responsive-web-design/)
*   [Retinize It: Free Photoshop Action For Slicing Graphics For HD Screens](https://www.smashingmagazine.com/2013/07/retinize-it-photoshop-action-slicing-graphics-retina/)

Of course, Android developers have always had to deal with many different sets of assets. Still, designers are finding themselves questioning their production workflow. In this article, we’ll focus on iOS, but you could easily extend this approach to Android and the web. We won’t try to provide a silver bullet, and perhaps other ways might seem easier at first, but this article lays out a solid workflow that scales up for big projects.

{{% feature-panel %}}

First off, your icon sets should be vector-based. The approach described in this article focuses on generating multiple asset versions from a single vector shape in a Photoshop document that contains all of your icons.

A unified icon document has the advantage of keeping everything together in one file, allowing you to see how well your icons and assets harmonize.

If you’re designing for iOS 7 and above, then you might think that 1x versions aren’t needed anymore. However, you’ll still need them for devices such as the original iPad Mini, the iPad 2 and potentially Android and the web.</p>

## Set Up Photoshop

First, I’ll show you how I set up Photoshop. If you know what you’re doing, you can use other settings. But for those curious about how I like to work, this is it:

1.  Disable eye candy like “Animated Zoom” and “Flick Panning.”
2.  Disable “Snap Vector Tools and Transforms to Pixel Grid.”

The first point is a matter of personal taste, but not following the second point can get in your way when you’re trying to be precise with the Direct Selection tool.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3188e197-8983-45c6-93e9-ba6ed476c8d7/01-photoshop-settings-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/522ce08a-985c-49cb-bd8d-6b9277dbdcc1/01-photoshop-settings-opt-500.png" alt="These selections will help you working precise with the Direct Selection tool." width="500" height="367" /></a><figcaption>These selections will help you working precise with the Direct Selection tool. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3188e197-8983-45c6-93e9-ba6ed476c8d7/01-photoshop-settings-opt.png">View large version</a>)</figcaption></figure>

Then, I’ll configure the Move tool (<code>V</code>) to select layers. You don’t need to check “Auto-Select” because you can select a layer automatically by pressing the <code>Command</code> key while clicking. Disabling this option protects you from moving layers unintentionally.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3019b4e-e0b1-49a1-93f2-007c4259be8c/02-move-tool-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d034dd92-0a8e-4340-b8c3-bde051feb3cc/02-move-tool-opt-500.png" alt="Configure the Move tool (V) to select layers." width="500" height="307" /></a><figcaption>Configure the Move tool (<code>V</code>) to select layers. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3019b4e-e0b1-49a1-93f2-007c4259be8c/02-move-tool-opt.png">View large version</a>)</figcaption></figure>

## Feel Free

First and foremost, I believe that design and production are two separate phases. <strong>When your creativity is flowing, you shouldn’t worry much about production constraints.</strong>

Design at your favorite resolution (perhaps 2x), and lay out using the dimensions of a device you’re familiar with. But definitely use a real device, and use apps like Skala Preview and xScope to mirror the design live on your device. You should not be working with apps unless you are constantly checking the design on a real device.</p>

## Tidy Up Those Vectors

As noted, I’ll assume that you’re designing your icons in Illustrator. Before copying them to Photoshop, you’ll need to tidy them up. Use Pathfinder to add and subtract paths until you have a single shape.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c59d6e8b-5ae0-4c38-a052-0e97c3c7ebe6/03-pathfinder-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9be071d9-f487-49c6-a09b-f2e831b0084a/03-pathfinder-opt-500.png" alt="If you design your icons in Illustrator, you need to tidy them up before copying them to Photoshop." width="500" height="293" /></a><figcaption>If you design your icons in Illustrator, you need to tidy them up before copying them to Photoshop. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c59d6e8b-5ae0-4c38-a052-0e97c3c7ebe6/03-pathfinder-opt.png">View large version</a>)</figcaption></figure>

On the left above is a complex icon made up of multiple shapes, including a white shape to simulate transparency. For the icon on the right, I subtracted the white rectangle from the black one behind it. Do this by selecting the two rectangles and pressing the “Minus Front” button in the Pathfinder panel. Then, select all shapes and click “Unite” to combine them into one.

Now, copy the path to Photoshop, and paste it as a shape layer.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81431c35-53e4-4009-ae94-b87be8c8b64a/04-shape-layer-opt.png" alt="Paste your path as a shape layer." width="500" height="323" /><br>
<figcaption>Paste your path as a shape layer.</figcaption></figure>

If your shape ends up a mess, that means you didn’t tidy the vector graphic properly.</p>

## Align Forces

When you paste the icon in Photoshop, it might look something like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c2d5aa8-9a1c-4413-8537-005f3d910a6d/05-blurry-asset-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afcf85f6-f0f7-450a-ba35-c6ae17a0384c/05-blurry-asset-opt-500.png" alt="When you paste the icon in Photoshop you will probably see those gray pixels around the shape." width="500" height="280" /></a><figcaption>When you paste the icon in Photoshop you will probably see those gray pixels around the shape. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c2d5aa8-9a1c-4413-8537-005f3d910a6d/05-blurry-asset-opt.png">View large version</a>)</figcaption></figure>

When you zoom in close on the icon, you will probably see those gray pixels around the shape. Those “partial pixels” occur if a shape does not fill an entire pixel. We don’t want any of those.

We want to start working from a 1x version of the icon because, when tidied up properly, you will be able to scale this version up to 2x and 3x without any problems. If you did the original design in 2x, then you’ll need to scale the shape down to 50%.

Now it’s time to align the horizontal and vertical lines to the next full pixel. It’s OK if curves and diagonal lines don’t fill up entire pixels.

Use Photoshop’s Direct Selection tool to mark a group of misaligned anchor points, and use the arrow keys to move these points between two pixels.</p>

<strong>Note:</strong> The closer you are zoomed in (use <code>Option + Shift + mouse wheel</code>), the more precisely you will be able to move the anchor points.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7db4b63b-62f8-4e58-b9c3-c891b2ef58d7/06-asset-step2-opt.png" alt="The anchor points of the bottom and the right side are now aligned to the pixel grid" width="500" height="400" /><br>
<figcaption>The anchor points of the bottom and the right side are now aligned to the pixel grid.</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52ff75e5-d195-44a2-a9d6-62b11d804860/07-asset-step3-opt.png" alt="All partial pixels are gone." width="500" height="382" /><br>
<figcaption>All partial pixels are gone.</figcaption></figure>

## Do A Check-Up

Now, make sure all anchor points are on the grid by scaling your 1x version up to 500%. If you see partial pixels, then align them as described above. If everything checks out, then scale the shape down to 20%.</p>

<strong>Remember:</strong> From now on, you should always scale proportionally from the upper-left corner, and always make sure that the X and Y values are round numbers.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91769143-82e2-463d-9c4c-b7ca520b3920/08-scale-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e25d7f1-7148-43bc-acd2-4728695a149c/08-scale-opt-500.png" alt="If you see partial pixels, then align them as described above." width="500" height="333" /></a><figcaption>If you see partial pixels, then align them as described above. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91769143-82e2-463d-9c4c-b7ca520b3920/08-scale-opt.png">View large version</a>)</figcaption></figure>

## Scale It

Let’s see how different resolutions of our icon work out. Select the 1x version (<code>V</code>, then <code>Command + mouse click</code>), and duplicate the icon (<code>Option + click and drag</code>) to a position next to the 1x version.

Scale the duplicated icon up to 200% proportionally from the upper-left corner. The 2x version should show no new partial pixels. It should only be bigger.

To keep things simple, we will assume you are happy with the 1x and 2x versions and that you now want to see the 3x one.

Duplicate the 2x version (<code>Option + click and drag</code>), move it off to the side, and then scale it up by 150%. (So, 200% × 150% = 300%)

Later in this article, I’ll tell you what to do if you are not happy with the results. But if you are happy with the 2x and 3x versions, then you know now that 2x and 3x versions can be generated from the 1x version without any problems.

Go ahead and delete the 2x and 3x versions — we will be generating them automatically.</p>

## Generate And Enjoy

Photoshop has a built-in tool called “Generator” that automatically renders a shape layer to multiple image versions. To do that, we have to create a layer group and give it a special name: the file name and scale factor for each version.

In this case, it should look like this: <code>cover.png</code>, <code>200% cover@2x.png</code>, <code>300% cover@3x.png</code>

The commas separate the versions, and the percentage tells Photoshop the amount of scaling.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c40bf3aa-36de-4dd1-85af-accd20ce762b/09-layer-naming-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/252a706c-1d6b-40cf-a84c-3bc908b14e62/09-layer-naming-opt-500.png" alt="The commas separate the versions, and the percentage tells Photoshop the amount of scaling." width="500" height="338" /></a><figcaption>The commas separate the versions, and the percentage tells Photoshop the amount of scaling. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c40bf3aa-36de-4dd1-85af-accd20ce762b/09-layer-naming-opt.png">View large version</a>)</figcaption></figure>

Now, activate Generator.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebc5cae7-08f9-4dfb-aefc-93fb0117f7e2/10-asset-generator-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fb56e4a-3295-435e-9819-bce9a11eb78f/10-asset-generator-opt-500.png" alt="Activate Generator." width="500" height="333" /></a><figcaption>Activate Generator. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebc5cae7-08f9-4dfb-aefc-93fb0117f7e2/10-asset-generator-opt.png">View large version</a>)</figcaption></figure>

Generator will create a folder next to your PSD file and will automatically save PNG files to it when you save the Photoshop document.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4319e993-0af9-4c97-8dba-488daae4edd8/11-finder-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0b0a04b-3608-4cc2-93b5-858e0fe22e80/11-finder-opt-500.png" alt="Generator will automatically save PNG files when you save the Photoshop document." width="500" height="287" /></a><figcaption>Generator will automatically save PNG files when you save the Photoshop document. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4319e993-0af9-4c97-8dba-488daae4edd8/11-finder-opt.png">View large version</a>)</figcaption></figure>

To add a new scale factor at a later point in time, you simply have to alter the layer’s file name.</p>

## Get Creative For Different Resolutions

Modifying artwork for different scaling factors is a common practice because you can show more detail in a 2x graphic than you can in a 1x version.

In the following example, the 1x version of the icon contains just a single eighth note, whereas the 2x version contains a beamed note.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08bb4680-2b19-44f2-86a9-b52b3f2c2209/12-asset-canvas-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08bb4680-2b19-44f2-86a9-b52b3f2c2209/12-asset-canvas-opt.png" alt="Create different icons for different resolutions." width="500" height="308" /></a><figcaption>Create different icons for different resolutions. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08bb4680-2b19-44f2-86a9-b52b3f2c2209/12-asset-canvas-opt.png">View large version</a>)</figcaption></figure>

Obviously, you wouldn’t delete the 2x version because it is different from the 1x. Create an extra group for the 2x version, and give it a layer name that is compatible with Generator. Because you’ve already scaled the 2x version in Photoshop, don’t add “200%.”

To end up with a 3x version after working in 2x, you’ll have to scale by 150%. So, you would add this number to the 3x file name.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cba07ff-dcb4-4b42-8837-256a6634d9a1/13-layer-naming-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f452d99-e811-454d-8b59-540b685c8027/13-layer-naming-opt-500.png" alt="To end up with a 3x version after working in 2x, you’ll have to scale by 150%." width="500" height="334" /></a><figcaption>To end up with a 3x version after working in 2x, you’ll have to scale by 150%. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cba07ff-dcb4-4b42-8837-256a6634d9a1/13-layer-naming-opt.png">View large version</a>)</figcaption></figure>

## Size Matters

Making the 2x versions of your assets exactly two times larger than the 1x assets is absolutely critical. Sometimes this is harder to do than you think. Consider this keyboard:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eded048b-e23b-43e2-947d-43c8f73b4178/14-keyboard-problem-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eded048b-e23b-43e2-947d-43c8f73b4178/14-keyboard-problem-opt.png" alt="Making the 2x versions of your assets is sometimes harder to do than you think." width="500" height="244" /></a><figcaption>Making the 2x versions of your assets is sometimes harder to do than you think. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eded048b-e23b-43e2-947d-43c8f73b4178/14-keyboard-problem-opt.png">View large version</a>)</figcaption></figure>

For the 1x version (the smaller keyboard on the left), I decided that 1-pixel-wide black keys were to thin, so I used 2 pixels.

When you scale that version up (marked in pink in the keyboard on the right), you end up with black keys that are 4 pixels wide, which looks a little too wide.

But with 3-pixel-wide keys, the distance between all of the keys changes. To keep everything symmetrical, we need to make the keyboard 1 pixel shorter. And because we can’t scale 3 pixels by 1.5 without ending up with fuzzy graphics, we also need a special 3x version.

To fix the export size of our 2x asset, we can add a layer mask. Generator will always use the dimensions of a layer mask if one is present.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2fff7ac-ed6b-4adb-8922-2fe6a53eba52/15-vector-mask-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2fff7ac-ed6b-4adb-8922-2fe6a53eba52/15-vector-mask-opt.png" alt="To fix the export size of our 2x asset, we can add a layer mask." width="500" height="261" /></a><figcaption>To fix the export size of our 2x asset, we can add a layer mask. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2fff7ac-ed6b-4adb-8922-2fe6a53eba52/15-vector-mask-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9903a67d-92a4-476d-9208-657bffadf449/16-vector-mask-layer-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e730b14a-26be-4b27-bcf4-382039180c94/16-vector-mask-layer-opt-500.png" alt="Generator will always use the dimensions of a layer mask if one is present." width="500" height="388" /></a><figcaption>Generator will always use the dimensions of a layer mask if one is present. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9903a67d-92a4-476d-9208-657bffadf449/16-vector-mask-layer-opt.png">View large version</a>)</figcaption></figure>

## Summary

Hopefully, the methods described here will simplify your workflow. As you can see, creating pixel-perfect assets for different screen sizes and densities isn’t such a chore when you use vector graphics to your advantage and let Photoshop do the grunt work.</p>

### Downsides of This Approach

*   Assets are stored at 1x in the Photoshop file.</p>

### Upsides of This Approach

*   Create multiple image assets from a single shape layer, potentially saving yourself a lot of time in the future.
*   Icons are all in one document.
*   Generating assets for other scale factors from your PSD becomes easy for other people.
*   Seeing which resolutions of an icon need special attention becomes easy for other designers.

{{< signature "ml, al" >}}


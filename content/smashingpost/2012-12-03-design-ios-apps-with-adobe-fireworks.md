---
title: Design Cutting Edge iOS Apps With Adobe Fireworks
slug: design-ios-apps-with-adobe-fireworks
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/500fe592-a366-4027-93c7-40f997a23fcd/illustrationwebdesign1.jpg
date: 2012-12-03T12:16:27.000Z
author: ivo-mynttinen
description: >-
  Since the release of iPhone 4 and the iPad 3 (known as "The new iPad"), Apple
  has doubled the resolution of the displays, which are now 640 x 960 pixels
  (iPhone 4 and 4s), 1536 x 2048 pixels (iPad 3), and 640 x 1136 pixels (iPhone
  5).
categories:
  - Fireworks
  - Workflow
  - iOS
---
Since the release of iPhone 4 and the iPad 3 (known as "The new iPad"), Apple has doubled the resolution of the displays, which are now 640 x 960 pixels (iPhone 4 and 4s), 1536 x 2048 pixels (iPad 3), and 640 x 1136 pixels (iPhone 5). To keep a good-looking user interface for both the old as well as the "Retina" resolution, Apple decided not to resize all graphics or make use of scalable image formats (such as <a href="https://en.wikipedia.org/wiki/Scalable_Vector_Graphics">SVG</a>), but instead it now requires <em>two sets of graphics</em> for each device.

When building an app for iOS, you have to provide the normal-sized and double-sized images for each graphic. This is where the strongest Adobe Fireworks feature comes in — the capability to create sharp <strong>vector elements which scale up and down without any quality loss</strong> (including all effects and filters).</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Sketch, Illustrator or Fireworks?](https://www.smashingmagazine.com/2016/04/exploring-a-new-illustration-ui-design-app-gravit/)
*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [The Present And Future Of Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

This article describes how to design an iOS app with Adobe Fireworks for the iPhone and shows a few techniques which allow you to design faster, achieving the best possible results.

{{% feature-panel %}}

## High Resolution First, Scale Down Later

When creating your new document, choose the <strong>@2x-resolution</strong> (2x) as your canvas size (for example, this means 640 x 960 px for iPhone 4/4s in portrait orientation) and keep the PPI at the default of 72. iOS ignores the PPI setting stored in PNG files — the only thing we need to care about is to double the resolution (in pixels) of our images when working on Retina display designs.

<img loading="lazy" decoding="async" title="Designing An iPhone 4/4s App In Retina Resolution" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3550460-d292-4572-813c-a25365202fbe/newdocument.png" alt="New Document in Adobe Fireworks" width="500" height="385" /><br>
<em>Creating a new document for designing an iPhone 4/4s app in Retina resolution (portrait orientation).</em>

Starting with the higher resolution is my preferred way to design apps for Apple devices, as it allows me to set the appearance of each single pixel, and add details which won‘t be visible on the scaled-down version. In the worst case, if you have to use bitmap textures for some reason, the scaled-down version will look a lot better than a scaled-up one (which will have blurry textures).

When designing in 2x resolution, you have to think a bit more about what you're doing. For example, you have to avoid sizes like 3 or 5 pixels for border widths, and the same applies to effects like drop shadows — a scaled-down blur ratio of 5 pixels would result in 2 or 3 px blur, and neither would be the result you want to achieve when aiming for real perfection.

I have seen other designers doing it the other way: starting with the normal size, and scaling the whole design up when it is done. Either way is absolutely fine — I think it always depends on the designer's personal preference. However, in this article I will only describe the way to start with the 2x resolution graphics first.</p>

## Vectors Whenever Possible

When creating elements for your app, always use vector shapes, and never rasterize them (since Fireworks has very powerful vector editing abilities, it is advice that's easy to follow). It's also a good idea not to use any Photoshop live effects unless you absolutely have to. Why?

### Use Fireworks Live Filters (They Scale Better)

The reason why you should only use Fireworks live filters is because Photoshop live effects <em>will not scale</em> as they keep their attributes (unless you change the size of the whole image or the separate shape). On the other hand, <strong>Fireworks will scale any attributes of your live filters</strong> (except in intensity-based filters, like the amount of noise), and this is something you should keep in mind when you are working a lot with drop shadows or glows.
<blockquote><strong>Useful tip:</strong> Fireworks is very flexible. If you don't want to scale effects or strokes when changing your document size, you can turn this option "off" in Preferences (Menu Edit → Preferences → General → Scale Strokes and Effects). Turning it back "on" is just as easy.</blockquote>

<img loading="lazy" decoding="async" title="Turn Scaling For Strokes And Effects On Or Off" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63246da6-a4fe-43f8-b34e-bdeff08e04f5/preferences.png" alt="Turn Scaling for Strokes and Effects On or Off" width="500" height="220" /><br>
<em>The Preferences dialog in Fireworks, when you can turn on or off the scaling of strokes and effects (live filters).</em>

In the few very rare cases when the result of a scaled-down (or scaled-up) live filter does not really fit your needs, you can easily fine-tune the filter attributes manually after scaling.

Here's a quick example of this feature — two buttons were resized, one had live filters applied to it, and the other Ps live effects.

<img loading="lazy" decoding="async" title="Comparison Between Fireworks Filters And PS Live Effects" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/718fb5f7-9f4e-4850-984a-a6e86b73e940/live-effects.png" alt="Buttons Built with Different Techniques, Demonstrating the Advantages of Fireworks Filters" width="500" height="344" /><br>
<em>Both buttons are looking the same when rendered in the resolution that they have been created in (Retina). Once we resize the image, though, you will clearly notice that only the effects of the button that uses Fireworks live filters were resized correctly.</em>

<strong>Note:</strong> Fireworks will scale attributes of your live filters, applied to both vector and bitmap objects. However, there is one exception to this rule: Fireworks will <em>not</em> scale live filters applied to <em>text objects</em>. For example, a Drop Shadow live filter (applied to a vector object), will scale along with the object. But a Drop Shadow applied to a text object will not — the text block will get smaller (or larger, depending on the direction of scaling) while the drop Shadow will retain its original attributes (Distance, Softness). This behavior of Fireworks is designed as such, and is something to keep in mind when text objects and live filters are involved.</p>

### Use Divisible Values for the Height/Width of Your Shapes

Be sure to always use <em>divisible values</em> (that is, able to be divided into a whole number) for the height and width of your shapes. Sizes that do not divide evenly will result in half-transparent pixels when scaled down, which often looks blurry and imprecise.

<img loading="lazy" decoding="async" title="Resized 3px Border" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6fc9a16-d8f2-4d00-813c-e7177f58bcad/3pxborder.png" alt="Resized 3px border" width="500" height="344" /><br>
<em>A 3px border will result in a blurry 2px border when resized. Since a width of 1.5 pixels is impossible, Fireworks is trying to achieve the logical result by adding half-transparent pixels — unfortunately the result doesn't look so good.</em>

When you are drawing icons, always keep them vectorized so you can scale them down later without the blurring that occurs from bitmap resizing (we will also cover icon resizing later in this article).</p>

## Dealing With Bitmaps (When You Have To)

When using bitmap textures, there are a few possibilities for how to get the most out of them:

### Repeatable Patterns

You can build a repeatable pattern from nearly any texture — this means a bit of extra work, but is often worth it. When you are looking for textures, it's often hard to find seamless, repeatable textures for your app. But in most cases, you just need to do a few color corrections for a "regular" texture before you can use it as a repeatable pattern.

<img loading="lazy" decoding="async" title="Building Repeatable Patterns" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40321612-4944-4e87-a1e4-12bdab8f4feb/reapeatable.png" alt="Building Repeatable Patterns" width="500" height="734" /><br>
<em>This is an example when a non-repeatable detailed leather texture can be transformed into a repeatable one, by just applying a few color corrections. I usually switch to Photoshop for this type of work, then import the pattern into Fireworks. You can also make the color corrections within Fireworks (if you prefer).</em><br>
<blockquote><strong>Useful tip:</strong> Download and try the <strong><a href="https://fireworks.abeall.com/extensions/commands/Modify/">Modify Commands</a></strong> pack, by <a href="https://twitter.com/aaronbeall">Aaron Beall</a>. It includes "<em>Seamless Tile</em>" -- a very useful command for seamless textures. It does not work equally well for all types of textures, but for the most types it can help you create a seamless pattern in Fireworks really easy. The command creates seamless textures from selected objects on the canvas, by blending their edges automatically (based on a specified percentage).</blockquote>

When you've built a repeatable pattern, you can apply it as background for any vector shape. To do this, just save your pattern as a normal PNG32 file somewhere (personally I prefer to have a "Materials" folder in my project folder, where I store any patterns I've used during a specific project). Then select the shape you want to apply the pattern to and set the fill mode to "Pattern Fill". Fireworks has a few basic patterns pre-installed, but if you want to use your own pattern, just select Pattern → Other..., and then choose the pattern you have saved on your computer first.

<img loading="lazy" decoding="async" title="Applying A Pattern In Adobe Fireworks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38eba038-ee61-42b6-a15c-67a912904039/applypattern.png" alt="Applying a Pattern in Adobe Fireworks" width="500" height="324" /><br>
<em>By setting the shape's fill mode to "Pattern Fill", you can easily apply either a pre-installed or a custom pattern.</em>

When it comes to iOS design in Adobe Fireworks, the important thing is: <strong>patterns do not scale while their shapes do</strong>. This means the pattern will look the same on both resolutions. This can be very handy when you are using a few textures in your design — for example, a leather texture for the title bar. If you want to keep all the details of the texture in both resolutions, use a repeatable background pattern.
<blockquote><strong>Useful tip:</strong> If you are looking for seamless repeatable patterns, take a look at <a href="https://subtlepatterns.com/">Subtle Patterns</a>. As of today, it offers 305 excellent free patterns... and counting!</blockquote>

### Masked High-Resolution Bitmaps

When you want to scale down textures or other bitmap graphics, I suggest you use high-resolution graphics masked with sharp vector masks (for the 2x-resolution images).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ced21af-8631-450c-877f-560d748fac65/mask.png"><img loading="lazy" decoding="async" title="A Vector Mask In Fireworks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ced21af-8631-450c-877f-560d748fac65/mask.png" alt="A Vector Mask in Fireworks" width="500" height="145" /></a><br>
<em>A vector mask in Fireworks.</em>

When scaled down, the vector masks ensure that the masked graphics will <em>keep their edges sharp</em> while the graphic itself will be <em>scaled down to its half-size</em>. The normal version will look like an exact (yet smaller) version of the 2x image.

If you are using a bitmap graphic with small or fine details, you might want to use a masked graphic that has not been scaled down for the the normal version. In this case, you will need to manually replace the masked bitmap after the 2x version has been scaled down. Here's how I'd recommend proceeding:

1.  Create the 2x-resolution image first and scale it down to half-size.
2.  Select the masked bitmap and ungroup it (`Ctrl/Cmd + Shift + G`), then delete the scaled-down bitmap.
3.  Add or import a new copy of the original, unscaled graphic, then create a new masked image with the scaled-down vector mask and the original graphic.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e890799a-98ca-4df7-ad17-ca902273c120/shapes-and-masks.png"><img loading="lazy" decoding="async" title="Masked Bitmaps In Adobe Fireworks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e890799a-98ca-4df7-ad17-ca902273c120/shapes-and-masks.png" alt="Masked Bitmaps in Adobe Fireworks" width="500" height="498" /></a><br>
<em>A simple vector mask in Fireworks, used to create a rounded rectangle filled with a wooden texture: while the first shape masks the @2x-texture <strong>(1)</strong>, you can see how to modify the result for the scaled-down masks by using the scaled-down texture <strong>(2)</strong>, or the texture re-applied to the scaled-down mask <strong>(3)</strong>.</em>

In general, bitmaps are your enemy when designing iOS apps. So instead, try to work more with vector shapes and live filters. The above mentioned techniques can be used in the cases where you can't proceed without bitmaps.</p>

## Scaling Down

When you are ready with the 2x-resolution design for your app, it's time to scale down everything. I suggest that you start by copying all pages into a new Fireworks document.

<strong>Note:</strong> Alternatively, you could also select all pages, right-click in the Pages panel, and choose the option "Duplicate Page" — pages will be duplicated, the duplicates will be placed immediately after the originals and each will have "Copy" appended at the end of its name. By using this method, you'll be able to manage all of your 2x and 1x graphics inside the same document. The drawback is that once you've duplicated the original pages, you'll need to scale down each 1x copy individually, since the Fw PNG document will now contain both the 2x and the 1x designs. Hence, I recommend going with the other approach and moving all page copies into a separate document, and then scaling the whole document down to 1x resolution.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d2d8a52-a29a-43d6-bf8a-7e376645a4b6/pagemanagement.png"><img loading="lazy" decoding="async" title="Manage Different Resolutions In Different Documents" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d2d8a52-a29a-43d6-bf8a-7e376645a4b6/pagemanagement.png" alt="Manage Different Resolutions in Different Documents" width="500" height="356" /></a><br>
<em>This is how you can manage both resolutions in separate Fireworks PNG documents: copy all 2x pages (left) into a new Fireworks document (right), then scale the new document down to 1x resolution.</em>

Once you copied all your pages into a new document, you can scale it down by changing the image size (use menu Modify → Canvas → Image size). If you started with 640 x 960 px Retina design (iPhone 4 or iPhone 4s, portrait orientation), scale down to 320 x 480 pixels. Be sure to choose bicubic interpolation for resizing and uncheck "Current page only" (but keep "Resample image" checked). Fireworks will now scale down <em>every page</em> in your document and automatically redraw any contained vector shapes.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6f1a122-6b47-44ed-8650-14c02d2bd1da/scaledown.png"><img loading="lazy" decoding="async" title="Scaling Down Your Design" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6f1a122-6b47-44ed-8650-14c02d2bd1da/scaledown.png" alt="Scaling Down your Design" width="500" height="390" /></a><br>
<em>Scaling down the current page using these options will optimize all included elements for normal resolution.</em>

### Fix Blurry Pixels

Since Fireworks is primarily a screen design tool, it almost always snaps objects (both vectors and bitmaps) to a precise pixel grid. But sometimes after scaling down your pages, even if you used only even values for the sizes of your vector shapes, Fireworks might render a few pixels as <em>half-transparent</em>. This is because after the transformation, it is possible that some of them might have fallen <em>between whole pixels</em> (and rendered blurry). The good news is that you can easily fix this by selecting all layers (all objects) with blurry edges and apply <strong>Snap to Pixel</strong> (use menu Modify → Snap to Pixel, or press <code>Ctrl/Cmd + K</code>). This Snap to Pixel command will realign all objects to the pixel grid, restoring their sharpness.

<img loading="lazy" decoding="async" title="Using Snap To Pixel To Sharpen Blurry Pixels In Fireworks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d921897-8618-45a8-9b83-8c4168c8e3dc/snaptopixel.png" alt="Using Snap to Pixel to Sharpen Blurry Pixels in Fireworks" width="500" height="600" /><br>
<em>By using "Snap to Pixel" you can easily fix blurry pixels in scaled-down designs. You can also apply "Snap to Pixel" to multiple elements by selecting all of them first.</em><br>
<blockquote><strong>Useful tip:</strong> Note that "Snap to Pixel" is available in Fireworks CS5 and later. However, if you still didn't upgrade to CS5 or CS6, you can use the <a href="https://www.senocular.com/fireworks/extensions/?entry=572">Transform panel</a> by Trevor McCauley, <a href="https://johndunning.com/fireworks/about/CustomNudge">Custom Nudge</a> extension by John Dunning, or Super Nudge extension by Linus Lim. All of these can help you fix any blurry pixels by manually adjusting vector paths (using <em>sub-pixel</em> values).</blockquote>

### Fine-Tune Rendering of Icons

Some icons (especially when they are very small) might look too "bold" after resizing. Applying the Snap to Pixel command won't change this if these icons are built from either circles or rounded bordered shapes. In addition, I can't recommend using Snap to Pixel for icons since this command often moves pixels in the wrong direction and may destroy the icon's proportions.

Instead, my suggestion is to use the <strong>legacy vector rendering</strong> option in Fireworks (it can be found in Commands → Selection → Use Legacy Vector Rendering). In this way, Fireworks makes use of an older rendering algorithm for the selected objects. In most cases, both the "Improved" and the "Legacy" vector renderings produce equal visual results. But when it comes to very detailed and small vector objects like icons, the old vector rendering algorithm renders them a lot sharper than the new one.

<img loading="lazy" decoding="async" title="Using Legacy Vector Rendering To Sharpen Icons In Fireworks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a5138e9-2867-4ada-818b-42e1e00eae0f/legacyrendering.png" alt="Using Legacy Vector Rendering to sharpen icons in Fireworks" width="500" height="344" /><br>
<em>The "Legacy Vector Rendering" option allows to sharpen really small icons with a lot of details.</em>

You can switch between the two rendering modes, depending on the task at hand.

<img loading="lazy" decoding="async" title="Different Vector Rendering Options In Fireworks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b1b2723-304e-4558-9e6a-d5d04e33df2e/vector-rendering-options.png" alt="Different Vector Rendering Options in Fireworks" width="500" height="110" /><br>
<em>You can easily apply the "Legacy Vector Rendering" to any vector objects (or switch back to the default "Improved Vector Rendering").</em>

### Fix Border Radii

When your design is scaled down, even the radius of rounded borders will be reduced in half. Some shapes in your design might have a very small border radius (under 4 px in the 2x-resolution), and these shapes may look like a square after they have been scaled-down. To fix this little issue, manually increase the vector radius by just one or two pixels.

<img loading="lazy" decoding="async" title="Scaled Border Radii" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1a33ab8-719e-469e-8cef-636412c943fd/borderradii-78x45.png" alt="Scaled Border Radii" width="500" height="291" /><br>
<em>Even if it might not be mathematically correct, it sometimes makes sense to increase the border radius for scaled-down elements. As you can see in this example, a scaled-down version on a 4 px border radius is so small that we wouldn't be able to recognize it.</em>

## Export Process

When it comes to the graphics export stage, I suggest that you use Fireworks's slice tool. It can be used to quickly create <a href="https://www.smashingmagazine.com/2012/06/25/create-interactive-prototypes-with-adobe-fireworks/">intertactive prototypes</a> (together with the Hotspot tool), but we can also make use of it for exporting graphics in a more efficient way.</p>

### Limitations of the Slice Tool

Unfortunately, we can't directly use the Slice tool in our Fireworks document because the slices to be exported won't have a <em>transparent background</em> if any other graphics are positioned in the background of the slice. For example, if you want to export a button which is arranged in front of a bitmap background and you don't isolate the button graphic on a transparent background first, the exported slice will include <em>both graphics</em> — the button, and parts of the bitmap background behind it. Also, it's important not to create <em>overlapping slices</em> — each slice should be isolated and cover only the graphics you wish to export.

<img loading="lazy" decoding="async" title="Comparison Between Exporting Of Slices With Background And Without Background" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/decf5dab-fb9a-4ddd-8e29-0820a68344eb/exportslicesoverlapping.png" alt="Comparison Between Exporting of Slices with Background and Without Background" width="500" height="300" /><br>
<em>In this example, you can see the difference between exporting slices with a non-transparent background, and isolated slices without a background.</em><br>
<blockquote><strong>Useful tip:</strong> Before I speak about my exporting method of preference in more detail, I'd like to briefly mention a very useful extension by <a href="https://twitter.com/fwextensions">John Dunning</a> -- <strong><a title="Download Export Selection (free Fireworks extension)" href="https://johndunning.com/fireworks/about/ExportSelection">Export Selection</a></strong>. This extension allows you to select an object (or group of objects) on the canvas and then export it <em>without</em> any backgrounds that may appear behind it. This method may come handy in scenarios when you need to quickly export one or two objects with a transparent background and you don't want to first copy and paste them into a new document for this specific purpose.</blockquote>

### Using the Slice Tool (in a Separate Document)

To overcome all of these limitations, I've developed my own preferred exporting method:

First, create a new document with a really big size, let's say 2000 x 4000 pixels (maybe you will have to increase the size of this document later if your app includes a lot of custom graphics). Next, create an export preset (this can be done inside the Optimize panel) with PNG32 as the selected file format and with a transparent background. When done, save the preset and name it however you want.

<img loading="lazy" decoding="async" title="Optimize Panel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45047583-28b0-4e5c-a3fb-a9d4fb329d8c/optimize1.png" alt="Optimize Panel" width="500" height="359" /><br>
<em>Create an export preset in the Optimize panel — I've called mine "iOS PNG32" (note that the preset you have created will be available anywhere in Fireworks where there is an optimization choice available: Optimize panel, Export Image Preview window, etc).</em>

After these little preparations, it’s time to copy all the graphics you want to export from your original document to the newly created document. Arrange all of the graphics on a simple grid, keeping in mind that they should not overlap. Then set your document's background color temporarily to grey to make sure you can see if any live filters (such as a subtle glow) are overlapping with others. Now you can use the Slice tool to create all the slices you want to export.
<blockquote><strong>Useful tip:</strong> When you need to create a lot of slices, creating them manually can become a time-intensive process. To generate all slices in a <em>single pass</em>, select all elements in your design, right-click and use the "Insert Rectangular Slice" option — Fireworks will ask you if you want to create a single slice or multiple slices for the selected elements. Just select "Multiple" and enjoy the time you are saving!</blockquote>

Make use of your created export preset for each slice and name your slices properly, since these will be the file names after export is completed. You can rename each of your slices in the Layers panel or in the Property Inspector panel. After you've prepared your 2x document, save it. You should also scale it down using the techniques as described above, and save it as a normal resolution (1x) document.

Export time! For both image files (2x and 1x), go to File → Export, and choose "Images Only" here. Because we only want to export all of the created slices, select "Export Slices" and uncheck both of the other options ("Selected Slices Only" and "Include Areas without Slices").

<img loading="lazy" decoding="async" title="Exporting in Adobe Fireworks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95fde4ef-c880-4c72-9a5c-09ae7e89fd56/exportdialog.png" alt="Exporting in Adobe Fireworks" width="500" height="416" /><br>
<em>Export all your slices with one click!</em>

These steps describing how to resize your designs should be applied to your new (down-scaled) document as well. In the end, you should have two separate image files: one with all 2x slices (included) and one with the normal resolution slices (1x).

<img loading="lazy" decoding="async" title="Export All Graphics At Once By Using Slices" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f55cb018-77d8-4616-9adf-5cd67ac16772/exportslice.png" alt="Export All Graphics at Once by Using Slices" width="500" height="300" /><br>
<em>This document will export all included slices into a folder. (Hint: name your slices if you want specific filenames for the exported images.)</em>

### A Few Words About File Types and Image Compression

Apple recommends that you use the PNG file format for any images used in iOS applications. PNGs are lossless, and I would recommend them for nearly any implementation into apps (or websites). However, when you're going to display huge images (such as high-resolution photos) it might be a good idea to use JPG files instead.

When working on website designs, it's really important to reduce the file size of your exported images. In general, designers use tools such as <a href="https://imageoptim.com/">ImageOptim</a> or Web services like <a href="https://www.punypng.com/">punypng</a> to radically reduce the size of images. However, in the case of iOS Apps, image compression is not important since Xcode will modify PNGs (by swapping the red, green and blue bytes) and will undo any previous compression applied.</p>

### Examples of iOS Designs Made with Adobe Fireworks

Finally, I would like to share a few examples of iOS designs, made with Fireworks. Some are mine, and some are by other designers who use Fireworks extensively. I hope that they can inspire you!

<a href="https://itunes.apple.com/de/app/branslesmart/id466045948?mt=8"><img loading="lazy" decoding="async" title="Bränslesmart iOS App" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b668a4b9-9496-4d3c-89eb-fbdf2b0a6bfe/branslesmart.png" alt="Bränslesmart iOS App by Ivo Mynttinen" width="500" height="710" /></a><br>
<em><a href="https://itunes.apple.com/de/app/branslesmart/id466045948?mt=8">Bränslesmart iPhone App</a> by Ivo Mynttinen</em>

<a href="https://dribbble.com/shots/400493-Graph-design"><img loading="lazy" decoding="async" title="Graph Design" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08b9b545-6f32-4efe-b481-78c13c0b96cd/graph-design.png" alt="Graph design" width="500" height="350" /></a><br>
<em><a href="https://dribbble.com/shots/400493-Graph-design">Graph design</a> by David Perel</em>

<a href="https://dribbble.com/shots/348520-Huh-2"><img loading="lazy" decoding="async" title="Huh 2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9778925e-8c6b-4f3c-848c-09cd573dbd3c/huh-2.png" alt="Huh 2" width="500" height="350" /></a><br>
<em><a href="https://dribbble.com/shots/348520-Huh-2">Huh 2</a> by Pete Lacey</em>

<img loading="lazy" decoding="async" title="iPhone Button Polish" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be0d5bc0-1858-454f-b43f-f2e4f251b10a/button-polish.png" alt="iPhone Button Polish" width="500" height="350" /><br>
<em>iPhone Button Polish by Anthony Lagoon</em>

<a href="https://dribbble.com/shots/432277-iOS-Trend-Chart"><img loading="lazy" decoding="async" title="iOS Trend Chart" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43f8cc1e-3423-42df-8acf-ec08d68f968a/trend-chart.png" alt="iOS Trend Chart" width="500" height="361" /></a><br>
<em><a href="https://dribbble.com/shots/432277-iOS-Trend-Chart">iOS Trend Chart</a> by Anthony Lagoon</em>

<a href="https://dribbble.com/shots/98647-UI-Touch-CDJ-Pro"><img loading="lazy" decoding="async" title="CDJ Pro" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f5307bb-790f-44a2-ab8f-d6104cf5903f/touch-cdj-pro.png" alt="UI Touch CDJ Pro" width="500" height="667" /></a><br>
<em><a href="https://dribbble.com/shots/98647-UI-Touch-CDJ-Pro">UI Touch CDJ Pro</a> by Gianluca Divisi</em>

<a href="https://dribbble.com/shots/399426-Nikon-Camera-iOS-Icon"><img loading="lazy" decoding="async" title="Nikon Icon" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cd1280c-e822-4e2d-8682-2bb4c372510f/nikon-ios-icon.png" alt="Nikon iOS icon by Gianluca Divisi" width="500" height="500" /></a><br>
<em><a href="https://dribbble.com/shots/399426-Nikon-Camera-iOS-Icon">Nikon iOS icon</a> by Gianluca Divisi</em>

## Conclusion

Hopefully my personal experience with designing iOS apps with Adobe Fireworks (as well as the tips and tricks that I shared) may help you with future projects, as well.

If you have any more useful hints about how to improve the iOS design workflow, please let me know in the comments!

### Further Reading

*   "[Refining Your Design In Adobe Fireworks](https://www.smashingmagazine.com/2012/05/07/refining-designs-adobe-fireworks/ "Refining Your Design In Adobe Fireworks")," by Benjamin De Cock
*   "[Clarification on Apple PPI](https://bjango.com/articles/ppiisatag/ "Pixels per inch is just a tag")," by Marc Edwards
*   "[How to achieve pixel perfection in your designs with Adobe Fireworks](https://ivomynttinen.com/blog/how-to-achieve-pixel-perfection-in-your-designs-with-adobe-fireworks/ "How to achieve pixel perfection in your designs with Adobe Fireworks")," by Ivo Mynttinen
*   "[10 tips to create perfect visual assets for iOS and Android](https://unitid.nl/2012/07/10-free-tips-to-create-perfect-visual-assets-for-ios-and-android-tablet-and-mobile/)," by Matthijs Collard
*   "[Get Started Writing iOS Apps With RubyMotion](https://www.smashingmagazine.com/2012/08/02/get-started-writing-ios-apps-with-rubymotion/)," Clay Allsopp
*   "[Designing for iPhone 4 Retina Display: Techniques and Workflow](https://www.smashingmagazine.com/2010/11/17/designing-for-iphone-4-retina-display-techniques-and-workflow/)," Marc Edwards
*   "[Simulating The Letterpress: From Live Filters In Fireworks To CSS Code](https://www.smashingmagazine.com/2012/07/20/letterpress-effect-fireworks-css/)," Jose Olarte

{{< signature "mb" >}}


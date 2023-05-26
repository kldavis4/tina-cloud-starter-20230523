---
title: How To Export From Photoshop
slug: exporting-from-photoshop
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a03911-5997-47cd-82cb-402ed308c0b5/ps-photoshop-illu.jpg
date: 2011-11-23T10:54:08.000Z
author: marc-edwards
description: >-
  Congratulations. You’ve just completed a pixel-perfect mock-up of an app, and you’ve gotten the nod from everyone on the team. All that’s left to do is save the tens, hundreds or maybe even thousands of production assets required to bring it to life.
categories:
  - Graphics
  - Photoshop
---
It’s probably the least interesting part of designing software, usually entailing hours of grinding. Saving images to multiple scales — as required by iOS and other platforms — adds complication to the process. But there are ways to streamline or automate the exporting process.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Photoshop Etiquette For Responsive Web Design](https://www.smashingmagazine.com/2016/08/photoshop-etiquette-for-responsive-web-design/)
*   [A Better Way To Design For Retina In Photoshop](https://www.smashingmagazine.com/2015/05/retina-design-in-photoshop/)
*   [Useful Photoshop Tools and Techniques For Your Workflow](https://www.smashingmagazine.com/2011/05/useful-photoshop-tools-and-techniques-for-your-workflow/)

## Copy Merged

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20ec3e58-d12e-4ae6-9544-d0278d6c81fd/photoshop-export1.png" alt="Screenshot" width="500" height="270" />

{{% feature-panel %}}

Cutting up a design with the “Copy Merged” feature is fairly easy: ensure that the layers are shown or hidden as needed; draw a Marquee selection around the element; choose Edit → Copy Merged, and then File → New; hit Return; and then “Paste.” The result is a new document with your item isolated, trimmed to the absolute smallest size possible.
From here, all you need to do is save the image using “Save As” or “Save for Web &amp; Devices.”

Rinse and repeat for every image needed for the app or website. The technique is simple and quick, but repetitive; and if you ever need to export the images again, you’ll have to start from scratch.

This seems to be the most common method and, for some designers, the only method, which is a shame, because better techniques exist.

You could create an action that triggers the “Copy Merged,” “New,” “Paste” process — a small time-saver, but ultimately not much of an improvement to the workflow.</p>

## Export Layers to Files

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d4a4afe-9a12-4306-87b9-05375f9bc248/photoshop-export2.gif" alt="Screenshot" width="500" height="458" />

If you’re lucky, and your goal is to export a lot of similar images (typically with identical dimensions), you might be able to use Photoshop’s “Export Layers to Files” script.

By choosing File → Scripts → Export Layers to Files, each layer of the document will be saved as a separate file, with a file name that matches the layer’s name. This means you’ll probably have to prepare the document by flattening all of the elements that you’d like to export down to bitmap layers — a time-consuming process, but often quicker than using “Copy Merged.” It could also trim the size of the resulting file, if you choose to remove completely transparent areas.

I can’t say that I’m a fan of the script’s Flash-based UI or of the way it works, but “Export Layers to Files” is handy if your desired result fits its limited range of use cases.</p>

## Slices

Photoshop’s <a href="https://help.adobe.com/en_US/photoshop/cs/using/WSfd1234e1c4b69f30ea53e41001031ab64-7570a.html">Slice tool</a> lets you define rectangular areas to export as individual images, with some limitations: only one set of slices can exist per document, and slices cannot overlap (if they do, then smaller rectangle slices will be formed). During the ’90s, the Slice tool was a good way to create table-based Web layouts, filled with images. These days, designers far more often need finer control over how images are sliced, especially when creating efficient, dynamic designs, typically with images that have transparency. But, with a twist on the original concept, the Slice tool can be put to great use.</p>

### Sprite Sheets With Slices

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/928d8106-6733-458d-955e-5b6c9cf5fb18/photoshop-export3.gif" alt="photoshop-export3" alt="Screenshot" width="499" height="252" />

<a href="https://en.wikipedia.org/wiki/File:Sprite-example.gif">Sprite sheets</a> are commonly used in CSS and OpenGL games, where <a href="https://en.wikipedia.org/wiki/Texture_atlas">texture atlasing</a> can have significant performance benefits. A similar method can be employed to build UI elements in Photoshop, even if the result is a set of images, rather than one large image.

By spreading out the elements that you need to export as a flat sprite sheet, you eliminate the need for slices to overlap. If there are too many elements to comfortably fit in one document, you can create multiple documents, eliminating the need for more than one set of slices per document.

The other benefit to working like this is that you’ll no longer need to build your main design documents with the same level of precision. Occasionally using a bitmap or forgetting to name a layer is fine, because you’ll have a chance to fix things when preparing the sprite sheet for exporting. But it does mean that the original mock-up document could get out of sync with the export documents if you make changes (for example, to adjust colors or layer effects).

Because we’re interested only in user-created slices, it might also be a good idea to click “Hide Auto Slices” (in the options toolbar when the Slice Select tool is enabled) and to turn off “Show Slice Numbers,” under “Guides, Grid &amp; Slices” in Preferences. This way, you’ll remove unnecessary clutter from Photoshop’s slice UI.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e55a75de-60e5-47b2-b688-18ffa756d7c3/photoshop-export4.png" width="500" height="128" alt="Screenshot" />

After you’ve created a sprite sheet with the slices all set up correctly, you’ll be able to export all of the images at once, using “Save for Web &amp; Devices.” Assuming you’ve <a href="https://www.smashingmagazine.com/2010/11/17/designing-for-iphone-4-retina-display-techniques-and-workflow/">done things correctly</a>, you’ll be able to scale up by 200%, save all of your Retina images, and then batch rename them (adding <em>@2x</em> to the file names) — or scale them down, if you built everything at Retina size to begin with.</p>

### Layer-Based Slices

If your UI element is one layer and you’d like the exported image to be the smallest possible size, you might want to consider using a “Layer-Based Slice.” To create one for the currently selected layer, choose “New Layer-Based Slice” from the Layers menu. A Layer-Based Slices moves, grows and shrinks with the layer it’s associated with. It also takes into account layer effects: strokes and shadows increase the size of a Layer-Based Slice, so the effects are included. Less control, but more automated.</p>

## My Exporting Workflow

For years, I’ve used Copy Merged as my primary exporting method, and used Export Layers to Files when it made sense. That was a poor choice. Sprite sheets have so many advantages, especially in medium- to large-scale projects, that the set-up time is made up for very quickly. This is even truer when exporting Retina and non-Retina images: each set can be exported in a few clicks and is far less likely to have issues with file names or sizes due to its automated nature.

It also creates an environment in which modifying production assets is easy, allowing for faster iteration and more experimentation. It lowers the barrier to improving artwork during development and when revising the app or website.

And that’s a very good thing.

<em>(al) (il)</em>


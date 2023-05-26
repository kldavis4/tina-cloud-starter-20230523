---
title: The Ultimate Guide To Clone Tools In Photoshop
slug: the-ultimate-guide-to-cloning-in-photoshop
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24894f7b-7605-4898-9a59-31fd655331d6/cloning.jpg
date: 2010-03-30T08:49:26.000Z
author: joshua-johnson
description: >-
  Photoshop's wide array of cloning tools is the cause of many of the absolute
  best and worst works created with the application. In a skilled and
  experienced hand, these tools lead to phenomenal results. In the hands of a
  careless artist, Photoshop cloning can be disastrous to the credibility of the
  result. This article introduces **the several cloning tools available in
  Photoshop** and goes over the proper usage and best practices of each.
categories:
  - Graphics
  - Photoshop
---
Photoshop's wide array of cloning tools is the cause of many of the absolute best and worst works created with the application. In a skilled and experienced hand, these tools lead to phenomenal results. In the hands of a careless artist, Photoshop cloning can be disastrous to the credibility of the result. This article introduces <strong>the several cloning tools available in Photoshop</strong> and goes over the proper usage and best practices of each.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Useful Photoshop Tips And Tricks For Photo Retouching](https://www.smashingmagazine.com/2011/03/useful-photoshop-tips-and-tricks-for-photo-retouching/)
*   [Mastering Photoshop: Noise, Textures, Gradients and Rectangles](https://www.smashingmagazine.com/2011/02/mastering-photoshop-noise-textures-gradients-and-rounded-rectangles/)
*   [Pixel Perfection When Rotating, Pasting And Nudging In Photoshop](https://www.smashingmagazine.com/2011/04/mastering-photoshop-pixel-perfection-when-rotating-pasting-and-nudging/)

## The Clone Stamp Tool

The Clone Stamp tool is the oldest and most widely known of the cloning tools. The basic concept is that you duplicate certain portions of an image using a source, destination and brush.

{{% feature-panel %}}

<img loading="lazy" decoding="async" class="alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5b201fe-fc28-4823-aa9a-fe3e21df92d7/clone1-1.jpg" alt="clone tool photoshop - Setting the source" width="500" height="557" />

Use the "Option" key ("Alt") to set the source.

To clone out the name on the tombstone above, you would select a source that shares the texture of the area you want to replace. In this case, the area around the words provides an ample source of stone texture from which to clone.

To begin, simply click on the preferred source area while holding down the "Option" key ("Alt" on a PC). Then, with no keys held down, begin painting over the area you want to replace. The image area from the source will be transferred to the destination.

To be able to use this tool effectively, let's look at the relevant settings.</p>

### Basic Settings: Brush

Below, you'll find the default settings when the clone stamp is selected.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33f9f965-1305-4e0c-900f-7451e8fab7cb/clone2.png" alt="Clone Stamp Options" width="500" height="80" />

The clone stamp's basic settings.

The first setting you'll want to familiarize yourself with is for the brush. Photoshop does not restrict cloning to a basic default brush. Instead, it allows you to use any brush you want, allowing you to create an unlimited number of effects. In the example above, and in most cases in fact, a small to medium-sized round <strong>soft brush gives the best result.</strong>

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="290852" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76fd4fc9-73eb-482b-9079-a4cd7edc5c07/clone3.jpg" alt="Clone Stamp Options" width="500" height="344" />

A hard brush creates noticeable seams.

As you can see, a hard brush often creates visible edges along the path of the clone. The transition is much smoother on the left side, where a soft brush was used. Both sides suffer from noticeable replication, but this was intentional to exaggerate the cloned area. We'll discuss how to avoid this later.

As stated, while a soft round brush is recommended for basic cloning, a number of interesting effects can be created using alternate brushes. For instance, below I've used a scatter brush shaped like a leaf to add some visual interest to the photo.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9d93435-d2f1-453b-8a9e-68e98549de16/clone4.jpg" alt="Clone Stamp Scatter" width="500" height="295" />

Use a scatter brush to create interesting particle effects.

Experiment with the opacity, blending mode and brush flow for an even wider variety of results. For more information on using these features, check out the article "<a href="https://www.smashingmagazine.com/2009/11/16/brushing-up-on-photoshops-brush-tool/">Brushing Up on Photoshop’s Brush Tool</a>."

### Basic Settings: Sample

Under the "Sample" menu are three options: <em>Current Layer</em>, <em>Current and Below</em> and <em>All Layers</em>. These options affect the area you are sourcing. Here's a visual illustration of how each mode works:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b29e33c3-e601-4308-9fb5-c4b7374b64dc/clone5-b.png" alt="Clone Stamp Sample" width="500" height="333" />

The area cloned depends on the selected layer and sample mode.

As you can see, with <em>Current Layer</em> selected, the clone stamp ignores pixel data contained in any other layer. Conversely, <em>All Layers</em> ignores all layer distinction and clones any visible pixels in the document (invisible layers will be ignored). Finally, <em>Current and Below</em> samples pixels from the selected layer and any visible layers behind it.</p>

### Basic Settings: Adjustment Layers

The final basic setting (the circle with a diagonal line through it) lets you decide whether the clone stamp tool should sample adjustment layers when cloning. Adjustment layers, such as Hue/Saturation and Levels, are meant to be a non-destructive way to change the appearance of layers. So, you can make drastic changes to a layer or group of layers without destroying the original pixels.

Because of this, turning on <em>Ignore Adjustment Layers When Cloning</em> is almost always a good idea. This allows you to clone the original image, which can then be affected by an ever-changeable adjustment layer. If you do not choose to ignore the adjustment layer, the adjustment becomes permanent in the cloned areas.

In the layer set-up below, turning on <em>Sample All Layers</em> would by default clone pixels from both the background layer and the adjustment layer in the foreground. Turning on <em>Ignore Adjustment Layers</em> prevents this.</p>

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="290859" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/458ed86c-33ed-4cd1-85ea-ef06be1549c6/clone6.png" alt="Clone Stamp Sample" width="500" height="302" />

You can choose to ignore adjustment layers when cloning.

## The Spot Healing Brush

As you can see below, the Spot Healing Brush tool is located under the Eyedropper tool and above the Brush tool, and it can be accessed quickly by hitting <em>J</em> on the keyboard.</p>

<a href="https://www.flickr.com/photos/thepapergoose/304474902/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="290861" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14e3abc2-167a-4a57-959b-182fe6b6f37f/clone7.jpg" alt="clone7" width="500" height="237" /><br>
</a>

Type J to bring up the Spot Healing Brush.

The Spot Healing Brush is by far <strong>the simplest cloning tool in Photoshop</strong>. With little to no experience, you can repair small areas of an image. The secret to using the tool is in the name: <em>Spot</em> Healing. The tool is intended not for large areas of replacement, but rather to remove little unwanted spots, such as a scratch on an old photograph or a mole on a person's face.

To use the tool, <strong>simply hover over the area you want to replace and click once</strong>. Photoshop does all the work by examining the pixel data around the spot and seamlessly integrating the data into the destination.</p>

<figure><a href="https://www.flickr.com/photos/thepapergoose/304474902/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5435f175-0167-4b27-a1f3-7726260dd43f/9-beforeafter.jpg" alt="Spot Healing Brush" width="500" height="300" /></a><figcaption>The Spot Healing Brush is perfect for repairing old photographs.</figcaption></figure>

As you can see above, the tool does a remarkable job of not leaving behind any noticeable artifacts or repeating patterns. The trick is to go slowly and work on very small portions of the image. Select a spot to fix, and <strong>use a brush that's only slightly bigger than the selected imperfection.</strong> The larger the brush, the more likely you are to clone unwanted portions of the surrounding area, and the more noticeable the repetition of pixels will be.</p>

<figure><a href="https://www.flickr.com/photos/thepapergoose/304474902/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/524cdb21-0248-49e6-b896-6ce128569a4c/8-smallbrush.jpg" alt="Spot Healing Brush" width="500" height="267" /></a><figcaption>Use a brush slightly bigger than the target spot.</figcaption></figure>

## The Healing Brush

The Healing Brush tool, located under the Spot Healing Brush tool, is very similar to the Clone Stamp tool. To begin, <em>Option + click</em> (<em>Alt + click</em> on a PC) to select your source, and then carefully paint over the destination to transfer the pixels. The Healing Brush performs this operation with <strong>more built-in intelligence than the Clone Stamp</strong>.

As with the Spot Healing Brush, the Healing Brush attempts to automatically blend in the cloned pixels with the environment around it.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f6abe32-33d3-4c59-877c-c07114bb50a6/clone8.jpg" alt="clone8" width="500" height="334" />

The Healing Brush tool automatically blends the source with the destination.

As you can see, using the Clone Stamp to clone the puppy's eye results in a straight copy of the pixels, while the Healing Brush does a much better job of blending with the background.

This built-in intelligence proves extremely helpful when cloning a subject with diverse colors, textures and lighting conditions. Using the Clone Stamp in these situations can <strong>leave you with a lot of noticeably patchy spots</strong> that really stand out from the surrounding area.</p>

<figure><a href="https://www.flickr.com/photos/steflo/1112033143/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8514a5ee-f947-4b05-a7bc-548063cc8c7d/10-facefix.jpg" alt="Healing Brush" width="500" height="342" /></a><figcaption>The Healing Brush Tool makes it easy to clone visually complicated areas.</figcaption></figure>

The photograph above is a good example of a subject with a fairly complicated surface. Using the Clone Stamp tool would have made it quite difficult to paint over the cracked areas while retaining the integrity of the stained stone. Much of the discoloration would have been sacrificed as you sourced smoother areas to erase the cracks. However, the Healing Brush was able to effectively replace the cracked areas with smoother areas, while sampling from the surrounding area to replicate the stains.</p>

## The Patch Tool

The final healing tool we'll examine is the Patch tool, which can be found under the Healing Brush tool, as seen below.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aae8b5f0-fefb-4a8a-a3d7-76ac0db083a1/clone9.jpg" alt="Patch Tool" width="500" height="291" />

Tip: hit Shift + J to cycle between the tools in the fly-out menu.

The cloning tools we've examined so far are best when used meticulously on small portions of an image. By contrast, the Patch tool is the best way to <strong>clone large, relatively uniform areas.</strong> As with the other healing tools, the Patch tool not only performs a straight clone but attempts to blend in the edge of the selected area with the target environment.

To use the Patch tool, either make a selection with any of the selection tools, or simply select an area with the Patch tool's built-in lasso. There are two modes to choose from for the behavior of the patch: "Source" and "Destination" (found in the menu bar above the document area).</p>

### Source Mode

With the source mode selected, first select the area of the image you want to replace, and then drag that selection to the area you want to source. For instance, to eliminate the golf ball in the image below, you would first select the area around the golf ball, and then drag that selection around to find the best source.</p>

<figure><a href="https://www.flickr.com/photos/maxshirley/93867103/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f0fcaee-bb4a-4e87-8f35-5048449370c6/13-source.jpg" alt="Patch Tool" width="500" height="333" /></a><figcaption>In source mode, first select the area you want to replace.</figcaption></figure>

As you drag the selection around to find a suitable source, watch the destination (i.e. your originally selected area) for a preview of what the source pixels will look like in that area. Keep in mind that this preview is a straight clone without any blending (the final image will look much better). Release the selection to see the actual result.</p>

<figure><a href="https://www.flickr.com/photos/maxshirley/93867103/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bd3b3cc-1557-4f7d-82c2-3cbcb987b267/14-noball.jpg" alt="Patch Tool" width="500" height="333" /></a><figcaption>The Patch tool's result.</figcaption></figure>

As you can see, it does a pretty impressive job of blending the source and destination pixels all on its own. But going over areas that need improvement with the Healing Brush is good practice.</p>

### Destination Mode

With "Destination" mode selected, the area you select first will be the area that is replicated elsewhere. For instance, if we start with the same selection as before, dragging the selection this time gives us a preview of copying the ball to a new location.</p>

<figure><a href="https://www.flickr.com/photos/maxshirley/93867103/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34e64fc5-e648-4835-854d-a26c4c400477/15-destination.jpg" alt="Patch Tool" width="500" height="333" /></a><figcaption>Patch tool destination mode.</figcaption></figure>

After you release the selection, the golf ball is copied to a new area of the image and blended with the surrounding pixels.</p>

<figure><a href="https://www.flickr.com/photos/maxshirley/93867103/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b167b181-fde4-4c94-931c-a0dfb30ce99e/16-twoballs.jpg" alt="Patch Tool" width="500" height="333" /></a><figcaption>Result of "Destination" mode.</figcaption></figure>

## The Clone Source Palette

The Clone Source palette (found under <em>Window → Clone Source</em>) is an invaluable resource for professional-quality cloning. This tool gives you much more control over the results and functionality of the Clone Stamp and Healing Brush.

The Clone Source palette contains three primary sections: cloning source, offset adjustment and overlay options.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e058bfb-f408-40ee-8216-3efe3521d911/clone10.png" alt="Patch Tool" width="500" height="248" />

The Clone Source palette.</p>

### Cloning Sources

In the first section in the Clone Source palette, <strong>you can define multiple areas of an image as a source</strong> from which to clone and/or heal.</p>

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="290869" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6a0aecf-3836-407f-b9ce-5bc79bd2e617/clone11-c.jpg" alt="clone11-c" width="500" height="322" />

Defining multiple sources.

The image above illustrates an example of when you might want to define multiple sources. To save a source, click on one of the five source buttons, and then <em>Option + click</em> (<em>Alt + click</em>) with either the Clone Stamp or Healing Brush. That location will now be saved to that button. Now, select the next button in line, and do the same in another part of the image. Once your sources are loaded, you can quickly shift between them simply by clicking the related button.

Notice that the file name appears just under the clone source buttons. This is because <strong>you can actually select a clone source outside of the image</strong> that you're working on. Simply open a different file and set the clone source. Then, when you go back to the primary file to paint with the Clone Stamp or Healing Brush, the pixels from the other image will function as the source of the clone.</p>

### Offset Options

The second section of commands in the Clone Source palette really increase the variety of cloned results available to you. You can set exact coordinates for the source, change the size of the cloned result relative to the original source, tweak the rotation of the result and set a precise offset (again, relative to the original source).</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5ce5f9d-eaaf-4f38-b375-847510f8f5ed/clone12.jpg" alt="clone12" width="500" height="322" />

Tweaking the cloned results.

You can see these transformation effects in action in the example above. The two bails of hay are actually one and the same, but they look considerably different because of the offset options. First, I set both the width and height to 90%, so that the cloned bail would appear slightly smaller than the original. Then I changed the width to -90% to flip the clone horizontally (you could change the height to a negative number to flip the image vertically). Finally, I set the rotation to 10° to give the illusion of a small hill.</p>

### Overlay Options

The overlay options are among the most helpful features in the Clone Source palette. Years ago, cloning involved a lot of guess work because it was difficult to tell exactly what the selected sample would look like without actually applying it. The guesswork has been eliminated with the "Show Overlay" command. When "Show Overlay" is selected in conjunction with the "Clipped" option, <strong>your brush is shown with a preview of the clone source inside</strong>. This is extremely helpful when attempting to clone inorganic areas with straight edges, such as a brick wall.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a95b5ca7-545a-4715-bde0-9b7d4f12edfa/clone13.jpg" alt="clone13" width="500" height="322" />

An overlay of the source is displayed within the brush.

Note that if you choose to turn on the overlay but turn off "Clipped," then your entire clone source layer will be shown surrounding the brush.

Working this way is actually quite difficult because the source significantly blocks your view of the destination. But if you prefer it, try reducing the opacity of the overlay so that you can see the image below.</p>

## Vanishing Point

Vanishing Point takes cloning to an entirely new dimension, literally. The tool makes it possible to set up primitive planes across your artwork, which a clone then follows to simulate a three-dimensional space. Vanishing Point has a ton of features and potential applications, and it really merits its own entire article, so this will be just a brief introduction.

When you open up the Vanishing Point dialog (found under the "Filter" menu item), you'll see a large preview of your image, along with a small set of tools on the left side.</p>

<figure><a href="https://www.flickr.com/photos/brent_nashville/441110329/sizes/o/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4530684e-b214-49be-a563-b245c93c95dc/22-vanishingpoint.jpg" alt="Patch Tool" width="500" height="359" /></a><br>
<em>The Vanishing Point dialog.</em></figure>

Grab the tool sitting second from the top to set up your initial plane. With this tool, click once on each of the four corners, outlining the desired plane. Once you've created an initial plane, you can <em>Command + click</em> (<em>Control + click</em> on a PC) to extend the plane perpendicularly. Some images, though, like this old barn, won't have perfect angles. In this case, you'll have to create a second plane, entirely distinct from the original.</p>

<figure><a href="https://www.flickr.com/photos/brent_nashville/441110329/sizes/o/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e95c8a2a-db7e-4cd9-b5f9-cf4fd2559573/23-twoplanes2.jpg" alt="Patch Tool" width="500" height="301" /></a><br>
<em>Setting up planes.</em></figure>

Once you're satisfied with the planes, grab the Clone Stamp (fourth from the top), and <em>Option + click</em> the desired source (in our case, the barn door). Then clone the door onto the front-facing wall using the same method you would use with the normal Clone Stamp tool. Turn "Healing" on in the drop-down menu above the image preview to ensure that the source is properly blended into the destination.</p>

<figure><a href="https://www.flickr.com/photos/brent_nashville/441110329/sizes/o/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ef13eb3-dd63-479e-9775-5e618833e358/24-vp-result2.jpg" alt="Patch Tool" width="500" height="361" /></a><br>
<em>Vanishing Point result.</em></figure>

As you can see, Photoshop interpreted the planes fairly well. Some fine-tuning and clean-up are definitely necessary if we want a believable image; but overall, the result is extremely impressive, given the lack of work required.</p>

## 5 Quick Tips For Better Cloning

Now that we've examined each tool in depth, let's close by recalling a few things to keep in mind if we want to clone with professional results.</p>

### Take Your Time

As you undertake a cloning project, the quality of the result is directly proportional to the amount of time you put into it. Cloning photographic details can be incredibly tedious work. The world has become well acquainted with Photoshop magic, so never assume that no one will notice your blunders.</p>

### Duplicate the Active Layer

The very first step to take when cloning parts of an image is to duplicate the layer you'll be working on (or to just work on a new transparent layer). Realizing that you made a mistake so long ago that your "Undos" don't go back far enough to fix it is beyond frustrating. Keeping the original image on a hidden layer gives you the flexibility to revert any part of an image to its original state.</p>

### Be Selective With Your Tools

Each cloning tool has its strengths and weaknesses, as outlined above. Never arbitrarily grab a tool and stick with it for the duration of a project. Consider which tool is best suited to the particular area of the image you're working on. On large projects, no single tool creates believable results on its own. Use two or more tools in synergy to achieve a realistic result.</p>

### Watch for Obvious Duplication

<figure><a href="https://www.flickr.com/photos/claudio_ar/2076303879/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72834459-cda8-41ee-ba6a-c8dca537e83a/25-grass.jpg" alt="Patch Tool" width="500" height="210" /></a><figcaption>Sloppy cloning results in noticeable patterns.</figcaption></figure>

If you're not careful, duplicated pixels can become painfully obvious. This is especially true of areas that should look fairly organic, like the grass above. Instead of appearing natural, an obvious pattern emerges when you use the same section of an image over and over. To avoid this, make heavy use of the Clone Source palette. Use multiple sources; and change the size, rotation and orientation of the areas you're cloning to give the illusion of an unmanipulated image.</p>

### Avoid Disasters

When retouching significant parts of an image, overlooking certain areas becomes all too easy.</p>

<figure><a href="https://photoshopdisasters.blogspot.com/2010/01/burberry-inexpliciamus.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/049c2a64-6f38-4531-8484-0ad6c783ddaa/26-disaster.jpg" alt="Patch Tool" width="500" height="518" /></a><figcaption>Where did her leg go!?</figcaption></figure>

If you're not careful, you could eliminate enough vital body parts to make the image humorous. Your goal is to prevent your work from showing up on <a href="https://photoshopdisasters.blogspot.com/2010/01/burberry-inexpliciamus.html">Photoshop Disasters</a>, which is where you'll find the image above.</p>

## Conclusion

Cloning in Photoshop is a difficult task that requires significant time, studious attention to detail and an in-depth knowledge of several tools and commands. To improve the quality of your results, invest some time learning Photoshop's entire cloning arsenal. Experiment with all of the options for each tool to get a better feel for where you can excel.</p>

### Additional Resources

*   [Vanishing Point Video Turorial](https://www.photoshopsupport.com/tutorials/tt-cs2/vanishing-point-tutorial.html)
*   [How to Use the Clone Stamp Tool in Photoshop](https://www.ourtuts.com/how-to-use-the-clone-stamp-tool-in-photoshop/)
*   [Cloning and Healing: Photoshop Tutorial](https://www.digidiversity.co.uk/2009/09/cloning-and-healing/)
*   [How to Mirror Your Clone Stamp](https://www.photoshopsupport.com/photoshop-blog/09/cs4-06/how-to-mirror-your-clone-stamp.html) (video tutorial)
*   [Retouching and Healing Tools](https://www.tutorial9.net/photoshop/retouch-and-healing-tools/), Tutorial9

{{< signature "al" >}}


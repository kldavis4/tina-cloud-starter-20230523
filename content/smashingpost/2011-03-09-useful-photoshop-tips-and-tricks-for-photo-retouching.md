---
title: Useful Photoshop Tips And Tricks For Photo Retouching
slug: useful-photoshop-tips-and-tricks-for-photo-retouching
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85481e44-2611-4b2f-8d1e-5e995372a160/photography.jpg
date: 2011-03-09T12:16:03.000Z
author: dirk-metzmacher
description: >-
  When it comes to designing in Photoshop, there is a myriad of ways one could use to achieve a certain result, especially when it comes to photo retouching.
  Designers use technique they are most confident as well as comfortable with, which is great because it's always useful to peek into the workflow of our colleagues and learn new design approaches. We have had articles on
  [cloning](https://www.smashingmagazine.com/2010/03/30/the-ultimate-guide-to-cloning-in-photoshop/),
  [compositing](https://www.smashingmagazine.com/2010/12/16/compositing-in-adobe-photoshop-time-saving-tips/),
  [masks](https://www.smashingmagazine.com/2009/12/17/unveiling-photoshop-masks/)
  and [obscure Photoshop time-savers](https://www.smashingmagazine.com/2010/01/20/obscure-adobe-photoshop-time-savers/)
  in the past. This article is different. [Updated May/02/2017]
categories:
  - Graphics
  - Techniques
  - Photoshop
  - Retouching
---
I'll be covering some of the useful techniques and tricks which I've learned from my experience. You may know some of them, but hopefully not all of them. All images used in this article were purchased and are used according to their licenses. 

Here is a short overview of the techniques we'll be covering:

{{% feature-panel %}}

*   [Naturally Increased Light](#technique1)
*   [Simulate Infrared Images](#technique2)
*   [Levels](#technique3)
*   [Color Look With An Adjustment Layer](#technique4)
*   [Controlling Mid-Tone Contrasts](#technique5)
*   [Sunset](#technique6)
*   [Creating Smiles](#technique7)
*   [Colorful Water Drops](#technique8)
*   [Skin Color](#technique9)
*   [Matching Skin Tones](#technique10)
*   [Reducing Noise](#technique11)
*   [Retro Look With Curves](#technique12)
*   [Identifying Layers](#technique13)
*   [Conserving Resources](#technique14)
*   [Classy Sepia Look](#technique15)
*   [Precise Positioning](#technique16)
*   [Applying Layer Styles Multiple Times](#technique17)

## Naturally Increased Light

The light of the sun creates texture. There are shadowy areas and spots where the sunlight can shine without interference. To control the intensity, you can draw more light onto a separate layer or increase already existing light. Create a new layer by going to Layer → New → Layer, or by pressing <code>Shift + Control + N</code> on Windows or <code>Shift + Command + N</code> on a Mac. Set the blending mode to “Color Dodge” and the opacity to about 15% - 30%.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b1fffce-66ea-49c9-a478-beed6e917419/photoshop-tip1a.jpg" alt="Increase light on a separate layer" width="464" height="449" />

Then use the brush tool with a soft brush, and hold the <code>Alt/Option</code> key to pick up colors from the area that you want to brighten. Continue to brush in some light, picking up appropriate colors if the background changes. Use a second layer in “Overlay” mode. This way, you increase not only the light, but the saturation, which makes for more realistic results.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbe0b2d4-8ea7-4995-8d9e-b96f07fe229f/photoshop-tip1b.jpg" alt="More realistic results with the blending mode Color Dodge" width="500" height="652" />

More realistic results with the blending mode Color Dodge

## Simulate Infrared Images

Open a photo in Camera Raw; you can do this either in Bridge, using the right mouse key and clicking “Open in Camera Raw,” or directly in Photoshop, by selecting File → Open as Smart Object. Apply basic adjustments to optimize your image (for example, with the “Recovery” and “Fill Light” slides), then switch to the “HSL/Grayscale” tab. Check “Convert to Grayscale,” and set the Blues down to around -85. Set the Greens to +90 and the Yellows to +20.

Trees and bushes should now shine in the typical white, and the sky should appear almost black. If you want to go on and simulate some grain, switch to the “Effects” tab, and enter 15 for the amount, 20 for size and 80 for roughness. You could also apply a “Vignette.” Here I used -30 for the amount, 40 for the midpoint and -35 for roundness.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f02c1079-9709-49c2-8860-96562d06db33/30-tips-and-tricks3.jpg" alt="Almost like an infrared image" width="500" height="341" /><br>
<figcaption>It’s almost like an infrared image.</figcaption></figure>

## Levels

When applying a “Levels adjustment,” you can set black and white points in order to decrease color tints, but where are the darkest and brightest spots in the image? Go to New Adjustment Layer → Threshold to find those areas. This function is available under the “Layer” menu.

Move the slider so far to the right that only a few white spots remain in the document. Use the “Color Sampler tool” and set down a point there. Move the slider to the left until only a few black spots remain, and set a second point down there.

One could also find a neutral gray in the image by using a “Threshold adjustment layer.” Add a new blank layer between the original image and the threshold adjustment layer, and fill this layer with 50% gray. Go to Edit → Fill or press <code>Shift + F5</code>, then select “50% Gray” under “Contents” and click “OK.”

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cba10b9-ee65-4660-a17c-145066e5e8ec/photoshop-tip2a.jpg" alt="Threshold adjustment layer at work" width="500" height="472" />

Here is the threshold adjustment layer at work.

Change the blending mode of this layer to “Difference.” Select the “Threshold adjustment layer” again and move the slider all the way to the left. Slowly move the slider back to the right until black dots start to appear. These are the neutral gray areas in the image (if neutral grays are present). Add a “Color Sampler spot.”

Now delete both the threshold adjustment layer and the 50% gray layer. Create a new adjustment layer, “Levels.” Use the first Eyedropper tool to click on the darkest area, then use the third Eyedropper on the brightest area.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db99be59-3769-47a1-8e2b-c0895e264fc0/photoshop-tip2b.jpg" alt="Before and after comparison" width="500" height="664" />

Here’s a before-and-after comparison.

Now you can use the gray Eyedropper tool on the third Color Sampler spot. The color tint will be decreased. Color Sampler spots can be deleted by dragging them off the canvas with the Color Sampler tool.</p>

## Color Look With An Adjustment Layer

Go to the Layer menu, and then New Adjustment Layer → Hue/Saturation, and set the blending mode to “Soft Light” and check “Colorize.” Use the Hue, Saturation and Lightness sliders to control the color: for a cool look, for example, set the hue at 210, the saturation at 50 and the lightness at 10; for a warm look, set the hue at 30, the saturation at 30 and the lightness at 5.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07422016-a7a4-4792-ba39-22afc5cfa5c9/photoshop-tip3a.jpg" alt="Hue/Saturation and Color Fill" width="500" height="485" /><br>
<em>Here is Hue/Saturation and Color Fill.</em>

Alternatively, you could use several color layers. Create them from the layer palette with the “New Fill/Adjustment Layer” button. Choose a color, then set the blending mode to “Vivid Light.” Reduce the opacity to about 25%, and invert the layer mask with <code>Control/Command + I</code>. Paint in the colored light with a big brush and white color. This works especially well for the lighting in portraits that have a textured background.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12ce2864-418a-480b-a7da-9084e953f86c/photoshop-tip3b.jpg" alt="Color Look with an Adjustment Layer" width="500" height="580" />

Here’s the Color Look with an Adjustment Layer.

## Controlling Mid-Tone Contrasts

To increase detail in landscape shots, boost the mid-tone contrast. Copy the background layer with <code>Control/Command + J</code>, and then click on Filter → Convert for Smart Filters in the menu. Then go to Filter → Other → High Pass and enter a radius of 3 pixels. Change the blending mode to “Overlay” and double-click the layer next to its name to open the “Layer Style” window.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cba95414-b815-4118-8cae-ce1eb6a6d20e/mid.png" alt="mid" width="500" height="436" /><br>
<figcaption>Layer Style window: This Layer</figcaption></figure>

For the first gradient, “This Layer,” split the sliders by holding the <code>Alt/Option key</code> and trim the layer effect to the “50/100” and “150/200” ranges. As soon as you move the sliders, you’ll see where those numbers are. This increases contrast only for the mid-tones. Double-click the “High Pass” filter in the layer palette to bring the dialog box up again in order to adjust the radius to your liking.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0e06b07-e02f-4558-979a-f66a2bd3fc0a/30-tips-and-tricks7b.jpg" alt="Better Midtone Contrasts" width="500" height="340" /><br>
<figcaption>Check out these mid-tone contrasts.</figcaption></figure>

## Sunset

A sunset, especially at sea, can be an amazing color spectacle. The hues will depend heavily on the weather, though — but you can push them a bit with a gradient map. Click on the “New Fill/Adjustment Layer” button in the Layer palette and select “Gradient Map” from the list. Click on the gradient to open the “Gradient Editor.”

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03c0999a-3b40-4560-a777-8b12b64e054d/sunset.png" alt="Sunset" width="500" height="352" /><br>
<figcaption>Gradient Map</figcaption></figure>

Click on the first color patch below the gradient, and change the color to red. Set the color patch on the opposite side to yellow, and click “OK.” Set the blending mode to “Soft Light” and reduce the opacity to about 50%. This will create a warm, almost golden sunset.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5976dc00-2f86-43f2-b420-9411bab1d824/30-tips-and-tricks8b.jpg" alt="From a blue to a golden sunset." width="500" height="600" /><br>
<figcaption>Observe the movement from a blue to a golden sunset.</figcaption></figure>

## Creating Smiles

Roughly select the area around the mouth with the Polygon Lasso tool. Go to Select → Modify → Feather, and enter a radius of 10 pixels. Confirm, then click on Layer → New → Layer via Copy (or press <code>Control/Command + J</code>), then Edit → Puppet Warp. Photoshop will put a mesh over the entire layer in the shape of your previous selection.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c9ae93e-94a2-4eb1-a9c8-5d1bd4bab8a9/30-tips-and-tricks10a.jpg" alt="Mesh over the layer" width="500" height="334" /><br>
<figcaption>Here’s the mesh over the layer.</figcaption></figure>

You can control the size of the mesh with the “Expansion” value in the Options bar. Increase the density to “More Points” for increased precision. Press <code>Control/Command + H</code> to hide the mesh, then set the first pins to the corners of the mouth. Add more pins to distinctive spots of the mouth. By clicking and dragging the mesh, you can shape a nice smile.</p>

## Colorful Water Drops

Macro shots of water drops are appealing, and shapes can be further accentuated with discreet coloring. You could treat the bland surface with a linear gradient from <code>#772222</code> (RGB 119, 34, 34) to <code>#3333bb</code> (RGB 51, 51, 187). If the photo is on a layer of its own, click on Layer → Layer Style → Gradient Overlay or double-click the layer next to its name.

Macro shots of water drops are appealing, and shapes can be further accentuated with discreet coloring. You could treat the bland surface with a linear gradient from <code>#772222</code> (RGB 119, 34, 34) to <code>#3333bb</code> (RGB 51, 51, 187). If the photo is on a layer of its own, click on Layer → Layer Style → Gradient Overlay or double-click the layer next to its name.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/595e4218-3a13-4dbf-acb3-e1f9e3779e65/gradient.png" alt="gradient" width="500" height="327" /><br>
<em>Layer Style: Gradient Overlay</em></figure>

Set the blend mode to Color, the opacity to 50%, the gradient to “Foreground to background color” and the angle to 90%. The gradient will be saved as a layer style, so you can come back at any time to adjust the values. Double-clicking the style name opens up the dialog window once more.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/713fcadd-1f28-41a9-a886-dd7dd4774999/30-tips-and-tricks12b.jpg" alt="Colorful drops with optimized colors" width="500" height="351" /><br>
<figcaption>See the colorful drops with optimized colors.</figcaption></figure>

## Skin Color

If the skin is not quite perfect after retouching, it might be because of the general hue. You can control it by going to New Adjustment Layer → Hue/Saturation. Click on the miniature mask, and press <code>Control/Command + I</code> to invert the mask.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49b87fec-d964-4f91-ac05-74c801f7dc75/skincolor.png" alt="skincolor" width="500" height="500" /><br>
<figcaption>Adjustment Layer: Hue/Saturation</figcaption></figure>

Using white color and a soft brush, paint over the skin areas so that only they get treated. For the adjustment, switch from Standard to “Reds” (found in the Hue drop-down menu of the Adjustment layer), and use the Hue, Saturation and Lightness sliders to adjust the skin color. Switch to “Yellows” and optimize the skin tone. Getting the colors exactly right depends very much on the image material. Rely on your common sense.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0beb09a9-ff3c-414e-a14b-2f69ef102c62/30-tips-and-tricks14b.jpg" alt="Optimized skin tones" width="500" height="375" /><br>
<figcaption>Optimized skin tones</figcaption></figure>

## Matching Skin Tones

A sunburn or a blush can disrupt a portrait, especially if there is a contrasting pale person nearby. Photoshop has a tool to correct that: “Match Color” offers control over skin tones. Open your image and use the Quick Selection tool to roughly select the red skin areas.

You can hold down the <code>Alt/Option</code> key and subtract areas from the selection. Click on Select → Modify → Feather and enter a value of about 15 pixels. Use the <code>Control/Command + J</code> shortcut to copy the selection to a new layer.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bb170ea-bf62-4ceb-a0cc-f26644eaa19b/matchcolor.png" alt="matchcolor" width="500" height="568" /><br>
<figcaption>Adjustments: Match Color</figcaption></figure>

Using the same technique, copy the non-reddened skin to a new layer. In the next step, you’ll have to differentiate between the source layer and the layer to edit, so rename these two layers meaningfully; all it takes is a double-click on the layer name. You could use the naming scheme shown here and call them “Beautiful skin” and “Reddened skin.”

Activate the layer with the red skin, and select Image → Adjustments → Match Color from the menu. For “Source,” select the current document, and for “Layer,” select the one with the beautiful skin. Control the effect using the “Luminance” and “Color Intensity” sliders in the Image Options area. Once you confirm, you can control the effect’s strength with the Opacity slider.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e0d1707-13af-4d86-8e90-3b8373597359/30-tips-and-tricks18b.jpg" alt="Paler skin after Match Color" width="500" height="600" /><br>
<figcaption>Paler skin after Match Color</figcaption></figure>

## Reducing Noise

Noisy images are annoying. One way to reduce noise is through the channels. Copy the background layer by pressing <code>Control/Command + J</code>, switch to the Channels palette, and select the channel that shows the least noise. Drag that channel down to the “New Channel” icon (next to the trash can) and go to Stylize → Find Edges. Then apply a Gaussian Blur with a radius of about 3 pixels.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d39315f7-5b06-40bf-8c9e-b9ec79dd9c98/30-tips-and-tricks19a.jpg" alt="Copy of the red channel" width="500" height="318" /><br>
<figcaption>Look at this copy of the red channel.</figcaption></figure>

Click on the new channel’s miniature icon while holding the Control/Command key to select the content. Activate the “RGB channel” (top-most), and switch back to the Layers palette. When the duplicated background is selected, click on the “Add Layer Mask” icon.

Click on the Layer Miniature icon, and select Filter → Blur → Surface Blur from the menu. Play around with the Radius and Threshold sliders until the noise has been reduced as much as possible. Thanks to the mask you created, the contours are safe.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/955712d3-5833-4d5f-98f8-11946f5ffcdd/30-tips-and-tricks19b.jpg" alt="With and without noise" width="500" height="600" /><br>
<figcaption>With and without noise</figcaption></figure>

## Retro Look With Curves

Go to Layer → New Adjustment Layer → Curves and switch from RGB to Reds. Then drag the line downwards a little for the shadows and upwards for the highlights, creating a slight “S” curve. Do the same for the Greens. For the Blues, drag the highlights down a little and the shadows up (for an inverted S shape). The shadows should now be slightly blue-ish, the highlights slightly yellow-ish.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06429e7b-8018-4a1f-a609-13ccaa4d2224/curves.png" alt="curves" width="500" height="483" /><br>
<figcaption>Adjustment Layer: Curves</figcaption></figure>

Create a new layer with <code>Shift + Control/Command + N</code>, and fill it with <code>#000066</code> (RGB 0, 0, 102). Set the blending mode to “Exclusion.” Now copy the background layer by clicking it and pressing <code>Control/Command + J</code>. Set the blending mode for this copy to “Soft Light.”

To decrease the effect overall, activate the top-most layer and then click on the background copy while holding the Shift key, thereby selecting both layers. Alternatively, you can add them to a group with <code>Control/Command + G</code>. Reduce the layer’s (or group’s) opacity. Note that in Photoshop versions prior to CS5, you’ll have to reduce the opacity for each layer individually.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e89faaa3-19ac-4ba3-8823-4e3b4753b064/30-tips-and-tricks20b.jpg" alt="Simple retro look in a few steps" width="500" height="600" /><br>
<figcaption>Achieve a simple retro look in a few steps.</figcaption></figure>

## Identifying Layers

If you’re ambitious with your collages, then you’ll be familiar with this problem: meaningful layer names are often neglected during the creative process. This can result in layer names like “Layer 4” and “Layer 5 Copy 2,” which are not very helpful when you need to quickly identify the contents of a layer.

Photoshop offers a number of solutions for our laziness. For example, you can click on the element you want to select by using the “Move tool” and holding the right mouse key; you’ll see which layer contents are below the tool. Photoshop will display a list in a drop-down menu, from which you can easily select the desired element.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ada522ca-7d32-4df0-aa2b-395bf98ae7b8/30-tips-and-tricks21.jpg" alt="Right Click with the Move tool" width="500" height="393" /><br>
<figcaption>Right click with the Move tool</figcaption></figure>

<code>Control/Command + left-click</code> with the Move tool selected and, in most cases, you’ll select the corresponding layer of the element that your mouse is over (unless Photoshop can’t distinguish between the multiple layers).

You could also <code>Control/Command + left-click</code> on a layer’s miniature icon to get a selection of the content of that layer. The marching ants will show you what is on that layer and where it is.

Another option is to click on the Layer palette’s Options icon, in the top-right corner, and select “Layers Palette Options.” From here you can adjust the size of the layer’s miniature preview and concentrate the miniature’s content to the layer’s bounds, which should cut down on future guesswork when it comes to layer contents.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47e3f055-08cb-4afc-b94c-b6e398a2c0a1/panels.png" alt="panels" width="500" height="585" /><br>
<figcaption>Layers Palette options</figcaption></figure>

## Conserving Resources

Plug-ins save time, but they’re a bit resource-hungry; at least, they lengthen Photoshop’s start-up time. Your plug-ins might have functionality that you rarely use, so deactivate them until you need them. To do so, create a new folder by going to Adobe → Adobe Photoshop CS5 (or whatever your version) and name it something like <em>Plugins_deactivated</em>.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ea6224f-50d8-448a-bbdd-2b3cb2e87352/30-tips-and-tricks24.jpg" alt="After disabling some plugins" width="500" height="377" /><br>
<figcaption>After disabling some plug-ins.</figcaption></figure>

Now move all of the extensions that you don’t need for the moment. When you restart Photoshop now, those plug-ins won’t load, so the program will start up quickly. Your RAM will be relieved. Because you neither deleted nor uninstalled the plug-ins, they’re available to use anytime. If you need them, just move them back to the plug-in folder.</p>

## Classy Sepia Look

The sepia look is an absolute classic. To enhance a black and white image with a classy sepia tone, follow these steps. Click on Layer → New Adjustment Layer → Photo Filter, and select the Sepia filter, with a density of 100%. Double-click the layer (not the layer name) to open up the Layer Style window. This will show the Blending options.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/234e3f28-4585-49b9-8fc5-339bec480f3f/layerstyle.png" alt="layerstyle" width="500" height="435" /><br>
<figcaption>A view of the Layer Style window.</figcaption></figure>

At the bottom of the dialog box for the first gradient, move the white slider to the left while holding the <code>Alt/Option</code> key. This creates a smooth transition between adjusted and unadjusted areas. The sepia will now look elegant.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d658b35-7740-440f-a749-ac144fb2ff62/30-tips-and-tricks26b.jpg" alt="Subtle Sepia Look" width="500" height="415" /><br>
<figcaption>Subtle sepia</figcaption></figure>

## Precise Positioning

I’m sure you’ve often been irritated by Photoshop’s tendency to position elements on its own, but the program is just trying to help you align an element that is on its own layer with the outer edge of the document or with the edge of another object. To your frustration, the layer’s content will jump to the edge, even though you wanted to leave a few pixels of space in between. You can temporarily deactivate the automatic snapping by holding the <code>Control/Command</code> key as you position.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63d95752-afb9-42db-835f-255d8f35ffba/30-tips-and-tricks27.jpg" alt="A banner close to the edge" width="500" height="365" /><br>
<figcaption>A banner, close to the edge.</figcaption></figure>

## Applying Layer Styles Multiple Times

Usually, layer styles can be applied only once. For example, if you click on Layer → Layer Style → Drop Shadow, you cannot create a double drop shadow, one of which has an angle of 120°, a distance of 2 pixels and a size of 2 pixels, and the other of which has an angle of 180°, a distance of 12 pixels and a size of 12 pixels.

Actually, it is possible! It just requires a little detour. Create the first drop shadow as you normally would. Then right-click on the layer and select “Convert to Smart Object” from the menu. This smart object can be assigned another drop shadow, and you can convert the smart object into yet another smart object. This way, you can easily add a third and fourth drop shadow. Alternatively, you could apply multiple strokes.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2ef120a-68e1-47d7-a51f-3e30bae5239f/30-tips-and-tricks31.jpg" alt="Three shadows in combination" width="500" height="343" /><br>
<figcaption>Three shadows in combination.</figcaption></figure>

By the way, to put one or even several styles onto their own layers at once, right-click on the FX symbol and select “Create Layer” from the list. Now you can apply filters to these styles, but they won’t be editable anymore.</p>

<em>Huge thanks to <a href="https://be.net/lanenga">Carlos Lanenga</a> for his valuable suggestions for this article.</em>

<em>(al) (ik) (vf)</em>


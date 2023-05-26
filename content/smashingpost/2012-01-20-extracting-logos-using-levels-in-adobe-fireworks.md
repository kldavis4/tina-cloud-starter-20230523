---
title: Extracting Logos Using Levels In Adobe Fireworks
slug: extracting-logos-using-levels-in-adobe-fireworks
image: null
date: 2012-01-20T16:41:01.000Z
author: jose-olarte
description: >-
  In all the years that I’ve been using Adobe Fireworks, I have always had to
  perform one task in every project: remove the background from a logo. Most of
  the time, it’s because the client doesn’t have the original raw file that
  their previous designer used to create their company’s logo, or because I need
  to work with a bunch of affiliate logos that I downloaded from the Web and not
  all of them have transparency information.
categories:
  - Fireworks
  - Tutorials
  - Techniques
---
In all the years that I’ve been using Adobe Fireworks, I have always had to perform one task in every project: remove the background from a logo. Most of the time, it’s because the client doesn’t have the original raw file that their previous designer used to create their company’s logo, or because I need to work with a bunch of affiliate logos that I downloaded from the Web and not all of them have transparency information.

With a rectangular or elliptical logo, I just trace over it with a shape and turn it into a mask. But when tracing a mask is impractical (as with complex shapes or text-based logos), I used to follow a method that I devised for extracting logos in Adobe Fireworks that doesn’t rely on the dreaded Magic Wand tool.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Sketch, Illustrator or Fireworks?](https://www.smashingmagazine.com/2016/04/exploring-a-new-illustration-ui-design-app-gravit/)
*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [The Present And Future Of Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

This method took advantage of a few Live Effects to remove the background and retain the logo form. It was simple, but also primitive: it worked perfectly only when the contrast between the logo and background was already ideal and the logo form had only one color. Otherwise, I ended up with jagged edges.

{{% feature-panel %}}

I have since much improved the process of handling multi-colored logos and non-white backgrounds; it works best on solid-colored text and shapes with clear outlines. Because it involves Fireworks’ awesome features and tools, this method is a quick and easy solution that you can incorporate in your Web and interface design workflows.

And yes, still no Magic Wand tool.</p>

## Let’s Begin!

To start off, fire up Adobe Fireworks and load your logo image on the canvas. In the example below, I created a three-color logo text, surrounded by a blu-ish hue, on a canvas with a transparent background.

Create a back-up of the image by selecting it using the Pointer tool (<code>V</code> on the keyboard), cloning it (<code>Shift</code> + <code>D</code>, or in the menu Edit → Clone) and hiding it (<code>L</code>, or View → Hide Selection). You will need this back-up near the end of the process, but for now, keep it hidden.

<img loading="lazy" decoding="async" class="111134" title="Logo image on canvas" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33ecc9a9-4282-473d-9a9b-a67f7cde4803/elul-00.png" alt="Logo image on canvas" width="500" height="500" /><br>
<em>Place the logo image on the Fireworks canvas.</em>

<strong>Tip:</strong> You can also use Duplicate (<code>Ctrl/Cmd</code> + <code>Alt/Opt</code> + <code>D</code>, or Edit → Duplicate) instead of Clone to copy the image. The difference is that Duplicate offsets the position of the copied object by 10 pixels down and 10 pixels to the right, whereas Clone creates the copy in the same exact position as the original object.

<img loading="lazy" decoding="async" class="111152" title="Original image and hidden backup in the Layers panel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a86b03e-5900-468a-8d8f-de6a33a853c1/elul-00a.png" alt="Original image and hidden backup in the Layers panel" width="248" height="291" /><br>
<em>The original image and hidden back-up in the Layers panel.</em>

## Step 1: Breakdown

To be able to deal with the different colors of the logo separately, we first need to break the logo down into “pieces,” one foreground color per piece. Use the Pointer tool to select the logo image, and use one or more bitmap selection tools (Marquee or Oval Marquee (<code>M</code>), Lasso or Polygon Lasso (L) — set the Edge to “Hard” in the Properties panel) to select a piece of the logo. Make sure the piece you select has only one color (not counting the image’s background). Cut and paste the selected piece (<code>Ctrl/Cmd</code> + <code>X</code>, and then <code>Ctrl/Cmd</code> + <code>V</code>) to separate it from the rest. Do this for each piece; cancel the Marquee selection (<code>Ctrl/Cmd</code> + <code>D</code> or <code>Esc</code>, or in the menu Select → Deselect) and switch back to the Pointer tool (<code>V</code>) if you need to select the logo image again.

<strong>Tip:</strong> Double-click on an image object to quickly switch from Pointer tool to Marquee tool.

<img loading="lazy" decoding="async" class="111135" title="Logo 'piece' selected" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32531c0b-2c5c-4aee-9c11-2f6c999ccf3f/elul-01.png" alt="" width="500" height="360" /><br>
<em>Select a piece of the logo.</em>

In our example, I’ve used a (rectangular) Marquee, but you can use the Oval Marquee for circular or elliptical selections, and the Lasso or Polygon Lasso for irregular shapes.

<img loading="lazy" decoding="async" class="111136" title="Cut up the logo into pieces" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/393b072d-255a-43a2-b7cc-0384f7605378/elul-01a.png" alt="Cut up the logo into pieces" width="500" height="360" /><br>
<em>Cut up the logo into pieces.</em>

If your logo has only one color, skip this step and treat the whole image as your only piece.</p>

## Step 2: Desaturate

Select all of the pieces of the logo image using the Pointer tool, and apply a Hue/Saturation filter (in the Properties panel, go to Filters: [+] → Adjust Color → Hue/Saturation…). Drag the Saturation slider all the way to the left (-100) to reduce the logo to grayscale. Make sure that Lightness is set to 0 and that Colorize is unchecked before clicking “OK.”

<img loading="lazy" decoding="async" class="111138" title="Desaturate all pieces" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/490b0ff0-6999-44ad-835f-35956ce414fc/elul-02.png" alt="Desaturate all pieces" width="500" height="500" /><br>
<em>Desaturate all pieces.</em>

### A Note on Filters

Adobe Fireworks features two almost identical sets of filters: one in the application menu and another in the Properties panel (the <a href="https://help.adobe.com/en_US/fireworks/cs/using/WSBFD1EA57-0750-4ca6-BEB4-4D66917CD996.html">Live Filters</a>).

<img loading="lazy" decoding="async" class="111176" title="Filters menu vs. Live Filters" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f22217be-7fa0-464d-936e-cf1f3b25127f/elul-02b.png" alt="Filters menu vs. Live Filters" width="500" height="500" /><br>
<em>Filters menu vs. Live Filters in the Properties panel</em>

Filters applied using the application menu are “destructive,” in that they can’t be undone by any other means except Undo (<code>Ctrl/Cmd</code> + <code>Z</code>, or in the menu Edit → Undo). Furthermore, target vector objects (shapes and text) need to be <em>converted into bitmap objects</em> before they can work their magic, which makes editing the original object harder. To adjust the effect of the filter that you just applied, you will need to undo that step and reapply the filter.

To maintain the ability to easily edit an object and its filters’ properties, <em>always</em> use the <strong>Live Filters</strong> in the Properties panel. This way, you can make changes to the original object, and the filters will adjust automatically. You will also be able to change a filter’s settings at any time, or disable or remove the filter, without adversely affecting the other filters.</p>

## Step 3: Levels

What makes this newer method different is <strong>the use of the Levels filter</strong> (as opposed to the Brightness/Contrast filter of the older method) to push the dark grays into pure black and the light grays into white, while maintaining the smooth edges of the logo’s curves.

Select one piece of the logo image using the Pointer tool, and apply a Levels filter (in the Properties panel, go to Filters: [+] → Adjust Color → Levels…). In the Levels dialog, set the Channel drop-down to “RGB” (which is the default). Below the histogram under Input Levels, move the left and right arrow sliders to change the intensity of the dark and light areas of the image piece, respectively. Make sure that the Preview checkbox is checked, so that you can see your changes in real time. Move the left arrow slider just enough to the left to get the logo part to show up completely black, but not so far left that the edges of the logo become jagged. The same goes for the right arrow slider: move it right to get a pure white background. You can leave the center slider untouched. Click “OK” to apply the filter.

<img loading="lazy" decoding="async" class="111139" title="Levels filter applied to first piece" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad66fbe8-1f33-4bc6-8e41-33d9642c306a/elul-03.png" alt="Levels filter applied to first piece" width="500" height="500" /><br>
<em>Apply the Levels filter to each piece.</em>

You can check the accuracy of your filter values by bringing up the Info panel (<code>Shift</code> + <code>Alt/Opt</code> + <code>F12</code>, or in the menu Window → Info) and hovering over the black area to obtain its RGB color value. The RGB values should all be set to <code>00</code>; otherwise, go back to the Levels dialog and readjust the slider.

<img loading="lazy" decoding="async" class="111293" title="Info Panel with RGBA reading" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d2ea519-d0f2-41bd-b36e-8f1874957687/elul-03m.png" alt="" width="227" height="155" /><br>
<em>Use the Info panel’s RGBA reading to check the color values.</em>

Do the same for the white area, this time setting all three RGB values to <code>FF</code> in the color reading.

You can further fine-tune the levels by changing the number values in the left and right text boxes in the Input Levels dialog, which correspond to the left and right sliders in the visual graph. Increase the value of the left text box to darken the dark-gray areas until all three RGB values are set to <code>00</code> in the Info panel; decrease the values if the edges of the logo become too jagged. The inverse is true for the right text box. This allows you to get pure black and white colors, while keeping the edges of the logo as smooth as possible.

Repeat the whole process in step 3 for all other image pieces.

<img loading="lazy" decoding="async" class="111140" title="Pieces with different Levels settings" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8ab1bad-9c6b-4ddd-bbec-18eb3485efd5/elul-03a.png" alt="Pieces with different Levels settings" width="500" height="360" /><br>
<em>Pieces with different settings in the Levels filter. Notice the same rightmost value across all instances, corresponding to the same background color.</em>

<strong>Bonus side effect:</strong> If your original logo image has <a href="https://en.wikipedia.org/wiki/Compression_artifact">compression artifacts</a>, this step could greatly reduce them.

## Step 4: Alpha Transparency

Once all of your image’s pieces have been “leveled” into black and white, use the Pointer tool to select an image piece and apply a “Convert to Alpha” filter (in the Properties panel, go to Filters: [+] → Other → Convert to Alpha). Doing this step <strong>separately per piece</strong> is important because each piece has a <em>different setting</em> in the Levels filter. If you were to apply a new filter to all pieces at once, Fireworks would equalize the settings for all of the other filters present.

<img loading="lazy" decoding="async" class="111142" title="Convert to Alpha filter" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72025b4a-cd4b-4437-b7ca-d763a4b124bc/elul-04.png" alt="Convert to Alpha filter" width="500" height="500" /><br>
<em>Apply a “Convert to Alpha” filter to each piece.</em>

In this step, you will again be able to check for the accuracy of your settings for the Levels filter; if the black area of an image piece is not completely black, it will show up as slightly transparent once the Alpha filter is applied. (This is where the checkerboard background of the canvas comes in handy.) Also, if the background is not completely white, you’ll see it faintly after converting the image piece to alpha.

<img loading="lazy" decoding="async" class="111143" title="Convert to Alpha filter applied to all pieces" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d953aa4-8ff7-43ba-8479-3c41344cc6b5/elul-04a.png" alt="" width="500" height="360" /><br>
<em>Applying the “Convert to Alpha” filter to all pieces.</em>

## Step 5: Recolor

At this point, you have successfully extracted the logo form from its background. The next step is to bring back the original colors. To do this, open the Layers panel (<code>F2</code>, or in the menu Window → Layers), and look for the object that you hid at the beginning of this tutorial. Click on the visibility box at the left end of that object to make it visible again. Nudge it down so that it’s below the processed logo pieces and in clear view. Use the Pointer tool to select an image piece and apply a Color Fill filter (in the Properties panel, go to Filters: [+] → Adjust Color → Color Fill). In the Color Fill settings, click on the color swatch, and sample the corresponding color from the original logo image. Do the same for all other image pieces.

<img loading="lazy" decoding="async" class="111156" title="Color Fill filter applied to first piece" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/350d1ff9-2f4b-4e53-b41a-b0390c5ec2bf/elul-05.png" alt="Color Fill filter applied to first piece" width="500" height="500" /><br>
<em>Apply a Color Fill filter to the first piece, picking the color from the original logo image.</em>

<img loading="lazy" decoding="async" class="111157" title="How to sample a color" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23fd0731-c8a1-4a58-98d1-8352bf1b0870/elul-05m.png" alt="" width="500" height="500" /><br>
<em>To sample a color for the Color Fill filter: 1. Click on the color swatch in the filter dialog, 2. Click on the part of the image whose color you want to sample, 3. The color swatch will update with the new color.</em>

## Step 6: Convert To Symbol

Once you have recolored all of the pieces, select the original logo image with the Pointer tool and hide it (<code>Ctrl/Cmd</code> + <code>L</code>, or in the menu View → Hide Selection). You can also click on the eye icon of that object in the Layers panel to hide it. Select all of the image pieces using the Pointer tool, and convert them into a symbol (<code>F8</code>, or Modify → Symbol → Convert to Symbol…) before using it in your layout, so that new filter changes affect the new logo as a whole.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a81b9219-9175-43f9-ac40-79b70ea1007a/elul-05n.png"><img loading="lazy" decoding="async" class="111158" title="Convert to Symbol dialog" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a81b9219-9175-43f9-ac40-79b70ea1007a/elul-05n.png" alt="" width="469" height="221" /></a><br>
<em>The Convert to Symbol dialog.</em>

If you wish to make changes to the objects inside the symbol, you can do one of the following:

*   With the instance of the symbol selected, go to Modify → Symbol → Edit Symbol;
*   Right-click on the instance of the symbol, and select Symbol → Edit Symbol;
*   Double-click on the instance of the symbol.

<img loading="lazy" decoding="async" class="111145" title="All logo pieces recolored" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d0a7299-d2a3-4845-b99f-3970b949b21c/elul-05a.png" alt="" width="500" height="360" /><br>
<em>All logo pieces recolored and converted into a Symbol.</em>

### Taking It Further

You now have a version of the logo that you can set against any type of background: solid, gradient, textured or tiled. You can even use it as a <a href="https://help.adobe.com/en_US/fireworks/cs/using/WS4c25cfbb1410b0021e63e3d1152b00db4b-7f7f.html">bitmap mask</a> over a photo, pattern or gradient if you want a different look. To do this, you’ll need to flatten the logo symbol first (<code>Ctrl/Cmd</code> + <code>Alt/Opt</code> + <code>Shift</code> + <code>Z</code>, or in the menu Modify → Flatten Selection), but you can always bring back your final logo by dragging an instance of the symbol from the Document Library panel (<code>F11</code>, or Window → Document Library) onto the canvas.

<img title="Extracting Logos Using Levels In Adobe Fireworks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/858c5f3e-b776-441a-991a-ee9d11cce30e/elul-final.png" alt="Extracting Logos Using Levels in Adobe Fireworks: the final result" width="500" height="360" /><br>
<em>The final result.</em>

If you are feeling adventurous, you could try turning it into a vector object using the Magic Wand tool first (<code>W</code>) and then running the “Convert Marquee to Path” command (Select → Convert Marquee to Path). Your mileage may vary, though: “Convert Marquee to Path” doesn’t always play well with complex shapes, but you can always tweak the vector paths that are created by that command until they match the logo.

<em>(al) (mb) (vf)</em>

## Downloads

Need a sample to study? <a href="https://smashingmagazine.com/provide/extracting-logos-using-levels.zip">Download the sample archive</a> for this tutorial (ZIP file, 57.6 KB), containing the Fireworks PNG (created in Adobe Fw CS5).</p>

## Further Reading

*   “Rapid Fire #8: Extracting Logos,” SixThings My original method for extracting logos.
*   “[About Live Filters](https://help.adobe.com/en_US/fireworks/cs/using/WSBFD1EA57-0750-4ca6-BEB4-4D66917CD996.html),” Adobe Fireworks CS5 Help All about Live Filters.
*   “[Symbols](https://help.adobe.com/en_US/fireworks/cs/using/WS4c25cfbb1410b0021e63e3d1152b00db4b-7fd4.html),” Adobe Fireworks CS5 Help Working with the Symbols feature.
*   “[Select Pixels](https://help.adobe.com/en_US/fireworks/cs/using/WS4c25cfbb1410b0021e63e3d1152b00cbdc-7ffb.html),” Adobe Fireworks CS5 Help A rundown of the different pixel-selection tools.
*   “[Working with masks in Adobe Fireworks](https://www.adobe.com/devnet/fireworks/articles/masking_preso.html),” Adobe Devnet An excellent video tutorial (by Jim Babbage).</p>

## Smashing Is Looking For Experts On Fireworks, Photoshop & Illustrator

As our crafts mature, so do our tools. Fireworks, Photoshop and Illustrator are powerful tools that we, as designers, use on a regular basis. Fireworks is surely more flexible for Web at times (and UI/screen design in general), since it is dedicated specifically to the Web designer's needs. And yet, it is underrated by many. We should all indeed be more open to try out new and different tools and share the techniques and our experiences with the community.

<a title="We look forward to hearing from you!" href="https://www.smashingmagazine.com/contact/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fb5956b-d3b8-46f5-9471-3c618c94f807/call-for-authors-fw-ps-ai-v10.png" alt="We look forward to hearing from you!" width="500" height="300" /></a>

We'd love to cover <em>more</em> articles on Fireworks, Photoshop and Illustrator explaining useful techniques, tips and "lessons learned" from professional designers. So, if you:

*   Have a solid knowledge of at least one of these tools,
*   Have a solid experience in design (especially Web/screen/mobile),
*   Have a couple of articles published on any of the tools mentioned,
*   Or perhaps have even released some extensions or tools for Fireworks, Photoshop or Illustrator...

Then please drop us an email at <strong>ideas@smashingmagazine.com</strong>. Please include details about your experience, examples of your work, links to your articles and your article ideas (at least two). Of course, all authors get paid :-)

We look forward to hearing from you!

<em>— Smashing Editorial Team</em>

### Further Reading

*   [Designing for iPhone 4 Retina Display: Techniques and Workflow](https://www.smashingmagazine.com/2010/11/17/designing-for-iphone-4-retina-display-techniques-and-workflow/)
*   [Productive Web Design With… Adobe Illustrator?](https://www.smashingmagazine.com/2011/01/17/productive-web-design-with-adobe-illustrator/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/17/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)


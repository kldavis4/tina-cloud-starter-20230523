---
title: How to Design the Firefox Logo in Photoshop
slug: how-to-design-the-firefox-logo-in-photoshop
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f114036-d87e-468c-bc3b-e2985487ba9d/firefox-logo-31.jpg
date: 2008-05-01T20:43:27.000Z
author: henryhoffman
description: >-
  This tutorial will go through how you can create the Firefox logo in a
  scalable Photoshop format.
categories:
  - Graphics
  - Logo Design
  - Photoshop
---
This tutorial will go through how you can create the Firefox <a href="https://www.smashingmagazine.com/2009/08/vital-tips-for-effective-logo-design/">logo</a> in a scalable <a href="https://www.smashingmagazine.com/professional-photoshop-techniques-tutorials/">Photoshop</a> format. 
<em><br>
</em>

## The World

Firstly create a new document at 1024px x 970px and start off with selecting the <strong>ellipse tool (U)</strong> and drawing a large circle (hold <em>SHIFT</em> to constrain the proportions) and make the top of the circle nearly touch the top of the document and the bottom of the circle nearly touch the base of the document. Change the colour of this new shape by double clicking the colour next to your shape in the <em>Layers Palette</em> and then entering <code>#1f0e6d</code> in the space underneath RGB. This is your basic shape for your globe and should look like this:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3daa88a-f78d-447f-95cd-0388821239f1/firefox-logo-1.jpg" alt="Firefox Logo Step 1" /><br>
<figcaption>We first create the world shape</figcaption></figure>

We now need to duplicate the world shape by right clicking on the circle we’ve just created in the <em>Layers Palette</em> and clicking <em>Duplicate</em>. We need to scale this down slightly, so press <em>CTRL+T</em> and you will be switched to <em>Free Transform</em> in which we can manipulate the shape freely. Scale the shape down ever so slightly by selecting the top-right resizing handle and by dragging inwards whilst holding both <em>SHIFT+ALT</em>.  Now we add a new gradient layer by going <em>Layer&gt;New Fill Layer&gt;Gradient</em>. Give it a name and click OK and you should be brought up with a gradient fill dialogue. Now you need to click on the gradient next to <em>Gradient:</em> (not the dropdown, the actual gradient) and this should bring up a gradient editor. Along the gradient slider there should be a black box on the bottom left and a white box on the bottom right. Double click on the left black box and change its colour to <code>#251979</code> and then double click the right box and change the colour to <code>#67c4d4</code>. Then click the top right box and change its <em>Opacity </em>value to <code>100%</code>. Click OK and you should be presented with a <em>Layers Palette</em> that looks like this:

{{% feature-panel %}}

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48ca9232-f21b-42d4-b61f-cdf33f6002c7/firefox-logo-2.jpg" alt="Firefox Logo Part 2" /><br>
<figcaption>Your layers palette should look like this.</figcaption></figure>

Now you need to click on your 3rd layers (or what should be called ‘Shape 1 Copy’) vector mask and drag it onto your newly created gradient fill layer. This should create a vector mask for your gradient fill layer and should look like this:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e044b4a-0bb0-4512-b70e-b3b077621597/firefox-logo-3.jpg" alt="Firefox Logo Part 3" /><br>
<figcaption>The layers palette with your new vector mask.</figcaption></figure>

Now comes the tricky part, creating the land on the globe. To achieve this we use the <strong>pen tool (P)</strong> to create the organic shapes required to look like the land. Select the <strong>pen tool (P)</strong> and make sure <em>Shape Layers</em> is selected in the tools menu instead of <em>Paths</em>. Now begin the clicking and dragging process involved in using the <strong><em>pen</em> tool</strong> until you achieve the following result (I can’t help any more than this for the <strong>pen tool (P)</strong> but if you want to cover the basics check out this tutorial):

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22695496-f677-478d-8009-d238277b685c/firefox-logo-4.jpg" alt="Firefox Logo Part 4" /><br>
<figcaption>The globe with the land added. </figcaption></figure>

Now we need to subtract a piece of land from the island we’ve created and to do this you click on the vector mask on the land shape in the <em>Layers Palette</em> (with the <strong>pen tool (P)</strong> still selected) to select the land; then click the <em>Subtract From Shape Area</em> button on the tool options bar. Now just remove the piece of land using the same method used for adding it until you have removed the piece shown in the image below:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b0b9d3b-edf0-4549-8806-88cd349711f5/firefox-logo-5.jpg" alt="Firefox Logo Part 5" /><br>
<figcaption>Remove the chunk displayed from your land shape. </figcaption></figure>

With your shape selected, we now need to invert the land so that it appears the same as on the Firefox logo. To do this, select the <strong>path selection tool (A)</strong> and select just your main land (not the subtracted one). Now press the ‘-‘ (minus) button to invert the selection and then click your subtracted piece of land and press ‘+’ (plus) to add the island back to the shape. Now right click on your layer in the layers palette and select <em>Create Clipping Mask</em> to clip your land to the globe and it should look like this:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/589a1046-6734-49e4-9bf2-f4b27d24e6da/firefox-logo-6.jpg" alt="Firefox Logo Part 6" /><br>
<figcaption>This is how you're globe should look with the land removed. </figcaption></figure>

Now to achieve a gradient effect utilising layer styles. To achieve this you need to select <em>Layer&gt;Layer Style&gt;Gradient Overlay</em> in the Photoshop menu and you will be presented with the options needed to edit a gradient. Click on the gradient next to <em>Gradient:</em> (not the dropdown, the actual gradient) and this should bring up a gradient editor. Along the gradient slider there should be a black box on the bottom left and a white box on the bottom right. Double click on the bottom left black box and change its colour to <code>#00022e</code> and slide it along until <em>Location</em> reads <code>40%</code>. Then double click the bottom right box and change the colour to <code>#0f80bc</code>, click OK, OK, OK and you should be presented with this:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38c2b6df-42fe-458c-9739-192adb772de2/firefox-logo-7.jpg" alt="Firefox Logo Part 7" /><br>
<figcaption>The globe with a subtle gradient. </figcaption></figure>

Now we need to create the classic Web 2.0 shiny orb effect (when will we tire of it?) by selecting the <strong>ellipse tool (u)</strong> and drawing an oval at the top of the globe so that it looks like this:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6b74be0-5c34-430c-bc98-cc89f2c15423/firefox-logo-8.jpg" alt="Firefox Logo Part 8" /><br>
<figcaption>Add the reflection. </figcaption></figure>

Now select <em>Layer&gt;Layer Style&gt;Gradient Overlay</em> in the Photoshop menu and you will be presented with the options needed to edit a gradient. Click on the gradient next to <em>Gradient:</em> (not the dropdown, the actual gradient) and this should bring up a gradient editor. Along the gradient slider double click the bottom left black box and change it to <code>#ffffff</code> (white). Now click the upper left black box and change the <em>Opacity</em> to <code>0%</code> and location to <code>40%</code>. Click OK and this will appear to make no difference. Click the <em>Blending Options</em> in the layer style dialogue and look for the <em>Advanced Blending</em> section. In this section should be a <em>Fill Opacity</em> slider which you need to drag to <code>0%</code>. Above that section is <em>General Blending</em> where you’ll find an <em>Opacity</em> slider which needs to be dragged to <code>50%</code>.

After this brief bit of advanced blending, click OK and you should be presented with this:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4989a93a-3562-4997-b9f4-ce93317f3db8/firefox-logo-9.jpg" alt="Firefox Logo Part 9" /><br>
<figcaption>The finished globe.</figcaption></figure>

## The Fox

The fox is definitely the tricky bit and you’ll need to have a good understanding of the pen tool and how it works to pull this off. I am writing the following on the presumption that you have managed to achieve the previous section of this tutorial and are confident with the pen tool and layer styles.

First we need to start off with the arm. Draw the following shape with the <strong>pen tool (P)</strong> and double click the layer to bring up the <em>Layer Style</em> dialogue. Change the gradient properties until you achieve a result that resembles the image following. I used the colours <code>#941403</code> and <code>#c04b11</code> to achieve the following effect (remember to tweak the angle and scale in the layer styles dialogue to achieve the desired result):

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c34e5ba2-befe-4676-9f82-aacb98598551/firefox-logo-10.jpg" alt="Firefox Logo Part 10" /><br>
<figcaption>We start with the arm. </figcaption></figure>

Now we have the base of the arm. We now need to duplicate this layer so we can add the orange upper-half of the arm. After the layer has been duplicated (right-click, duplicate in <em>Layers Palette</em>) we need to subtract a chunk out of it in the same way we removed land from the globe in the first part of this tutorial; click on the vector mask of your duplicated shape in the<em> Layers Palette</em> and with the <strong>pen tool (p)</strong> selected click the <em>Subtract Shape Area</em> Button. Now draw a curve that matches the image that follows, removing the lower part of the foxes arm. Once complete, double-click the colour at the side of the layer and apply <code>#d46518</code> as the shapes fill colour. Tweak the angle and scale in the layer styles dialogue to achieve the desired result and you should now have something that resembles this:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a71b278-1ab9-4c94-a626-9b7f77889c97/firefox-logo-11.jpg" alt="Firefox Logo Part 11" /><br>
<figcaption>The arm and shading. </figcaption></figure>

We now need to create a quick highlight. To do this select the <strong>pen tool (p)</strong> and draw a shape on the fox’s paw that resembles the image that follows. Apply a simple layer style with a gradient that uses <code>#f5f498</code> colour for the left gradient box and the same colour on the right but with <code>0%</code> opacity. Click Ok, Ok and go to <em>Blending Options</em> in the layer styles dialogue and in <em>Advanced Blending</em> change <em>Fill Opacity</em> to <code>0%</code>. Tweak the angle and scale in the <em>layer style</em> dialogue to achieve the desired result and he result should be something like the following:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a007550b-e36a-49dd-845d-23466c5ef8f8/firefox-logo-12.jpg" alt="Firefox Logo Part 12" /><br>
<figcaption>The completed arm with highlights. </figcaption></figure>

Now we need to start creating the bulk of the fox’s shape. We’ll start with the initial outline and can then build the details of the fox as individual layers. Begin by creating the fox outline that includes the ear but excludes the head as the following image demonstrates (using the <strong>pen tool (p)</strong>).</p>

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6681f1af-b80f-4bbe-8540-da81cfd3550b/firefox-logo-13.jpg" alt="Firefox Logo Part 13" /><br>
<figcaption>The body base shape. </figcaption></figure>

Then bring up the <em>layer style</em> dialogue and apply a new gradient using the colours in a similar manner to what I have used as follows (to add new colours to the palette, click an empty space on the gradient slider). Tweak the angle and scale in the layer styles dialogue to achieve the desired result.</p>

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1d758b0-d714-4cc3-98ac-4043a35b9369/firefox-logo-14.jpg" alt="Firefox Logo Part 14" />The fox's body gradient.
<figcaption>The foxes outline should hopefully now look like this:</figcaption></figure>

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7821f1a5-4b5c-4df7-ab3a-67aa49e4863c/firefox-logo-15.jpg" alt="Firefox Logo Part 15" /><br>
<figcaption>The fox with the gradient applied. </figcaption></figure>

You’ll notice that the fox’s tail is far too red with the existing gradient applied. A quick and easy way to get rid of this is to duplicate the foxes outline and with the pen tool selected and <em>Subtract From Shapes Area</em> selected, draw a shape removing everything but the foxes tail. Then in the <em>layer style</em> dialogue, tweak the gradient to remove the redness of the tail tip.

Now using the techniques employed before we need to begin on the fox’s jaw and snout. Begin by drawing the lower part of the snout with the <strong>pen tool (P)</strong> and change the shapes fill colour to <code>#ffffcc</code>.</p>

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/253f3949-275c-4673-b03b-e8d7024c49d3/firefox-logo-16.jpg" alt="Firefox Logo Part 16" /><br>
<figcaption>The beginnings of the jaw. </figcaption></figure>

We now create a new shape to act as the jaw’s highlight. Draw a shape similar to that which follows, using the fill colour <code>#eea273</code>. The shape can spill over the bottom half of the jaw because we then apply a clipping mask by right-clicking on the new layer and selecting <em>Create Clipping Mask</em>. This should nicely anchor your new shape to the jaw and remove any of the shapes overspill.</p>

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa9c6e6c-24c7-40a1-8876-2e4aed88f9de/firefox-logo-17.jpg" alt="Firefox Logo Part 17" /><br>
<figcaption>The jaw shading. </figcaption></figure>

The upper snout now needs to be created, so with the <strong>pen tool (P)</strong> draw the following shape and change the gradient in the layer styles dialogue (double click the layer in the <em>layers palette</em>) to use the colours <code>#9a1d06</code> and <code>#db5009</code>, remembering to tweak the scale and angle in the layer styles dialogue.</p>

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4959efd0-0262-4fea-8c9b-c8ef4726d970/firefox-logo-18.jpg" alt="Firefox Logo Part 18" /><br>
<figcaption>The upper snout starts to take shape. </figcaption></figure>

We now need to create a subtle highlight to the fox’s upper snout. To do this, duplicate the upper snout you’ve just created and with the <strong>pen tool (P)</strong> selected, select the <em>Subtract From Shape Area</em> and remove the chunk as illustrated below.</p>

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ea5ef41-b99d-4454-a8b9-1220915f3be4/firefox-logo-19.jpg" alt="Firefox Logo Part 19" height="398" /><br>
<figcaption>Add subtle highlights to the fox's snout. </figcaption></figure>

Now change the layer style of this highlight to have a gradient using the colour <code>#df731b</code> in both boxes, but with the right box having <code>0%</code> opacity. Then remember to go to <em>Blending Options</em>, look for <em>Advanced Blending</em>and change the <em>Fill Opacity</em> to <code>0%</code>. Remember to go back to <em>Gradient Overlay</em> in the layer style dialogue and tweak the <em>Angle</em> and <em>Scale</em> to match the image below. You should end up with something like this:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c68f4f3-f779-4f37-a2e6-a904b28988bf/firefox-logo-20.jpg" alt="Firefox Logo Part 20" /><br>
<figcaption>Fade out the highlights of the highlights. </figcaption></figure>

Finally add a black button nose with a simple black/white <em>Gradient Overlay</em> and drag the layer beneath the other snout shapes in the layers palette.

Now we need to refine the details of the fox’s tail. Create a shape that resembles the following and apply a <em>Gradient Overlay</em> layer style with a gradient that resembles the following (remember to tweak the angle and scale in the <em>Gradient Overlay</em> options in the <em>Layer Style</em> dialogue):

The shape should look like this:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3919956-f66d-48b0-87ac-d27ebad5bfd3/firefox-logo-21.jpg" alt="Firefox Logo Part 21" /><br>
<figcaption>Fox's tail highlight shape. </figcaption></figure>

The gradient should look like this:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7be0920a-d7f9-4232-b479-c806f6061c11/firefox-logo-22.jpg" alt="Firefox Logo Part 22" /><br>
<figcaption>The gradient for the tail highlights. </figcaption></figure>

Together they should look like this:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a957c4ef-34ea-4b88-94b4-885f15ef1a35/firefox-logo-23.jpg" alt="Firefox Logo Part 23" /><br>
<figcaption>The tail highlight with gradient applied. </figcaption></figure>

Repeat this process until all the detail on the tail is complete, using the same gradient styles, just tweaking them slightly to suit each separate bit of detail. After you have finished the detail you should have something that looks like this:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f216abe1-e805-45aa-abd5-8e592b2acf0e/firefox-logo-24.jpg" alt="Firefox Logo Part 24" /><br>
<figcaption>The tail starts to look more defined. </figcaption></figure>

Now you need to create the final piece of detail to the tail that also acts as the shadow to the fox’s back. To do this, duplicate the shape that makes up the fox’s body and in the <em>Layers Palette</em>, drag in to the top so that it overlays all your existing layers. Now select the <strong>pen tool (P)</strong> and <em>CTRL+click</em> your shape to bring up the shapes outline with all the anchor points displayed. Single click the majority of the anchor points to delete them and pull a few of the existing ones about until you get a shape that resembles the image that follows. Change the gradient overlay in the <em>Layer Style</em> dialogue to also resemble the following (tweak the layer style you used for the tails detail before):

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e3d1ce6-6058-409a-bd5e-bbe066c49216/firefox-logo-25.jpg" alt="Firefox Logo Part 25" /><br>
<figcaption>The fox's back and finished tail definition. </figcaption></figure>

The fox’s head of hair now needs to be created by drawing the following shape with the <strong>pen tool (P)</strong>. You need to create a <em>Layer Style</em> with a <em>Gradient Overlay</em> that uses the colours <code>#df731b</code> and <code>#e79041</code> and in the <em>Gradient Overlay</em> properties in the <em>Layer Style</em> palette, change the gradient type to <em>Radial</em> instead of <em>Linear</em>. This way we can add a circular highlight that follows the arch of the fox’s head. Your result should look something like this:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94781520-a6c5-4eb3-859b-ebd525b7571b/firefox-logo-26.jpg" alt="Firefox Logo Part 26" /><br>
<figcaption>Nearly done - the fox's head begins to take shape. </figcaption></figure>

This radial gradient that we employed previously unfortunately hasn’t encompassed the top of the fox’s head as hoped, so we need to duplicate the previous layer and using the <strong>pen tool (p)</strong> select <em>Subtract From Shapes Area</em> and remove <code>80%</code> of the fox’s hair from roughly below the snout. I have highlighted the shape as green in the following example so you can see what I mean:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8a8e7c8-15f4-4e6d-be4b-8e428effadd8/firefox-logo-27.jpg" alt="Firefox Logo Part 27" /><br>
<figcaption>The area you need to subtract from the duplicated shape. </figcaption></figure>

Now change the gradient overlay in the <em>Layer Style</em> dialogue to create a highlight on the upper part of the fox’s head. The result should be as follows:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94776af7-c1a4-4c87-8510-fa48ad53ca99/firefox-logo-28.jpg" alt="Firefox Logo Part 28" /><br>
<figcaption>The gradient applied to the upper head. </figcaption></figure>

Now we need the ear to appear in front of the head, so we have to duplicate the layer you just created and cut off everywhere apart from the ear using the <strong>pen tool (P)</strong> with <em>Subtract From Shape Area</em> selected. I have an example below, with the ear highlighted in green so you can see the exact shape that needs to be used:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36e38b3c-edc3-4de5-840d-ece8d2b884c5/firefox-logo-29.jpg" alt="Firefox Logo Part 29" /><br>
<figcaption>The ear shape to remove from your duplicated layer. </figcaption></figure>

Now apply a gradient overlay in the <em>Layer Style</em> dialogue and modify the gradient so it resembles the following image:

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79893f22-4cce-4052-b470-3ee8a960e7d0/firefox-logo-30.jpg" alt="Firefox Logo Part 30" /><br>
<figcaption>The ear with a gradient applied. </figcaption></figure>

Finally you need to create the last bits of detail to the fox’s hair in a similar fashion to how you created the detail to the fox’s tail. Draw a succession of spiky hair shapes as seen in the image below and create a gradient that uses the colours <code>#e27d23</code> and <code>#efa869</code>, making sure you alter the angle and scale for the gradient in each spike to blend it in with the fox’s hair.</p>

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f114036-d87e-468c-bc3b-e2985487ba9d/firefox-logo-31.jpg" alt="Firefox Logo Part 31 - Final Result" /><br>
<figcaption>The final result!</figcaption></figure>

## Whew. . .

That should be it, you should end up with a Firefox logo that looks like the one above. This uses several techniques that perhaps aren't as manageable as if you approached the same task in Illustrator, but it avoids the classic problem of having to jump between Illustrator and Photoshop to make alterations, giving you a bit more flexibility. Now you have a customisable, scalable Firefox logo for whatever uses you desire. If there are any questions, please leave a comment below and I’ll try and help you as best I can.

You can download the source file here: <a href="https://smashingmagazine.com/provide/Freebies/firefoxlogo.psd">Download Source </a>


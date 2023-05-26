---
title: The Retina Asset Workflow You've Always Wanted For Photoshop
slug: the-retina-asset-workflow-youve-always-wanted-for-photoshop
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d50d0777-f642-4e05-a29a-8d302365d0e7/projectmockup-500px-opt.jpg
date: 2016-03-22T17:28:56.000Z
author: murdochcarpenter
description: >-
  If you’ve dreamed of the day when **you could design more than one thing at
  once** in Photoshop, the wait is over. You can now have multiple designs right
  next to each other. Design mobile layouts alongside your tablet and desktop
  layouts. And in this article, we’ll design an entire set of assets all at
  once.

  What many Photoshop users have been hoping for — with a push from Sketch, no
  doubt — finally arrives in the form of **artboards**. No longer are you
  constrained to one canvas. Turning layer groups on and off, be gone. Create as
  many canvases as you like in one PSD.
categories:
  - Mobile
  - Graphics
  - Workflow
  - Photoshop
  - Retina
---
If you’ve dreamed of the day when <strong>you could design more than one thing at once</strong> in Photoshop, the wait is over. You can now have multiple designs right next to each other. Design mobile layouts alongside your tablet and desktop layouts. And in this article, we’ll design an entire set of assets all at once.

What many Photoshop users have been hoping for — with <a href="https://www.smashingmagazine.com/2015/04/using-sketch-for-responsive-web-design-case-study/">a push from Sketch</a>, no doubt — finally arrives in the form of <strong>artboards</strong>. No longer are you constrained to one canvas. Turning layer groups on and off, be gone. Create as many canvases as you like in one PSD.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Create Pixel-Perfect Assets For Multiple Scale Factors](https://www.smashingmagazine.com/2014/10/create-assets-for-multiple-scale-factors/)
*   [A Better Way To Design For Retina In Photoshop](https://www.smashingmagazine.com/2015/05/retina-design-in-photoshop/)
*   [Photoshop Etiquette For Responsive Web Design](https://www.smashingmagazine.com/2016/08/photoshop-etiquette-for-responsive-web-design/)
*   [Retinize It: Free Photoshop Action For Slicing Graphics For HD Screens](https://www.smashingmagazine.com/2013/07/retinize-it-photoshop-action-slicing-graphics-retina/)

Combine artboards with the <strong>Generate</strong> feature and you get the workflow you’ve always wanted. Slicing and “Save for Web,” step aside. Automatically export @1x to @3x Retina assets just by renaming layers.

{{% feature-panel %}}

Let me walk you through the basics of artboards and Generate. Then we’ll look at a real project in which I used these techniques together, making for a major time-saver. First up, artboards.</p>

## Artboards

While layer comps were an attempt to address the goal of working on multiple pages in a PSD, they were a bit clunky and restricted you to the same canvas dimensions. Artboards free you from these contraints and let you get on with design. At first, it might not sound like a big deal, but trust me, it is. Once you go artboards, you never go back.

In the past, working on Photoshop files needed some file-management skills. You would name your pages something like <code>01_home.psd</code>, <code>02_products.psd</code>, <code>03_contact.psd</code>, etc. For complex websites, your files would quickly reach into the tens or even hundreds (especially counting versions). With artboards, you can consolidate all of these individual PSDs into a single <code>website.psd</code>. Think of all the time wasted opening and closing PSDs.

Not to mention duplication. Take a humble header as an example. It could be duplicated through tens or hundreds of PSDs. What a waste of file size and memory. Think how the same goes for the footer and many other components.

OK, enough of me preaching about how great artboards are. Let’s get into it.</p>

### Artboard Tool

Hidden behind the Move tool is the new Artboard tool, introduced in Photoshop CC (2015). Select the tool in the menu, or hit <code>Shift + V</code> to switch between the Move and Artboard tools. You are now ready to create your first artboard.</p>

<figure><img title="The Artboard tool" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/906e08a3-77da-483a-a80a-f95a507bbb89/artboardstool-500px-opt.jpg" alt="The new Artboard tool" /><br>
<figcaption>The new Artboard tool.</figcaption></figure>

### Creating and Duplicating Artboards

Simply click and drag an area to create an artboard. The default names are <code>Artboard 1</code>, <code>Artboard 2</code> and so on. You will see your new artboard in the Layers panel. Any layers will be neatly nested below, just like a layer group.</p>

<figure><img title="New Artboard is added and shown in the Layers panel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c440817-8914-4592-98b4-2b40b40fecbe/artboardscreate-500px-opt.jpg" alt="New Artboard is added and shown in the Layers panel" /><br>
<figcaption>New Artboard is added and shown in the Layers panel.</figcaption></figure>

To create another artboard, simply drag an area again in the empty background space. You can create as many artboards as you like.</p>

<figure><img title="A second artboard created by dragging a new area" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb98f7ba-2d7a-41e1-b88e-aa610b9f217a/artboardsdrag-500px-opt.jpg" alt="A second Artboard created by dragging a new area" /><br>
<figcaption>A second artboard created by dragging a new area.</figcaption></figure>

You can also duplicate an artboard in the contextual menu. In the Layers panel, right-click on <code>Artboard 1</code> and select “Duplicate Artboard.” This will create another artboard of the exact same size and position.</p>

<figure><img title="Artboard contextual menu showing further options" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3424d905-9238-4d21-8597-289433f8bc53/artboardsduplicate-500px-opt.jpg" alt="Artboard contextual menu showing further options" /><br>
<figcaption>Artboard contextual menu showing further options.</figcaption></figure>

Duplicating artboards is probably the feature I use the most. Normally, when creating assets, I need a full set of exactly the same layer structure. In the example project I’ll discuss later, once I set up my first artboard, I duplicate all of the rest. Then, with the layers, icon and type in the correct positions, all I need to do is swap these assets out. It’s a very quick way to keep everything pixel-perfect.</p>

### Resizing and Moving Artboards

There are a few ways to resize and move artboards. You have probably already noticed the first way: When an artboard is selected, you can resize using the transform handles that appear. This is very handy for resizing on the fly and seeing the layers beneath an artboard while resizing.</p>

<figure><img title="Using the transform handles to resize an artboard" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae224e92-0639-4eee-b9fa-7a16de66bec3/artboardsresize-500px-opt.jpg" alt="Using the transform handles to resize an artboard" /><br>
<figcaption>Using the transform handles to resize an artboard.</figcaption></figure>

While an artboard is selected, you can also use the Options panel just below the “File” menu. There are options to choose preset sizes, set custom widths and heights, and perform common tasks like switching to portrait or landscape.</p>

<figure><img title="Change an artboard's size using the Options panel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3365f7ed-8f8a-4dcb-a0ed-532412f63fd6/artboardsoptions-500px-opt.jpg" alt="Change an artboard's size using the Options panel" /><br>
<figcaption>Change an artboard’s size using the Options panel.</figcaption></figure>

If those aren’t enough options for you, there is also the Properties panel when an artboard is selected. This gives you the option to change the size and position and to access the preset sizes.</p>

<figure><img title="Resizing and positioning using the Properties panel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/338568b5-b108-4db7-b8c0-70e654e149a9/artboardsporperties-500px-opt.jpg" alt="Resizing and positioning using the Properties panel" /><br>
<figcaption>Resizing and positioning using the Properties panel.</figcaption></figure>

Moving an artboard can also be done with your keyboard, just like a regular layer or object. While the artboard is selected, use an arrow key for a 1-pixel nudge, or hold <code>Shift</code> for 10 pixels.

The last way to move an artboard is by clicking the name of the artboard so that it is selected, and then clicking and dragging to any position. This is particularly useful because it is smart-guide-enabled, which means you can align all of your artboards by, say, 50 pixels and their positions will lock according to your previous spacing. Now that you’ve got the hang of artboards, let’s check out the Generate feature.

You can also check out the “<a href="https://helpx.adobe.com/photoshop/using/artboards.html">Artboards</a>” section of Photoshop Help if you want to learn more.

## Generate

This is another Photoshop feature that you might not have delved into yet; it is well worth your while. Generate lets you export layers and groups by using a special naming convention in your layer names. Think of it as a “Save for Web” shortcut just by renaming a layer. In most cases, it will completely replace having to go through the “Save for Web” dialog, which will save you precious time and keep you focused on what matters: the design. Let’s take a look.</p>

### Turn on Generate

Generate can be turned on and off for each PSD. When it’s active, any layers with the special naming syntax will automatically be exported. Make sure you have it checked by going to “File” → “Generate” → “Image Assets.”

<figure><img title="Generate menu option" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f2606ae-c00f-4a48-84e0-c36d20968c33/generatemenu-500px-opt.jpg" alt="Generate menu option" /><br>
<figcaption>Generate menu option.</figcaption></figure>

### What Can Be Generated?

Basically, any layer in the Layers panel can be used with Generate, be it a bitmap layer, shape layer, layer group, smart object, etc. Even layers within layer groups can be exported. As long as the layer name has the correct syntax, it’s good to go. We will discuss later how this can be applied to artboards, but let’s not get ahead of ourselves. Let’s start with the basics.</p>

### Generate Basics

Now that we are all set up to generate images assets, having checked the menu item, let’s try out some of the options. Just by adding an extension — <code>-opt.jpg</code>, <code>.gif</code> or <code>.png</code> — to your layer or group name, you can save out an <code>opt.jpg</code>, GIF or PNG. These are the three image options currently supported by Generate. When image assets are created, they are saved in a new folder alongside your PSD. And they have the same name, but with an <code>-assets</code> suffix:

<pre>[ end1a-opt.jpg ][ end1b.gif ][ end1c.png ]</pre>

<figure><img title="Showing generated images from layer names" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54b40a3b-a3fa-4a2f-b9df-40547bc02499/generateextension-500px-opt.jpg" alt="Showing generated images from layer names" /><br>
<figcaption>Showing generated images from layer names.</figcaption></figure>

Notice from the screenshot that only the layers with <code>-opt.jpg</code>, <code>.gif</code> or <code>.png</code> have generated image assets. The layer groups <code>end2a</code>, <code>end2b</code>, <code>end2c</code> didn’t export. Any layers that don’t include extensions are not exported.

There are also compression options for <code>opt.jpg</code> and PNG. For <code>opt.jpg</code>, I would recommend using the percentage syntax, which is 1 to 100%. For PNG, the options are simply 8, 24 or 32, which correlate to their bit formats. Just add the compression options directly to the layer name after the extension of <code>-opt.jpg</code> or <code>.png</code>, as shown here:

<pre>[ end1a-opt.jpg100% ][ end1b-opt.jpg40% ][ end1c-opt.jpg10% ]</pre>

<figure><img title="Output showing opt.jpg compression" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bac15967-ef6f-41d6-bf11-b4adea06f8c6/generatecompression-500px-opt.jpg" alt="Output showing opt.jpg compression" /><br>
<figcaption>Output showing <code>opt.jpg</code> compression.</figcaption></figure>

You can also export multiple images from the same layer. Use a comma (<code>,</code>) or plus (<code>+</code>) separator between image names, as shown below. Just make sure that each name is unique (a requirement of Generate).

<pre>[ 1a_1-opt.jpg, 1a_2-opt.jpg, 1a_3-opt.jpg ] or [ 1a_1-opt.jpg + 1a_2-opt.jpg + 1a_3-opt.jpg ]</pre>

<figure><img title="Output showing multiple images exported from one layer" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d22536dc-e2fd-4d9c-bc5b-2aea7a3220c2/generatemultiple-500px-opt.jpg" alt="Output showing multiple images exported from one layer" /><br>
<figcaption>Output showing multiple images generated from one layer.</figcaption></figure>

You can also set the scale of the output as a percentage or in pixels. This goes in the layer name before the image name. The percentage is easy to figure out, and pixels is simply the standard width by height. Here is an example:

<pre>[ 50% end1a-opt.jpg ][ 75% end1b-opt.jpg ][ 100% end1c-opt.jpg ] or [ 100x50 end1a-opt.jpg ][ 200x100 end1b-opt.jpg ][ 300x150 end1c-opt.jpg ]</pre>

<figure><img title="Output showing various scales in percentage" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c85de3e-587d-4fe8-b6c8-645accdf8ce2/generatescale-500px-opt.jpg" alt="Output showing various scales in percentage" /><br>
<figcaption>Output showing various scales in percentage.</figcaption></figure>

All of these custom syntaxes can be combined with each other to form complex image assets from your layers. Here is an example of scale, compression and image types all on one layer:

<pre>[ 150% layername-opt.jpg80% + 50% layername.png8 ]</pre>

As I’m sure you can see, the combination of scale, compression and image types is a powerful way to consistently export image assets.</p>

### Advanced Generate

If those aren’t enough options for you, there is also the default setting that gets applied to all Generate layers in your document. The default is created by making an empty layer in your document. I use the very top layer of my PSD so that I can always find it. Let’s look at an example.

<pre>[ default 150% large/_large + 50% small/_small ]</pre>

<figure><img title="Default layer example in the Layers panel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4667e530-a20b-4edd-96e7-122a84986873/generatedefaultline-500px-opt.jpg" alt="Default layer example in the Layers panel" /><br>
<figcaption>Default layer example in the Layers panel.</figcaption></figure>

The <code>default</code> keyword defines this layer as the default setting. Do not change this. The <code>150%</code>, which is next, defines the scale. After that is something new. The <code>large/</code> and <code>small/</code> set the folders where these will be saved. And then <code>_large</code> and <code>_small</code> add suffixes to your file names. All you need to do to activate the output is to add an extension to the layer, such as <code>-opt.jpg</code> or <code>.png</code>. Now, all of the images with Generate layer names will be exported with these settings. Awesome, right?

Not convinced? Let me illustrate how this saves time. Below is Generate on individual layers.</p>

<figure><img title="Using layer names can get repetitive" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3abc431-2ea9-4898-941d-f29a8e9d149e/generatelayers-500px-opt.jpg" alt="Using layer names can get repetitive" /><br>
<figcaption>Showing the Layers panel using each and every layer.</figcaption></figure>

And here is the same but using the default:

<figure><img title="Showing Layers panel using default" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7977f91-8105-4e28-820d-9e30d313333b/generatedefault-500px-opt.jpg" alt="Showing Layers panel using default" /><br>
<figcaption>Showing Layers panel using default.</figcaption></figure>

As you can see, this will save you from repetitively naming layers. It also adds some very advanced options for folder outputting and default settings across all of your generated output. It is a massive time-saver for sure. Once you give this a try, I doubt you will ever go back to the traditional “Save for Web” dialog and layers.

Still excited and want more on Generate and its syntax? Then check out “<a href="https://helpx.adobe.com/photoshop/using/generate-assets-layers.html">Generate Image Assets From Layers</a>” by Chris Converse, posted in Photoshop Help.</p>

## The Perfect Combo

As I hinted at the beginning of this article, these techniques really shine when used together: the combination of artboards to visualize multiple canvases at once, and Generate to export multiple image resolutions.

I put this into practice in a recent project while being contracted by <a href="https://www.bigdb.co.uk/">BIG</a>. This project occurred in conjunction with <a href="https://www.gotobermuda.com/">Bermuda Tourism</a> and <a href="https://www.expedia.com/"> Expedia</a>. You can view the result on the <a href="https://explorebermuda.us/">Explore Bermuda</a> website. Basically, the experience lets you see Bermuda through first-person video by picking your own path. Cool, right?

What we will focus on here are the final images, for which I used the combined technique of artboards and Generate. During the experience, you can choose A, B or C at five decision points, which then builds an itinerary based on your choices. Here are screenshots of the itinerary:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83d48631-b423-4cae-9bf3-cd7f10f2a44a/projectmockup-large-opt.jpg"><img title="Screenshots showing the itinerary screen of the Bermuda experience" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d50d0777-f642-4e05-a29a-8d302365d0e7/projectmockup-500px-opt.jpg" alt="Screenshots showing the itinerary screen of the Bermuda experience" /></a><figcaption>Screenshots showing the itinerary screen of the Bermuda experience. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83d48631-b423-4cae-9bf3-cd7f10f2a44a/projectmockup-large-opt.jpg">View large version</a>)</figcaption></figure>

### Image Assets

To support phones, tablets and desktop, the final images needed to be exported at @1x, @2x and @3x. There were also wide and tall versions to better fit on phones. The PSD used as an example here is for the tall version. So, the 15 images quickly became 45 for each tall and wide version to support Retina displays!

If you are not familiar with the terms @1x, @2x and so on, then I’d suggest having a quick read of my article, “<a href="https://www.smashingmagazine.com/2015/05/retina-design-in-photoshop/">A Better Way to Design for Retina in Photoshop</a>.” It explains why I think this is the best technique when working with Retina assets and also why I design @1x.

Great! So, now you know what I needed to produce. Let’s walk through how I got there.</p>

### Layers to Artboards

The first improvement to my regular workflow was to change from layers to artboards. This is really powerful from a design perspective. You can now compare all of your assets that need to work together. I could make sure that all of the color options were correct and that all of the images work together as a set.</p>

<figure><img title="Comparison of layer groups and artboards in the Layers panel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8800a3c-2e10-46c2-8e5f-01fb2ad7854b/projectlayersvsartboards-500px-opt.jpg" alt="Comparison of layer groups and artboards in the Layers panel" /><br>
<figcaption>Comparison of layer groups and artboards in the Layers panel.</figcaption></figure>

Look at the comparison of layer groups and artboards above. As you can see, there isn’t much change here, nothing to scare you off: layers on the left and artboards on the right of the image. Instead of having top-level layer groups for each image, they now become an artboard. Sublevel folders and assets are kept neatly nested below the Artboard layer. Business as usual really.

Let’s see the biggest advantage. Here’s what you see with layers when working in a traditional Photoshop workspace:

<figure><img title="Workspace with layers" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ecfc73e1-0f33-4623-8b52-774eee6a5495/projectlayers-500px-opt.jpg" alt="Workspace with layers" /><br>
<figcaption>Workspace with layers.</figcaption></figure>

And here’s what you get when working with artboards:

<figure><img title="Workspace with artboards" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a40911d-a30d-437d-8779-326474b173a9/projectartboards-500px-opt.jpg" alt="Workspace with artboards" /><br>
<figcaption>Workspace with artboards.</figcaption></figure>

As you can see from the traditional layer setup, you get only one canvas. This allows you to work on only one image at a time, with no easy way to compare with others. To view another image, you must turn off the visibility on all other layer groups and turn on the layer group you want to see. A bit painful, really.

With artboards, you can see the full set of images at once. I have also arranged the images in rows and columns to keep them neat. Much better.

It doesn’t stop there. Let’s see how Generate works on top of this artboard setup.</p>

### Artboards Combined With Generate

As if artboards aren’t great enough already, let’s see them in action with Generate. My previous workflow with layers would be very different at this point. I would either use “Save for Web” if it was just a few layers, or use a script to export the layers I wanted if there were many layers. The difficulty arises when you need three images at different resolutions and with the correct naming to support Retina. Thankfully, Generate solves this for us.

I do need to give a quick shout out to Martin Pitt for his comment on my <a href="https://www.smashingmagazine.com/2015/05/retina-design-in-photoshop/">previous article</a>. He mentioned that you could use Generate on layer comps, which got me thinking: Maybe Generate would work on artboards. To my surprise, it does!

OK, from what we walked through earlier in the article, Generate with the defaults will be the most efficient setup for the multiple images I need. Here is the default layer name I used:

<pre>[ default 100% end/@1x, 200% end/@2x, 300% end/@3x ]</pre>

<figure><img title="Default Generate layer name used to export @1x – @3x" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10fd4f4f-32fb-4a90-b687-8ee4da5c1790/projectgeneratedefault-500px-opt.jpg" alt="Default Generate layer name used to export @1x – @3x" /><br>
<figcaption>Default Generate layer name used to export @1x to @3x.</figcaption></figure>

Generate will automatically create a tidy folder named <code>end</code>. In this folder, the 15 artboards will get outputted to 45 images, all scaled and neatly suffixed. Could you ask for anything better than that? Here are the image assets that are generated:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f74f974-01d7-4c50-acaa-af98778d6687/projectoutputthumbs-large-opt.jpg"><img title="Output images in the 'end' folder" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82d61d3b-1a8c-413a-8e0a-4d36f2cc0f5d/projectoutputthumbs-500px-opt.jpg" alt="Output images in the 'end' folder" /></a><figcaption>Output images in the <code>end</code> folder. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f74f974-01d7-4c50-acaa-af98778d6687/projectoutputthumbs-large-opt.jpg">View large version</a>)</figcaption></figure>

The combined technique of artboards and Generate greatly sped up my workflow with these image assets and kept everything neat and tidy. Working on images as a set and producing Retina assets became much easier.

You might have noticed that I used the comma separator (<code>,</code>). I prefer it to using the plus sign (<code>+</code>) simply to keep my layer names a bit shorter. When working with artboards, you need all the real estate you can get. The last thing you need is a wide Layers panel cluttering up the workspace.</p>

## Wrapping Up

I hope you’ve enjoyed looking at artboards and Generate. Both are great features that are definitely worth a look, and they work well together when you need to export multiple image assets for Retina, as my example should have highlighted. Don’t be shy — give them a try! Thanks for reading.

Say “Hi” <a href="https://twitter.com/MurdochCarpentr">on Twitter</a>, and feel free to comment below.</p>

### Performance Tip

Unfortunately, not everyone has the latest and greatest high-spec machine. For those who don’t, artboards and Generate can be a bit taxing. To save a bit of CPU, you can just turn on Generate when you need to create new image assets.

I use this technique when working on a mobile or desktop page design, because working through extensive layers and groups every time I edit something can get a bit heavy! Again, the menu option is “File” → “Generate” → “Image Assets.” Keep it in mind.</p>

<figure><img title="Menu option to turn Generate on and off" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f2606ae-c00f-4a48-84e0-c36d20968c33/generatemenu-500px-opt.jpg" alt="Generate menu option" /><br>
<figcaption>Menu option to turn Generate on and off.</figcaption></figure>

### Further Resources

*   [Retinize It](https://retinize.it/) “The best Photoshop actions for preparing designs for iOS or optimized for Retina-display websites.”
*   “[Design Resources](https://bjango.com/designresources/),” Bjango
*   [Slicy](https://macrabbit.com/slicy/), MacRabbit “Slice PSDs in a whole new way.”

{{< signature "da, jb, ml, al" >}}


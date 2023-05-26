---
title: 'How To Create A Flat Vector Illustration In Affinity Designer'
slug: flat-vector-illustration-affinity-designer
author: isabel-aracama
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5d031f8-b066-4c3e-bb55-eb8c6fdb0cc9/12-car-with-lines-800w.png
date: 2018-07-11T20:00:02+02:00
summary:
  While this tutorial was kindly sponsored by Serif, the creator of Affinity, we’d like to point out that it is written by an independent design professional who personally enjoys using the software and shares her lessons learned. The author is not affiliated with the product in any way, and the article has been reviewed independently by Serif as well as SmashingMag’s editors.
description:
  As of today, July 11, Affinity Designer is also available for the iPad. This tutorial introduces some of its very user-friendly main tools and features and shows you how you can create a nice flat vector illustration of a Volkswagen Beetle.
categories:
  - Illustrations
  - Graphics
  - Tutorials
disable_ads: true
disable_panels: true
---
<p>(<em>This is a sponsored post</em>.) If you are in the design world, chances are that you’ve already heard about <a href="https://affinity.serif.com/en-gb/designer/">Affinity Designer</a>, a vector graphics editor for Apple’s macOS and Microsoft Windows.</p>

<p>It was July 2015 when Serif Europe launched the amazing software that many designers and illustrators like me are using now as their main tool for professional work. Unlike some other packages, its price is really affordable, there’s no subscription model and, as mentioned already, it’s available for both Macs and PCs.</p>

<p>In this article, I would like to walk you through just some of its <strong>very user-friendly main tools and features</strong> as an introduction to the software and to show you how we can create a nice flat vector illustration of a Volkswagen Beetle. The illustration will scale up to whatever resolution and size needed because no bitmaps will be used.</p>

<p><strong>Note</strong>: <em>As of today, July 11, <a href="https://affinity.serif.com/designer/ipad">Affinity Designer is also available for the iPad</a>. Although the iPad app’s features and functionality almost completely match the desktop version of Affinity Designer, it relies much more on using the touch screen (and the Apple Pencil) and because of that, you may expect to find some differences in the workflows.</em></p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ee149b8-782c-49f4-9f36-3a8d1a5ba33f/finished-beetle.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ee149b8-782c-49f4-9f36-3a8d1a5ba33f/finished-beetle.png" sizes="100vw" caption="Final image that we’ll be creating in this tutorial. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ee149b8-782c-49f4-9f36-3a8d1a5ba33f/finished-beetle.png'>View large version</a>)" alt="Final image that we’ll be creating in this tutorial." >}}

<p>I will also explain some of the <strong>decisions</strong> I take and <strong>methods</strong> I follow as I work. You know the old saying, “All roads lead to Rome”? In this case, many roads will take us where we’d like to get to, but some are better than others.</p>

<p>We will see how to work with the Pen tool to trace the main car outline, how to break curves and segments, how to convert objects into curves, and how to use the wonderful Corner tool. We will also, among other things, learn how to use the Gradient tool, what is a “Smart copy”, how to import a color palette from an image that we can use as a reference for our artwork, how to use masks, and how to create a halftone pattern. Of course, along the way, you will also learn some helpful keyboard shortcuts and commands.</p>

<p><strong>Note:</strong> <em>Affinity Designer has three work environments, referred to as “personas”. By default, Affinity Designer is set to the draw persona. To switch from the draw persona to the pixel persona or to the export persona, you have to click on one of the three icons located in the top-left corner of the main window. You can start working in the draw persona and switch to the pixel persona at any time, when you need to combine vectors and bitmaps.</em></p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee665268-a281-4165-8aff-421cb80ed105/3-personas.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee665268-a281-4165-8aff-421cb80ed105/3-personas.png" width="466" height="222" alt="The three work environments: draw persona (leftmost icon), bitmap persona (middle icon) and export persona (rightmost icon)." /></a><figcaption>The three work environments: draw persona (leftmost icon), bitmap persona (middle icon) and export persona (rightmost icon). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee665268-a281-4165-8aff-421cb80ed105/3-personas.png">View large version</a>)</figcaption></figure>

## Introduction: The Flat Design Era

<p>In recent years, we’ve seen the rise of <a href="https://en.wikipedia.org/wiki/Flat_design">"flat design"</a>, in contrast to what is known as skeuomorphic representation in design.</p>

<p>To put it simply, flat design gets rid of the metaphors that skeuomorphic design uses to communicate with users, and we’ve seen these metaphors in design, especially in user interface design, for years. Apple had some of the best examples of skeuomorphism in its early iOS and app designs, and today it is widely used in many industries, such as music software and video games. With Microsoft’s (with <a href="https://en.wikipedia.org/wiki/Metro_(design_language)">Metro</a>) and later Google’s <a href="https://material.io/guidelines/">material design</a> and Apple’s iOS 7, mobile apps, user interfaces and most systems and OS’ have moved away from skeuomorphism, using it or elements of it as mere enhancements to a new design language (including gradients and shadows). As you can imagine, illustrations on these systems were also affected by the new design currents, and illustrators and designers started creating artwork that would be consistent with the new times and needs. A whole new world of flat icons, flat infographics and flat illustrations opened in front of our eyes.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5db1b06b-fef6-4587-9fc7-4969801f3c58/iphone-home-screen.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5db1b06b-fef6-4587-9fc7-4969801f3c58/iphone-home-screen.png" sizes="100vw" caption="iPhone’s home screen (iOS 6 versus iOS 7). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5db1b06b-fef6-4587-9fc7-4969801f3c58/iphone-home-screen.png'>View large version</a>)" alt="iPhone’s home screen (iOS 6 versus iOS 7)." >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de0b8fed-374c-4cd9-a437-4b2afb182557/01-how-to-create-a-flat-vector-illustration-in-affinity-designe.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de0b8fed-374c-4cd9-a437-4b2afb182557/01-how-to-create-a-flat-vector-illustration-in-affinity-designe.png" sizes="100vw" caption="(<a href='https://dribbble.com/shots/3296825-Holocards/attachments/711099'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de0b8fed-374c-4cd9-a437-4b2afb182557/01-how-to-create-a-flat-vector-illustration-in-affinity-designe.png'>View large version</a>)" alt="" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c51eee35-db64-4981-9dc4-f87ecdb3ccff/02-how-to-create-a-flat-vector-illustration-in-affinity-designe.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c51eee35-db64-4981-9dc4-f87ecdb3ccff/02-how-to-create-a-flat-vector-illustration-in-affinity-designe.png" sizes="100vw" caption="(<a href='https://dribbble.com/shots/2350717-The-second-part'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c51eee35-db64-4981-9dc4-f87ecdb3ccff/02-how-to-create-a-flat-vector-illustration-in-affinity-designe.png'>View large version</a>)" alt="" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f8d4735-0573-48bf-8785-fd5c18d2446d/03-how-to-create-a-flat-vector-illustration-in-affinity-designe.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f8d4735-0573-48bf-8785-fd5c18d2446d/03-how-to-create-a-flat-vector-illustration-in-affinity-designe.png" sizes="100vw" caption="(<a href='https://dribbble.com/shots/1036448-Flat-Design-Icons-Set-Vol1'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f8d4735-0573-48bf-8785-fd5c18d2446d/03-how-to-create-a-flat-vector-illustration-in-affinity-designe.png'>View large version</a>)" alt="" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a2f6aff-9a59-4b78-875a-967c1aa34d08/04-how-to-create-a-flat-vector-illustration-in-affinity-designe.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a2f6aff-9a59-4b78-875a-967c1aa34d08/04-how-to-create-a-flat-vector-illustration-in-affinity-designe.png" sizes="100vw" caption="(<a href='https://dribbble.com/shots/2495305-Infographic/attachments/490101'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a2f6aff-9a59-4b78-875a-967c1aa34d08/04-how-to-create-a-flat-vector-illustration-in-affinity-designe.png'>View large version</a>)" alt="" >}}

## Let’s Draw A Flat Illustration!

<p>I am providing the source file for this work over <a href="https://smashingmagazine.com/provide/IsabelAracama_Beetle_source-file.zip">here</a>, so you can use it to explore it and to better follow along as we design it. If you do not yet have a copy of Affinity Designer, you can <a href="https://affinity.serif.com/en-gb/signup/trial/designer/">download a trial</a>.</p>

### 1. Canvas Settings

<p>Open Affinity Designer, and create a new document by clicking <kbd>Cmd</kbd> + <kbd>N</kbd> (Mac) or <kbd>Ctrl</kbd> + <kbd>N</kbd> (Windows). Alternatively, you can go to “Menu” &rarr; “File” &rarr; “New”. Be sure not to check the “Create Artboard” box.</p>

<p>Set the type to “Web”, which will automatically set the field DPI to 72. It should be understood now as PPI, but we won’t dive into the details here. If you want to learn more on the topic, check the following two resources:</p>

<ul>
<li>“<a href="https://forum.affinity.serif.com/index.php?/topic/25774-its-ppi-not-dpi/">
It’s PPI not DPI</a>,” Forums, Affinity</li>

<li>“<a href="https://en.99designs.es/blog/tips/ppi-vs-dpi-whats-the-difference/">PPI vs. DPI: What’s the Difference?</a>,” Alex Bigman, 99designs</li>
</ul>

<p>Also, remember that you can change this setting at any time. The vectors’ quality won’t be affected by scaling them.</p>

<p>Set the size to 2000 &#215; 1300 pixels, and click “OK”.</p>

<p>Our white canvas is now set, but before we start, I’d suggest you first save this file and give it a name. So, go to “File” &rarr; “Save”, and name it “Beetle”.</p>

### 2. Importing A Color Palette From An Image

<p>One of the things I use a lot in Affinity Designer is its ability to <strong>import the colors</strong> contained in an image and creating a palette from them.</p>

<p>Let’s see how this is done.</p>

<p>For the illustration I want to draw, I thought of warm colors, like in a sunset, so I searched Google with this query: “warm colors yellows oranges reds palette”. From all the images it found, I chose one that I liked and copied it into Affinity Designer in my recently created canvas. (You can copy and paste the image to the canvas directly from the browser.)</p>

<p>If the Swatches panel isn’t open yet, use menu “View” &rarr; “Studio” &rarr; “Swatches”. Click the menu in the top-right corner of the panel, and select the option “Create Palette From Document”, and then click on “As Document Palette”. Click “OK” and you’ll see the colors contained in the image form a new palette in the Swatches panel. The default name for it will be “Palette” if you still haven’t saved your file with a name. In case you have, the name of this palette will be the same as your document, but if you want to rename it, simply go to the menu on the right in the Swatches panel again and select the option “Rename Palette”.</p>

<p>I will call it “Beetle Palette”.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/586785ca-7203-45ff-907c-b0a3302cc670/01-doc-palette.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/586785ca-7203-45ff-907c-b0a3302cc670/01-doc-palette.png" sizes="100vw" caption="Creating a palette from an image. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/586785ca-7203-45ff-907c-b0a3302cc670/01-doc-palette.png'>View large version</a>)" alt="Creating a palette from an image." >}}

<p>We can now get rid of that reference image, or simply hide it in the Layers panel. We will be using this palette as a guide to create our artwork with harmonious colors.</p>

<p><strong>Interface:</strong> Before we continue, I will present a quick overview of the main sections of the user interface in Affinity Designer, and the names of some of the most used tools.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfe876e7-8485-4ff6-b88e-5c5087d1dc6b/main-parts-ui.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfe876e7-8485-4ff6-b88e-5c5087d1dc6b/main-parts-ui.png" sizes="100vw" caption="Main areas of the UI in Affinity Designer when using the draw persona. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6797bca1-d782-447c-b84a-2b81483a5e12/05-how-to-create-a-flat-vector-illustration-in-affinity-designe.png'>View large version</a>)" alt="Main areas of the UI in Affinity Designer when using the draw persona." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f6a1f3a-4bec-4e39-9599-a2e151eb32cd/tools-tooltips-draw-persona.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f6a1f3a-4bec-4e39-9599-a2e151eb32cd/tools-tooltips-draw-persona.png" sizes="100vw" caption="Tools for the (default) draw persona in Affinity Designer. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f6a1f3a-4bec-4e39-9599-a2e151eb32cd/tools-tooltips-draw-persona.png'>View large version</a>)" alt="Tools for the (default) draw persona in Affinity Designer." >}}

### 3. Creating The Background With The Gradient Tool

<p>The next thing is to create a background. For this, go to the tools displayed on the left side, and select the Rectangle tool. Drag it along the canvas, making sure to give it an initial random fill color so that you can see it. The fill color chip is located in the top toolbar.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/116a8b28-97b7-4020-8cbb-62a6da16474b/02-background-color.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/116a8b28-97b7-4020-8cbb-62a6da16474b/02-background-color.png" sizes="100vw" caption="Click the Rectangle tool and drag it along the canvas. Fill it with a random color. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/116a8b28-97b7-4020-8cbb-62a6da16474b/02-background-color.png'>View large version</a>)" alt="Click the Rectangle tool and drag it along the canvas. Fill it with a random color." >}}

<p>Next, select the Fill tool (the color wheel icon, or press <kbd>G</kbd> on the keyboard), and in the top Context toolbar, select the type: “Linear”.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/955fcebc-41c6-4bdd-9d6e-ad48ccf3521e/03-linear-gradient.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/955fcebc-41c6-4bdd-9d6e-ad48ccf3521e/03-linear-gradient.png" sizes="100vw" caption="Select “Linear” from the Fill tool’s contextual menu. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/955fcebc-41c6-4bdd-9d6e-ad48ccf3521e/03-linear-gradient.png'>View large version</a>)" alt="Select “Linear” from the Fill tool’s contextual menu." >}}

<p>We have several options here: “None” removes the fill color, “Solid” applies one solid color, and all of the rest are different types of gradients.</p>

<p>To straighten the gradient and make it vertical, place your cursor over one of the ends and pull. When you are near the vertical line, press <kbd>Shift</kbd>: This will make it perfectly vertical and perpendicular to the base of the canvas.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcbf8dd4-c4a6-48a9-b544-df83b27721cc/gradient-shift.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcbf8dd4-c4a6-48a9-b544-df83b27721cc/gradient-shift.gif" width="800" height="500" alt="To straighten a linear gradient, pull from one end, and then press the Shift key to make it perfectly vertical." /></a><figcaption>To straighten a linear gradient, pull from one end, and then press the Shift key to make it perfectly vertical. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcbf8dd4-c4a6-48a9-b544-df83b27721cc/gradient-shift.gif">View large version</a>)</figcaption></figure>

<p>Next, in the Context toolbar, click on the color chip, and you’ll see a dialog that corresponds exactly with the gradient we just applied. Click now on the color chip, and an additional dialog will open.</p>

<p>In the combo, click on the “Color” tab, and then select “RGB Hex Sliders”; in the field marked with a <strong>#</strong>, input the value: <code>FE8876</code>. Press “OK”. You’ll see now how the gradient has been updated to the new color. Repeat this action with the other color stop in the gradient dialog, and input this value: <code>E1C372</code>.</p>

<p>You should now have something like this:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cac8348c-a33d-454e-896d-3b8454ce646e/05-gradient-finished.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cac8348c-a33d-454e-896d-3b8454ce646e/05-gradient-finished.png" sizes="100vw" caption="Setting gradient colors (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cac8348c-a33d-454e-896d-3b8454ce646e/05-gradient-finished.png'>View large version</a>)" alt="Setting gradient colors." >}}

<p>Let’s go to the Layers panel and rename the layer to “Background”. Double-click on it to rename it, and then lock it (by clicking on the little lock icon in the top-right corner).</p>

### 4. Drawing The Car Outline With The Pen Tool

<p>The next thing we need to do is look for an image that will serve as our reference to draw the outline of the car. I searched Google for “Volkswagen Beetle side view”. From the images I found, I selected one of a green Beetle and copied and pasted it into my document. (Remember to lock the layer with the reference image, so that it doesn’t move accidentally.)</p>

<p>Next, in the side toolbar, select the Pen tool (or press <kbd>P</kbd>), zoom in a bit so that you can work more comfortably, and start tracing a segment, following the outline of the car in the picture. Give the stroke an 8-pixel width in the Stroke panel.</p>

<p><strong>Note:</strong> <em>You won’t need to create a layer, because the segments you trace will be automatically placed on top of the image.</em></p>

<p>The Pen tool is one of the most daunting tools for beginners, and it is obviously one of the most important tools to learn in vector graphics. While practice is needed to reach perfection, it is also a matter of understanding some simple actions that will help you use the tool better. Let’s dive into the details!</p>

<p>As you trace with the Pen tool in Affinity Designer, you will see <strong>two types</strong> of nodes: <strong>squared</strong> nodes appear first, and as you pull the handles, they will turn into <strong>rounded</strong> nodes.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/569aec2b-7231-407c-9415-84b5e00748fb/06-nodes-handlers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/569aec2b-7231-407c-9415-84b5e00748fb/06-nodes-handlers.png" sizes="100vw" caption="Sharp, smooth nodes and handles on a path segment (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/569aec2b-7231-407c-9415-84b5e00748fb/06-nodes-handlers.png'>View large version</a>)" alt="Sharp, smooth nodes and handles on a path segment" >}}

<p>Affinity Designer comes with several pen modes, but we will only be using the default one, called “Pen Mode”, and as we trace the car, we will get rid of one of the handles by clicking <kbd>Alt</kbd> in such a way that the next section of the segment to be traced will be independent of the previous one, even if connected to it.</p>

<p>Here’s how to proceed. Select the Pen tool, click once, move some distance away, click a second time (a straight line will be created between nodes 1 and 2), drag the second node (this will create a curve), <kbd>Alt</kbd>-click the node to <strong>remove</strong> the second control handle, then proceed with node 3, and so on.</p>

<p>An alternative way would be to select the Pen tool, click once, move some distance away, click a second time (a straight line will be created between nodes 1 and 2), drag the second node (this will create a curve), then, without moving the mouse, <kbd>Alt</kbd>-click the second handle’s point to remove this handle, then proceed with node 3, and so on.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6800cf00-0f55-4ad4-86f5-67a73bf9649e/pen-tool.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6800cf00-0f55-4ad4-86f5-67a73bf9649e/pen-tool.gif" width="600" height="375" alt="Trace the outline of the car and get rid of the handles we don’t need by Alt-clicking." /></a><figcaption>Trace the outline of the car and get rid of the handles we don’t need by Alt-clicking. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6800cf00-0f55-4ad4-86f5-67a73bf9649e/pen-tool.gif">View large version</a>)</figcaption></figure>

<p><strong>Note:</strong> <em>Don’ be afraid to trace segments that are not perfect. With time, you’ll get a better grip of the Pen tool. For now, it’s not very important that each node and line looks as we want it to look in the end. In fact, Affinity Designer makes it really easy to amend segments and nodes, so tracing a rough line to start is just fine. For more insight on how to easily use the Pen tool (for beginners), check out Isabel Aracama’s <a href="https://www.youtube.com/watch?v=BSomsJpKDaw">video tutorial</a>.</em></p>

### 5. Resculpting Segments And Using The Corner Tool

<p>What we need now is to make all of those rough lines look smooth and curvy. First, we will pull the straight segments to smoothen them, and then we will improve them using the Corner tool.</p>

<p>Click the Node tool in the side toolbar, or select it by pressing <kbd>A</kbd> on your keyboard. Now, start pulling segments to follow the lines of your reference picture. You can also use the handles to help make the line take the shape you need by moving and pulling them accordingly. Just do it in such a way that it all fits the reference image, but don’t bother much if it’s not yet perfect. With the Node tool (A), you can both <strong>select and move nodes</strong>, but you can also click and drag the curves themselves to change them.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72b9eccb-ae02-4972-9269-95bdbc9ca91c/amend-segments.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72b9eccb-ae02-4972-9269-95bdbc9ca91c/amend-segments.gif" width="600" height="375" alt="Resculpt and correct segments with the Node tool A." /></a><figcaption>Resculpt and correct segments with the Node tool (<kbd>A</kbd>). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72b9eccb-ae02-4972-9269-95bdbc9ca91c/amend-segments.gif">View large version</a>)</figcaption></figure>

<p>Once all of the segments are where we need them, we are going to smoothen their corners using the Corner tool (shortcut: <kbd>C</kbd>). This is one of my favorite tools in Affinity Designer. The live Corner tool allows you to adjust your nodes and segments to perfection. Select it by pressing <kbd>C</kbd>, or select it from the Tools sidebar. The method is pretty simple: Pass the corner tool over the sharp nodes (squared nodes) that you want to smoothen. If you need to, switch back to the Node tool (<kbd>A</kbd>) to adjust a section of a segment by pulling it or its handles. (Smooth nodes (rounded nodes) don’t allow for more softening, and they will display a smaller circle the moment you select the Corner tool.)</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45e25645-d195-487d-8bd9-620d4f7c9464/07-corner-tool-icon.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45e25645-d195-487d-8bd9-620d4f7c9464/07-corner-tool-icon.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45e25645-d195-487d-8bd9-620d4f7c9464/07-corner-tool-icon.png'>View large version</a>" alt="" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c31db59-cf3a-4621-b352-82e2f37b660d/08-nodes-corner.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c31db59-cf3a-4621-b352-82e2f37b660d/08-nodes-corner.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c31db59-cf3a-4621-b352-82e2f37b660d/08-nodes-corner.png'>View large version</a>" alt="" >}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9046c1a0-9b9e-4efd-8af6-7d41cffb3d62/corner-tool.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9046c1a0-9b9e-4efd-8af6-7d41cffb3d62/corner-tool.gif" width="800" height="500" alt="Use the Corner tool on sharp nodes to smoothen the lines." /></a><figcaption>Use the Corner tool on sharp nodes to smoothen the lines. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9046c1a0-9b9e-4efd-8af6-7d41cffb3d62/corner-tool.gif">View large version</a>)</figcaption></figure>

<p>Once our corners and segments look good, we’ll want to fill the shape and change the color of the stroke. Select the closed curve line that we just created for the car, click on the fill color chip, and in the HEX color field input <code>FFCF23</code>. Click on the stroke color chip beside it and input <code>131000</code>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fdb970e-8cdb-4e34-a58f-92471f4d5064/09-fill-and-stroke.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fdb970e-8cdb-4e34-a58f-92471f4d5064/09-fill-and-stroke.png" sizes="100vw" caption="This is what you should have after applying the fill color and stroke color. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fdb970e-8cdb-4e34-a58f-92471f4d5064/09-fill-and-stroke.png'>View large version</a>)" alt="This is what you should have after applying the fill color and stroke color." >}}

<p>Create now a shape with the Pen tool, and fill it with black (<code>000000</code>). Place it behind the car’s bodywork (the yellow shape). The exact shape of the new object that you will create does not really matter, except that its bottom side needs to be straight, as in the image below. Place it behind the main bodywork (the yellow shape) via either the Layers panel or through the menu “Arrange” &rarr; “Back One”.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ac8fd84-9de9-4910-886d-83f05d102eb5/10-black-behind.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ac8fd84-9de9-4910-886d-83f05d102eb5/10-black-behind.png" sizes="100vw" caption="Black shape behind the car bodywork (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ac8fd84-9de9-4910-886d-83f05d102eb5/10-black-behind.png'>View large version</a>)" alt="Black shape behind the car bodywork." >}}

### 6. Creating The Wheels Using Smart Copy

<p>We need to put the wheels in place next. In the Tools, pick the Ellipse tool, and drag over the canvas, creating a circle the same size as the wheel in the reference picture. Click <kbd>Shift</kbd> as you drag to make the circle proportionate. Additionally, holding <kbd>Ctrl</kbd> (Windows) or <kbd>Cmd</kbd> (Mac), you can create a perfect circle <strong>from the center out</strong>.</p>

<p><strong>Note:</strong> <em>If you need to, hide the layers created thus far to see better, or simply reduce their opacity temporarily. You can change the opacity by selecting any shape and pressing a number on the keyboard, from 1 to 9, where 1 will apply a 10% opacity and 9 a 90% opacity value. To reset the opacity to 100%, press 0 (zero).</em></p>

<p>Choose a random color that contrasts with the rest. I like to do so initially just so that I can see the shapes well contrasted and differentiated. When I am happy with them, I apply the final color. Set the opacity to 50% (click <kbd>5</kbd> on the keyboard) to be able to see through as you draw it.</p>

<p>Zoom into your wheel shape. Press <kbd>Z</kbd> to select the Zoom tool, and drag over the shape while holding <kbd>Alt</kbd> key, or double-click on the thumbnail corresponding to it in the Layers panel. (It doesn’t need to be previously selected, although this will help you to visually locate it in the Layers panel.)</p>

<p>We will now learn how to use Smart copy, and we will paste some concentric circles.</p>

<p>Select the circle and press <kbd>Cmd</kbd> + <kbd>J</kbd> (Mac) or <kbd>Ctrl</kbd> + <kbd>J</kbd> (Windows). A new circle will be placed on top of the original one. Select it. This command is found under “Edit” &rarr; “Duplicate”, and it’s also known as Smart copy or Smart duplicate.</p>

<p>Click <kbd>Shift</kbd> + <kbd>Cmd</kbd> (Mac) or <kbd>Shift</kbd> + <kbd>Ctrl</kbd> (Windows), and drag in to transform it into a smaller concentrical circle. Repeat three times, reducing a bit more in size each time, to fit your reference. Smart duplicating a shape by pressing <kbd>Shift</kbd> + <kbd>Cmd</kbd> (Mac) or <kbd>Shift</kbd> + <kbd>Ctrl</kbd> (Windows) will make the shape transform in a relative way. This will happen from your third smart-duplicated shape onwards.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bbecb15-e054-4076-9a17-565f87261204/smart-copy.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bbecb15-e054-4076-9a17-565f87261204/smart-copy.gif" width="" height="" alt="smart copy via keyboard shortcuts" /></a><figcaption>Smart copy via <kbd>Cmd</kbd> + <kbd>J</kbd> or <kbd>Ctrl</kbd> + <kbd>J</kbd>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bbecb15-e054-4076-9a17-565f87261204/smart-copy.gif">View large version</a>)</figcaption></figure>

<p>So, we have our concentric circles for the wheel, and now we have to change the colors. Go to the Swatches panel, and in the previously created palette, choose colors that work well with the yellow that we have applied to the car’s bodywork. You can select a color and modify it slightly to adapt to what you think works best. We need to apply fill and stroke colors. Remember to give the stroke the same width as the rest of the car (8 pixels) except for the innermost circle, where we will apply a stroke of 11.5 pixels. Also, remember to put back to 100% the opacity of each concentric circle.</p>

<p>I chose these colors, from the outer to inner circles: <code>5D5100</code>, <code>918A00</code>, <code>CFA204</code>, <code>E5DEAB</code>.</p>

<p>Now we want to select and group all of them together. Select them all and press <kbd>Cmd</kbd> + <kbd>G</kbd> (Mac) or <kbd>Ctrl</kbd> + <kbd>G</kbd> (Windows). Name the new group “Front Wheel” in the Layers panel. Duplicate this group and, while pressing <kbd>Shift</kbd>, select it and drag along the canvas until it overlaps with the back wheel. Name the layer accordingly.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9299d0ce-08c4-403d-82b3-4632a77dc7be/11-wheels.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9299d0ce-08c4-403d-82b3-4632a77dc7be/11-wheels.png" sizes="100vw" caption="The car should look similar to this now. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9299d0ce-08c4-403d-82b3-4632a77dc7be/11-wheels.png'>View large version</a>)" alt="The car should look similar to this now." >}}

### 7. Breaking Curves And Clipping Masks To Draw The Inner Lines Of The Car’s Bodywork

<p>To keep working, either hide all layers or bring down the opacity so that they don’t get in your way. We need to trace the front and back fenders. We have to do the same as what we did for the main bodywork. Pick the Pen tool and trace an outline over it.</p>

<p>Once it is traced, modify it by using the handles, nodes and Corner tool. I also modified the black shape behind the car a bit, so that it shows a bit more in the lower part of the body work.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/448978d1-df3a-4426-bae4-d43a0d33eb35/car-fenders.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/448978d1-df3a-4426-bae4-d43a0d33eb35/car-fenders.png" sizes="100vw" caption="Fenders added to the car. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/448978d1-df3a-4426-bae4-d43a0d33eb35/car-fenders.png'>View large version</a>)" alt="Fenders added to the car." >}}

<p>Now we want to trace some of the inner lines that define the car. For this, we will duplicate the main yellow shape, remove its fill color and place it onto our illustration in the canvas.</p>

<p>Press <kbd>A</kbd> on the keyboard, and click on any of the bottom nodes of the segment. In the top Context toolbar, click on “Action” &rarr; “Break Curve”. You will see now that the selected node has turned into a red-outlined squared node. Click on it and pull anywhere. As you can see, the segment is now <strong>open</strong>. Click the <kbd>Delete</kbd> or <kbd>Backspace</kbd> key (Windows) or the <kbd>Delete</kbd> key (Mac), and do the same with all of the bottom nodes, leaving just the leftmost and rightmost ones, and also being very careful that what is left of the top section of the segment is not deformed at all.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d80949f2-23c6-42df-9674-b3c5610b1a61/inner-lines-bodywork.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d80949f2-23c6-42df-9674-b3c5610b1a61/inner-lines-bodywork.gif" width="600" height="375" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d80949f2-23c6-42df-9674-b3c5610b1a61/inner-lines-bodywork.gif">View large version</a>)</figcaption></figure>

<p>I use this method for one main reason: Duplicating an existing line allows for a more consistent look and for more harmonious lines.</p>

<p>Select now the newly opened curve, and make it smaller in such a way that it fits into the main yellow shape when you place them on top of one another. In the Layers panel, drag this curve into the yellow shape layer to create a <strong>clipping mask</strong>. The reason for creating a clipping mask is simple: We want an object inside another object so that they do not overlap (i.e. both objects are visible), but one nested inside the other. Not doing so would result in some bits of the nested object being visible, which is not what we want; we need perfect, clean-cut lines.</p>

<p><strong>Note:</strong> <em>Clipping masks are not to be mistaken for <strong>masks</strong>. You will know you’re clipping and not masking because of the thumbnail (masks show a crop-like icon when applied) and because when you are about to clip, a <strong>blue stripe is displayed horizontally</strong>, a bit more than halfway across the layer. Masks, on the other hand, display a <strong>small vertical</strong> blue stripe beside the thumbnail.</em></p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/653633d3-eade-476d-b95c-f819348cef62/clippin-vs-masking.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/653633d3-eade-476d-b95c-f819348cef62/clippin-vs-masking.png" sizes="100vw" caption="Clipping versus masking in Affinity Designer (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/653633d3-eade-476d-b95c-f819348cef62/clippin-vs-masking.png'>View large version</a>)" alt="Clipping versus masking in Affinity Designer" >}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44920dea-1158-4347-828c-f03cd1915b8b/clipping.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44920dea-1158-4347-828c-f03cd1915b8b/clipping.gif" width="600" height="375" alt="Clipping mask once it is applied" /></a><figcaption>Clipping mask once it is applied (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44920dea-1158-4347-828c-f03cd1915b8b/clipping.gif">View large version</a>)</figcaption></figure>

<p>Now that we have applied our clipping mask to insert the newly created segment inside the main shape of the car, I’ve broken some nodes and moved some others around a bit in order to place them exactly how I want. I’ve stretched the width a bit, and separated the front from the rest of the segment using exactly the same methods we’ve already seen. Then, I applied a bit more Corner tool to soften whatever I felt needed to be softened. Finally, with the Pen tool, I added some extra nodes and segments to create the rest of the inner lines that define the car.</p>

<p><strong>Note:</strong> <em>In order to select an object in a mask, a clipping mask or a group when not selecting the object directly in the Layers panel, you have to double-click until you select the object, or hold <kbd>Ctrl</kbd> (Windows) or <kbd>Cmd</kbd> (Mac) and click.</em></p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99fb6b96-3c61-48da-8dfa-26c45f5d88bb/adding-lines.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99fb6b96-3c61-48da-8dfa-26c45f5d88bb/adding-lines.gif" width="600" height="375" alt="Adding extra lines to a segment." /></a><figcaption>Adding extra lines to a segment (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99fb6b96-3c61-48da-8dfa-26c45f5d88bb/adding-lines.gif">View large version</a>)</figcaption></figure>

<p>After some amendments and tweaking using the mentioned methods, our car looks like this:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca4743e0-d5b3-4a49-b046-7ccdcb5a3921/12-car-with-lines.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca4743e0-d5b3-4a49-b046-7ccdcb5a3921/12-car-with-lines.png" sizes="100vw" caption="How the car looks after a little tweaking of the segments and nodes (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca4743e0-d5b3-4a49-b046-7ccdcb5a3921/12-car-with-lines.png'>View large version</a>)" alt="How the car looks after a little tweaking of the segments and nodes" >}}

### 8. Drawing The Windows Using Some Primitive Shapes

<p>In the side Toolbar, select the Rounded Rectangle tool. Drag on the canvas to create a shape. The size of the shape should fit in the car’s bodywork and look proportionate. No matter how you create it, you will be able to resize it later, so don’t worry much.</p>

<p><strong>Note:</strong> <em>When you create a shape with strokes and resize it, be sure to check “Scale with object” in the Stroke panel if you want the <strong>stroke to scale in proportion with the object</strong>. I recommend that you visually compare the difference between having this option checked and unchecked when you need to resize an object with a stroke.</em></p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df546f95-2056-41db-a67f-cfebc797abc0/scale-with-object.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df546f95-2056-41db-a67f-cfebc797abc0/scale-with-object.png" sizes="100vw" caption="Make sure this is checked if you plan to resize your artwork, so that it scales the strokes accordingly. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df546f95-2056-41db-a67f-cfebc797abc0/scale-with-object.png'>View large version</a>)" alt="Make sure this is checked if you plan to resize your artwork, so that it scales the strokes accordingly." >}}

<p>Once you have placed your rounded rectangle on the canvas, fill it with a blue-ish colour. I’ve used <code>#93BBC1</code>. Next, select it with the Node tool (press <kbd>A</kbd>). You will now see a little orange circle in the top-left corner. If you pull outwards or inwards, you’ll see how the angle in that corner changes. In the top Context toolbar, you can uncheck “Single radius”, and apply the angle you want to each corner of the rectangle individually. <strong>Uncheck it</strong>, and pull inwards on the tiny orange circle in the top-left corner. If you pull, you will be able to round it to a certain percentage, but you can also input the desired value in the input field for it, or even use the slider it comes with (it will show whether you’ve clicked on the little chevron). Let’s apply a value of 100%.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6a364f5-a232-4292-b281-eeb4969bd7d0/rounded-rectangle1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6a364f5-a232-4292-b281-eeb4969bd7d0/rounded-rectangle1.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6a364f5-a232-4292-b281-eeb4969bd7d0/rounded-rectangle1.png'>View large version</a>" alt="" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb5eefc4-2cc8-43bb-9cca-b6c9122b4806/rounded-rectangle2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb5eefc4-2cc8-43bb-9cca-b6c9122b4806/rounded-rectangle2.png" sizes="100vw" caption="How the rounded rectangle primitive shape looks in default mode and how it changes when we uncheck the single radius box. Now we can manipulate the corners individually. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb5eefc4-2cc8-43bb-9cca-b6c9122b4806/rounded-rectangle2.png'>View large version</a>)" alt="How the rounded rectangle primitive shape looks in default mode and how it changes when we uncheck the single radius box. Now we can manipulate the corners individually." >}}

<p>Primitive shapes are not so flexible in terms of vector manipulation (compared to curves and lines), so, in order to apply further changes to such a shape (beyond fill, stroke, corners, width and height), we will need to convert it to curves.</p>

<p><strong>Note:</strong> <em>Once you convert a primitive shape into curves, there is no way to go back, and there will be no option to manipulate the shape through the little orange stops. If you need further tweaking, you will need to do it with the Corner tool.</em></p>

<p>Select the rectangle with the Node tool (<kbd>A</kbd>), and in the top Context toolbar, click the button “Convert to Curves”. The bounding box will disappear, and all of the nodes forming the shape will be shown. Also, note how in the Layers panel, the name of the object changes from “Rounded Rectangle” to “Curve”.</p>

<p>Now you need to manipulate the shape in order to create an object that looks like a car window. Look at the reference picture to get a better idea of how it should look. Also, tweak the rest of the drawn lines in the car, so that it all fits together nicely. Don’t worry if the shapes don’t look perfect (yet). Getting them right is a matter of practice! Using the Pen tool, help yourself with the <kbd>Alt</kbd> and <kbd>Shift</kbd> keys and observe how differently the segment nodes behave. After you have created the front window, go ahead and create the back one, following the same method.</p>

<p>We also need to create the reflections of the window, which we’ll do by drawing three rectangles, filling them with white color, overlapping them with a bit of offset from one another, and setting the opacity to 50%.</p>

<p>Place the cursor over the top bounding-box white circle, and when it turns into a curved arrow with two ends, move it to give the rectangles an angle. Create a clipping mask, dragging it over the window shape in the Layers panel as we saw before. You can also do this by following the following alternative methods:</p>

<ul>
<li>Under the menu “Layer” &rarr; “Insertion” &rarr; “Insert Inside” the selected window object.</li>

<li>With the keyboard shortcut <kbd>Ctrl</kbd> + <kbd>X</kbd> (Windows) and <kbd>Cmd</kbd> + <kbd>X</kbd> (Mac), select your window object &rarr; “Edit” &rarr; “Paste Inside” (<kbd>Ctrl</kbd>/<kbd>Cmd</kbd> + <kbd>Alt</kbd> + <kbd>V</kbd>).</li>
</ul>

<p>Repeat this for the back window. To add visual interest, you can duplicate the reflections and slightly change the rectangles’ opacities and widths.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a03b711e-7e0e-4a71-9738-fd0c723395ac/window-reflections.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a03b711e-7e0e-4a71-9738-fd0c723395ac/window-reflections.gif" width="600" height="375" alt="Create the reflections on the windows, and clip them inside." /></a><figcaption>Create the reflections on the windows, and clip them inside. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a03b711e-7e0e-4a71-9738-fd0c723395ac/window-reflections.gif">View large version</a>)</figcaption></figure>

### 9. Adding Visual Interest: Halftone Pattern, Shadows And Reflections

<p>Before we start with the shadows and reflections, we need to add an extra piece onto the car so that all of the elements look well integrated. Let’s create the piece that sits below the doors. It is a simple rectangle. Place it on the corresponding layer order, so that it looks like the picture below, and keep inserting all of the pieces together so that it looks compact. I will also move a bit the front fender to make the front shorter.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c642e4c2-3151-4ce6-97f5-cb30ed750c73/13-car-integratedpieces.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c642e4c2-3151-4ce6-97f5-cb30ed750c73/13-car-integratedpieces.png" sizes="100vw" caption="The car, once the final bodywork pieces have been placed and tweaks made. We’re getting there! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c642e4c2-3151-4ce6-97f5-cb30ed750c73/13-car-integratedpieces.png'>View large version</a>)" alt="The car, once the final bodywork pieces have been placed and tweaks made. We’re getting there!" >}}

<p>Now let’s create the <strong>halftone pattern</strong>.</p>

<p>Grab the Pen tool (<kbd>P</kbd>) and trace a line on your canvas. In the Stroke panel (you can also do this in the Pen tool’s Context toolbar section for the stroke, at the top), set the size to something like 7 pixels. We can easily change this value later if needed. Select the “Dash” line style, and the rest of the dialog settings should be as follows:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f533a815-efab-471a-92f7-8acf7479c311/halftone.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f533a815-efab-471a-92f7-8acf7479c311/halftone.png" sizes="100vw" caption="Settings for the first part of creating the halftone pattern. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f533a815-efab-471a-92f7-8acf7479c311/halftone.png'>View large version</a>)" alt="Settings for the first part of creating the halftone pattern." >}}

<p>Now, duplicate this line, and place the new one below with a bit of an offset to the left.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61ec4877-437c-4eed-85cf-290517aa0d73/halftone2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61ec4877-437c-4eed-85cf-290517aa0d73/halftone2.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61ec4877-437c-4eed-85cf-290517aa0d73/halftone2.png'>View large version</a>" alt="" >}}

<p>Group both lines, duplicate this group with a Smart copy, and create something like this:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1171ae0-b7ae-4fd5-b6f6-e6f5cc91cfc6/smartcopyhalftone.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1171ae0-b7ae-4fd5-b6f6-e6f5cc91cfc6/smartcopyhalftone.png" sizes="100vw" caption="Smart copy the first two lines, and create the whole pattern. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1171ae0-b7ae-4fd5-b6f6-e6f5cc91cfc6/smartcopyhalftone.png'>View large version</a>)" alt="Smart copy the first two lines, and create the whole pattern." >}}

<p>When you drag a selection in Affinity Designer, only objects that are completely within the selection area will be selected. If you want to select all objects without having to drag over all of them completely, you have the following options:</p>

<ul>
<li>Mac: Holding the <kbd>⌃</kbd> (<kbd>Ctrl</kbd>) key will allow you to select all objects touching the selection marquee as you draw it.</li>

<li>Windows: Click and hold the left mouse button, start dragging a selection, and then click and hold the right mouse button as well. As you are holding both buttons, all objects touching the selection marquee will be selected.</li>

<li>Alternatively, you can make this behavior a global preference. On Mac, go to “Affinity Designer” &rarr; “Preferences” &rarr; “Tools”, and check “Select object when intersects with selection marquee”. On Windows, go to “Edit” &rarr; “Preferences” &rarr; “Tools”, and check “Select object when intersects with selection marquee”.</li>
</ul>

<p>To make the illustration more interesting, we are going to vary the beginning and end of some of the lines a bit. To do this, we select the Node tool (<kbd>A</kbd>), and move the nodes a bit inwards.</p>

<p>It should now look like this:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36b055bf-4ce2-44ad-9191-52aaecf8bf5a/halftone3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36b055bf-4ce2-44ad-9191-52aaecf8bf5a/halftone3.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36b055bf-4ce2-44ad-9191-52aaecf8bf5a/halftone3.png'>View large version</a>" alt="" >}}

<p>To apply the pattern to our design, make sure everything is grouped, copy and paste it into our car artwork, reduce its opacity to 30%, and also reduce the size (making sure “Scale with object” is checked in the Stroke panel). We will then create a clipping mask. It is important to keep consistency in the angle, color and size of this pattern throughout the illustration.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe5e7630-8f70-4167-a6ce-9b51f384d49f/halftonemask.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe5e7630-8f70-4167-a6ce-9b51f384d49f/halftonemask.gif" width="600" height="375" alt="Applying the halftone mask." /></a><figcaption>Applying the halftone mask (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe5e7630-8f70-4167-a6ce-9b51f384d49f/halftonemask.gif">View large version</a>)</figcaption></figure>

<p>Now, apply the halftone pattern to the back fender and to the car’s side; make sure to create a placeholder for it first, be it the fender itself or a new shape. Make some tweaks if you need to adapt the pattern to your drawing in a harmonious way. You can change the overall size, the dots’ size, the transparency, the angle and so on, but try to be consistent when applying these changes to the pattern bits.</p>

<p>For the shadow below the windows, I drew a curve to be the placeholder, and applied the color <code>#CFA204</code> so that it looks darker.</p>

### 10. Creating The Remaining Elements Of The Car

<p>Now, it’s all about creating the rest of the elements that make up the car: the bumpers, the back wheel and the surf board, plus the design stickers.</p>

- **The front and back lights**  
For the front light, switch to the Segment tool and draw the shape. Then we need to rotate it a bit and place it somewhere below the car’s main bodywork. The same can be done for the back light but using the Rectangle tool. The colors are `#FFDA9D` for the front light and `#FF0031` for the back light.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6867a304-9fa6-48cc-93e8-64559e8756c6/frontlight.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6867a304-9fa6-48cc-93e8-64559e8756c6/frontlight.gif" width="600" height="375" alt="Creating the front light" /></a><figcaption>Creating the front light (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6867a304-9fa6-48cc-93e8-64559e8756c6/frontlight.gif">View large version</a>)</figcaption></figure>

- **Surfboard**  
To create the surfboard, we will use the Ellipse tool and draw a long ellipse. Convert it to curves and pull up the lower segment, adjusting a bit the handles to give it the ideal shape.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de3e0e4d-35b0-47c5-af72-1239cfb3253b/surfboard.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de3e0e4d-35b0-47c5-af72-1239cfb3253b/surfboard.gif" width="600" height="375" alt="Creating the surf board" /></a><figcaption>Creating the surf board (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de3e0e4d-35b0-47c5-af72-1239cfb3253b/surfboard.gif">View large version</a>)</figcaption></figure>

<p>Now, just create two small rounded rectangles, with a little extra line on top for the board’s rack. Place them in a layer behind the car’s main body shape.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/606f1fc7-6b22-4fa4-9e93-8927fb19e480/rack.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/606f1fc7-6b22-4fa4-9e93-8927fb19e480/rack.png" sizes="100vw" caption="Board rack pieces (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/606f1fc7-6b22-4fa4-9e93-8927fb19e480/rack.png'>View large version</a>)" alt="Board rack pieces" >}}

<p>With the Pen tool, add the rudder. Its color is <code>#B2E3EF</code>. And for the stroke, use a 6-pixel width and set the color to <code>#131000</code>.</p>

- **Spare wheel**  
Now let’s create the the spare wheel! Switch to the Rounded Rectangle tool. Drag over the canvas to draw a shape. Color it `#34646C`, and make the stroke `#131000` and 8 pixels in size. The size of the spare wheel should fit the proportions of your car and should have the same diameter as the other wheels, or perhaps just a bit smaller. Pull the orange dots totally inwards, and give it a 45-degree angle. For the rack that holds the wheel, create a small piece with the Rectangle tool, and give it the same 45-degree angle, color it `#4A8F99`, and make the stroke `#131000` and 4.5 pixels in size. Create the last piece that rests over the car in the same way, with a color of `#34646C`, and a stroke that is `#131000` and 4.5 pixels in size.

Lastly, let’s create a shadow inside the wheel to add some more interest. For this, we’ll create a clipping mask and insert an ellipse shape with a color of `#194147`, without a stroke.

<p><strong>Note:</strong> <em>We may want to create the same shadow effect for the car wheels. Use the Rectangle tool and a color of <code>#312A00</code>, create a clipping mask, and insert it in the wheel shape, placing it halfway.</em></p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fc4b860-d5e7-4ef5-a706-2001513227b2/spare-wheel.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fc4b860-d5e7-4ef5-a706-2001513227b2/spare-wheel.png" sizes="100vw" caption="Three simple shapes to draw the spare wheel and its rack (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fc4b860-d5e7-4ef5-a706-2001513227b2/spare-wheel.png'>View large version</a>)" alt="Three simple shapes to draw the spare wheel and its rack" >}}

- **Bumpers**  
For the bumpers, we will apply the boolean operation “add” to two basic shapes and then clip-mask a shadow, just as we did for the wheels.

<p>Boolean operations are displayed in the section of icons labeled “Geometry” (Mac) and “Operations” (Windows). (Yes, the label names are inconsistent, but the Affinity team will likely update them in the near future, and one of the labels will become the default for both operating systems.) If you don’t see them in the upper toolbar, go to “View” &rarr; “Customize Toolbar”, and drag and drop them into the toolbar.</p>

<p><strong>Important:</strong> If you want the operation to be non-destructive, hold the Alt key while clicking on the “Add” icon (to combine the two basic shapes).</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcc188fa-a469-488a-a0bc-0c80c351d056/geometry.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcc188fa-a469-488a-a0bc-0c80c351d056/geometry.png" sizes="100vw" caption="Boolean operations: Add, Subtract, Intersect, Divide, Combine. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcc188fa-a469-488a-a0bc-0c80c351d056/geometry.png'>View large version</a>)" alt="Boolean operations: Add, Subtract, Intersect, Divide, Combine." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57987244-ea91-4dba-837f-e52626f61926/single-shape-from-two-shapes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57987244-ea91-4dba-837f-e52626f61926/single-shape-from-two-shapes.png" sizes="100vw" caption="Applying the (destructive) Add operation to create a single shape from two shapes. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57987244-ea91-4dba-837f-e52626f61926/single-shape-from-two-shapes.png'>View large version</a>)" alt="Applying the (destructive) Add operation to create a single shape from two shapes." >}}

<p><strong>Note:</strong> <em>If you try to paste the “shadow” object inside the bumper, it will <strong>only</strong> work if the bumper is one whole object (a destructive operation). So, if you used <kbd>Alt</kbd> + “Add”, this will not work now. However, you can still work around this by converting the Compound shape (the result of a non-destructive operation that is a group of two objects) to one Curve (one whole vector object). You just need to click on the Compound shape, then in the menu go to “Layer” &rarr; “Convert to Curves” (or use the key combination <kbd>Ctrl</kbd> + <kbd>Enter</kbd>).</em></p>

- **Back window**  
We are still missing the back window, which we will create with the Pen tool, and the decoration for the car. For the two colored stripes, we need the Square tool and then clip-mask these two rectangles into the main bodywork. The size is 30 &#215; 380 pixels, and the colors are <code>#0AC8CE</code> and <code>#FF6500</code>. Clip them by making sure you’ve put them on the right layer, so that the dark lines we drew before are <strong>above them</strong>.</p>

- **Number 56**  
For the number “56” decoration, use the Artistic Text tool (“T”), and type in “56”. Choose a nice font that matches the style of the illustration, or [try the one I’ve used](https://www.fontsec.com/fonts/51416/phosphateinline.html)</a>.</p>

<p>The color for the text object is <code>#FFF3AD</code>.</p>

<p>(I added an extra squared shape behind the back fender, which will look like the end of the exhaust pipe. The color is <code>#000000</code>.)</p>

- **Color strips**  
Now that we’ve done this, check the color stripes and the window they overlap with. As you can see (and because we put some transparency in the window glass), the orange stripe is **visible through it**. Let’s use some Boolean power again to fix this.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d619a22a-3da9-4019-9262-1c0741207d1f/almost-car.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d619a22a-3da9-4019-9262-1c0741207d1f/almost-car.png" sizes="100vw" caption="Bumpers and exhauster added. Check out the overlapped window and the orange stripe! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d619a22a-3da9-4019-9262-1c0741207d1f/almost-car.png'>View large version</a>)" alt="Bumpers and exhauster added. Check out the overlapped window and the orange stripe!" >}}

<p>Duplicate the window object. Select both the window object (the one you just duplicated) and the orange stripe in the Layers panel. Apply a “subtract” operation.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec089a03-5e01-4727-8f38-a121410da6cc/window-stripe1-new.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec089a03-5e01-4727-8f38-a121410da6cc/window-stripe1-new.png" sizes="70vw" caption="Stage 1, before the subtract operation. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ba7c520-df98-407c-b5d2-8bb13bef9792/window-stripe1.png'>View large version</a>)" alt="Stage 1, before the subtract operation." >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f72b1ece-b4fd-49ff-ab64-c8d55a8015e3/window-stripe2-new.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ea231b6-8e2c-4eb8-8b1c-8b3b90875e5a/window-stripe2-1000.png" sizes="70vw" caption="Stage 2, once the subtract operation is applied. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba4dd967-8aa5-40b2-9d53-d4288657f247/window-stripe2.png'>View large version</a>)" alt="tage 2, once the subtract operation is applied." >}}

<p>Now, the orange stripe has the perfect shape, fitting the window in such a way that they don’t overlap.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b99ea04-ba78-4520-83d8-967904858075/stripe-window-boolean.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b99ea04-ba78-4520-83d8-967904858075/stripe-window-boolean.png" sizes="70vw" caption="Stripe and window with subtraction operation applied. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b99ea04-ba78-4520-83d8-967904858075/stripe-window-boolean.png'>View large version</a>)" alt="Stripe and window with subtraction operation applied." >}}

- **Smoke**  
To create the **smoke** from the exhaust, draw a circle with a white stroke, 5.5 pixels in size and no fill. Transform it to curves and break one of its points. From the bottom node, trace a straight line with the Pen tool.

<p>Duplicate this “broken” circle, and resize to smaller circles, and flip and place them so that they look like this:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64055ff5-709f-426b-af35-4dd4de02d36e/exhauster-smoke.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64055ff5-709f-426b-af35-4dd4de02d36e/exhauster-smoke.png" sizes="100vw" caption="Creating the exhaust smoke (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64055ff5-709f-426b-af35-4dd4de02d36e/exhauster-smoke.png'>View large version</a>)" alt="Creating the exhaust smoke" >}}

<p><strong>Note:</strong> <em>Now that the car is finished, group all of its layers together. It will be much easier to keep working if you do so!</em></p>

### 11. Creating The Ground And The Background Elements.

- **Ground**  
Let’s trace a simple line for the ground, and add two bits breaking it in order to create visual interest and suggest a bit of movement. We also want to add an extra piece to create the ground. For this, we will use the Rectangle tool and draw a rectangle with a gradient color of `#008799` for the left stop and `#81BEC7` for the right stop. Give it 30% opacity.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30dd3816-8849-41ad-8e86-06d1751ebf9e/17-gradient-floor.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30dd3816-8849-41ad-8e86-06d1751ebf9e/17-gradient-floor.png" sizes="100vw" caption="Gradient for the ground piece and the grouped car layers for a clean view in the Layers panel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30dd3816-8849-41ad-8e86-06d1751ebf9e/17-gradient-floor.png'>View large version</a>)" alt="Gradient for the ground piece and the grouped car layers for a clean view in the Layers panel." >}}

- **Clouds**  
For the clouds, select the Cloud tool from the list of (primitive) vector shapes. Draw a cloud by holding Shift to keep the proportions. Make it white. Transform it into curves, and with the Node tool (<kbd>A</kbd>) select the bottom nodes and delete them. Sub-select the bottom-left and bottom-right nodes (after deleting all of the others), and then in the Context toolbar, select “Convert to Sharp” in the Convert section. This will make your bottom segment straight. Apply some transparency with the Transparency tool (<kbd>Y</kbd>), and duplicate this cloud. Place the clouds in your drawing, spread apart as you wish and in different sizes.

<p>My clouds have 12 bubbles and an inner radius of 82%. You can do the same or change these values to your liking.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34b65b64-d2fe-41d8-9f7f-1f6c7e263864/clouds.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34b65b64-d2fe-41d8-9f7f-1f6c7e263864/clouds.gif" width="600" height="375" alt="Creating the clouds with the Cloud tool and the Transparency tool" /></a><figcaption>Creating the clouds with the Cloud tool and the Transparency tool (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34b65b64-d2fe-41d8-9f7f-1f6c7e263864/clouds.gif">View large version</a>)</figcaption></figure>

- **Palm trees**  
To create the palm trees, use the Crescent tool from the list of primitive shapes on the left. Give it a gradient color, with a left stop of `#F05942` and a right stop of `#D15846`.

<p>Drag to draw the crescent shape. Move its center of rotation to the bottom of the bounding box, and give it a -60-degree angle.</p>

<p>The center of rotation can be made visible in the Contextual toolbar section for the Move (and Node) tool. It looks like a little crosshair icon. When you click on it, the crosshair for moving the rotation center of an object will show. Duplicate it, either via <kbd>Cmd</kbd> + <kbd>C</kbd> and <kbd>Cmd</kbd> + <kbd>V</kbd> (Mac) or <kbd>Ctrl</kbd> + <kbd>C</kbd> and <kbd>Ctrl</kbd> + <kbd>V</kbd> (Windows), or by clicking and then <kbd>Alt</kbd> + dragging on the object, and move the angle of the new crescent to -96 degrees. Make it a bit smaller. Copy the two shapes and flip them horizontally.</p>

<p>I also created and extra crescent.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8a0abee-c070-4b23-9998-12c46a0555e8/palm1.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8a0abee-c070-4b23-9998-12c46a0555e8/palm1.gif" width="600" height="375" alt="Creating the palm leaves" /></a><figcaption>Create the palm leaves (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8a0abee-c070-4b23-9998-12c46a0555e8/palm1.gif">View large version</a>)</figcaption></figure>

<p>To create the indentations on the leaves, transform the object to curves, add a node with the Node tool, and pull inwards. To make the vortex sharp, use “Convert” &rarr; “Sharp”.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0eb7a64-952f-4c2b-978b-fd11c9c87275/palm2.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0eb7a64-952f-4c2b-978b-fd11c9c87275/palm2.gif" width="600" height="375" alt="Creating the leaves’ indentations" /></a><figcaption>Creating the leaves’ indentations (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0eb7a64-952f-4c2b-978b-fd11c9c87275/palm2.gif">View large version</a>)</figcaption></figure>

<p>Create the trunk of the palm tree with the Pen tool, group all of the shapes together, and apply an “add” boolean. This way, all of the shapes will transform into just one. Apply a 60% opacity to it.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbbb670d-a3b5-45f0-ae33-74dbd7ba0b29/joint-palmtree.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbbb670d-a3b5-45f0-ae33-74dbd7ba0b29/joint-palmtree.png" sizes="100vw" caption="The palm tree once the Add boolean operation has been applied (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbbb670d-a3b5-45f0-ae33-74dbd7ba0b29/joint-palmtree.png'>View large version</a>)" alt="The palm tree once the Add boolean operation has been applied." >}}

<p>Duplicate the tree shape several times, changing the sizes and tweaking to make the trees slightly different from one another. (Making them exactly the same would result in a less interesting image.)</p>

<p>The last thing we need to make is the sun.</p>

- **The sun**  
For this, simply draw an ellipse and apply a color of `#FFFFBA` to it. Apply a transparency with the Transparency tool (<kbd>Y</kbd>), where the bottom is transparent and gets opaque at the top.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31e2fada-5b56-430c-a296-6ba0cbe9b2fe/sun.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31e2fada-5b56-430c-a296-6ba0cbe9b2fe/sun.png" sizes="100vw" caption="Transparency applied to the sun shape (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31e2fada-5b56-430c-a296-6ba0cbe9b2fe/sun.png'>View large version</a>)" alt="Transparency applied to the sun shape" >}}

<p>Now we will add some detail by overlapping several rounded rectangles over the sun circle and subtracting them (click <kbd>Alt</kbd> for a non-destructive action, if you prefer).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8682f945-ffc3-4eca-9ecc-911f664e6003/sun-subtract.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8682f945-ffc3-4eca-9ecc-911f664e6003/sun-subtract.gif" width="600" height="375" alt="Applying a subtract operation" /></a><figcaption>Applying a subtract operation (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8682f945-ffc3-4eca-9ecc-911f664e6003/sun-subtract.gif">View large version</a>)</figcaption></figure>

<p>Place your sun in the scene, and we are done!</p>

### 12. A Note On The Stacking Order (And Naming Of Layers)

<p>While you work, and as the number of objects (layers) grows, which will also make your illustration more and more complex, keep in mind the <strong>stacking order</strong> of your layers. The sooner you start naming the layers <strong>and</strong> placing them in the right order, the better. Also, lock those layers that you’re done with (especially for things such as the background), so that they don’t get in the way as you work.</p>

<p>In this illustration, the order of elements from bottom to top is:</p>

<ul>
<li>background,</li>
<li>ground,</li>
<li>sun,</li>
<li>clouds,</li>
<li>palm trees,</li>
<li>car.</li>
</ul>

## Conclusion

<p>I hope you could follow all of the steps with no major problems and now better understand some of Affinity Designer’s main tools and actions. (Of course, if you have some questions or need help, leave a comment below!)</p>

<p>These tools will allow you to create not only flat illustrations, but many other kinds of artwork as well. The tools, actions and procedures we’ve used here are some of the most useful and common that designers and illustrators use daily (including me), be it for simple illustration projects or much more complex ones.</p>

<p>However, even my <a href="https://dribbble.com/shots/2373851-1957-Chevy-Corvette-Roadster-Vector-Drawing">most complex illustrations</a> usually need the same tools that we’ve seen in action in this tutorial! It’s mainly a matter of understanding how much you can get out of each tool.</p>

<p>Remember the few important tips, such as locking the layers that could get in your way (or using half-transparency), stacking the layers in the right order, and naming them, so that even the most complex of illustrations are easy to organize and work with. Practice often, and try to organize things so that your workflow improves &mdash; this will lead to better artwork and better time management as well.</p>

<p>Also, to learn more about how to create this type of illustration, check out the <a href="https://www.youtube.com/watch?v=V0c9f270zFU">video tutorial</a> that I posted on my YouTube channel.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e25a538e-9616-4cc1-887f-3ac549e6277c/finished-beetle.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e25a538e-9616-4cc1-887f-3ac549e6277c/finished-beetle.png" sizes="100vw" caption="The completed Volkswagen Beetle illustration. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e25a538e-9616-4cc1-887f-3ac549e6277c/finished-beetle.png'>View large version</a>)" alt="The completed Volkswagen Beetle illustration." >}}

{{< signature "mb, ms, ra, yk, al, il" >}}
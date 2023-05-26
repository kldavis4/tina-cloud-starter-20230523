---
title: A Deep Dive Into Adobe Edge Reflow
slug: deep-dive-into-adobe-edge-reflow
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19687287-aa5b-4d51-b6bc-6e4ab8797ede/10-reflow-editing-breakpoints-500.png
date: 2015-02-17T18:00:33.000Z
author: brian-wood
description: >-
  Most of us were thrown for a loop when responsive design came into being. We
  tried to jam it into our existing, pixel-perfect, old-as-the-web-itself
  processes. It’s been a steep learning curve (and still is). In my previous
  article “[Next-Generation Responsive Web Design Tools: Webflow, Edge Reflow,
  Macaw](https://www.smashingmagazine.com/2014/05/23/next-generation-responsive-web-design-tools-webflow-edge-reflow-macaw/)”
  for Smashing Magazine, I didn't have enough space to dive as deep into those
  tools, as I wanted. So, in this article, I’m going to dive deep into just one
  of those tools: Adobe Edge Reflow CC.

  Edge Reflow is one in an avalanche of tools that have come out that make it
  possible to **visually design a responsive website**. What you do with that
  design is up to you (and the capabilities of the tool). Edge Reflow was
  created to address how responsive design has changed our web workflows.
categories:
  - Graphics
  - Workflow
  - Wireframing
  - Prototyping
---
Most of us were thrown for a loop when responsive design came into being. We tried to jam it into our existing, pixel-perfect, old-as-the-web-itself processes. It’s been a steep learning curve (and still is).

In my previous article “<a href="https://www.smashingmagazine.com/2014/05/23/next-generation-responsive-web-design-tools-webflow-edge-reflow-macaw/">Next-Generation Responsive Web Design Tools: Webflow, Edge Reflow, Macaw</a>” for Smashing Magazine, I didn't have enough space to dive as deep into those tools, as I wanted. So, in this article, I’m going to dive deep into just one of those tools: Adobe Edge Reflow CC.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Web Design Techniques, Tools and Strategies](https://www.smashingmagazine.com/2011/07/responsive-web-design-techniques-tools-and-design-strategies/)
*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [Using Sketch For Responsive Web Design](https://www.smashingmagazine.com/2015/04/using-sketch-for-responsive-web-design-case-study/)
*   [Photoshop Etiquette For Responsive Web Design](https://www.smashingmagazine.com/2016/08/photoshop-etiquette-for-responsive-web-design/)

Edge Reflow is one in an avalanche of tools that have come out that make it possible to visually design a responsive website. What you do with that design is up to you (and the capabilities of the tool). Edge Reflow was created to address how responsive design has changed our web workflows.

{{% feature-panel %}}

Reflow takes your static Photoshop (PSD) files and breathes responsiveness into them. Instead of having to create 3, 7, 14 or however many Photoshop comps for each necessary device or size, you can let Reflow convert the Photoshop content into HTML and CSS and then visually adjust the design using breakpoints in Reflow.</p>

## Where Does Reflow Fit In Our Web Workflow?

This is the question I get most often. As Adobe states, Reflow is meant to “start responsive designs faster and create high-fidelity prototypes through media query breakpoints, precise CSS layouts, grouping and more.” A big plus is that it connects directly with Photoshop, so the thought is that you can go from a static design to a responsive prototype (or at least a starting point) in a few moves.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47fef511-3685-4a23-9408-fd564d235a18/01-reflow-workspace-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e11a516-3059-4054-a1cf-fcda41dab6a9/01-reflow-workspace-opt-500.png" alt="Edge Reflow product page." width="500" height="422" /></a><figcaption>Edge Reflow’s product page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47fef511-3685-4a23-9408-fd564d235a18/01-reflow-workspace-opt.png">View large version</a>)</figcaption></figure>

What can you use Reflow for right now? I’ve seen Reflow used as a simple way to mock up a one-page concept for a client, which can work well. Reflow can also be used to visually resolve a website design problem. It's a <strong>great tool for wireframing</strong>. If you want to build a complete responsive website without getting your fingers dirty with code, however, you'll work too hard to accomplish a goal that other tools do better in less time.

Reflow may be part of a web developer's toolbox, but it's not meant to be a one-stop website creation tool. You’ll need to decide if it could (or should) play a part in your workflow based on what it can and can't do. If you work with designers upstream, or you are a designer, then it might fit. As a developer myself, I'll cut to the chase and add also that the code it generates is not how I would do it. For starters, it uses IDs for style names and is only optimized for WebKit browsers. Does that mean you throw the code in the trash? Not necessarily, as you'll see.</p>

## You Can Start With Photoshop

Currently, Reflow is being positioned as a visual design tool, which means you can drag and drop content and make formatting edits using panels, but it does require some knowledge of HTML and CSS (at least the basics). If you step into Reflow not knowing what a float is or how margins affect a layout, then the learning curve will be steeper.

There are a few ways to start a responsive design project in Edge Reflow. You could crack open Reflow and choose File → New Project and start jamming on a blank canvas, pulling content from Photoshop or pushing content from Photoshop to Reflow (or a combination of those methods). Adobe focuses on the Photoshop connection because that’s how most designers used to start their designs (and maybe still do, depending on their workflow and distaste for code), so we’ll do the same.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3529d72-917d-46e2-a6f1-ab8b908f4a03/02-photoshop-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e29045f1-9afd-4c1a-8504-b4fef15bd0a0/02-photoshop-opt-500.png" alt="Edge Reflow CC's workspace." width="500" height="379" /></a><figcaption>Edge Reflow CC’s workspace. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3529d72-917d-46e2-a6f1-ab8b908f4a03/02-photoshop-opt.png">View large version</a>)</figcaption></figure>

A lot of people I talk to start designing in Photoshop and then push (or export) to Reflow. This way, they use the same design features and knowledge of Photoshop that they've always had. That said, here are a few best practices for working with Photoshop if you plan to go to Reflow from it.

*   **Use smart objects**.  Smart objects are useful because they link shared content, such as navigation and footer content, to your Photoshop file. Smart objects for images also allow you to keep full-resolution versions for later editing (think non-destructive editing).
*   **Be careful about _linked_ smart objects**.  Right after I said to use them, right? Highly suspect, Brian. Currently, any linked smart objects (PSB) files in Photoshop will be simply flattened when exported to Reflow. Suppose you have shared navigation with text — that will become rasterized.
*   **Set the right size**.  This doesn’t really need to be said, but start in Photoshop with the size that you are aiming for, whether it’s mobile first or something else.
*   **Set up Extract Assets**.  This is a must if you plan to export from Photoshop to Reflow. File → Extract Assets in Photoshop will generate the optimized assets (you’ll learn about this shortly).
*   **Round your numbers**.  As with all things web, we try not to keep our formatting values at things like `12.347655893pt`.
*   **Use shapes, not filled layers**.  Shapes become `<div>`s in Reflow, and filled layers become nothing (they are dropped when you export).
*   **Organize your layers**.  The HTML that is generated follows the stacking order in the Layers panel. Content at the top of the Layers panel will appear at the top of the HTML document. In other words, make sure that your footer content isn’t a top layer in the Layers panel, otherwise it will be close to the opening `<body>` tag, and you’ll have to use some unsavory methods to position it at the bottom of the page in the HTML.
*   **Mind layered images**.  Images with content layered on top of them are treated as background images in a `<div>` in Reflow.
*   **Think about naming layers**.  If you name a layer something like _image.png, 200% image@2x.png_, then two images will be generated. The first image in the list will be placed in the design in Reflow, and the other will be generated and will hang out in the _assets_ folder.
*   **Mind text objects**.  Text objects that are drawn in Photoshop as a type area will have a dimension in Reflow. If you simply click with the Type tool in Photoshop, then the paragraph in Reflow will not have a width.</p>

## Photoshop Extract Assets

Adobe Photoshop CC has a feature called Extract Assets (File → Extract Assets) which utilizes Adobe Generator. You can generate JPEG, PNG, GIF, or SVG image assets from the contents of a layer or layer group in a PSD file when you export to Reflow. Choosing File → Extract Assets allows you to optimize assets, setting sizes, formats, and more. After setting up the optimization settings, your layer names are altered, adding a supported extension for an image format (PNG, GIF, JPG, or SVG) to a layer name or a layer group name. Generator will create the images used in Reflow and free us from having to slice in most cases (yay!). Even if you wind up not using Reflow, Extract Assets is worth a look. You can then export to Reflow and the optimized assets will be automatically generated.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfd9c7b5-a0b5-46bf-9fd8-c7cabae325a7/03b-photoshop-name-layers-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9ee8b0c-cee1-42ff-97cc-31af1d68570f/03b-photoshop-name-layers-opt-500.jpg" alt="Named layers in Photoshop CC 2014." /></a><figcaption>Named layers in Photoshop CC 2014.</figcaption></figure>

With the content named in the Layers panel, you can finally breathe responsiveness into your Photoshop file by exporting to a Reflow project file (File → Generate → Edge Reflow Project). When it’s complete, a folder will be generated in the same folder as the PSD. This folder contains a Reflow project (<i>.rflw</i>), as well as the generated assets in an <i>assets</i> folder.</p>

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b960dc57-7340-4bd1-9e3c-e6908463d072/04-export-to-reflow.jpg" alt="The generated content after exporting to Reflow from Photoshop." width="500" height="282" /><br>
<figcaption>The generated content after exporting to Reflow from Photoshop.</figcaption></figure>

## Toss It Over To Reflow

After you export from Photoshop, you can open the Reflow project file (<i>.rflw</i>) in Edge Reflow to see what was created. If any fonts are missing, Reflow will show a prompt allowing you to fix them with Typekit fonts, Edge Web Fonts, web-safe fonts or local fonts.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10c89781-d582-4114-ab56-568affdf36ce/05-reflow-missing-font-dialog-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56a74718-7c1a-4bb8-9da0-64476cdbee8c/05-reflow-missing-font-dialog-opt-500.png" alt="Dialog for missing fonts in Edge Reflow CC." width="500" height="347" /></a><figcaption>Dialog for missing fonts in Edge Reflow CC. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10c89781-d582-4114-ab56-568affdf36ce/05-reflow-missing-font-dialog-opt.png">View large version</a>)</figcaption></figure>

The Photoshop content was converted to HTML and CSS according to the original content (text, vector, raster) and the layer structure in Photoshop. If you click the Elements panel icon on the right, you will see the code (DOM) for the HTML that has been generated. If you look at the structure and naming, you will see that it is loosely based on the Layers panel in Photoshop. You will find that hidden content is ignored and that groups (the folders) are also ignored, but that the content within is not. Also, text is still editable (in most cases), and named vector content and raster content are now raster images.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/998453a8-7a3f-4171-b57c-45b27083a575/06-reflow-element-panel-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fce92b1c-cb02-4113-a047-d8c69bf21e5f/06-reflow-element-panel-opt-500.png" alt="The Elements panel in Reflow showing the DOM." width="500" height="353" /></a><figcaption>The Elements panel in Reflow showing the DOM. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/998453a8-7a3f-4171-b57c-45b27083a575/06-reflow-element-panel-opt.png">View large version</a>)</figcaption></figure>

The code that is generated uses HTML5 Boilerplate for a CSS “normalize” sheet, but the layout really isn’t based on an existing framework, such as Twitter’s Bootstrap. Below is an example of code generated for the <code>&lt;head&gt;</code> of a page when exported.</p>

<pre><code class="language-markup">
&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;link rel="stylesheet" href="boilerplate.css"&gt;
    &lt;link rel="stylesheet" href="page.css"&gt;
    &lt;meta charset="utf-8"&gt;
    &lt;meta name="viewport" content="initial-scale = 1.0,maximum-scale = 1.0"&gt;
  &lt;/head&gt;
  &lt;body&gt;
  …
</code></pre>

The image content that is generated from your named layers in Photoshop is in the <i>assets</i> folder (as we saw earlier) and can be found in the Asset Library panel on the right in Reflow. The Asset Library panel shows <em>all</em> images in the <i>assets</i> folder, even those not currently in the design, and it functions similarly to the Links panel in InDesign and Illustrator. You can tell which images are not being used in your design because they have a number <code>0</code> to the right of their name in the panel. In this panel, you can search for assets, replace assets, update assets and more.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bec56ec-563a-440f-a980-82d1269a581e/07-reflow-asset-library-panel-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0af137dc-176f-4bae-bc18-1d554adb1b22/07-reflow-asset-library-panel-opt-500.png" alt="Asset Library panel in Reflow." width="500" height="453" /></a><figcaption>Asset Library panel in Reflow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bec56ec-563a-440f-a980-82d1269a581e/07-reflow-asset-library-panel-opt.png">View large version</a>)</figcaption></figure>

## The Photoshop CC Connection

Once you export from Photoshop CC, the connection to your Photoshop design is still somewhat alive in Reflow. I say “somewhat” because any changes to generated image content made in Photoshop (and that you named in the Layers panel) can be updated in Reflow. Text, page elements and other unnamed content will not.

In Reflow, the Photoshop CC Connect panel (on the right) is where you will see the connection to Photoshop. If Photoshop CC is open, then the panel will show you that Reflow is connected to whatever file is open in Photoshop. This threw me at first. You could have a PSD open in Photoshop that has nothing to do with the Reflow design, and it will still show you that it’s connected.

“Connected” can mean a few things. You can open the PSD file that the Reflow project was created from and make updates, which in turn will update the applicable content in Reflow. You can open a different PSD (or even show a different layer comp) — say, for a new page on the website — and create a new page from that PSD content by clicking the “Create New Page” button in Reflow. You can even open a PSD file and simply generate the named layer content and save it into the project’s <i>assets</i> folder (maybe from a PSD that contains icons or other elements) by clicking the “Import Assets” button in Reflow.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ee859c6-fb07-4733-ad31-d559fead464d/08-reflow-connect-panel-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/874af92f-65df-4b77-9dc0-82376f14cdd8/08-reflow-connect-panel-opt-500.png" alt="Photoshop CC Connect panel in Reflow." width="500" height="453" /></a><figcaption>Photoshop CC’s Connect panel in Reflow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ee859c6-fb07-4733-ad31-d559fead464d/08-reflow-connect-panel-opt.png">View large version</a>)</figcaption></figure>

To make changes to the design in Photoshop and update the Reflow project, you will first need to turn on “Photoshop Asset Sync” (an arrow is pointing to it in the following screenshot). You can then open the PSD in Photoshop and make changes to the design, and any named layer content that is generated by Photoshop Generator will need to be updated in the Asset Library panel in Reflow (circled below).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/643dadd8-acdb-4eaf-bc7f-d6fb4679923e/09-reflow-update-photoshop-content-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b2b83af-bb9a-49af-a701-9247ca9d8d36/09-reflow-update-photoshop-content-opt-500.png" alt="Updating Photoshop content in turn updates Reflow content." width="500" height="453" /></a><figcaption>Updating Photoshop content in turn updates Reflow content. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/643dadd8-acdb-4eaf-bc7f-d6fb4679923e/09-reflow-update-photoshop-content-opt.png">View large version</a>)</figcaption></figure>

## Adding And Editing Breakpoints

By default, your project in Reflow contains no breakpoints (i.e. media queries) and is a purely fluid design (set to percentage widths, with no maximums or minimums). It’s your job to <strong>add breakpoints where you see fit</strong> (usually where the design falls apart). Clicking the “+” (plus) button in the upper-right corner will add an initial breakpoint (which is a good idea). If you click and hold down “+” in the upper-right corner, a menu will appear that lists all of the breakpoints. Here is where you can edit an existing breakpoint (the value or the label) or delete a breakpoint. You can also set the breakpoints (media queries) to be either minimums or maximums (one or the other).

I really wish Reflow would take media queries further, allowing for a mixture of max/min or other types of media queries (think Retina), but at its core, it's a visual responsive design tool meant to prototype.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd30ee1a-72b7-4e0a-bac1-b65d4a0fa21d/10-reflow-editing-breakpoints.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19687287-aa5b-4d51-b6bc-6e4ab8797ede/10-reflow-editing-breakpoints-500.png" alt="Editing breakpoints for a Reflow project." width="500" height="261" /></a><figcaption>Editing breakpoints for a Reflow project. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd30ee1a-72b7-4e0a-bac1-b65d4a0fa21d/10-reflow-editing-breakpoints.png">View large version</a>)</figcaption></figure>

If you drag the gripper bar on the right edge of the page’s content to the right or left, you will see how the design responds. When you need to make a design change, click “+” to set a new breakpoint. Click on the colored bars above the ruler (indicating a breakpoint) to resize the design to that breakpoint.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f557fb4-c2a4-4953-9f4f-5a462fe38b92/11-reflow-resize-handle-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f13d4ae-eb13-4a51-9b3d-f0577bc3bc4d/11-reflow-resize-handle-opt-500.png" alt="The handles for setting breakpoints and resizing in the design." width="500" height="578" /></a><figcaption>The handles for setting breakpoints and resizing in a design. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f557fb4-c2a4-4953-9f4f-5a462fe38b92/11-reflow-resize-handle-opt.png">View large version</a>)</figcaption></figure>

Adding and deleting breakpoints are easy, but there is a catch in Reflow (and other programs like this). If you go to make a design change, make sure to select the correct breakpoint! If not, it’ll bite you at some point because undoing in Reflow (Edit → Undo) still needs some work.</p>

## How Reflow Interprets Your Design (Floats, `<div>`s, Etc.)

With the Selection tool selected in the Tools panel (by default), you can select content on the page. All of your page’s content lies within a primary container (<code>&lt;div&gt;</code>) that is set to center horizontally and that has a 100% width. Shapes in Photoshop typically become <code>&lt;div&gt;</code>s in Reflow; text becomes <code>&lt;p&gt;</code> elements with styles applied; images become either regular images or background images, and so on. Almost all of the content in your Reflow project will be positioned using the CSS properties <code>float: left</code> and <code>margin</code>. Knowing this is important when you attempt to edit the design in Reflow by simply dragging content. I’ve seen a lot of people get tripped up if they haven’t learned the basics of layout, including margins, padding and floating.

The layout editing and formatting controls are found in the Layout and Styling panels on the left. The Layout panel is where you will find typical CSS properties like sizing (including maximum and minimum widths and heights), margins and padding, positioning, floats, clears and more. The more advanced formatting options are hidden initially in the Advanced section of the Layout panel. In Reflow, most people either use a combination of dragging and sizing the content manually or adjusting the layout options “by the numbers” in the Layout panel.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02c81f22-83d2-48e7-8839-8436d03a5611/12-reflow-layout-options-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ab8a993-2543-49c1-b47a-5c5d93c64e8a/12-reflow-layout-options-opt-500.png" alt="The layout options in Reflow." width="500" height="470" /></a><figcaption>The layout options in Reflow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02c81f22-83d2-48e7-8839-8436d03a5611/12-reflow-layout-options-opt.png">View large version</a>)</figcaption></figure>

Styling options for text formatting, backgrounds, shadows, rounded corners and more are found in the Styling panel on the left. Text formatting is relatively straightforward, and Reflow allows you to use Edge Web Fonts, web-safe fonts, fonts on your hard drive, and fonts via a Typekit kit that you create. The Styling panel is where you also go to add rounded corners, borders and drop-shadows and to edit the opacity of other objects as well.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f861c30-d381-4823-9ae5-55adef9835d0/13-reflow-font-formatting-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69956d6b-16c6-473f-b8da-5546692736a3/13-reflow-font-formatting-opt-500.png" alt="Font formatting and other styling options." width="500" height="395" /></a><figcaption>Font formatting and other styling options. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f861c30-d381-4823-9ae5-55adef9835d0/13-reflow-font-formatting-opt.png">View large version</a>)</figcaption></figure>

If you’ve designed to a grid in Photoshop or you know that the goal for the project is to work with a particular grid or framework, then you can edit the visible grid in Reflow to match. With nothing selected (by clicking in a blank area of the design area), you will see the grid settings below the Tools panel in the upper-left corner. Of course, the grid in Reflow is merely a guide. It doesn’t generate a series of CSS styles, such as for fluid grids.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5341e473-22c7-49c5-8436-1fd0884fc785/14-reflow-grid-setting-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c5baf93-5103-498d-8a51-ccc496d3deef/14-reflow-grid-setting-opt-500.png" alt="Settings for the grid in Reflow." width="500" height="490" /></a><figcaption>Settings for the grid in Reflow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5341e473-22c7-49c5-8436-1fd0884fc785/14-reflow-grid-setting-opt.png">View large version</a>)</figcaption></figure>

## Editing The DOM

As mentioned, you can see the HTML structure in the Elements panel on the right side of the workspace. In that panel, you can hover over an element to see the corresponding content in the design (it will be highlighted) and click to select it. The eye icon in the Elements panel is a toggle for the <code>display</code> CSS property. Renaming content in the panel will change the name of the ID applied to the HTML object (as you can see in the screenshot below). Yes, I said ID. Reflow doesn't generate classes in the CSS, and currently there is no way to add a style name or change the type of style (to a class, for instance). This is limiting, because <strong>you can't inject any code</strong> (any code — even JavaScript) or make actual style changes outside of what the program can do. You need to export the code and take it somewhere else with no chance of bringing that code back in.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b2f6377-645e-48e1-84df-14c7166c4a14/15-reflow-editing-dom-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed860489-6c67-4c72-a4d6-36ceae5d7d49/15-reflow-editing-dom-opt-500.png" alt="Editing the DOM using the Elements panel in Reflow." width="500" height="237" /></a><figcaption>Editing the DOM using the Elements panel in Reflow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b2f6377-645e-48e1-84df-14c7166c4a14/15-reflow-editing-dom-opt.png">View large version</a>)</figcaption></figure>

You can also organize content in the Elements panel by dragging content, which will directly affect the HTML’s ordering and layout. You cannot nest content within, say, a new <code>&lt;div&gt;</code> using the Elements panel, but content that is nested may be moved out or moved between those groups. To nest selected content in a parent element (a <code>&lt;div&gt;</code>) to make a column, for instance, you could use the menu item Edit → Add Parent or even group the selected content (Edit → Group).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/474af1ec-9c2f-4cfc-9c8c-9c538a15f6a3/16-reflow-selected-content-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/763cf1ac-06ba-4138-910d-0d347e5ce1fa/16-reflow-selected-content-opt-500.png" alt="Selected content in the design (left) after choosing Edit → Add Parent to add a parent div to the content." width="500" height="147" /></a><figcaption>Selected content in the design (left) after choosing Edit → Add Parent to add a parent <code>&lt;div&gt;</code> to the content (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/474af1ec-9c2f-4cfc-9c8c-9c538a15f6a3/16-reflow-selected-content-opt.png">View large version</a>)</figcaption></figure>

<strong>Note:</strong> Clicking the “Page” element in the Elements panel allows you to edit the layout and styling properties of the <code>&lt;body&gt;</code> tag. Clicking the “Container” element allows you to edit the properties of the main containing <code>&lt;div&gt;</code> that all content is within by default.</p>

## Creating Pages

You can create pages in your Reflow project using the Page menu, Photoshop’s Assets panel (by clicking the “Create New Page” button) or the super-simple Pages panel on the right side of the workspace. In the Pages panel in Reflow, you can either duplicate a page or add a new blank page. If you duplicate a page, it will have no connection to the original page except for the images (which are linked to the same source images). In later builds of Reflow, thankfully, breakpoints are copied in duplicate layouts. If you create a series of pages that share navigation or footer content, the only real way (currently) to update that content on all pages is to go to each and make the changes, or to copy and paste the content from one page to the next. There are no such things as library items, symbols, or whatever you would call them to edit shared content in one place.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bf33c56-f42e-47c1-8be4-015fe687a703/17-reflow-duplicating-page-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1f84ca0-c78f-4eb1-b5e8-f3e3b20246b7/17-reflow-duplicating-page-opt-500.png" alt="Duplicating a page in the Pages panel in Reflow." width="500" height="453" /></a><figcaption>Duplicating a page in the Pages panel in Reflow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bf33c56-f42e-47c1-8be4-015fe687a703/17-reflow-duplicating-page-opt.png">View large version</a>)</figcaption></figure>

Each page in Reflow becomes a separate HTML page that gets its file name from the page’s name in the Pages panel. Each page has its own CSS file, and formatting that is the same across pages is not pulled into a shared CSS; it’s simply duplicated across multiple CSS files. The screenshot below shows what was generated when I chose File → Export For Code Editor.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5c5a21b-f62a-4722-91d2-40b92d9952bb/18-reflow-project-generation-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03c246c7-b0b8-4241-a594-507ff5cf1ada/18-reflow-project-generation-opt-500.png" alt="What is generated when I create a Reflow project and duplicate the only page." width="500" height="219" /></a><figcaption>What is generated when I create a Reflow project and duplicate the only page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5c5a21b-f62a-4722-91d2-40b92d9952bb/18-reflow-project-generation-opt.png">View large version</a>)</figcaption></figure>

## Working With Images

Within Reflow, you can insert PNG, GIF, JPEG and SVG images by dragging images into the design from the Assets panel or from a folder on your hard drive or by using the Add An Image tool to click and add an image. If you use the Add An Image tool, then you would choose an image and, with the place gun, click and place the image where you’d like.</p>

<strong>Note:</strong> The best practice is to put images in the <i>assets</i> folder that was generated by Reflow when you exported from Photoshop. If you insert an image in the design using the Add An Image tool that is outside of the <i>assets</i> folder, then it will be copied there.

Reflow also allows for multiple layered background images (and solid-color and gradient backgrounds), and it supports the most widely used CSS3 properties for adjusting the background images.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f86e042d-25b7-42f0-8a11-b272a8167f23/19-reflow-css3-properties-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d5d0f80-17cf-4c0e-bdf8-3a8b70154d87/19-reflow-css3-properties-opt-500.png" alt="A few of the CSS3 properties for background images in Reflow." width="500" height="494" /></a><figcaption>A few of the CSS3 properties for background images in Reflow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f86e042d-25b7-42f0-8a11-b272a8167f23/19-reflow-css3-properties-opt.png">View large version</a>)</figcaption></figure>

One of my favorite commands in Reflow is to select an image on the page (not a background image), right-click on it and choose “Move to New Box Background.” This will remove the <code>&lt;img&gt;</code> tag from the HTML, insert a <code>&lt;div&gt;</code> instead and creates a style with the same image but as a background image. You can even right-click on an image in the Asset Library panel and choose “Set as Background” for a selected object.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d4ea679-2220-494d-838b-87376fc23edf/20-reflow-convert-image-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06c026ec-23a7-4309-b40a-0a319134e649/20-reflow-convert-image-opt-500.png" alt="Converting an image to a background image in Reflow." width="500" height="386" /></a><figcaption>Converting an image to a background image in Reflow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d4ea679-2220-494d-838b-87376fc23edf/20-reflow-convert-image-opt.png">View large version</a>)</figcaption></figure>

<strong>Note:</strong> Currently, there is no mechanism for working with Retina images in Reflow.</p>

## Creating Forms

I wanted to add a section on working with forms, not to show how to insert them, but to discuss what they are and aren’t. The Form tools are found in the Tools panel. If you click and hold down the “Add a Button” button, you will see them all. By clicking or clicking and dragging, you can position and format each field pretty simply using the same properties as in the Layout and Styling panels.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57fcc7a8-e6ee-457c-bcd1-43b11887a1b3/21-reflow-form-tools.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fda6743-d35e-4065-bc51-1215bce64b3b/21-reflow-form-tools-500.png" alt="The form tools in Reflow." width="500" height="386" /></a><figcaption>The form tools in Reflow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57fcc7a8-e6ee-457c-bcd1-43b11887a1b3/21-reflow-form-tools.png">View large version</a>)</figcaption></figure>

The form you create in Reflow will not submit data. That’s because the tools will create form tags like <code>&lt;input&gt;</code> and <code>&lt;select&gt;</code> but will not add an actual <code>&lt;form&gt;</code> element to the code, which means you can’t set typical options for the <code>&lt;form&gt;</code> tag in Reflow by default (such as <code>method</code> and <code>action</code>). A form in Reflow can be used only as a visualization or starting point, to be edited in another program later.

Below is an example of code generated for a simple form created in Reflow.</p>

<pre><code class="language-markup">
&lt;label id="formgroup"&gt;
  &lt;p id="text"&gt;Name&lt;/p&gt;
  &lt;input id="textinput" type="text" value="Name"&gt;
&lt;/label&gt;
&lt;label id="formgroup2"&gt;
  &lt;p id="text2"&gt;Sign up?&lt;/p&gt;
  &lt;select id="select" type="select"&gt;
    &lt;option&gt;Choose one&lt;/option&gt;
    &lt;option&gt;Yes&lt;/option&gt;
    &lt;option&gt;No&lt;/option&gt;
  &lt;/select&gt;
&lt;/label&gt;
&lt;input id="input" type="button" value="Submit"&gt;
</code></pre>

## Edge Inspect Testing

Built in to Reflow is the ability to test on devices using Adobe Edge Inspect CC. Edge Inspect allows you to preview Edge Reflow content across multiple devices. Simply test the page, take screenshots from any connected device, and then see real-time results of changes to the design.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37b5b2d2-9c76-4088-be7a-c7cd1890a8fc/22-reflow-edge-inspect.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f84be69-0e67-407a-a181-de4bb62bcadf/22-reflow-edge-inspect-500.jpg" alt="Using Edge Inspect in Reflow to inspect a design." width="500" height="271" /></a><figcaption>Using Edge Inspect in Reflow to inspect a design. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37b5b2d2-9c76-4088-be7a-c7cd1890a8fc/22-reflow-edge-inspect.jpg">View large version</a>)</figcaption></figure>

<strong>Note:</strong> To preview Reflow content on a device, you’ll need to download Edge Inspect to your computer and then install the Edge Inspect CC app on an approved device (iOS, Android or Kindle Fire).</p>

## What Reflow Doesn’t Do

If you are using the program to create quick comps as a visual aid, then Reflow might work. But if you dig into the program and want to use the code that is generated, then be aware of what it can and can’t do. The things listed below are the <em>major</em> things it can’t do (as with any program, there are little things we each wish it could do, I know).</p>

### What About the Code It Generates?

The styling it generates is not very succinct, and IDs are used for just about everything. You can’t insert your favorite jQuery slideshow or other code in Reflow because code currently can’t be injected. Reflow does not really support much in the way of SEO content (who needs that anyway?), tables or lists. You can’t edit its CSS (the actual code) unless you make changes in the Styling panel. You also can’t add a blog or e-commerce functionality in Reflow (because code can’t be inserted).

Nick Halbakken’s good <a href="https://blogs.adobe.com/edgereflow/2014/05/07/q-a-from-talk-to-the-team/">Q&amp;A with the Adobe Reflow team</a> answers some of these questions.</p>

### What Can You Do With the Design?

As you edit a design, you can preview in two WebKit-based browsers (Safari and Chrome) by choosing View → Preview In… The code is not optimized for non-WebKit browsers. When you preview a page, the HTML and CSS are generated (this is how we used to get at the code if we wanted to use what Reflow generates). In later builds of Reflow, you can export the code by selecting File → Export for Code Editor. Exporting the code removes a line from the code stating that it’s only meant to be used for previewing, and then a copy of the content is created in a new folder of your choosing, and an HTML file is dumped in, which you will use as a frame for the pages when previewing.

If the code is not suitable for your production environment, then you can <strong>copy and paste CSS snippets</strong> from within Edge Reflow (this is how I use it, if at all). When you select content, you can click the “&lt; &gt;” icon in the tag selector at the bottom of the document’s window (an arrow is pointing to it in the screenshot below). This will display the CSS associated with the selected object, even giving you the CSS for each media query that affects the selected object. Click the clipboard icon at the bottom of the menu to copy all of the CSS, or click the clipboard icon for the CSS that you hover over to select just that code.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ac536b0-0649-463e-8886-7798e2df1fa3/23-reflow-copy-css.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dd2e75b-813e-49a0-ae3a-22a345bcb268/23-reflow-copy-css-500.png" alt="Copy CSS from Reflow." width="500" height="311" /></a><figcaption>Copy CSS from Reflow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ac536b0-0649-463e-8886-7798e2df1fa3/23-reflow-copy-css.png">View large version</a>)</figcaption></figure>

## Final Notes

There you have it: a quick-ish tour of the features in Edge Reflow CC. I know that this program can be polarizing, especially for those of us who can code. But I do have a use for this program in some of my projects. Would I use the code? Most likely not. But that’s also because my themes and frameworks are dialed in to how I like to create websites. I find it useful for my designers to <strong>use for quick prototypes or wireframing</strong>, mostly when they start the design in Photoshop. I also like to use it to see those niggly little text formatting properties that designers pore over, like <code>line-height</code>.

The program has a long way to go before its code can be used as is in a production workflow. I can’t tell you the ultimate direction it’s headed in — will it eventually integrate with an existing framework as a building point, or will it let you inject code? Will it survive the crush of tools coming out today or be an experiment that gets scrapped? — it's a risk we all take with tools these days. In my opinion, for it to be a one-stop shop tool to build sites in, it would have to come a long way from where it is now.

Where to go from here? Here are several resources to learn more about working with Edge Reflow CC:

*   [Lynda.com](https://www.lynda.com)
*   “[What is Edge Reflow CC?](https://tv.adobe.com/watch/learn-edge-tools/what-is-edge-reflow/)” (video), Justin Seeley, Adobe TV
*   [Brian Wood Training](https://www.youtube.com/user/askbrianwood) (video channel), YouTube

{{< signature "da, ml, al, og" >}}


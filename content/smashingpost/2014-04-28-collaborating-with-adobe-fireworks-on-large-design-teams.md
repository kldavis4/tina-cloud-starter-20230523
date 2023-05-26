---
title: Collaborating With Adobe Fireworks On Large Design Teams
slug: collaborating-with-adobe-fireworks-on-large-design-teams
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67d3b622-33a4-4976-a2a3-d1b78a21b403/fireworks-small-illu.jpg
date: 2014-04-28T21:49:06.000Z
author: dan-nisbet
description: >-
  Working with people can be hard. But get it right, and you’ll be able to
  produce stunning work more smartly and quickly than ever before. With
  methodologies such as _agile_ and _lean_ influencing how design teams work, some interesting challenges lie ahead. Iterative and collaborative practices vary greatly across work environments and even projects, and they can, and most likely will, bring your time-honed workflow to its knees.
categories:
  - Fireworks
  - Workflow
  - Communication
---
Working with people can be hard. But get it right, and you’ll be able to produce stunning work more smartly and quickly than ever before.

With methodologies such as <a title="Read: Explanation of Agile methodology" href="https://www.gov.uk/service-manual/agile">agile</a> and <a title="Read: Lean software development" href="https://en.wikipedia.org/wiki/Lean_software_development">lean</a> influencing how design teams work, some interesting challenges lie ahead. Iterative and collaborative practices vary greatly across work environments and even projects, and they can, and most likely will, bring your time-honed workflow to its knees.

A shared understanding of the tools (and the way you use them) is crucial, then. By sharing assets, constructing files systematically and generating objects using core techniques, the team is freed to focus on crafting concepts and solving problems, rather than fighting unwieldy file structures and obtuse working practices. This shared understanding should underpin everything the team works on, becoming part of an ever-evolving process of refinement and learning.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Developing A Design Workflow In Adobe Fireworks](https://www.smashingmagazine.com/2012/06/developing-a-design-workflow-in-adobe-fireworks/)
*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [The Present And Future Of Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

{{% feature-panel %}}

In this article, we’ll see how to start that journey by <strong>creating a stronger foundation for collaboration</strong>, even before the design process begins. I’ll also explore some techniques that are unique to Adobe Fireworks and that have the potential to transform your collaboration. (While these techniques involve Fireworks — my team’s tool of choice — you could apply them to your own workflow, even if you use another UI design tool.)

## The Right Tools For The Job

You don’t have to listen too hard to be deafened by the passionate war cries of designers defending their program of choice, or else ditching it altogether. With Adobe’s decision to <a href="https://blogs.adobe.com/fireworks/2013/05/the-future-of-adobe-fireworks.html">cease active development</a> of Fireworks, focusing on this design tool might seem strange. However, neither Photoshop nor Illustrator can yet be used to design interfaces and Web graphics as efficiently.

The open extension architecture of Adobe Fireworks keeps its pulse beating, enabling the wider community to pick up Adobe’s slack. (The article “<a title="The Present And Future Of Adobe Fireworks (an article by Michel Bozgounov)" href="https://www.smashingmagazine.com/2013/12/19/present-future-adobe-fireworks/">The Present and Future of Adobe Fireworks</a>” covers this topic in depth and is well worth digging into.)

When it comes to UI design, <strong>Fireworks still has numerous advantages</strong> and is without doubt my team’s preferred design tool. In fear of repeating others, I’ll refrain from describing every Fireworks feature, focusing instead on what works best for us and on how Fireworks improves our workflow.

To get primed, consider reading some of Smashing Magazine’s other detailed articles about Fireworks, covering such essentials as vector graphics, direct selection, master pages, symbols, prototyping and extensions:

*   “[Developing a Design Workflow in Adobe Fireworks](https://www.smashingmagazine.com/2012/06/11/developing-a-design-workflow-in-adobe-fireworks/),” Joshua Bullock
*   “[Useful Fireworks Techniques and Features for Large Design Teams](https://www.smashingmagazine.com/2012/10/12/adobe-fireworks-enterprise/),” Kris Niles
*   “iOS Prototyping With TAP and Adobe Fireworks,” [Part 1](https://www.smashingmagazine.com/2013/01/11/ios-prototyping-adobe-fireworks-tap-part1/), [Part 2](https://www.smashingmagazine.com/2013/01/ios-prototyping-with-tap-and-adobe-fireworks-part-2/), [Part 3](https://www.smashingmagazine.com/2013/02/15/ios-prototyping-adobe-fireworks-tap-part3/), Shlomo Goltz
*   “Optimizing the Design Workflow With Fireworks Extensions,” [Part 1](https://www.smashingmagazine.com/2012/08/28/fireworks-extensions-for-better-workflow/), [Part 2](https://www.smashingmagazine.com/2013/09/20/fireworks-extensions-for-better-workflow-part-2/), [Part 3](https://www.smashingmagazine.com/2013/11/06/even-more-fireworks-extensions-optimized-design-workflow/), Ashish Bogawat

What we’re really interested in is how best to exploit what’s available to improve collaboration. Below is a rundown of the juiciest parts.</p>

### Multiple Pages in a Single Document

Fireworks PNG (<code>*.fw.png</code>) is a neat, self-contained editable file format that contains all of a website or section’s layouts. This affords us a couple of advantages because we can apply a common page and layer structure to all pages in a document by using master pages and shared layers.

<img title="Multiple pages in Fireworks." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4457bae5-4aeb-4552-86d5-7d8f19fac534/01-multiple-pages.png" alt="Multiple pages in Fireworks." width="500" height="120" /><br>
<em>Multiple pages in Fireworks help to organize your workflow. (Image credit: <a href="https://www.smashingmagazine.com/2012/07/03/interactive-prototypes-timesavers-adobe-fireworks/">Trevor Kay</a>)</em>

Multiple pages also help with cross-device design, because each page can have its own dimensions. You could have laptop, tablet and mobile phone screens all in one file, and even 1× and 2× versions that share assets and styles!

### Using Symbols for Common UI Elements

By turning common UI elements into symbols, we can reuse them throughout the document. Update once and the changes will propagate everywhere!

Symbols can also make any transformations to a rasterized image non-destructive. Import an image, turn it into a symbol and then scale without a care.

<strong>Note:</strong> When using symbols to make bitmaps lossless when rescaled, you are still limited by the original image size. Scaling a symbol larger than the original will obviously introduce artifacts. Turning a bitmap into a symbol only facilitates lossless rescaling, as long as the symbol is as large as or smaller than the original.</p>

### External Libraries

With the Common Library, you can save a group of symbols outside of your PNG files to be reused across projects — think browser scroll bars, social icons and other handy stuff. Adobe Fireworks already comes preinstalled with a selection of symbols, ranging from fair to best forgotten. Unfortunately, these (and any libraries you create) must be saved locally in a particular folder on your computer, so sharing them with the team could be painful.

Fear not. This workflow can still be useful, and we’ll walk through a way that is not as well documented. Avoiding many of the limitations mentioned above, we can <strong>create a Fireworks master document</strong>: a single self-contained file that houses all of your shared symbols and that will feed all of your separate artwork files.</p>

### Export, Import and Update Graphic and Typographic Styles

Similar to other Adobe programs, Fireworks allows you to <strong>create a library of styles</strong>. Save any color, typographic style (font family, font weight, font color, etc.) or combination of live filters into a preset. Then, at the click of a button, the selected element will adopt the styles you’ve defined. These styles may be grouped, exported and imported between documents and, again, updated globally.

The workflow described in this article assumes a team of people, but the techniques will save you time even if you work alone.</p>

## Creating A Strong Foundation: Boilerplate To The Rescue

We’re going to have to overcome a few hurdles in order to use Fireworks effectively and to prepare a given project for the team. <strong>Creating and sharing a common starting point is key</strong>. A solid folder structure outside of Fireworks and a boilerplate will enable us to start quickly and to pick up a document where another team member left off, with minimal fuss and fewer headaches.</p>

### Creating a Boilerplate

The boilerplate should be the first file your team opens when it starts to design. It needs to be a living document, evolving as you improve your workflow and learn. Every team will have its own preferences, but here are some principles to guide you.

To get started, download the <strong><a title="Download: Sample Boilerplate" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79f10bec-7eb0-4fda-b741-a8ec9aecd4c2/projectboilerplate.v1">sample boilerplate</a></strong> (ZIP, 200 KB) that I created for this article.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4ea1e8d-fb65-40cc-849a-efe6e66967b5/02-image-boilerplate.png"><img title="Boilerplate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8debccd2-1125-49ec-8eeb-614503f09767/02-image-boilerplate-500.png" alt="Boilerplate" width="500" height="438" /></a><br>
<em>Your boilerplate should be a living document. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4ea1e8d-fb65-40cc-849a-efe6e66967b5/02-image-boilerplate.png">Large version</a>)</em>

The sample boilerplate (<code>ProjectBoilerplate_1140_v1.0.fw.png</code>) contains two pages: “1. Blank” and “2. Modular Scale.” I also took advantage of the “Share Layer to Pages…” feature in Fireworks to organize the file.</p>

### Structure and Layers

Fireworks layers (identifiable by a folder icon) may contain multiple objects, groups of objects and sublayers.

<img title="Fireworks layers panel." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0723dfc-bb9b-446f-ad29-c4f6f1446b5d/03-image-layerpanel.png" alt="Fireworks layers panel." width="500" height="540" /><br>
<em>Fireworks’ Layers panel. Every layer, sublayer and individual object (or group of objects) can be easily renamed.</em>

Keep the base structure high level and abstracted. In my experience, three layers, named “Foreground,” “Background” and “Guides” are usually more than enough. With fewer layers, you will enjoy the benefits of easy object ordering and direct selection. Photoshop users will feel uncomfortable as they try to confine each element to a separate layer group. Resist the urge! It will restrict your flow and efficiency.

Select any object on the canvas with the Selection (the <code>V</code> key is a shortcut) and Sub-selection (<code>A</code>) tools, and rearrange the stacking order easily with <code>Control/Command + up/down</code> or <code>Control/Command + Shift + up/down</code>. Manipulating objects in this way is incredibly quick. Note that an object may be arranged only within the current layer; so, the higher the number of layers, the more restricted an object’s movement will be. If you find yourself working with the Layers panel for specific actions, like naming, visibility and masking, then try to simplify your file structure by reducing the number of layers (perhaps by consolidating layers).</p>

### Labelling

That being said, don’t get (too) lazy. Labeling (or renaming) symbols and locking objects are still important. Because the naming of object groups is non-persistent, there is little point in going over the top.

Use the Pointer tool (i.e. the Direct Selection tool — <code>V</code>) and Subselection tool (<code>A</code>) to highlight the objects you’re working with and to work more quickly. The Pointer tool is usually used to select an individual object or a group of objects, while the Subselection tool will select an object in a particular group of objects.

When working with more complex objects, the Select Behind tool (press <code>V</code> twice) might be handy, too.

<strong>Important:</strong> Once a group of objects that you have named is ungrouped, the name will be lost, even if you regroup them. To help you work with groups, <a href="https://twitter.com/fwextensions">John Dunning</a> has created a smart <a href="https://johndunning.com/fireworks/about/GroupCommands">set of commands</a>. These commands enable you to add elements to existing groups, to easily ungroup objects without losing the attributes of the individual objects within the group, and more.</p>

### Grids

<strong>There are no hard and fast rules about grids</strong>. Different grids suit different briefs, technologies and situations. Test different systems, though, to get a quick start when you need one. Use both solid shapes and guides (<code>Control/Command + ;</code> or <code>View → Guides → Show Guides</code>) to define horizontal spacing and gutters. Some great Fireworks extensions for creating grids are covered in Ashish Bogawat’s article “<a href="https://www.smashingmagazine.com/2012/08/28/fireworks-extensions-for-better-workflow/">Optimizing the Design Workflow With Fireworks Extensions, Part 1</a>” (see the sections on “Grids Panel” and “Guides Panel”).</p>

### Common Viewport Dimensions

By c<strong>reating a small library of graphical silhouettes</strong> that match the dimensions of common monitor resolutions, you can quickly sense-check your layouts (and page folds) by toggling their visibility. The silhouettes can also help you frame content when designing long pages.</p>

### Baseline

Make a vertical baseline with the Grid tool (<code>Alt + Control/Command + G</code>), and turn on “Snap to Grid.” Now, when you resize elements, you’ll find that snapping their height to the baseline value becomes natural. This enables you not only to run the baseline down the canvas infinitely, but to control each one independently, viewing it separately or alongside the horizontal grid.</p>

### Modular and Typographic Scale

As part of creating a coherent design, you will be defining the space between page elements. Not only is this a necessary element of a design system, but it enables the design team to make informed decisions going forward.

Normally, these values settle into multiples of 10. Why? Because that is the number of pixels that the extended nudge command (<code>Shift + down/up/left/right</code>) moves in most of Adobe’s applications (Fireworks, Illustrator, Photoshop and so on). And, realistically speaking, who doesn’t prefer to deal with nice, clean round numbers? As convenient as that may be, though, it makes little sense. <strong>Defining a modular scale up front will help here</strong>. Like a musical scale, a modular scale is a prearranged set of harmonious proportions that run through the design, forming relationships between elements and pulling them into a balanced whole. Because the Web is primarily a medium for textual content, our scale should be driven by typography.

The website <a title="Modular Scale" href="https://modularscale.com/">Modular Scale</a> is incredibly useful both for defining a typographic scale and for gathering a set of proportions to define spacing and size. Use solid shapes in the proper dimensions as measurement guides to lay out the design.

Like all rules, these too may be broken. But by educating your design and development teams and by giving them logical, predictable rules to follow, they will find their own efficiencies and achieve wonderful things. If this piques your interest, you can find out more from the following resources:

*   “[More Perfect Typography](https://vimeo.com/17079380)” (video) Tim Brown, Build Conference
*   “[More Meaningful Typography](https://alistapart.com/article/more-meaningful-typography),” Tim Brown, A List Apart
*   “[Composing the New Canon: Music, Harmony, Proportion](https://24ways.org/2011/composing-the-new-canon/),” Owen Gregory, 24 Ways
*   “[R(a|ela)tional Design](https://blog.8thlight.com/billy-whited/2011/10/28/r-a-ela-tional-design.html),” Billy Whited, 8th Light blog

### Common Folder Structures and Naming Conventions

Any folder that is accessed and organized by many hands has the potential to get ugly, and fast. Agree on common folders and file-naming conventions for templates, assets, source PNGs and documents, and then stick to the system. The team should adhere to the rules, or at least try to <strong>maintain some level of discipline</strong>.

<strong>Tip:</strong> Try numbering your project’s folders to order them according to your agency’s convention or creative process. It also forces people to think about structure before offloading their files.

If you’re using Fireworks CS6, then you’re probably aware that the file names of artwork you save now include <code>.fw</code> before the <code>.png</code> file extension (i.e. <code>*.fw.png</code>). If you’re using an older version of Adobe Fireworks (CS5.1 or lower), get into the habit of manually following this convention. Not only does it immediately distinguish an editable PNG file from a regular (flattened) PNG, but it also fixes an old bug when opening Fireworks documents in Photoshop.</p>

### Version Control

Versioning software can be incredibly powerful for a team. It can certainly help to kill the <code>final_final_finalv8_last</code> schema that we all know and love. But popular technology such as <a href="https://en.wikipedia.org/wiki/Apache_Subversion">SVN</a> and <a href="https://en.wikipedia.org/wiki/Git_%28software%29">GIT</a> have their downsides. They are not developed with a designer’s needs at heart, instead treating our files like any other flat asset and preventing us from accessing individual pages. We also can’t visually browse the history of our artwork, and we often need a certain level of technical knowledge to use them comfortably.

But things are changing. Services such as <a title="Visit: LayerVault - Simple version control for designers" href="https://layervault.com/">LayerVault</a>, <a title="Visit: Pixelapse - Visual version control for designers" href="https://www.pixelapse.com/">Pixelapse</a> and <a title="Visit: Beanstalk App" href="https://beanstalkapp.com/features/collaboration">Beanstalk</a> (with its design preview) are now releasing the potential of version control. They keep things simple and streamlined, and they can show the evolution of a design through every save and comment (comments are tied to particular versions). If you have not considered version control, now is the time to introduce it into your workflow.

<img title="Visual version control" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce0a8458-6478-4f42-b999-f6f3ed28e3be/04-visual-version-control.png" alt="Visual version control" width="500" height="308" /><br>
<em>Visual version control</em>

## Style Guide-Powered Visuals

Like most graphic design apps, Fireworks was built from the ground up for individual users. Only one designer can open and work on a given file at any time. You will more than likely fall into the natural habit of separating a file into sections, saving individual PNGs that reflect the website’s architecture. This will enable other designers to work on the project at the same time.

There is a downside. When you split a project into separate files, you lose many of Fireworks’ advantages — namely, shared layers, master pages, symbols and more. This is where the Common Library saves us a lot of heartache by keeping things consistent across multiple documents.</p>

### Fireworks Library Panels

Fireworks has two library panels: the Document Library and the Common Library.

The <strong>Document Library</strong> panel (<code>Window → Document Library</code> or <code>Alt + F11</code>) lists any symbols that you create, import and use in the active document.

<img title="Fireworks Document Library panel." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba0ed2bb-7140-4a1b-9aad-10d20a2982a2/05-document-library.png" alt="Fireworks Document Library panel." width="500" height="459" /><br>
<em>The Document Library panel.</em>

The <strong>Common Library</strong> panel (<code>Window → Common Library</code> or <code>F7</code>) holds non-project symbols that have the possibility of being used across multiple projects or in more than one document.

<img title="Fireworks Common Library panel." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8fe6c5f-3357-49b3-ac8d-8786cbc92496/06-common-library.png" alt="Fireworks Common Library panel." width="500" height="481" /><br>
<em>The Common Library panel.</em>

The name of this panel — “Common Library” — sometimes causes confusion. The panel is simply a way to navigate and select symbols that are available across any (and all) Fireworks documents at any time (think of a common library of symbols). A symbol taken from the Common Library panel will appear in the Document Library panel (for that file) only after it has been selected and included from the Common Library.

Let’s make things a little clearer by creating a Common Library symbol. First, draw a simple shape and turn it into a symbol (<code>F8</code> or <code>Modify → Symbol → Convert to Symbol</code>).

<img title="Symbol creation dialogue." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8802620e-72e9-42f3-9b56-cde982980260/07-common-save.png" alt="Symbol creation dialogue." width="500" height="243" /><br>
<em>Creating a Common Library symbol.</em>

Name your symbol, and make sure to check the Common Library box (see the screenshot above).

You should now be presented with a “File Save…” dialog box. (Notice that the file name ends in <code>*.graphic.png</code>, which is how Fireworks defines a Common Library symbol, although the <code>graphic</code> part isn’t strictly necessary.) To include this symbol with the other assets available in the Common Library panel, we need to save it to a particular folder in the Fireworks config folder on your computer. Here are the exact paths for Fireworks CS6:

*   **Mac OS X** `~/Library/Application Support/Adobe/Fireworks CS6/Common Library/…`
*   **Windows Vista, 7, 8 and 8.1** `[system drive]:Users<USERNAME>AppDataRoamingAdobeFireworks CS6Common Library…`
*   **Windows XP** `[system drive]:Documents and Settings<USERNAME>Application DataAdobeFireworks CS6Common Library…`

Save the symbol, and then return to the Common Library panel. Hit “Refresh” in the bottom-right of the panel, and your new custom symbol should appear, ready to be used across any number of documents!

<img title="Common library (refresh button)." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98b7b0e1-65cb-42bf-b406-ff0478a6dc13/08-common-library-refresh-button.png" alt="Common library (refresh button)." width="500" height="136" /><br>
<em>The refresh button in the Common Library panel.</em>

On the face of it, this seems pretty useful. Yet it has some significant limitations for large teams:

*   Each symbol must exist as a separate Fireworks PNG file, which means it will show no context of the design around it.
*   There is no easy way to alter the location of the graphic files, which makes it difficult for a team to share and update the symbol files.

Let’s dig a little deeper.</p>

## How To Create A Fireworks Style Guide (Symbol Library)

Although there is little in the way of documentation, there is another way to implement a Common Library, one that is far more useful: by leveraging a single external library, which can feed any number of symbols to multiple PNGs, which, in turn, can be updated globally. If this gets you excited, just wait till I show you its potential to become more: a master document, <strong>a backbone for your project</strong>, all driven from your multi-paged style guide. Exciting times!

### The Configuration

From this point on, it will help to work with an established design, once you’ve agreed on the direction and have an initial framework in place.

Create a new Fireworks PNG file, which will act as a source file for your external library and style guide. Enlarge the canvas and save the file (for example, as <code>styleguide.fw.png</code>). If you’re part of a team, then save the file on a shared space or common server.</p>

### Adding Objects

Our empty document isn’t exactly fulfilling our hope of it being a global style guide. Let’s add some of our design elements.

Select a component from your artwork. Copy and paste it into your style guide. To turn this object into a shared asset, convert it into a symbol. And this time, leave the “Save to Common Library” box unchecked.

<strong>Reminder</strong>: If you add any symbols in the style guide, remember to leave the “Save to Common Library” box unchecked.

At this point, following a naming convention when creating the symbols would be useful. I like to use prefixes like <code>Global_</code>, <code>Form_</code> and <code>Btn_</code> to categorize symbols, but you can follow your own convention, of course. Prefixes makes it easier to find the right asset when you later need to import it back into your original artwork files.

<strong>Note:</strong> You can also split the document into a number of pages and add supporting graphics. It won’t affect how we import the symbols into our artwork.</p>

### Importing Symbols

Returning to the original file, open the Document Library panel (<code>F11</code>), and select “Import symbols” from the drop-down menu in the top-right of the Document Library panel.

<img title="Importing a Symbol" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acb361d7-0f3c-48a4-8316-3f678aa76d09/09-image-import.png" alt="Importing a Symbol" width="500" height="481" /><br>
<em>Importing a symbol into the current Fireworks PNG file.</em>

In the file browser, navigate and select the style guide library file that you have just saved (<code>styleguide.fw.png</code>). You will be presented with a list of all of the symbols available to be imported from your style guide. Select the symbols you need and click “Import.”

<img title="Updating a Symbol in Fireworks." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fced9cf-41ab-4040-97ce-f84715c5e3e0/10-importselect.png" alt="Updating a Symbol in Fireworks." width="500" height="404" /><br>
<em>Selecting a symbol (or symbols) to import</em>

Once they’re imported, you’ll find the symbols in the Document Library panel, with an <code>_imported</code> suffix. From this point on, you can treat them like any other symbols. You can drag and drop them into your current Fireworks artwork file, rename them and so on.</p>

### Summary: Creating a New External Library of Symbols

1.  Create a new Fireworks source file for your external library and style guide (for example, `styleguide.fw.png`).
2.  Copy the assets and symbols from the working design document(s) to the `styleguide.fw.png` file.
3.  Convert the assets and objects in the `styleguide.fw.png` file into symbols (if they are not already symbols).
4.  Save the `styleguide.fw.png` file in a location that will not change.
5.  Create a new working design file.
6.  Open the Document Library panel and choose “Import” from the context menu.
7.  Navigate to and select the `styleguide.fw.png` file, then open it.
8.  Choose the symbols that you want to import from the `styleguide.fw.png` file.
9.  Import the symbols, which will now appear in the Document Library. Done!

## Updating The Style Guide

We’ve created our style guide library (<code>styleguide.fw.png</code>), identified the elements to share between documents and started rolling out templates across multiple Fireworks PNG files. But wait! What happens when we need to change one of our components?

Remember that we’re feeding all of our artwork Fireworks PNGs from our external library, so any changes need to originate from there.

Open the style guide file, double-click the symbol that needs to be updated, apply the corrections, and resave the file. Next, return to your current artwork; in the Document Library panel, select the imported symbol(s) that you wish to update (holding <code>Shift</code> to select multiple items); and, from the drop-down menu in the top-right of the panel, select “Update…”

<img title="Updating a Symbol in Fireworks." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2108fce0-d8e9-4d27-90fa-97154b3a2c37/11-update.png" alt="Updating a Symbol in Fireworks." width="500" height="459" /><br>
<em>Updating a Symbol in Fireworks.</em>

Adobe Fireworks will look for the file that the symbol was originally imported from, automatically updating the relevant symbols in your artwork, regardless of how many pages it contains. Repeat this step for any Fireworks PNG artwork files that source symbols from the same library.

<strong>Note:</strong> For large files, the updating process might take some time. When the process is complete, Fireworks will display a success message.</p>

### Summary: Updating the External Library

1.  Amend the symbols you wish to change in your style guide file.
2.  Save the changes to the file.
3.  Navigate to and open your artwork file(s).
4.  Open the Document Library, and select the symbols you wish to update.
5.  Choose “Update…” from the context menu.
6.  Wait for the success message to appear.
7.  Repeat for all of the artwork files you wish to update.

<strong>Your style guide will now serve as a single reference library</strong>, accessible to everyone on the team, and detailing all of your designs components and development notes. It will also <strong>serve as a master symbol library</strong>, powering all of your artwork files.</p>

### Things to Be Aware Of

Nesting a symbol within another symbol is possible. With this method, both symbols will be imported, and the symbols will be displayed as separate items in the Document Library panel. But if you enable the “Select Unused Symbols…” option, it will highlight the nested symbol to be deleted, not recognizing that it’s being used in the active document canvas. So, I wouldn’t recommend nesting symbols.</p>

## Tips And Tricks

By keeping your source files clean, deleting unused symbols, grouping complex objects and doing regular housekeeping, you’ll keep Fireworks from getting too hungry for system resources. But if you find yourself running into problems and Fireworks slows down, there are few tricks worth knowing.</p>

### Pages (Un)limited

Multiple pages are a great feature in Fireworks but at times can give you some trouble.

There is no limit to the number of pages you can add to a document. (In his article “<a href="https://www.smashingmagazine.com/2012/07/03/interactive-prototypes-timesavers-adobe-fireworks/">Interactive Prototypes and Time-Savers With Adobe Fireworks</a>,” Trevor Kay mentions that he was able to use Fireworks PNG files with more than 150 pages.) But the more complex each page is, the more memory Fireworks will need.

Add too many pages, and there’s a good chance Fireworks will use too much RAM and slow down a bit (or even become unresponsive or crash). So, for complex designs, <strong>I recommend keeping Fireworks PNG files to under 25 pages</strong>. And if you mostly use lightweight simple vectors, you can push that number to 40. Staying within these limits will prevent frustration down the line.

<strong>Tip:</strong> While there is no upper limit to the number of pages you can add to a document, there is a small bug with page numbers when you create more than 100 pages. Adobe planned for only two digits in the page-number field; so, <code>98-99-100-101</code> becomes <code>98-99-10-10</code> and so on (i.e. the third digit cannot be displayed). Luckily, you would rarely need more than 100 pages.</p>

### Learn to Love Control/Command + S

This could be said of any application, but you should really learn to love <code>Control/Command + S</code> in Fireworks. Save your files regularly! On Mac OS X, if you forget to save regularly and Fireworks crashes for some reason, it will try to restore a backup copy of your Fireworks PNGs on the desktop — but don’t count on it.

If auto-saving is your thing, a number of great free extensions are available:

*   Auto Save This panel automatically saves the active document at an interval of your choosing (for example, every 5 or 10 minutes). An updated and improved version of it is also available, hosted on Project Phoenix.
*   [Auto Backup](https://www.isfireworksbetterthanphotoshop.com/web/extensions/Fireworks_AutoBackup_v1.0.air) This small AIR extension backs up all of your open documents, saving the copies in separate folder at an interval of your choosing. Sarthak Singhal has [more about the extension](https://blogs.adobe.com/sarthak/2008/12/auto_save_in_fireworks_cs3_cs4.html).</p>

### Temporarily Lock Complex Assets

Group and lock heavy, complex vector shapes. Locking assets in a document can speed up rendering of the canvas substantially. When you do it, Fireworks will “know” that you’re unable to select that thousand-pointed vector object and will free up a fair bit of resources as a result. You’d be surprised by how much better Fireworks performs once you master this simple tip.

Of course, once you need to edit an object again, you can unlock it at any time.</p>

### Unused Symbols

Throughout the creative process, things change and elements are added, expanded and removed. If you are doing things right, you will be turning a lot of these elements into symbols. But symbols hang around, taking up memory and filling the document library. Solution? Simple yet effective, you can <strong>clean up the garbage</strong> by selecting the context menu in the top-right of the Document Library panel and then hitting the “Select Unused Symbols” option. Fireworks will automatically highlight all symbols that are not in use on any pages in the document. Now, you can easily delete them. Reducing the overall file size is a good housekeeping practice.</p>

### Clear Your History

If you really find yourself in a tight spot, clear the undo history from the History panel’s context menu, saving the Fireworks PNG file immediately after.</p>

## Conclusion

Taking the time to create a broad foundation is a simple and effective way to enhance understanding among team members. It is an important first step to unlocking better collaboration and facilitating the future involvement of other designers. It also provides an opportunity for discussion and a point of focus for iterations on a design.

By exploiting Fireworks’ libraries to their full potential, we can <strong>improve our workflow and roll out our artwork more quickly</strong>. When we adapt the master symbol library into a global style guide, we create a single entity with multiple facets of use. In fact, the majority of the workflow we’ve covered here could theoretically be applied to any graphic design application that supports symbols in a way similar to Fireworks!

So, why not try implementing this for your next team project? And if you have any other collaboration tips or any questions, we’d love to hear them in the comments below!

{{< signature "mb, al, ml" >}}


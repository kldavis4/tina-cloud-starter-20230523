---
title: Interactive Prototypes And Time-Savers With Adobe Fireworks
slug: interactive-prototypes-timesavers-adobe-fireworks
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af093bdb-dce8-42db-95b6-9a0278a08fcc/music-player-small.png
date: 2012-07-03T11:53:09.000Z
author: trevor-kay
description: >-
  As interface designers, we’re often required to demonstrate the look and feel (and interactions) of the interfaces we design. We often begin with a series of flat images, and while these may be pixel perfect and show some amazing detail, they lack the **context** of the user experience.
categories:
  - Fireworks
  - Tutorials
  - Techniques
  - Prototyping
---
Without context, it would be difficult for your clients to understand the flow of an app or website in the way you originally planned it. The best way to introduce context is by adding <strong>interactivity</strong>. By providing an interactive prototype (or <strong>interactive mockup</strong>), your clients can play around with it to their hearts’ content to get an idea of how the app will work and to test the interactions.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Sketch, Illustrator or Fireworks?](https://www.smashingmagazine.com/2016/04/exploring-a-new-illustration-ui-design-app-gravit/)
*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [The Present And Future Of Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

The tool for creating interactive prototypes that wins hands down is Adobe Fireworks. Fireworks focuses on designing, prototyping and exporting for the Web, and it has a few hidden features that can easily add interaction to your prototypes and that will speed up your workflow.

{{% feature-panel %}}

But first, a little introduction. My name’s Trevor Kay and I’m a designer for <a href="https://exvo.com">Exvo</a>. At Exvo, we create a range of Web apps, from small widgets to full desktop-like Web apps. Using Adobe Fireworks has increased our efficiency in designing and maintaining our app prototypes. “How?”, you may ask. The answer is simple: <strong>pages</strong> and <strong>symbols</strong>: the best kept secrets in interface design!

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f126d78a-bcf1-4415-b2a2-7bada5fef2bd/banner.png" alt="" width="500" height="250" />

## Prototyping In Code Vs. Prototyping In Fireworks

There are many prototyping techniques, and the one you use will depend on your level of technical skill in coding, the speed at which you need to produce the prototype, and the level of visual fidelity needed. Lately, prototyping in the browser has become a popular trend. So, do we still need <strong>visual tools</strong> such as Photoshop and Fireworks, or can we start right in the browser?

The answer is, it depends! Sometimes <a title="Prototyping in Code (by Alex Morris)" href="https://www.netmagazine.com/features/prototyping-code">prototyping in code</a> is best, and sometimes designing (and prototyping) in the browser is <a title="Designing in the Browser is Not the Answer (by Andy Budd)" href="https://www.andybudd.com/archives/2012/03/designing_in_the_browser_is_not_the_answ/">certainly not the answer</a>.

When the prototype needs only simple interactivity, must be created quickly or requires detail and polish in its appearance, then Adobe Fireworks is the perfect tool because you don’t need to know any code to make a live prototype in very little time.

Why not Photoshop? While both Fireworks and Photoshop are excellent design tools (and often compared in UI design), Fireworks can take you one step further and produce a <strong>live prototype</strong> right from your design. In this article, we’ll cover this subject in more detail.

Fireworks is also very good when you need to create graphics for more complex prototypes that are created in development environments or even in the browser, because it can quickly slice, optimize and export graphic assets and can even help provide the CSS code for layout and text styles.

On the other hand, if you are proficient with code and need to make a prototype with complex interactivity, then prototyping in the browser might be the better option.

Now, let me show you why Fireworks works so well for me in both the prototyping and design phases of my projects!

## PNG, Pages, Master Pages

### Pages (and PNG)

Fireworks’ best friend is the PNG file format. Together, they achieve some pretty cool things, such as storing a <strong>multi-page document in one</strong> Fireworks PNG file (known as a Fw PNG). But I hear you say, “PNG is a flat file format!” While this is generally true, a <a title="More information about the PNG Format" href="https://secure.wikimedia.org/wikipedia/en/wiki/Portable_Network_Graphics">PNG</a> can also be extended to include various types of meta data. By using this ability to add meta data, Adobe Fireworks can store multiple pages in one PNG file, while maintaining complete editability within Fireworks itself (of vectors, bitmap objects, pages, layers, live filters and so on).

The benefit of this is two-fold. First, editable PNG files are usually very small, much smaller than comparable Photoshop PSD files. The actual difference in size can be stunning, as some designers report: one Fireworks PNG editable file with approximately 30 pages (equivalent to 30 separate PSD files or one PSD file containing 30 layer comps) can be as low as <a href="https://twitter.com/Rude/status/158638847880732673">9 MB</a> in size, while in some cases a three-page PSD file (with layer comps, which can partially simulate pages) can be as big as <a href="https://twitter.com/MattSanders/status/158728168386211840">100 MB</a> or more! A small size also means that Fireworks’ editable PNG files are easy to share and quick and simple to sync, even over a slow Internet connection.

Secondly, by storing all of the screens of your app’s prototype as pages in one file, nothing gets lost, and sending the file itself to coworkers and clients is easy.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3bbf6f3-57d1-454e-9788-0bd9787c0077/img11-b.png" alt="One PNG File vs Many PSD files" width="500" height="120" /><br>
<em>One Fw PNG file may contain many pages.</em>

Pages give you almost unlimited freedom. You can have many pages in one PNG file, and each page can have its own unique settings. You can also give each page its own name (just like you can rename layers and states). Naming your pages clearly will help you when you make the prototype interactive.

Pages actually enhance the layer model that you might already be familiar with from working with Photoshop, because each page in Fireworks is like a separate file: each page may have its own size, optimization settings, and unique content as well as shared content from other pages. Fireworks also uses layers and states.

Think of each page as a flat canvas for you to place objects on. You can move these objects around and reorder them easily, because you can <strong>interact with them directly</strong> on the canvas (just as you would with objects in Illustrator), and not through the Layers panel, which can speed up your workflow considerably!

### Master Page

Fireworks also has a master page feature, which is a template for all of the other pages in your prototype. Let’s say that the same toolbar appears on all pages of your app: simply place the toolbar on the master page, and it will appear on every page. This eliminates the need to constantly duplicate elements and can save you many hours. Creating a master page is easy: just right-click on any page in the Pages panel and select “Set as Master Page.”

If you need to update an element that appears on all pages, edit it on the master page and it will be automatically updated on all other pages!

Note that objects placed on the master page will appear at the <strong>same coordinates on all other pages</strong> connected to the master page. You cannot move or change the position of master-page objects on a per-page basis.

You can also <strong>share layers to pages</strong>, which is an alternative to using a master page. However, the master page <strong>always shares all of its layers to all pages</strong>, whereas sharing a layer from a page allows you to <strong>select which pages the contents of the shared layer should appear on</strong>.</p>

## Select Behind Tool, Subselection Tool, Symbols

Fireworks also provides two powerful tools to help you avoid touching the Layers panel (and work more efficiently): the Select Behind tool and the Subselection tool.

(A layer in Fireworks is a container for objects (much like a group in Photoshop), whereas a layer in Photoshop is an individual object.)

### Select Behind Tool

The Select Behind tool (located in the Tools panel or by pressing <code>V</code> twice) enables you to select a top-most object, and, with repeated clicking, select each of the elements directly beneath it in turn. This is yet another feature that helps you work more efficiently by not requiring you to awkwardly navigate the Layers panel, searching for an object either by name or tiny thumbnail.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec1b6392-8aad-4d73-b8dc-81570de6e5ae/fw-select-behind-tool.png" alt="Select Behind tool" width="500" height="270" /><br>
<em>In this example, five individual objects are placed on the canvas. With the Select Behind tool, selecting any object beneath another object is easy.</em>

### Subselection Tool

The Subselection tool (located in the Tools panel or by pressing <code>A</code>) enables you to select <strong>individual objects that are part of a group</strong>. This speeds things up because you won’t have to continually ungroup and regroup objects.

<img title="Sub- selection tool" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a01666c0-53a2-45b2-a829-99688c7eb6bc/fw-subselection-tool.png" alt="" width="500" height="270" /><br>
<em>In this example, five objects are grouped together. With the Subselection tool, selecting any object inside the group is easy.</em>

Once you get into the habit of working with pages and objects, you will feel a weight lift from your shoulders. The Select, Select Behind and Subselection tools make it a breeze to interact with the elements in your design!

See the article “<a href="https://www.adobe.com/devnet/fireworks/articles/pages_states_layers.html">Using Pages, States, and Layers in Fireworks CS4</a>” by David Hogue for an excellent explanation of how all three elements interact with each other in Adobe Fireworks.</p>

### Symbols

Symbols are another powerful feature in Fireworks, and they complement pages and master pages quite nicely. A symbol is a special graphic group that gives you “edit once, update everywhere” functionality, which saves a lot of time, too. Any object, layer or group of objects can be turned into a symbol simply by pressing <code>F8</code> or by going to <code>Modify → Symbol → Convert to Symbol</code> in the menu. (We’ll talk about symbols in detail later.)

Want to learn a bit more about symbols in Fireworks? Watch the useful video tutorial “The Power of Symbols in Adobe Fireworks” by <a href="https://twitter.com/rogie">Rogie King</a>.</p>

## How To Create Interactive Prototypes

All of the Fireworks workflow improvements mentioned so far are important on their own, but the real magic happens when you start making interactive prototypes. Fireworks was originally created by Macromedia as a tool <strong>targeted specifically at Web designers</strong>, and Adobe continues to develop Fireworks in this direction. It covers a lot of the things we need: pages, master pages, symbols, styles, bitmap- and vector-editing tools, and one of the best image exporting and compression features. But Fireworks has another feature that the Web has pretty much forgotten about: <a href="https://en.wikipedia.org/wiki/Image_map">image maps</a>.</p>

### Image Maps and Hotspots

Fireworks uses hotspots to generate image map areas. An image map encompasses multiple areas, which are referred to as “hotspots.” Adding a hotspot is as simple as selecting an object on the canvas, right-clicking on it and selecting “Insert Hotspot.” Alternatively, you can use the shortcut <code>Control/Command + Shift + U</code>, or in the menu go to Edit → Insert → Hotspot. You can also manually add hotspots with the Hotspot tool (found in the Tools panel).

Hotspots may be <strong>rectangular, circular or polygonal</strong>, but the best practice is to use rectangular hotspots because you can’t replicate circular or polygonal hotspots with normal links, which the final product will have. Also, if you decide to export the prototype to a PDF, <strong>only the rectangular hotspots will export</strong>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/151c70e3-c00c-4b07-ad32-0ea77c7a457c/1.-Multiple-Hotspots" alt="Two Hotspots in Fireworks" width="500" height="500" /><br>
<em>Two hotspots (notice the blue-colored overlay).</em>

Once added, a hotspot will appear as a blue-colored overlay above everything else. If you wish, you can change the color of a hotspot in the Properties panel. Hotspots exist in the Web Layer, which always resides at the top of all layers in the Layers panel.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f6813e6-1346-4458-9a0b-05273924621c/2.-Web-Layer" alt="Web Layer in the Layers panel" width="500" height="500" /><br>
<em>Inside the Web Layer.</em>

Note that when you export a prototype to HTML, the names that you gave to the pages in the Fireworks PNG document will become the names of the exported HTML files.</p>

### Manipulating Hotspots

When a hotspot is selected, the Properties panel will change and give you the option to add a link to the currently selected hotspot, as well as to specify how that link should open (in the same window or a new one, for example). The link could point to an external website (such as <code>https://www.smashingmagazine.com</code>) or to an internal Fireworks page. By linking to an internal page, you have taken the <strong>first step in making your prototype interactive</strong>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cfd9f04-20ba-478c-a48f-0c21afe45f93/3.-Properties-Panel" alt="Properties Panel" width="500" height="121" /><br>
<em>The Properties panel when a hotspot is selected.</em>

The selector for <code>link:</code> is divided into two sections, separated by a horizontal divider. Below the divider are the pages in the current Fireworks file; above the divider are all links currently in use in the open Fireworks document, and they may be either internal or external links.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91d909b1-fbaa-4a09-b223-751d47d3ff69/listhotspots.jpg"><img class="aligncenter size-full wp-image-112792" title="listhotspots" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91d909b1-fbaa-4a09-b223-751d47d3ff69/listhotspots.jpg" alt="" width="500" height="123" /></a><br>
<em>A list of URLs in the Properties panel.</em>

Now, all you have to do is go through the rest of the prototype and add the links. Remember, anything may be a linked hotspot. Need that button to open a new page? Done. Need that image in the slideshow to look like it progresses to the next image? Done. Achieving these effects really is that simple, and it will change the way you present your design prototypes. Also, you don’t have to worry if the names of your pages change; Fireworks will handle that for you as well and will <strong>automatically change all relevant hotspot links</strong> so that nothing becomes unlinked.</p>

### Export the Prototype

Once you have created all of your hotspots, how do you go about sending your clients the interactive prototype? Of course, you wouldn’t send them the editable Fw PNG file. While the PNG file contains all of your pages and links, it isn’t interactive. Clicking on a hotspot in Fireworks would not take you to the linked page; it would just select the hotspot. To make the prototype interactive, you need to export it to HTML files. These HTML files are what your clients can view and click through. They can be opened in any browser (Firefox, Safari, Chrome, Internet Explorer, Opera), so you don’t need to worry about compatibility.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0de2ee2e-1a4e-44fd-a311-b956ba41b349/4.-Export" alt="The Export Dialog in Fireworks" width="500" height="350" /><br>
<em>The Export dialog in Fireworks.</em>

When exporting an interactive prototype, use the default option of “Put images in Subfolder” to keep everything neat and organized. This has the added benefit of allowing you to easily send only the images to the client, if required. The exported images may be in any common image file format: PNG8, PNG24, PNG32, JPG, JPG Progressive, GIF. Note that the default format of the exported images is determined by their page’s optimization settings and then overridden by any slice’s individual optimization settings, which gives you a fair amount of control and flexibility.</p>

## Fireworks Pages: What Is Their Limit?

Pages allow for the efficient creation of prototypes, but what happens if they become <em>too</em> efficient?

### Handling a Fireworks PNG Document With Many Pages

I don’t know what the record is for a Fireworks document with the most pages in it, but I currently have one with over 150 pages, and it is still growing! While this is a complex file with a large number of objects, it shows how awesome Fireworks’ PNG file format is: the file’s actual size is only 16.6 MB!

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c47fb02-e9c6-493e-a1b7-ad203d2c45fb/img1.png" alt="Moar pages??" width="500" height="500" /><br>
<em>150 pages in one Fireworks PNG document? Possible!</em>

Why would anyone need a prototype that big? The simple answer is that I’m designing a complex app (Exvo’s Web app), and many intricate parts need to be covered by the prototype, so I’ve let it keep growing and growing.

While Fireworks can handle that many pages, it is certainly not recommended, for performance reasons. Try to keep your documents to fewer than 50 pages inside. Once you get past 50 pages, you might notice that Fireworks starts to use more RAM and opens and saves the document more slowly than usual. Performance also depends on each page’s canvas size, the number of objects and more, so keep the pages to a reasonable number to maintain an efficient file.</p>

### Pages Under Control: Splitting a Complex PNG File

Should our Fireworks PNG file become too large and unwieldy, how do we reduce the number of pages and optimize it? Because we are now relying on Fireworks’ ability to link pages and hotspots to create an interactive prototype, the hotspot links need to remain intact, even if we split the complex Fireworks PNG into several files. So, how do we proceed? Is it possible?

First, go through the prototype and make sure it is structured as defined sections. If the prototype is properly structured, we can split it up into smaller, more manageable pieces. To do this, we will need to count how many sections are in the prototype. If there are 10 main sections, for example, we would duplicate the file 10 times.

After that, we rename the duplicated files to match the sections of the prototype. Then, we open each of the duplicated prototype files and simply <strong>delete the pages that are irrelevant</strong> to that section; this will take some time and you have to be careful, but it is worth the effort. And… that’s it! You have now successfully split up your massive project file into more manageable pieces.

We also have to ensure that the smaller prototype files keep things together so that the exported HTML continues to link up correctly. To do this, we have to make sure that all of our top-level page names stay the same. While the relevant links will be changed within the single prototype file to make sure there is no unlinking, the other files will not update and will thus become unlinked. If you do opt to change the name of a top-level page, you would have to go through all of the other Fw PNGs and alter the hotspot links by hand.

If you do opt to split up a Fireworks PNG into multiple PNGs, then the master page and symbols will become unlinked. If you make a change to one PNG file, you will need to make the same change in all corresponding PNG files.

<img title="One prototype now Split into Several Smaller Ones" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ef1160e-6e61-4afc-b8ca-98a933916706/img10.png" alt="One prototype now Split into Several Smaller Ones" width="500" height="256" /><br>
<em>The prototype (Fw PNG) is now split into several smaller files.</em>

The massive prototype file we had is now split up into smaller pieces, so you will surely want to export it to be interactive. This is still possible and made easier if you still have the original large prototype file. Export the large prototype to a folder so that all pages are in the one folder. Keep this folder around because when you make changes to your smaller prototype files in the future, all you will have to do is export to this folder and overwrite the old files. Because all of our top-level links are still the same, everything will link up correctly <strong>as long as all of the exports are saved to the same folder</strong>.</p>

## Symbols

While pages facilitate file management and enable us to easily make interactive prototypes, Fireworks gives us other workflow improvements, too, such as symbols. Symbols originate in Flash and are an easy way to build a <strong>library of reusable elements</strong>. If UI design has one defining characteristic, it is reusable elements. Here are a few things that make symbols in Fireworks so powerful:

*   Once a symbol is created, you can save it to the Fireworks Common Library;
*   Fireworks symbols allow for intelligent scaling with the use of 9-slice scaling guides;
*   Symbols can be scaled as much as you like without losing quality.

Let’s take a close look at these features.</p>

### Reusability of Symbols

One of the best features of symbols in Fireworks is their reusability.

Symbols can be document-specific or available globally through the Common Library panel. Saving symbols to the Common Library means that no matter what document is open, all of your symbols will be available to use. The benefit is that you don’t have to recreate common UI elements across each prototype. If all of your apps have the same theme, then once your symbols have been created and saved to the Common Library, you will save yourself a lot of time by not having to redraw everything from scratch. This is an amazing time-saver because now all of your UI elements can be simply dragged and dropped into the current project!

The Document Library contains all of the symbols that have been used in the current document; these could include symbols selected from the Common Library, as well as symbols created specifically for that document. A benefit of the Document Library is that anyone who opens the Fireworks file will have access to all of the symbols being used in that document, including any symbols that were not created on their computer.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eccb28d9-7e0d-4137-bd1d-a55c82769a07/5.-Symbol-Library" alt="Symbol libraries" width="500" height="249" /><br>
<em>The Fireworks libraries of symbols: Common Library (left) and Document Library (right).</em>

### 9-Slice Scaling Guides

Symbols may also include 9-slice scaling guides. These guides make it possible for you to define how a symbol will scale intelligently in all directions, and they reduce the number of times you need to manually edit vector points in order to change the object’s size. You can learn more about 9-slice scaling in a <a title="9-slice scaling in Fireworks (by Jim Babbage)" href="https://tv.adobe.com/watch/learn-fireworks-cs4/scale-objects-with-9slice-scaling/">video tutorial by Jim Babbage</a> and in a <a title="Improved 9-slice scaling in Fireworks (by Sarthak Singhal)" href="https://www.adobe.com/devnet/fireworks/articles/9-slice_scaling.html">detailed article by Sarthak Singhal</a>.

The 9-slice scaling guides are optional and are not included by default. You can decide whether to use them based on the type of object that you’re converting to a symbol. To make things even easier, Fireworks also gives you the option to activate or deactivate the guides for any existing symbol.

When you edit a symbol for which the 9-slice scaling guides are enabled, Fireworks presents you with the graphic for the symbol as well as four guides overlaid on top. These guides effectively <strong>divide the symbol into nine slices</strong>, with each determining how a particular part of the symbol will transform when scaled:

1.  Corner slices All corners will not resize and will stay the same size no matter what. This is very effective for buttons made out of rounded rectangles.
2.  Left and right slices These two slices will transform vertically but not horizontally.
3.  Top and bottom slices These two slices will transform horizontally but not vertically.
4.  Center slice This slice will transform both horizontally and vertically.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45933330-924b-4e0d-b9f5-d4ab8af9d602/6.-Nine-Slice-Guides" alt="A Symbol in Symbol-editing mode" width="500" height="182" /><br>
<em>A Symbol in symbol-editing mode.</em>

The ability to reuse and resize symbols without losing quality is what makes them so powerful. You will have a common set of elements ready to be dragged and dropped into your prototypes. The amount of time this alone will save you is amazing.

Just as Fireworks uses PNG as its primary file format, symbols are also stored as PNG files. All Common Library symbols can be found in the following location:

*   Mac OS X `~/Library/Application Support/Adobe/Fireworks CS5/Common Library`
*   Windows XP `C:Documents and Settings*username*Application DataAdobeFireworks CS5Common Library`
*   Windows Vista and 7 `C:Users*username*AppDataRoamingAdobeFireworks CS5Common Library`

(If you are using a different version of Fireworks, just replace “CS5” with the version you’re using.)

If you ever need to migrate to a new machine or give a coworker access to your symbols, all you need to do is copy your symbols to the new location and Fireworks will recognize them instantly!

<img title="The Common Library" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5979431-4b7c-4087-b355-b846b8582e67/img8.png" alt="The Common Library" width="500" height="394" /><br>
<em>The Common Library in Fireworks.</em>

## Download A Sample Fireworks PNG File

Want to jump right into pages and symbols and easily make an interactive prototype with <a title="Adobe Fireworks (download a trial from adobe.com)" href="https://www.adobe.com/products/fireworks.html">Fireworks</a>? To help you, we have created a three-page prototype of an iPhone music player for you to download. You can open the <code>music-player-demo.fw.png</code> file in Fireworks and export it to a small interactive prototype.

*   [Download the Fireworks music player prototype](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5de7b01-c588-4ff4-97c6-5a9420bc8fd8/music-player-demo.zip) (ZIP, 4.0 MB)

<a title="Download the Music Player prototype in Fireworks PNG format (ZIP, 4 MB)" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5de7b01-c588-4ff4-97c6-5a9420bc8fd8/music-player-demo.zip"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3f69a20-197e-42ba-97dd-6c91df69c571/music-player-screen.jpg" alt="Three-page demo prototype for download" /></a>

The sample Fireworks PNG not only will show you how hotspot links and pages work, but will give you a chance to play around with symbols. To export the Fireworks PNG as “HTML and Images,” just go to <code>File → Export</code>. Set the “Export” type to “HTML and Images” and set “Pages” to “All,” and then select where on your computer to export it to. After the export, open one of the HTML files in a browser and try interacting with the prototype, navigating through the app by clicking the links.

When you’re testing the file, make sure the following panels are open in Fireworks: Pages, Layers, Document Library and Properties. Feel free to experiment with the prototype, add more hotspots and pages, and navigate around to see how the file is organized and how the pages inside are linked together. (Seeing which parts will be clickable once they’re exported is easy because the hotspots are marked in blue.) The file also makes use of symbols (stored in the PNG file itself — see the Document Library panel), shared layers and a master page.</p>

## Further Reading

*   “[Interaction Design and Rapid Prototyping With Fireworks](https://www.adobe.com/devnet/fireworks/articles/atv_fw_interaction_design.html),” David Hogue, Adobe Developer Connection
*   “[Rapid Interactive Prototyping With HTML, CSS, and JavaScript (Using Fireworks and Dreamweaver)](https://www.adobe.com/devnet/fireworks/articles/rapid_interactive_prototyping.html),” Dave Hogue and Mariano Ferrario, Adobe Developer Connection
*   “[Prototyping in Code](https://www.netmagazine.com/features/prototyping-code),” Alex Morris, Mark Boulton Design
*   “[Designing in the Browser Is Not the Answer](https://www.andybudd.com/archives/2012/03/designing_in_the_browser_is_not_the_answ/),” Andy Budd
*   “[Pages, Layers and States in Adobe Fireworks](https://www.adobe.com/devnet/fireworks/articles/pages_states_layers.html),” Dave Hogue, Adobe Developer Connection
*   “[Scale Objects With 9-Slice Scaling in Fireworks](https://tv.adobe.com/watch/learn-fireworks-cs4/scale-objects-with-9slice-scaling/),” Jim Babbage, Adobe TV
*   “[Improved 9-Slice Scaling in Fireworks](https://www.adobe.com/devnet/fireworks/articles/9-slice_scaling.html),” Sarthak Singhal, Adobe Developer Connection
*   “[Create Interactive Prototypes With Adobe Fireworks](https://www.smashingmagazine.com/2012/06/25/create-interactive-prototypes-with-adobe-fireworks/),” André Reinegger
*   “[Refining Your Design In Adobe Fireworks](https://www.smashingmagazine.com/2012/05/07/refining-designs-adobe-fireworks/),” Benjamin De Cock
*   “[Why Your Links Should Never Say “Click Here”](https://www.smashingmagazine.com/2012/06/20/links-should-never-say-click-here/),” Anthony T

<em>(al) (jc)</em>


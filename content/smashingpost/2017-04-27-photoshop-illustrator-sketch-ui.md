---
title: 'Moving From Photoshop And Illustrator To Sketch: A Few Tips For UI Designers'
slug: photoshop-illustrator-sketch-ui
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a98c9f4d-69b6-4ed0-80d0-e78fb0a4928c/framer-500w-opt.png
date: 2017-04-27T19:22:49.000Z
author: lachezarpetkov
description: >-
  I’ve been a long time Photoshop and Illustrator user. **Both programs are
  really useful and powerful**, and they’ll remain a key part of any digital
  artist’s or designer’s toolset, including mine. However, for all user
  interface, web and icon design workflows, I recently converted to
  [Sketch](https://www.smashingmagazine.com/sketch-handbook/). Here is why.

  While Photoshop is awesome at what it does, defining what it is might not be
  so easy anymore. I remember watching a storyboarding tutorial by Massive
  Black’s El Coro (unfortunately, it doesn’t seem to be available for sale
  anymore). In it, he says that 17 or so years ago, Adobe had no idea that
  digital artists were using Photoshop to digitally paint pictures! So, it had
  to catch up with its own user base by adding more — you guessed it — painting
  features.
categories:
  - Graphics
  - Workflow
  - Plugins
  - Sketch
---
While Photoshop is awesome at what it does, defining what it is might not be so easy anymore. I remember watching a [storyboarding tutorial](https://www.youtube.com/watch?v=uXg2reSswpA) by [Massive Black](https://massiveblack.com/)’s [El Coro](https://coro36ink.com/) (unfortunately, it doesn’t seem to be available for sale anymore). In it, he says that 17 or so years ago, Adobe had no idea that digital artists were using Photoshop to digitally paint pictures! So, it had to catch up with its own user base by adding more — you guessed it — painting features.

I feel that the same kind of thing happened a bit later with Photoshop and user interface design. It was the only robust graphics tool that people knew or had access to some years ago, so they started using it for UI design, as well as for illustration and [photo editing](https://www.google.com/search?q=photoshop+tutorials+for+editing+photos).</p>

<figure><a href="https://twitter.com/smashingmag/status/839750650233749505"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a1c2a13-8e99-4c5a-a228-4095ff154f97/what-tool-photoshop-preview-opt.png" width="750" height="" alt="" /></a><figcaption>Photoshop is still <a href="https://twitter.com/smashingmag/status/839750650233749505">widely used</a> as a tool for UI design, even if Sketch has taken the lead. (<a href="https://twitter.com/smashingmag/status/839750650233749505">Poll source</a>: <a href="https://twitter.com/smashingmag">@smashingmag</a>.)</figcaption></figure>

Then, as a result, Adobe started adding more and more features targeted at interface designers, even though the program was initially intended and designed for a completely different purpose.

{{% feature-panel %}}

## Switching To Illustrator: The Annoyances

### From Photoshop to Illustrator

Because using Photoshop for user interface design is, in my view, a needlessly painful experience (and [I am not alone](https://hackingui.com/sketch-design/a-year-using-sketch/) in this view), I first tried switching to Illustrator. Illustrator made things much better for me for a few reasons: Dealing with a lot of artboards is easier; I can select any object on any layer or any artboard with a single click, without ever having to hunt down layer names in the Layers panel; also, exporting assets in the latest Creative Cloud versions has been greatly improved; and so on.

Illustrator’s vector nature has a lot of advantages for designing icons and scalable interfaces, and using it I find it much easier and quicker to draw, modify and expand shapes. It can export my assets to SVG, and it gives me control over the SVG output code. Illustrator also feels more appropriate for this type of work because the paradigm of working with vector graphics is very similar to working with web technologies (containers, CSS styles, document structure, vector fonts). After all, web browsers are essentially vector-rendering engines.</p>

### Problems With Illustrator

However, I hit some silly problems every now and again. For example, previewing a design on a mobile device — there is simply no software that allows me to do this directly. Photoshop has [Device Preview](https://helpx.adobe.com/photoshop/how-to/live-preview-mobile-device.html), but it’s for iOS only, and there is no such tool for Illustrator. So, I had to use a third-party tool named [The Preview](https://play.google.com/store/apps/details?id=com.spreadsong.pspreview&hl=en). And every time I wanted to device-preview a screen, I had to copy my Illustrator artboard into Photoshop, scale it up (I always work in [mdpi](https://sebastien-gabriel.com/designers-guide-to-dpi/), and my devices are xhdpi or xxhdpi), and then run The Preview on my device — which sometimes refused to work and which doesn’t support scrolling.

Also, even with the [addition of CC libraries](https://helpx.adobe.com/creative-cloud/how-to/creative-cloud-libraries.html) and with Illustrator’s dynamic symbols feature, some tasks remained kind of annoying or tedious, like using a large set of icons. In Illustrator, there is no simple and straightforward way to quickly add a premade icon and to quickly override its size or color (without creating a bunch of duplicates).</p>

### Specifying My Files

[Specifying my files](https://www.smashingmagazine.com/2014/10/front-end-development-ode-to-specifications/) was a problem for me, too. It is, of course, my job to provide developers with a well-specified design. This helps to prevent questions such as “What is the distance between this element and that element?” and “What font size is this text object?”

Photoshop has a whole bunch of specification tools, but I’ve never used them. There aren’t that many for Illustrator, and all have their drawbacks. Arguably, the most feature-full is [Specctr](https://www.smashingmagazine.com/2013/11/specctr-an-adobe-illustrator-plugin-freebie/), but I had technical difficulties running it (also, it has no dp as a measuring unit). So, I ended up using a slightly modified version of the Illustrator [Specify script](https://github.com/adamdehaven/Specify) to measure the sizes of and distances between objects for design specifications. However, as great as that script is, specifying my designs with it was still rather tedious and time-consuming.</p>

### My Deal-Breaker

While these problems are arguably annoying and slow down my work, they aren’t things that I couldn’t get used to and overcome. However, the two Android projects I’m currently working on are a file manager and an email client — which means that a lot of my high-fidelity mockups are full of lists, avatars, file icons, file sizes and other types of data.

To further complicate the situation, both projects come with a light and a dark UI theme. Also, a lot of my designs need to be tailored to both phones and tablets in both landscape and portrait modes. This means a lot of copying and pasting, symbol-editing, typing, selecting and deselecting, and so on.</p>

### Illustrator’s Dynamic Symbols

Admittedly, Illustrator’s symbols and libraries features can be handy and save me some manual labor. But they can be quite limited — for example, one can’t have multiple iterations of the same symbol or of the same library graphic. For me, this meant that I couldn’t use the same symbol (say, an icon or a button) in both my dark and light theme mockups because I couldn’t change its color without modifying the symbol graphic itself. The same goes for the library feature.</p>

### Problems With Data-Driven Design in Illustrator

Now, the most efficient way for me to avoid having to copy and paste is to have all text entries — see “Subject,” “From,” “Content Preview” and “Time” in the example below — as variables and to dynamically load predefined strings of data for each entry.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3edebf4-9c90-4c04-a938-0dd59bfec544/strings-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3edebf4-9c90-4c04-a938-0dd59bfec544/strings-preview-opt.png" width="670" height="" alt="" /></a><figcaption>These are the four strings of data for my email app’s Inbox mockup.</figcaption></figure>

This is, in fact, [possible in Illustrator](https://www.youtube.com/watch?v=eCBrK8tZAXQ&feature=youtu.be). I could create my spreadsheet with data, import it in Illustrator with the help of [a plugin](https://github.com/Silly-V/Adobe-Illustrator/blob/master/Variable%20Importer/VariableImporter.jsx) and be ready… with one huge caveat, however: There can be only **one variable entry** per iteration of the file!

This makes the feature perfect for something like a business-card project, where you’d want to keep the design the same and only change some text (such as the name and phone number). When you export the final PDF files, you’d simply iterate a hundred times through a spreadsheet of data to get a hundred different names and phone numbers. This would produce a hundred nice, corporate business cards for a hundred happy employees.

However, this behavior renders Illustrator’s data features pretty much useless to me, because I need to populate a lot of of text entries **simultaneously**, each with a **different string**, on multiple artboards, and so on.</p>

### A Potential Creative Cloud Solution?

If you must stay in the Adobe Creative Cloud realm, or if switching to a Mac is not an option, there still might be a solution. Adobe’s new tool, [Adobe XD](https://www.adobe.com/products/experience-design.html), handles [working with dynamic data](https://medium.com/@anirudhs/project-comet-designing-with-real-data-959beccb5c1a) fairly well. However, because it’s a new tool, it can feel limited in other ways. Also, Adobe XD’s Windows version currently lags behind the Mac one.</p>

## The Solution: Switching To Mac And Sketch

Because of all of the little (and big) issues mentioned, I started to search for a better solution. So, I thought about the Sketch app.

I hadn’t had a Mac for the previous three years, and when I did have one I’d never used Sketch on it. However, I missed the operating system, and it always bothered me that Mac users always get the best software gadgets! I did plenty of research on Sketch and on other tools such as Origami, and I got tired of hacking my way through [Framer](https://framer.com/) on Windows.

So, a couple of months ago, I decided to switch back to a Mac — both at home and at work.</p>

### Enter Sketch!

Sketch cures a lot of my pains — and not just by itself, but also with the help of its vast plugin ecosystem. Compared to Illustrator and Photoshop, Sketch is focused on the needs of the UI and icon designer. And, unlike Photoshop, Sketch was made [for UI design](https://blog.mengto.com/sketch-vs-photoshop/) right from the start; UI wasn’t an afterthought.

Of course, it’s not perfect. I miss things, such as Illustrator’s Knife tool when I draw illustrations; it lacks some handy filters; there is no basic Photoshop Layer Styles alternative; and so on. But that’s kind of beside the point. Sketch doesn’t seem to be aimed at artists doing complex vector illustrations, and it only covers the very basics of raster editing.

At first, if you’ve been using Photoshop for all of your design tasks so far, you’ll be in awe when you see how you’re able to directly select any piece of graphic on any layer with just a couple of clicks or less. And if you (like me) have been also using Illustrator, then you’ll be impressed by Sketch’s more powerful Symbols feature, better artboard organization and more intuitive interface.

Measuring distances and objects is so much fun in Sketch! I just hold the `Alt` key, mouse over the objects on the canvas, and I’m able to see all margins, paddings and sizes. I can adjust them on the fly and just have fun, while keeping my designs really neat.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e41963e-c741-4ce5-bc77-dcdfceb898dc/hovering-animated.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e41963e-c741-4ce5-bc77-dcdfceb898dc/hovering-animated.gif" width="480" height="" alt="" /></a><figcaption>All margins, paddings and sizes seen at a glance</figcaption></figure>

The little things are also important! One example is the ability to do simple math in an object property’s input field in the [Inspector panel](https://sketchapp.com/learn/documentation/the-interface/inspector/). I can scale a rectangle object by typing something like `12 / 3` or `2 + 2`. Very helpful sometimes.</p>

## InVision’s Craft Plugins

I’ve already mentioned Sketch’s plugins. And [InVision’s Craft plugins](https://www.smashingmagazine.com/2017/02/design-with-real-data-sketch-using-craft-plugin/) are probably among the most powerful and useful.

Craft actually solved my aforementioned problem of **loading data** into my designs. For the email app I’m working on, I can now create a list of (actual or fictitious) email addresses, subjects, content strings and more in a spreadsheet. I only need to make sure that every spreadsheet column’s first entry serves as the title (for example, “Content”).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53817cc4-98be-4a4f-8807-4bd8d526e9a3/spreadsheet-titles-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26d0f9c8-fb6c-4bc6-8c56-9b6e56f8f72c/spreadsheet-titles-780w-opt.png" width="780" height="69" alt="" /></a><figcaption>The first row of my document (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53817cc4-98be-4a4f-8807-4bd8d526e9a3/spreadsheet-titles-large-opt.png">View large version</a>)</figcaption></figure>

Unfortunately, the Craft plugin doesn’t support importing data in XLS, CSV or ODS format. It only supports JSON (a file format specifically for exchanging data). I use Google Spreadsheets, and because it doesn’t support direct exporting to JSON, I have to first save to a CSV file, then use an online CSV-to-JSON converter to get the format I need.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05b7c2e3-3863-463f-9945-ac8c95f85358/spreadsheet-save-as-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e50a8914-ba30-4c07-8914-bd44a5961cb2/spreadsheet-save-as-780w-opt.png" width="780" height="528" alt="" /></a><figcaption>Download your spreadsheet as a comma-separated values (CSV) document. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05b7c2e3-3863-463f-9945-ac8c95f85358/spreadsheet-save-as-large-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d054044c-2378-43d5-931d-502162ae71fb/csv-json-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44f231e1-a196-48a6-853f-e05243fcaf2e/csv-json-780w-opt.png" width="780" height="346" alt="Here’s how CSV looks like, compared to JSON" /></a><figcaption>Here’s how CSV looks compared to JSON. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d054044c-2378-43d5-931d-502162ae71fb/csv-json-large-opt.png">View large version</a>)</figcaption></figure>

Now, I only have to save the JSON file on my computer and drag it into Craft’s Data panel.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaf87682-c938-4037-99b5-79cb235596f1/import-json-animated.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaf87682-c938-4037-99b5-79cb235596f1/import-json-animated.gif" width="780" height="480" alt="" /></a><figcaption>Importing my JSON file</figcaption></figure>

The entire conversion process might sound complicated, but it only takes a couple of minutes.

Now, I only need to tell Craft which Sketch text field corresponds to which JSON string. Then, I use the duplicate functionality to make as many duplicate entries as I want:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00ecb077-f331-4f03-a0cf-59f61190cc47/populate-animated.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00ecb077-f331-4f03-a0cf-59f61190cc47/populate-animated.gif" width="480" height="" alt="" /></a><figcaption>Assigning and duplicating data strings</figcaption></figure>

As for those avatars with letters inside, I don’t need to bother with a spreadsheet. Here’s what I did instead: I [used a nested symbol](https://www.youtube.com/watch?v=uXg2reSswpA) to tint each avatar with a different color. And Sketch’s overrides feature does the job of dynamically replacing each letter!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ba22582-4564-409c-b807-0aeeac519fa5/overrides-animated.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ba22582-4564-409c-b807-0aeeac519fa5/overrides-animated.gif" width="480" height="" alt="" /></a><figcaption>Sketch’s native overrides feature is what makes its dynamic symbols <a href="https://medium.com/ux-power-tools/designing-a-top-nav-in-one-symbol-295b8b0a05a5">so powerful</a>.</figcaption></figure>

This approach works well for expanding phone designs into tablet designs because I only need to adjust Sketch’s text fields.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6d94743-d59a-438c-9b7e-59337b5097e5/resizing-animated.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6d94743-d59a-438c-9b7e-59337b5097e5/resizing-animated.gif" width="640" height="" alt="" /></a><figcaption>Your data is there! Simply adjust the width of the text fields according to your needs.</figcaption></figure>

## My Other Favorite Sketch Plugins

It’s not only about the Craft plugin, of course. I rely on quite a few plugins in my daily work, and all of them help me to be more efficient.</p>

### Sketch Style Inventory Plugin

As mentioned, the projects I’m currently involved in come with a light and a dark theme. Having to provide designs for both themes and for each screen can be tedious and time-consuming. However, using Sketch’s [Style Inventory](https://github.com/getflourish/Sketch-Style-Inventory) plugin, I can select all items in all of my artboards by name or by current color or by another property, and then batch-adjust them as I like.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54d0836d-2534-46b5-95f6-5609750620e9/sketch-inventory-menu-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d795c6c-ab5a-4448-ae94-df06f327b296/sketch-inventory-menu-780w-opt.png" width="780" height="279" alt="" /></a><figcaption>Batch-selecting design elements is super-easy with the Sketch Style Inventory plugin. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54d0836d-2534-46b5-95f6-5609750620e9/sketch-inventory-menu-large-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d14216c-e7d5-4fb3-819b-8878cbcd3b08/dark-theme-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d14216c-e7d5-4fb3-819b-8878cbcd3b08/dark-theme-preview-opt.png" alt="" /></a><figcaption>The dark theme mockup with the exact same data.</figcaption></figure>

Thus, I can recreate my designs for different themes in just a minute!

### Sketch Icon Font Plugin

Adding a Material icon (or an icon from another font icon set) is a no-brainer with the Sketch [Icon Font plugin](https://github.com/keremciu/sketch-iconfont). It takes only seconds! I don’t have to leave Sketch, and the icon can be scaled, colored and edited in any way I like.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c6d4072-78f5-4057-86e1-3f0120f02953/sketch-icon-plugin-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5d53822-1429-4e27-bf4f-b17f6b340477/sketch-icon-plugin-780w-opt.png" width="780" height="575" alt="" /></a><figcaption>The entire Material icon set is at my disposal with just a couple of clicks. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c6d4072-78f5-4057-86e1-3f0120f02953/sketch-icon-plugin-large-opt.png">View large version</a>)</figcaption></figure>

### Skala Preview Plugin

Sketch includes previewing functionality called [Mirror](https://www.sketchapp.com/learn/documentation/mirror/mirror/). However, it works only with iOS devices and web browsers (for web design mockups). [Skala Preview](https://bjango.com/mac/skalapreview/), on the other hand, provides excellent device-previewing functionality and (what is most important to me at the moment) support for Android devices.

Skala by itself does not support Sketch directly, but there is the Sketch [Preview](https://github.com/marcisme/sketch-preview) plugin to help with that. It’s reliable and has never crashed for me, but every now and again I have connection issues. What I love about it is the simple scrolling functionality that The Preview and Photoshop combination lacks.</p>

### Swatches Plugin

Sketch has functionality similar to Photoshop’s and Illustrator’s swatches. It’s called global and document colors, but it has some minor limitations. For example, the palette colors can’t have names; they can’t be organized in subfolders; and no commonly used palettes come preloaded in Sketch. Also, I think the margins around the color squares are a bit too wide, so a large palette might not fit comfortably in there.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f957ef44-4b7a-47ac-881d-2527298f6b88/sketch-palette-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f957ef44-4b7a-47ac-881d-2527298f6b88/sketch-palette-preview-opt.png" width="420" height="" alt="" /></a><figcaption>Sketch’s native palette isn’t that comfy for some use cases.</figcaption></figure>

The [Swatches](https://github.com/Ashung/Sketch_Swatches) plugin improves the situation. It comes preloaded with plenty of standard palettes, such as the Material palette, Pantone and others. I can mouse over a color to see its name, and I can apply it as a fill or stroke color or copy its HEX value with just a click.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b4b7285-9fe5-4c84-9882-37df48357a8e/swatches-plugin-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b4b7285-9fe5-4c84-9882-37df48357a8e/swatches-plugin-preview-opt.png" width="476" height="" alt="" /></a><figcaption>The Swatches plugin with the Material design palette</figcaption></figure>

### Zeplin Plugin

Last, but not least, I need plugins to create design specifications. One of them is Zeplin.

[Zeplin](https://zeplin.io/) is a cloud-based toolset for creating automated design specifications and for designer-developer collaboration. Its main feature is that it reads and parses all of your Sketch artboards in a file, uploads them to a web server, and provides a web interface for other collaborators to view them. Once your artboards have been crunched and uploaded, anyone who checks them out on a computer can click and hover about and see all margins, paddings, fonts, HEX codes and other properties of all objects in the design.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5aaa694c-f1ac-4b5c-bcd5-4dab5ca0150e/zeplin-animated.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5aaa694c-f1ac-4b5c-bcd5-4dab5ca0150e/zeplin-animated.gif" width="640" height="" alt="" /></a><figcaption>Zeplin plugin in action</figcaption></figure>

This approach to design specifications is quite helpful because it saves the designer from the time-consuming task of doing specifications manually. It could also reduce confusion and misunderstanding with the development team.

Other features of Zeplin that I find quite helpful are: organization for multiple projects, screen versioning (kind of like [Git](https://www.atlassian.com/git/tutorials/what-is-git) but designed for screen mockups), project style guidelines, and optimized asset exporting.

A potential downside of Zeplin is that some companies may have concerns over its cloud-based nature.</p>

### Sketch Measure Plugin

Zeplin is good for managing and working on entire projects that contain many screens. However, if you’re looking for a simpler (and free) solution, you may want to choose something else: Sketch [Measure](https://github.com/utom/sketch-measure).

Using this plugin, you can specify your own design document or let the plugin do the dirty work. Like Zeplin, it will export a web page with your design on it, together with an interactive specification overlay! Unlike Zeplin, everything is done locally, but you won’t have the extra project-management tools at your disposal.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f18c5f17-93b5-4d81-a49c-49967ac71cef/sketch-measure-animated.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f18c5f17-93b5-4d81-a49c-49967ac71cef/sketch-measure-animated.gif" width="480" height="" alt="" /></a><figcaption>Sketch Measure plugin in action</figcaption></figure>

Compress the generated files to ZIP, give them to your developer, and you might save yourself quite a few hours of work!

### Managing My Sketch Plugins

With so many plugins, one needs a reliable way to find, install, manage and update them. Sketch’s built-in manager only lists the plugins that are already available, allowing the user to enable and disable each one. This can be useful when you want to debug a plugin that’s acting up, but having to manually search for and install new plugins can be a hassle.

The best solution to this problem is probably the [Sketch Toolbox](https://sketchtoolbox.com/) app, a simple yet very useful tool. It allows you to install (and uninstall) almost any Sketch plugin out there with a single click. Highly recommended!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfc82e3d-b56b-4556-b3f7-6a023fea5e35/sketch-toolbox-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e809d289-5674-4fb5-9a08-8a05029a18bb/sketch-toolbox-780w-opt.png" width="780" height="793" alt="Sketch Toolbox’s long list of available plugins." /></a><figcaption>Sketch Toolbox’s long list of available plugins (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfc82e3d-b56b-4556-b3f7-6a023fea5e35/sketch-toolbox-large-opt.png">View large version</a>)</figcaption></figure>

## Prototyping And Framer Integration

Sometimes, static mockups don’t quite cut it if you need to communicate a more complex idea to developers, particularly for motion design and microinteractions. Some very good [tools for interactive prototyping](https://www.smashingmagazine.com/2016/09/choosing-the-right-prototyping-tool/) are out there, and each takes a different approach to the task.

My prototyping tool of choice is [Framer](https://framer.com/).</p>

### Framer

Framer takes the programming approach: The designer is required to program their prototype in [CoffeeScript](https://coffeescript.org/). The prototype is immediately previewable in Framer Studio and can also be viewed on actual devices or in the browser.

I personally like the coding approach to creating prototypes, despite the steep learning curve. It will pay off eventually, because programming gives me a lot of control, and it also forces me to think a bit like a developer, which can be an advantage.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04543bc9-157b-4197-9408-412c92f1b89f/framer-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef1a6758-a495-421e-b2f3-88ca5e1c18eb/framer-780w-opt.png" width="780" height="546" alt="" /></a><figcaption>Meet Framer. On the left side is the code editor; on the right is my preview; and in the middle is the layer structure of the prototype (or of the imported Sketch file). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04543bc9-157b-4197-9408-412c92f1b89f/framer-large-opt.png">View large version</a>)</figcaption></figure>

### Using Framer and Sketch

Including Framer in my Sketch workflow was fairly easy because it integrates by default. I only need to import the Sketch design file I’m working on, and I can immediately start to animate or otherwise manipulate any group of layers. The Framer-Sketch integration supports multiple artboards, but you can only import a single page at a time.

I’m still figuring out the most efficient way to work with Sketch and Framer. Currently, I think it’s best to have large per-project Sketch files, with separate pages for each screen of the app (or website) I’m working on. This enables me to easily reuse and organize all project assets, such as icons and buttons, into dynamic symbols. However, this approach produces larger files and slows down the Framer importing process. So, usually I’ll copy and paste the elements or screens that I want to prototype into a new file and then import them from there.</p>

## How Photoshop And Illustrator Fit My Workflow Now

I’ve moved to Sketch, but Photoshop and Illustrator are still part of my toolbox.

Because Sketch is a tool for UI design, it’s not the best-suited for creating very complex illustrations, and it doesn’t easily replace a solid vector application for illustration (nor does it attempt to).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd9a17e1-0f88-427c-b14e-ea391bafe563/sketch-app-dream-car-by-mirko-santangelo-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86e16388-0f41-4cb3-8a53-61d2f7864bab/sketch-app-dream-car-by-mirko-santangelo-780w-opt.jpg" width="780" height="444" alt="" /></a><figcaption>While Sketch can be used to create complex illustrations, that is not its main purpose. (Source: illustration made in Sketch by <a href="https://dribbble.com/shots/1303723--Sketch-app-Dream-Car">Mirko Santangelo</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd9a17e1-0f88-427c-b14e-ea391bafe563/sketch-app-dream-car-by-mirko-santangelo-large-opt.jpg">View large version</a>)</figcaption></figure>

I currently use Illustrator when I want to use my Wacom tablet for freehand drawing work, or if I’m doing something that requires complex artistic brushes and filters, or if I need to trace a raster image and convert it vectors. And, though nowadays I rarely do vector work for print (posters, leaflets, etc.), if I have to, I would again choose to use Illustrator.

Now I exclusively use Sketch for all interface and icon design tasks, but I continue to use Photoshop when I need to edit or refine product imagery, when I’m in the mood for some digital painting or drawing, or when I want to enhance a few photos. It has also happened a few times that I’ve opened Photoshop to quickly stitch together a few UI design mockups, so that I could send design previews for approval.</p>

## Conclusion

Sketch has solved many of my problems and has made my day-to-day life as a user interface designer a lot better. Mundane little things such as measuring distances and sizes are now much easier and quicker for me. I can now automate parts of my workflow and use real data in my Sketch designs. I can also organize my files more optimally (with the help of pages, artboards, states and symbols); I can reuse assets (through the dynamic symbols feature); and more.

Sketch also has a vibrant community. All of the open-source (and mostly free) plugins that completely transform the app and add some excellent functionality make Sketch a very versatile tool for UI design!

I really like Sketch’s focused approach, and hopefully I’ll continue to discover tiny features, tricks and plugins that make me go, “Whoa, that is so cool!”

If you’re a UI designer and are still using mostly Photoshop or Illustrator, I highly recommend you try Sketch. You might never want to look back!

{{< signature "mb, al" >}}


---
title: 'Optimizing The Design Workflow With Fireworks Extensions, Part 3'
slug: even-more-fireworks-extensions-optimized-design-workflow
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd0838cc-acff-47ea-bcfd-f30788eb8048/useful-05.jpg
date: 2013-11-06T10:10:10.000Z
author: ashish-bogawat
description: >-
  This article is the third part of an article series about improving your
  design workflow in Adobe Fireworks with some of the best extensions currently
  available. You may want to check out the
  [first](https://www.smashingmagazine.com/2012/08/28/optimizing-the-design-workflow-with-extensions/)
  and [second](https://www.smashingmagazine.com/2013/09/20/fireworks-extensions-for-better-workflow-part-2/)
  parts if you're not already familiar with them.
categories:
  - Fireworks
  - Workflow
  - Extensions
---
<em>This article is the third part of an article series about improving your design workflow in Adobe Fireworks with some of the best extensions currently available. You may want to check out the <a href="https://www.smashingmagazine.com/2012/08/28/optimizing-the-design-workflow-with-extensions/">first</a> and <a href="https://www.smashingmagazine.com/2013/09/20/fireworks-extensions-for-better-workflow-part-2/">second</a> parts if you're not already familiar with them. – Ed.</em>

We have already covered over a dozen brilliant extensions to add to your Fireworks arsenal, just the tip of the iceberg. With all-around great guys such as <a href="https://www.twitter.com/fwextensions">John Dunning</a>, <a href="https://www.twitter.com/aaronbeall">Aaron Beall</a>, <a href="https://www.twitter.com/stowball">Matt Stow</a> and <a href="https://www.twitter.com/chunwui">Linus Lim</a> continuing to support the app (an app that Adobe has finally decided <a href="https://blogs.adobe.com/fireworks/2013/05/the-future-of-adobe-fireworks.html">it has had enough of</a>), the power of Fireworks continues to make the lives of designers all over the world easier and more productive.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Sketch, Illustrator or Fireworks?](https://www.smashingmagazine.com/2016/04/exploring-a-new-illustration-ui-design-app-gravit/)
*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [The Present And Future Of Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

More on Adobe’s decision in a bit. For now, let’s dive into the extensions:

{{% feature-panel %}}

1.  [Export Commands](#exportcommands)
2.  [Lorem Ipsum](#loremipsum)
3.  [Greeked Text](#greekedtext)
4.  [Page Commands](#pagecommands)
5.  [Gradient Panel and Gradient Direction Editor](#gradientpanel)
6.  [Keyboard Resize](#keyboardresize)
7.  [Generate Web Assets](#generatewebassets)

## Export Commands

If you find yourself reaching for <code>Control/Command + Shift + X</code> to bring up the “Export Preview” dialog a couple dozen times a day, like I do, then you owe it to your fingers to download this extension. As easy as Fireworks makes it to create designs for the Web and mobile, it is surprisingly dull when it comes to optimizing the exporting process. Why must we struggle with the Optimize panel to change the exporting settings for each page before exporting it? And why can’t we export natively created vector elements to SVG (now one of the most preferred vector formats for the Web)?

<a href="https://fireworks.abeall.com/extensions/commands/#Export">Export Commands</a> by <a href="https://twitter.com/aaronbeall">Aaron Beall</a> is a set of commands that makes this whole process much simpler — and more!

This set contains the following commands: “Export SVG,” “Export Pages and States,” “Export Slices As Sprites” and “Export Styles as CSS.” Let’s review each in detail.</p>

### Export SVG

With high-resolution screens gaining in popularity, the need for scalable images on the Web is ever increasing.

<a href="https://en.wikipedia.org/wiki/Scalable_Vector_Graphics#Support_for_SVG_in_web_browsers">SVG</a> is by far the most popular and best-supported vector image format. However, while you can create vector artwork in Fireworks, you can’t export it as an SVG file. Well, with the “Export SVG” command, now you can!

When exporting to SVG, you can choose whether to export the entire document or a selected element on the canvas.

Note, though, that if any bitmap objects are in your Fireworks PNG image file, they will be exported as embedded bitmap images within the SVG (which pretty much defeats the point of using SVG in the first place). And any custom fonts won’t work, so text will render in the browser’s default font when you view the SVG in a browser. If you have to have the exact font you’ve used and don’t care about search engines not being able to read the text, then you might want to convert the text to SVG paths before exporting the file (go to <code>Text → Convert to Paths</code>).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71586add-6fc0-4cad-9131-a5dda4741320/exportsvg.png" alt="PNG vs SVG" width="500" height="250" /><br>
<em>SVG files are infinitely scalable, making them a good choice for creating Retina-friendly websites.</em>

<strong>Note:</strong> A couple of months ago, <a href="https://twitter.com/joshje">Josh Emerson</a> forked Aaron’s Export SVG command and updated it to optimize the SVG code for the exported files and to give you more precise control over how the resulting SVG is created. His new version of the command, <a href="https://joshemerson.co.uk/blog/svg-for-web/">SVG for Web</a>, creates smaller exported SVG files with good quality. If you’d like to try SVG for Web, you can <a href="https://github.com/joshje/svg-for-web/archive/master.zip">grab it from GitHub</a>. The extension is completely free.</p>

### Import SVG in Fireworks?

Aaron’s command, Export SVG, enables you to export your vector artwork in SVG format, but <strong>what about importing SVG files</strong>, you might ask? <a href="https://twitter.com/fwextensions">John Dunning</a>’s excellent <a href="https://johndunning.com/fireworks/about/SVG">SVG</a> extension makes this possible. With it, Fireworks can both open and import SVG files.

If you work with SVG files a lot and Fireworks is your primary design tool, then you owe it to yourself to download both of these extensions.</p>

### Export Pages and States

Suppose you’re done with a design and need to save all pages and states as PNGs to share with the team? Fireworks already lets you save all pages to files and all states to files easily from within the “Export” dialog, but not both at the same time. The “Export Pages and States” command does just that. As a bonus, it even lets you customize how the files will be named before exporting them.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfb36c68-51f6-482c-abdd-09a18d6883bb/export-pages.jpg" alt="Export Pages" width="500" height="320" /><br>
<em>The Export Pages command lets you define how the exported files will be named.</em>

### Export Slices As Sprites

If you have a lot of icons that need to go <a href="https://www.smashingmagazine.com/2012/04/11/css-sprites-revisited/">as a sprite</a> to the development phase, copying them all and composing them in a new file is tedious enough, let alone figuring out the measurements for the CSS after that. The “Export Slices as Sprites” command takes the grunt work out of this process by automatically creating a sprite from the selected slices in a document (or all slices if nothing in the document is selected), all neatly aligned. It will even create an HTML file with the appropriate CSS properties, if needed.

<strong>Note:</strong> If you work a lot with sprites, you may want to look at the <a href="https://www.adobe.com/cfusion/exchange/index.cfm?event=extensionDetail&amp;loc=en_us&amp;extid=2384542">CSS Sprite Maker</a> extension, which I covered in depth in an previous article about Fireworks extensions. Also, Fireworks CS6 integrates an “Export CSS Sprites” feature; the article “<a href="https://www.adobe.com/devnet/fireworks/articles/css-sprites.html">Working With CSS Sprites in Fireworks CS6</a>” is quite detailed and useful, if you want to learn more.</p>

### Export Styles as CSS

Finally, there is an “Export Styles as CSS” command, which will generate the CSS for all of the styles in the current document — styles that you have explicitly created and/or saved. This command is not as powerful as the new “CSS Export” in Fireworks CS6, though — it doesn’t recognize drop shadows, transparency or a few other properties.

So, if you are using the latest version of Fireworks (CS6), go with the built-in CSS panel in Fireworks CS6 (which was <a href="https://blogs.adobe.com/fireworks/2013/06/fireworks-cs6-update-12-0-1-is-live.html">recently updated</a>, by the way), and use it with the excellent <a href="https://mattstow.com/css-professionalzr.html">CSS Professionalzr</a> extension by <a href="https://www.twitter.com/stowball">Matt Stow</a>.

<iframe loading="lazy" src="//www.youtube.com/embed/iBzXt9Y6cBw?rel=0" width="500" height="375" frameborder="0" allowfullscreen="allowfullscreen"></iframe>
<em>CSS Professionalzr in action with the CSS Panel in Fireworks CS6 (screencast).</em>

## Lorem Ipsum

<strong>One of Fireworks’ strengths is its excellent UI prototyping capability</strong> — be it for the Web, desktop or mobile.

We’ve already covered this topic in detail on Smashing Magazine:

*   “[Create Interactive Prototypes With Adobe Fireworks](https://www.smashingmagazine.com/2012/06/25/create-interactive-prototypes-with-adobe-fireworks/),” André Reinegger
*   “[Developing a Design Workflow in Adobe Fireworks](https://www.smashingmagazine.com/2012/06/11/developing-a-design-workflow-in-adobe-fireworks/),” Joshua Bullock
*   “[Interactive Prototypes and Time-Savers With Adobe Fireworks](https://www.smashingmagazine.com/2012/07/03/interactive-prototypes-timesavers-adobe-fireworks/),” Trevor Kay
*   “iOS Prototyping With TAP and Adobe Fireworks,” [Part 1](https://www.smashingmagazine.com/2013/01/11/ios-prototyping-adobe-fireworks-tap-part1/), [Part 2](https://www.smashingmagazine.com/2013/01/ios-prototyping-with-tap-and-adobe-fireworks-part-2/), [Part 3](https://www.smashingmagazine.com/2013/02/15/ios-prototyping-adobe-fireworks-tap-part3/), Shlomo Goltz

Almost every designer I’ve known prefers Fireworks to Photoshop for prototyping and wireframing. And with wireframes comes the ubiquitous placeholder text, the ever popular lorem ipsum.

For years, I religiously went through the process of opening a text file, copying some random text from it and pasting it into Fireworks. More recently, I’ve been using the Lorem Ipsum command from Aaron Beall’s excellent Text Commands pack, which I talked about in my previous article.

That is, until I came across the <a href="https://johndunning.com/fireworks/about/LoremIpsum">Lorem Ipsum</a> auto shape by <a href="https://www.twitter.com/fwextensions">John Dunning</a>. Apart from giving auto shapes in Fireworks an entirely new dimension, the extension makes adding lorem ipsum extremely simple.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e96ae8db-8195-4880-91ff-270cd976c341/lorem-ipsum.gif" alt="Lorem Ipsum Smart Shape" width="500" height="300" /><br>
<em>Change the properties of the placeholder text block using the yellow control points. Easy!</em>

Although the auto shape does only one thing, the amount of control it provides sets it apart. To start with, it adds just the <strong>amount of text that will fit the shape you’ve drawn</strong>. No more copying and pasting or deleting text to fit the space! Resizing the boxes using one of the yellow handles or changing the font size will automatically adjust the amount of dummy text, so you will always have exactly as much text as you need.

Apart from the resizing handles, there are handles for aligning the text, setting text as a single block or as paragraphs (with the ability to define how many sentences make a paragraph), and changing the case between sentences (title case or uppercase). You can also click the target icon in the middle to set the exact height and width of the text object (which is especially handy because the smart resizing handles don’t do a good job of snapping to guidelines).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7749d796-bedf-416d-a201-079319d1221f/lorem-ipsum-options.png" alt="Lorem Ipsum Smart Shape Properties" width="500" height="444" /><br>
<em>Click the target in the middle of the Lorem Ipsum shape to open this dialog for more advanced settings.</em>

## Greeked Text

Sometimes, even lorem ipsum is too distracting. Ever had a reviewer from the client’s team come back saying that hundreds of spelling mistakes are in the design you sent? Me, too! Rather than waste time explaining Latin text to them, try using the <a href="https://johndunning.com/fireworks/about/GreekedText">Greeked Text</a> smart shape by <a href="https://www.twitter.com/fwextensions">John Dunning</a>, which makes the text completely unreadable.

This extension lets you define placeholders for blocks of text using flat colored lines or hash marks to depict the position, size and amount of text, without the distraction of “fake” text. You can choose between black, gray or hatched text blocks, depending on how obvious or rough you want the blocks to look. While the commands are for black or gray lines only, you can change the color as you wish once the object has been created.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a970b5d6-6235-468d-b12c-ecdc3aeeb23d/greeked-text.png" alt="Greeked Text Smart Shape" width="500" height="280" /><br>
<em>The Greeked Text smart shape has a ton of customizable options via these control points.</em>

A few yellow control points are all over the smart shape to let you resize it, change the alignment, line height and line spacing, and show paragraph breaks. For even finer control, click the crosshair in the middle of the shape, and a properties dialog box will pop up in which you can fine-tune every aspect of the shape to make it exactly match your wireframe.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f3e7aec-b321-4634-8426-38b27268911f/greeked-text-properties.png" alt="Greeked Text Smart Shape Properties" width="500" height="444" /><br>
<em>If you click the target icon, a properties dialog will open up for finer editing.</em>

## Page Commands

When working with multiple pages in a Web or UI design project — or when creating layouts for different breakpoints in a responsive design — the <a title="Dave Hogue about using Pages, Layers and States in Fireworks." href="https://www.adobe.com/devnet/fireworks/articles/pages_states_layers.html">Pages feature</a> in Fireworks comes in real handy. You can create Fireworks documents with many pages, each page with its own canvas size and optimization settings.

<strong>Note:</strong> You can have certain layers <strong>shared across pages</strong>, kind of like the master page template in PowerPoint and InDesign. Shlomo Goltz has covered this in detail in part one of his excellent “<a href="https://www.smashingmagazine.com/2013/01/11/ios-prototyping-adobe-fireworks-tap-part1/">iOS prototyping With TAP and Adobe Fireworks</a>.”

<a href="https://www.twitter.com/fwextensions">John Dunning</a>’s <a href="https://johndunning.com/fireworks/about/PageCommands/">Page Commands</a> extension packs together a set of commands to supercharge the way you work with pages in Fireworks.

The highlight of the extension is a set of commands to quickly go to a page. Assign keyboard shortcuts to each of the commands, and you’ll have a home-grown set of hotkeys to quickly access a page in your design. Of course, the default <code>PageUp</code> and <code>PageDown</code> keys will take you to the previous and next pages, respectively, but this extension lets you easily jump to <em>any</em> page in the design with a single keystroke.

Then we have a couple of commands to distribute layers or states to their own pages (in Fireworks, “states” were formerly called “frames”). Let’s say you’re working on a set of icons and need to create them on the same page to retain context. Just keep them on their own layers and distribute the layers to pages; you will then be able to export all pages at once. The same is true of states when you’re working on buttons with multiple states. Another neat feature is the ability to crop all pages to the selection at once.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31a0a949-693d-482e-87fa-ab4293a7c332/distribute-to-pages.gif" alt="Distribute States to Pages" width="500" height="350" /><br>
<em>The command gives you one-click conversion of states to pages.</em>

If you need to work on a set of files at once, you can import them all into separate pages, instead of doing it one by one, with the Import Files Into Pages command. When it’s time to export, Fireworks lets you export all pages at once, but each page might have different export settings attached to it; in these cases, use the Apply Export Settings to All Pages command to apply the settings from the current page to all other pages.</p>

## Gradient Panel And Gradient Direction Editor

Gradients are an integral part of any design. While working with gradients in Fireworks is now easier (much progress was made in versions CS4 through CS6), some things related to control could still be improved. You can, for example, add new color stops to a gradient pretty easily, but there is no way to set them accurately with numeric position markers. Changing the gradient direction can also get pretty messy.

<a href="https://www.granthinkson.com/2007/01/23/fireworks-gradient-panel/">Gradient Panel</a> and <a href="https://www.granthinkson.com/2008/05/15/new-fireworks-panel-gradient-direction-editor/">Gradient Direction Editor</a> are a couple of extensions by Grant Hinkson that greatly enhance our control of gradients in Fireworks.

Once you have chosen a gradient for the selected object, the Gradient Panel lets you <a title="Using the Gradient panel in Fireworks (an article by Grant Hinkson)" href="https://www.adobe.com/devnet/fireworks/articles/gradient_panel.html">add color stops with pinpoint accuracy</a>. Want to place stops very close together? Use the zoom and pan slider to get as close as you need. You can easily get close enough to start seeing the gradient pixel by pixel! Alternatively, use the table (see below) to define the exact position and color values of each gradient stop. You can also quickly switch between a vertical and horizontal gradient right from the panel.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62e50281-101f-44b4-a8a1-b36ed7a592f5/gradient-panel.png" alt="Gradient Panel" width="500" height="350" /><br>
<em>The Gradient Panel provides fine control over every aspect of a gradient.</em>

Ever get frustrated when rotating the gradient line on very thin objects? This is especially bothersome when dealing with short wide boxes (such as horizontal rules) because Fireworks insists on making every new linear gradient a vertical one. That’s where the Gradient Direction Editor panel comes in handy. Quickly change the angle of the gradient by using the buttons, or simply drag and drop the start and end points in the panel. But the real power of the Gradient Direction Editor panel lies in its ability to specify precise coordinates for the gradient’s end points. Fireworks can natively change the angle just as easily, but only this panel offers precise numerical control over the <em>location</em> of the end points.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1297baf8-b2ec-453e-9113-c9b0a3b729c0/gradient-direction-editor.png" alt="Gradient Direction Editor" width="500" height="350" /><br>
<em>The Gradient Direction Editor panel gives you precise control over a gradient’s angle.</em>

<strong>Note:</strong> These extensions were created almost four years ago and are not being developed or supported anymore, but they run just fine in Fireworks CS5, CS5.1 and CS6. If you are using the latest version of Fireworks (CS6), then you already know that the workflow with gradients has been considerably improved; numeric control over the gradient stops and angles have been added. My only complaint is that gradient presets were removed (although this could be somewhat corrected by using <a title="Learn more about Styles and Symbols (video tutorial by Jim Babbage)" href="https://www.adobe.com/designcenter-archive/fireworks/articles/lrvid4033_fw.html">Styles</a>).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18fc3339-604f-4982-b65e-35f466a9c1d8/fireworks-cs6-gradients.png" alt="Gradient Panel in Fireworks CS6" width="500" height="410" /><br>
<em>Handling gradients is much easier in Fireworks CS6. We now have fine numeric control over both angles and gradient stops.</em>

## Keyboard Resize

Resizing elements is one of the most fundamental tasks in any visual editing application, and having done this in a certain way for years, I find it hard to imagine that the tools built into Fireworks — or any similar application for that matter — might be hugely deficient.

Let me explain. Say you’ve created a button with a text label inside it. Now you need to increase the width of this button by a few pixels on the right. You select the rectangle and either stretch it to the right using the Scale tool or change its width in the Properties panel. Then, you select the text and repeat the same action, because selecting both and scaling them would have distorted the text and messed up the margins on the side.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd094008-caef-43d2-b73a-79482e3f3547/smart-resize-wrong.gif" alt="Resizing multiple objects" width="500" height="220" /><br>
<em>Resizing multiple objects together can be extremely error-prone.</em>

Is there a better way to do this? Select both elements, press <code>Alt + right arrow</code> a few times and voilà! Your button is wider, and so is the text block; text is not distorted, and the margins between the text block and the button are intact! This is precisely what the <a href="https://johndunning.com/fireworks/about/KeyboardResize">Keyboard Resize</a> commands by <a href="https://www.twitter.com/fwextensions">John Dunning</a> do. The extension comes with 16 commands that let you resize elements one side at a time.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07bf98d-f784-4576-8b1c-d94022263e00/smart-resize.gif" alt="Smart Resize" width="500" height="220" /><br>
<em>Assign keyboard shortcuts to the Smart Resize commands for quick and easy resizing of multiple elements, without any distortion.</em>

To be frank, I never thought I needed this extension until I used it, but once I got used to it, I started wondering how I ever survived without it! The idea is simple: Resize elements using keyboard shortcuts. You decide which side to extend or contract using the appropriate command or shortcut. There are different shortcuts for 1-pixel increments and 10-pixel increments — hence, the total of 16: four sides, two actions (expand or contract), and two modes (1 pixel or 10 pixels).

Apart from making it stupidly easy to resize elements using keyboard shortcuts, the commands are extremely smart about figuring out what the selection is and resizing them accordingly. For text, it resizes only the text blocks, not the text itself, something even Fireworks’ built-in Scale tool is too imperfect to understand.

Note that, as with all third-party commands, keyboard shortcuts will not be automatically assigned when you install the Keyboard Resize commands pack. Either add them manually using the Keyboard Shortcuts dialog in Fireworks (go to <code>Edit → Keyboard Shortcuts</code>), or use the Assign Keyboard Shortcuts command, which is part of this extension. Easy!

A word of caution: The keyboard shortcuts assigned might conflict with your system-wide shortcuts. In my case, <code>Control/Command + Alt + arrow keys</code> were already assigned to changing the orientation of my monitor. I had to disable them from my video settings panel before I could get them to work in Fireworks.</p>

## Generate Web Assets

No matter how many extensions you use or how optimized your workflow is, generating assets for the development phase after finishing up your design composites is always a chore. C’mon, by show of hands, who here likes the process of taking each individual design element and exporting it in the right format to be integrated in a website, application or whatever else you’re building?

The <a href="https://johndunning.com/fireworks/about/GenerateWebAssets">Generate Web Assets</a> extension by <a href="https://www.twitter.com/fwextensions">John Dunning</a> makes this whole process almost trivial, to the point that I’m beginning to wonder how I lived without it for so long! The process is simple: Once you are done with a design, simply change the names of the objects that you want to export to the file names you want for them, including the file extensions. Then, run the Generate Web Assets command, define a folder, and presto! All of your assets will magically appear in this folder.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/084947c9-66a1-402c-bcce-7f429f38e4f2/generate-assets.jpg" alt="Generate Assets" width="500" height="320" /><br>
<em>Exporting background and UI elements is simply a matter of naming them appropriately in the Layers panel.</em>

The file names may be applied directly to objects, groups or layers in the Fireworks Layers panel. The command is smart enough to recognize the names and to include everything in the named element, irrespective of what it is. JPG files are saved with the “Better Quality” setting, PNGs are saved as PNG32 (i.e. PNG24 + alpha transparency), and GIFs are saved as GIF Adaptive-256 with index/alpha transparency.

The Generate Web Assets command will export all named elements to a Fireworks file by default. To export only some assets in a file, select them and use the Generate Web Assets from Selection command.

<strong>Note:</strong> The command will ask you to select a folder only the first time you use it in a document. After that, it will continue to save files to the same location. If you want to change the folder, run the “Generate Web Assets — Change Export Location” command.</p>

## Conclusion

Over the span of these three articles, I’ve covered the extensions that I find indispensable in my daily workflow with Fireworks. The tools extend the already excellent functionality of the application multifold. With passionate Fireworks developers around the world not showing any sign of slowing down their development of new extensions for the app, this list in all probability will only grow, whether Fireworks gets seriously updated in the future by Adobe or not.

<strong>Note:</strong> For some very interesting up-and-coming work with Fireworks extensions, keep an eye out for the <a href="https://phoenix-project.tumblr.com/">Phoenix Project</a> by <a href="https://www.twitter.com/chunwui">Linus Lim</a>.

Finally, Adobe’s decision to cease further development on one of the most useful applications in the Creative Suite is a pity, especially for any designer who designs exclusively for the screen. Adobe has promised to update the current version (CS6) with critical patches when necessary, but there won’t be a major release of Fireworks anymore.

My take is that Adobe failed to tap into the potential of the app, which perennially played second fiddle to that monster of a design application, Photoshop. Only time will tell if Adobe can successfully transition Fireworks’ unique features over to Photoshop or an entirely new application. Regardless, Fireworks will continue to live on all of my computers and relentlessly toil away on all of my for-screen designs for the foreseeable future.

There are rumors that Adobe is working on a new application that will pick up where Fireworks left off, but no specific news as of yet. I’ll be keeping an eye out on what it comes up with, of course. Till then, it’s Fireworks FTW!

{{< signature "mb, al, il" >}}


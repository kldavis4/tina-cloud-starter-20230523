---
title: 'A Web Developer’s Guide To Adobe InDesign'
slug: a-web-developer-s-guide-to-adobe-indesign
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d147c826-4141-4ed0-a164-9a93970ae4b8/paint-brush-pink-photoshop.jpg
date: 2011-06-23T15:10:06.000Z
author: matthew-potter
summary: >-
  Adobe InDesign is the primary application of print designers for laying out multiple pages and assembling print documents. In this post, Matthew Potter gives you, Web-based developer, a look at some of the tools in InDesign that translate directly into what you currently use. 
description: >-
  Adobe InDesign is the primary application of print designers for laying out multiple pages and assembling print documents. In this post, Matthew Potter gives you, Web-based developer, a look at some of the tools in InDesign that translate directly into what you currently use.
categories:
  - Graphics
  - InDesign
  - Best Practices
---

Over the past several years, there has been a big divide between designers: those who work in print distribution and those in digital distribution. The irony is that, despite the disputes, name-calling and flat-out arguments between the two camps, their techniques and methods are far more common than many believe. Both sides of this communications field are heavily influenced by each other. Grid systems and typography now play a strong role in Web-based design, and usability and user experience play a big part in developing print material.

Adobe InDesign is the primary application of print designers for laying out multiple pages and assembling print documents. This article gives you, the Web-based developer, a look at some of the tools in InDesign that translate directly into what you currently use. We’ll look at how the terminology in the two fields compare and how to apply your expertise to this other industry.

{{% feature-panel %}}

## Jumping Right In

### Folder Structure

As with any Web development project, organizing from the start ensures that you will have minimal problems with the files later on. Similar to many website root folders, InDesign gives you a main document folder and a resources folder:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a415fba7-9742-4dac-acc9-8643f6753ddd/folder-structures-large.png"><img class="106203 alignnone" title="Folder Structures" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4be6819-5b89-48e1-9cdb-da4c5e7e8939/folder-structures.png" alt="Folder Structures" width="500" height="260" /></a><figcaption>Folder structures.</figcaption></figure>

Above on the left is my folder structure for InDesign, and on the right the folder structure for my website. They are so similar that, if not for the different file extensions (*.indd* and *.html*), they would be practically the same.

### Setting Up The Document

Setting up an InDesign document is similar to setting up a mobile website. You specify the height, width and purpose of the document. For print-based items, set the “Intent” to “Print.” If you will be using the file for an eBook or digital publication, then specify “Web.” If you will be using the document for both, then specify “Print” to ensure that the colors are maintained properly.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2016a01e-07b2-4cb8-b598-58ebe78265cf/indesign-new-document-large.png"><img loading="lazy" decoding="async" class="106204" title="InDesign’s New Document Window" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8e2d87a-0afd-4787-b7c9-7dfaa740dad0/indesign-new-document.png" alt="Highlights of InDesign’s New Document Window" width="500" height="362" /></a><figcaption>Highlights of InDesign’s new document window.</figcaption></figure>

The margins in InDesign are guidelines that are positioned on the page and are not like Web margins that affect objects on the page.

### Your Main Tools

If you’re familiar with Photoshop and Illustrator, then you are used to finding the main group of tools on the left side of the workspace, at least by default. InDesign is the same. The way you interact with and build objects on the page, though, works slightly different than Adobe’s other design software. Containers are needed in order to place images, vector objects and textual content on the page.

You can import vector objects directly into the document, but you will usually be importing files into content boxes that you position in the layout. This should come easily to you because Web design operates on the same principle: creating DOMs that contain images or text, and then positioning them in the layout. The one major difference is that, while objects are positioned in a Web document relative to their structure (unless otherwise styled), objects on an InDesign layout are always given an x and y position based on the overall page (by default, the top-left corner, similar to absolute positioning).

Because we are working with a vector- and object-based layout, one of the main tools you will use for the majority of your editing is the Selection tool <img style="vertical-align: middle" title="Pointer tool button" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a136708-26dd-4b9c-ae64-691901215555/tool-selection.gif" alt="Pointer Tool Button" width="25" height="20" />, which gives you control of position and size. It also is used to select an object in order to change its properties. This is quite different from Photoshop, in which you edit individual layers. To change the color of an object, you need to select it first using the Selection tool, and then adjust it using one of the various ways to change color.

These content boxes can be created with various tools. The Type tool <img style="vertical-align: middle" title="Type tool button" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5f4ca72-b495-4dfa-a56a-99f07eaa43de/tool-text.gif" alt="Type tool button" width="25" height="20" /> enables you to create a box for text. The Rectangle Frame tool <img style="vertical-align: middle" title="Rectangle Frame tool button" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc50c1a2-29ec-45b3-9f48-dae23f22128a/tool-frame.gif" alt="Rectangle Frame tool button" width="25" height="20" /> creates a box to add an image or linked resource. The Rectangle tool <img style="vertical-align: middle" title="Rectangle tool button" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35c9a75c-debd-46a2-9e5c-b4bc6f5d5f5c/tool-rect.gif" alt="Rectangle tool button" width="25" height="20" /> is not assigned to any particular kind of content. These three frame types allow you to build the layout any way you want.

In spite of both the Rectangle and Rectangle Frame tools, many designers who were trained on older software use only the Frame tool. The one difference between them is that the Frame tool shows a placeholder (an *x*). The Rectangle tool merely allows for a cleaner workspace but does not affect the final output.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59c20c0f-4af6-417a-ba0e-6b9828b61bc5/context-bars-large.png"><img loading="lazy" decoding="async" class="106202" title="InDesign’s Text Contextual Bars" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/429718d2-d68c-4886-b4e6-a9f37fdc669e/context-bars.png" alt="InDesign’s Text Contextual Bars" width="500" height="56" /></a><figcaption>InDesign’s text contextual bars.</figcaption></figure>

The context bars and option panes help you style the content. As in Photoshop, various objects will open up a context-sensitive toolbar at the top, allowing for quick editing based on the type of object(s) selected and the tool selected.

Also like in Photoshop and Illustrator, a multitude of panes are available to control the values associated with an object. Again, they apply only to selected objects. Selecting an option from a pane when an object is not selected will not cause any objects to change.

{{% ad-panel-leaderboard %}}

## Style Sheets And Their Origins

CSS did not originate with the Web. The model of defining a set of instructions in order to style content was originally built for desktop publishing applications. In InDesign, this takes the form of object styles, paragraph styles and character styles. There are also table styles, row styles and cell styles for designing table objects, but we’ll stay away from these in this lesson.

Styles in InDesign work similar to Web-based CSS but have one major difference: you cannot group multiple style sheets of the same type. For example, you cannot apply multiple paragraph styles to one paragraph. However, you can apply a character style sheet to content in a paragraph that already has a style sheet applied to it.

Shortcuts and menu locations for the panes are given below. But the panes will already be open on the right side of your workspace if you have selected <code>Window</code> → <code>Workspace</code> → <code>Advanced</code> or have selected the “Typography” option. These function exactly like the panes in Illustrator and Photoshop: you can snap them together and arrange them to your liking, and they contract to icon format.

### Object Style Sheets

Draw a content box on the page using the Rectangle tool. With the box selected, you can modify the content box &mdash; including the border, background and corner effects &mdash; as you would a div object. If you give it, say, a background color, a drop shadow and rounded corners, you can save that style by selecting a new “Object Style” in the Object Style pane when the object is selected (<code>Window</code> → <code>Styles</code> → <code>Object Styles</code>, or <code>Command/Contro</code>l + <code>F7</code>). You can give the style a name (much like a class name) and modify any of the style properties you’ve assigned.

After saving this new style, you’ll still need to apply it to the object. This may sound redundant; however, you’ve only created a new style based on the properties of the selected object. By clicking on the new style with the object selected, you will apply that style. Think of it like adding <code>class="object_style"</code> to an HTML element after you’ve set up the CSS.

### Paragraph Style Sheets

Select the Text tool, and click in the newly styled box. Add a few paragraphs of content (you can cheat by going to <code>Type</code> → <code>Fill With Placeholder Text</code>). With your cursor in the first paragraph, you can start changing some of the properties of what, in Web terms, would be the <code>&lt;p&gt;</code> tag by using the Paragraph pane (<code>Window</code> → <code>Type &amp; Tables</code> → <code>Paragraph</code>, or <code>Command/Control</code> + <code>Alt</code> + <code>T</code>).

Notice that options for modifying font size, letter spacing and weight are not available. This is because these aspects relate to the characters of the paragraph. While a paragraph style can and most likely will include instructions for these values, the Paragraph pane does not provide access to them.

Let’s create a paragraph style via the Paragraph Style pane (<code>Window</code> → <code>Styles</code> → <code>Paragraph Styles</code>, or <code>Command/Control</code> + <code>F11</code>). This opens a new window that gives you God-like control over all aspects of the text. Name your style, and jump to the “Basic Character Formats” option on the left.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dad95eb3-b783-4266-ba92-ff206b336822/paragraph-styles-window-large.png"><img loading="lazy" decoding="async" class="106205" title="InDesign’s Paragraph Styles Window" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/486ccd32-def0-4ee9-9d51-04af4697f771/paragraph-styles-window.png" alt="InDesign’s Paragraph Styles Window" width="500" height="405" /></a><figcaption>InDesign’s paragraph styles window.</figcaption></figure>

This is what I meant when I said that character properties could be defined in the paragraph style. Change the font size, weight and spacing here, and click “OK.” As you did with the object styles, you will still need to apply it to the paragraph you are working with. To do this, put your cursor in the paragraph text or select a portion of it, and then click on the paragraph style’s name. If you have selected the entire object using the Selection tool, then the paragraph style will be applied to all of the content.

### Character Style Sheets

With the Type tool still selected and your cursor in the paragraph, highlight a portion of the text. Using the Character pane (<code>Window</code> → <code>Type &amp; Tables</code> → <code>Character</code>, or <code>Command/Control</code> + <code>T</code>), adjust the properties of the characters. You can add italics or bold or change the font family.

Once more, let’s create a style that incorporates these modifications. In the Character Styles pane (<code>Window</code> → <code>Styles</code> → <code>Character Styles</code>), create a new “class.” Name it something relevant, save it, and then apply it to the highlighted text. This would be akin to adding a little <code>&lt;span&gt;</code> tag to some text in a paragraph, which allows you to apply styles to that text independent of the parent element.

### CSS vs. Style Sheets

We’ve just gone over a lot here. The reason we went over these three things is to illustrate that, unlike CSS styling, I cannot add a second style sheet of the same type to an element. In CSS, I can do something like this:

<pre><code class="language-css">&lt;div class="orange_box rounded"&gt;&lt;/div&gt;</code></pre>

This would apply two styles to the same object (the orange box). InDesign attributes of a given type (whether object, paragraph or character) must be contained in a single style. Higher-level styles are overwritten by child items. For example, character styles overwrite paragraph styles, which in turn overwrite object styles; but you cannot apply multiple styles to a single object, etc.

As in CSS, I could overwrite an object manually. For instance, I could apply a style sheet that gives a paragraph a font size of 11 points and a leading (line height) of 14 points, but then manually change the leading to 16 points by adjusting it in the Character pane. This would result in Web code like:

<pre><code class="language-css">&lt;p class="standard_body" style="line-height: 16px;"&gt;&lt;/p&gt;</code></pre>

As you can see, we end up with code that would be considered poor practice by most people. However, it does allow us to customize as issues arise.

## Play Around With The Tools

Now that you’ve been introduced to how set up a document, start playing around with the tools, using what you already know of Photoshop or Flash. Position elements on the page, modify their color and font face, and create the layout for a product that you’ve already built.

In the next lesson, we’ll dive head first into learning how to create consistent layouts with some advanced style sheet options, and we’ll examine how to build a page structure from scratch. So, don’t forget your <a title="Most useful thing in the universe!" href="https://en.wikiquote.org/wiki/The_Hitchhiker's_Guide_to_the_Galaxy">towel</a>.

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Adobe InDesign Tips I Wish I’d Known When Starting Out](https://www.smashingmagazine.com/2011/03/17/indesign-tips-i-wish-i-d-known-when-starting-out/ "Adobe InDesign Tips I Wish I’d Known When Starting Out")
*   [Useful InDesign Scripts And Plugins To Speed Up Your Work](https://www.smashingmagazine.com/2013/08/indesign-scripts-and-plugins-to-speed-up-your-work/)
*   [10 Pre-Press Tips For Perfect Print Publishing](https://www.smashingmagazine.com/2009/10/10-pre-press-tips-for-perfect-print-publishing/)
*   [Creating Wireframes And Prototypes With InDesign](https://www.smashingmagazine.com/2013/03/creating-wireframes-and-prototypes-with-indesign/)

{{< signature "al, il, mrn" >}}

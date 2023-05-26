---
title: How To Optimize The Design Workflow With Fireworks Extensions
slug: fireworks-extensions-for-better-workflow
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd0838cc-acff-47ea-bcfd-f30788eb8048/useful-05.jpg
date: 2012-08-28T13:26:35.000Z
author: ashish-bogawat
description: >-
  As a platform, Fireworks gives its users a lot of freedom, when it comes to
  extending it. Because of that, Fireworks has a thriving ecosystem of add-ons
  (extensions) that add a lot of valuable functionality with newer options.
categories:
  - Fireworks
  - Workflow
  - Extensions
---
I've been using Adobe Fireworks for over a decade now and I can recommend it to anyone searching for the optimal screen design workflow. Much has been said about Fireworks' capabilities as a design application, but today I want to focus on one of its other biggest strengths — its _extensibility_.

As a platform, Fireworks gives its users a lot of freedom, when it comes to extending it. Because of that, Fireworks has a thriving ecosystem of add-ons (extensions) that add a lot of valuable functionality with newer options.

In this article, I'll try to list some of my top extensions for Fireworks. These are not necessarily the most complex or powerful extensions, but rather those that have helped me be more productive with my Fireworks workflow over the years. Also, all of these are free to test and use, so you can even try them right away!

My article is pretty detailed, so to help you navigate it, you can use the following list:

1.  [Grids Panel](#grids)
2.  [Guides Panel](#guides)
3.  [Smart Resize Auto Shape](#smartresize)
4.  [Tables Auto Shape](#tables)
5.  [Placeholder Auto Shape](#placeholder)
6.  [Orange Commands](#orangecommands)
7.  [QuickFire](#quickfire)

{{% feature-panel %}}

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [Sketch, Illustrator or Fireworks? Exploring A New Free UI Design App: Gravit](https://www.smashingmagazine.com/2016/04/exploring-a-new-illustration-ui-design-app-gravit/)
*   [Sketch With Material Design](https://www.smashingmagazine.com/2015/05/sketch-with-material-design/)
*   [Using Sketch For Responsive Web Design (A Case Study)](https://www.smashingmagazine.com/2015/04/using-sketch-for-responsive-web-design-case-study/)

## Working With Extensions In Fireworks

<p>Fireworks can be easily extended, but the extensions are installed and maintained via the Adobe Extension Manager &mdash; a tool that must be run separatey from Fireworks.

<p>Before we review in detail the extensions that I can personally recommend, I would like to share a few general tips and suggestions on how to work with extensions in Fireworks. Although these tips are mostly geared towards Fireworks CS5 and CS5.1, there are actually only a few minor differences if you are using version CS6.

### Easy fix for issues with Windows Vista / Windows 7

<p>If you are using Fireworks on Windows Vista or Windows 7, the Extension Manager may give you strange errors when you attempt to install an extension. The easiest solution to this problem is to <strong>run the Extension Manager as administrator</strong>. Simply right-click the "Extension Manager" shortcut and select "Run as administrator".</p>

<blockquote><p><strong>Note</strong>: The reason why the EM needs to be run sometimes with administrator privileges in Windows Vista and Windows 7 is simple &mdash; some extensions specify installation locations in the Program Files folder, and Windows requires administrator approval to install <em>anything</em> in this area, for security reasons. Usually older extensions (that were not recently updated) are installed into the Program Files folder, while new extensions are installed into the User Application Data folder. Fireworks can run extensions from either the Program Files folder or from the "User Application Data" folders in order to maintain backward compatibility with older extensions.</p></blockquote>

### Where are the installed extensions located?
<p>If you are installing Fireworks extensions for the first time, keep in mind that:</p>

<ul>
<li>Commands will usually appear in the Fireworks Commands menu.</li>
<li>If an extension also installs a panel, you will find it in the Window menu.</li>
<li>If an extension installs an auto shape, it could be found in the Auto Shapes panel.</li>
</ul>

### Extension descriptions

<p>The best way to learn how an extension is supposed to work, or in which menu / submenu you'll find it, is to look for the extension description in the Extension Manager. However, please note, that the Extension Manager lets extension developers link to descriptions online, which means that if you are not connected to the Internet, you will see <em>empty</em> description boxes in the Extension Manager. If you do come across these, know that a missing internet connection might be the cause.</p>

### Using shortcuts

<p>If there are some commands that you find yourself using very often, you may want to assign keyboard shortcuts to them for gaining more productivity.</p>

<p>To do so, go to menu <code>Edit</code> &#8594; <code>Keyboard Shortcuts</code>, duplicate the default shortcuts set, then select your command from the list and add a shortcut combination of your choice. Fireworks will let you know if the shortcut you want to assign is already in use. Then, depending on what it already does, you can either choose to replace it with the new one, or select a different key combination.</p>

### Updating extensions

<p>Updating extensions in Fireworks is pretty straightforward &mdash; you just have to open the Extension Manager every once in a while. If an extension has an update available, you'll see a notification in the list of extensions. Then, simply select the extension and click "Update".</p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75e456c4-8c9e-458b-8f9f-a4f81fd8c4cf/updating-extensions-process.png" width="500" height="560" alt="Updating Extensions Using the Adobe Extension Manager" /><br /><em>Process of updating extensions.</em></p>

<p>Please note that not all Fireworks extensions have the "Automatically Check For Updates" option built-in. So alternatively, you can simply download a newer version (if there is one available, of course) from the website where the extension was originally posted, and then run the Extension Manager. The EM will ask you if you'd like to replace the old version with the new one &mdash; select "Yes", and the process will complete automatically.</p>

<p>Now that we've covered the basics, let's move on to the list of extensions!</p>

## 1. <a href="https://johndunning.com/fireworks/about/Grids">Grids Panel</a>

<p><a href="https://twitter.com/fwextensions">John Dunning</a> is a legend in the Fireworks community, and his <a href="https://johndunning.com/fireworks/" title="See the full list of extensions by John Dunning">growing list of powerful extensions</a> often compete with themselves for the top spots as valuable and useful. His <a href="https://johndunning.com/fireworks/about/Grids" title="Get Grids Panel Extension for Adobe Fireworks">grids extension</a> is unquestionably the first one I reach out for every time I start a new project.</p>

<p>In a nutshell, the extension <strong>lets you set up a grid for your design</strong>. You set the parameters (the column width, gutter width, number of columns, etc.) and it then creates a locked layer with the columns, rows and guides spanning the height of your canvas. Since there are a couple of setups that I usually prefer to work with, I've saved them as <em>presets</em>, so it's simply a matter of opening the panel and selecting an existing preset.</p>

<p>For responsive designs, what I typically do is create a few grid setups for different viewport sizes. Then I simply create a new page for each breakpoint and apply the appropriate grid before pasting the content in for realignment.</p>

<p><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/647b6673-38ba-4d89-bd7c-3da6dd7b3dd1/grid-big.png" title="Grids panel [view large]"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e5be8b4-e89d-432a-9a2a-4102d2294d48/grid-small1.png" width="500" height="462" alt="Insert Grid Panel" /></a><br /><em>Insert Grid Panel: Typical setup for a 12-column grid. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/647b6673-38ba-4d89-bd7c-3da6dd7b3dd1/grid-big.png">Large preview</a>.</em></p>

<p>The features of the grid panel are evident from the screenshot, and make it easy to control columns, gutters, and baselines as wells the appearance of the overlay (and whether or not guides should be created). If you have ever tried to set up a grid in Fireworks without this extension, you’ve wasted a whole lot of time!</p>

<p><strong>Useful tip:</strong> Using Photoshop and need something similar? The <a href="https://www.smashingmagazine.com/2012/01/03/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/" title="GuideGuide, a free panel for grids in Photoshop (by Cameron McEfee)">GuideGuide</a> panel might be something worth giving a try.</p>

## 2. <a href="https://www.adobe.com/devnet/fireworks/articles/guides_panel.html">Guides Panel</a>

<p>As awesome as the grid panel is, it's probably not suitable for every situation. Sometimes you may need to just create a set of guides without all of the other grid structures (e.g., if you are creating individual assets such as banner ads, rather than entire pages &mdash; grids are great for entire pages and screens, but they can be an overkill for specific components).</p>

<p>Also, for those of you who work extensively with guides, it often seems much easier to quickly set up the <strong>grid precisely with guides</strong>. If you are like me, and addicted to the fine control that guides offer in Fireworks (or any other design application for that matter), you most certainly would like to check out the <a href="https://www.adobe.com/devnet/fireworks/articles/guides_panel.html" title="Get Guides Panel Extension for Adobe Fireworks">Guides panel</a> by Eugene Jude.</p>

<p>The panel gives you several options to add guides to the canvas with precise numerical control: you can set margins on either (or all) four sides, create columns and rows, or add individual guides at specific coordinates.</p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2eb926e4-37cd-400c-b7f3-5e4c99573c1c/guides-tab1.png" width="500" height="355" alt="Guides Panel General" /><br /><em>Guides Panel (with the "General" tab selected in it).</em></p>

<p>You can copy entire collections of guides and paste them into another page or document, or even <em>save sets</em> to retrieve later (this feature is pure gold if you have a setup that you work with often, and want to reuse).</p>

<p>But where this panel really shines is in its ability to <em>work with selected objects</em>. Lets say you need guides all around and through the middle of that image you just placed in your design, so you can align objects around it. Simply select the object, go to the "Selection" tab in the Guides Panel and select the appropriate boxes. You can even set an offset value between the object and the guides.</p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae30bac6-8ea9-4a33-804a-1646a3136e41/guides-selection.png" alt="Guides Panel Selection" width="500" height="355" /><br /><em>Adding guides through the center of a selected object.</em></p>

<p>Finally, there's the ability to delete all guides, or at least only the vertical or horizontal ones (oh, how I wish I had this panel a little earlier &mdash; this would have easily saved me a couple of precious weeks every year!).</p>

## 3. <a href="https://johndunning.com/fireworks/about/SmartResize">Smart Resize Auto Shape</a>

<p>Since Adobe Fireworks is used extensively for UI design, a very common use case is to create an interface element by grouping a few objects together &mdash; rectangles, text fields, buttons, etc.</p>

<p>Fireworks' <strong>object-based workflow</strong> makes this an easy task (compared to Photoshop's predominantly <em>layer-based structure</em>). The problem though is that once you have created such a group, resizing it can be difficult. You can't just select the group and change its width or height, since Fireworks will simply stretch everything in the direction specified, and deformations to the individual objects will occur.</p>

<p>That's where John Dunning's <strong><a href="https://johndunning.com/fireworks/about/SmartResize" title="Get Smart Resize Auto Shape (Extension) for Adobe Fireworks">Smart Resize</a></strong> comes into play.</p>

<p>Once you've selected a group that you need to resize, use menu <code>Commands</code> &rarr; <code>Smart Resize</code> &rarr; <code>Attach</code>, and the command will convert your group into a special <strong>smart object</strong> with the typical yellow resize handles.</p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce41eb2b-26fc-4c20-9526-b2f1ec91d0d6/smart-resize-01.png" alt="Smart Resize: Saving Time When Resizing Groups of UI Objects" width="336" height="200" /><br /><em>Smart Resize: Saving Time When Resizing Groups of UI Objects.</em></p>

<p>You can use these handles to resize the group in any direction and witness the magic in action. The extension will resize <em>only elements that extend across more than 50% of the group's size</em> &mdash; which is typically your background boxes &mdash; and <em>retain the rest of the elements in position</em> relative to the closest edge of the group.</p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc627e9f-25df-4f89-8425-57367c95b8e8/smart-resize.gif" alt="Smart Resize in Action" width="497" height="197" /><br /><em>Smart Resize in action.</em></p>

<p>For extra control over how elements in your Smart Resize group scale or are being repositioned, you can set <strong>anchor points</strong> for each individual object. For example, elements that have their <code>X</code> anchor set to the left will only scale on the <em>right side</em>; the left edge will stay fixed in proportion with the rest of the group.</p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89c62284-ded7-46d7-8b8b-f90d974ba2fe/smart-resize-anchors.png" alt="Smart Resize: Selecting Anchor Points" width="336" height="200" /><br /><em>In this example, the X anchor was set to the left, then the group was resized.</em></p>

<p>Text boxes will be resized while maintaining their text properties intact &mdash; the height and width of the text box will change, but not the text itself. John demonstrates the extension's usefulness when working with a mock-up of a dialog box on his website. But of course, there are many more cases where you can save time with this extension. Personally having used it for a couple of months now, I've found my workflow immensely optimized, especially when creating wireframes where quick changes to try out variations become the "need of the day".

## 4. <a href="https://johndunning.com/fireworks/about/Tables">Tables Panel</a>

<p>If there is one extension in this list that I would award as the "Most Underrated", it would have to be the <strong><a href="https://johndunning.com/fireworks/about/Tables" title="Get Tables Panel Extension for Adobe Fireworks">Tables Panel</a></strong> from John Dunning.</p>

<p>It does something that seems very simple but is actually much more complex and tedious: <strong>building and editing tables</strong> (painlessly!) in Fireworks. It can also be an indispensable tool for editing many other design elements, including buttons, styled boxes, and placeholders.</p>

<p>We've all been there, haven't we? Every designer knows that often the task of mocking-up a table inside a Web design (or a Web design prototype) can come up. Unfortunately, it is rare for a graphics editor to provide a decent level of support for building tables, and Fireworks is no exception. Everything from deciding whether to use rectangles for rows or individual cells, or aligning things manually every time there's a change in the design, tables in Fireworks can be a pain.</p>

<p>But things change a lot with the introduction of the "Tables" extension!</p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/934632dc-c444-4514-ace1-e8bda199cfa7/tables.gif" alt="Tables Panel: Easily Build Tables in Fireworks" width="500" height="340" /><br /><em>Tables Panel: Easily build and modify tables in Fireworks.</em></p>

<p>To create a table, you simply lay out the content of the table roughly on the canvas, in the sequence you want. Select all objects, and hit the "Create" button in the Tables Panel. The extension will add individual boxes for each element and lay them out with the height and width of the biggest element that appears in a row or column. You can change the padding, decide whether you want to see the table outlines (or not), and so on &mdash; and what's better, everything always remains editable. Lets say you changed some text in the table, and now it's too long for the cell that contains it? Simply press the "Update" button and the table will auto-adjust accordingly!</p>

<p>Apart from the obvious goal of creating tables and grids, one can use the extension in a few other scenarios. For example, you could use it in adding a background and border to text boxes for pull-quotes, so that the box always adapts to the size of text.</p>

<p>I often find myself using it for buttons when creating wireframes. It has always been very annoying to me that I have to keep managing a rectangle <em>and</em> a text field every time I need a button. With this extension it's all taken care of, and I never have to manually change the width of a new button to fit the text inside it! Besides, you can even have borders of different widths around the button by changing the border widths in the Tables Panel.</p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abaccaaf-c830-4b85-91d9-bb5d69195184/tables-button1.png" alt="Tables Panel: Creating Dynamically-Sized Buttons Quickly." width="500" height="340" /><br /><em>Tables Panel: Creating dynamically-sized buttons quickly.</em></p>

<p>The Tables Panel is pretty flexible and has many other options. You can even insert a table from a text file (tab-delimited or comma-separated text file &mdash; .txt or .csv). After you select the file, the contents of the table will be inserted at the upper-left corner of the document (you can later drag the table around and position and style it in any way that you want). You can also import a table from a Web page &mdash; you'll just need to first convert it to tab-delimited or CSV format. </p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb20211e-85a7-47f7-80ce-f9f4573ee28c/tables-panel-settings.png" width="500" height="350" alt="Tables Panel" /><br /><em>Tables Panel: it provides you with a high level of customization and with various options.</em></p>

<p>As you can see, the possibilities for working with tables are almost unlimited. All of this is possible again thanks to the power of Fireworks and the talented extension developers that give so much to the community!</p>

## 5. <a href="https://johndunning.com/fireworks/about/Placeholder">Placeholder Auto Shape</a>

<p>If you use Fireworks extensively for wireframing, you are no doubt aware of the frustration of maintaining <em>placeholder boxes</em> and the necessary information contained within. I usually draw gray boxes for my images and include a descriptive label, the height and width co-ordinates within the box. The problem is, this metadata often needs to change with the size and position of the placeholder. Updating this information manually and re-aligning the text so that it is always in the center can be a pain.</p>

<p>John Dunning to the rescue again, with his <strong><a href="https://johndunning.com/fireworks/about/Placeholder" title="Get Placeholder Extension for Adobe Fireworks">Placeholder</a></strong> auto shape extension.</p>

<p>To create an image placeholder, pick this auto shape from the Tools panel (instead of the standard Rectangle tool), and it will draw a box with the necessary data already filled in. Every time you resize and reposition the placeholder, the coordinates will automatically update as necessary.</p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b657fbb-5109-4f19-95be-9afe8e3e9545/placeholder.png" alt="Placeholder Auto Shape: Dynamic Placeholders that Always Stay Up-To-Date" width="500" height="400" /><br /><em>Placeholder auto shape: Dynamic placeholders that always stay up-to-date.</em></p>

<p>It's interesting to mention that the Placeholder tool can be found in the Tools panel. But also, this extension installs a <em>Placeholder auto shape</em>, which can be found in the Auto Shapes panel. Both the tool and the auto shape do the same thing, and the difference between their use is very minor (you can select the Placeholder tool and drag it to any size on the canvas, while the Placeholder auto shape should be first dragged and dropped to the canvas, and then resized).</p>

<p>As you can see in the screenshot above, you can decide what information gets displayed in the placeholder. The choice is between showing a custom label for the placeholder (like "logo", "screenshot", "banner", etc.), and the coordinate of the image (height, width, x &amp; y coordinates). Clicking the crosshairs in the middle of the placeholder opens up a dialog box where you can turn these details on or off. You can also change the size and position of the paceholder precisely right from within this dialog box and change (or remove) the fill color.</p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb123b1b-6974-4126-ae60-9fab002fe47b/placeholder-controls.png" alt="Placeholder Auto Shape: Choose What Content You Want on the Placeholder" width="500" height="410" /><br /><em>Placeholder auto shape: choose what content you want on the placeholder.</em></p>

<p><strong>Useful tip:</strong> If you have multiple placeholder shapes in your file, you can select them and <em>resize them all at the same time</em>. Neat!</p>

## 6. Orange Commands

<p>If there's anything I would call a Swiss Army Knife for Fireworks, it would have to be <strong>Orange Commands</strong> by Ale Muñoz.</p>

<p>Unlike every other extension in this roundup that focuses on a single task or a group of tasks, Orange Commands aim to bring efficiency to tasks across your entire Fireworks workflow. From aligning objects, to setting guides around selected objects, to combining two text objects into one &mdash; Orange Commands are a collection of small tasks that you would typically perform through a series of steps. And what's more, they're not only free, but are also <em>open-source</em>, letting anyone with enough know-how to tweak and extend them even further!</p>

<p>Here are a few of my favorite commands from the 100+ that this extension comes with:</p>

<ul>

<li>Most designers don't know this, but there is a way to change the alpha / opacity of a stroke in Fireworks CS5.1 as well as earlier versions. Unfortunately, to change it you will need to go into the "Edit Stroke" panel and then inside "Advanced" to get to this control &mdash; the feature is pretty much buried. Orange Commands bring this ability right up to a single click with the <strong>Stroke Alpha</strong> set of commands under <strong>Alpha</strong>.

(Using Fireworks CS6? You're lucky! A few new options were added in the Properties panel, which include <em>independent control</em> over the opacity of both stroke and fill!)

<li>If you like to number your pages so they appear in a specific sequence after being exported, just set them in the right order in the Pages panel. Then hit <strong>Numberize</strong> under <strong>Pages</strong>, which adds a number in front of the name for each page. Need to change the order? Reorganize the pages and hit the command again. There is also a <strong>De-Numberize</strong> command that will let you get rid of those numbers, if needed.</li>

<li>Need to swap the position of two objects in your design? Select them and hit the <strong>Swap</strong> command under <strong>Position</strong>. Easy!</li>

<li>Fireworks has shortcuts for aligning multiple objects to each other, but you still need the Align panel if you want to align something in reference to the canvas. That's where the <strong>Center on canvas</strong> set of commands under <strong>Align</strong> comes into play.</li>

<li>You can use the <strong>Space horizontal</strong> and <strong>Space vertical</strong> commands under <strong>Align</strong> to distribute selected objects with a specified distance between them.</li>

</ul>

<p>This is just a small part of what Orange Commands can do. You can check out the detailed documentation for more details on what's available.</p>

<p>Since Fireworks lets you assign keyboard shortcuts to all menu items, you can assign them also to your favorite commands, converting any series of steps into single, keyboard-driven actions. Although I have a few favorite ones, virtually every one of the commands has contributed to "shaving" precious seconds off my workflow, which amount to <strong>hours saved</strong> every month.</p>

<p><strong>Useful tip:</strong> Did you know that Orange Commands come with their <em>own keyboard shortcut sets</em> that pair perfectly with the commands themselves? If you'd like to use one of them, simply copy the shortcut XML files to the "Keyboard Shortcuts" folder (see "Installation" for reference), restart Fireworks, and then select one of the "+ Extras" sets. Of course, you can can further customize these shortcut sets, as well.</p>

## 7. <a href="https://johndunning.com/fireworks/about/QuickFire">QuickFire Command</a>

<p>With the large number of useful extensions available for Fireworks, it doesn't take very long before your "Commands" menu becomes overcrowded with items. At this point it could be really difficult to get to the command you need <em>right at that moment</em>. On the other hand, remembering countless shortcuts for quick access of all the commands, panels and menu items in Fireworks can also be difficult.</p>

<p>And that's where <strong><a href="https://johndunning.com/fireworks/about/QuickFire" title="Get QuickFire Extension for Adobe Fireworks">QuickFire</a></strong> comes into play. This extension is again from John Dunning, and it is a fitting tribute to the power and flexibility of Fireworks. QuickFire is similar to <a href="https://qsapp.com/">Quicksilver</a> on Mac OS and <a href="https://www.launchy.net/">Launchy</a> or <a href="https://colibri.leetspeak.org/">Colibri</a> on Windows. It is a super simple, keyboard-driven interface for getting to the Fireworks command you need, without all the slow digging through various menus and sub-menus.</p>

<p>Once you've installed QuickFire, assign a keyboard shortcut to it and restart Fireworks. Then, when you hit the QuickFire key combination, you can start typing what you need. It will instantly list everything that matches what you are typing, with various icons to easily differentiate between panels, commands, auto shapes, pages and more! The most relevant item will be at the top of the list and ready to be run once you press <code>Enter</code>. The icing on the cake is that QuickFire works with everything in Fireworks, and not only the custom commands that you have installed.</p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6f959ca-3eea-4f5d-bd7d-5fcfcc8ab6be/quickfire-static.png" alt="QuickFire: Access any Command, Panel and Auto-Shape in Your Fireworks Set-Up with a Few Keystrokes." width="500" height="280" /><br /><em>QuickFire: access any command, panel and auto shape in your Fireworks set-up with a few keystrokes.</em></p>

<p>Let me take a real-life example to demonstrate how I use the QuickFire panel to increase my productivity in Fireworks on a day-to-day basis. Let's say I need three lines that I need to align to each other, position them with even spaces from one another and add vertical shadows to each one. Here's how I do it (without ever touching the mouse) once I've drawn and selected one of the lines:

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ce9801a-2a31-405c-9fe9-cf22a5d8d030/quickfire.gif" alt="QuickFire: Lightning Fast Editing Workflow." width="500" height="340" /><br /><em>QuickFire: lightning fast editing workflow.</em></p>

<p><strong>Useful tip:</strong> When you open QuickFire and search for a specific command in the list, pressing <code>Enter</code> normally executes the selected command and closes the dialog, while pressing <code>Shift + Enter</code> runs the selected command but <em>keeps QuickFire open</em> &mdash; this will allow you to run several commands in a row (and save a few more keystrokes).</p>

<p>QuickFire offers many more productivity enhancements. It will let you:</p>

<ul>
  <li>Open panels quickly.</li>
  <li>Insert Symbols from the Common Library.</li>
  <li>Insert Auto Shapes.</li>
  <li>Access standard Fireworks menu commands.</li>
  <li>Apply textures and patterns to selected objects.</li>
  <li>Open recent files or create new files from templates.</li>
  <li>Select layers and pages, and also move or copy selected objects across layers and pages.</li>
</ul>

<p>Again, you can check the detailed description of QuickFire and its common uses on <a href="https://johndunning.com/fireworks/about/QuickFire">John's website</a>.</p>

## Conclusion

<p>As you have probably already guessed, I'm a huge fan of extensions and use them quite regularly in my design workflow with Adobe Fireworks. The list of extensions I use on a daily basis is much longer than what I can include in just one article &mdash; what's covered here are just a few of them that address critical areas in Fireworks, to make a designer's life a bit easier. And please note: in a possible follow-up to this article, I'll try to review in detail a few more extensions that address several more specific areas within Fireworks.</p>

<p>Also, with the sheer number of extensions available for Fireworks, I've only scratched the surface of <strong>what's possible</strong>. If you feel I missed any important ones, do let me know in the comments &mdash; I would love to learn about those and try experimenting with them myself.</p>

### (In)complete List Of Useful Resources

<p>Finally, I think that this article should end with a list of places to get (or to learn about) the best extensions for Fireworks:</p>

<ul>
  <li>“<a href="https://www.fireworksinterviews.com/">Fireworks Interviews</a>”<br />The idea behind this project is to interview designers all around the world who use Adobe Fireworks on a daily basis. You'll also see there are quite a few recommended extensions (with tips and tricks) by many skillful designers, such as: <a href="https://fireworksinterviews.com/keith-lang">Keith Lang</a>, <a href="https://fireworksinterviews.com/nick-myers">Nick Myers</a>, <a href="https://fireworksinterviews.com/benjamin-de-cock">Benjamin De Cock</a>, <a href="https://fireworksinterviews.com/jonathan-snook-97516">Jonathan Snook</a> and many others.</li>
  <li>“Extending Fireworks”<br />All about articles on Fireworks extensions and commands, interviews with their authors and helpful tips. The website is relatively new but already has a few valuable resources posted on it.</li>  
<li>“<a href="https://fwpolice.com/">Fw Police</a>”<br />Brings many free resources to people using Adobe Fireworks &mdash; extensions, Fireworks PNG files and other freebies. (By the way, the same FwPolice guys are now working on a <a href="https://adobefireworks.org">new project</a> that will relate to Fireworks extensions, as well.)</li>
  <li>“Adobe Fireworks: The Most Awesome Extensions”<br />Designer Mikko Vartio talks about his favorite extensions and what they do.</li>
  <li>“<a href="https://www.idux.com/2012/07/11/favorite-adobe-fireworks-extensions/">Favorite Adobe Fireworks Extensions</a>”<br />A long list of Fireworks extensions, prepared by UX designer Dave Hogue.</li>
  <li>“<a href="https://johndunning.com/fireworks/">John Dunning's extensions</a>”<br />John Dunning's extensions for Fireworks. Make sure to check all of them out!</li>
  <li>“<a href="https://fireworks.abeall.com/">Aaron Beall's extensions</a>”<br />Aaron Beall (who is an experienced user and developer for both Fireworks and Flash) has some pretty useful extensions, too.</li>
  <li>“<a href="https://www.mattstow.com/fireworks.html">Matt Stow's extensions</a>”<br />Matt Stow has a few extensions that will help any professional Web designer and developer.</li>
  <li>“<a href="https://www.adobe.com/cfusion/exchange/index.cfm?s=5&amp;from=1&amp;o=desc&amp;cat=-1&amp;l=-1&amp;event=productHome&amp;exc=6">Fireworks extensions | Adobe Exchange</a>”<br />List of all Fireworks extensions published on the Adobe Exchange website.</li>
</ul>

### Further Reading
<ul>
<li><a href="https://www.smashingmagazine.com/2009/08/18/mastering-photoshop-with-paths/">Mastering Photoshop With Paths</a></li>
<li><a href="https://www.smashingmagazine.com/2011/09/16/an-in-depth-study-of-symbols-in-illustrator-cs5/">An In-Depth Study Of Symbols In Illustrator CS5</a></li>
<li><a href="https://www.smashingmagazine.com/2009/10/12/setting-up-photoshop-for-web-app-and-iphone-development/">Setting Up Photoshop For Web, App and iPhone Development</a></li>
</ul>

<em>(mb) (jvb)</em>


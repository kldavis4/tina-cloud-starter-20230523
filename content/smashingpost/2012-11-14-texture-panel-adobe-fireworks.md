---
title: Using The Texture Panel In Adobe Fireworks
slug: texture-panel-adobe-fireworks
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b86faae6-ccdc-49ff-a136-2ba142d82de4/psych-7.jpg
date: 2012-11-14T13:18:15.000Z
author: matt-curtis
summary: >-
  When you’re working in Fireworks &mdash; be it for a website design, mobile design or graphic asset for a project &mdash; one need you will undoubtedly have is support for textures. While Fireworks is an amazing tool in other areas, the usability of the textures feature could definitely be improved. In this article, we’ll look at an extension that does just that: the Texture Panel.
description: >-
  When you’re working in Fireworks &mdash; be it for a website design, mobile design or graphic asset for a project &mdash; one need you will undoubtedly have is support for textures. In this article, we’ll look at the Texture Panel.
categories:
  - Fireworks
  - Tutorials
  - Extensions
---
Currently in Fireworks, you can apply textures (which are pulled from your “Textures” folder) to whatever vector shape you’re working on. Unfortunately, the way Fireworks lists textures isn’t as intuitive (or fast) as it could be. As it is, you’re presented with a text listing of all of your textures.

When you mouse over a name, a preview window of that texture pops up, but there is no easy way to get to or to quickly identify your most commonly used textures, and if you often use a lot of textures (like I do), your workflow can get cramped a bit.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/065137fc-a467-41db-bc97-cffec3e1147e/article-images-11.png" alt="Applying a texture in Fireworks." width="500" height="499" /><br>
<em>Applying a texture in Fireworks (using the Properties panel).</em>

Being a Fireworks user myself, after noticing this issue, I got right to work on finding an improvement. OK well, not <em>right</em> to work &mdash; I had never made a Fireworks extension before, and this kind of thing always has a learning curve, right?

- [Download the Texture Panel extension](https://sourceforge.net/projects/texturepanel/)

{{% feature-panel %}}

## A Dedicated Texture Panel To The Rescue

First, I did some research to see whether an extension of such sort had been made before. I found a few, but many of them were unmaintained or not up to my standard of quality. So, I said “Why not? It’ll be fun!” (which I think every developer should say now and then), and started developing my own extension. I wanted to create something that would do the following:

*   Sort textures into lists,
*   Optionally display the textures as thumbnails,
*   Provide an intuitive interface to manipulate textures,
*   Allow you to add your own textures and refresh the current list,
*   Make you coffee (OK, maybe not, but that would be a nice feature).

I built my first prototype with the help of John Dunning’s <a href="https://johndunning.com/fireworks/about/JSMLLibrary">JSML Library</a>, which makes it a snap for anyone looking to develop a panel. It basically enables you to write the panel in JavaScript. Ultimately, though, I had to use native <a href="https://www.adobe.com/products/flex.html">Flex</a> and <a href="https://www.adobe.com/devnet/actionscript.html">ActionScript 3</a> &mdash; neither of which I knew &mdash; to make the panel into what I wanted. I had to figure out a lot of stuff for myself, but I was right about one thing: the experience was fun! Mostly.

My work resulted in what I call the Texture panel. (A pretty creative name, don’t you think?)

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b07aca5e-a0ea-49e9-9652-eaa7d863b54d/panel-shot.png" alt="Texture panel screenshot" width="285" height="366" /><br>
<em>The Texture panel</em>

After some brief instructions, we’ll highlight the features and options of the panel.

{{% ad-panel-leaderboard %}}

## Downloading And Installing

First, download the Texture panel.

After downloading the installation MXP file, double-click it, and the Adobe Extension Manager should take over from there. I’ve tested this extension only with Fireworks CS5 and CS6, but there should be no issues with other versions.

<strong>Note:</strong> While we’re discussing application versions and compatibility, it’s worth noting that in Fireworks CS6, you can place textures located in the “Textures” folder into subfolders, and Fireworks will automatically load them in its textures list. This differs from the behavior of Fireworks CS5.1 and older, where texture files in subfolders aren’t read and, when placed there, remain unlisted (i.e. “invisible” to Fireworks). Now in Fireworks CS6+, the panel adapts to this and will list subfolder textures.

## Using The Panel

After installing the extension, you can open the panel via the menu <code>Window → Texture Panel</code>. If you use the default workspace layout in Fireworks, I recommend dragging the panel into the panels sidebar on the right.

<img loading="lazy" decoding="async" class="114189" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4af68b98-9d82-45bb-8fbf-a263b745182e/icon-in-the-sidebar.png" alt="Sidebar with panels in Fireworks" width="285" height="342" /><br>
<em>The Texture panel icon in the panels sidebar</em>

The Texture panel’s interface is divided into three main areas: <strong>display area, bottom toolbar, top toolbar</strong>. Let’s look at each in detail.

### Display Area

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a275a92e-6fa9-46e1-8a46-bfc555c3268b/display-area.png" alt="Display area" width="283" height="364" /><br>
<em>Texture panel: display area</em>

The most immediate and important part of the panel is the display area. By default, it displays your textures as thumbnails. Clicking a thumbnail applies that texture to whatever object (or objects) is currently selected.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/975515b5-eca6-46e9-a659-73943e9f8fc2/applying-a-texture-with-the-tp.png" alt="Applying a texture with the Texture panel" width="500" height="373" /><br>
<em>Applying a texture in the panel</em>

<strong>Note: Make sure that your texture's opacity is greater than zero, or you will not notice the added texture.</strong> Secondly, make sure that the object you’re applying a texture to has a stroke or fill; otherwise, you’ll get an error message. Below, for example, we’re trying to apply a fill texture to an object that doesn’t have a fill.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/998eea19-fbd9-421d-b86c-d00a2c57f655/error-message.png" alt="Error message" width="500" height="389" /><br>
<em>You’ll get an error message if an object does not have a fill. A similar message shows up if you try to apply a stroke texture to an object that does not have a stroke.</em>

The display area has two views, <strong>list and tiled</strong>, which you can toggle with a button in the bottom toolbar.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0b2e06e-8e19-4bcd-887d-2105781ccd5c/display-area-views1.png" alt="Switching views" width="500" height="600" /><br>
<em>Switching between list and tile view is very easy: just click the dedicated button at the bottom of the panel.</em>

The size of the thumbnails can be changed in the panel’s settings area: <code>Settings → View → Texture Size: [enter size in pixels] → Save</code>.

### Bottom Toolbar

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0b556c3-b8c6-448d-8d63-c750cdcd4f43/bottom-bar.png" alt="Bottom toolbar" width="309" height="438" /><br>
<em>Texture panel: bottom toolbar</em>

The <strong>settings</strong> button takes you to the settings (which we’ll look at later). With the <strong>opacity control</strong>, you can enter a specific level (0 to 100) or use the pop-up slider. The <strong>miscellaneous</strong> button opens a menu with a few simple options to add and reload textures. (We covered the button for the list and tile view, to the left of the miscellaneous button, in the previous section.)

### Top Toolbar

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a3a7664-9027-4d11-b69b-7ab4e46ddd90/top-bar.png" alt="Top toolbar" width="295" height="410" /><br>
<em>Texture panel: top toolbar</em>

The <strong>lists</strong> button shows a menu that lets you switch between whatever lists you’ve created. The <strong>search</strong> field lets you search all of your textures by keyword. The <strong>“Fill” and “Stroke”</strong> toggle lets you choose whether the texture you click on is applied to the fill of the object or to the stroke.

## Playing With Settings

When you click the settings button, you’re taken to a dialog that gives a couple of options.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7197049-4b95-4319-a42c-dbd5b9dfc2c8/settings-shot.png" alt="Settings in the Texture panel" width="285" height="366" /><br>
<em>Settings in the Texture panel</em>

Under the “View” tab, the only option, “Texture size,” is fairly straightforward. Changing it to 30, for example, would make the thumbnails in the list view 30 × 30 pixels and would make the tiles in the tile view 30 pixels in height.

Enter any value here that suits your needs.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ac5868b-1547-4b53-b9e1-8e1312cc45aa/texture-size.png" alt="Texture size setting" width="500" height="499" /><br>
<em>Here we’re changing the size of the thumbnails to 30 × 30 pixels. What are these, thumbnails for ants?!</em>

The “Other” tab has just one option, “Auto-select texture.” If it’s enabled, then whenever you select a vector object in Fireworks, the panel will update to whatever texture the object has.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9020f09-1f3a-40b0-9b7a-f42ae0bd9719/auto-select-option.png" alt="Auto-select option" width="285" height="366" /><br>
<em>The Auto-select option</em>

Once you’re ready, clicking the “Save Settings” button will do the obvious. Then, you will automatically return to the main view of the panel.

## Organizing Textures: Using Lists

By clicking the “Edit Lists” button, a dialog window will pop up, where you can create and delete lists and perform a few other tasks.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/990c195b-c5e4-4017-943b-93a2eebfb214/list-dialog-thumb.png" alt="List dialog" width="492" height="342" /><br>
<em>The list dialog (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/647c830d-9f77-4e49-8023-4b9d265e4407/list-dialog.png">large view</a>)</em>

The list dialog has three main areas: display area, sidebar, toolbar.

### Display Area

Like the Texture panel itself, the list dialog has a display area.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ad0b44b-8f22-4d45-aefb-f6f152999156/list-dialog-display-area.png" alt="List dialog - display area" width="500" height="499" /><br>
<em>List dialog: display area.</em>

The process of organizing textures into lists is pretty intuitive. It works in a drag-and-drop Explorer-type way: select (i.e. click on) a thumbnail, and then drag it to whatever list you want to assign it to.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/406128ec-961a-416b-bc0c-fcfb2df28908/list-dialog-drag-example.png" alt="List dialog - drag-and-drop example" width="497" height="456" /><br>
<em>To add a texture to a list, click on its thumbnail, and then drag it to a list on the left.</em>

Dragging <strong>multiple textures</strong> to a list is easy, too. Just select the ones you want using the standard <code>Control/Command</code> or <code>Shift</code> shortcuts. You can also use the <code>Delete</code> key to remove a texture from a list. (Note that the <code>Delete</code> command does not remove the texture from your computer, only from the list.)

### Lists Sidebar

The sidebar displays all of your lists. Clicking on a list name will display all of the textures contained in that list.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcc1e830-8f26-4d31-b2e9-e5dbd1d7e83c/list-dialog-list-example.png" alt="List dialog - list example" width="500" height="446" /><br>
<em>Viewing textures in the “Stripes” list</em>

You can also perform certain tasks on a list. When you mouse over a list’s name, a little arrow will pop up to its right, containing a menu with several options.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fd8234a-1447-47d9-abc9-452df32ec153/list-menu-screen.png" alt="List menu screenshot" width="500" height="152" /><br>
<em>Clicking this arrow will open a menu with a few options: “Empty” the list of all items, “Delete” the list, and “Edit” the list’s name.</em>

Also, double-clicking a list lets you quickly change its name.

To delete a list, either select the “Delete” option in the menu or press the <code>Delete</code> key.

### Lists Toolbar

<img title="List dialog toolbar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45d8c8d0-a140-4ce4-8224-7206099deba5/list-dialog-toolbar.png" alt="" width="515" height="145" /><br>
<em>Lists dialog: toolbar (at the top)</em>

Let’s go through what clicking these buttons will do:

*   “New List” Create a new list. (Surprise!)
*   “Show all textures” Show all textures (as opposed to the textures in whatever list is currently selected).
*   “Show unsorted textures” Show all textures that haven’t been assigned to a list.

Once you’re done making changes to your lists and organizing the textures in them, click “Save Changes” (in the top right of the lists toolbar), and you’ll return to the main view of the Texture panel.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/612e1ef4-544f-43e6-aace-9cb8f7062777/lists-save-changes.png" alt="Lists menu (Save Changes button)" width="500" height="112" /><br>
<em>List dialog: “Save Changes” button</em>

(Of course, exiting the lists dialog <em>without</em> saving your changes is also possible. Just close it by clicking the “x” in the top right, and you’ll return to the main view of the panel.)

### Accessing the List Menu

In the Texture panel, you can easily open the list menu by clicking the “Lists” button in the top left. From there, you can switch between displaying textures in a selected list and showing all available textures.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fa3546e-b15e-4f32-b11a-587856ec4c5b/lists-menu.png" alt="List menu" width="285" height="366" /><br>
<em>The list menu in the Texture panel</em>

## Conclusion (And Future Plans)

Fireworks can be extended and adapted to suit your needs. I have built the Texture panel to enable me to work more easily with textures; hopefully, the extension will help you, too.

In the future, I plan to add more features to the panel. One feature is the ability to export and import lists; if you use many custom textures and spend a lot of time organizing them into lists, then this option would come in very handy &mdash; it will be probably added in version 2.2. So, your suggestions, ideas and bug reports are more than welcome.

Once you’ve tried the panel, I’d be happy to answer any questions you have about using its features.

{{% ad-panel-leaderboard %}}

### Additional Resources

Many other free extensions created by the Fireworks community will increase the power and versatility of this screen design tool. Here are some of my favorite collections by developers:

*   [Aaron Beall](https://fireworks.abeall.com/extensions/)
*   [John Dunning](https://johndunning.com/fireworks/)
*   [Matt Stow](https://www.mattstow.com/)
*   Ale Muñoz (a special set dubbed “Orange Commands”)
*   [Linus Lim](https://phoenix-project.posterous.com/)

And a couple of helpful resources:

*   [Fireworks Interviews](https://fireworksinterviews.com/) Interviews with a variety of Fireworks designers.
*   [Fireworks Police](https://fwpolice.com/) An updated collection of Fireworks resources.

Finally, if you’re interested in developing extensions for Fireworks, I highly recommend John Dunning’s <a href="https://johndunning.com/fireworks/about/JSMLLibrary">JSML Library</a>, which makes panels a snap to build.

In the coming weeks I plan to write another article that looks in depth at developing Fireworks extensions, so keep an eye on Smashing Magazine’s <a href="https://www.smashingmagazine.com/">Fireworks section</a>.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Sketch, Illustrator or Fireworks?](https://www.smashingmagazine.com/2016/04/exploring-a-new-illustration-ui-design-app-gravit/)
*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [The Present And Future Of Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

{{< signature "al, mb, il" >}}
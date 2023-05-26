---
title: Sketch With Material Design
slug: sketch-with-material-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c0668e0-0838-4e61-998f-a81ee83bfefa/04-sizes-opt-small.png
date: 2015-05-15T14:21:46.000Z
author: patrickkeenan
description: >-
  In the past year, adoption of
  [Sketch](https://www.smashingmagazine.com/2015/04/17/using-sketch-for-responsive-web-design-case-study/)
  at Google, where I work at, has taken off and is now a widely preferred tool.
  The more tools in our belts, the better, so here’s my take on why Sketch and
  the new material design system are a great match.

  Tools are an extension of our hands, and as such, they should be versatile,
  quick and intuitive. A lot has changed between the print era of offset presses
  and the digital era of cross-platform screens. Developers have attempted to
  adapt our tools, but
  [Sketch](https://www.smashingmagazine.com/2015/01/30/prototyping-ios-android-apps-sketch-freebie/)
  is perhaps the most successful app in this regard — its creators have removed
  the bloat, started afresh and presented a smaller, fit-for-purpose feature
  set. What may seem on the surface to be a simple drawing tool in fact nails
  the core workflows of digital design.
categories:
  - Graphics
  - Tools
  - Sketch
  - Material Design
---
In the past year, adoption of <em>Sketch</em> at Google, where I work at, has taken off and is now a widely preferred tool. The more tools in our belts, the better, so here’s my take on why Sketch and the new <a href="https://www.smashingmagazine.com/2015/07/material-design-icons-templates-tools/">material design</a> system are a great match.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Getting The Sketch Workflow Right: Meet “The Sketch Handbook”</span>](https://www.smashingmagazine.com/sketch-handbook/)
*   [Using Sketch For Responsive Web Design (A Case Study)](https://www.smashingmagazine.com/2015/04/using-sketch-for-responsive-web-design-case-study/)
*   [Material Design Icons, Goodies And Starter Kits](https://www.smashingmagazine.com/2015/07/material-design-icons-templates-tools/)
*   [Prototyping iOS And Android Apps With Sketch (With A Freebie!)](https://www.smashingmagazine.com/2015/01/prototyping-ios-android-apps-sketch-freebie/)

Tools are an extension of our hands, and as such, they should be versatile, quick and intuitive. A lot has changed between the print era of offset presses and the digital era of cross-platform screens. Developers have attempted to adapt our tools, but Sketch is perhaps the most successful app in this regard — its creators have removed the bloat, started afresh and presented a smaller, fit-for-purpose feature set. What may seem on the surface to be a simple drawing tool in fact nails the core workflows of digital design.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8874d88b-2d9a-4fa9-aeae-b5b46c5dc689/01-stickersheet-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d20fb9bf-51dc-46da-89ae-224751c21504/01-stickersheet-opt-small.png" alt="Sketch 3.2 comes ready with a material design sticker sheet to give you a jumpstart on new projects." /></a><figcaption>Sketch 3.2 comes ready with a material design sticker sheet to give you a jumpstart on new projects. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8874d88b-2d9a-4fa9-aeae-b5b46c5dc689/01-stickersheet-opt.png">View large version</a>)</figcaption></figure>

{{% feature-panel %}}

The latest version of Sketch (3.2) ships with something special for those interested in Google’s latest visual design language: the material design sticker sheet. In this tutorial, we’ll design a test app with the help of Sketch and the material design sticker sheet.</p>

## Let’s Create a Notes App!

In this article, we’re going to make a very simple app — a notes app. Luckily for us, all of the components we need are already available in the latest Sketch app. These are the screens we’ll create:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdffe4c8-b71d-444b-a110-773a3ef4609e/02-allscreens-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73e3234b-dae9-41b8-be70-0e9826bf7465/02-allscreens-opt-small.png" alt="The exported screens" /></a><figcaption>The exported screens.(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdffe4c8-b71d-444b-a110-773a3ef4609e/02-allscreens-opt.png">View large version</a>)</figcaption></figure>

You can also download the <a href="https://smashingmagazine.com/provide/sketch-material-design.sketch.zip">Sketch file</a> (ZIP) that was used to make this notes app prototype; it could help you along in the tutorial.</p>

### The Template

In our template — <code>File → New from Template → Material Design</code> — you’ll see a wide set of components, icons and layouts. The sheet itself was designed by the hardworking material design team at Google and has been ported with the love and care of Amar Sagoo and myself. The groups and objects are named, styled and organized in a truly Sketch-friendly way.</p>

### It All Starts With an Artboard

With your new document open — <code>File → New</code> (or <code>Command + N</code>) — press the <code>A</code> key (which is a shortcut for the Artboard tool). You can draw an artboard just as you would draw a shape, a slice or any other object. That’s because Sketch has a simple set of objects that all work the same way (more on that later). When the Artboard tool is selected, you can see on the right side a list of artboard sizes, including — you guessed it — all of the material design sizes. Click on the “Mobile Portrait” size and a white box should appear.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4f17aa5-2014-4786-a1c2-2cc4b8e83cd2/03-artboards-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4855f5f-4a2d-4dd7-8b9b-b92fa28d63e5/03-artboards-opt-small.png" alt="Sketch 3.2 provides the material design sizes within the new Artboard tool." /></a><figcaption>Sketch 3.2 provides the material design sizes within the new Artboard tool. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4f17aa5-2014-4786-a1c2-2cc4b8e83cd2/03-artboards-opt.png">View large version</a>)</figcaption></figure>

## Sketch’s Killer Feature #1: Scale-Independent Exports

<strong>Note:</strong> Material design is defined using <a href="https://developer.android.com/training/multiscreen/screendensities.html#TaskUseDP">density-independent pixels</a>. As the <a href="https://developer.android.com/training/multiscreen/screendensities.html">Android Developers page explains</a>, a density-independent pixel (DP) unit corresponds to the physical size of a pixel at 160 DPI. Though we’ll be using <a href="https://en.wikipedia.org/wiki/Pixel">pixel units</a> (<code>px</code>) in this Sketch tutorial, these are really density-independent pixels because you can scale them up or down upon exporting.

In today’s world, you can’t depend on the same pixel density, so DP units allow us to talk the same language when dealing with different device layouts. Sometimes you may be compelled to work at double or triple pixel size because you want to match the pixel size of your surface — don’t go down that route.

Stay at 1x pixels and then just <strong>export</strong> at the upscaled sizes. Sketch makes that as easy as a simple drag and drop. You’ll see a panel in the bottom left showing you the sizes slotted for exports, and you can even add your own suffix conventions for file names. When you do an “Export All” operation (<code>Command + Shift + E</code>), you’ll see that artboard, and Sketch will export all versions of the bitmap.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e1309b-ddc2-46da-bc53-aae597f07a4f/04-sizes-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c0668e0-0838-4e61-998f-a81ee83bfefa/04-sizes-opt-small.png" alt="Always work at 1× pixels. You can easily scale up or down in the “Export” panel." /></a><figcaption>Always work at 1× pixels. You can easily scale up or down in the “Export” panel. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e1309b-ddc2-46da-bc53-aae597f07a4f/04-sizes-opt.png">View large version</a>)</figcaption></figure>

Now, head to the sticker sheet template and select the “mobile global elements” artboard. Only the important stuff there is selectable, so just click on that artboard and copy and paste into your document. You now have the basic layout of a mobile material design app. As you can see in the Layers panel, you have a group named “screen”. You’ll only need the contents of that group, so just go ahead and ungroup (<code>Command + Shift + G</code>) the “screen” group. You’ll now see four layers:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90fad54a-2c4c-4a57-a415-c163da7bf9ae/05-globalelements-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3c24409-da3b-4fd6-99ef-dee0c9df3993/05-globalelements-opt-small.png" alt="In the sticker sheet, you’ll find some ready-made artboards that you can copy and paste directly into your sketch file." /></a><figcaption>In the sticker sheet, you’ll find some ready-made artboards that you can copy and paste directly into your sketch file. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90fad54a-2c4c-4a57-a415-c163da7bf9ae/05-globalelements-opt.png">View large version</a>)</figcaption></figure>

*   **navbar**.  This is a symbol (symbols in the Layers panel are marked with purple color), which means it will be the same everywhere, and if you change the contents of the symbol, it will change everywhere in the file.
*   **status bar**.  This is the top bar on the screen with Wi-Fi, time and status information.
*   **app bar**.  This is your main navigation header, which displays the name of the current page and a button to go up or open the drawer.
*   **screen bg**.  This is a background color, but it’s also a mask. You can delete this because your artboard will act as the mask for your screen.</p>

## Masks in Sketch Work… Upward!

In Sketch, masks work upward, meaning that layers above a masking object are cropped by that object. In Adobe Illustrator, however, you would place a shape on top of other layers to create a clipping mask; this threw me off at first. For more on masks, check <a href="https://bohemiancoding.com/sketch/learn/">Bohemian Coding’s documentation</a>.

If you move these layers around within an artboard, you’ll see that they are masked by that artboard. That’s the only case when an object that is higher in the Layers panel masks the objects below. Artboards always mask their contents and also house the coordinate space; so, an x value of <code>0</code> and a y value of <code>0</code> would mean the top-left corner.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9cd5fbd-089e-4eae-9125-5b93de112c9f/06-cards-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea800e8a-0f12-42a8-9f28-fc01aae7ba6f/06-cards-opt-small.png" alt="Cards are a standard pattern and work well for heterogenous information." /></a><figcaption>Cards are a standard pattern and work well for heterogenous information. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9cd5fbd-089e-4eae-9125-5b93de112c9f/06-cards-opt.png">View large version</a>)</figcaption></figure>

Let’s go back to the sticker sheet. Let’s grab the half-width <a href="https://www.google.com/design/spec/components/cards.html">card components</a> and paste them in our composition. The suggested margins for these cards is 8 pixels, so go ahead and space them out.</p>

## Sketch’s Killer Feature #2: Hover Guides

One of Sketch’s most useful features has to do with spacing: Select an object, hold down <code>Alt</code>, and then mouse around to see distances from your selection to other objects. And holding down <code>Command + Alt</code> and mousing around will measure objects that are deep within the hierarchy relative to other objects contained in groups.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b213b8a1-89d3-4359-8cbc-4f9aecd8395d/07-fab-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4526cac1-df66-4729-9dee-4e7eabd87fff/07-fab-opt-small.png" alt="The floating action button is a unique component in material design." /></a><figcaption>The floating action button is a unique component in material design. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b213b8a1-89d3-4359-8cbc-4f9aecd8395d/07-fab-opt.png">View large version</a>)</figcaption></figure>

Finally, let’s get the floating action button from our buttons components and put that in. It should be 16 pixels from the navbar and 16 pixels from the right side.

Great! So, we’ve got the composition for our first Material app. It’s a scrolling card view.

## The Navigation Drawer

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f29e7bf-e8d1-443b-b29b-256dc1dc5dcc/08-navdrawer-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80d9f095-9000-4f56-a47a-6a3c2da18225/08-navdrawer-opt-small.png" alt="Navigation drawers provide navigation to primary sections within the app and global functions such as account switching and configuration." /></a><figcaption>Navigation drawers provide navigation to primary sections within the app and global functions such as account switching and configuration. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f29e7bf-e8d1-443b-b29b-256dc1dc5dcc/08-navdrawer-opt.png">View large version</a>)</figcaption></figure>

To get around the various areas of our app, we’ll make use of the navigation drawer component. Let’s duplicate our original artboard: Click on the artboard in the Layers panel list or on the title of the artboard on the page, then press <code>Command + D</code>. This will duplicate the artboard and move the new artboard 100 pixels to the right. You can continue your flow simply by duplicating and modifying, which is what we’ll do now.

Grab the navigation drawer from the mobile artboard — the layer is called “side nav.” Paste it onto your new artboard. You can change the categories in the navigation, but the top area is reserved for switching user accounts.</p>

## Material Forms

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c693dc0f-9cfa-4174-9b32-bf512a55f79b/09-forms-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e360c41-6a4f-4ec0-bc2f-41b60276bf35/09-forms-opt-small.png" alt="Forms in material design morph. Depending on their state, placeholder text becomes labels." /></a><figcaption>Forms in material design morph. Depending on their state, placeholder text becomes labels. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c693dc0f-9cfa-4174-9b32-bf512a55f79b/09-forms-opt.png">View large version</a>)</figcaption></figure>

What happens when you tap that big plus button? Well, you should probably be able to make a note. Let’s grab some of the form’s components in the sticker sheet and make a new artboard for them. Here, we can make use of the keyboard, which is a symbol that can be placed whenever we need it. We’ll use the dark one to fit our dark app.</p>

## Reusing Artboards

Of course, after you’ve created a note, you should see it added to the card view. Let’s duplicate the first screen and add in our new note. Just click on the name of the artboard right above the artboard itself. Now that the artboard is selected, press <code>Command + D</code>. That will duplicate the artboard and move it 100 pixels to the right, perfect for quickly mocking up a flow.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00ae5864-2933-4e50-9481-1bdae4072bea/10-noteadded-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e53b050e-4bfe-4cdf-b879-deb4c6956c53/10-noteadded-opt-small.png" alt="You can duplicate artboards and they’ll move to the right side of your flow." /></a><figcaption>You can duplicate artboards and they’ll move to the right side of your flow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00ae5864-2933-4e50-9481-1bdae4072bea/10-noteadded-opt.png">View large version</a>)</figcaption></figure>

## Sketch’s Killer Feature #3: The Color Picker

Sketch provides a powerful color picker. Just press <code>Control + C</code> to select a color anywhere on the screen. Combining this with <code>Command</code> + click to click through to any element, you can easily recolor any object in no time.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32bb3d08-da91-4279-b25e-b062128bf31c/11-colopicker-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f7a93a7-356a-49ca-86a3-ae01dfa843fc/11-colopicker-opt-small.png" alt="The color picker is quick and accurate and can be used on anything on the screen." /></a><figcaption>The color picker is quick and accurate and can be used on anything on the screen. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32bb3d08-da91-4279-b25e-b062128bf31c/11-colopicker-opt.png">View large version</a>)</figcaption></figure>

## Covering The Tabs

Tabs are a great way to show different sets of content. In our app, we will have notes of importance and notes shared with others. Let’s make some tabs for “saved” and “shared” notes, with our current view being “all” notes. Jump back to the sticker sheet and click on the “tabs” component. Copy and paste that and position it next to the app bar. If you’ve grabbed the whole “app bar” tab from the sticker sheet, you’ll notice that it’s the wrong color. So, change the background color: Click through (<code>Command</code> + click) to the background of the tabs, and change the color to our main color. Move the tabs to the top, and you’re set.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/773a72ab-f265-4438-b35c-e7b42c59291f/12-tabs-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31de43f8-47d7-41e0-903a-1267feb823d4/12-tabs-opt-small.png" alt="Tabs allow for multiple views of the same content types." /></a><figcaption>Tabs allow for multiple views of the same content types. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/773a72ab-f265-4438-b35c-e7b42c59291f/12-tabs-opt.png">View large version</a>)</figcaption></figure>

When copying components from the sticker sheet, you can take any level of elements. This means you can take a whole screen, just the components within or even just the icons. The tabs, as well as other components, have been prepared with a transparent background. Move within the “app bar” group and you’ll be able to copy the “tabs” group and paste onto any existing background. The advantage of a transparent background is that you will get the proper spacing around the component, but you can quickly place it on top of an existing background or toolbar.</p>

## Making A List

You’ll use lists a lot. They’re a fundamental component to any app, and material design gives us a number of options. We’ll have our “shared” tab contain a list view.

Copy the “three-line item” list from the sticker sheet and paste it in a new artboard. Ungroup the list and then just <code>Alt</code> + drag to duplicate an item, a set of items or a group. Do this until you have a full page of rows.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2a03ace-4ba7-44bb-bba8-d4558ef1bbfc/13-rows-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4aa6b98b-15d5-4425-b634-beacd184a6d0/13-rows-opt-small.png" alt="Lists are a common way to display collections of data." /></a><figcaption>Lists are a common way to display collections of data. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2a03ace-4ba7-44bb-bba8-d4558ef1bbfc/13-rows-opt.png">View large version</a>)</figcaption></figure>

## Secondary Actions Are Shortcuts

You’ll notice a box on the right side of the list. This box is a secondary action. Tapping anywhere to the right of this action would open up that list item; but for quick actions (such as calling a contact or opening information about a document) you can use the secondary action. We’ll replace this placeholder box with a heart so that the user can quickly save notes.

In the sticker sheet you’ll find a small set of icons in the top left under “typography.” Grab the heart icon and paste it where the gray box is located. The icon should be in a group containing the heart icon and a transparent 24 × 24 box. This box helps with spacing, so make sure to grab the whole group.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b10e814e-a6a0-41a0-84aa-2399b3960699/14-rowssymbol-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9cec60b-8439-4532-bc68-1ce62d40e3d1/14-rowssymbol-opt-small.png" alt="Symbols allow us to quickly manipulate many instances of the same icon, component or even layout." /></a><figcaption>Symbols allow us to quickly manipulate many instances of the same icon, component or even layout. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b10e814e-a6a0-41a0-84aa-2399b3960699/14-rowssymbol-opt.png">View large version</a>)</figcaption></figure>

## Sketch’s Killer Feature #4: Shared Symbols And Styles

Now, let’s make the row group into a symbol. This will allow us to edit its contents in many places at once. When you select a group, you’ll see a field in the toolbar that says “No symbol.” Click on this field and select “Create new symbol.” The name will default to the selected group’s name: “row.” Now you’ve got a symbol!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a46a1f96-2f03-45f8-a566-8c5326613c38/15-switchsymbol-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3aacf96d-7ba9-4e55-8908-d4136cbc6dd9/15-switchsymbol-opt-small.png" alt="Symbols allow us to quickly manipulate many instances of the same icon, component or even layout." /></a><figcaption>Symbols allow us to quickly manipulate many instances of the same icon, component or even layout. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a46a1f96-2f03-45f8-a566-8c5326613c38/15-switchsymbol-opt.png">View large version</a>)</figcaption></figure>

Select each of the other row groups you’ve positioned on the artboard and, once again, click on the area that says “No symbol.” This time you’ll see your row symbol available for use; select it. Now that you’ve got a bunch of rows using the row symbol, when you change one, they will all change. Just like that, you have an interconnected set of elements.

Using our newfound power, let’s replace the heart with an overflow icon. The overflow icon is a set of three vertically stacked dots and indicates that more than one action is available. All you have to do is copy the “overflow icon” group (along with the padding) from the sticker sheet and paste it right beside the existing heart icon. Line it up with the heart icon, and then delete the heart icon. As you’re doing this, you should see the other rows automatically update. Yay for symbols!

With Sketch’s symbols, there is no editing mode. Symbols act just like groups and update immediately. This makes it easy to change symbols. Watch out, though: You may be editing a symbol in one place only to find that it has also changed in many other places across the canvas!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e8fce03-3247-4ba9-89a8-8eb84838b076/16-rowssymbol-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f20aa210-63df-4c5a-b4f1-463af3cd570a/16-rowssymbol-opt-small.png" alt="Symbols allows us to quickly switch out icons or whole compositions. But be careful: A change in one place will be reflected everywhere, even on other pages." /></a><figcaption>Symbols allows us to quickly switch out icons or whole compositions. But be careful: A change in one place will be reflected everywhere, even on other pages. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e8fce03-3247-4ba9-89a8-8eb84838b076/16-rowssymbol-opt.png">View large version</a>)</figcaption></figure>

## Bottom Sheets

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1984acbd-b510-49d5-adc8-6f8c783526a7/17-bottomsheet-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fa65c2c-5c82-4bfd-8e58-3b0363d58d7b/17-bottomsheet-opt-small.png" alt="In material design, bottom sheets display a set of actions without covering the screen. These sheets emerge from the bottom of the screen, then drop back down when dismissed." /></a><figcaption>In material design, bottom sheets display a set of actions without covering the screen. These sheets emerge from the bottom of the screen, then drop back down when dismissed. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1984acbd-b510-49d5-adc8-6f8c783526a7/17-bottomsheet-opt.png">View large version</a>)</figcaption></figure>

In material design, bottom sheets are a great way for the user to take action without leaving the current context. These enter from the bottom of the screen and display a set of actions. In our app, the bottom sheet will be invoked when the user taps the forward icon in the top right.

Let’s grab the bottom sheet from the sticker sheet and paste it in a new artboard. Also, grab the scrim (semitransparent background) from the previous navigation drawer artboard and paste it behind the bottom sheet.</p>

## Dialogs When Needed

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32a04c1b-05fe-4fb7-8579-b59d5d4b2ce5/18-dialog-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acebedda-d9a8-47fe-b2b3-c8c6ab722743/18-dialog-opt-small.png" alt="Dialogs can be used for stopping actions, but use them sparingly because they could be unnecessary roadblocks for repeated flows." /></a><figcaption>Dialogs can be used for stopping actions, but use them sparingly because they could be unnecessary roadblocks for repeated flows. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32a04c1b-05fe-4fb7-8579-b59d5d4b2ce5/18-dialog-opt.png">View large version</a>)</figcaption></figure>

As a last step, we’ll add in a dialog. This will be invoked when the user selects the delete action from the bottom sheet. In this case, we want to be really really sure that they want to delete this note. And finally, speaking of deleting, I encourage you to start fresh with your own designs. Sketch is such a quick program and material design is such an enabling guide that you can think big and different about how to delight users in your app. So, happy sketching!

## Quick Start With Sketch Resources

Here’s a list of material design resources built for Sketch to get you up and running quickly:

*   [Material design sticker sheet](https://github.com/BohemianCoding/SketchTemplates/blob/master/Material%20Design.sketch) This is the latest sticker sheet. It holds a good set of components and styles, and it is easy to copy and paste in your new compositions.
*   [Material design icon sheet](https://github.com/patrickkeenan/SketchTemplates/blob/master/Material%20Design%20Icons.sketch) This set of icons is ripped from the [Material design repository on GitHub](https://github.com/google/material-design-icons).
*   [Material design whiteframes](https://github.com/patrickkeenan/SketchTemplates/blob/master/Material%20Design%20Whiteframes.sketch) This set of colors and icons is also ripped from the [Material design repository on GitHub](https://github.com/google/material-design-icons).</p>

## Conclusion: Keep The Principle In Mind With The Tool In Hand

Thanks for walking through material design in Sketch with me and making an awesome notes app. We have not only learned a new tool, but also started on our way to a new design system.

One final note of caution: Sometime we focus on existing components and miss an opportunity to address our users’ needs in a new way. You can always check your designs against <a href="https://www.google.com/design/spec/material-design/introduction.html#introduction-goals">material design’s principles</a>:

*   **Material is the metaphor**.  A material metaphor is the unifying theory of a rationalized space and a system of motion. The material is grounded in tactile reality, inspired by the study of paper and ink, yet technologically advanced and open to imagination and magic.
*   **Bold, graphic, intentional**.  The foundational elements of print-based design — typography, grids, space, scale, color, and use of imagery — guide visual treatments. These elements do far more than please the eye. They create hierarchy, meaning, and focus.
*   **Motion provides meaning**.  Motion respects and reinforces the user as the prime mover. Primary user actions are inflection points that initiate motion, transforming the whole design.

Remember, no matter how good it looks, the greater focus is not on the pixels, but on the user. If your sight is true, all else will follow.

{{< signature "mb, al, ml" >}}


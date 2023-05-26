---
title: 'Mojo Motors’ Responsive Redesign With Fireworks: Visual Design Stage'
slug: mojo-motors-responsive-redesign-with-adobe-fireworks-part-2
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01449d62-0aba-4f4f-b9a0-8f1334ba2611/mojo-motors-illu.jpg
date: 2014-03-24T14:35:41.000Z
author: olawale-oladunni
description: >-
  In the [previous
  article](https://www.smashingmagazine.com/2013/08/26/mojo-motors-responsive-redesign-with-adobe-fireworks-part-1/)
  in this series, I discussed our ideation and initial prototyping process. In this article, we’ll share how we used Adobe Fireworks in our iterative visual design process, along with other useful tips.
categories:
  - Fireworks
  - Workflow
  - Tutorials
  - Techniques
---
We covered details on how to use Adobe Fireworks to set up a responsive design wireframe, reusable components, prototypes and ways to share designs.

In this article, we’ll share how we used Adobe Fireworks in our iterative visual design process, along with other useful tips.

Recommended reading: [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)

{{% feature-panel %}}

### In Search of the Key Design Tool

As discussed in the “Creating Wireframes And Prototypes” section of part 1, our choice of a design tool came down to the following:

*   **Speed**.  Fireworks proved to be quicker for directly creating and manipulating visual elements on the screen than other tools, like Photoshop and Illustrator. The combination of integrated vector tools and bitmap-editing capabilities in one package, plus pages, states, symbols, styles and extensions, was something unique and worked best for us.
*   **File size**.  We found that PSD visual design files created in Photoshop for the same screen designs are much larger than those created in Fireworks — sometimes **two to five times** larger.
*   **Team learning curve**.  When Gabriel Gross (our visual UI designer) joined the team, we had already created a lot of wireframes in Fireworks. He initially considered just translating those wireframes to Photoshop. Because of the amount of work that would have been required, he decided to try Fireworks on a few screens. About a week later, he suggested working directly from the Fireworks PNG wireframe files, instead of recreating the designs from scratch. From this point forward, we’ve been using the wireframe files as the starting point for visual design screens.
*   **Workflow and efficiency**.  Reusing wireframes as a staring point really helped us get from wireframes to high-fidelity visuals in record time. We were able to take advantage of the efficiencies built into sharing files and iterating on them together. For a detailed look at a similar workflow, check out “[Designing Interactive Products With Fireworks](https://www.adobe.com/devnet/fireworks/articles/cooper_interactive.html)” by Nick Myers of [Cooper](https://www.cooper.com/) and “[iOS Prototyping With Adobe Fireworks and TAP](/2013/01/ios-prototyping-adobe-fireworks-tap-part1/)” by [Shlomo Goltz](/author/shlomo-goltz/).</p>

<strong>Note</strong>: Gabriel was also familiar with Adobe Flash and its various features and quirks. The transition to Fireworks was fairly straightforward — the Properties panel that spans the bottom of the screen, navigation of nested symbols, the symbols library and so on are quite similar in Fireworks and Flash.</p>

## Exploring Branding and Style

As discussed in the previous article, the design team decided on a pragmatic approach to creating visual elements. We decided early on in the project that we would only do as much visual layout and style exploration as necessary in graphics applications — the rest would be done through an iterative process in the browser. With this in mind, we ditched any elaborate branding exercise needed just for <strong>stakeholder buy-in</strong> and opted to create style tiles and a revised logo.</p>

### So, What Are Style Tiles?

Style tiles are a design document consisting of fonts, colors and interface elements that communicate the essence of the visual brand of a website or application. They help to communicate a proposed common visual language and can be used to discuss style preferences that meet the goals of the stakeholders or client. <a href="https://samanthatoy.com">Samantha Warren</a> explains the workflow pretty well in her article on A List Apart, “<a href="https://alistapart.com/article/style-tiles-and-how-they-work">Style Tiles and How They Work</a>,” so I won’t go into deeper detail than this:
<blockquote>Websites are so much more than just usable interfaces: they tell a story...

Style tiles are a flexible starting point that define a style to communicate the web in a way that clients understand. A style tile is more refined than a traditional identity mood board and less detailed than a website mockup or comp. When an interior designer redesigns a room they don’t build multiple options of the designs they’re proposing, they bring color swatches, paint chips, and architectural drawings. Style tiles act as paint chips and color swatches for the interface that we can execute on any device or at any dimension. It’s a truly responsive solution to visual design.</blockquote>

To learn more about style tiles, I recommend also visiting Samantha’s website <a href="https://www.styletil.es">Style Tiles</a>.</p>

<figure><a href="/wp-content/uploads/2014/03/Mojo_Style_Tile_lg-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df2f9609-daf3-4987-a768-c034d23586d4/mojo-style-tile-sm1-opt.png" alt="Mojo Style Tile" width="500" height="373" /></a><figcaption>An sample style tile from Mojo Motors’ redesign process. (<a href="/wp-content/uploads/2014/03/Mojo_Style_Tile_lg-opt.jpg">View large version</a>)</figcaption></figure>

### Typography and Typecast

Most designers would agree that their favorite graphics application does not provide an accurate preview of how text will appear in the browser. With this in mind, we did as much text layout as was needed in graphics applications and then explored the finer typographical details in the browser. There, we could also accurately evaluate the effect of responsive layouts on the type as we moved through breakpoints.

In working with fonts, we faced the same <a href="https://typecast.com/about">dilemma explained by the Typecast team</a>:
<blockquote>We discovered that working with system fonts in Fireworks was faster for our designers, but build was slow because our developers had to interpret fonts and classes, resolve inconsistencies and negotiate font compromises with the designers. Plus there was that pesky problem of comp fonts not always resembling site fonts due to the rendering.

And when we moved to designing with web fonts, it was the opposite problem. It was faster for developers because there were fewer negotiations and less guesswork. But designers were wasting valuable project time stepping through a really repetitious process to get the web fonts into their layouts. You know the deal:

<em>Go to URL → Paste copy → Preview → Capture → Import to comp → Resize → Arrange – Repeat<sup>40</sup> → Find typos → Pull hair out → Repeat → Show client comp → Get requests to make bigger, smaller, different → Die a little inside → Repeat<sup>20</sup></em>

Both approaches had serious drawbacks.</blockquote>

So, to help us compare and narrow down Web fonts for Mojo Motors’ website, we turned to Typecast’s own solution.</p>

<figure><a href="/wp-content/uploads/2014/03/Typecast_lg1_A-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/195163e1-2bd2-4ef9-aeb2-3cf941b88403/typecast-sm1-a-opt.png" alt="Typecast interface" width="500" height="434" /></a><figcaption>Exploring typography in Typecast.</figcaption></figure>

<a href="https://typecast.com">Typecast</a> is a powerful browser-based design tool that makes it easy to experiment and design with the actual Web fonts that you plan to use on your website. The application lets you design visually and builds standards-compliant HTML and CSS in the background. Each Typecast subscription also comes with access to Web fonts from Typekit, Font Deck and Google, as well as a free Fonts.com account. Other features include the ability to create style guides and to share projects. Typecast is really a game-changer, and I highly recommend considering it as part of your responsive design toolkit.</p>

### Redesigning Mojo Motors’ Logo

As part of the website redesign, our team was also tasked with rethinking the company’s logo. All of the logo explorations were done in Illustrator, which is better suited to this type of work. Using Illustrator made more sense because it enabled us to create and output both CMYK files for print and RGB files for the screen.</p>

<figure><a href="/wp-content/uploads/2014/03/mojoLogo_B-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af1c80f7-fbdc-45b8-8f79-f4e102732319/mojologo-b-opt.png" alt="Mojo Logo" width="500" height="232" /></a><figcaption>The logo redesign combined elements of the old wordmark, a symbol and a new typeface.</figcaption></figure>

<figure><a href="/wp-content/uploads/2014/03/mojo_business_cards_B_lg-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1a2833b-d53f-404e-a68b-5d4bf9164f77/mojo-business-cards-opt.jpg" alt="Redesigned Mojo Motors business cards" width="500" height="437" /></a><figcaption>Mojo Motors’ business cards, before and after.</figcaption></figure>

## Setting Up The Workspace For Visual Design

The key to using an existing Fireworks wireframe file for visual design work is to set up the application and the files properly. As discussed in the previous article, we did this up front so that we could take advantage of the application’s pixel-precise layout capabilities and increase our overall efficiency throughout the project.

Let’s quickly cover the basics.</p>

### Keyboard Shortcuts

One thing that can speed up the completion of tasks in Fireworks is mastering the keyboard shortcuts. For someone transitioning from another Adobe application, Fireworks provides the option to customize the keyboard shortcuts to closely match those of Photoshop, Illustrator or InDesign — or any variation you may need, for that matter. Our team settled on Photoshop’s shortcuts because they were the most familiar.

Changing these settings in Fireworks is easy. In Windows go to <code>Edit → Keyboard Shortcuts</code>, or on a Mac go to <code>Edit → Fireworks → Keyboard Shortcuts</code>. Then, select “Photoshop” or another shortcut set from the “Current Set” dropdown menu, and click “OK.”

<figure><a href="/wp-content/uploads/2014/03/keyboard_shortcuts_AA-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fccd167d-056f-466d-a87e-295f511e49a1/keyboard-shortcuts-aa-opt.png" alt="Keyboard shortcut window" width="500" height="619" /></a><figcaption>Customizing shortcuts in Fireworks.</figcaption></figure>

To customize further, open the “Keyboard Shortcuts” dialog again:

1.  In the “Commands” field, select a specific Fireworks menu command or tool.
2.  Type a new shortcut combo in the “Press Key” field, and click the “Change” button;
3.  When you are done editing the shortcuts, save the shortcut set as a variant of the set you selected previously (e.g. “My_Custom_Set”).

Now you can work faster using the keyboard shortcuts that you are familiar with!

### Grids, Guides, Rulers and Tooltips

The great thing about carefully setting our responsive design grids during the process of creating a wireframe is that all of the grids and guides that we needed were already in place for the visual design process. Below are some of the options that we enabled when setting up our initial files.</p>

<strong>Rulers</strong> are really handy for orienting yourself visually and are required for working with guides on the screen (in the menu, <code>View → Rulers</code>).</p>

<figure><a href="/wp-content/uploads/2014/03/fw-rulers-mac_lg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f09a3b9-8e9b-453f-a5b0-d97651ca4b23/fw-rulers-mac-sm-opt.png" alt="Rulers in Fireworks" width="500" height="368" /></a><figcaption>Rulers around the canvas.</figcaption></figure>

We set our visible horizontal and vertical <strong>background grids</strong> to 10 pixels. Grids and of some their options can be accessed by going to <code>View → Grid → Show Grid/Snap to Grid/Edit Grid…</code> or by going to <code>Edit → Preferences → Guides and Grids</code>.</p>

<figure><a href="/wp-content/uploads/2014/03/bkg_grid_window_B_lg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0895a85a-2fb9-430a-9237-e685635b8b2c/bkg-grid-window-opt.png" alt="Guides and Grids Settings window" width="500" height="383" /></a><figcaption>The guides and grids settings in “Preferences”.</figcaption></figure>

This setting works well also because it matches the pixel increment (10 pixels) when objects are moved on the screen (for example, when we nudge an element using the <code>Shift + arrow</code> key shortcut). We often toggle this setting on and off as needed when drawing.</p>

<figure><a href="/wp-content/uploads/2014/03/bkg_grids-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bf66364-d9f0-423c-a27a-78eed6d5b64b/bkg-grids-opt.png" alt="Background grid shown on canvas over artwork" width="500" height="364" /></a><figcaption>A vertical and horizontal background grid of 10-pixel increments.</figcaption></figure>

We typically add <strong>guides</strong> to match the responsive grid layers and other objects as needed; guides are then toggled on and off while drawing. Guides in Fireworks are page-specific and don’t automatically appear on all pages unless placed on a master layer.

Here are a few useful tips:

*   Position unlocked guides precisely in Fireworks by clicking on a guide and entering the position directly.
*   Check guide’s spacing by placing your cursor between two guides and holding down the `Shift` key.
*   If you move a guide while holding down the `Shift` key, you can also precisely dial in the spacing.</p>

<figure><a href="/wp-content/uploads/2014/03/guidemove_precision-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c814c57-4fde-4301-a35f-286a1d21eed1/guidemove-precision-opt.jpg" alt="Moving guide with precision" width="500" height="214" /></a><figcaption>Position guides accurately by double-clicking a guide.</figcaption></figure>

<figure><a href="/wp-content/uploads/2014/03/Guides_measure_small-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c610135-0143-498b-9d00-338792f54085/guides-measure-small-opt.png" alt="Guides Spacing Measurement" width="500" height="156" /></a><figcaption>Measure guide spacing by pressing <code>Shift</code> between guides.</figcaption></figure>

<figure><a href="/wp-content/uploads/2014/03/Guides_move_sm_cropped-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3351f1d-6d91-41ef-9093-a1f6fae4e468/guides-move-sm-cropped-opt.png" alt="Guides visual positioning" width="500" height="161" /></a><figcaption>Reposition guides visually by holding down <code>Shift</code> while moving a guide.</figcaption></figure>

Guides and their options can be accessed via <code>View → Guides → Show Guides/Lock Guides/Snap to Guides/Clear Guides…</code>. You can also use keyboard shortcuts to speed up these operations.</p>

<strong>Note:</strong> To do more with guides, I highly recommend the <a href="https://www.adobe.com/devnet/fireworks/articles/guides_panel.html">Guides</a> panel extension by Eugene Jude, which enables you to create guides from selections, copy and paste guides, etc.

For an in-depth look at grid and guide workflows, check the “<a href="/2012/08/28/fireworks-extensions-for-better-workflow/#grids">Grids Panel</a>” and the “<a href="/2012/08/28/fireworks-extensions-for-better-workflow/#guides">Guides Panel</a>” sections in Ashish Bogawat’s article “<a href="/2012/08/28/fireworks-extensions-for-better-workflow/">Optimizing the Design Workflow With Fireworks Extensions</a>.” (By the way, a similar panel named <a href="/2012/01/03/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/">GuideGuide</a> has recently become available for Photoshop users as well.)

<figure><a href="/wp-content/uploads/2014/03/Guides_panel_blur-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0b0b27d-6e3f-4ebe-917f-6b0818f0004a/guides-panel-blur-opt.jpg" alt="Guides panel showing selection tab" width="500" height="384" /></a><figcaption>Guides panel extension.</figcaption></figure>

<strong>Smart guides</strong> are really helpful and enable you to visually align objects on the screen without having to use the Align panel. Turning these on (by going to <code>View → Smart Guides</code>) will allow you to see the precise adjustments to the location or size of an object when performing a free transform operation.</p>

<figure><a href="/wp-content/uploads/2014/03/smart_guides-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeb6eb67-c8dc-4e7f-8f78-4776ca40db68/smart-guides-opt.png" alt="Smart Guide" width="500" height="337" /></a><figcaption>Smart guides for visual alignment.</figcaption></figure>

<strong>Useful tip:</strong> If you find yourself creating a lot of responsive design grids, then you might also want to consider the <a href="https://johndunning.com/fireworks/about/Grids">Insert Grids</a> extension by <a href="https://twitter.com/fwextensions">John Dunning</a>.</p>

### Color Management, Color Picker and Swatches

Unlike the rest of Adobe’s Creative Suite, Fireworks does not require any particular color management settings for you to get started. The application was designed from the ground up for screen design, and it is set to the <strong>RGB color space</strong> out of the box.</p>

<strong>Note:</strong> The Color Palette panel, in addition to the RGB, HSV and HLS color spaces, also shows a CMYK option, but it is not recommended for print work.</p>

<figure><a href="/wp-content/uploads/2014/03/color-modes-lg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ec5926d-6756-4598-9f62-80407faf5e1a/color-modes-sm-opt.png" alt="Smart Guide" width="500" height="329" /></a><figcaption>Options in the Color Palette panel.</figcaption></figure>

The popup <strong>color picker</strong> is quite easy to use and is one of the best ways to specify colors for a user interface. It supports RGB and HEX color selection by default, as well as the more flexible RGBa specification that is supported by all modern browsers. Another useful feature is the one-click color copy feature. (As of the time of writing, Sketch is the only other app that has similar RGBa capabilities. Also worth mentioning is that Adobe has just added color-picker options for fills and strokes in Photoshop CS6 and CC.)

<figure><a href="/wp-content/uploads/2014/03/colorbox_picker-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9c30bab-0015-426e-9134-603d9a005597/colorbox-picker-opt.jpg" alt="Color Box Picker" width="500" height="348" /></a><figcaption>Fireworks’s color picker.</figcaption></figure>

To bring in the color palette from our exploration, we saved an RGB <code>.ASE</code> file in Illustrator and imported it into Fireworks with the help of the <strong>Swatches</strong> panel. Once imported, the color scheme became immediately available in the color picker.</p>

<figure><a href="/wp-content/uploads/2014/03/ASE_swatch_lg1-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/422a30df-4eaf-4fa3-8ae7-e7d5ec83ba78/ase-swatch-sm-opt.jpg" alt="ASE swatch import export" width="500" height="438" /></a><figcaption>Export the .ASE swatch file from illustrator and import it into Fireworks.</figcaption></figure>

The <strong>Color Palette</strong> panel is a great alternative to using the Swatches panel or color picker to specify colors. The panel is broken down into “Selector,” “Mixer” and “Blender” tabs.</p>

<figure><a href="/wp-content/uploads/2014/03/color_palette_B_lg-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/458f9609-ba35-491b-97dc-eb90e3c47440/color-palette-b-lg-opt.jpg" alt="Color Palette" width="500" height="315" /></a><figcaption>The 'Color Palette' panel.</figcaption></figure>

*   **“Selector” tab** This allows you to choose between different color models and select colors using an Adobe-like color picker, instead of the default color cubes swatches. The available options include [HSV, HSL, CMYK and RGB](https://en.wikipedia.org/wiki/List_of_color_spaces_and_their_uses); for most of our redesign work, we used the RGB model.
*   **“Mixer” tab** This is great for recoloring artwork and creating color tints. We relied on this greatly for stretching the range of our color palette. To try two different palettes in your document, follow these steps:
    1.  Click “Palette1” on the left of the panel to set the base colors for the first palette.
    2.  Click “Palette2” on the right side of the panel, and then select the base colors for the second palette.
    3.  To switch back and forth between the two palettes, select the palette to recolor with and then click the “Replace Color” icon.
*   **“Blender” tab** Here, you can create a color gradation series, which is really handy for exploring gradients. All you have to do is this:
    1.  Fill the color boxes at the bottom of the panel to select the beginning and ending colors.
    2.  Use the “Steps” slider to select the number of steps in the series.
*   **Exporting**.  Exporting any palette out of this panel requires saving it as an [.ACT](https://www.adobe.com/devnet-apps/photoshop/fileformatashtml/#50577411_pgfId-1070626) swatch file, which can be shared with other Fireworks or Photoshop users. Unfortunately, Illustrator cannot open this swatch file format. To share with Illustrator, consider exporting an [.ASE](https://www.selapa.net/swatches/colors/fileformats.php#adobe_ase) file via the Swatches panel, which will work across all Adobe products.</p>

<strong>Note:</strong> The most recent versions of Fireworks (CS5, CS5.1, CS6) all natively support both <code>.ACT</code> and <code>.ASE</code> swatch formats. Earlier versions of Fireworks (CS4 and older) support only <code>.ACT</code>.</p>

## Setting Up The Document For High-Resolution Displays

Another decision we had to make before starting the visual design process was how to set up our files for high pixel-density (or “Retina”) displays. We could approach this in a few ways:

1.  Start with standard-resolution files and scale up for Retina graphics. We opted for this because we were starting from standard-resolution wireframes.
2.  Start with high-resolution files and scale down for non-Retina graphics.

Both conversion methods should be quite seamless and yield the same results. Objects in Fireworks are created as vector shapes by default, and any effects applied will also scale (assuming, of course, that you have not created any shapes using filled selections, which were popular in Photoshop prior to the more robust shape layer option available today). All text objects in Fireworks will scale without problems, too.</p>

### Working With Raster Images (Bitmaps)

Any bitmap images can be replaced with a higher-resolution versions. The key is to always start with high-resolution images where needed and scale down. Below are a few other options to consider:

*   **Image symbols**.  An alternative to replacing your images (and one I highly recommend) is to turn your high-resolution images into symbols (`Modify → Symbol → Convert to Symbol`, or `F8`) and scale down their placed instances in the layout. Once you turn a raster image into a symbol, you can scale it down to any size and then back up to the original size as many times as you’d like without any loss in quality. If you choose this method, you won’t have to replace your images!
*   **Linked images**.  An option I discovered recently is to link images. This requires installing the free [Linked Images](https://johndunning.com/fireworks/about/LinkedImages) extension by [John Dunning](https://twitter.com/fwextensions). With this option, your layouts will be refreshed with the high-resolution images upon being scaled up (the images are stored in a folder outside of the Fireworks file). For a detailed overview of this method, please check the “Linked Images” section of “[Fireworks Extensions for a Better Design Workflow, Part 2](/2013/09/fireworks-extensions-for-better-workflow-part-2/).”

<strong>Note:</strong> For layout purposes, we used the first option to set image symbols of cars as placeholders. The final car images are generated dynamically on the server and rendered on the live website. We won’t cover this production process in this article.

Hint: A good read on Retina graphics is “<a href="https://retinafy.me">Retinafy Your Websites and Apps</a>” by Thomas Fuchs.</p>

## Live (Pre)View: Bringing Wireframes To Life

### Live View, Skala Preview and Xscope

Just as when we were creating the wireframes, we frequently had to check how the mockups looked and scaled on real devices, such as the iPhone and iPad.

For quick previews while designing, we turned again to the <a href="https://www.zambetti.com/projects/liveview/">LiveView</a> app (check out <a href="/2013/08/26/mojo-motors-responsive-redesign-with-adobe-fireworks-part-1/">my previous article</a> for details on our process). Alternatives to LiveView are <a href="https://bjango.com/mac/skalapreview/">Skala Preview</a> and <a href="https://xscopeapp.com">Xscope</a>, which provide similar functionality but integrate better with Photoshop. Skala Preview is also compatible with Android devices.</p>

### Bringing Wireframes to Life

Once the file was set up, the next step was to add pixel precision to the interface and content. This is also when we applied brand elements such as color, typography, iconography and the logo from our style tiles. Putting the pages for each breakpoint in one working file made it easier to transpose screen elements between mobile, tablet and desktop layouts (see part 1 of this series for details on pages, states and symbols in Fireworks).</p>

## Favorite Fireworks Features During The Visual Design Stage

In this next part, we’ll cover some Fireworks features, tools and workflows that really came in handy during the visual design stage.</p>

### Properties Panel (Property Inspector Panel)

A lot of great features in Fireworks make creating screen graphics fast and efficient, but the single most powerful UI feature for us was the contextual <strong>direct editing of objects</strong>, available via the Properties panel (also called the Property Inspector (or PI) panel). This powerful panel changes contextually based on the type of object selected on the canvas.

The Properties panel is normally found at the bottom of the screen when a document is first opened in Fireworks. It allows you to manage all attributes, such as fills, strokes, gradients, patterns, textures, size, position, scale, opacity, blend modes, live filters, text properties, masks (and masks properties), symbols and much more, for any selected object or group of objects.</p>

<figure><a href="/wp-content/uploads/2014/03/Property_inspector_context_lg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86f94dc4-bce0-43fb-8f2b-93521910f788/property-inspector-context-sm-opt.png" alt="Property Inspector" width="500" height="269" /></a><figcaption>In these three sample screenshots, you can see how the Properties panel adapts to the type of object selected. (<a href="/wp-content/uploads/2014/03/Property_inspector_context_lg-opt.png">View large version</a>)</figcaption></figure>

Once you understand how the Properties panel works, quickly inspecting and changing the properties of all types of objects with pixel-level precision become really easy. You might also find that making changes is a lot faster than in any other graphics application (including Sketch!).</p>

### Gradients

Creating gradients is quite simple and intuitive. Adjusting and changing the fill type can be easily done at any time. Fireworks also offers 12 gradient types out of the box. And the dither option reduces banding when images are exported.</p>

<figure><a href="/wp-content/uploads/2014/03/gradients_panel_lg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a045a80b-0fb9-409c-bff6-f44b824235b6/gradients-panel-sm3-opt.png" alt="Gradient Selector" width="500" height="458" /></a>Side note: Starting with CS6, Adobe added some similar features to Photoshop, including the ability to add fills and strokes to shape layers as an alternative to live filters such as gradient overlay effects. Unfortunately, you can’t change the fill type as easily once you have committed to a gradient or any other type. Changing the fill type requires selecting the shape layer with the Path Selection tool, which will reveal your options in the options bar (in CS6) or in the Properties panel (in CC), at which point you can make your changes.
### Textures
In addition to applying fills to vector objects in Fireworks, you can add textures to any fill type or stroke. Being able to apply textures to strokes is really useful for simulating CSS border-image effects, which is now supported by most modern browsers. Other features include being able to use your own texture files and specifying the opacity level.</p>

<figure><a href="/wp-content/uploads/2014/03/textures_menu_A_lg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd4c9344-17bc-40b6-b62a-336f07e41381/textures-menu-a-opt.png" alt="Textures Menu" width="500" height="320" /></a><figcaption>Apply textures with (again!) the mighty Properties panel.</figcaption></figure>If you plan on using textures a lot, the free Texture Panel extension by <a href="/author/matt-curtis/?rel=author">Matt Curtis</a> is a good addition to Fireworks. For details on this extension, check out Matt’s article, “<a href="/2012/11/14/texture-panel-adobe-fireworks/">Using the Texture Panel in Adobe Fireworks</a>.”

<figure><a href="/wp-content/uploads/2014/03/texture_panel_A-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45397574-43ac-4ca2-a100-a1bcec39d2e7/texture-panel-a-opt.png" alt="Texture Panel" width="500" height="380" /></a><figcaption>Texture Panel extension.</figcaption></figure>

### Fireworks Live Filters and Photoshop Live Effects
Fireworks comes with most of the important non-destructive effects that you will need to bring screen designs to life, and it includes some familiar Photoshop live effects as options. I typically opt for Fireworks’ native filters before considering the Photoshop ones.

Fireworks’s live filters can be applied to any type of object (vector, bitmap, symbol, etc.) non-destructively, and the stacking order of applied live filters may be changed simply by dragging and dropping. Another key feature is the ability to apply <strong>multiple filters of the same type</strong> to a single object.</p>

<figure><a href="/wp-content/uploads/2014/03/filters_applied_lg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/caa70c21-c43b-4c3d-974e-2cd603d66c51/filters-applied-sm-opt.png" alt="Fireworks Live Filters" width="500" height="449" /></a><figcaption>Fireworks’ live filters in the Properties panel.</figcaption></figure>I find the native filters to be quite adequate for most tasks, and I need to switch to Photoshop only for complex compositing, correcting photo colors and creating textures.
### Blend Modes
Blend modes in Fireworks are similar to Photoshop’s and Illustrator’s. For a long time, Fireworks was the only Adobe application that allowed you to apply blend modes to multiple selected objects (or layers) at once. (Similar features were introduced to Photoshop in CS6. Illustrator requires the opacity option to be edited in the Appearance or Transparency panel.)

<figure><a href="/wp-content/uploads/2014/03/blendmodes-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d98f5e6-401f-4f1b-9473-7f85c7e8beb6/blendmodes-opt.png" alt="Blend Modes" width="500" height="553" /></a><figcaption>Blend Modes may be modified in the Layers panel (top screenshot) and in the Properties panel (bottom screenshot).</figcaption></figure>

### Pasting Attributes
Copying and pasting attributes (using the simple <code>Control/Command + C</code> and <code>Control/Command + Alt + Shift + V</code> shortcuts) between objects is an awesome feature and a huge timesaver, one we often leveraged during the process of going from wireframes to visual comps. Unlike copying and pasting layer styles in Photoshop, Fireworks transfers all attributes — including font type, font size, fill type, stroke type, applied live filters and so on — from one selected object to another.

Pasting attributes can even be done selectively (see the “Paste Selective Attributes” section of “<a href="/2013/09/fireworks-extensions-for-better-workflow-part-2/">Fireworks Extensions for a Better Design Workflow, Part 2</a>”), which makes the feature even more powerful.
### Styles and the Styles Panel
While being able to copy and paste attributes is very useful, using Fireworks’ styles is a lot more efficient and an essential part of creating visual mockups.

Styles in Fireworks are analogous to CSS in Web design. They can be quickly applied to objects on the screen to mock up variations or can be used to apply a final style guide for brand consistency. Whenever a style definition changes, all objects that have the same style are updated automatically.</p>

<figure><a href="/wp-content/uploads/2014/03/styles_button_panel_lg_A-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c38c14e8-ce06-4a22-97b2-cb24a53c43c0/styles-button-panel-sm-a-opt.png" alt="Styles Panel large" width="500" height="297" /></a><figcaption>Apply styles via the Styles panel from the built-in library.</figcaption></figure><figure><a href="/wp-content/uploads/2014/03/styles_menu_A-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67ad0033-6316-4851-b1d2-9c5178b3f9fa/styles-menu-a-opt.png" alt="Styles Menu in Property Inspector" width="500" height="202" /></a><figcaption>Apply styles via the Properties panel.</figcaption></figure>Style can be created and managed in both the Styles panel and the Properties panel. As a bonus, Fireworks ships with a large library of premade styles that can be applied very quickly to any mockup. You can also easily create, edit and reuse your own styles.
### Rounded Rectangles
Creating (and modifying) rounded rectangles is very easy, and Fireworks is the most flexible here of the three Adobe applications typically used for screen design (the other two being Photoshop and Illustrator). Create one by modifying the roundness of a rectangle shape (i.e. the border-radius of each corner) directly in the Properties panel or by inserting a rounded rectangle auto shape.</p>

<figure><a href="/wp-content/uploads/2014/03/rounded-rectangles-lg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96e2935c-4dc8-4704-955a-6a42529b30dd/rounded-rectangles-sm-opt.png" alt="Rounded rectangles" width="500" height="323" /></a><figcaption>You can control the roundness of a rectangle’s corners in one of two ways. (<a href="/wp-content/uploads/2014/03/rounded-rectangles-lg-opt.png">View large version</a>)</figcaption></figure>My preference is to use the Properties panel because you can specify the roundness in percentages or pixels. But modifying the roundness at any time is easy either way. You can also modify individual corners of a rounded rectangle. When you’re using the Rounded Rectangle auto shape, the roundness can be also controlled with the Auto Shape Properties panel.

(Photoshop CC just added an option to apply rounding to individual corners of a rectangle or to a rounded rectangle shape layer via the Properties panel. This is a welcome change and a great alternative to adding rounded corners as an appearance effect in Illustrator.)
### Multi-Border Rectangle Auto Shape
The <a href="https://johndunning.com/fireworks/about/MultiBorderRect">Multi-Border Rectangle</a> auto shape is an extension by John Dunning that makes it easy to mock up CSS-style borders on vector rectangles. You can specify a different border width and color for each of the four borders of a rectangle, just as you do with CSS for each border of an HTML element. This extension proved very useful during our visual design process.</p>

<figure><a href="/wp-content/uploads/2014/03/multi-border_autoshape_lg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b51a57b-7d01-4068-9401-51e45d933747/multi-border-autoshape-sm1-a-opt.png" alt="Multi-border autoshape" width="500" height="623" /></a><figcaption>We used the Multi-Border Rectangle auto shape to add top and bottom borders to rectangles.</figcaption></figure>

### Path Panel
Fireworks has an easy to use and robust set of vector-editing tools, with many of the same features found in Illustrator. Most of the tools can be accessed from the Path panel (and a few are in the “Modify” menu). In CS6, some of the basic path tools were added to the Properties panel, for easy access.</p>

<strong>Note:</strong> There is a <a href="https://fireworks.abeall.com/extensions/panels/Path/">more recent version of the Path panel</a> (with many additions and improvements) than the one that ships with Fireworks CS6. (In case you’re wondering, <a href="https://fireworks.abeall.com">Aaron Beall</a> is the talented developer responsible for the latest versions of the Path panel in Fireworks, including the one in CS6.)

<figure><a href="/wp-content/uploads/2014/03/Path_panel_A-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f7fb595-011c-430c-82a5-cc9e5cdca6a1/path-panel-a-opt.png" alt="Path Panel" width="500" height="350" /></a><figcaption>The 'Path' panel.</figcaption></figure>

### Importing From and Exporting to Illustrator
Fireworks handles <code>.AI</code> files very well, and we used it whenever we had to work with vector art created in Illustrator or in Illustrator-compatible applications. As part of the importing process, you are even presented with a “Vector File Options” window, giving you the option to select a specific Illustrator artboard to import.

We especially took advantage of this workflow with our company’s logo and illustrations throughout the website. Our freelance illustrator worked in Illustrator and imported directly into our Fireworks layouts. For smaller artwork, you could also copy a single object or group of objects in Illustrator and then paste them directly in Fireworks.</p>

<figure><a href="/wp-content/uploads/2014/03/illustrator_import_lg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1ad33bd-b695-4347-923a-5d40ea2be440/illustrator-import-sm-a-opt.png" alt="Illustrator Import to Fireworks" width="500" height="750" /></a><figcaption>The illustration for Mojo Motors’ “Tour” page was created in Illustrator and then imported into Fireworks, with all vectors perfectly preserved and editable. (<a href="/wp-content/uploads/2014/03/illustrator_import_lg-opt.png">View large version</a>)</figcaption></figure>Exporting vector objects to Illustrator for further refinement is as easy as selecting the object (or group of objects) in Fireworks, then going to <code>Edit → Copy as Vectors</code>, and then pasting the vector objects in Illustrator. (Simply copying and pasting objects would put bitmap objects in Illustrator, instead of vectors, so always go to <code>Edit → Copy as Vectors</code>, instead of <code>Edit → Copy</code>.)

To export large artwork in Fireworks, save the entire file as an <code>.AI</code> file and then open that <code>.AI</code> file in Illustrator.</p>

<strong>Note:</strong> In Illustrator CC, Adobe removed the importing and exporting options described above. If you are using Illustrator CC, you might need to save your files as “Illustrator v. CS6” to take advantage of all of these capabilities, or work in Illustrator CS6 or lower, which supports all of these options out of the box.
### Importing From and Exporting to Photoshop
Importing and exporting with Photoshop is a breeze with Fireworks — Fireworks can save to <code>.PSD</code> and also open <code>.PSD</code> files. In both cases, layers and naming conventions will be preserved.

The results will vary according to the options you’ve set during the importing or exporting process and how much editability you would like to retain. My suggestion is to experiment a little to see which settings work best for your purpose.</p>

<figure><a href="/wp-content/uploads/2014/03/photoshop-import-and-open_lg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5539d1d9-e96d-44d8-9b75-e87ec4a009ed/photoshop-import-and-open-sm-opt.png" alt="Photoshop import and open." width="500" height="910" /></a><figcaption>The Photoshop importing and file-opening dialogs in Fireworks.</figcaption></figure><strong>Note:</strong> As of the time of writing, Photoshop importing and exporting still works well in Photoshop CC and CS6.
### Align Panel
If you intend to create pixel-precise layouts, then you cannot do without the Align panel. With it, you can align multiple objects to each other or relative to the canvas. (Adobe Illustrator has a similar feature, and it was just introduced to Photoshop CS6 as well, although its functionality is not as robust.)

Two useful features that are unique to the Align panel in Fireworks are the “Match Size” and “Space Evenly” options.</p>

<figure><a href="/wp-content/uploads/2014/03/align_panel-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c74210ae-eb47-4e8e-bc5d-e1ab4a8f5924/align-panel-opt.png" alt="Align Panel" width="500" height="366" /></a><figcaption>The 'Align' panel.</figcaption></figure>

<ul>
 	<li><strong>Match size</strong>
This option lets you match the size of the selected object to the height or width (or both — but usually the longer dimension) of another object.</li>
 	<li><strong>Space evenly</strong>
This is different than distribution, enabling you to align objects a fixed distance apart.</li>
</ul>
The Align panel is invaluable. The only option that I wish Fireworks had adopted from Illustrator is the alignment object reference, which enables you to pick the object to align your selection to.
### Symbols
During the visual design process, we continued to look for opportunities to modularize interface components by creating <strong>reusable symbols</strong>. In some cases, we simply applied visual styles to existing wireframe symbols.

Styled component symbols are very efficient and reduced the time we took to create alternate layouts and iterations. For details on creating symbols, read the section “Creating Reusable Modular Elements” in <a href="/2013/08/26/mojo-motors-responsive-redesign-with-adobe-fireworks-part-1/">part 1 of this series</a>.
### 9-Slice Scaling
The 9-Slice Scaling tool is original to Fireworks and was adopted later by Flash and recently by Illustrator. With it, you can scale objects without distorting <strong>protected areas</strong>. A popular use of the tool is to protect rounded corners in a symbol when scaled.</p>

<figure><a href="/wp-content/uploads/2014/03/9-Slice_Guides_lg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d38205f-c312-4403-beae-6c6203012c95/9-slice-guides-sm-opt.png" alt="9-Slice Guides (UI button)" width="500" height="721" /></a><figcaption>Use the 9-Slice guides to preserve rounded corners in a button.</figcaption></figure>The 9-Slice Scaling tool works on symbols and on both vector and bitmap objects, making it extremely versatile.
### Single-Layer Editing
This feature is really geared to designers who are coming to Fireworks from Photoshop and who are used to selecting layers before working on them. I personally prefer the default auto layer selection method in Fireworks because it is faster, especially in files with a ton of layers.</p>

<figure><a href="/wp-content/uploads/2014/03/SingleLayer_editing_A-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/444117e8-9b07-43bd-9252-2ceeab7bcc08/singlelayer-editing-a-opt.png" alt="Single layer editing mode" width="500" height="550" /></a><figcaption>The single-layer editing option in the Layers panel menu.</figcaption></figure>

## Conclusion

I was really torn about whether this article would still be relevant in light of the announcement that Fireworks has been <a href="https://blogs.adobe.com/fireworks/2013/05/the-future-of-adobe-fireworks.html">feature-frozen</a>. However, as I explored all of the alternative ways to make one’s workflow efficient, I realized that Fireworks is still powerful and will continue to be the best option until Adobe unveils its replacement or until another competitor supports all of its features, including integration with other Adobe products, as Fireworks currently provides. (In my opinion, Photoshop and Illustrator have recently gained some sorely needed features that make the process of designing for screens more efficient, but they’re not there yet.)

<figure><a href="/wp-content/uploads/2014/03/Mojo_desktop_B_lg-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a7fdbf8-f7a5-4290-b28b-4236a4598639/mojo-desktop-small-opt.jpg" alt="Mojo Motors Dashboard" width="500" height="298" /></a><figure><a href="/wp-content/uploads/2014/03/Mojo_iPhone-5C_B_lg-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58cce074-ea73-43b8-b11a-901f2c307cf2/mojo-iphone-5c-small-opt.jpg" alt="Mojo Motors mobile web screens" width="500" height="365" /></a><figure><a href="/wp-content/uploads/2014/03/tablet_B_lg-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08134b2c-9250-4705-8358-3dbaebb968f0/tablet-small-opt.jpg" alt="Mojo Motors tour screen on iPad tablet" width="500" height="447" /></a><figcaption>Screenshots of Mojo Motors’ website after the redesign (Click each image for a larger version).</figcaption></figure>

### Alternatives?
Are there alternatives to Fireworks? Of course.

For example, for teams comfortable stepping outside of the Adobe world, the Mac-only <a href="https://www.bohemiancoding.com/sketch/">Sketch</a> is a great replacement, and I hope to see it integrate more of the time-saving features offered by Fireworks. Read about some of the benefits of using Sketch for UI design in the following articles:
<ul>
 	<li>“<a href="https://medium.com/design-ux/c59ff242715d">It’s Time to Dump Photoshop and Embrace Sketch</a>,” Baz Deas</li>
 	<li>“<a href="https://medium.com/design-ux/25545f6cb161">Discovering Sketch</a>,” Jean-Marc Denis</li>
</ul>
Sketch doesn’t totally replace Fireworks, but it’s getting pretty close in my opinion. (Craig Erskine, who uses both Sketch and Fireworks, has <a href="https://dribbble.com/shots/1434819/">shared his thoughts</a> on the matter.)

At the other end of the spectrum, I am quite excited about applications such as <a href="https://macaw.co">Macaw</a>, which are embracing a more modern approach to designing for screens with a native desktop application. I recently supported Macaw’s Kickstarter effort and am currently trying out the product with my early-bird license. (The product will launch sometime in March or April 2014.)

Another noteworthy project is Evolve UI, a somewhat secret yet exciting initiative by <a href="https://tribaloid.com">Tribaloid</a> and one that could shake up our workflow in the next few years. Evolve UI is being developed by Alan Musselman, who worked as Fireworks’ project manager for quite some time, and it is currently in <a href="https://groups.google.com/forum/#!forum/underdog-discussions">alpha development</a>.
### Awards
Last but not least, I’d like to mention that Mojo Motors’ redesigned website received quite a few awards after it launched — namely, the Web Marketing Association’s <a href="https://www.webaward.org/winner.asp?eid=19327#.UxnW9dzWJ7G">WebAward for 2013</a>, the <a href="https://www.interactivemediaawards.com/winners/certificate.asp?param=283891&amp;cat=1">Interactive Media Award for 2013</a> and the Automotive Website Awards’ <a href="https://www.automotivewebsiteawards.com/20140124-mojo-motors-named-a-rising-star-at-2014-awas/">Rising Star award for 2014</a>. I feel very proud of the work we did on this project. Fireworks was invaluable to our team, minimizing the production work and freeing us to focus on designing a good product for our users.
### Note
All of the screenshots of Mojo Motors’ website are from the initial launch state at the end of 2012. Some of the screenshots in this article might not match the current website because pages are frequently optimized according to analytics, user testing and performance.</p>

<figure><a href="/wp-content/uploads/2014/03/Mojo_errorPage_B_lg-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b06b9532-255f-4442-a0f8-cf52827a2e44/mojo-errorpage-b-sm-opt.png" alt="Mojo Error Page" width="500" height="360" /></a><figcaption>The 404 page.</figcaption></figure>

### Further Reading
Should you want to explore more of Fireworks’ features and options, these resources might be helpful:
<ul>
 	<li>“<a href="/2012/05/07/refining-designs-adobe-fireworks/">Refining Your Design in Adobe Fireworks</a>,” Benjamin De Cock</li>
 	<li>“<a href="/2012/06/11/developing-a-design-workflow-in-adobe-fireworks/">Developing a Design Workflow in Adobe Fireworks</a>,” Joshua Bullock</li>
 	<li>“<a href="/2012/10/12/adobe-fireworks-enterprise/">Useful Fireworks Techniques and Features for Large Design Teams</a>,” Kris Niles</li>
 	<li>“<a href="/2010/09/17/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/">The Power of Adobe Fireworks: What Can You Achieve With It?</a>,” Michel Bozgounov</li>
 	<li>“<a href="https://firetuts.com/adobe-fireworks-siri-icon/">Replicate the Siri Icon in Adobe Fireworks</a>,” Firetuts</li>
 	<li>“<a href="https://firetuts.com/sprite-animation-using-adobe-fireworks-and-axure/">Sprite Animation Using Adobe Fireworks and Axure</a>,” Joseph Reni, Firetuts</li>
 	<li>“iOS Prototyping With TAP and Adobe Fireworks,” Shlomo Goltz: <a href="/2013/01/ios-prototyping-adobe-fireworks-tap-part1/">Part 1</a>, <a href="/2013/01/ios-prototyping-adobe-fireworks-tap-part2/">Part 2</a>, <a href="/2013/02/ios-prototyping-adobe-fireworks-tap-part3/">Part 3</a></li>
 	<li>“Optimizing the Design Workflow With Fireworks Extensions,” Ashish Bogawat: <a href="/2012/08/fireworks-extensions-for-better-workflow/">Part 1</a>, <a href="/2013/09/fireworks-extensions-for-better-workflow-part-2/">Part 2</a>, <a href="/2013/11/even-more-fireworks-extensions-optimized-design-workflow/">Part 3</a></li>
</ul>
### What’s Next?
We’ve planned this case study of Mojo Motors to span three articles. <a href="/2013/08/26/mojo-motors-responsive-redesign-with-adobe-fireworks-part-1/">Part 1</a> covered the UX and interaction design stage. Part 2 has covered the visual design stage. Part 3 (currently on the drafting board) will discuss how our team translated the visual design to the front-end iterative development cycle. Stay tuned!

<em>(mb, al, il) </em>

</figure></figure></figure>


---
title: Photoshop Performance - 10 Simple Steps
slug: 10-simple-steps-to-better-photoshop-performance
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b761e5b8-21ab-4952-95e9-31088a6393c5/illuphotoshop61.gif
date: 2009-08-13T11:47:59.000Z
author: guest-author
description: >-
  Before getting started with Photoshop, we all should have first visited the
  "Edit > Preferences" menu and change the "Performance" settings to fit our
  personal taste and computer specifications, but this isn't always the case –
  in many situations designers simply forget these aspects.
categories:
  - Graphics
  - Tutorials
  - Photoshop
  - Performance
---
If you never changed the default performance settings in your Photoshop or you just want to double check them to improve the Photoshop performance, <strong>here are 10 important and useful points that you may want to consider.</strong>

Before getting started with Photoshop, we all should have first visited the "Edit &gt; Preferences" menu and change the "Performance" settings to fit our personal taste and computer specifications, but this isn't always the case – in many situations designers simply forget these aspects.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Top 10 Killer Photoshop Combo Moves](https://www.smashingmagazine.com/2008/08/13/top-10-killer-photoshop-combo-moves/)
*   [20 Time-Saving Tips to Improve Designer’s Workflow](https://www.smashingmagazine.com/2009/05/26/20-time-saving-tips-to-improve-designers-workflow-part-1/)
*   [Compositing in Adobe Photoshop: Time-Saving Tips](https://www.smashingmagazine.com/2010/12/compositing-in-adobe-photoshop-time-saving-tips/)

## 1\. Adjust The Number Of History States

Maybe you already went through that bad feeling of clicking "undo" dozens of times and realizing that Photoshop wouldn't provide you with more previous steps, but this problem can be easily resolved by changing the <strong>History States setting</strong> in the <strong>Edit &gt; Preferences &gt; Performance</strong> menu.

{{% feature-panel %}}

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0326d16e-aee7-4d97-91ff-840cb5c29a02/ps-tuning1.gif" alt="Photoshop Performance" width="500" height="318" />

There are more efficient ways of going back and forward in your projects like using the "Snapshots" feature, which are essentially comfortable checkpoints of your work that you can go back to. But if you use Undo a lot, you may want to consider <strong>adding more states</strong>, e.g. set them to '30'. However, be aware that too many states on a single image will usually result in <strong>History Palette literally "eating" RAM</strong> and if you work with less than 8GB of RAM, you probably shouldn't using the Undo Feature that often! Overall, you may add up to 1,000 history state levels in Photoshop.</p>

## 2\. How Many Cache Levels Do You Need?

The Cache Levels setting can be found inside the <strong>Edit &gt; Preferences &gt; Performance</strong> menu, right under the History States. It controls the histogram and the time it takes an image to reappear on the screen after an action is applied to it.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6cd720f-c099-41d0-9a88-77284235ffaf/ps-tuning2.gif" alt="Photoshop Performance" width="500" height="344" />

By default, there are 6 cache levels; the number of levels <strong>can be increased to the maximum of 8</strong> which will – obviously – increase the rendering speed. It is particular effective when you are working with high-resolution images. When workin with smaller view-sizes, e.g. viewing an image at 50% Zoom, the cache levels will determine the number of "down samplings" allowing Photoshop to perform operations faster.

Photoshop uses Image Caching and if you have a good amount of RAM, like at least 8GB and work with high-resolution images, you might want to raise the level to 8 as the speed performance will compensate the memory loss, but if you have a low RAM amount and usually work with small images only (1-4MB), you may want to lower the value to 1 or 2 as the RAM will be better allocated – storing the images rather then caching them.</p>

## 3\. Keep An Eye On Your Memory Usage

Photoshop really likes RAM and will use every little bit it can grab, but it also allows you to <strong>limit the RAM resources of your computer that Photoshop will use</strong>, and it even gives you good suggestions for the appropriate range of RAM values it wants. This setting, of course, can be found inside the <strong>Edit &gt; Preferences &gt; Performance</strong> menu, on the Left Side.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6d505c8-9d07-4f97-a7da-00f2651c840f/ps-tuning3.gif" alt="ps-tuning3" width="500" height="336" />

The displayed available RAM is the value left for applications after the Operating System loads into memory. If you are going to use mostly only Photoshop, or if you have a low amount of memory, you will probably want to give it 75-80% of the available RAM. But if, on the other hand, you are more of a multi-task kind of person with browser, word processor, mail, Twitter client etc. being always opened, then you might want to limit Photoshop to around 50%.

### Efficient Use of Memory for Photoshop Performance

After setting up your memory values, you can keep an eye on how Photoshop is performing. At the base of your image window, click to the right of the document size information and you will be able to choose "Efficiency" which will show you a percentage value. If this value is not 100%, it indicates that <strong>if you allocate more RAM to Photoshop, the operations would perform faster</strong>. Closing applications or images that you are not using can also increase the efficiency – not exactly a secret, but worth mentioning nevertheless.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d81c2a3d-852e-4c4b-aaa5-e2c3414fb3e9/ps-tuning4.gif" alt="ps-tuning4" width="500" height="294" />

## 4\. Use Proper Scratch Disks

Similar to what happened with RAM, Photoshop also uses a good amount of your hard drive space as the so-called "scrath disk" (Edit &gt; Preferences &gt; Scratch Disks) which works as the secondary memory resource. <strong>Photoshop assumes that your primary hard drive is its scratch disk, but you can set it up differently</strong> with a secondary internal or external hard drive.

If you are going to work with large images, it is recommended that you have a dedicated scratch disk that is different from the one containing the image file. Using different scratch disks is good, especially to avoid killing your primary boot drive when you have just a few gigabytes left.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/967a00a9-8983-48d3-8fec-fd02b6cc4e92/ps-tuning5.gif" alt="ps-tuning5" width="500" height="292" />

## 5\. Turn Font Preview Off

Photoshop users (and especially designers) like to have a good selection of fonts always installed and ready to be used; but when the font preview is active, having too many fonts can slow you down. <strong>Turning the font preview feature off</strong> can be a simple and instant step towards improving your Photoshop performance. To do so, simply go to <strong>Type &gt; Font Preview Size &gt; None</strong>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc1ce475-eeea-4ec8-b6b5-0be3209640fc/ps-tuning6.gif" alt="ps-tuning6" width="500" height="480" />

## 6\. Use Thumbnails In Your Palettes

Displaying preview thumbnails in the Layers, Channels, and Paths palettes will cause Photoshop to consume some more of your RAM as it will be constantly updating the thumbnails to reflect the changes you will be doing in your project. <strong>The memory consumption will keep growing with the amount of thumbnails</strong> you have opened at the same time as well as their size.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c42ee942-1bde-457a-90cc-4f318c1f88a4/ps-tuning7.gif" alt="ps-tuning7" width="500" height="500" />

You could use the smaller thumbnail size or no thumbnail at all to increase your Photoshop performance. To do so, in each palette, select <strong>Panel Options</strong> from the palette menu as it is shown on the picture above and select the smallest thumbnail size or "None".</p>

## 7\. Learn How To Use Purge

When you are working on your images, Photoshop stores image data for the Undo, Clipboard, and History features. This data consumes memory, especially if you have been working for a while and have a high number of History States defined <em>(see Point 1 for more on History States).</em>

To eliminate that extra image data consuming your RAM, go to: <strong>Edit &gt; Purge &gt; ( option )</strong>. Keep in mind that clearing History will remove all the history states saved previously and you will not be able to undo your latest actions.

<img loading="lazy" decoding="async" class="276356" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de0b640e-507e-4db1-9dec-70261ce966c7/ps-tuning8.gif" alt="ps-tuning8" width="500" height="400" />

## 8\. Set Maximize PSD And PSB File Compatibility to Always or Ask

Maximize PSD and PSB File Compatibility increases the size of your file by attaching a flattened copy of your image when you save your image. A small amount of extra data is included in the file when you choose this option that ensures that PSD and PBS files saved in Photoshop will open in previous versions.

Additionally, if you want to use the Edit in Photoshop feature in Photoshop Lightroom, this option needs to be on. To change the Maximize File Compatibility option choose <strong>Photoshop &gt; Preferences &gt; File Handling</strong>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0afa7f3-7003-4567-9816-3fda42bf5cd6/ps-tuning9.gif" alt="ps-tuning9" width="500" height="332" />

## 9\. Don't clutter your Photoshop

Of course, you can easily find an enormous amount of free stuff to add up to the default Photoshop brushes, fonts, patterns, etc. but that doesn't mean you need to download every freebie that comes in your way. Keep it simple! Having too many plugins and other resources installed  will greatly decrease Photoshop performance. Most top designers use a small selection of fonts and brushes that define their style and that can be used in a great amount of ways for literally millions of different results.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e981fca-7bc7-4f37-acf8-4337551de427/ps-tuning10.gif" alt="ps-tuning10" width="500" height="456" />

## 10\. Reset Default Settings

If you are using a shared machine for your Photoshop needs there is <strong>a little Photoshop start-up trick</strong> that may come in handy. When the application is launching, if you press and hold: <em>Alt + Control + Shift (Windows)</em> or <em>Command + Option + Shift (Mac)</em>, a window will pop up asking you if you want to delete the Photoshop settings file, resetting all of the preferences to their default.


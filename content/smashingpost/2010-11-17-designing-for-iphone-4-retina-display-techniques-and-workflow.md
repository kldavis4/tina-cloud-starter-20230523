---
title: 'Designing for iPhone 4 Retina Display: Techniques and Workflow'
slug: designing-for-iphone-4-retina-display-techniques-and-workflow
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32878e53-46b8-49d0-96ed-8964d29a48d3/promo-2x1.jpg'
date: 2010-11-17T13:14:48.000Z
author: marc-edwards
description: >-
  The iPhone 4 features a vastly superior display resolution (614400 pixels) over previous iPhone models, containing quadruple the 153600-pixel display of the iPhone 3GS. The screen is the same physical size, so those extra dots are used for additional detail — twice the detail horizontally, and twice vertically. For developers only using Apple’s user interface elements, most of the work is already done for you.
categories:
  - Mobile
  - Business
  - Workflow
  - Techniques
  - iOS
  - iPhone
---
The iPhone 4 features a vastly superior display resolution (614400 pixels) over previous iPhone models, containing quadruple the 153600-pixel display of the iPhone 3GS. The screen is the same physical size, so those extra dots are used for additional detail — twice the detail horizontally, and twice vertically. For developers only using Apple’s user interface elements, most of the work is already done for you.

For those with highly custom, image-based interfaces, a fair amount of work will be required in scaling up elements to take full advantage of the <strong>iPhone 4 Retina display</strong>. Scaling user interfaces for higher detail displays — or increasing size on the same display — isn’t a new problem. Interfaces that can scale are said to have <a href="https://en.wikipedia.org/wiki/Resolution_independence">resolution independence</a>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Better Way To Design For Retina In Photoshop](https://www.smashingmagazine.com/2015/05/retina-design-in-photoshop/)
*   [<span class="headline">Towards A Retina Web</span>](https://www.smashingmagazine.com/2012/08/towards-retina-web/)
*   [Ready For Retina HD: Create Pixel-Perfect Assets For Multiple Scale Factors](https://www.smashingmagazine.com/2014/10/create-assets-for-multiple-scale-factors/)
*   [Beautiful iPhone And iPad Retina Wallpapers](https://www.smashingmagazine.com/2012/07/beautiful-iphone-and-ipad-retina-wallpapers/)

In a recent article, Neven Mrgan described <a href="https://mrgan.tumblr.com/post/708404794/ios-app-icon-sizes">resolution independence</a>: “RI [resolution independence] is really a goal, not a technique. It means having resources which will look great at different sizes.” If it’s a goal, not a specific technique, then what techniques exist? How has Apple solved the problem in iOS?

{{% feature-panel %}}

## Fluid Layouts

While apps that take advantage of Apple's native user interface elements require a lot less work when designing for the Retina display, we're here to talk about highly custom, graphic-driven apps that need a fair amount of work to take full advantage of the Retina display.

While not strictly a resolution-independent technique, using a <a href="https://en.wikipedia.org/wiki/Web_design#Layout_types">fluid layout</a> can help an app grow to take advantage of a larger window or screen by adding padding or by changing the layout dynamically. A lot of Mac, Windows and Linux apps use this method, as do some websites.

This is partially how Apple handled the difference in resolution from iPhone to iPad — a lot of UI elements are the same pixel size, but padded to make use of the extra screen real estate. The status bar is a good example of this. It works because the pixel densities of the iPhone 3GS and iPad are similar (163 ppi vs 132 ppi).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19593418-ec84-402f-a50a-bdecf5314e94/lockscreen.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fb4af70-6e3d-412d-9c0a-9d4d7bd2e49f/lockscreen.jpg" alt="Screenshot" width="500" height="140" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19593418-ec84-402f-a50a-bdecf5314e94/lockscreen.png">Full view</a></em>

Fluid layouts work when the change in density is minor, but aren’t any help with the iOS non-Retina to Retina display transition (163 ppi to 326 ppi). The image below demonstrates what would happen if an iPhone app was simply padded to cater for the higher resolution display of the iPhone 4. Buttons and tap areas would be the same size in pixels, but half the physical size due to the higher pixel density, making things harder to read and to tap.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/866d24f7-8d69-417e-96e2-792023ec8ea1/phone-app-fluid.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb0e2b3c-760f-4b6e-882f-da1ea52ccbb0/phone-app-fluid.jpg" alt="Screenshot" width="500" height="140" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/866d24f7-8d69-417e-96e2-792023ec8ea1/phone-app-fluid.png">Full view</a></em>

## Just-in-time Resolution Independence

Another approach to handling widely different resolutions and pixel densities is to draw everything using code or vector-based images (like PDFs) at runtime. Without trying to stereotype anyone, it’s usually the approach engineering-types like. It’s clean, simple and elegant. It lets you design or code once, and display at any resolution, even at fractional scales.

Unfortunately, using vector-based images tends to be more <strong>resource-hungry and lacks pixel level control</strong>. The increase in resources may not be an issue for a desktop OS, but it is a considerable problem for a mobile OS. The lack of pixel level control is a very real problem for smaller elements. Change an icon's size by one pixel, and you will lose clarity.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/747e7fbf-3f68-4fb6-877d-07a8d94f7a98/timer-icon.jpg" alt="Screenshot" width="319" height="386" />

Neven emphasizes in his <a href="https://mrgan.tumblr.com/post/708404794/ios-app-icon-sizes">article</a> that:
<blockquote>“...it is simply not possible to create excellent, detailed icons which can be arbitrarily scaled to very small dimensions while preserving clarity. Small icons are caricatures: they exaggerate some features, drop others and align shapes to a sharp grid. Even if all icons could be executed as vectors, the largest size would never scale down well.”</blockquote>

Although here he is talking exclusively about icons, his description is apt for most UI elements. The decisions involved in scaling are creative, not mechanical. Vector-based elements aren’t suitable for all resolutions, if you value quality.</p>

## Ahead-of-time Resolution Independence

The best quality results — and the method Apple chose for the iPhone 3GS to iPhone 4 transition — comes from pre-rendered images, built for specific devices, at specific resolutions: bespoke designs for each required size, if you will. It’s more work, but pre-rendering images ensures everything always looks as good as possible.

Apple chose to <strong>exactly double the resolution from the iPhone 3GS to the iPhone 4</strong>, making scaling even easier (different from the approach of <a href="https://developer.android.com/guide/practices/screens_support.html">Google</a> and <a href="https://msdn.microsoft.com/en-us/library/bb278110.aspx">Microsoft</a> — notice that this article is not relevant to the latest version of Microsoft's mobile OS — proving yet again that controlling the entire stack has huge advantages).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/287e7469-b4e1-4e3b-bbdb-5b03264c8383/double.jpg" alt="Screenshot" width="298" height="303" />

Currently, there are three iOS resolutions:

*   320 × 480 (iPhone/iPod touch)
*   640 × 960 (iPhone 4 and iPod with Retina display)
*   768 × 1024 / 1024 × 768 (iPad)

In a few years, it seems highly likely that the line-up will be:

*   640 × 960 (iPhone/iPod touch with Retina display)
*   1536 × 2048 / 2048 × 1536 (iPad with Retina display)
*   Some kind of iOS desktop iMac-sized device with a Retina display

There are significant differences between designing iPhone and iPad apps, so completely reworking app layouts seems necessary anyway — you can’t just scale up or pad your iPhone app, and expect it to work well or look good on an iPad. The difference in screen size and form factor means each device should be treated separately. The iPad's size makes it possible to show more information on the one screen, while iPhone apps generally need to be deeper, with less shown at once.</p>

## Building Designs That Scale

Building apps for the iPhone 4 Retina display involves creating two sets of images — one at 163 ppi and another at 326 ppi. The 326 ppi images include @2x at the end of their filename, to denote that they’re double the resolution.

When it comes to building UI elements that scale easily in Adobe Photoshop, <strong>bitmaps are your enemy</strong> because they pixelate or become blurry when scaled. The solution is to create solid color, pattern or gradient layers with vector masks (just make sure you have "snap to pixel" turned on, where possible). While a little awkward at times, switching to all vectors does have significant advantages.

Before anyone mentions it, I’m not suggesting any of the methods are new; I'm willing to bet that most icon designers have been working this way for years. I’ve been using vector shapes for ages too, but the Retina display has changed my practice from using vector shapes only when I could be bothered, to building entire designs exclusively with vector shapes.

I usually <strong>draw simple elements directly in Photoshop</strong> using the Rectangle or Rounded Rectangle Tool. Draw circles using the Rounded Rectangle Tool with a large corner radius, because the ellipse tool can’t snap to pixel. Layer groups can have vector masks too, which is handy for complex compositing (option-drag a mask from another layer to create a group mask).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a3647e8-8bfa-44eb-a971-10162daa259c/vector-only-psd.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53a55fc7-dd61-426c-8265-009273907587/iconpsd.jpg" alt="Screenshot" width="500" height="396" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a3647e8-8bfa-44eb-a971-10162daa259c/vector-only-psd.png">Full view</a></em>

More complex objects get drawn in Adobe Illustrator to the exact pixel size, and then pasted into Photoshop as a shape layer. Be careful when pasting into Photoshop, as the result doesn’t always align as it should — it’s often half a pixel out on the x-axis, y-axis or both. The workaround is to zoom in, scroll around the document with the Hand Tool, and paste again. Repeat until everything aligns. Yes, it’s maddening, but the method works after a few attempts. Another option is to zoom in to 200%, select the path with the Direct Selection Tool, and nudge once, which will move everything exactly 0.5px.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d3f320a-42d2-440d-99ea-0ecd818865e7/complexshapes.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e6a40fe-4522-453c-8e81-3dbf9cd7946e/complex.jpg" alt="Screenshot" width="500" height="196" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d3f320a-42d2-440d-99ea-0ecd818865e7/complexshapes.png">Full view</a></em>

Even more complex objects requiring multiple colors get drawn in Illustrator to the exact pixel size, and then pasted into Photoshop as a Smart Object. It is a last resort, though — gradients aren’t dithered, and editing later is more difficult.

If you need to use a bitmap for a texture, there are three options: use a pattern layer, a pattern layer style, or build a bitmap layer at the 2× size and turn it into a Smart Object. I prefer to <strong>use pattern layer styles</strong> in most cases, but be warned: patterns are scaled using bicubic interpolation when you scale the entire document, so they become "softer." The solution is to create two versions of each pattern, then to manually change pattern layer styles to the correct pattern after scaling — a little tedious, but totally do-able approach.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47985335-7304-4a7b-adee-523ddc109645/vector-only-psd-consume.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1271e163-b0ca-4268-b93e-59078a5f1e4c/delete.jpg" alt="Screenshot" width="550" height="436" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47985335-7304-4a7b-adee-523ddc109645/vector-only-psd-consume.png">Full view</a></em>

## Scaling Up

At this point, your document should be able to scale to exactly double the size, without a hitch.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f0aabeb-24b5-4b94-b998-29f970f1a486/scaling2.jpg" alt="Screenshot" width="500" height="398" />

I have a Photoshop Action set up that takes a History Snapshot, then scales to 200%. That means, previewing at the Retina display’s resolution is only a click away. If you’re feeling confident you’ve built everything well, you should be able to scale up, edit, then scale down and continue editing without degradation. If you run into trouble, a Snapshot is there to take you back. Using one document for both resolutions, means not having to keep two documents in sync — a huge advantage.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab38380e-739d-4857-aa2e-4ff0657220b3/actions2.jpg" alt="Screenshot" width="500" height="94" />

A word of warning: layer styles can only contain integer values. If you edit a drop shadow offset to be 1 px with the document at 2× size, and then scale it down, the value will end up as 1 px because it can’t be 0.5 px (a non-integer value). If you do require specific changes to the 2× version of the Photoshop file, you’ll have to save that version as a separate file.</p>

## Exporting, Exporting, Exporting

Now for some bad news: exporting all the images to build an app <strong>can be extremely tedious</strong>, and I don’t have much advice here to assist you. As my documents act as full screen mockups, they’re not set up in a way that Photoshop’s Slice feature is any use. Layer comps don’t help either — I already have folders for each app state or screen, so switching things off and on is easy.

The best export method seems to be: enable the layers you’d like visible, make a marquee selection of the element, then use Copy Merged and paste the selection into a new document — not much fun when you have hundreds of images to export.

The problem is amplified when saving for the Retina display, where there are twice as many images and the 1× images must match the 2× images precisely.

The best solution I’ve come up with so far:

*   Build your design at 1×
*   Use Copy Merged to save all the 1× images
*   Duplicate the entire folder containing the 1× images
*   Use Automator to add @2x to all the filenames
*   Open each @2x image and run the "Scale by 200%" Photoshop action. This gives you a file with the correct filename and size, but with upscaled content
*   Scale your main Photoshop design document by 200%
*   Use Copy Merged to paste the higher quality elements into each @2x document, turn off the lower quality layer, then save for the Web, overwriting the file.

In some cases, Photoshop’s "Export Layers To Files" can help. The script can be found under the File menu.</p>

## Mac Actions and Workflows

All the Actions and Workflows that I use myself can be downloaded from the blog post link below. The Automator Workflows can be placed in your Finder Toolbar for quick access from any Finder window, without taking up any space in your Dock.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d07e5e2-40a8-4fa7-90f3-84eece378dbf/retina-actions-and-workflows1.zip">Download: Retina Actions and Workflows.zip</a>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/371f7faa-56e8-4102-93fe-254ecd17a02d/promo-2x.jpg" alt="Screenshot" width="505" height="330" />

Fortunately, Apple chose to exactly double the resolution for the iPhone 4, and for using ahead-of-time resolution independence. As complex as the process is now, things would have been far worse if they had chosen a fractional scale for the display.
<em>(rs) (ik) (vf)</em>


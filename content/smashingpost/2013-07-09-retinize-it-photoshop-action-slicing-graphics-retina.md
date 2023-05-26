---
title: 'Retinize It: Free Photoshop Action For Slicing Graphics For HD Screens'
slug: retinize-it-photoshop-action-slicing-graphics-retina
image: null
date: 2013-07-09T18:00:13.000Z
author: artiom-dashinsky
description: >-
  High-definition (or “Retina”) displays have spread wider and wider, and
  evidently their numbers will keep growing. So, as creators of products that
  will be consumed on Retina devices, we have to optimize our design and
  development workflow accordingly.
categories:
  - Graphics
  - Freebies
  - Photoshop
---
High-definition (or “Retina”) displays have spread wider and wider, and evidently their numbers will keep growing. So, as creators of products that will be consumed on Retina devices, we have to optimize our design and development workflow accordingly.

Slicing graphics from finished designs to use for development is one of the less enjoyable parts of building a website or app. And it takes a long time. Because slicing is a monotonous and straightforward task, using the right tool and workflow <strong>can save you hours or even days of work</strong>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09c58e57-0e62-4527-bcbc-ecc140075f28/retinize-it-action-mini.png"><img loading="lazy" decoding="async" class="162055" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09c58e57-0e62-4527-bcbc-ecc140075f28/retinize-it-action-mini.png" alt="retinize-it-action" width="500" height="354" /></a>

Preparing graphics for development mostly entails saving user-interface elements from the final mockups, with transparent backgrounds. And to support Retina displays, we also need to create double-sized versions of elements.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Retina Asset Workflow You’ve Always Wanted For Photoshop](https://www.smashingmagazine.com/2016/03/the-retina-asset-workflow-youve-always-wanted-for-photoshop/)
*   [Create Pixel-Perfect Assets For Multiple Scale Factors](https://www.smashingmagazine.com/2014/10/create-assets-for-multiple-scale-factors/)
*   [Photoshop Etiquette For Responsive Web Design](https://www.smashingmagazine.com/2016/08/photoshop-etiquette-for-responsive-web-design/)
*   [<span class="headline">Towards A Retina Web</span>](https://www.smashingmagazine.com/2012/08/towards-retina-web/)

{{% feature-panel %}}

Upon failing to find a tool that fits my design team’s workflow, <strong>I created a set of two time-saving Photoshop actions</strong> for slicing graphics for Retina and standard displays. The great feedback from my team inspired me to share it with other designers. The tool has gotten good buzz in the Web design and front-end development community, so today I’m happy to introduce <a href="https://retinize.it">Retinize It</a> on Smashing Magazine.

<a href="https://retinize.it/"><img loading="lazy" decoding="async" class="162057" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b47802e-8d42-45f2-8a25-6844d88d2d42/retinize-it-website-mini.jpg" alt="Retinize It website" width="500" height="482" /></a><br>
<em>Retinize It uses Photoshop actions and <a href="https://retinajs.com">retina.js</a> to optimize for Retina displays.</em>

## How It Works

Select one layer, several layers or a group of layers, and run the action. Once you’ve activated it, you just need to name the files and set the directory to save them to.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e9ca96-f45b-495d-a36a-484a2a2692ba/steps1-mini.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ea1b40b-24ae-4be2-b365-e1e4d8b3209b/steps2-mini.jpg" alt="Retinize It" width="500" height="556" /></a>

In the background, Retinize It copies the selected layers to a new file, makes the background transparent and trims the space around the element. Once that’s done, the action asks what you want to name the file, saves it, scales the original element by 200%, and saves that as a separate file. After this process, you’ll be returned to the original file.</p>

### How Much Of The Slicing Process The Action Saves

Almost all of it. The only thing you have to do is choose the directory and name the files. Remember to add a high-resolution modifier, <code>@2x</code>, for the Retina versions of the files. This convention was <a href="https://developer.apple.com/library/ios/#documentation/2DDrawing/Conceptual/DrawingPrintingiOS/SupportingHiResScreensInViews/SupportingHiResScreensInViews.html#//apple_ref/doc/uid/TP40010156-CH15-SW1">established</a> in Apple’s iOS Developer Library.

If you’re building an iOS application, then you’ll need to provide a background and splash screen in three resolutions: standard (320 × 480 pixels), Retina (640 × 960 pixels) and iPhone 5 (1136 × 640 pixels). The naming convention for the standard and Retina versions is straightforward. For images for the iPhone 5’s screen resolution, Apple recommends adding a <code>-568h@2x</code> suffix, although Apple doesn’t require it.

Apparently, this happens because Xcode does not automatically associate <code>-568h@2x</code> images with the iPhone 5’s resolution; developers may set the suffix manually for this kind of file. I’ve worked with an iOS developer who has asked Apple to add a <code>@5x</code> suffix. So, the best way to determine the naming convention for iPhone 5 images in future is to ask your developer. In other cases, use the <code>-568h@2x</code> suffix.

The techniques presented in the article “<a href="https://www.smashingmagazine.com/2012/08/20/towards-retina-web/">Towards A Retina Web</a>” bring the <code>@2x</code> convention from mobile apps to the Web, helping us to optimize websites for Retina displays very quickly.</p>

### Why Scale by 200% and Not 50%?

Retinize It is <strong>good for those who start designing at non-Retina sizes</strong>, which is a better practice for two reasons. First, the non-Retina version of an image will look much closer to the final product, giving you more accurate feedback on how the design will actually look.

Secondly, an element with an odd size value that is scaled by 50% will end up with a x.5 pixel value, making the element blurry. Bjango explains this issue in his article “<a href="https://bjango.com/articles/designingforretina2/">Designing for Retina Display</a>,” as does Niklaus Gerber in his article “<a href="https://niklausgerber.com/blog/designing-for-iphone4/">Designing for the iPhone 4</a>.”

### What Kind of Layers Will This Work With?

The non-Retina action in this pack will work with any kind of layer. If you’re using the Retina version, then you should work with shapes and smart objects, so that the 200%-scaled file will not look pixelated.

Also, if your layer has an inner or drop shadow, then uncheck “Use Global Light”; otherwise, those effects in the sliced version of the layer will inherit Photoshop’s default angle.</p>

## What Does The Set Include?

The set includes two Photoshop actions:

*   **Slice It**.  This action slices a 100%-sized version of an element.
*   **Retinize It**.  This action saves a 100%-sized version and a 200%-scaled version.</p>

## What Makes It Special?

*   It’s free to use.
*   Install in one click.
*   You don’t need to change the layer structure in PSD files.
*   You don’t need to name layers.
*   It’s optimized for Retina displays.
*   Run in one click, no setup needed.
*   Windows and Mac support.</p>

## Download And Documentation

*   [Retinize It](https://retinize.it) website includes FAQ and additional information.
*   [Download](https://retinize.it/RetinizeIt.atn.zip) (ZIP, 4 KB)

## Additional Tools

### PNG EXPRESS (MAC & Windows, $29)

<a href="https://www.pngexpress.com"><img loading="lazy" decoding="async" class="163988" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcb90830-7fa7-4c81-8812-e84b684bd4e2/png-express-mini.jpg" alt="png-express" width="500" height="301" /></a><br>
<em>A specification created by PNG Express</em>

If you will be having limited interaction with the developer who will be coding your design and you’re not sure it will be pixel-perfect, <a href="https://www.pngexpress.com">PNG Express</a> can be a great time-saver. It helps you to create specifications with instructions on element positions, margins, fonts and font sizes.

PNG Express also has an option for slicing images including Retina support.</p>

### ImageOptim (Mac Only, Free)

<a href="https://imageoptim.com"><img loading="lazy" decoding="async" class="163990" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fd7d576-b605-4892-bcd1-f59aec8f381b/imageoptim-mini.jpg" alt="imageoptim" width="652" height="426" /></a>

<a href="https://imageoptim.com">ImageOptim</a> reduces image sizes while maintaining quality. The tool removes internal data embedded by graphics editors, such as comments and color profiles. I recommend adding an images folder from your website to this app before compiling and going live. ImageOptim will reduce around 30% of an image’s size on average.</p>

### Slicy (Mac Only, $29)

<a href="https://macrabbit.com/slicy/"><img loading="lazy" decoding="async" class="165811" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5509fc0b-1775-4d68-a131-a3ce766bc447/slicy-mini.jpg" alt="slicy_mini" width="500" height="300" /></a>

<a href="https://macrabbit.com/slicy/">Slicy</a> is great-designed tool most designers and developers are using for slicing graphics for iOS apps. The tool exports graphics from PSDs automatically, but it requires to organize your layers in Photoshop and name them in certain way. In addition once you make changes in Photoshop, Slicy updates the slices automatically. The main reason I decided not to use Slicy is no ability for quick export for couple of elements from PSD without preparing it for Slicy.

{{< signature "al" >}}


---
title: Automatically Art-Directed Responsive Images? Here You Go.
slug: automatically-art-directed-responsive-images-go
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6a1b7a6-e94c-4dd6-bff3-17b098e05740/obama-demo-large.png
date: 2016-02-08T09:03:57.000Z
author: vitaly-friedman
description: >-
  In many projects, [responsive images](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/) aren’t a technical issue but a strategic concern. Delivering different images to different screens is technically possible with srcset and sizes and <picture> element and [Picturefill](https://github.com/scottjehl/picturefill) (or a similar) polyfill; but all of those variants of images have to be created, adjusted and baked into the logic of the existing CMS. And that's not easy. 
categories:
  - Coding
  - Tools
  - Responsive Images
---
In many projects, <a href="https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/">responsive images</a> aren’t a technical issue but a <strong>strategic concern</strong>. Delivering different images to different screens is technically possible with srcset and sizes and &lt;picture&gt; element and <a href="https://github.com/scottjehl/picturefill">Picturefill</a> (or a similar) polyfill; but all of those variants of images have to be created, adjusted and baked into the logic of the existing CMS. And that's not easy.

On top of that, <a href="https://dev.opera.com/articles/responsive-images/">responsive images markup</a> has to be generated and added into HTML as well, and if a new image variant comes into play at some point (e.g. a file format like WebP or a large landscape/portrait variant), the markup has to be updated. The amount of extra work required often causes trouble — so if you have a perfect product shot, you need to either manually create variants for mobile and portrait and landscape and larger views, or build plugins and extensions to somehow automate the process.</p>

<figure><a href="https://www.netvlies.nl/tips-updates/design-interactie/retina-revolution"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f192a0b6-0361-4cca-968b-04d54ba29ca8/retina-revolution-large.png" alt="Compressive Images Technique" width="410" height="367" /></a><figcaption><a href="https://www.netvlies.nl/tips-updates/design-interactie/retina-revolution">Compressive images technique</a>: doubling in file dimensions, saving with the worst possible quality.</figcaption></figure>

Sometimes workarounds work just well, too. One of them is <a href="https://www.netvlies.nl/tips-updates/design-interactie/retina-revolution">compressive</a> <a href="https://www.filamentgroup.com/lab/compressive-images.html">images</a>, a clever technique which suggests that the <strong>level of compression makes more of a difference</strong> than its physical dimensions. So, in Scott Jehl's words, "given two identical images that are displayed at the same size on a website, one can be dramatically smaller than the other in file size if it is both highly compressed and dramatically larger in dimensions than it is displayed."

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Simple Responsive Images With CSS Background Images](https://www.smashingmagazine.com/2013/07/simple-responsive-images-with-css-background-images/)
*   [Automate Your Responsive Images With Mobify.js](https://www.smashingmagazine.com/2013/10/automate-your-responsive-images-with-mobify-js/)
*   [How To Solve Adaptive Images In Responsive Web Design](https://www.smashingmagazine.com/2013/06/clown-car-technique-solving-for-adaptive-images-in-responsive-web-design/)
*   [Responsive Images In WordPress With Art Direction](https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/)

{{% feature-panel %}}

So basically we could enlarge a given image, save it in the worst possible quality in Photoshop, and let the browser do the rescaling — on average, the actual image sent down the network would be larger in dimensions but approximately <strong>50–65% smaller</strong> in file size. Now, that's quite a difference. <a href="https://www.smashingmagazine.com/2013/09/responsive-images-performance-problem-case-study/">And it works in real projects.</a>

The downside: we offload the work to the client and if the user chooses to save the image, they'll get a pretty suboptimal version of it. And it doesn't help us with art-directed images either. That's not quite a clean solution that we are looking for.</p>

## The Devil Is In The... Back-End!

A common scenario would be to integrate some sort of a back-end logic in the CMS, allowing content managers to upload images, define focal points for every given image and generate all of those cropped variants of each image on the fly.</p>

<figure><a href="https://blog.imgix.com/2015/10/21/automatic-point-of-interest-cropping-with-imgix.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5651d22f-8995-4397-87d2-789128cdd3d6/imgix-entropy.jpg" alt="Cropping entropy with imgix." width="500" height="213" /></a><figcaption><a href="https://blog.imgix.com/2015/10/21/automatic-point-of-interest-cropping-with-imgix.html">Automatic Point-of-Interest Cropping with imgix</a>, using the <code>crop=entropy</code> parameter for intelligent automated cropping.</figcaption></figure>

The "cropping" bit is a tricky one, and if you're perfectly fine with resizing the images without art direction and allowing the browser to select an image that it feels would fit best, it won’t be a big hassle — you could use <a href="https://github.com/excellenteasy/grunt-image-resize">ImageMagick</a> or any other image editing tool for rescaling, or CMS plugins could take care of it for you: e.g. <a href="https://www.smashingmagazine.com/2013/10/automate-your-responsive-images-with-mobify-js/">Mobify.js API</a>, <a href="https://www.smashingmagazine.com/2015/12/responsive-images-in-wordpress-core/">Responsive Images in WordPress core</a> and there is a <a href="https://www.drupal.org/project/responsive_images">solution for Drupal</a>, too.

However, if art direction <em>does</em> matter — e.g. if you want to send very specific product shots to different kinds of screens — you’ll have to look into more advanced options. A wide landscape photo scaled down for the narrow viewport won't be particularly helpful, and neither would a narrow image scaled up to fill the entire viewport on a wide screen. That's where we need better, smarter solutions.</p>

## So What Are The Options?

Well, we could run batch processing through the <a href="https://www.youtube.com/watch?v=rSNbxL57QaI">content aware fill in Photoshop</a>, or use tools like <a href="https://github.com/jwagner/smartcrop.js/">Smartcrop.js</a>, which is a fairly simple implementation of <strong>content aware image cropping</strong> with JavaScript. Potentially we could even integrate the <a href="https://github.com/jwagner/smartcrop-cli">smartcrop-cli</a> (along with <a href="https://github.com/JamieMason/ImageOptim-CLI">ImageOptim-CLI</a>) into our Grunt- and Gulp-building processes and crop images on the fly. You could also use <a href="https://blog.imgix.com/2015/10/21/automatic-point-of-interest-cropping-with-imgix.html">imgix</a> with its automatic point-of-interest cropping. That's already a great start, but we'd need to write the markup for all those variants manually.</p>

<figure><a href="https://github.com/jwagner/smartcrop.js/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff51a01a-20a4-4b25-89c7-2844e7042b74/smartcrop-large.png" alt="Smartcrop.js" width="500" height="328" /></a><figcaption><a href="https://github.com/jwagner/smartcrop.js/">Smartcrop.js</a>, a fairly simple implementation of content aware image cropping with JavaScript.</figcaption></figure>

Good news: there is a new kid around the block. Just a few days ago we’ve written about the <a href="https://www.smashingmagazine.com/2016/01/responsive-image-breakpoints-generation/">Responsive Image Breakpoints Generator</a>, a little open source tool that allows you to calculate breakpoints for your images interactively. Basically, you can upload an image, and the tool will detect appropriate breakpoints, rescale images and <strong>generate responsive images markup</strong> that you can then copy/paste into your HTML. You can go even further and <a href="https://cloudinary.com/blog/automatically_art_directed_responsive_images">automatically art direct responsive images</a> using the tool’s API.</p>

<figure><a href="https://cloudinary.com/blog/automatically_art_directed_responsive_images"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04841541-2ed2-49cf-a0e8-33a7b17541b4/obama-demo-500px.png" alt="Smartcrop.js" width="500" height="328" /></a><figcaption>An <a href="https://ericportis.com/etc/cloudinary/">art-directed responsive images demo</a> by Eric Portis, based on his <a href="https://cloudinary.com/blog/automatically_art_directed_responsive_images">article</a> on automatically generated art-directed images.</figcaption></figure>

As Eric Portis <a href="https://cloudinary.com/blog/automatically_art_directed_responsive_images">explains in his article</a>, when using Cloudinary API, you can specify a <code><a href="https://cloudinary.com/documentation/image_transformations#crop_modes">crop_mode</a></code> which allows you to mimic <code>background-size: cover</code> in CSS. In addition to providing heights and widths, you can also specify the focal point using the <code>gravity</code> parameter, zooming factor and supply aspect ratios, which can make URLs a bit easier to read. In fact, the API supports face detection, so if your images contain human faces, art direction can be automated with a higher probability of pretty decent cropping.

If you want to be able to <strong>define focal points for images explicitly</strong>, you might want to look into <a href="https://www.sizzlepig.com/">Sizzlepig</a> (not free), an in-browser image batch processing tool that can be integrated with Google Drive and Dropbox, and allows you to change cropping and scaling for each image.

## Summary

Ideally, we'd love to have one tool that would either generate "smart enough" crops and plug in the responsive images markup in the build automatically, or provide one interface to visually adjust the focal point of images and output "ready-to-go" markup. We aren't quite there yet, but we might be soon.

In the meantime, the tools listed above could be good enough options to consider when tackling a quite daunting task of producing art-directed variants of images — either manually or by building custom CMS plugins.

{{< signature "vf" >}}


---
title: Efficient Image Resizing With ImageMagick
slug: efficient-image-resizing-with-imagemagick
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e09f5015-21d2-42b1-bd66-54595b784dcb/excerpt-image-resizing.jpg
date: 2015-06-25T20:11:31.000Z
author: david-newton
summary: >-
  <a href="https://www.smashingmagazine.com/2014/05/14/responsive-images-done-right-guide-picture-srcset/">Responsive</a> <a href="https://www.smashingmagazine.com/2014/02/03/one-solution-to-responsive-images/">images</a> have been keeping us on our toes for quite some time, and now that they are getting traction in browsers, they come with a scary problem: the need to efficiently resize all our image assets.
description: >-
  <a href="https://www.smashingmagazine.com/2014/05/14/responsive-images-done-right-guide-picture-srcset/">Responsive</a> <a href="https://www.smashingmagazine.com/2014/02/03/one-solution-to-responsive-images/">images</a> have been keeping us on our toes for quite some time, and now that they are getting traction in browsers, they come with a scary problem: the need to efficiently resize all our image assets.
categories:
  - Workflow
  - Optimization
  - Performance
  - Responsive Images
---
The way responsive images work is that an appropriately sized image is sent to each user &mdash; small versions for users on small screens, big versions for users on big screens. It’s fantastic for web performance, but we have to face the grim reality that serving different sizes of images to different users means that we first need to create all of those different files, and <a href="https://twitter.com/tessthornton/status/565960345467252739">that can be a huge pain</a>.

Many tools out there automate image resizing, but too often they create large files that cancel out the performance benefits that responsive images are supposed to deliver. In this article, we’ll see how we can use <a href="https://imagemagick.org/">ImageMagick</a> &mdash; an open-source command-line graphics editor &mdash; to quickly resize your images, while <strong>maintaining great visual quality</strong> and really tiny file sizes.

{{% feature-panel %}}

## Big Images == Big Problem

The <a href="https://httparchive.org/interesting.php?a=All&amp;l=May%2015%202015">average web page is about 2 MB</a> in size, and about two thirds of that weight is from images. At the same time, millions of people are accessing the Internet on 3G-or-worse connections that make a 2 MB website a horror show to use. Even on a fast connection, a 2 MB website can wreak havoc on your users’ data plans and <a href="https://whatdoesmysitecost.com/">cost them real money</a>. Improving web performance and giving a better experience to our users is our job as developers and designers.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c46cc42-3cf7-4e02-a69c-93dff5fe83e0/01-httparchive-opt.png"><img loading="lazy" decoding="async"  class="alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58f72418-b5ee-4765-8e80-e463623a921d/01-httparchive-opt-small.png" alt="imagemagick resize " width="500" height="350" /></a><figcaption>The average web page is 2,099 KB, 1,310 KB of which comes from images. (Image: <a href="https://httparchive.org//">HTTP Archive</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c46cc42-3cf7-4e02-a69c-93dff5fe83e0/01-httparchive-opt.png">View large version</a>)</figcaption></figure>

<a href="https://responsiveimages.org/">Responsive images</a> to the rescue! Right? Well, yes, but first we have to generate our responsive image assets, and we have to make sure those assets look good and have a small enough footprint to improve the website’s performance.

For a very small website, saving a few different sizes of each image directly in our image editor is trivial &mdash; Photoshop even provides a handy “Save for Web” option that keeps file sizes low. But what about a large website with a lot of images? An online store, for example, might have hundreds or thousands of image assets, and having to create different sizes of each of these is an enormous task.

## ImageMagick

This is where <strong>automated image resizing</strong> comes in handy. A bunch of tools out there do this, including <a href="https://libgd.github.io/">GD</a> and <a href="https://www.graphicsmagick.org/">GraphicsMagick</a>, but <a href="https://imagemagick.org/">ImageMagick</a> strikes a good balance between power and availability in hosting environments. ImageMagick has been around for almost 25 years and is a full-fledged command-line image editor. It is widely supported by content management systems (CMS) such as <a href="https://wordpress.org/">WordPress</a> and <a href="https://www.drupal.org/">Drupal</a>, integrated with task runners such as <a href="https://gruntjs.com/">Grunt</a>, and used on its own to automate image editing &mdash; including resizing.

It’s also available on desktop systems (Mac, Windows and Linux). If you use <a href="https://brew.sh/">Homebrew</a> on a Mac, you can install it like this:

<pre><code class="language-bash">brew install imagemagick</code></pre>

Otherwise, look for it in your favorite package manager, or <a href="https://imagemagick.org/script/binary-releases.php">download it directly from the ImageMagick website</a>.

ImageMagick provides a fast, simple way to automate image resizing. Unfortunately, with the default settings, the resized files it outputs are often really big &mdash; sometimes bigger than the inputted image, even though the output has fewer pixels. These big files completely negate the performance gains you’d expect to get from responsive images and, in fact, can make things worse for your users than if you’d simply loaded the huge unshrunk assets.

Below, I’ll describe why this problem exists and show you how to change ImageMagick’s default settings to solve this problem and get small, great-looking images.

{{% ad-panel-leaderboard %}}

## How Image Resizing Works

The best way to solve the problem is to understand why it’s happening, and that means understanding the basics of how image resizing works.

By definition, when a computer resizes an image, the number of pixels in that image will change. If the image is being enlarged, the output will have more pixels than the input; if the image is being shrunk, the output will have fewer pixels than the input. The challenge is in figuring out the best way to store the original image’s <em>content</em> in this different number of pixels. In other words, we need to figure out the best way to add or remove pixels without changing what the image looks like.

Although not as common a use case, image <strong>upsampling</strong> (i.e. making images larger) can be a little easier to visualize, so let’s start with that. Consider an image of a blue 4 × 4 pixel square that we want to double in size to 8 × 8 pixels. What we’re doing is taking the same image and applying it to a new pixel grid; this is called <strong>resampling</strong> and is usually what we mean when we talk about resizing images. To resample our 4 × 4 blue square to 8 × 8 pixels, we need to add 48 extra pixels somewhere. Those pixels will need some color value, and the process of determining that color value is called <strong>interpolation</strong>. When you’re resampling, the algorithm for determining how the interpolation works is called a <strong>resampling filter</strong>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55ca2887-6ef3-4c91-bd0d-f445005c2ee6/02-squares-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee21959b-6242-4fc7-8890-dce57652d024/02-squares-opt-small.png" alt="Two blue squares, one 4 by 4 pixels, the other 8 by 8" /></a><figcaption>How do we resample a 4 × 4 pixel square to an 8 × 8 pixel grid? (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55ca2887-6ef3-4c91-bd0d-f445005c2ee6/02-squares-opt.png">View large version</a>)</figcaption></figure>

We could use all sorts of resampling filters and interpolation methods to figure out those 48 extra pixels. The absolute simplest thing we could do is to add four more rows and four more columns of pixels in some arbitrary color &mdash; say, red. This is called <strong>background interpolation</strong>, because the empty pixels are simply exposing a background color (red). This is what you’re doing in Photoshop when you resize using “Image” → “Canvas Size,” instead of “Image” → “Image Size.”

This, of course, is a terrible outcome when we want to resize an image: we don’t perceive the new outputted image to really look like the original inputted image at all; the original square is blue, the new one is blue and red. Background interpolation is only possible when adding pixels (i.e. when making the image bigger or when upsampling), and even then it is essentially useless for resizing, except as a means to show where the new pixels are.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/118f3aba-033b-4396-9361-38f4543997dc/03-square-background-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/612817b7-d837-4a52-a525-374e7aa7ef33/03-square-background-opt-small.png" alt="A pink and blue square" /></a><figcaption>Background interpolation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/118f3aba-033b-4396-9361-38f4543997dc/03-square-background-opt.png">View large version</a>)</figcaption></figure>

Another very simple interpolation method is to <strong>make our new pixels the same color</strong> as their neighboring pixels; this is called nearest-neighbor interpolation. This produces a much better result than background interpolation, especially for a simple square like this.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5531c3a3-77f3-4c4f-b770-ba6f5d7883ca/04-square-nearestneighbour-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edec96e9-c016-4305-bb4b-3faf7f3e62fb/04-square-nearestneighbour-opt-small.png" alt="A blue square" /></a><figcaption>Nearest-neighbor interpolation: upsampling a square. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5531c3a3-77f3-4c4f-b770-ba6f5d7883ca/04-square-nearestneighbour-opt.png">View large version</a>)</figcaption></figure>

<strong>Downsampling</strong> (i.e. making the image smaller) with nearest-neighbor interpolation is not as intuitive as upsampling, but it helps to remember that the math involved is OK with fractional pixels. First, the new pixel grid gets applied to the orignal image. Because there are fewer pixels to store the image information, some of the pixels in this new grid will contain multiple colors; in the example below, some pixels contain both blue and white.

Outputting the image in this way to the physical pixels in the real world isn’t possible, though &mdash; each pixel can be only one color. The final color of each pixel in the new grid is determined by the color at its center point. In other words, that center <strong>point</strong> is <strong>sampled</strong> to determine the final color, which is why nearest-neighbor interpolation is sometimes called <strong>point sampling</strong>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6896827d-8e5a-439c-8373-c55c2d93c06b/05-nearest-neighbour-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7659af34-04de-4526-aef1-f1d7e07d4de3/05-nearest-neighbour-opt-small.png" alt="Four images: a circle; an 8×8 pixel grid; the grid overlayed on top of the circle with the center marked; and the resized circle, which is blocky and not very circular" /></a><figcaption>Nearest-neighbor interpolation: downsampling a circle. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6896827d-8e5a-439c-8373-c55c2d93c06b/05-nearest-neighbour-opt.png">View large version</a>)</figcaption></figure>

For anything more complicated than a line or square, nearest-neighbor interpolation produces very jagged, blocky images. It’s fast and creates small files but doesn’t look very good.

Most resampling filters use some sort of variation on nearest-neighbor interpolation &mdash; they sample multiple points to determine the color of a pixel and use math to try to come up with a smart compromise for those values. Bilinear interpolation, for example, creates a weighted average of colors. It produces much nicer results than nearest-neighbor interpolation.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce31d2ac-5381-4644-b00b-1177d7a7a295/06-circles-bilinear-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/928245a5-d1a4-4ced-aa69-bad0db57a0ad/06-circles-bilinear-opt-small.png" alt="Two circles" /></a><figcaption>Bilinear interpolation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce31d2ac-5381-4644-b00b-1177d7a7a295/06-circles-bilinear-opt.png">View large version</a>)</figcaption></figure>

One way that resampling &mdash; and the specific resampling filter used &mdash; can affect file size is by affecting the colors in the image. Bilinear interpolation gives the circle smooth edges, but that means giving the image more colors. The original blue circle has two colors, blue and white. The resized circle has more &mdash; some pixels are a pale bluey-white. All else being equal, more colors in an image will make the file size bigger. This is one reason why resizing an image to have fewer pixels sometimes gives it more bytes.

### What All This Means for Us

In order to make our outputted images smaller, we’ll want to look at ways to reduce the number of colors without sacrificing quality. Choosing an appropriate resampling filter has one of the biggest effects, but other settings can affect the number of colors in the output as well. I’ll also discuss settings that control file compression and quality and that eliminate extraneous data.

{{% ad-panel-leaderboard %}}

## Optimal Settings For ImageMagick

### ImageMagick Basics

ImageMagick has a <a href="https://www.imagemagick.org/script/command-line-options.php">ton of options and functions</a>, and finding a good combination of these can be tricky.

Two main ImageMagick settings are of interest to us, <code>convert</code> and <code>mogrify</code>. Both of these perform similar operations, but <code>mogrify</code> is intended to be used with multiple files at once, while <code>convert</code> handles only one image at a time.

A simple ImageMagick operation might look like this:

<pre><code class="language-bash">convert input.jpg -resize 300 output.jpg</code></pre>

This says that we want ImageMagick’s <code>convert</code> function to take <code>input.jpg</code> and resize it to 300 pixels wide, and then save that to <code>output.jpg</code>. The <code>-resize 300</code> part is an example of one of ImageMagick’s many built-in functions. Each function uses the same format: <code>-functionName option</code>.

Using <code>mogrify</code> is similar, but with the syntax reordered a bit:

<pre><code class="language-bash">mogrify -path output/ -resize 300 *.jpg</code></pre>

This says that we want ImageMagick’s <code>mogrify</code> function to take all JPEG files in the current directory (<code>*.jpg</code>), resize them to 300 pixels wide and then save them in the <code>output</code> directory.

Functions can be combined for more complex results:

<pre><code class="language-bash">convert input.jpg -resize 300 -quality 75 output.jpg</code></pre>

As before, this resizes <code>input.jpg</code> to 300 pixels wide, but this time it also sets the JPEG quality to 75 before saving it to <code>output.jpg</code>.

I’ve performed <a href="https://github.com/nwtn/image-resize-tests">hundreds of tests</a> to see which combinations of functions and options produce the smallest results at an acceptable quality.

### Testing and Results

I wanted to keep the file size as low as possible but keep the quality high &mdash; indistinguishable from Photoshop’s “Save for Web.” To do this, I used both a subjective quality measure &mdash; my own opinion on whether the output looks good &mdash; and an objective quality measure &mdash; <a href="https://en.wikipedia.org/wiki/Structural_similarity">structural dissimilarity</a> (DSSIM). DSSIM compares two images &mdash; in this case, my test image and a control generated by Photoshop’s “Save for Web” &mdash; and generates a score. The lower the score, the more the images resemble each other; a score of zero means they are identical. To make sure test images look the same as Photoshop’s output, I wanted a mean DSSIM score of 0.0075 or lower. In <a href="https://www.radware.com/neurostrata-fall2014/">research released last year</a>, <a href="https://www.radware.com/">RadWare</a> found that image pairs with a DSSIM score of 0.015 were indistinguishable to their test users.

To make sure the results weren’t biased by outliers, I tested on 40 images that are a mixture of JPEGs and PNGs; photos, drawings and line art; color and monochrome; transparent and opaque. I also tested at three output sizes (300, 600 and 1200 pixels wide) from a variety of input sizes. Finally, I tested both with and without image optimization.

From my tests, running ImageMagick with the following settings <strong>produced the smallest results</strong>, while generally being visually indistinguishable from Photoshop’s output:

<div class="break-out">

 <pre><code class="language-bash">mogrify -path OUTPUT_PATH -filter Triangle -define filter:support=2 -thumbnail OUTPUT_WIDTH -unsharp 0.25x0.25+8+0.065 -dither None -posterize 136 -quality 82 -define jpeg:fancy-upsampling=off -define png:compression-filter=5 -define png:compression-level=9 -define png:compression-strategy=1 -define png:exclude-chunk=all -interlace none -colorspace sRGB -strip INPUT_PATH
</code></pre>
</div>

That’s a lot to take in, so let’s go through each bit and see what it means.

### Mogrify vs. Convert

As mentioned, ImageMagick provides two similar tools for manipulating images: <code>convert</code> is the basic image editor and works on one image at a time; <code>mogrify</code> is mostly used for batch image manipulation. In an ideal world, these two tools would produce identical results; unfortunately, that’s not the case &mdash; <code>convert</code> <a href="https://www.imagemagick.org/discourse-server/viewtopic.php?f=3&amp;t=27177">has a bug</a> that makes it ignore one of the settings I recommend using (the <code>-define jpeg:fancy-upsampling=off</code> setting, discussed below), so using <code>mogrify</code> is better.

### Resampling

Choosing a resampling filter in ImageMagick is surprisingly complicated. There are three ways you can do this:

*   with the resizing **function** you choose,
*   with the `-filter` setting,
*   or with the `-interpolate` setting.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66a56988-2537-426f-b25b-149c7a720ac7/07-functions-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2012471e-8992-4904-9389-678093224d9b/07-functions-opt-small.jpg" alt="Example output from twelve different resizing functions" /></a><figcaption>One of these things just doesn’t belong here, but the rest look pretty much the same, which is why I used an objective quality measure. (Image: <a href="https://commons.wikimedia.org/wiki/File:Lesser_Sooty_Owl_at_Bonadio%27s_Mabi_Wildlife_Reserve.jpg">Richard Fisher</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66a56988-2537-426f-b25b-149c7a720ac7/07-functions-opt.jpg">View large version</a>)</figcaption></figure>

The most obvious resizing function to use is <code>-resize</code>, but it creates files that are too large. I looked at 11 different functions and found that <code>-thumbnail</code> does the best job of optimizing quality and file size. In most cases, the <code>-thumbnail</code> function uses a three-step process to resize images:

1.  It resizes the image to five times the output size using the `-sample` function, which has its own built-in resampling filter that’s similar to the nearest-neighbor approach discussed above.
2.  It resizes the image to its final output size using the basic `-resize` filter.
3.  It strips meta data from the image.

This means that if we were resizing an image to be 500 pixels wide, <code>-thumbnail</code> would first resize it to 2,500 pixels wide using <code>-sample</code>; the result might be blocky and pixelated, as we saw in the examples above, but the operation would be fast and would produce a result with a small file size. Then, ImageMagick would resize this image from 2,500 pixels wide to 500 pixels wide using <code>-resize</code>. This smooths out the blockiness, but the file size stays pretty low. Finally, ImageMagick would remove meta data to get an even smaller file.

The second way to choose a resampling filter in ImageMagick is with the <code>-filter</code> setting. Some resizing functions (such as <code>-sample</code>) have a built-in resampling function that’s always used, but others (such as <code>-resize</code>) have defaults that can be overridden with <code>-filter</code>. The <code>-filter</code> setting gets used in <code>-thumbnail</code>’s second step, because that step uses <code>-resize</code>.

I tested 31 different settings for <code>-filter</code> and got the best results with <code>Triangle</code>. The <code>Triangle</code> resampling filter is also known as <strong>bilinear interpolation</strong>, which I discussed above. It determines pixel color by looking at a <strong>support area</strong> of neighboring pixels and produces a weighted average of their colors. I found it best to specify this support area at two pixels using the <code>-define filter:support=2</code> setting.

The third way to choose a resampling filter, the <code>-interpolate</code> setting, is ignored by <code>-thumbnail</code>, so it’s not needed here.

In addition to the settings above, by default ImageMagick also uses something called <a href="https://johncostella.webs.com/magic/">JPEG fancy upsampling</a>, an algorithm that tries to produce better-looking JPEGs. I’ve found that it produces larger files and that the quality difference is negligible, so I recommend turning it off with <code>-define jpeg:fancy-upsampling=off</code>.

### Sharpening

Images pretty often get a little blurry when resized, so programs such as Photoshop will often apply some sharpening afterwards to make the images a little crisper. I recommend using an <strong>unsharp</strong> filter &mdash; which, despite its name, actually does sharpen the image &mdash; with the setting <code>-unsharp 0.25x0.25+8+0.065</code>.

Unsharp filters work by first applying a <a href="https://en.wikipedia.org/wiki/Gaussian_blur">Gaussian blur</a> to the image. The first two values for the unsharp filter are the <strong>radius</strong> and <strong>sigma</strong>, respectively &mdash; in this case, both have a value of <code>0.25</code> pixels. These values are often the same and, combined, tell ImageMagick how much to blur the image. After the blur is applied, the filter compares the blurred version to the original, and in any areas where their brightness differs by more than a given <strong>threshold</strong> (the last value, <code>0.065</code>), a certain <strong>amount</strong> of sharpening is applied (the third value, <code>8</code>). The exact meanings of the threshold and numerical amounts aren’t very important; just remember that a higher threshold value means that sharpening will be applied less often, and a higher numerical amount means that the sharpening will be more intense wherever it is applied.

### Color Reduction

I mentioned that one of the biggest reasons why resized images get bloated is because of all the extra colors in them. So, try to reduce the number of colors &mdash; but not so much that the quality suffers.

One way to reduce colors is with <strong>posterization</strong>, a process in which gradients are reduced to bands of solid color. Posterization reduces colors to a certain number of <strong>color levels</strong> &mdash; that is, the number of colors available in each of the red, green and blue color channels that images use. The total number of colors in the final image will be a combination of the colors in these three channels.

Posterization can drastically reduce file size, but can also drastically change how an image looks. With only a few color levels, it creates an effect like what you might see in <a href="https://www.pinterest.com/pin/445363850621483734/">1970s rock posters</a>, with a few discrete <strong>bands</strong> of color. With many color levels &mdash; for example, <code>136</code>, as I’m suggesting &mdash; you get a smaller file without losing much image quality.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd07f82e-a30d-4e93-a2cf-0c16ea2b7f40/08-owl-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cafb806e-cf0d-41f7-a008-604d297b875d/08-owl-opt-small.jpg" alt="Close up of an owl with reduced colors" /></a><figcaption>Original image. (Image: <a href="https://commons.wikimedia.org/wiki/File:Lesser_Sooty_Owl_at_Bonadio%27s_Mabi_Wildlife_Reserve.jpg">Richard Fisher</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd07f82e-a30d-4e93-a2cf-0c16ea2b7f40/08-owl-opt.jpg">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/242ce817-97a3-48fe-9acd-b1bf97930b01/09-posterization-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca824611-afed-4386-9eca-1df494a3567c/09-posterization-opt-small.jpg" alt="Close up of an owl with reduced colors" /></a><figcaption>Posterization reduces the colors in the image. (Image: <a href="https://commons.wikimedia.org/wiki/File:Lesser_Sooty_Owl_at_Bonadio%27s_Mabi_Wildlife_Reserve.jpg">Richard Fisher</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/242ce817-97a3-48fe-9acd-b1bf97930b01/09-posterization-opt.jpg">View large version</a>)</figcaption></figure>

<strong>Dithering</strong> is a process that is intended to mitigate color banding by adding noise into the color bands to create the illusion that the image has more colors. In theory, dithering seems like a good idea when you posterize; it helps the viewer perceive the result as looking more like the original.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68dd54ca-60cf-4ef7-898b-26d7cbe48ec7/10-dithering-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b3660a1-ef8c-4baa-b2ad-db24e0cdd07b/10-dithering-opt-small.jpg" alt="Two images of an old woman, the second full of image rendering artifacts" /></a><figcaption>Dithering. (Image: <a href="https://commons.wikimedia.org/wiki/File:Lesser_Sooty_Owl_at_Bonadio%27s_Mabi_Wildlife_Reserve.jpg">Richard Fisher</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68dd54ca-60cf-4ef7-898b-26d7cbe48ec7/10-dithering-opt.jpg">View large version</a>)</figcaption></figure>

Unfortunately, ImageMagick has a bug that ruins images with transparency when dithering is used like this. So, it’s best to turn dithering off with <code>-dither None</code>. Luckily, even without dithering, the posterized images still look good.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a892446-da7e-4fd1-81ec-ecdfe8744f9e/11-dithering-bug-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84bf361e-9a4b-42eb-be68-f2d58fe7e385/11-dithering-bug-opt-small.png" alt="Two images of an old woman, the second full of image rendering artifacts" /></a><figcaption>ImageMagick dithering bug. (Image: <a href="https://pixabay.com/en/lady-nurse-spectacled-woman-female-311672/">Nemo</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a892446-da7e-4fd1-81ec-ecdfe8744f9e/11-dithering-bug-opt.png">View large version</a>)</figcaption></figure>

### Color Space

While not strictly a matter of color reduction, setting an image’s <strong>color space</strong> is a related concept. The color space defines what colors are available for an image. The image below shows that the ProPhoto RGB color space contains more colors than the Adobe RGB color space, which in turn contains more colors than the sRGB color space. All of these contain fewer colors than are visible to the human eye.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/738ecc44-26cd-4a0a-b018-670349046bb8/12-colourspaces-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1451ba90-983c-4275-8e18-d18b0aa6bc60/12-colourspaces-op-small.png" alt="Map that compares how much of the color spectrum is covered by different color spaces; sRGB covers the least" /></a><figcaption>Color spaces. (Image: <a href="https://commons.wikimedia.org/wiki/File:Colorspace.png">Cpesacreta</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a892446-da7e-4fd1-81ec-ecdfe8744f9e/11-dithering-bug-opt.png">View large version</a>)</figcaption></figure>

sRGB was created to be the one true king of color spaces on the Internet. It has been endorsed by the W3C and other standards bodies; it is the required color space in the <a href="https://www.w3.org/TR/css3-color/">CSS Color Module Level 3</a> and the <a href="https://www.w3.org/TR/SVG11/single-page.html">SVG specification</a> and is the assumed color space of the <a href="https://developers.google.com/speed/webp/docs/riff_container">WebP</a> specification; and it is explicitly referenced in the <a href="https://www.w3.org/TR/PNG/">PNG specification</a>. It’s also the default color space in Photoshop. In short, sRGB is the color space of choice for the web platform, and, assuming you want your images to render predictably, using it is probably a good idea.

### Quality and Compression

With lossy image formats such as JPEG, <strong>quality</strong> and <strong>compression</strong> go hand in hand: the higher the compression, the lower the quality and the lower the file size. We could drastically reduce file size by setting a high JPEG compression factor, but this would also drastically reduce quality. A balance is needed.

When I was doing my tests, the control images I created with Photoshop had a JPEG quality setting of <code>high</code>, or <code>60</code>. I’ve found that this setting works well for me and strikes the right balance between quality and file size. However, in my ImageMagick settings, I’m recommending <code>-quality 82</code>. Why?

It turns out that JPEG quality scales are not defined in a specification or standard, and they are not uniform across encoders. A quality of <code>60</code> in Photoshop might be the same as a quality of <code>40</code> in one program, quality <code>B+</code> in another and quality <code>fantastico</code> in a third. In my tests, I found that Photoshop’s <code>60</code> is closest to <code>-quality 82</code> in ImageMagick.

For <strong>non-lossy image formats</strong>, such as PNG, quality and compression are not related at all. High compression doesn’t change how an image looks at all and only comes at the expense of processing load (in terms of CPU usage, memory usage and processing time). Assuming that our computers can handle this load, there’s no reason not to max out PNG compression.

PNG compression in ImageMagick can be configured with three settings, <code>-define png:compression-filter</code>, <code>-define png:compression-level</code> and <code>-define png:compression-strategy</code>. <strong><a href="https://www.libpng.org/pub/png/book/chapter09.html">Compression filtering</a></strong> is a pre-compression step that reorganizes the image’s data so that the actual compression is more efficient; I got the best results using adaptive filtering (<code>-define png:compression-filter=5</code>). <strong>Compression level</strong> is the amount of compression that gets applied; I recommend maxing this out to <code>9</code> (<code>-define png:compression-level=9</code>). Finally, the <strong>compression strategy</strong> setting determines the actual algorithm that’s used to compress the files; I got the best result with the default compression strategy (<code>-define png:compression-strategy=1</code>).

### Meta Data

In addition to the actual image data, image files can contain meta data: information about the image, such as when it was created and the device that created it. This extra information could take up space without providing any benefit to our users and should usually be removed. Above, when describing the <code>-thumbnail</code> function that handles the actual resizing of the image, I mentioned that its third step involves stripping meta data. Even though that’s true, <code>-thumbnail</code> doesn’t remove <em>all</em> of the meta data, and there are gains to be had by using <code>-strip</code> and <code>-define png:exclude-chunk=all</code> as well. Neither of these should affect quality at all.

### Progressive Rendering

JPEGs and PNGs can be saved to use either <strong>progressive</strong> or <strong>sequential rendering</strong>. Sequential rendering is usually the default: The image will load pixels row by row from top to bottom. Progressive rendering means the image is delivered and rendered in stages.

For JPEGs, progressive rendering can happen in any number of stages, as determined when the file is saved. The first stage will be a very low-resolution version of the full image; at each subsequent stage, a higher-resolution version is delivered until, in the last stage, the full-quality version is rendered.

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0a23aa8-e08a-44d2-8e59-c703cd485753/13-progressive-jpeg.gif" alt="An owl, rendering at progressively higher quality" /><br>
<figcaption>Progressive JPEG simulation. (Image: <a href="https://commons.wikimedia.org/wiki/File:Lesser_Sooty_Owl_at_Bonadio%27s_Mabi_Wildlife_Reserve.jpg">Richard Fisher</a>)</figcaption></figure>

PNGs use a type of progressive rendering called <a href="https://en.wikipedia.org/wiki/Adam7_algorithm">Adam7 interlacing</a>, in which the pixels of the image are delivered in seven stages based on an 8 × 8 pixel grid.

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ffd5238-4745-4889-af1a-44bcee6e4e8c/14-progressive-png.gif" alt="Pixels being rendered in seven passes" /><br>
<figcaption>Adam7 interlacing. (Image: <a href="https://commons.wikimedia.org/wiki/File:Adam7_passes.gif">CountingPine</a>)</figcaption></figure>

Both types of progressive rendering can be controlled in ImageMagick using the <code>-interlace</code> setting. But should progressive rendering be turned on or not?

For both JPEGs and PNGs, progressive rendering increases the file size, but for a long time <a href="https://blog.patrickmeenan.com/2013/06/progressive-jpegs-ftw.html">conventional wisdom held that it was worth turning on</a> because it delivered a better experience to the user. The idea is that even if the full, perfect image doesn’t load quite as quickly, users would be able to see <em>something</em> earlier, and that something is probably better than nothing.

Last year, though, <a href="https://www.radware.com/">Radware</a> released <a href="https://www.radware.com/neurostrata-fall2014/">research on progressive JPEGs</a> that shows users actually tend to prefer sequential image rendering. This is just one study (and one that hasn’t gone through a formal peer review process), but the results are interesting. Radware’s results, combined with the fact that sequential images have smaller file sizes, lead me to recommend the <code>-interlace none</code> setting in ImageMagick.

### Image Optimization

I mentioned above that I ran tests both with and without image optimization. All of the settings I’ve described so far are what I’d recommend if you’re not optimizing your images. If you can optimize them, though, my recommendations would change slightly: I found that slightly different <code>-unsharp</code> settings work better (<code>-unsharp 0.25x0.08+8.3+0.045</code> versus <code>-unsharp 0.25x0.25+8+0.065</code> without optimization) and that there’s no need to use <code>-strip</code>.

<div class="break-out">

 <pre><code class="language-bash">mogrify -path OUTPUT_PATH -filter Triangle -define filter:support=2 -thumbnail OUTPUT_WIDTH -unsharp 0.25x0.08+8.3+0.045 -dither None -posterize 136 -quality 82 -define jpeg:fancy-upsampling=off -define png:compression-filter=5 -define png:compression-level=9 -define png:compression-strategy=1 -define png:exclude-chunk=all -interlace none -colorspace sRGB INPUT_PATH
</code></pre>
</div>

A lot of different image optimizers are out there. I tested <a href="https://github.com/toy/image_optim">image_optim</a>, <a href="https://github.com/ajslater/picopt">picopt</a> and <a href="https://imageoptim.com/">ImageOptim</a>, all of which run images through a battery of different optimization steps. I tested these tools both individually and in combination, and I found that the best results come from running files through all three, in the order listed above. That said, there are diminishing returns: After the first round of optimization with image_optim, the extra compression that picopt and ImageOptim achieve is quite small. Unless you have a lot of time and processing power, using multiple image optimizers is probably overkill.

## The Results (Or, Is This Even Worth It?)

The settings I’m recommending are, admittedly, complicated, but they are absolutely worthwhile for your users. When I set out to do these tests, I did so hoping that I’d be able to drastically reduce file size without sacrificing image quality. I’m happy to report that, using the settings described above, I was successful.

On average, my recommended settings and optimizations reduced file sizes by 35% compared to Photoshop’s “Save for Web”:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap><caption>Savings compared to Photoshop Creative Cloud</caption>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Condition</th>
      <th>File size: mean</th>
      <th>File size: % difference</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>My settings, with optimization</td>
      <td>218,274 bytes</td>
      <td></td>
    </tr>
    <tr>
      <td>My settings, without optimization</td>
      <td>259,852 bytes</td>
      <td>19.05%</td>
    </tr>
    <tr>
      <td>Photoshop CC, with optimization</td>
      <td>260,305 bytes</td>
      <td>19.28%</td>
    </tr>
    <tr>
      <td>Photoshop CC, without optimization</td>
      <td>299,710 bytes</td>
      <td>35.26%</td>
    </tr>
  </tbody>
</table>

My settings <em>without</em> optimization even beat Photoshop’s output <em>with</em> optimization!

Compared to ImageMagick’s default image resizing, my recommendations resulted in file sizes that were 82% smaller on average:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap><caption>Savings compared to ImageMagick defaults</caption>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Condition</th>
      <th>File size: mean</th>
      <th>File size: % difference</th>
    </tr>
</thead>
<tbody>
  <tr>
    <td>My settings, with optimization</td>
    <td>218,274 bytes</td>
    <td></td>
  </tr>
  <tr>
    <td>My settings, without optimization</td>
    <td>259,852 bytes</td>
    <td>19.05%</td>
  </tr>
  <tr>
    <td><code>-resize</code></td>
    <td>397,588 bytes</td>
    <td>82.15%</td>
  </tr>
</tbody>
</table>

Compared to WordPress’s default image resizing (which uses ImageMagick under the hood), my recommendations resulted in file sizes that were 77% smaller on average:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap><caption>Savings compared to WordPress</caption>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Condition</th>
      <th>File size: mean</th>
      <th>File size: % difference</th>
    </tr>
</thead>
<tbody>
  <tr>
    <td>My settings, with optimization</td>
    <td>218,274 bytes</td>
    <td></td>
  </tr>
  <tr>
    <td>My settings, without optimization</td>
    <td>259,852 bytes</td>
    <td>19.05%</td>
  </tr>
  <tr>
    <td><a href="https://wordpress.org/">WordPress</a>*</td>
    <td>385,795 bytes</td>
    <td>76.75%</td>
  </tr>
  </tbody>
  <tfoot>
  <tr>
  <td colspan="3"><small>* Simulation using ImageMagick with the settings that these CMS’ use by default. The specific settings used can be found in the <a href="https://github.com/nwtn/image-resize-tests/tree/no-optimization/test38-cms-comparison#settings-used-for-this-simulation">GitHub repository for these tests</a>.</small></td>
  </tr>
</tfoot>
</table>

Compared to other CMS’ and tools that use ImageMagick, my recommendations resulted in file sizes that were up to 144% smaller:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap><caption>Savings compared to other tools</caption>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Condition</th>
      <th>File size: mean</th>
      <th>File size: % difference</th>
    </tr>
</thead>
<tbody>
  <tr>
    <td>My settings, with optimization</td>
    <td>218,274 bytes</td>
    <td></td>
  </tr>
  <tr>
    <td>My settings, without optimization</td>
    <td>259,852 bytes</td>
    <td>19.05%</td>
  </tr>
  <tr>
    <td><a href="https://www.codeigniter.com/">CodeIgniter</a>/<a href="https://ellislab.com/expressionengine">ExpressionEngine</a>*</td>
    <td>340,461 bytes</td>
    <td>55.98%</td>
  </tr>
  <tr>
    <td><a href="https://typo3.org/">TYPO3.CMS</a>*</td>
    <td>359,112 bytes</td>
    <td>64.52%</td>
  </tr>
  <tr>
    <td><a href="https://www.drupal.org/">Drupal</a>*</td>
    <td>397,588 bytes</td>
    <td>82.15%</td>
  </tr>
  <tr>
    <td><a href="https://grabaperch.com/">Perch</a>*</td>
    <td>416,790 bytes</td>
    <td>90.95%</td>
  </tr>
  <tr>
    <td><a href="https://buildwithcraft.com/">Craft CMS</a>*</td>
    <td>425,259 bytes</td>
    <td>94.83%</td>
  </tr>
  <tr>
    <td><a href="https://github.com/andismith/grunt-responsive-images">grunt-responsive-images</a></td>
    <td>533,030 bytes</td>
    <td>144.20%</td>
  </tr>
  </tbody>
  <tfoot>
  <tr>
<td colspan="3"><small>* Simulation using ImageMagick with the settings that these CMS’ use by default. The specific settings used can be found in the <a href="https://github.com/nwtn/image-resize-tests/tree/no-optimization/test38-cms-comparison#settings-used-for-this-simulation">GitHub repository for these tests</a>.</small></td>
</tr>
</tfoot>
</table>

And remember, this is all with the images being visually indistinguishable from the Photoshop output, on average.

Using the settings I described above can get you <em>huge</em> file size savings without hurting quality. This can be a huge boon to your website’s performance!

## How To Implement This In Your Projects

I hope the benefits of using this technique are obvious. Luckily for you, the hard part &mdash; figuring all of this out &mdash; is all done. Despite the apparent complexity of the recommended settings, implementing this in your own projects can be fairly quick and easy. Although running this whopper of a command from the terminal every time you want to resize an image may be inconvenient, there are simpler options that require very little muss or fuss.

### bash shell

Most command-line shells allow you to setup aliases and functions for complicated commands. If you use a bash shell, you can add a function to your <code>.bash_aliases</code> (or <code>.bashrc</code>) file that acts as an alias for my recommended command:

<div class="break-out">

 <pre><code class="language-bash">smartresize() {
   mogrify -path $3 -filter Triangle -define filter:support=2 -thumbnail $2 -unsharp 0.25x0.08+8.3+0.045 -dither None -posterize 136 -quality 82 -define jpeg:fancy-upsampling=off -define png:compression-filter=5 -define png:compression-level=9 -define png:compression-strategy=1 -define png:exclude-chunk=all -interlace none -colorspace sRGB $1
}
</code></pre>
</div>

Then, you can call it like this:

<pre><code class="language-bash">smartresize inputfile.png 300 outputdir/</code></pre>

### Node.js

An npm package called, unsurprisingly, <a href="https://www.npmjs.com/package/imagemagick">imagemagick</a> allows you to use ImageMagick via <a href="https://nodejs.org/">Node.js</a>. If you’re using this module, you can add resizing using my recommended settings like this:

<pre><code class="language-javascript">var im = require('imagemagick');

var inputPath = 'path/to/input';
var outputPath = 'path/to/output';
var width = 300; // output width in pixels

var args = [
   inputPath,
   '-filter',
   'Triangle',
   '-define',
   'filter:support=2',
   '-thumbnail',
   width,
   '-unsharp 0.25x0.25+8+0.065',
   '-dither None',
   '-posterize 136',
   '-quality 82',
   '-define jpeg:fancy-upsampling=off',
   '-define png:compression-filter=5',
   '-define png:compression-level=9',
   '-define png:compression-strategy=1',
   '-define png:exclude-chunk=all',
   '-interlace none',
   '-colorspace sRGB',
   '-strip',
   outputPath
];

im.convert(args, function(err, stdout, stderr) {
   // do stuff
});
</code></pre>

### Grunt

If you use <a href="https://gruntjs.com/">Grunt</a> as a task runner, good news: I’ve built a Grunt task named <a href="https://github.com/nwtn/grunt-respimg">grunt-respimg</a> (<a href="https://www.npmjs.com/package/grunt-respimg">npm</a>) that handles everything I’ve described above. You can include it in your projects by running:

<pre><code class="language-bash">npm install grunt-respimg --save-dev</code></pre>

Then, you can run it in your Grunt file like this:

<pre><code class="language-javascript">grunt.initConfig({
  respimg: {
    default: {
      options: {
        widths: [200, 400]
      },
      files: [{
        expand: true,
        cwd: 'src/img/',
        src: ['**.{gif,jpg,png,svg}'],
        dest: 'build/img/'
      }]
    }
  },
});
grunt.loadNpmTasks('grunt-respimg');
</code></pre>

### PHP

<a href="https://php.net/">PHP</a> has ImageMagick integration called <a href="https://php.net/manual/en/book.imagick.php">Imagick</a> that makes it relatively easy to run ImageMagick operations from within your PHP scripts. Unfortunately, Imagick is a bit limited and doesn’t let you do some things that I recommend, like setting a resampling filter to be used with the thumbnail function.

But, again, you’re in luck: I’ve created a composer package called <a href="https://github.com/nwtn/php-respimg">php-respimg</a> (<a href="https://packagist.org/packages/nwtn/php-respimg">packagist</a>) that handles everything described above. You can include it in your projects with <a href="https://getcomposer.org/">Composer</a> by running:

<pre><code class="language-bash">composer require nwtn/php-respimg
</code></pre>

Then, you can resize your images like this:

<pre><code class="language-php">require_once('vendor/autoload.php');
use nwtn\Respimg as Respimg;
$image = new Respimg($input_filename);
$image-&gt;smartResize($output_width, 0, false);
$image-&gt;writeImage($output_filename);
</code></pre>

### Content Management Systems

If you use a CMS, you might want to take advantage of these savings for the thumbnails and other resized images that get generated when users upload images. A few options are available to you.

If your CMS is built on PHP, you could bake the PHP stuff above into a theme or plugin. However, if your PHP-based CMS happens to be WordPress, then there’s no need for you to do that work: This is now integrated into the Responsive Issues Community Group’s plugin <a href="https://wordpress.org/plugins/ricg-responsive-images/">RICG Responsive Images</a> as an experimental feature. After you install the plugin, all you’ll need to do to activate these ImageMagick settings is add the following lines to your <code>functions.php</code> file:

<pre><code class="language-php">function custom_theme_setup() {
   add_theme_support( 'advanced-image-compression' );
}
add_action( 'after_setup_theme', 'custom_theme_setup' );
</code></pre>

If you don’t use WordPress and don’t want to try to hack this into your CMS, most CMS’ include some way to modify image defaults (especially for quality). You might be able to get a lot of these benefits with a few simple changes to your CMS’ configuration. Check out the documentation and see what options are available to you.

## Performance

The settings I’m recommending are obviously far more complex than simply using <code>-resize</code>, and this complexity brings a performance hit with it. Using my recommendations will take longer and use more resources on your computer or server. In my tests, I found that memory and CPU usage peaks were comparable but that my settings took an average of 2.25 times longer to render an image than from just using <code>-resize</code> alone.

## Conclusion

As designers and developers, we have an enormous amount of power to shape how &mdash; and how well &mdash; the web works. One of the biggest impacts we can have is to make our websites more performant, which will <strong>improve our users’ experiences</strong> and even <a href="https://blog.chriszacharias.com/page-weight-matters">make our content available to whole new markets</a>. Cutting image weight is a relatively simple and hugely impactful way to increase performance, and I hope the information outlined above helps you make a difference to your users.

### Links

*   [grunt-respimg](https://github.com/nwtn/grunt-respimg)
*   [php-respimg](https://github.com/nwtn/php-respimg)
*   [RICG Responsive Images](https://wordpress.org/plugins/ricg-responsive-images/) plugin

<em>Thank you to Mat Marquis for reviewing a draft of this article.</em>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Automatically Art-Directed Responsive Images? Here You Go.</span>](https://www.smashingmagazine.com/2016/02/automatically-art-directed-responsive-images-go/)
*   [Leaner Responsive Images With Client Hints](https://www.smashingmagazine.com/2016/01/leaner-responsive-images-client-hints/)
*   [Choosing A Responsive Image Solution](https://www.smashingmagazine.com/2013/07/choosing-a-responsive-image-solution/)
*   [Responsive Image Container: A Way Forward For Responsive Images?](https://www.smashingmagazine.com/2013/09/responsive-image-container/)

{{< signature "da, ml, al" >}}

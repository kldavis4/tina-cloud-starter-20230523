---
title: How To Optimize PNG
slug: clever-png-optimization-techniques
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09d9c613-2d11-4b2f-9653-3ed18df1de18/illucopernicsummarizer.gif
date: 2009-07-15T15:34:01.000Z
author: sergey-chikuyonok
description: >-
  This post describes some **techniques that may help you optimize your
  PNG-images**. These techniques are derived from laborious hours spent on
  studying how exactly the PNG encoder saves data. We'll start with some
  essentials about the PNG format and will then move to advanced optimization
  techniques.
categories:
  - Graphics
  - Design
  - Optimization
  - PNG
---
As a web designer you might be already familiar with the PNG image format which offers a full-featured transparency. It's a lossless, robust, very good replacement of the elder GIF image format. As a Photoshop (or any other image editor) user you might think that there is not that many options for PNG optimization, especially for truecolor PNG's (PNG-24 in Photoshop), which doesn't have any. Some of you may even think that this format is "unoptimizable". Well, in this post we'll try to debunk this myth.

This post describes some <strong>techniques that may help you optimize your PNG-images</strong>. These techniques are derived from laborious hours spent on studying how exactly the PNG encoder saves data. We'll start with some essentials about the PNG format and will then move to advanced optimization techniques.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Clever JPEG Optimization Techniques](https://www.smashingmagazine.com/2009/07/01/clever-jpeg-optimization-techniques/)
*   [How Optimized Are Your Images? Meet ImageOptim-CLI](https://www.smashingmagazine.com/2013/12/imageoptim-cli-batch-compression-tool/)
*   [Efficient Image Resizing With ImageMagick](https://www.smashingmagazine.com/2015/06/efficient-image-resizing-with-imagemagick/)

## <a name="boring"></a>The boring part

Before we dive into image optimization techniques, we have to learn some technical details about the PNG format. Each graphic format has its own advantages and weaknesses; knowing them will allow you to <em>modify original image for better visual quality and compression</em>. This is a key concept behind professional image optimization.

{{% feature-panel %}}

PNG was developed as an <strong>open-source replacement of the proprietary GIF format</strong>. They have some common features (like indexed color palette), but PNG is much better than GIF in every aspect. It introduced some cool features for image packing and compression, but for us – web designers and developers – the most important one is the <em>scanline filtering</em> (also known as 'delta filters').</p>

### Scanline filtering

Here is how it works. For example, we have a 5×5 pixels image with horizontal gradient. Here is a schematic view of this image (each number represents a unique color):

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bf01547-5f18-401d-be17-954ead8891e6/scanline1.png" alt="optimize png" width="455" height="219" />

As you can see, all identical colors spread vertically, not horizontally. Such images will have a very poor compression ratio in GIF, because it compresses colors that spread horizontally. Let's see how this image data <em>can be packed</em> by scanline filtering:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f4badca-f636-4ff8-84dc-e3aafe997444/scanline2.png" alt="optimize png" width="455" height="219" />

Number 2 before each line represents applied filter, which is "Up" in this case. The "Up" filter sends the message to the PNG decoder: “For the current pixel take the value of the above pixel and add it to the current value.” We have 0 value for lines 2—5 because all pixels in each vertical line have the same color. And such data would be compressed better if the image was relatively large. For example, 15 pixels of value 0 can be written as 0(15) and this is much shorter than fifteen 0's—this is how compression works in common.

I wrote "can be packed" because in this ideal test case the "Sub" filter (number 1 before each line) will give much better result:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3002b11-ed97-49c7-9b1c-c88ef5d62baa/scanline3.png" alt="Screenshot" width="455" height="219" />

The filter "Sub" sends the message to the decoder: “Take the value of the left pixel and add it to the current value.” In this case, it’s 1. As you may already have guessed, such data will be compressed very effectively.

Scanline filtering is important for us because we can use them: in particular, we can do some image manipulation to make filtering better. There are five filters: None (no filtering), Sub (subtract the left pixel value from the current value), Up (subtract the above pixel value), Average (subtract the average of the left and the upper pixels) and Paeth (substitute the upper, left or upper left pixel value, named after Alan Paeth).

And here's how these filters affect the image size in comparison with the good ol' GIF:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2daeafb0-ca75-45c7-95cc-ff3b4ac6ba64/gradient.gif" alt="Screenshot" width="100" height="150" />

<em>GIF, 2568 bytes</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/289da723-17ac-4875-befa-14182f55acf1/gradient24.png" alt="Screenshot" width="100" height="150" />

<em>PNG, 372 bytes</em>

As you can see, the <strong>GIF image is 7 times larger than the same PNG-image</strong>.</p>

### Image type

Another important thing to know about PNG is <em>image type</em>, the meta-data stored inside the file. As a Photoshop user, you are familiar with PNG-8 (indexed image) and PNG-24 (truecolor image). As a Fireworks user, you may know PNG-32 (truecolor with transparency), which is quite confusing, because Photoshop's PNG-24 may also store truecolor with transparency. Well, it's worth knowing that these names are not official, and you won't find them in PNG specs. For your convenience we'll use Photoshop's naming convention of PNG image types in this article.

There are <strong>5 available image types in PNG</strong>: Grayscale, Truecolor, Indexed-color, Grayscale with alpha and Truecolor with alpha. There are also two subtypes of indexed-color type (non-official, too): <em>bit transparency</em> (each pixel can be fully transparent or fully opaque) and <em>palette transparency</em> (each pixel can be semi-transparent). In second case each color is stored in palette with its alpha value. Thus, opaque red and 50%-transparent red are two different colors and they take 2 cells inside palette.

The worst thing is that Photoshop can save PNG with only 3 of these types: Indexed-color with bit transparency, Truecolor and Truecolor with transparency. That's why you may find a lot of opinions that Adobe Fireworks is the best tool for PNG optimization. Personally, I don't agree with them: Fireworks doesn't have enough tools for image manipulation, it's only have slightly more options for saving PNG image, but it's a topic for another discussion.

This is where utilities such as <a href="https://optipng.sourceforge.net/">OptiPNG</a> or <a href="https://pmt.sourceforge.net/pngcrush/">pngcrush</a> come in handy. Essentially, these tools do the following:

1.  Pick up the best image type for an image (for example, truecolor can be converted to indexed-color if there aren't too many colors in the image).
2.  Pick up best delta filters.
3.  Pick up the best compression strategy and, optionally, reduce the color depth.

All these operations do not affect image quality at all, but do reduce the file size of the PNG-images, so I highly recommend you to use such tools every time you save a PNG image.

Now enough with the boring part, let's do some magic!

## <a name="posterization"></a>1\. Posterization

This is a well-known method of the truecolor image optimization. Open up the example image in Photoshop, press the <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd97e8e7-8e58-4899-9f64-da21b9446fbb/adj-layer.png" alt="Adjustments layer" width="17" height="12" /> icon in the Layers palette and choose Posterize:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b10f2051-348b-4e61-b6ba-04fd0379197c/posterize-example.jpg" alt="Screenshot" width="565" height="415" />

Pick the smallest possible amount of Levels (usually 40 is enough) and save the image:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e53a149-d00f-407d-a87a-8281e2b3ec5b/original.png)

<em>Original, 84 KB</em>

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/977fe9f1-dc2b-422f-b5af-ac73e29fb786/original-posterized.png)

<em>Posterized, 53 KB</em>

Here is how it works: the posterization simply reduces the amount of colors, converting similar colors to the single one, thus creating posterized regions. This helps to perform a better scanline filtering and achieve a better compression. The downside of this method is color alternation, which is especially visible if you are trying to stitch image with a HTML background:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e85ed36f-8aaf-412a-bbe4-7871ec964894/downside-posterize1.png)

_Original image_

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85a5f7a7-3e5b-4136-8c5c-c6b933e6d62f/downside-posterize2.png)

_Posterized image_

## <a name="dirty-transparency"></a>2\. Dirty Transparency

Take a look at the following images:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90c67c74-06f3-4ea2-b75e-3a86b4e7bf35/dirty-tr-sample1.png)

_75 KB_

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47b69f0d-963f-4671-b64d-a38a866561f9/dirty-tr-sample2.png)

_30 KB_

Both of them were saved in Photoshop without any optimization. Even if you do a per-pixel comparison of these images, you won't notice any difference. But why is the first image 2.5x larger than the second one?

You need a special plugin for Photoshop to see hidden details. It's called <strong>Remove Transparency</strong> and available for free download on the <a href="https://www.thepluginsite.com/products/photowiz/photofreebies/index.htm">PhotoFreebies plugin suite</a>. You have to install it first before proceeding with the next step.

Open both images form the example above in Photoshop and choose <em>Filer > Photo Wiz > Remove Transparency</em>. Now you can see the actual pixel data that was saved in the image:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e90d8a4-7796-48d8-96ca-9cc08f29318c/dirty-tr-sample1-2.jpg)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b216d7cb-e027-4163-92a3-ea337573d7c8/dirty-tr-sample2-2.jpg)

What's happening? How is it possible to reveal the data from the original image from a single-layered PNG image? Well, it's quite simple. Each pixel in the truecolor image with alpha is described by four bytes: RGBA. The last one is Alpha, which controls pixel transparency: the value of 0 means fully transparent pixel and 255 means fully opaque. And this means that every pixel (with any RGB value) can be hidden with just Alpha byte set to 0. But this RGB data still exists and, moreover, it prevents PNG encoder from effectively packing and encoding the data stream. Thus, we have to remove this hidden data (fill it with solid black, for example) before saving the image. Here is a quick method how to do this:

1.  Open the [first image from the example above](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90c67c74-06f3-4ea2-b75e-3a86b4e7bf35/dirty-tr-sample1.png) in Photoshop.

2.  Ctrl+click (or Cmd+click on Mac) on image thumbnail in Layers palette to create a selection, then invert it: _Select > Inverse_.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78193a86-d787-448b-93af-8e7089f42d8f/dirty-qmask1.png)

3.  Switch to Quick Mask mode by pressing Q key:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fa83860-d5c1-4d9b-9198-d82762286727/dirty-qmask2.png)

4.  We have created a mask for a semi-transparent image, but we need to leave fully transparent pixels only. Choose _Image > Adjustments > Threshold_ and move Threshold Level slider to the right, thus leaving fully transparent pixels of the selection:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff6a9cac-b3ae-4aaa-9918-9644e23b7307/dirty-qmask3.png)

5.  Leave Quick Mask mode (press Q key again) and fill the selection with black:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82ba2e0d-8e35-49d2-a7f6-f06fbbe3e2b5/dirty-qmask4.png)

6.  Invert the seleciton again (_Select > Inverse_) and click on the ![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4271fca-09e2-4934-9431-648054e3e130/mask-icon.png) icon in the Layers palette to add mask.

That's it, now you can save this image in PNG-24 and ensure that the 75 KB image is now 30 KB. By the way, all these steps can be easily recorded into Photoshop's Action and reused later with a single keystroke.

You might think about "dirty transparency" as some kind of a bug in image editors: if those image regions can't be seen and take so much space, why can't they be removed automatically before saving? Well, this "bug" can be easily turned into a "feature". Take a look at the following pictures:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb0d19f2-3766-4c70-8807-06c2455bed0a/ex3-1.png)

_5 537 bytes_

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14b6d98c-31f8-46c5-8391-f02d32723fe5/ex3-2.png)

_6 449 bytes_

If you remove transparency from those images, you'll see the following:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a35c239b-c4f7-48ba-83f6-6199d855c0fa/ex3-1-color.png)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30a95855-02a0-4c19-8081-d2beb24b0fa3/ex3-2-color.png)

Despite the fact that the first image contains more complex image data, it's 1Kb lighter than the second one, which was optimized as described above. The explanation of this "abnormal" behavior is simple: image data stream in the first example was effectively packed by delta filters, which works better for smooth color transitions (like gradients).

Tech geeks may look at OptiPNG's output log and ensure that filters were not applied at all for the second image. That's why I highly recommend you to read <a href="#boring">The boring part</a> of this article first before using these techniques: if you don't understand what you're doing, you can make your image even larger.

The ultimate solution to preserve original image data is to create a mask on the image layer in Photoshop (we'll come back to this later):

<div class="image"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d633a929-619a-45ce-a644-51d73a6f9aa5/ex3-mask.png" alt="Screenshot" width="445" height="255" /></div>

As you can see, Dirty transparency is a very powerful yet very delicate technique. You have to know how and why it works before using it. If you are saving PNG-24 images with transparent areas, the first thing you have to do is to check image data in these areas and make the right decision on clearing or leaving them as is.</p>

## <a name="split-by-transparency"></a>3\. Split by transparency

Sometimes you have to save image in the "heavy" PNG-24 because of few semi-transparent pixels. You can save extra Kbs if you split such images in two parts — one with solid pixels, the second one with semi-transparent — and save them in appropriate graphic formats. For example, you can save semi-transparent pixels in PNG-24, and solid pixels in PNG-8 or even JPEG. Here is a quick (and recordable for Actions) solution to do this. For our experiments we'll use this elder Russian iPod ancestor:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ad7c668-2187-4979-a77f-8c61a52e7c43/split-reference.png)

_PNG-24, 62 KB_

1.  Ctrl+click/Cmd+click on image thumbnail in Layers palette to create a selection:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d6c970b-8d21-4961-9f76-3a610efc012c/split1.png)

2.  Go to Channels palette and create new channel from selection:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d1520e3-47c1-4d6e-8589-69bdb097f629/split2.png)

3.  Remove selection (Ctrl+D or Cmd+D), select the newly created channel and run Threshold (_Image > Adjustments > Threshold_). Move the slider to the very right:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e053a58c-fc5f-430d-bb67-af0f7d9ce185/split3.png)

4.  We’ve made a mask for selecting dead solid pixels. Now we have to split original layer by this mask. Ctrl+click/Cmd+click on Alpha 1 channel, go to Layers palette, select the original layer and run _Layer > New > Layer via Cut_. As a result, there are two layers with separated solid and semi-transparent pixels.

Now you need to save those two images in separate files: solid pixels in PNG-8, semi-transparent ones in PNG-24. You can apply <a href="#posterization">Posterization</a> technique on semi-transparent pixels layer to make image file even smaller.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c253963e-48fd-4579-a12b-42b4e7c8a9cb/split4-1.png)

_PNG-8 128 colors + dithering 17 KB_

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccd21f0d-10d2-4f0e-be20-e38f79dfde69/split4-2.png)

_PNG-24 posterization 35 6 KB_

And here is the result for comparison:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ad7c668-2187-4979-a77f-8c61a52e7c43/split-reference.png)

_Before 63 KB_

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c253963e-48fd-4579-a12b-42b4e7c8a9cb/split4-1.png)

_After 23 KB_

This method has an obvious drawback: you get two images instead of one, which may be not so convenient to use (for instance, when making a product catalog in the CMS).</p>

## <a name="influence-mask"></a>4\. Influence masks

Actually, is is not a PNG-specific optimization technique, but demonstration of rarely-used Save for Web properties: Color reduction influence mask and Dithering influence mask.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71f9d07b-fbef-4e93-b73e-2b4f47035872/save-for-web.png)

Sadly, these properties were removed in Photoshop CS4, so you can try this optimization approach only in the pre-CS4 versions (I'm using CS3).

To understand how influence masks works, let's open this <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2038df7b-5cd9-4674-8da7-f05ba664b012/demo.png">demo image</a> in PS and save it in PNG-8 with the following settings: <em>Color reduction: Adaptive, Dither: No dithering, Colors: 256</em>.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38a8b68c-f846-4c30-aa29-ce67c6c67709/step2.png)

_42 KB_

The first thing I've noticed about this image is a very fuzzy pendulum. It is a very bright spot on the image and it attracts way too much attention. Let's try to smooth pendulum's color transitions by setting dithering to 100%:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38a8b68c-f846-4c30-aa29-ce67c6c67709/step2.png)

_46 KB_

The pendulum looks better now, but we got another problems: image size increased by 4 KB and solid-color background became very noisy:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a8b6321-e848-4713-bf4a-8d18d39c2d30/step2-noise.png)

We can try to get rid of this noise by lowering dithering value, but the image quality may also be reduced.

Based on these problems, let's try to do the incredible: <em>increase image quality by lowering the number of colors and image size</em>. Influence masks will help us.

Let's start with the color. Go to Channels palette, create a new channel and name it <em>color</em>. We've already determined that the pendulum is our top priority region to improve image quality, so we need to draw a white circle right on its place (you can enable RGB channel for better precision).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7190b67f-08c8-4741-b0e4-ee08b3d993d2/step3.jpg" alt="Screenshot" width="706" height="533" />

Go to Save for Web dialog and set the following properties: <em>Color reduction: Adaptive, Dither: No, Colors: 128</em> (as you can see, we reduced number of colors from 256 to 128). Now we have to select an influence mask: click on the <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edfea438-4b7e-46af-87cc-386e1ac74eae/mask-icon.png" alt="Screenshot" width="12" height="12" /> near Color reduction list and select the <em>color</em> channel from drop-down list: Now our image looks as follows:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88bc1176-b60b-4331-a581-21409623f720/step4.png" alt="Screenshot" width="330" height="533" />

You can see the <strong>influence mask in action</strong>: the pendulum looks perfect, but the other parts of image look really bad. By setting influence mask, we said to Photoshop: "Look, mate, the pendulum is very important part of image so try to preserve as much colors in this area as possible". Influence mask works exactly the same as regular transparency mask: white color means highest priority in corresponding image region, black color means lowest priority. All intermediate shades of gray affect on image proportionally.

The pendulum now takes the highest color priority, so we have to lower the intensity of white circle to leave more colors for other areas. Close Save for Web dialog, go to Channels palette, select <em>color</em> channel and open Levels dialog (<em>Image > Adjustments > Levels</em>). Set the maximum output level to 50 to lower the white color intensity:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac4e1004-d68e-4653-9434-cfcfb3ca4d05/step5.png" alt="Screenshot" width="660" height="618" />

Try to save for Web again with the same properties:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11fd95d2-1dec-4651-9428-684a9e84663d/step6.png)

Looks better now, but now we've got problems in other image areas:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8607dba-72a5-4837-be47-6de16bd7a00f/step7.png)

I think you already understand how influence masks works: you provide Photoshop with some clues about important image areas with different shades of gray. With trials and errors I've got the following color mask (you can copy it and apply to the image):

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2103619f-5d8c-41ee-9eec-58d949c72638/step8.png)

Dithering influence mask works exactly the same, but instead of colors, it affects the dithering amount of different image areas. <strong>Lighter color means more dithering</strong>. This is a very useful feature, because dithering creates irregular pixel patterns which hinders the PNG compressor to use delta filters. You can determine the exact areas where dithering must be applied while leaving other areas intact, thus gaining better compression of image data.

My dithering channel looks like this:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9423196-91a5-4dda-9d4c-0cd118a5dd0c/step9.png)

Applying both color and dithering influence channels with the same optimization settings (Adaptive, 128 colors):

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64f3f7e3-d64c-4592-8930-7aed8cd53081/step10.png)

Pretty good for 128 colors, isn't it? Let's do some finishing touches: set colors to 180 and max dithering to 80%. And here is our final result compared to original, non-optimized version:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38a8b68c-f846-4c30-aa29-ce67c6c67709/step2.png)

_256 colors, no dithering, non-optimized 42 KB_

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9322bfa1-cd84-4467-ba3f-6d99f111b631/result.png)

_180 colors, optimized 34 KB_

## <a name="grayscale"></a>Grayscale

Photoshop can't save grayscale PNGs, so you would have to use OptiPNG after saving black-and-white images, like this:

<pre class="js">optipng -o5 bw-image.png</pre>

Grayscale images takes much less space than RGBs, because each pixel described with only one byte, not three:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4711f417-9ef0-4269-bafd-2b078e5907e6/grayscale-ps.png" width="104" height="96" /><br><em>PNG-24 (Photoshop → true-color), 8167 bytes.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad3de056-16ed-4716-ab81-20876a09d2a8/grayscale-opti.png" width="104" height="96" /><br><em>PNG-24 (Photoshop + OptiPNG → grayscale), 6132 bytes</em>

Setting the Grayscale color mode (Image → Mode → Grayscale) for images prior to saving them in PNG is very important, especially for semi-transparent images (see <a href="https://www.smashingmagazine.com/2009/07/15/clever-png-optimization-techniques/#dirty-transparency">Dirty transparency</a> method for more information).</p>

## <a name="less-colors"></a>Fewer Colors

This is an alternative to the <a href="https://www.smashingmagazine.com/2009/07/15/clever-png-optimization-techniques/#posterization">Posterization</a> method of reducing colors in an image. Posterization can dramatically change the colors in your image, which is unacceptable if you have to blend the image into the background of your website. This method gives you more control over color but is limited to 256 colors.

The method is basically to extract image data from the semi-transparent image (i.e. remove transparency), convert it to an indexed color and apply the original mask. Reducing the amount of colors will make image data stream packing by the PNG compressor more effective. Let's see how it works.

1. Open the <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ad7c668-2187-4979-a77f-8c61a52e7c43/split-reference.png">original image</a> in Photoshop and duplicate it (Image → Duplicate).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ad7c668-2187-4979-a77f-8c61a52e7c43/split-reference.png" width="144" height="287" /><br><em>63 KB</em>

2. Remove transparency from the duplicated image (Filter → Photo Wiz → Remove Transparency):

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af1126b3-8495-4a67-93b9-889ca85cdc99/step1.png" width="144" height="287" />

3. Set the image mode to Indexed Color (Image → Mode → Indexed Color). In the new dialog window, enter the following settings:

*   Colors: 190,
*   Dither: Diffusion,
*   Amount: 80%.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3a9838a-30b2-4362-8bb6-668eead3b6e3/step2.png" width="144" height="287" />

4. Set the image mode back to RGB and copy the image layer to the original file. Align the copied layer with the referenced one and apply its mask. Now save it to PNG-24:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cb42659-bc2d-4b95-8ee1-3118214c1444/step3.png" width="144" height="287" /><br><em>51 KB</em>

As you can see, these easy steps have saved us 11 KB of the original image without any noticeable effect on image quality. But this method has another advantage: running OptiPNG on these images often saves even more bytes. In this example, the image's size was reduced by 36%, from 51 KB to 33 KB. Instead of converting the image to Indexed Color mode, you can save it for the Web and apply the <a href="https://www.smashingmagazine.com/2009/07/15/clever-png-optimization-techniques/#influence-mask">Influence mask</a> to save extra bytes.

Please note that this method is not the same as PNG-8 with palette transparency in Fireworks. In most cases <em>fewer colors</em> will give you more than 256 colors, so you will have to save the image in PNG-24, not PNG-8. Remember, solid red and 50%-transparent red are two different colors.</p>

## <a name="lowering-details"></a>Reducing Detail

This technique is useful for optimizing shadows, reflections, glows, etc. The idea is to reduce detail in areas of the image that are barely visible. As you will recall from the <a href="https://www.smashingmagazine.com/2009/07/15/clever-png-optimization-techniques/#dirty-transparency">Dirty transparency</a> method, each pixel of a true-color image with transparency is described in four bytes: RGBA. The last one controls pixel transparency. For pixels whose Alpha value is too low (i.e. pixels that are barely visible), you can replace the RGB data for better image compression. Let's try that.

1. Open <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ad7c668-2187-4979-a77f-8c61a52e7c43/split-reference.png">iPod retro</a> in Photoshop, again.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ad7c668-2187-4979-a77f-8c61a52e7c43/split-reference.png" width="144" height="287" /><br><em>63 KB</em>

2. As you can see, the radio has a reflection below it, which is a good candidate for optimization. Ctrl + click or ⌘ + click on the image thumbnail in the Layers palette to create a selection. Go to the Channels palette and create a new channel from the selection:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ea36c7d-be02-4d89-9b3a-6fedcee219f8/mask.png" width="144" height="287" />

*   3\. We have to localize only those pixels that are barely visible. Invert the channel (Image → Adjustments → Invert) and open the Threshold dialog (Image → Adjustments → Invert). Setting the Threshold Level to 170 is good enough:

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8413492b-7ada-4990-874c-72591b046b8e/threshold.png)

4\. We've got the mask that includes barely visible pixels only. Ctrl + click or ⌘ + click on the channel in the palette to create a selection. Go back to the Layers palette, select the image layer and open Filter → Noise → Median. This filter will smooth out pixels in the selection, making them more conducive to compression. Set the Radius value to 5:

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/278c5517-f690-434b-b264-869f594debd3/median.png)

Now save this image "for the Web" in PNG-24 and see how its size has been reduced from 63 KB to 59 KB. You can vary the threshold level and median radius to compress more or preserve more details.

## <a name="tips"></a>More Tips For PNG Use And Optimization

1. Each optimization must begin with a thorough image analysis. Choose the best technique for each image or combine techniques to achieve better results.

2. Be creative. Use these techniques as a starting point for your own methods customized to your particular images.

3. Many people think that PNG-8 is always better than PNG-24 for low-color images. It's not. In some cases, PNG-24 may give you better results:

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c742ed30-1539-4bc5-9518-be16dc535edd/ex1-png8.png)

_PNG-8, 833 bytes_

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1880de43-3df1-4e80-b076-d0b1c1717047/ex1-png24.png)

_PNG-24, 369 bytes_

In this example, there is an overhead in PNG-8: 3 bytes were used to describe the pixels in the color palette, and 1 byte to describe the pixel color in the image data stream, while PNG-24 took up only 3 bytes for each pixel. So, if you're saving low-color images in PNG _without transparency_, test whether PNG-8 or PNG-24 gives you the smaller file.

If you are using an older version of Photoshop (prior CS3), you may find that PNG images in the image editor look different from ones in a Web browser. This is because of the gAMA chunk that is saved in the PNG file, which controls image gamma. You can safely remove it with tools such as [TweakPNG](https://entropymine.com/jason/tweakpng/) (Windows only) or [smush.it](https://smush.it).

A "special" PNG image type allows you to save a semi-transparent image as an indexed-color PNG-8\. This image type isn't available in Photoshop (Fireworks has it), but you can prepare the image in Photoshop and then convert it with OptiPNG. OptiPNG will convert truecolor images to 8-bit palette by default if your image contains less than 256 colors. To do this, you can apply “Less colors” and “Lowering details” techniques and “guess” number of colors.

But it may be very time consuming. There’s a tool called [PNGNQ](https://pngnq.sourceforge.net/ ) which can convert truecolor image to 256 palette, but you won’t have enough control over resulting image. You will have to reduce the total amount of different colors, including semi-transparent ones, to 256 or fewer. This format is "special" because of how it displays in IE6:

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6128f07-6f5b-4906-bb8d-da28b8cef6f6/ex2-1.png)

_IE6_

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/335c0017-5d00-4049-82ae-fcd76ecb2b3a/ex2-2.png)

_Other browsers_

As you can see, IE6 displays only the opaque pixels. The good thing is that you can include such images with the regular <code>&lt;img&gt;</code> tag or as background images (i.e. without using the resource-greedy AlphaImageLoader CSS filter), making for graceful degradation.

Don't use the "Save As" dialog to save PNG images for the Web; use the "Save for Web" dialog instead. By default, Photoshop saves an image preview as additional info in the file, making the file a few times larger than it needs to be.

## <a name="screencast"></a>PNG Optimization In Real Life

A screencast demonstrating how most of these techniques work in real life:<iframe loading="lazy" src="https://player.vimeo.com/video/5685903" width="640" height="400" frameborder="0" webkitallowfullscreen="" mozallowfullscreen="" allowfullscreen=""></iframe>

[Advanced PNG Optimization](https://vimeo.com/5685903) from [Sergey Chikuyonok](https://vimeo.com/user2060676) on [Vimeo](https://vimeo.com).

And here is the [result](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24cbc99c-d082-4559-a660-2d619f01312e/index.html). You can also download [source PSD](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7970610b-4d6d-414a-932c-b015904d80c1/clock.psd) to try it yourself.

_(al)_
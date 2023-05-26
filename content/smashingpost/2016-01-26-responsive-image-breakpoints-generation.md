---
title: 'Responsive Image Breakpoints Generator, A New Open Source Tool'
slug: responsive-image-breakpoints-generation
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77fbe1be-c2e5-42da-9757-753266209a9b/11-aspect-ratio-opt.jpg
date: 2016-01-26T18:35:12.000Z
author: nadavsoferman
summary: >-
  This article introduces a new free open source web tool that will allow you to generate breakpoints for your images interactively: the Responsive Breakpoints Generator.
description: >-
  This article introduces a new free open source web tool that will allow you to generate breakpoints for your images interactively: the Responsive Breakpoints Generator.
categories:
  - Coding
  - Techniques
  - Responsive Design
  - Responsive Images
---

Responsive websites, even the most modern ones, often struggle with **selecting image resolutions that best match the various user devices**. They compromise on either the image dimensions or the number of images. We can solve these issues and start calculating image breakpoints more mathematically, rather than haphazardly.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf5eade6-5d54-46b4-9060-aff97e797226/08-responsive-breakpoints-opt-preview.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf5eade6-5d54-46b4-9060-aff97e797226/08-responsive-breakpoints-opt-preview.png" width="500" height="500" alt="responsive image generator logo"></a><figcaption> "Responsive Breakpoints, an open source tool for responsive images." /></figcaption></figure>

The lives of web developers aren’t getting any simpler as the number of different devices and potential screen resolutions increase. The high&ndash;resolution arms race seems to be never&ndash;ending as vendors try to top one another with innovations in laptop and mobile device screens. New devices such as TVs and smartwatches are entering the market, making the race even more complex.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6a7987a-0087-4f2e-ae0c-feccfa2b9d0f/01-responsive-image-breakpoints-generator-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a22e1ecb-cbb1-4677-b707-650dcf8cd346/01-responsive-image-breakpoints-generator-opt-preview.jpg" width="800" height="561" alt="Responsive Image Breakpoints Generator Preview of 5 image sizes" /><a><figcaption>Responsive Image Breakpoints Generator Preview (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6a7987a-0087-4f2e-ae0c-feccfa2b9d0f/01-responsive-image-breakpoints-generator-opt.jpg">Large preview</a>)</figcaption></figure>

To support the wide range of resolutions and devices, a website’s markup must adapt itself to look perfect on all the different devices and in various resolutions, pixel densities and orientations. **Managing, manipulating and delivering media** &mdash; specifically images &mdash; is one of the main challenges developers face when building responsive websites.

Implementing a responsive design means building your website where slightly different variants of images will be displayed at various dimensions to save bandwidth and optimize image deliery. While there are several responsive frameworks and responsive image solutions available, they often lack a response to the common need of deciding which image resolutions to select and how many different image versions  &mdash; [responsive image breakpoints](https://blog.cloudfour.com/how-do-you-pick-responsive-images-breakpoints/)  &mdash; to include in your responsive website.

In this article I want to further describe the responsive breakpoints challenge, analyze the mistakes currently being made, and suggest **a solution to intelligently find optimal breakpoints for each specific image**. This article introduces a new free open source web tool that will allow you to generate breakpoints for your images interactively: the [Responsive Breakpoints Generator](https://www.responsivebreakpoints.com/).

{{% feature-panel %}}

## Common Mistakes

Many modern websites are responsive. This means that an image adjusts itself to be displayed in various dimensions. Usually there are different image width limits for each display resolution and each device pixel density  &mdash; a large widescreen image isn’t very helpful on a small screen, and a small image will not look crisp on widescreen displays. In addition, many responsive layouts involve [art direction](https://blog.cloudfour.com/responsive-images-101-definitions/#artdirection), which means that images are not only scaled down, but are also cropped or styled differently for each device, based on its resolution or the browser’s window size.

It seems that most websites still solve this issue in a non&ndash;optimal way, either delivering the same high&ndash;resolution image to all devices or creating too many different versions for each original image.

### Mistake #1: Delivering The Highest Image Resolution To All Users

Website owners want their site to look perfect on modern high&ndash;resolution devices. Often developers deliver the same hi&ndash;res version of each image to everyone: all device resolutions, browser window dimensions and device pixel ratios (DPR). Using this approach, the websites depend on browser&ndash;side scaling to fit the images in their responsive layouts.

The websites look great, especially on hi&ndash;res displays with high pixel density. However, the same large image files are delivered to devices with much smaller resolutions, resulting in the **unnecessary delivery of huge files**, which means slower page load times, a negative impact on the user’s experience, and a waste of money on image delivery bandwidth.

For example, take a look at the website for Mango, a popular fashion brand. The following screenshots show a page displayed in a regular laptop’s browser and in standard smartphone resolution.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7216c06-4ee2-4687-b9c6-54fdb1852163/02-mango-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/115f75c7-8254-4b66-bd90-d28cac7c7b7b/02-mango-opt-preview.jpg" width="800" height="301" alt="Mango’s Responsive Website (Desktop left, Mobile right)" /></a><figcaption>Mango’s Responsive Website (Desktop left, Mobile right). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7216c06-4ee2-4687-b9c6-54fdb1852163/02-mango-opt.jpg">Large preview</a>)</figcaption></figure>

While the responsive site looks fine both on desktop and mobile, there’s a significant bandwidth waste behind the scenes that also affects the website visitor by slowing down the image load time.

The web page image above is delivered in its highest resolution of 1,934&times;2,048 pixels to all devices. The actual dimensions available in the desktop view above are 700&times;442, while the mobile view allows dimensions of 200&times;213 pixels only. This means that a huge 1,934px&ndash;wide image is delivered to much smaller displays. This hi&ndash;res image weighs 766KB. If you scale it down to exactly 700px wide for the desktop (DPR 1.0), this image would only weigh 119KB, an **84% saving in file size**.

If you scale the image down even further to exactly 200px wide (required by the smaller mobile device resolution), the same image weighs only 14KB, **reducing file size by 98%**, significantly speeding page load time and dramatically saving bandwidth, especially when there are multiple images on each web page.

Another example is, well, Smashing Magazine. Take a look at the two screenshots below of a responsive web page on Smashing’s website, first in a laptop display and second in a mobile device:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7b8666e-4f28-43d1-9a62-2d88a69dfc52/04-smashing-magazine-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bb0e7c0-84b3-40c2-951a-8f905b2276cc/04-smashing-magazine-opt-preview.jpg" width="800" height="602" alt="Smashing Magazine’s Responsive Website (Desktop left, Mobile right)" /></a><figcaption>Smashing Magazine’s Responsive Website (Desktop left, Mobile right). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7b8666e-4f28-43d1-9a62-2d88a69dfc52/04-smashing-magazine-opt.jpg">Large preview</a>)</figcaption></figure>

The same original image of 500&times;750 is delivered to all the different device resolutions and browser dimensions. The original image weighs 92.4KB. We can easily decrease file size by reducing the JPEG quality to 80% and further optimizing the image to get a file size of only 66.8KB. But even then, the same image is delivered when the available dimensions are only 356&times;534 pixels. For the smaller dimensions we could have scaled down the image to exactly 356px wide, to get an optimized JPEG file of 36.2KB, **saving 46% of the file size**, reducing the bandwidth involved and improving user experience.

### Mistake #2: &mdash; Creating Too Many Different Image Versions

Web developers who want to better match the available display resolutions with the delivered images may create multiple versions for each image. There are frameworks and cloud services (shameless plug: such as [Cloudinary](https://cloudinary.com/)) that simplify this process by **dynamically scaling down images for all the different resolutions**. This approach ensures that the correct images are delivered to the different devices and displays. The visual quality is great, the user experience is better and no bandwidth waste is involved.

However, matching image dimensions to display resolutions means that developers might need to create dozens, or even hundreds, of **different versions for each image**. Furthermore, if the responsive design of the website involves art direction aspects, images are displayed in different aspect ratios and styles, and you need to create many different scaled down versions for each one.

Creating so many different images is quite costly: increased image processing CPU time, larger storage space required, and greater image management complexity and costs.

In addition, having too many different image versions significantly reduces the chances of a CDN cache hit. If a user gets tailored image dimensions from your servers, they might be the first user to request this specific image from your CDN layer. An increase in cache misses might mean a negative impact on user experience and an increase in traffic to your origin image servers.

{{% ad-panel-leaderboard %}}

## The Breakpoints Selection Challenge

To avoid making these mistakes, we’ll need to understand the **trade&ndash;off** between the number of different images, the visual quality and the bandwidth involved. The challenge is to find the best breakpoints for your images.

If scaling down images by a certain level doesn’t significantly save enough bandwidth, you can deliver bigger images to your users and let the browser handle resizing. On the other hand, if a small dimension reduction significantly reduces the file size of the image, you should definitely create another scaled down image version.

The **file size reduction when scaling down images varies for different images**. It depends on the specific content of your images, which has a different sensitivity to the compression algorithms of JPEG, opt&ndash;png, WebP and other image formats. For some images, a small scale&ndash;down saves significant file size, while for other images even a more prominent scale&ndash;down will not significantly affect it. Therefore, you want to define the file size step where it is worth creating another scaled down image version. Jason Grigsby of [Cloud Four](https://cloudfour.com/) called this file size step **performance budget** in his [article about image breakpoints](https://blog.cloudfour.com/responsive-images-101-part-9-image-breakpoints/).

What Jason showed, and what was verified by Cloudinary’s analysis, was that different images require a different number of versions to balance the bandwidth reduction trade&ndash;off, according to your performance budget.

Consider the following JPEG image:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/889d9e36-5740-4792-bf0e-6f4cc7d775bb/06-responsive-image-example-woman-0-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/889d9e36-5740-4792-bf0e-6f4cc7d775bb/06-responsive-image-example-woman-0-opt.jpg" width="436" height="290" alt="Responsive image of a business woman as an exemple" /></a></figure>

Assume you need to display this image in your responsive website at various width dimensions between 200 and 1,000 pixels. Define the file size step (performance budget) to be about 20KB. As the table below shows, you only need to create and deliver five different versions of this image to all the different devices and browsers.

<table class="tablesaw break-out">
<thead>
<tr>
<th>No.</th>
<th>Width</th>
<th>Height</th>
<th>File size</th>
<th>Image</th>
</tr>
</thead>
<tbody>
<tr>
   <td>1</td>
   <td>200</td>
   <td>133</td>
   <td>6.9 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/600175d1-fc46-46df-b252-255827080bbd/06-responsive-image-example-woman-1-opt.jpg">View image</a></td>
</tr>
<tr>
   <td>2</td>
   <td>477</td>
   <td>318</td>
   <td>27.2 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b067bd2-6ddd-4178-9639-c364a05dcdef/06-responsive-image-example-woman-2-opt.jpg">View image</a></td>
</tr>
<tr>
   <td>3</td>
   <td>681</td>
   <td>454</td>
   <td>48.0 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c379cc37-5dd7-444e-b311-ed63cc782089/06-responsive-image-example-woman-3-opt.jpg">View image</a></td>
</tr>
<tr>
   <td>4</td>
   <td>847</td>
   <td>565</td>
   <td>67.6 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea432e84-61d7-40a6-92c4-2af7865d7a58/06-responsive-image-example-woman-4-opt.jpg">View image</a></td>
</tr>
<tr>
   <td>5</td>
   <td>1,000</td>
   <td>667</td>
   <td>86.9 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28ecb204-7259-4762-96b2-89482ee43fde/06-responsive-image-example-woman-5-opt.jpg">View image</a></td>
</tr>
</tbody>
</table>

Now let’s take another JPEG photo:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2f40514-758b-491b-98d7-8c947e729080/07-responsive-image-example-castle-0-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2f40514-758b-491b-98d7-8c947e729080/07-responsive-image-example-castle-0-opt.jpg" width="500" height="333" alt="07-responsive-image-example-castle-0-opt" /></a></figure>

Trying to find the best breakpoints for this image using the same settings of 200 to 1,000 pixels wide and about 20KB file size steps, results in this image needing nine different versions as the table below shows.

<table class="tablesaw break-out">
<thead>
<tr>
<th>No.</th>
<th>Width</th>
<th>Height</th>
<th>File size</th>
<th>Image</th>
</tr>
</thead>
<tbody>
<tr>
   <td>1</td>
   <td>200</td>
   <td>133</td>
   <td>8.7 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90983300-c3f2-4307-a4ab-ba012d0cd7e7/07-responsive-image-example-castle-1-opt.jpg">View image</a></td>
</tr>
<tr>
   <td>2</td>
   <td>380</td>
   <td>253</td>
   <td>27.8 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13d091a6-7c4e-4a8b-b7c4-43ccbf0b0a7a/07-responsive-image-example-castle-2-opt.jpg">View image</a></td>
</tr>
<tr>
   <td>3</td>
   <td>514</td>
   <td>343</td>
   <td>48.5 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6df1a0e1-f32c-4b13-bbd6-3c378f43a693/07-responsive-image-example-castle-3-opt.jpg">View image</a></td>
</tr>
<tr>
   <td>4</td>
   <td>619</td>
   <td>413</td>
   <td>68.3 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a101508b-dd60-41da-beed-43250832f382/07-responsive-image-example-castle-4-opt.jpg">View image</a></td>
</tr>
<tr>
   <td>5</td>
   <td>711</td>
   <td>474</td>
   <td>87.7 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/731ef198-7cbc-43bf-b69e-d90314e74a8d/07-responsive-image-example-castle-5-opt.jpg">View image</a></td>
</tr>
<tr>
   <td>6</td>
   <td>804</td>
   <td>536</td>
   <td>108.5 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfa1c27e-ea70-4a41-a508-24852e3e91ef/07-responsive-image-example-castle-6-opt.jpg">View image</a></td>
</tr>
<tr>
   <td>7</td>
   <td>883</td>
   <td>589</td>
   <td>129.3 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7562f3e8-c1ef-44b1-9496-bf2ef86ab64c/07-responsive-image-example-castle-7-opt.jpg">View image</a></td>
</tr>
<tr>
   <td>8</td>
   <td>957</td>
   <td>638</td>
   <td>148.2 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a164e818-06fb-45cd-83f1-367e04229cc6/07-responsive-image-example-castle-8-opt.jpg">View image</a></td>
</tr>
<tr>
   <td>9</td>
   <td>1,000</td>
   <td>667</td>
   <td>160.7 KB</td>
   <td><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4f4ecde-e04c-4cb5-947c-821aeb55b96d/07-responsive-image-example-castle-9-opt.jpg">View image</a></td>
</tr>
</tbody>
</table>

As shown above, the number of versions required for one image is **almost half of the number** required for another one. The difference might be even more dramatic for other kinds of photos. If you multiply this difference by millions of user uploaded images, the result is huge savings in storage, image processing costs and image management complexity, while still delivering the best&ndash;looking images and preserving the user experience.

## A Solution: The Responsive Breakpoints Generator

To perfectly balance the number of image versions for your responsive website, we need to find the correct breakpoints according to the **file size step** (performance budget) that you define. How can you do that? You can generate images for all possible width values and select only the ones that reflect a significant enough file size reduction. However, this is inefficient and can be expensive.

We’ve come up with a new solution for generating responsive image breakpoints. Analyzing the behavior of the compression mechanisms for various image formats (mainly JPEG, opt&ndash;png and WebP), we created **algorithms to efficiently and intelligently find image breakpoints** that match dimensions and file size saving requirements.

This solution is a new free public web tool called the [Responsive Image Breakpoints Generator](https://www.responsivebreakpoints.com/). I believe you will enjoy trying it out (duh!).

<figure><a href="https://www.responsivebreakpoints.com"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf5eade6-5d54-46b4-9060-aff97e797226/08-responsive-breakpoints-opt-preview.png" width="500" height="500" alt="Logo of Responsive Breakpoints, an open source tool for responsive images." /></a><figcaption><a href="https://www.responsivebreakpoints.com/">Responsive Breakpoints</a>, an open source tool for responsive images.</figcaption></figure>

The tool allows you to upload your images and define settings to **find matching image dimensions and breakpoints** that fit your design requirements. As you can see in the screenshot below, you can define the required **image width range**, the **file size step** in kilobytes and a safety limit of the **maximum number of images** you allow. In addition, you can request that the results include double resolution images for DPR 2.0 displays (e.g. Retina display).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6fa2936-ee3f-4fd5-b955-35c8eda3de89/09-responsive-breakpoints-settings-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84767f3c-268b-44d1-a28e-afc4752871d1/09-responsive-breakpoints-settings-opt-preview.png" width="800" height="740" alt="Generator settings including Resolution, Size step, Maximum images, Retina resolution and Aspect ratio" /></a><figcaption>Generator settings. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6fa2936-ee3f-4fd5-b955-35c8eda3de89/09-responsive-breakpoints-settings-opt.png">Large preview</a>)</figcaption></figure>

When you upload an image, the breakpoints are generated according to your settings and are performed automatically in the cloud. The generated breakpoints are displayed in a summary table and are also illustrated on your uploaded image. You can also download all scaled down and optimized images that match the generated breakpoints.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bfd0679-334e-49a3-973c-241f02f2ac4f/10-aspect-ratio-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc1381eb-6407-4a9f-b538-afd2d55927e1/10-aspect-ratio-opt-preview.jpg" width="800" height="565" alt="Screen showing the result of generated images" /></a><figcaption>Generated images. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bfd0679-334e-49a3-973c-241f02f2ac4f/10-aspect-ratio-opt.jpg">Large preview</a>)</figcaption></figure>

The generator tool **generates HTML markup** that you can copy and paste into your code. The [`srcset` attribute of the `img` tag](https://cloudinary.com/blog/responsive_images_with_srcset_sizes_and_cloudinary) is set to list the image versions and width values according to the smartly selected breakpoints. Modern browsers that process `img` tag will then know how to select the correct image version according to the available space of the image in your responsive web layout. You can also use the tool to create and download a ZIP file of all image files specified in the source set.

<pre><code class="language-markup"> &lt;img sizes="(max-width: 1000px) 100vw, 1000px"
      srcset="dog_c_scale,w_200-opt.jpg 200w,
              dog_c_scale,w_508-opt.jpg 508w,
              dog_c_scale,w_721-opt.jpg 721w,
              dog_c_scale,w_901-opt.jpg 901w,
              dog_c_scale,w_1000-opt.jpg 1000w"
      src="dog_c_scale,w_1000-opt.jpg" alt="A nice dog"&gt;
</code></pre>

As mentioned earlier, **responsive layouts involve art direction** as well. The original images may need to be cropped to match a different aspect ratio required by the graphic design, for a mobile device for example. The breakpoints generator tool enables you to select multiple aspect ratios. Breakpoints will be generated for each aspect ratio separately, while the original image is cropped to match the required aspect ratio.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bfd0679-334e-49a3-973c-241f02f2ac4f/10-aspect-ratio-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc1381eb-6407-4a9f-b538-afd2d55927e1/10-aspect-ratio-opt-preview.jpg" width="800" height="565" alt="Screen showing the result of generated images" /></a><figcaption>Generated images. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bfd0679-334e-49a3-973c-241f02f2ac4f/10-aspect-ratio-opt.jpg">Large preview</a>)</figcaption></figure>

You can download all the images of all the aspect ratios together. In addition, the tool generates a [HTML5 `picture` sample code](https://blog.cloudfour.com/responsive-images-101-part-6-picture-element/) that combines the different aspect ratios and their breakpoints into a single responsive HTML solution. Modern browsers, such as Chrome and Firefox, already [support the `picture` element](https://caniuse.com/#search=picture), while Microsoft’s Edge and Apple’s Safari have recently added support to their new official or beta versions. If you want to support older browsers as well, you can use the [Picturefill polyfill JavaScript library](https://scottjehl.github.io/picturefill/).

<pre><code class="language-markup">&lt;picture&gt;
  &lt;source media="(max-width: 480px)"
    sizes="(max-width: 1000px) 100vw, 1000px"
    srcset="dog_ar_3_4,c_fill__c_scale,w_200-opt.jpg 200w,
            dog_ar_3_4,c_fill__c_scale,w_386-opt.jpg 386w,
            dog_ar_3_4,c_fill__c_scale,w_522-opt.jpg 522w,
            dog_ar_3_4,c_fill__c_scale,w_632-opt.jpg 632w,
            dog_ar_3_4,c_fill__c_scale,w_739-opt.jpg 739w,
            dog_ar_3_4,c_fill__c_scale,w_834-opt.jpg 834w,
            dog_ar_3_4,c_fill__c_scale,w_920-opt.jpg 920w,
            dog_ar_3_4,c_fill__c_scale,w_1000-opt.jpg 1000w"&gt;
  &lt;source media="(max-width: 768px)"
    sizes="(max-width: 1000px) 100vw, 1000px"
    srcset="dog_ar_16_9,c_fill__c_scale,w_200-opt.jpg 200w,
            dog_ar_16_9,c_fill__c_scale,w_525-opt.jpg 525w,
            dog_ar_16_9,c_fill__c_scale,w_746-opt.jpg 746w,
            dog_ar_16_9,c_fill__c_scale,w_934-opt.jpg 934w,
            dog_ar_16_9,c_fill__c_scale,w_1000-opt.jpg 1000w"&gt;
  &lt;img
    sizes="(max-width: 1000px) 100vw, 1000px"
    srcset="dog_c_scale,w_200-opt.jpg 200w,
            dog_c_scale,w_508-opt.jpg 508w,
            dog_c_scale,w_721-opt.jpg 721w,
            dog_c_scale,w_901-opt.jpg 901w,
            dog_c_scale,w_1000-opt.jpg 1000w"
    src="dog_c_scale,w_1000-opt.jpg" alt="A nice dog"&gt;
&lt;/picture&gt;</code></pre>

The tool is freely available. It’s open sourced under the MIT license and is hosted on [GitHub](https://github.com/cloudinary/responsive_breakpoints_generator), while the actual breakpoints generation algorithms and the image resizing and cropping transformations run in the cloud.

## Automate Breakpoints Generation

The tool allows you to process your images, which is useful if you have a reasonable amount of statically uploaded images. However, what if your web application involves **user&ndash;generated content of dynamically uploaded images**?

To generate breakpoints for images uploaded by users, you need to programmatically generate them from your code. For each uploaded image, you probably need to call an API to generate the breakpoints, store or cache them on your side and then build your HTML5 or CSS snippets according to these breakpoints.

You may want to try out [Cloudinary’s API to programmatically request the breakpoints](https://cloudinary.com/documentation/image_upload_api_reference#upload) for newly uploaded images or existing ones. You can specify settings such as the width range, file size step, maximum number of images and request one or more image transformations to apply on the original image. Such transformations include aspect ratio&ndash;based cropping, face detection&ndash;based cropping and applying various image effects, filters and optimizations.

You can call the cloud&ndash;based API from your development framework code using open source SDKs. For example, the following Node.js code can be used to generate the breakpoints and the matching images for an uploaded image:

<pre><code class="language-javascript">cloudinary.uploader.v2.upload("sample-opt.jpg",
  { responsive_breakpoints:
      {
        create_derived: true,
        bytes_step: 20000,
        min_width: 200,
        max_width: 1000,
        transformation: { crop: 'fill', aspect_ratio: '16:9', gravity: 'face' },
      } },
  function(error, result) { console.log(result); }); </code></pre>

A quite generous free tier (for 75,000 images and 7,500 monthly transformations) is included for running it on your dynamically uploaded images.

{{% ad-panel-leaderboard %}}

## Summary

I hope the tool will help you address some of the challenges related to responsive images. This complexity is the driving force for new solutions that keep arising, such as the HTML5 `picture` element and `srcset` image attribute, the [Client-Hints specification](https://www.smashingmagazine.com/2016/01/leaner-responsive-images-client-hints/), and plenty of other client-side and server-side solutions.

Whichever responsive design solution or framework you choose, **you still need to generate and deliver multiple versions of each image**. The challenge of finding the best fitting resolutions, which are the responsive breakpoints for each specific image, is common for all approaches and frameworks.

Depending on the content of images and as a result of the nature of image compression algorithms, you may have to generate more versions for certain images and fewer for others.

Breakpoint generation should be streamlined in your web application when user&ndash;uploaded media is involved. Web pages should be rendered dynamically according to the generated breakpoints that allow browsers to download and show images of the best visual quality with optimized file sizes for any device and resolution. These actions will result in reduced bandwidth and processing costs, an improved user experience and an increase in user engagement and conversion rate.

### Further Reading on SmashingMag:

- “[Automating Art Direction With The Responsive Image Breakpoints Generator](https://www.smashingmagazine.com/2016/09/automating-art-direction-with-the-responsive-image-breakpoints-generator/),” Eric Portis
- “[Responsive Images Done Right: A Guide To <picture>And srcset</picture>](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/),” Eric Portis
- “[WordPress Responsive Images With Art Direction](https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/),” Laurie Laforest
- “[Responsive Images Now Landed In WordPress Core](https://www.smashingmagazine.com/2015/12/responsive-images-in-wordpress-core/),” Tim Evko

{{< signature "og, nl" >}}
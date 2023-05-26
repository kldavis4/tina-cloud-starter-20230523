---
title: 'Automatically Transforming And Optimizing Images And Videos On Your WordPress Website'
slug: transforming-optimizing-images-videos-wordpress-website
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8aaa9d52-375d-4e64-bdaa-151ef40a3f3c/transforming-optimizing-images-videos-wordpress-website.jpg
date: 2021-11-09T09:30:00.000Z
summary: >-
  In this article, Leonardo Losoviz explains how Cloudinary’s integration can be used with WordPress to produce and deliver optimal digital experiences.
description: >-
  In this article, Leonardo Losoviz explains how Cloudinary’s integration can be used with WordPress to produce and deliver optimal digital experiences.
categories:
  - Images
  - Plugins
  - WordPress
  - Optimization
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Cloudinary
  link: https://cloudinary.com/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e255398-3840-4aa3-a9d7-7ffd8949eaaa/cloudinary-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://cloudinary.com/">Cloudinary</a> whose mission is to help companies unleash the full potential of their media to create the most engaging visual experiences. <em>Thank you!</em>
---

So, you want to give personality to your site by making it stand out from all other websites out there. To do that, you develop a personalized design style, including a certain combination of colors, typography, spacing, animations, and others, and apply the style consistently throughout your site.

An example in case is this same website, Smashing Magazine. One of the objectives of [its big redesign](https://www.smashingmagazine.com/2017/03/a-little-surprise-is-waiting-for-you-here/) was to infuse the site with a uniquely distinctive personality. That’s why all avatars, the arrow button, and many other elements are all tilted, at the same angle as the Smashing logo is:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13b433e7-9c0e-4ee9-a907-04259176eb8f/1-transforming-optimizing-images-videos-wordpress-website.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13b433e7-9c0e-4ee9-a907-04259176eb8f/1-transforming-optimizing-images-videos-wordpress-website.png" width="800" height="567" sizes="100vw" caption="Tilted elements in Smashing Magazine (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13b433e7-9c0e-4ee9-a907-04259176eb8f/1-transforming-optimizing-images-videos-wordpress-website.png'>Large preview</a>)" alt="Tilted elements in Smashing Magazine" >}}

What about images? They can also take part in the unique design so that visitors browsing your site will immediately recognize it simply by looking at the content. For instance, I remember The Verge’s old bold design, which placed striking colors over its images:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/013a1286-fa8c-4010-8ccd-d61013e5abab/2-transforming-optimizing-images-videos-wordpress-website.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/013a1286-fa8c-4010-8ccd-d61013e5abab/2-transforming-optimizing-images-videos-wordpress-website.jpg" width="800" height="641" sizes="100vw" caption="Old homepage for The Verge (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/013a1286-fa8c-4010-8ccd-d61013e5abab/2-transforming-optimizing-images-videos-wordpress-website.jpg'>Large preview</a>)" alt="Old homepage for The Verge" >}}

Applying style to the images can be achieved with CSS. However, then the style will not be present when referencing the image directly (such as the image shared in social media via the `<meta property="og:image" content="{image-url}">` tag), making the image devoid of personality.

The images embedded in social media when sharing our content are of particular interest. These **images should carry the personality of the site**, for which the style must be embedded in the image itself, instead of being applied via CSS. For instance, in [SmashingMag’s Twitter account](https://twitter.com/smashingmag), the article’s featured image has a customized and consistent style, giving it a unique personality:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52d641b0-b877-47c4-a3ef-f5b90f3c1827/3-transforming-optimizing-images-videos-wordpress-website.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52d641b0-b877-47c4-a3ef-f5b90f3c1827/3-transforming-optimizing-images-videos-wordpress-website.png" width="800" height="690" sizes="100vw" caption="Smashing Magazine’s article shared on Twitter (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52d641b0-b877-47c4-a3ef-f5b90f3c1827/3-transforming-optimizing-images-videos-wordpress-website.png'>Large preview</a>)" alt="Smashing Magazines article shared on Twitter" >}}

Adding the style to the images on our site can be done manually (with Photoshop or some other image editing tool), but editing images is effort-intensive. The images need to be manipulated and re-uploaded to the site, for all the possible sizes (such as the featured image and each of the thumbnails) and all defined sets of styles (for instance, a page for the Black Friday sales could have its own style).

It makes more sense to automate this task. **Automation** is doable when the design is based on a series of transformations, to be applied one after the other, such as:

- Adding a watermark;
- Making the image round;
- Rotating the image to a certain angle;
- Adding a border, with a specific thickness and color;
- Adding a shadow;
- Cropping the image to a certain aspect ratio or fixed dimensions;
- Cropping the image around the face of the person;
- Converting the image to grayscale, or adding hue;
- Sharpening the image.

By defining a list of transformations, **the task to apply the desired style to our images can be automated**. As a result, the effort to produce a consistent style throughout the website, and change it at any time down the road, is greatly reduced.

Applying styles throughout the website now becomes:

- We preselect the styles to be applied to the images, for the whole site or a custom section, via configuration on the website’s back-end;
- We upload the original images.

Then, the images will be automatically applied transformations to produce the desired styles, and readily available to be inserted into the page via the website’s media manager.

We can do exactly this via [Cloudinary](https://cloudinary.com), a service that helps produce and deliver optimal digital experiences. Being based on the cloud, Cloudinary can be integrated with any site, based on any stack or technology. For this article, I’ll be using its integration with WordPress to demonstrate its transformation capabilities.
 
Specifically, I’ll be using [Cloudinary’s plugin for WordPress v3.0](https://wordpress.org/plugins/cloudinary-image-management-and-manipulation-in-the-cloud-cdn/), which is set to release this week. Let’s start!

## Adding Transformations To The Images

Cloudinary offers an extensive [list of transformations](https://cloudinary.com/documentation/transformation_reference), including all the ones I mentioned earlier on and many more, to manipulate not only images but also videos. Adding the desired transformations to an image’s URL, **the image can be modified in myriad ways**. I’ll demonstrate this by creating a thumbnail for an image.

In this pic, I’m with a couple of friends in sunny Barcelona:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e21faee5-c745-4d7e-a8a1-759bf2394a1c/4-transforming-optimizing-images-videos-wordpress-website.jpeg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e21faee5-c745-4d7e-a8a1-759bf2394a1c/4-transforming-optimizing-images-videos-wordpress-website.jpeg" width="600" height="450" alt="A picture of me and two friends in sunny Barcelona" /></a><figcaption>A picture of me and two friends in sunny Barcelona (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e21faee5-c745-4d7e-a8a1-759bf2394a1c/4-transforming-optimizing-images-videos-wordpress-website.jpeg">Large preview</a>)</figcaption></figure>

This picture in full size will be my post’s featured image. For the homepage, I want to link to the post using a thumbnail 300 pixels wide. To scale the image down, I attach transformation `w_300` to the image’s URL:

<table class="tablesaw">
  <thead>
    <tr>
      <th>Image</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Original</td>
      <td><a href="https://res.cloudinary.com/dpelr4pk9/images/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg">https://res.cloudinary.com/dpelr4pk9/images/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg</a></td>
    </tr>
    <tr>
      <td>Resized</td>
      <td><a href="https://res.cloudinary.com/dpelr4pk9/images/w_300/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg">https://res.cloudinary.com/dpelr4pk9/images/<code>w_300</code>/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg</a></td>
    </tr>
  </tbody>
</table>

The result is this one:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c9a66f3-a34b-4725-b45c-6db7b9ad393a/5-transforming-optimizing-images-videos-wordpress-website.jpeg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c9a66f3-a34b-4725-b45c-6db7b9ad393a/5-transforming-optimizing-images-videos-wordpress-website.jpeg" width="300" height="225" alt="Image resized to 300px wide" /></a><figcaption>Image resized to 300px wide (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c9a66f3-a34b-4725-b45c-6db7b9ad393a/5-transforming-optimizing-images-videos-wordpress-website.jpeg">Large preview</a>)</figcaption></figure>

Being a scaled-down version of the original image, the people inside this thumbnail look small. Let’s make them bigger, by cropping the image. For that, we attach transformation `c_crop` after the previous transformation:

<table class="tablesaw">
  <thead>
    <tr>
      <th>Transformation</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Resized + cropped</td>
      <td><a href="https://res.cloudinary.com/dpelr4pk9/images/w_300,c_crop/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg">https://res.cloudinary.com/dpelr4pk9/images/w_300,<code>c_crop</code>/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg</a></td>
    </tr>
  </tbody>
</table>

The result is this one:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72f37d76-4c98-46c3-bf92-d246e033ef30/6-transforming-optimizing-images-videos-wordpress-website.jpeg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72f37d76-4c98-46c3-bf92-d246e033ef30/6-transforming-optimizing-images-videos-wordpress-website.jpeg" width="300" height="225" alt="Image resized and cropped" /></a><figcaption>Image resized and cropped (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72f37d76-4c98-46c3-bf92-d246e033ef30/6-transforming-optimizing-images-videos-wordpress-website.jpeg">Large preview</a>)</figcaption></figure>

Yikes! What happened? One of my friends has been cropped out of the image! Let’s put him back in by applying the cropping around the south-west section of the image via the gravity transformation `g_south_west`:

<table class="tablesaw">
  <thead>
    <tr>
      <th>Transformation</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Resized + cropped + focused</td>
      <td><a href="https://res.cloudinary.com/dpelr4pk9/images/w_300,c_crop,g_south_west/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg">https://res.cloudinary.com/dpelr4pk9/images/w_300,c_crop,<code>g_south_west</code>/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg</a></td>
    </tr>
  </tbody>
</table>

The result is this one:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2aca48a-39f5-4050-83d8-07bf205e7b84/7-transforming-optimizing-images-videos-wordpress-website.jpeg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2aca48a-39f5-4050-83d8-07bf205e7b84/7-transforming-optimizing-images-videos-wordpress-website.jpeg" width="300" height="225" alt="Image resized, cropped and focused" /></a><figcaption>Image resized, cropped and focused (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2aca48a-39f5-4050-83d8-07bf205e7b84/7-transforming-optimizing-images-videos-wordpress-website.jpeg">Large preview</a>)</figcaption></figure>

Ok, my friend is back, but now the heads of my two friends have been chopped off! To fix this, Cloudinary offers a better option: using transformation `g_faces` will have an AI identify the faces in the image, and perform the cropping around these:

<table class="tablesaw">
  <thead>
    <tr>
      <th>Transformation</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Resized + cropped + focused around faces</td>
      <td><a href="https://res.cloudinary.com/dpelr4pk9/images/w_300,c_crop,g_faces/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg">https://res.cloudinary.com/dpelr4pk9/images/w_300,c_crop,<code>g_faces</code>/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg</a></td>
    </tr>
  </tbody>
</table>

The result is this one:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80d9355b-1770-4170-8ed1-8eb47caf55e8/8-transforming-optimizing-images-videos-wordpress-website.jpeg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80d9355b-1770-4170-8ed1-8eb47caf55e8/8-transforming-optimizing-images-videos-wordpress-website.jpeg" width="300" height="225" alt="Image resized, cropped and focused around faces" /></a><figcaption>Image resized, cropped and focused around faces (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80d9355b-1770-4170-8ed1-8eb47caf55e8/8-transforming-optimizing-images-videos-wordpress-website.jpeg">Large preview</a>)</figcaption></figure>

This looks much better! Now, what would happen if there were no people in the picture, so we can’t use `g_faces`? Cloudinary offers a still better option: using `g_auto`, an AI will automatically decide which is the most interesting section of the image, and perform the cropping around it:

<table class="tablesaw">
  <thead>
    <tr>
      <th>Transformation</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Resized + cropped + focused around the most interesting content</td>
      <td><a href="https://res.cloudinary.com/dpelr4pk9/images/w_300,c_crop,g_auto/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg">https://res.cloudinary.com/dpelr4pk9/images/w_300,c_crop,<code>g_auto</code>/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg</a></td>
    </tr>
  </tbody>
</table>

The result is this one:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e22e63fe-8362-4e0d-b420-3148b8b0019f/9-transforming-optimizing-images-videos-wordpress-website.jpeg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e22e63fe-8362-4e0d-b420-3148b8b0019f/9-transforming-optimizing-images-videos-wordpress-website.jpeg" width="300" height="225" alt="Image resized, cropped and focused around the most interesting content" /></a><figcaption>Image resized, cropped and focused around the most interesting content (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e22e63fe-8362-4e0d-b420-3148b8b0019f/9-transforming-optimizing-images-videos-wordpress-website.jpeg">Large preview</a>)</figcaption></figure>

Now the thumbnail looks perfect.

Finally, I want to apply some distinctive style that makes my site unique. I’ve decided to apply the hue level to `40`, via transformation `e_hue:40`:

<table class="tablesaw">
  <thead>
    <tr>
      <th>Transformation</th>
      <th>URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Resized + cropped + focused + custom hue</td>
      <td><a href="https://res.cloudinary.com/dpelr4pk9/images/w_300,c_crop,g_auto,e_hue:40/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg">https://res.cloudinary.com/dpelr4pk9/images/w_300,c_crop,g_auto,<code>e_hue:40</code>/v1636082490/wpPlayground/me-and-friends/me-and-friends.jpg</a></td>
    </tr>
  </tbody>
</table>

The result is this one:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1ce824c-8f5b-46c4-bbc2-834d6a99cd80/10-transforming-optimizing-images-videos-wordpress-website.jpeg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1ce824c-8f5b-46c4-bbc2-834d6a99cd80/10-transforming-optimizing-images-videos-wordpress-website.jpeg" width="300" height="225" alt="Image resized, cropped, focused and with distinctive hue level" /></a><figcaption>Image resized, cropped, focused and with distinctive hue level (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1ce824c-8f5b-46c4-bbc2-834d6a99cd80/10-transforming-optimizing-images-videos-wordpress-website.jpeg">Large preview</a>)</figcaption></figure>

I finally got it: the transformation I want to apply to my images, to obtain the thumbnails for the homepage, is `w_300,c_crop,g_auto,e_hue:40`.

## Serving The Most Optimal Images

In addition to using image transformations for styling, we can use them to compress images in order to load them faster. Indeed, **reducing the size of the images is exceptionally important** in order to [improve the performance of the site](https://www.smashingmagazine.com/2021/01/front-end-performance-quick-wins/).

Cloudinary is ideal to optimize performance, for two main reasons:

1. The images are served via a CDN, located near the user browsing the site, greatly reducing the latency of the request;
2. The service automatically compresses the images to the most optimal version, sparing this effort to the team.

In order to deliver the most optimal version of the image, Cloudinary offers a couple of handy transformations:

- `f_auto`: Automatically uses the most suitable image format, including AVIF, WebP, PNG and JPG.
- `q_auto`: Automatically calculates and serves the best tradeoff between visual quality and file size.

For instance, if the browser supports the [new AVIF format](https://www.smashingmagazine.com/2021/09/modern-image-formats-avif-webp/), then the served image will be of type `image/avif`, producing significant savings in file size while not decreasing the visual quality. Otherwise, it will serve `image/webp` if supported, or fall back to `image/png` or `image/jpg` (or some other format).

In the screenshot below, I have appended transformation `f_auto,q_auto` to the image from earlier on, and loaded it in Firefox and Safari. While in Safari the image is retrieved as `image/jp2`, in Firefox it is served as `image/webp`, thus transferring fewer bytes:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d7bfd8d-db37-41a5-bc8b-d9b9702990f1/11-transforming-optimizing-images-videos-wordpress-website.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d7bfd8d-db37-41a5-bc8b-d9b9702990f1/11-transforming-optimizing-images-videos-wordpress-website.png" width="800" height="754" sizes="100vw" caption="Contrasting an image loaded in Firefox and Safari (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d7bfd8d-db37-41a5-bc8b-d9b9702990f1/11-transforming-optimizing-images-videos-wordpress-website.png'>Large preview</a>)" alt="Contrasting an image loaded in Firefox and Safari" >}}

## Transforming Images In WordPress

Cloudinary has recently released v3.0 of its WordPress plugin, with [several handy new features](https://wordpress.org/plugins/cloudinary-image-management-and-manipulation-in-the-cloud-cdn/). Let’s use this plugin to automatically apply transformations to the images on a WordPress site.

If we are not Cloudinary users yet, we can [create an account for free](https://cloudinary.com/users/register/free). When installing the plugin, we will need to provide the connection information of our Cloudinary account:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ea5b040-791b-453a-8370-054e5595c931/12-transforming-optimizing-images-videos-wordpress-website.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ea5b040-791b-453a-8370-054e5595c931/12-transforming-optimizing-images-videos-wordpress-website.png" width="800" height="640" sizes="100vw" caption="Installing the plugin (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ea5b040-791b-453a-8370-054e5595c931/12-transforming-optimizing-images-videos-wordpress-website.png'>Large preview</a>)" alt="Installing the plugin" >}}

Once installed, the plugin’s dashboard will provide statistics of the transformations, bandwidth and storage the website is using:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47b690d4-faf5-4d1a-9ce9-d0bcbaa73adc/13-transforming-optimizing-images-videos-wordpress-website.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47b690d4-faf5-4d1a-9ce9-d0bcbaa73adc/13-transforming-optimizing-images-videos-wordpress-website.png" width="800" height="533" sizes="100vw" caption="Plugin dashboard (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47b690d4-faf5-4d1a-9ce9-d0bcbaa73adc/13-transforming-optimizing-images-videos-wordpress-website.png'>Large preview</a>)" alt="Plugin dashboard" >}}

In the "General settings" page we can configure if to synchronize the uploaded images to Cloudinary automatically or manually, under what folder to save the images for the site (which is particularly useful if we’re using Cloudinary for more than one site), and where to host the images.

By default, images are hosted in both the Cloudinary cloud and the WordPress server, giving us the chance to disable the Cloudinary plugin at any time **without any data loss**:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ba21ac9-23a0-410a-974d-b2a7526e7aaf/14-transforming-optimizing-images-videos-wordpress-website.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ba21ac9-23a0-410a-974d-b2a7526e7aaf/14-transforming-optimizing-images-videos-wordpress-website.png" width="800" height="587" sizes="100vw" caption="Plugin’s general settings (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ba21ac9-23a0-410a-974d-b2a7526e7aaf/14-transforming-optimizing-images-videos-wordpress-website.png'>Large preview</a>)" alt="Plugin’s general settings" >}}

In the "Image Settings" page, we can define global transformations to apply to all images. By default, all images have properties "Image format" and "Image quality" set to "Auto", which (as explained earlier on) will produce the most optimal version of the image according to the specific device and browser:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d74fe89e-e994-4916-8407-ee2c74bb2901/15-transforming-optimizing-images-videos-wordpress-website.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d74fe89e-e994-4916-8407-ee2c74bb2901/15-transforming-optimizing-images-videos-wordpress-website.png" width="800" height="587" sizes="100vw" caption="Plugin’s image settings (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d74fe89e-e994-4916-8407-ee2c74bb2901/15-transforming-optimizing-images-videos-wordpress-website.png'>Large preview</a>)" alt="Plugin’s image settings" >}}

On this page, we can also define "Additional image transformations", to be applied to all images. For instance, I can define here transformation `e_hue:40` to apply a hue level of 40 to all the images on my site.

We can also be more **selective when applying the style**. We can define transformations for a specific tag or category, which will be applied to the media elements added to the post with that tag or category:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6207c22e-2337-4138-868d-d81ead77fee8/16-transforming-optimizing-images-videos-wordpress-website.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6207c22e-2337-4138-868d-d81ead77fee8/16-transforming-optimizing-images-videos-wordpress-website.png" width="800" height="734" sizes="100vw" caption="Image transformations for a specific category (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6207c22e-2337-4138-868d-d81ead77fee8/16-transforming-optimizing-images-videos-wordpress-website.png'>Large preview</a>)" alt="Image transformations for a specific category" >}}

The other pages under the "Cloudinary" menu enable us to **configure the general options of the plugin**, so that we can do all of the following:

- Define transformations for videos (in addition to images);
- Use lazy loading, which improves performance by loading an image only when it appears within the viewport;
- Define breakpoints for responsive images, which improves performance by allowing the browser to load the smallest image that fits within the device’s screen;
- Configure Cloudinary’s Gallery block for the WordPress editor.

## Applying Transformations To Individual Images

In addition to defining transformations to be applied across the site, or for a specific tag or category, we can also apply transformations individually to a certain image, right when inserting the image into the post.

When opening the Media Manager, there will be a new tab "Cloudinary". Clicking there we can browse all the images hosted in our account, and **apply custom transformations** to them. As a result, a new image will be created on the WordPress site, to be added to the post as usual:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc04b4ec-9222-4fca-b839-cb57fc42c216/17-transforming-optimizing-images-videos-wordpress-website.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc04b4ec-9222-4fca-b839-cb57fc42c216/17-transforming-optimizing-images-videos-wordpress-website.gif" width="800" height="556" alt="Applying an individual transformation" /></a><figcaption>Applying an individual transformation (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc04b4ec-9222-4fca-b839-cb57fc42c216/17-transforming-optimizing-images-videos-wordpress-website.gif">Large preview</a>)</figcaption></figure>

I also want to add an overlay caption "Me and my friends in sunny Barcelona" on the image. To achieve this, the transformation `l_text:Arial_25:Me and my friends in sunny Barcelona,g_north_west,y_70,x_25` will add an overlay text and position it on a specific place on top of the image:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ceb6f64-1601-4add-8df5-99f99ab43e5f/18-transforming-optimizing-images-videos-wordpress-website.jpeg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ceb6f64-1601-4add-8df5-99f99ab43e5f/18-transforming-optimizing-images-videos-wordpress-website.jpeg" width="600" height="450" alt="Placing an overlay text on the image" /></a><figcaption>Placing an overlay text on the image (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ceb6f64-1601-4add-8df5-99f99ab43e5f/18-transforming-optimizing-images-videos-wordpress-website.jpeg">Large preview</a>)</figcaption></figure>

Now, since the transformed image is yet another image on the WordPress site, we can also use the WordPress editor to add the overlay text. For this, we can transform the image into a Cover block and add a caption:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46d32732-e6bc-43d4-9152-dcde173138c8/19-transforming-optimizing-images-videos-wordpress-website.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46d32732-e6bc-43d4-9152-dcde173138c8/19-transforming-optimizing-images-videos-wordpress-website.png" width="800" height="539" sizes="100vw" caption="Converting the image to Cover block (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46d32732-e6bc-43d4-9152-dcde173138c8/19-transforming-optimizing-images-videos-wordpress-website.png'>Large preview</a>)" alt="Converting the image to Cover block" >}}

In addition to the WordPress editor, Cloudinary’s plugin is also fully compatible with all popular page builders, including Elementor and Divi.

## Conclusion

If we want to make our websites successful, we need to pay special attention to two concerns:

1. **Design**  
You need to have the website stand out from all other websites out there by giving it a unique personality.
2. **Speed**  
Make sure that the website is as fast as possible for an optimal user experience, and to score the highest Core Web Vitals so that it can index higher in Google.

In both accounts, Cloudinary can help us out. All it takes to add a custom design for our images is to select the desired transformations, and the image (optimized to the specific browser and device) will be served from a CDN with data centers all over the world &mdash; delivering a super-fast experience.

If you have a WordPress site, the [latest version of the plugin](https://wordpress.org/plugins/cloudinary-image-management-and-manipulation-in-the-cloud-cdn/) provides an enhanced experience, including seamless integration with the WordPress editor, full compatibility with the major page builders, a new dashboard providing stats on the usage of the service, and improved features to optimize your site. Check it out!

{{< signature "vf, il" >}}

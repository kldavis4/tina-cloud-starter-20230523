---
title: 'A Guide To Optimizing Images For Mobile'
slug: imagekit-guide-optimizing-images-mobile
author: suzanne-scacca
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d024ba2-5531-4af6-9c9d-8fdf7a84857e/imagekit-full-sized.png
date: 2019-10-22T12:30:59+02:00
summary: >-
  You want to build a mobile website or PWA that converts visitors into leads or customers. But with Google and consumers alike becoming ever more demanding when it comes to loading speeds, what more can you do? ImageKit, a digital image optimization service, might have the all-in-one hands-off solution you need.
description: >-
  You want to build a mobile website or PWA that converts visitors into leads or customers. But with Google and consumers alike becoming ever more demanding when it comes to loading speeds, what more can you do? ImageKit, a digital image optimization service, might have the all-in-one hands-off solution you need.
categories:
  - Performance
  - Media
  - Mobile
  - Guides
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---
<p>(<em>This is a sponsored article.</em>) You know how critical it is to <a href="https://www.smashingmagazine.com/2019/06/web-designers-speed-mobile-websites/">build websites that load quickly</a>. All it takes is for a page to load one second too long for it to start losing visitors and sales. Plus, now that Google has made mobile-first indexing the default, you really can’t afford to let any performance optimizations fall by the wayside what with how difficult it can be to get your mobile site as speedy as your desktop.</p>

<p>Google takes many factors into account when ranking a website and visitors take maybe a handful of factors into account when deciding to explore a site. At the intersection of the two is <strong>website speed</strong>.</p>

<p>It should come as no surprise that images cause a lot of the problems websites have with speed. And while you could always just trim the fat and build more minimally designed and content-centric sites, why compromise?</p>

<p><strong>Images are a powerful force on the web.</strong></p>

<p>Not only can well-chosen images improve the aesthetics of a site, but they also make it easier for your visitors to consume content. Of course, there are the SEO benefits of images, too.</p>

<p>So, today, let’s focus on how you can still design with as many images as you want without slowing down your website. This will require you to update your image optimization strategy and adopt a tool called <a href="https://synd.co/2NgacDp">ImageKit</a>, but it shouldn’t take much work from you to get this new system in place.</p>

## The Necessity Of An Image Optimization Strategy For Mobile

<p>According to <a href="https://httparchive.org/reports/page-weight">HTTP Archive</a>:</p>

<ul>
<li>The median size of a <strong>desktop website in 2019 is 1939.5 KB</strong>.</li>
<li>The median size of a <strong>mobile website in 2019 is 1745.0 KB</strong>.</li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9ed8892-e624-4d14-b3d9-4e52e4e79a2d/http-archive-total-kilobytes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9ed8892-e624-4d14-b3d9-4e52e4e79a2d/http-archive-total-kilobytes.png" sizes="100vw" caption="HTTP Archive charts how many kilobytes desktop and mobile websites are, on average. (Source: <a href='https://httparchive.org/reports/page-weight'>HTTP Archive</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9ed8892-e624-4d14-b3d9-4e52e4e79a2d/http-archive-total-kilobytes.png'>Large preview</a>)" alt="HTTP Archive desktop and mobile kilobytes" >}}

<p>If we don’t get a handle on this growth, it’s going to be impossible to meet consumer and Google demands when it comes to providing fast websites. That or we’re going to have to get <em>really</em> good at optimizing for speed.</p>

<p>Speaking of speed, let’s see what HTTP Archive has to say about image weight.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df7e14c3-ad1d-4ea9-9e7a-dff3b04590a5/http-archive-image-bytes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df7e14c3-ad1d-4ea9-9e7a-dff3b04590a5/http-archive-image-bytes.png" sizes="100vw" caption="HTTP Archive plots out how much images weigh on desktop vs mobile websites. (Source: <a href='https://httparchive.org/reports/page-weight'>HTTP Archive</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df7e14c3-ad1d-4ea9-9e7a-dff3b04590a5/http-archive-image-bytes.png'>Large preview</a>)" alt="HTTP Archive image bytes desktop vs mobile" >}}

<p>As it stands today:</p>

<ul>
<li>The median size of <strong>images on desktop is 980.3 KB</strong> out of the total 1939.5 KB.</li>
<li>The median size of <strong>images on mobile is 891.7 KB</strong> out of the total 1745.0 KB.</li>
</ul>

<p>Bottom line: images add a lot of weight to websites and consume a lot of bandwidth. And although this data shows that the median size of images on mobile is less than their desktop counterparts, the proportion of images-to-website is slightly larger.</p>

<p>That said, if you have the right image optimization strategy in place, this can easily be remedied.</p>

<p>Here is what this strategy should entail:</p>

### 1. Size Your Images Correctly

<p>There are lots of tedious tasks you’d have to handle without the right automations in place. Like resizing your images.</p>

<p>But you have to do it, right?</p>

<p>Let’s say you use <a href="https://unsplash.com/photos/k6SFjtLiZWI">Unsplash</a> to source a number of images for a website you’re working on.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc72e8cd-cb58-4854-97c8-59e2a1671105/unsplash-image.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc72e8cd-cb58-4854-97c8-59e2a1671105/unsplash-image.png" sizes="100vw" caption="An example of a photo you’d find on Unsplash, this one comes from Mark Boss. (Source: <a href='https://unsplash.com/photos/k6SFjtLiZWI'>Unsplash</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc72e8cd-cb58-4854-97c8-59e2a1671105/unsplash-image.png'>Large preview</a>)" alt="Unsplash photo from Mark Boxx" >}}

<p>Unlike premium stock repositories where you might get to choose what size or file format you download the file in, you don’t get a choice here.</p>

<p>So, you download the image and any others you need. You then have the choice to use the image as is or manually resize it. After looking at the size of the file and the dimensions of the image, you realize it would be a good idea to resize it.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04421551-6e73-44e5-be46-a3f374e3bc95/unsplash-image-sizes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04421551-6e73-44e5-be46-a3f374e3bc95/unsplash-image-sizes.png" sizes="100vw" caption="These are the original dimensions of the Unsplash image: 5591&times;3145 px. (Source: <a href='https://unsplash.com/'>Unsplash</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04421551-6e73-44e5-be46-a3f374e3bc95/unsplash-image-sizes.png'>Large preview</a>)" alt="Original dimensions of image from Unsplash" >}}

<p>This particular image exported as a 3.6 MB file and a 5591&times;3145 px image. That’s way too big for any website.</p>

<p>There’s no reason to upload images larger than 1 MB &mdash; and that’s even pushing it. As for dimensions? Well, that depends on the width of your site, but I think somewhere between 1200 and 2000 px should be your max.</p>

<p>You’re going to have to go through this same process whether images come from a stock site or from someone’s DSLR. The point is, no source image is ever going to come out the “right” size for your website, which means resizing has to take place at some point.</p> 

<p>What’s more, responsive websites display images in different sizes depending on the device or browser they’re viewed on. And then there are the different use cases &mdash; like full-sized image vs. thumbnail or full-sized product photo vs. featured image.</p>

<p><strong>So, there’s more resizing that has to be done even after you’ve gone through the trouble of manually resizing them.</strong></p>

<p>Here’s what you <em>shouldn’t</em> do:</p>

<ul>
<li>Resize images one-by-one on your own. It’s time-consuming and inefficient.</li>
<li>Rely on browser resizing to display your images responsively as it can cause issues.</li>
</ul>

<p>Instead, you can integrate your existing image server (on your web host) or external storage service (like S3) with ImageKit. Or you can use ImageKit’s Media Library to store your files.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4efc97b2-cbda-462f-840e-9706e1494fcf/imagekit-image-upload.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4efc97b2-cbda-462f-840e-9706e1494fcf/imagekit-image-upload.png" sizes="100vw" caption="This is how easy it is to upload a new file to the ImageKit Media Library. (Source: <a href='https://synd.co/2NgacDp'>ImageKit</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4efc97b2-cbda-462f-840e-9706e1494fcf/imagekit-image-upload.png'>Large preview</a>)" alt="ImageKit Media Library upload" >}}

<p>As you can see, ImageKit has accepted the upload of this Unsplash photo at its original dimensions and sizes. The same goes for wherever your files originate from.</p>



<p>However, once you integrate your images or image storage with ImageKit, the tool will take control of your image sizing. You can see how that’s done here:</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f2bcc92-c9ad-4444-979d-6a4ba0390938/imagekit-url-endpoints.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f2bcc92-c9ad-4444-979d-6a4ba0390938/imagekit-url-endpoints.png" sizes="100vw" caption="ImageKit image URL endpoints enable users to more easily control image resizing parameters. (Source: <a href='https://synd.co/2NgacDp'>ImageKit</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f2bcc92-c9ad-4444-979d-6a4ba0390938/imagekit-url-endpoints.png'>Large preview</a>)" alt="ImageKit image URL endpoints" >}}

<p>Let me briefly explain what you’re looking at above:</p>

<ul>
<li>The <strong>Image Origin Preference</strong> tells ImageKit where images need to be optimized from. In this case, it’s the ImageKit Media Library and they’ll be served over my website.</li>
<li>The <strong>Old Image URL</strong> is a reminder of where our images lived on the server.</li>
<li>The <strong>New Image URLs</strong> explains where your images will be optimized through ImageKit.</li>
</ul>

<p>The formula is simple enough. You take the original URL for your image and you transform it with the new ImageKit URL.</p>

<p>The ImageKit URL alone will instantly shrink the size of your image files. However, if you want to do some resizing of your image’s dimensions while you’re at it, you can use transformation parameters to do so.</p>

<p>For example, this is the Unsplash photo as seen from the media library of my website. It lives on my own servers, which is why the address shows my own URL:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d024ba2-5531-4af6-9c9d-8fdf7a84857e/imagekit-full-sized.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d024ba2-5531-4af6-9c9d-8fdf7a84857e/imagekit-full-sized.png" sizes="100vw" caption="How a full-sized image from Unsplash might appear if you leave it as is on your server. (Source: <a href='https://unsplash.com/'>Unsplash</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d024ba2-5531-4af6-9c9d-8fdf7a84857e/imagekit-full-sized.png'>Large preview</a>)" alt="An Unsplash image without resizing" >}}

<p>To see what it looks like once ImageKit has transformed it, I swap out my domain name with the endpoint provided by ImageKit. I then add my image resizing parameters (<a href="https://synd.co/2N3fiTb">they allow you to do more than just resize</a>, too) and reattach the remainder of the URL that points to my image storage.</p>

<p>This is what happens when I use ImageKit to automatically resize my image to 1000&times;560 pixels:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/853235ec-64e9-4926-a03e-90358f4221d2/imagekit-resized.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/853235ec-64e9-4926-a03e-90358f4221d2/imagekit-resized.png" sizes="100vw" caption="ImageKit endpoints enable users to define how their images are to be resized like in this example. (Source: <a href='https://synd.co/2NgacDp'>ImageKit</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/853235ec-64e9-4926-a03e-90358f4221d2/imagekit-resized.png'>Large preview</a>)" alt="ImageKit endpoint image resizing" >}}

<p>To create this resized image, I transformed the ImageKit URL into the following:</p>

<p><em>https://imagekit.io/vq1l4ywcv/<strong>tr:w-1000,h-560/…</strong></em></p>

<p>It’s the width (w-) and height (h-) parameters that reduced the file’s dimensions.</p>

<p>Now, as you can see, this isn’t as pixel-perfect as the original image, but that’s because I have quite a bit of compression applied to the file (80%). I’ll cover how that works below.</p>

<p>In the meantime, let’s focus on how great the image still looks as well as the gains we’re about to get in speed.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e3843ad-cecb-4457-9502-0ff2005019b6/imagekit-resized-photo.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e3843ad-cecb-4457-9502-0ff2005019b6/imagekit-resized-photo.png" sizes="100vw" caption="This is what can happen after ImageKit users resize their images. (Source: <a href='https://unsplash.com/'>Unsplash</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e3843ad-cecb-4457-9502-0ff2005019b6/imagekit-resized-photo.png'>Large preview</a>)" alt="ImageKit resizing example on original Unsplash photo" >}}

<p>Previously, this was a 3.6 MB file for the 5591&times;3145 px image. Now, it’s a <strong>128 KB</strong> file for the 1000&times;560 px image.</p> 

<p>To sweeten the deal further, ImageKit makes it easy to resize your images this way using URL-based image transformation. Essentially, it works like this:</p>

<ul>
<li>You save one master image to ImageKit’s media library or your preferred server.</li>
<li>ImageKit automatically uses multiple techniques to bring down the image size significantly.</li>
<li>You can then use ImageKit’s resizing and cropping parameters to modify each image to cater to different device resolutions and sizes.</li>
</ul>

<p>When <a href="https://synd.co/2NgacDp">91mobiles</a> took advantage of this form of image optimization, it saved its website 3.5 TB every month of bandwidth. And they didn’t have to do anything but integrate with the platform. There was no need to move their images to ImageKit or another third-party storage service. It all took place within their legacy infrastructure.</p>

### 2. Use Faster-loading Image Formats

<p>It’s not just the size of your images that drain storage space and bandwidth. The file types you use have an impact, too.</p>

<p><strong>PNGs</strong>, in general, are used for things like logos, images containing text and other super-fine images that have a transparent background. While you can use them to save your photos, they tend to produce the largest sizes. Even when lossless compression is applied, PNGs still remain larger in size than other file types.</p>

<p><strong>GIFs</strong> are the animated counterpart of PNGs and use lossless compression as well.</p>

<p><strong>JPGs</strong>, on the other hand, are best suited for colorful images and photos. They’re smaller in size and they shrink down with lossy compression. It’s possible to compress JPGs enough to get them to a manageable size, but you have to be careful as lossy compression degrades the overall quality of a file and there’s no turning back once it’s been done.</p>

<p><strong>WebPs</strong> have been gaining in popularity since Google introduced them in the early 2010s. According to a Google study, <a href="https://developers.google.com/speed/webp/docs/webp_study">WebPs can be anywhere between 25% and 34% smaller than JPGs</a>. What’s more, you can use both lossy and lossless compression on WebPs to get them down to even smaller sizes.</p>

<p>Something to keep in mind with WebPs is that they’re not universally accepted. As of writing this, WebPs aren’t accepted by iOS devices. However, the latest versions of all other browsers, Google or otherwise, will gladly display them.</p>

<p>As for how ImageKit helps with this, it’s simple really:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/072aa21f-3cc8-4dfb-986a-5890ca38c878/imagekit-image-format-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/072aa21f-3cc8-4dfb-986a-5890ca38c878/imagekit-image-format-settings.png" sizes="100vw" caption="This ImageKit setting puts the responsibility on ImageKit to serve the best file format. (Source: <a href='https://synd.co/2NgacDp'>ImageKit</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/072aa21f-3cc8-4dfb-986a-5890ca38c878/imagekit-image-format-settings.png'>Large preview</a>)" alt="Image Kit image format settings" >}}

<p>When this setting is configured, ImageKit automatically determines the best file format to deliver each of your files in. It takes into account what the original image format and content was along with whether or not the visitor’s device supports it.</p>

<p>JPGs, PNGs and GIFs will all be converted into WebPs when possible &mdash; say, if the visitor visits from Chrome (which accepts them). If it’s not possible &mdash; say, if the visitor visits from Safari (which doesn’t accept them) &mdash; ImageKit will convert to the best (i.e. smallest) format with the defined transformations. This might be a PNG or JPG.</p>

<p><a href="https://synd.co/2NgacDp">Nykaa</a> was able to capitalize on this image optimization strategy from ImageKit. Even though their website had already been designed using a mix of JPGs and PNGs and were stored in a number of places around the web, ImageKit took care of automating the image formats right from the original URLs.</p>

### 3. Compress Images

<p>Next, we need to talk about image compression. I’ve already referenced this a couple times, but it breaks down to two types:</p>

#### Lossless

<p>This form of compression is used on PNGs and GIFs. To compress the file, metadata is stripped out. This way, the integrity of the image remains intact, but the file shrinkage isn’t as substantial as you’d get with lossy compression.</p>

#### Lossy

<p>This form of compression is applied to JPGs and WebPs. To compress the file, some parts of the image are “lost”, which can give certain spots a granier appearance than the original image. In most cases, it’s barely noticeable unless you look closely at a side-by-side of the two images. But to your visitors, the degradation is easy to miss since there’s no original to compare against.</p>

<p>With lossy compression, you get to control what percentage of the file degrades. A safe range would be anything over 70% to 80%. ImageKit, by default, sets its optimization for 80% and it estimates that you can save at least 20% to 25% of your file size just from that. In reality, though, it’s probably more (we’re looking at upwards of 40% like in the Unsplash image example above):</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5175d79-3ebd-41da-a58e-db40790e3445/imagekit-image-size-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5175d79-3ebd-41da-a58e-db40790e3445/imagekit-image-size-settings.png" sizes="100vw" caption="This ImageKit setting enables its users to decide how much lossy compression they want applied to their JPGs. (Source: <a href='https://synd.co/2NgacDp'>ImageKit</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5175d79-3ebd-41da-a58e-db40790e3445/imagekit-image-size-settings.png'>Large preview</a>)" alt="ImageKit lossy compression settings" >}}

<p>You can change this to whatever default you believe will maintain quality while giving you the image sizes that help your site load quickly.</p>

<p>Whether you use the default or your own optimization setting, remember to switch on the additional compression settings available under the Advanced tab.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8355fa12-bd1d-4c5d-8a35-2afe3909eaa3/imagekit-optimization-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8355fa12-bd1d-4c5d-8a35-2afe3909eaa3/imagekit-optimization-settings.png" sizes="100vw" caption="ImageKit provides Advanced image optimization settings for JPGs and PNGs. (Source: <a href='https://synd.co/2NgacDp'>ImageKit</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8355fa12-bd1d-4c5d-8a35-2afe3909eaa3/imagekit-optimization-settings.png'>Large preview</a>)" alt="ImageKit advanced optimization settings" >}}

<p>These three settings, in particular, will enable you to do as much compressing and as safely as possible.</p>

<p>The first setting “Save a Copy”, for instance, keeps your original images on the ImageKit server. That way, you have a copy of the image pre-compression without having to manage the burden of it on your own server.</p>

<p>The second setting “Preserve Image Metadata” enables you to apply lossless compression when feasible.</p>

<p>And the last setting “PNG Image Compression Mode” allows you to decide what level of lossless optimization you want to use on your PNGs: maximum, minimum or none.</p>

<p>When done, you’ll end up with results like this side-by-side comparison:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3eb701f-8ef1-4c31-9877-80deb80b7297/imagekit-compressed-vs-original.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3eb701f-8ef1-4c31-9877-80deb80b7297/imagekit-compressed-vs-original.png" sizes="100vw" caption="This side-by-side comparison of an Unsplash image from Luke Jeremiah shows a compressed file and an original JPG. (Source: <a href='https://unsplash.com/photos/GQYPMTHUjbU'>Unsplash</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3eb701f-8ef1-4c31-9877-80deb80b7297/imagekit-compressed-vs-original.png'>Large preview</a>)" alt="Comparison between compressed and original JPG from Unsplash" >}}

<p>This is a JPG from Unsplash. Can you tell which is the original and which is the compressed and resized version from ImageKit?</p>

<p>The one on the left with the black trim is:</p>

<ul>
<li>1500&times;1005 px</li>
<li>266 KB</li>
<li>Compressed at 95%</li>
</ul>

<p>The one on the right with the white trim is:</p>

<ul>
<li>5444&times;3649 px</li>
<li>2.5 MB</li>
<li>Original</li>
</ul>

<p>It’s up to you to decide which of the ImageKit compression and optimization settings you’re most comfortable using and then configure accordingly.</p>

### 4. Save to and Pull Images from External Server

<p>There are two ways to run images through ImageKit.</p>

<p>The first is by uploading your images directly to its Media Library:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b69e8ab-7c1d-436b-8f78-b34f8393edfd/imagekit-media-library.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b69e8ab-7c1d-436b-8f78-b34f8393edfd/imagekit-media-library.png" sizes="100vw" caption="ImageKit allows users to store their images in its Media Library instead of their own servers. (Source: <a href='https://synd.co/2NgacDp'>ImageKit</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b69e8ab-7c1d-436b-8f78-b34f8393edfd/imagekit-media-library.png'>Large preview</a>)" alt="ImageKit Media Library" >}}

<p>The second is by integrating with your website or external storage service. We’ve actually already seen this part of ImageKit. It’s where you get your URL endpoints from so you can define your image parameters:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/325c36e9-0370-4cf3-b030-dd9507f069e2/imagekit-integration.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/325c36e9-0370-4cf3-b030-dd9507f069e2/imagekit-integration.png" sizes="100vw" caption="ImageKit integrates with content management systems, third-party storage and Cloudinary. (Source: <a href='https://synd.co/2NgacDp'>ImageKit</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/325c36e9-0370-4cf3-b030-dd9507f069e2/imagekit-integration.png'>Large preview</a>)" alt="ImageKit integrations" >}}

<p>Even with all of the optimizations above, you might still be having a hard time with image storage and maintenance &mdash; either because of how they affect your speed or how much storage you have to hold them.</p>

<p>For instance, if you store your images on your server, you’ll eventually be constrained for space (unless you have a monster-sized hosting account).</p>

<p>When you’re building massive e-commerce stores or business websites with thousands or even millions of images and corresponding image sizes, you can’t afford to be hosting those images on your own. Granted, there is a way to serve them more quickly to visitors (which I’ll explain in the next point), but why take on the burden and cost of additional storage if you don’t have to?</p>

### 5. Add a CDN

<p>A CDN is another essential optimization tool for large repositories of images. Think of it like a second server, only this one caches (copies) your website and serves them through data centers located significantly closer to your visitors around the world.</p>

<p>As a result, the time it takes to send your website and its thousands of product images from New York, New York to Bangladesh, India happens insanely fast.</p>

<p>With ImageKit, you get to enjoy the privilege of serving your images not just through its core processing servers, but through AWS CloudFront CDN (included in all plans) which has over 150 locations worldwide.</p>

<p><a href="https://synd.co/2NgacDp">Sintra</a>, a client of ImageKit, saw a big leap in performance after moving to ImageKit. With the ImageKit image CDN (which has delivery nodes all around the globe), it saw an 18% drop in page load times.</p>

## Wrapping Up

<p>What’s especially nice about ImageKit is that it’s not just a preventative measure against slowdowns caused by images. You can use it to retroactively fix and improve mobile websites and PWAs, even if they already have millions of images on them. What’s more, the performance center makes it easy to keep an eye on your website’s images and identify opportunities for speed enhancements.</p>

<p>Plus, as you can see from the tips above, ImageKit has simplified a lot of the work you’d otherwise have to do, whether you’d handle it manually or configure it through a plugin.</p>

<p>With consumers and Google becoming pickier by the day about how quickly websites load on mobile, this is the kind of image optimization strategy you need. It’ll lighten your load while ensuring that any images added before or after ImageKit are optimized to the fullest. Even better, your clients will reap the benefits of more leads and greater conversions.</p>

{{< signature "yk" >}}


---
title: 'Image Optimization In WordPress'
slug: image-optimization-wordpress
author: adelina-tuca
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f5322c8-dec7-46a5-9256-bb9d75f2c4aa/blog-post-demo.jpg
date: 2019-06-06T14:00:34+02:00
summary: >-
  Are you using many full-sized images on your WordPress site? Take note that this is causing your pages to load slowly. A slow website affects your SEO, increases the bounce rates, and keeps your audience at a distance. This article will help you learn how to easily optimize all the images on your site (manually or on autopilot) in order to gain better loading times.
description: >-
  In this article, Adelina Țucă explains how you can easily optimize all the images on your website (manually or on autopilot) in order to gain better loading times.
categories:
  - WordPress
  - Media
  - Optimization
  - Workflow
---
<p>A slow website is everyone’s concern. Not only that it chases visitors away but it also affects your SEO. So trying to keep it ‘in shape’ is definitely one of the main items to tick when you run a business or even a personal site.</p>

<p>There are many ways to speed up your WordPress site, each one complementing the other. There is not a universal method. Improving your site speed is actually the sum of more of these methods combined. One of them is image optimization, which we will tackle extensively in this post.</p>

<p>So read further to learn how to manually and automatically optimize all the images on your WordPress site. This is a step-by-step guide on image optimization that will make your site lightweight and faster.</p>

## The Importance Of Image Optimization

<p>According to <a href="https://snipcart.com/blog/images-optimization-page-load-time">Snipcart</a>, the three main reasons why images are affecting your WordPress site are:</p>

<ul>
  <li><strong>They are too large.</strong> Use smaller sizes. <em>I will talk about this later in the article.</em></li>
  <li><strong>They are too many</strong>, which demands as many HTTP requests. <em>Using a CDN will help.</em></li>
  <li><strong>They contribute to a synchronous loading of elements</strong>, together with HTML, CSS, and JavaScript. This ends up with an increase of the render time. <em>Displaying your images progressively</em> (via lazy loading) will stop your images from loading at the same time with the other elements, which will make the page load quicker.</li>
</ul>

<p>So yes, optimizing your images is an essential practice to make your site lighter. But first, you need to discover what makes your site load slowly. This is where speed tests intervene.</p>

{{% feature-panel %}}

## How To Test Your WordPress Site Speed

<p>There are many tools that test your website’s speed. The simplest method is Pingdom.</p>

<p>Pingdom is a popular tool used by both casual users and developers. All you need to do is to open <a href="https://tools.pingdom.com/">Pingdom</a> and insert your WordPress site URL, choose the location that’s closest to the data center location of your hosting (based on your hosting’s servers), and start the test. If you have a CDN installed on your site, the location matters a great deal. But <a href="#cdn">more on that later</a>.</p>

<p>What’s nice about this tool is that, regardless of how simple its interface is, it displays advanced information about how a website performs, which is pure music to developers’ ears.</p>

<p>From these statistics, you will find out whether your site is doing well or it needs to be improved (or both). It’s nice because it gives you plenty of data and advice on pages, requests, and other sorts of issues and performance analysis.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b92abcc0-fde3-4d20-84f0-57d669e4c1d1/pingdom-2.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b92abcc0-fde3-4d20-84f0-57d669e4c1d1/pingdom-2.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b92abcc0-fde3-4d20-84f0-57d669e4c1d1/pingdom-2.jpg'>Large preview</a>)" alt="pingdom website speed test" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24cb8de6-b751-416a-9a3c-4b9e4dde9ddf/pingdom-3.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24cb8de6-b751-416a-9a3c-4b9e4dde9ddf/pingdom-3.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24cb8de6-b751-416a-9a3c-4b9e4dde9ddf/pingdom-3.jpg'>Large preview</a>)" alt="pingdom website speed test for image optimization" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c1bc933-ffcf-46dc-a635-185566056527/pingdom-4.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c1bc933-ffcf-46dc-a635-185566056527/pingdom-4.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c1bc933-ffcf-46dc-a635-185566056527/pingdom-4.jpg'>Large preview</a>)" alt="pingdom website speed test performance example" >}}

<p>On the same page, <a href="https://gtmetrix.com/">GTmetrix</a> is another cool tool that’s similar to Pingdom and which will analyze your site’s speed and performance in depth.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac02c4b8-6ed8-4e37-860f-bb25171f75ae/gtmetrix.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac02c4b8-6ed8-4e37-860f-bb25171f75ae/gtmetrix.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac02c4b8-6ed8-4e37-860f-bb25171f75ae/gtmetrix.jpg'>Large preview</a>)" alt="gtmetrix website performance test" >}}

<p><strong>Note</strong>: <em>GTmetrix usually displays a rather slower WordPress website than Pingdom; this is how the tool calculates the metrics. There are no discrepancies, it’s just that GTmetrix measures the fully loaded time, unlike Pingdom which only counts the onload time.</em></p>

<p>The <strong>onload time</strong> calculates the speed after a page has been processed completely and all the files on that page have finished downloading. That’s why the onload time will always be faster than the fully loaded time.</p>

<p>The <strong>fully loaded time</strong> happens after the onload process when a page starts transferring data over again, which means that GTmetrix includes the onload times when it calculates the speed of a page. It basically measures the whole cycle of responses and transfers it gets from the page in question. Hence the slower times.</p>

<p><a href="https://developers.google.com/speed/pagespeed/insights/">Google PageSpeed Insights</a> is yet another popular tool for testing your site speed. Unlike the first two tools that only display your site performance on desktops, Google’s official testing tool is good at measuring the speed of your website’s mobile version, too.</p>

<p>Apart from that, Google will also give you its best recommendations on what needs to be improved on your site for getting faster loading times.</p>

<p>Usually, with either of these three tools, you can detect how heavily your images are affecting your site speed.</p>

{{% ad-panel-leaderboard %}}

## How To Speed Up Your WordPress Website

<p>Of course, since this article is about image optimization, you guessed right that this is one of the methods. But before getting into the depths of the image optimization per se, let’s briefly talk about other <strong>ways that will help you if you have loads of images uploaded</strong> on your site.</p>

### Caching

<p>Caching is the action of temporarily storing data in a cache so that, if a user accesses your site frequently, the data will be automatically delivered without going through the initial loading process again (which takes place when the site files are requested for the first time). A cache is a sort of memory that collects data that’s being requested many times from the same viewport and is used to increase the speed of serving this data.</p>

<p>Caching is in fact really simple. No matter if you do it manually or by installing a plugin, it can be implemented on your site pretty quickly. Some of the best plugins are <a href="https://wordpress.org/plugins/wp-super-cache/">WP Super Cache</a> and <a href="https://wordpress.org/plugins/w3-total-cache/">W3 Total Cache</a> and <a href="https://wordpress.org/plugins/wp-super-cache/">WP Super Cache</a> &mdash; they are both free and best rated on WordPress.org official repository.</p>

### Content Delivery Networks

<p>A CDN will request your site content from the nearest server location to your readers’ accessing point. It means that it keeps a copy of your site in many data centers located in different places around the world. Once a visitor accesses your site via their home location, the nearest server will request your content, which translates into faster loading times. <a href="https://www.cloudflare.com/">Cloudflare</a> and <a href="https://www.stackpath.com/maxcdn/">MaxCDN</a> (now StackPath) are the most popular solutions for WordPress.</p>

### GZIP compression

<p>Through this method, you can compress your site’s files by making them smaller. This will reduce your site bandwidth and will transfer the respective files to the browser faster.</p>

<p>Both WP Super Cache and W3 Total Cache come with GZIP compression feature that you can enable after installation. Also, many of the popular WordPress hosting providers have this feature already enabled via their standard packages. To find out if GZIP compression is enabled on your site, use this <a href="https://smallseotools.com/check-gzip-compression/">tool</a> for a quick inspection.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b49dcb51-4a8c-401f-ad58-1402291adfe4/gzip-compression-test.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b49dcb51-4a8c-401f-ad58-1402291adfe4/gzip-compression-test.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b49dcb51-4a8c-401f-ad58-1402291adfe4/gzip-compression-test.jpg'>Large preview</a>)" alt="wordpress site test gzip compression enabled" >}}

<p>You can also add GZIP compression to your WordPress site manually by <a href="https://technumero.com/gzip-compression-in-wordpress/">modifying the .htaccess file</a>.</p>

<p>Other simple and common (sometimes omitted, though) tricks would be to use a <strong>lightweight WordPress theme, deactivate unnecessary plugins</strong> (those that you don’t use anymore or those that you don’t need temporarily), and <a href="https://wp-rocket.me/blog/make-wordpress-database-clean-whistle/">clean your WordPress database</a> regularly.</p>

<p>Paying attention to these details also contributes to reducing the time that WordPress needs to build and display a page. Sometimes, a feature-heavy theme or plugin can be a major factor in slowing down your site. Caching plugins can intervene in this situation but keeping your WordPress site as light and clean as possible might be a better approach.</p>

### Image Optimization

<p>This is a very efficient and simple technique that contributes to speeding up your WordPress site. And this is today’s topic, so let’s break it down into pieces.</p>

{{% ad-panel-leaderboard %}}

## Why Image Optimization?

<p>Nowadays, websites are using more visuals than ever in their quest to catch the user’s attention. Multimedia (images, videos, podcasts) grew in popularity so much over the last five years, which led site owners to use pages that are increasingly graphical and image-heavy.</p>

<blockquote>At this very moment, we are surrounded by billions of high-resolution images, videos, and graphics. They are the key to better-converting sites, hence to better marketing and business cards.</blockquote>

<p>Sometimes, people tend to forget or simply do not pay enough attention to the fact that uploading images on a regular basis affects their WordPress site speed gradually.</p>

<p>Especially if you have an image-heavy site and your content relies mostly on images and visuals, this should be your main concern.</p>

## How To Optimize Your Website Images

<p>This can be done either manually or with plugins. Let’s start with the manual method. (This is mostly for those of you who are very keen on having control over your site and doing everything on your own.) Optimizing images manually will also help you understand to a great extent how plugins (the <a href="#image-optimization-autopilot">automated method</a> that we’ll talk about a bit later) work.</p>

<p>If you want to automate the process of image optimization, you have a backup. There are lots of great WordPress plugins out there that can save you a lot of time and also deliver great results. We’ll talk more about that and <a href="#testing-tools">test a few tools</a> later on.</p>

### Optimize Your Website Images Manually

<p>Optimizing might mean a lot of stuff. Here, we can talk about compression, resizing, using the right formats, cropping and so on.</p>

#### Use The Right Image Format

<p>How can you tell what format is the best for your site images and which one has a higher resistance when it comes to editing and compression? The answer is, there is no general best format, but there are recommended formats based on the content that each image has.</p>

<p><strong>PNG</strong> is mostly used for graphics, logos, illustrations, icons, design sketches or text because it can be easily edited in photo editors and still keep a great quality after compression. That’s because the PNGs are lossless &mdash; they don’t lose any significant data during compression.</p>

<p><strong>JPG</strong> is more popular among photographers, casual users, or bloggers. It is lossy and can be compressed to smaller sizes while still preserving a good quality as seen with the naked eye. JPG is the format that supports millions of colors, that’s why people use it mostly for photos. It also supports high-compression levels.</p>

<p>An alternative to JPG and PNG could be <strong>WebP</strong>, a web image format introduced by Google, which has the role of providing even smaller sizes than JPG (or any other formats) while keeping the image quality similar to the latter. WebP format allows both lossy and lossless compression options. According to <a href="https://developers.google.com/speed/webp/docs/webp_study">Google</a>, a WebP image can get up to 34% smaller than a JPG image and up to 26% smaller than PNG images.</p>

<p>But WebP image format has its cons, such as not being supported by all browsers yet or by WordPress by default (you need tools for that). Learn more about how to <a href="https://themeisle.com/blog/what-is-webp/">integrate WebP images with WordPress</a>.</p>

<p>The conclusion regarding the image formats is that there is no such thing as a universally right format. It really depends on the type of images that you need on your site. If you’re using photos with a large variety of colors, JPG might be the right format because it’s good at compressing color-heavy photos, which can be reduced to a considerable extent. It does not suit images with only a few color data like graphics or screenshots.</p>

<p>Let’s do a quick test. I saved a JPG image containing a multitude of colors, then converted it to PNG. After conversion, the photo became much bigger in size. Then, I used <a href="https://imageresize.org/compress-images">ImageResize.org</a> tool to compress both images (I chose this tool because it allowed me to compress both formats and use files larger than 1MB).</p>

<p>This is the uncompressed image (via <a href="https://mystock.themeisle.com/">MyStock.photos</a>):</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb29e311-addc-47ab-bcb4-508b897098cc/shop.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb29e311-addc-47ab-bcb4-508b897098cc/shop.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb29e311-addc-47ab-bcb4-508b897098cc/shop.jpg'>Large preview</a>)" alt="testing jpg compression original image" >}}

<p>And these are the results:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7015acf8-cda8-4d55-b6e2-b355ff719496/results-jpg-compression.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7015acf8-cda8-4d55-b6e2-b355ff719496/results-jpg-compression.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7015acf8-cda8-4d55-b6e2-b355ff719496/results-jpg-compression.png'>Large preview</a>)" alt="results after testing JPG image compression" >}}

<p>On the other hand, PNG is the right format if you’re using many screenshots, graphics, logos, or transparent images &mdash; in general, images with very few colors or images that contain block colors (for instance, transitions between light and dark backgrounds). PNG is lossless and can often result in very small sizes after compression, which could otherwise be bigger as JPG. Saving this kind of images as JPG can make them low-quality and blurry.</p>

<p>Let’s do another test. I saved a screenshot of my WordPress dashboard both as JPG and PNG. Then I used the same ImageResize.org for compressing each format. It’s worth mentioning that the PNG file was saved in a significantly smaller size than the JPG to begin with.</p>

<p>This is the image:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7a0b843-41c4-4011-b170-17fdc93afb9c/png.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7a0b843-41c4-4011-b170-17fdc93afb9c/png.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7a0b843-41c4-4011-b170-17fdc93afb9c/png.png'>Large preview</a>)" alt="testing png compression original image" >}}

<p>The results after compression:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c534eb5-9c6e-43e0-903b-e5898a6f0649/results-png-compression.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c534eb5-9c6e-43e0-903b-e5898a6f0649/results-png-compression.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c534eb5-9c6e-43e0-903b-e5898a6f0649/results-png-compression.png'>Large preview</a>)" alt="results after testing PNG image compression" >}}

#### Find Out The Maximum Display Size Of Your Images

<p>If you’re into optimizing images by yourself, you should first find out what’s their maximum display size. Since your site is responsive, all the images you upload will be served at different resolutions based on the user viewport (the device they’re browsing your site from).</p>

<p>The maximum display size is the largest resolution the image can take counting all the potential viewports and screens that can access it.</p>

<p>How can you check the maximum display size of an image?</p>

<p>First, open a page or a post that contains the image you want to check. You need to resize your browser manually (make it gradually smaller by dragging its edges) to the point where the image jumps to the largest dimension. This point is called a “breakpoint” &mdash; because the image size suddenly breaks.</p>

<p>After the image jumped to the large dimension, press right click -> Inspect (if your browser is Chrome). Hover over the URL of the image in the top-right of the screen and you’ll see both the dimensions it is served at and its original dimensions (intrinsic). The latter is what the users will be downloading, while the former ones represent the maximum display size of the image on that page.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fd74e6f-ebe1-4a87-96af-a0a244951cbc/maximum-display-size1.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00b72e62-8891-4757-a215-3e4c959d1e25/maximum-display-sizing.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fd74e6f-ebe1-4a87-96af-a0a244951cbc/maximum-display-size1.jpg'>Large preview</a>)" alt="find maximum display size of an image Chrome" >}}

<p>With this information in mind, you can now resize and crop your image so it can correspond to the given dimensions. This way, you’ll make sure you will optimize it efficiently so it can still look great on the screen and, at the same time, not weigh much on your site.</p>

<p>For instance, if you want your images to be Retina-friendly, edit them using twice the maximum display size for better quality. The image in the screenshot has 428x321 pixels, so make it 856x642 pixels for a better Retina quality.</p>

#### Resize And Crop Images

<p>When you’re dealing with files that have dimensions a lot bigger than you normally need to showcase on your site, you can simply resize or crop them and only then upload them on your site. You will save disk space and keep your site lighter.</p>

<p>Of course, if you have a photography portfolio and it’s important for you that the visitors see your works in their original form, then yes, you have a real motive for presenting them at their best.</p>

<p>You can also crop your images anytime if there’s only one single detail that you want to show to the people and there’s no reason to upload the broad, full image if the rest of the content is redundant.</p>

#### Compress Images

<p>All the photo editors have this option where they ask you at what quality you want to save your edited image. You usually go with a quality of 100% (for obvious reasons), but you can lower it a bit to, say, 70-80%. You won’t notice a big difference if the image already has a huge resolution. Its size will be smaller in this case.</p>

<p>After you’ve set a lower quality percentage and saved the image, you can go deeper with another round of optimization of the same image by using an online tool to reduce its size even more.</p>

<p><a href="https://jpeg-optimizer.com/">JPEG Optimizer</a> and <a href="https://www.jpeg.io/">JPEG.io</a> have a reduction percentage of around 60%, while <a href="https://tinypng.com/">TinyPNG</a> (if you choose to work with PNGs) of around 70%. <a href="https://kraken.io/web-interface">Kraken</a> is good for both formats, returning files of around 70% smaller via lossy compression.</p>

<p>Mac users can try <a href="https://imageoptim.com/api">ImageOptim</a>, which compresses both JPG and PNG formats up to 50%.</p>

## Set Image Optimization On Autopilot

<p>In order to automate the image optimization process on your site, you need tools (aka WordPress plugins). It means that they will do all the things that we talked about earlier but on autopilot.</p>

<p>There are several automatic WordPress solutions for image optimization but, in this post, I will only present to you those that come with solid features that can put on the table the full set for complete image optimization.</p>

<p>I’ll also show you the tests I conducted with each of the next three tools so you can observe everything in detail.</p>

<p>We are going to compare Optimole, ShortPixel, and Smush.</p>

### <a href="https://optimole.com/">Optimole</a>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d0df6c0-7050-43d3-ac33-19cfeff5facc/optimole.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d0df6c0-7050-43d3-ac33-19cfeff5facc/optimole.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d0df6c0-7050-43d3-ac33-19cfeff5facc/optimole.jpg'>Large preview</a>)" alt="optimole best image optimization wordpress plugins" >}}

<p>Optimole is probably the most complex of them all because it encapsulates all the features one might need for efficient image optimization. So if you’re looking for smart image optimization in its all aspects, then you might like Optimole.</p>

<p>Optimole transfers your images to a cloud where they are being optimized. Then, the optimized images are sifted through a CDN that makes them load fast. The plugin replaces each image’s URL with a custom one.</p>

<p>Adapting the images to each user’s screen size is another key feature of Optimole. It means that it automatically optimizes your images to the right dimension based on the user viewport, so if you’re seeing the image from a tablet, it will deliver the perfect size and quality for a tablet standard. These transformations are being made fast, without consuming any extra space on your site.</p>

<p>Another smart approach that you will enjoy about Optimole is its wit for detecting when a user has a slower connection. When it recognizes a slow connection, the plugin compresses the images on your site on a higher rate so that your visitors’ page loading time won’t be affected.</p>

<p>If you want lazy loading, the plugin also allows you to use it on your site. You just tick one box and Optimole does the work for you.</p>

<p>Another interesting thing about Optimole is that it won’t optimize all the images in your WordPress media library automatically. It only optimizes the images that people request by entering a page on your site. So don’t panic if you install the plugin and nothing happens. Once an image is requested by a user, the plugin will do what I already explained above. This is very space-saving since this plugin only uses one image, which it transforms in the cloud based on the users’ requests and devices.</p>

<p>What I love about this plugin is that it is smart and efficient and it’s never doing unnecessary work or conversions. We are using it on three of our sites: <a href="https://themeisle.com/blog/">ThemeIsle</a>, <a href="https://www.codeinwp.com/blog/">CodeinWP</a>, and <a href="https://justfreethemes.com/">JustFreeThemes</a>. You can check them out as demos.</p>

### <a href="https://shortpixel.com/">ShortPixel</a>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb81a8b0-ae9f-4672-bfe0-9a81003411a9/shortpixel.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb81a8b0-ae9f-4672-bfe0-9a81003411a9/shortpixel.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb81a8b0-ae9f-4672-bfe0-9a81003411a9/shortpixel.jpg'>Large preview</a>)" alt="shortpixel best image optimization wordpress plugins" >}}

<p>ShortPixel is a popular WordPress plugin that’s great at optimizing your images in bulk. The plugin works on autopilot and optimizes by default every image that you upload to your media library. You can deactivate this option if you don’t need it, though.</p>

<p>The plugin offers lossy, glossy, and lossless compression, which you can apply even to thumbnails. All the modified images are saved in a separate folder on your site where you can always go back and forth to undo/redo an optimization. For example, convert back from lossless to lossy and vice-versa, or simply restore to the original files.</p>

<p>Moreover, if you go to the WordPress media library and select the list view instead of the grid view that comes by default, you will notice that the last column keeps you up to date regarding the compression status. This way, you can manually skim through all the images and compress/decompress those that you need. For every image, you will see by what percentage it was compressed.</p>

<p>If you want to optimize them all at once, just select Bulk Actions -> Optimize with ShortPixel (or any of its sub-items), and click Apply. Your images will be compressed in just a few moments.</p>

<p>Moreover, ShortPixel lets you convert PNG to JPG automatically, create WebP versions of your images, and optimize PDF files. It also provides CMYK to RGB conversion. It works with Cloudflare CDN service to upload the optimized images on a cloud server.</p>

### <a href="https://wordpress.org/plugins/wp-smushit/">Smush</a>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcbf4f0d-504a-4d0d-bda8-1b8e3b630f42/smush.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcbf4f0d-504a-4d0d-bda8-1b8e3b630f42/smush.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcbf4f0d-504a-4d0d-bda8-1b8e3b630f42/smush.jpg'>Large preview</a>)" alt="smush best image optimization wordpress plugins" >}}

<p>Another big name in the WordPress plugin space, Smush is a friendly tool that optimizes your images on the run. Smush comes with a beautiful tracking dashboard where it keeps you up to date on your website’s total savings, how many items were not optimized yet, how many were optimized already, and what methods it used for that.</p>

<p>It also has bulk compression, lazy loading, automatic PNG to JPG, and CDN integration. Same as ShortPixel, Smush also adds the compression status to each image in your media library, so you can either manage them individually or in bulk.</p>

<p>Smush uses lossless compression by default, focusing on keeping the images as close to their original version as possible. The downside of this plugin is that it doesn’t offer the same amount of features in the free version, like the aforementioned plugins do. You need to pay for some of the basic functionality.</p>

## Testing The Three Image Optimization Plugins

<p>I took the next image of <strong>904 KB</strong> from <a href="https://mystock.themeisle.com/">MyStock.photos</a> and ran it through a series of tests with the three plugins I presented above.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfdeecc5-39c6-4452-9029-f7c66c712416/parrots.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfdeecc5-39c6-4452-9029-f7c66c712416/parrots.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfdeecc5-39c6-4452-9029-f7c66c712416/parrots.jpg'>Large preview</a>)" alt="image optimization wordpress plugins test - original image" >}}

<p>This is how the plugins performed:</p>

<ul>
  <li><strong>Optimole:</strong> 555 KB (312 KB if you pick the High compression level)</li>
  <li><strong>ShortPixel:</strong> 197.87 KB</li>
  <li><strong>Smush:</strong> 894 KB</li>
</ul>

<p><em>*Optimole and ShortPixel are using lossy compression, while Smush is using lossless compression.</em></p>

<p>The next approach is even more interesting.</p>

<p>I uploaded this very image on my WordPress site and used it in a blog post afterwards. Both <strong>Optimole and ShortPixel automatically reduced its size to make it match my screen resolution and post layout.</strong> So instead of using an almost 1 MB image, shrunk to fit the post, I am now using the same <strong>image reduced to its maximum display size</strong>. The plugins found the right size and dimensions needed in my blog post and modified the image accordingly.</p>

<p>And these are the reduced dimensions per each plugin:</p>

<ul>
  <li><strong>Optimole:</strong> 158 KB, 524x394 pixels</li>
  <li><strong>ShortPixel:</strong> 71.7 KB, 768x577 pixels</li>
  <li><strong>Smush:</strong> didn’t optimize for this specific request</li>
</ul>

<p>That being said, it’s important to note down two things:</p>

<ol>
<li>ShortPixel returned the best compression size but in larger dimensions; overall, a good result only it lost a bit of the image’s original quality.</li>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcd01b6b-2485-4fd7-b2bd-f18234c2e691/parrots-by-shortpixel.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcd01b6b-2485-4fd7-b2bd-f18234c2e691/parrots-by-shortpixel.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcd01b6b-2485-4fd7-b2bd-f18234c2e691/parrots-by-shortpixel.jpg'>Large preview</a>)" alt="shortpixel image optimization test result desktop" >}}

<li>Optimole (which I set on Auto compression this time) returned a higher size but with smaller dimensions and with better quality as seen with the naked eye. Optimole somehow found a great mix between size and dimensions so that the quality won’t lose much ground here.</li>
</ol>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc69452f-7f6e-4076-aa94-d5736d2afc88/parrots-by-optimole.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc69452f-7f6e-4076-aa94-d5736d2afc88/parrots-by-optimole.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc69452f-7f6e-4076-aa94-d5736d2afc88/parrots-by-optimole.jpg'>Large preview</a>)" alt="optimole image optimization test result desktop" >}}

<p>This is how it’s supposed to look on the live website:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f5322c8-dec7-46a5-9256-bb9d75f2c4aa/blog-post-demo.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f5322c8-dec7-46a5-9256-bb9d75f2c4aa/blog-post-demo.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f5322c8-dec7-46a5-9256-bb9d75f2c4aa/blog-post-demo.jpg'>Large preview</a>)" alt="wordpress blog post demo image optimization display" >}}

<p>If you ask me, Optimole adapted better to this specific request and the user’s viewport (in this case, my laptop screen).</p>

<p>Now, let’s have a quick peek at <strong>how these plugins adapt to mobile screens</strong>:</p>

<p>I followed the same routine. I activated one plugin at once and requested the same website page via my mobile (Android). The results:</p>

<figure>
  <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c274ed46-016a-49a0-a1dd-fe16c4f55e46/parrots-optimole-mobile.jpg">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c274ed46-016a-49a0-a1dd-fe16c4f55e46/parrots-optimole-mobile.jpg" alt="optimole image optimization test result mobile">
  </a>
  <figcaption class="op-vertical-bottom">
    <strong>Optimole</strong>: 96 KB, 389x292 pixels.
  </figcaption>
</figure>

<figure>
  <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0991bc9-a829-4777-a76b-4ff6e927da96/parrots-shortpixel-mobile.jpg">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0991bc9-a829-4777-a76b-4ff6e927da96/parrots-shortpixel-mobile.jpg" alt="shortpixel image optimization test result mobile">
  </a>
  <figcaption class="op-vertical-bottom">
    <strong>ShortPixel</strong>: 19 KB, 300x225 pixels.
  </figcaption>
</figure>

<p><strong>Smush</strong>: didn’t optimize the image for mobile.</p>

<p>My mobile demo screen:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc9eb205-3fbd-4352-b0fd-a021f77f4695/mobile-demo.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a866d4d-1fb2-4715-9dc5-48fd7e6ab21f/mobile-demo-wide.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc9eb205-3fbd-4352-b0fd-a021f77f4695/mobile-demo.png'>Large preview</a>)" alt="wordpress blog post demo image optimization mobile display" >}}

<p>As it happened in the first example, Optimole returned a bigger, more quality-focused version, while ShortPixel converted the image to a better size but with a slight loss in quality.</p>

<p>I initially used an image of 6 MB for the main desktop test but, since Smush doesn’t allow files larger than 1 MB in its free version (the others do allow), I had to pick an image under 1 MB.</p>

<p>I’ll do this test anyway with Optimole and ShortPixel only.</p>

<p>So, let’s do the fourth test, this time on a larger image.</p>

<p>The original image has <strong>6.23 MB</strong>.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2e265cb-7ee2-4990-aa42-78184999805c/dog.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2e265cb-7ee2-4990-aa42-78184999805c/dog.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2e265cb-7ee2-4990-aa42-78184999805c/dog.jpg'>Large preview</a>)" alt="image optimization wordpress plugins test - original image" >}}

<p>The optimized sizes are:</p>

<ul>
  <li><strong>Optimole</strong>: 798 KB with Auto compression level, 480 KB with High compression level</li>
  <li><strong>ShortPixel</strong>: 400.58 KB</li>
</ul>

<p>There’s also <a href="https://wordpress.org/plugins/ewww-image-optimizer/">EWWW Image Optimizer plugin</a> that, similarly to Smush, only uses lossless compression and only reduces images by a fairly small percentage.</p>

<p>The conclusions after the four tests:</p>

<ul>
  <li><strong>ShortPixel is delivering the best optimization rates</strong> (around 70-80%), while Optimole is somewhere at 40% on Auto compression level and at 70% on High compression level.</li>
<li><strong>Optimole is adapting the content better to the users’ viewport and internet connection.</strong> If you set it on Auto, it will know how to both reduce size consistently and preserve a great quality. I like that it knows how to juggle with all these variables so it both helps to improve your site’s loading time and display high-quality images to your visitors.</li>
</ul>

<p>If I had to put together not only the results of the tests but also the other features of the plugins (aka simplicity and user-friendliness), I would go with Optimole. But ShortPixel is also a great contender that I warmly recommend. Smush is a decent option too if you are willing to pay for it or you are a photographer that wants to keep their images as little processed as possible.</p>

## Wrapping Up

<p>Do not underestimate the impact of image optimization. Images are always one of the main reasons for a slow website. Google doesn’t like slow websites and nor do your visitors and clients. Especially if you’re seeking monetization via your WordPress site. An unoptimized site will influence your SEO, drag you down in SERPs, increase your bounce rates, and will lose you money.</p>

<p>No matter if you prefer doing the image optimization manually or choosing a plugin to automate it for you, you will see the good results sooner rather than later.</p>

<p>What other methods are you using to hold the images in check on your WordPress site?</p>

{{< signature "dm, yk, il" >}}

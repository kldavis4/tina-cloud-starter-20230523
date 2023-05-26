---
title: 'Speed Up Your Website With WebP'
slug: speed-up-your-website-webp
author: suzanne-scacca
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ee3808d-0f2e-4838-b3ee-8d48470b9fec/image4-speed-up-your-website-webp.png
date: 2019-10-29T12:30:59+02:00
summary: >-
  Images are a big part of the web and, yet, they can cause a lot of challenges for the user experience if not properly optimized or delivered. It’s been almost a decade since Google introduced the world to WebP as a solution to this problem. As more of our browsers, devices and software support it, it’s time that web designers started adopting it as their default image format.
description: >-
  Images are a big part of the web and, yet, they can cause a lot of challenges for the user experience if not properly optimized or delivered. It’s been almost a decade since Google introduced the world to WebP as a solution to this problem. As more of our browsers, devices and software support it, it’s time that web designers started adopting it as their default image format.
categories:
  - Performance
  - Media
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---
(This is a sponsored post.) Spend enough time running websites through [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/) and you’ll notice that Google has a major beef with traditional image formats like JPG, PNG and even GIF. As well it should. 

Even if you resize your images to the exact specifications of your website and run them through a compressor, they can still put a strain on performance and run up bandwidth usage. Worse, all of that image manipulation can compromise the resulting quality. 

Considering how important images are to web design, this isn’t an element we can dispose of so easily nor can we afford to cut corners when it comes to optimizing them. So, what’s the solution?

Here’s what Google suggests: 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b71f7305-80f7-4e27-887c-2867879f1447/image1-speed-up-your-website-webp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b71f7305-80f7-4e27-887c-2867879f1447/image1-speed-up-your-website-webp.png" sizes="100vw" caption="PageSpeed Insights demonstrates how much storage and bandwidth websites stand to save with WebP. (Source: <a href='https://developers.google.com/speed/pagespeed/insights/'>PageSpeed Insights</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b71f7305-80f7-4e27-887c-2867879f1447/image1-speed-up-your-website-webp.png'>Large preview</a>)" alt="PageSpeed Insights WebP tips" >}}

Years ago, Google aimed to put a stop to this problem by creating a next-gen image format called WebP. You can see in this screenshot from PageSpeed Insights that Google recommends using WebP and other next-gen formats to significantly reduce the size of your images while preserving their quality.

And if .75 seconds doesn’t seem like much to you (at least in this example), it could make a big difference in the lives of your visitors, the people who sit there wondering how long is too long to wait. **Just one less second of loading could make a world of difference to your conversion rate.**

But is WebP the best solution for this problem? Today, we’re going to examine: 

<ul>
<li><a href="#meaning-of-webp">What WebP is</a>,</li>
<li>What are the <a href="#webp-advantages">advantages</a> of using it,</li>
<li><a href="#how-webp-works">How it works</a> with browsers and devices,</li>
<li>What are the <a href="#webp-challenges">challenges</a> of converting and delivering WebP, and</li>
<li>How to <a href="#simplify-webp-keycdn">simplify conversion</a> and delivery with KeyCDN.</li>
</ul>

## What is WebP?

Google developed WebP back in 2010 after [acquiring a company called On2 Technologies](https://en.wikipedia.org/wiki/WebP). On2 had worked on a number of video compression technologies, which ended up serving as the basis for Google’s new audiovisual format WebM and next-gen image format WebP. 

Originally, WebP used lossy compression in an attempt to create smaller yet still high-quality images for the web. 

{{% pull-quote %}}
 If .75 seconds doesn’t seem like much to you, it could make a big difference in the lives of your visitors, the people who sit there wondering how long is too long to wait.
{{% /pull-quote %}}

### Lossy Compression For WebP

Lossy compression is a form of compression used to greatly reduce the file sizes of JPGs and GIFs. In order to make that happen, though, some of the data (pixels) from the file needs to be dropped out or “lost”. This, in turn, leads to some degradation of the quality of the image, though it’s not always noticeable.

WebP entered the picture with a much more efficient use of lossy compression (which I’ll explain below) and became the much-needed successor to JPG. 

You can see a great demonstration of this difference as KeyCDN [compares the difference in file sizes of a compressed JPG vs. WebP](https://www.keycdn.com/blog/convert-to-webp-the-successor-of-jpeg): 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42497b1c-4b3b-49fa-ba0e-16dcfb4020cd/image3-speed-up-your-website-webp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42497b1c-4b3b-49fa-ba0e-16dcfb4020cd/image3-speed-up-your-website-webp.png" sizes="100vw" caption="KeyCDN shows how five images differ in size between the original, a compressed JPG and a WebP. (Source: <a href='https://www.keycdn.com/blog/convert-to-webp-the-successor-of-jpeg'>KeyCDN</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42497b1c-4b3b-49fa-ba0e-16dcfb4020cd/image3-speed-up-your-website-webp.png'>Large preview</a>)" alt="KeyCDN compares original file size against compressed JPG and WebP" >}}

Notice how significant a difference this is in terms of file size, even after the JPG has been compressed to a comparable quality. [As Adrian James explains here](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/), though, you have to be careful with WebP compression. 

<blockquote>“Compression settings don’t match up one-to-one with JPEG. Don’t expect a 50%-quality JPEG to match a 50%-quality WebP. Quality drops pretty sharply on the WebP scale, so start at a high quality and work your way down.”</blockquote>

Considering how much more file sizes shrink with WebP compared to JPG, though, that shouldn’t be too much of a sticking point. It’s just something to think about if you’re considering pushing the limits of what WebP can do even further. 

Now, as time passed, Google continued to develop WebP technology, eventually getting it to a point where it would support not just true-color web graphics, but also XMP metadata, color profiles, tiling, animation, and transparency. 

Eventually, Google brought lossless compression to WebP, **turning it into a viable contender for PNG**, too. 

### Lossless Compression For WebP

Lossless compression does not degrade image quality the way lossy does. Instead, it achieves smaller file sizes by removing excess metadata from the backend of the file. This way, the quality of the image remains intact while reducing its size. That said, lossless compression can’t achieve the kinds of file sizes lossy compression can.

That was until WebP’s lossless compression came along.

You can see some beautiful examples of how WebP’s lossy and lossless compression stands up against PNG in [Google’s WebP galleries](https://developers.google.com/speed/webp/gallery ): 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3d84205-58e9-4190-9268-b57b8a89be02/image2-speed-up-your-website-webp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3d84205-58e9-4190-9268-b57b8a89be02/image2-speed-up-your-website-webp.png" sizes="100vw" caption="The Google WebP Galleries show how PNG images compare in quality and size to compressed WebPs. (Source: <a href='https://developers.google.com/speed/webp/gallery'>Google</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3d84205-58e9-4190-9268-b57b8a89be02/image2-speed-up-your-website-webp.png'>Large preview</a>)" alt="Google WebP Gallery comparison against PNG" >}}

If there’s any degradation in the quality of the WebP images, it’s going to be barely noticeable to your visitors. The only thing they’re really going to notice is how quickly your site loads. 

## What Are The Advantages Of Using WebP?

It’s not enough to say that WebP is “better” than JPG and PNG. It’s important to understand the mechanics of how WebP works and why it’s so beneficial to use over other file formats as a result.

With traditional image formats, compression always results in a tradeoff. 

JPG lossy compression leads to degradation of the clarity and fineness of an image. Once applied, it cannot be reversed. 

WebP lossy compression, on the other hand, uses what’s known as prediction coding to more accurately adjust the pixels in an image. As Google explains, [there are other factors at work](https://developers.google.com/speed/webp/docs/compression), too: 

<blockquote>“Block adaptive quantization makes a big difference, too. Filtering helps at mid/low bitrates. Boolean arithmetic encoding provides 5%-10% compression gains compared to Huffman encoding.”</blockquote>

**On average, Google estimates that WebP lossy compression results in files that are between 25% and 34% smaller than JPGs of the same quality.**

As for PNG lossless compression, it does work well in maintaining the quality of an image, but it doesn’t have as significant an impact on image size as its JPG counterpart. And certainly not when compared to WebP.

WebP handles this type of compression more efficiently and effectively. This is due to the variety of compression techniques used as well as entropy encoding applied to images. Again, Google explains how it works:

<blockquote>“The transforms applied to the image include spatial prediction of pixels, color space transform, using locally emerging palettes, packing multiple pixels into one pixel and alpha replacement.”</blockquote>

**On average, Google estimates that WebP lossless compression results in files that are roughly 26% smaller than PNGs of the same quality.**

That’s not all. WebP has the ability to do something that no other file formats can do. Designers can use WebP lossy encoding on RGB colors and lossless encoding on images with transparent backgrounds (alpha channel). 

Animated images, otherwise served in GIF format, also benefit from WebP compression systems. There are a number of reasons for this: 

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist"></th>
      <th>GIF</th>
      <th>WebP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Compression</td>
      <td>Lossless</td>
      <td>Lossless + lossy</td>
    </tr>
    <tr>
      <td>RBG Color Support</td>
      <td>8-bit</td>
      <td>24-bit</td>
    </tr>
    <tr>
      <td>Alpha Channel Support</td>
      <td>1-bit</td>
      <td>8-bit</td>
    </tr>
  </tbody>
</table>

As a result of this powerful combo of lossless and lossy compression, animated videos can get down to much smaller sizes than their GIF counterparts. 

**Google estimates the average reduction to be about 64% of the original size of a GIF when using lossy compression and 19% when using lossless.**

{{% pull-quote %}}
 Needless to say, there’s nothing that can beat WebP when it comes to speed while maintaining image integrity.
{{% /pull-quote %}}

## Acceptance Of WebP Among Browsers, Devices And CMS

As you can imagine, when WebP was first released, it was only supported by Google’s browsers and devices. Over time, though, other platforms have begun to provide support for WebP images. 

That said, [WebP still doesn’t have universal support](https://www.keycdn.com/support/webp-browser-support), which can cause problems for web designers who use this image format by default. 

Let’s take a look at where you can expect full acceptance of your WebP images, where you won’t and then we’ll discuss what you can do to get around this hiccup. 

As of writing this in 2019, [Can I use…](https://caniuse.com/#feat=webp) has accounted for the following platforms that support WebP:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ee3808d-0f2e-4838-b3ee-8d48470b9fec/image4-speed-up-your-website-webp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ee3808d-0f2e-4838-b3ee-8d48470b9fec/image4-speed-up-your-website-webp.png" sizes="100vw" caption="‘Can I Use’ breaks down which browsers and versions of those browsers provide support for WebP. (Source: <a href='https://caniuse.com/#feat=webp'>Can I use...</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ee3808d-0f2e-4838-b3ee-8d48470b9fec/image4-speed-up-your-website-webp.png'>Large preview</a>)" alt="‘Can I Use’ data on WebP support" >}}

The latest versions of the following platforms are supported: 

*   Edge
*   Firefox
*   Chrome
*   Opera
*   Opera Mini
*   Android Browser
*   Opera Mobile
*   Chrome for Android
*   Firefox for Android
*   UC Browser for Android
*   Samsung Internet
*   QQ Browser
*   Baidu Browser

The platforms that continue to hold back support are: 

*   Internet Explorer
*   Safari
*   iOS Safari
*   KaiOS Browser

It’s not just browsers that are on the fence about WebP. Image editing software and content management systems are, too. 

[ImageMagick](https://imagemagick.org/script/webp.php), [Pixelmator](https://www.pixelmator.com/blog/2010/10/06/pixelmator-1-6-2-adds-webp-support/) and [GIMP](https://www.gimp.org/news/2018/04/27/gimp-2-10-0-released/) all support WebP, for instance. [Sketch](https://www.sketch.com/docs/exporting/file-formats/) enables users to export files as WebP. And for software that doesn’t natively support WebP, like Photoshop, users can usually [install a plugin](https://developers.google.com/speed/webp/docs/webpshop) which will allow them to open and save files as WebP. 

Content management systems are in a similar spot. Some have taken the lead in moving their users over to WebP, whether they uploaded their files in that format or not. [Shopify](https://changelog.shopify.com/posts/online-stores-automatically-serve-webp-images) and [Wix](https://support.wix.com/en/article/images-and-site-performance) are two site builders that automatically convert and serve images in WebP format.

Although there are other platforms that don’t natively support WebP, there are usually extensions or plugins you can use to upload WebP images or convert uploaded ones into this next-gen format. 

[WordPress](https://wordpress.org/) is one of those platforms. Drupal is another popular CMS that provides users with WebP [modules](https://www.drupal.org/project/webp) that add WebP support. [Magento](https://www.yireo.com/software/magento-extensions/webp) is yet another. 

It’s pretty rare not to find some sort of add-on support for WebP. The only example that I’m aware of that doesn’t accept it is [Squarespace](https://support.squarespace.com/hc/en-us/articles/206542517-Formatting-your-images-for-display-on-the-web).

## Challenges Of Converting And Delivering WebP

Okay, so WebP doesn’t have 100% support on the web. Not yet anyway. That’s okay. For the most part, we have some sort of workaround in terms of adding support to the tools we use to design and build websites. 

But what do we do about the browser piece? If our visitors show up on an iOS device, how do we make sure they’re still served an image if our default image is WebP? 

First, you need to know how to convert images into WebP. 

Last year, front end developer Jeremy Wagner wrote up [a guide for Smashing Magazine](https://www.smashingmagazine.com/2018/07/converting-images-to-webp/) on this very topic. In it, he covers how to convert to WebP using: 

*   Sketch,
*   Photoshop,
*   The command line,
*   Bash,
*   Node.js,
*   gulp,
*   Grunt,
*   webpack.

Any of these options will help you convert your PNGs and JPGs into WebPs. Your image editing software will only get you halfway to your destination though. 

It’ll handle the conversion, but it won’t help you modify your origin server so that it knows when to deliver WebPs and when to deliver a traditional image format to visitors. 

Some of these methods let you dictate how your server delivers images based on the restraints of your visitors’ browsers. Still, it takes a bit of work to modify the origin servers to make this happen. If you’re not comfortable doing that or you don’t want to deal with it, KeyCDN has a solution.

## The Solution: Simplify WebP Delivery With KeyCDN

[KeyCDN](https://www.keycdn.com/) understands how important it is to have a website that loads at lightning-fast speeds. It’s what KeyCDN is in the business to do. That’s why it’s no surprise that it’s developed a built-in WebP caching and image processing solution that helps developers more easily deliver the right file formats to visitors. 

### What Is WebP Caching?

Caching is an integral part of keeping any website running fast. And WebP caching is only going to make it better. Essentially, it’s a form of content negotiation that takes place in the HTTP header. 

It works like this: 

Someone visits a website that has KeyCDN’s WebP caching enabled. The visitor’s browser sends an <code>accept</code> HTTP header as part of the request to the server with a list of asset types it prefers. But rather than go to the origin server (at the web host), the request is processed by the edge server (at KeyCDN). The edge server reviews the list of acceptable file types and sends a <code>content-type</code> header in response. 

Here’s an example of how that might look: 

<div class="break-out">

 <pre><code class="language-bash">curl -I 'https://ip.keycdn.com/example.jpg' -H 'accept: image/webp'
HTTP/2 200
server: keycdn-engine
date: Thu, 06 Jun 2019 08:29:50 GMT
content-type: image/webp
content-length: 56734
last-modified: Tue, 14 May 2019 23:36:28 GMT
etag: "5cdb50fc-1040a"
expires: Thu, 13 Jun 2019 08:29:50 GMT
cache-control: max-age=604800
x-ip: 1
x-ip-info: osz=56734 odim=700x467 ofmt=webp
x-cache: HIT
x-shield: active
x-edge-location: chzh
access-control-allow-origin: *
accept-ranges: bytes
</code></pre>
</div>

<p><em>An example of a content-type request that KeyCDN sends to browsers that accept WebP. (Source: <a href="https://www.keycdn.com/blog/webp-caching">KeyCDN</a>)</em></p>

So, for Google Chrome visitors, the <code>content-type: image/webp</code> would automatically be accepted and the cached WebP assets would be delivered to the browser. 

For Safari users, on the other hand, the request would go unaccepted. But that’s okay. Your CDN will know which file format to send instead. In the first line in the example above, you can see that the original image format is JPG, so that’s the version of the file that would be delivered.

As you can see, there’s no need to modify the origin server or prepare multiple versions of your files in order to account for WebP compatibility. KeyCDN WebP caching handles all of it. 

### How Do You Use KeyCDN WebP Caching? 

There are two ways in which KeyCDN users can take advantage of the WebP caching feature.

#### Image Processing Through KeyCDN

The first requires nothing more than flipping a switch and turning on [KeyCDN’s image processing](https://www.keycdn.com/support/image-processing). Once enabled, the <code>accept</code> request header will automatically load. 

You can, of course, use the image processing service for more than just WebP caching. You can use it to adjust the size, crop, rotation, blur, and other physical attributes of your delivered images. But if you’re trying to simplify your image delivery system and simply want to speed things up with WebP, just enable the feature and let KeyCDN do the work. 

#### WebP Caching Through Your Origin Server

Let’s say that you generated your own WebP image assets. You can still reap the benefits of KeyCDN’s WebP caching solution. 

To do this, you’ll need to correctly generate your WebPs. Again, here’s [a link to the guide](https://www.smashingmagazine.com/2018/07/converting-images-to-webp/) that shows you how to do that. 

It’s then up to you to configure your origin server so that it only delivers WebPs when `accept: image/webp` is present. KeyCDN provides some examples of how you’ll do this with Nginx: 

<pre><code class="language-bash"># http config block
map $http_accept $webp_ext {
    default "";
    "~*webp" ".webp";
}

# server config block
location ~* ^(/path/to/your/images/.+)\.(png|jpg)$ {
    set $img_path $1;
    add_header Vary Accept;
    try_files $img_path$webp_ext $uri =404;
}
</code></pre>

<p><em>KeyCDN demonstrates how you can modify the origin server with Nginx to deliver your own cached WebP assets. (Source: <a href="https://www.keycdn.com/blog/webp-caching">KeyCDN</a>)</em></p>

And with Apache: 

<div class="break-out">

 <pre><code class="language-bash">&lt;IfModule mod_rewrite.c&gt;
    RewriteEngine On
    RewriteCond %{HTTP_ACCEPT} image/webp
    RewriteCond %{DOCUMENT_ROOT}/$1.webp -f
    RewriteRule ^(path/to/your/images.+)&#92;.(jpe?g|png)$ $1.webp [T=image/webp,E=accept:1]
&lt;/IfModule&gt;

&lt;IfModule mod_headers.c&gt;
    Header append Vary Accept env=REDIRECT_accept
&lt;/IfModule&gt;

AddType image/webp .webp
</code></pre>
</div>

<p><em>KeyCDN demonstrates how you can modify the origin server with Apache to deliver your own cached WebP assets. (Source: <a href="https://www.keycdn.com/blog/webp-caching">KeyCDN</a>)</em></p>

Obviously, this option gives you more control over managing your image formats and how they’re served to visitors. That said, if you’re new to using WebP, KeyCDN’s automated WebP caching and image processing is probably your best bet.

#### An Alternative For WordPress And Magento Designers

If you design websites in WordPress or Magento, KeyCDN has plugins you can use to add WebP support and caching. 

For WordPress, you’ll use KeyCDN’s custom [Cache Enabler](https://wordpress.org/plugins/cache-enabler/) along with [Optimus](https://optimus.io/en/). 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d81b861-a6bf-4370-b393-6f5a49ba60e5/image5-speed-up-your-website-webp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d81b861-a6bf-4370-b393-6f5a49ba60e5/image5-speed-up-your-website-webp.png" sizes="100vw" caption="The Cache Enabler plugin offers delivery support for WebPs in WordPress. (Source: <a href='https://wordpress.org/plugins/cache-enabler/'>Cache Enabler</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d81b861-a6bf-4370-b393-6f5a49ba60e5/image5-speed-up-your-website-webp.png'>Large preview</a>)" alt="Cache Enabler plugin from KeyCDN" >}}

Cache Enabler checks to see if your images have a WebP version. If it exists and the visitor’s browser supports it, that’s what it will deliver in the cached file. If it doesn’t exist, then it’ll simply turn to the JPG, PNG or GIF that’s there.

Magento developers have a simplified workaround for converting and delivering WebP, too. First, you’ll need to install the [Webp extension](https://www.yireo.com/software/magento-extensions/webp). Then, you’ll have to configure the WebP binaries on your server.

## Wrapping Up

There’s a reason why Google went to the trouble of developing a new image format and why more and more browsers, design systems and content management systems are supporting it. 

Images can cause a lot of problems for websites that have otherwise been built to be lean and mean. If they’re not uploaded at the right size, if they’re not compressed and if caching isn’t enabled, your images could be the reason that your website’s speed is driving visitors away. 

But with WebP, your website is sure to load more quickly. What’s more, there doesn’t need to be a tradeoff between image quality (or quantity!) in order to gain that speed. WebP efficiently compresses files while preserving the integrity of the image content. 

If you’re really struggling to increase the speed of your website then WebP should be the next tool you turn to for help. 

{{< signature "ms, ra, il" >}}

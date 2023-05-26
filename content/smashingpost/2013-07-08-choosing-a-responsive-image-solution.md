---
title: Choosing A Responsive Image Solution
slug: choosing-a-responsive-image-solution
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4ba22f6-0587-426c-859b-46d5a36344a8/picnic-without-art-direction-mini.jpg
date: 2013-07-08T08:40:20.000Z
author: sherri-alexander
description: >-
  If you code websites, it’s a good bet that at least one of your clients has
  asked about or requested a mobile-friendly website. If you go the responsive
  design route (whereby your website is flexible enough to adjust visually from
  mobile to desktop widths), then you’ll need a strategy to make images
  flexible, too — a responsive image solution.
categories:
  - Mobile
  - Techniques
  - jQuery
  - Responsive Design
---
If you code websites, it’s a good bet that at least one of your clients has asked about or requested a mobile-friendly website. If you go the responsive design route (whereby your website is flexible enough to adjust visually from mobile to desktop widths), then you’ll need a strategy to make images flexible, too — a responsive image solution.

The basics are fairly simple to learn, but once you’ve mastered them, you’ll find that scaling images is only the beginning — you might also have performance and art direction conundrums to solve. You’ll be faced with a wide field of responsive image solutions to choose from, each with its own strengths and weaknesses -- and none of them is perfect! This article leads you through the basics, and then arms you with the information you’ll need to <strong>pick the best responsive image solution for your situation</strong>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [One Solution To Responsive Images](https://www.smashingmagazine.com/2014/02/one-solution-to-responsive-images/)
*   [Simple Responsive Images With CSS Background Images](https://www.smashingmagazine.com/2013/07/simple-responsive-images-with-css-background-images/)
*   [How To Solve Adaptive Images In Responsive Web Design](https://www.smashingmagazine.com/2013/06/clown-car-technique-solving-for-adaptive-images-in-responsive-web-design/)
*   [Responsive Images In WordPress With Art Direction](https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/)

## The Basics

Styling foreground images to adjust to the width of their container is very easy. In your style sheet, perhaps in your normalize or reset style sheet, you’d add the following code:
<pre class="language-css"><code class="language-css">img {
    max-width: 100%;
}</code>
</pre>

In most cases, that tiny style rule will do the trick! Once it’s in place, if the container around the image becomes narrower than the width of the image, then the image will scale down to match the width of its container. Setting the <code>max-width</code> to <code>100%</code> also <strong>ensures that the image does not scale larger than its actual size</strong>, which would significantly reduce the image’s quality. If you’re still stuck providing support for IE 6 or 7, you’ll want to add a <code>width: 100%</code> style rule targeted only to those browsers, because they don’t understand <code>max-width</code>.

{{% feature-panel %}}

High-resolution “Retina” images can make this basic implementation a bit tricky. Let’s say you want your 150 × 150-pixel logo to display at double the usual pixel density, and the image is small enough that having two separate versions wouldn’t be a problem. So, you create a 300 × 300-pixel version of the logo and plug it in — and now it’s huge! Your first inclination is probably to try something like this in CSS:
<pre class="language-css"><code class="language-css">img.sitelogo {
    max-width: 150px;
}</code>
</pre>

Unfortunately, this doesn’t work as expected — the logo image will now refuse to scale nicely with the other images on the page.

To limit the maximum width of an adaptive image, you’d have to <strong>limit the maximum width of the image’s container</strong>, rather than of the image itself! Let’s say you’ve wrapped your logo image in a module with a class of <code>branding</code>. Here is the style that will do the trick:
<pre class="language-css"><code class="language-css">.branding {
    max-width: 150px;
}</code>
</pre>

So, now we have scalable responsive images in our website’s fluid layout. Mission accomplished. Time to go find out what this strange “outdoors” place has to offer to a sun-starved developer, right?

Not so fast! We still have two main challenges to overcome.</p>

## The Performance Problem

With the responsive image solution outlined above, all devices are fed the same images. Small icons and logos might not be too bad, but the problem compounds quickly as the images get larger and heftier. Retina images exacerbate the problem — you don’t want to send a big Retina image to a device that isn’t capable of displaying its full detail!

Think about it. Should we really be sending a 990 × 300-pixel 100 KB image meant for desktop viewers to a mobile phone? Sure, the mobile visitor might be on their local coffee shop’s Wi-Fi connection — however, they might be on the road trying to get crucial information from your website, with one shaky bar of wireless service. Every mobile user who gives up when your page takes too long to load is a potential customer lost!

Many mobile websites that are just as big or bigger than their desktop counterparts can be found in the wild today. <a href="https://twitter.com/guypod">Guy Podjarny</a> ran some tests a year apart, and there hasn’t been much improvement: in 2011, 86% of websites were the same size or larger, and in 2012 that number went down to 72%, but the overall sizes of websites increased. Dave Rupert also captured the problem beautifully in his article “<a href="https://alistapart.com/article/mo-pixels-mo-problems">Mo’ Pixels Mo’ Problems</a>.”

### Complicating It Further: Browser Preloading

When I first began wrestling with performance issues on responsive websites, my initial thought was to put all of the image variations on the page, and set up some CSS classes with media queries that would hide big images and show small images at small widths, and vice versa at desktop widths. It seemed logical: shouldn’t the browser only download the visible images?

The problem is that browsers are too quick for us! In order to provide the fastest loading time possible, <strong>browsers preload all of the images that they can identify</strong> in the source code before any CSS or JavaScript is processed. So, this approach would actually penalize mobile visitors <em>more</em>, by forcing them to download <em>all</em> of an image’s variants!

Because of this preloading, most solutions require either a back-end solution (to preempt the preloading) or special markup and JavaScript.</p>

### Bandwidth Detection

The last piece of the performance puzzle is network speed. We know that we want to feed only the large images to devices that are on a speedy network, but how do we determine that? A few techniques are out there to estimate network speed, but they aren’t foolproof yet.

The W3C has been working on a <a href="https://www.w3.org/TR/netinfo-api/">Network Information API</a>, which could be very helpful in future, but currently it’s supported by only a handful of devices (and not the big ones, unfortunately). It is currently implemented in a few responsive image solutions, but I don’t expect it to be widely adopted until it’s more widely supported. <a href="https://www.smashingmagazine.com/2013/01/09/bandwidth-media-queries-we-dont-need-em/">Network measurements are difficult</a> and as Yoav Weiss states in his Smashing Magazine's article, reliable "bandwidth media queries" don’t seem to be something that can be accurately implemented in the near future.</p>

<a href="https://github.com/adamdbradley/foresight.js">Foresight.js</a> by <a href="https://twitter.com/adamdbradley">Adam Bradley</a> uses JavaScript to test how long the browser takes to download a 50K image, then stores that information and uses it to make bandwidth decisions. It does have a few small drawbacks: it does add a 50K image download to your page, and it can block download of other images on your page until the test image download is complete. Many of the responsive image solutions that currently implement bandwidth detection use a variation or adaptation of Foresight.js.</p>

## The “Art Direction” Problem

Let’s say you’ve got a beautiful wide image on your home page. It shows a wide bucolic expanse of fields and forest, blue sky and fluffy clouds above, and a happy family having a picnic on the grass.

Now scale it down to 300 pixels wide, mobile-style. At this scale, our vacationing family looks more like the ants at the picnic!

<figure><a href="https://www.flickr.com/photos/tingy/32067554/in/photostream/"><img loading="lazy" decoding="async" class="136841" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6103f576-92ae-418f-ba4d-a54d74063366/picnic-without-art-direction-mini.jpg" alt="" width="500" height="544" /></a><figcaption>Detail is lost when this large image is scaled down. (Image: <a href="https://www.flickr.com/photos/tingy/32067554/in/photostream/">Mark McQuitty</a>)</figcaption></figure>

Herein lies what we call the “art direction” problem. Some images just don’t scale well; fine detail is lost, and dramatic impact is reduced. In the case of our hero image, it would be much nicer visually if the mobile version of the photo was zoomed in, cropped and focused on our happy family. To solve this problem, we need a responsive image solution that enables you either to specify different versions of the image for different situations or to adjust the image on the fly.</p>

<figure><a href="https://www.flickr.com/photos/tingy/32407984/in/photostream/"><img loading="lazy" decoding="async" class="136840" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5a0584c-d7e0-454b-aad7-b5f0dbd0563a/picnic-with-art-direction-mini.jpg" alt="" width="500" height="544" /></a><figcaption>Sometimes a different crop or zoom of the image is desirable for narrow widths. (Images: <a href="https://www.flickr.com/photos/tingy/32407984/in/photostream/">Mark McQuitty</a>)</figcaption></figure>

## Choosing Your Solution

Luckily, the web development and design community has no shortage of creative, smart people who have been working to solve these problems. Of course, the flip side of that coin is that it’s easy to get overwhelmed by the sheer number of responsive image solutions out there. How do you decide which is best for you?

Choosing between them can be an extremely complicated matter, because so many factors come into play. No current solution is perfect for every situation; each was <strong>designed to solve a particular set of problems</strong>. To decide, you’ll need to weigh each solution against your project’s particular needs. Chris Coyier has done a great job of <a href="https://css-tricks.com/which-responsive-images-solution-should-you-use/">summarizing the deciding factors</a> (including a spreadsheet to track them all, although some newer solutions aren’t mentioned).

Here are some factors to consider:

*   Do you need to solve the art direction problem (i.e. different image ratios, crops and sizes for different widths)?
*   Do you have a huge website or a CMS on which going back to add special markup to every image is not feasible?
*   Are all images present upon the page loading, or are some images loaded dynamically via JavaScript?
*   Do you want to test for the user’s bandwidth to determine whether their connection is fast enough to handle high-resolution images?
*   Does the solution require a platform that is unavailable to you (such as jQuery or PHP)?
*   Is a third-party solution acceptable, or do you need to keep the solution hosted in-house?

With this in mind, let’s look at some responsive image solutions that have been out there for a while and that are widely used within the developer community.</p>

<strong>Please note:</strong> The list of solutions below is by no means comprehensive. They are the ones either that I’ve found most useful personally or that have proven track records for reliability. Have a favorite solution of your own that’s not here? Let us know in the comments!

## Tried And True Responsive Image Solutions

### Picturefill

The Web is truly worldwide, and we have to confront the fact that not everyone has access to fiberoptic connections and 4G networks. <a href="https://twitter.com/scottjehl">Scott Jehl</a> encountered this digital divide first-hand while travelling and working his way through Southeast Asia, and he is a strong advocate of mobile-first and responsive websites that don’t put an undue burden on mobile users. His <a href="https://github.com/scottjehl/picturefill">Picturefill</a> script is a polyfill for the proposed <code>&lt;picture&gt;</code> element — JavaScript code that mimics the picture API, enabling us to use it on our websites today. The future is now, baby!

<figure><img loading="lazy" decoding="async" class="136845" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0cc7cd8-65e6-4bd4-820d-61dfe89d8d1a/solution-picturefill-mini.jpg" alt="" width="500" height="350" /></figure>

Picturefill does not require jQuery, but obviously it does require the <code>picturefill.js</code> script to be included somewhere in the page. Picturefill also <strong>requires some special markup</strong>, with divs to represent the image variations, differentiated by <code>data-media</code> attributes that act just like media queries in CSS. You may also optionally put an image in conditional comments for browsers that don’t support media queries (I’m looking at you, IE 8), and a fallback in a <code>&lt;noscript&gt;</code> tag for browsers that don’t have JavaScript enabled (I’m looking at you, BlackBerry).

Here’s an example of a typical Picturefill setup:
<pre class="language-markup"><code class="language-markup">&lt;span data-picture data-alt="Descriptive alt tag"&gt;
    &lt;span data-src="images/myimage_sm.jpg"&gt;&lt;/span&gt;
    &lt;span data-src="images/myimage_lg.jpg" data-media="(min-width: 600px)"&gt;&lt;/span&gt;

    &lt;!--[if (lt IE 10) &amp; (!IEMobile)]&gt;
    &lt;span data-src="images/myimage_sm.jpg"&gt;&lt;/span&gt;
    &lt;![endif]--&gt;

    &lt;!-- Fallback content for non-JS browsers. --&gt;
    &lt;noscript&gt;
        &lt;img src="images/myimage_sm.jpg" alt="Descriptive alt tag" /&gt;
    &lt;/noscript&gt;
&lt;/span&gt;</code>
</pre>

That’s all you need to display adaptive images at page-loading time using Picturefill. Drop in the script, configure the markup, and everything just works. You can also call Picturefill programmatically if you need to add images to the page on the fly.

Picturefill requires a lot of custom markup, so it might not be the best choice for those who cannot alter their website’s source code for any reason. It also doesn’t do any bandwidth detection. If bandwidth detection is important to your project, then have a look at this next solution.</p>

### HiSRC

<a href="https://github.com/teleject/hisrc">HiSRC</a>, by <a href="https://twitter.com/1marc">Marc Grabanski</a> and <a href="https://twitter.com/teleject">Christopher Schmitt</a>, is a jQuery plugin that enables you to create low-, medium- and high-resolution versions of an image, and the script will show the appropriate one based on Retina-readiness and network speed.</p>

<figure><a href="https://github.com/teleject/hisrc"><img loading="lazy" decoding="async" class="136843" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b55d40c-9f8d-4389-93c7-4b18ea45e20e/solution-hisrc-mini.jpg" alt="" width="500" height="350" /></a></figure>

To set it up, first make sure that jQuery and the HiSRC script is included somewhere on the page.

In your HTML code, first add a regular image tag to the page, and set the source to be the low-resolution (or smallest) version of the image. Add a class to the image or its wrapper (like <code>.hisrc</code>) to specify which images HiSRC should process. Then, add some special markup to your image tag: <code>data-1x</code> and <code>data-2x</code> attributes, pointing to the medium- and high-resolution versions, respectively. For example:
<pre class="language-markup"><code class="language-markup">&lt;img src="https://placekitten.com/200/100" data-1x="https://placekitten.com/400/200" data-2x="https://placekitten.com/800/400" class="hisrc" /&gt;</code>
</pre>

Then, after the DOM has loaded, just call the function on the image class that you’re using, like so:
<pre class="language-javascript"><code class="language-javascript">$(document).ready(function(){
  $(".hisrc").hisrc();
});</code>
</pre>

In practice, the browser will first load the image source — i.e. the mobile version of the image. Then, the script checks to see whether the visitor is using mobile bandwidth (such as 3G). If so, it leaves the mobile-first image in place. If the connection is speedy and the browser supports a Retina image, then the <code>@2x</code> version is delivered. If the connection is speedy but Retina is not supported, then the <code>@1x</code> version is delivered.

You might have noticed that the low-resolution image always loads, even if the script later decides that the user’s device is a good candidate for high resolution. Even though this is technically a double-download, it only penalizes those on speedy connections. I’m willing to accept that compromise!

HiSRC can handle images that are added to the page dynamically. It also allows for multiple images, so you can specify different crops and sizes to beat the art-direction problem.

As for weaknesses, HiSRC does require jQuery, so it won’t be useful unless you’re using that library. It also requires custom markup in the HTML, so it might not be the best choice if you have a huge website with a lot of legacy images or a CMS in which the output of the image tag can’t be altered. If that’s your situation, read on!

### Adaptive Images

Unlike the previous two scripts, <a href="https://adaptive-images.com/">Adaptive Images</a>, by <a href="https://twitter.com/MattWilcox">Matt Wilcox</a>, is mostly a server-side solution. It requires a tiny bit of JavaScript, but the real work is done via the Apache 2 Web server, PHP 5.x and the GD library.

To install it on your Web server, you’ll need to alter or add an <code>.htaccess</code> file, upload some PHP files to your website’s root directory, add some JavaScript to your pages (which will add a cookie to record the user’s screen resolution), and configure some breakpoint variables in the PHP files to match your website’s media queries.</p>

<figure><a href="https://adaptive-images.com/"><img loading="lazy" decoding="async" class="136842" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45bca813-6407-407e-96d2-93eb0804265d/solution-adaptiveimages-mini.jpg" alt="" width="500" height="350" /></a></figure>

The installation instructions are quite verbose — a bit too lengthy for the scope of this article. For more information, visit the official website and click the “Details” link at the top.

The best feature of Adaptive Images is that it <strong>requires no custom markup on any of your images</strong>. Once you’ve installed and configured it correctly, you’re all set! The PHP script will intercept any request for an image and will resize it on the fly as needed to your specified breakpoint sizes and serve it on your pages automatically.

The PHP has a lot of configurable options, such as image quality, breakpoints, caching, and even a sharpening filter to apply to the generated scaled images.

It has a few limitations:

*   Because it requires the combination of Apache and PHP, Adaptive Images might not match up with your website’s platform or be available on your Web host’s server.
*   It relies on the Web server’s ability to intercept any requests for images (via the `.htaccess` file). So, if your images are hosted elsewhere, such as on a content delivery network, then it won’t work.
*   It doesn’t detect bandwidth.
*   It’s not meant to solve the art direction problem, because it only rescales the original images. It can’t crop or create different aspect ratios from the original image.

You may have noticed that all of the solutions thus far require JavaScript, and often some detailed configuration. If you’re looking for one that doesn’t require JavaScript and that is fairly simple to implement, then have a look at this next one.</p>

### Sencha.io Src

Previously known as TinySrc, <a href="https://www.sencha.com/products/io/">Sencha.io Src</a> is a third-party solution that acts as a proxy for images, so you don’t need to configure anything on your server. Just point your image at Sencha’s servers (with or without some options specified), and Sencha will process it and send back a resized version as needed.</p>

<figure><a href="https://www.sencha.com/products/io/"><img loading="lazy" decoding="async" class="136847" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/694f2ea3-a339-4537-b7ca-56068396b4c5/solution-senchaio-mini.jpg" alt="" width="500" height="350" /></a></figure>

Let’s say you have a big image:
<pre class="language-markup"><code class="language-markup">&lt;img src="https://www.your-domain.com/path/to/image.jpg" alt="My large image" /&gt;</code>
</pre>

At its simplest, you’d just prefix the <code>src</code> attribute with <code>https://src.sencha.io/</code>, like so:
<pre class="language-markup"><code class="language-markup">&lt;img src="https://src.sencha.io/https://www.your-domain.com/path/to/image.jpg" alt="My large image" /&gt;</code>
</pre>

By default, Sencha.io will resize your image to fit the width of the device’s screen, using the user-agent string for detection. Phones might be sent a 320-pixel-wide image, tablets a 768-pixel-wide image, etc.

You can also configure the Sencha.io prefix string to return particular measurements, orientations, percentage sizes or any number of complex calculations.

Sencha.io is a free service for individual users and can be a very convenient adaptive image solution. However, you’re adding a third-party dependency, with the possibility of downtime and problems beyond your control. Weigh these risks carefully.</p>

## Responsive Image Solutions To Watch

The solutions outlined till now are usable today, but they’re not the only fish in the sea. Some newer solutions show a lot of promise, and I’m keeping a sharp eye on them to see how they evolve with current Web technology. Below are two in particular that you might want to watch.</p>

### Capturing/Mobify.js 2.0

<a href="https://www.mobify.com/mobifyjs/v2/docs/capturing/">Capturing</a> is a new feature of the in-development Mobify.js 2.0, which proposes to give you access to (or to “capture”) the HTML source markup <strong>before it is parsed or rendered by the browser</strong>. Accessing the source code at this stage enables you to swap an image’s <code>src</code> attribute before the browser downloads it. You can even craft a fallback to one of the other solutions, such as Picturefill, in case something fails.</p>

<figure><a href="https://www.mobify.com/mobifyjs/v2/docs/capturing/"><img loading="lazy" decoding="async" class="136844" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f362cf41-cb9c-4532-b50c-0c805435093f/solution-mobifyjs-mini.jpg" alt="" width="500" height="350" /></a></figure>

Since this technique directly circumvents native browser preloading, it is a bit controversial in web performance circles. If misused, it could actually create performance problems on a site instead of alleviating them!

The other thing holding me back from running to this solution with open arms is its cross-browser support. Capturing won’t work in any version of IE lower than 10, so IE 8 and 9 users will be left out in the cold. I’ll keep watching, though — down the road a ways, when IE 8 and 9 finally fade into the sunset, this solution might be more viable!

If you’re interested in finding out more about Capturing, the Mozilla team goes into more detail in its blog post, “<a href="https://hacks.mozilla.org/2013/03/capturing-improving-performance-of-the-adaptive-web/">Capturing: Improving Performance of the Adaptive Web</a>.”

### ReSRC.it

<a href="https://www.resrc.it/">ReSRC.it</a> is another third-party solution (recently out of beta) that delivers responsive images from the cloud. It seems to be very similar in implementation to Sencha.io Src, but adds image filters and bandwidth detection and doesn’t rely on user-agent detection or cookies.</p>

<figure><a href="https://www.resrc.it/"><img loading="lazy" decoding="async" class="136846" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40fb5e46-e089-4e60-92dd-daee276f8edb/solution-resrcit-mini.jpg" alt="" width="500" height="350" /></a></figure>

To get started, you first need to sign up for a trial account at ReSrc.it.

Second, you'll need to insert their Javascript file on your page (this is the simple JS code; they offer an asynchronous embed method as well to improve performance):
<pre class="language-markup"><code class="language-markup">&lt;script src="//use.resrc.it"&gt;&lt;/script&gt;</code>
</pre>

Then, suppose you have an image like this:
<pre class="language-markup"><code class="language-markup">&lt;img src="https://path/to/image.jpg" alt="My large image" /&gt;</code>
</pre>

You would prefix the image source’s URL with a path to ReSRC.it’s servers, and add a CSS class of "resrc" to the image. They currently have two servers, one for paid accounts and one for trial accounts — we’ll use the trial one for our example:
<pre class="language-markup"><code class="language-markup">&lt;img src="https://trial.resrc.it/https://www.your-domain.com/path/to/image.jpg" alt="My large image" class="resrc" /&gt;</code>
</pre>

ReSRC.it allows you to add parameters to the requested URL to perform operations on the image, such as rotating, cropping and flipping. This allows for quite a bit of flexibility and potentially addresses the art-direction problem. The parameters are processed in order from left to right and can be strung together.

Here’s an example of an image that’s being flipped horizontally, resized to 300-pixels wide, with the resulting image optimized to an 80%-quality JPEG:
<pre class="language-markup"><code class="language-markup">&lt;img src="https://trial.resrc.it/r=h/s=w300/o=80/https://www.your-site.co/image.jpg" alt="My large image" class="resrc" /&gt;</code>
</pre>

ReSRC.it is recently out of beta, so if anyone using the service has tips or advice (pro or con), we’d love to hear more about it in the comments.</p>

## Test, Test, Test!

After you’ve chosen and implemented a responsive image solution, testing the performance of your website is absolutely necessary to making sure that the solution is working well. Below are a few useful online testing tools to help you.</p>

### YSlow

Created by Yahoo, <a href="https://developer.yahoo.com/yslow/">YSlow</a> is a client-side tool that analyzes your website against 23 testable rules that Yahoo has determined can adversely affect Web page performance. YSlow awards your website a grade for each rule, explaining each one and suggesting how to improve your website’s performance. YSlow is available for Firefox, Chrome, Safari and Opera (as well as by a few other means, such as the command line).</p>

### WebPageTest

The online tool <a href="https://webpagetest.org">WebPageTest</a> is an open-source project maintained by Google. You enter your website’s URL, perform a speed test from a chosen location, and specify which browser to use. Advanced settings allow you to perform multi-step transactions, pick a network speed (cable, DSL, FiOS, etc.), disable JavaScript, block ads and make other requests, and more. The results come in the form of tables, charts, screenshots, a performance review and a lot of great data to dig into!

The Yottaa blog has an article detailing <a href="https://www.yottaa.com/test-results-performance-benefits-of-responsive-image-loadi/">how they used WebPageTest to test out their website both with and without responsive image loading</a> -- check it out!

## Conclusion

If you read Smashing Magazine, you’re probably already on board with creating the best possible website experience for your audience. So, the next time you craft a beautiful, usable experience for mobile visitors, try out one of these responsive image solutions and take your website the extra mile. Your mobile visitors will thank you!

### Delve Deeper

*   Jeremy Keith took some wonderful notes on Scott Jehl’s presentation “[Responsive and Responsible](https://adactio.com/journal/6052/)” at An Event Apart in Atlanta.
*   Jordan Moore has written a great article that goes deeper into [responsible considerations for responsive design](https://www.smashingmagazine.com/2013/03/11/responsible-web-design/).
*   Feeling confused and frustrated? It’s OK; we’re all figuring out this responsive design thing together! Josh Long exhorts us all to band together and share our experiences in “[I Have No Idea What I’m Doing With Responsive Web Design](https://blog.teamtreehouse.com/i-have-no-idea-what-im-doing-with-responsive-web-design).”
*   Want to take it further? Get involved! Join forces with the folks in the [Responsive Images Community Group](https://responsiveimages.org). You can also [follow them on Twitter](https://twitter.com/respimg).

{{< signature "al" >}}


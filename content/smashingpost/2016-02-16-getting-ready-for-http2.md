---
title: 'Getting Ready For HTTP2: A Guide For Web Designers And Developers'
slug: getting-ready-for-http2
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72e3ebe8-098f-49d3-8c7c-8dfa4d4f9b51/getting-ready-for-http2.png
date: 2016-02-16T18:30:54.000Z
author: rachel-andrew
description: >-
  A detailed look at the basics of HTTP/2 as they apply to web
  designers and developers. We'll look at the key features of the new
  protocol, browser and server compatibility, and detail the things you
  might need to think about as we see more adoption of HTTP/2.
categories:
  - Coding
  - Workflow
  - Browsers
  - Performance
  - Security
---
The Hypertext Transfer Protocol (HTTP) is the protocol that governs the connection between your server and the browsers of your website’s visitors. For the first time since 1999, we have a <strong>new version of this protocol</strong>, and it promises far faster websites for everyone.

In this article, we’ll look at the basics of HTTP2 as they apply to web designers and developers. I’ll explain some of the <strong>key features of the new protocol</strong>, look at browser and server compatibility, and detail the things you might need to think about as we see more adoption of HTTP2.</p>

## <span class="rh">Further reading</span> on Smashing: 

*   [Preload: What Is It Good For?](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/)
*   [Everything You Need To Know About AMP](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)
*   [Improving Smashing Magazine’s Performance](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)

By reading this article, you will get an overview of what to consider changing in your workflow in the short and long term. I’ll also include plenty of resources if you want to dig further into the issues raised. My aim is to give you enough of the background to be able to make good decisions as you plan your move to HTTP2.

{{% feature-panel %}}

## A Brief History Of HTTP

HTTP is an old protocol, <a href="https://www.w3.org/Protocols/HTTP/AsImplemented.html">initially defined in 1991</a>, with the last major revision — <a href="https://www.ietf.org/rfc/rfc2616.txt">HTTP/1.1</a> — published in 1999. Websites in 1999 were very different to the websites we develop today. In <a href="https://daniel.haxx.se/http2/"><em>http2 explained</em></a>, Daniel Sternberg notes that the amount of data now required to load the home page of an average website is 1.9 MB, with over 100 individual resources required to display a page — a “resource” being anything from an image or a font to a JavaScript or CSS file.

HTTP/1.1 does not perform well when retrieving the large number of resources required to display a modern website. As we’ll see later in this article, many of the performance best practices we know as web developers come from our coping with the limitations of HTTP/1.1.</p>

### SPDY

In 2009, two engineers at Google posted about a research project they had been working on named <a href="https://googleresearch.blogspot.co.uk/2009/11/2x-faster-web.html">SPDY</a>. This project addressed some of the issues in HTTP/1.1. SPDY set out to:

*   allow concurrent requests across a single TCP connection, known as _multiplexing_;
*   allow browsers to prioritize assets so that resources vital to the display of a page could be sent by the server first;
*   compress and reduce HTTP headers;
*   implement _server push_, whereby a server can push vital resources to the browser before being asked for them.

In addition, SPDY requires an encrypted (HTTPS) connection between the browser and server.

SPDY doesn’t replace HTTP; rather, it’s a <strong>tunnel for the protocol</strong> and modifies the way existing HTTP requests and responses are sent. It <strong>requires support from both the server and the browser</strong> connecting to that server. With support available in NGINX and packages available from Google to enable support in Apache, there was a reasonable amount of adoption of SPDY. Browser support is pretty good, too, with <a href="https://caniuse.com/#feat=spdy">modern versions of all major browsers</a> supporting it.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d16c0265-d04a-4d48-8912-9e74fe58111a/01-caniuse-spdy-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a871fd5-c1ed-40f0-b3bb-36b2bc830094/01-caniuse-spdy-preview-opt.png" alt="SPDY browser support information on Can I Use" /></a><figcaption>SPDY browser support information on Can I Use. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d16c0265-d04a-4d48-8912-9e74fe58111a/01-caniuse-spdy-opt.png">View large version</a>)</figcaption></figure>

### HTTP2

We’ve seen SPDY enjoy some success, gaining adoption with both servers and browsers. However, you might also have spotted that, despite Internet Explorer 11 being supported, Microsoft’s Edge browser has dropped it. What’s happening here?

Support for SPDY has been dropped in Edge due to Microsoft implementing support for HTTP2, the latest version of the HTTP protocol. While other current browsers still maintain support for SPDY, Chrome will remove support in 2016, and other browsers will likely follow. At the time of writing, Edge, Firefox, Chrome and Opera support both SPDY <em>and</em> HTTP2. Safari, including on iOS, will join that group later this year with the launch of Safari 9.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f612102-d6f7-4719-b35b-b211baea64e8/02-caniuse-http2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae972261-e9c1-4329-970a-84bf19772075/02-caniuse-http2-preview-opt.png" alt="SPDY browser support information on Can I Use" /></a><figcaption>SPDY browser support information on Can I Use. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f612102-d6f7-4719-b35b-b211baea64e8/02-caniuse-http2-opt.png">View large version</a>)</figcaption></figure>

HTTP2 builds on the success of SPDY, which was used as a starting point for the new protocol. As such, the majority of SPDY’s objectives are <a href="https://http2.github.io/faq/#what-are-the-key-differences-to-http1x">met in HTTP/2</a>. The requirement for an HTTPS connection <a href="https://http2.github.io/faq/#does-http2-require-encryption">has been dropped</a>. That said, all of the browser vendors have decided to only implement HTTP2 for TLS (https) connections. So while you could potentially use HTTP/2 with clear text in server to server communications, our use case of serving HTTP2 to browsers means that you need to have your site running on https before you can even think of moving to HTTP2.

The HTTP2 specification was finalized in February 2015; a year on, browser support in modern browsers is excellent. As with SPDY, HTTP2 requires support both on the browser and server level, and there are already many web server implementations. You can keep track of these on the <a href="https://github.com/http2/http2-spec/wiki/Implementations">HTTP/2 wiki</a>. W3Techs also has a post from July 2015 <a href="https://w3techs.com/blog/entry/http2_adoption_is_still_low_at_0_4_but_growing_fast_thanks_to_litespeed">detailing adoption rates</a>. Adoption of this protocol is happening rapidly, considering how relatively new it is.

## Will We Have To Change Our Websites?

<strong>HTTP/2 is backwards-compatible with HTTP/1.1</strong>, so it would be possible to ignore it completely and everything will continue to work as before. The protocol change is completely transparent to users. Many readers of this article will have been using a protocol other than HTTP/1.1 for years. If you have a Gmail account and use Chrome to access it you will have been using SPDY and then HTTP/2 without knowing anything about it.

However, many of the things you think of as being best practices can be detrimental to performance under HTTP/2. Over time, as more servers update to use HTTP/2 and more people have browsers that support HTTP/2, your website, at one time well optimized according to best practices, will start to seem slower than websites optimized for the new protocol.</p>

## What Do We Need To Change To Embrace HTTP/2?

In the rest of this article, we’ll look at some of the common best practices that will <strong>become anti-patterns as HTTP/2 is adopted</strong>. As we’ve seen, the transition will be a slow one for many websites. To move to HTTP/2, your server software will need to be updated to support the protocol — which may be easy or almost impossible depending on how you are being hosted.

Before making changes to your website specifically for HTTP/2, you’ll also need to consider whether your visitors tend to have browsers that support it. Owners of websites that attract a lot of people using very up-to-date browsers will be able to make that switch sooner than owners whose logs show a majority of users on older browsers. To reflect this, I’ll also give you some suggestions on how to work in this transition time.</p>

### Make the Move to TLS

For a lot of websites the hardest thing about moving to HTTP/2 may not be HTTP/2 at all, but instead the requirement to run the site over a secure connection. If you are developing a new site or updating an old one your first move should be to make sure that you launch on or move to https as soon as possible. This is important not just for HTTP/2, Google uses <a href="https://googlewebmastercentral.blogspot.co.uk/2014/08/https-as-ranking-signal.html">secure connections as a ranking signal</a>, and browsers are starting to flag non-https websites as 'not secure'. In the future you will find that some powerful HTML5 features, such as geolocation, <a href="https://code.google.com/p/chromium/issues/detail?id=464874">are unavilable without a secure connection</a>.

If you have a site that is currently http only then my suggestion would be to prioritize a move to https first and then decide on your HTTP/2 strategy.</p>

### Turning Multiple Image Files Into Sprites

In HTTP 1.1, retrieving one large image is much more efficient for the browser than making a lot of requests for small ones. This is because multiple requests queue up behind each other. To work around this, we have been advised to turn our little icons into a <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/CSS_Image_Sprites">sprite file</a>.

The resulting sprite is returned with one HTTP request, preventing the problem of multiple requests being queued. However, even if the visitor is on a page that shows only one of those icons, they will still have to download a much larger file than they need to in order to see that one image.

With the <strong>multiplexing ability of HTTP/2</strong>, this queuing of resources is no longer an issue. Serving the small images individually will be better in many cases; you will only need to serve what is required for the page that the visitor is on. Creating a sprite will still be warranted in some cases; HTTP requests are only one aspect of performance. Combining some images together in a sprite might achieve better compression and, thus, a smaller download size overall, especially if all of those images are used on the page being loaded. However, it will no longer be the case that a sprite is always the best choice.</p>

### Inlining Images Using Data URIs

Another workaround for the problem of multiple HTTP requests in HTTP/1.1 is to <a href="https://css-tricks.com/data-uris/">inline images in CSS using data URIs</a>. Embedding images in this way will make a style sheet much larger. If you have combined this with another optimization technique for concatenating assets, then a visitor will likely download all of this code even if they never visit the pages where the images are being used.

With HTTP requests being very cheap in HTTP/2, this “best practice” will hinder rather than help performance.</p>

### Concatenating CSS And JavaScript

As the final step in our build process, many of us will concatenate all of the small CSS and JavaScript files used on our website. We often want to keep these separated while developing to make it easier to manage these resources — but we know that delivering one file to the browser is more efficient for performance than delivering five. Once again, we are trying to limit HTTP requests.

If you are doing this, then a visitor who lands on your home page might download all of the CSS and JavaScript required for your website, even if they never use most of it. As a developer, you can get around this problem by carefully selecting and including specific files for each area of the website in your build process, but that can be quite a lot of work.

An additional issue with concatenation is that everything will need to be purged from the cache at once. You can’t give some files that never change a long expiry date while giving often changing parts of the code base a shorter date. It all has to be expired if even one line of CSS, used on a single page, is changed.

I imagine you see where this is going! <strong>HTTP requests are cheap in the world of HTTP/2</strong>. Organizing your assets during development according to the pages on which they will be used will be far better. You can then serve up only the code that the visitor needs. Downloading a lot of tiny style sheets won’t matter. You could also organize based on how frequently things change; assets with longevity could then be cared for longer.</p>

### Splitting Resources Between Hosts: Sharding

With HTTP/1.1, you are restricted to the number of open connections. If loading a large number of resources is unavoidable, one method to get around this restriction is to retrieve them from multiple domains. This is known as <a href="https://www.stevesouders.com/blog/2009/05/12/sharding-dominant-domains/">domain sharding</a>. This can achieve better loading times, yet can <a href="https://calendar.perfplanet.com/2013/reducing-domain-sharding/">cause problems itself</a>, not to mention the development overhead of preparing this for your website.</p>

<strong>HTTP/2 removes this need for domain sharding</strong> because you can request as many resources as you need. In fact, this technique will likely hurt performance because it creates additional TCP connections and hinders HTTP/2 from prioritizing resources.</p>

## How To Prepare For HTTP/2 Now

If you are starting a project that you expect to have some longevity but cannot launch of HTTP/2 perhaps due to server support, it would be worth considering how you can prepare for HTTP/2. You could add a few things to your build process now that will make the switch easier later on.</p>

### Create Individual Assets in Addition to Sprites and Data URIs

If you are creating sprites, add to your process the creation and optimization of those individual assets as well, or smaller page-specific sprites if you feel performance would be best enhanced by these. This will make it easier for you to switch from big sprites to small (or no) sprites when the tipping point for your website is reached.

The same is true for data URIs. If you are currently using these in your CSS, have the images ready for when you switch away from this technique.</p>

### Organize Your Assets By Website Section

With CSS and JavaScript concatenation, there is a temptation to optimize for ease of development because the files will all get squashed together anyway. When you switch over to HTTP/2, you will <strong>get the best performance by carefully managing resources</strong> so that only the things needed by a certain page are delivered to that page. Therefore, starting to organize your development in this way now will pay off. For now, you may well still concatenate, and when the tipping point is reached, you can stop that part of your build process and serve the resources individually.</p>

### Manage Domain Sharding

The current best practice for HTTP/1.1 is to limit sharding to two host names. There is a way to get HTTP/2 to coalesce the connections, if the TLS certificate is valid for both hosts and the hosts resolve to the same IP. Since browser implementors require HTTP/2 to be running over HTTPS, it's <strong>necessary to get the TLS certificate</strong> to run over HTTP/2. See more on <a href="https://docs.google.com/presentation/d/1r7QXGYOLCh4fcUq0jDdDwKJWNqWK1o4xMtYpKZCJYjM/present#slide=id.g40fbe7d8c_076">slide 26</a> of Ilya Grigorik’s slidedeck from the Velocity Conference.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75af4190-f376-48b2-9bab-626052fa4edc/03-domain-sharding-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fedd07e6-ee85-43b6-9e72-561113db34c2/03-domain-sharding-preview-opt.png" alt="Slide from Ilya Grigorik's presentation" /></a><figcaption>Slide from Ilya Grigorik’s presentation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75af4190-f376-48b2-9bab-626052fa4edc/03-domain-sharding-opt.png">View large version</a>)</figcaption></figure>

### More To Come

Ultimately, we’ll get a whole slew of best practices for HTTP/2. For best performance, this protocol will hand a lot of control back to you, which means you will need to make decisions for each project. I haven’t covered in this article how to take advantage of new features of HTTP/2 such as server push. This technology allows you to decide which resources are a priority and instructs the server to hand those out before less important things.</p>

## When To Switch?

For designers and developers who do not have full control over the servers they deploy to, the decision may have to wait until the servers they use are updated. There are hosting companies ofering HTTP/2 already - even for [shared hosting](https://inmotion-hosting.evyy.net/c/1233229/260033/4222) - so deploying to a supporting server is something you could recommend to a client if you know they would benefit.

Once your website is hosted on a server that supports HTTP/2, the decision of whether to continue optimizing for HTTP/1.1 or to optimize for HTTP/2 will come down to the <strong>protocol supported by the majority of your users</strong>. Remember that HTTP/2 is backwards-compatible — you don’t need to do anything specific. The decision you need to make is when to optimize for it.

You’ll need to decide according to your analytics data. If more visitors are using HTTP/2-supporting browsers than not, then I’d suggest that’s a reasonable tipping point for optimizing for those users. Many of us will <a href="https://caniuse.com/#feat=http2">already have reached that point</a>. You should use data from sites such as Can I Use along with data gathered from your own analytics and knowledge of your likely audience. For example, many of the benefits of HTTP/2 will be felt most keenly by users of HTTP/2 supporting mobile devices. If you have a high percentage of mobile traffic that might be an indication to move to HTTP/2 sooner. However, if you have a high percentage of mobile traffic from users who browse using Opera Mini then that would be a reason to hold off on the move to HTTP/2 as it currently does not have support while having a high number of users in some parts of the world.

If you are building a brand new website today, I’d suggest keeping HTTP/2 optimization in mind throughout your build. If at launch, you feel that you need to make concessions for HTTP/1.1 due to browser or server support, a lot of that can be done in the build process, allowing you to switch to the HTTP/2 version as soon as you feel the time is right.</p>

## Your HTTP/2 Action Plan

1.  **Launch with a secure connection or make the move to TLS now** This should be your priority.
2.  **Prepare for HTTP/2 in your build process.** Any website you build now would likely benefit from being optimized for HTTP/2 over its lifetime. Use the tips above to create a build process that can be optimized for both protocols.
3.  **Check your statistics.** By comparing browser usage on your website with the [support table on Can I Use](https://caniuse.com/#feat=http2), you can see what percentage of visitors would benefit from HTTP/2 optimization.
4.  **Check your hosting.** When you reach the point when you would benefit from switching, you will need to ensure that your server supports HTTP/2\. Speak to your hosting provider or server administrator to find out their migration plan.
5.  **Roll out HTTP/2 optimization.** Once your server supports HTTP/2, the rest is up to you. Stop using the old best practices and switch to the new. This will mean that users with browsers that do not support HTTP/2 will get a slower experience, which is why the driver behind your change should be the tipping point when the majority would benefit.

When you do move to HTTP/2, it would be interesting to benchmark the speed increases and to see which techniques have made the biggest differences on your websites. I’m looking forward to seeing information from real-world cases as people migrate websites. That information will help us develop a whole new generation of best practices.</p>

## Find Out More

An increasing amount of information about HTTP/2 is available online. I’ve listed some resources here for your reference, many of which I referred to while writing this article.

*   “[Hypertext Transfer Protocol Version 2 (HTTP/2)](https://httpwg.github.io/specs/rfc7540.html)” (specification), Internet Engineering Task Force This is for people who enjoy reading specifications or who need to understand the finer points. For everyone else, the [HTTP/2 FAQ](https://http2.github.io/faq/) is an excellent summary of the main features.
*   [_http2 explained_](https://daniel.haxx.se/http2/), Daniel Sternberg This free ebook is worth reading if you want to dig into details of the protocol as you plan your strategy.
*   [_High Performance Browser Networking_](https://chimera.labs.oreilly.com/books/1230000000545), Ilya Grigorik, O’Reilly This book covers both HTTP/1.1 best practices and HTTP/2\. It would be useful for anyone who wants to both enhance performance today and prepare for the future.
*   “[HTTP/2 Is Here, Let’s Optimize](https://docs.google.com/presentation/d/1r7QXGYOLCh4fcUq0jDdDwKJWNqWK1o4xMtYpKZCJYjM/present#slide=id.p19)” (slidedeck) Ilya Grigorik This excellent set of slides has more information on some of the points covered in this article.
*   HTTP/2 Indicator: [Firefox](https://addons.mozilla.org/en-US/firefox/addon/http2-indicator/) and [Chrome](https://chrome.google.com/webstore/detail/http2-and-spdy-indicator/mpbpobfflnpcgagjijhmgnchggcjblin?hl=en) This browser plugin tells you whether the website you are on is being served over HTTP/2.
*   For more reading see [this huge list of links curated by Rebecca Murphey](https://pinboard.in/u:rmurphey/t:http2/).

{{< signature "rb, jb, al, ml" >}}


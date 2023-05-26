---
title: Bandwidth Media Queries? We Don't Need ’Em!
slug: bandwidth-media-queries-we-dont-need-em
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a034b950-aed2-4128-b466-8a160c034e10/brushessmoke.jpg
date: 2013-01-09T13:48:59.000Z
author: yoav-weiss
description: >-
  From time to time, when a discussion is taking place about ways to implement
  responsive images, someone comes along and says, “Hey, guys! What we _really_
  need is a media query that enables us to send high-resolution images to people
  on a fast connection and low-resolution images to people on a slow
  connection.” At least early on, a lot of people agreed.
categories:
  - Mobile
  - Performance
  - Responsive Design
  - Media Queries
---
From time to time, when a discussion is taking place about ways to implement responsive images, someone comes along and says, “Hey, guys! What we <em>really</em> need is a media query that enables us to send high-resolution images to people on a fast connection and low-resolution images to people on a slow connection.” At least early on, a lot of people agreed.

At first glance, this makes a lot of sense. High-resolution images have a significant performance cost, because they take longer to download. On a slow network connection, that cost can have a negative impact on the user’s experience. Users might prefer low-resolution images if it means that pages will download significantly faster. On the other hand, for users on a high-speed connection, the performance cost of delivering high-resolution images diminishes, and users would probably prefer better-quality images in this case.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Techniques For Gracefully Degrading Media Queries](https://www.smashingmagazine.com/2011/08/techniques-for-gracefully-degrading-media-queries/)
*   [Breakpoints And The Future Of Websites](https://www.smashingmagazine.com/2014/07/breakpoints-and-the-future-websites/)
*   [<span class="headline">Looking Beyond Common Media Query Breakpoints</span>](https://www.smashingmagazine.com/2012/10/beyond-common-media-query-breakpoints/)
*   [How To Solve Adaptive Images In Responsive Web Design](https://www.smashingmagazine.com/2013/06/clown-car-technique-solving-for-adaptive-images-in-responsive-web-design/)
*   [Learning CSS3: A Reference Guide](https://www.smashingmagazine.com/learning-css3-useful-reference-guide/)

If only we had a media query (and the HTML element that allows us to use that media query) that enables Web developers to have that degree of control over served images as a function of bandwidth, life would be peachy.

{{% feature-panel %}}

As it turns out, accurately implementing such a dream media query is not a whole lot easier than implementing a machine that can accurately predict how much it will rain two weeks from next Tuesday. And even if it were possible to implement, its side effects would result in a worse user experience, rather than a better one.</p>

## What Is Bandwidth?

Since we’re discussing bandwidth, let’s pause for a minute to define it.

When network operators publish their network speed, what they’re usually referring to is the amount of raw data that can be sent on the radio band, usually in ideal conditions.

That number has little relevance to Web developers. <strong>The bandwidth that we care about is the “effective” bandwidth</strong>. That bandwidth is usually a function of several factors: the network’s bandwidth, its delay, packet loss rate, and the protocol used to download the data. In our case, the protocol in question is TCP.

<a href="https://en.wikipedia.org/wiki/Transmission_Control_Protocol">TCP</a> is the dominant protocol for the reliable transfer of data on the Internet. The protocol itself has a certain overhead that results in a difference between the theoretical and the effective bandwidth. But another factor is responsible for an even more significant gap between the two. TCP doesn’t always use all of the bandwidth available to it, simply because it doesn’t know the bandwidth’s size.

Sending more data than the available bandwidth can cause <a href="https://en.wikipedia.org/wiki/Network_congestion">network congestion</a>, which has disastrous implications on the network. Therefore, TCP uses a couple of congestion control mechanisms: <a href="https://en.wikipedia.org/wiki/Slow-start">slow-start</a> and <a href="https://en.wikipedia.org/wiki/TCP_congestion_avoidance_algorithm">congestion avoidance</a>.

Each TCP connection is created with a very limited bandwidth “allowance,” called a <a href="https://en.wikipedia.org/wiki/Congestion_window">congestion window</a>. The congestion window grows exponentially over time, until the TCP connection sends enough data to “fill the pipe.” That is the slow-start phase, which can take up to several seconds, depending on the network’s delay. Then, TCP periodically tries to send just a little more, to see if it can increase the amount of data it sends without causing congestion. That is the congestion-avoidance phase.

<a href="https://www.flickr.com/photos/elliotjaystocks/7073360897"><img loading="lazy" decoding="async" class="133722" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0e4ec22-db63-40a0-a414-0d9269f20037/media-queries.jpg" alt="Media query download tests" width="500" height="296" /></a><br>
<em>Is network speed the issue in responsive Web design? More often it's images are being downloaded when they aren't supposed to. Image credit: <a href="https://www.flickr.com/photos/elliotjaystocks/7073360897">Elliot Jay Stocks</a>.</em>

Both of these mechanisms assume that packet loss is always caused by congestion; so, packet loss results in a significant reduction to the congestion window, as well as to the rate at which data is sent. On wireless and mobile networks, this behavior is not always ideal because they can suffer from packet loss for reasons other than congestion (for example, poor reception), which can result in under-utilization of the network.</p>

## Bandwidth Changes

Bandwidth, by its very nature, is variable over time. During the downloading of a single resource, the bandwidth of a mobile user can change significantly for multiple reasons:

*   The user has switched cells or moved to an area with different cellular coverage.
*   Other users have moved into the cell that the user is in.
*   Network congestion on the server side of the network has caused the effective bandwidth to drop.

The bandwidth of Wi-Fi users can also vary widely. This is mainly due to packet loss, which has a significant impact on effective bandwidth, because TCP considers packet loss a result of congestion.

The bandwidth of desktop users can also vary depending on their connection type, although not likely as significantly as for mobile and Wi-Fi users. ADSL can suffer from weather conditions; cable can suffer from uplink sharing; and other networks could have their own share of problems.

One more thing. When we think about the user’s bandwidth, we tend to think of the user’s connection to the Internet; but the connection of the Web server to the Internet, its load and its proximity to the user can also have a significant impact on the effective bandwidth that the browser sees. So, <strong>another variable is at play here</strong>: the Web server itself. When we say that we want to measure bandwidth, are we talking about the bandwidth between the user and the Web server, or just the radio link’s bandwidth? It all depends on where the bandwidth bottleneck is.

This variability is the major reason why making predictions about future bandwidth is likely to be highly inaccurate and error prone.</p>

## Measuring Bandwidth Is Hard

OK, so predicting bandwidth is complicated, but measuring it must be easy, right? After all, the browser is already downloading resources. It knows their sizes and how long it took to download them — the number of bits downloaded divided by the time it took to download them. How hard can it be?

Well, if you want to measure bandwidth accurately, it <em>is</em> kinda hard. The above calculation is true when you download a large file over a single warmed-up TCP connection. That is rarely the case.

Let’s look at a typical scenario of loading a Web page, shall we?

1.  **Initial HTML page is downloaded** During this phase, most of the time, the browser downloads the initial HTML page on a new TCP connection. That new TCP connection needs to be careful not to send more data than the physical link can handle, so it uses its slow-start mechanism. This means that, during this phase, if the browser needs to measure the effective bandwidth it’s got, it will significantly underestimate the available bandwidth. When we’re discussing bandwidth media queries, this phase is the critical one. When the browser needs to decide which resources to download according to the media query, this measurement is most likely the only bandwidth measurement that the browser will have with this particular server.
2.  **CSS and JavaScript external resources are loaded.** During this phase, the browser has a collection of new TCP connections, all in their slow-start phase, and they are not all necessarily to the same destination server. Again, estimating bandwidth in this phase is not straightforward.
3.  **Images are loaded.** Here the browser has multiple connections, each one downloading a resource. The problem is that these connections are not always in the same phase of their life cycle. Some might be in the slow-start phase; some may have suffered a packet loss and, thus, reduced their window and the bandwidth they are trying to fill; and some might be warmed-up TCP connections, ready to fill the bandwidth. These TCP connections are not necessarily all to the same destination server, and the bandwidth towards the various destination servers might be different between one another.

So, estimating bandwidth is possible, but it is far from simple, and it is possible only for certain phases of the page-loading process. And because having several TCP connections to various destination servers is common (for example, a CDN could host the image resources of a Web page), we cannot really tell what is the bandwidth we want to measure.</p>

## Media Query Is An Order

As far as the browser is concerned, a media query is a direct order with which the browser must comply. It has no room for optimizations. It cannot avoid obeying it, even when it makes absolutely no sense. Let’s explore what that means for bandwidth media queries.

Let’s assume for a minute that browsers actually do have an accurate way to measure the current bandwidth and that a solution for responsive images is in place and can use a bandwidth media query.

<img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7c49c62-4500-4d64-89e0-5c50b58367b5/column-layout-with-ios.jpg" alt="" width="500" height="705" /><br>
<em>Latency is the network killer. It can significantly slow down the loading of a responsive website, especially if it has loads of images. Image credit: Andy Chung.</em>

The natural thing to do, then, would be to <strong>define a responsive image with multiple sources</strong> — a high-resolution image to use when the bandwidth exceeds a certain value, and a low-resolution image when the bandwidth is low. The browser loading the page that contains the image would then download the high-resolution image, since it has good bandwidth conditions.

Let’s say that, after a few seconds, the bandwidth conditions change for some reason. The browser (sharp at detecting bandwidth as it is) will immediately detect that the bandwidth is down. The browser is now obligated to download the lower-resolution image and replace the high-resolution one with it. The result is a useless download of the low-resolution image and a worse user experience, because the quality of the image that the user sees is worse than it could be. Even if this happens to only a low percentage of users, that’s bad news.

Now, you could argue that the browser could optimize and use the version it already has. But the fact of the matter is, it can’t; not with media queries — at least not without changing the whole meaning of them.

## So, What’s The Alternative?

Well, if media queries can’t be used for bandwidth detection, is there no hope? Shouldn’t we, as Web developers, be able to define image resolution according to the available bandwidth?

I hate to say it, but we shouldn’t.

Web developers should be able to define image resources of various resolutions, which would later be used by the browser to perform heuristic optimizations. This can be done by a declarative syntax, similar to the syntax of the <code>srcset</code> responsive images proposal. The syntax would define various resources and would hint to the browser which images to use for various criteria, such as screen density and screen size. The browser would then use these hints, but with room left open for further optimizations (related to bandwidth, user preference, data plan costs, you name it).

While I have reservations about the <code>srcset</code> proposal, and many agree that the syntax it uses is confusing, the declarative model is better when bandwidth optimizations (and other browser heuristics) are involved.</p>

## Why Do We Need Media Queries, Then?

Media queries are necessary when the browser must <em>not</em> be allowed to use heuristics to pick the right image resource to present. One of the best examples of this (and an illustration of one of the biggest shortcomings of the <code>srcset</code> proposal) is the <a href="https://usecases.responsiveimages.org/#art-direction">art direction use case</a>. This is the use case where the proposed <a href="https://picture.responsiveimages.org/">picture element</a> really shines.

<a href="https://usecases.responsiveimages.org/#art-direction"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f601aea2-a9a7-4688-812f-f8bc63052cb5/art-direction-500.jpg" alt="" width="500" height="325" /></a><br>
<em>The "Art Direction" use case. Image credit: <a href="https://usecases.responsiveimages.org/#art-direction">W3C</a>.</em>

This is the reason why we need <a href="https://www.w3.org/community/respimg/2012/06/18/florians-compromise/">both approaches</a> in order to achieve a well-rounded responsive-images solution that covers all use cases.</p>

## Network Measurements

Don’t get me wrong. I’m not saying that we should give up on network measurement as a whole on the Web platform.

Work is being done on the <a href="https://www.w3.org/TR/netinfo-api/">network information API</a> to figure out how to expose network characteristics to Web developers. In the work being done on this specification, one of the major issues is — surprise! — how to measure bandwidth.

I believe that browser makers will find a way one day to measure bandwidth at the end of the initial page load in a semi-accurate way, which would be useful for various progressive-enhancement decisions. But we’re not there yet.</p>

## Conclusion

The main reason why Web developers want bandwidth media queries is to be able to serve image resolutions according to their users’ network conditions. Basically, they want to have a say in the trade-off between beautiful images and slow page loading.

Unfortunately, this doesn’t seem to be something that can be accurately implemented in the near future. Even if it could be implemented, because a media query is an <em>order</em>, it would force the downloading of multiple resources for the same image in many cases, resulting in a worse user experience. Bandwidth optimizations are better left to the browser, which know the user, their preferences and their network conditions better.

{{< signature "al" >}}


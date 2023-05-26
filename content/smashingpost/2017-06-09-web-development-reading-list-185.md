---
title: >-
  Web Development Reading List #185: Safari 11, New Edge Build, Chrome 59, And
  CSS Optimization Insights
slug: web-development-reading-list-185
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f94dd229-b6f5-45c5-82ea-005109c0b69b/wdrl-185-opt.png'
date: 2017-06-09T17:23:10.000Z
author: anselm-hannemann
description: >-
  This week was full of **great browser vendor news**: Safari 11 was announced
  with long-awaited features such as WebRTC and tracking protection, and a new
  Edge build with new CSS features is now available, too.

  But the past few days also had some valuable articles up their sleeves: about
  implementing HTTP/2 push, using `datetime-local`, and slimming down your CSS,
  for example. I collected everything in this reading list for you, so you don’t
  miss out on anything. Enjoy!
categories:
  - Web Development Reading List
---
### <span class="rh">Further Reading</span> on SmashingMag:

*   [Getting Ready For HTTP/2: A Guide For Web Designers And Developers](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [A Comprehensive Guide To HTTP/2 Server Push](https://www.smashingmagazine.com/2017/04/guide-http2-server-push/)
*   [The Current State Of Authentication: We Have A Password Problem](https://www.smashingmagazine.com/2016/06/the-current-state-of-authentication-we-have-a-password-problem/)
*   [Why Coding Style Matters](https://www.smashingmagazine.com/2012/10/why-coding-style-matters/)

## News

*   With [Microsoft’s Edge build 16215](https://developer.microsoft.com/en-us/microsoft-edge/platform/changelog/desktop/16215/) available now, the browser [finally supports `object-fit` and `object-position`](https://wpdev.uservoice.com/forums/257854-microsoft-edge-developer/suggestions/6263790-object-fit-and-object-position) as well as [`position: sticky`](https://wpdev.uservoice.com/forums/257854-microsoft-edge-developer/suggestions/6263621-position-sticky). Additionally, `passive` and `once` event listeners are now supported, too, and the developer tools also got some improvements.
*   In an attempt to prevent privacy violations by advertisers, Apple’s [Safari browser will soon come with Intelligent Tracking Prevention built in](https://webkit.org/blog/7675/intelligent-tracking-prevention/). It’s a machine-learning-driven algorithm that auto-deletes tracking cookies and other data. And to make it even cooler, the learning algorithm will run on your local device, not in the cloud.
*   This week, [Chrome 59](https://developers.google.com/web/updates/2017/05/nic59) was released. It brings headless Chrome and native notifications for macOS.
*   Yep, [Safari 11](https://developer.apple.com/library/content/releasenotes/General/WhatsNewInSafari/Safari_11_0/Safari_11_0.html) was announced at WWDC this week, and it’ll bring some nifty features to users in fall this year. And for us developers, there’s a lot of good stuff coming up, too: WebRTC, Website Snapshots, WebAssembly, drag and drop on iOS, and home screen apps running on the same, latest WebKit as Safari apps, for example. As for APIs, we can look forward to Media Capture, WebCrypto, and Resource Timing APIs. Variable fonts and `stroke` will also be supported, and developer tools will get an update, too.
*   [Safari’s Technology Preview 32](https://webkit.org/blog/7627/safari-technology-preview-32/) brings a lot of the announced features of the upcoming Safari 11 to developers already today, including [WebRTC support](https://webkit.org/blog/7726/announcing-webrtc-and-media-capture/), WebAssembly, and auto-play prevention.

{{% feature-panel %}}

<figure><a href="https://developers.google.com/web/updates/2017/05/nic59"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41b6f2a8-95d2-4e26-8e52-d75b58135cf1/chrome59-notifications-opt.png" width="800" height="408" alt="New Chrome notifications on macOS" /></a><figcaption>With the new Chrome 59, Chrome notifications on macOS will finally <a href="https://developers.google.com/web/updates/2017/05/nic59">use the native notification system</a>. And they’ll respect “Do not disturb” settings, too. (<a href="https://developers.google.com/web/updates/2017/05/nic59">Image credit</a>)</figcaption></figure>

## Tools & Workflows

*   Wes Bos has [a clever git trick](https://mobile.twitter.com/wesbos/status/872521465417039872) for you: Use `git checkout -` to quickly jump back to your last git branch.</p>

## Security

*   Egor Homakov published [SecureLogin](https://medium.com/@homakov/securelogin-forget-about-passwords-c1bf7b47f698), an [open-source](https://github.com/sakurity/securelogin) authentication implementation that wants to be convenient, secure, and independent of social media services. A promising technology.</p>

## Web Performance

*   Jake Archibald shares his [experience with implementing HTTP/2 push](https://jakearchibald.com/2017/h2-push-tougher-than-i-thought/) and why it’s tougher as we might think.

<figure><a href="https://jakearchibald.com/2017/h2-push-tougher-than-i-thought/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e48d4a0a-8947-41c3-a249-6788e53a90a1/http2-push-opt.png" width="800" height="447" alt="How HTTP/2 push works" /></a><figcaption>HTTP/2 push is promising but not free of pitfalls. Jake Archibald <a href="https://jakearchibald.com/2017/h2-push-tougher-than-i-thought/">takes a closer look</a>. (<a href="https://jakearchibald.com/2017/h2-push-tougher-than-i-thought/">Image credit</a>)</figcaption></figure>

## HTML & SVG

*   Andrea Giammarchi explains how we can use [input `datetime-local`](https://medium.com/@WebReflection/using-the-input-datetime-local-9503e7efdce) already today.</p>

## CSS/Sass

*   Jens Oliver Meiert conducted a study to find out [how often we repeat declarations in our style sheets](https://meiert.com/en/blog/20170531/70-percent-css-repetition/). The result: in 70% of cases. An article with great insights into how we can do better when optimizing CSS.</p>

## Work & Life

*   “Economists believe in full employment. Americans think that work builds character. But [what if jobs aren’t working anymore](https://aeon.co/essays/what-if-jobs-are-not-the-solution-but-the-problem)?”

## Going Beyond…

*   When it comes to phones and other small devices, it’s possible to demand users to exchange their hardware from time to time. But now that cars are getting smarter and Internet-driven software will control them in the future, it’s time to ask [how this will affect our safety and security](https://www.lightbluetouchpaper.org/2017/06/01/when-safety-and-security-become-one/).

Thanks for reading this. If you like it, consider [supporting my work](https://wdrl.info/donate).

_—Anselm_


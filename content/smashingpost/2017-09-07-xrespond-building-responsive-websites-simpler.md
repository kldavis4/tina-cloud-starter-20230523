---
title: 'Meet XRespond Testing Tool: Let’s Make Building Responsive Websites Simpler'
slug: xrespond-building-responsive-websites-simpler
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b640ab8f-5cb4-4e9a-a820-e65afe439a70/xrespond-preview-opt.png
date: 2017-09-07T20:00:33.000Z
author: indrekpaas
description: >-
  The way people consume information is constantly evolving. As web designers
  and developers, we keep up with all of the different screen shapes and sizes,
  learning to create beautiful, flexible software. Yet most of the available
  tools still don’t reflect the nature and diversity of the platform we’re
  building for: the browser.
categories:
  - Mobile
  - Tools
  - Responsive Design
---
When I was making my first responsive website in 2012, I quickly realized how inefficient and time-consuming the constant browser window resizing was. I had just moved from Estonia to Australia, and with a newborn, time was very much a precious resource.

I began looking for better ways to see the effects of my media queries.

I came across Matt Kersley’s [Responsive Web Design Testing Tool](https://mattkersley.com/responsive/) and was blown away. It **cut my development time in half**. Even though the app was quite basic, it quickly became indispensable, and I continued to use it for several years.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f51fed6e-6d3c-46a0-959f-89f6c9ccc07d/mattkersley-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fd1cc65-0249-45fa-ae2f-b24e99b75ca4/mattkersley-800w-opt.png" alt="Matt Kersley’s Responsive Web Design Testing Tool" width="800" height="519" /></a><figcaption>Matt Kersley’s Responsive Web Design Testing Tool. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f51fed6e-6d3c-46a0-959f-89f6c9ccc07d/mattkersley-large-opt.png">View large version</a>)</figcaption></figure>

{{% feature-panel %}}

It was very much to my surprise that I never saw this brilliant concept taken any further. This, combined with the lack of features, set me on a journey to create the open-source virtual device lab [XRespond](https://www.xrespond.com).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4523577-5493-45fb-b72d-f4371c46d179/xrespond-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9309487b-978c-404e-b8cc-1fab1f2eac40/xrespond-800w-opt.png" alt="The new Smashing Magazine website previewed in XRespond" width="800" height="519" /></a><figcaption>The new Smashing Magazine website previewed in XRespond (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4523577-5493-45fb-b72d-f4371c46d179/xrespond-large-opt.png">View large version</a>)</figcaption></figure>

## Understanding The Problem

When it comes to developing responsive websites, the problem lies in having to constantly resize the browser window. Although this unavoidable action feels second nature to most, it also masks aspects of design we don’t often appreciate — most notably, inconsistency and time management.

With designs usually appearing in some combination of mobile, tablet and desktop context, anything in between is left in a somewhat uncertain state. And filling these gaps requires a lot of time and effort.

The problem lies in the difficulty of looking at one screen size at a time, as opposed to getting an all-in-one overview of different screen sizes. When we’re building for a variety of screen types, it doesn’t make sense to view only a single instance of a design at any given time — we’d be unable to gain the context of how the styles of elements change across breakpoints.

Current practices just don’t cater to these modern ways of developing. Fortunately, it’s not all bad news.</p>

## Simple Solution

[XRespond](https://www.xrespond.com) is a virtual device lab for designing, developing and testing responsive websites. The idea is simple: It enables you to make website comparisons side by side, as if you had different devices on the wall in front of you.

You don’t have to leave your desk, laptop or even favorite browser. And with zero setup, you can start comparing websites right away.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2647ca3b-6db3-4902-9efa-c851f2338ea0/xrespond-banner-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cf2af2b-d0be-4e98-8ff6-8b0274610290/xrespond-banner-800w-opt.png" alt="" width="800" height="400" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2647ca3b-6db3-4902-9efa-c851f2338ea0/xrespond-banner-large-opt.png">View large version</a>)</figcaption></figure>

XRespond can help if you’re building a pattern library or a style guide, because you can focus on a single component at different screen sizes simultaneously. As you’d expect from a development tool, it works well with local servers.

Just bear in mind that, as with any emulation, XRespond can't compete with testing on real devices, but it will get you 90% of the way there — and in a fraction of the time.</p>

## How To Use It?

Enter a website address, click the button, and XRespond will automatically display the website on different virtual devices — which you can choose and customize as you see fit.

XRespond works well with other development tools, notably one of my favorites: [Browsersync](https://www.browsersync.io/). Browsersync enables you to set up live reloads and synchronized scrolling — all simultaneously across virtual (and real) devices. This makes spotting problems simpler, because issues become more apparent.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb18fe6b-3802-4922-85c6-bc9e99bc0f51/browsersync.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/569e9b55-dab4-4fb9-be1d-328b80a2e34f/browser-sync.gif" alt="Synchronized scrolling across devices with Browsersync" width="800" height="595" /></a><figcaption>Synchronized scrolling across devices with Browsersync (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb18fe6b-3802-4922-85c6-bc9e99bc0f51/browsersync.gif">View large version</a>)</figcaption></figure>

### What To Do If Your Website Won’t Load?

Occasionally, you might run into a problem of your website failing to load. This most likely has to do with your website preventing itself from being loaded in an iframe. If you own the website, you can temporarily [disable `X-Frame-Options`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options) or the [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP), depending on your setup.</p>

## Conclusion

I love XRespond — and not just because I love making it, but because it simplifies my life. I can spend less time and effort working, and use the spare time for something else. It’s given me an opportunity to improve the quality of my work. I hope you’ll find XRespond just as useful and will start enjoying the time it saves you.

Feel free to share, and [follow me](https://twitter.com/indrekpaas) on Twitter for updates. Cheers!

{{< signature "da, il, al" >}}


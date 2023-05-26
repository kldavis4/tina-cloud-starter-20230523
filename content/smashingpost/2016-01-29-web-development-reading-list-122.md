---
title: >-
  'Web Development Reading List #122: A Performance Budget Builder, Streams, And
  The Web Push API'
slug: web-development-reading-list-122
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcd5e681-9d0f-4bad-bb66-e7b3657696b4/european-government-debt-1000px.jpeg
date: 2016-01-29T19:50:29.000Z
author: anselm-hannemann
summary: >-
  What’s going on in the industry? What new techniques have emerged recently? Anselm Hannemann is collecting everything that popped up over the last week in his web development reading list so that you don’t miss out on anything. The result is a carefully curated list of articles and resources that are worth taking a closer look at.
description: >-
  This list of articles gather information about the Web Develpment industry, Web Development tools and Web Design insights, tools, tips and tricks.
categories:
  - Web Development Reading List
  - Coding
  - Tools
---

I’ll make it short this week: Thank you so much for the [great, constructive discussion last week](https://www.smashingmagazine.com/2016/01/web-development-reading-list-121/#comments) about hiring people and web development basics. I took away some very interesting thoughts from it, and I hope you did so, too. Now, let’s go through the newest things I found.

## News

- This week, [Firefox 44 has been released](https://developer.mozilla.org/en-US/Firefox/Releases/44) to the public. The new version offers better video support (VP9, WebM in addition to h.264) and adds support for Brotli compression (a new, better compression than gzip) for HTTPS connections. Service Workers are also supported now. Furthermore, the new Firefox requires add-ons to be signed and it doesn’t connect to sites anymore that allow RC4 ciphers in their HTTPS configuration.
- The new Chrome Beta channel build [now includes a security panel in the developer tools](https://blog.chromium.org/2016/01/introducing-security-panel-in-devtools.html). This panel shows you how secure your site is, including details on HTTPS and mixed content warnings. Unfortunately, it’s not super detailed yet, and it also doesn’t provide information like HSTS, HKPK and other security details, but I’m excited to see this and bet that they’ll integrate more features over time.

## General

- Francesco Iovine wrote down [how you can make your web application installable](https://medium.com/@franciov/how-to-make-your-web-app-installable-8b71571605e) on most mobile (and some Desktop) browsers and operating systems with the latest web standards.

## Concepts & Design

- Most of the time, we see boring data visualizations. But they don’t have to be boring &mdash; instead, with inspiration from artists, [we can make data very beautiful](https://medium.com/accurat-studio/beautiful-reasons-c1c6926ab7d7) and enhance the user experience through it.

<figure><a href="https://medium.com/accurat-studio/beautiful-reasons-c1c6926ab7d7"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcd5e681-9d0f-4bad-bb66-e7b3657696b4/european-government-debt-1000px.jpeg" width="800" height="553" alt="Beautiful data visualization" /></a><figcaption>Data visualization <a href="https://medium.com/accurat-studio/beautiful-reasons-c1c6926ab7d7">doesn’t have to be boring</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcd5e681-9d0f-4bad-bb66-e7b3657696b4/european-government-debt-1000px.jpeg">Large preview</a>)</figcaption></figure>

## Tools

- If you already have your logo as an SVG file, you might want to optimize it not only for bright but also for dark backgrounds. With [logomono](https://logomono.com/) you can now automate the process easily to get a great, reliable SVG that works on both types of backgrounds.

{{% feature-panel %}}

## Web Performance

- Brad Frost has built a super-simple [Performance Budget Builder](https://bradfrost.com/blog/post/performance-budget-builder/). You just need to enter your personal project goals to see if you match your performance budget or not.
- Since responsive images are a thing you can (and should) use now in production, we face the problem of resizing our images in various resolutions, sizes and qualities. There are some neat server integrations that help you with that, however, for many cases, it’s still a problem. Luckily, [there’s now an open source tool you can use](https://www.responsivebreakpoints.com/), along with [a guide on the whole topic](https://www.smashingmagazine.com/2016/01/responsive-image-breakpoints-generation/).

## HTML / SVG

- Many people don’t know that the `hidden` HTML&ndash;attribute has quite decent browser support. Steve Faulkner explains [how you can use it](https://www.paciellogroup.com/blog/2016/01/the-state-of-hidden-content-support-in-2016/) and also describes other attributes to properly hide elements.

## Accessibility

- Adrian Roselli explains [when we should use an `&lt;a&gt;`, a `&lt;button&gt;`, or an `&lt;input type="submit"&gt;` element for a clickable action item](https://adrianroselli.com/2016/01/links-buttons-submits-and-divs-oh-hell.html) and why using a `&lt;div&gt;` is never a valid option for such cases.
- When we [see our development stack as an accessibility stack](https://simplyaccessible.com/article/the-accessibility-stack/) and follow some basic principles, we can easily build an accessible web solution that integrates all kind of users, no matter _how_ they consume the content on the website.

{{% ad-panel-leaderboard %}}

## JavaScript

- Jake Archibald [introduces us to the world of Streams in JavaScript](https://jakearchibald.com/2016/streams-ftw/) and tells us why we can serve content more efficiently and faster using Streams.
- It’s not a new resource but worth reading if you haven’t yet fully understood how the JavaScript scope works: [Everything you wanted to know about JavaScript scope](https://toddmotto.com/everything-you-wanted-to-know-about-javascript-scope/) by Todd Motto.
- [Firefox 44 also introduces the Web Push API](https://hacks.mozilla.org/2016/01/web-push-arrives-in-firefox-44/), and you can learn in this article how to use it to notify users about an incoming WebRTC call for example.

<figure class="fwi"><a href="https://jakearchibald.com/2016/streams-ftw/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3da945ab-8f5e-4f8a-bd44-ed96256255a4/jake-archibald-stream.png" width="800" height="500" alt="Streams in JavaScript Illustration" /></a><figcaption>Jake Archibald explains how we can <a href="https://jakearchibald.com/2016/streams-ftw/">serve content more efficiently and faster using Streams</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3da945ab-8f5e-4f8a-bd44-ed96256255a4/jake-archibald-stream.png">Large preview</a>)</figcaption></figure>

## CSS / Sass

- The floating label pattern on form input fields is a nice way to give hints on a form field. And now, there is a method to [do it just with CSS](https://thatemil.com/blog/2016/01/23/floating-label-no-js-pure-css/), no additional JavaScript needed.
- [With the CSS flexbox module, we can achieve a masonry layout relatively easily](https://medium.com/@_jh3y/how-to-pure-css-masonry-layouts-a8ede07ba31a) without adding JavaScript to calculate positions but just CSS.
- Mikito Takada wrote a mini-book about CSS. _[Learn CSS Layout The Pedantic Way](https://book.mixu.net/css/)_ explains basic CSS properties in a very detailed, clear way so that no questions are left unanswered.

{{% ad-panel-leaderboard %}}

## Work & Life

- As an industry, we have become accustomed to getting hundreds of hours of work and the benefit of years of hard&ndash;won knowledge for free. But we often forget that [free software (OSS) is not entirely free, as it is paid for by people paying their time for it](https://alistapart.com/article/the-high-price-of-free).

## Go beyond…

- Discussions about Uber need to go beyond the fact that they offer a cheaper ride. In fact, [Uber challenges courts and politics, lawmakers and many other established systems](https://www.cbc.ca/beta/news/business/uber-canada-gig-economy-1.3414206) and people. They try to circumvent existing laws, and while this offers a great chance for lawmakers to finally improve such laws, the issue is, that if Uber succeeds in a case, other companies will use the same strategy as well.

And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via E&ndash;Mail, RSS and online.

_Thanks and all the best,
Anselm_

### Further reading on Smashing Magazine:

- “[Front-End Performance Checklist 2021](https://www.smashingmagazine.com/2021/01/front-end-performance-2021-free-pdf-checklist/),” Vitaly Friedman
- “[Getting Ready For HTTP/2](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/),” Rachel Andrew
- “[Everything You Need To Know About AMP](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/),” Christian Cantrell

{{< signature "nl" >}}
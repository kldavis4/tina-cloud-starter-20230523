---
title: >-
  Web Development Reading List #168: Preload With Webpack, A Guide To Security
  Headers, And Service Worker Fallacies
slug: web-development-reading-list-168
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51eedf9e-c904-4af5-b8ed-69aa1d6c7a8d/wdrl-168-opt.png'
date: 2017-02-03T21:38:50.000Z
author: anselm-hannemann
description: >-
  **With great power comes great responsibility**. This week I found some
  resources that got me thinking: Service Workers that download 16MB of data on
  the user’s first visit? A Bluetooth API in the browser? Private browser
  windows that aren’t so private at all?

  We have a lot of methods and strategies to fix these kinds of things. We can
  give the browser smarter hints, put security headers and HTTPS in place, serve
  web fonts locally, and build safer network protocols. The responsibility is in
  our hands.
categories:
  - Web Development Reading List
---
We have a lot of methods and strategies to fix these kinds of things. We can give the browser smarter hints, put security headers and HTTPS in place, serve web fonts locally, and build safer network protocols. The responsibility is in our hands.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)
*   [Content Security Policy, Your Future Best Friend](https://www.smashingmagazine.com/2016/09/content-security-policy-your-future-best-friend/)
*   [Making A Service Worker: A Case Study](https://www.smashingmagazine.com/2016/02/making-a-service-worker/)
*   [Managing Mobile Performance Optimization](https://www.smashingmagazine.com/2016/03/managing-mobile-performance-optimization/)

## News

*   Joseph Medley tells us about [API deprecations and removals in the upcoming Chrome 57](https://developers.google.com/web/updates/2017/02/chrome-57-deprecations). `<keygen>` will be removed, for example, as well as the prefix in some `webkit`-prefixed APIs.
*   [Chrome 56 is here](https://developers.google.com/web/updates/2017/01/nic56) with support for the Web Bluetooth API and the WebGL 2.0 API. The new version also finally supports `position: sticky` (the only browser still lacking support for it now is MS Edge).
*   [Safari 10.1 will be out soon](https://developer.apple.com/library/prerelease/content/releasenotes/General/WhatsNewInSafari/Articles/Safari_10_1.html) with a lot of new features: `fetch()`, Custom Elements, CSS Grid Layout, Reduced Motion Media Query, and ES6 native modules are notable ones.
*   Thanks to browser vendors pushing it aggressively, [HTTPS adoption has now reached the tipping point](https://www.troyhunt.com/https-adoption-has-reached-the-tipping-point/). Good to see, especially since man-in-the-middle traffic modifications increased a lot on non-encrypted traffic in the last few months. Sadly, these interceptions are not executed by federal authorities or hackers but by companies like Comcast, Norwegian Airlines, hotel WiFi network companies and the like.

{{% feature-panel %}}

<figure><a href="https://www.troyhunt.com/https-adoption-has-reached-the-tipping-point/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25536cd3-99c3-44b3-b301-0b37f99e163e/https-growth-opt.png" width="800" height="445" alt="Alexa top 1 Million sites redirecting to HTTPS" /></a><figcaption>A step into the right direction: Analyzing the Alexa top million websites, the percentage of sites that are redirecting users’ browsers from HTTP to HTTPs has <a href="https://www.troyhunt.com/https-adoption-has-reached-the-tipping-point/">doubled from August 2015 to August 2016</a>. (<a href="https://www.troyhunt.com/https-adoption-has-reached-the-tipping-point/">Image credit</a>)</figcaption></figure>

## Tools & Workflows

*   Addy Osmani wrote the Webpack plugin [preload-webpack-plugin](https://github.com/googlechrome/preload-webpack-plugin) for wiring up `<link rel='preload'>` (and prefetch) automatically.</p>

## Security

*   Max Veytsman summarized [everything you need to know about HTTP security headers](https://blog.appcanary.com/2017/http-security-headers.html). An all-embracing but concise guide to security headers and when and how to use them.</p>

## Privacy

*   DuckDuckGo published the results of a study they conducted on the question [if private browsing really is private](https://spreadprivacy.com/private-browsing-9276d6d16ea4). Interestingly, most people have no idea about what the private mode in browsers exactly does and 84% of Americans would consider trying another major web browser if it offered more features to help protect their privacy. The [full paper](https://duckduckgo.com/download/Private_Browsing.pdf) gives interesting insights into how people actually use search engines and how they try to protect their privacy.

<figure><a href="https://spreadprivacy.com/private-browsing-9276d6d16ea4"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8b73c2f-4a2e-4f8b-9520-ee6477a16bfb/private-browsing-opt.png" width="800" height="514" alt="Is Private Browsing Really Private?" /></a><figcaption>Privacy please! DuckDuckGo surveyed 5,710 random Americans to find out <a href="https://spreadprivacy.com/private-browsing-9276d6d16ea4">what they know about private browsing</a> and how they use the common privacy feature.</figcaption></figure>

## Web Performance

*   Not too long ago, I mentioned an article about [QUIC](https://www.smashingmagazine.com/2016/08/web-development-reading-list-148/#web-performance), Google’s protocol that uses UDP instead of TCP to make transfers to a client even faster than HTTP/2\. Now Facebook shares [details about their even faster Zero protocol](https://code.facebook.com/posts/608854979307125/building-zero-protocol-for-fast-secure-mobile-connections/) that builds on top of QUIC while still being compatible with TCP. I like that there’s now an alternative to Google’s approach and that people think about innovating the core of the Internet, the network itself, again.
*   Nicolas Hoizey analyzes [why it’s not a good idea to just hook up Service Workers](https://nicolas-hoizey.com/2017/01/how-much-data-should-my-service-worker-put-upfront-in-the-offline-cache.html) and save all resources offline. Given the fact that a lot of users might never come back or that they simply won’t read through all the pages of a website, downloading megabytes of data on first load might be a very bad practice — especially when we keep data plan costs in mind. Looking at these numbers, the 3MB of an average web page are nearly negligible if a Service Worker loads 16MB of useless data on initial page load without further ado.</p>

## Accessibility

*   [axe-cli](https://www.npmjs.com/package/axe-cli/) brings the accessibility testing tool axe-core to the command line. It does require Webdriver but runs smoothly nevertheless. So integrating it into your local workflow or even on a CI server shouldn’t be a problem.</p>

## JavaScript

*   Kyle Mathews published [_typefaces_](https://github.com/KyleAMathews/typefaces), a self-host font-face loading package that makes it simple to host web fonts on your own. He also explains [why self-hosting web fonts is faster and why it even works offline](https://github.com/KyleAMathews/typefaces).
*   Paul Kinlan explains [how you can use the Shape Detection API to detect text in an image on the web in real-time](https://paul.kinlan.me/detecting-text-in-an-image/). An experiment that would be great for web applications to ease the user experience. You could, for example, provide a very easy sign-up form and read the name and address from a business card using this API and a device’s camera.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_


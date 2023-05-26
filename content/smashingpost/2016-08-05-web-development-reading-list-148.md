---
title: >-
  Web Development Reading List #148: CSS Color Syntax Change, Browser News, And
  Hidden Expectations
slug: web-development-reading-list-148
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/941bc8ae-a774-4030-9b5d-4e85c46eec72/wdrl-148-opt.png'
date: 2016-08-05T19:47:45.000Z
author: anselm-hannemann
description: >-
  I shut down my browser on Wednesday, accidentally having a setting switched on
  that clears history and all sessions. First, I was sad to have lost many tabs
  with articles I stored “for later”. At the same time, it felt refreshing,
  **liberating to have a clean browser window** with zero tabs open. So my new
  goal is to start work in the morning with a completely clean browser window at
  least once a week.

  In other news: I spent several hours fixing broken links this week, and as a
  result I can’t say how happy I am that [archive.is](https://archive.is/) and
  [archive.org](https://archive.org/) exist to prevent content from disappearing
  forever. Still, some of the resources I found broken have left forever. So
  remind yourself about redirecting content.
categories:
  - Web Development Reading List
---
I shut down my browser on Wednesday, accidentally having a setting switched on that clears history and all sessions. First, I was sad to have lost many tabs with articles I stored “for later”. At the same time, it felt refreshing, <strong>liberating to have a clean browser window</strong> with zero tabs open. So my new goal is to start work in the morning with a completely clean browser window at least once a week.

In other news: I spent several hours fixing broken links this week, and as a result I can’t say how happy I am that <a href="https://archive.is/">archive.is</a> and <a href="https://archive.org/">archive.org</a> exist to prevent content from disappearing forever. Still, some of the resources I found broken have left forever. So remind yourself about redirecting content.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Hex Color – The Code Side Of Color](https://www.smashingmagazine.com/2012/10/the-code-side-of-color/)
*   [A Simple Web Developer’s Guide To Color](https://www.smashingmagazine.com/2016/04/web-developer-guide-color/)
*   [Everything About Color Contrast And Why You Should Rethink It](https://www.smashingmagazine.com/2014/10/color-contrast-tips-and-tools-for-accessibility/)

## News

*   There’s a big change coming up for how we write colors in CSS. Tab Atkins [recently changed the color functions syntax](https://www.xanthir.com/b4iW0) in the CSS specification. So in future, we will write `rgb(0 255 0 / 50%)` instead of `rgba(0, 255, 0, 50%)`. This might sound awkward after years of doing it differently, but the reason for it are the new color functions available in CSS Colors Level 4, including `color()`. You can read more about this in Tab’s blog post, but for now be assured that the old syntax is likely to be supported forever in our browsers thanks to legacy support.
*   Opera 39 and Chromium 52 hit the streets this week and with them [a couple of new features](https://dev.opera.com/blog/opera-39/): The Fetch API now supports a custom referrer policy, [Performance Observer](https://developers.google.com/web/updates/2016/06/performance-observer) is supported, just like alpha channel for RGB colors in hex notation (`#ffffff50`), and CSP 3’s `strict-dynamic` directive is now available as well.
*   The [new Docker for Mac and Windows is finally production-ready](https://blog.docker.com/2016/07/docker-for-mac-and-windows-production-ready/) after several months in beta. Great news for all users who eagerly awaited it but always had issues with the previous version (i.e. disk and permission management problems).
*   Big news from Mozilla this week: With [Firefox 48](https://blog.mozilla.org/blog/2016/08/02/exciting-improvements-in-firefox-for-desktop-and-android/), the multi-process engine e10s is now enabled for many users, making Firefox much more robust, faster and more reliable. Also, [protection against harmful downloads has been improved](https://blog.mozilla.org/security/2016/08/01/enhancing-download-protection-in-firefox/) and unsigned/unverified add-ons won’t load anymore. [Web Extensions support](https://blog.mozilla.org/addons/2016/04/29/webextensions-in-firefox-48/) including CSP enforcements for web extensions is also new, just like the `about:debugging` developer page. For developers, the DevTools come with an improved font inspector, `calc()` is now supported for `line-height` and can be nested, and, last but not least, support for the CSP directive `upgrade-insecure-requests` has been added, too.
*   [Microsoft pushed Edge 14 this week](https://developer.microsoft.com/en-us/microsoft-edge/platform/changelog/desktop/14393/?compareWith=10586) and with it [a lot of great new things](https://blogs.windows.com/msedgedev/2016/08/04/introducing-edgehtml-14/). Notably, the new version got a lot of accessibility improvements and now competes as one of the best browsers in the [HTML5 Accessibility test](https://www.html5accessibility.com/). New features also include extensions and pinned tabs and performance got better to improve battery life, too. Fellow developers will be happy to hear about web notifications, the Fetch API, Beacon Interface, JavaScript’s `async\await`, and support for `<time>` and WOFF2.

{{% feature-panel %}}

<figure><a href="https://www.html5accessibility.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d3fddfa-c94a-4c00-b04a-7b70ac1af59a/html5-accessibility-opt.png" alt="Browsers’ score in terms of HTML5 accessibility." width="500" height="288" /></a><figcaption>The new version of Edge, Edge 14, got a lot of improvements and now scores 100% in the <a href="https://www.html5accessibility.com/">HTML5 Accessibility test</a>.</figcaption></figure>

## General

*   Dave Rupert reflected on [hidden expectations](https://daverupert.com/2016/08/hidden-expectations/) and why the hardest parts of the web are the ones the client doesn’t see. Accessibility, security, and performance serve very well as main examples for such hidden expectations.</p>

## Concept & Design

*   In our industry, it’s important to have [a connected workflow between design and development](https://simon.fyi/articles/aligning-design-and-development) to make sure we’re aligned and to make real collaboration possible. Subjects like “avoiding assumptions, team up with our peers or sharing knowledge” will help us work together in a better way, says Simon Colijn.</p>

## Tools & Workflows

*   Users don’t care what tools we use; they care when we ship something useful. A great presentation by Liz Abinante on the [simplicity of tooling](https://twitter.com/AndyHieb/status/761272450554269696) and [reasonable choices](https://speakerdeck.com/feministy/in-defense-of-static-sites).
*   We take GitHub for granted. We pay for it and we use it as the primary end point for our git-repositories. Now Fabio Akita shares why it’s the more expensive option and how you can [use the open-source alternative gitlab](https://www.akitaonrails.com/2016/08/03/moving-to-gitlab-yes-it-s-worth-it) on a pre-configured <abbr title="virtual private server">VPS</abbr> that is cheaper and more flexible. At least worth reading.</p>

## Security

*   Proofpoint published a very interesting [in-depth analysis of a big malvertising network](https://www.proofpoint.com/us/threat-insight/post/massive-adgholas-malvertising-campaigns-use-steganography-and-file-whitelisting-to-hide-in-plain-sight) that they found in the wild and that hid itself from plain sight by using steganography and file whitelisting. There’s evidence that they targeted a daily traffic of 1-5 million high-quality client hits.
*   Mathy Vanhoef and Tom Van Goethem presented a new HEIST-attack on HTTPS pages to steal SSNs, email addresses, and more. You can [view the slides](https://tom.vg/talks/BlackHatUSA2016_HEIST-presentation.pdf) (PDF) or [read the write-up](https://tom.vg/papers/heist_blackhat2016.pdf) (PDF) to understand the attack and what you can do to prevent it.
*   Mike West, one of the main persons pushing security web standards at the moment, proposes to [introduce an origin-wide policy manifest](https://discourse.wicg.io/t/proposal-set-origin-wide-policies-via-a-manifest/1617/4) to reduce the risk that security policies aren’t applied to specific resources. The proposal suggests to use a file in the `/.well-known/origin-policy/[name-goes-here]` directory on the origin server, adapting an already used folder name and path.
*   The well-known security researcher Jonathan Zdziarski found an issue in Whatsapp’s iOS app that seems wide-spread in iOS apps in general: [Deleted chats aren’t deleted](https://www.zdziarski.com/blog/?p=6143), which means that forensic experts could reconstruct them. Any app that uses SQLite on iOS has the same issue since deleted entries are only set “free” to be overwritten instead of actually deleted. In fact, Apple’s Messages app faces the same issues, and cloud sync makes this even worse as it spreads the deleted information to other devices. Jonathan finally shows how to implement an SQLite database in an iOS app to prevent this issue.

<figure><a href="https://www.zdziarski.com/blog/?p=6143"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0569eaa2-deaa-42f9-9876-6542a61617b0/forensic-artifacts-opt.png" alt="" width="500" height="270" /></a><figcaption>A wide-spread issue in iOS apps that use SQLite: <a href="https://www.zdziarski.com/blog/?p=6143">Deleted entries aren’t deleted</a> but only set free to be overwritten. (Image credit: <a href="https://www.zdziarski.com/blog/?p=6143">Jonathan Zdziarski</a>)</figcaption></figure>

## Privacy

*   The Battery Status API in general sounds like a great addition to our web platform. Initially built by Mozilla to complete the API-set on the web, we can use it on websites to reduce the amount of interactivity and animation or serve videos in low resolutions when the battery is nearly empty, for example. Lukasz Olejnik, however, found out that this API is actually [already used](https://go.lynxbroker.de/eat_heartbeat.js) as a user tracking identifier by ad networks and others. And last but not least, it can also be used to charge more for a service when a user’s battery is low — [as reportedly done by Uber](https://www.telegraph.co.uk/business/2016/05/22/uber-app-can-detect-when-a-users-phone-is-about-to-die/).</p>

## Web Performance

*   Mattias Geniar had a look at [Google’s new QUIC protocol](https://ma.ttias.be/googles-quic-protocol-moving-web-tcp-udp/) that uses UDP instead of TCP and manages to be more reliable and faster — an ideal candidate as a successor to the TCP protocol. While it’s still at an early stage, the IETF is considering to make it a standard, Google uses it for some of their services already, and several server and browser vendors have plans to implement it, too.
*   For very big websites, we often tend to use a CMS, as this seems to be the best option at first glance. But what about choosing a static site generator for better performance and less security risks? Stefan Baumgartner shares his experience with [using static site generators at scale](https://www.smashingmagazine.com/2016/08/using-a-static-site-generator-at-scale-lessons-learned/) and how they even built something like a content management system around it.</p>

## JavaScript

*   React is a bit different when it comes to technical design decisions. Chris James Hycner looks into [SVG icon systems for React.js](https://blog.goguardian.com/nerds/an-odyssey-to-find-a-sustainable-icon-system-with-svgs-in-react) and how to build a well-working module for it.
*   “Add this JS-snippet to the project.” — a request that developers hear quite often. Kevin J. Dolan shares his eye-opening experience with a QA-person on why it’s a very, very bad idea to follow such requests blindly and [why you shouldn’t include external third-party JavaScript references without extensive reviews](https://tech.metriccollective.com/of-course-ill-let-you-execute-arbitrary-javascript-code-in-my-users-browsers-3032eca3480e).
*   Ben Frain explains the [native JavaScript array methods](https://benfrain.com/understanding-native-javascript-array-methods/) and how they differ from each other. A great introduction (or reminder) of what we can use today to get data out of arrays.</p>

## CSS/Sass

*   For long articles, a scroll indicator can be very useful to indicate the reading progress. Most people use some sort of JavaScript code to do this (which is calculation-expensive); some people, however, find clever tricks to do it with CSS. The [CSS-only scroll indicator](https://codepen.io/MadeByMike/pen/ZOrEmr?editors=0100) by Mike Riethmuller is an awesome show-off of using gradients, viewport units and a pseudo-element.

{{< codepen height="265" theme_id="0" slug_hash="ZOrEmr" default_tab="result" caption="CSS-only scroll indicator by Mike Riethmuller." >}} <a href="https://codepen.io/MadeByMike/pen/ZOrEmr/">CSS only scroll indicator</a> by Mike Riethmuller (<a href="https://codepen.io/MadeByMike">MadeByMike</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## Work & Life

*   Hannah Rosefield [puts exhaustion, the ‘status symbol’ of today, into perspective](https://newrepublic.com/article/135468/exhaustion-became-status-symbol).
*   Tom Bartel shares some great thoughts on [recalibrating your productivity sensors as a developer](https://www.tombartel.de//2016/07/05/recalibrate-your-productivity-sensors/). Reframe your work, whether it’s managing people, talking to others, or actual coding work whenever you think you’re not productive. Most of the time it’s simply untrue.</p>

## Going Beyond…

*   Simon St. Laurent on [decentralizing the web](https://www.oreilly.com/ideas/decentralize-now). Some useful thoughts about our current lock-in on technology, service providers, and centralized solutions, and how we might be able to break that up again to unlock the real power of the web.
*   Katharine Viner writes about [how social media swallowed the news](https://www.theguardian.com/media/2016/jul/12/how-technology-disrupted-the-truth) and how the consequences of this go far beyond journalism. Does the truth even matter any more? An interesting essay on how well-done social marketing has an enormous influence on the decisions people make — no matter if it’s about buying a product or making a political decision.
*   Since the financial crisis, the private equity industry has become hugely influential. The New York Times curated a lovely, interactive story about [how private equity plays out in your daily life](https://www.nytimes.com/interactive/2016/08/02/business/dealbook/this-is-your-life-private-equity.html?_r=0).

<em>And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</em>

{{< signature "ah" >}}


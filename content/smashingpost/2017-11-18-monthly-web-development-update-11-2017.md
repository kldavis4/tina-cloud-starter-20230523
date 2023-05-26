---
title: >-
  Monthly Web Development Update 11/2017: Browser News, KRACK and Vary Header
  Caching
slug: monthly-web-development-update-11-2017
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea7fe146-23b1-4405-9715-bfe12a9c10f5/monthly-web-development-update-november-2017-opt.png
date: 2017-11-18T00:14:15.000Z
author: anselm-hannemann
description: >-
  _Editor’s Note: Our dear friend Anselm Hannemann summarizes what happened in
  the web community in the past few weeks in one handy list, so that you can
  catch up on everything new and important. Enjoy!_

  Welcome back to our monthly reading list. Before we dive right into all the
  amazing content I stumbled upon — admittedly, this one is going to be quite a
  long update — I want to make a personal announcement. This week I launched a
  personal project called Colloq, a new conference and event service for users
  and organizers. If you’re going to events or are organizing one or if you’re
  interested in the recorded content of conferences, this could be for you. So
  if you like, go ahead and check it out.
categories:
  - Web Development Reading List
---
_Editor’s Note: Our dear friend Anselm Hannemann summarizes what happened in the web community in the past few weeks in one handy list, so that you can catch up on everything new and important. Enjoy!_

Welcome back to our monthly reading list. Before we dive right into all the amazing content I stumbled upon — admittedly, this one is going to be quite a long update — I want to make a personal announcement. This week I launched a personal project called [Colloq](https://colloq.io/), a new conference and event service for users and organizers. If you’re going to events or are organizing one or if you’re interested in the recorded content of conferences, this could be for you. So if you like, go ahead and check it out.

In this issue, we’ll focus on some usually rather underaddressed things, such as numerals in web typography, variable fonts, or the image `async` attribute that’s coming to Chrome soon. So without further ado, let’s get started.</p>

## News

*   WebKit just got [support for the Touch Bar Web API](https://trac.webkit.org/changeset/224457/webkit/) that will make use of the `menuitem`. It’s still in WebKit trunk currently and likely to land in Safari next year at the earliest.
*   [Chrome 62 was released this week](https://developers.google.com/web/updates/2017/10/nic62) with some important updates to the Network Information API that now reflects the actual connection type even when tethering. Support for OpenType Variable Fonts and Media Capture from DOM elements also landed in the new version. Notably, Chrome 62 on iOS got support for the Payment Request API which is interesting because the iOS WebKit doesn’t support it yet in stable channel. It seems that they used a custom extension to support this feature. Might get interesting to see what else could be supported this way.
*   This [week’s Safari Technology Preview 42](https://webkit.org/blog/8001/release-notes-for-safari-technology-preview-42/) brings along `font-display` loading behaviors and `<link rel=preconnect>` support.
*   With the new Windows 10 fall update, [Edge 16 is pushed to customers](https://blogs.windows.com/msedgedev/2017/10/17/edgehtml-16-fall-creators-update/) — with full CSS Grid support, `object-fit` and `object-position`, the Payment Request API, Service Worker preview behind flags, and Motion Controllers in WebVR.

{{% feature-panel %}}

<figure><a href="https://blogs.windows.com/msedgedev/2017/10/17/edgehtml-16-fall-creators-update/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf93ea66-f241-4d65-a8ce-cb6900a05d6a/edge-motion-controllers-opt.png" width="800" height="448" alt="Motion controllers in Edge" /></a><figcaption><a href="https://blogs.windows.com/msedgedev/2017/10/17/edgehtml-16-fall-creators-update/">WebVR for Edge</a> has added support for motion controllers that allow for fine grained interaction with digital objects in virtual reality. (<a href="https://blogs.windows.com/msedgedev/2017/10/17/edgehtml-16-fall-creators-update/">Image credit</a>)</figcaption></figure>

## General

*   Kailash Ahirwar has created [essential cheat sheets for machine learning and deep learning engineers](https://startupsventurecapital.com/essential-cheat-sheets-for-machine-learning-and-deep-learning-researchers-efb6a8ebd2e5). A massive resource and very recommended if you’re working with any of these engines.
*   David Yates’ plea for “[RSS: there’s nothing better](https://davidyat.es/2017/05/18/rss-nothing-better/)” is a thoughtful column that praises the idea of the good old RSS over the siloed, algorithm-driven feeds of social media services.</p>

## UI/UX

*   Right-to-left development is quite hard already but [designing for mobile design is a challenge](https://www.smashingmagazine.com/2017/11/right-to-left-mobile-design/).
*   [Inter UI](https://rsms.me/inter/) is a nice, completely free to use open-source font family optimized for screen readability.
*   Adobe announced [the first stable version of their screen design tool XD](https://blogs.adobe.com/creativecloud/whats-next-for-adobe-xd-cc/) at this year’s MAX conference. Besides a lot of smaller improvements, XD now supports sharing, as well as first-class integrations of third-party tools like Zeplin and Sympli. Apart from that, Adobe provided major updates for nearly all their software products during the event.
*   InVision had a big announcement to make this week: They are going to bring a new screen design tool called “[Studio](https://www.invisionapp.com/studio)” to the market in January and now invite beta testers to preview it.

<figure><a href="https://www.invisionapp.com/studio"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04da094a-4df4-482e-a4f6-4541f1b632bb/studio-opt.png" width="800" height="488" alt="Studio" /></a><figcaption>InVision announced <a href="https://www.invisionapp.com/studio">Studio</a>, a new screen design tool that will be released publicly in January. (<a href="https://www.invisionapp.com/studio">Image credit</a>)</figcaption></figure>

## Web Performance

*   Vlad Krasnov got the chance to compare the newest server processors at Cloudflare. The results are pretty interesting: Qualcomm achieves a similar performance as the fastest Intel processors, but it [needs about 30% less power](https://blog.cloudflare.com/arm-takes-wing/), sometimes even less. So while newer Qualcomm chips might have some issues with software incompatibilities, it’s going to be interesting what will happen on the server market. Especially with large data centers in mind where saving energy is quite important — not only because our planet benefits from less power consumption but also because it’s cheaper.
*   David Jonathan Ross [compared the file sizes of normal web fonts to a variable font file](https://stuff.djr.com/gimlet-vf-size-test/). Depending on how many font styles are used on a website, you can save 44% with a variable font.
*   Nikita Prokopov shares how one single option that Chrome promoted [ruined the performance of his web application](https://tonsky.me/blog/chrome-intervention/).
*   Andrew Betts summed up his knowledge about a great HTTP feature in the article “[Understanding The Vary Header](https://www.smashingmagazine.com/2017/11/understanding-vary-header/)”.
*   Chrome is implementing an [`async` attribute for HTMLImageElement and SVGImageElement](https://www.chromestatus.com/feature/4897260684967936). It’ll have two states: “On” will indicate that the developer prefers responsiveness and performance over the atomic presentation of image and non-image content, while “off” will indicate that the developer prefers atomic presentation of content over responsiveness.
*   Alexey Ivanov shares [how to optimize web servers for high throughput and low latency](https://blogs.dropbox.com/tech/2017/09/optimizing-web-servers-for-high-throughput-and-low-latency/). But please note: These are small, fine-tuning methods that can be very useful but we should apply them one after another, measure them and then decide if they are useful for the project or not. A thoughtful post that gives us insights into how the Dropbox team improves their edge network servers.</p>

## Tooling

*   [Webpack Monitor](https://webpackmonitor.com/) is a nice dashboard for your JavaScript toolchain. It gives insights into bundle size, the individual parts of the bundle and how the bundle and its size change over time. With tips for optimizing the output, the dashboard is quite useful if you care about reducing the payload for users on your website.

<figure><a href="https://webpackmonitor.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d122677-02a1-4e2b-a47c-d2fa3e660cf1/webpack-monitor-opt.png" width="800" height="570" alt="Webpack Monitor" /></a><figcaption><a href="https://webpackmonitor.com/">Webpack Monitor</a> displays your bundle so you can make informed decisions about your optimizations. (<a href="https://webpackmonitor.com/">Image credit</a>)</figcaption></figure>

## Security

*   This week, the [“KRACK”-attack](https://www.krackattacks.com/) was widely discussed. It’s effectively breaking WPA2 encryption on most WiFi hardware. But vendors aren’t sleeping, some already updated their systems and offer software updates for the devices which you should patch as soon as possible. One thing to note here is that websites that use HSTS preloading aren’t affected by the issue, which reminds us that we should consider adding this header to our websites.</p>

## Privacy

*   We know targeted ads can be a bit frightening sometimes when they show up and are incredibly accurate. With mobile ads, it’s even worse: Andy Greenberg shares a study that shows that [it takes only $1000 to track someone’s location using mobile ads](https://www.wired.com/story/track-location-with-mobile-ads-1000-dollars-study).</p>

## Accessibility

*   Scott Vinkle explains how we can [create accessible React apps](https://simplyaccessible.com/article/react-a11y/).
*   Laura Kalbag wrote a book called “[Accessibility for Everyone](https://abookapart.com/products/accessibility-for-everyone)”. Here’s a [short excerpt](https://alistapart.com/article/planning-for-accessibility) explaining how to plan for accessibility.</p>

## CSS

*   Vincent De Oliveira wrote about [the amazing CSS `element()` function](https://iamvdo.me/en/blog/css-element-function) which is only available in Firefox currently (but that might change). Actually, it’s not even a new function, but it allows us to use images from the HTML DOM in our CSS, e.g. for a background-image.
*   Richard Rutter wrote a guide about how to [use old-style numerals on the web](https://alistapart.com/article/web-typography-numerals) with the `font-variant-numeric` CSS property, if available. Proper sub- and superscripts are explained, too, and we can learn when to use which feature for a specific purpose.

<figure><a href="https://alistapart.com/article/web-typography-numerals"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39965034-7e06-464e-a20e-1ac92fbe0096/web-typography-opt.png" width="800" height="300" alt="Web typography" /></a><figcaption>Medieval scribes and Renaissance printers placed notes in the margins rather than at the bottom — no need for superscripts. But <a href="https://alistapart.com/article/web-typography-numerals">how should we handle sub- and superscripts on the web</a>? (Image credit: <a href="https://www.e-codices.unifr.ch/en/sbe/0172/20">Einsiedeln, Stiftsbibliothek, Codex 172(1128)</a>, via <a href="https://alistapart.com/article/web-typography-numerals">Richard Rutter</a>)</figcaption></figure>

## JavaScript

*   Lea Verou shares how we can use [different remote and local resource URLs with Service Workers](https://lea.verou.me/2017/10/different-remote-and-local-resource-urls-with-service-workers/).
*   Dustin Driver explains the fundamentals of the Firefox Debugger and [how to go beyond `console.log`](https://hacks.mozilla.org/2017/11/go-beyond-console-log-with-the-firefox-debugger/).
*   Jake Archibald wrote about [Netflix removing client-side React](https://jakearchibald.com/2017/netflix-and-react/) and why this step makes the site more robust while still benefiting from the advantages of React.
*   GitHub open-sourced their own [client-side accessibility error scanner](https://github.com/github/accessibilityjs). It’s basically a JavaScript module that you import into your codebase, and that then reports back basic issues such as images without `alt` attribute, links without labels and similar accessibility errors.</p>

## Work & Life

*   200 universities just launched 560 free online courses. Here’s [the full list](https://medium.freecodecamp.org/200-universities-just-launched-560-free-online-courses-heres-the-full-list-d9dd13600b04).</p>

## Going Beyond…

*   The Guardian recently published an interesting article called “[Ashamed to work in Silicon Valley: how techies became the new bankers](https://www.theguardian.com/technology/2017/nov/08/ashamed-to-work-in-silicon-valley-how-techies-became-the-new-bankers)”. Seeing that working at tech giants like Facebook is considered negatively by a growing number of people is something I didn’t expect. The article also shares that employees at such companies are even ashamed of their jobs — an interesting change when you remember how most people craved to land a job at one of these companies only until this year.
*   It’s a common question that I’ve asked myself quite often in the past that now has been answered: [Electric cars emit significantly fewer greenhouse gases over their lifetimes](https://www.theguardian.com/environment/2017/oct/25/electric-cars-emit-50-less-greenhouse-gas-than-diesel-study-finds) as diesel engines, as a new study found out. Even when they are powered by the most carbon-intensive energy.
*   A chatbot called DoNotPay has saved motorists millions in parking fines — without charging a cent. [Its next target: divorce law](https://www.wsj.com/articles/this-robot-will-handle-your-divorce-free-of-charge-1509022800). And airlines, landlords, and telemarketers will follow, too, in the future.

_We hope you enjoyed this Web Development Update. The next one is scheduled for December 15th. Stay tuned!_


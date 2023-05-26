---
title: >-
  Web Development Reading List: Announcing Changes, A Design Kit, DNA Malware,
  And Why Meaning Is An Advantage
slug: web-development-reading-list-announcing-changes
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c40a864b-21c3-4958-be5c-c6c3d4ff15a3/wdrl-announcing-changes-opt.png
date: 2017-08-18T18:00:52.000Z
author: anselm-hannemann
description: >-
  _You might have noticed it already: in the past few weeks you might have
  missed Anselm's [Web Development Reading
  List](https://www.smashingmagazine.com/tag/web-development-reading-list/)
  issues here on SmashingMag. No worries, from now on, we’ll switch to
  collecting the most important news of each month in **one handy, monthly
  summary** for you. If you'd like to continue reading Anselm's weekly reading
  list (and we encourage you to!), you can still do so [via
  email](https://wdrl.info/), on [wdrl.info](https://wdrl.info/) or via
  [RSS](https://wdrl.info/feed)._ — Editorial Team

  Hello again! I’ll continue publishing this resource and am grateful for
  everyone who supports my ongoing work. And to celebrate the last weekly
  edition, I found a lot of great articles for you: Biohacking news that sound
  like science fiction, advances in deep learning with JavaScript, and a lot
  more. Happy reading!
categories:
  - Web Development Reading List
---
Hello again! I’ll continue publishing this resource and am grateful for everyone who supports my ongoing work. And to celebrate the last weekly edition, I found a lot of great articles for you: Biohacking news that sound like science fiction, advances in deep learning with JavaScript, and a lot more. Happy reading!

## News

*   The upcoming [Chrome 61](https://blog.chromium.org/2017/08/chrome-61-beta-javascript-modules.html) (in beta channel now) brings support for JavaScript modules, the Payment Request API on desktop, `smooth-scrolling` in CSS, 8-digit hex colors (with alpha transparency), and the new `Expect-CT` HTTP header.
*   Edward Thomson shares [why you should upgrade your git installation](https://www.edwardthomson.com/blog/upgrading_git_for_cve2017_1000117.html) to 2.14.1 to fix vulnerabilities.
*   Microsoft will [change their Edge rendering engine](https://blogs.windows.com/msedgedev/2017/08/17/making-web-smoother-independent-rendering/), making it independent of and asynchronous to the main thread.
*   This week, Opera announced [the end of Opera Max](https://blogs.opera.com/mobile/2017/08/upcoming-changes-opera-max/), their data-saving browser product. The service will still stay active for a while but probably not for too long.</p>

## UI/UX

*   The Facebook design team shares a [Sketch template full of design elements found in macOS](https://facebook.design/desktopkit). And if you’re looking for iOS GUI resources, [they’ve got you covered](https://facebook.design/ios10), too.

{{% feature-panel %}}

<figure><a href="https://facebook.design/desktopkit"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd16a8f7-821c-424e-815f-603c2186fc20/macos-desktop-kit-opt.png" width="800" height="471" alt="macOS Desktop Kit" /></a><figcaption>The macOS <a href="https://facebook.design/desktopkit">Desktop Kit</a> includes desktop application and web UI elements a designer could need when building a user flow through a web app or constructing a Mac interface. (<a href="https://facebook.design/desktopkit">Image credit</a>)</figcaption></figure>

## Tooling

*   [Puppeteer](https://github.com/GoogleChrome/puppeteer) is a Node.js library that provides an API to control headless Chrome. It can also be configured to use full (non-headless) Chrome.</p>

## Security

*   Biohackers found a way to [encode malware into a strand of DNA](https://www.wired.com/story/malware-dna-hack) so that the gene sequencer will get infected once it analyzes the DNA.
*   Pavel Durov shares why [they chose not to use end-to-end encryption by default at Telegram](https://telegra.ph/Why-Isnt-Telegram-End-to-End-Encrypted-by-Default-08-14). An interesting point of view that gives more insights into why Telegram is different from other messengers.</p>

## Web Performance

*   Andreya Grzegorzewski explains how we can [use the Cache API for offline POST requests](https://medium.com/web-on-the-edge/offline-posts-with-progressive-web-apps-fc2dc4ad895) in Progressive Web Apps. This super cool trick allows us to queue POST requests, such as a form submission/data upload, cache it, and send it to the server once the user is back online.</p>

## HTML & SVG

*   If you want to use `<details>`/`<summary>` elements together with `rem` font-size values on your site, be aware that there’s a bug in Safari that renders parts of a website with that CSS combination useless. After tracking it down and debugging it, I finally [summarized the case](https://colloq.io/blog/safaris-detailssummary-rem-font-size-issue).</p>

## Accessibility

*   Eva Ferreira shares [ten guidelines to improve your web accessibility](https://aerolab.co/blog/web-accessibility/) — from reliance on colors to proper markup and other tips.

<figure><a href="https://aerolab.co/blog/web-accessibility/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47fbf74b-9112-4d71-b517-e42f3781a724/accessibility-guidelines-opt.png" width="800" height="437" alt="10 guidelines to improve your web accessibility" /></a><figcaption>Eva Ferreira shares <a href="https://aerolab.co/blog/web-accessibility/">ten web accessibility guidelines</a> to guarantee access to your site to any person, in spite of disabilities. (<a href="https://aerolab.co/blog/web-accessibility/">Image credit</a>)</figcaption></figure>

## JavaScript

*   [deeplearn.js](https://github.com/tambien/deeplearnjs) is a hardware-accelerated machine intelligence library for the web. You can use it to build and train neural networks in your browser, to play color sequences or detect objects in images, for example.
*   [flatpickr](https://chmln.github.io/flatpickr/) is a dependency-free, lightweight and powerful datetime picker.
*   Peter Kröner shares how he achieved [immutable arrays and objects in JavaScript in only 33 lines](https://www.microsofttranslator.com/bv.aspx?from=&to=en&a=http%3A%2F%2Fwww.peterkroener.de%2Fimmutable-arrays-und-objekte-fuer-javascript-mit-proxies%2F) (German article, automatically translated) without any library with ECMAScript Proxies.</p>

## CSS

*   This nice Codepen experiment by Giana shows that you can [create beautiful directionally-aware hover effects only with CSS](https://codepen.io/giana/pen/YZWjQy).

<figure><a href="https://codepen.io/giana/pen/YZWjQy"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc8f974d-2662-41b9-989d-403065cbcb83/directionally-aware-hover-opt.png" width="800" height="464" alt="CodePen Directionally-Aware Hover Only With CSS" /></a><figcaption>Giana uses <code>:hover</code> and the sibling selector to apply different styles to elements based on their position and, thus, create a <a href="https://codepen.io/giana/pen/YZWjQy">CSS-only, directionally-aware hover effect</a>.</figcaption></figure>

## Work & Life

*   Christian Heilmann wrote about [why he wants to take a break and change his work life](https://christianheilmann.com/2017/08/16/taking-a-break-and-so-should-you/) to be more productive and focus on coaching others. A good read.</p>

## Going Beyond…

*   John Battelle [compares our addiction to social media with tobacco](https://shift.newco.co/is-social-media-the-new-tobacco-936d28a2bfe2). This is not how we want to raise our children.
*   Darius Foroux on why [you should spend less time in your head](https://getpocket.com/explore/item/stop-spending-so-much-time-in-your-head-1381441550), thinking, worrying, stressing, but exercise pragmatism instead. An article about mastering your mind and realizing that most of our thoughts cannot make it into practice.
*   Bernadette Jiwa shares her thoughts on [why meaning is a competitive advantage](https://thestoryoftelling.com/meaning-advantage/) and why we are fortunate that we can pursue our passion in our work.

_—Anselm_


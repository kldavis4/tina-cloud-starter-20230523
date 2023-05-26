---
title: >-
  Web Development Reading List #176: Safari 10.1, Prompt()-Deprecation, And
  Professional Pride
slug: web-development-reading-list-176
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11a8bafa-0982-4b41-8ab1-6c58aad3c8ec/wdrl-176-opt.png'
date: 2017-03-31T18:48:51.000Z
author: anselm-hannemann
description: >-
  What a busy week! To stay on top of things, let’s review what happened in the
  web development world the last few days — from browser vendors pushing new
  updates and building new JavaScript guidelines and security standards to why
  we as web professionals need to **review our professional pride**. How can we
  properly revoke certificates in browsers, for example? And how can we build
  accessibility into a style guide? Let’s take a look.

  Safari 10.1 was announced a while ago already, and this week it finally came
  to Macs and iOS devices around the world. The new Safari version ships CSS
  Grid Layouts, `fetch()`, IndexedDB2.0, Custom Elements, Form Validation, Media
  Capture, and much more.
categories:
  - Web Development Reading List
---
### <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Make Modal Windows Better For Everyone](https://www.smashingmagazine.com/2014/09/making-modal-windows-better-for-everyone/)
*   [Creating A Living Style Guide: A Case Study](https://www.smashingmagazine.com/2016/05/creating-a-living-style-guide-case-study/)
*   [How To Integrate Motion Design In The UX Workflow](https://www.smashingmagazine.com/2016/03/integrate-motion-design-animation-ux-workflow/)
*   [Smart Transitions In User Experience Design](https://www.smashingmagazine.com/2013/10/smart-transitions-in-user-experience-design/)

## News

*   Safari 10.1 was announced a while ago already, and this week it finally came to Macs and iOS devices around the world. The new Safari version ships CSS Grid Layouts, `fetch()`, IndexedDB2.0, Custom Elements, Form Validation, Media Capture, and much more. You can read more about the [new features and how to use them](https://webkit.org/blog/7477/new-web-features-in-safari-10-1/) in detail on the WebKit blog.
*   Chromium [is advising developers to not use `alert()`, `confirm()`, and `prompt()` methods in JavaScript anymore](https://developers.google.com/web/updates/2017/03/dialogs-policy), and, in the future, they might even deprecate sites that still use them. The suggestion is to use the Web Notification API instead, in the hope that its asynchronous nature will prevent it from being misused against users. As a nice side effect, using the API will also speed up browser performance significantly.
*   This week, Mozilla started with their [Security/Binary Transparency](https://wiki.mozilla.org/Security/Binary_Transparency) project which allows third parties to verify that binaries from Mozilla match the original public source code exactly and also to check for its integrity. This is a huge step in open-source and binary app development that other applications out there would benefit from, too.
*   The Chromium project is [implementing](https://groups.google.com/a/chromium.org/forum/#!topic/blink-dev/uKO1CwiY3ts) the WICG proposal of a [Feature Policy](https://wicg.github.io/feature-policy/) ([see launch status](https://www.chromestatus.com/feature/5694225681219584)), an interesting concept to complete other policies such as the Content Security Policy. By allowing site owners to explicitly allow or disallow browser features such as geolocation, webcam/microphone access and similar things, sites can better protect their users from exploits.

{{% feature-panel %}}

<figure><a href="https://wiki.mozilla.org/Security/Binary_Transparency"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbe6febb-a75e-480c-b05a-05851850120a/binary-transparency-opt.png" width="699" height="357" alt="Binary Transparency" /></a><figcaption>As a protection against compromised binaries, Mozilla’s <a href="https://wiki.mozilla.org/Security/Binary_Transparency">Security/Binary Transparency project</a> allows third parties to verify that all Firefox binaries are public. (<a href="https://wiki.mozilla.org/Security/Binary_Transparency">Image credit</a>)</figcaption></figure>

## General

*   Jens Grochtdreis shared his thoughts on [professional pride](https://medium.com/@Flocke/professional-pride-7b84287ae747), aiming at all the people who write JavaScript tutorials without focusing on the HTML or CSS. A bad practice that leads to incomplete and sometimes even false code examples that are then used in the wild.</p>

## Concept & Design

*   We all know the annoying overlays that prompt website visitors to take action — “sign up for the newsletter”, “like the page on Facebook”. Bureau of Programming now shares thoughts on why it was easier to get rid of annoying pop-up windows and [why it’s up to us developers to not build annoying features](https://python.sh/2017/3/i-dont-want-to-subscribe-to-your-newsletter) if we want to make the web a useful, friendly place.

<figure><a href="https://python.sh/2017/3/i-dont-want-to-subscribe-to-your-newsletter"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba18d8b6-5e7d-43d4-b443-5360fd86aa31/popup-modals-opt.png" width="800" height="419" alt="Pop-Up Modals" /></a><figcaption>Pop-up modals are annoying and make a site unnecessarily hard to use. Bureau of Programming summarized the dilemma and <a href="https://python.sh/2017/3/i-dont-want-to-subscribe-to-your-newsletter">what we can do against it</a>.</figcaption></figure>

## Security

*   A new paper from a joint venture of universities and Akamai Technologies introduces CRLite, [a scalable system for pushing all TLS revocations to all browsers](https://www.ccs.neu.edu/home/cbw/static/pdf/larisch-oakland17.pdf) (PDF, 1.3MB). Currently, no major browser fully checks for TLS/SSL certificate revocations, but that could be changing soon if vendors agree with this research paper and start implementing the system.</p>

## Accessibility

*   Carie Fisher shares her approach to a [style guide that has accessibility guidelines built in](https://a11y-style-guide.com/style-guide/).</p>

## CSS/Sass

*   Paul Lewis and Stephen McGruer summarized [how you can build performant ‘expand’ and ‘collapse’ animations](https://developers.google.com/web/updates/2017/03/performant-expand-and-collapse), for menus, for example.</p>

## Going Beyond…

*   Scientists came up with a [detailed “roadmap” for meeting the Paris climate goals](https://www.vox.com/energy-and-environment/2017/3/23/15028480/roadmap-paris-climate-goals). It’s an eye-opening, entertaining read that convinces with its storytelling style.
*   Emily Dreyfuss from WIRED wrote an article about why Silicon Valley contributes to inequality by focusing on cool technological innovation instead of targeting real-world problems. The piece is titled “[Silicon Valley Would Rather Cure Death Than Make Life Worth Living](https://www.wired.com/2017/03/silicon-valley-rather-cure-death-make-life-worth-living/)” — a provocative but probably accurate title. And while there sure are exceptions (as there are always exceptions), we should remember to not blindly glorify tech, especially if it doesn’t engage with real problems.
*   Ken Doctor wrote about “[slower structural developments that shape society](https://www.niemanlab.org/2017/03/slower-structural-developments-that-shape-society-a-qa-with-de-correspondent-editor-rob-wijnberg/),” charting out what’s in between the extremes that we see in the news.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_


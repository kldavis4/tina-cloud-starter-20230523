---
title: >-
  Web Development Reading List #174: The Bricks We Lay, Remynification, And
  0-RTT
slug: web-development-reading-list-174
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62a74eec-3b0d-4b8c-a8bf-dc8392aceed0/wdrl-174-opt.png'
date: 2017-03-17T18:34:04.000Z
author: anselm-hannemann
description: >-
  We’re all designers. Whether we do a layout, a product design or write code to
  design a product technically doesn’t matter here. What does matter though, is
  that we always **take the context of a project into consideration**. Because
  as someone shaping a project so that it is appealing to the clients and works
  in the best way possible for the target audience, we have a pretty big
  responsibility.

  Imagine architects building a wall out of recycled material that also looks
  nice — sounds pretty great, right? But seen in the context that this will be a
  wall that divides people and encourages racism and even more inequality in our
  society, our first impression of the undertaking suddenly shifts into the
  opposite direction. We have to make new decisions every time we start a new
  project, and seeing things in context is crucial to live up to our
  responsibility — both in our work and our lives.
categories:
  - Web Development Reading List
---
Imagine architects building a wall out of recycled material that also looks nice — sounds pretty great, right? But seen in the context that this will be a wall that divides people and encourages racism and even more inequality in our society, our first impression of the undertaking suddenly shifts into the opposite direction. We have to make new decisions every time we start a new project, and seeing things in context is crucial to live up to our responsibility — both in our work and our lives.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Getting The Sketch Workflow Right: Meet “The Sketch Handbook”](https://www.smashingmagazine.com/sketch-handbook/)
*   [A Glimpse Into The Future With React Native For Web](https://www.smashingmagazine.com/2016/08/a-glimpse-into-the-future-with-react-native-for-web/)
*   [Front-End Performance Checklist 2017 (PDF, Apple Pages)](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)

## News

*   We waited for this update 2.5 years, now [Microsoft is finally working on `object-fit` and `object-position` for Microsoft Edge](https://wpdev.uservoice.com/forums/257854-microsoft-edge-developer/suggestions/6263790-object-fit-and-object-position). A great step towards better web compatibility and I really hope that it’ll land in an official build soon.
*   With Sketch 43, the app developers announced that [the Sketch file format will be open-source](https://medium.com/sketch-app-sources/sketch-43-is-coming-to-town-with-a-new-game-an-open-file-format-ae62e7e7c223) from now on. This is great news because it means that everyone will be able to build a Windows app or a Sketch file viewer app. Since the format of choice will be JSON, we can even think of building automation for files via web services.

{{% feature-panel %}}

<figure><a href="https://medium.com/sketch-app-sources/sketch-43-is-coming-to-town-with-a-new-game-an-open-file-format-ae62e7e7c223#.y94mlusbd"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ee00ab2-240f-4f62-bffa-1ab1c3a3702f/sketch-plugins-opt.png" width="800" height="602" alt="Plugins in Sketch" /></a><figcaption>Sketch already benefits from a thriving third-party plugin ecosystem and thanks to it’s new open-source file format, Sketch 43 will <a href="https://medium.com/sketch-app-sources/sketch-43-is-coming-to-town-with-a-new-game-an-open-file-format-ae62e7e7c223">enable even more powerful integrations</a> for third-party developers. (<a href="https://medium.com/sketch-app-sources/sketch-43-is-coming-to-town-with-a-new-game-an-open-file-format-ae62e7e7c223#.y94mlusbd">Image credit</a>)</figcaption></figure>

## General

*   Ethan Marcotte wrote a thought-provoking article about “[the bricks we lay](https://ethanmarcotte.com/wrote/the-bricks-we-lay/)”. In it, he describes a situation where people do work claiming they’re only focusing on the task they do and therefore are apolitical. But your work is never neutral.
*   In the last edition of the web development reading list, I shared [the first part](https://www.smashingmagazine.com/2017/03/world-wide-web-not-wealthy-western-web-part-1/) of Bruce Lawson’s story about the “World Wide Web, Not Wealthy Western Web”. Today comes the [second part](https://www.smashingmagazine.com/2017/03/world-wide-web-not-wealthy-western-web-part-2/) of the mandatory read of this week.</p>

## Tools & Workflows

*   Remy Luisant came up with a tool that optimizes your CSS output just a little bit better than you’re used to: [CSS Remynification](https://luisant.ca/remynifier).
*   [Bit](https://github.com/teambit/bit) is an interesting concept of a distributed virtual component repository that combines a lot of existing strategies into one universal component manager.</p>

## Security

*   Maybe it’s still not a good idea to use a messenger that’s build to gather as much data as it can, as a recent data leak of [Google’s Allo messenger shows](https://www.recode.net/2017/3/13/14912394/google-allo-search-history-privacy-messaging-app).
*   Scott Arciszewski explains why [JOSE (Javascript Object Signing and Encryption) is a bad standard that everyone should avoid](https://paragonie.com/blog/2017/03/jwt-json-web-tokens-is-bad-standard-that-everyone-should-avoid). Note that JOSE is part of JSON Web Tokens to which not all of the complaints and issues apply.
*   Researchers just [broke MAC address randomization](https://www.bleepingcomputer.com/news/security/researchers-break-mac-address-randomization-and-track-100-percent-of-test-devices/) and tracked 100% of the test devices, including Android and Apple devices.</p>

## Web Performance

*   Nick Sullivan from Cloudflare explains how they [enabled Zero Round Trip Time Resumption for all free users](https://blog.cloudflare.com/introducing-0-rtt/), now serving TLS 1.3 for better performance.
*   This week, Google announced their project [Guetzli](https://research.googleblog.com/2017/03/announcing-guetzli-new-open-source-jpeg.html), a new open source JPEG encoder that can save up to 35% of file size. This is great, but to put things into perspective, we also have to consider that it’s [up to 100 times slower](https://mobile.twitter.com/kornelski/status/842513840898228224) as Mozilla’s mozJPEG encoder and in many cases it doesn’t achieve the same quality at the same file size either.
*   Jacob Beltran shares [lessons learned from optimizing performance in React applications](https://blog.vixlet.com/react-at-light-speed-78cd172a6411).

<figure><a href="https://blog.cloudflare.com/introducing-0-rtt/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfcb4447-b3b2-400e-8862-ccb53094c665/0-rtt-opt.png" width="800" height="445" alt="0-RTT" /></a><figcaption>With 0-RTT, encrypted HTTPS requests become <a href="https://blog.cloudflare.com/introducing-0-rtt/">just as fast as unencrypted HTTP requests</a>. (<a href="https://blog.cloudflare.com/introducing-0-rtt/">Image credit</a>)</figcaption></figure>

## JavaScript

*   Firefox 52 hit the release channel last week, and it [includes a few changes to `setTimeout()` and `setInterval()`](https://blog.wanderview.com/blog/2017/03/13/firefox-52-settimeout-changes/). Please read this update post and check if your code still works as expected.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_


---
title: >-
  Web Development Reading List #179: Firefox 53, The Top Web Browsers, And
  Vue.js Authentication
slug: web-development-reading-list-179
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50166d5d-bbd2-420a-8b3b-974787da760e/wdrl-179-opt.png'
date: 2017-04-21T19:59:10.000Z
author: anselm-hannemann
description: >-
  Bots and Artificial Intelligence are probably the most hyped concepts right
  now. And while some people praise the existing technologies, others claim they
  don’t fear AI at all, citing examples where it fails horribly. Examples of
  Facebook or Amazon advertising (both claim to use machine learning) that don’t
  match our interests at all are quite common today.

  But what happens if we look at **autonomous cars, trains or planes** that have
  the very same machine learning technologies in place? How about the military
  using AI for its actions? While we’re still experimenting with these capable
  technologies, we also need to consider the possible consequences, the
  responsibilities that we have as developers and how all of this might affect
  the people the technology is being served to.
categories:
  - Web Development Reading List
---
But what happens if we look at **autonomous cars, trains or planes** that have the very same machine learning technologies in place? How about the military using AI for its actions? While we’re still experimenting with these capable technologies, we also need to consider the possible consequences, the responsibilities that we have as developers and how all of this might affect the people the technology is being served to.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [The Current State Of Authentication: We Have A Password Problem](https://www.smashingmagazine.com/2016/06/the-current-state-of-authentication-we-have-a-password-problem/)
*   [Conversational Design Essentials: Tips For Building A Chatbot](https://www.smashingmagazine.com/2016/12/conversational-design-essentials-tips-for-building-a-chatbot/)
*   [How To Design Error States For Mobile Apps](https://www.smashingmagazine.com/2016/09/how-to-design-error-states-for-mobile-apps/)
*   [Writing Next Generation Reusable JavaScript Modules in ECMAScript 6](https://www.smashingmagazine.com/2016/02/writing-next-generation-reusable-javascript-modules/)

## News

*   This week, [Firefox 53 rolled out](https://hacks.mozilla.org/2017/04/firefox-53-quantum-compositor-compact-themes-css-masks-and-more/) to end users, shipping performance benefits, positioned CSS Masks, and the new `display: flow-root` value [that effectively replaces our common clearfix methods](https://helloanselm.com/2017/flow-root-supports/). The update also comes with a revamped media player design. Finally, this is the first Firefox version without Windows XP and Vista support, so if you rely on one of these operating systems, consider switching to the ESR version of Firefox and upgrade to a newer system as soon as possible (the OS are not supported by Microsoft anymore).
*   [Chrome 58](https://developers.google.com/web/updates/2017/04/nic58) comes with support for IndexedDB 2.0, fullscreen support for progressive web apps, and improvements for sandboxed iframes. Alongside Firefox 53, the new Chrome is the second browser to support `display: flow-root`, [the new clearfix replacement](https://helloanselm.com/2017/flow-root-supports/). There’s also `PointerEvents.getCoalescedEvents()` as a new method to give you access to all input events that took place since the last time a PointerEvent was delivered — a useful feature for drawing applications but also quite risky when we look at it from a privacy and user tracking perspective.
*   Mozilla finally simplified the developer experience and [got rid of the Firefox Developer Edition](https://hacks.mozilla.org/2017/04/simplifying-firefox-release-channels/). If you still use it, switch to the [Firefox Nightly Edition](https://nightly.mozilla.org/). While there’s still a beta channel, I recommend Nightly as it’s relatively free of bugs that impact the general usage while supporting the latest features, deprecations and development tools already weeks or even months ahead of public launch. This is great as you have more time to adjust code on live sites when something breaks in the Nightly channel. I use WebKit Nightly and Chrome Canary similarly.</p>

## General

*   [Peter O'Shaughnessy challenges us to estimate which web browsers have the most users](https://medium.com/samsung-internet-dev/think-you-know-the-top-web-browsers-458a0a070175). And as you can probably assume, our existing idea of Chrome, Firefox, Safari, and IE leading the field isn’t up to date anymore. Instead, we need to acknowledge that UC Browser has an impressive market share, Opera Mini still does, too, Yandex in certain regions and Samsung Internet usage grows fast as more devices are shipped with it. And Google Analytics isn’t telling us the truth anyway — big parts of “Chrome” might actually be Samsung Internet.

{{% feature-panel %}}

<figure><a href="https://medium.com/samsung-internet-dev/think-you-know-the-top-web-browsers-458a0a070175"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8bd1db9-d2fc-4db9-ba5a-10693156f813/browser-usage-opt.png" width="800" height="244" alt="Browser usage on mobile" /></a><figcaption><a href="https://medium.com/samsung-internet-dev/think-you-know-the-top-web-browsers-458a0a070175">Browser usage</a> on mobile as of February 2017. Not as you would have expected, right? (<a href="https://medium.com/samsung-internet-dev/think-you-know-the-top-web-browsers-458a0a070175">Image credit</a>)</figcaption></figure>

## Concept & Design

*   Dan Leech built a great set of [very simple SVG icons of popular brands](https://simpleicons.org/). It’s available under a Creative Commons Zero license.</p>

## Tools & Workflows

*   Google Chrome can now be run in headless mode, replacing PhantomJS or SlimerJS. Jim Cummins explains [how to set it up on Mac OS](https://objectpartners.com/2017/04/13/how-to-install-and-use-headless-chrome-on-osx/). For Windows and Linux it should be similar using bash and a few adaptions to the local commands.</p>

## Security

*   Martin Vigo shares his findings from [analyzing Lastpass’ two factor authentication implementation](https://www.martinvigo.com/design-flaws-lastpass-2fa-implementation/). The article is a great reference to help you check your own implementation for the same fallacies and avoid the same design flaws.
*   Vue.js is becoming more popular and, with its popularity, the amount of tutorials grows as well. In this one, Prosper Otemuyiwa explains [how to get things right when adding authentication to your Vue.js 2 application](https://auth0.com/blog/vuejs2-authentication-tutorial/).</p>

## Privacy

*   Jeremy Thomas experimented with browsers and [tried to disable cookies entirely](https://jgthms.com/browsing-the-web-with-cookies-disabled.html). Read about how successful he was with it and what challenges he faced with modern web applications.

<figure><a href="https://jgthms.com/browsing-the-web-with-cookies-disabled.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3326a5a-b0d2-45a9-8cd2-94a1ad5611a4/disabling-cookies-opt.png" width="799" height="509" alt="Browsing Soundcloud with cookies disabled isn’t possible" /></a><figcaption><a href="https://jgthms.com/browsing-the-web-with-cookies-disabled.html">What happens when you disable cookies completely</a>? Well, some sites don’t even load, on others, basic interactions aren’t possible anymore. (<a href="https://jgthms.com/browsing-the-web-with-cookies-disabled.html">Image credit</a>)</figcaption></figure>

## Accessibility

*   Hidde de Vries shares how you can [make error messages accessible with a very easy method](https://hiddedevries.nl/en/blog/2017-04-04-how-to-make-error-messages-accessible).</p>

## JavaScript

*   Etienne Margraff shares a tutorial about [building a web chat with a bot and sending push notifications](https://meulta.com/en/2017/04/17/bot-framework-web-chat-and-push-notifications/) when the app is in the background.
*   Stefan Judis started a discussion about [whether it’s time to rethink bundling](https://www.contentful.com/blog/2017/04/04/es6-modules-support-lands-in-browsers-is-it-time-to-rethink-bundling/) as support for ES6 modules is now landing in browsers (currently in Safari, and behind a flag in Firefox and Edge, while Chrome has it in development).

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_


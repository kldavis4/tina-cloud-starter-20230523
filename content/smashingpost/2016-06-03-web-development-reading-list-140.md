---
title: >-
  Web Development Reading List #140: CSS-Only Dropdowns, Toggles And HTML
  Sliders
slug: web-development-reading-list-140
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc51affe-d46b-4c87-a9c3-c57cadd11661/wdrl-140-opt.png'
date: 2016-06-03T18:03:10.000Z
author: anselm-hannemann
description: >-
  In times where Facebook announces to track all web users whenever it can, it
  feels weird to work on disaster management tools. You may now ask why, but if
  you consider what data you work with in such a project, **you’re likely to be
  monitored** because of a lot of keywords in there.

  And that’s what bothers me most: that people who want to do good need to fear
  that they’re under complete surveillance. I like Tor and secure VPNs more than
  ever for that reason. Speaking about web development, here’s why using Tor or
  VPNs for testing performance is a great idea.
categories:
  - Web Development Reading List
---
In times where Facebook announces to track all web users whenever it can, <a href="https://twitter.com/helloanselm/status/737316074354577408">it feels weird to work on disaster management tools</a>. You may now ask why, but if you consider what data you work with in such a project, <strong>you’re likely to be monitored</strong> because of a lot of keywords in there. And that’s what bothers me most: That people who want to do good need to fear that they’re under complete surveillance. I like Tor and secure VPNs more than ever for that reason. Speaking about web development, here’s why <a href="https://helloanselm.com/2016/using-vpn-tor-for-web-development/">using Tor or VPNs for testing performance</a> is a great idea.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Design Error States For Mobile Apps](https://www.smashingmagazine.com/2016/09/how-to-design-error-states-for-mobile-apps/)
*   [High-Impact, Minimal-Effort Cross-Browser Testing](https://www.smashingmagazine.com/2016/02/high-impact-minimal-effort-cross-browser-testing/)
*   [Automating Art Direction With The Responsive Image Breakpoints Generator](https://www.smashingmagazine.com/2016/09/automating-art-direction-with-the-responsive-image-breakpoints-generator/)
*   [When 24/7/365 Fails: Turning Off Work On Weekends](https://www.smashingmagazine.com/2010/11/when-24-7-365-fails-turn-off-work-on-weekends/)

## News

*   [Chrome 51 is out](https://googlechromereleases.blogspot.de/2016/06/stable-channel-update.html) and with it, various security issues have been fixed. No big new features but more stability and improved performance for Chrome this time :)

## General

*   Peter-Paul Koch shares why he thinks that the adage [“Don’t Repeat Yourself” isn’t always useful in browser contexts](https://www.quirksmode.org/blog/archives/2016/05/dry_do_repeat_y.html). We’re building our websites for browsers, and to make the page work properly, we need to repeat ourselves, especially when using [progressive enhancement](https://www.smashingmagazine.com/2013/09/progressive-enhancement-is-faster/).
*   It’s about raising the barrier. Jeremy Keith has talked and written about this a couple of times already, and now in times where the term “Progressive Web Apps” is shared all over the web, Jeremy says that [Google makes web apps regressive](https://adactio.com/journal/10708). A web app requires HTTPS, service workers, a manifest JSON and a few recent visits by the user to be installable — for most websites dealbreakers. Also the fact that the URL must not be displayed in the web app turns out to be harmful to the web itself as it depends on URLs.</p>

## Tools & Workflow

*   You can [add autocomplete to npm commands](https://medium.com/@jamischarles/adding-autocomplete-to-npm-install-5efd3c424067), including `npm install`.</p>

## Security

*   Since we have widespread support for web storage solutions like Session Storage, the question arises if we still need cookies at all. [James Kettle researched](https://blog.portswigger.net/2016/05/web-storage-lesser-evil-for-session.html) and concluded that cookies are insecure by default, and you need to set `__Host-absolutely=secure; Path=/; HTTPOnly; Secure; SameSite=strict;` ([source](https://twitter.com/0x6D6172696F/status/738335320467472384)) to make them secure while Session Storage is secure by default. On the other hand, one aspect speaks clearly for cookies: They are controllable by the client and the server.</p>

## Privacy

*   Facebook is already known for not respecting privacy. They [now announced](https://www.theverge.com/2016/5/27/11795248/facebook-ad-network-non-users-cookies-plug-ins): “[…] we’re expanding Audience Network so publishers and developers can show better ads to everyone — including those who don’t use or aren’t connected to Facebook.” This basically means that they now track every user who gets in touch with some Facebook tracking technology (cookies, web storage, embedded fb-scripts, etc.) without asking. For Firefox, I added the [Self-Destructing Cookies](https://addons.mozilla.org/en-US/firefox/addon/self-destructing-cookies/) extension in addition to my [Canvas Blocker](https://addons.mozilla.org/en-US/firefox/addon/canvasblocker/) and [uBlock Origin](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/) to browse more safely. But remember that an open Facebook tab still might track you on other sites, so the browser’s private mode seems more appropriate.

{{% feature-panel %}}

<figure><a href="https://addons.mozilla.org/en-US/firefox/addon/self-destructing-cookies/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3333dc4a-9a3f-481f-ab7e-4ae553deab52/self-destructing-cookies-opt.png" alt="Self-Destructing Cookies browser extension" width="500" height="343" /></a><figcaption>The Firefox extension <a href="https://addons.mozilla.org/en-US/firefox/addon/self-destructing-cookies/">Self-Destructing Cookies</a> protects you against trackers by deleting a site’s cookies and LocalStorage as soon as you close its tabs. (Image credit: <a href="https://addons.mozilla.org/en-US/firefox/addon/self-destructing-cookies/">Self-Destructing Cookies</a>)</figcaption></figure>

## Web Performance

*   Lara Callender Hogan now published her book [“Designing for Performance” for free as an online HTML book](https://designingforperformance.com/). If you like it, consider purchasing it nevertheless to support the author.</p>

## Accessibility

*   [Accessibility is not just about morals](https://una.im/a11y-for-the-masses/) and making the web usable to a small group of citizens. It’s about making the web usable to the masses.</p>

## JavaScript

*   Since browsers don’t support multirange sliders natively very well, a polyfill is needed. But most polyfills are really hacky and bring problems with customized styles. Not so Lea Verou’s [tiny, flexible polyfill for multirange inputs](https://lea.verou.me/2016/05/introducing-multirange-a-tiny-polyfill-for-html5-two-handle-sliders/).
*   Alex Castillo shares how you make your web application [send native web push notifications with Angular 2](https://www.castillo.io/blog/2016/4/14/push-notifications-with-angular-2).
*   Many projects feature a star-rating component. But very often they are a nightmare to build properly across various browsers and most of the time the solution isn’t accessible either. [Starability](https://lunarlogic.github.io/starability/) comes as an accessible, simple module to solve the issue.

<figure><a href="https://www.castillo.io/blog/2016/4/14/push-notifications-with-angular-2"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1314899-913f-468c-92a1-a0f5d451d36c/native-push-notifications-opt.png" alt="Send native web push notifications with Angular 2" width="500" height="346" /></a><figcaption>Alex Castillo’s ng2-notifications lets you <a href="https://www.castillo.io/blog/2016/4/14/push-notifications-with-angular-2">send native web push notifications with Angular 2</a>. (Image credit: <a href="https://www.castillo.io/blog/2016/4/14/push-notifications-with-angular-2">Alex Castillo</a>)</figcaption></figure>

## CSS/Sass

*   We’re [using tooltips, dropdowns, toggles all the time in web projects](https://www.smashingmagazine.com/2016/04/inspiring-ui-demos-logins-menus-toggles-and-more/), and most of the time we choose to do this with JavaScript. But [you don’t necessarily need JavaScript for that](https://robots.thoughtbot.com/you-don-t-need-javascript-for-that) but can use CSS instead. If that’s not enough, you can still enhance with JavaScript and have a progressively enhanced module.</p>

## Going Beyond…

*   Do you know how the Internet works? Ars Technica [dives deep into Internet infrastructure](https://arstechnica.com/information-technology/2016/05/how-the-internet-works-submarine-cables-data-centres-last-mile/) and provides a rare glance into a subsea cable landing site.

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.

<em>Thanks and all the best,
Anselm</em>


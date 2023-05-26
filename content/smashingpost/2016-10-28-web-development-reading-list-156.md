---
title: >-
  Web Development Reading List #156: Browser News, Webpack 2, And Lessons
  Learned From HPKP
slug: web-development-reading-list-156
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22aa39d9-920f-496d-ba48-df81374da99d/wdrl-156-opt.png'
date: 2016-10-28T17:55:22.000Z
author: anselm-hannemann
description: >-
  Is a person who is sitting by herself in a room alone? From an outside
  perspective, it might seem so, but the human brain is way more interesting in
  these regards. We carry a map of relationships inside ourselves, and it
  depends on this map if the person actually does feel alone or not.

  I just read “[Stress and the Social Self: How Relationships Affect Our Immune
  System](https://www.brainpickings.org/2015/10/07/esther-sternberg-stress-relationships/)”,
  and I feel that we can learn a lot from it. In fact, I might see social media
  from a different perspective now. We’re _social_ beings, I love sharing good
  content with you, so, without further ado, here’s this week’s web dev reading
  list.
categories:
  - Web Development Reading List
---
Is a person who is sitting by herself in a room alone? From an outside perspective, it might seem so, but the human brain is way more interesting in these regards. We carry a map of relationships inside ourselves, and it depends on this map if the person actually does feel alone or not.

I just read “<a href="https://www.brainpickings.org/2015/10/07/esther-sternberg-stress-relationships/">Stress and the Social Self: How Relationships Affect Our Immune System</a>”, and I feel that we can learn a lot from it. In fact, I might see social media from a different perspective now. We’re <em>social</em> beings, I love sharing good content with you, so, without further ado, here’s this week’s web dev reading list.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)
*   [Be Afraid Of HTTP Public Key Pinning (HPKP)](https://www.smashingmagazine.com/be-afraid-of-public-key-pinning/)
*   [Getting More Work Done Without Simply Working More Hours](https://www.smashingmagazine.com/2015/12/getting-work-done-without-simply-working-hours/)
*   [Introduction to DNS: Explaining The Dreaded DNS Delay](https://www.smashingmagazine.com/2011/05/introduction-to-dns-explaining-the-dreaded-dns-delay/)

## News

*   [Opera 41 and Chrome 54 are out](https://dev.opera.com/blog/opera-41/), and they come with some interesting new features. The updates now support Custom Elements v1 as well as some new and convenient JavaScript methods like `ParentNode.prototype.append()` or unprefixed CSS `user-select`. On the other hand, they removed `TouchEvent.prototype.initTouchEvent` (you’ll need to use the constructor from now on), and `KeyboardEvent.prototype.keyIdentifier` has been replaced by `KeyboardEvent.prototype.key`.
*   Following a suggestion by other major browser vendors, Mozilla will [distrust WoSign and StartCom certificates](https://blog.mozilla.org/security/2016/10/24/distrusting-new-wosign-and-startcom-certificates/) from January 1st, 2017 due to backdated certificates and non-disclosure and denial of an acquisition of the two companies. A great step for better CA security.
*   [Node.js v6 transitioned to the current LTS version](https://medium.com/@nodejs/node-js-v6-transitions-to-lts-be7f18c17159) this week and [Node.js v7 has been released](https://nodejs.org/en/blog/release/v7.0.0/), too. It covers 98% of ES6, brings the new V8 engine, improved reliability and performance, and a new URL-parser based on the WHATWG URL standard.</p>

## General

*   With the [upcoming Chrome 55](https://blog.chromium.org/2016/10/chrome-55-beta-input-handling.html) (now in beta), the browser will finally get support for Pointer Events. It will also support JavaScript `async`/`await`-functions and revive the CSS `hyphens` property after years of absence in Chromium browsers. The `once` Event Listener option will also be added and, to improve load times and prevent failed navigations, cross-origin and parser-blocking scripts injected using `document.write()` will no longer load over 2G connections (which also means that [3rd-party fallbacks as used by the HTML5Boilerplate](https://github.com/h5bp/html5-boilerplate/blob/master/src/index.html#L26) won’t work anymore in upcoming Chrome versions).</p>

## Tools & Workflows

*   Jack Franklin explains how to [migrate from the current Webpack 1 to the upcoming Webpack 2](https://javascriptplayground.com/blog/2016/10/moving-to-webpack-2/) and where the differences between the two lie.
*   Similar to the already showcased [Boxy SVG Editor](https://wdrl.info/archive/135/boxy-svg-editor), [Vectr](https://vectr.com/) is a new online/desktop vector graphics editor with real-time sharing.

{{% feature-panel %}}

<figure><a href="https://vectr.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8bf38ac-2a92-436d-931b-f413a415e74d/vectr-editor-opt.png" alt="Vectr" width="500" height="259" /></a><figcaption><a href="https://vectr.com/">Vectr</a> is a simple yet powerful cross-platform vector graphics editor. (Image credit: <a href="https://vectr.com/">Vectr</a>)</figcaption></figure>

## Security

*   Paragon Initiative Enterprises share a comprehensive [guide to automatic security updates for PHP developers](https://paragonie.com/blog/2016/10/guide-automatic-security-updates-for-php-developers) that everyone developing with PHP should be aware of.
*   Last week, Smashing Magazine had to deal with an expiring SSL certificate. While this is usually an easy thing to renew, problems may arise if you have HTTP Public Key Pinning (HPKP) enabled and set to a long expiry date (which usually is intended). Mathias Biilmann Christensen now wrote about the lessons learned from this and [why you should be aware (and afraid!) of HPKP](https://www.smashingmagazine.com/be-afraid-of-public-key-pinning/) and [how to issue a new certificate with an old key](https://www.smashingmagazine.com/how-to-issue-a-new-ssl-certificate-with-an-old-ssl-key/) so that the site won’t break for your users with HPKP enabled.</p>

## Privacy

*   Mattias Geniar shares how you can easily [block ads and trackers from your entire home network](https://ma.ttias.be/pi-hole-dns-based-blacklist-ads-tracking-raspberry-pi/) using [Pi-Hole](https://pi-hole.net/), a DNS-based blacklist for Raspberry Pi.</p>

## Web Performance

*   Brian Armstrong from Canopy explains [why you shouldn’t rely on default DNS settings](https://medium.com/@brianarmstrong/youre-probably-doing-dns-wrong-like-we-were-6625efaed390), as the recent Dyn DNS outage has shown. He covers how to configure DNS the right way, why a longer TTL is important, and why having different nameservers from different providers can save your service’s uptime.

<figure><a href="https://medium.com/@brianarmstrong/youre-probably-doing-dns-wrong-like-we-were-6625efaed390"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76d25fcc-71c0-431d-bf10-988da6b1ff0b/nameservers-opt.png" alt="Multiple nameservers from only one DNS provider" width="500" height="199" /></a><figcaption>Having multiple nameservers is good, but make sure that they come from different DNS providers so that requests can be resolved by others if one fails. (Image credit: <a href="https://medium.com/@brianarmstrong/youre-probably-doing-dns-wrong-like-we-were-6625efaed390">Brian Armstrong</a>)</figcaption></figure>

## JavaScript

*   [Fuse.js](https://fusejs.io/) is a new and light-weight JavaScript fuzzy-search library.</p>

## CSS/Sass

*   Roman Komarov wrote about [conditions in CSS Custom Properties](https://kizu.ru/en/fun/conditions-for-css-variables/), about solutions, challenges, and how you can benefit from preprocessors when it comes to more complex conditions. The article also mentions a couple of interesting ideas on how the web standard could be extended.</p>

## Work & Life

*   Cal Newport shares his thoughts on [how deep breaks during work can help your mind recharge and, thus, improve your productivity](https://calnewport.com/blog/2016/09/14/on-deep-breaks/).</p>

## Going Beyond…

*   It’s really interesting to see this kind of back-story: Katie Singer reveals [the real amount of energy used to power the internet](https://www.electronicsilentspring.com/real-amount-energy-power-internet/) and puts these figures into perspective by comparing how much power anyone of us would need to generate to power a website.

<em>And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS, and online.</em>

{{< signature "ah" >}}


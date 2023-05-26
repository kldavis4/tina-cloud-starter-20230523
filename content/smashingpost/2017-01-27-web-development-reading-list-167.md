---
title: >-
  Web Development Reading List #167: On Team Retreats, Immutable Cache, And
  Eliminating Clearfix Hacks
slug: web-development-reading-list-167
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1695e23d-f026-42d7-8f0b-746a8cd6130e/wdrl-167-opt.png'
date: 2017-01-27T20:43:12.000Z
author: anselm-hannemann
description: >-
  When working in a team, we focus so much on the work, that we often forget
  that we all have something in common. Something that is so obvious that we
  underestimate it: we all are human beings. And well, if we want to **grow as a
  team** and get better at what we do, we should embrace this fact more. In
  fact, I just came back from a week-long team retreat where we had team
  activities, team games, and sessions and discussions about how we can achieve
  just that.

  We figured out how much we value diversity, we realized how different the
  English language and its words are perceived by people from different
  countries, and we’ve seen short talks on various topics like work-life-balance
  but also on technical stuff like Docker or intercepting any computer’s traffic
  with a Raspberry Zero. So if you have the chance to work in a team, use the
  opportunity and exchange views and share information with your co-workers.
  Work is part of your life, so why not make it a lovely part?
categories:
  - Web Development Reading List
---
We figured out how much we value diversity, we realized how different the English language and its words are perceived by people from different countries, and we’ve seen short talks on various topics like work-life-balance but also on technical stuff like Docker or intercepting any computer’s traffic with a Raspberry Zero. So if you have the chance to work in a team, use the opportunity and exchange views and share information with your co-workers. Work is part of your life, so why not make it a lovely part?

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Styling And Animating SVGs With CSS](https://www.smashingmagazine.com/2014/11/styling-and-animating-svgs-with-css/)
*   [6 Simple Ways For Freelancers To Increase Productivity](https://www.smashingmagazine.com/2009/08/simple-ways-freelancers-can-increase-productivity/)
*   [The Messy Art Of UX Sketching](https://www.smashingmagazine.com/2011/12/the-messy-art-of-ux-sketching/)
*   [Why You Should Stop Installing Your WebDev Environment Locally](https://www.smashingmagazine.com/2016/04/stop-installing-your-webdev-environment-locally-with-docker/)

## News

*   Say hello to [Firefox 51](https://developer.mozilla.org/en-US/Firefox/Releases/51). It ships unprefixed `::placeholder`, broader ES2015 support, WebGL 2, IndexedDB v2, and `tabindex` for SVG. Scripts served with an `image/*`, `video/*`, `audio/*` or `text/csv` MIME type are now blocked.
*   Samuel Reed shares how Google Chrome 56 will make [throttling of background tabs more aggressive](https://blog.strml.net/2017/01/chrome-56-now-aggressively-throttles.html), what this actually means and what the plans for Chrome 57 are.</p>

## General

*   Firefox has been supporting [Immutable Caching](https://wdrl.info/archive/137/bits-up-cache-control-immutable) since version 49\. Now they share [how efficient the technique is](https://hacks.mozilla.org/2017/01/using-immutable-caching-to-speed-up-the-web/) for Facebook and other big sites that are frequently visited by the same people.</p>

## Tools & Workflow

*   Anne van Kesteren shares tips on [using SSH securely in the context of a CI service](https://annevankesteren.nl/2017/01/secure-secure-shell) such as Travis CI or Circle CI.</p>

## Security

*   Joschi Kuphal explains [how to implement HPKP with Certbot](https://jkphl.is/articles/certbot-http-public-key-pinning-hpkp/), the Let’s Encrypt client.
*   In response to the recent MongoDB ransom attack, Mattias Geniar shares his thoughts on the [return of unauthenticated, unfirewalled protocols](https://ma.ttias.be/return-unauthenticated-unfirewalled-protocols/).</p>

## Web Performance

*   Mazdak Hashemi gives [insights into Twitter’s infrastructure](https://blog.twitter.com/2017/the-infrastructure-behind-twitter-scale). They focus mostly on the large amount of traffic and the challenges that come with it.</p>

## HTML & SVG

*   SVG icons often have one problem: They don’t align well to the text surrounding them. Elliot Dahl explains [how to fix that](https://blog.prototypr.io/align-svg-icons-to-text-and-say-goodbye-to-font-icons-d44b3d7b26b4).

{{% feature-panel %}}

<figure><a href="https://blog.prototypr.io/align-svg-icons-to-text-and-say-goodbye-to-font-icons-d44b3d7b26b4"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d3faca7-59e2-42e5-b347-23697adde174/svg-icon-alignment-pen-opt.png" width="800" height="544" alt="Aligning SVG Icons To Text" /></a><figcaption>SVG icons and text neatly aligned. Elliot Dahl explains <a href="https://blog.prototypr.io/align-svg-icons-to-text-and-say-goodbye-to-font-icons-d44b3d7b26b4">how to do it</a>.</figcaption></figure>

## JavaScript

*   Sara Soueidan shows [how to build a fully accessible help tooltip](https://sarasoueidan.com/blog/accessible-tooltips/) and why CSS-only methods sound neat but often aren’t.
*   Mathias Bynens shares [what’s currently happening at the TC39 in regards to Regular Expressions](https://mathiasbynens.be/notes/es-regexp-proposals) and shows what the proposals could look like and what problems they would solve.

<figure><a href="https://sarasoueidan.com/blog/accessible-tooltips/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee2098af-f4a3-452e-b7e5-0d323559a921/accessible-tooltip-opt.png" width="800" height="408" alt="How To Build An Accessible Tooltip" /></a><figcaption>How can you make a tooltip like the one in the top right corner accessible? <a href="https://sarasoueidan.com/blog/accessible-tooltips/">Sara Soueidan explains</a>. (<a href="https://sarasoueidan.com/blog/accessible-tooltips/">Image credit</a>)</figcaption></figure>

## CSS/Sass

*   Rachel Andrew explains the [new `display` property value `flow-root`](https://www.rachelandrew.co.uk/archives/2017/01/24/the-end-of-the-clearfix-hack/) that was added to Chrome and Firefox (both Nightly/Canary only) and why it will finally replace the old clearfix hacks that we’re currently using to fix parent box sizes when floating inner elements.</p>

## Work & Life

*   Lara Hogan on how to hold [better meetings](https://larahogan.me/blog/better-meetings/). A concise list of tips and tricks to make your meetings a lot more efficient and interesting.
*   With tons of productivity articles out there, it’s easy to feel overwhelmed or even bad about how you get work done. But each one of us is an individual, and, thus, [productivity is not only a subjective matter but also has a personality](https://superyesmore.com/productivity-has-a-personality-8d71d90938e9a85b64bb67dcfe06012c).</p>

## Going Beyond…

*   [Ben Sauer questions the use of digital media for everything](https://slapdashery.org/thinking-with-paper-6e1064b1c67a) and asks himself if embracing paper to share information in a team is a better idea.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_


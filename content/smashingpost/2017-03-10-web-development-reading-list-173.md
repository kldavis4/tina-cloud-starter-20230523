---
title: >-
  Web Development Reading List #173: CSS Grid Support, A Virtual DOM
  Alternative, And Designing Better Cards
slug: web-development-reading-list-173
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9108ae5f-0331-471b-9f89-a3af2c080a5f/wdrl-173-opt.png'
date: 2017-03-10T22:22:11.000Z
author: anselm-hannemann
description: >-
  This week was a big week in terms of web development news. We got much
  **broader support for CSS Grids** and Web Assembly, for example, but I also
  stumbled across some great resources that teach us a lot of valuable things.

  With this Web Development Reading List, we’ll dive deep into security and
  privacy issues, take a look at a lightweight virtual DOM alternative, and get
  insights into how we can overcome our biases (or at least how we can better
  deal with them). So without further ado, let’s dive right in!
categories:
  - Web Development Reading List
---
With this Web Development Reading List, we’ll dive deep into security and privacy issues, take a look at a lightweight virtual DOM alternative, and get insights into how we can overcome our biases (or at least how we can better deal with them). So without further ado, let’s get started!

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Designing Card-Based User Interfaces](https://www.smashingmagazine.com/2016/10/designing-card-based-user-interfaces/)
*   [Web Design Criticism: A How-To](https://www.smashingmagazine.com/2010/03/web-design-criticism-a-how-to/)
*   [Dealing With Loud And Silent Burnout](https://www.smashingmagazine.com/2015/10/dealing-with-loud-silent-burnout/)

## News

*   [Chrome 57](https://blog.chromium.org/2017/02/chrome-57-beta-css-grid-layout-improved.html) was released this week, and it brings us CSS Grids, the Media Session API, and Web Assembly. Also new is that Chrome will return an error for SHA1 certificates from now on.
*   A new Firefox version was released to the public this week: [Firefox 52](https://developer.mozilla.org/en-US/Firefox/Releases/52). The new version will display a prominent warning if a user fills in their password on a non-secure page, `rel="noopener"` was implemented, too, just like broad [support for CSS Grids](https://hacks.mozilla.org/2017/03/firefox-52-introducing-web-assembly-css-grid-and-the-grid-inspector/), Web Assembly, and `async`/`await`. They also disabled all plugins except for Adobe Flash.
*   The [Samsung Internet browser beta is now available](https://medium.com/samsung-internet-dev/samsung-internet-beta-now-available-without-sign-up-e0d5d4010838) in the Google Play Store and via Samsung Galaxy Apps. It runs on Chromium 51, has support for progressive web apps, Service Worker, and content blockers.</p>

## General

*   By analyzing the large-scale issues the web faced in the past month (think Amazon’s S3 outage causing a downtime of millions of websites, Cloudflare’s data leak that required users of very popular websites to change their passwords, or Google’s accidental WiFi reset which wiped out customers’ Internet profiles) [Tristan Louis reflects on the question if we are breaking the Internet](https://www.fastcompany.com/3068627/are-we-breaking-the-internet). The trend towards a few services hosting a majority of the Internet’s infrastructure is causing more and more large-scale problems. If we want to avoid issues like these, we need to rethink this new kind of centralization and fix it.
*   Bruce Lawson wrote about the “[World Wide Web, Not Wealthy Western Web](https://www.smashingmagazine.com/2017/03/world-wide-web-not-wealthy-western-web-part-1/)”. It’s about the bias of western web developers, about ignoring other continents, and why we need to see the bigger picture instead. A piece you should definitely take the time to read.</p>

## Concept & Design

*   It’s easy to build a standard card design, but we could do so much more with them. Andrew Coyle wrote about [designing better cards](https://uxdesign.cc/design-better-cards-c0d12ab581c4), a component we use in nearly every design today.

{{% feature-panel %}}

<figure><a href="https://uxdesign.cc/design-better-cards-c0d12ab581c4#.dfp2dsxh2"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5479a1a-20ad-47d1-acb6-8b465c3476ea/design-better-cards-opt.png" width="800" height="331" alt="Design Better Cards" /></a><figcaption>Cards — the component that symbolizes the web. Andrew Coyle shares <a href="https://uxdesign.cc/design-better-cards-c0d12ab581c4#.dfp2dsxh2">how we can make even more of them</a>. (<a href="https://uxdesign.cc/design-better-cards-c0d12ab581c4#.dfp2dsxh2">Image credit</a>)</figcaption></figure>

## Security

*   In an attempt to participate in their own bug bounty program, Brett Buerhaus and Ben Sadeghipour analyzed AirBNB’s web service. And indeed, they stumbled over some pretty good examples of [how to bypass a lot of security measurements](https://buer.haus/2017/03/08/airbnb-when-bypassing-json-encoding-xss-filter-waf-csp-and-auditor-turns-into-eight-vulnerabilities/) they already had implemented.
*   We know backups are crucial in IT operations. But what we often don’t think about is the backup’s security. A company that’s responsible for a lot of email spam recently [exposed their backups to the public](https://www.csoonline.com/article/3176433/security/spammers-expose-their-entire-operation-through-bad-backups.html) for over a month. Initially, we might think that’s great as this mishap makes it relatively easy to bring their operations to a halt, but then others have probably already picked up all the data to use it for their operations and, thus, producing an increase of spam.
*   Tobias Laudinger and some of his co-workers [conducted the first comprehensive study of client-side JavaScript library usage](https://blog.acolyer.org/2017/03/07/thou-shalt-not-depend-on-me-analysing-the-use-of-outdated-javascript-libraries-on-the-web/) and the security implications it brings along. Based on data from over 133K websites, they found that 37% of websites include at least one library with a known vulnerability. Time to reconsider our use of external dependencies and how we can keep them up-to-date.</p>

## Privacy

*   Another big data leak was revealed by WikiLeaks this week, this time it’s called “[Vault7 — CIA Hacking Tools Revealed](https://wikileaks.org/ciav7p1/)”. And, well, it does, in fact, confirm the worst fears privacy researchers had: The CIA [is spying on Samsung TVs](https://motherboard.vice.com/en_us/article/the-cia-spied-on-people-through-their-smart-tvs-leaked-documents-reveal?asd), and it’s extremely likely that [Amazon’s Alexa is no exception](https://twitter.com/BusterUSMC/status/839489658283261952), just like a lot of other centralized, not end-to-end-encrypted services, too. The findings also caused a lot of discussion about whether messaging apps like Whatsapp and Signal are safe since their encryption was reportedly broken as well. But you need to differentiate here, because, in the case of the messaging apps, the encryption was broken by infecting only selected targeted devices with malware. Together with [this news about decrypted PGP messages](https://motherboard.vice.com/en_us/article/dutch-cops-say-theyve-decrypted-pgp-messages-on-seized-server), the published data shows that apps like Signal do indeed work as expected: They prevent third parties from mass-capturing private data and instead force them to target individual devices.</p>

## JavaScript

*   Andrea Giammarchi shared his latest project, a lightweight virtual DOM alternative called [hyperHTML](https://medium.com/@WebReflection/hyperhtml-a-virtual-dom-alternative-279db455ee0e).

<figure><a href="https://medium.com/@WebReflection/hyperhtml-a-virtual-dom-alternative-279db455ee0e"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22d6c195-6e5c-458f-ad33-354870cceccb/hyperhtml-opt.png" width="800" height="438" alt="hyperHTML" /></a><figcaption>Andrea Giammarchi built <a href="https://medium.com/@WebReflection/hyperhtml-a-virtual-dom-alternative-279db455ee0e">hyperHTML</a>, a lightweight virtual DOM alternative. (<a href="https://medium.com/@WebReflection/hyperhtml-a-virtual-dom-alternative-279db455ee0e">Image credit</a>)</figcaption></figure>

## CSS/Sass

*   Since this week, we’re able to play around with CSS Grids in a lot [more public browsers](https://caniuse.com/#search=grid) (Chrome, Firefox, Edge with the old spec). When you do, this quite [complete guide to CSS grid](https://tympanus.net/codrops/css_reference/grid/) might come in handy.
*   Did you know you can [use CSS to lint your HTML markup](https://bitsofco.de/linting-html-using-css/)? Ire Aderinokun shared a couple of use cases and some very neat tricks — how to check for unlabelled form elements or inaccessible viewport attributes, for example.

<figure><a href="https://tympanus.net/codrops/css_reference/grid/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd259db9-04b2-491f-ac4b-c62afe5cbdc0/grid-opt.png" width="800" height="601" alt="CSS Grid" /></a><figcaption><a href="https://tympanus.net/codrops/css_reference/grid/">CSS Grid introduces a series of powerful possibilities</a> that give us more control over our layouts. (<a href="https://tympanus.net/codrops/css_reference/grid/">Image credit</a>)</figcaption></figure>

## Work & Life

*   Behavioral economist Dan Ariely [wants to fix an issue that consumes an ever-expanding portion of his time: email](https://www.theatlantic.com/business/archive/2017/03/economist-email-less-painful/518934/). He already gained a lot of insights from which everyone can profit, so it’s worth following the story a bit.
*   Lots of celebrities from presidents to actors and many others recommend getting only six hours of sleep, so you have 18 hours of the day to get things done. But [Sara Soueidan disagrees and shares her experiences, including dealing with burnout](https://superyesmore.com/its-not-how-many-hours-of-sleep-you-get-31511419ec81ce17835eeeb6c1a570a5).
*   We know that giving feedback is never really objective. But [acknowledging our bias](https://www.fastcompany.com/3068689/the-science-of-work/your-feedback-will-always-be-biased-but-heres-what-to-do-about-it) before giving feedback can improve the way it will be perceived.</p>

## Going Beyond…

*   A team around the co-inventor of Lithium-ion batteries [developed the first all-solid-state battery cells](https://news.utexas.edu/2017/02/28/goodenough-introduces-new-battery-technology) that could lead to safer, faster-charging, longer-lasting rechargeable batteries.
*   Jelmer Mommers recently stumbled across a video from the oil company Shell that shows that they were aware of the dangers that global warming brings along already more than 25 years ago. Unfortunately, they decided to focus on short-term solutions nevertheless, for financial reasons. This great article shows [how money can make us ignore important facts](https://thecorrespondent.com/6311/shell-took-a-good-long-look-at-climate-change-and-then-went-back-to-looking-for-oil/2244455904680-2a618a43). I really believe that you and me, we can do better than Shell.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_


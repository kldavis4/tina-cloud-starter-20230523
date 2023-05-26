---
title: >-
  Web Development Reading List #146: Peermaps, Passive Event Listener Note, And
  A Shift Of Focus
slug: web-development-reading-list-146
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebaa3822-3711-4359-becb-cd53d9f223d4/httppoxy-500-opt.png
date: 2016-07-22T18:50:09.000Z
author: anselm-hannemann
description: >-
  So, what do we have this week? Well, it’s quite a lot actually. For example,
  there’s now a deal that might make Opera’s browser a Chinese business, leaving
  all privacy and security efforts that have recently been made in the browser
  uncertain.

  If you want to dive into learning ECMAScript 6, Wes Bos has published a huge
  [series of ES6 screencasts](https://es6.io/) this week that are absolutely
  worth the money. Besides, there are a few other recommendations for you to
  read this week. Let's get started.
categories:
  - Web Development Reading List
---
So, what do we have this week? Well, it’s quite a lot actually. For example, there’s now <a href="https://www.zdnet.com/article/1-2bn-offer-for-opera-scrapped-new-600m-deal-centres-on-browser-and-consumer-business/">a deal that might make Opera’s browser a Chinese business</a>, leaving all privacy and security efforts that have recently been made in the browser uncertain. If you want to dive into learning ECMAScript 6, Wes Bos has published a huge <a href="https://es6.io/">series of ES6 screencasts</a> this week that are absolutely worth the money. Besides, there are a few other recommendations for you to read this week. Let's get started.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [SEO For Responsive Websites](https://www.smashingmagazine.com/2013/11/seo-for-responsive-websites/)
*   [What The Heck Is SEO? A Rebuttal](https://www.smashingmagazine.com/2012/12/what-heck-seo-rebuttal/)
*   [How Content Creators Benefit From The New SEO](https://www.smashingmagazine.com/2012/06/content-creators-benefit-from-new-seo/)
*   [The Importance Of HTML5 Sectioning Elements](https://www.smashingmagazine.com/2013/01/the-importance-of-sections/)

## News

*   The new "technology preview" version of [Safari now supports Google’s WebP format](https://www.cnet.com/news/apple-ios-macos-tests-googles-webp-graphics-to-speed-up-web/). Note that it's currently a beta test version, and the final support is unknown — however, it could be interesting since it would mean native support of the file-format for Mac OS as well, making it the first large OS supporting [WebP](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/).
*   [httpoxy](https://httpoxy.org/) is a set of vulnerabilities that affect application code running in CGI, or CGI-like environments. This means it’s a critical vulnerability test for your php-fpm, mod_php, Python and Go CGI handlers that you should check and fix security issues immediately. Note that only serving HTTPS doesn’t help here; to mitigate the attack, you need to block proxy request headers as early as possible, and definitely before they hit your application.</p>

## Tools & Workflows

*   [Peermaps](https://github.com/substack/peermaps) provides a decentralized, cooperative alternative to commercial map providers like Google Maps. Instead of fetching data from a centralized service, fetch map data from your peers using webtorrent.
*   With [ZeroNet](https://zeronet.io/) is another decentralized hosting technology, currently in development. The Bitcoin-crypto and BitTorrent-driven technology is an alternative approach to the decentralized idea of [IPFS](https://ipfs.io/).</p>

## Security

*   [Firefox 48, out August 2, 2016](https://www.ghacks.net/2016/07/18/firefox-48-blocklist-against-plugin-fingerprinting/), will block known plugin fingerprinting services thanks to a new blocklist that Mozilla developed to improve user privacy. For example, Flash files that are known for fingerprinting (or "super cookies") are automatically blocked. In other news, Mozilla also announced that they will [implement Tor’s privacy settings in Firefox](https://www.ghacks.net/2016/07/04/tor-privacy-settings-coming-to-firefox/), starting in Firefox 50 with the first features such as plugin information leaks and other techniques known to track down user behavior.
*   It seems like most people are unaware of [how big of an attack vector browser extensions have become](https://kjaer.io/extension-malware/). They’re still a quite unregulated territory, and although there are inherent limits to what they can do, there is little to no protection against extension malware — your antivirus can’t help you here.
*   A [new `require-sri-for` directive](https://www.chromestatus.com/feature/5635811978510336) in Content Security Policy gives developers the ability to assert to the browser that every resource of a given type ought to be checked for integrity. If a resource of that type is loaded without integrity metadata, it will be rejected without triggering a network request.

{{% feature-panel %}}

<figure><a href="https://kjaer.io/extension-malware/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/808e8b64-d620-4f41-86c9-bb759ed83a09/extension-content-age-verify-opt.png" alt="" width="500" height="357" /></a><figcaption>Getting hacked by a Chrome extension is easier than you think. (<a href="https://kjaer.io/extension-malware/">Image source</a>)</figcaption></figure>

## Privacy

*   Is Google's Project Fi nothing more than an attempt to collect even more data from users? The main goal behind getting into Wi-Fi and cellular network services business seems to be a great addition to [collecting data about users’ online behavior](https://www.computerworld.com/article/2914838/data-privacy/project-fi-will-help-google-amass-even-more-data-about-you.html) and it attracts people by its very low pricing.
*   Google adjusted their privacy settings [once again](https://www.wired.com/2016/06/latest-ad-tracking-move-google-gets-opt-right/). I’ll leave you with these useful links where you can adjust your privacy settings for [Maps](https://www.google.com/maps/timeline), [All Account Activity](https://myactivity.google.com/myactivity), [more activity controls](https://myaccount.google.com/activitycontrols), and finally [Google Payment privacy settings](https://payments.google.com/s/?page=privacySettings) which have opt-in for data sharing and analysis for advertising on by default. Note that Chrome has its own settings in the app as well. So far, privacy…

## JavaScript

*   Paul Irish left a note this week on [Passive Event Listeners](https://dom.spec.whatwg.org/#dom-eventlisteneroptions-passive). Apparently, [they’re only needed for touch and pointer-events](https://twitter.com/paul_irish/status/755175394140053505) and have no advantage when used in other cases.</p>

## Work & Life

*   Andy Budd analyzes the problem of the always recurring question on “[Why can’t designers solve more meaningful problems?](https://www.andybudd.com/archives/2016/07/why_cant_designers_solve_more_meaningful/)”. An essay on how to find the right work for yourself, and why it’s sometimes challenging to acknowledge that their vision differs from the type of job they want to work in. Andy concludes that we need to create an alternative success narrative to what we have now.</p>

## Going Beyond…

*   The NASA has just published the first 2016 climate trend according to which [we’re continuing to break all records](https://www.nasa.gov/feature/goddard/2016/climate-trends-continue-to-break-records) with an average temperature 1.3 degrees Celsius (2.4 degrees Fahrenheit) warmer than the late nineteenth century.
*   Katie Rogers asked experts [what happens to our human brain when there’s a constant cycle of violent news](https://www.nytimes.com/2016/07/16/health/what-is-a-constant-cycle-of-violent-news-doing-to-us.html?_r=0). While it of course depends on the individual person, a higher frequency of such news increases fear and the sense of vulnerability and powerlessness. And I’m not saying you shouldn’t follow the news anymore but maybe limiting access to it for yourself is a good idea, as is filtering it on social media (use mute keywords or similar) so you don’t get flooded about violent, horrible news all the time. It’s enough to check it once per day or so and it’s unhealthy if you’re surrounded by anxiety everywhere, all the time.

<em>And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</em>

<em>— Anselm</em>


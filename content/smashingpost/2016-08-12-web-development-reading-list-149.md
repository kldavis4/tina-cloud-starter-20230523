---
title: >-
  Web Development Reading List #149: CSS Dynamic Colors, Refactoring CSS, And
  CSP Hashing
slug: web-development-reading-list-149
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb44cbd1-0f25-44de-8e0b-49a7cedb7f72/wdrl-149-opt.png'
date: 2016-08-12T17:36:32.000Z
author: anselm-hannemann
description: >-
  Even though we think everything happens in real-time nowadays, we need
  patience. While technology has been capable of real-time for long now, the
  “bottleneck” are human beings. Whether it’s a pull request that’s waiting for
  review since days or weeks or an email response, we need to keep in mind that
  delays might happen for a good reason.
categories:
  - Web Development Reading List
---
Even though we think everything happens in real-time nowadays, we need patience. While technology has been capable of real-time for long now, the “bottleneck” are human beings. Whether it’s a pull request that’s waiting for review since days or weeks or an email response, we need to keep in mind that delays might happen for a good reason.

Different people have different priorities, they might be focusing on something else at the moment, or they just take a break. Training patience is an important aspect of mental health, and, in the end, <strong>a well-thought-out, not instantly written feedback is better</strong>, too. Take your time and let others do the same.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Prioritizing Devices: Testing And Responsive Web Design](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [Noah’s Transition To Mobile Usability Testing](https://www.smashingmagazine.com/2016/02/mobile-usability-testing/)
*   [Where Are The World’s Best Open Device Labs?](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [A Guide To Simple And Painless Mobile User Testing](https://www.smashingmagazine.com/2015/12/simple-and-painless-mobile-user-testing/)

<em>To my readers in or near Germany: Some of you might be aware that I organize a small event, and this week I have one ticket to give away for the <a href="https://nightlybuild.io/">NightlyBuild conference 2016</a> in Cologne, Germany on September, 2nd. If you want to attend, just <a href="mailto:mail@wdrl.info">send me an email</a>, and <strong>I’ll raffle the ticket on Tuesday</strong>.</em>

{{% feature-panel %}}

## News

*   WebKit now [supports `<script>` and `<style>` hashes](https://webkit.org/blog/6830/a-refined-content-security-policy/) so you don’t need to set your Content Security Policy to allow `'unsafe-inline'`.</p>

## Privacy

*   While researching a bit on user tracking, I found out about header enrichment, a technique used by mobile network providers to set unique identifiers. But more interestingly, while it’s advised by the IETF to not expose any of these headers to public servers, many ISPs do it anyway and leak the private IP addresses of devices, the IMEI/IMSI or even the phone number, to any server. [This research paper](https://www.icsi.berkeley.edu/pubs/networking/headerenrichment15.pdf) by the <abbr title="International Computer Science Institute">ICSI</abbr> analyzed the worldwide spread and impact on users’ privacy.
*   Many of you might be aware that we can’t style `:visited` states and similar browser-history-based features in CSS very well. With CSS’ new `mix-blend-mode`-feature there seems to be a leak again that lets rogue sites inspect your browsing history. [Michał Zalweski explains how it works](https://lcamtuf.blogspot.de/2016/08/css-mix-blend-mode-is-bad-for-keeping.html).
*   Netflix engineers now share [insights into how they protect the viewing privacy](https://techblog.netflix.com/2016/08/protecting-netflix-viewing-privacy-at.html) of their users by adding TLS to their video streams, which at that scale is a pretty challenging and interesting problem.</p>

## JavaScript

*   Damon Bauer shares how you can [build an image uploader in React.js](https://css-tricks.com/image-upload-manipulation-react/) and use it to manipulate the image for later usage.
*   Peter van der Zee outlines [how to reduce complexity in your code by thinking outside the box](https://qfox.nl/weblog/371). In another article worth reading, he also reflects on the question [if we need JavaScript for everything](https://qfox.nl/weblog/361). The outcome of this little anecdote is nothing ground-breaking, but something we all should remind ourselves of from time to time.</p>

## CSS/Sass

*   Erik Jung explores new ways to add [dynamic themes in CSS with CSS variables and CSS Colors Level 4](https://cloudfour.com/thinks/building-themes-with-css4-color-features/) features like the new `color()` function.
*   Meanwhile, Abbey Fitzgerald wrote a great tutorial on [how to use CSS and SVG clipping and masking techniques](https://getflywheel.com/layout/css-svg-clipping-and-masking-techniques/) to create new types of layouts on websites.
*   Harry Roberts now shares the slides to his talk “[Refactoring CSS Without Losing Your Mind](https://speakerdeck.com/csswizardry/refactoring-css-without-losing-your-mind)”. Having experienced many of the mentioned problems already in the past, I think there are a lot of great tricks in there that can be really helpful.

<figure><a href="https://getflywheel.com/layout/css-svg-clipping-and-masking-techniques/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7adb1513-90af-4984-afff-d051a889663e/svg-mask-opt.png" alt="An SVG mask on an SVG element" width="500" height="247" /></a><figcaption>Clipping and masking allows for interesting ways to show or hide pieces of your graphics. Abbey Fitzgerald explains <a href="https://getflywheel.com/layout/css-svg-clipping-and-masking-techniques/">how to do it with CSS and SVG</a>.</figcaption></figure>

## Work & Life

*   Today I read an interesting [statement about constant learning](https://further.net/tricky-goals/) (see the blockquote below) with which I fundamentally disagree. So instead of following this advice, I want to encourage you to take a break from constant learning every few days. There are reasons why you should rest on a weekend and recover from learning new things during the week: By taking a break, you’ll eagerly await learning something new afterwards.

<blockquote>“In today’s highly competitive business environment, we all need to be in constant learning mode. No one can afford to take a vacation from developing new skills, especially as economic and political uncertainty threaten businesses and job stability and make future career prospects unclear.”</blockquote>

*   Rose Marcario, CEO of Patagonia, has published an essay on [why it’s important that employers support families](https://www.linkedin.com/pulse/why-should-employers-care-families-rose-marcario). It’s not just about saying this but about taking meaningful, real action to make employees feel comfortable, have a good life, and enjoy working for their employer.</p>

## Going Beyond…

*   The NASA started a new blog called “[Science WOW!](https://blogs.nasa.gov/educationsciencewow/)” which shares educational articles on science each week. If you’re interested in learning how hurricanes form or about space exploration stuff, this might be for you.

<em>And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</em>

{{< signature "ah" >}}


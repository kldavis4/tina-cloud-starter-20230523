---
title: >-
  Web Development Reading List #166: Efficient Docker, CSP Learnings, And
  JavaScript’s Global Object
slug: web-development-reading-list-166
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/335a3259-7808-4b02-b177-6677e63ab5ea/wdrl-166-opt.png'
date: 2017-01-20T20:35:22.000Z
author: anselm-hannemann
description: >-
  What fuels your work? What fuels your mind? What do you do on a non-productive
  day or when you’re sad? Nowadays, I try to embrace these times. I try to relax
  and not be angry at myself for not being productive.

  And the fun fact about it? Well, most of the times when I could convince my
  mind that not being productive is nothing to feel bad about, things take a
  sudden turn: I get my ideas back, my productivity rises and, in effect, I even
  achieve more work than on an average day. It’s important to try to be
  human.
categories:
  - Web Development Reading List
---
And the fun fact about it? Well, most of the times when I could convince my mind that not being productive is nothing to feel bad about, things take a sudden turn: I get my ideas back, my productivity rises and, in effect, I even achieve more work than on an average day. **It’s important to try to be human.**

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Why You Should Stop Installing Your WebDev Environment Locally](https://www.smashingmagazine.com/2016/04/stop-installing-your-webdev-environment-locally-with-docker/)
*   [Progressive Enhancement Is Faster](https://www.smashingmagazine.com/2013/09/progressive-enhancement-is-faster/)
*   [But The Client Wants IE 6 Support!](https://www.smashingmagazine.com/2011/11/but-the-client-wants-ie-6-support/)
*   [The WAI Forward](https://www.smashingmagazine.com/2014/07/the-wai-forward/)

## News

*   I recently mentioned that most major browsers are blocking certificates from StartCom and WoSign entirely or plan to do so in the future. However, [it seems that these certificate authorities still sell certificates](https://ma.ttias.be/despite-revoked-cas-startcom-wosign-continue-sell-certificates/). Don’t buy from them, their certificates will be useless by next month.</p>

## General

*   Rachel Andrew recently wrote about [why it’s important to reframe browser support for websites](https://www.rachelandrew.co.uk/archives/2017/01/12/browser-support-for-evergreen-websites/) and how you can deal with an IE9 supporting website and modern web technologies at the same time.</p>

## Tools & Workflows

*   Harry Roberts shares why he [prefers to use `ack` over `grep` in the command line](https://csswizardry.com/2017/01/ack-for-css-developers/) to search for strings or regular expressions in files.
*   Many of our projects are using Docker nowadays. But many Dockerfiles are written inefficiently, especially if you’re using npm. David Weinstein shares why you should [use caching to improve the performance of your Docker container](https://bitjudo.com/blog/2014/03/13/building-efficient-dockerfiles-node-dot-js/).
*   Tobias Tom [explores Docker and explains from scratch how to use it](https://tobiastom.name/explains/docker), including how to clean up your computer when you don’t need the image anymore.</p>

## Security

*   A few months ago, Github shared their [learnings from using the `Content Security Policy` at github.com](https://githubengineering.com/githubs-csp-journey/). Now they share more learnings in “[GitHub’s post-CSP journey](https://githubengineering.com/githubs-post-csp-journey/)”. The focus lies on `img-src`, form nonces, same-site cookies, and more.
*   Whoops. We already knew that fingerprint mechanisms are easy to circumvent due to their design. However, with high-quality cameras on most smartphones, [researchers now warn that your fingerprint could get stolen when you flash a ‘peace’ sign in a photo](https://www.japantimes.co.jp/news/2017/01/11/national/crime-legal/researchers-warn-fingerprint-theft-peace-sign/). This type of attack is pretty similar to what the speaker Ursel presented at a Chaos Computer Club event in 2014 about [iris scan theft from photos](https://www.ccc.de/en/updates/2014/ursel).</p>

## Web Performance

*   Scott Jehl shares how they [improved and modernized their Progressive Enhancement delivery at Filament Group](https://www.filamentgroup.com/lab/modernizing-delivery.html). With HTTP/2, Service Worker, and web app manifests, there are new tools that can speed up delivery of a site non-destructively.

{{% feature-panel %}}

<figure><a href="https://www.filamentgroup.com/lab/modernizing-delivery.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdf18973-d211-45dc-94b5-b14661f070a0/filament-group-progressive-web-app-opt.png" width="800" height="442" alt="Filament Group Modernizing Progressive Enhancement Delivery" /></a><figcaption>With its <a href="https://www.filamentgroup.com/lab/modernizing-delivery.html">modernized progressive enhancement delivery</a> in place, the Filament Group website can even be deemed a bonified Progressive Web App.</figcaption></figure>

## Accessibility

*   ARIA 1.1 was published and there have been [some additions to the `role` attribute](https://www.ssbbartgroup.com/blog/differences-aria-1-0-1-1-additions-role/). New, for example, are `role=term`, `role=feed`, and `role=switch`.
*   Rodney Rehm updated his focus management library ally.js with SVG support and wrote a tutorial on [how to manage focus in your SVG code](https://allyjs.io/tutorials/focusing-in-svg.html).</p>

## JavaScript

*   [Chart.js](https://www.chartjs.org/) is a nice library that uses subtle animations to draw canvas charts on a page. Mixed chart types are available.
*   Stefan Judis wrote about [the global object in JavaScript](https://www.contentful.com/blog/2017/01/17/the-global-object-in-javascript/), variables and the issues around it. This is not only useful for people with beginner or intermediate JavaScript knowledge but also for advanced users who want to understand the topic better.
*   Todd Motto published an “[Angular 2+ Fundamentals](https://ultimateangular.com/angular-2-fundamentals)” video course in which he explains Angular, Typescript, component architecture, and other modern programming concepts.

<figure><a href="https://www.contentful.com/blog/2017/01/17/the-global-object-in-javascript/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de575013-4fb4-4717-96f1-a56c01468ed5/global-object-javascript-opt.png" width="800" height="335" alt="The Global Object In JavaScript" /></a><figcaption>Stefan Judis takes a new look at the <a href="https://www.contentful.com/blog/2017/01/17/the-global-object-in-javascript/">global object in JavaScript</a>. (<a href="https://www.contentful.com/blog/2017/01/17/the-global-object-in-javascript/">Image credit</a>)</figcaption></figure>

## Work & Life

*   Raquel Vélez shares [six tricks to leading a healthy, productive life](https://superyesmore.com/rockbots-6-tricks-to-leading-a-healthy-productive-life-8b553b6c4ac1112787d2d52d3804ea64).</p>

## Going Beyond…

*   This [visual introduction to machine learning](https://www.r2d3.us/visual-intro-to-machine-learning-part-1/) explains how computers apply statistical learning techniques to automatically identify patterns in data. If you’re not familiar with how machine learning works, this will give you a rough idea.
*   As we’ve seen in statistics and data from the NASA before, this is, unfortunately, the truth: [2016 was the hottest year on record](https://www.bloomberg.com/graphics/hottest-year-on-record/). The consequences: Nearly a quarter of the Great Barrier Reef died, Canada had to deal with the costliest wildfires ever, and the Arctic sea ice has been at its smallest winter maximum for two years now. And do you remember Hurricane Matthew? Such weather events are mostly driven by the climate change that we’re facing right now, with no trend of change over the upcoming years. Fortunately, there’s something everyone of us can do: The UN shows [how we can take action, even from the couch at home](https://www.un.org/sustainabledevelopment/takeaction/).

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_


---
title: >-
  Web Development Reading List #142: Contextual Identities, Form Hints, And
  ApplePay.js
slug: web-development-reading-list-142
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79749cdf-e129-4469-8138-cb75a9263ea4/wdrl-142-opt.png'
date: 2016-06-24T20:01:00.000Z
author: anselm-hannemann
description: >-
  Today will be a day in history regardless of what happens over the next weeks.
  The majority of people in the UK voted to leave the EU, and this made clear
  once again that many people in our society think the current situation is no
  longer acceptable. Unfortunately, we think blaming those people is the
  solution, but, as we see, it isn’t. Instead, we should focus on **teaching
  people about the root causes of problems**, and we should retain from posting
  everything right away.

  In other news, I’m back from vacation to bring you new articles to read. And I
  realized one thing: While mountaineering holds real risks and dangers, working
  on websites mostly does not. Of course, the **security** of our websites
  should be a top priority, but even if we fail, if a website is down for a few
  minutes, if we screwed up the layout on some devices, you won’t be dead. We
  have the opportunity to improve our work by making mistakes and fixing them.
categories:
  - Web Development Reading List
---
Today will be a day in history regardless of what happens over the next weeks. The majority of people in the UK voted to leave the EU, and this made clear once again that many people in our society think the current situation is no longer acceptable. Unfortunately, we think blaming those people is the solution, but, as we see, it isn’t. Instead, we should focus on <strong>teaching people about the root causes of problems</strong>, and we should refrain from posting everything right away.

In other news, I’m back from vacation to bring you new articles to read. And I realized one thing: While mountaineering holds real risks and dangers, working on websites mostly does not. Of course, the <strong>security</strong> of our websites should be a top priority, but even if we fail, if a website is down for a few minutes, if we screwed up the layout on some devices, you won’t be dead. We have the opportunity to improve our work by making mistakes and fixing them.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Website Performance: What To Know and What You Can Do](https://www.smashingmagazine.com/2010/01/page-performance-what-to-know-and-what-you-can-do/)
*   [Data-Driven Design In The Real World](https://www.smashingmagazine.com/2013/09/data-driven-design-in-the-real-world/)
*   [A Roadmap To Becoming An A/B Testing Expert](https://www.smashingmagazine.com/2014/07/roadmap-to-becoming-an-a-b-testing-expert/)
*   [Multivariate Testing 101: A Scientific Method Of Optimizing Design](https://www.smashingmagazine.com/2011/04/multivariate-testing-101-a-scientific-method-of-optimizing-design/)

## News

*   [Safari 10 has been announced](https://developer.apple.com/library/prerelease/content/releasenotes/General/WhatsNewInSafari/Articles/Safari_10_0.html) at WWDC, and it has some great new features: IndexedDB support, <abbr title="Content Security Policy">CSP 2.0</abbr>, Shadow DOM 1, complete ES6/ES2015 support, ES internationalization API support, inline and auto video playback on iOS, Picture in Picture on OS X, and WOFF2 support as well as font loading support (yay!). In CSS we now have `object-position` for the already available `object-fit` property and clipping using SVG paths. Last but not least, from now on, even if `user-scalable=no` is set as viewport rule, [users will be able to pinch-and-zoom](https://twitter.com/thomasfuchs/status/742531231007559680).</p>

## Concept & Design

*   Mozilla introduced a [new way to differentiate between life contexts in your browser](https://blog.mozilla.org/tanvi/2016/06/16/contextual-identities-on-the-web/). You can now open a “work” or a “banking” tab, each created in its own context so that you can login to different Twitter accounts in one browser window, for example. This is an interesting concept, especially since the workflow is pretty well thought out already, making the browser experience way better.

{{% feature-panel %}}

<figure><a href="https://blog.mozilla.org/tanvi/2016/06/16/contextual-identities-on-the-web/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95f82590-c776-4d5b-85bf-14adf52a39dc/contextual-identities-opt.png" alt="Contextual identities in Firefox Nightly" width="500" height="334" /></a><figcaption><a href="https://blog.mozilla.org/tanvi/2016/06/16/contextual-identities-on-the-web/">Contextual identities in Firefox Nightly</a> enable users to open tabs in different contexts — Personal, Work, Banking, Shopping — and segregates site data for improved privacy and security. (Image credit: <a href="https://blog.mozilla.org/tanvi/2016/06/16/contextual-identities-on-the-web/">Mozilla</a>)</figcaption></figure>

## Tools & Workflows

*   This week, Adobe presented a new beta of their code editor Dreamweaver. [I had a look at it, and am pretty impressed](https://medium.com/@helloanselm/dreamweaver-is-back-for-us-coders-2a1be75ae595) that they managed to turn the tide and make it an appealing, modern editor for professional coders again. I’m curious what the open feedback will bring to the final product in the future.</p>

## Security

*   CIA director John Brennan is a pretty confident man. He recently told US senators to [not worry about mandatory encryption backdoors hurting American businesses](https://www.theregister.co.uk/2016/06/17/non_us_encryption_is_theoretical_claims_cia/), simply because there are no non-US products that are successful. Unfortunately, he’s right. There aren’t a lot of products that aren’t US-based, and that’s all the CIA wants, as it’s enough to tap on most traffic which comes from Facebook, Google, Microsoft, Apple, and Yahoo anyways.</p>

## Privacy

*   “Starting with iOS 10, Apple is using Differential Privacy technology to help discover the usage patterns of a large number of users without compromising individual privacy.” [Matthew Green comments on this new technology](https://blog.cryptographyengineering.com/2016/06/what-is-differential-privacy.html) and tries to find out the advantages, disadvantages and implications of it.
*   Facebook wants to prove that its ads lead to actual purchases. That’s why Facebook advertisers can now add their physical store locations, and Facebook will then track users by their phone locations and report if they have visited the store. Of course, Facebook is not the first company doing that: Google folks are proud of [having done the same already for quite some time](https://twitter.com/Speroman/status/742792033358647297). I’m glad I don’t have apps of these brands on my phone anymore.
*   Archive.org — the project that saves our online history every day. A project that we all love since it can recover sites that don’t even exist anymore, right? Well, it seems not everyone is happy about it, and Brewster Kahle explains the problems they face: While trying to protect the privacy of their users, they face massive DDoS attacks and are blocked by various restrictive countries. Now they share [why routing the DNS via Cloudflare isn’t an option](https://blog.archive.org/2016/06/16/geez-now-internet-insurance/0) and why they rely on our donations to run the project.</p>

## HTML & SVG

*   Following [Safari that introduced the feature already in iOS 8](https://lmjabreu.com/post/ios-8-privacy-updates/#safari-keychain-improvements), you’ll now be able to [add `autocomplete="new-password"`](https://twitter.com/rem/status/744928019605766144) to hint upcoming Chrome versions at generating a password. It’s possible to [add other hints](https://html.spec.whatwg.org/multipage/forms.html#autofill), too — `current-password` or `username`, for example.
*   Despite being a simple and old attribute, you can find a lot of websites doing it wrong: HTML’s `lang`. Sometimes it’s not declared at all, and sometimes its value is `"en"` although the content is not in English. Learn [how to use the `lang`-attribute properly and where you can apply it](https://www.paciellogroup.com/blog/2016/06/using-the-html-lang-attribute/).</p>

## Accessibility

*   Rob Dodson explains why we should [build better accessibility primitives](https://robdodson.me/building-better-accessibility-primitives/) at the example of modals and disabling tabindex.
*   Google released a [free web accessibility course on udacity](https://www.udacity.com/course/web-accessibility--ud891).

<figure><a href="https://robdodson.me/building-better-accessibility-primitives/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0ab5ebc-a8ef-4ad1-ac94-ad8391dd9b10/accessibility-primitives-opt.png" alt="Modal window on an e-commerce site" width="500" height="280" /></a><figcaption>Modals are usually an accessibility bottleneck. Rob Dodson explains <a href="https://robdodson.me/building-better-accessibility-primitives/">how we can improve them</a>. (Image credit: <a href="https://robdodson.me/building-better-accessibility-primitives/">Rob Dodson</a>)</figcaption></figure>

## JavaScript

*   [AOS](https://css-tricks.com/aos-css-driven-scroll-animation-library/) is a CSS-driven on-scroll animation library that gives the user full control over styling.
*   You can now start implementing Apple Pay into your website by using the company’s [ApplePay JavaScript framework](https://developer.apple.com/reference/applepayjs). It’s interesting that Google and Apple both heavily work on getting their payment systems directly into the browser. Unfortunately, but also usual for Apple, they don’t follow a web standard such as the [Web Payment API](https://www.w3.org/blog/wpwg/2016/03/04/fpwd/) here but provide only their own ecosystem.</p>

## CSS/Sass

*   In his CodePen demo, Jonathan Neal shares how to make a [decorative text underline with box-shadow](https://codepen.io/jonneal/pen/PzGYEE?editors=0100) that weaves between text descenders and preserves the text color.
*   Client-side form validation is hard, we all know that. But thanks to the browsers’ internal validation API, we can display very clever messages telling the user what went wrong. This article shows how to do that effectively and even offers a boilerplate.
*   Often we don’t use the full potential of CSS for [form validation UX](https://css-tricks.com/form-validation-ux-html-css/). Chris Coyier shares some CSS trickery to get it right.</p>

## Going beyond…

*   It’s not surprising that big data companies like Google are no opponents of CETA or TPP/TTIP. What’s more surprising is that [Google now takes a firm stand on supporting TPP](https://publicpolicy.googleblog.com/2016/06/the-trans-pacific-partnership-step.html). With bloodcurdling logic they argument why it would be a step forward for the internet: “But Internet restrictions — like censorship, site-blocking, and forced local storage of data — threaten the Internet’s open architecture.” None of these issues would disappear with TPP except for local storage (which is a feature that the EU finally enforced last year in its fight to protect users’ privacy). TPP instead enforces copyright protections, can do nothing to prevent non-TPP-partners from blocking parts of the internet, and actually does a lot of harm to existing privacy, to existing laws and to countries’ courts as it gives companies the possibility to bring matters to arbitral courts — a fact that helps corrupt, capitalistic companies gain more power while normal citizens are at a disadvantage. You can see how much influence private companies already have on politicians in the excellent Netflix series “[House of Cards](https://en.wikipedia.org/wiki/House_of_Cards_(U.S._TV_series)#Reception)”.
*   I already linked to NASA’s “Mars Explorers Wanted” posters recently, but now they [added new ones](https://mars.nasa.gov/multimedia/resources/mars-posters-explorers-wanted/) for you to download. Still very nice examples on how to design beautiful, unique posters.

<em>And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</em>

{{< signature "ah" >}}


---
title: >-
  Web Development Reading List #151: Microinteraction UX, Feature Policy, And
  Passport.js
slug: web-development-reading-list-151
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd5ec61c-c976-4574-9f9e-ed4069724678/wdrl-151-opt.png'
date: 2016-08-26T18:16:58.000Z
author: anselm-hannemann
description: >-
  In the last few years, I’ve seen a lot of code. As a freelancer working on
  multiple big projects with a lot of people, you’ll inevitably see all
  varieties of code styles. But I also realized how much writing JavaScript
  changed over the past years.

  Having learned JavaScript before ES6 was there, a great mentor ([Hans
  Christian Reinl](https://drublic.de/)) taught me the most important lesson:
  **Always write clean, understandable code**. Avoid ternary operators, declare
  variables in one place, make functions as simple as possible. Basically things
  that so many JavaScript style guides also advise. But with the growing
  adoption of ES6/ES2015, I also saw an increase of code where most of these
  principles (except for keeping functions small) are ignored.
categories:
  - Web Development Reading List
---
In the last few years, I’ve seen a lot of code. As a freelancer working on multiple big projects with a lot of people, you’ll inevitably see all varieties of code styles. But I also realized how much writing JavaScript changed over the past years.

Having learned JavaScript before ES6 was there, a great mentor ([Hans Christian Reinl](https://drublic.de/)) taught me the most important lesson: **Always write clean, understandable code**. Avoid ternary operators, declare variables in one place, make functions as simple as possible. Basically things that so many JavaScript style guides also advise. But with the growing adoption of ES6/ES2015, I also saw an increase of code where most of these principles (except for keeping functions small) are ignored.

I think it has something to do with the **increased flexibility of ES6**. A lot of developers probably think since arrow functions — which are shorter than a normal function — can be used, they should also write everything else in the shortest, smartest way. However, in my opinion and experience, this leads to a less maintainable codebase, one that’s hard to read for people who don’t work on it on a daily basis. Be smarter! By applying simplicity and not cleverness to your code.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Why Coding Style Matters](https://www.smashingmagazine.com/2012/10/why-coding-style-matters/)
*   [Functional Animation In UX Design](https://www.smashingmagazine.com/2015/05/functional-ux-design-animations/)
*   [Keys To Better Communication With Clients](https://www.smashingmagazine.com/2012/07/keys-better-client-communication/)
*   [How To Communicate Design Decisions To Clients?](https://www.smashingmagazine.com/2008/07/how-to-communicate-design-decisions-to-clients/)

## News

*   [Carbide Alpha](https://alpha.trycarbide.com/) is a new kind of programming environment which requires no installation/setup, has auto-import for npm and GitHub, and does some other crazy stuff. Just have a look at all the amazing features that are listed on the website.</p>

## Concept & Design

*   Ali Torbati shares the process of [reimagining Spokeo’s advanced search tools](https://medium.com/@alitorbati/death-to-complexity-how-we-simplified-advanced-search-a9ab2940acf0). All about making a very complex interface as simple as possible.
*   Little details are often important details. Nick Babich explores how [animated microinteractions improve usability in mobile apps](https://www.smashingmagazine.com/2016/08/experience-design-essentials-animated-microinteractions-in-mobile-apps/).

{{% feature-panel %}}

<figure><a href="https://medium.com/@alitorbati/death-to-complexity-how-we-simplified-advanced-search-a9ab2940acf0"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4aa07db3-3eac-4970-ac2f-5467e60e734f/spokeo-opt.png" width="500" height="354" alt="Spokeo navigation" /></a><figcaption>Spokeo declared death to complexity and <a href="https://medium.com/@alitorbati/death-to-complexity-how-we-simplified-advanced-search-a9ab2940acf0">simplified their advanced search</a>. (Image credit: <a href="https://medium.com/@alitorbati/death-to-complexity-how-we-simplified-advanced-search-a9ab2940acf0">Ali Torbati</a>)</figcaption></figure>

## Security

*   Both the W3C and WICG (Web Incubator CG) share ideas on two new headers: [`Clear-Site-Data`](https://www.w3.org/TR/clear-site-data/) and [`Feature-Policy`](https://wicg.github.io/feature-policy/). They both improve the security and privacy of users. While the first one can clean locally-stored objects, the latter declares features the browser is allowed to use within the origin, such as geolocation, cookies, and WebRTC. As a site-owner, you can use this to prevent a third-party from tracking your users.
*   [<abbr title="United States National Institute for Standards and Technology">NIST</abbr>’s new password rules](https://nakedsecurity.sophos.com/2016/08/18/nists-new-password-rules-what-you-need-to-know/) say that text messages shouldn’t be used for two-factor authentication anymore. A huge progress that will hopefully lead to less crappy <abbr title="Two-factor authentication">2FA</abbr> in the future.
*   I recently shared [an attack abusing `target="_blank"`](https://wdrl.info/archive/129/977fcb771e018ba5f347e68a1ab515878c5bebb2) on pages where users can add custom URLs. To make clear how bad the attack is, Ben Halpern now shows [how he made it work on Instagram](https://dev.to/ben/the-targetblank-vulnerability-by-example) (they fixed it pretty fast). So remember to use `rel="noopener"` for any URL that you didn’t hard-code into the source.

<figure><a href="https://nakedsecurity.sophos.com/2016/08/18/nists-new-password-rules-what-you-need-to-know/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf5694c-13d1-4a1b-82f0-7162ca1a2b65/nist-opt.png" width="500" height="297" alt="New password rules" /></a><figcaption>The United States National Institute for Standards and Technology (NIST) formulated new <a href="https://nakedsecurity.sophos.com/2016/08/18/nists-new-password-rules-what-you-need-to-know/">guidelines for password policies</a> to be used in the US government. (Image credit: <a href="https://nakedsecurity.sophos.com/2016/08/18/nists-new-password-rules-what-you-need-to-know/">Naked Security</a>)</figcaption></figure>

## Web Performance

*   Eduardo Bouças explains [how to use the WebPageTest API](https://css-tricks.com/use-webpagetest-api/) to improve your quality assurance process.</p>

## JavaScript

*   The JavaScript library [Grade.js](https://benhowdle.im/grade/) produces complementary gradients generated from the top two dominant colors of an image.
*   Brecht Billiet explains why you don’t always need a third-party component and illustrates this with an example of [building a modal in Angular 2](https://blog.brecht.io/Modals-in-angular2/).
*   [Passport.js](https://www.passportjs.org/) is an authentication middleware for Node.js, supporting authentication via username and password, Facebook, Twitter, and many more.</p>

## Work & Life

*   When dealing with clients, it’s important to [ask the right questions](https://alistapart.com/article/why-arent-you-asking-questions). It’s your job to find out what the end user needs and to guide the client to what they want.

## Going Beyond…

*   We’ve been breaking global temperature records since ten months. And [July was the hottest July on record](https://www.slate.com/blogs/bad_astronomy/2016/08/16/july_2016_was_the_hottest_july_on_record.html).
*   You can now [contribute to OpenStreetView](https://www.openstreetmap.org/user/mvexel/diary/39274) with your phone. The aim of creating an open-source alternative to Google’s Streetview functionality is really promising and has already [some locations covered](https://openstreetview.org/map/@36.77409249464195,-122.83126831054686,8z). This is especially interesting in situations where people need fast updates — like in the case of the earthquake that stroke Italy this week and in which contributors updated all the maps in OpenStreetMap within a few hours.
*   [Xaddress](https://xaddress.org/) is an interesting idea of a universal address for every human on the world. It’s great to see the challenges of such systems and how we could solve them.
*   [This interview with Steven Pinker](https://www.vox.com/2016/8/16/12486586/2016-worst-year-ever-violence-trump-terrorism), psychology professor at Harvard University, explains why we think 2016 is the worst year ever. And next year will be the same. It’s a psychological issue since the news share only things that happened but not things that didn’t happen. If we look at the overall statistics of threats worldwide, we live in a safer and better world than ever before.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_


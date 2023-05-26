---
title: 'Monthly Web Development Update 2/2019: Web Authentication And The Problem With UX'
slug: monthly-web-development-update-2-2019
author: anselm-hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31d9e667-e2d2-42ad-bc70-0a6646d4277c/humans-not-users-opt.png
date: 2019-02-15T11:42:15+01:00
summary: >-
  Browser news, valuable lessons learned, best practices, inspiring coding experiments. In his monthly reading list, Anselm Hannemann summarized the most important things that happened in the web development world in the past few weeks.
description: >-
  Browser news, valuable lessons learned, best practices, inspiring coding experiments. In his monthly reading list, Anselm Hannemann summarized the most important things that happened in the web development world in the past few weeks.
categories:
  - Web Development Reading List
---
The only constant in life is change, they say. And it’s true, even if we think nothing changes at all. Whether you notice change or not is only a question of how you perceive and how you observe things. In the tech industry, it’s easy to see how fast things evolve — read a summary article like this one, and you’ll suddenly become aware of how much has happened in just one month. Since I [took up meditation again](https://helloanselm.com/writings/evolvement-through-meditation), I gained a new perspective, and it helps me to deliberately appreciate such change and find **personal value and gratefulness** even in things that didn’t seem particularly positive at first.

Like this week, for example. I was reminded of a fact we usually forget: how the Internet is structured. If you browse the web, most traffic is directed through Amazon at some point, so if you block their servers, — or Google’s or Apple’s, or all of them —, there’s not much left of the Internet. I have used a [Pi-Hole DNS blocker](https://pi-hole.net/) in my network for three years now, but never really appreciated it, until I learned about its real value this week — [the security and privacy it provides](https://helloanselm.com/writings/tech-giants-dependency) considering our dependency on tech giants. Isn’t it remarkable how a big part of my perceived online security relies on one piece of open-source software that the authors spent so much time and efforts on to provide it for free in the end?

## News

- [Firefox 65 was released](https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/65). The new version dispatches events on `disabled` HTML elements and comes with support for the `referrerpolicy` attribute on `script` elements, CSS environment variables ([the `env()` function](https://developer.mozilla.org/en-US/docs/Web/CSS/env)), `Intl.RelativeTimeFormat` for JavaScript, and WebP images.
- [Safari Tech Preview 74](https://webkit.org/blog/8566/release-notes-for-safari-technology-preview-74/) brings abortable `fetch`, support for U2F HID Authenticators on macOS, and new Web Authentication API features.
- With [Chrome 72](https://developers.google.com/web/updates/2019/01/nic72), Chrome introduced the User Activation API. The new version also disallows popups on `pageunload`.
- The Chrome 72 update for Android shipped the long-awaited Trusted Web Activity feature, which means we can now [distribute PWAs in the Google Play Store](https://medium.com/@firt/google-play-store-now-open-for-progressive-web-apps-ec6f3c6ff3cc).
- [Safari 12.1 release notes are up](https://developer.apple.com/documentation/safari_release_notes/safari_12_1_release_notes?language=objc) (iOS 12.2, macOS 10.14.4). What’s new? Dark mode for the web, intelligent tracking prevention, the push notification prompt for Safari on macOS now requires a user gesture, motion and orientation settings on iOS to enable `DeviceMotionEvent` and `DeviceOrientationEvent` (this means it’s disabled by default now). Also new are the Intersection Observer API, Web Share API, and the `<datalist>` element.

{{% feature-panel %}}

## General

- Max Böck shares his thoughts on why [simplicity is the most valuable and important thing in projects](https://mxb.at/blog/on-simplicity/).
- [Ian Littman on Twitter](https://twitter.com/iansltx/status/1088786098564808704): “Moving 50% of servers to PHP 7 from PHP 5 would save $2.5 (edited to 2.0) billion in energy costs per year, and avoid billions of kilograms of CO2 emissions. Upgrade to PHP 7. Save the planet.”
- How did you start to learn web development? I guess most of us relied on our browsers’ “view source” functionality and still do. But with JavaScript SPAs and more tooling that mangles, minifies and uglifies sources, we block this road of self-education for countless people out there. Let’s move to a more open approach and at least [provide source maps on production servers](https://m.signalvnoise.com/paying-tribute-to-the-web-with-view-source/) so that people can access the actual sources via Developer Tools.

## UI/UX

- What makes the difference between a good digital product and a great digital product? Two letters: UX. User Experience Design. But there’s a fundamental problem with that. Johannes Ippen on why we should see [humans, not users](https://johannesippen.com/2019/humans-not-users/).
- This is a nice roundup of [how popular websites have changed over the past ten years](https://www.arun.is/blog/10-year-challenge/) — including Google, YouTube, Amazon, Facebook, Apple, and eBay. You can clearly see that we’re in a different era today.
- Colin Eagan sums up [the dozens of possibilities we have to personalize a web experience for the user](https://alistapart.com/article/emerging-ux-role-in-personalization) and which of them work and which don’t. He concludes with a valuable piece of advice: to start simple instead of following the cult of complex, no matter how tech-savvy the company and its team are.

{{< rimg href="https://johannesippen.com/2019/humans-not-users/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31d9e667-e2d2-42ad-bc70-0a6646d4277c/humans-not-users-opt.png" sizes="100vw" caption="To create stellar user experiences we need to <a href='https://johannesippen.com/2019/humans-not-users/'>see our users as humans</a>. (<a href='https://johannesippen.com/2019/humans-not-users/'>Image credit</a>)" alt="Sketch of a face with the terms see, say and do, hear, think and feel floating around it" >}}

## HTML &amp; SVG

- Sara Soueidan wrote a [101 course on SVG filters](https://tympanus.net/codrops/2019/01/15/svg-filters-101/) to help you understand what they are and how to use them to create your own visual effects.

## Accessibility

- Rob Dodson shares a great summary on [how to build better accessibility primitives](https://robdodson.me/building-better-accessibility-primitives/).

## Privacy

- Google is one of those companies which [always find new, clever ways to expose user location data](https://theintercept.com/2019/01/28/google-alphabet-sidewalk-labs-replica-cellphone-data/) and sell it to third parties. Now Google wants to sell the exact location data of users to improve planning for urban planners, for example. Useful on the one hand, but still worrying for all users of Google products who might not be aware of what happens with their data.
- “[I was wrong about Google and Facebook: there’s nothing wrong with them](https://ar.al/2019/01/11/i-was-wrong-about-google-and-facebook-theres-nothing-wrong-with-them-so-say-we-all/) (so say we all),” says Aral Balkan. This piece explains how even the most honorable open-source projects struggle to make ethical choices and the fallacies of offering the best UX instead of promoting ethically correct solutions.

{{% ad-panel-leaderboard %}}

## Web Performance

- Jens Oliver Meiert shares his research on [how the way you write HTML influences performance](https://meiert.com/en/blog/html-performance/). Leaving out optional tags and quotes can make a difference, even though we’re able to use gzip or other techniques to optimize the document response in the browser.

## JavaScript

- With most data breaches happening due to weak and reused passwords, web authentication is a hot topic these days. The new *[Guide to Web Authentication](https://webauthn.guide/)* is an excellent example that a security implementation guide can be beautiful, too.
- Mathias Schäfer summarized his [lessons learned from maintaining large JS codebases](https://9elements.com/io/maintaining-large-javascript-projects/) in long-term projects.
- Dr. Axel Rauschmayer describes [what is still missing in JavaScript](https://2ality.com/2019/01/future-js.html) and what could be implemented in the future.
- [Intersection Observer](https://webkit.org/blog/8582/intersectionobserver-in-webkit/) landed in WebKit, and the Webkit team wrote a helpful tutorial for it.

{{< rimg href="https://webauthn.guide/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23d82bb7-a2e8-4a7c-bdac-81776babd06f/web-authn-guide-opt.png" sizes="100vw" caption="The <em><a href='https://webauthn.guide/'>Guide to Web Authentication</a></em> is a handy introduction to securing sensitive information online. (<a href='https://webauthn.guide/'>Image credit</a>)" alt="Excerpt from the guide. It shows an illustration of a tiny woman who tries to prevent a giant wad of keys from tumbling over." >}}

## CSS

- Rik Schennink explains how to use smart CSS to [apply styles based on the user scroll position](https://pqina.nl/blog/applying-styles-based-on-the-user-scroll-position-with-smart-css/).
- It’s incredible how Fabricius Seifert created this [Solar System 3D animation with pure CSS](https://codepen.io/briziel/full/oJdNdB).
- Preethi Sam explains how to use the [little-known CSS `element()` function to create a minimap navigator](https://css-tricks.com/using-the-little-known-css-element-function-to-create-a-minimap-navigator/).
- Roman Komarov shares his approach to a [flexible blog layout with an optional sidebar](https://www.kizu.ru/my-grid-layout/). Made with CSS Grid and Custom Properties.

{{< rimg href="https://codepen.io/briziel/full/oJdNdB" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/706efd45-d6ad-4ee3-a02a-b200968b46dc/solar-system-opt.png" sizes="100vw" caption="<a href='https://codepen.io/briziel/full/oJdNdB'>Explore the solar system</a> in Fabricius Seifert’s fantastic CSS experiment. (<a href='https://codepen.io/briziel/full/oJdNdB'>Image credit</a>)" alt="Solar system built with CSS" >}}

## Work &amp; Life

- Paul Greenberg is [in search of lost screen time](https://www.nytimes.com/2018/12/31/opinion/smartphones-screen-time.html) and explores what our lives could look like and how much more time we’d have if we escaped the screens. There are some revealing numbers in the article: The average American spends $14,000 per decade on smartphones. That’s $70,000 over the course of an average working life. More than 29% of Americans would rather give up sex for three months than give up their smartphone for a single week. Or you could plant 150 trees and buy half an acre of land for the amount of money you’d spent on your smartphone and apps per year.
- Are you a patient person? Regardless of if you are or not, the experiment that Jason Fried wants to try is certainly a challenge: [Try to pick the longest line at the supermarket](https://m.signalvnoise.com/putting-on-some-wait/), cancel Amazon Prime so that delivery takes longer, and take the chance to wait whenever possible. Embrace slowness.
- “[In Praise of Extreme Moderation](https://hbr.org/2018/06/in-praise-of-extreme-moderation)” shares an interesting perspective on why the culture of over-committing, over-working, and over-delivering in all areas of life isn’t healthy, and how we can shift towards a more moderate, calmer path.

## Going Beyond…

- “[It must be free.](https://helloanselm.com/writings/it-must-be-free)” On services we obviously don’t need but want to have. My essay about the importance of seeing value in the things we really need and why less is more.
- [How can we make our lives better](https://www.bakadesuyo.com/2019/02/make-your-life-fantastic/)? By maintaining essential relationships, avoiding technology, and embracing values instead of lifehacks, says Eric Barker.
- Watch this [talk of Greta Thunberg](https://www.youtube.com/watch?v=M7dVF9xylaw), a sixteen-year-old woman who tells all the well-known and influential people out there that she doesn’t care about money and why we need to view climate change from a perspective like hers — her life is in danger and no money will be able to save it. We need more people like her who aren’t led by corporate or financial rules.

{{< signature "cm" >}}
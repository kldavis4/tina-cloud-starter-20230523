---
title: >-
  Web Development Reading List #128: Firefox 45, A Multi-Colored Font And Better
  Force-Pushing
slug: web-development-reading-list-128
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6732afc-e122-4869-bc42-5e911e9a7caf/wdrl-128-opt.png'
date: 2016-03-11T21:20:01.000Z
author: anselm-hannemann
description: >-
  Another week comes to an end, with **new browser announcements, releases and
  cool new tools** that you might want to check out. I make it short: Have fun
  reading this week’s reading list and enjoy your weekend!

  Firefox 45 is out and now re-evaluates responsive images in srcset on resize
  or viewport changes. Also, the Web Speech Synthesis API and `window.onstorage`
  were implemented, and you can now test CSS Grid Layouts. Firefox Nightly also
  got an interesting new feature: the browser can read text in Reader View.
categories:
  - Web Development Reading List
---
Another week comes to an end, with <strong>new browser announcements, releases and cool new tools</strong> that you might want to check out. I make it short: Have fun reading this week’s reading list and enjoy your weekend!

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A User-Centered Approach To Web Design For Mobile Devices](https://www.smashingmagazine.com/2011/05/a-user-centered-approach-to-web-design-for-mobile-devices/)
*   [<span class="headline">The Elements Of The Mobile User Experience</span>](https://www.smashingmagazine.com/2012/07/elements-mobile-user-experience/)
*   [A Guide To Designing Touch Keyboards (With Cheat Sheet)](https://www.smashingmagazine.com/2013/08/guide-to-designing-touch-keyboards-with-cheat-sheet/)
*   [Beyond The Button: Embracing The Gesture-Driven Interface](https://www.smashingmagazine.com/2013/05/gesture-driven-interface/)

## News

*   [Firefox 45 is out](https://developer.mozilla.org/en-US/Firefox/Releases/45) and now re-evaluates responsive images in srcset on resize or viewport changes. Also, the Web Speech Synthesis API and `window.onstorage` were implemented, and you can now test CSS Grid Layouts. Firefox Nightly also got an interesting new feature: [the browser can read text in Reader View](https://blog.monotonous.org/2016/03/07/narrate-a-new-feature-in-firefox-nightly/).
*   Opera’s desktop browser for developers now has an [option to natively block ads on websites](https://www.opera.com/blogs/desktop/2016/03/native-ad-blocking-feature-opera-for-computers/). This is a big experiment since it’ll block ads completely, without any options, and unlike Firefox’s privacy protection mode that only removes trackers but not ads in general, the Opera experiment uses the big adblock EasyList. The goal seems to be saving customer’s data budgets, and, respectively, their money.</p>

## Concepts & Design

*   These [tips for saving SVG for the web with Adobe Illustrator](https://www.viget.com/articles/5-tips-for-saving-svg-for-the-web-with-illustrator) are a great guide for creating graphics for the web.
*   [Bixa Color](https://pixelambacht.nl/2016/building-bixa-color/) is a multi-color font face for the web. Multi-color in that case means indeed that a glyph can have not only one but multiple colors.
*   Sometimes micro-copy and [tiny word changes make a big difference for a page’s UX](https://uxplanet.org/microcopy-tiny-words-with-a-huge-ux-impact-90140acc6e42).

{{% feature-panel %}}

<figure class="fwi"><a href="https://pixelambacht.nl/2016/building-bixa-color/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b878fe4-88f3-43c9-a634-f5011c19dc68/multi-color-font-opt.png" alt="Multi-color font" width="500" height="284" /></a><figcaption>Each glyph of the <a href="https://pixelambacht.nl/2016/building-bixa-color/">Bixa Color</a> font can have not only one but multiple colors.</figcaption></figure>

## Tools

*   In the last reading list, I wrote about team retrospectives. Indeed, for remote teams, this is a bit harder to achieve. That’s why it’s very interesting to read a tutorial on how to [build a real-time retrospective board with video chat](https://www.smashingmagazine.com/2016/03/building-a-real-time-retrospective-board-with-video-chat/).
*   Pushing git updates with `--force` is something you usually should avoid. There are reasons why some teams forbid this entirely, I personally like to use it for edge-cases where you want to squash your feature branch before merging. Tute Costa shares a way to [prevent you from overwriting remote changes when force-pushing](https://robots.thoughtbot.com/git-push-force-with-lease) by using the [`--force-with-lease`](https://git-scm.com/docs/git-push#_options_a_id_options_a) option instead.</p>

## Security

*   You think `PBKDF2` is pretty secure and takes long to brute-force? Well, it’s not the case when you replace the cryptographic keys with precomputed values. [Attackers are able to save 50% of PBKDF2’s CPU intensive operations](https://eprint.iacr.org/2016/273) by doing that, cutting the security in half. Given this fact, you might want to consider using Argon2 from now on.</p>

## Privacy

*   When you use location data in your web application, you should be aware of [the legal implications of using geodata](https://www.smashingmagazine.com/2016/03/location-data-web-development-and-the-law/) of your users. The article explains what you should take care of, how you can implement this behavior properly and how to respect your users’ privacy.</p>

## Web Performance

*   There is now a way to save your user’s data. It’s only available in Chrome 49 (and Opera, Yandex) where users can opt in to a feature that sends a new header to each HTTP request. As developers, [we can use this header to serve smaller assets to such users](https://deanhume.com/Home/BlogPost/service-workers--save-your-users-data-using-the-save-data-header/10139). Pretty great!
*   The MIT has found [a way to speed up website loading by decreasing network trips](https://news.mit.edu/2016/system-loads-web%20pages-34-percent-faster-0309). I’m curious how this concept will be built into software solutions in the future.</p>

## JavaScript

*   Ever heard of `[Element.scrollIntoView()](https://developer.mozilla.org/en/docs/Web/API/Element/scrollIntoView)`? It’s a nice JavaScript function to scroll the current element into the visible area of the browser window. You can pass along options for the positioning as well, but unfortunately, `scrollIntoViewOptions` only works in Firefox at the moment. The generic support for it however is pretty good already.</p>

## CSS/Sass

*   Toggling stuff is not always easy. That’s why Kitty Giraudel from Edenspiekermann released [a11y-toggle](https://dev.edenspiekermann.com/2016/03/07/introducing-a11y-toggle/), a small JavaScript plugin that creates easy, accessible toggle elements.
*   Have you ever thought of [styling how a broken image is displayed on your website](https://bitsofco.de/styling-broken-images/)? Because broken images happen quite often (especially on mobile connections) it might be worth thinking about this.</p>

## Work & Life

*   Ted Goas shares [how he works as the sole designer in a team full of developers](https://www.tedgoas.com/blog/design-in-a-sea-of-engineering). This is particularly interesting as we often hear about teams where it’s the other way round and also because we often have a developer-centered perspective on the matter.</p>

<figure class="fwi"><a href="https://www.tedgoas.com/blog/design-in-a-sea-of-engineering"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f6907be-75f7-43fc-86cc-61fc6bbdb73b/designing-in-the-sea-of-engineering-opt.png" alt="Design in a sea of engineering" width="500" height="284" /></a><figcaption>What is it like to be the sole designer in a team of engineers? Designer Ted Goas shares <a href="https://www.tedgoas.com/blog/design-in-a-sea-of-engineering">how he gets by in an engineering led company</a>. (Image credit: Ted Goas)</figcaption></figure>

## Going beyond…

*   Since Facebook announced that they donate to good causes and try to improve the health of the human species itself, Google joined this marketing train. Davey Alba from WIRED [explains why they did so, and what benefits such corporations get](https://www.wired.com/2016/03/giving-google-way/) from it. Because, as stated back when Mark Zuckerberg announced the big donation to his own charity, they could also just pay more taxes and help people that way. But of course, there’s another side to it, and that’s why they want to do this on their own.

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</p>

<em>Thanks and all the best,
Anselm</em>


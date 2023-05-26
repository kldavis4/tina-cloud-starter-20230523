---
title: >-
  Monthly Web Development Update 10/2017: CSS Grid, CAA Pitfalls, And Image
  Optimization
slug: monthly-web-development-update-10-2017
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f7ea58b-8b42-4cad-bfb4-66c0c367b2cf/web-dev-update-october-2017-opt.png
date: 2017-10-13T17:56:11.000Z
author: anselm-hannemann
description: >-
  _Editor’s Note: Welcome to this month’s web development update. Anselm has
  summarized **the most important happenings in the web community** that have
  taken place over the past few weeks in one handy list for you. Enjoy!_

  As web developers, we’re working in a very diverse environment: We have
  countless options to specialize in, but it’s impossible to keep up with
  everything. This week I read an article from a developer who realized that
  even though he has been building stuff for the web for over seven years,
  sometimes he just doesn’t understand what’s going on: “**I’m slamming my
  keyboard in frustration** as another mysterious error appears in my build
  script,” he writes.
categories:
  - Web Development Reading List
---
As web developers, we’re working in a very diverse environment: We have countless options to specialize in, but it’s impossible to keep up with everything. This week I read [an article](https://medium.com/@paulvm/javascript-development-is-not-fun-for-me-anymore-ac4e9d7b89a3) from a developer who realized that even though he has been building stuff for the web for over seven years, sometimes he just doesn’t understand what’s going on: “**I’m slamming my keyboard in frustration** as another mysterious error appears in my build script,” he writes. For him, writing JavaScript isn’t fun anymore. The tool chain got too complex, the workflows are built mainly for developer convenience, and many things that exist in the languages itself are reinvented in external libraries.

Now when I look at the articles I collected for you this month, I can relate to the kind of frustration he’s feeling. Soon we won’t be able to use .dev domains anymore, HTTPS CAA checks don’t work with private network interfaces, and when I look at a (admittedly great) tutorial on how we can replace `scroll` events with `IntersectionObserver`, I see code that might have better performance but that is more complex as what we used to do with `EventListener`.

The web is developing and changing so fast, and we need to acknowledge that we as individual persons can’t know and understand everything. And that’s fine. Choose what you want to do, **set your priorities**, and, most importantly of all, don’t hesitate to hire someone else for the things you can’t do on your own.</p>

## News

*   Mattias Geniar reminds us that Chrome, according to [a recent commit](https://chromium-review.googlesource.com/c/chromium/src/+/669923) in Chromium, will very [soon preload `.dev` domains as HTTPS via preloaded HSTS](https://ma.ttias.be/chrome-force-dev-domains-https-via-preloaded-hsts/). Google bought the domain name, and they now want it to be accessible only via HTTPS. So if you use a `.dev` name in your projects (which often is the case on your local machine, registered manually via the `hosts` file), you should switch to the reserved `.test` domain name now or consider using `localhost` instead. Once the patch lands in Chrome, you’ll not be able to access your projects anymore without a valid TLS certificate in place.
*   [HTTP Immutable Responses are now an official Internet standard](https://tools.ietf.org/html/rfc8246), and they are already available in most browsers.
*   [React 16 is out now](https://facebook.github.io/react/blog/2017/09/26/react-v16.0.html) — under a full MIT license which finally ends the debate about the previously used patent-clause copyright license. The new version comes with a rewritten core, better error handling, custom DOM attributes, and it returns fragments and strings (so no more useless `span`-elements). Also, it’s footprint has decreased by 30%.</p>

## Tooling

*   [Infusion](https://developer.paciellogroup.com/blog/2017/09/infusion-an-inclusive-documentation-builder/) is an inclusive, accessible documentation builder.
*   [Sketch 47 is out](https://blog.sketchapp.com/introducing-libraries-and-smooth-corners-in-sketch-47-2abc5dfc1fb3) with two major new features: libraries and smooth corners. Especially libraries are a huge step forward as they allow us to sync, share and update symbols from any Sketch document and even in collaboration with other people.</p>

## Web Performance

*   “[Essential Image Optimization](https://images.guide/)” by Addy Osmani is a free eBook that explains almost everything you can and should know about image optimization for the web. Be sure to take a look at it.
*   [News from Cloudflare](https://blog.cloudflare.com/introducing-cloudflare-workers/): You’ll soon be able to deploy JavaScript to Cloudflare’s edge, written against an API similar to Service Workers. Sounds pretty amazing.

{{% feature-panel %}}

<figure><a href="https://images.guide/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f04d61d-eaa8-492f-a381-b749507c9f5b/images-guide-opt.png" width="800" height="446" alt="Essential Image Optimization" /></a><figcaption>Images are still the number one bloat on the web. <a href="https://images.guide/">Addy Osmani’s new eBook</a> explains how you can change that by compressing your images efficiently. (<a href="https://images.guide/">Image credit</a>)</figcaption></figure>

## CSS

*   Mozilla built a [CSS Grid playground](https://mozilladevelopers.github.io/playground/) that helps you wrap your head around and build with the new layouting technique.
*   Lea Verou started a very useful discussion about specificity of the `:not()` selector and why [it would be useful to have a pseudo-class `:matches`](https://github.com/w3c/csswg-drafts/issues/1170) which doesn’t carry any specificity.
*   [Balloon.css](https://kazzkiq.github.io/balloon.css/) lets you add tooltips to elements without JavaScript and in just a few lines of CSS.
*   Mina Markham shares why and how [Slack engineers re-built the Slack website with CSS Grid](https://slack.engineering/rebuilding-slack-com-b124c405c193). The positive effect: leaner, cleaner code with more predictable CSS specificity and drastically improved performance.

<figure><a href="https://slack.engineering/rebuilding-slack-com-b124c405c193"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/284ebe4d-dde0-4eb9-b6f7-05c4e70bef00/slack-grid-opt.png" width="800" height="554" alt="Slack Grid" /></a><figcaption>The Slack engineering team lets us sneak a peek <a href="https://slack.engineering/rebuilding-slack-com-b124c405c193">behind the scenes of their recent CSS Grid powered website redesign</a>. (<a href="https://slack.engineering/rebuilding-slack-com-b124c405c193">Image credit</a>)</figcaption></figure>

## JavaScript

*   Eric Bidelman shares how we can [use an `IntersectionObserver` to control or react to `position: sticky` changes](https://developers.google.com/web/updates/2017/09/sticky-headers). This replaces the need for `scroll` events, offering a much better performance.
*   [The Intl.PluralRules API](https://developers.google.com/web/updates/2017/10/intl-pluralrules) is an extension to the Internationalization API that will soon be available in Firefox 58 and Chrome 63\. It solves a quite tricky issue with plurals in internationalized contexts.</p>

## Accessibility

*   Heydon Pickering added a new reference article to the Inclusive Components blog that explains [how we can build tabbed interfaces in an inclusive, accessible way](https://inclusive-components.design/tabbed-interfaces/).
*   Manuel Matuzovic wrote about how you should [write CSS with accessibility in mind](https://medium.com/@matuzo/writing-css-with-accessibility-in-mind-8514a0007939) and what to avoid.
*   Ian Devlin shares [how they handle accessibility at Trivago](https://tech.trivago.com/2017/09/26/accessibility-at-trivago/). An interesting read, especially because they explain the internal challenges, how to increase awareness for accessibility, and what they did, do and try to achieve in the future.

<figure><a href="https://inclusive-components.design/tabbed-interfaces/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f3eb6a-8db9-41db-9fb3-4ff59f297286/tabbed-interfaces-opt.png" width="800" height="450" alt="Accessible tabbed interfaces" /></a><figcaption>Heydon Pickering explains <a href="https://inclusive-components.design/tabbed-interfaces/">how to make tabbed interfaces accessible</a>. (<a href="https://inclusive-components.design/tabbed-interfaces/">Image credit</a>)</figcaption></figure>

## Security

*   The University of Cambridge shares why [they can’t issue TLS certificates anymore for their internal network domain](https://news.uis.cam.ac.uk/articles/2017/09/20/unable-to-issue-tls-certs-for-names-in-private-cam-ac-uk) `private.cam.ac.uk` due to the now required CAA check. In short: As the hostname cannot be checked by the certificate authority, it declines to issue a certificate. The drawback of the otherwise quite useful mandatory CAA checks.
*   With PHP7.2 coming in November, the Libsodium extension will be available in PHP. This means we’ll finally have a relatively easy way to use the Argon2 algorithm for hashing user passwords. [Here’s how you can do it](https://framework.zend.com/blog/2017-08-17-php72-argon2-hash-password.html).
*   If you sent a S/MIME encrypted message via Microsoft Outlook in the past six months, [it’s quite likely that nothing of the email was actually encrypted](https://www.sec-consult.com/en/blog/2017/10/fake-crypto-microsoft-outlook-smime-cleartext-disclosure-cve-2017-11776/index.html). The latest software update from this week fixes the issue (v1705+).
*   Carl Chenet explores [why communicating over Slack can be problematic](https://carlchenet.com/the-slack-threat/) as nothing of what we write in the app is encrypted. So better never share any business secrets or credentials via Slack.</p>

## Privacy

*   Judith Duportail asked the dating platform Tinder for her data and [got back more than 800 pages filled with very personal details](https://www.theguardian.com/technology/2017/sep/26/tinder-personal-data-dating-app-messages-hacked-sold) and a lot more than she’d remembered. Tinder, of course, is just an example here — the same is probably true for most apps on your phone.
*   Detectify cares about privacy. That’s why [they built a Chrome extension to show how easy it is to stalk your Facebook friends](https://labs.detectify.com/2017/09/26/trackmania-a-chrome-plugin-to-stalk-your-friends/) when using Tinder. The privacy leaks here allow users to identify another user’s location and more.</p>

## Work & Life

*   Ivan Mir shares [how he optimized his work routine](https://qotoqot.com/blog/improving-focus/) to become more productive without working more hours.
*   Jonathan Golden from Airbnb shares [what they learned from scaling Airbnb](https://medium.com/@jgolden/lessons-learned-scaling-airbnb-100x-b862364fb3a7). A good article about company management, setting goals and optimizing work.

<figure><a href="https://qotoqot.com/blog/improving-focus/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a081e9b-04e5-4fd6-82a8-61dd9ea1316a/improving-focus-opt.png" width="800" height="374" alt="Improving Focus" /></a><figcaption>Get more out of your work week without working more hours. <a href="https://qotoqot.com/blog/improving-focus/">Ivan Mir shares how he did it</a>. (<a href="https://qotoqot.com/blog/improving-focus/">Image credit</a>)</figcaption></figure>

## Going Beyond…

*   More and more people working at Google, Twitter, Facebook and other tech giants disconnect themselves from smartphones. By radically limiting the feature set to a normal wireless phone, they want to gain back control over their lives. Paul Lewis spoke to some people and researched why tech insiders who actually build the apps and operating systems for smartphones and other smart devices [fear a smartphone dystopia](https://www.theguardian.com/technology/2017/oct/05/smartphone-addiction-silicon-valley-dystopia). A good read on mental health issues.
*   Here are [10 hours of ambient arctic sounds to help you relax, meditate, or study](https://www.openculture.com/2017/03/10-hours-of-ambient-arctic-sounds-will-help-you-relax-meditate-study-sleep.html).
*   Julian Oliver shares [how he used wind energy to mine cryptocurrency and fund climate research](https://julianoliver.com/output/harvest).
*   Jens Oliver Meiert emailed the companies that are responsible for 71% of all greenhouse gas emissions. [Here’s what they replied](https://meiert.com/en/blog/email-all-the-companies/), but the most important point about this experiment is what the author concludes:

> “Perhaps I didn’t get to email the people who’re truly responsible here; and what they do with my requests, I don’t know, either.  
> But the point is that reaching out is one of the few options we have at our disposal; and if even one small thing changes and improves, it may be a success. And as such I believe more people should reach out. Instead of waiting for politicians or law enforcement to act, let’s act ourselves, let’s make ourselves heard. Constructive action always helps.”

_We hope you enjoyed this Web Development Update. The next one is scheduled for November 17th. Stay tuned!_


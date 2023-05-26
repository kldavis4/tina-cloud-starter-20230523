---
title: 'Web Development Reading List #108'
slug: web-development-reading-list-108
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3e0ad02-e9ef-4482-89e8-8bc1ff12e62e/ios-gui-templates.png
date: 2015-10-16T17:55:25.000Z
author: anselm-hannemann
description: >-
  _**What's happening in the industry?** What important techniques have emerged
  recently? What about new case studies, insights, techniques and tools? Our
  dear friend [Anselm Hannemann](/author/anselm-hannemann/?rel=author) is
  keeping track of everything in the [web development reading
  list](https://wdrl.info/) so you don't have to. The result is a carefully
  collected list of articles that popped up over the last week and which might
  interest you. — Ed._

  Last week I asked for some comments on how web development got more complex in
  my opinion and [I got great
  feedback](/2015/10/web-development-reading-list-107/#comments). It’s great to
  see a good discussion as the outcome, and I say “thank you” for all your
  support!
categories:
  - Web Development Reading List
---
Last week I asked for some comments on how web development got more complex in my opinion and <a href="https://www.smashingmagazine.com/2015/10/web-development-reading-list-107/#comments">I got great feedback</a>. It’s great to see a good discussion as the outcome, and I say “thank you” for all your support – whether financially or some kind words you sent me via email. Have a great weekend y’all!

## <span class="rh">Further Reading</span> on SmashingMag:

*   <span>[MUD: Minimum Usable Design](https://www.smashingmagazine.com/2012/05/mud-minimum-usable-design/)</span>
*   <span>[Providing The Best Mobile User Experience Possible](https://www.smashingmagazine.com/2013/05/providing-the-best-mobile-user-experience-possible/)</span>
*   <span>[Streamlining Mobile Interactions](https://www.smashingmagazine.com/2014/05/streamline-mobile-interactions/)</span>

## News

*   Here’s bad news. Again, a very bad [Flash security vulnerability has been found](https://bgr.com/2015/10/15/adobe-flash-player-security-vulnerability-warning/), and there’s no fix on the way yet — apart from **uninstalling Flash**. If you can’t do that, please use click-to-play and be very careful. You might also want to tell your friends about this problem. Let’s hope Adobe will supply a fix soon.</p>

## General

*   Cody Lindley’s massive efforts resulted in a great resource for folks who are new to our industry: [The Front-end Handbook](https://frontendmasters.gitbooks.io/front-end-handbook/content/index.html) is an open and free book about how to get started in the web industry. It not only shares the basic technological aspects but also business and social advice.</p>

## Concepts & Design

*   The founders of Teehan+Lax, now at Facebook, shared a massive [set of iOS9 GUI templates](https://facebook.github.io/design/ios9.html) which you can use for free with Photoshop or Sketch (only for mock-ups though, according to the license).

{{% feature-panel %}}

<figure class="fwi"><a href="https://facebook.github.io/design/ios9.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3e0ad02-e9ef-4482-89e8-8bc1ff12e62e/ios-gui-templates.png" alt="iOS GUI Templates" width="500" height="276" /></a><figcaption>A massive set of iOS9 UI templates for Photoshop and Sketch.</figcaption></figure>

## Tools

*   Jack Franklin started reflecting on the state of front-end tooling after a conference attendee asked him why he uses all those tools in his stack. Interesting thoughts with some very good advice on using what we feel comfortable with.
*   I often stumble across browser extensions that are very cool. However, a lot of them are Chrome-only, so as a Firefox user I often get neglected. Luckily, **Firefox changed its extension ecosystem to use WebExtensions**, which makes it super easy to convert a Chrome to a Firefox extension.</p>

## Security

*   If you’re building an application with node.js you may want to read [the node.js security checklist](https://blog.risingstack.com/node-js-security-checklist/) that helps you circumvent lot of security pitfalls.</p>

## Privacy

*   A recent report explains [how the NSA breaks our crypto](https://freedom-to-tinker.com/blog/haldermanheninger/how-is-nsa-breaking-so-much-crypto/). It even seems that they break Diffie-Hellman primes, meaning that **HTTPS/VPN wouldn’t be secure anymore**.</p>

## Web Performance

*   Jeremy Keith is always good for a well-thought-out article on ideas that spread on the internet. This time, he [criticizes Google’s new AMP project](https://adactio.com/journal/9646) that, [for a lot of people](https://groups.google.com/forum/#!msg/amphtml-discuss/TxoKtSXK148/xNoagN6DAgAJ), [leads to more questions](https://andydavies.me/blog/2015/10/13/accelerated-mobile-pages-ive-more-questions-than-answers/) [than it answers](https://www.niemanlab.org/2015/10/get-ampd-heres-what-publishers-need-to-know-about-googles-new-plan-to-speed-up-your-website/).
*   How to enable HTTP/2 in Apache? With Apache httpd 2.4.17, HTTP/2 is finally supported and [here we have a guide on how to set it up and configure it](https://icing.github.io/mod_h2/howto.html) for usage on your server. Let’s hope this version will get deployed on servers worldwide as soon as possible.
*   _imgix_, a well-known real-time image processing service, implemented client hints now and explains how they did so in a short, informative article. Although only Chrome currently supports this, it will be a technique you should keep in mind for big performance improvements.</p>

## HTML / SVG

*   Bram Stein started writing a series of articles, the so-called [Web Font Anti-Patterns](https://bramstein.com/writing/web-font-anti-patterns.html). Starting with [overusing web fonts](https://bramstein.com/writing/web-font-anti-patterns-overusing.html), [inlining fonts](https://bramstein.com/writing/web-font-anti-patterns-inlining.html), and [using too aggressive subsettings](https://bramstein.com/writing/web-font-anti-patterns-subsetting.html), he will continue the series with even more useful information on web fonts.</p>

## CSS / Sass

*   Making so-called “diamond grids” was always a big effort. But using Sass to calculate it, makes things a lot easier. Chen Hui Jing explains in her blog post [how you can create a diamond grid with SCSS](https://www.chenhuijing.com/blog/diamond-grid-using-sass/).</p>

## Work & Life

*   The worst situation as a developer is [when you’re constantly interrupted during your work](https://thetomorrowlab.com/2015/01/why-developers-hate-being-interrupted/). It massively affects productivity and code quality and should be avoided by company managers at all cost.
*   Companies often struggle with the communication with their employees. To avoid conflicts, Zach Holman shares [a way to let people in the company opt-in to business details](https://zachholman.com/posts/opt-in-transparency/). An idea to put an end to the “why do we have to build this crap?” question.
*   While the article “The Elephant in the Room” is a bit biased, it shows how difficult it is to make money with apps. It takes the example of Marco Arment’s most recent move to offer his podcast app on a donation-basis and compares it to developers who need to make a living from apps and struggle to charge for updates.</p>

## Go beyond…

*   We can’t look into someone else’s mind. And sometimes this bothers us. We struggle with ourselves, thinking of impostor syndrome and comparing ourselves to the cool people on social media. However, these people are often not that different from us. [Nobody Knows What The Hell They Are Doing](https://99u.stfi.re/articles/32985/nobody-knows-what-the-hell-they-are-doing) reveals that we’re all in the same boat.
*   This week, Tesla pushed a new software update to its cars, enabling them to drive on autopilot. This is the [first car in public that can do this](https://www.wired.com/2015/10/tesla-self-driving-over-air-update-live/?mbid=social_twitter) and it seems to work great. I’m curious how it will work out for them and moreover what the impact on the industry will be.

And with that I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via E-Mail, RSS and online.

Thanks and all the best,
Anselm


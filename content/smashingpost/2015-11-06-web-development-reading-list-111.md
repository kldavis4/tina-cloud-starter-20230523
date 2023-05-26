---
title: >-
  Web Development Reading List #111: Preconnect, Dynamic Responsive Images, DOM
  Event Listeners
slug: web-development-reading-list-111
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57d635e5-3df5-497a-9a42-d5e8ddce1ce7/ava.png'
date: 2015-11-06T19:27:19.000Z
author: anselm-hannemann
description: >-
  _**What’s going on in the industry?** What new techniques have emerged
  recently? What insights, tools, tips and tricks is the web design community
  talking about? [Anselm Hannemann](/author/anselm-hannemann/?rel=author) is
  collecting everything that popped up over the last week in his [web
  development reading list](https://wdrl.info/) so that you don’t miss out on
  anything. The result is a carefully curated list of articles and resources
  that are worth taking a closer look at. — Ed._

  Each week when reviewing links I’m grateful that so many people write such
  great articles. Useful technical articles that help you resolve front-end
  issues, inspirational articles that motivate you to enjoy work again, and sort
  of "social" articles that reveal that there are still start-ups out there that
  do their best to be meaningful, and not just seeking an exit strategy to sell
  out. I’d love more people in the world think like that, embrace their
  employees’ work time, try to **force workaholics to stop working**, and build
  health monitors in the team.
categories:
  - Web Development Reading List
---
<em><strong>What’s going on in the industry?</strong> What new techniques have emerged recently? What insights, tools, tips and tricks is the web design community talking about? <a href="/author/anselm-hannemann/?rel=author">Anselm Hannemann</a> is collecting everything that popped up over the last week in his <a href="https://wdrl.info/">web development reading list</a> so that you don’t miss out on anything. The result is a carefully curated list of articles and resources that are worth taking a closer look at. — Ed.</em>

Each week when reviewing links I’m grateful that so many people write such great articles. Useful technical articles that help you resolve front-end issues, inspirational articles that motivate you to enjoy work again, and sort of "social" articles that reveal that there are still start-ups out there that do their best to be meaningful, and not just seeking an exit strategy to sell out. I’d love more people in the world think like that, embrace their employees’ work time, try to <strong>force workaholics to stop working</strong>, and build health monitors in the team.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [Responsive Web Design Techniques, Tools and Strategies](https://www.smashingmagazine.com/2011/07/responsive-web-design-techniques-tools-and-design-strategies/)
*   [The State Of Responsive Web Design](https://www.smashingmagazine.com/2013/05/the-state-of-responsive-web-design/)
*   [Design Process In The Responsive Age](https://www.smashingmagazine.com/2012/05/design-process-responsive-age/)

## News

*   Only a few weeks after Node.js 4 was released, [Node.js v5 has followed](https://nodejs.org/en/blog/release/v5.0.0/). You can grab it now, but don’t worry – version 4 will still be supported and updated for a quite long time as it’s a _long-term release_. You can also [read about the new version releases and what’s important](https://nodejs.org/en/blog/community/node-v5/).
*   Latest Chrome and [Opera 33](https://dev.opera.com/blog/opera-33/) now support `<link rel=preconnect>` as well as extended sandboxed iframe options, `history.scrollRestoration`, [CSS intrinsic sizing](https://drafts.csswg.org/css-sizing-3/), Client Hints, and <abbr title="HTTP Public Key Pinning">HKPK</abbr> support.
*   [Firefox has released v42](https://www.mozilla.org/en-US/firefox/42.0/releasenotes/). It includes the new, more bullet-proof tracking protection in private windows, extended security and privacy settings, mute audio tabs instantly, and WiFi debugging in DevTools.</p>

## Concepts & Design

*   The Awesome collections got a new member: [Awesome Stock Resources](https://github.com/neutraltone/awesome-stock-resources) with a comprehensive overview of freely available stock photos and videos.

{{% feature-panel %}}

<figure class="fwi"><a href="/wp-content/uploads/2015/11/ava-large.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57d635e5-3df5-497a-9a42-d5e8ddce1ce7/ava.png" alt="AVA test runner" width="500" height="274" /></a></figure>

## Tools

*   For me personally this is a very annoying thing: deprecated, abandoned branches in git repositories. A [how to mass-delete local and remote branches](https://stackoverflow.com/questions/2003505/delete-a-git-branch-both-locally-and-remotely/23961231) is a good round-up of solutions to this problem, and just a good reminder to keep things clean and focused.
*   The new [AVA test runner](https://github.com/sindresorhus/ava) finally enables us to run tests much faster as it uses concurrency. You might want to check it out for your next project.
*   With iOS 9 Apple has introduced a new kind of WebView. A hint: with an iOS app you can [test all available WebViews on iOS](https://itunes.apple.com/us/app/webview-wkwebview-uiwebview/id928647773?mt=8) easily.</p>

## Security

*   [Snyk](https://snyk.io/) finds and fixes known vulnerabilities in your Node.js dependencies. Also check out [nsp](https://github.com/nodesecurity/nsp) which also can help you find vulnerabilities in your node.js applications.</p>

## Web Performance

*   Dean Hume describes [how to create dynamic reponsive images with WebP or JPEGXR images using Service Workers](https://deanhume.com/Home/BlogPost/service-workers--dynamic-responsive-images-using-webp-images/10132/).</p>

## JavaScript

*   Learn how to [create and remove DOM Event Listeners the proper way](https://www.webreflection.co.uk/blog/2015/10/22/how-to-add-dom-events-listeners).
*   You can use [Segment](https://lmgonzalves.github.io/segment/) to animate your SVG path strokes easily. It’s a tiny library, so if you need only this functionality, consider using it instead of big libraries like GSAP.
*   Ditch jQuery or use the upcoming release of jQuery 3? This question might keep you busy for a while. But [jQuery is still relevant and you need to understand what jQuery is good for](https://developer.telerik.com/featured/jquerys-relevancy-there-and-back-again/). It’s not just a DOM wrapper.
*   The Pointer Events Polyfill is now [available in version 0.4.0](https://blog.jquery.com/2015/11/05/pep-0-4-0/) which improves support for Webpack, Browserify and many small fixes.</p>

## Work & Life

*   “[Workaholics aren't heroes.](https://madebysidecar.com/journal/standards-work-to-live) They don't save the day, as they just use it up. The real hero is somebody who leaves work at work and comes home earlier because she figured out a faster way.” On how we all should put more focus on our work and get more spare time.
*   Kickstarter’s Yancey Strickler speaks about the recent move of the company to become a public benefit corporation. He talks about venture capital, the poisonous urge to profit maximisation, idealism and [how important it is for a company and people to not out-sell its values](https://www.theguardian.com/technology/2015/nov/03/kickstarter-chooses-public-good-over-private-riches).
*   Atlassian shares thoughts on [establishing a health monitor in your project team](https://www.atlassian.com/inside-atlassian/project-team-health-monitor).

## Go beyond…

*   Make Me Uncomfortable: [The Discomfort Zone](https://medium.com/@verbagetruck/discomfort-zone-talking-diversity-at-epicurrence-ba77fda4a784) at Epicurrence was a new and interesting experience for Jessica Collier, she says.
*   One of the founders of Basecamp reflects on whether we should aim for owning the universe [or rather focus on the one thing we want to actually solve](https://signalvnoise.com/posts/3972-reconsider). Because a lot of start-ups nowadays hardly focus on really making something better.

And with that I’ll close for this week. Please feel free to <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via E-Mail, RSS and online.

<em>Thanks and all the best,
Anselm</em>

&nbsp;


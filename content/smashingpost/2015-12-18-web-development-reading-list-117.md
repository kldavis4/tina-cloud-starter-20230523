---
title: >-
  Web Development Reading List #117: Storytelling, Security in Devtools and
  350ms Tap Delay
slug: web-development-reading-list-117
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18cdf54d-bb10-42b9-afdb-df52df36a4d0/storytellingmap.jpg
date: 2015-12-18T18:01:17.000Z
author: anselm-hannemann
description: >-
  _**What’s going on in the industry?** What new techniques have emerged
  recently? What insights, tools, tips and tricks is the web design community
  talking about? [Anselm Hannemann](/author/anselm-hannemann/?rel=author) is
  collecting everything that popped up over the last week in his [web
  development reading list](https://wdrl.info/) so that you don’t miss out on
  anything. The result is a carefully curated list of articles and resources
  that are worth taking a closer look at. — Ed._

  The end of the year is near and some people are enjoying their well-deserved
  holidays already. For others, the pressure increases when managers or clients
  want to finish a project before Christmas. And then, the Christmas and New
  Year celebrations — so many things to prepare, to buy, to think of. I hope you
  either belong to the ones who can enjoy their vacation already or that you can
  stay calm while having a stressful time. Try to take your time with friends
  and beloved ones and enjoy some moments of silence.
categories:
  - Web Development Reading List
---
<em><strong>What’s going on in the industry?</strong> What new techniques have emerged recently? What insights, tools, tips and tricks is the web design community talking about? <a href="/author/anselm-hannemann/?rel=author">Anselm Hannemann</a> is collecting everything that popped up over the last week in his <a href="https://wdrl.info/">web development reading list</a> so that you don’t miss out on anything. The result is a carefully curated list of articles and resources that are worth taking a closer look at. — Ed.</em>

The end of the year is near and some people are enjoying their well-deserved holidays already. For others, the pressure increases when managers or clients want to finish a project before Christmas. And then, the Christmas and New Year celebrations — so many things to prepare, to buy, to think of. I hope you either belong to the ones who can enjoy their vacation already or that you can stay calm while having a stressful time. Try to take your time with friends and beloved ones and enjoy some moments of silence.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Better User Experience With Storytelling](https://www.smashingmagazine.com/2010/01/better-user-experience-using-storytelling-part-one/)
*   [A Closer Look At Personas](https://www.smashingmagazine.com/2014/08/a-closer-look-at-personas-part-1/)
*   [How To Sell Your UX Design Solution To Clients](https://www.smashingmagazine.com/2013/02/sell-design-solution-clients/)
*   [Stop Redesigning And Start Tuning Your Site Instead](https://www.smashingmagazine.com/2012/05/stop-redesigning-start-tuning-your-site/)

## News

*   [Firefox 43 is out](https://developer.mozilla.org/en-US/Firefox/Releases/43) and brings us a couple of new features: CSS [`hypens`](https://developer.mozilla.org/en-US/docs/Web/CSS/hyphens) are supported now, [Screen Orientation API](https://developer.mozilla.org/en-US/docs/Web/API/Screen/orientation), [Subresource integrity](https://w3c.github.io/webappsec/specs/subresourceintegrity/) has been implemented for `<script>`, `<link>` elements. Finally, the Privacy Protection Mode can be modified in settings and I’ve written a short article about [how this helps you to find interesting issues with your website](https://helloanselm.com/2015/see-the-progress/).
*   As the majority of mobile websites disable zoom, leaving users without choice to get a bigger font-size or zoom into images, [Opera for Android now force enables zoom on every site](https://www.opera.com/blogs/mobile/2015/12/force-enable-zoom-opera-34-for-android/).</p>

## Tools

*   Most of us use github. But what happens if the service goes down or unresponsive? Chris Ball thought about that and tries to create an alternative approach [baking git and the torrent protocol together](https://blog.printf.net/articles/2015/05/29/announcing-gittorrent-a-decentralized-github/).</p>

## Security

*   [Chrome’s developer tools now have a security tab](https://developers.google.com/web/updates/2015/12/security-panel). This gives you an overview on the HTTP(S) status of the page, secure resources, and mixed content.</p>

## Privacy

*   This week I read that [web analytics services are about to track emotions](https://thenextweb.com/insider/2015/12/14/web-analytics-are-about-to-get-seriously-next-level-with-emotion-tracking/). And indeed it’s relatively easy to detect if a smartphone has been thrown (Device Orientation API), if a user clicks angrily on the screen with the mouse. It just hasn’t been done yet.
*   Ibrahim Altaweel, Nathaniel Good, and Chris Jay Hoofnagle repeated a research from 2012 to see how many trackers the TOP100 websites use. [They found out that dozens of cookies are set on each site to track users](https://techscience.org/a/2015121502/), fingerprinting methods and other techniques are widely used as well. And over 90% of the data is somehow aggregated by Google, leaving it with such an incredible dataset that should scare you.</p>

## Web Performance

*   Until now, WebKit and Safari on iOS have a 350ms delay before single taps activate links or buttons to allow people to zoom into pages with a double tap. Chrome changed this a couple of months ago already by using a smarter algorithm to detect that and now [WebKit will follow with a similar approach](https://webkit.org/blog/5610/more-responsive-tapping-on-ios/). The article gives some great insights how browsers work with touch gestures and how browsers can still get so much smarter than they are today.
*   With his last part, Denys Mishunov gives us some great techniques to [cover up unavoidable waiting times on websites](https://www.smashingmagazine.com/2015/12/performance-matters-part-3-tolerance-management/) to make it a convenient experience for the users.

{{% feature-panel %}}

<figure class="fwi"><a href="https://tympanus.net/codrops/2015/12/16/animated-map-path-for-interactive-storytelling/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18cdf54d-bb10-42b9-afdb-df52df36a4d0/storytellingmap.jpg" alt="An interactive storytelling map using SVG" width="500" height="272" /></a><figcaption>An interactive storytelling map using SVG and Canvas.</figcaption></figure>

## HTML / SVG

*   Lucas Bebber created a beautiful experiment [using SVG and Canvas to create an interactive storytelling map](https://tympanus.net/codrops/2015/12/16/animated-map-path-for-interactive-storytelling/). Although the code does not work in every browser, I love the concept to illustrate a journey in a travel diary.
*   With SVG, you can achieve [partial blur and iOS style translucency](https://w3.eleqtriq.com/2015/11/svg-partial-blur/). All done with CSS filters and some little tricks.
*   Filling out forms on Mobile is a pain simply because most websites don't use appropriate HTML and therefore don’t help the user avoiding errors. Christian Holst explains [what you should do for what type of form fields to enhance the user experience](https://baymard.com/blog/mobile-touch-keyboards).</p>

## Accessibility

*   [Rodey Rehm has published](https://www.smashingmagazine.com/2015/12/making-accessibility-simpler/) a new open source library to enhance your website’s accessibility: [ally.js](https://allyjs.io/). It took him months to build this — now he tells you how to properly handle a modal’s focus behavior.
*   Given that most people don’t know how to improve accessibility on their site or application, here are some important [basics that are extremely easy to implement](https://www.marcozehe.de/2015/12/14/the-web-accessibility-basics/). Next time you build something, consider incorporating those few thingies.

## JavaScript

*   Remy Sharp runs JSBin, a platform for collaborative JavaScript debugging which is being used by millions of users. Running tests is pretty crucial for this mostly one-man show project. You can now [read about his Node.js test strategy](https://remysharp.com/2015/12/14/my-node-test-strategy) on his blog.
*   Instead of using a random jQuery plugin for putting a search field on your site, use this tutorial to build a [responsive progressive accessible vanilla search](https://adrianroselli.com/2015/12/responsive-progressive-accessible-vanilla-search.html).</p>

## Work & Life

*   It’s anything but easy to organize an event. Compared to what we can read about web development, there are only few resources that explain what it means to run an event. [Marc Thiele now wrote up a few things](https://beyondtellerrand.com/blog/an-events-lifecycle) that happen in the background of his events.
*   Most of us haven’t quite realized there is something extraordinary happening. [The world is changing and it’s only the start](https://medium.com/the-global-future-of-work/there-is-something-extraordinary-happening-10492495c715#.h2gznsihu). Our society is moving away from normal employment and classic entrepreneurship models, and there are many more things that change slowly but steadily.</p>

## Go beyond…

*   Peter Sunde, the founder of pirate bay, [has published a few things to think about](https://motherboard.vice.com/read/pirate-bay-founder-peter-sunde-i-have-given-up). I disagree with a lot of things in the article and really hope that we figure out better ways than letting a country “crash” to make things better, but he definitely has also some points when he says that we keep breaking the internet. I’m optimistic and hope that we together can fix this.

And with that, I’ll close for this week. In case you like what I write, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via E-Mail, RSS and online.

Thanks and all the best,
Anselm


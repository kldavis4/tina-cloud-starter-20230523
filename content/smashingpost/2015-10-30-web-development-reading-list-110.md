---
title: >-
  Web Development Reading List #110: Jekyll, libSass, 2G Tuesdays and Service
  Workers
slug: web-development-reading-list-110
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15bb5653-5a31-4ac0-85fc-c946795f10bd/jekyll-opt.png'
date: 2015-10-30T12:38:49.000Z
author: anselm-hannemann
description: >-
  _**What’s going on in the industry?** What new techniques have emerged
  recently? What insights, tools, tips and tricks is the web design community
  talking about? [Anselm Hannemann](/author/anselm-hannemann/?rel=author) is
  collecting everything that popped up over the last week in his [web
  development reading list](https://wdrl.info/) so that you don’t miss out on
  anything. The result is a carefully curated list of articles and resources
  that are worth taking a closer look at. — Ed._

  My friend [Tobias](https://tobiastom.name/) told me of an interesting approach
  a few weeks ago. If you work on a big project with a team, just force all
  developers to delete the project before they leave on Friday, and have them
  reinstall and set it up every Monday morning (or every other week). This way,
  you’ll ensure that the process of onboarding people and the whole project’s
  setup is as simple as possible. And you will love it if the server crashes and
  you can set up the whole thing again within a couple of minutes. Now, enjoy
  this list and have a great weekend!
categories:
  - Web Development Reading List
---
<em><strong>What’s going on in the industry?</strong> What new techniques have emerged recently? What insights, tools, tips and tricks is the web design community talking about? <a href="/author/anselm-hannemann/?rel=author">Anselm Hannemann</a> is collecting everything that popped up over the last week in his <a href="https://wdrl.info/">web development reading list</a> so that you don’t miss out on anything. The result is a carefully curated list of articles and resources that are worth taking a closer look at. — Ed.</em>

My friend <a href="https://tobiastom.name/">Tobias</a> told me of an interesting approach a few weeks ago. If you work on a big project with a team, just force all developers to delete the project before they leave on Friday, and have them <strong>reinstall and set it up every Monday morning</strong> (or every other week).</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Inspiring Everyday Graphic Design</span>](https://www.smashingmagazine.com/2016/03/inspiring-graphic-design/)
*   [33 Tempting E-Commerce Icons For Free](https://www.smashingmagazine.com/2013/09/freebie-e-commerce-icons-33-png-ps-ai/)
*   [Breaking Out Of The Box: Design Inspiration](https://www.smashingmagazine.com/2016/08/breaking-out-of-the-box-design-inspiration-august-2016/)
*   [Modern Art Movements To Inspire Your Logo Design](https://www.smashingmagazine.com/2010/01/12-modern-art-movements-to-inspire-your-logo-design/)

This way, you’ll ensure that the process of onboarding people and the whole project’s setup is as simple as possible. And you will love it if the server crashes and you can set up the whole thing again within a couple of minutes. Now, enjoy this list and have a great weekend!

{{% feature-panel %}}

## News

<figure><a href="https://jekyllrb.com/news/2015/10/26/jekyll-3-0-released/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15bb5653-5a31-4ac0-85fc-c946795f10bd/jekyll-opt.png" alt="Jekyll 3.0" width="500" height="387" /></a><figcaption><a href="https://jekyllrb.com/news/2015/10/26/jekyll-3-0-released/">Jekyll 3</a> is out. It has big performance improvements, especially due to its new incremental builds.</figcaption></figure>

*   Firefox will be [removing `Element.mozMatchesSelector` very soon](https://www.fxsitecompat.com/en-US/docs/2015/element-mozmatchesselector-will-be-removed/), in favor of the new standard `Element.matches` method. Prepare your code to be ready for that.
*   [Jekyll 3](https://jekyllrb.com/news/2015/10/26/jekyll-3-0-released/) is out. It has big performance improvements, especially due to its new incremental builds. If you use Jekyll already, test the new version and use it — the update is mostly seamless (just some configuration changes).
*   This week has been pretty bad for the Internet. In Europe, the very controversial [Net neutrality law was passed, leaving many loopholes open](https://www.theguardian.com/technology/2015/oct/27/eu-net-neutrality-laws-fatally-undermined-by-loopholes-critics-say) for certain corporations. In fact, it’s worse than before. And in the US, [CISA was passed](https://www.eff.org/deeplinks/2015/10/eff-disappointed-cisa-passes-senate), [too](https://www.theguardian.com/world/2015/oct/27/cisa-cybersecurity-bill-senate-vote).
*   [libSass 3.3](https://github.com/sass/libsass/releases/tag/3.3.0) is out, bringing us more tests, better performance, shadow DOM support, [all Sass 3.4 selector functions](https://sass-lang.com/documentation/file.SASS_CHANGELOG.html#selector_functions), and improvements to `url()`.</p>

## General

*   [Here is James Williams](https://blog.practicalethics.ox.ac.uk/2015/10/why-its-ok-to-block-ads/) with his highly ethical thoughts on the topic of ad-blocking:

    > What I find remarkable is the way both sides of this debate seem to simply assume the large-scale capture and exploitation of human attention to be ethical and/or inevitable in the first place. This demonstrates how utterly we have all failed to understand the role of attention in the digital age — as well as the implications of spending most of our lives in an environment designed to compete for it.</p>

## Concepts And Design

<figure><a href="https://medium.com/@mwichary/system-shock-6b1dc6d6596f"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f08216e-cd3f-4649-9744-e58b4ab71184/medium-fonts-opt.png" alt="Medium Fonts" /></a><figcaption>The new version of Medium (2.0) <a href="https://medium.com/@mwichary/system-shock-6b1dc6d6596f">uses system fonts when available</a>.</figcaption></figure>

*   The new version of Medium (2.0) [uses system fonts when available](https://medium.com/@mwichary/system-shock-6b1dc6d6596f). That means, if you’re on a Mac, you’ll get the San Francisco font. That’s cool not only because it’s a nice font but also because Apple decided not to make it available under its real name in CSS, so you’ll need to use the workaround. This way, you’ll get a seamless experience between the OS and the website.</p>

## Tools

*   Remy Sharp tells us how he [got Travis CI to work with npm’s new private modules](https://remysharp.com/2015/10/26/using-travis-with-private-npm-deps). Of course, you can get any other continuous integration service to work with that method in a similar way, too.</p>

## Security

*   MITM attacks are a problem not only for websites. [Intercepting emails that way](https://conferences2.sigcomm.org/imc/2015/papers/p27.pdf) is very common, too. The IETF is trying to do something about the problem now by enforcing [DANE and TLS](https://datatracker.ietf.org/doc/rfc7672/) for mailserver connections.</p>

## Web Performance

*   [Brotli compression](https://github.com/google/brotli) is the hot new topic in web performance. But we need to set theoretical performance wins in context. [Cloudflare has tested it under real conditions](https://blog.cloudflare.com/results-experimenting-brotli/) and found that it will be a big win for large, static files but not ideal for small, dynamic content blocks. Configure and use it wisely, or else just stick with Gzip.
*   Facebook started [2G/EDGE Tuesdays](https://uk.businessinsider.com/facebook-2g-tuesdays-to-slow-employee-internet-speeds-down-2015-10), so that its employees can better relate to their users’ problems. This is a great idea, and we all should do it regularly.</p>

## JavaScript

*   If you work with React, then [Michael Chan’s cheat sheet](https://reactcheatsheet.com/) might come in handy. It’s a searchable website with a short but clear overview of React’s coding methods.
*   [We can use service workers](https://ponyfoo.com/articles/serviceworker-revolution) in our applications today, and they’re a great way to add support via progressive enhancement.
*   [BackstopJS](https://garris.github.io/BackstopJS/) allows us to test for CSS regressions in a simple way. It uses Resemble, Casper, and SlimerJS and PhantomJS for reports, whatever you prefer.</p>

## Work And Life

*   This week is Geek Mental Health Week, and Alexander Charchar reflects on how we can [detect and deal with silent burnout](https://www.smashingmagazine.com/2015/10/dealing-with-loud-silent-burnout/). Take care of yourself, and be selfish with your workload.
*   We read everywhere that having rituals is a good thing. The gist of it is this: [Have rituals — embrace them](https://www.bakadesuyo.com/2015/10/ritual/), and remember that the best rituals come not from celebrities, but from your heart.
*   [Life is full of ups and downs](https://the-pastry-box-project.net/marcy-sutton/2015-october-26), and you can often draw those ups and downs as an oscillating line. If you accept this and think of it as riding big waves on an ocean, you can deal better with those down times. And then, you can break your routine, escape the wave and do something else to fight the down.

And with that, I’ll close for the week. In case you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project</a> on the WDRL website. The list is available via email, RSS and the web.

<em>Thanks and all the best,
Anselm</em>

{{< signature "al" >}}


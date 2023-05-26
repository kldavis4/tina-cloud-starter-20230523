---
title: >-
  Web Development Reading List #145: Font Loading Strategies, Scaling SVGs And
  Infinite Scrolling Done Right
slug: web-development-reading-list-145
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87fd5569-8d3e-4377-9372-22166c57b54b/ipfs-screenshot-opt.png
date: 2016-07-15T18:49:47.000Z
author: anselm-hannemann
description: >-
  I love articles that specifically focus on tiny little details within web
  development. For example, this week I stumbled upon an article featuring all
  the fine details about scheduling in `requestAnimationFrame`. Another gem I
  discovered is a widely unknown but very practical SVG attribute to preserve
  stroke widths while scaling an illustration.

  All of these little details can make such a huge difference in our projects,
  so I’m particularly thankful for having discovered these articles to share
  with you this week. Let's dive in.
categories:
  - Web Development Reading List
---
I love articles that specifically focus on tiny little details within web development. For example, this week I stumbled upon an article featuring all the fine details about scheduling in <code>requestAnimationFrame</code>. Another gem I discovered is a widely unknown but very practical SVG attribute to preserve stroke widths while scaling an illustration. All of these little details can make such a huge difference in our projects, so I’m particularly thankful for having discovered these articles to share with you this week. Let's dive in.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Terrible JavaScript Mistakes To Avoid With A Static Code Analyzer](https://www.smashingmagazine.com/2015/02/avoid-javascript-mistakes-with-static-code-analyzer/)
*   [An Introduction To Full-Stack JavaScript](https://www.smashingmagazine.com/2013/11/introduction-to-full-stack-javascript/)
*   [ESLint: The Next-Generation JavaScript Linter](https://www.smashingmagazine.com/2015/09/eslint-the-next-generation-javascript-linter/)
*   [Why Coding Style Matters](https://www.smashingmagazine.com/2012/10/why-coding-style-matters/)

## News

*   The beloved [Git Tower app is coming to Windows](https://www.git-tower.com/p/windows-beta). I’m pretty sure that the pricing will be the same as for the Mac app and it’s great to see that this useful Mac app will soon be available to Windows users as well.</p>

## Generic

*   [A Comprehensive Guide to Font Loading Strategies](https://www.zachleat.com/web/comprehensive-webfonts/) by Zach Leatherman is the current best pocket guide on how to load fonts.</p>

## Tools & Workflows

*   [Mango](https://medium.com/@alexberegszaszi/mango-git-completely-decentralised-7aef8bcbcfe6) is a new tool that uses git as it was thought: in a decentralized, distributed way. They achieve that by baking in [IPFS](https://ipfs.io/) to store git objects. I’m happy this is available now and I’ll be sure to try it with an upcoming project.

{{% feature-panel %}}

<figure><a href="https://ipfs.io/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87fd5569-8d3e-4377-9372-22166c57b54b/ipfs-screenshot-opt.png" alt="Introducing the IPFS Alpha: it includes a fully functioning ipfs node, a unique style command line interface, an importable library, a json api for controlling the node programmatically, a gateway for exposing ipfs to regular web browsers, and a webui for managing your node." width="500" height="367" /></a><figcaption>Introducing the IPFS Alpha: it includes a fully functioning ipfs node, a unique style command line interface, an importable library, a json api for controlling the node programmatically, a gateway for exposing ipfs to regular web browsers, and a webui for managing your node. (<a href="https://ipfs.io/">Image credit</a>)</figcaption></figure>

## HTML & SVG

*   All people say using links and buttons is very easy in web development. The truth is, I don’t think that’s true, especially since the decision makes a huge difference when it comes to accessibility for which the semantic choice can make a huge difference. Marcy Sutton tries to give real-world hints how you can figure out if an element visually looking like a button [should be a button or a link instead](https://marcysutton.com/links-vs-buttons-in-modern-web-applications/).
*   Nick Salloum shares how you can [scale SVG graphics without scaling their borders](https://callmenick.com/post/svg-vector-effects). This is very useful for outline icons which you want to homogeneously display in various sizes altogether. The effect is achieved through the widely unknown `vector-effect` attribute, which for example can have the `non-scaling-stroke` value.

<figure><a href="https://callmenick.com/post/svg-vector-effects"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2e953fa-0087-491a-8a0a-0fbee857ee88/vector-effect-featured-opt.png" alt="Nick Salloum shows us how a SVG attribute can help us scale SVGs without scaling their strokes." width="500" height="203" /></a><figcaption>Nick Salloum shows us how a SVG attribute can help us scale SVGs without scaling their strokes. (<a href="https://codepen.io/callmenick/full/jryOjN/">Check out the demo</a>)</figcaption></figure>

## JavaScript

*   I already shared a couple of Service Worker resources but which one to choose when you want to use it? Likely the best option is to [search for the suitable use-case in the Awesome Service Workers list](https://github.com/TalAter/awesome-service-workers).
*   A lot of projects nowadays have an infinite scrolling implemented. But most of these implementations lack certain details such as DOM recycling or scroll anchoring. The tutorial “[Complexities of an infinite scroller](https://developers.google.com/web/updates/2016/07/infinite-scroller)” shows you how to build this with solid code.
*   Philip Walton shares his approach of setting up [automated, cross-browser JavaScript unit testing with Saucelab](https://philipwalton.com/articles/learning-how-to-set-up-automated-cross-browser-javascript-unit-testing/).
*   Paul Irish shares quite interesting [details on requestAnimationFrame Scheduling](https://medium.com/@paul_irish/requestanimationframe-scheduling-for-nerds-9c57f7438ef4).
*   In [a multi-part story about Web Notifications](https://medium.com/the-guardian-mobile-innovation-lab/web-notifications-introduction-news-on-lock-screens-ba0d685cb4e2#.y60mm017q), developers from The Guardian Mobile Innovation Lab share their experience and findings of implementing notifications into their news site. For each individual step, they explain what you need to do, can do and what can still be improved.

<figure><a href="https://medium.com/the-guardian-mobile-innovation-lab/web-notifications-introduction-news-on-lock-screens-ba0d685cb4e2#.wyd7o6jbz"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11c59d5b-8f76-42db-8e50-04baf7f02dfe/notifications-example-opt.jpg" alt="An Android lock screen at the beginning of our EU referendum experiment." width="500" height="291" /></a><figcaption>An Android lock screen at the beginning of our EU referendum experiment. (<a href="https://medium.com/the-guardian-mobile-innovation-lab/web-notifications-introduction-news-on-lock-screens-ba0d685cb4e2#.wyd7o6jbz">Image credit</a>)</figcaption></figure>

## Work & Life

*   “When you change your location, it’s a lot easier to wash away a lot of bad habits. That’s not to say if you move somewhere, you’ll become a different person, but you have a greater opportunity to make dramatic changes in your identity. […] This process, done over and over, makes you a more robust person. You not only become more adaptable, you gain increasing confidence and self-assurance that who you are is congruent with who you want to be.”—Taylor Pearson in “[Change your location, change your life](https://taylorpearson.me/change-your-location-change-your-life/)”.
*   When you work on a project that is complex, it’s not easy to turn into [a workflow where your team is able to ship small features fast](https://www.smashingmagazine.com/2016/07/how-we-started-releasing-features-twice-as-fast-a-case-study/). Vanja Mimic shares how you can turn a project and deliver much faster.
*   Chen Hui Jing wrote a piece on [Strategies for Healthier Dev](https://www.chenhuijing.com/blog/healthier-dev/). It’s an important article about doing something about your fitness, including strategies for lazy people who don’t like pain and suffering, and things you can do with nearly zero effort.

<em>And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</em>

<em>– Anselm</em>


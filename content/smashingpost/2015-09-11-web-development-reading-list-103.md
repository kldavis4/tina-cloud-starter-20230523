---
title: 'Web Development Reading List #103'
slug: web-development-reading-list-103
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf98069-c7fe-4b00-9a18-4ccbc373c70c/hello-opt.png'
date: 2015-09-11T16:42:20.000Z
author: anselm-hannemann
description: >-
  _**What's happening in the industry?** What important techniques have emerged
  recently? What about new case studies, insights, techniques and tools? Our
  dear friend Anselm Hannemann is keeping track of everything in the [web
  development reading list](https://wdrl.info/), so you don't have to. The
  result is a carefully collected list of articles that popped up over the last
  week and which might interest you. — Ed._

  Hey there! I gathered some useful articles for you again this week. Let me
  inspire you to do something new, improve yourself or just think outside the
  box.
categories:
  - Web Development Reading List
---
<em><strong>What's happening in the industry?</strong> What important techniques have emerged recently? What about new case studies, insights, techniques and tools? Our dear friend Anselm Hannemann is keeping track of everything in the <a href="https://wdrl.info/">web development reading list</a> so you don't have to. The result is a carefully collected list of articles that popped up over the last week and which might interest you. — Ed.</em>

Hey there! I gathered some useful articles for you again this week. Let me inspire you to do something new, improve yourself or just think outside the box.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Lean UX Manifesto: Principle-Driven Design](https://www.smashingmagazine.com/2014/01/lean-ux-manifesto-principle-driven-design/)
*   [Effectively Planning UX Design Projects](https://www.smashingmagazine.com/2013/01/effectively-planning-ux-design-projects/)
*   [Incorporating More Quiet Into The UX Design Process](https://www.smashingmagazine.com/2013/10/incorporating-quiet-into-ux-design-process/)
*   [A Collaborative Lean UX Research Tool](https://www.smashingmagazine.com/2013/04/rainbow-spreadsheet-collaborative-ux-research-tool/)

## News

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00f470b8-a04c-4322-b056-fc1c0b82b642/ghub-opt.png" alt="GitHub" width="500" /><br>
<figcaption>Github now finally supports options for <a href="https://github.com/blog/2051-protected-branches-and-required-status-checks">protected and required status checks in branches now</a>.</figcaption></figure>

{{% feature-panel %}}

*   Github now finally supports options for [protected and required status checks in branches now](https://github.com/blog/2051-protected-branches-and-required-status-checks). That means you can now restrict the `master` branch so people can’t force push (edit history) or only allow merges when the status checks (like CI, unit/integration tests ran successfully) pass.
*   Following the announcement of a [shared video codec alliance](https://aomedia.org/), Microsoft Edge will get WebM/VP9 support soon.
*   This week Opera Mini on Android got a big update with a new data saving mode. You can now choose between speed and experience. The new speed mode can save up to 90% of data but will remove much of the page layout and heavily compresses images while the experience mode still saves about 30-40% of data but will display most of the layout features and videos. Want to know more about how that affects you as developer? [Here you go](https://dev.opera.com/blog/opera-mini-11-modes/).
*   Ashley Nolan just published the results of a front end tooling survey. [The results](https://ashleynolan.co.uk/blog/frontend-tooling-survey-2015-results) are very interesting and show how uncommon JavaScript unit testing still is or that Gulp is already used more than Grunt while Sass is dominating the market.
*   io.js and node.js are united again. [node.js 4.0](https://nodejs.org/en/blog/release/v4.0.0/) now gives you the best of both worlds and from now on it will be less confusion again. It has an updated V8 (4.5) engine and things like a long term support plan.</p>

## Concepts & Design

<figure><a href="https://overpassfont.org/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf98069-c7fe-4b00-9a18-4ccbc373c70c/hello-opt.png" alt="GitHub" width="500" height="481" /></a><figcaption><a href="https://overpassfont.org/">Overpass</a>, a new sans-serif, free, open source web font.</figcaption></figure>

*   [Daily UI Elements for 100 days straight](https://www.100daysui.com/) gives you inspiration on how differently you could design elements on websites. A great inspiration resource with fresh ideas.
*   [Overpass](https://overpassfont.org/) is a new sans-serif free, open source web font.</p>

## Tools

*   [gulp-shell](https://www.npmjs.com/package/gulp-shell) lets you execute shell commands right from within your gulpfile. This can become very handy when you don’t want to or can’t use a gulp plugin for certain actions.
*   By using [Release It!](https://medium.com/@webprolific/using-release-it-60b96515c073), you can save yourself the endless pain of manually updating version numbers, tagging, linting, writing a changelog and publishing to npm. The interactive wizard guides you through the release in five steps. If you’re using Grunt, there’s also [grunt-release](https://github.com/geddski/grunt-release) available.</p>

## Privacy

*   Following the announcements of Content Blockers in iOS9 and [the just launched](https://adblockplus.org/blog/first-official-ad-blocker-for-ios-launches-today-ditto-for-android) [AdBlock iOS/Android browser](https://adblockbrowser.org/), the first association of the advertising industry [is considering options to fight ad blockers](https://adage.com/article/digital/iab-surveys-options-fight-ad-blockers-including-lawsuits/300228/), including law suits.</p>

## Web Performance

*   By using ServiceWorker and AppCache, [UpUp](https://www.talater.com/upup/) will help you set up your website to be available offline.
*   If you don’t want all your images be loaded directly on page load, this simple technique by Christian Heilmann might be for you: By [wrapping images with a `<template>` element](https://christianheilmann.com/2015/09/08/quick-trick-using-template-to-delay-loading-of-images/) and some lines of JavaScript the load gets deferred in all browsers that support the `<template>` element.</p>

## HTML / SVG

*   In this [guide to building SVG maps](https://www.smashingmagazine.com/2015/09/making-svg-maps-from-natural-earth-data/) you can learn how to code interactive maps from natural earth data.</p>

## Accessibility

*   Most of us, even if we add accessibility improvements to our code, don’t know much about how screen readers are used. That’s why the [results of the screen reader survey](https://webaim.org/projects/screenreadersurvey6/) are very handy to look at.</p>

## JavaScript

*   Dr Axel Rauschmayer continues to share detailed articles about specific ES6 functions. This time I want to recommend [how to use Typed Arrays in ECMAScript 6](https://www.2ality.com/2015/09/typed-arrays.html).
*   As Flash declines and is actively being blocked in browsers now, it’s good to see that [cut, copy and paste are available natively](https://hacks.mozilla.org/2015/09/flash-free-clipboard-for-the-web/) now. The technology has some drawbacks due to security though.
*   Following Dr. Rauschmayer, the _ponyfoo_ blog has launched a big series on ES6\. One article explains the [ES6 arrow functions in depth](https://ponyfoo.com/articles/es6-arrow-functions-in-depth). Another one explains [ES6 Iterators](https://ponyfoo.com/articles/es6-iterators-in-depth) and the third is all about [ES6 Generators](https://ponyfoo.com/articles/es6-generators-in-depth).</p>

## CSS / Sass

*   Rachel Andrew has written a [basic introduction to the fresh CSS Grid module](https://rachelandrew.co.uk/archives/2015/09/02/css-grid-and-the-box-alignment-module/) that is supposed to revolutionize how we code layouts in CSS. It shows how easy it is to get started and then hints you slowly to more advanced examples. Patrick Brosset has also written a guide on [CSS Grid Layouts which features interactive demos](https://medium.com/@patrickbrosset/css-grid-layout-6c9cba6e8a5a) and highly advanced techniques for which you should know the basics already.</p>

## Work & Life

*   Steve Jobs was known to be a great person when it comes to his ideas and innovation. But he also was a great thinker and [knew how to properly respond to insults](https://medium.com/ux-launchpad-notes-on-design/steve-jobs-insult-response-cbd1d6f4d73a) or how to take care of negative feedback.
*   As an interviewer, it can be hard to not be influenced by certain factors. This guide gives a few tips [how to be a less biased interviewer](https://medium.com/@joelle_emerson/raising-the-bar-how-to-be-a-less-biased-interviewer-ecda0892f8f5). Another article shares [how to hire more diverse people](https://medium.com/tech-diversity-files/want-to-hire-more-diverse-people-raise-your-bar-b5d30f91cbd9).
*   Aarron from Mailchimp says you should “[Hire People, Not Skills](https://blog.mailchimp.com/hire-people-not-skills/)” and tells us why that is the better approach.</p>

## Go beyond…

*   If it was for Geoffrey A. Fowler, [we need the right to repair our gadgets](https://www.wsj.com/articles/we-need-the-right-to-repair-our-gadgets-1441737868). The industry wants us to waste broken gadgets and buy new ones, even if it would only take minutes for anyone to repair it. But without companies sharing how we can repair things, it’s a tough task. We, including the gadget vendors need to start thinking about how to produce less waste.

And with that I’ll close for this week. In case you like what I write each week, please support me via <a href="https://paypal.me/anselm">PayPal</a>, <a href="https://gratipay.com/~Anselm%20Hannemann/">gratipay</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via E-Mail, RSS and online.

<em>Thanks and all the best,
Anselm</em>


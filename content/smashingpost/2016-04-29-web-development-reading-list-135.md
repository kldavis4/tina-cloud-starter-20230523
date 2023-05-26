---
title: 'Web Development Reading List #135: Boxy SVG, How To Keep Up, CSS Frameworks'
slug: web-development-reading-list-135
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57aae225-6b57-4b62-be48-f6488efc0863/wdrl-135-opt.png'
date: 2016-04-29T17:12:52.000Z
author: anselm-hannemann
description: >-
  After spring has started marvelously, this week brought us some snow again.
  But today, the sun is shining, it’s getting warmer, and nature is flourishing.
  Inspired by the fresh green of spring, I’d like to announce The Evergreen
  List.

  This is a sub-part of my reading list, collecting **important links that stay
  relevant over a longer time** so that you can find them more easily. Give the
  page a try and if you have feedback, just email me.
categories:
  - Web Development Reading List
---
After spring has started marvelously, this week brought us some snow again. But today, the sun is shining, it’s getting warmer, and nature is flourishing. Inspired by the fresh green of spring, I’d like to announce <a href="https://wdrl.info/evergreen">The Evergreen List</a>. This is a sub-part of my reading list, collecting <strong>important links that stay relevant over a longer time</strong> so that you can find them more easily. Give the page a try and if you have feedback, just email me.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Which Responsive Design Framework Is Best?](https://www.smashingmagazine.com/2017/03/which-responsive-design-framework-is-best/)
*   [Frameworks: Just Because You Can, Should You?](https://www.smashingmagazine.com/2014/02/responsive-design-frameworks-just-because-you-can-should-you/)
*   [Creating A Complete Web App In Foundation For Apps](https://www.smashingmagazine.com/2015/04/creating-web-app-in-foundation-for-apps/)

## News

*   [Node.js 6.0 has been released](https://nodejs.org/en/blog/release/v6.0.0/) and it’ll be the new <abbr title="Long Term Support">LTS</abbr> version. However, the release also brought along a lot of changes. While this is great because performance and security have improved and cool new features were added, it also forces a lot of modules based on Node.js to update their code. That said, test carefully before upgrading it in a production environment.</p>

## Generic

*   “[The web isn’t uniform](https://medium.com/@fox/the-web-isn-t-uniform-fd67eb631501#.a6effstzk)” is probably one of the best expressions to describe how a request to a website works. Karolina Szczur shares why we should embrace this fact more.</p>

## Concept & Design

*   It’s not a secret that agile work methods have positive effects on both workers and managers, but do you know [the history of agile innovation](https://hbr.org/2016/04/the-secret-history-of-agile-innovation)? And while we’re at it, this story shares [interesting insights into how effective it can be to apply Scrum to schools](https://www.scrumalliance.org/home-old/scrummy-school-learners-successfully-self-organize). Last but not least, an article by Atlassian explains [the differences between Kanban and Scrum](https://www.atlassian.com/agile/kanban) very well.</p>

## Tools & Workflows

*   There are different ways to compare screenshots. Usually, for testing tools, this has been done with command line applications, but you can now also [create visual diffs easily by using CSS blend modes](https://una.im/diffee/).
*   React Native brings coding for the web to iOS applications, providing a great alternative to [Cordova](https://cordova.apache.org/). A new article by Nash Vail teaches you to [use React Native to build an iOS application](https://www.smashingmagazine.com/2016/04/the-beauty-of-react-native-building-your-first-ios-app-with-javascript-part-1).
*   Very often, when you have git changes, some indentation or whitespace setting is altered, too. This is a bit annoying as it results in very confusing diffs. But you can actually [add a `w=1` query param to GitHub diff URLs](https://twitter.com/SlexAxton/status/725193003220893696) to ignore whitespace.

{{% feature-panel %}}

<figure class="fwi"><a href="https://una.im/diffee/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddb08ea3-76fc-41aa-bf22-4b8c07f2fa78/diffee-checker-opt.png" alt="Una Kravets found a neat way to create visual diffs using CSS blend modes." width="500" height="350" /></a><figcaption>Una Kravets found a neat way to <a href="https://una.im/diffee/">create visual diffs using CSS blend modes</a>.</figcaption></figure>

## Security

*   Alexa’s [top one million sites were analyzed for their CSP implementation](https://pokeinthe.io/2016/04/25/state-of-csp-alexa-top-one-million-2016-04/). The result: 99.62% don’t have a Content Security Policy at all, and of the remaining share only 53 sites integrated it without `unsafe-inline` options.</p>

## Web Performance

*   Jake Archibald elaborates on common caching mistakes and how to build a [caching concept for your documents that works with the browser’s native cache and Service Workers](https://jakearchibald.com/2016/caching-best-practices/). If you think `no-cache` or `must-revalidate` means the browser does not cache such resources, or if you ever wanted to understand caching properly, read his article.</p>

## HTML & SVG

*   You can build vector graphics in SVG format with the [Boxy SVG editor](https://boxy-svg.com/), a Chrome application that is based on web technologies. A pretty cool alternative to the heavy-weighted Illustrator and Sketch applications which often create SVG code that not every browser understands.</p>

<figure class="fwi"><a href="https://boxy-svg.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f608b16f-36c7-49ba-bfa0-6e561013eca8/boxy-svg-opt.jpg" alt="Boxy SVG" width="500" height="361" /></a><figcaption>When it comes to SVGs, <a href="https://boxy-svg.com/">Boxy SVG</a> is a good alternative to Illustrator and Sketch.</figcaption></figure>

## JavaScript

*   In the upcoming version of Chrome, the [`NodeList` object will finally be an iterable](https://medium.com/@devlucky/nodelist-object-is-finally-an-iterator-cc529d6e2490#.253qv4l0q). This is great because we’ll be able to use `const elements = document.querySelectorAll('a'); elements.forEach(a => console.log(a.getAttribute('href')))` to get a list of all `href` attributes instead of an error. And as it’s [defined as an iterable in the spec](https://www.w3.org/TR/dom/#nodelist), too, we can hope for `NodeList` to gain wide-spread browser support in the future.
*   In promise-based asynchronous code, rejections are used for error handling. One risk is that [rejections may get lost, leading to silent failures](https://www.2ality.com/2016/04/unhandled-rejections.html).</p>

## CSS/Sass

*   A lot of developers think about this differently, but a lot of others use frameworks for every project, even if it’s not the best decision to make. Read on [why you might not need a CSS framework](https://hacks.mozilla.org/2016/04/you-might-not-need-a-css-framework/), about drawbacks and alternatives to the framework approach that won’t sacrifice efficiency when developing a project.</p>

## Work & Life

*   Being a young developer is easy. One learns fast, new technology is exciting, and every type of work is accomplished easily. But if you’re getting older, things change. You might have a family, not enough time for learning, or just have realized that you value your spare time more if you’re not programming. Adrian Kosmaczewski shares his experience with [being a developer after 40](https://medium.freecodecamp.com/being-a-developer-after-40-3c5dd112210c#.p3ijf2n9h) and why learning the basics of a programming language is more important than focusing on frameworks and specific libraries.</p>

## Going beyond…

*   The story of Blake Ross is touching as for most people imagining something in their minds is an ability they make use of all the time. But [Blake can’t visualize anything in his mind](https://www.facebook.com/notes/blake-ross/aphantasia-how-it-feels-to-be-blind-in-your-mind/10156834777480504), and now he shares how he lives with that fact.

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</p>

<em>Thanks and all the best,
Anselm</em>


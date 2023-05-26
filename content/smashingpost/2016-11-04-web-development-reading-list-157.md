---
title: >-
  Web Development Reading List #157: FlyWeb, Lying Charts, And Feedback Without
  Context
slug: web-development-reading-list-157
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f774da4b-b318-43d5-ac12-f14413087c26/wdrl-157-opt.png'
date: 2016-11-04T18:45:02.000Z
author: anselm-hannemann
description: >-
  We all have visions and dreams. Whether it’s about our personal lives, our
  work, or about complex concepts that target issues which are hard to grasp.
  The important thing is to **listen to your ideas**, to write them down, and,
  if they wake strong feelings, to pursue them.

  It can be easy to achieve this, yet sometimes it’s not. A nice technique is to
  start small and take small steps instead of going 100% all-in or do nothing at
  all. We like to play with new things, we like to try out new technology, and
  our minds want to explore new paths — let’s do it!
categories:
  - Web Development Reading List
---
We all have visions and dreams. Whether it’s about our personal lives, our work, or about complex concepts that target issues which are hard to grasp. The important thing is to **listen to your ideas**, to write them down, and, if they wake strong feelings, to pursue them.

It can be easy to achieve this, yet sometimes it’s not. A nice technique is to start small and take small steps instead of going 100% all-in or do nothing at all. We like to play with new things, we like to try out new technology, and our minds want to explore new paths — let’s do it!

### <span class="rh">Further Reading</span> on SmashingMag:

*   [The Do’s And Don’ts Of Infographic Design](https://www.smashingmagazine.com/2011/10/the-dos-and-donts-of-infographic-design/)
*   [Designing Flexible, Maintainable Pie Charts With CSS And SVG](https://www.smashingmagazine.com/2015/07/designing-simple-pie-charts-with-css/)
*   [A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)
*   [Writing Next Generation Reusable JavaScript Modules in ECMAScript 6](https://www.smashingmagazine.com/2016/02/writing-next-generation-reusable-javascript-modules/)

## News

*   [FlyWeb](https://flyweb.github.io/posts/2016/11/01/introducing-flyweb.html) is a new experimental Web API that allows web pages to host local web servers for exposing content and services to nearby browsers. It also adds the ability to discover and connect to nearby local web servers to the web browser itself. This might be a bit hard to grasp now, but imagine this in combination with a decentralized service picking the nearest edge server via FlyWeb. You wouldn’t need any complex external CDN solutions that choose the “nearest” edge server via geolocation resolution or similar unreliable technologies anymore. Another use case could be an “off-grid on-the-fly network” with devices that use FlyWeb together with Bluetooth and WiFi chips to find other devices in the vicinity and hereby introduce a whole new area of network reliability. As FlyWeb is a technology experimentally developed by Mozilla, you need to have Firefox Nightly installed to test this out.</p>

## Concept & Design

*   Coding a line chart isn’t a big deal anymore thanks to libraries like D3 or Highcharts. But what seems so easy, actually isn’t: there are quite some [pitfalls which can distort the results](https://m.signalvnoise.com/lets-chart-stop-those-lying-line-charts-60020e299829#.wlf3o0bji) and lead to false assumptions about the presented data. Line-smoothing is one of them.

{{% feature-panel %}}

<figure><a href="https://m.signalvnoise.com/lets-chart-stop-those-lying-line-charts-60020e299829#.wlf3o0bji"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc00600f-68eb-48c0-b79c-59ddbef92fe3/line-charts-opt.png" width="500" height="293" alt="Lying line chart" /></a><figcaption>A basic chart, right? Well, actually it’s lying to you in a couple of significant ways. Noah Lorang <a href="https://m.signalvnoise.com/lets-chart-stop-those-lying-line-charts-60020e299829#.wlf3o0bji">explains why and how you can do better</a>. (Image credit: <a href="https://m.signalvnoise.com/lets-chart-stop-those-lying-line-charts-60020e299829#.wlf3o0bji">Noah Lorang</a>)</figcaption></figure>

## Tools & Workflow

*   Last week I shared a Webpack [version 1 to 2 migration guide](https://wdrl.info/archive/156/migrating-to-webpack-2). Now Drew Powers wrote [a tutorial to get started with Webpack 2](https://blog.madewithenvy.com/getting-started-with-webpack-2-ed2b86c68783), and, as a bonus, it uses Yarn as a package manager instead of npm’s native CLI client.</p>

## Web Performance

*   Monica Dinculescu just spent a week traveling Taiwan with a 2G roaming plan and now reminds us that we need to [care more about proper lazy font loading](https://meowni.ca/posts/web-fonts/) if we use web fonts to not annoy our users.</p>

## JavaScript

*   Afshin Mehrabani illustrates [the impact of Web Workers](https://afshinm.github.io/50k/) when sorting a 50K array with JavaScript on the main thread or in a background task. Great to see why we should consider using asynchronous worker tasks for complex and non-time-critical operations.
*   Keith Cirkel explains how you can [replace a templating language like Handlebars with the more powerful ES6 Template Literals](https://www.keithcirkel.co.uk/es6-template-strings/). [styled-components](https://styled-components.com/), for example, a tool for writing inline styles for front-end applications, makes great use of this.</p>

## Work & Life

*   Tobias Tom wrote about [doing what you think is right _for you_](https://tobiastom.name/articles/doing-what-you-think-is-right) and why it matters to slowly change your habits and take small steps to reach your goals instead of seeing only black and white.
*   Tom Bartel shares tips for [giving feedback without much context](https://tombartel.de//2016/11/03/feedback-without-much-context/) in development teams and how you can express concerns without making accusations.
*   Kate Lunau from Vice Motherboard wrote an article explaining why [the only good future of commuting is no more commuting](https://motherboard.vice.com/read/the-only-good-future-of-commuting-is-no-more-commuting). Nice to see the topic of how we can work together without sitting in the same room and still be social and productive being picked up.
*   Jonathan MacDonald’s article “[The Paradox of Life Balance](https://ten.io/the-paradox-of-life-balance/)” targets a social problem we all face: While our connected devices offer great things, they also make us neglect real life and social communication. A great piece on why innovation is important and why it’s equally important to balance our activity and prioritize the non-digital reality.

<figure><a href="https://motherboard.vice.com/read/the-only-good-future-of-commuting-is-no-more-commuting"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d762717c-63c7-47ff-9810-3eb3b8201f4d/not-commuting-opt.png" width="500" height="368" alt="Uber envisions a future of on-demand air transportation." /></a><figcaption>While Uber <a href="https://medium.com/@UberPubPolicy/fast-forwarding-to-a-future-of-on-demand-urban-air-transportation-f6ad36950ffa#.xneuw9y5e">envisions a future of on-demand urban air transportation</a>, Kate Lunau argues why the <a href="https://motherboard.vice.com/read/the-only-good-future-of-commuting-is-no-more-commuting">only good future of commuting is no more commuting</a>. (Image credit: <a href="https://medium.com/@UberPubPolicy/fast-forwarding-to-a-future-of-on-demand-urban-air-transportation-f6ad36950ffa#.i08b6w4wj">Uber/Medium</a>)</figcaption></figure>

## Going Beyond…

*   People research what types of economy our society could transfer to after the current form of capitalism. Recently, I learned about [The Venus Project](https://www.thevenusproject.com/resource-based-economy/), a trial balloon for a resource-based economy. As Albert Einstein said decades ago: “We cannot solve our problems with the same thinking we used when we created them.” I’m excited to see this being tested out and curious if other proposals and tests will lead to a transformation of our current economy in the future. Not only we as developers need to play and test in search for better technology and better solutions, but we as human beings need to do this in all areas of our life.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_


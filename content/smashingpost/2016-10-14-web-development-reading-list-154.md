---
title: >-
  Web Development Reading List #154: Yarn, Deep-Fried Data, And A Guide To
  Stateful Components
slug: web-development-reading-list-154
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e1f7452-8bc9-4d97-97c7-d40dac4c41b0/wdrl-154-opt.png'
date: 2016-10-14T17:32:57.000Z
author: anselm-hannemann
description: >-
  With new frameworks and libraries emerging, **the tools we have at hand are
  constantly changing**. But it’s not only our toolkit but also the way we write
  code that constantly evolves — new CSS conventions are developed all the time
  and the best practices to write JavaScript change at least every year.

  But then again, we have to remind ourselves that we shouldn’t immediately jump
  to a new tool just because it’s available, to not rewrite the whole code of a
  project just because conventions have changed. No project will stop working
  because you’re using OOCSS instead of ITCSS or Backbone.js instead of
  React.js. If the project is an ongoing process and will be developed and
  maintained for another few years, you should evaluate to change tools from
  time to time, of course. But take your time. Better evaluate first, then
  reconsider, before you immediately jump on a train from which you don’t know
  where it’s heading.
categories:
  - Web Development Reading List
---
With new frameworks and libraries emerging, **the tools we have at hand are constantly changing**. But it’s not only our toolkit but also the way we write code that constantly evolves — new CSS conventions are developed all the time and the best practices to write JavaScript change at least every year.

But then again, we have to remind ourselves that we shouldn’t immediately jump to a new tool just because it’s available, to not rewrite the whole code of a project just because conventions have changed. No project will stop working because you’re using OOCSS instead of ITCSS or Backbone.js instead of React.js. If the project is an ongoing process and will be developed and maintained for another few years, you should evaluate to change tools from time to time, of course. But take your time. Better evaluate first, then reconsider, before you immediately jump on a train from which you don’t know where it’s heading.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'The WAI Forward'" href="https://www.smashingmagazine.com/2014/07/the-wai-forward/" rel="bookmark">The WAI Forward</a></li>
<li><a title="Read 'A Detailed Introduction To Webpack
" href="https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/" rel="bookmark">A Detailed Introduction To Webpack</a></li>
<li><a title="Read 'Redefining Lazy Loading With Lazy Load XT'" href="https://www.smashingmagazine.com/2015/02/redefining-lazy-loading-with-lazy-load-xt/" rel="bookmark">Redefining Lazy Loading With Lazy Load XT</a></li>

## News

*   With [Chrome 54 now available](https://googlechromereleases.blogspot.de/2016/10/stable-channel-update-for-desktop.html), we get a couple of new features: [the new Custom Elements specification](https://www.smashingmagazine.com/2014/03/introduction-to-custom-elements/) is among them, just like the BroadcastChannel API. Also, `initTouchEvent` has been replaced by `new TouchEvent()`, `KeyEvent.keyIdentifier` by `KeyboardEvent.key`. So please update your code if you use any of these.</p>

## General

*   Rey Bango recently wrote about not knowing everything in web development, and why we should [reframe our view on being comfortable in our industry](https://blog.reybango.com/2016/10/07/you-cant-get-comfortable-in-web-development-anymore/).</p>

## Tools & Workflows

*   This week, the [Yarn npm client](https://yarnpkg.com/) was published. It’s an open-source project that builds on top of npm’s registry, replacing the default npm client with a faster, more reliable client. But before you hop on the new train, consider that some features like custom registries and private packages are still missing and that the concept of locking down dependencies is fundamentally different to bower’s or npm’s principles of dependency management. Therefore you should try it out and read the concept before using it in your projects.

{{% feature-panel %}}

<figure><a href="https://yarnpkg.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/702ba2ec-40f5-4f02-b5c5-9e6cc0d3c212/yarn-opt.png" width="500" height="342" alt="A cat in a rocket — the mascot of Yarn" /></a><figcaption>Speed is one of the strengths of the new and open-source npm client <a href="https://yarnpkg.com/">Yarn</a>. (Image credit: <a href="https://yarnpkg.com/">Yarn</a>)</figcaption></figure>

## Privacy

*   Maciej Ceglowski has given quite a lot of great talks already. At the Library of Congress he recently spoke about “[deep-fried data](https://idlewords.com/talks/deep_fried_data.htm),” and the transcript really is worth a read if you’re interested in machine learning, data gardening, archiving data and the responsible use of it.
*   Stoyan Stefanov explains why using autocomplete fields in forms is great for some fields but can easily [lead to data oversharing](https://www.phpied.com/oversharing-with-the-browsers-autofill/) when used on fields that aren’t required.</p>

## Accessibility

*   Steve Faulkner points out [the importance of not overusing ARIA](https://www.paciellogroup.com/blog/2016/10/a-not-so-short-note-on-aria-to-the-rescue/) when native elements are available for the same purpose.
*   Jordan Scales shares how to build [dynamic links while maintaining the focus state](https://medium.com/@jdan/dynamic-links-and-focus-958a99099763#.i6o25l4o9).

<figure><a href="https://medium.com/@jdan/dynamic-links-and-focus-958a99099763#.i6o25l4o9"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1df46b4-c2b8-49e5-aefe-72c5f1ff969d/dynamic-link-opt.png" width="500" height="149" alt="Resend email link" /></a><figcaption>Jordan Scales shares the <a href="https://medium.com/@jdan/dynamic-links-and-focus-958a99099763#.i6o25l4o9">accessibility gotchas</a> that popped up while developing this seemingly trivial “Resend email” link. (Image credit: <a href="https://medium.com/@jdan/dynamic-links-and-focus-958a99099763#.i6o25l4o9">Jordan Scales</a>)</figcaption></figure>

## JavaScript

*   To serve a high-performance application, we only want to serve the assets and code needed for the first view. David Den Toom wrote up how you can [implement lazy loading in Angular 2 with Webpack](https://medium.com/@daviddentoom/angular-2-lazy-loading-with-webpack-d25fe71c29c1).
*   Lazy loading images is a great way to save your users data. However, on bad network connections, JavaScript can easily break, and, thus, users often won’t be able to see the images at all. To tackle the issue, Robin Osborne shares an approach in which he first goes through the obvious JavaScript-enabled, then JavaScript-disabled scenarios, and concludes with a clever solution to [solve broken JavaScript for image lazy loading](https://robinosborne.co.uk/2016/05/16/lazy-loading-images-dont-rely-on-javascript/).
*   Remy Sharp shares a great [developer tools trick for working with elements on a page](https://remysharp.com/2016/10/10/one-devtools-trick): Select an element with `$('element')` as in jQuery, and get a real array of elements with `$$('div')`.
*   Todd Motto wrote [the missing manual on stateful and stateless components](https://toddmotto.com/stateful-stateless-components). This is a pretty good round-up for everyone writing JavaScript.</p>

## Work & Life

*   “[Mind The Work](https://m.signalvnoise.com/show-up-mind-the-work-2c3e9dcc3979)” is a great piece by Mercedes De Luca about how we tend to judge colleagues based on false assumptions and why and how we should seek to better understand them and their actions.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS, and online._

_— Anselm_


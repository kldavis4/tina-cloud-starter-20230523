---
title: 'Getting Your `head` Straight: A New CSS Performance Diagnostics Snippet'
slug: css-head-tag
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5bbafda-ded4-4bd3-bb2a-8c4188693d30/head-2.png
date: 2021-09-22T15:00:00.000Z
summary: >-
  We love little useful tools and techniques to help folks get their work done better and faster. Today, we’d love to shine the spotlights on a little helper that helps spot common performance bottlenecks easily: [ct.css](https://csswizardry.com/ct/).
description: >-
  We love little useful tools and techniques to help folks get their work done better and faster. Today, we’d love to shine the spotlights on a little helper that helps spot common performance bottlenecks easily: [ct.css](https://csswizardry.com/ct/).
categories:
  - CSS
  - Tools
  - Workflow
  - Performance
disable_ads: true
---

There are plenty of ways to [detect performance bottlenecks](https://www.smashingmagazine.com/2021/01/smashingmag-performance-case-study/) and [audit CSS](https://www.smashingmagazine.com/2021/03/css-auditing-tools/). We can look into common performance bottlenecks and the complexity of stylesheets, the way we load assets, and the order in which it happens. 

One helpful way to spot common problems easily is to use some sort of a [performance diagnostics CSS](https://gist.github.com/tkadlec/683b26344cde774170b94c0fcf0088b4) &mdash; a dedicated stylesheet that highlights potential problems and errors.

Today, during his talk at Webexpo Prague 2021, [Harry Roberts](https://csswizardry.com/), a web performance consultant and front-end engineer, introduced a little helper that helps him spot common performance bottlenecks easily. And that is mostly related to the order of how assets are loaded in the `<head>`.

As Harry says,

<blockquote>“I spend a lot of my time looking through clients’ <code>&lt;head&gt;</code> tags to ensure everything in there is in the best possible shape it can be. There are a lot of complex and often conflicting rules that constitute ‘good’ <code>&lt;head&gt;</code> tags, and cross-referencing everything can soon grow unwieldy, so to make my life easier, I developed <a href="https://csswizardry.com/ct/">ct.css</a> &mdash; a quick and dirty way of seeing inside of your <code>&lt;head&gt;</code>.”</blockquote>

[`ct.css`](https://csswizardry.com/ct/) is a little diagnostic snippet, named after Computed Tomography (CT) scans, that exposes potential performance issues in your page’s `<head>` tags, and will disappear as soon as you’ve fixed them.

{{< rimg href="https://csswizardry.com/ct/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b713dab1-412a-4a4c-883c-a3fb06c2a8df/head-article-1.png" width="800" height="" sizes="100vw" caption="The tool in action. In his session, <a href='https://speakerdeck.com/csswizardry/get-your-head-straight'>Get Your Head Straight</a>, Harry explains what exactly makes good or bad <code>&lt;head&gt;</code> tags. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b713dab1-412a-4a4c-883c-a3fb06c2a8df/head-article-1.png'>Large preview</a>)" alt="A screenshot of the ct.css tool at work on the Smashing Magazine website showing inline styles and a warning of JS blocked by CSS" >}}

Harry has put all the insights he’s learned from his performance work to a perfect `<head>` order, and the tool exposes some of the issues that often result from a suboptimal arrangement of `<head>` tags.

{{< rimg href="https://csswizardry.com/ct/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5bbafda-ded4-4bd3-bb2a-8c4188693d30/head-2.png" width="800" height="" sizes="100vw" caption="<a href='https://csswizardry.com/ct/'>csswizardry.com/ct</a> is a simple bookmarket that you can drag into your browser’s toolbar. Each color and border style represent critical and intermediate warnings as well as a reassuring hint that everything is done well. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5bbafda-ded4-4bd3-bb2a-8c4188693d30/head-2.png'>Large preview</a>)" alt="Colors and border style represent critical and intermediate warnings: orange and red with full and dashed lines shown in the screenshot" >}}

With the bookmarklet in the browser’s toolbar, browse to a website of your choice, click or activate the bookmarklet, and the tool **highlights useful pointers** for you to double-check when working around performance bottlenecks. Just a little helper to make your work a bit easier, and find all those hidden issues faster.

If you just want to play with the snippet, you can get it at [csswizardry.com/ct](https://csswizardry.com/ct/). Happy debugging, everyone!

{{% feature-panel %}}

{{< signature "vf, il" >}}

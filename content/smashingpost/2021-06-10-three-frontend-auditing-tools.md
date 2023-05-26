---
title: 'Three Front-End Auditing Tools I Discovered Recently'
slug: three-frontend-auditing-tools
author: stefan-judis
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e21066b1-baa0-4a85-90ee-8074029d0a32/three-frontend-auditing-tools.jpg
date: 2021-06-10T11:15:00.000Z
summary: >-
  Building a faster website can be a rocket task these days. There are so many things to consider, so it’s challenging to get everything right. Here are three less-known tools that might help you get there.
description: >-
  Building a faster website can be a rocket task these days. There are so many things to consider, so it’s challenging to get everything right. Here are some less-known tools that might help you get there.
categories:
  - Tools
  - Performance
  - Browsers
  - Techniques
disable_ads: true
---

Is every resource properly minified and compressed? Are all the caching headers set correctly? Does the site load all the resources in the best order to guarantee a fast first paint? These are only a few questions to consider when having the goal of building a fast website. Building for the web is complex these days.

But how do you find all these things causing performance issues?

Let me share three tools that will **help you spot performance issues** and ship high-quality and fast websites.

**Note**: *If you’re looking for a complete overview of best practices and tools, have a look at [the Frontend performance checklist](https://www.smashingmagazine.com/2021/01/front-end-performance-2021-free-pdf-checklist/).*
## Waterfaller: A Tool Focusing On Network Waterfalls

I discovered [Waterfaller](https://waterfaller.dev/) just recently. Contrary to Lighthouse or WebPage Test, Waterfaller focuses on one thing alone &mdash; issues in the network waterfall. 

{{< rimg breakout="true" href="https://waterfaller.dev/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a237fa3-b03d-4647-a0eb-723d2f36dec6/1-frontend-auditing-tools.png" width="800" height="590" sizes="100vw" caption="<a href='https://waterfaller.dev/'>Waterfaller</a> focuses on issues in the network waterfall and provides recommendations for improvement." alt="Waterfaller screenshot" >}}

The tool analyzes what resources are loaded on the website and in what order these resources come in. You can find advice on what you could implement to make every resource load faster right in the tool.

I love Waterfaller’s narrow scope! Run a test, find problematic files and receive advice &mdash; that’s all doable in 30 seconds. It’s beautiful!

{{% feature-panel %}}

## Yellow Lab: A Tool That Analyses Your Site Top To Bottom

If you’re looking for an extensive overview of how well your site is structured, give [Yellow Lab](https://yellowlab.tools) a try. The number of included performance tests and checks is outstanding! It provides standard metrics such as page weight and request count and analyzes your HTML, CSS, and JavaScript. 

{{< rimg breakout="true" href="https://yellowlab.tools" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3a8719e-0fdf-49db-b7cc-996eed209528/2-frontend-auditing-tools.png" width="800" height="288" sizes="100vw" caption="<a href='https://yellowlab.tools'>Yellow Lab Tools</a> runs a number of audits, from CSS to JavaScript to performance and provides a detailed overview of issues and how to fix them." alt="Yellow Lab Tools screenshot" >}}

It’s a beautiful tool to find issues in your CSS architecture in the form of duplicated selectors or too many color declarations. It also points out a too complex HTML structure, and it also checks your server and cache header configuration. It’s a perfect companion to build a high-quality website.

## webhint: The Pickiest Tool Out There

Let me introduce you to the end boss. Say hello to [Microsoft’s webhint](https://webhint.io/). webhint is comparable to Lighthouse, and it scans your site for issues in the areas of accessibility, compatibility, progressive web apps, performance, and security. 

{{< rimg breakout="true" href="https://webhint.io/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/572c65c1-f004-4218-928a-2273d355772f/3-frontend-auditing-tools.png" width="800" height="779" sizes="100vw" caption="<a href='https://webhint.io/'>webhint</a> often finds issues that other tools don’t quite catch when looking for ways to improve your site." alt="webhint screenshot" >}}

What astonishes me about webhint is that it’s incredibly picky. I encountered situations in the past where I had a completely green Lighthouse score, WebPage Test gave me straight A’s, but still, webhint was offering me areas for improvement. 

If you haven’t used it yet, I recommend giving it a try. You might find surprising things to improve.

## Use The Best Tools To Build The Best Websites 

As you’ve seen, the tooling landscape includes many valuable tools. And while some of the tools scan for a wide range of issues, there’s no tool covering everything. The usual mantra applies:

<blockquote>“Use the right tool for the job.”</blockquote>

What web performance tools do you use? I’d love to learn more about your favorite tools helping you to ship the best and fastest websites.

{{< signature "vf, il" >}}

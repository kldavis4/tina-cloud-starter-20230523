---
title: 'Make Your Sites Fast, Accessible And Secure With Help From Google'
slug: web-dev-live-google-event-2020
author: dion-almaer
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8945bcbb-c4b7-41d6-8e8e-827c3cf4fa65/5-web-dev-live-google-event.png
date: 2020-07-06T14:00:00.000Z
summary: >-
  From June 30th to July 2nd, Google’s web platform team brought together the web community for [web.dev LIVE](web.dev/live?utm_source=SmashingMag&utm_medium=Fpost), a digital event to talk about the latest development to the platform and tools ecosystem, give developers a chance to talk to each other and ask their burning questions to the team. Over the three days, the Google team shared a round of updates and news in the spirit of helpfulness and to give web developers all the tools and guidance they need to keep their sites stable, powerful and accessible in these challenging times.
description: >-
  Last week, Google’s web platform team shared some of the latest updates to the Web Platform across themes such as performance, UX and design, modern front-end development, PWAs, privacy, and security on the web.
categories:
  - Events
  - Core Web Vitals
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: web.dev LIVE
  link: https://web.dev/live/?utm_source=SmashingMag&utm_medium=Fpost
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33935d2d-aaa2-4c89-94ff-2a4bbee4112f/web-dev-live-logo-opt.png
  description: >-
    This article has been kindly supported by our dear friends at Google and organizers of <a href="https://web.dev/live/?utm_source=SmashingMag&utm_medium=Fpost" style="text-shadow: none;">web.dev LIVE</a>, a digital event dedicated to web development and its latest techniques. <em>Thank you!</em>
---

Earlier this year, the Chrome team [announced](https://blog.chromium.org/2020/05/introducing-web-vitals-essential-metrics.html) the [Web Vitals](https://web.dev/vitals?utm_source=SmashingMag&utm_medium=Fpost) initiative to provide unified guidance, metrics, and tools to help developers deliver great user experiences on the web. The Google Search team also [recently announced](https://webmasters.googleblog.com/2020/05/evaluating-page-experience.html) that they will be evaluating page experience as a ranking criteria, and will include [Core Web Vitals](https://web.dev/vitals/#core-web-vitals?utm_source=SmashingMag&utm_medium=Fpost) metrics as its foundation.

The three pillars of 2020 Core Web Vitals are loading, interactivity, and visual stability of page content, which are captured by the following metrics:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2f84021-bb49-441f-bfdf-4b72c01ce3ec/2-web-dev-live-google-event.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2f84021-bb49-441f-bfdf-4b72c01ce3ec/2-web-dev-live-google-event.png" sizes="100vw" caption="<a href='https://web.dev/vitals/#core-web-vitals?utm_source=SmashingMag&utm_medium=Fpost'>Core Web Vitals 2020</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2f84021-bb49-441f-bfdf-4b72c01ce3ec/2-web-dev-live-google-event.png'>Large preview</a>)" alt="An illustration of the three metrics explained: Largest Contentful Paint, First Input Delay and Cumulative Layout Shift" >}}

- **[Largest Contentful Paint](https://web.dev/lcp/?utm_source=SmashingMag&utm_medium=Fpost)** measures perceived load speed and marks the point in the page load timeline when the page's main content has likely loaded.
- **[First Input Delay](https://web.dev/fid/?utm_source=SmashingMag&utm_medium=Fpost)** measures responsiveness and quantifies the experience users feel when trying to first interact with the page.
- **[Cumulative Layout Shift](https://web.dev/cls/?utm_source=SmashingMag&utm_medium=Fpost)** measures visual stability and quantifies the amount of unexpected movement of page content.

At web.dev LIVE, we shared best practices on how to [optimize for Core Web Vitals](https://youtu.be/AQqFZ5t8uNc) and how to use [Chrome DevTools to explore your site or app’s vitals values](https://youtu.be/OHb3xZIqUeU). We also shared plenty of other performance-related talks that you can find at [web.dev/live](https://web.dev/live?utm_source=SmashingMag&utm_medium=Fpost) in the Day 1 schedule.

## tooling.report

The web is a complex platform and developing for it can be challenging at the best of times. Build tools aim to make a web developer’s life easier, but as a result build tools end up being quite complex themselves. 

To help web developers _and_ tooling authors conquer the complexity of the web, we built [tooling.report](https://tooling.report). It’s a website that helps you choose the right build tool for your next project, decide if migrating from one tool to another is worth it, or figure out how to incorporate best practices into your tooling configuration and codebase. We aim to explain the tradeoffs involved when choosing a build tool and document how to follow best practices with any given build tool. 

We designed a suite of tests for the report based on what we believe represents the best practices for web development. The tests allow us to determine which build tool allows you to follow what best practice and we worked with the build tool authors to make sure we used their tools correctly and represented them fairly. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fae26af4-a28a-4573-958c-d4a14463b60b/1-web-dev-live-google-event.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fae26af4-a28a-4573-958c-d4a14463b60b/1-web-dev-live-google-event.png" sizes="100vw" caption="Comparison report of current set of libraries on <a href='https://tooling.report'>tooling.report</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fae26af4-a28a-4573-958c-d4a14463b60b/1-web-dev-live-google-event.png'>Large preview</a>)" alt="An overview and comparison between the well-known build toolks webpack v4, Rollup v2, Parcel v2 and Browserify+Gulp" >}}

The initial release of tooling.report covers webpack v4, Rollup v2, and Parcel v2 as well as Browserify+Gulp, which we believe are the most popular build tools right now. We built tooling.report with the flexibility of adding more build tools and additional tests with help from the community.

So if you think a best practice that should be tested or is missing, please [propose it in a GitHub issue](https://github.com/GoogleChromeLabs/tooling.report/issues/new) and if you’re up for writing adding a new tool we did not include in the initial set, we welcome you to [contribute](https://github.com/GoogleChromeLabs/tooling.report/blob/dev/CONTRIBUTING.md)!

Meanwhile, you can read more about our [approach towards building tooling.report](https://web.dev/introducing-tooling-report?utm_source=SmashingMag&utm_medium=Fpost) and watch our [session from web.dev LIVE](https://youtu.be/vsMJiNtQWvw) for more.

## Latest In Chrome DevTools And Lighthouse 6.0

Most web developers spend a lot of time of their day in their developer tools so we want to ensure that our tools enable greater productivity, whether it’s for debugging or for auditing and fixing issues to improve user experience.

### Chrome Devtools: New Issues Tab, Color Deficiency Emulator And Web Vitals support 

One of the most powerful features of Chrome DevTools is its ability to spot issues on a webpage and bring them to the developer’s attention &mdash; this is most pertinent as we move into the next phase of a [privacy-first web](https://blog.chromium.org/2020/01/building-more-private-web-path-towards.html). To reduce notification fatigue and clutter of the Console, we’ve launched the “[Issues Tab](https://developers.google.com/web/tools/chrome-devtools/issues)” that focuses on three types of critical issues to start with: [Cookie problems](https://web.dev/samesite-cookies-explained?utm_source=SmashingMag&utm_medium=Fpost), [Mixed content](https://developers.google.com/web/fundamentals/security/prevent-mixed-content/what-is-mixed-content) and [COEP issues](https://web.dev/coop-coep/?utm_source=SmashingMag&utm_medium=Fpost). Watch our session on [finding and fixing problems with the Issues Tab](https://youtu.be/1TbkSxQb4bI) for more.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dad8f02d-56fd-4943-8897-a14f16ec3686/4-web-dev-live-google-event.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dad8f02d-56fd-4943-8897-a14f16ec3686/4-web-dev-live-google-event.png" sizes="100vw" caption="New <a href='https://developers.google.com/web/tools/chrome-devtools/issues'>Issues Tab</a> in Chrome DevTools (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dad8f02d-56fd-4943-8897-a14f16ec3686/4-web-dev-live-google-event.png'>Large preview</a>)" alt="A screenshot of the Chrome DevTools timeline where developers can track and measure metrics, performance and more" >}}

Moreover, with [Core Web Vitals](https://web.dev/vitals/#core-web-vitals?utm_source=SmashingMag&utm_medium=Fpost) becoming one of the most critical sets of metrics that we believe every developer must track and measure, we want to ensure developers are able to easily track how they perform against these thresholds. So we’ve added the three metrics in the [Chrome DevTools timeline](https://youtu.be/OHb3xZIqUeU).

And finally, with an increasing number of developers focusing on accessibility, we also introduced a [Color Vision Deficiency Emulator](https://twitter.com/mathias/status/1237393102635012101?) that allows developers to simulate vision deficiencies, including blurred vision & various other types of color blindness. We’re super excited to bring this feature to developers who’re looking to make their websites more color-blind friendly and you can see more about this and many other features in our session on [What’s the latest in DevTools](https://youtu.be/6yrJZHqJe2k). 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8945bcbb-c4b7-41d6-8e8e-827c3cf4fa65/5-web-dev-live-google-event.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8945bcbb-c4b7-41d6-8e8e-827c3cf4fa65/5-web-dev-live-google-event.png" sizes="100vw" caption="New <a href='https://twitter.com/mathias/status/1237393102635012101?'>Color Vision Deficiency Emulator</a> in Chrome DevTools (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8945bcbb-c4b7-41d6-8e8e-827c3cf4fa65/5-web-dev-live-google-event.png'>Large preview</a>)" alt="A screenshot from YouTube of a session featuring Jake Archibald and Surma" >}}

### Lighthouse 6.0: New Metrics, Core Web Vitals Lab Measurement, An Updated Performance Score, And Exciting New Audits

[Lighthouse](https://developers.google.com/web/tools/lighthouse) is an open-source automated tool that helps developers improve their site’s performance. In its latest version, we focused on providing insights based on metrics that give you a balanced view of your user experience quality against critical dimensions. 

To ensure consistency, we’ve added support for the Core Web Vitals &mdash; [LCP](https://web.dev/lcp/?utm_source=SmashingMag&utm_medium=Fpost), [TBT](https://web.dev/tbt/?utm_source=SmashingMag&utm_medium=Fpost) (lab equivalent for [FID](https://web.dev/fid/?utm_source=SmashingMag&utm_medium=Fpost) as Lighthouse is a lab tool) and [CLS](https://web.dev/cls/?utm_source=SmashingMag&utm_medium=Fpost) &mdash; and removed three old ones: [First Meaningful Paint](https://web.dev/first-meaningful-paint/?utm_source=SmashingMag&utm_medium=Fpost), [First CPU Idle](https://web.dev/first-cpu-idle/), and [Max Potential FID](https://web.dev/lighthouse-max-potential-fid/?utm_source=SmashingMag&utm_medium=Fpost). These removals are due to considerations like metric variability and newer metrics offering better reflections of the part of user experience that we're trying to measure. Additionally, we also made some [adjustments](https://web.dev/lighthouse-whats-new-6.0/#score?utm_source=SmashingMag&utm_medium=Fpost) to the weights based on user feedback.

We also added a super nifty [scoring calculator](https://googlechrome.github.io/lighthouse/scorecalc/) to help you explore your performance scoring, by providing a comparison between version v5 and v6 scores. When you run an audit with Lighthouse 6.0, the report comes with a link to the calculator with your results populated.

And finally, we added a bunch of [useful new audits](https://web.dev/lighthouse-whats-new-6.0/#new-audits?utm_source=SmashingMag&utm_medium=Fpost), with a focus on JavaScript Analysis and accessibility.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14255db6-d350-4c45-b5af-7a529d69bda4/3-web-dev-live-google-event.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14255db6-d350-4c45-b5af-7a529d69bda4/3-web-dev-live-google-event.png" sizes="100vw" caption="All <a href='https://web.dev/lighthouse-whats-new-6.0/#new-audits?utm_source=SmashingMag&utm_medium=Fpost'>new audits in Lighthouse 6.0</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14255db6-d350-4c45-b5af-7a529d69bda4/3-web-dev-live-google-event.png'>Large preview</a>)" alt="" >}}

There are many others that we spoke about at web.dev LIVE &mdash; watch the session on [What’s latest in speed tooling](https://youtu.be/yDHfrhCGFQw) and the [latest in Puppeteer](https://youtu.be/ZO7XWLudGKI).

During web.dev LIVE, we shared more new features and updates that have come to the web over the past few months. Watch all the [sessions](https://web.dev/live?utm_source=SmashingMag&utm_medium=Fpost) to stay up to date and [subscribe](web.dev/newsletter?utm_source=SmashingMag&utm_medium=Fpost) to the web.dev newsletter if you’d like more such content straight to your inbox.   

{{< signature "ef, ra, il" >}}

---
title: 'Web Development Reading List #159: Code Splitting, A New Bundler, And Blake2x'
slug: web-development-reading-list-159
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/122a3105-dff2-4b20-8a0e-a7a90f02754a/wdrl-159-opt.png'
date: 2016-11-18T21:03:58.000Z
author: anselm-hannemann
description: >-
  As developers, are we paid to _write code_? This challenging question raises
  concerns about product quality, code quality, and **our purpose as
  developers** in a world of coded applications. You’ll find an interesting post
  that dives deeper into the matter in the “Work & Life” section of our reading
  list this week.

  But we have other amazing resources to look at this week, too: new tools, new
  tutorials, and we’ll also take some time to reconsider CSS print styles. Let’s
  get started!
categories:
  - Web Development Reading List
---
As developers, are we paid to _write code_? This challenging question raises concerns about product quality, code quality, and **our purpose as developers** in a world of coded applications. You’ll find an interesting post that dives deeper into the matter in the “Work & Life” section of our reading list this week.

But we have other amazing resources to look at this week, too: new tools, new tutorials, and we’ll also take some time to reconsider CSS print styles. Let’s get started!

### <span class="rh">Further Reading</span> on SmashingMag:

*   [A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)
*   [Content Security Policy, Your Future Best Friend](https://www.smashingmagazine.com/2016/09/content-security-policy-your-future-best-friend/)
*   [How To Set Up A Print Style Sheet](https://www.smashingmagazine.com/2011/11/how-to-set-up-a-print-style-sheet/)
*   [On Building Digital Capacity And Attracting Talent](https://www.smashingmagazine.com/2015/11/building-digital-capacity-attracting-talent/)

## News

*   [Firefox 50 was released this week](https://developer.mozilla.org/en-US/Firefox/Releases/50). The new version comes with support for the `once` option for Event Listeners, the `referrerpolicy` attribute and a fix for dashed and dotted borders. On the other hand, `box-sizing: padding-box` was removed. The upcoming version, [Firefox 51](https://www.fxsitecompat.com/en-CA/versions/51/), which is currently in beta, will introduce a couple of changes, too: `<img>` with empty `src` will now fire an error event and JavaScript will be blocked if it’s served with a wrong MIME type. Furthermore, the non-standard Web Payments API will be removed, Accept header for XHR will be simplified, and SHA-1 certificates issued by public CA will no longer be accepted.</p>

## Tools & Workflow

*   Dennis Brotzky wrote [a beginner’s step-by-step guide to Code Splitting with Webpack 2 and React Router](https://brotzky.co/blog/a-beginners-step-by-step-guide-to-code-splitting-with-webpack-2-and-react-router/).
*   Rahul Yadav shares how to [use Webpack and WebPagetest on a Continuous Integration server](https://medium.com/engineering-housing/continuous-integration-using-webpagetest-and-webpack-1f4465d95405) to collect metrics and performance statistics on your web application.
*   [Splittable](https://www.npmjs.com/package/splittable) is a next-generation module bundler for JavaScript that aims at combining efficiency with ease of use. It supports code splitting and tree shaking and uses Babel and Browserify to resolve modules and their dependencies and Google’s Closure Compiler for efficient compilation of code. Definitely one of the most advanced module bundlers available today. Unfortunately, it still needs the Java version of Closure Compiler to work, since the JavaScript variant doesn’t support the relevant feature yet.</p>

## Security

*   [blake2x](https://cybermashup.com/2016/11/11/blake2x-unlimited-hashing/) is a new hashing function that is even better than blake2\. It does not only allow hashes of any arbitrary size but also has a key derivation function and a deterministic random bit generator.
*   What to do if a third party causes your site to throw mixed content warnings? Thanks to the `upgrade-insecure-requests` headers you can [fix your site by applying the header via your Content Security Policy](https://www.troyhunt.com/disqus-mixed-content-problem-and-fixing-it-with-a-csp/).

{{% feature-panel %}}

<figure><a href="https://www.troyhunt.com/disqus-mixed-content-problem-and-fixing-it-with-a-csp/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c181253-a8e9-41ab-a6e8-f099a05308a3/mixed-content-warning-opt.png" width="650" height="415" alt="Mixed content warning" /></a><figcaption>Troy Hunt explains <a href="https://www.troyhunt.com/disqus-mixed-content-problem-and-fixing-it-with-a-csp/">how you can fix a mixed content problem caused by a third party</a>. (Image credit: <a href="https://www.troyhunt.com/disqus-mixed-content-problem-and-fixing-it-with-a-csp/">Troy Hunt</a>)</figcaption></figure>

## JavaScript

*   [When should we use `for … in` and when `for … of` loops](https://bitsofco.de/for-in-vs-for-of/)? Ire Aderinokun explains the differences and advantages of these basic JavaScript loops in detail.</p>

## CSS/Sass

*   Manuel Matuzovic confesses that [he totally forgot about CSS print styles and how easy it actually is](https://medium.com/@matuzo/i-totally-forgot-about-print-style-sheets-f1e6604cfd6) to provide a basic printing experience for users. Manuel only realized this when he saw [Aaron Gustafson complaining](https://twitter.com/AaronGustafson/status/788073583528538112) about Indiegogo’s completely messed up print layout.

<figure><a href="https://medium.com/@matuzo/i-totally-forgot-about-print-style-sheets-f1e6604cfd6#.rzuj25yfk"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efbec6b1-5ccd-4db4-93e1-bf5edd5525f8/indogogo-print-opt.png" width="650" height="435" alt="Indigogo’s messed up print layout" /></a><figcaption><a href="https://twitter.com/AaronGustafson/status/788073583528538112">Aaron Gustafson’s tweet about Indigogo’s messed up print layout</a> reminded Manuel Matuzovic that <a href="https://medium.com/@matuzo/i-totally-forgot-about-print-style-sheets-f1e6604cfd6#.rzuj25yfk">print style sheets are still a thing</a>. (Image credit: <a href="https://twitter.com/AaronGustafson/status/788073583528538112">Aaron Gustafson</a>)</figcaption></figure>

## Work & Life

*   Do you have a plan for your hiring interviews? The people at GitLab certainly have, and they share it with the public: Read their [Hiring Guide](https://about.gitlab.com/handbook/hiring/) to get some useful advice on writing job ads, handling rejections, and conducting interviews.
*   Garann Means quit the web industry about two years ago. Now [she shares what that really meant to her](https://garann.com/dev/2016/wish-you-would-step-back-from-that-ledge-my-friend/), why she did it, and why it’s important that we think very carefully about it before we take this step for real. It’s easy to joke about leaving the industry, but the consequences are real and might differ a lot from what we expect.
*   Theo Nicolaou wrote about [web development and pressure](https://theonicolaou.blogspot.de/2016/10/web-development-and-pressures.html). Even if we don’t read articles every day, work on side-projects all the time, or contribute to open-source projects regularly, the web will still be here tomorrow, and we can still help to move it forward and make an impact. We need to remind ourselves that sometimes it’s okay to just do something different, to relax or go out with friends.
*   “[You Are Not Paid to Write Code](https://bravenewgeek.com/you-are-not-paid-to-write-code/).” Tyler Treat wrote about our job as developers and why we introduce the possibility of failure into a system every time we write code or introduce third-party services. Our job is to find solutions that (if possible) don’t require a new system and to keep out everything else from a codebase unless it’s really necessary.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_


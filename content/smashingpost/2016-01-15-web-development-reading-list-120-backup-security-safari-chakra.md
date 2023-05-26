---
title: >-
  'Web Development Reading List #120: Safari 9.1, Chakra Core Open Sourced, ES6 Object Shorthand Syntax'
slug: web-development-reading-list-120-backup-security-safari-chakra
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed02a80c-eb2c-4d33-9a00-d169f4f35043/when-disaster-strikes-opt.png
date: 2016-01-15T21:08:34.000Z
author: anselm-hannemann
summary: >-
  What’s going on in the industry? What new techniques have emerged recently? Anselm Hannemann is collecting everything that popped up over the last week in his web development reading list so that you don’t miss out on anything. The result is a carefully curated list of articles and resources that are worth taking a closer look at.
description: >-
  This list of articles gather information about the Web Development industry, Web Development tools and Web Design insights, tools, tips and tricks.
categories:
  - Web Development Reading List
  - Coding
  - Tools
---
One thing we should learn to embrace more this year is to **enjoy the good things** and focus more on the positive news than on the negative. I started to learn more ES6 this year and have scheduled 1 to 2 small learning modules of ES6 and 1 to 2 accessibility features I don’t know yet to study each week. Currently, this works out great. If you learn something from this resource and are able to spend a few bucks this month, [consider rewarding my efforts](https://wdrl.info/donate).

## News

- This week, [Apple announced the pre-release of Safari 9.1](https://developer.apple.com/library/prerelease/mac/releasenotes/General/WhatsNewInSafari/Articles/Safari_9_1.html) which will introduce the `<picture>`&ndash;element, Fast Tap on iOS, changes to modal dialogs, CSS Variable support, `all`, `unset`, `font-variant-*` and `will-change` property support as well as unprefixed CSS `filter`. Let’s hope that shorter release&ndash;cycles are Apple’s new strategy for a more open, more responsive browser culture.
- [jQuery 2.2 and 1.12](https://blog.jquery.com/2016/01/08/jquery-2-2-and-1-12-released/) have been released &mdash; probably the last minor updates before jQuery 3\. The updates include selector performance improvements, SVG class manipulation, and a couple of other small changes.
- As still a lot of websites are horribly broken in Firefox, [Firefox starts accepting `-webkit-` prefixes](https://www.otsukare.info/2016/01/04/webkit-resolved-fixed). With that step, they follow Microsoft with its Edge browser. Another occurrence of why vendor prefixes are nothing we should be proud of using.
- Following Microsoft’s earlier announcement, its JavaScript engine [Chakra Core is now open-source](https://blogs.windows.com/msedgedev/2016/01/13/chakracore-now-open/). If you want to see how it performs compared to Blink’s engine, you’ll find a small comparison [here](https://twitter.com/rauchg/status/687333090809610240).

{{% feature-panel %}}

## General

- Phew, I always wondered about how much of the internet Amazon AWS transports. In fact, we still don’t know it, but we now know that [up to 70% of the global internet traffic goes through Northern Virginia](https://www.nextgov.com/big-data/2016/01/70-percent-global-internet-traffic-goes-through-northern-virginia/124976/), so we can assume that the global share of what’s hosted on AWS is even higher. A scary thought by all means, as this makes the majority of the internet very vulnerable to any kind of attack or catastrophe. Did you ever think of [having a backup plan](https://www.ricohidc.com/services/disaster-recovery.php) for your AWS hosted application? [Can you make the switch to another data center](https://signalvnoise.com/posts/3857-when-disaster-strikes) within minutes?

<figure><a href="https://signalvnoise.com/posts/3857-when-disaster-strikes"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed02a80c-eb2c-4d33-9a00-d169f4f35043/when-disaster-strikes-opt.png" width="500" height="234" alt="hand made illustration showing a character scaping a storm going towards a safe and sunny fortress" /></a><figcaption>When disaster strikes, <a href="https://signalvnoise.com/posts/3857-when-disaster-strikes">can you make the switch to another data center within minutes</a>?</figcaption></figure>

## Tools

- [Typography Supply](https://typography.supply/) is an inventory of typographic tools. They help you find out which fonts are used somewhere, and also include type testers, type measurements, and many more.
- If you use the ZSH shell, [this short guide](https://grml.org/zsh/zsh-lovers.html) gives you a lot of advice to enhance and customize your shell.

## Security

- Guy Podjarny shares how you can [eliminate known node.js / npm vulnerabilities easily](https://www.smashingmagazine.com/2016/01/eliminating-known-security-vulnerabilities-with-snyk/).
- If you store passwords, you probably use bcrypt for hashing them (or let’s hope so, at least). But times change, and given our computing power today, bcrypt isn’t very safe anymore. In fact, with a highly&ndash;parallelized GPU, it’s easy to crack bcrypt in a short time. That’s why you should upgrade to [Argon2](https://github.com/p-h-c/phc-winner-argon2), which will soon be the official new standard by the IETF. [Now check out how to use it](https://hynek.me/articles/storing-passwords/).

{{% ad-panel-leaderboard %}}

## JavaScript

- Ian Feather shows the new [ES6 object shorthand syntax](https://ianfeather.co.uk/destructuring-rest-properties-and-object-shorthand/) and rest properties.
- Starting with the soon to be released Firefox 46, [Firefox will warn you to alter scroll positions in a `scroll` event listener](https://www.fxsitecompat.com/en-US/docs/2016/scroll-linked-positioning-effects-may-not-work-well-with-async-scrolling-console-warns/). This is due to the newly implemented asynchronous scrolling technique. The Firefox Site Compatibility Working Group also provides [workarounds and fixes](https://www.fxsitecompat.com/en-US/docs/2016/scroll-linked-positioning-effects-may-not-work-well-with-async-scrolling-console-warns/) for that.
- It’s easy to forget when you build JavaScript applications, but you should [always remember to provide meaningful fallback content via the `<noscript>` element](https://webdesign.tutsplus.com/tutorials/quick-tip-dont-forget-the-noscript-element--cms-25498). It also targets people disabling scripts in their browsers or using content blockers.

## Work & Life

- Seeing [Basecamp’s article about employee benefits](https://m.signalvnoise.com/employee-benefits-at-basecamp-d2d46fd06c58) made me again aware of the big gaps that exist in social and employee care around the world. In Germany, many of the mentioned benefits are a requirement for companies and supported by the government (health insurance, parental leave, retirement plan). It’s great to see such things being provided unsolicitedly by the company and my hope is that this will become a government standard all over the world in the next decade.

{{% ad-panel-leaderboard %}}

## Go beyond…

- I have written about plastic trash in our oceans over and over again here. I don’t know about you but I, even though informed about the issue, could not imagine how my trash ends up polluting the oceans even though I don’t live anywhere by the sea. [The LA Times now shares an example of how this happens](https://www.latimes.com/visuals/graphics/la-me-g-snapshot-storm-drains-20150401-htmlstory.html).
- These times we’re used to bad news. In fact, that’s the reason I gave up reading newspapers and general social media streams. But it’s not that things are getting so much worse, the problem is no one looks at the bigger numbers. Actually, [the world is getting a better place](https://www.vox.com/2014/11/24/7272929/charts-thankful) &mdash; it just happens much slower than we’re used to in times of real&ndash;time media. We should acknowledge the good news more again this year. And to back this up, I recommend you to [watch this short video](https://vimeo.com/143685854).
- This impressive article lists [all the things Google/Alphabet is working on for the new year](https://arstechnica.com/gadgets/2016/01/2016-google-tracker-everything-google-is-working-on-for-the-new-year/). It gave me a new perspective on _how_ big the company has actually grown by now.
- The New York Public Library released 180,000 copyright&ndash;free images to the public and also gives access to its collection’s metadata and making updates to its API. [A Quartz post highlights the most fascinating pieces](https://qz.com/587894/the-most-fascinating-images-from-the-new-york-public-librarys-release-of-180000-copyright-free-materials/) but you can [search on your own on the official site](https://digitalcollections.nypl.org/). It’s amazing to see another big archive making its materials publicly available.
- [With Bitcoin, we not only introduce a new era of money but also new problems](https://motherboard.vice.com/read/bitcoin-is-unsustainable). A single Bitcoin transaction for example uses roughly as much electricity as is needed to power 1.57 American households for one(!) day. I don’t think the new concurrency makes things better as long as we haven’t fixed issues like these.

<figure><a href="https://digitalcollections.nypl.org/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ed5bb30-703b-4a8e-9cbd-5efa06eafad0/new-york-library-opt.png" width="500" height="483" alt="The anatomy of 6 sea cucumbers"/></a><figcaption>The anatomy of sea cucumbers &mdash; one of the <a href="https://digitalcollections.nypl.org/">180,000 copyright&ndash;free images</a> that the New York Public Library released to the public.</figcaption></figure>

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via E&ndash;Mail, RSS and online.

_Thanks and all the best,
Anselm_

### Further Reading on SmashingMag:

- “[Building Hybrid Apps With ChakraCore>](https://www.smashingmagazine.com/2016/09/building-hybrid-apps-with-chakracore/),” Eric Rozell
- “[Inside Microsoft’s New Rendering Engine For The “Project Spartan”](https://www.smashingmagazine.com/2015/01/inside-microsofts-new-rendering-engine-project-spartan/),” Jacob Rossi
- “[Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/),” Dmitry Nutels
- “[A Beginner’s Guide To jQuery-Based JSON API Clients](https://www.smashingmagazine.com/2012/02/beginners-guide-jquery-based-json-api-clients/),” Ben Howdle

{{< signature "nl" >}}
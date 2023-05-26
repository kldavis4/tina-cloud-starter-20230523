---
title: 'Web Development Reading List #127: jQuery 3, UX Research And XSS In Ads'
slug: web-development-reading-list-127
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66ede2bf-d969-4e29-899f-b5efd9ffe160/wdrl-127-opt.png'
date: 2016-03-04T19:40:46.000Z
author: anselm-hannemann
description: >-
  Working on very different projects, in different teams and with different
  people can sometimes be a challenge. But one thing that works out remarkably
  well is doing **retrospectives** with your team.

  In retrospectives, you talk about how a certain project went, and the whole
  team shares what problems/challenges they faced, what was good and what was
  annoying people, why people were unhappy. And after each person has written
  this down on a wall (you can use Post-Its), you try to find useful solutions,
  small improvements that avoid conflicts, that avoid people feeling bad in a
  project, and that avoid unnecessary stress situations. Ideally, you do this
  often — like every two weeks. In every team so far, talking about issues and
  addressing them has helped to **bind the team together and improve future
  work**. Let’s work more together in our teams instead of on our own.
categories:
  - Web Development Reading List
---
Working on very different projects, in different teams and with different people can sometimes be a challenge. But one thing that works out remarkably well is doing **retrospectives** with your team.

In retrospectives, you talk about how a certain project went, and the whole team shares what problems/challenges they faced, what was good and what was annoying people, why people were unhappy. And after each person has written this down on a wall (you can use Post-Its), you try to find useful solutions, small improvements that avoid conflicts, that avoid people feeling bad in a project, and that avoid unnecessary stress situations. Ideally, you do this often — like every two weeks. In every team so far, talking about issues and addressing them has helped to **bind the team together and improve future work**. Let’s work more together in our teams instead of on our own.</p>

## Concepts & Design

*   We often complain about infinite lazy-loading of elements on a page but what do actual users think about such features in comparison to an old-school pagination? Christian Holst [researched it for online shops and wrote up the effectiveness of modern UX elements](https://www.smashingmagazine.com/2016/03/pagination-infinite-scrolling-load-more-buttons/).</p>

## Tools

*   Zach Holman summarized “[basically everything he knows about deployments](https://zachholman.com/posts/deploying-software),” with the goal of making the deploys of your project as boring, straightforward, and stress-free as possible.</p>

## Security

*   Maybe not surprising but still as bad as it sounds: [Many ad networks allow code execution and are vulnerable to XSS attacks](https://randywestergren.com/widespread-xss-vulnerabilities-ad-network-code-affecting-top-tier-publishers-retailers/), as this research by Randy Westergren shows. I really hope that ad networks will spend more effort on finally fixing their data leaks, security and privacy issues.
*   If you’ve been thinking to just connect to a SSL VPN to be more secure or anonymous, I have bad news for you. A recent [survey showed that about 90% of all SSL VPNs out there are hopelessly insecure](https://www.theregister.co.uk/2016/02/26/ssl_vpns_survey/?mt=1456779955788), and are feigning security to its users that isn’t there. So double-check the VPN before using it and if you’re in a company VPN, let them check the network for the security problems mentioned in the article.

{{% feature-panel %}}

<figure class="fwi"><a href="https://randywestergren.com/widespread-xss-vulnerabilities-ad-network-code-affecting-top-tier-publishers-retailers/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a021fde5-4f65-4031-b3f7-d609f0245e44/ad-network-opt.png" alt="Ad networks" width="500" height="283" /></a><figcaption>Many <a href="https://randywestergren.com/widespread-xss-vulnerabilities-ad-network-code-affecting-top-tier-publishers-retailers/">code networks are vulnerable to XSS attacks</a> as Randy Westergren shows. (Image credit: <a href="https://randywestergren.com/widespread-xss-vulnerabilities-ad-network-code-affecting-top-tier-publishers-retailers/">Randy Westergren</a>)</figcaption></figure>

## Web Performance

*   [Yoav Weiss clarifies Preload](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/), a relatively new specification to define custom loading logic without suffering the performance penalty that script-based resource loaders incur.
*   Bruce Lawson explains [why he personally thinks ad blockers are important](https://www.brucelawson.co.uk/2016/on-ad-blocking/). While that is just another opinion, it also reveals some lesser known problems of advertising these days. The major point here being the cost of large JavaScript files, graphics and banners that matters way more in developing countries than in our cheap-data-plan countries. Notably, he also mentions that we finally need to find alternatives to displaying ads to gain money from publishing content on the web.</p>

## HTML/SVG

*   There’s a lot of confusion about whether you should include `width/height` attributes for responsive SVG files. Sara Soueidan shares why it’s still a good idea to [use sizing attributes for SVG elements in a clever way and then enhance the responsiveness via CSS](https://sarasoueidan.com//blog/svg-style-inheritance-and-FOUSVG/) later on.</p>

## Accessibility

*   Georgie Luhur shares the basic concepts of how to [use ARIA with your existing markup without spending much time on it](https://www.sitepoint.com/how-to-use-aria-effectively-with-html5/) but bringing great benefit to your users.
*   Do you know what it feels like to read a text if you have dyslexia? Dyslexic people _can_ read text, but it takes them a lot of concentration, and the letters seem to “jump around”. Here’s [a demonstration that simulates Dyslexia](https://geon.github.io/programming/2016/03/03/dsxyliea). And now imagine how difficult this must be if there’s not enough contrast or a movie playing in the background.</p>

## JavaScript

*   What’s new in jQuery’s version 3 that will be released soon? `for … of` loops, `requestAnimationFrame` for animations, and many more cool changes. Check out the [most important innovations of jQuery 3 here](https://developer.telerik.com/featured/whats-new-in-jquery-3/).</p>

## Work & Life

*   Estimating a web development job is very hard, especially in front-end where you have so many variables. But with some clever tricks you can [achieve a better estimation and cost proposal](https://hanserino.github.io/2016/02/11/estimating-a-front-end-web-dev-job/) by splitting things into small tasks and by creating user stories.
*   It’s not a new finding but still so many start-ups and [companies think that people are more effective if they work longer](https://medium.com/@hcatlin/the-myth-of-long-hours-49a1f5072482). The opposite is the case, and it’s hurting creativity, productivity and the work-life balance of employees.

And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online.

_Thanks and all the best,  
Anselm_


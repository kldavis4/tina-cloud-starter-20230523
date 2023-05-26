---
title: >-
  Web Development Reading List #136: Design Usability, Meaningful CSS And
  Project Include
slug: web-development-reading-list-136
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6317011-b3e6-42d4-baec-74c10addeac9/designing-for-everyone-opt.jpg
date: 2016-05-06T17:08:32.000Z
author: anselm-hannemann
description: >-
  The past week showed yet again **how fractured opinions in our industry can
  be** and that to some problems there’s definitely more than just one answer,
  or we still have to figure out what the proper way is in the end. This is why
  talking about technical problems matters, and this should certainly be done
  from time to time with your colleagues.

  We all know that by sharing and talking to other people, our jobs get more
  interesting. So, let’s work together more instead of on our own — that would
  be my advice.
categories:
  - Web Development Reading List
---
The past week showed yet again <strong>how fractured opinions in our industry can be </strong> and that to some problems there’s definitely more than just one answer, or we still have to figure out what the proper way is in the end. This is why talking about technical problems matters, and this should certainly be done from time to time with your colleagues.

We all know that by sharing and talking to other people, our jobs get more interesting. So, let’s work together more instead of on our own — that would be my advice. By the way, if you’re around for the upcoming BTConf in Düsseldorf, Germany, I’ll be there from Sunday to Tuesday. Feel free to come over and talk to me if you like!

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Conversational Design Essentials: Tips For Building A Chatbot](https://www.smashingmagazine.com/2016/12/conversational-design-essentials-tips-for-building-a-chatbot/)
*   [Finding Better Mobile Analytics](https://www.smashingmagazine.com/2016/10/finding-better-mobile-analytics/)
*   [How To Build A Real-Time Commenting System](https://www.smashingmagazine.com/2012/05/building-real-time-commenting-system/)
*   [How To Develop A Chat Bot With Node.js](https://www.smashingmagazine.com/2016/10/how-to-develop-a-chat-bot-with-node-js/)

## News

*   [With the Chromium 50 and Opera 37 release](https://dev.opera.com/blog/opera-37/), Regular Expressions can now handle Unicode better, `<link rel="preload" as="…">` is supported, [CSS `column-fill`](https://drafts.csswg.org/css-multicol-1/#cf) can balance multi-column layout content better, and Geolocation and App Cache API won’t work on non-HTTPS contexts anymore, so that `Object.observe` won’t work anymore.
*   The European Comission agreed on [new rules for websites and mobile apps](https://europa.eu/rapid/press-release_IP-16-1654_en.htm) of public sector bodies to make them more accessible. This is great to see and means quite some changes for developers who build for institutions affected by the new ruling, since regular monitoring and reporting will be required as well. It’s still not approved but after this step, member states have 21 months to make this a requirement in all countries of the EU.
*   Starting in EdgeHTML 14.14316, [Microsoft Edge will support WOFF 2.0 fonts](https://blogs.windows.com/msedgedev/2016/05/03/woff2-fonts-in-microsoft-edge/). This is great as it implies up to 30% smaller font files served to the user and makes browser support pretty good.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](#further-reading-on-smashingmag)

*   [Inclusive Design Patterns (Book)](https://shop.smashingmagazine.com/products/pre-release-inclusive-design-patterns-by-heydon-pickering "Inclusive Design Patterns (Book)")
*   [Chrome, Firefox, Safari, Opera, Edge? Impressive Web Browser Alternatives](https://www.smashingmagazine.com/2015/09/chrome-firefox-safari-opera-edge-impressive-web-browser-alternatives/ "Chrome, Firefox, Safari, Opera, Edge? Impressive Web Browser Alternatives")
*   [Inside Microsoft’s New Rendering Engine For The “Project Spartan”](https://www.smashingmagazine.com/2015/01/inside-microsofts-new-rendering-engine-project-spartan/ "Inside Microsoft’s New Rendering Engine For The “Project Spartan”")

## Concept & Design

*   Accessibility is often seen as a technical task but in reality, it’s an integral process that should be taken into account by everyone. Here’s [what designers can do](https://medium.com/salesforce-ux/7-things-every-designer-needs-to-know-about-accessibility-64f105f0881b#.u8wj07e17) to improve the usability and accessibility of the product.

{{% feature-panel %}}

<figure><a href="https://medium.com/salesforce-ux/7-things-every-designer-needs-to-know-about-accessibility-64f105f0881b#.sw6tg7mtt"><img title="7 Things Every Designer Needs to Know about Accessibility" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6317011-b3e6-42d4-baec-74c10addeac9/designing-for-everyone-opt.jpg" alt="7 Things Every Designer Needs to Know about Accessibility" width="500" /></a><figcaption>It's important to design for the diverse set of users who will interact with your products. (<a href="https://medium.com/salesforce-ux/7-things-every-designer-needs-to-know-about-accessibility-64f105f0881b#.sw6tg7mtt">Image credit</a>)</figcaption></figure>

## Tools & Workflows

*   With recent versions of npm, you can [easily use local modules as (dev)-dependencies](https://medium.com/@arnaudrinquin/build-modular-application-with-npm-local-modules-dfc5ff047bcc). Most people don’t know of it but it’s as easy as writing `"mymodule": "file:local_modules/my-module"` in the `package.json` file.</p>

## Security

*   CSP (Content-Security-Policy) is a good method to restrict browsers from loading malicious code on your website. But be aware that nothing is perfect, and so isn’t the implementation in Chrome and Firefox, as [this example of a reflected XSS](https://labs.detectify.com/2016/04/04/csp-bypassing-form-action-with-reflected-xss/) shows.</p>

## Privacy

*   On Thursday, [the U.S. Supreme Court quietly approved a rule change](https://www.thelastamericanvagabond.com/constitutional-rights/fbi-labled-tor-browser-users-criminals/) that would allow a federal magistrate judge to issue a search and seizure warrant for any target using anonymity software like Tor to browse the internet. So if you use Tor or anything similar, it’s now possible that you’ll be directly labelled as a possible criminal and can be targeted for surveillance — starting this December!

## Accessibility

*   Luke McGrath now provides a free and pretty complete, understandable [checklist for WCAG 2.0](https://www.wuhcag.com/wcag-checklist/). Use it for your upcoming projects and even to recognize what could be improved in future.

## JavaScript

*   Closures are a fundamental JavaScript concept that every serious programmer should know inside-out. [So let’s learn this now properly](https://medium.freecodecamp.com/lets-learn-javascript-closures-66feb44f6a44).</p>

<figure><a href="https://medium.freecodecamp.com/lets-learn-javascript-closures-66feb44f6a44"><img title="JavaScript can give you headaches, but not when you understand the nuts and bolts of how it works." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5811dfa2-8b81-45a0-bdd1-bb1de3f8f8f4/js-code-example-opt.png" alt="JavaScript can give you headaches, but not when you understand the nuts and bolts of how it works." width="500" /></a><figcaption>JavaScript can give you headaches, but not when you understand the nuts and bolts of how it works. (<a href="https://medium.freecodecamp.com/lets-learn-javascript-closures-66feb44f6a44">Image credit</a>)</figcaption></figure>

## CSS/Sass

*   It’s somewhat astonishing how much discussion this article created: Tim Baxter wrote [Meaningful CSS: Style Like You Mean It](https://alistapart.com/article/meaningful-css-style-like-you-mean-it) in order to plea to developers to start using semantic selectors instead of artificially created ones following some made-up convention. While I mostly agree with the author (that we should try to use the native selectors from HTML more), there’s the other party that defends conventions like BEM in order to create an easily understandable, maintainable code-base. A discussion where neither one or the other party will be the winner. Sometimes, a reasonable compromise is better than sticking to one or the other principle. Personally, I think state-classes can be better replaced by `aria-*` state attributes while for other modules, using class-selectors are better than chaining endless generic HTML-elements.</p>

## Work & Life

*   Previously, I’ve linked to Zach Holman’s great [remote-first vs. remote-friendly article](https://wdrl.info/archive/107/remote-first-vs-remote-friendly). Now, Karolina Szczur wrote up [what’s needed to build a great remote first team](https://medium.com/@fox/building-remote-first-teams-a98bf8581db).</p>

<figure><a href="https://zachholman.com/posts/remote-first/"><img title="Having a remote team that's spread out across the globe will force you to use tools differently." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1087bb76-42d9-4535-bebe-1811255ba69b/remote-work-worldwide-opt.jpg" alt="Having a remote team that's spread out across the globe will force you to use tools differently." width="500" /></a><figcaption>Having a remote team that's spread out across the globe will force you to use tools differently. (<a href="https://zachholman.com/posts/remote-first/">Image credit</a>)</figcaption></figure>

## Going Beyond…

*   True diversity is inclusive, comprehensive, and measurable. [Project Include](https://projectinclude.org/) is an open community working toward providing meaningful diversity and inclusion solutions for tech companies. The initiative wants to provide collected perspectives, recommendations, materials, and tools to help CEOs and their teams build meaningful inclusion.
*   “Everything from fatness to school marks and career advancement must always be someone else’s fault. In fact, the concept of an accident is disappearing from our collective consciousness. If you fall over on a street made slippery by dead leaves, then someone should have swept them away. If you fall off a cliff, someone should have warned you by putting up a notice warning that it is too far to jump.” [We’ve forgotten how to take blame](https://www.independent.ie/opinion/comment/weve-forgotten-how-to-take-blame-for-our-actions-34676475.html) for our own actions.

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more about the costs of the project <a href="https://wdrl.info/costs/">here</a>. It’s available via email, RSS and online.</p>

<em>Thanks and all the best,
Anselm</em>


---
title: >-
  Web Development Reading List #129: CSRF, Modern Tooling And The UX Of Web
  Fonts
slug: web-development-reading-list-129
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99fc52af-1a24-424e-a2e8-99b2002af9c0/wdrl-129-opt.png'
date: 2016-03-18T18:15:59.000Z
author: anselm-hannemann
description: >-
  Every week I learn so many new things about front-end development. By building
  various kinds of projects, by talking to other developers, by reading new
  articles. Of course, it can be overwhelming, but to me this is the best part
  of the job. By **sharing and talking to other people**, my job gets more
  interesting.

  For example, this week I learned how to build malicious links with
  `target="_blank"`, I learned how CSRF works, and how important it is that an
  icon clearly indicates what it is thought for — the latter after I implemented
  the icons and only found some of them helpful as I saw the fallback/title text
  for them. Always stay curious.
categories:
  - Web Development Reading List
---
Every week I learn so many new things about front-end development. By building various kinds of projects, by talking to other developers, by reading new articles. Of course, it can be overwhelming, but to me this is the best part of the job. By <strong>sharing and talking to other people</strong>, my job gets more interesting.

For example, this week I learned how to build malicious links with <code>target="_blank"</code>, I learned how CSRF works, and how important it is that an icon clearly indicates what it is thought for — the latter after I implemented the icons and only found some of them helpful as I saw the fallback/title text for them. Always stay curious.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Effectively Planning UX Design Projects](https://www.smashingmagazine.com/2013/01/effectively-planning-ux-design-projects/)
*   [How To Spark A UX Revolution](https://www.smashingmagazine.com/2017/03/spark-ux-revolution/)
*   [The Lean UX Manifesto: Principle-Driven Design](https://www.smashingmagazine.com/2014/01/lean-ux-manifesto-principle-driven-design/)
*   [How To Become A UX Leader](https://www.smashingmagazine.com/2015/04/how-to-become-a-ux-leader/)

## News

*   [What’s new in Chromium 49 and Opera 36](https://dev.opera.com/blog/opera-36/)? They support ES6 default function parameter values, ES6 destructuring assignment, ES6 Proxy and Reflect, CSS custom properties, `"a rel=noopener"` (see article in the security section), and many things more.</p>

## General

*   With the provocative title “[Frameworks don’t make much sense — good coders code, great coders reuse](https://www.catonmat.net/blog/frameworks-dont-make-sense/)”, Peteris Krumins writes about why he thinks it’s not sustainable to focus on learning frameworks and why he sees them as an anti-pattern for software development.</p>

## Tools

*   Wes Bos’ new [slide deck about modern workflow and tooling](https://wesbos.github.io/Modern-Workflow-and-Tooling-Talk/) in front-end development is pretty interesting and gives you some insight if you want to know if your workflow is still state-of-the-art.</p>

## Security

*   If you run git on a server, if you use git, please update your software clients immediately. [An exploit has been published](https://ma.ttias.be/remote-code-execution-git-versions-client-server-2-7-1-cve-2016-2324-cve-2016-2315/) that allows remote code execution in all versions up to 2.7.4 (the version containing the fix).
*   How [`target="_blank"` can be abused to serve malicious links](https://mathiasbynens.github.io/rel-noopener/) is shown in this demo by Mathias Bynens.
*   Mozilla implemented a new [block-all-mixed-content CSP directive](https://bugzilla.mozilla.org/show_bug.cgi?id=1122236) that lets websites opt in to hard-fail on mixed content (it won’t be shown and no warning will be triggered).
*   Do you know how a cross-site request forgery (CSRF) works? There is now an infographic that visually explains how CSRF works.

{{% feature-panel %}}

<figure class="fwi"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/497e5e60-5626-4485-8634-4159ea8661cb/csrf-explained-opt.png" alt="Infographic explaining CSRF" width="500" height="361" /><br>
<figcaption>Cross-site request forgery (CSRF) visually explained. (Image credit: Barricade)</figcaption></figure>

## Privacy

*   What happens when a surveillance state becomes an affordable gadget? Maybe it doesn’t faze you that your local police has a $400,000 device that listens in on cell phones. But [how do you feel when your neighbor has a $1,500 version](https://www.bloomberg.com/news/articles/2016-03-10/what-happens-when-the-surveillance-state-becomes-an-affordable-gadget)? In most countries it’s illegal to buy such devices, however, a recent study revealed that anyone can buy one very easily nonetheless.</p>

## HTML/SVG

*   If you use React, it’s relatively easy to implement an SVG icon system with the `<use>` element. But [Sarah Drasner found an even better way](https://css-tricks.com/creating-svg-icon-system-react/) that uses React’s core principles of a virtual DOM.</p>

## Accessibility

*   Rodney Rehm published the first big update to [his amazing accessibility library ally.js](https://github.com/medialize/ally.js/releases/tag/1.1.0). Version 1.1 has completely rewritten tests, supports way more browsers, and is even more reliable to handle focus states on your web application. And finally, you can also learn a lot about how to maintain an open-source project — just look at the incredibly detailed release notes or at the test suite that’s behind it.

## JavaScript

*   Mathias Schäfer summarized [how important progressive enhancement is for large JavaScript applications](https://molily.de/javascript-failure/). To back it up, he analyzes a recent issue on twitter.com that prevented people from tweeting because a JavaScript regex failed and no fallback was available.
*   If you want to know if a specific Node.js version supports some ECMAScript language feature yet, here is an article that explains [how you can find out](https://bytearcher.com/articles/how-to-check-if-node-implements-es6-language-feature/).</p>

## CSS/Sass

*   Toggling passwords is considered a great UX pattern for users. On the other hand, there are some risks and challenges that you should know of. [Avoid caching of the passwords and disabling autofill managers](https://codepen.io/shellbryson/post/toggle-passwords) by following this short article.
*   Adam Morse shares his experience with user testing web projects and [sums up what he thinks about using web fonts](https://mrmrs.io/writing/2016/03/17/webfonts/) in the context of providing a good user experience. I have to admit that while it can be cool and necessary to use a web font, it often doesn’t have to be. A lot of projects don’t care about using a proper fallback font that matches the web font — and these days, with content and privacy blockers available for every device, there are a lot of people not seeing any web fonts at all.</p>

## Work & Life

*   Casey Gerald gave a great [talk at this year’s SXSW](https://www.entrepreneur.com/article/272389) questioning the traditional approach of doing work and also asking the question “With all the power we hold in our hands, why are people still suffering?”
*   One year after being fired, Zach Holman wrote up his [knowledge on firing people](https://zachholman.com/talk/firing-people). A great read for both employees and employers.
*   “Most offices are the average of what works for everyone,” says Mike Del Ponte who believes that [companies should offer employees the best of both worlds](https://www.fastcompany.com/3057608/most-creative-people/why-your-company-should-do-a-work-from-anywhere-week) — working remote and on-site — and give them the choice of both. We’ve already seen a lot of such articles but what I found particularly interesting here is that the article is talking about benefits of on-site work as well as remote work and puts both into perspective.

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</p>

<em>Thanks and all the best,
Anselm</em>


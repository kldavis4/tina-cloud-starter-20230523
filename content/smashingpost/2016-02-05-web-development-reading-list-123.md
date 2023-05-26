---
title: 'Web Dev Reading List #123'
slug: web-development-reading-list-123
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f2e8ca4-0844-46fa-ab04-9e1541068094/apple-san-francisco-1.png
date: 2016-02-05T20:16:03.000Z
author: anselm-hannemann
description: >-
  This week I mostly spent time on fixing bugs, improving a deployment workflow
  and on getting another new front-end project structured. One major takeaway
  from this was that **it’s good to have a proper deployment workflow** in place
  already in the early stages of a project.

  To document appropriately in git what has been done in a commit instead of
  sleazily writing “changed [XY] because of [some arbitrary reason]”. By doing
  so, it becomes easier for myself, or someone else, to identify bugs at a later
  stage.
categories:
  - Web Development Reading List
---
This week I mostly spent time on fixing bugs, improving a deployment workflow and on getting another new front-end project structured. One major takeaway from this was that <strong>it’s good to have a proper deployment workflow</strong> in place already in the early stages of a project.

We should document appropriately in git what has been done in a commit instead of sleazily writing “changed [XY] because of [some arbitrary reason]”. By doing so, it becomes easier for myself, or someone else, to identify bugs at a later stage.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [40+ Excellent Freefonts For Professional Design](https://www.smashingmagazine.com/2007/11/40-excellent-freefonts-for-professional-design-2/)
*   [Typographic Design Patterns And Best Practices](https://www.smashingmagazine.com/2009/08/typographic-design-survey-best-practices-from-the-best-blogs/)
*   [Industrial-Strength Types](https://www.smashingmagazine.com/2012/11/industrial-strength-types/)
*   [When Typography Speaks Louder Than Words](https://www.smashingmagazine.com/2012/04/when-typography-speaks-louder-than-words/)

## News

*   [Opera 35 has been released](https://dev.opera.com/blog/opera-35/) and brings CSS Font Loading API improvements, Fetch API `data:` and `blob:` URL scheme support, `Touch` and `TouchEvent` constructors.
*   So Facebook [will shut down Parse at the end of the year](https://medium.com/@burkeholland/facebook-is-creating-a-house-of-cards-33ce47144154) and Burke Holland explains why the company basically builds a house of cards. Of course, Facebook is not the only one, and Firebase or Heroku are building a similar lock-in we shouldn’t rely on with our products.</p>

## General

*   [What could be simpler than returning HTTP status codes?](https://racksburg.com/choosing-an-http-status-code/) Yet, we often do not care about returning the correct code, although it would massively improve the quality of your web application or website. There is a great specification for common statuses available for HTTP, and you should make use of it to help users, browsers and third-party crawlers identify the status of web content.</p>

## Concepts & Design

*   Stephanie Briones shares lessons learned and concepts on [how to redesign an interactive editor](https://blog.invisionapp.com/redesigning-interactive-editor/).
*   Nick Keppol shares some insights on [why Apple built its new font family San Francisco](https://medium.com/martiancraft-s-syndicate/why-san-francisco-b86bd45f3273). A lovely, comprehensive post from which we can learn a lot about specific typographic details.

{{% feature-panel %}}

<figure class="fwi"><a href="https://medium.com/martiancraft-s-syndicate/why-san-francisco-b86bd45f3273"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f2e8ca4-0844-46fa-ab04-9e1541068094/apple-san-francisco-1.png" alt="Nick Keppol’s post about Apple’s new font family San Francisco teaches a lot about specific typographic details" /></a><figcaption>Nick Keppol’s <a href="https://medium.com/martiancraft-s-syndicate/why-san-francisco-b86bd45f3273">post about Apple’s new San Francisco font family</a> contains a lot of valuable insights into typographic details.</figcaption></figure>

## Tools

*   Most of us are using git on a daily basis. However, we often use it not in the way it’s intended to be. When you try to trace back a bug (`git bisect`, `git log`) or want to create release notes, [it’s crucial to have meaningful and well written commit messages](https://alistapart.com/article/the-art-of-the-commit).</p>

## Security

*   Diogo Mónica explores how to [apply sane defaults for a Content Security Policy](https://diogomonica.com/2015/12/30/creating-a-csp-policy-from-scratch/) on your website and shares why it’s a bad idea to allow inline scripts.</p>

## Accessibility

*   Léonie Watson collected the [basic commands to use and control the most common screen readers](https://www.paciellogroup.com/blog/2015/01/basic-screen-reader-commands-for-accessibility-testing/) (including the OS X built-in Voice Over) so that everyone can test websites for accessibility compatibility.
*   This page contains [standard elements for a normal website](https://www.html5accessibility.com/html5elements/) with accessibility defaults. If you build such projects, have a look at the source code and apply it next time.</p>

## JavaScript

*   Lately, there’s a lot to read about functional programming in JavaScript. [Elm](https://elm-lang.org/) claims to help us with functional programming and Dennis Reimann now wrote up a [step-by-step guide on how to get started with Elm](https://dennisreimann.de/articles/elm.html) and functional front-end development.
*   [Feature.js](https://featurejs.com/) is a fast, simple and light­weight browser feature detection library. It has no dependencies and weighs only 1kb minified and gzipped. It automatically initializes itself on page load, so you don’t have to. However, what it doesn’t do is run tests while initializing. It will only run them when you ask it to.
*   No, not another ES2015/2016 article. This one, however, is a great primer on [how to build modules in JavaScript](https://medium.freecodecamp.com/javascript-modules-a-beginner-s-guide-783f7d7a5fcc). You can use its approach without a tooling library like Babel, but if you want to know how it’s done in ES2015, the article has got you covered, too.

<figure class="fwi"><a href="https://medium.freecodecamp.com/javascript-modules-a-beginner-s-guide-783f7d7a5fcc"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0ec191b-5d7f-4658-87f1-d00bb2957870/javascript-modules-opt.png" alt="Writing JavaScript modules" /></a><figcaption>Preethi Kasireddy has written a <a href="https://medium.freecodecamp.com/javascript-modules-a-beginner-s-guide-783f7d7a5fcc">great primer on how to build modules in JavaScript</a>. Image credit: <a href="https://www.flickr.com/photos/qubodup/16258492451">Iwan Gabovitch</a></figcaption></figure>

## CSS / Sass

*   Speaking of good practice for writing CSS, fantasai from the CSSWG shares what we should focus on and which [aspects to take care of when we write CSS](https://fantasai.inkedblade.net/style/talks/best-practices/).
*   [BigCommerce shares their approach on structuring CSS](https://www.bigeng.io/how-we-css-at-bigcommerce/). A sane and simple process.
*   I’ve rarely seen basic CSS articles lately, but this one is just great: Thierry Koblentz re-analyzes our commonly used old `display: table` clearfix method and shares [how we can achieve a solid clearfix method for modern browsers in a cleaner way](https://cssmojo.com/the-very-latest-clearfix-reloaded/).</p>

## Work & Life

*   A Navy SEAL held a speech at a university and told the students [how we can change something in the world](https://www.farnamstreetblog.stfi.re/2014/05/10-life-lessons-william-mcraven/) if we change our mindset.</p>

## Going beyond…

*   As Silicon Valley firms hail the benefits of disruption, some [European leaders are pushing to develop the industry’s moral compass](https://www.theguardian.com/technology/2016/jan/30/europe-google-facebook-technology-ethics-eu-martin-schulz). This is a real chance to make better decisions, fight fatalism and build a humane future.

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via E-Mail, RSS and online.

<em>Thanks and all the best,
Anselm</em>


---
title: 'Monthly Web Development Update 5/2019: Over-Complication And Performative Workaholism'
slug: monthly-web-development-update-5-2019
author: anselm-hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4141162d-b209-431b-aecc-d236657356e0/internet-health-report-opt.png
date: 2019-05-17T14:24:00+02:00
summary: >-
  This new edition of the Monthly Web Development Update takes a look at what moves the web and the people working on it. From browser updates and handy tools to how we do work.
description: >-
  This new edition of the Monthly Web Development Update takes a look at what moves the web and the people working on it. From browser updates and handy tools to how we do work.
categories:
  - Web Development Reading List
---
This week, I was at the amazing [beyondtellerrand conference](https://beyondtellerrand.com/events/duesseldorf-2019/speakers) once again, and every single time I come home from such an event, I try to understand our industry and our society better. There’s so much **input and inspiration** around, I meet a lot of friends and [people I see only once a year](https://tobiastom.name/articles/digital-loneliness), I listen to great talks. People tell me how frustrated they are with their jobs, we hear amazing stories of people who seem to have an amazing life, we hear people moaning about bad players on the web, but rarely do we hear real insights or solutions.

Presentations highlighting the good parts and uncommon paths in life are quite rare, but one of the exceptions is [Rob Draper’s beyondtellerand talk](https://beyondtellerrand.com/events/duesseldorf-2019/speakers/rob-draper#talk) in which he shares his story and how an unexpected series of events created the role he is in today. And, well, I’m glad that there are amazing people who believe in humans and share how we all as individuals can do something to have a better job and life: It might be as Stephen Hay suggests to [trust your own ideas](https://vimeo.com/336085876), building [your own website and social system](https://vimeo.com/336343886), or, as my good friend Andy is doing it, building [a non-profit initiative to build schools in Africa](https://makuyuni.org/support?ref=wdrl.info), a project into which he invests not only a lot of time but money as well.

It’s great to see these visions of a better world, and it feels like a good community to be in. **The web is so much more** than just a space to build technical solutions and write code; it’s a place to create helpful, meaningful, and beautiful individual things.

{{% feature-panel %}}

## News

- Let’s make things official: [Safari 12.1 now supports Dark Mode](https://webkit.org/blog/8840/dark-mode-support-in-webkit/). Check the full article for how to apply it to your pages or take a look at one of the sites like Twitter or [Colloq](https://colloq.io/) that already support it. Safari’s Developer Tools feature a [debug mode for Dark Mode](https://webkit.org/blog/8892/dark-mode-in-web-inspector/) now as well.
- [Chrome 74 is public](https://developers.google.com/web/updates/2019/04/nic74). The new version lets us detect if a user requested reduced motion and the Feature Policy API got updates, too, so now we can request `document.featurePolicy.allowedFeatures()` for all allowed features, `allowsFeature()` for single features, or `document.featurePolicy.getAllowlistForFeature()` for a domain list that gets the allowed features.
- [Googlebot is evergreen now](https://webmasters.googleblog.com/2019/05/the-new-evergreen-googlebot.html). This means that Google’s search crawler gets the newest Chromium version automatically. From now on, it supports ES6, ECMAScript Modules and newer functionality and understands lazy-loaded content via IntersectionObserver and the WebComponents v1 APIs. It might be time to drop our ES6 transpilers soon.
- The Web Share API is a nice addition to make more use of websites. And while it has been available on Chrome for Android for quite some time now, [Safari is bringing the feature to macOS and iOS](https://webplatform.news/issues/2019-05-10#safari-brings-web-share-to-desktop) in its latest version.

## General

- Stefan Judis shares a roundup article on how to keep the web a safe place, making it affordable and fast and tailoring the response to the user — [all with HTTP headers](https://www.twilio.com/blog/a-http-headers-for-the-responsible-developer). A good read for everybody as we all tend to forget about these things in our daily work.
- The annual [Mozilla 2019 Internet Health Report](https://blog.mozilla.org/blog/2019/04/23/its-complicated-mozillas-2019-internet-health-report/) examines how humanity and the internet intersect. Here’s [the report itself](https://internethealthreport.org/2019/) with some short answers for those who don’t want to read it completely.
- On-call rotation is a common thing in tech, and I know that a lot of teams struggle with it. That’s why I found this guide on “[On-call at any size](https://increment.com/on-call/on-call-at-any-size/)” quite informative and useful. It explains how to prepare and what to do — no matter if you’re a small team or part of a big corporation.
- Emily Shaffer shares [how to annotate regular expressions](https://nasamuffin.github.io/regex/documentation/2019/05/08/documenting-regex.html) to make them comprehensible for others as well.

{{< rimg href="https://internethealthreport.org/2019/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4141162d-b209-431b-aecc-d236657356e0/internet-health-report-opt.png" sizes="100vw" caption="If there were only 100 people in the world, who would be online? That’s only one of the questions which Mozilla’s <a href='https://internethealthreport.org/2019/'>Internet Health Report 2019</a> answers. (<a href='https://internethealthreport.org/2019/'>Image credit</a>)" alt="Stick figures showing how many people are online and how many offline in which part of the world. Most people who are online come from Asian and Pacific countries, followed by the Americas." >}}

## UI/UX

- A pretty good crossover app that deserves a highlight here: [Concepts app](https://concepts.app/en/) is a super-flexible sketching, drawing, planning app for creating concepts and digital ideas.
- Patrick Faller explains [how to reverse over-complication in product design](https://medium.com/@patfaller/google-ux-designer-david-hogue-shares-how-to-reverse-over-complication-in-product-design-and-how-90c00bcad5d7).

{{< rimg href="https://medium.com/@patfaller/google-ux-designer-david-hogue-shares-how-to-reverse-over-complication-in-product-design-and-how-90c00bcad5d7" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0855b07e-d844-459f-9323-5c64dd49c503/over-complication-opt.png" sizes="100vw" caption="How do you fix the UX of a product that has become overly complicated? Patrick Faller shows <a href='https://medium.com/@patfaller/google-ux-designer-david-hogue-shares-how-to-reverse-over-complication-in-product-design-and-how-90c00bcad5d7'>paths to simplification</a>. (<a href='https://medium.com/@patfaller/google-ux-designer-david-hogue-shares-how-to-reverse-over-complication-in-product-design-and-how-90c00bcad5d7'>Image credit</a>)" alt="Paths to simplification illustrated with circles and arrows. Subtract, Consolidate, Redistribute, Prioritize, Clarify." >}}

## Tooling

- GitHub is completing the experience by [integrating their own npm registry](https://github.com/features/package-registry) (but also ruby, Docker, Maven, NuGet) into the platform. This is a huge step as it makes publishing custom and private packages a lot easier.

## Privacy

- As web developers, we know how to inspect which third parties and trackers are included in a website. However, it’s very different when it comes to applications. [Blocking ads or privacy-invading tracking mechanisms in a desktop or mobile app](https://tobiastom.name/notes/4e556692) is hard, and it’s even harder to notice the tracking at all. Let’s raise awareness for this and build software that doesn’t betray the users.

## Security

- The Google AMP project announced that they’re going to [“simplify” AMP domains in Google Chrome](https://twitter.com/AMPhtml/status/1118318585678577664). This means that users would see the original URL in the browser bar while really being on a Google AMP server. An interesting approach, given the fact that this is something that browser vendors usually don’t allow in order to prevent URL spoofing.

## Accessibility

- [stylelint-a11y](https://github.com/YozhikM/stylelint-a11y) is a plugin for stylelint that enforces accessibility best practices via the CSS linter.

## JavaScript

- You never fully understood the MutationObserver API? [Here’s the guide to make sense of it](https://www.smashingmagazine.com/2019/04/mutationobserver-api-guide/).

## CSS

- Andy Clarke shows us how we can do art direction and create [more elaborate layouts on the web using CSS shapes](https://www.smashingmagazine.com/2019/04/art-direction-for-the-web-using-css-shapes/).

{{% ad-panel-leaderboard %}}

## Work &amp; Life

- How do [productivity and promises](https://shawnblanc.net/2019/04/productivity-and-promises/) correlate? In times of constant demands, too much work to do, and blurry information about priorities and different senses of urgency, you can hardly blame people for breaking with their promises anymore. If we’re constantly confronted with other people’s expectations like “please get back to me by 1 PM today”, how can we stick to our original schedule for the day and be productive? Should we ignore such external demands and say “we had better things to do” than replying to the non-urgent but urgency-creating email “in time”? It definitely takes some courage to do so, but in the end, this is what productivity is about: sticking to a schedule and dedicating focus time to one single task.
- [When did performative workaholism become a lifestyle?](https://www.nytimes.com/2019/01/26/business/against-hustle-culture-rise-and-grind-tgim.html) The New York Times takes a closer at the culture of business, hustling, and the weird love we develop for working faster and more. But what about our lives when we work for 12 or 18 hours a day? And what about that promise that automation will take off the work from us?
- Do you do standup calls? Here’s [why this is a costly thing](https://m.signalvnoise.com/status-meetings-are-the-scourge/) that even hurts your teammates’ efficiency.
- “[Stop being so busy and just do nothing. Trust us.](https://www.nytimes.com/2019/04/29/smarter-living/the-case-for-doing-nothing.html)” This claim in the New York Times has its reasons: In a world of stress and an environment where we embrace working all day, we need to remember to stop and take time for ourselves.
- We love to tend to make judgments about other people’s work. That’s why we tend to declare something as “low-hanging fruit,” assuming that the task is easy to do and doesn’t take much time or effort. But we forget that we might miss a couple of circumstances and it might become a bigger task than anticipated. Jason Fried says that [we should be careful when we use the word “easy” to describe other people’s jobs](https://m.signalvnoise.com/the-myth-of-low-hanging-fruit/).
- The founder of ConvertKit, Nathan Barry, shares a couple of insights into [how they run the business in an unconventional way](https://nathanbarry.com/unconventional/): They pay standardized salaries, make their revenue public, and distribute 60% of company profits to the team.

{{< rimg href="https://www.nytimes.com/2019/01/26/business/against-hustle-culture-rise-and-grind-tgim.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30137ddf-695e-4157-89c2-f30f4d03d034/hustle-opt.png" sizes="100vw" caption="<a href='https://www.nytimes.com/2019/01/26/business/against-hustle-culture-rise-and-grind-tgim.html'>When did performative workaholism become a lifestyle?</a> The New York Times dedicated an article to the topic. (<a href='https://www.nytimes.com/2019/01/26/business/against-hustle-culture-rise-and-grind-tgim.html'>Image credit</a>)" alt="Screenshot from the New York Times article ‘Why are young people pretending to love work’. Under the heading, there’s a propaganda-poster style illustration of three young people holding laptops, phones, and tablets, making a fist with their right hand. The background of the poster says ‘Hustle’." >}}

## Going Beyond…

- “If anything about this age is rare, perhaps it is the possibility that our fraught networked systems have finally reached such a unique point, with their environmental and social consequences so visibly intertwined, that they have become impossible to ignore.” — Ingrid Burrington in “[A rare and toxic age](https://increment.com/energy-environment/a-rare-and-toxic-age/).”
- [Let’s hand over the best possible](https://helloanselm.com/writings/handover-the-best). The best environment for the next generation. The best work for the employees that take over work from you. Keep it at heart for every aspect of life, and you’ll see that it makes a difference. To other people and to you. It feels good to do good.
- What’s low-tech, sustainable, and possibly the most effective thing we can do to fight climate change? [Planting trees. A trillion of them.](https://edition.cnn.com/2019/04/17/world/trillion-trees-climate-change-intl-scn/index.html)
- What are we doing to our earth? It seems despite the rising awareness of plastic pollution, [global sales of plastic and glass bottles, cans, and cartons are still rising](https://www.theguardian.com/environment/2019/may/09/runaway-consumption-2tn-drinks-containers-being-used-every-year). There are so many alternatives, can we please stop buying one-time plastic packaging and coffee to-go — each of us, now?
- When we feel overloaded, we tend to lash out at someone in frustration and anger. This comes from the hope that things will be calm, orderly, simple, solid, and under control. However, the world doesn’t comply with this hope, as it is chaotic, constantly changing, never fixed, groundless. So we get anxious and angry at others. But we can [create a habit of calm when feeling frustrated](https://zenhabits.net/frustrating/).
- [What energy impact does your phone, that small screen you hold in your hands every day, have](https://increment.com/energy-environment/the-secret-energy-impact-of-your-phone/)? We use video calls, messengers, or upload our photos to the cloud. But all the cloud services, the 4G network itself use a huge amount of energy that we tend to forget about. This article dives deeper into the dependencies of using a smartphone these days, and why it matters to save data and reduce your phone usage — and if it’s just for your own sake.

One more thing: If you like my reading lists, please consider [making a donation](https://wdrl.info/donate). [Donating to Makuyuni](https://makuyuni.org/support?ref=wdrl.info) counts as well.

*—Anselm*

{{< signature "cm" >}}
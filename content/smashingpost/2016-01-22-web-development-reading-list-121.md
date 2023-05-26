---
title: >-
  'Web Development Reading List #121: The Illusion Of Completeness, Client Hints,
  CSS Subgrids'
slug: web-development-reading-list-121
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cab649a-8fc6-4364-a166-3bc80c4bf8a7/anatomy-of-a-web-app-attack-opt.png'
date: 2016-01-22T20:12:08.000Z
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
Over the last two weeks, I had the chance to review about **eighty job applications for a front&ndash;end position**. The position requires strong JavaScript knowledge, but it also requires HTML and CSS. And here’s a thing: nearly no one could show off substantial markup skills, not to talk about accessibility.

Although I only had the chance to review their personal websites or GitHub profiles and this might of course not be a full show&ndash;off of their knowledge, it assured my lately developed opinion on web developers. Many are not able to choose the right HTML elements, to explain why and how a `clearfix` works, or what ARIA roles are for, but they can use React and Angular. If you got some spare time over the next weeks, [learn semantics](https://www.smashingmagazine.com/2011/11/html5-semantics/) and re&ndash;read the basics (or specs if you like the challenge) of HTML and CSS from time to time.

## General

*   There’s a lot of discussion currently about the web getting too complex, and some even claim the web is broken. Remy Sharp instead [has a different view](https://remysharp.com/2016/01/20/why-i-love-working-with-the-web) on the new technologies, options we have today and how we can use them together with our base technology from 25 years ago. The article is best described by Remy’s own words: “Why I love working with the web”.

{{% feature-panel %}}

## Concepts & Design

*   [Overpass](https://overpassfont.org/) is a new open source web font family inspired by Highway Gothic, looking fresh and solid.
*   Kim Flaherty examines [the user’s illusion of completeness on websites](https://www.nngroup.com/articles/illusion-of-completeness/) and explains why it’s important to clearly show a user that additional content exists off&ndash;screen.

## Security

*   Jack Leonard from Barricade, a security service provider, explains with a very nice infographic how an attack to a web app works today. In another post he also describes how you can develop for security.
*   As a follow&ndash;up to my recent article on [being careful when choosing a third party to handle your HTTPS](https://helloanselm.com/2016/choose-your-own-https/), Robin Rendle [interviewed me for CSS&ndash;Tricks](https://css-tricks.com/interview-web-security/). In the interview, I give a deeper insight and some more practical advice and background on the topic.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cab649a-8fc6-4364-a166-3bc80c4bf8a7/anatomy-of-a-web-app-attack-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cab649a-8fc6-4364-a166-3bc80c4bf8a7/anatomy-of-a-web-app-attack-opt.png" width="500" height="326" alt="The anatomy of a web app attack" /><figcaption>Jack Leonard’s infographic explains the anatomy of a web app attack.</figcaption></figure>

## Web Performance

*   Because a `<picture>`&ndash;element can get really bloated when you provide a lot of resolutions and image sources, Jon Arne Sæterås explains [how to use Client Hints for a leaner, more automated approach to serve responsive images](https://www.smashingmagazine.com/2016/01/leaner-responsive-images-client-hints/). The only issue here is that you need a server to support it and that not all browsers support Client Hints at the moment, so you need to find a smart fallback for those.
*   This [amazing guide](https://surma.link/things/h2setup/) gives you a full introduction into how to set up HTTP/2 from scratch &mdash; including the required TLS certificate and server configurations needed.

{{% ad-panel-leaderboard %}}

## Accessibility

*   [pa11y](https://pa11y.org/) is your new best friend if you want to have automated accessibility testing. It monitors your website and reports accessibility issues. In that, it is similar to [Tenon](https://tenon.io/), a commercial SaaS alternative that you don’t need to set up and maintain on your own.

<figure><a href="https://pa11y.org/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b15d8372-d0e1-4cab-8262-c4349cefd18f/pa11y-opt.png" width="500" height="274" alt="pa11y, automated accessibility testing" /></a><figcaption><a href="https://pa11y.org/">pa11y</a>, your new best friend when it comes to automated accessibility testing.</figcaption></figure>

## JavaScript

*   Ada Rose Edwards shares how she writes modern ES6 JavaScript code and why she follows the approach to “use `const` by default, `let` only where it is required and `var` to identify code which needs to be refactored”.
*   Since years we use `console` in our code all the time to debug our applications. Finally, the WHATWG created [a specification that standardizes APIs for console debugging facilities](https://console.spec.whatwg.org/).
*   This [neat trick for CSS object&ndash;fit fallback on Edge (and other browsers)](https://medium.com/@primozcigler/neat-trick-for-css-object-fit-fallback-on-edge-and-other-browsers-afbc53bbb2c3) by Primož Cigler explains how you can build an easy, basic fallback for IE11 and MS Edge for `object-fit`. Actually, as my own [polyfill](https://github.com/anselmh/object-fit/) for this is non&ndash;functional in Edge, this is a great way to add support for it. And if you really love the property, [let Microsoft know with your vote](https://wpdev.uservoice.com/forums/257854-microsoft-edge-developer/suggestions/6263790-object-fit-and-object-position).
*   This short guidance article gives you some of the best resources on [how to learn ES6](https://medium.com/javascript-scene/how-to-learn-es6-47d9a1ac2620).

## CSS / Sass

*   Eric Meyer wrote about why CSS grid layouts are such a great thing for us developers but also noted why [they will utterly fail if browsers ship them without providing support for subgrids](https://meyerweb.com/eric/thoughts/2016/01/15/subgrids-considered-essential/).
*   Alex Sharp explains why Facebook created a solution to write CSS in JavaScript and concludes [why you should avoid following this approach at all cost](https://medium.com/@ajsharp/please-please-don-t-use-css-in-js-ffeae26f20f).

{{% ad-panel-leaderboard %}}

## Work & Life

*   After reviewing a lot of applications in the past days, I can only agree with Kristian Glass here and say: “[If you get the chance, always send a cover letter](https://blog.doismellburning.co.uk/cover-letters-always-send-one/)”. It’s your opportunity to say something about yourself and make clear why you apply for the job.

## Going beyond…

*   We have an ongoing problem with growing inequality around the world and a few super rich people (latest numbers say it’s down to 65) have as much money as the poorest 3.5 billion people. If we don’t change anything and do not oblige people to [pay their taxes in their own countries](https://www.aljazeera.com/indepth/opinion/2016/01/world-inequality-countdown-160118072153499.html) or [reject trickle-down economics](https://www.oxfam.org/en/pressroom/reactions/oxfam-applauds-world-banks-rejection-trickle-down-economics-and-recognition-huge) as the World Bank officially declared just recently, this system will break and our own lives are likely to be affected.

And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via e&ndash;mail, RSS and online.

*Thanks and all the best,
Anselm*

### Further Reading on Smashing Magazine:

*   “[Mind Your En And Em Dashes: Typographic Etiquette](https://www.smashingmagazine.com/2011/08/mind-your-en-and-em-dashes-typographic-etiquette/),” David Kadavy
*   “[Macrotypography For A More Readable Web Page](https://www.smashingmagazine.com/2012/05/applying-macrotypography-for-readable-web-page/),” Nathan Ford
*   “[How To Choose A Typeface &mdash; A Step-By-Step Guide!](https://www.smashingmagazine.com/2011/03/how-to-choose-a-typeface/),” Douglas Bonneville
*   “[Respect Thy Typography](https://www.smashingmagazine.com/2012/03/respect-thy-typography/),” Espen Brunborg

{{< signature "nl" >}}
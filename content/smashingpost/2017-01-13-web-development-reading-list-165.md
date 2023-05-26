---
title: >-
  Web Development Reading List #165: Starting The New Year With Browser News,
  Container Architecture, And React “Aha” Moments
slug: web-development-reading-list-165
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac6be872-99c5-4019-831f-0f84394fb1d8/wdrl-165-opt.png'
date: 2017-01-13T21:26:46.000Z
author: anselm-hannemann
description: >-
  Happy new year! I hope you had a good start and can **feel positive about what
  2017 might bring**. As mentioned in the last edition of the past year, I don’t
  like New Year’s resolutions too much, but I’d like to point you to something
  that [Marc Thiele wishes for this year](https://marcthiele.com/notes/think):

  “So my wish then also is, that you reflect and ask yourself, if you want to
  post the text or maybe even just have another, a second look on the text you
  are about to post. Maybe you decide, that you don’t post it. Maybe this helps,
  that less negative posts and emotions are spread.”
categories:
  - Web Development Reading List
  - Web Development
  - Web Development Reading List
---
<blockquote>
<p>“So my wish then also is, that you reflect and ask yourself, if you want to post the text or maybe even just have another, a second look on the text you are about to post. Maybe you decide, that you don’t post it. Maybe this helps, that less negative posts and emotions are spread.”</p>
</blockquote>

By the way, to recall the most important milestones that the web has gone through in the past twelve months, you can visit the [Almanac 2016](https://wdrl.info/almanac/2016). It’s a yearbook that sums up all the 47 editions of past year’s Web Development Reading Lists.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Don’t Get Lost In Translation: How To Conduct Website Localization](https://www.smashingmagazine.com/2014/12/how-to-conduct-website-localization/)
*   [You, Me And The Emoji: Character Sets, Encoding And Emoji](https://www.smashingmagazine.com/2016/11/character-sets-encoding-emoji/)
*   [How To Design A Better Mobile Checkout Process](https://www.smashingmagazine.com/2013/03/designing-a-better-mobile-checkout-process/)
*   [Quick UX Prototyping With Adobe XD Shortcuts (PDF Cheat Sheet)](https://www.smashingmagazine.com/2016/07/quick-ux-prototyping-with-adobe-xd-shortcuts-pdf-cheatsheet/)

## News

*   Firefox 52 is scheduled for March 7th this year, and it will bring [better font fingerprinting protection](https://www.ghacks.net/2016/12/28/firefox-52-better-font-fingerprinting-protection/). This means that when checking for system fonts, Firefox will only return the fonts that you have whitelisted instead of returning all fonts installed on the operating system.
*   The Windows 10 build 15002 comes with [a new Microsoft Edge release](https://developer.microsoft.com/en-us/microsoft-edge/platform/changelog/desktop/15002/). It includes a number of improvements such as a preview of the Web Payments API, Flash content is now blocked by default, TCP Fast Open is now default, too, and support for Content-Security-Policy 2.0 and the WebVR API have also been added.
*   Do you remember or even use the font “Source Serif”? [Version 2](https://blog.typekit.com/2017/01/10/introducing-source-serif-2-0/) is a major step forward. The character set was upgraded from Adobe Latin 3 to Adobe Latin 4 which means nearly double the number of characters and broader language support. The existing characters also got updates and now look even better. Last but not least, [Source Serif 2 is completely open- source](https://github.com/adobe-fonts/source-serif-pro) under the SIL Open Font License.

{{% feature-panel %}}

<figure><a href="https://blog.typekit.com/2017/01/10/introducing-source-serif-2-0/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86e34563-76e6-4a6c-9b81-cdfc156047fe/source-serif-800w-opt.png" width="800" height="511" alt="Source Serif" /></a><figcaption>The open-source font <a href="https://blog.typekit.com/2017/01/10/introducing-source-serif-2-0/">Source Serif</a> got an update and now supports more languages than ever. (<a href="https://blog.typekit.com/2017/01/10/introducing-source-serif-2-0/">Image credit</a>)</figcaption></figure>

## General

*   “As we move our code to CodePen, our writing to Medium, our photographs to Instagram we don’t just run the risk of losing that content and the associated metadata if those services vanish. We also lose our own place to experiment and add personality to that content, in the context of our own home on the web.” — Rachel Andrew in “[It’s more than just the words](https://rachelandrew.co.uk/archives/2017/01/05/its-more-than-just-the-words/)”.
*   In her “[Guide to 2017 Conferences](https://css-tricks.com/guide-2017-conferences/)”, Sarah Drasner collected a vast selection of web design related events that’ll take place this year. If you can, talk to your boss, select the event(s) you like most and attend them if possible.
*   John Saito shares his thoughts on the importance of [designing for internationalization](https://medium.com/dropbox-design/design-for-internationalization-24c12ea6b38f).
*   Chen Hui Jing gives insights into the world of [East Asian character emojis](https://www.chenhuijing.com/blog/east-asian-character-emojis/). For Western people like me, this is an interesting exploration into foreign languages and how emojis can be different around the world. ㊗️, for example, is a Kanji character meaning “congratulations”.</p>

## Concept & Design

*   [Open Color](https://yeun.github.io/open-color/) is an open-source color scheme optimized for UI design.
*   Christian Holst wrote an insightful article about [the importance of ‘Credit Card Number’ fields allowing and auto-formating spaces](https://baymard.com/blog/credit-card-field-auto-format-spaces). Unfortunately, about 80% of e-commerce sites currently don’t do that. Let’s try to improve this.
*   Various authors have taken the effort to create [new designs for The New York Times](https://www.behance.net/gallery/47160365/The-New-York-Times-Redesign). Their Behance gallery is quite good for inspiration and understanding editorial design patterns.

<figure><a href="https://www.behance.net/gallery/47160365/The-New-York-Times-Redesign"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eefa48b3-08b6-4ec1-b4a2-0110579d1dde/new-york-times-redesign-800w-opt.png" width="800" height="517" alt="The New York Times Redesign" /></a><figcaption>Slava Kornilov and Bohdan Kononets’ <a href="https://www.behance.net/gallery/47160365/The-New-York-Times-Redesign">concept for a redesign of the New York Times</a> gives valuable insights into editorial design patterns. (<a href="https://www.behance.net/gallery/47160365/The-New-York-Times-Redesign">Image credit</a>)</figcaption></figure>

## Tools & Workflows

*   Ole Fredrik Lie shares his [thoughts about Adobe XD](https://medium.com/@olefredrik/adobe-xd-your-new-favorite-design-tool-f03e45ee3f3c) and why he thinks it’s a great tool with a lot of potential.
*   Eric Chiang [explains Container architecture from scratch](https://ericchiang.github.io/post/containers-from-scratch/) so you might finally be able to understand what all the container virtualization is about.
*   Harry Roberts shares a simple trick to [set up a git commit message template](https://mobile.twitter.com/csswizardry/status/819539972722200576). First, create a file `.git-commit-template` with the content (i.e. `[refs #0000] Subject line`) and save it to your project root. Then add `[commit] template = {pathtoyour .git-commit-template file}` to your `.gitconfig` file.
*   We all know how to host a Jekyll site on GitHub, but Chen Hui Jing now explores and documents what it takes to [host a Jekyll site on gitlab pages](https://www.chenhuijing.com/blog/hosting-static-site-gitlab-pages/).
*   Juho Vepsäläinen wrote [a book about Webpack](https://survivejs.com/webpack/introduction/). It’s available for free, but [to support the author, you can also buy the book](https://leanpub.com/survivejs-webpack). A great documentation of Webpack that offers a lot of insights into the tool.</p>

## Security

*   Rita Zhang from Microsoft explains how you can [set up your own L2TP/IPsec VPN Server on a Raspberry Pi](https://ritazh.com/setup-your-own-l2tp-vpn-server-with-raspberry-pi-170d3d4df04c), which can be useful to do in your home network so you’ll be able to connect to it when you’re traveling and using public WiFi.
*   If you have a MongoDB installation, [it’s now the time to check if it’s secure](https://www.mongodb.com/blog/post/how-to-avoid-a-malicious-attack-that-ransoms-your-data). Tim Kadlec from Snyk explains [why it’s important that tools provide and use secure defaults](https://snyk.io/blog/mongodb-hack-and-secure-defaults/) to protect users from attacks.</p>

## Privacy

*   [The current revision of the European Union ePrivacy law](https://www.theguardian.com/technology/2017/jan/10/whatsapp-facebook-google-privacy-rules-ec-european-directive) tries to protect communication confidentiality, block nonconsensual tracking, and lessen cookie warnings. A step in the right direction to make the web a safer, clearer place. For us developers it’s also great since the annoying cookie warnings are now questioned.

## Web Performance

*   Ian McKay from Netflix shares insights from [crafting a high-performance TV user interface with React](https://techblog.netflix.com/2017/01/crafting-high-performance-tv-user.html). A lot of valuable insights into the performance of React.js that everyone using the library should keep in mind.
*   Mattias Geniar explains why, due to hypervisor scheduling, [less CPUs are more](https://ma.ttias.be/virtual-environments-less-cpus/) in virtual environments.</p>

## HTML & SVG

*   Ire Aderinokun explains what you have to keep in mind to [create a valid document outline in HTML 5.1.](https://bitsofco.de/document-outlines-in-html-5-1/).</p>

## Accessibility

*   The W3C now has a web page that explains the [general principles of ARIA](https://w3c.github.io/aria-practices/examples/landmarks/).
*   Federal agency websites now need to [comply with Web Content Accessibility Guidelines 2.0 Levels A and AA](https://www.lexology.com/library/detail.aspx?g=e627e1be-eddf-44cb-9459-c8f72de48334&utm_term=&utm_content=buffer7c5a6&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer) as their accessibility standard and it’s expected that the Department of Justice will likely adopt this as the standard for public accommodations websites as well. Be prepared or, even better, comply early to save yourself trouble later.</p>

## JavaScript

*   Max Stoiber explores [what it takes a front-end developer to build their first Node.js microservice](https://mxstbr.blog/2017/01/your-first-node-microservice/).
*   Dr. Axel Rauschmayer on the [ECMAScript proposal `import()` that would enable dynamic loading of ECMAScript modules](https://www.2ality.com/2017/01/import-operator.html) (in contrary to the currently specified static ECMAScript modules).
*   The ESLint plugin [eslint-plugin-compat](https://github.com/amilajack/eslint-plugin-compat) checks the APIs used in your code for browser compatibility.
*   Tyler McGinnis shares his [React “Aha” moments](https://tylermcginnis.com/react-aha-moments/). A concise list that reminds us how we should write code when using React.

<figure><a href="https://tylermcginnis.com/react-aha-moments/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/572723a2-6c7f-4a55-9e8b-626eca90825b/react-aha-moments-800w-opt.png" width="800" height="573" alt="React Aha Moments" /></a><figcaption>Tyler McGinnies shares his <a href="https://tylermcginnis.com/react-aha-moments/">React “Aha” Moments</a>. (<a href="https://tylermcginnis.com/react-aha-moments/">Image credit</a>)</figcaption></figure>

## CSS/Sass

*   CSS is getting more and more flexible. With the [CSS Color Level 4 specification](https://drafts.csswg.org/css-color/#color-function), we will get a feature to define colors dynamically based on functions (e.g. such as `color(#eb8fa9 alpha(75%) blackness(20%));`) as [this article by Chris Coyier](https://css-tricks.com/colorme-css-color-level-4/) shows.</p>

## Work & Life

*   When you work remotely with a team, you will have conference calls from time to time. To make them successful and enjoyable for everyone, make sure to [follow Chris Heilmann’s tricks for conference calls](https://www.christianheilmann.com/2017/01/10/7-tricks-to-have-very-successful-conference-calls/): Be on time and stick to the duration, have a meeting agenda and stick to it, avoid unnecessary sounds.
*   Alex Duloz, the head behind [The Pastry Box project](https://the-pastry-box-project.net/), has started a new project. “[The Human In The Machine](https://superyesmore.com/publication/the-human-in-the-machine-a4064599cde2cb3397239e8d72219f48)” will be a 365 articles in one year project, about how humans define and deal with ‘productivity’.

## Going Beyond…

*   Julia Evans on [how to ask good questions](https://jvns.ca/blog/good-questions/). Some great considerations we should follow before asking questions to make communication more effective and generally better.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_


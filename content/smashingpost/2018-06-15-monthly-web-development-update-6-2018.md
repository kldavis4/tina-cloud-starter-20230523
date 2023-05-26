---
title: 'Monthly Web Development Update 6/2018: Complexity, DNS Over HTTPS, And Push Notifications'
slug: monthly-web-development-update-6-2018
author: anselm-hannemann
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9339f2fb-1c4e-45ce-a223-cf355564cbd2/dns-over-https-opt.png
date: 2018-06-15T12:32:58+02:00
summary: >-
  Anselm Hannemann summarized the most important things that happened in the web development world in the past four weeks so that you can easily catch up on everything that’s new.
description: >-
  Anselm Hannemann summarized the most important things that happened in the web development world in the past four weeks so that you can easily catch up on everything that’s new.
categories:
  - Web Development Reading List
---
<p>We see complexity in every corner of a web project these days. We’ve read quite a bunch of articles about how complex a specific technology has become, and we discuss this over and over again. Coming from a time where we uploaded websites via FTP and had no git or anything comparable, now living in a time where we have a build system, transpilers, frameworks, tests, and a CI even for the smallest projects, this is easy to understand. But on the other hand, web development has grown up so much in the past 15 years that <strong>we can’t really compare today to the past anymore</strong>. And while it might seem that some things were easier in the past, we neglect the advantages and countless possibilities we have today. When we didn’t write tests back then, well, we simply had no test — meaning no reliable way to test for success. When we had no deployment process, it was easy to upload a new version but just as easy to break something — and it happened a lot more than today when a Continuous Integration system is in place.</p>
<p>Jeffrey Zeldman wrote an interesting article on the matter: “<a href="https://alistapart.com/article/cult-of-the-complex">The Cult of Complex</a>” outlines how we lose ourselves in unnecessary details and often try to <strong>overthink problems</strong>. I like the challenge of building systems that are not too complex but show a decent amount of responsibility (when it comes to ethics, privacy, security, a great user experience, and performance) and are working reliably (tests, deployments, availability, and performance again). I guess the problem of finding the right balance won’t go away anytime soon. Complexity is everywhere — we just need to decide if it’s useful complexity or if it was added simply because it was easier or because we were over-engineering the original problem.</p>

## News
<ul>
<li>The upcoming Safari version 12 was unveiled at Apple’s WWDC. Here’s what’s new: icons in tabs, strong passwords, as well as a password generator control via HTML attributes including two-factor authentication control, a 3D and AR model viewer, the Fullscreen API on iPads, <code>font-display</code>, and, very important, <a href="https://webkit.org/blog/8311/intelligent-tracking-prevention-2-0/">Intelligent Tracking Prevention 2.0</a> which is more restrictive than ever and might have a significant impact on the functionality of existing websites.</li>
<li>The headless Chrome automation library <a href="https://pptr.dev/#?product=Puppeteer&amp;version=v1.5.0&amp;show=api-release-notes">Puppeteer</a> is now out in version 1.5. It brings along Browser contexts to isolate cookies and other data usually shared between pages, and Workers can now be used to interact with Web Workers, too.</li>
<li>Google released <a href="https://developers.google.com/web/updates/2018/05/lighthouse3">Lighthouse 3.0</a>, the third major version of their performance analyzation tool which features a new report interface, some scoring changes, a CSV export, and First Contentful Paint measurement.</li>
<li><a href="https://developers.google.com/web/updates/2018/05/nic67">Chrome 67 is here</a>, bringing Progressive Web Apps to the Desktop, as well as support for the Generic Sensor API, and extending the Credential Management API to support U2F authenticators via USB.</li>
<li>We’ve seen quite some changes in the browsers’ security interfaces over the past months. First, they emphasized sites that offer a secured connection (HTTPS). Then they decided to indicate insecure sites, and now Chrome announced new changes coming in fall that will make HTTPS the default by <a href="https://blog.chromium.org/2018/05/evolving-chromes-security-indicators.html">marking HTTP pages as “not secure”</a>.</li>
</ul>

<figure><a href="https://developers.google.com/web/updates/2018/05/nic67"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7f3d411-a402-4570-9ed0-6f6804a373e5/desktop-pwas-opt.png" width="800" height="533" alt="Desktop PWA in Chrome 67" /></a><figcaption><a href="https://developers.google.com/web/updates/2018/05/nic67">Desktop Progressive Web Apps are now supported in Chrome OS 67</a>, and the Chrome team already started working on support for Mac and Windows, too. (<a href="https://developers.google.com/web/updates/2018/05/nic67">Image credit</a>)</figcaption></figure>

## General
<ul>
<li>In “<a href="https://alistapart.com/article/cult-of-the-complex">The Cult of the Complex</a>”, Jeffrey Zeldman writes about how we often seem to forget that simplicity is the key and goal of everything we do, the overall goal for projects and life. He explains why it’s so hard to achieve and why it’s so much easier — and tempting — to cultivate complex systems. A very good read and definitely a piece I’ll add to <a href="https://wdrl.info/evergreen">my ‘evergreen’ list</a>.</li>
<li>Heydon Pickering shared a new, very interesting article that teaches us to build a web component properly: This time he explains <a href="https://inclusive-components.design/cards/">how to build an inclusive and responsive “Card” module</a>.</li>
</ul>

## UI/UX
<ul>
<li><a href="https://coolbackgrounds.io/">Cool Backgrounds</a> is a cool side project by Moe Amaya. It’s an online generator for polygonal backgrounds with gradients that can generate a lot of variants and shapes. Simply beautiful.</li>
</ul>

## Tooling
<ul>
<li>Ben Frain shares some useful <a href="https://benfrain.com/text-editing-techniques-every-front-end-developer-should-know/">text editing techniques</a> that are available in almost all modern code editors.</li>
</ul>

## Security
<ul>
<li>As security attacks via DNS gain popularity, DNS over HTTPS gets more and more important. Lin Clark <a href="https://hacks.mozilla.org/2018/05/a-cartoon-intro-to-dns-over-https/">explains the technology with a cartoon</a> to make it easier to understand.</li>
<li>Windows Edge is now <a href="https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/">previewing support for <code>same-site</code> cookies</a>. The attribute to lock down cookies even more is already available in Firefox and Chrome, so Safari is the only major browser that still needs to implement it, but I guess it’ll land in their Tech Preview builds very soon as well.</li>
</ul>

<figure><a href="https://hacks.mozilla.org/2018/05/a-cartoon-intro-to-dns-over-https/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9339f2fb-1c4e-45ce-a223-cf355564cbd2/dns-over-https-opt.png" width="800" height="294" alt="DNS Over HTTPS" /></a><figcaption>Lin Clark created a cartoon to explain how you can better protect your users’ privacy with <a href="https://hacks.mozilla.org/2018/05/a-cartoon-intro-to-dns-over-https/">DNS over HTTPS</a>. (<a href="https://hacks.mozilla.org/2018/05/a-cartoon-intro-to-dns-over-https/">Image credit</a>)</figcaption></figure>

## Privacy
<ul>
<li>The ACLU discovered that <a href="https://www.aclunc.org/blog/amazon-teams-law-enforcement-deploy-dangerous-new-face-recognition-technology">Amazon now officially teamed up with law enforcement</a> and provides a mass-face recognition technology that is already used in cities around the world.</li>
</ul>

## Web Performance
<ul>
<li>KeyCDN asked 15 people who know a lot about web performance to share their best advice with readers. Now they shared this article containing a lot of <a href="https://www.keycdn.com/blog/web-performance-advice-2018/">useful performance tips for 2018</a>, including a few words by myself.</li>
<li>Stefan Judis discovered that we can already <a href="https://twitter.com/stefanjudis/status/998682708753764352">preload ECMA Script modules in Chrome 66</a> by adding an HTML header tag <code>link rel="modulepreload"</code>.</li>
</ul>

## Accessibility
<ul>
<li>It’s relatively easy to build a loading spinner — for a Single Page Application during load, for example —, but we rarely think about making them accessible. Stuart Nelson now explains <a href="https://codeburst.io/how-to-create-a-simple-css-loading-spinner-make-it-accessible-e5c83c2e464c">how to do it</a>.</li>
<li>Paul Stanton shares <a href="https://medium.com/pulsar/which-accessibility-testing-tool-should-you-use-e5990e6ef0a">which accessibility tools we should use</a> to get the best results.</li>
</ul>

## JavaScript
<ul>
<li>JavaScript has lately been bullied by people who favor Elm, Rust, TypeScript, Babel or Dart. But <a href="https://medium.com/@WebReflection/js-is-not-worse-than-84a5fca0e87d">JavaScript is definitely not worse</a>, as Andrea Giammarchi explains with great examples. This article is also a great read for everyone who uses one of these other languages as it shows a couple of pitfalls that we should be aware of.</li>
<li>For a lot of projects, we want to use analytics or other scripts that collect personal information. With GDPR in effect, this got a lot harder. <a href="https://github.com/snipsco/yett">Yett</a> is a nice JavaScript tool that lets you block the execution of such resources until a user agrees to it.</li>
<li>Ryan Miller created a new publication called “The Frontendian”, and it features <a href="https://frontendian.co/cors">one of the best explanations and guides to CORS</a> I’ve come across so far.</li>
<li>The folks at Microsoft created a nice interactive demo page to show <a href="https://webpushdemo.azurewebsites.net/">what Web Push Notifications can and should look like</a>. If you haven’t gotten to grips with the technology yet, it’s a great primer to how it all works and how to build an interface that doesn’t disturb users.</li>
<li><a href="https://github.com/pqina/filepond">Filepond</a> is a JavaScript library for uploading files. It looks great and comes with a lot of adapters for React, Vue, Angular, and jQuery.</li>
<li><a href="https://reactjs.org/blog/2018/05/23/react-v-16-4.html">React 16.4 is out</a> and brings quite a feature to the library: Pointer Events. They’ll make it easier to deal with user interactions and have been requested for a long time already.</li>
</ul>

<figure><a href="https://webpushdemo.azurewebsites.net/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c49adead-79eb-4a16-a972-f7b15564c22c/web-push-opt.png" width="800" height="433" alt="The Frontendian" /></a><figcaption>Inspired by the parallels between basic astrological ideas and push notification architecture, the team at Microsoft explains <a href="https://webpushdemo.azurewebsites.net/">how to send push notifications to a user</a> without needing the browser or app to be opened. (<a href="https://webpushdemo.azurewebsites.net/">Image credit</a>)</figcaption></figure>

## CSS
<ul>
<li>Oliver Schöndorfer shares <a href="https://www.zeichenschatz.net/typografie/how-to-start-with-variable-fonts-on-the-web.html">how to start with variable fonts on the web</a> and how we can style them with CSS. A pretty complete summary of things you need to consider as well as possible pitfalls.</li>
<li>With the upcoming macOS Mojave supporting a ‘dark mode’, <a href="https://twitter.com/kkuldar/status/1006208146464002049">Safari will begin to automatically set the background color of websites to a black color</a> if no <code>background-color</code> is explicitly set. This is a great reminder that browsers can set and alter their default styles and that we need to set our site defaults carefully. I’m still hoping that the ‘dark mode’ will be exposed to a CSS Media Query so we can officially add support for it.</li>
<li>Rafaela Ferro shares how to <a href="https://medium.com/deemaze-software/css-grid-responsive-layouts-and-components-eee1badd5a2f">use CSS Grid to create a photo gallery that looks not only good but actually great</a>. This article has the answers to many questions I regularly get when talking about Grid layout.</li>
<li>Marcin Wichary explains how <a href="https://medium.com/@mwichary/dark-theme-in-a-day-3518dde2955a">we can create a dark theme in little time with modern CSS Custom Properties</a>.</li>
</ul>

## Work &amp; Life
<ul>
<li>Anton Sten wrote about <a href="https://www.antonsten.com/moral-implications-apps/">the moral implications for our apps</a>. A meaningful explanation why the times of “move fast and break things” are definitely over as we’re dealing with Artificial Intelligence, social networks that affect peoples’ lives, and privacy matters enforced by GDPR.</li>
<li>Basecamp now has a new chart type to display a project’s status: the so-called “<a href="https://m.signalvnoise.com/new-in-basecamp-see-where-projects-really-stand-with-the-hill-chart-ca5a6c47e987">hill chart</a>” adds a better context than a simple progress bar could ever do it.</li>
<li><a href="https://werd.io/2018/what-youre-proud-of">Ben Werdmüller shares his thoughts about resumes</a> and how they always fail to reflect who you are, what you do, and why you should be hired.</li>
</ul>

<p>I hope you enjoyed this monthly update. The next one is scheduled for July 13th, so stay tuned. In the meantime, if you like what I do, <a href="https://wdrl.info/donate">please consider helping me fund the Web Development Reading List financially</a>.</p>

<p>Have a great day!</em></p>

<p><em>&mdash; Anselm</em></p>

{{< signature "cm" >}}
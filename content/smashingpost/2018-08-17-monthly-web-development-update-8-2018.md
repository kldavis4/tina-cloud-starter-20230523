---
title: 'Monthly Web Development Update 8/2018: The Cost Of JavaScript, Ethics In Open Source, And QUIC'
slug: monthly-web-development-update-8-2018
author: anselm-hannemann
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16d1bfc3-5cc5-4ca6-98ea-34276f6d21d7/js-processing-opt.png
date: 2018-08-17T11:57:10+02:00
summary: >-
  What happened in the web industry in the past four weeks? To keep you up-to-date, Anselm summarizes the latest techniques, browser updates, and hot topics in one handy reading list.
description: >-
  What happened in the web industry in the past four weeks? To keep you up-to-date, Anselm summarizes the latest techniques, browser updates, and hot topics in one handy reading list.
categories:
  - Web Development Reading List
---
<p>Building technology and software has become a very responsible job. People trust the products we create, and they can have a significant impact on their lives, too. Considering this, we not only need to think about inclusive solutions, but also stand up and advocate for ethics, reliability, and security. It’s a position that gives us power.</p>

<p>Eric Meyer published an article elaborating the problems which an HTTPS-only web is bringing along. In it, <a href="https://meyerweb.com/eric/thoughts/2018/08/07/securing-sites-made-them-less-accessible/">he reveals that developing countries suffer a lot from this development</a> as they often have bad internet connections and, due to the encryption, they now experience <strong>more website errors than before</strong>. Ben Werdmüller jumped in and published the article “<a href="https://werd.io/2018/stop-building-for-san-francisco">Stop building for San Francisco</a>” in which he points out one of the biggest problems we have as developers: We use privileged hardware and infrastructure. We build experiences using the latest iPhones, Macbooks with Gigabit or fast 4G connections but never consider that most people we’re building for use devices and infrastructures that are far from being that well-equipped. Making the web more secure is a great idea, beyond question, but we should also keep in mind the consequences that the latest tech and our design decisions might have for others.</p>

## News

<ul>
<li><a href="https://blogs.msdn.microsoft.com/typescript/2018/07/30/announcing-typescript-3-0/">TypeScript 3.0 was released</a> with a couple of convenient language features and fixes.</li>
<li>Implemented in Chrome since quite a while already, Client Hints are an amazing feature. To improve privacy, <a href="https://cloudinary.com/blog/client_hints_and_responsive_images_what_changed_in_chrome_67">the functionality of Client Hints for responsive images changed with Chrome 67</a>. Colin Bendell explains the differences and why Client Hints are so useful for performance.</li>
<li>Developers have been asking a lot about Safari’s Intelligent Tracking Prevention (ITP) and how to debug websites with it enabled. Now <a href="https://webkit.org/blog/8387/itp-debug-mode-in-safari-technology-preview-62/">the WebKit team shares the ITP Debug Mode</a> which gives you a lot more flexibility and tools to track down issues.</li>
<li>Starting in October, <a href="https://blog.mozilla.org/security/2018/07/30/update-on-the-distrust-of-symantec-tls-certificates/">most browsers will distrust Symantec TLS certificates entirely</a> and, thus, block access to websites which still use them. Please update your certificate if you haven’t already.</li>
<li>The latest version of Chrome (68) brings a new <a href="https://www.blog.google/products/chrome/milestone-chrome-security-marking-http-not-secure/">“not secure” notification when visiting HTTP pages</a>. Be aware of this and upgrade your sites accordingly. Also <a href="https://developers.google.com/web/updates/2018/07/nic68">new in Chrome 68</a> are the new Page Lifecycle API, a great new API for page events, as well as the Payment Handler API. HTTP cache is now ignored when requesting updates to a service worker, bringing Chrome in line with the spec and other browsers. Apart from that, the <code>cursor</code> values <code>grab</code> and <code>grabbing</code> are now unprefixed in the new version — finally.</li>
</ul>

{{% feature-panel %}}

## General

<ul>
<li>If you’re building for Open Source, you need to decide which license your project should use. Now there’s a new option, the <a href="https://github.com/raisely/jwl">Just World License</a>. It’s for developers who “agree in general with the principles of open source software but are uncomfortable with their software being used as part of efforts to destroy lives, our environment and our future”.</li>
<li>Deep-learning machines are a big topic these days, but some people are exploring even <a href="https://www.technologyreview.com/s/611568/evolutionary-algorithm-outperforms-deep-learning-machines-at-video-games/">better algorithms that outperform deep-learning machines easily at video games</a>.</li>
<li>Drew DeVault’s “<a href="https://drewdevault.com/2018/07/09/Simple-correct-fast.html">Simple, correct, fast: in that order</a>” is a great reminder to set priorities straight in web and software development.</li>
<li>Jonathan Fulton wrote a handy resource called “<a href="https://engineering.videoblocks.com/web-architecture-101-a3224e126947">The basic architecture concepts I wish I knew when I was getting started as a web developer</a>”, which is a great web architecture 101 and foundation for newcomers in our industry.</li>
</ul>

## UI/UX

<ul>
<li><a href="https://ethicsfordesign.com/">Ethics for Design</a> is a project where twelve designers and researchers from eight European cities discuss the, sometimes harmful, impact of design on our societies and what designers can do to work for the good of all and not just a few.</li>
</ul>

## Tooling

<ul>
<li>Prashant Palikhe wrote a long story about <a href="https://medium.com/frontmen/art-of-debugging-with-chrome-devtools-ab7b5fd8e0b4">the art of debugging with Chrome’s Developer Tools</a>, which I can highly recommend as it’s a very complete reference to get to know the developer tools of a browser. If you use another browser, that’s not a big problem as most tools are quite similar.</li>
<li>WebP is an image format with a couple of nice features and likely one of the best-known new formats besides the common JPEG/PNG ones. However, creating WebP images can still be a challenge, so <a href="https://www.smashingmagazine.com/2018/07/converting-images-to-webp/">Jeremy Wagner wrote a guide on how to convert images to WebP</a>.</li>
<li><a href="https://dcreager.net/nel/intro/">Douglas Creager introduces</a> the new <a href="https://wicg.github.io/network-error-logging/">Network Error Logging</a> which allows you to instruct user agents to collect the same set of information that would appear in your server logs.</li>
<li>Many of us are addicted to communication tools like Slack. The folks from Wildbit decided to <a href="https://wildbit.com/blog/2018/07/17/our-week-off-from-slack">shut down Slack for a week</a> — with a significant effect on how they work. An interesting case study about how we tend to get too comfortable with a useful tool and don’t use it as we should anymore. From time to time, it’s important to reset our minds.</li>
<li>Dennis Reimann published the first stable version of <a href="https://dennisreimann.de/articles/uiengine-1-0.html">UIEngine</a>, a workbench for UI-driven development.</li>
</ul>

## Security

<ul>
<li>A new Observer is around: <a href="https://developers.google.com/web/updates/2018/07/reportingobserver">The ReportingObserver API</a> lets you know when your site uses a deprecated API or runs into a browser intervention. So far, it’s available in Chrome 69. You could easily use this to send errors that previously were only available in the Console to your backend or error handling service.</li>
</ul>

## Web Performance

<ul>
<li>Do you remember QUIC (Quick UDP Internet Connections)? The protocol engineered by Google that they use internally and that is shaping up quite well for larger use? While the IETF is currently standardizing the format towards the end of the year, <a href="https://blog.cloudflare.com/the-road-to-quic/">Cloudflare engineers now share their experience from testing it</a>.</li>
</ul>
<figure><a href="https://blog.cloudflare.com/the-road-to-quic/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34706ade-81b4-4aee-a10f-dba8c437d942/quic-opt.png" width="800" height="494" alt="HTTP request over QUIC" /></a><figcaption>A QUIC handshake only takes a single round-trip between client and server to complete, whereas TCP and TLS usually need two. (<a href="https://blog.cloudflare.com/the-road-to-quic/">Image source</a>)</figcaption></figure>
## HTML &amp; SVG
<ul>
<li>When you have user-generated content, you often don’t know if you have just one element or a list of elements to output. At Colloq, we wanted to do semantics right and <a href="https://colloq.io/blog/better-design-system-component-semantics">built a system that allows us to output a <code>p</code> tag when only one element is in the container</a>, otherwise a <code>ol</code>/<code>ul</code> list with various list items.</li>
</ul>

## Accessibility

<ul>
<li>Dave Rupert shares the <a href="https://davatron5000.github.io/a11y-nutrition-cards/">A11Y Nutrition Cards</a>, a project that attempts to digest and simplify the accessibility expectations when it comes to component authoring.</li>
<li>Skip links are quite common accessibility features. Hampus Sethfors now wrote an article on <a href="https://axesslab.com/skip-links/">why many of the links are still broken and how to fix them properly</a>.</li>
</ul>

## JavaScript

<ul>
<li>One year after they introduced their Progressive Web App, Zack Argyle from the Pinterest engineering team <a href="https://medium.com/@Pinterest_Engineering/a-one-year-pwa-retrospective-f4a2f4129e05">takes a look back</a>. It’s important to note why they decided to build a PWA: “Our mobile web experience for people in low-bandwidth environments and limited data plans was not good”. But the results for them are amazing to see.</li>
<li>Philip Walton <a href="https://developers.google.com/web/updates/2018/07/page-lifecycle-api">introduces the new Page Lifecycle API</a> which helps us determine page states in the browser more easily via events, such as the page being in the background (not visible), active, frozen or even terminated.</li>
<li>Whoops, you all know <code>eval()</code> in JavaScript is bad, right? That’s why we usually forbid its usage in Content Security Policies. But Remy Sharp reminds us that <a href="https://remysharp.com/2018/07/25/when-helpful-turns-into-super-bad-security">there’s a line of code which is equally bad for security</a>.</li>
<li>Addy Osmani researched <a href="https://medium.com/@addyosmani/the-cost-of-javascript-in-2018-7d8950fbb5d4">the cost of JavaScript in 2018</a> and now shares evidence that every byte of JavaScript is still the most expensive resource we can send to mobile phones because it can delay interactivity significantly. This is a problem especially for not so capable phones that are widely used outside the tech industry.</li>
<li>Hidde de Vries explains <a href="https://hiddedevries.nl/en/blog/2018-07-19-accessible-page-titles-in-a-single-page-app">how we can make page titles accessible in JavaScript Single Page Application</a>.</li>
</ul>

<figure><a href="https://medium.com/@addyosmani/the-cost-of-javascript-in-2018-7d8950fbb5d4"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16d1bfc3-5cc5-4ca6-98ea-34276f6d21d7/js-processing-opt.png" width="800" height="463" alt="The Cost Of JavaScript In 2018" /></a><figcaption>What’s the real <a href="https://medium.com/@addyosmani/the-cost-of-javascript-in-2018-7d8950fbb5d4">cost of JavaScript</a>? One of the findings from Addy Osmani’s research: It takes a low-end 2018 phone 32 seconds longer than an iPhone 8 to process JavaScript for CNN.com. (<a href="https://medium.com/@addyosmani/the-cost-of-javascript-in-2018-7d8950fbb5d4">Image source</a>)</figcaption></figure>

## CSS

<ul>
<li>Max Böck explored a few CSS Grid techniques <a href="https://mxb.at/blog/layouts-of-tomorrow/">to build the layouts of tomorrow with relatively simple code</a>.</li>
<li>Sara Soueidan explains how we can <a href="https://www.sarasoueidan.com/blog/toggle-switch-design/">build inclusive toggle switches</a> with modern HTML and CSS.</li>
<li>Jen Simmons shares <a href="https://hacks.mozilla.org/2018/07/9-biggest-mistakes-with-css-grid/">common CSS Grid mistakes and how to solve them</a>.</li>
<li>Ethan Marcotte <a href="https://ethanmarcotte.com/wrote/fractional/">explains the still relatively new <code>fr</code>-unit</a> that we mostly use for CSS Grids.</li>
</ul>

{{% ad-panel-leaderboard %}}

## Work &amp; Life

<ul>
<li>Paris Marx wrote about why he thinks <a href="https://medium.com/@parismarx/digital-nomads-are-not-the-future-be360c7911b4">digital nomads are not the future</a>. He argues that location independence is only possible because of communication infrastructures built with public funds and that it’s not fair to abuse them.</li>
<li>This week I learned how useful it can be to think outside the box and <a href="https://helloanselm.com/writings/solving-problems-remotely-on-the-bus">how remote work and pursuing your hobby can help solve technical challenges</a>.</li>
<li>It’s not the first time a company <a href="https://www.nytimes.com/2018/07/19/world/asia/four-day-workweek-new-zealand.html">is testing a 4-day workweek</a>. However, it’s great to see how the concept can be established successfully and with benefits for both — the employees <em>and</em> the work done.</li>
</ul>

## Going Beyond…

<ul>
<li>Tobias van Schneider wrote about why the Sagmeister-Walsh studio is so successful by staying small and <a href="https://www.vanschneider.com/how-sagmeister-became-one-of-the-greatest-design-studios-by-staying-small">why dreaming big but staying small is so important for creative thinking</a>.</li>
<li>Ben Werdmüller shares his thoughts on how different it has become to start a business when you’re, for example, in San Francisco. This is <a href="https://werd.io/2018/startup-economics-in-san-francisco">a story where $117,000 are considered a “low income” in San Francisco</a> and how this limits ideas.</li>
<li>Jeremy Nagel makes us think about the <a href="https://hackernoon.com/is-open-source-working-for-the-enemy-80f113ca1b0">impact of our open-source code</a>: As developers we tend to believe that making our code freely available is an amazing move but we forget that we make it available to bad players as well — to coal miners, to pollution-contributing companies, to those who use people to get rich while mistreating them, to those who rip you off indirectly. It’s not that you can’t do anything about it; you have to be aware of these issues and apply a better license or add a dedicated statement to your code.</li>
<li>India has a big plastic waste problem. Since a couple of months, a <a href="https://www.weforum.org/agenda/2018/06/these-indian-fishermen-take-plastic-out-of-the-sea-and-use-it-to-build-roads">couple of fishers don’t ignore the plastic problem anymore</a> but collect all the waste in their nets instead, and bring it back to the shore where it’s used to build roads. A great idea of making use of trash efficiently.</li>
</ul>

{{< signature "cm" >}}
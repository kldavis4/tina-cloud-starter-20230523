---
title: >-
  Monthly Web Development Update 1/2018: Browser Diversity, Ethical Design, And
  CSS Alignment
slug: monthly-web-development-update-1-2018
author: Anselm Hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2124d48-7ee8-4e70-8489-409f65646037/css-alignment-opt.png
date: 2018-01-19T15:17:55+01:00
summary: >-
  Anselm Hannemann summarized what happened in the web development world in the
  past few weeks. A reading list full of browser news, handy guides, thoughtful
  reads, and more.
description: >-
  Anselm Hannemann summarized what happened in the web development world in the
  past few weeks. A reading list full of browser news, handy guides, thoughtful
  reads, and more.
disable_panels: true
categories:
  - Web Development Reading List
---
<p>I hope you had a great start into the new year. And while it’s quite an arbitrary date, many of us take the start of the year as an <strong>opportunity to try to change something in their lives</strong>. I think it’s well worth doing so, and I wish you the best of luck for accomplishing your realistic goals. I for my part want to start working on my mindfulness, on being able to focus, and on pursuing my dream of building an ethically correct, human company with <a href="https://colloq.io/">Colloq</a> that provides real value to users and is profitable by its users.</p>

<p>Technology-wise, 2018 already brought big news and great articles for us web developers. I personally started the year attending the <a href="https://beyondtellerrand.com/events/munich-2018/speakers">beyondtellerrand conference</a> and <a href="https://colloq.io/events/accessibility-club/2018/munich/1/links">a11y club</a> in Munich, Germany, and got to learn a lot about design, performance, art, and many other things. We also discussed the topic around Mozilla’s HTTPS announcement (see the News section for more details) and talked about doing purposeful work and finding better ways to balance life and work — a topic that I talk about a lot, and recently it seems that more and more people get interested in it as well. But now let’s go straight to the news.</p>

<div class="c-felix-the-cat">
<h4 class="h3">On Balancing Life And Work</h4>
<p>As web designers and developers you invest a lot of time and effort in nurturing professional relationships. But what about your private life? Do you manage to keep the balance? <a href="https://www.smashingmagazine.com/2014/05/fostering-healthy-non-professional-relationships/" class="btn btn--medium btn--blue">Read a related article →</a></p>

</div>

{{% feature-panel %}}

## News

<ul>

<li>The biggest announcement comes from Mozilla: Starting immediately, <a href="https://blog.mozilla.org/security/2018/01/15/secure-contexts-everywhere/">Firefox will require HTTPS for all new features built into the browser</a>. So this means not only privacy- or security-relevant information such as the Geolocation API requires HTTPS to work now, but the next CSS property or a new JavaScript feature, for example, will only be usable if a site is served via HTTPS, too. Google Chrome made a similar announcement last year, but the team hasn’t clarified yet when it will be put into practice. While these decisions might lead to even faster adoption of HTTPS, there’s also a risk that new features won't be adopted by developers as quickly anymore. We might temporarily see even more “optimized for Chrome” messages on websites until this browser follows the same strategy. One thing at least is for sure: This week marks a quite important point in the history of the web — no matter what the feedback will be, it’ll be interesting and change the way we build our websites.</li>

<li>This week also brought news from Google’s web search team: Starting from July 2018, the well-known <a href="https://webmasters.googleblog.com/2018/01/using-page-speed-in-mobile-search.html">Pagespeed tool will become a ranking factor</a> for mobile searches. This means that finally a lot more web standards and best practices will be enforced by this change, leading to better web performance and better adoption of web standards and also accessibility features.</li>

<li>The W3C announced that <a href="https://www.w3.org/blog/2017/12/html-5-2-is-done-html-5-3-is-coming/">HTML 5.2 is done now</a>. They removed the web’s plugin system from the spec, changed the definition of the <code>&lt;main&gt;</code> element, allowed <code>style</code> elements to be set inside <code>body</code>, and a couple of other things.</li>

<li>To reduce typosquatting of packages, the <a href="https://blog.npmjs.org/post/168978377570/new-package-moniker-rules">npm registry does not allow similar namings for packages anymore</a>. An active push and encouragement to make people use their user scope for publishing packages.</li>

<li>Starting February 15th, Google Chrome will comply with the <a href="https://betterads.org/standards">Better Ads Standard</a>. Here are more details about <a href="https://developers.google.com/web/updates/2017/12/better-ads">what that means for you</a>.</li>

<li>Chrome 63/64 will bring developers the ability to <a href="https://developers.google.com/web/updates/2017/12/chrome-63-64-media-updates">predict whether playback will be smooth and power-efficient</a>. It will also pause autoplay videos that are in the background and have no audio tracks.</li>

<li>The <a href="https://webkit.org/blog/8042/release-notes-for-safari-technology-preview-46/">Safari Technology Preview Release 46</a> brings some very interesting news: First of all, it introduces full Service Worker support and a smart security warning if a user is about to fill credit card data or passwords on non-secure websites. Also important to know is that Safari’s UserAgent string won't change anymore from now on: They froze it to reduce web compatibility risk and to prevent its use for fingerprinting. Also new: For images, they now support <code>decoding="asy"</code>.</li>

<li>Researchers showed that <a href="https://googleprojectzero.blogspot.de/2018/01/reading-privileged-memory-with-side.html">nearly every CPU from the last decade (or even longer) is vulnerable</a> to memory side-channel timing attacks. Quite nasty, especially if you think about what this means for Cloud providers whose complete server and CPU architecture are based on shared hardware. Even worse, the bugs cannot be fixed with a simple software update — it’ll require new processor architectures to eliminate the fundamental issues. By now, most operating systems, browser vendors, and CPU vendors have released software patches for the known attack surfaces which should keep the biggest issues away for a while. But with it, huge performance impacts have shown up, for some doubling the load on their servers. Here’s the <a href="https://googleprojectzero.blogspot.de/2018/01/reading-privileged-memory-with-side.html">Project Zero announcement</a> of the vulnerability, the <a href="https://www.chromium.org/Home/chromium-security/ssca">Chromium statement</a>, the <a href="https://support.apple.com/en-us/HT208394">Apple statement</a> and Mozilla’s explanation of <a href="https://blog.mozilla.org/security/2018/01/03/mitigations-landing-new-class-timing-attack/">how they try to mitigate the attacks in Firefox</a>.</li>

</ul>

<figure><a href="https://betterads.org/standards"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90dce3bf-aadf-4d1c-b696-24446676b7e0/better-ads-opt.png" width="800" height="510" alt="Coalition For Better Ads" /></a><figcaption>In less than a month from now, Chrome will comply with the <a href="https://betterads.org/standards">Better Ads Standard</a> to fight bad ad experiences.</figcaption></figure>

## General

<ul>

<li>Chris Krycho shares his thoughts on the importance of browser diversity and <a href="https://www.chriskrycho.com/2017/chrome-is-not-the-standard.html">why we as developers need to stop building solutions for one browser only</a>. Just think a moment about what we’d lose if there’s only one browser — Chrome, for example — left: There probably wouldn't be any WebAssembly, no CSS Grids, no concurrent JavaScript. Innovation can only happen as long as there's variety.</li>

<li>Chris Heilman wrote a thoughtful, impactful article about <a href="https://christianheilmann.com/2017/12/17/the-web-we-may-have-lost/">the real value of net neutrality</a>. Having the web as an educative, enabling place for everyone is an important factor many of us took advantage of: We learnt by using a neutral web that made a lot of information that would cost a lot more money otherwise (using print or other channels) available to us and let us decide what to read and what to consume.</li>

</ul>

## UI/UX

<ul>

<li>Anna Monus explains <a href="https://webdesign.tutsplus.com/articles/how-to-use-variable-fonts-on-the-web--cms-30212">how we can use variable fonts on the web</a> and shares some neat examples of how useful they can be.</li>

<li>I wrote an article sharing my thoughts on <a href="https://helloanselm.com/2018/whats-behind-ethical-design/">the often overused and misinterpreted term “Ethical Design”</a> and explain why the underlying premise is going to be important this year.</li>

<li>Phil Nash shares <a href="https://philna.sh/blog/2018/01/08/permissions-on-the-web-suck/">why permissions on the web suck</a>. Bringing the issues of how they’re (mis)used by sites and missing information together, he elaborates what would be necessary to make notifications a great idea on the web.</li>

<li>Matthias Ott wrote about <a href="https://matthiasott.com/articles/saving-your-web-workflows-with-prototyping">creating great web workflows with prototyping</a> instead of using tools that don’t reflect how the web and websites work in reality.</li>

</ul>

<figure><a href="https://webdesign.tutsplus.com/articles/how-to-use-variable-fonts-on-the-web--cms-30212"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5cd9432-eb06-4356-8e42-facf44d2448a/decovar-opt.png" width="800" height="542" alt="Variable font" /></a><figcaption>One font, different looks. Variable fonts allow designers to derive an unlimited number of font variants from the same font file. Anna Monus <a href="https://webdesign.tutsplus.com/articles/how-to-use-variable-fonts-on-the-web--cms-30212">explains how it works</a>. (<a href="https://webdesign.tutsplus.com/articles/how-to-use-variable-fonts-on-the-web--cms-30212">Image source</a>)</figcaption></figure>

## Security

<ul>

<li>Gunes Acar shows <a href="https://freedom-to-tinker.com/2017/12/27/no-boundaries-for-user-identities-web-trackers-exploit-browser-login-managers/">how ad scripts can pull data from user’s password managers in the browser</a>. There’s help for users using proper adblock plugins, and <a href="https://twitter.com/derSchepp/status/948665256204783617">things site owners can do</a>.</li>

<li>J.C. Jones and Tim Taubert explain how we can <a href="https://hacks.mozilla.org/2018/01/using-hardware-token-based-2fa-with-the-webauthn-api/">use the Web Authentification API to implement hardware token-based two-factor authentification</a> and use it in browsers that support this API already.</li>

<li>I quite like the way the folks from WebKit write blog posts to explain certain changes in the browser engine. This time, they share <a href="https://webkit.org/blog/8048/what-spectre-and-meltdown-mean-for-webkit/">what Spectre and Meltdown mean for WebKit</a>, why the browser is affected by them, and what they changed to try to mitigate the risk of an attack.</li>

<li><a href="https://hackernoon.com/im-harvesting-credit-card-numbers-and-passwords-from-your-site-here-s-how-9a8cb347c5b5">David Gilbertson shares a (not so) true story</a> which is pretty alarming if you think about the possibility that this could be real. He shares how to obtain credit card numbers, passwords and other personal data from any site out there by providing an open-source package that seems useful to other people.</li>

</ul>

## Web Performance

<ul>

<li>Vitaly Friedman updated last year’s <a href="https://www.smashingmagazine.com/2018/01/front-end-performance-checklist-2018-pdf-pages/">Front-end Performance Checklist for 2018</a> so you can use it for every project this year.</li>

<li><a href="https://font-display.glitch.me/">The <code>font-display</code> playground</a> is a nice interactive page that shows and explains the different options we now have when using the new CSS <code>font-display</code> property to optimize web font loading.</li>

</ul>

## CSS

<ul>

<li><a href="https://blogs.igalia.com/mrego/2018/01/11/display-contents-is-coming/"><code>display: contents</code> is a rather new CSS display property value</a>, and Manuel Rego Casasnovas has written a summary of how we can make use of the new feature.</li>

<li>Keith J Grant shares how we can <a href="https://keithjgrant.com/posts/2018/meet-the-new-dialog-element/">use the new <code>&lt;dialog&gt;</code> element</a> introduced in HTML5.2 to show modals on websites.</li>

<li>Peter Mouland explains <a href="https://medium.com/@petermouland/css-grid-flexbox-solving-real-world-problems-1cce3ecb2b51">a series of real-world problems we can solve with CSS Grid and Flexbox</a> easily these days.</li>

<li>Patrick Brosset <a href="https://medium.com/@patrickbrosset/demystifying-css-alignment-2d3ea7a02a36">demystifies CSS alignment</a>, especially for Flexbox and Grid, and provides <a href="https://patrickbrosset.com/lab/2018-01-10-css-alignment-cheatsheet/">a nice alignment cheatsheet for CSS</a>.</li>

</ul>

<figure><a href="https://medium.com/@patrickbrosset/demystifying-css-alignment-2d3ea7a02a36"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2124d48-7ee8-4e70-8489-409f65646037/css-alignment-opt.png" width="800" height="445" alt="CSS alignement" /></a><figcaption>Which direction is justify and which is align? Patrick Brosset <a href="https://medium.com/@patrickbrosset/demystifying-css-alignment-2d3ea7a02a36">sheds some light</a> into the dark corners of CSS alignment. (<a href="https://medium.com/@patrickbrosset/demystifying-css-alignment-2d3ea7a02a36">Image source</a>)</figcaption></figure>

## JavaScript

<ul>

<li>Addy Osmani wrote about <a href="https://medium.com/dev-channel/the-cost-of-javascript-84009f51e99e">the cost of JavaScript</a>, analyzing the impact of JavaScript, comparing it to the same byte size of images, and explaining how we can use this knowledge to improve performance.</li>

<li>The JavaScript programming language is an essential tool, and websites ship more and more JavaScript to the browser to be more interactive. But the more complex client-side JavaScript gets, the more error-prone and fragile the user experience might get. Why do we need to talk about robust JavaScript and how do we achieve it? Here’s “<a href="https://molily.de/robust-javascript/">Robust Client-Side JavaScript</a>”, a guide by Mathias Schäfer.</li>

<li>Bill Sourour shares his late appreciation of something he was told quite some time ago: Sometimes it’s better to <a href="https://medium.freecodecamp.org/dont-do-it-at-runtime-do-it-at-design-time-c4f59d1775e4">code things upfront</a> — at design time and not at runtime. Under the premise of building scalable solutions, we often tend to build things as flexible as they can be, resulting in a lot of runtime calculations. However, the alphabet, for example, won’t change, so there’s no point in not hardcoding the array for it but instead looping through it at runtime.</li>

<li><a href="https://github.com/russellgoldenberg/scrollama">Scrollama</a> is a modern and lightweight JavaScript library for scrollytelling using IntersectionObserver in favor of scroll events.</li>

<li>Peter O'Shaughnessy shares how to get started with the <a href="https://www.smashingmagazine.com/2018/01/online-purchase-payment-request-api/">Payment Request API</a> for online payments in the browser.</li>

<li>Jason Grigsby explains why it’s important to be careful when to ask for additional permission on a website. With a <a href="https://wdrl.info/archive/208/new-in-chrome-63-web-google-developers">recent change in Chrome 63</a>, a user won’t see the permission screen again if they block it the first time. This is the result of 90% of the requests not being allowed by Chrome users previously.</li>

</ul>

<figure><a href="https://medium.com/dev-channel/the-cost-of-javascript-84009f51e99e"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3426cde0-25ce-4acb-b1db-5a2ffe1fb22a/cost-of-js-opt.png" width="800" height="426" alt="The Cost of JavaScript" /></a><figcaption>Addy Osmani shares best practices for <a href="https://medium.com/dev-channel/the-cost-of-javascript-84009f51e99e">reducing how much JavaScript you're shipping</a> to your users. (<a href="https://medium.com/dev-channel/the-cost-of-javascript-84009f51e99e">Image credit</a>)</figcaption></figure>

## Accessibility

<ul>

<li>When Rob Dodson started to ensure accessibility for websites, he wanted to write automated tests. Now he shares <a href="https://robdodson.me/why-you-cant-test-a-screen-reader-yet/">why it’s not possible to test a screen reader yet</a> and what will come in the future.</li>

</ul>

## Work &amp; Life

<ul>

<li>Dan Mall shares some insights into <a href="https://danmall.me/articles/how-to-scope-work/">how he learned to scope work</a>. This is a very useful skill — no matter if you’re a freelancer or employee — to estimate costs and time. I can only recommend you to read this article.</li>

<li>In the past year, rising inequality was a highly prioritized topic. <a href="https://www.theguardian.com/inequality/2018/jan/04/inequality-is-under-attack-but-what-should-equality-really-look-like">But what should equality really look like?</a> A question that has rarely been asked. Jo Litter is taking a stand now.</li>

</ul>

## Going Beyond…

<ul>

<li>Susan Wu says <a href="https://www.wired.com/story/its-time-for-innovators-to-take-responsibility-for-their-creations/">it’s time for innovators to take responsibility for their creations</a>. This is about the problems Twitter, Facebook, Uber, Airbnb and lots of other services cause. This is about Facebook causing people to end their lives, others watching them, Twitter actively helping hate speech to be seen by loads of people, Airbnb destroying house rents in cities all over the world, sending people indirectly into homelessness. But most importantly, this is a thoughtful article about what social networks and platforms like the named ones could do to improve peoples’ lives, and why it’s not smart to only go after profit.</li>

<li>The folks from Information Architects explain why <a href="https://ia.net/topics/distractions-and-how-to-fight-them/">we’re most vulnerable to distractions when we should focus</a> and what we can do about it.</li>

<li>The chances are high that <a href="https://grist.org/article/let-it-go-the-arctic-will-never-be-frozen-again/">humanity will not see the Arctic frozen again</a> as it was years and decades ago.</li>

<li>It will be 12 years from now when, according to <a href="https://www.theguardian.com/environment/2018/jan/16/eu-declares-war-on-plastic-waste-2030">the newest plans of the European Union</a>, we won't need to produce new plastic materials anymore but will be able to recycle and reuse existing packaging. This bold plan follows China’s directive to stop the import of foreign recyclable material which was a profitable business and solved the plastic issue for the EU and other countries for quite some time. Now it’s time to find solutions on our own, recycle in the same country instead of loading the problem off to other countries. I’m happy about these plans and can only hope that we will match the timeframe and make the world a still enjoyable place to live in the future.</li>

</ul>

<p><em>We hope you enjoyed this Web Development Update. The next one is scheduled for February 16th. Stay tuned.</em></p>


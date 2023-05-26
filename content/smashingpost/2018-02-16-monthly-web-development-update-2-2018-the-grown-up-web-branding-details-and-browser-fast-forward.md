---
title: >-
  Monthly Web Development Update 2/2018: The Grown-Up Web, Branding Details, And
  Browser Fast Forward
slug: monthly-web-development-update-2-2018
author: anselm-hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e27eed31-2d4f-4706-b321-2ff9a94f8262/best-practices-modals-opt.png
date: '2018-02-16T13:37:50+01:00'
summary: >-
  Staying on top of the newest techniques, browser updates, and hot topics can
  be hard. Anselm Hannemann summarized what happened in the web industry in the
  past few weeks, so you can easily catch up on everything new and important.
description: >-
  Staying on top of the newest techniques, browser updates, and hot topics can
  be hard. Anselm Hannemann summarized what happened in the web industry in the
  past few weeks, so you can easily catch up on everything new and important.
disable_panels: false
categories:
  - Web Development Reading List
---
<p>Every profession is a wide field where many people find their very own, custom niches. So are design and web development today. I started building my first website with framesets and HTML4.0, images and a super limited set of CSS, and — oh so fancy — GIFs and inline JavaScript (remember the <code>onclick=""</code> attribute?) about one and a half decades ago. It took me four days to learn the initial, necessary skills for that.</p>

<p>But times are very different today, and when I see how capable the web has become, it’s reasonable to say that it can give people a hard time to start out in this field, and it can be reasonable for people to say that they want to <strong>focus on one specific part of web development only</strong>. Nowadays, we have JavaScript developers who don’t know much HTML or CSS, and we have developers who aren’t able to work on a modern JavaScript stack but are heroes in what they achieve with CSS. There are people specializing in web font loading, in web performance, in security, in privacy, or in usability.</p>

<p>Web development has <strong>grown up to be a solid profession</strong> — something that needs a vast amount of knowledge to be an expert in, something that cannot be learned in a few days anymore. Instead, we’re now able to build applications on the web and do things I would never have imagined the web to be capable of when I started out 16 years ago. If we look at how much effort it is to get into woodworking, for example, we realize that web development isn’t much different. Of course, one can achieve some result in a few hours, but producing something that lasts, something that is solid <em>and</em> looks great requires a lot of knowledge, experience, failures, and patience. So does building a great web experience.</p>

{{% feature-panel %}}

## News

<ul>

<li>The big news from browser vendors don’t stop coming in: Google Chrome now announced that starting in Chrome 68 (to be released in July 2018) <a href="https://security.googleblog.com/2018/02/a-secure-web-is-here-to-stay.html">the browser will mark non-secure sites (HTTP) as “not secure”</a> — the end of non-HTTPS websites. I just imagine all the clients with their small business sites and portfolios desperate about this change. It’s great to see the shift to a more secure web, but sometimes I have the feeling that those who decide don’t think enough about the impact their decisions have on small entities using the Internet as well.</li>

<li>Safari’s <a href="https://developer.apple.com/safari/technology-preview/release-notes/">Technology Preview 49</a> brings some interesting features: The Intelligent Tracking Protection now has a debug tool in experimental mode, <code>column-gap</code> is now supporting <code>%</code>-values, <code>active-descendant</code> is supported, too, and Console will throw a warning if AppCache is used.</li>

<li>Here we go with the announcement of the last major browser vendor to support Progressive Web Apps: this time <a href="https://blogs.windows.com/msedgedev/2018/02/06/welcoming-progressive-web-apps-edge-windows-10/">Microsoft in Windows and the Edge browser</a>. Edge 17 will come with Service Workers and push notifications, but what's even more interesting is that the company shares their strategy on how they will support such apps at an operating system level: The Microsoft Store will start listing Progressive Web Apps by manual submission which is a big step forward for making web apps as usable as native apps. I can imagine many Electron apps to become obsolete if this concept gets adopted by other OS vendors as well.</li>

<li><a href="https://developers.google.com/web/updates/2018/01/nic64">Google Chrome 64 is out</a> and brings <code>ResizeObserver</code>, a way stronger popup blocker mechanism. <code>window.alert</code> won't change the focus anymore, and, to save bandwidth, the new Chrome also changes the preload behavior of media files to metadata only.</li>

<li>In the <a href="https://developers.google.com/web/updates/2018/02/chrome-65-deprecations">upcoming Chrome version 65</a>, the browser will block certificates from Symantec’s Legacy PKI and, to protect users' safety, the <code>download</code>-attribute if the target is a cross-origin reference.</li>

<li><a href="https://developer.mozilla.org/en-US/Firefox/Releases/58">Firefox 58 was released</a> this week with big performance improvements. It throttles timers in background tabs, brings <code>font-display</code> as a CSS property, and supports <code>Intl.PluralRules</code>. Also new is that the WebVR API is enabled by default on macOS now, and WebAssembly has gotten <a href="https://hacks.mozilla.org/2018/01/making-webassembly-even-faster-firefoxs-new-streaming-and-tiering-compiler/">the amazing streaming compiler</a>.</li>

<li><a href="https://developer.apple.com/library/content/releasenotes/General/WhatsNewInSafari/Articles/Safari_11_1.html">Safari 11.1</a> is shipping with iOS 11.3 and macOS 10.13.4. It is also available in older macOS 10.12.6 and 10.11.6 versions. The update brings Service Workers, the Payment Request API including Apple Pay, <code>HTMLImageElement.decode()</code>, the File and Directory Entries API, Beacon API, video as an image asset in <code>&lt;img&gt;</code> elements, support for Encrypted Media Extensions in Safari on iOS, support for <code>allow="camera"</code> in WebRTC and Media Capture, the CSS <code>font-display</code> property to control flash of unstyled text with web fonts, and the Web App Manifest. Security-wise it adds support for subresource integrity, "website not secure" warnings, a frozen Safari User-Agent string. I think this marks quite a milestone that shows that Apple is putting a lot of effort into keeping Safari up to date. It's also interesting to see that Safari automatically drops old Service Workers that haven’t been used in a long time to not waste users’ disc space.</li>

</ul>

<figure><a href="https://hacks.mozilla.org/2018/01/making-webassembly-even-faster-firefoxs-new-streaming-and-tiering-compiler/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cce54dfc-ba60-443d-ba3d-cf89f264bb5b/firefox-streaming-compiler-opt.png" width="800" height="326" alt="Firefox streaming and tiering compiler" /></a><figcaption>Firefox 58 includes a <a href="https://hacks.mozilla.org/2018/01/making-webassembly-even-faster-firefoxs-new-streaming-and-tiering-compiler/">new two-tiered compiler</a> that compiles code 10&ndash;15 times faster than the optimizing compiler. (<a href="https://hacks.mozilla.org/2018/01/making-webassembly-even-faster-firefoxs-new-streaming-and-tiering-compiler/">Image credit</a>)</figcaption></figure>

## General

<ul>

<li>Frank Chimero published a new article in which he explains <a href="https://frankchimero.com/writing/everything-easy-is-hard-again/">that it's normal to struggle with constantly changing technologies</a>. It's also a fun journey through starting out in a business and exploring the in-depth details of a craft.</li>

<li>Eric Meyer is one of the people who have worked with CSS since the beginning and have deep insights into how it developed. He now wrote up some thoughts on <a href="https://meyerweb.com/eric/thoughts/2017/11/14/declining-complexity-in-css/">how the complexity of CSS changed over time</a>.</li>

<li>Vitaly Friedman wrote an article in which he asks us as developers, us as company founders <a href="https://www.smashingmagazine.com/2018/01/respect-always-comes-first/">to respect users</a>, and why it should matter more to all of us.</li>

<li>Last year, Matt Ludwig published an article about the problem of software compatibility over time and <a href="https://dockyard.com/blog/2017/10/24/software-rot-and-the-case-for-the-pwa-rewrite">why a Progressive Web App rewrite will be the solution to make it still work in fifty years</a>. The fallacy here is to think that the web is the same as twenty-five years ago. Today we face browsers removing a lot of APIs after a few years, putting existing features behind an HTTPS wall, and developers building code based on countless dependencies that are abandoned after some time by their authors. And once we’re building upon anything that is not the plain web standard, we’re not in a position anymore to say that the code will last for long.</li>

<li>Tim Kadlec is <a href="https://timkadlec.com/remembers/2018-02-14-the-two-faces-of-amp/">questioning the two faces of Google AMP</a> and claims that it can be either a Google search marketing tool or a tool for the open web to improve site performance but not both, as it’s trying to be.</li>

<li>John Cobb shares <a href="https://medium.freecodecamp.org/why-i-changed-the-way-i-think-about-code-quality-88c5d8d57e68">why he started to think about code quality differently</a> and why code reviews need to involve more than just viewing the code.</li>

</ul>

## UI/UX

<ul>

<li>This <a href="https://www.underconsideration.com/brandnew/archives/new_logo_identity_and_livery_for_lufthansa_done_in_house.php">case study</a> of how the Lufthansa brand evolved its design language and logo over time, including the latest subtle but still very different branding change, shows how much small details matter when it comes to improving a brand’s visual appearance.</li>

<li>Naema Baskanderi shares <a href="https://heydesigner.com/blog/best-practices-modals-overlays-dialog-windows/">best practices for modal windows and dialogs</a>, analyzing well-known modals and improving them.</li>

</ul>

<figure><a href="https://heydesigner.com/blog/best-practices-modals-overlays-dialog-windows/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e27eed31-2d4f-4706-b321-2ff9a94f8262/best-practices-modals-opt.png" width="800" height="324" alt="Best Practices For Modals" /></a><figcaption>Modals can be annoying and users often automatically dismiss these windows. Naema Baskanderi shares what you can do to <a href="https://heydesigner.com/blog/best-practices-modals-overlays-dialog-windows/">ensure your modal doesn't get in the way</a>. (<a href="https://heydesigner.com/blog/best-practices-modals-overlays-dialog-windows/">Image credit</a>)</figcaption></figure>

## Privacy

<ul>

<li>Firefox has been shipping with a privacy tracking protection for quite some time. Now they share the learnings from it and how we can <a href="https://blog.mozilla.org/data/2018/01/26/improving-privacy-without-breaking-the-web/">improve privacy without breaking the web</a>.</li>

<li>Holger Bartel takes Vitaly Friedman’s article “<a href="https://www.smashingmagazine.com/2018/01/respect-always-comes-first/">Respect Always Comes First</a>” as an opportunity to highlight the importance of respecting users by asking a very interesting question: <a href="https://www.foobartel.com/articles/respecting-users">Everyone wants to create better experiences, but what are you willing to do for it?</a> It’s not easy to find an answer and to blaze the trail for this in our work but an important part of building products.</li>

</ul>

## Security

<ul>

<li><a href="https://mobile.twitter.com/s_englehardt/status/960563090151628800">As it seems</a>, <a href="https://www.reddit.com/r/analytics/comments/7ukw4n/mixpanel_js_library_has_been_harvesting_passwords/">Mixpanel has inadvertently collected user passwords</a> for months with their Autotrack feature. If you use Mixpanel, you should upgrade to the latest version as soon as possible.</li>

</ul>

## Tooling

<ul>

<li>Monica Dinculescu shares how she wrote a script with Puppeteer, the Chrome team’s reference library to <a href="https://meowni.ca/posts/2017-puppeteer-tests/">automate headless Chrome to achieve automated visual diffing</a>.</li>

<li>Chrome 65 is coming soon, and it’ll bring a very handy feature to the Developer Tools: A <a href="https://mobile.twitter.com/ChromeDevTools/status/958037045795897344">contrast ratio tool in the color picker</a> that'll help identify contrast in color pairings.</li>

<li><a href="https://medium.com/webpack/webpack-4-beta-try-it-today-6b1d27d7d7e2">Webpack 4 is underway</a> with some performance improvements. It is now an out of the box zero configuration bundler and has way better bundle sizes due to massively better tree shaking.</li>

</ul>

<figure><a href="https://mobile.twitter.com/ChromeDevTools/status/958037045795897344"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f58bddc-2a18-4e4e-8d32-1b443ae52ac7/devtools-contrast-ratio-tool-opt.png" width="800" height="603" alt="DevTools Contrast Checker" /></a><figcaption>Coming soon to Chrome DevTools: a <a href="https://mobile.twitter.com/ChromeDevTools/status/958037045795897344">contrast ratio checker</a> in the color picker. (<a href="https://mobile.twitter.com/ChromeDevTools/status/958037045795897344">Image credit</a>)</figcaption></figure>

## Web Performance

<ul>

<li>Ben Robertson shares how we can <a href="https://benrobertson.io/front-end/lazy-load-connection-speed">lazy load videos and choose the quality based on the user’s connection speed</a>.</li>

<li>Seva Zaikov asks if the trend to build everything as Single Page Applications can be in the interest of users, and tries to find out <a href="https://blog.bloomca.me/2018/02/04/spa-is-not-silver-bullet.html">whether his assumption that they make websites slower can be backed by data</a>. The article is not a rant about tools like React but asks important questions we should ask ourselves before starting to build the technical architecture of a new project.</li>

</ul>

## HTML &amp; SVG

<ul>

<li>Did you know that for accessible tables it is required to have a <code>caption</code> element in your HTML? Stefan Judis explains <a href="https://www.stefanjudis.com/today-i-learned/the-for-accessibility-required-caption-element-in-html-tables/">how to do it</a>.</li>

</ul>

## JavaScript

<ul>

<li>There’s a new JavaScript framework around: <a href="https://stimulusjs.org/">Stimulus</a>, and it’s completely compatible with the HTML you already have and enhances the experience of your static templates.</li>

<li>Dave Rupert shares a very simple, modern way to <a href="https://daverupert.com/2018/02/cheapass-parallax/">create a parallax effect by manipulating CSS Custom Properties with JavaScript</a>.</li>

<li>For unidirectional data flow, we usually use WebSockets. But <a href="https://www.smashingmagazine.com/2018/02/sse-websockets-data-flow-http2/">with HTTP/2 we can use Server-Sent Events</a> as well, as Martin Chaov explains in his exemplary article.</li>

</ul>

<figure><a href="https://stimulusjs.org/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce8e8210-094a-4931-a97f-ed466eee73f6/stimulus-opt.png" width="800" height="611" alt="Stimulus" /></a><figcaption>The JavaScript framework <a href="https://stimulusjs.org/">Stimulus</a> is designed to augment your HTML. (<a href="https://stimulusjs.org/">Image credit</a>)</figcaption></figure>

## CSS

<ul>

<li>We already heard a couple of times about Houdini in browsers, a way to add our own CSS functionality via JavaScript. Now Surma shares <a href="https://developers.google.com/web/updates/2018/01/paintapi">how the CSS Paint API works</a> which will be available from Chrome 65 upwards. Effectively, this brings us a lot of possibilities that usually are only available for graphics or SVG to CSS.</li>

<li>Sarah Dayan explains how we can <a href="https://medium.freecodecamp.org/lets-make-your-svg-symbol-icons-multi-colored-with-css-variables-cddd1769fca4">create multi-colored icons with SVG symbols and CSS variables</a>.</li>

</ul>

## Accessibility

<ul>

<li>Marcy Sutton’s slide deck “<a href="https://marcysutton.github.io/a11y-and-ci/">Automating Peace Of Mind With Accessibility Testing &amp; Continuous Integration</a>” gives an idea and some hints on how we can continuously test the accessibility of websites.</li>

</ul>

## Work &amp; Life

<ul>

<li>Jon Gold wrote about <a href="https://jon.gold/2018/02/exhaust-ports/">finding the exhaust ports</a>. A good read about how technology influences us.</li>

<li>There’s some sort of common sense that tech companies who are doing well are always hiring. David Heinemeier Hansson explains why at Basecamp they now decided that <a href="https://m.signalvnoise.com/things-are-going-so-well-were-doing-a-hiring-freeze-5f66372a4214">things are going so well that they’re doing a hiring freeze</a>.</li>

<li>How do we decide when to iterate on things and when to rebuild? I ask myself this question a lot and now wrote up <a href="https://helloanselm.com/2018/making-things-better/">some conclusions on how to make things better</a>.</li>

</ul>

## Going Beyond…

<ul>

<li>Stephen Ilardi shares why <a href="https://www.wsj.com/articles/why-personal-tech-is-depressing-1509026300">personal tech is depressing</a>.</li>

<li>Mike Gifford shares his thoughts on <a href="https://medium.com/@mgifford/office-waste-reduction-591ab643dd8">reducing office waste</a>, a topic we talk about rarely, yet it’d be so simple to improve the situation and shape a future we still want to live in.</li>

</ul>

<p>Finally, I wrote up some personal notes about <a href="https://helloanselm.com/notes/2018-01-26-slack-notifications/">dealing with Slack notifications</a> and about <a href="https://helloanselm.com/notes/2018-01-26-acronyms/">why using acronyms is a bad idea</a>. If you have any thoughts about it, you're welcome to reply to me here or on Twitter.</p>

<p><em>We hope you enjoyed this Web Development Update. The next one is scheduled for March 16th. Stay tuned.</em></p>

{{< signature "cm" >}}


---
title: >-
  Monthly Web Development Update 3/2018: Service Workers, Building A CDN, And
  Cheating At Design
slug: monthly-web-development-update-3-2018
author: anselm-hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cc16c10-a98a-4941-91e2-f2fe2d69027a/sketch49-opt.png
date: '2018-03-16T14:29:29+01:00'
summary: >-
  As every month, Anselm Hannemann summarized what happened in the web
  development world in the last few weeks. A handy reading list full of browser
  news, performance tips, UX advice,  and much more to help you stay on top of
  things.
description: >-
  As every month, Anselm Hannemann summarized what happened in the web
  development world in the last few weeks. A handy reading list full of browser
  news, performance tips, UX advice,  and much more to help you stay on top of
  things.
categories:
  - Web Development Reading List
---
<p>Service Worker is probably one of the most misrepresented technologies we currently have. When I hear people talking about it, the topic almost always revolves around serving an app when a user is offline. However, Service Worker can do so much more than that, and every week I come across new articles that show how powerful the technology really is.</p>

<p>This month, for example, we can learn how to use Service Worker for cross-tab messaging and to load off requests into the background with the Background Sync API. I think the toolset we now have in our browsers already allows us to build great experiences regardless of the network state. Now it’s up to us to make the experiences so great that users truly love them. And that’s probably the hardest part.</p>

## News

<ul>

<li>Microsoft announced that <a href="https://blogs.windows.com/msedgedev/2018/03/13/bringing-expressive-performant-typography-to-microsoft-edge-with-variable-fonts/">support for Variable Fonts is coming in EdgeHTML 17</a>. This means that all major browser vendors are now working on implementing variable fonts into their software.</li>

<li>The <a href="https://theblog.adobe.com/march-2018-update-adobe-xd/">latest Adobe XD Update</a> brings a Photoshop and Sketch integration, so you can now open .psd and .sketch files, copy symbols between documents, and style grouped elements.</li>

<li>Chrome 65 is out, now shipping with the CSS Paint API, the Server Timing API, and support for <code>display: contents</code> (which is already built into Firefox and Safari as well). <a href="https://developers.google.com/web/updates/2018/03/nic65">This article explains the new features in detail</a>.</li>

<li>Great news: The <a href="https://mailman.nginx.org/pipermail/nginx-announce/2018/000207.html">nginx server now supports HTTP/2 Push</a> in the mainline release 1.13.9 (not stable yet).</li>

<li><a href="https://blog.sketchapp.com/prototyping-libraries-on-sketch-cloud-and-an-official-ios-ui-kit-in-sketch-49-bf090c70796c">Sketch 49</a> brings prototyping as native functionality.</li>

<li><a href="https://medium.com/webpack/webpack-4-released-today-6cdb994702d4">Webpack 4</a> was released and brings along build performance improvements of up to 98% and easier configuration.</li>

</ul>

<figure><a href="https://blog.sketchapp.com/prototyping-libraries-on-sketch-cloud-and-an-official-ios-ui-kit-in-sketch-49-bf090c70796c"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cc16c10-a98a-4941-91e2-f2fe2d69027a/sketch49-opt.png" width="800" height="429" alt="Sketch 49" /></a><figcaption><a href="https://blog.sketchapp.com/prototyping-libraries-on-sketch-cloud-and-an-official-ios-ui-kit-in-sketch-49-bf090c70796c">Sketch 49 has arrived</a>, and with it comes the new Prototyping in Sketch feature which lets you see the entire flow in action. (<a href="https://blog.sketchapp.com/prototyping-libraries-on-sketch-cloud-and-an-official-ios-ui-kit-in-sketch-49-bf090c70796c">Image credit</a>)</figcaption></figure>

{{% feature-panel %}}

## General

<ul>

<li>Ed Ellson examined <a href="https://notes.eellson.com/2018/02/11/chrome-the-background-sync-api-and-exponential-backoff/">Chrome’s Background Sync API</a> and the retry strategy it uses to perform a request. By allowing synchronization in the background after a first attempt has failed, the API helps us improve the browsing experience for users who go offline or are on unstable connections.</li>

</ul>

## UI/UX

<ul>

<li>Adam Wathan and Steve Schoger share <a href="https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886">seven practical tips for cheating at design</a> which we can apply directly. Strategies for clearer interfaces are also included.</li>

<li>Vivian Zhang explores the importance of <a href="https://uxplanet.org/designing-for-working-memory-6af1c0975304">designing for human working memory</a> and shares reasons why our designs should reduce cognitive loads.</li>

</ul>

<figure><a href="https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/417aa269-da65-486d-b480-3b0cd5b386f0/cheating-at-design-opt.png" width="800" height="310" alt="Cheating At Design" /></a><figcaption>Use color and weight to create visual hierarchy instead of size is only one of the <a href="https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886">seven practical tips for cheating at design</a> that Adam Wathan and Steve Schoger share. (<a href="https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886">Image credit</a>)</figcaption></figure>

## Security

<ul>

<li>With GraphQL you can query exactly what you want whenever you want. This is amazing for working with an API but also has complex security implications. Instead of asking for legitimate, useful data, a malicious actor could submit an expensive, nested query to overload your server, database, network, or all of these. To prevent this from happening, Max Stoiber shows us <a href="https://dev-blog.apollodata.com/securing-your-graphql-api-from-malicious-queries-16130a324a6b">how we can secure the GraphQL API</a> in our projects.</li>

</ul>

## Privacy

<ul>

<li>WebKit is <a href="https://webkit.org/blog/8124/introducing-storage-access-api/">introducing the Storage Access API</a>. The new API targets one of the major issues with Safari’s Intelligent Tracking Protection (ITP): Identifying users who are logged in to a first-party service but view content of it embedded on a third party (YouTube videos on a blog, for example). The Storage Access API allows third-party embeds to request access to their first-party cookies when the user interacts with them. A good solution to protect user privacy by default and allow exceptions on request.</li>

</ul>

## Web Performance

<ul>

<li>Janos Pasztor built his own Content Delivery Network because he thinks it can be a <a href="https://pasztor.at/blog/building-your-own-cdn">better solution than using existing third parties</a>. The code for the CDN of his personal website is <a href="https://github.com/janoszen/pasztor.at/tree/master/_ansible">now available on Github</a>. A nice web performance article that looks at common solutions from a different angle.</li>

<li>A year after Facebook’s announcement to broadly use <code>Cache-Control: Immutable</code>, Paul Calvano examined <a href="https://discuss.httparchive.org/t/cache-control-immutable-a-year-later/1195">how widespread its usage is on the web</a> — apart from the few big players. Interesting research and it’s still sad to see that this useful performance tool is used so little. At <a href="https://colloq.io/">Colloq</a>, we use it quite a lot, which saves us a lot of traffic and load on our servers and enables us to serve a lot of pages nearly instantly to recurring users.</li>

</ul>

<figure><a href="https://pasztor.at/blog/building-your-own-cdn"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a770185d-e93c-4dbe-a84f-490e89608e6a/building-you-own-cdn-opt.png" width="800" height="517" alt="Global stats of a self-built CDN" /></a><figcaption>Global stats for the <a href="https://pasztor.at/blog/building-your-own-cdn">custom CDN that Janos Pasztor built</a>. (<a href="https://pasztor.at/blog/building-your-own-cdn">Image credit</a>)</figcaption></figure>

## HTML &amp; SVG

<ul>

<li>Scott Jehl wrote about <a href="https://www.filamentgroup.com/lab/sizes-swap/">swapping images with the <code>sizes</code> attribute</a> without any JavaScript magic. A nice reminder of how powerful <code>sizes</code> and <code>srcset</code> are when combined.</li>

</ul>

## JavaScript

<ul>

<li>Addy Osmani wrote up the fundamentals of <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/loading-third-party-javascript/">loading third-party JavaScript</a>. The guide takes privacy, security and performance problems into account.</li>

<li>Jad Joubran shares how to <a href="https://medium.com/@JoubranJad/running-fetch-in-a-web-worker-700dc33ac854">run <code>fetch</code> in a Web Worker</a> to offload it from the main thread into its own. This could be a useful experiment for tasks where expensive requests are triggered, and maybe even at regular intervals.</li>

<li>James Milner shares how we can <a href="https://www.loxodrome.io/post/tab-state-service-workers/">use a Service Worker to send messages between browser tabs</a> that are in the same domain scope.</li>

</ul>

## CSS

<ul>

<li>Sara Soueidan explains the <a href="https://css-tricks.com/auto-sizing-columns-css-grid-auto-fill-vs-auto-fit/">difference between CSS Grid’s <code>auto-fill</code> and <code>auto-fit</code></a>.</li>

<li>Jens Oliver Meiert’s new article “<a href="https://alistapart.com/article/we-write-css-like-we-did-in-the-90s-and-yes-its-silly">We write CSS like we did in the 90s, and yes, it’s silly</a>” is a thought-provoking piece that shows that despite more tooling and conventions, we fail to improve how we write CSS. This is not about writing CSS in Javascript or a class naming convention but more about how our tools work and how we try to optimize things while keeping the bigger picture intact.</li>

<li>Preethi Sam shares various tricks on how to create <a href="https://css-tricks.com/css-techniques-and-effects-for-knockout-text/">knockout text effects with pure CSS</a>. Interesting to see how many different techniques we have nowadays to create such effects.</li>

</ul>

## Accessibility

<ul>

<li>Stefan Judis <a href="https://www.stefanjudis.com/useful-accessibility-resources/">collected good and useful accessibility resources</a>.</li>

<li>Heydon Pickering wrote about <a href="https://inclusive-components.design/notifications/">building inclusive notifications</a>, not only from a technical perspective but the user experience point of view. This resource gives useful advice for designing notifications, what content to include, and how and when to present them to users.</li>

<li>Harris Schneiderman explains how to create an <a href="https://www.smashingmagazine.com/2018/01/dragon-drop-accessible-list-reordering/">accessible list reordering component</a>.</li>

<li>Vox Media shared their <a href="https://accessibility.voxmedia.com/">accessibility guidelines</a>. A great interactive checklist we can use to confirm that we did our job correctly.</li>

</ul>

<figure><a href="https://accessibility.voxmedia.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6da96ca-9aae-449a-895c-59102a749477/accessibility-checklist-opt.png" width="800" height="515" alt="Accessibility Checklist" /></a><figcaption>The <a href="https://accessibility.voxmedia.com/">Accessibility Checklist</a> helps build accessibility into your process no matter your role or stage in a project. (<a href="https://accessibility.voxmedia.com/">Image credit</a>)</figcaption></figure>

## Work &amp; Life

<ul>

<li>This week I read an <a href="https://the-pastry-box-project.net/alex-duloz/2018-march-9">article by Alex Duloz</a>, and his words still stick with me: “When we develop a new application, when we post content on the Internet, whatever we do that people will have access to, we should consider just for a minute if our contribution adds up to the level of dumbness kids/teenagers are exposed to. If it does, we should refrain from going live.” The truth is, most of us, including me, don’t consider this before posting on the Internet. We create funny things, share funny pictures and try to get fame with silly posts. But in reality, we shape society with this. Let’s try to provide more useful resources and make the consumption of this more enjoyable so young people can profit from our knowledge and not only view things we think are funny. “We should always consider how teenagers will use what we release.”</li>

<li>The MIT OpenCourseWare released <a href="https://ocw.mit.edu/courses/audio-video-courses/">a lot of free audio and video lectures</a>. This is amazing news and makes great content available to broader masses.</li>

<li>Jake Knapp says <a href="https://medium.com/@jakek/great-work-requires-idealism-and-cynicism-7d19f4f61aa0">great work requires idealism and cynicism</a> and has strong arguments to back up this theory. An article worth reading.</li>

<li>There’s an important article on <a href="https://qz.com/1190151/why-am-i-unhappy-a-new-study-explains-americas-unhappiness-epidemic/">how unhappiness has grown in America’s population since around the year 2000</a>. It reveals that while income inequality might play a role, the more important aspect is that young people who use a lot of digital media are unhappier than those who use it only up to an hour a day. Interestingly, people who don’t use digital media at all, are unhappy, too, so the outcome of this could be that we should try to use digital media only moderately — at least in our private lives. I bet it’ll make a big difference.</li>

<li>Following the theory of Michael Bradley, projects don’t necessarily need a roadmap for success. Instead, he suggests to <a href="https://purpose.do/success-roadmap-moral-compass/">create a moral compass that points out <em>why</em> the project exists</a> and what its purpose is.</li>

</ul>

## Going Beyond…

<ul>

<li><a href="https://kottke.org/18/02/why-do-we-forget-most-of-what-we-read-and-watch">Why do we forget most of what we read and watch?</a> Jason Kottke tries to find answers.</li>

<li>Anton Sten reminds us of wise words from Apple CEO Tim Cook: “<a href="https://www.antonsten.com/timcook/">You have to make sure that you’re focused on the thing that matters</a>.” We can not only apply that to business but also to our own lives: Focus on things that really matter, and embrace them.</li>

</ul>

<p>We hope you enjoyed this Web Development Update. The next one is scheduled for April 13th. Stay tuned.</p>


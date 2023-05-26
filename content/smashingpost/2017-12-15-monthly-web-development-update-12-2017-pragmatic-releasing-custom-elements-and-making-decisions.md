---
title: >-
  Monthly Web Development Update 12/2017: Pragmatic Releasing, Custom Elements,
  And Making Decisions
slug: monthly-web-development-update-12-2017
author: anselm-hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fef2c4b0-a81c-4d71-84e0-d8d9716d1e3f/pragmatic-releasing-opt.png
date: '2017-12-15 12:18:30'
summary: >-
  What happened in the web community in the last few weeks? Anselm Hannemann
  summarizes everything that’s new and important so that you don’t miss out on
  anything.
description: >-
  What happened in the web community in the last few weeks? Anselm Hannemann
  summarizes everything that’s new and important so that you don’t miss out on
  anything.
draft: false
categories:
  - Web Development Reading List
---
<p>Today I read an <a href="https://highline.huffingtonpost.com/articles/en/poor-millennials/">eye-opening article</a> about the current young generation and their financial future. It’s hard to grasp words like “Millenials”, and there’s much talk about specific issues they face, but, for many of us, it’s not easy to understand their struggle — no matter if you’re older or younger than me (I qualify under the Millenial generation). But Michael Hobbes’ entertaining and super informative article revealed a lot to me. Not only that I now understand — and even relate to — quite some of the facts outlined there, but also because the article shows how different age groups form a society, unaware of the <strong>impact their decisions might have</strong> on other people’s lives.</p>

<p>As web professionals, we can relate to that in many aspects. When building web projects, we make decisions and often base them on what is best for us — as a developer, as an entrepreneur, as a marketing strategist, as support staff —, not thinking about how these decisions might affect other people. By building inaccessible websites, we exclude millions of users; by implementing better analytics events and libraries, we give data of our users to third-parties. It sometimes seems impossible to make a decision that is right, and we feel so overwhelmed by the fact that we can’t do the right thing that we dismiss all the reasonable, all the well-informed decisions, and focus solely on what’s best for ourselves. We can be smarter. And while we probably <strong>won’t be able to do everything right</strong>, we can still take small steps instead of getting overwhelmed. It’s not easy, but maybe it’s something for a new year’s resolution?</p>

{{% feature-panel %}}

## News

<ul>

<li>Big <a href="https://blog.whatwg.org/working-mode-changes">news regarding the WHATWG</a>: The organizations behind the four major integrated browser engines — Apple, Google, Microsoft, and Mozilla — developed an Intellectual Property Rights (IPR) Policy and governance structure for the WHATWG. This will hopefully result in an improved living standard that provides a more useful resource.</li>

<li>Actually launched already back in November, here’s what’s new in <a href="https://developer.mozilla.org/en-US/Firefox/Releases/57">Firefox 57</a>. It now comes with a new, super-fast Quantum engine. Web extensions have become a reality, too, and a lot more bugfixes for old issues and performance improvements can be expected in the future. But what about us developers? Firefox 57 supports <code>&lt;input type="\\[date|time]"&gt;</code>, lots of CSS bugs were fixed thanks to the new engine, and the Performance Observer API is now enabled, just like the Storage API and the Abort API (e.g. for fetch-requests). Last but not least, the headless mode now supports the incredibly useful <code>--screenshot</code> flag. By the way, the Quantum engine is coming to Firefox on Android 59 soon as well.</li>

<li><a href="https://developers.google.com/web/updates/2017/12/nic63">Chrome 63 is out now</a> with some awesome new features: Dynamic JavaScript modules, <code>async</code> iterators and generators, CSS <code>overscroll-behavior</code> (which natively supports pull to refresh), and support for the <code>Intl.PluralRules</code> API</a>, for example. Furthermore, the Permissions UI now asks for permission in a modal to make clear that site owners should only ask for additional permissions when necessary and useful. The <a href="https://wdrl.info/archive/201/the-intl-pluralrules-api-web-google-developers"><code>Intl.PluralRules</code> API</a> is also included in this version.</li>

</ul>

## General

<ul>

<li>Amazon is amazing, right? Their cloud is fast, big, and cheap. Their shop offers everything and delivers quickly. This week, Amazon Web Services announced something very interesting: “AWS now provides the U.S. Intelligence Community a commercial cloud capability across all classification levels: Unclassified, Sensitive, Secret, and Top Secret.” Yes, you read it right: It seems like Amazon will be the responsible company for hosting U.S. Intelligence service’s top-secret data. I’m pretty sure it’s not a good idea that government services start to fully rely on a company’s exclusive Cloud service with no option to easily switch back to a competitor or their own alternative. Put it in relation to what Amazon is: Up to <a href="https://www.smashingmagazine.com/2016/01/web-development-reading-list-120-backup-security-safari-chakra/#general">70% of the internet traffic</a> goes through the AWS Virginia data center, Amazon wants a <a href="https://www.smashingmagazine.com/2017/04/web-development-reading-list-180/#privacy">camera and microphone in your bedroom</a>, your living room and also a smart key to your flat or house, and it’s already <a href="https://www.smashingmagazine.com/2017/05/web-development-reading-list-183/#going-beyond">impossible to not use AWS</a> if you use the internet. What will happen to the U.S. Intelligence community if this AWS secure cloud <a href="https://www.smashingmagazine.com/2017/03/web-development-reading-list-173/#general">suffers from an outage as it happened this year</a>? Will they still be able to operate? What if it happens during an active investigation?</li>

</ul>

## Tooling

<ul>

<li>Who of us doesn’t know the big challenges of releases and how time-consuming they can be. Raymond Rutjes now suggests that <a href="https://blog.algolia.com/pragmatic-releasing/">making a release should be possible for everyone</a> in the team. It should be easy, worry-free and — maybe most importantly — fast.</li>

<li>Francesco Schwarz built a <a href="https://francescoschwarz.de/en/blog/introducing-the-specificity-visualizer/">new tool to visualize your CSS’ specificity</a>. Very helpful to analyze some misconceptions in your structure or to identify modules that should be refactored.</li>

</ul>

<figure><a href="https://blog.algolia.com/pragmatic-releasing/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/596c0690-15e1-457e-9e50-8537a5a5f4ee/pragmatic-releasing-opt.png" width="800" height="444" alt="Pragmatic releasing" /></a><figcaption>Less worry, more shipping. That’s <a href="https://blog.algolia.com/pragmatic-releasing/">pragmatic releasing</a>. (<a href="https://blog.algolia.com/pragmatic-releasing/">Image source</a>)</figcaption></figure>

## UI/UX

<ul>

<li>With <a href="https://design.google/library/spectral-new-screen-first-typeface/">Spectral</a>, there’s a new screen-first serif typeface available under an open-source license.</li>

<li>John Moore Williams shares his <a href="https://webflow.com/blog/best-practices-for-site-search-design">best practices for site search design</a>. Important tips if you want to provide your users with an impactful, powerful search experience.</li>

</ul>

## Web Performance

<ul>

<li>Michael Scharnagl explains how we can use Service Workers (which are basically a web proxy) to <a href="https://justmarkup.com/log/2017/11/network-based-image-loading/">load images based on the Network Information API</a>.</li>

<li>Harry Roberts often finds the right words to uncover issues that aren’t obvious to a lot of people. His article “<a href="https://csswizardry.com/2017/11/the-fallacies-of-distributed-computing-applied-to-front-end-performance/">The Fallacies of Distributed Computing (Applied to Front-End Performance)</a>” is about making assumptions for users and about actively neglecting or overthinking problems such as network performance.</li>

<li>“<a href="https://alistapart.com/article/the-best-request-is-no-request-revisited">The Best Request Is No Request, Revisited</a>” is a new article by Stefan Baumgartner that explains what you can do with HTTP/2 right now and the changes that work in theory but not yet in practice.</li>

<li>Samuel Parkinson explains <a href="https://medium.com/@samparkinson_/making-a-request-to-the-financial-times-b2119a2f422d">what happens when you visit ft.com</a>. An in-depth insight that starts with the DNS and continues the journey through the complete request workflow of the Financial Times.</li>

</ul>

<figure><a href="https://medium.com/@samparkinson_/making-a-request-to-the-financial-times-b2119a2f422d"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/288ba761-6497-4dce-8c58-7d3bc425df83/ft-performance-opt.png" width="800" height="334" alt="Financial Times Stack" /></a><figcaption>The simplified ft.com stack. For more insights, be sure to check out <a href="https://medium.com/@samparkinson_/making-a-request-to-the-financial-times-b2119a2f422d">Sam Parkinson’s article</a>. (<a href="https://medium.com/@samparkinson_/making-a-request-to-the-financial-times-b2119a2f422d">Image source</a>)</figcaption></figure>

## Security

<ul>

<li>4iQ, an identity safeguarding company, found a <a href="https://medium.com/4iqdelvedeep/1-4-billion-clear-text-credentials-discovered-in-a-single-database-3131d0a1ae14">leaked database containing 1.4 billion clear text credentials</a> in the Dark Web. It’s probably the largest known resource available yet, and shows once more how important it is to use unique passwords for each service.</li>

<li>HSTS is a method to tell a browser to only connect to certain hostnames via the secure HTTPS protocol. However, the way it currently is implemented in browsers is <a href="https://blog.en.elevenpaths.com/2017/12/breaking-out-hsts-and-hpkp-on-firefox.html">pretty much broken</a> and vulnerable to attacks, as research prominently shows.</li>

<li>Tobias Tom shares how at Colloq they implemented a <a href="https://colloq.io/blog/how-our-password-check-works">password check</a> that prevents users from choosing a password that has been exposed in a public data breach. It’s based on the amazing dataset by Troy Hunt and shares some interesting data on how to check against a 40GB Postgres dataset without affecting your site’s performance.</li>

<li>You’ve probably heard of crypto mining in the browser already. A newly discovered script <a href="https://blog.malwarebytes.com/cybercrime/2017/11/persistent-drive-by-cryptomining-coming-to-a-browser-near-you/">checks for WebAssembly support</a> to make full advantage of the hardware’s capability and then launch a pop-under window that mines cryptocurrency in the background. The only mitigation is to manually force close all the task processes of the browser. However, there are also some browser extensions available that block the most common mining scripts directly.</li>

</ul>

## Accessibility

<ul>

<li>What’s the best approach to designing and coding a table that works for everyone? Adrian Roselli shares <a href="https://adrianroselli.com/2017/11/a-responsive-accessible-table.html">how to create responsive, accessible tables</a>.</li>

<li>This is Marcy Sutton taking on <a href="https://www.24a11y.com/2017/writing-automated-tests-accessibility/">the value of writing automated tests for accessibility</a> and why having such doesn’t mean we don’t need to do manual accessibility work anymore.</li>

</ul>

## CSS

<ul>

<li>Jonathan Snook explains how we can <a href="https://snook.ca/archives/html_and_css/calendar-css-grid">build a calendar layout with CSS Grid</a>.</li>

<li>With the <a href="https://drafts.csswg.org/selectors-4/#is">upcoming CSS Selectors Level 4 specification</a> we will get an <code>:is</code> pseudo selector similar to <code>:matches</code> but without increasing the specificity.</li>

</ul>

## JavaScript

<ul>

<li>Brian Kardell wrote an important post about how we can soon use <a href="https://bkardell.com/blog/TheWalrus.html">Custom Elements as an extension of a common native element</a>. This is especially great as we then won’t need to build everything from scratch but will be able to extend native elements with customizations while still inheriting the full accessibility and usability from the native element. Apart from that, this feature allows building progressively enhanced Custom Elements.</li>

<li>Achieving container queries with modern tools in JavaScript? Ali Alaa shares <a href="https://codeburst.io/media-queries-based-on-element-width-with-mutationobserver-cf2eff172787">how we can do it with MutationObserver</a>.</li>

<li>Safari has dynamic JavaScript <code>import()</code> support already in the preview builds, and Chrome 63 will support it as well. Mathias Bynens <a href="https://developers.google.com/web/updates/2017/11/dynamic-import">explains what this means and how we can use it</a>. <code>import()</code> basically is <code>import</code> on fire and lets you load entire JavaScript modules on the fly only when you really need them.</li>

<li>Jake Archibald explains <a href="https://jakearchibald.com/2017/await-vs-return-vs-return-await/">the subtle but vital difference</a> between <code>await</code>, <code>return</code>, and <code>return await</code> and gives tips on when to use which.</li>

</ul>

<figure><a href="https://codeburst.io/media-queries-based-on-element-width-with-mutationobserver-cf2eff172787"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b61475-4640-48c0-abb8-0c2706a4f5ef/mutation-observer-opt.png" width="800" height="484" alt="Media Queries with MutationObserver" /></a><figcaption>If you’ve ever wished that media queries were based on elements’ width rather than the entire viewport, <a href="https://codeburst.io/media-queries-based-on-element-width-with-mutationobserver-cf2eff172787">Ali Alaa’s workaround</a> is for you. (<a href="https://codeburst.io/media-queries-based-on-element-width-with-mutationobserver-cf2eff172787">Image source</a>)</figcaption></figure>

## Work & Life

<ul>

<li>“There was a time when you could write a few poems, die of TB, and call it a life well lived.” Quinn Norton published a thought “<a href="https://medium.com/message/against-productivity-b19f56b67da6">Against Productivity</a>” and about the weird strive in all of us for more productivity in life.</li>

<li>James Clear explains <a href="https://jamesclear.com/entropy">why life always seems to get more complicated</a> and what we can do to not feel overwhelmed by this.</li>

<li>According to The Guardian, a lot of employers are already using a range of technologies to <a href="https://www.theguardian.com/world/2017/nov/06/workplace-surveillance-big-brother-technology">monitor their employees’ web-browsing patterns</a>, keystrokes, social media posts and even private messaging apps. It’s work surveillance that shows absolute mistrust of the company towards its staff. But what can you do if your employer does the same? Best is probably to talk to your boss that you think they don’t value your work and that it feels as if they mistrust you if they monitor you.</li>

<li>Ryan Singer shares why just <a href="https://m.signalvnoise.com/running-in-circles-aae73d79ce19">doing Agile doesn’t work</a>. The problems lie in doing the wrong things, building to specs, and getting distracted. Finding the right things to work on, doing them carefully and in cycles is real agile working. Don’t be distracted by numbers and terms, and focus on the important things instead.</li>

<li>Alida Miranda-Wolff broaches the issue of why “move fast and break things” is a bad idea when it comes to people because then <a href="https://blog.usejournal.com/dontmovefastandbreakthings-697e6a5b3d7a">the “thing” being broken is a person</a>. The issue of working hours, happiness at work, growing talent and why it’s tempting to follow hurtful patterns.</li>

<li>Dan Kim shares why he thinks <a href="https://m.signalvnoise.com/its-time-for-recurring-meetings-to-end-bb462441076e">it’s time for recurring meetings to end</a> in order to work together in a way that doesn’t waste time but focuses on important things that need to be discussed. A plea to think reasonably about recurring meetings.</li>

</ul>

<figure><a href="https://m.signalvnoise.com/running-in-circles-aae73d79ce19"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69c3f34a-0fda-4f0f-85ce-b03883ee19f4/running-in-circles-opt.png" width="800" height="421" alt="Running In Circles" /></a><figcaption>Work that requires problem solving is like a hill. Ryan Singer <a href="https://m.signalvnoise.com/running-in-circles-aae73d79ce19">explains why Agile doesn’t work</a> in that case. (<a href="https://m.signalvnoise.com/running-in-circles-aae73d79ce19">Image source</a>)</figcaption></figure>

## Going Beyond…

<ul>

<li>Scott Berkun explains <a href="https://scottberkun.com/2017/why-the-right-change-often-feels-wrong/">why the right change often feels wrong</a>. If you can relate to it, I recommend reading this article as it helps you understand why we feel that way and why this is natural.</li>

<li>The folks behind the great Do Lectures series shared <a href="https://medium.com/@dolectures/100-must-read-books-of-2017-12ab9b648d03">100 books of 2017</a> they recommend us to read. And while I won’t be able to read all hundred books, there are some great tips in the list which qualify as a nice end-of-year read.</li>

<li>In the past months, I’ve read more and more articles from people who work or have worked for social media companies and now talk about <a href="https://www.theverge.com/2017/12/11/16761016/former-facebook-exec-ripping-apart-society">how such services are contributing massively to ripping apart our society</a>. This is another one showing the problem of misinformation, AI-influenced aggregated “timelines” that only make things worse instead of unifying society and helping people. While there is much value in social media, there’s an underlying issue in most big services: In strive for more revenue and new features, these services try to match interests to people and fail horribly because they match the interests quite good instead of providing eye-opening, neutral and objective content to users that would make them reflect their views and interests.</li>

</ul>

<p><em>We hope you enjoyed this Web Development Update. The next one is scheduled for January 19th. Stay tuned!</em></p>

{{< signature "il" >}}


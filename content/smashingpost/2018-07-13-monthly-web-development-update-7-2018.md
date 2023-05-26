---
title: 'Monthly Web Development Update 7/2018: Practical Accessibility, Design Mistakes, And Feature Control'
slug: monthly-web-development-update-7-2018
author: anselm-hannemann
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c524a3a0-3a7a-49ef-81b5-5219a7b37b9e/form-with-color-based-indicators.jpg
date: 2018-07-13T14:20:17+02:00
summary: >-
  Staying up to date with the latest techniques, browser updates, and hot topics can be quite a challenge. Every month, Anselm summarizes what’s been going on in the web industry, so you can easily catch up on everything new and important. 
description: >-
  Staying up to date with the latest techniques, browser updates, and hot topics can be quite a challenge. Every month, Anselm summarizes what’s been going on in the web industry, so you can easily catch up on everything new and important.
categories:
  - Web Development Reading List
drafts: true
---
<p>The web continues to amaze me. With all its variety and different changes to the platform, it’s hard to see a straight pattern &mdash; if there even is (just) one. But it’s wonderful to see what is being changed, which features are added to the platform, which ones get deprecated, and how browsers implement more and more technology to protect the user from malicious website attacks. It’s interesting to see that these security features nowadays are getting as much attention as a feature for developers; this shows <strong>the importance of privacy and security</strong> and how unstable and insecure the web was in the past. </p>

<p>But the best thing about all of this is that it shows how important it is to stick to the things that people give us. Instead of implementing our own solutions for everything, it’s often much better to re-use an existing system. Not only is it safer to rely on, but also less work while more inclusive to extend a native DOM element with a custom element (instead of writing our own custom element from scratch). If we think about whether we should build our own version of SSL or use an existing software for this, why would we build a clickable element based on nothing instead of altering the behavior of an <code>a</code> or <code>button</code> element? And why would we check for resource host validation on our own, if the browser already gives us an API for that? This week’s articles are all dedicated to these topics.</p>

<p>Another thing that has been stuck in my head is Andrea Giammarchi’s article, “<a href="https://medium.com/@WebReflection/a-bloatless-web-d4f811c7991b">A Bloatless Web</a>,” in which he describes how we blindly use Babel as developers when we write JavaScript to be able to write modern ECMAScript. But we usually don’t realize that transpiling all of our modern code in modern browsers isn’t the most efficient way. I’m glad that Andrea offers some ideas on how we can improve that situation and improve our web apps’ performance. Wouldn’t it be amazing to just serve a third of the bundle size by not transpiling the code anymore for each and every browser?</p>

## News

<ul>
<li>Site Isolation effectively makes it harder for untrusted websites to access or steal information from your accounts on other websites. <a href="https://developers.google.com/web/updates/2018/07/site-isolation">Chrome 67 is now shipping with it</a> and Cross-Origin Read Blocking (CORB) will no longer load, e.g. a JSON file as image. But even further, these changes mean that full-page layout is no longer guaranteed to be synchronous. This new feature affects you if you read out calculated sizes from an element in JavaScript or use <code>unload</code> event listeners.  Ensure that you know about this and check if your sites still work as expected.</li>
<li>By now, we know a bit about Content Security Policies — a feature that lets developers limit the load of certain resources by hostnames. But browser vendors have come up with something new now: Feature Policy. This allows web developers to selectively enable, disable, or modify the behavior of certain APIs and web features in the browser. It’s like CSP but instead of controlling security, it controls features and <a href="https://developers.google.com/web/updates/2018/06/feature-policy">Eric Bidelman wrote an introduction to Feature Policy</a> explaining everything.</li>
<li>The Brave browser team shows their latest feature to protect their users’ privacy: <a href="https://brave.com/tor-tabs-beta/">Tabs that connect via the Tor network</a>.</li>
</ul>

{{% feature-panel %}}

## Generic

<ul>
<li>Anton Sten asks if <a href="https://www.antonsten.com/values/">Tech Sector Values are Broken?</a> Analyzing the marketing strategies by Apple, Microsoft, Google, Amazon but also small other companies and how we can do really purposeful work and stick to our values instead of treating them as marketing-material that we don’t need to respect or stick to.</li>
<li>Now that the technology sector of the world is rapidly transforming all of the world’s things into digital things, many have called for more ethics in our field. That is in many instances quite a vague goal, so let’s apply it to one part of digital: front-end development. <a href="https://hiddedevries.nl/en/blog/2018-07-05-what-kind-of-ethics-do-front-end-developers-need">How can we be more ethical as front-end developers, what kinds of things can we do</a>? Hidde de Vries wrote an article about that.</li>
</ul>

## Security

<ul>
<li>Ticketmaster’s customer data has been compromised and as it seems, <a href="https://www.itwire.com/security/83416-uk-researcher-says-one-line-of-code-caused-ticketmaster-breach.html">it’s due to a customized single line of code that includes a third-party script</a>.</li>
</ul>

## UI/UX

<ul>
<li>Eugen Eşanu shows <a href="https://uxplanet.org/10-small-design-mistakes-we-still-make-1cd5f60bc708">ten small design mistakes we still make</a> and what we can do instead to make our design more user-friendly.</li>
</ul>

{{< rimg href="https://uxplanet.org/10-small-design-mistakes-we-still-make-1cd5f60bc708" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9c093b8-ed81-46f8-8dfc-758c3a591bb1/what-we-design.png" sizes="100vw" caption="Users do not have time to read more than necessary, and yet designers still tend to put a lot of text because they think people need to know that. (<a href='https://uxplanet.org/10-small-design-mistakes-we-still-make-1cd5f60bc708'>Image source</a>)" alt="what we design vs. what a user needs" >}}

## Privacy

<ul>
<li>This is an interesting report about <a href="https://www.businessinsider.de/google-allows-app-developers-to-read-peoples-gmails-report-2018-7">how Google allows outside app developers to read people’s Google emails</a> when they grant permission during app authorization. The issue with that is that there is no way to easily prevent that and it might have quite some impact if you use Gmail for your company as it might affect privacy policies and is under subject of GDPR.</li>
</ul>

## Web Performance

<ul>
<li>Max Böck on how we can build <a href="https://mxb.at/blog/connection-aware-components/">components that react to the actual device connection speed</a> using the Network Information API. And despite it’s currently only available in Chrome and Samsung Internet browsers, it’s worth trying it out and maybe already serve it to these users.</li>
<li>From time to time, we can still read articles mentioning the importance of optimizing CSS selectors in order to improve performance. This originates in research done several years ago but Ivan Čurić researched this again <a href="https://www.sitepoint.com/optimizing-css-id-selectors-and-other-myths/">and found out it doesn’t matter</a>.</li>
</ul>

## Accessibility

<ul>
<li>Microsoft’s developer team shares a <a href="https://www.youtube.com/playlist?list=PLtSVUgxIo6KqBBGqNdPQG64f-hTs1YxFM">video playlist about practical accessibility</a>, including how to optimize presentations or language for inclusion or how to build a proper “skip navigation” functionality on your website.</li>
<li>Sara Novak shares how she managed to show empathy by <a href="https://blog.prototypr.io/going-colorblind-an-experiment-in-empathy-and-accessibility-98b7003737ca">experimenting with going colorblind</a> to understand how other people experience the world differently.</li>
<li>The Developer Tools of Firefox now have an <em>Accessibility Inspector</em> mode. <a href="https://developer.mozilla.org/en-US/docs/Tools/Accessibility_inspector#Accessing_the_accessibility_inspector">Here’s how to activate it and how to use it</a>.</li>
</ul>

{{< rimg href="https://blog.prototypr.io/going-colorblind-an-experiment-in-empathy-and-accessibility-98b7003737ca" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c524a3a0-3a7a-49ef-81b5-5219a7b37b9e/form-with-color-based-indicators.jpg" sizes="100vw" caption="In her article, Sara Novak explains why it's important not to rely on color alone as an indicator. Symbols and error message can be much more helpful to users. (The image above shows a form with color-based indicators. Left: How a person with normal vision sees a form with color-based indicators. Right: How a deuteranomalous person sees the same form.) (<a href='https://blog.prototypr.io/going-colorblind-an-experiment-in-empathy-and-accessibility-98b7003737ca'>Image source</a>)" alt="A form with color-based indicators" >}}

## JavaScript

<ul>
<li>Leon Revill show us how we can <a href="https://blog.revillweb.com/extending-native-dom-elements-with-web-components-233350c8e86a">extend existing native DOM elements with Web Components</a>. This is extremely helpful and useful as we can not only save a lot of time by using prebuilt templates for custom elements but also get all the optimizations and defaults (semantics, accessibility, browser functionality) for free and still can build our own behavior on top of it. At the very least, <a href="https://caniuse.com/#feat=custom-elementsv1">if we could use Custom Elements at all</a>, but that’s a different story.</li>
<li>Gerardo Rodriguez shows how we can easily fail to optimize websites for performance with Service Workers and the Fetch API and how this can result in a quota exception in browsers. Luckily, he found out the reason of this and by setting the proper CORS headers, Gerardo finally <a href="https://cloudfour.com/thinks/when-7-kb-equals-7-mb/">solved the mystery of single-cached opaque responses</a> and tells us how to avoid the issues.</li>
<li>Filepond is a nice open-source JavaScript file uploader. Rik Schennink <a href="https://itnext.io/filepond-frontend-trickery-a3073c934c77">shares the challenges faced building it</a>.</li>
<li>Andrea Giammarchi about <a href="https://medium.com/@WebReflection/a-bloatless-web-d4f811c7991b">the problem of bundling JavaScript with Babel and why transpiling code isn’t the best solution anymore</a>. Instead, we should think about how to serve different bundles depending on the browser support to decrease the bundle size and improve performance.</li>
<li>Justin Fuller shares <a href="https://medium.freecodecamp.org/here-are-three-upcoming-changes-to-javascript-that-youll-love-387bce1bfb0b">three great new features coming to JavaScript soon</a> that will help us write code that is easier to understand, such as operational chaining, nullish coalescing, or the pipeline operator.</li>
<li>Addy Osmani and Mathias Bynens wrote a primer introduction on <a href="https://developers.google.com/web/fundamentals/primers/modules">how we can use JavaScript modules on the web today</a>.</li>
</ul>

{{% ad-panel-leaderboard %}}

## CSS

<ul>
<li>An article series that covers how we can <a href="https://css-tricks.com/css-grid-in-ie-faking-an-auto-placement-grid-with-gaps/">fake an auto-placement grid with gaps in Internet Explorer</a>.</li>
<li>CSS Grid is nice, but I often hear that people can’t use it because IE11 doesn’t support it well. But that’s not exactly true as IE11 has a prior version of CSS Grid available that we can easily transpile with autoprefixer. Daniel Tonon explains the <a href="https://css-tricks.com/css-grid-in-ie-debunking-common-ie-grid-misconceptions/">CSS Grid differences and which features we can and cannot use</a> and <a href="https://css-tricks.com/css-grid-in-ie-css-grid-and-the-new-autoprefixer/">will continue with even more tips</a>.</li>
<li>For many people, CSS Grid is still very new, and it’s very capable and helps us solve a lot of problems when creating grid-based layouts in CSS. But in the current version, there are a couple of things that are still not possible. <a href="https://www.smashingmagazine.com/2018/07/css-grid-2/">CSS Grid level 2 will bring us sub-grids</a> and Rachel Andrew explains what you need that for.</li>
<li>Is CSS-in-JS good? Is it just bad? Why we constantly fall into the trap of arguing when there are no clear winners and <a href="https://foobartel.com/articles/css-in-js-kindness-and-evolution">how we can do better</a> by acknowledging evolution and seeing things in context.</li>
</ul>

## Work & Life

<ul>
<li>Why <a href="https://helloanselm.com/writings/build-to-last">the concept of patience and the strive to build something to last should gain more attention in business</a>. Some thoughts that came into my mind when reading another article and it seems many people like the idea behind this.</li>
<li><a href="https://ethanmarcotte.com/wrote/just-work/">Ethan Marcotte on how he approaches to choose clients</a> and why he thinks it’s important to only choose clients that you can ethically support. But this also shows how difficult this can be sometimes, as recent discussions about Microsoft’s business cooperations with legal entities show.</li>
</ul>

{{< signature "il" >}}
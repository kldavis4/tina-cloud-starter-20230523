---
title: 'How Partytown Eliminates Website Bloat From Third-Party Scripts'
slug: partytown-eliminates-website-bloat-third-party-apps
author: steve-sewell
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9925c2d1-b244-434d-9173-7e11efbdf617/partytown-eliminates-website-bloat-third-party-scripts.jpg
date: 2022-04-29T10:30:00.000Z
summary: >-
  Introducing Partytown, a lightweight open-source solution that reduces execution delays due to third-party JavaScript by offloading third-party scripts to web workers, which run in background threads.
description: >-
  Introducing Partytown, a lightweight open-source solution that reduces execution delays due to third-party JavaScript by offloading third-party scripts to web workers, which run in background threads.
categories:
  - Performance
  - JavaScript
  - Apps
---

Great user experience starts with a page that loads instantly. The average user doesn’t spend much time waiting for a web page to load or to interact with the page: According to Google, if a page’s load time goes up from 1 second to 3 seconds, the [probability of the user bouncing increases by 32%](https://www.thinkwithgoogle.com/marketing-strategies/app-and-mobile/page-load-time-statistics/). However, it’s not always easy to maintain high performance in websites. And slow websites are, in a way, discrimination: The [majority of the world’s population](https://www.gsma.com/mobileeconomy/wp-content/uploads/2022/02/280222-The-Mobile-Economy-2022.pdf) don’t have access to high-speed Internet or fast CPUs. Even if your website is designed with usability in mind, these factors impede users from fully benefiting from the website’s features.

This is why performance is crucial when building websites. Performance needs to be built in starting at the code level, and user-centric metrics like time to interactive (TTI), total blocking time (TBT), and first input delay (FID) help you gauge how fast a website is. But modern web pages are heavy and ever-growing in size (known fondly as “website bloat”): The [average web page is over 2 megabytes large with over 200 requests](https://httparchive.org/reports/state-of-the-web). Large, unwieldy websites, with several third-party scripts embedded, are usually behind a frustrating user experience. When you need these third-party scripts on your website to run your business, as most websites do, you have a massive challenge on your hands:

<blockquote>How can you improve your key performance metrics and keep your users happy without compromising on important capabilities?</blockquote>

## The JavaScript Tax

It’s a known fact that [JavaScript is one of the main culprits](https://hackernoon.com/web-bloat-isnt-a-knowledge-problem-46e561031663) behind website bloat. Providing rich, interactive website experiences needs added assets that consume your users’ resources, from CPU and GPU to memory and network. Large images and videos aside, third-party scripts like pixel trackers, A/B testing, ads, widgets, CDNs, etc., are usually the biggest pieces of the performance puzzle. Third-party scripts, which are code that is embedded within your site and not directly under your developers’ control, compete with a website’s own code for the browser’s main thread, which delays content rendering and makes websites feel sluggish.  

It’s also important to remember that your end user’s mobile devices are way less sophisticated than the ones your website was built on: All the JavaScript on your website is the reason the average web page takes [more than 14 seconds](https://httparchive.org/reports/loading-speed#ttci) to load and get interactive on mobile. This leads to a negative effect on [Lighthouse scores](https://developers.google.com/web/tools/lighthouse), [Core Web Vitals](https://web.dev/vitals/), and [search rankings](https://developers.google.com/search/docs/advanced/experience/page-experience) and reduced user engagement.

According to [Google Web Fundamentals](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/loading-third-party-javascript), third-party scripts can cause several issues including:

- Too many network requests to multiple servers;
- Sending [too much JavaScript](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/javascript-startup-optimization);
- Resource-intensive script parsing and execution;
- Insufficient [HTTP caching](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching);
- Lack of sufficient [server compression](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer) of resources;
- Blocking content display until they complete processing;
- Use of legacy APIs (e.g [document.write()](https://developers.google.com/web/updates/2016/08/removing-document-write)) known to be [harmful](https://developers.google.com/web/tools/lighthouse/audits/document-write) to the user experience;
- Excessive DOM elements or expensive CSS selectors.

When you have lots of third-party scripts on your web page, they will block your own JavaScript. This becomes especially critical for eCommerce sites and online marketplaces that need these third-party scripts to run their business and where time really is money.

Offloading third-party scripts to [web workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) running in background threads is a potential solution that allows users to keep their scripts while improving performance. Web workers execute synchronously but can only communicate with the main thread asynchronously. Web workers also don’t have direct access to the DOM &mdash; only the main thread does. So, the key challenges are providing JavaScript code running inside the web worker with some kind of access to the DOM and making that access synchronous (even though communication with the main thread has to remain asynchronous). 

{{% feature-panel %}}

## Introducing Partytown 

Partytown is a lightweight open-source solution that reduces execution delays due to third-party JavaScript by offloading third-party scripts to web workers, which run in background threads. This frees up the browser’s main thread to run your own code. It’s maintained by [Builder.io](https://www.builder.io/) and is currently in beta. 

Builder.io is also home to [Qwik](https://github.com/builderio/qwik), an open-source HTML-first, resumable web app framework which makes interactive sites load fast with only HTML and CSS, pulling JavaScript only when needed. 

While Partytown does not address all the bottlenecks caused by third-party scripts (listed in the section above), it does address the biggest challenges to building high-performance websites by:

- Freeing up main thread resources to be used only for the primary web app execution;
- Sandboxing third-party scripts and allowing or denying their access to main-thread APIs;
- Isolating long-running tasks within the web worker thread;
- Reducing layout thrashing coming from third-party scripts by batching DOM setters/getters into group updates;
- Throttling third-party scripts’ access to the main thread;
- Allowing third-party scripts to run exactly how they’re coded and without any alterations;
- Reading and writing main-thread DOM operations synchronously from within a web worker, allowing scripts running from the web worker to execute as expected.

### The Architecture Behind Partytown

Despite innovations that speed up how we deliver JavaScript to the browser (minifying, compression, distributing, code-splitting, async, defer), executing the code once it’s in the browser is constrained by the fact that JavaScript is a single-threaded language &mdash; only one script can run at a time.  

Partytown is a lazy-loaded JavaScript library to help redirect resource-intensive scripts to a web worker. To ensure apps of all sizes can continue to use third-party scripts without running into performance snags, Partytown offloads these third-party scripts into a web worker, and lets you either allow or deny their access to main-thread APIs. In other words, third-party scripts that are not required to be in the critical rendering path are executed in a background thread. This frees up the browser’s main thread to execute first-party JavaScript, which is often responsible for handling user input or painting the screen. 

Consider Google Analytics, which collects and sends tracking data using `navigator.sendBeacon()`. On the one hand, it’s a background task that can run asynchronously. On the other hand, Google Analytics still requires synchronous DOM API access when reading values from `document `and `window`. Partytown allows executing scripts like Google Analytics from the background while accessing the DOM as if it were in the main thread. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d7a864a-d5d7-44a4-871f-edf69bf6108e/1-partytown-eliminates-website-bloat-third-party-apps.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ae2f1b6-6c71-488a-94f8-ddb8708d242e/partytown-visual.jpg" width="800" height="459" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d7a864a-d5d7-44a4-871f-edf69bf6108e/1-partytown-eliminates-website-bloat-third-party-apps.png'>Large preview</a>)" alt="A picture showing how the code works with Partytown and without Partytown" >}}

### How Partytown Works

The main challenge with a web worker is that it doesn’t have direct access to DOM APIs accessible from the main thread, such as `window, document, `or `localStorage`. While a messaging system can be created between the two threads to proxy DOM operations, the `postMessage` API used for web worker/main thread communication is asynchronous. This means third-party scripts relying on synchronous DOM operations will simply fail.

Partytown provides synchronous access to the DOM API from within web workers using JavaScript proxies, service workers and synchronous XHR requests. Access to the DOM API within the web worker is proxied, creating synchronous XHR requests with the methods and values being accessed (for example, `document.title` or `window.screen.width`).

These requests are intercepted by a service worker, which uses `postMessage` to relay the API request to the main thread asynchronously. By mapping each DOM API request to a synchronous XHR, however, the web worker pauses execution until the service worker responds. The end result is that, from the perspective of the third-party script in the web worker, it’s all synchronous.

The benefit of this approach is that you don’t need to rewrite or refactor your third-party scripts to make them work within web workers. They’re executed exactly as coded; they just work from the background thread.

Furthermore, by proxying all DOM API access, Partytown can log every read and write and even restrict access to certain DOM APIs.

{{% ad-panel-leaderboard %}}

## Setting Up Partytown

Partytown does not automatically move all third-party scripts to a web worker. To get started, developers need to “opt in” &mdash; that is, they must choose which scripts are loaded and executed through Partytown. Use `npm `at the command line to install Partytown.

<pre><code class="language-bash">npm install @builder.io/partytown</code></pre>

Next, add the `type="text/partytown"` attribute to each third-party script that you want to run from a web worker.

<pre><code class="language-javascript">- &lt;script&gt;...&lt;/script&gt;
+ &lt;script type="text/partytown"&gt;...&lt;/script&gt;</code></pre>

Partytown is only enabled for specific scripts when they have the `type="text/partytown"` attribute. This does two things:

1. Prevents the main thread from executing the script;
2. Provides a selector for Partytown to query, such as `document.querySelectorAll('script[type="text/partytown"]')`.

The next step is inlining the Partytown snippet in the `<head>`. If you're using React, we recommend using the `<Partytown/> React` component.

The following is an example of including the `<Partytown/>` component in a Next.js page. 

<div class="break-out">

<pre><code class="language-javascript">import Head from "next/head";
import { Partytown } from "@builder.io/partytown/react";

const Home = () =&gt; {
  return (
    &lt;&gt;
      &lt;Head&gt;
        &lt;title&gt;My App&lt;/title&gt;
        &lt;script type="text/partytown" src="https://example.com/analytics.js"&gt;&lt;/script&gt;
        &lt;Partytown /&gt;
      &lt;/Head&gt;
      &lt;main&gt;...&lt;/main&gt;
    &lt;/&gt;
  );
};

export default Home;</code></pre>
</div>

For special cases, a minor amount of configuration might be required. Partytown works with any HTML page and doesn’t require a specific framework, but there are a few [integrations (plugins/wrappers)](https://partytown.builder.io/integrations) available, including for Next.js, Nuxt.js, React, and Shopify Hydrogen. Partytown also provides documentation and [walkthroughs](https://partytown.builder.io/common-services) for some third-party services like Facebook Pixel, Adobe Launch, and Google Tag Manager. 

While setting Partytown up, it’s important to try it first on a few pages and measure improvements using Google PageSpeed Insights. Once you confirm that all your scripts are working, you can turn it on for all the pages on the site.

## Partytown In Action

The [Builder.io](https://www.builder.io/) website managed to [cut 99% of its JavaScript](https://www.builder.io/blog/how-we-cut-99-percent-js-with-qwik-and-partytown) using a combination of Partytown and Qwik. This dramatically improved performance, with a 100/100 Google Lighthouse score on PageSpeed Insights even on mobile. There was also a huge decrease in total blocking time (TBT) and time to interactive (TTI), metrics that measure how long third-party scripts delay the execution of first-party JavaScript.

[Atoms](https://www.atoms.com/), the online footwear store, currently uses Partytown on their marketing pages (specifically on [Why Atoms](https://www.atoms.com/why-atoms/), [About](https://www.atoms.com/about), [Press](https://www.atoms.com/press), and [Gift Cards](https://www.atoms.com/products/gift-card)). They’re currently working to enable Partytown sitewide. 

{{% ad-panel-leaderboard %}}

## Come Party With Builder

Partytown is still in beta, so [not every script works](https://partytown.builder.io/trade-offs). Builder.io actively invites people to test out Partytown and share their thoughts with the team. Users can report issues, request integrations and walkthroughs, or contribute code at [Partytown’s GitHub](https://github.com/builderio/partytown). Partytown also has a lively [Discord community](https://discord.gg/tw5qMfgQ), where you can help us test Partytown and join the conversation. 

Builder.io aims to make high performance the default for websites. A fast website with the best performance should be possible without any configuration. Builder has taken the first step toward this ideal with their open-source solutions, Partytown and Qwik, which are both pivotal in making near-zero-JavaScript websites attainable for anyone. 

### Further Resources

- [Partytown](https://partytown.builder.io/) by Builder.io
- [Partytown's GitHub repo](https://github.com/BuilderIO/partytown)
- [Partytown Discord community](https://discord.com/invite/hbuEtxdEZ3)
- [Qwik’s GitHub repo](https://github.com/builderio/qwik)
- “[Introducing Partytown 🎉: Run Third-Party Scripts From a Web Worker](https://dev.to/adamdbradley/introducing-partytown-run-third-party-scripts-from-a-web-worker-2cnp)”, Adam Bradley’s two-part series on Partytown

{{< signature "vf, yk, il" >}}

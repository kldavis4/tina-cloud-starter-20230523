---
title: 'Front-End Performance 2021: Defining The Environment'
slug: front-end-performance-defining-the-environment
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08a226c5-5a9a-4bd2-bba7-dad7e74f69e9/adaptive-media-serving-opt.png
date: 2021-01-12T08:00:13.000Z
summary: >-
  Let’s make 2021... fast! An annual front-end performance checklist with everything you need to know to create fast experiences on the web today, from metrics to tooling and front-end techniques. Updated since 2016.
description: >-
  Let’s make 2021... fast! An annual front-end performance checklist with everything you need to know to create fast experiences on the web today, from metrics to tooling and front-end techniques. Updated since 2016.
canonical: https://www.smashingmagazine.com/2021/01/front-end-performance-2021-free-pdf-checklist/
categories:
  - Performance
  - PDF
  - Checklists
disable_ads: true
disable_newsletterbox: true
disable_panels: true
disable_comments: true
sponsor:
  title: Logrocket
  link: https://logrocket.com/?utm_source=smashing&amp;utm_medium=syndication&amp;utm_campaign=sm_q12021#utm_source=smashing&amp;utm_medium=syndication&amp;utm_campaign=sm_q12021
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69c20fe9-8fc8-47e1-98a3-89c3670eea4d/logrocket-logo.svg
  description: >-
    This guide has been kindly supported by our friends at <a href="https://logrocket.com/?utm_source=smashing&amp;utm_medium=syndication&amp;utm_campaign=sm_q12021#utm_source=smashing&amp;utm_medium=syndication&amp;utm_campaign=sm_q12021">LogRocket</a>, a service that combines <strong>frontend performance monitoring</strong>, session replay, and product analytics to help you build better customer experiences. <em>LogRocket</em> tracks key metrics, incl. DOM complete, time to first byte, first input delay, client CPU and memory usage. Get <a href="https://logrocket.com/?utm_source=smashing&amp;utm_medium=syndication&amp;utm_campaign=sm_q12021#utm_source=smashing&amp;utm_medium=syndication&amp;utm_campaign=sm_q12021">a free trial of LogRocket</a> today.
---

## Table Of Contents

<ol>
  <li><a href="/2021/01/front-end-performance-getting-ready-planning-metrics/">Getting Ready: Planning And Metrics</a></li>
  <li><a href="/2021/01/front-end-performance-setting-realistic-goals/">Setting Realistic Goals</a></li>
  <li><strong>Defining The Environment</strong></li>
  <li><a href="/2021/01/front-end-performance-assets-optimizations/">Assets Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-build-optimizations/">Build Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-delivery-optimizations/">Delivery Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-networking-http2-http3/">Networking, HTTP/2, HTTP/3</a></li>
  <li><a href="/2021/01/front-end-performance-testing-monitoring/">Testing And Monitoring</a></li>
  <li><a href="/2021/01/front-end-performance-quick-wins/">Quick Wins</a></li>
  <li><strong><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/">Everything on one page</a></strong></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/#download-the-checklist">Download The Checklist (PDF, Apple Pages, MS Word)</a></li>
  <li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next guides.</li>
</ol>

<style>
  .drop-caps{display:none !important}
  ol.start {
  	  counter-set: perfcounter 9;
      padding: 1em 0;
      max-width: 100%;
  }
  ol.start > li:before, ol.continue > li:before {
      content: counters(perfcounter, '.', decimal-leading-zero);
      counter-increment: perfcounter;
  }

@media all and (min-width: 1024px) {
  ol.start > li, ol.continue > li {
      list-style: none;
      margin-bottom: 1.5em;
      margin-top: 2em;
      padding-left: calc(1.65em + .7vw);
      position: relative;
  }
  ol.start > li:first-child, ol.continue > li:first-child {
      margin-top: 1em;
  }
  ol.start > li:before, ol.continue > li:before {
      margin-left: -1.1em;
      margin-right: 2.4%;
      font-family: "Mija", Arial, sans-serif;
      display: inline-block;
      line-height: 1.1em;
      text-align: center;
      background-color: #E53B2C;
      color: #fff;
      padding: .65em .5em .5em .5em;
      border-radius: 11px;
      font-size: .7em;
      font-weight: 700;
      left: .8em;
      position: absolute;
    }
  ol.start p, ol.continue p {
      font-size: inherit;
  }
}
@media (min-width: 1100px) {
.c-garfield-the-cat>ol li, .c-garfield-the-cat>ul li {
    margin-bottom: calc((1em + .5vw)/ 2);
}
}
</style>

## Defining The Environment

<ol class="start">
<li><strong>Choose and set up your build tools.</strong><br /><a href="https://24ways.org/2017/all-that-glisters/">Don’t pay too much attention to what’s supposedly cool</a> <a href="https://2018.stateofjs.com/">these days</a>. Stick to your environment for building, be it Grunt, Gulp, Webpack, Parcel, or a combination of tools. As long as you are getting results you need and you have no issues maintaining your build process, you’re doing just fine.</p>

<p>Among the build tools, Rollup keeps gaining traction, so does <a href="https://www.snowpack.dev/">Snowpack</a>, but Webpack seems to be the most established one, with literally hundreds of plugins available to optimize the size of your builds. Watch out for the <a href="https://webpack.js.org/blog/2020-12-08-roadmap-2021/">Webpack Roadmap 2021</a>.</p>

<p>One of the most notable strategies that appeared recently is <a href="https://web.dev/granular-chunking-nextjs/">Granular chunking with Webpack in Next.js and Gatsby</a> to minimize duplicate code. By default, modules that aren't shared in every entry point can be requested for routes that do not use it. This ends up becoming an overhead as more code is downloaded than necessary. With granular chunking in Next.js, we can use a <strong>server-side build manifest file</strong> to determine which outputted chunks are used by different entry points.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/733b3ac0-489e-44d5-b7ed-bcfa67a6a575/js-size-reductions-across-all-routes.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/733b3ac0-489e-44d5-b7ed-bcfa67a6a575/js-size-reductions-across-all-routes.jpg" sizes="100vw" caption="To reduce duplicate code in Webpack projects, we can use granular chunking, enabled in Next.js and Gatsby by default. Image credit: <a href='https://twitter.com/addyosmani/status/1256153891135258624'>Addy Osmani</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/733b3ac0-489e-44d5-b7ed-bcfa67a6a575/js-size-reductions-across-all-routes.jpg'>Large preview</a>)" alt="To reduce duplicate code in Webpack projects, we can use granular chunking, enabled in Next.js and Gatsby by default" >}}

<p>With <a href="https://webpack.js.org/plugins/split-chunks-plugin/">SplitChunksPlugin</a>, multiple split chunks are created depending on a number of conditions to prevent fetching duplicated code across multiple routes. This improves page load time and caching during navigations. Shipped in Next.js 9.2 and in Gatsby v2.20.7.</p>

<p>Getting started with Webpack can be tough though. So if you want to dive into Webpack, there are some great resources out there:</p>

<ul>
<li><a href="https://webpack.js.org/concepts/">Webpack documentation</a> &mdash; obviously &mdash; is a good starting point, and so are <a href="https://medium.com/@rajaraodv/webpack-the-confusing-parts-58712f8fcad9">Webpack &mdash; The Confusing Bits</a> by Raja Rao and <a href="https://nystudio107.com/blog/an-annotated-webpack-4-config-for-frontend-web-development">An Annotated Webpack Config</a> by Andrew Welch.</li>
<li>Sean Larkin has a free course on <a href="https://webpack.academy/p/the-core-concepts">Webpack: The Core Concepts</a> and Jeffrey Way has released a fantastic free course on <a href="https://laracasts.com/series/webpack-for-everyone">Webpack for everyone</a>. Both of them are great introductions for diving into Webpack.</li>
<li><a href="https://frontendmasters.com/courses/webpack-fundamentals/">Webpack Fundamentals</a> is a very comprehensive 4h course with Sean Larkin, released by FrontendMasters.</li>
<!-- <li>If you are slightly more advanced, Rowan Oulton has published a <a href="https://slack.engineering/keep-webpack-fast-a-field-guide-for-better-build-performance-f56a5995e8f1">Field Guide for Better Build Performance with Webpack</a> and Benedikt Rötsch’s made a tremendous research on <a href="https://www.contentful.com/blog/2017/10/27/put-your-webpack-bundle-on-a-diet-part-3/">putting Webpack bundle on a diet</a>.</li> -->
<li><a href="https://github.com/webpack/webpack/tree/master/examples">Webpack examples</a> has hundreds of ready-to-use Webpack configurations, categorized by topic and purpose. Bonus: there is also a <a href="https://webpack.jakoblind.no/">Webpack config configurator</a> that generates a basic configuration file.</li>
<li><a href="https://github.com/webpack-contrib/awesome-webpack">awesome-webpack</a> is a curated list of useful Webpack resources, libraries and tools, including articles, videos, courses, books and examples for Angular, React and framework-agnostic projects.</li>
<li><a href="https://codeascraft.com/2020/02/03/production-webpack-builds/">The journey to fast production asset builds with Webpack</a> is Etsy’s case study on how the team switched from using a RequireJS-based JavaScript build system to using Webpack and how they optimized theird builds, managing over 13,200 assets in <strong>4 mins</strong> on average.</li>
<li><a href="https://twitter.com/iamakulov/status/1275769142809944064">Webpack performance tips</a> is a goldmine thread by Ivan Akulov, featuring many performance-focused tips, including the <a href="https://twitter.com/iamakulov/status/1275809813692321796">ones</a> <a href="https://twitter.com/iamakulov/status/1275820821567725569">focused</a> <a href="https://twitter.com/iamakulov/status/1275810295060082688">specifically</a> <a href="https://twitter.com/iamakulov/status/1275812674354413568">on</a> <a href="https://twitter.com/iamakulov/status/1275819105644412942">Webpack</a>.</li>
<li><a href="https://github.com/iamakulov/awesome-webpack-perf">awesome-webpack-perf</a> is a goldmine GitHub repo with useful Webpack tools and plugins for performance. Also maintained by Ivan Akulov.</li>
</ul>
</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df28a3b5-b899-4a9e-93d1-be97569e9198/etsy-journey-fast-production-builds-webpack.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df28a3b5-b899-4a9e-93d1-be97569e9198/etsy-journey-fast-production-builds-webpack.jpg" sizes="100vw" caption="Etsy’s <a href='https://codeascraft.com/2020/02/03/production-webpack-builds/'>journey to fast production builds with Webpack</a> (via <a href='https://twitter.com/addyosmani/status/1240563662143668224'>Addy Osmani</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df28a3b5-b899-4a9e-93d1-be97569e9198/etsy-journey-fast-production-builds-webpack.jpg'>Large preview</a>)" alt="A visualization of Etsy's journey to fast production builds with Webpack" >}}

<ol class="continue">
<li><strong>Use progressive enhancement as a default.</strong><br />Still, after all these years, keeping <a href=" https://briefs.video/videos/is-progressive-enhancement-dead-yet/">progressive enhancement</a> as the guiding principle of your front-end architecture and deployment is a safe bet. Design and build the core experience first, and then enhance the experience with advanced features for capable browsers, creating <a href="https://resilientwebdesign.com/">resilient</a> experiences. If your website runs fast on a slow machine with a poor screen in a poor browser on a sub-optimal network, then it will only run faster on a fast machine with a good browser on a decent network.</p>

<p>In fact, with <a href="https://www.youtube.com/watch?v=puUPpVrIRkc&t=488s">adaptive module serving</a>, we seem to be taking progressive enhancement to another level, serving "lite" core experiences to low-end devices, and enhancing with more sophisticated features for high-end devices. Progressive enhancement isn’t likely to fade away any time soon.</p>
</li>

<!--
<p>If you need a practical implementation of the strategy on mid-scale and large-scale projects, Scott Jehl’s <a href="https://www.filamentgroup.com/lab/modernizing-delivery.html">Modernizing our Progressive Enhancement Delivery</a> article is a good place to start.</p>
-->

<li><strong>Choose a strong performance baseline.</strong><br />With so many unknowns impacting loading &mdash; the network, thermal throttling, cache eviction, third-party scripts, parser blocking patterns, disk I/O, IPC latency, installed extensions, antivirus software and firewalls, background CPU tasks, hardware and memory constraints, differences in L2/L3 caching, RTTS &mdash; <a href="https://v8.dev/blog/cost-of-javascript-2019">JavaScript has the heaviest cost of the experience</a>, next to web fonts blocking rendering by default and images often consuming too much memory. With the performance bottlenecks <a href="https://calendar.perfplanet.com/2017/tracking-cpu-with-long-tasks-api/">moving away from the server to the client</a>, as developers, we have to consider all of these unknowns in much more detail.</p>

<p>With a 170KB budget that already contains the critical-path HTML/CSS/JavaScript, router, state management, utilities, framework, and the application logic, we have to thoroughly <a href="https://www.twitter.com/kristoferbaxter/status/908144931125858304">examine network transfer cost, the parse/compile-time and the runtime cost</a> of the framework of our choice. Luckily, we’ve seen a huge improvement over the last few years in <a href="https://v8.dev/blog/cost-of-javascript-2019">how fast browsers can parse and compile scripts</a>. Yet the execution of JavaScript is still the main bottleneck, so paying close attention to script execution time and network can be impactful.</p>

<p>Tim Kadlec has conduct a fantastic research on the performance of modern frameworks, and summarized them in the article <a href="https://timkadlec.com/remembers/2020-04-21-the-cost-of-javascript-frameworks/">"JavaScript frameworks have a cost"</a>. We often speak about the impact of standalone frameworks, but as Tim notes, in practice, it's not uncommon to have <strong>multiple frameworks in use</strong>. Perhaps an older version of jQuery that's being slowly migrated to a modern framework, along with a few legacy applications using an older version of Angular. So it's more reasonable to explore the <strong>cumulative cost</strong> of JavaScript bytes and CPU execution time that can easily make user experiences barely usable, even on high-end devices.</p>

<p>In general, modern frameworks <strong>aren't prioritizing less powerful devices</strong>, so the experiences on a phone and on desktop will often be dramatically different in terms of performances. According to research, sites with React or Angular spend more time on the CPU than others (which of course isn’t necessarily to say that React is more expensive on the CPU than Vue.js).</p>

<p>According to Tim, one thing is obvious: "if you’re using a framework to build your site, you’re making a trade-off in terms of <strong>initial performance</strong> &mdash; even in the best of scenarios."</p>
</li>
</ol>
{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f892dfcd-f690-40b5-ad33-218a33cc85b3/cost-of-frameworks-cpu-mobile-only.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f892dfcd-f690-40b5-ad33-218a33cc85b3/cost-of-frameworks-cpu-mobile-only.png" sizes="100vw"  alt="The cost of frameworks, JavaScript CPU time: SPA-sites peform poorly" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/876d32d5-0a68-4a08-b3f1-d4c103729cfa/cost-of-frameworks-bytes-desktop.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/876d32d5-0a68-4a08-b3f1-d4c103729cfa/cost-of-frameworks-bytes-desktop.png" sizes="100vw" caption="Scripting related CPU time for mobile devices and JavaScript bytes for desktopv devices. In general, sites with React or Angular spend more time on the CPU than others. But it depends on how you build the site. <a href='https://timkadlec.com/remembers/2020-04-21-the-cost-of-javascript-frameworks/'>Research by Tim Kadlec</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/876d32d5-0a68-4a08-b3f1-d4c103729cfa/cost-of-frameworks-bytes-desktop.png'>Large preview</a>)" alt="The cost of frameworks, JavaScript byes: SPA-sites (still) peform poorly" >}}

<ol class="continue">
<li><strong>Evaluate frameworks and dependencies.</strong><br />Now, <a href="https://twitter.com/jaffathecake/status/923805333268639744">not every project needs a framework</a> and <a href="https://medium.com/dev-channel/a-netflix-web-performance-case-study-c0bcde26a9d9">not every page of a single-page-application needs to load a framework</a>. In Netflix’s case, "removing React, several libraries and the corresponding app code from the client-side reduced the total amount of JavaScript by over 200KB, causing <a href="https://www.youtube.com/watch?t=11m32s&v=V8oTJ8OZ5S0&feature=youtu.be">an over-50% reduction in Netflix’s Time-to-Interactivity</a> for the logged-out homepage." The team then utilized the time spent by users on the landing page to prefetch React for subsequent pages that users were likely to land on (<a href="https://jakearchibald.com/2017/netflix-and-react/">read on for details</a>).

<p>So what if you remove an existing framework on critical pages altogether? With Gatsby, you can check <a href="https://www.npmjs.com/package/gatsby-plugin-no-javascript">gatsby-plugin-no-javascript</a> that removes all JavaScript files created by Gatsby from the static HTML files. On Vercel, you can also <a href="https://github.com/vercel/next.js/pull/11949">allow disabling runtime JavaScript in production for certain pages</a> (experimental).</p>

<p>Once a framework is chosen, we’ll be staying with it for at least a few years, so if we need to use one, we need make sure our choice <a href="https://www.youtube.com/watch?v=6I_GwgoGm1w">is informed</a> and <a href="https://medium.com/@ZombieCodeKill/choosing-a-javascript-framework-535745d0ab90#.2op7rjakk">well considered</a> &mdash; and that goes especially for key performance metrics that we care about.</p>

<p>Data shows that, by default, frameworks are quite expensive: <a href="https://twitter.com/hdjirdeh/status/1280731085379211265">58.6% of React pages ship over 1 MB of JavaScript</a>, and 36% of Vue.js page loads have a First Contentful Paint of &lt;1.5s. According to a <a href="https://blog.uncommon.is/the-baseline-costs-of-javascript-frameworks-f768e2865d4a">study by Ankur Sethi</a>, "your React application <strong>will never load faster than about 1.1 seconds</strong> on an average phone in India, no matter how much you optimize it. Your Angular app will always take at least 2.7 seconds to boot up. The users of your Vue app will need to wait at least 1 second before they can start using it." You might not be targeting India as your primary market anyway, but users accessing your site with suboptimal network conditions will have a comparable experience.</p>

<p>Of course it <em>is</em> possible to make SPAs fast, but they aren't fast out of the box, so we need to account for the time and effort required to <em>make</em> and <em>keep</em> them fast. It's probably going to be easier by choosing a lightweight baseline performance cost early on.</p>

<!-- <p>Inian Parameshwaran <a href="https://youtu.be/wVY3-acLIoI?t=699">has measured performance footprint of top 50 frameworks</a> (against <a href="https://developers.google.com/web/tools/lighthouse/audits/first-contentful-paint"><em>First Contentful Paint</em></a> &mdash; the time from navigation to the time when the browser renders the first bit of content from the DOM). Inian discovered that, out there in the wild, Vue and Preact are the fastest across the board &mdash; both on desktop and mobile, followed by React (<a href="https://drive.google.com/file/d/1CoCQP7qyvkSQ4VG9L_PTWD5AF9wF28XT/view">slides</a>). You could examine your framework candidates and the proposed architecture, and study how most solutions out there perform, e.g. with server-side rendering or client-side rendering, on average.</p> -->

<p><strong>So how do we choose a framework</strong>? It’s a good idea to consider <em>at least</em> the total cost on size + initial execution times before choosing an option; lightweight options such as <a href="https://github.com/developit/preact">Preact</a>, <a href="https://github.com/infernojs/inferno">Inferno</a>, <a href="https://vuejs.org/">Vue</a>, <a href="https://svelte.technology/">Svelte</a>, <a href="https://www.smashingmagazine.com/2020/03/introduction-alpinejs-javascript-framework/">Alpine</a> or <a href="https://github.com/Polymer/polymer">Polymer</a> can get the job done just fine. The size of your baseline will define the constraints for your application’s code.</p>

<p>As <a href="https://twitter.com/sebmarkbage/status/829733454119989248">noted</a> by Seb Markbåge, a good way to measure start-up costs for frameworks is to <strong>first render a view, then delete it and then render again</strong> as it can tell you how the framework scales. The first render tends to warm up a bunch of lazily compiled code, which a larger tree can benefit from when it scales. The second render is basically an emulation of how code reuse on a page affects the performance characteristics as the page grows in complexity.</p>

<p>You could go as far as evaluating your candidates (or any JavaScript library in general) on Sacha Greif’s <a href="https://medium.freecodecamp.org/the-12-things-you-need-to-consider-when-evaluating-any-new-javascript-library-3908c4ed3f49">12-point scale scoring system</a> by exploring features, accessibility, stability, performance, <strong>package ecosystem</strong>, community, learning curve, documentation, tooling, track record, team, compatibility, security for example.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c1d426d-cf12-43de-a926-cea743ac1bf3/perf-track-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c1d426d-cf12-43de-a926-cea743ac1bf3/perf-track-opt.png" sizes="100vw" caption="<a href='https://perf-track.web.app/'>Perf Track</a> tracks framework performance at scale. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c1d426d-cf12-43de-a926-cea743ac1bf3/perf-track-opt.png'>Large preview</a>)" alt="Perf Track tracks framework performance at scale" >}}

<p>You can also rely on data collected on the web over a longer period of time. For example, <a href="https://perf-track.web.app/">Perf Track</a> tracks framework performance at scale, showing origin-aggregated <strong>Core Web Vitals scores</strong> for websites built in Angular, React, Vue, Polymer, Preact, Ember, Svelte and AMP. You can even specify and compare websites built with Gatsby, Next.js or Create React App, as well as websites built with Nuxt.js (Vue) or Sapper (Svelte).</p>

<p>A good starting point is to choose a <strong>good default stack</strong> for your application. <a href="https://gatsbyjs.org/">Gatsby</a> (React), <a href="https://nextjs.org/">Next.js</a> (React), <a href="https://vuepress.vuejs.org/">Vuepress</a> (Vue), <a href="https://github.com/developit/preact-cli">Preact CLI</a>, and <a href="https://github.com/Polymer/pwa-starter-kit">PWA Starter Kit</a> provide reasonable defaults for fast loading out of the box on average mobile hardware. ​​Also, take a look at <a href="https://web.dev/learn/#frameworks">web.dev framework-specific performance guidance for React and Angular</a> (<em>thanks, Phillip!</em>).</p>

<p>And perhaps you could take a slightly more refreshing approach to building single-page applications altogether &mdash; <a href="https://github.com/turbolinks/turbolinks">Turbolinks</a>, a 15KB JavaScript-library that uses HTML instead of JSON to render views. So when you follow a link, Turbolinks automatically fetches the page, swaps in its <code>&lt;body&gt;</code>, and merges its <code>&lt;head&gt;</code>, all without incurring the cost of a full page load. You can check <a href="https://twitter.com/dhh/status/1341420143239450624">quick detils</a> and <a href="https://hotwire.dev/">full documentation about the stack (Hotwire)</a>.</p>
</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb9e201e-6247-4cf2-911f-ab968623981c/09-high-sell-phones-front-end-performance-checklist-2020.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb9e201e-6247-4cf2-911f-ab968623981c/09-high-sell-phones-front-end-performance-checklist-2020.jpg" sizes="100vw" caption="CPU and compute performance of top-selling phones (Image credit: <a href='https://speakerdeck.com/addyosmani/the-cost-of-javascript-in-2019'>Addy Osmani</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb9e201e-6247-4cf2-911f-ab968623981c/09-high-sell-phones-front-end-performance-checklist-2020.jpg'>Large preview</a>)" alt="A histogram-like graph showing compute performance of top-selling phones" >}}

<ol class="continue">
<li><strong>Client-side rendering or server-side rendering? Both!</strong><br />That’s a quite heated conversation to have. The ultimate approach would be to set up some sort of <a href="https://aerotwist.com/blog/when-everything-is-important-nothing-is/">progressive booting</a>: Use server-side rendering to get a quick First Contenful Paint, but also include some minimal necessary JavaScript to keep the time-to-interactive close to the First Contentful Paint. If JavaScript is coming too late after the FCP, the browser will <a href="https://davidea.st/articles/measuring-server-side-rendering-performance-is-tricky">lock up the main thread</a> while parsing, compiling and executing late-discovered JavaScript, hence handcuffing the <a href="https://philipwalton.com/articles/why-web-developers-need-to-care-about-interactivity/">interactivity of site or application</a>.

<p>To avoid it, <strong>always break up the execution</strong> of functions into separate, asynchronous tasks, and where possible use <code>requestIdleCallback</code>. Consider lazy loading parts of the UI using WebPack’s <a href="https://developers.google.com/web/updates/2017/11/dynamic-import">dynamic <code>import()</code> support</a>, avoiding the load, parse, and compile cost until users really need them (<em>thanks Addy!</em>).</p>

<p>As mentioned above, Time to Interactive (TTI) tells us the time between navigation and interactivity. In detail, the metric is defined by looking at the first five-second window after the initial content is rendered, in which no JavaScript tasks take <strong>longer than 50ms</strong> (<em>Long Tasks</em>). If a task over 50ms occurs, the search for a five-second window starts over. As a result, the browser will first assume that it reached <em>Interactive</em>, just to switch to <em>Frozen</em>, just to eventually switch back to <em>Interactive</em>.</p>

<p>Once we reached <em>Interactive</em>, we can then &mdash; either on demand or as time allows &mdash; boot non-essential parts of the app. Unfortunately, as <a href="https://aerotwist.com/blog/when-everything-is-important-nothing-is/#which-to-use-progressive-booting">Paul Lewis noticed</a>, frameworks typically have no simple concept of priority that can be surfaced to developers, and hence progressive booting isn’t easy to implement with most libraries and frameworks.</p>

<p>Still, we are getting there. These days there are a couple of choices we can explore, and Houssein Djirdeh and Jason Miller provide an excellent overview of these options in their talk on <a href="https://www.youtube.com/watch?v=k-A2VfuUROg">Rendering on the Web</a> and Jason's and Addy's write-up on <a href="https://developers.google.com/web/updates/2019/02/rendering-on-the-web">Modern Front-End Architectures</a>. The overview below is based on their stellar work.</p>

<ul>
<li><strong>Full Server-Side Rendering</strong> (SSR)<br />In classic SSR, such as WordPress, all requests are handled entirely on the server. The requested content is returned as a finished HTML page and browsers can render it right away. Hence, SSR-apps can’t really make use of the DOM APIs, for example. The gap between First Contentful Paint and Time to Interactive is usually small, and the page can be rendered right away as HTML is being streamed to the browser.

<p>This avoids additional round-trips for data fetching and templating on the client, since it’s handled before the browser gets a response.
However, we end up with <strong>longer server think time</strong> and consequently Time To First Byte and we don’t make use of responsive and rich features of modern applications.</p>
</li>
<li><strong>Static Rendering</strong><br />We build out the product as a single page application, but all pages are prerendered to static HTML with minimal JavaScript as a build step. That means that with static rendering, we produce individual HTML files <strong>for every possible URL</strong> ahead of time, which is something not many applications can afford. But because the HTML for a page doesn't have to be generated on the fly, we can achieve a consistently fast Time To First Byte.

Thus, we can display a landing page quickly and then prefetch a SPA-framework for subsequent pages. <a href="https://medium.com/dev-channel/a-netflix-web-performance-case-study-c0bcde26a9d9">Netflix has adopted this approach</a> decreasing loading and Time-to-Interactive by 50%.</p>
</li>

<li><strong>Server-Side Rendering With (Re)Hydration</strong> (Universal Rendering, SSR + CSR)<br />We can try to use the best of both worlds &mdash; the SSR and the CSR approches. With hydration in the mix, the HTML page returned from the server also contains a script that loads a fully-fledged client-side application. Ideally, that achieve a fast First Contentful Paint (like SSR) and then continue rendering with (re)hydration. Unfortunately, that's rarely the case. More often, the page does look ready but it can't respond to user's input, producing rage clicks and abandonments.

<p>With React, we can <a href="https://alligator.io/react/server-side-rendering/">use <code>ReactDOMServer</code> module on a Node server like Express</a>, and then call the <code>renderToString</code> method to render the top level components as a static HTML string.</p>

<p>With Vue.js, we can <a href="https://ssr.vuejs.org/">use the vue-server-renderer</a> to render a Vue instance into HTML using <code>renderToString</code>. In Angular, we can <a href="https://angular.io/guide/universal">use <code>@nguniversal</code></a> to turn client requests into fully server-rendered HTML pages. A fully server-rendered experience can also be achieved out of the box with <a href="https://nextjs.org/">Next.js</a> (React) or <a href="https://nuxtjs.org/">Nuxt.js</a> (Vue).</p>

<p>The approach has its downsides. As a result, we do gain full flexibility of client-side apps while providing faster server-side rendering, but we also end up with a <strong>longer gap</strong> between First Contentful Paint and Time To Interactive and increased First Input Delay. <a href="https://addyosmani.com/blog/rehydration/">Rehydration is very expensive</a>, and usually this strategy alone will not be good enough as it heavily delays Time To Interactive.</p>
</li>

<li><strong>Streaming Server-Side Rendering With Progressive Hydration</strong> (SSR + CSR)<br />To minimize the gap between Time To Interactive and First Contentful Paint, we render multiple requests at once and <strong>send down content in chunks</strong> as they get generated. So we don’t have to wait for the full string of HTML before sending content to the browser, and hence improve Time To First Byte.

<p>In React, instead of <code>renderToString()</code>, we can use <a href="https://reactjs.org/docs/react-dom-server.html#rendertonodestream">renderToNodeStream()</a> to pipe the response and send the HTML down in chunks. In Vue, we can use <a href="https://ssr.vuejs.org/guide/streaming.html">renderToStream()</a> that can be piped and streamed. With React Suspense, we might use <a href="https://medium.com/maxime-heckel/asynchronous-rendering-with-react-c323cda68f41">asynchronous rendering</a> for that purpose, too.</p>

<p>On the client-side, rather than booting the entire application at once, we <strong>boot up components progressively</strong>. Sections of the applications are first broken down into standalone scripts with code splitting, and then hydrated gradually (in order of our priorities). In fact, we can hydrate critical components first, while the rest could be hydrated later. The role of client-side and server-side rendering can then be defined differently per component. We can then also <strong>defer hydration</strong> of some components until they come into view, or are needed for user interaction, or when the browser is idle.</p>

<p>For Vue, Markus Oberlehner has published a guide on reducing Time To Interactive of SSR apps <a href="https://markus.oberlehner.net/blog/how-to-drastically-reduce-estimated-input-latency-and-time-to-interactive-of-ssr-vue-applications/">using hydration on user interaction</a> as well as <a href="https://github.com/maoberlehner/vue-lazy-hydration">vue-lazy-hydration</a>, an early-stage plugin that enables component hydration on visibility or specific user interaction. The Angular team works on progressive hydration with <a href="https://github.com/vikerman/ivy-universal">Ivy Universal</a>. You can implement <a href="https://medium.com/@luke_schmuke/how-we-achieved-the-best-web-performance-with-partial-hydration-20fab9c808d5">partial hydration with Preact and Next.js</a>, too.</p>
</li>

<li><a href="https://developers.google.com/web/updates/2019/02/rendering-on-the-web#trisomorphic"><strong>Trisomorphic Rendering</strong></a><br />With service workers in place, we can use <strong>streaming server rendering</strong> for initial/non-JS navigations, and then have the service worker taking on rendering of HTML for navigations after it has been installed. In that case, service worker prerenders content and enables SPA-style navigations for rendering new views in the same session. Works well when you can share the same templating and routing code between the server, client page, and service worker.</p></li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1c78c47-f803-4923-96ff-99c6a4a14cbb/08-trisomorphic-front-end-performance-checklist-2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1c78c47-f803-4923-96ff-99c6a4a14cbb/08-trisomorphic-front-end-performance-checklist-2020.png" sizes="100vw" caption="Trisomorphic rendering, with the same code rendering in any 3 places: on the server, in the DOM or in a service worker. (Image source: <a href='https://developers.google.com/web/updates/2019/02/rendering-on-the-web#trisomorphic'>Google Developers</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1c78c47-f803-4923-96ff-99c6a4a14cbb/08-trisomorphic-front-end-performance-checklist-2020.png'>Large preview</a>)" alt="An illustration showing how trisomorphic rendering works in 3 places such as DOM rendering, service worker prerendering and server-side rendering" >}}

<ul>
<li><strong>CSR With Prerendering</strong><br />Prerendering is similar to server-side rendering but rather than rendering pages on the server dynamically, we render the application to static HTML at build time. While static pages are fully interactive without much client-side JavaScript, <strong>prerendering works differently</strong>. Basically it captures the initial state of a client-side application as static HTML at build time, while with prerendering the application must be booted on the client for the pages to be interactive.</p>

<p>With Next.js, we can use <a href="https://nextjs.org/docs/advanced-features/static-html-export">static HTML export</a> by prerendering an app to static HTML. In <a href="https://www.gatsbyjs.org/">Gatsby</a>, an open source static site generator that uses React, uses <code>renderToStaticMarkup</code> method instead of <code>renderToString</code> method during builds, with main JS chunk being preloaded and future routes are prefetched, without DOM attributes that aren’t needed for simple static pages.</p>

<p>For Vue, we can use <a href="https://vuepress.vuejs.org/">Vuepress</a> to achieve the same goal. You can also use <a href="https://github.com/GoogleChromeLabs/prerender-loader">prerender-loader with Webpack</a>. Navi provides <a href="https://frontarm.com/navi/en/guides/static-rendering/">static rendering</a> as well.</p>

<p>The result is a better Time To First Byte and First Contentful Paint, and we reduce the gap between Time To Interactive and First Contentful Paint. We can’t use the approach if the content is expected to change much. Plus, all URLs have to be known ahead of time to generate all the pages. So some components might be rendered using prerendering, but if we need something dynamic, we have to rely on the app to fetch the content.</p></li>

<li><strong>Full Client-Side Rendering</strong> (CSR)<br />All logic, rendering and booting are done on the client. The result is usually a <em>huge</em> gap between Time To Interactive and First Contentful Paint. As a result, applications <strong>often feel sluggish</strong> as the entire app has to be booted on the client to render anything.

<p>As JavaScript has a performance cost, as the amount of JavaScript grow with an application, aggressive code-splitting and deferring JavaScript will be absolutely necessarily to tame the impact of JavaScript. For such cases, a <strong>server-side rendering</strong> will usually be a better approach in case not much interactivity is required. If it's not an option, consider using <a href="https://developers.google.com/web/fundamentals/architecture/app-shell">The App Shell Model</a>.</p>

<p>In general, <a href="https://itnext.io/server-side-rendering-with-react-redux-and-react-router-fa5b67d4965e">SSR is faster than CSR</a>. Yet still, it’s a quite frequent implementation for many apps out there.
</li>
</ul>

<p>So, client-side or server-side? In general, it’s a good idea to <strong>limit the use of fully client-side frameworks</strong> to pages that absolutely require them. For advanced applications, it’s not a good idea to rely on server-side rendering alone either. Both server-rendering and client-rendering are a disaster if done poorly.</p>

<p>Whether you are leaning towards CSR or SSR, make sure that you are rendering important pixels as soon as possible and minimize the gap between that rendering and Time To Interactive. Consider prerendering if your pages don’t change much, and defer the booting of frameworks if you can. <strong>Stream HTML in chunks</strong> with server-side rendering, and implement <strong>progressive hydration</strong> for client-side rendering &mdash; and hydrate on visibility, interaction or during idle time to get the best of both worlds.</p>

</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8d2728f-ab3c-4b56-a265-e6c6d456e600/03-jason-front-end-performance-checklist-2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8d2728f-ab3c-4b56-a265-e6c6d456e600/03-jason-front-end-performance-checklist-2020.png" sizes="100vw" caption="The spectrum of options for client-side versus server-side rendering. Also, check Jason’s and Houssein’s talk at Google I/O on <a href='https://www.youtube.com/watch?v=k-A2VfuUROg'>Performance Implications of Application Architecture</a>. (Image source: <a href='https://twitter.com/_developit/status/1093223382223605762'>Jason Miller</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8d2728f-ab3c-4b56-a265-e6c6d456e600/03-jason-front-end-performance-checklist-2020.png'>Large preview</a>)" alt="A table comparing options for client-side versus server-side rendering" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7b675e3-6338-40ea-b7a1-5a07ee6e52cc/08-progressive-hydration-front-end-performance-checklist-2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7b675e3-6338-40ea-b7a1-5a07ee6e52cc/08-progressive-hydration-front-end-performance-checklist-2020.png" sizes="100vw" caption="AirBnB has been experimenting with progressive hydration; they defer unneeded components, load on user interaction (scroll) or during idle time and testing show that it can improve TTI. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7b675e3-6338-40ea-b7a1-5a07ee6e52cc/08-progressive-hydration-front-end-performance-checklist-2020.png'>Large preview</a>)" alt="An example of AirBnB’s website showing without progressive hydration on the left, and with progressive hydration on the right" >}}

<ol class="continue">
<li><strong>How much can we serve statically?</strong><br />Whether you're working on a large application or a small site, it's worth considering what content could be <strong>served statically from a CDN</strong> (i.e. <a href="https://jamstack.org/">JAM Stack</a>), rather than being generated dynamically on the fly. Even if you have thousands of products and hundreds of filters with plenty of personalization options, you might still want to serve your critical landing pages statically, and decouple these pages from the framework of your choice.

<p>There are plenty of <a href="https://jamstack.org/generators/">static-site generators</a> and the pages they generate <a href="https://www.11ty.dev/speedlify/">are often very fast</a>. The more content we can pre-build ahead of time instead of generating page views on a server or client at request time, the better performance we will achieve.</p>

<p>In <a href="https://markus.oberlehner.net/blog/building-partially-hydrated-progressively-enhanced-static-websites-with-isomorphic-preact-and-eleventy/">Building Partially Hydrated, Progressively Enhanced Static Websites</a>, Markus Oberlehner shows how to build out websites with a static site generator and an SPA, while achieving progressive enhancement and a minimal JavaScript bundle size. Markus uses <strong>Eleventy and Preact</strong> as his tools, and shows how to set up the tools, add partial hydration, lazy hydration, client entry file, configure Babel for Preact and bundle Preact with Rollup &mdash; from start to finish.</p>

<p>With JAMStack used on large sites these days, a new performance consideration appeared: the <strong>build time</strong>. In fact, building out even thousands of pages with every new deploy can take minutes, so it's promising to see <a href="https://www.gatsbyjs.com/blog/2020-04-22-announcing-incremental-builds/">incremental builds in Gatsby</a> which improve build times by <strong>60 times</strong>, with an integration into popular CMS solutions like WordPress, Contentful, Drupal, Netlify CMS and others.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93501951-ccc7-48be-8f01-f148cbfa6c75/incremental-static-regeneration.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93501951-ccc7-48be-8f01-f148cbfa6c75/incremental-static-regeneration.png" sizes="100vw" caption="Incremental static regeneration with Next.js. (Image credit: <a href='https://www.prisma.io/blog/jamstack-with-nextjs-prisma-jamstackN3XT'>Prisma.io</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93501951-ccc7-48be-8f01-f148cbfa6c75/incremental-static-regeneration.png'>Large preview</a>)" alt="A flow chart showing User 1 on the top left and User 2 on the bottom left showing the process of incremental status re-generation" >}}

<p>Also, Next.js announced <a href="https://nextjs.org/blog/next-9-5#stable-incremental-static-regeneration">ahead-of-time and incremental static generation</a>, which allows us to add new static pages at runtime and update existing pages after they've been already built, by re-rendering them in the background as traffic comes in.</p>

<p>Need an even more lightweight approach? In his talk on <a href="https://www.youtube.com/watch?v=taOyVmLgym4">Eleventy, Alpine and Tailwind: towards a lightweight Jamstack</a>, Nicola Goutay explains the differences between CSR, SSR and everything-in-between, and shows how to use a more lightweight approach &mdash; along with a <a href="https://github.com/orbit-love/orbit-web">GitHub repo</a> that shows the approach in practice.</p>
</li>

<li><strong>Consider using PRPL pattern and app shell architecture.</strong><br />Different frameworks will have different effects on performance and will require different strategies of optimization, so you have to clearly understand all of the nuts and bolts of the framework you’ll be relying on. When building a web app, look into the <a href="https://developers.google.com/web/fundamentals/performance/prpl-pattern/">PRPL pattern</a> and <a href="https://developers.google.com/web/updates/2015/11/app-shell">application shell architecture</a>. The idea is quite straightforward: Push the minimal code needed to get interactive for the initial route to render quickly, then use service worker for caching and pre-caching resources and then lazy-load routes that you need, asynchronously.</li>
</ol>

<figure class="article__image break-out"><a href="https://developers.google.com/web/fundamentals/performance/prpl-pattern/"><img loading="lazy" decodig="async" fetchpriority="low" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4716e5-d25b-4b80-b468-f28d07bae685/app-build-components-dibweb-c-scalew-879-opt.png 400w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4716e5-d25b-4b80-b468-f28d07bae685/app-build-components-dibweb-c-scalew-879-opt.png 800w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4716e5-d25b-4b80-b468-f28d07bae685/app-build-components-dibweb-c-scalew-879-opt.png 1200w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4716e5-d25b-4b80-b468-f28d07bae685/app-build-components-dibweb-c-scalew-879-opt.png 1600w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4716e5-d25b-4b80-b468-f28d07bae685/app-build-components-dibweb-c-scalew-879-opt.png 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4716e5-d25b-4b80-b468-f28d07bae685/app-build-components-dibweb-c-scalew-879-opt.png" sizes="100vw" alt="PRPL Pattern in the application shell architecture"></a>
  <figcaption>
    <a href="https://developers.google.com/web/fundamentals/performance/prpl-pattern/">PRPL</a> stands for Pushing critical resource, Rendering initial route, Pre-caching remaining routes and Lazy-loading remaining routes on demand.
  </figcaption>
</figure>

<figure class="article__image break-out"><a href="https://developers.google.com/web/updates/2015/11/app-shell"><img loading="lazy" decodig="async" fetchpriority="low" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6423db84-4717-4aeb-9174-7ae96bf4f3aa/appshell-1-o0t8qd-c-scalew-799-opt.jpg 400w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6423db84-4717-4aeb-9174-7ae96bf4f3aa/appshell-1-o0t8qd-c-scalew-799-opt.jpg 800w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6423db84-4717-4aeb-9174-7ae96bf4f3aa/appshell-1-o0t8qd-c-scalew-799-opt.jpg 1200w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6423db84-4717-4aeb-9174-7ae96bf4f3aa/appshell-1-o0t8qd-c-scalew-799-opt.jpg 1600w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6423db84-4717-4aeb-9174-7ae96bf4f3aa/appshell-1-o0t8qd-c-scalew-799-opt.jpg 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6423db84-4717-4aeb-9174-7ae96bf4f3aa/appshell-1-o0t8qd-c-scalew-799-opt.jpg" sizes="100vw" alt="Application shell architecture"></a>
  <figcaption>
    An <a href="https://developers.google.com/web/updates/2015/11/app-shell">application shell</a> is the minimal HTML, CSS, and JavaScript powering a user interface.
  </figcaption>
</figure>

<ol class="continue">
<li><strong>Have you optimized the performance of your APIs?</strong><br />APIs are communication channels for an application to expose data to internal and third-party applications via <em>endpoints</em>. When <a href="https://www.smashingmagazine.com/2012/10/designing-javascript-apis-usability/">designing and building an API</a>, we need a reasonable protocol to enable the communication between the server and third-party requests. <a href="https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/">Representational State Transfer</a> (<a href="https://web.archive.org/web/20130116005443/https://tomayko.com/writings/rest-to-my-wife"><em>REST</em></a>) is a well-established, logical choice: it defines a set of constraints that developers follow to make content accessible in a performant, reliable and scalable fashion. Web services that conform to the REST constraints, are called <em>RESTful web services</em>.

<p>As with good ol' HTTP requests, when data is retrieved from an API, any delay in server response will propagate to the end user, hence <strong>delaying rendering</strong>. When a resource wants to retrieve some data from an API, it will need to request the data from the corresponding endpoint. A component that renders data from several resources, such as an article with comments and author photos in each comment, may need several roundtrips to the server to fetch all the data before it can be rendered. Furthermore, the amount of data returned through REST is often more than what is needed to render that component.</p>

<p>If many resources require data from an API, the API might become a performance bottleneck. <a href="https://graphql.org/">GraphQL</a> provides a performant solution to these issues. Per se, GraphQL is a query language for your API, and a server-side runtime for executing queries by using a type system you define for your data. Unlike REST, GraphQL can retrieve all data <strong>in a single request</strong>, and the response will be exactly what is required, without <em>over</em> or <em>under</em>-fetching data as it typically happens with REST.<p>

<p>In addition, because GraphQL is using <em>schema</em> (metadata that tells how the data is structured), it can already organize data into the preferred structure, so, for example, <a href="https://medium.com/@wmdmark/how-graphql-replaces-redux-3fff8289221d">with GraphQL, we could remove JavaScript code used for dealing with state management</a>, producing a cleaner application code that runs faster on the client.</p>

<p>If you want to get started with GraphQL or encounter performance issues, these articles might be quite helpful:</p>
<ul>
<li><a href="https://www.smashingmagazine.com/2018/01/graphql-primer-new-api-part-1/">A GraphQL Primer: Why We Need A New Kind Of API</a> by Eric Baer,</li>
<li><a href="https://www.smashingmagazine.com/2018/01/graphql-primer-new-api-part-2/">A GraphQL Primer: The Evolution Of API Design</a> by Eric Baer,</li>
<li><a href="https://blog.logrocket.com/designing-graphql-server-optimal-performance/">Designing a GraphQL server for optimal performance</a> by Leonardo Losoviz,</li>
<li><a href="https://medium.com/@wtr/graphql-performance-explained-cb4b43412fb4">GraphQL performance explained</a> by Wojciech Trocki.</li>
</ul>

</li>
</ol>

{{< rimg breakout="true" href="https://web.archive.org/web/20180324125829/https://hackernoon.com/how-graphql-replaces-redux-3fff8289221d?gi=47fd50e442aa" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fda8d85-1151-4d0b-b2f6-da354ebae345/redux-rest-apollo-graphql.png" sizes="100vw" caption="A difference between REST and GraphQL, illustrated via a conversation between Redux + REST on the left, an Apollo + GraphQL on the right. (Image source: <a href='https://web.archive.org/web/20180324125829/https://hackernoon.com/how-graphql-replaces-redux-3fff8289221d?gi=47fd50e442aa'>Hacker Noon</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fda8d85-1151-4d0b-b2f6-da354ebae345/redux-rest-apollo-graphql.png'>Large preview</a>)" alt="Two examples of mobile interfaces for messages while using Redux/REST (left) and Apollo/GraphQL (right)" >}}

<ol class="continue">
<li><strong>Will you be using AMP or Instant Articles?</strong><br />Depending on the priorities and strategy of your organization, you might want to consider using Google’s <a href="https://www.ampproject.org/">AMP</a> or Facebook’s <a href="https://www.facebook.com/formedia/solutions/instant-articles">Instant Articles</a> or Apple’s <a href="https://developer.apple.com/news-publisher/">Apple News</a>. You can achieve good performance without them, but AMP <em>does</em> provide a solid performance framework with a <em>free</em> content delivery network (CDN), while Instant Articles will boost your visibility and performance on Facebook.</p>

<p>The seemingly obvious benefit of these technologies for users is <strong>guaranteed performance</strong>, so at times they might even prefer AMP-/Apple News/Instant Pages-links over "regular" and potentially bloated pages. For content-heavy websites that are dealing with a lot of third-party content, these options could potentially help speed up render times dramatically.</p>

<p><a href="https://timkadlec.com/remembers/2018-03-19-how-fast-is-amp-really/">Unless they don't.</a> According to Tim Kadlec, for example, "AMP documents tend to be faster than their counterparts, but they don’t necessarily mean a page is performant. AMP is not what makes the biggest difference from a performance perspective."</p>

<p>A benefit for the website owner is obvious: discoverability of these formats on their respective platforms and <a href="https://ethanmarcotte.com/wrote/ampersand/">increased visibility in search engines</a>.</p>

<p>Well, at least that's how it used to be. As AMP is <a href="https://developers.google.com/search/blog/2020/05/evaluating-page-experience">no longer a requirement</a> for <em>Top Stories</em>, publishers might be <a href="https://searchengineland.com/will-publishers-drop-amp-when-its-no-longer-a-requirement-for-top-stories-335612">moving away from AMP</a> to a traditional stack instead (<em>thanks, Barry!</em>).</p>

<p>Still, you could build <a href="https://www.smashingmagazine.com/2016/12/progressive-web-amps/">progressive web AMPs</a>, too, by reusing AMPs as a data source for your PWA. Downside? Obviously, a presence in a walled garden places developers in a position to produce and maintain a separate version of their content, and in case of Instant Articles and Apple News <a href="https://www.w3.org/blog/TAG/2017/07/27/distributed-and-syndicated-content-whats-wrong-with-this-picture/">without actual URLs</a> <em>(thanks Addy, Jeremy!)</em>.</p></li>

<li><strong>Choose your CDN wisely.</strong><br />As mentioned above, depending on how much dynamic data you have, you might be able to "outsource" some part of the content to a <a href="https://www.staticgen.com/">static site generator</a>, pushing it to a CDN and serving a static version from it, thus avoiding requests to the server. In fact, some of those generators are actually <a href="https://tomdale.net/2017/09/compilers-are-the-new-frameworks/">website compilers</a> with many automated optimizations provided out of the box. As compilers add optimizations over time, the compiled output gets smaller and faster over time.</p>

<p>Notice that CDNs can serve (and offload) dynamic content as well. So, restricting your CDN to static assets is not necessary. Double-check whether your CDN performs compression and conversion (e.g. image optimization and resizing at the edge), whether they provide <a href="https://www.filamentgroup.com/lab/servers-workers.html">support for servers workers</a>, <a href="https://www.youtube.com/watch?v=W-tBI_n0m_w">A/B testing</a>, as well as edge-side includes, which assemble static and dynamic parts of pages at the CDN’s edge (i.e. the server closest to the user), and other tasks. Also, check <a href="https://blog.cloudflare.com/the-quicening/">if your CDN supports HTTP over QUIC (HTTP/3)</a>.</p>

<p>Katie Hempenius has written a <a href="https://web.dev/content-delivery-networks/">fantastic guide to CDNs</a> that provides insights on <strong>how to choose a good CDN</strong>, how to finetune it and all the little things to keep in mind when evaluating one. In general, it’s a good idea to cache content as aggressively as possible and enable CDN performance features like Brotli, TLS 1.3, HTTP/2, and HTTP/3.</p>

<p><strong>Note</strong>: based on research by Patrick Meenan and Andy Davies, HTTP/2 prioritization is <a href="https://github.com/andydavies/http2-prioritization-issues#cdns--cloud-hosting-services">effectively broken on many CDNs</a>, so be careful when choosing a CDN. Patrick has more details in his talk on <a href="https://youtu.be/sgjxuhFQktE?t=2626">HTTP/2 Prioritization</a> (<em>thanks, Barry!</em>).</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/647c043f-c4f7-4d6f-ad28-31ca1828352b/cdnperf-preview.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/647c043f-c4f7-4d6f-ad28-31ca1828352b/cdnperf-preview.png" sizes="100vw" caption="<a href='https://www.cdnperf.com/'>CDNPerf</a> measures query speed for CDNs by gathering and analyzing 300 million tests every day. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/647c043f-c4f7-4d6f-ad28-31ca1828352b/cdnperf-preview.png'>Large preview</a>)" alt="CDNPerf preview of CDN names and query speed in ms" >}}

<p>When choosing a CDN, you can use these <strong>comparison sites</strong> with a detailed overview of their features:</p>

<ul>
<li><a href="https://cdncomparison.com/">CDN Comparison</a>, a CDN comparison matrix for Cloudfront, Aazure, KeyCDN, Fastly, Verizon, Stackpach, Akamai and many others.</li>
<li><a href="https://www.cdnperf.com/">CDN Perf</a> measures query speed for CDNs by gathering and analyzing 300 million tests every day, with all results based on RUM data from users all over the world. Also check <a href="https://www.dnsperf.com/">DNS Performance comparison</a> and <a href="https://www.cloudperf.com/">Cloud Peformance Comparison</a>.</li>
<li><a href="https://www.cdnplanet.com/guides/">CDN Planet Guides</a> provides an overview of CDNs for specific topics, such as Serve Stale, Purge, Origin Shield, Prefetch and Compression.</li>
<li><a href="https://almanac.httparchive.org/en/2019/cdn#cdn-adoption-and-usage">Web Almanac: CDN Adoption and Usage</a> provides insights on top CDN providers, their RTT and TLS management, TLS negotiation time, HTTP/2 adoption and others. (Unfortunately, the data is only from 2019).</li>
</ul>

</li>
</ol>


## Table Of Contents

<ol>
  <li><a href="/2021/01/front-end-performance-getting-ready-planning-metrics/">Getting Ready: Planning And Metrics</a></li>
  <li><a href="/2021/01/front-end-performance-setting-realistic-goals/">Setting Realistic Goals</a></li>
  <li><strong>Defining The Environment</strong></li>
  <li><a href="/2021/01/front-end-performance-assets-optimizations/">Assets Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-build-optimizations/">Build Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-delivery-optimizations/">Delivery Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-networking-http2-http3/">Networking, HTTP/2, HTTP/3</a></li>
  <li><a href="/2021/01/front-end-performance-testing-monitoring/">Testing And Monitoring</a></li>
  <li><a href="/2021/01/front-end-performance-quick-wins/">Quick Wins</a></li>
  <li><strong><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/">Everything on one page</a></strong></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/#download-the-checklist">Download The Checklist (PDF, Apple Pages, MS Word)</a></li>
  <li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next guides.</li>
</ol>

{{< signature "il" >}}

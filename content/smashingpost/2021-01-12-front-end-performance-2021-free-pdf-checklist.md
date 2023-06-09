---
title: 'Front-End Performance Checklist 2021 (PDF, Apple Pages, MS Word)'
slug: front-end-performance-2021-free-pdf-checklist
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08a226c5-5a9a-4bd2-bba7-dad7e74f69e9/adaptive-media-serving-opt.png
date: 2021-01-12T08:00:13.000Z
summary: >-
  Let’s make 2021... fast! An annual front-end performance checklist (available as <a href="https://www.dropbox.com/s/34noajrbm324iai/performance-checklist-1.4.pdf?dl=0">PDF</a>, <a href="https://www.dropbox.com/s/ikuk5ikcxxv39uu/performance-checklist-1.4.pages?dl=0">Apple Pages</a>, <a href="https://www.dropbox.com/scl/fi/s7ctdj89zd5zlvtt7dkhi/performance-checklist-1.4.docx?dl=0&rlkey=2xzs55e3kdg1jcraw5u1tnpl8">MS Word</a>), with everything you need to know to create fast experiences on the web today, from metrics to tooling and front-end techniques. Updated since 2016. Ah, you can also <a href='/the-smashing-newsletter/'>get useful front-end tips in our email newsletter</a>.
description: >-
  Let’s make 2021... fast! An annual front-end performance checklist, with everything you need to know to create fast experiences on the web today, from metrics to tooling and CSS/JavaScript techniques.
categories:
  - Performance
  - Debugging
  - CSS
  - JavaScript
  - PDF
  - Checklists
  - Guides
  - Core Web Vitals
disable_ads: true
disable_newsletterbox: true
disable_panels: true
last_updated: 2021-07-15T11:30:00.000Z
sponsor:
  title: Logrocket
  link: https://logrocket.com/?utm_source=smashing&amp;utm_medium=syndication&amp;utm_campaign=sm_q12021#utm_source=smashing&amp;utm_medium=syndication&amp;utm_campaign=sm_q12021
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69c20fe9-8fc8-47e1-98a3-89c3670eea4d/logrocket-logo.svg
  description: >-
    This guide has been kindly supported by our friends at <a href="https://logrocket.com/?utm_source=smashing&amp;utm_medium=syndication&amp;utm_campaign=sm_q12021#utm_source=smashing&amp;utm_medium=syndication&amp;utm_campaign=sm_q12021">LogRocket</a>, a service that combines <strong>frontend performance monitoring</strong>, session replay, and product analytics to help you build better customer experiences. <em>LogRocket</em> tracks key metrics, incl. DOM complete, time to first byte, first input delay, client CPU and memory usage. Get <a href="https://logrocket.com/?utm_source=smashing&amp;utm_medium=syndication&amp;utm_campaign=sm_q12021#utm_source=smashing&amp;utm_medium=syndication&amp;utm_campaign=sm_q12021">a free trial of LogRocket</a> today.
---

<p>Web performance is a tricky beast, isn’t it? How do we actually know where we stand in terms of performance, and what <em>exactly</em> our performance bottlenecks are? Is it expensive JavaScript, slow web font delivery, heavy images, or sluggish rendering? Have we optimized enough with tree-shaking, scope hoisting, code-splitting, and all the fancy loading patterns with intersection observer, progressive hydration, clients hints, HTTP/3, service workers and &mdash; oh my &mdash; edge workers? And, most importantly, <strong>where do we even start improving performance</strong> and how do we establish a performance culture long-term?</p>

<p>Back in the day, performance was often a mere <em>afterthought</em>. Often deferred till the very end of the project, it would boil down to minification, concatenation, asset optimization and potentially a few fine adjustments on the server’s <code>config</code> file. Looking back now, things seem to have changed quite significantly.</p>

<p>Performance isn’t just a technical concern: it affects everything from accessibility to usability to search engine optimization, and when baking it into the workflow, design decisions have to be informed by their performance implications. <strong>Performance has to be measured, monitored and refined continually</strong>, and the growing complexity of the web poses new challenges that make it hard to keep track of metrics, because data will vary significantly depending on the device, browser, protocol, network type and latency (CDNs, ISPs, caches, proxies, firewalls, load balancers and servers all play a role in performance).</p>

<p>So, if we created an overview of all the things we have to keep in mind when improving performance &mdash; from the very start of the project until the final release of the website &mdash; what would that look like? Below you’ll find a (hopefully unbiased and objective) <strong>front-end performance checklist for 2021</strong> &mdash; an updated overview of the issues you might need to consider to ensure that your response times are fast, user interaction is smooth and your sites don’t drain user’s bandwidth.</p>

## Table Of Contents

<ul>
  <li><strong><a href="/2021/01/front-end-performance-getting-ready-planning-metrics/">All on separate pages</a></strong></li>
  <li><a href="#getting-ready-planning-and-metrics">Getting Ready: Planning And Metrics</a><br />Performance culture, Core Web Vitals, performance profiles, CrUX, Lighthouse, FID, TTI, CLS, devices.</li>
  <li><a href="#setting-realistic-goals">Setting Realistic Goals</a><br />Performance budgets, performance goals, RAIL framework, 170KB/30KB budgets. </li>
  <li><a href="#defining-the-environment">Defining The Environment</a><br />Choosing a framework, baseline performance cost, Webpack, dependencies, CDN, front-end architecture, CSR, SSR, CSR + SSR, static rendering, prerendering, PRPL pattern.</li>
  <li><a href="#assets-optimizations">Assets Optimizations</a><br />Brotli, AVIF, WebP, responsive images, AV1, adaptive media loading, video compression, web fonts, Google fonts.</li>
  <li><a href="#build-optimizations">Build Optimizations</a><br />JavaScript modules, module/nomodule pattern, tree-shaking, code-splitting, scope-hoisting, Webpack, differential serving, web worker, WebAssembly, JavaScript bundles, React, SPA, partial hydration, import on interaction,  3rd-parties, cache.</li>
  <li><a href="#delivery-optimizations">Delivery Optimizations</a><br />Lazy loading, intersection observer, defer rendering and decoding, critical CSS, streaming, resource hints, layout shifts, service worker.</li>
  <li><a href="#networking-and-http-2">Networking, HTTP/2, HTTP/3</a><br />OCSP stapling, EV/DV certificates, packaging, IPv6, QUIC, HTTP/3.</li>
  <li><a href="#testing-and-monitoring">Testing And Monitoring</a><br />Auditing workflow, proxy browsers, 404 page, GDPR cookie consent prompts, performance diagnostics CSS, accessibility.</li>
  <li><a href="#quick-wins">Quick Wins</a></li>
  <li><a href="#download-the-checklist">Download The Checklist (PDF, Apple Pages, MS Word)</a></li>
  <li><a href="#off-we-go">Off We Go!</a></li>
</ul>

<p>(You can also just <a href="https://www.dropbox.com/s/34noajrbm324iai/performance-checklist-1.4.pdf?dl=0">download the checklist PDF</a> (166 KB) or <a href="https://www.dropbox.com/s/ikuk5ikcxxv39uu/performance-checklist-1.4.pages?dl=0">download editable Apple Pages file</a> (275 KB) or <a href="https://www.dropbox.com/scl/fi/s7ctdj89zd5zlvtt7dkhi/performance-checklist-1.4.docx?dl=0&rlkey=2xzs55e3kdg1jcraw5u1tnpl8">the .docx file</a> (151 KB). Happy optimizing, everyone!)</p>

<style>
  .drop-caps{display:none !important}
  ol.start {
      counter-reset: perfcounter;
      padding: 0;
      margin: 1em 0;
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

{{% feature-panel %}}

## Getting Ready: Planning And Metrics

<p>Micro-optimizations are great for keeping performance on track, but it’s critical to have clearly defined targets in mind &mdash; <em>measurable</em> goals that would influence any decisions made throughout the process. There are a couple of different models, and the ones discussed below are quite opinionated &mdash; just make sure to set your own priorities early&nbsp;on.</p>

<ol class="start">
<li><strong>Establish a performance culture.</strong><br />In many organizations, front-end developers know exactly what common underlying problems are and what strategies should be used to fix them. However, as long as there is no established endorsement of the performance culture, each decision will turn into a battlefield of departments, breaking up the organization into silos. You need a business stakeholder buy-in, and to get it, you need to establish a case study, or <a href="https://medium.com/@armelpingault/how-to-convince-your-client-to-focus-on-web-performance-a-case-study-35f12385689">a proof of concept</a> on how speed — especially <em>Core Web Vitals</em> which we'll cover in detail later — benefits metrics and Key Performance Indicators (<em>KPIs</em>) they care about.

<p>For example, to make performance more tangible, you could expose the <a href="https://simplified.dev/performance/impact-of-web-performance">revenue performance impact</a> by showing the correlation between the conversion rate and time to application load, as well as rendering performance. Or the <a href="https://drive.google.com/file/d/1o0lWk3c-d3xRuLw61jVeQwHJr_SdOCYP/view">search bot crawling rate</a> (PDF, pages 27–50).</p>

<p>Without a strong alignment between dev/design and business/marketing teams, performance isn’t going to sustain long-term. Study common complaints coming into customer service and sales team, study analytics for high bounce rates and conversion drops. Explore how improving performance can help relieve some of these common problems. <a href="https://youtu.be/SE0HhF4TO0Q?t=1052">Adjust the argument</a> depending on the group of stakeholders you are speaking to.</p>

<p>Run performance experiments and measure outcomes &mdash; both on mobile and on desktop (for example, <a href="https://dev.to/thegreengreek/show-me-the-money-justifying-performance-improvements-using-google-analytics-3231">with Google Analytics</a>). It will help you build up a company-tailored case study with real data. Furthermore, using data from case studies and experiments published on <a href="https://wpostats.com/">WPO Stats</a> will help increase sensitivity for business about why performance matters, and what impact it has on user experience and business metrics. Stating that performance matters alone isn’t enough though &mdash; you also need to establish some measurable and trackable goals and observe them over time.</p>

<p>How to get there? In her talk on <a href="https://vimeo.com/album/4970467/video/254947097">Building Performance for the Long Term</a>, Allison McKnight shares a comprehensive case-study of how she helped establish a performance culture at Etsy (<a href="https://speakerdeck.com/aemcknig/building-performance-for-the-long-term">slides</a>). More recently, Tammy Everts has spoken about <a href="https://www.youtube.com/watch?v=SE0HhF4TO0Q">habits of highly effective performance teams</a> in both small and large organizations.</p>

<p>While having these conversations in organizations, it’s important to keep in mind that just like UX is a spectrum of experiences, <a href="https://medium.com/firebase-developers/how-fast-should-your-site-load-cfb14be48e8b">web performance is a distribution</a>. As Karolina Szczur <a href="https://mailchi.mp/perf.email/56?e=7a7df41374">noted</a>, "expecting a single number to be able to provide a rating to aspire to is a flawed assumption." Hence performance goals need to be granular, trackable and tangible.</p>
</li>
</ol>

{{< rimg breakout="true" href="https://twitter.com/addyosmani/status/1231117789970124800" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b76f03b-6b76-4d18-9c54-f1280ba3e91b/conversion-rate-tracking-performance-szptss.jpg" sizes="100vw" caption="On mobile, per session, users who experienced fast load times bring 17% more revenue than average. (<a href='https://simplified.dev/performance/impact-of-web-performance'>Impact of Web Performance</a>, via <a href='https://twitter.com/addyosmani/status/1231117789970124800'>Addy Osmani</a>)" alt="On mobile, per session, users who experienced fast load times bring 17% more revenue than average" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e69134f-4ec0-4bb7-803b-ebce880b8029/bounce-rate-time-to-app-load-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e69134f-4ec0-4bb7-803b-ebce880b8029/bounce-rate-time-to-app-load-opt.png" sizes="100vw" caption="Expecting a single number to be able to provide a rating to aspire to is a flawed assumption. (Image credit: <a href='https://simplified.dev/performance/impact-of-web-performance'>Performance is a distribution</a> via <a href='https://mailchi.mp/perf.email/56?e=7a7df41374'>Karolina Czczur</a>)" alt="Expecting a single number to be able to provide a rating to aspire to is a flawed assumption" >}}

<ol class="continue">
<li><strong>Goal: Be at least 20% faster than your fastest competitor.</strong><br />According to <a href="https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/#the-need-for-performance-optimization-the-20-rule">psychological research</a>, if you want users to feel that your website is faster than your competitor’s website, you need to be <em>at least</em> 20% faster. Study your main competitors, collect metrics on how they perform on mobile and desktop and set thresholds that would help you outpace them. To get accurate results and goals though, make sure to first get a thorough picture of your users' experience by studying your analytics. You can then mimic the 90th percentile’s experience for testing.

<p>To get a good first impression of how your competitors perform, you can <a href="https://web.dev/fast/chrome-ux-report">use Chrome UX Report</a> (<em>CrUX</em>, a ready-made RUM data set, <a href="https://vimeo.com/254834890">video introduction</a> by Ilya Grigorik and <a href="https://dev.to/rick_viscomi/a-step-by-step-guide-to-monitoring-the-competition-with-the-chrome-ux-report-4k1o">detailed guide</a> by Rick Viscomi), or <a href="https://treo.sh/sites">Treo</a>, a RUM monitoring tool that is powered by Chrome UX Report. The data is gathered from the Chrome browser users, so the reports will be Chrome-specific, but they will give you a fairly thorough distribution of performance, most importantly Core Web Vitals scores, across a wide range of your visitors. Note that new CrUX datasets are released on the <strong>second Tuesday of each month</strong>.</p>

<p>Alternatively, you can also use:</p>
<ul><li>Addy Osmani’s <a href="https://crux-compare.netlify.app/">Chrome UX Report Compare Tool</a>,</li><li><a href="https://www.thinkwithgoogle.com/feature/mobile/">Speed Scorecard</a> (also provides a revenue impact estimator),</li><li><a href="https://ruxt.dexecure.com/compare">Real User Experience Test Comparison</a> or</li><li><a href="https://www.sitespeed.io/">SiteSpeed CI</a> (based on synthetic testing).</li></ul>

<p><strong>Note</strong>: If you use <a href="https://developers.google.com/speed/pagespeed/insights/">Page Speed Insights</a> or <a href="https://dev.to/addyosmani/monitoring-performance-with-the-pagespeed-insights-api-33k7">Page Speed Insights API</a> (no, it isn’t deprecated!), you can get CrUX performance data for specific pages instead of just the aggregates. This data can be much more useful for setting performance targets for assets like “landing page” or “product listing”. And if you are using CI to test the budgets, you need to make sure your tested environment matches CrUX if you used CrUX for setting the target (<em>thanks Patrick Meenan!</em>).</p>

<p>If you need some help to show the reasoning behind prioritization of speed, or you’d like to visualize conversion rate decay or increase in bounce rate with slower performance, or perhaps you’d need to advocate for a RUM solution in your organization, Sergey Chernyshev <a href="https://calendar.perfplanet.com/2019/visualizing-speed-without-real-data/">has built</a> a <a href="https://ux-speed-calculator.netlify.com/">UX Speed Calculator</a>, an open-source tool that helps you simulate data and visualize it to drive your point across.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5eebba0-3123-4d14-8ead-4be33834e6c0/smashing-distribution-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5eebba0-3123-4d14-8ead-4be33834e6c0/smashing-distribution-opt.png" sizes="100vw" caption="CrUX generates an overview of performance distributions over time, with traffic collected from Google Chrome users. You can create your own on <a href='https://g.co/chromeuxdash'>Chrome UX Dashboard</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5eebba0-3123-4d14-8ead-4be33834e6c0/smashing-distribution-opt.png'>Large preview</a>)" alt="CrUX generates an overview of performance distributions over time, with traffic collected from Google Chrome users" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/430e2362-e8f8-4db9-9ac2-2187fd638d52/16-ux-speed-calculator-front-end-performance-checklist-2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/430e2362-e8f8-4db9-9ac2-2187fd638d52/16-ux-speed-calculator-front-end-performance-checklist-2020.png" sizes="100vw" caption="Just when you need to make a case for performance to drive your point across: <a href='https://ux-speed-calculator.netlify.com/'>UX Speed Calculator</a> visualizes an impact of performance on bounce rates, conversion and total revenue &mdash; based on real data. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/430e2362-e8f8-4db9-9ac2-2187fd638d52/16-ux-speed-calculator-front-end-performance-checklist-2020.png'>Large preview</a>)" alt="Just when you need to make a case for performance to drive your point across: UX Speed Calculator visualizes an impact of performance on bounce rates, conversion and total revenue, based on real data" >}}

<p>Sometimes you might want to go a bit deeper, combining the data coming from CrUX with any other data you already have to work out quickly where the slowdowns, blindspots, and inefficiencies lie &mdash; for your competitors, or for your project. In his work, Harry Roberts has been using a <a href="https://csswizardry.com/2020/11/site-speed-topography/">Site-Speed Topography Spreadsheet</a> which he uses to break down performance by key page types, and track how different key metrics are across them. You can <a href="https://gumroad.com/l/site-speed-topography">download the spreadsheet</a> as Google Sheets, Excel, OpenOffice document or CSV.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc19294f-7bed-4974-ab6f-6344b51e538c/milestones-chart-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc19294f-7bed-4974-ab6f-6344b51e538c/milestones-chart-opt.png" sizes="100vw" caption="<a href='https://csswizardry.com/2020/11/site-speed-topography/'>Site speed topography</a>, with key metrics represented for key pages on the site. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc19294f-7bed-4974-ab6f-6344b51e538c/milestones-chart-opt.png'>Large preview</a>)" alt="Site speed topography, with key metrics represented for key pages on the site" >}}

<p>And if you want to go <em>all</em> the way, you can <a href="https://cloudfour.com/thinks/big-picture-performance-analysis-using-lighthouse-parade/">run a Lighthouse performance audit on every page of a site</a> (via <a href="https://www.npmjs.com/package/lighthouse-parade">Lightouse Parade</a>), with an output saved as CSV. That will help you identify which specific pages (or types of pages) of your competitors perform worse or better, and what you might want to focus your efforts on. (For your own site, it’s probably better to <a href="https://github.com/GoogleChrome/web-vitals/">send data to an analytics endpoint</a> though!).</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98a2d45b-e3b6-468b-994e-1bd6b08b0794/hero-lighthouse-parade-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98a2d45b-e3b6-468b-994e-1bd6b08b0794/hero-lighthouse-parade-opt.png" sizes="100vw" caption="With <a href='https://cloudfour.com/thinks/big-picture-performance-analysis-using-lighthouse-parade/'>Lighthouse Parade</a>, you can run a Lighthouse performance audit on every page of a site, with an output saved as CSV. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98a2d45b-e3b6-468b-994e-1bd6b08b0794/hero-lighthouse-parade-opt.png'>Large preview</a>)" alt="With Lighthouse Parade, you can run a Lighthouse performance audit on every page of a site, with an output saved as CSV" >}}

<p>Collect data, set up a <a href="https://danielmall.com/articles/how-to-make-a-performance-budget/">spreadsheet</a>, shave off 20%, and set up your goals (<em>performance budgets</em>) this way. Now you have something measurable to test against. If you’re keeping the budget in mind and trying to ship down just the minimal payload to get a quick time-to-interactive, then you’re on a reasonable path.</p>

<p>Need resources to get started?</p>

<ul>
<li>Addy Osmani has written a very detailed write-up on <a href="https://medium.com/@addyosmani/start-performance-budgeting-dabde04cf6a3">how to start performance budgeting</a>, how to quantify the impact of new features and where to start when you are over budget.</li>
<li>Lara Hogan’s <a href="https://designingforperformance.com/weighing-aesthetics-and-performance/#approach-new-designs-with-a-performance-budget">guide on how to approach designs with a performance budget</a> can provide helpful pointers to designers.</li>
<li>Harry Roberts has published <a href="https://csswizardry.com/2018/05/identifying-auditing-discussing-third-parties/">a guide on setting up a Google Sheet</a> to display the impact of third-party scripts on performance, using <a href="https://requestmap.webperf.tools/">Request Map</a>,</li>
<li>Jonathan Fielding’s <a href="https://www.performancebudget.io/">Performance Budget Calculator</a>, Katie Hempenius' <a href="https://perf-budget-calculator.firebaseapp.com/">perf-budget-calculator</a> and <a href="https://browserdiet.com/calories/">Browser Calories</a> can aid in creating budgets (thanks to <a href="https://medium.com/@fox/talk-the-state-of-the-web-3e12f8e413b3">Karolina Szczur</a> for the heads up).</li>
<li>In many companies, performance budgets shouldn’t be aspirational, but rather pragmatic, serving as a holding sign to avoid slipping past a certain point. In that case, you could pick your worst data point in the past two weeks as a threshold, and take it from there. <a href="https://csswizardry.com/2020/01/performance-budgets-pragmatically/">Performance Budgets, Pragmatically</a> shows you a strategy to achieve that.</li>
<li>Also, make both performance budget and current performance <em>visible</em> by setting up dashboards with graphs reporting build sizes. There are many tools allowing you to achieve that: <a href="https://www.sitespeed.io/">SiteSpeed.io dashboard</a> (open source), <a href="https://speedcurve.com/">SpeedCurve</a> and <a href="https://calibreapp.com/">Calibre</a> are just a few of them, and you can find more tools on <a href="https://perf.rocks/tools/">perf.rocks</a>.</li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc5615ec-2ffd-4510-a94f-d781c17267a7/browser-calories-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc5615ec-2ffd-4510-a94f-d781c17267a7/browser-calories-opt.png" sizes="100vw" caption="<a href='https://browserdiet.com/calories/'>Browser Calories</a> helps you set a performance budget and measure if a page is exceeding these numbers or not. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc5615ec-2ffd-4510-a94f-d781c17267a7/browser-calories-opt.png'>Large preview</a>)" alt="Browser Calories helps you set a performance budget and measure if a page is exceeding these numbers or not," >}}

<p>Once you have a budget in place, incorporate them into your build process <a href="https://web.dev/fast/incorporate-performance-budgets-into-your-build-tools">with Webpack Performance Hints and Bundlesize</a>, <a href="https://github.com/GoogleChrome/lighthouse-ci">Lighthouse CI</a>, <a href="https://github.com/paulirish/pwmetrics">PWMetrics</a> or <a href="https://www.sitespeed.io/">Sitespeed CI</a> to enforce budgets on pull requests and provide a score history in PR comments.</p>

<p>To expose performance budgets to the entire team, <a href="https://web.dev/use-lighthouse-for-performance-budgets/">integrate performance budgets in Lighthouse via Lightwallet</a> or <a href="https://github.com/treosh/lighthouse-ci-action">use LHCI Action for quick Github Actions integration</a>. And if you need something custom, you can use <a href="https://github.com/trulia/webpagetest-charts-api">webpagetest-charts-api</a>, an API of endpoints to build charts from WebPagetest results.</p>

<p>Performance awareness shouldn’t come from performance budgets alone though. Just like <a href="https://medium.com/@Pinterest_Engineering/a-one-year-pwa-retrospective-f4a2f4129e05">Pinterest</a>, you could create a <a href="https://medium.com/pinterest-engineering/a-one-year-pwa-retrospective-f4a2f4129e05#d6bc">custom <em>eslint</em> rule</a> that disallows importing from files and directories that are known to be dependency-heavy and would bloat the bundle. Set up a listing of “safe” packages that can be shared across the entire team. </p>

<p>Also, think about critical customer tasks that are most beneficial to your business. Study, discuss and define acceptable <strong>time thresholds for critical actions</strong> and establish "UX ready" <a href="https://developer.mozilla.org/en-US/docs/Web/API/Performance">user timing marks</a> that the entire organization has approved. In many cases, user journeys will touch on the work of many different departments, so alignment in terms of acceptable timings will help support or prevent performance discussions down the road. Make sure that additional costs of added resources and features are visible and understood.</p>

<p>Align performance efforts with other tech initiatives, ranging from new features of the product being built to refactoring to reaching to new global audiences. So every time a conversation about further development happens, performance is a part of that conversation as well. It’s much easier to reach performance goals when the code base is fresh or is just being refactored.</p>

<p>Also, as <a href="https://twitter.com/patmeenan">Patrick Meenan</a> suggested, it’s worth to <strong>plan out a loading sequence and trade-offs</strong> during the design process. If you prioritize early on which parts are more critical, and define the order in which they should appear, you will also know what can be delayed. Ideally, that order will also reflect the sequence of your CSS and JavaScript imports, so handling them during the build process will be easier. Also, consider what the visual experience should be in "in-between"-states, while the page is being loaded (e.g. when web fonts aren’t loaded yet).</p>

<p>Once you’ve established a strong performance culture in your organization, aim for being <em>20% faster than your former self</em> to keep priorities in tact as time passes by (<em>thanks, Guy Podjarny!</em>). But account for the different types and usage behaviors of your customers (which Tobias Baldauf called <a href="https://calendar.perfplanet.com/2020/y-u-no-revenue-cadence-cohorts-trained-behavior/">cadence and cohorts</a>), along with bot traffic and seasonality effects.</p>

<p><em>Planning, planning, planning.</em> It might be tempting to get into some quick "low-hanging-fruits"-optimizations early on &mdash; and it might be a good strategy for quick wins &mdash; but it will be very hard to keep performance a priority without planning and setting realistic, company-tailored performance goals.</p></li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbbae59c-44fa-4967-9598-33e56ab07475/10-treo-front-end-performance-checklist-2020.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbbae59c-44fa-4967-9598-33e56ab07475/10-treo-front-end-performance-checklist-2020.jpeg" sizes="100vw" caption="<a href='https://treo.sh/'>Treo</a> provides competitive analysis based on real-world data. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbbae59c-44fa-4967-9598-33e56ab07475/10-treo-front-end-performance-checklist-2020.jpeg'>Large preview</a>)" alt="Treo Sites provides competitive analysis based on real-world data" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ae6761d-b6d6-4a0f-baa6-22e7543a3830/11-metrics-front-end-performance-checklist-2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ae6761d-b6d6-4a0f-baa6-22e7543a3830/11-metrics-front-end-performance-checklist-2020.png" sizes="100vw" caption="New metrics landed in Lighthouse v6 in early 2020. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ae6761d-b6d6-4a0f-baa6-22e7543a3830/11-metrics-front-end-performance-checklist-2020.png'>Large preview</a>)" alt="New metrics landed in Lighthouse v6 in early 2020" >}}

<ol class="continue">
<li><strong>Choose the right metrics.</strong><br /><a href="https://speedcurve.com/blog/rendering-metrics/">Not all metrics are equally important</a>. Study what metrics matter most to your application: usually, it will be defined by how fast you can start to render <em>most important pixels of your interface</em> and how quickly you can provide <strong>input responsiveness</strong> for these rendered pixels. This knowledge will give you the best optimization target for ongoing efforts. In the end, it’s not the load events or server response times that define the experience, but the perception of how snappy the interface <em>feels</em>.

<p>What does it mean? Rather than focusing on full page loading time (via <em>onLoad</em> and <em>DOMContentLoaded</em> timings, for example), prioritize page loading <a href="https://web.dev/user-centric-performance-metrics/">as perceived by your customers</a>. That means focusing on a slightly different set of metrics. In fact, choosing the right metric is a process without obvious winners.</p>

<p>Based on Tim Kadlec’s research and Marcos Iglesias’ notes in <a href="https://docs.google.com/presentation/d/e/2PACX-1vTk8geAszRTDisSIplT02CacJybNtrr6kIYUCjW3-Y_7U9kYSjn_6TbabEQDnk9Ao8DX9IttL-RD_p7/pub?start=false&loop=false&delayms=10000&slide=id.g3ccc19d32d_0_98">his talk</a>, <strong>traditional metrics</strong> could be grouped into a few sets. Usually, we’ll need all of them to get a complete picture of performance, and in your particular case some of them will be more important than others.</p>

<ul>
  <li><em>Quantity-based metrics</em> measure the number of requests, weight and a performance score. Good for raising alarms and monitoring changes over time, not so good for understanding user experience.</li>
  <li><em>Milestone metrics</em> use states in the lifetime of the loading process, e.g. <em>Time To First Byte</em> and <em>Time To Interactive</em>. Good for describing the user experience and monitoring, not so good for knowing what happens between the milestones.</li>
  <li><em>Rendering metrics</em> provide an estimate of how fast content renders (e.g. <em>Start Render</em>  time, <em>Speed Index</em>). Good for measuring and tweaking rendering performance, but not so good for measuring when <em>important</em> content appears and can be interacted with.</li>
  <li><em>Custom metrics</em> measure a particular, custom event for the user, e.g. Twitter’s <a href="https://blog.alexmaccaw.com/time-to-first-tweet">Time To First Tweet</a> and Pinterest’s <a href="https://medium.com/@Pinterest_Engineering/driving-user-growth-with-performance-improvements-cfc50dafadd7">PinnerWaitTime</a>. Good for describing the user experience precisely, not so good for scaling the metrics and comparing with with competitors.</li>
</ul>

<p>To complete the picture, we’d usually look out for useful metrics among all of these groups. Usually, the most specific and relevant ones are:</p>

<ul>
  <li><a href="https://calibreapp.com/blog/time-to-interactive/">Time to Interactive</a> <em>(TTI)</em><br />The point at which layout has <strong>stabilized</strong>, key webfonts are visible, and the main thread is available enough to handle user input &mdash; basically the time mark when a user can interact with the UI. The key metrics for understanding how much <em>wait</em> a user has to experience to use the site without a lag. Boris Schapira has written a detailed post on <a href="https://blog.dareboost.com/en/2019/05/time-to-interactive-tti-measure-interactivity/">how to measure TTI reliably</a>.</li>
  <li><a href="https://developers.google.com/web/updates/2018/05/first-input-delay">First Input Delay</a> <em>(FID)</em>, or <em>Input responsiveness</em><br />The time from when a user first interacts with your site to the time when the browser is actually <strong>able to respond</strong> to that interaction. Complements TTI very well as it describes the missing part of the picture: what happens when a user actually interacts with the site. Intended as a RUM metric only. There is a <a href="https://github.com/GoogleChromeLabs/first-input-delay">JavaScript library</a> for measuring FID in the browser.</li>
  <li><a href="https://web.dev/lcp/">Largest Contentful Paint</a> <em>(LCP)</em><br />Marks the point in the page load timeline when the page’s <strong>important content</strong> has likely loaded. The assumption is that the most important element of the page is <a href="https://medium.com/speedrank-app/new-performance-metric-what-is-largest-contentful-paint-dc784a497dd5">the largest one visible in the user’s viewport</a>. If elements are rendered both above and below the fold, only the visible part is considered relevant.</li>
  <li><a href="https://web.dev/tbt/">Total Blocking Time</a> (<em>TBT</em>)<br />A metric that helps quantify the <strong>severity of how non-interactive a page is</strong> prior to it becoming reliably interactive (that is, the main thread has been free of any tasks running over 50ms (<a href="https://calendar.perfplanet.com/2017/tracking-cpu-with-long-tasks-api/"><em>long tasks</em></a>) for at least 5s). The metric measures the total amount of time between the first paint and Time to Interactive (TTI) where the main thread was blocked for long enough to prevent input responsiveness. No wonder, then, that a low TBT is a good indicator for good performance. <em>(thanks, Artem, Phil)</em></li>
  <li><a href="https://web.dev/cls">Cumulative Layout Shift</a> (<em>CLS</em>)<br />The metric highlights how often users experience unexpected <strong>layout shifts</strong> (<em>reflows</em>) when accessing the site. It examines <em>unstable</em> elements and their impact on the overall experience. The lower the score, the better.</li>
  <li><a href="https://dev.to/borisschapira/web-performance-fundamentals-what-is-the-speed-index-2m5i">Speed Index</a><br />Measures how quickly the page contents are visually populated; the lower the score, the better. The Speed Index score is computed based on the <strong>speed of visual progress</strong>, but it’s merely a computed value. It’s also sensitive to the viewport size, so you need to define a range of testing configurations that match your target audience. Note that it is becoming less important with LCP becoming a more relevant metric (<em>thanks, <a href="https://twitter.com/borisschapira">Boris</a>, Artem!</em>).</li>
  <li>CPU time spent<br />A metric that shows <em>how often</em> and <em>how long</em> the main thread is blocked, working on painting, rendering, scripting and loading. High CPU time is a clear indicator of a <em>janky</em> experience, i.e. when the user experiences a noticeable lag between their action and a response. With WebPageTest, you can <a href="https://deanhume.com/ten-things-you-didnt-know-about-webpagetest-org/">select "Capture Dev Tools Timeline" on the "Chrome" tab</a> to expose the breakdown of the main thread as it runs on any device using WebPageTest.</li>
  <li><a href="https://calendar.perfplanet.com/2019/javascript-component-level-cpu-costs/">Component-Level CPU Costs</a><br />Just like with the <em>CPU time spent</em>, this metric, proposed by Stoyan Stefanov, explores the <strong>impact of JavaScript on CPU</strong>. The idea is to use CPU instruction count per component to understand its impact on the overall experience, in isolation. Could be implemented <a href="https://calendar.perfplanet.com/2019/javascript-component-level-cpu-costs/">using Puppeteer and Chrome</a>.</li>
  <li><a href="https://www.frustrationindex.com/">FrustrationIndex</a><br />While many metrics featured above explain when a particular event happens, Tim Vereecke’s FrustrationIndex looks at the <em>gaps</em> between metrics instead of looking at them individually. It looks at the key milestones perceived by the end-user, such as Title is visible, First content is visible, Visually ready and Page looks ready and calculates a score indicating the level of frustration while loading a page. The bigger the gap, the bigger the chance a user gets frustrated. Potentially a good KPI for user experience. Tim has published a <a href="https://calendar.perfplanet.com/2019/frustrationindex-mind-the-gap/">detailed post about FrustrationIndex</a> and how it works.</li>
  <li><a href="https://calendar.perfplanet.com/2017/measuring-adweight/">Ad Weight Impact</a><br />If your site depends on the revenue generated by advertising, it’s useful to track the weight of ad related code. Paddy Ganti’s <a href="https://calendar.perfplanet.com/2017/measuring-adweight/">script</a> constructs two URLs (one normal and one blocking the ads), prompts the generation of a video comparison via WebPageTest and reports a delta.</li>
  <li><a href="https://phabricator.wikimedia.org/phame/live/7/post/117/performance_testing_in_a_controlled_lab_environment_-_the_metrics/">Deviation metrics</a><br />As <a href="https://phabricator.wikimedia.org/phame/live/7/post/117/performance_testing_in_a_controlled_lab_environment_-_the_metrics/">noted by Wikipedia engineers</a>, data of how much <strong>variance</strong> exists in your results could inform you how reliable your instruments are, and how much attention you should pay to deviations and outlers. Large variance is an indicator of adjustments needed in the setup. It also helps understand if certain pages are more difficult to measure reliably, e.g. due to third-party scripts causing significant variation. It might also be a good idea to track browser version to understand bumps in performance when a new browser version is rolled out.</li>
  <li><a href="https://speedcurve.com/blog/user-timing-and-custom-metrics/">Custom metrics</a><br />Custom metrics are defined by your business needs and customer experience. It requires you to identify <em>important</em> pixels, <em>critical</em> scripts, <em>necessary</em> CSS and <em>relevant</em> assets and measure how quickly they get delivered to the user. For that one, you can monitor <a href="https://speedcurve.com/blog/web-performance-monitoring-hero-times/">Hero Rendering Times</a>, or use <a href="https://css-tricks.com/breaking-performance-api/">Performance API</a>, marking particular timestamps for events that are important for your business. Also, you can <a href="https://github.com/WPO-Foundation/webpagetest-docs/blob/master/user/custom_metrics.md">collect custom metrics with WebPagetest</a> by executing arbitrary JavaScript at the end of a test.</li>
</ul>

<p>Note that the <a href="https://developers.google.com/web/tools/lighthouse/audits/first-meaningful-paint">First Meaningful Paint</a> <em>(FMP)</em> doesn’t appear in the overview above. It used to provide an insight into how quickly the server outputs <em>any</em> data. Long FMP usually indicated JavaScript blocking the main thread, but could be related to back-end/server issues as well. However, the metric has been <a href="https://calendar.perfplanet.com/2019/developing-the-largest-contentful-paint-metric/">deprecated</a> recently as it appears not to be accurate in about 20% of the cases. It was effectively replaced with LCP which is both more reliable and easier to reason about. It is <a href="https://web.dev/first-meaningful-paint/">no longer supported in Lighthouse</a>. Double check <a href="https://web.dev/metrics/">latest user-centric performance metrics and recommendations</a> just to make sure you are on the safe page (<em>thanks, Patrick Meenan</em>).</p>

<p>Steve Souders has a <a href="https://speedcurve.com/blog/rendering-metrics/">detailed explanation of many of these metrics</a>. It’s important to notice that while Time-To-Interactive is measured by running automated audits in the so-called <em>lab environment</em>, First Input Delay represents the <em>actual</em> user experience, with <em>actual</em> users experiencing a noticeable lag. In general, it’s probably a good idea to always measure and track both of them.</p>

<p>Depending on the context of your application, preferred metrics might differ: e.g. for Netflix TV UI, <a href="https://medium.com/netflix-techblog/crafting-a-high-performance-tv-user-interface-using-react-3350e5a6ad3b">key input responsiveness, memory usage and TTI</a> are more critical, and for Wikipedia, <a href="https://phabricator.wikimedia.org/phame/live/7/post/117/performance_testing_in_a_controlled_lab_environment_-_the_metrics/">first/last visual changes and CPU time spent metrics</a> are more important.</p>

<p><strong>Note</strong>: both FID and TTI do not account for scrolling behavior; scrolling can happen independently since it’s off-main-thread, so for many content consumption sites these metrics might be much less important (<em>thanks, Patrick!</em>).</p></li>
</ol>

{{< rimg breakout="true" href="https://twitter.com/__treo/status/1068163152783835136" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d80f91c-9807-4565-b616-a4735fcd4949/network-requests-first-input-delay.png" sizes="100vw" caption="User-centric performance metrics provide a better insight into the actual user experience. <a href='https://developers.google.com/web/updates/2018/05/first-input-delay'>First Input Delay</a> (FID) is a new metric that tries to achieve just that. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d80f91c-9807-4565-b616-a4735fcd4949/network-requests-first-input-delay.png'>Large preview</a>)" alt="User-centric performance metrics provide a better insight into the actual user experience" >}}

{{< rimg breakout="true" href="https://twitter.com/addyosmani/status/1231117789970124800" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7231a3c8-f610-4609-9829-27628aaf54bf/core-web-vitals-opt.jpg" sizes="100vw" caption="New Core Web Vitals in an oveview, LCP < 2.5s, FID <100ms, CLS < 0.1. (<a href='https://twitter.com/addyosmani/status/1257704191528599552/photo/1'>Core Web Vitals</a>, via <a href='https://twitter.com/addyosmani/status/1257704191528599552'>Addy Osmani</a>)" alt="New Core Web Vitals in an oveview, LCP < 2.5s, FID <100ms, CLS < 0.1" >}}

<ol class="continue">
<li><strong>Measure and optimize the Core Web Vitals</strong>.<br />For a long time, performance metrics were quite technical, focusing on the engineering view of how fast servers are at responding, and how quick browsers are at loading. The metrics have changed over the years — attempting to find a way to capture the <em>actual</em> user experience, rather than server timings. In May 2020, Google has announced <a href="https://web.dev/vitals/">Core Web Vitals</a>, a set of new user-focused performance metrics, each representing a distinct <a href="https://blog.chromium.org/2020/05/the-science-behind-web-vitals.html">facet of the user experience</a>.

<p>For each of them, Google recommends a range of acceptable speed goals. At least <strong>75% of all page views</strong> should exceed the <em>Good range</em> to pass this assessment. These metrics quickly gained traction, and with <a href="https://developers.google.com/search/blog/2020/11/timing-for-page-experience">Core Web Vitals becoming ranking signals for Google Search</a> in May 2021 (<em>Page Experience ranking algorithm update</em>), many companies have turned their attention to their performance scores.</p>

<p>Let’s break down each of the Core Web Vitals, one by one, along with <strong>useful techniques and tooling</strong> to optimize your experiences with these metrics in mind. (It’s worth noting that you will end up with better Core Web Vitals scores by following a general advice in this article.)</p>

<ul>
<li><a href="https://web.dev/optimize-lcp/"><strong>Largest Contentful Paint</strong></a> (<em>LCP</em>) &lt; 2.5 sec.<br />
Measures the <em>loading</em> of a page, and reports the render time of the <strong>largest image or text block</strong> that’s visible within the viewport. Hence, LCP is affected by everything that’s deferring the rendering of important information &mdash; be it slow server response times, blocking CSS, in-flight JavaScript (first-party or third-party), web font loading, expensive rendering or painting operations, lazy-loaded images, skeleton screens or client-side rendering.<br /><br />For a good experience, LCP should occur <strong>within 2.5s</strong> of when the page first starts loading. That means that we need to render the first visible portion of the page as early as possible. That will require tailored critical CSS for each template, orchestrating the <code>&lt;head&gt;</code>-order and prefetching critical assets (we’ll cover them later).</p>

<p>The main reason for a low LCP score is usually <a href="https://youtu.be/YMqnPeZHcuc?t=417">images</a>. To deliver an LCP in &lt;2.5s on Fast 3G &mdash; hosted on a well-optimized server, all static without client-side rendering and with an image coming from a dedicated image CDN &mdash; means that the <strong>maximum theoretical image size is only around 144KB</strong>. That’s why responsive images matter, as well as preloading critical images early (with <code>preload</code>).</p>

<p><em>Quick tip</em>: to discover what is considered LCP on a page, in DevTools you can <a href="https://twitter.com/tkadlec/status/1262756549090398209">hover over the LCP badge</a> under "Timings" in the Performance Panel (<em>thanks, Tim Kadlec</em>!).</p>
</li>
<li><a href="https://web.dev/fid/"><strong>First Input Delay</strong></a> (<em>FID</em>) &lt; 100ms.<br />
Measures the <em>responsiveness</em> of the UI, i.e. <strong>how long the browser was busy</strong> with other tasks before it could react to a discrete user input event like a tap, or a click. It’s designed to capture delays that result from the main thread being busy, especially during page load.<br /><br />The goal is to stay within <a href="https://youtu.be/iNfz9tg-wyg?t=259">50–100ms</a> for every interaction. To get there, we need to identify long tasks (blocks the main thread for &gt;50ms) and break them up, code-split a bundle into multiple chunks, reduce JavaScript execution time, optimize data-fetching, defer script execution of third-parties, move JavaScript to the background thread with Web workers and use progressive hydration to reduce rehydration costs in SPAs.</p>

<p><em>Quick tip</em>: in general, a reliable strategy to get a better FID score is to <strong>minimize the work on the main thread</strong> by breaking larger bundles into smaller ones and serving what the user needs when they need it, so user interactions won’t be delayed. We’ll cover more on that in detail below.</p>
</li>
<li><a href="https://web.dev/cls/"><strong>Cumulative Layout Shift</strong></a> (<em>CLS</em>) &lt; 0.1.<br />
Measures <strong>visual stability</strong> of the UI to ensure smooth and natural interactions, i.e. the sum total of all individual layout shift scores for every unexpected layout shift that occurs during the lifespan of the page. An individual layout shift occurs any time an element which was already visible changes its position on the page. It’s scored based on the size of the content and distance it moved.<br /><br />So every time a shift appears — e.g. when fallback fonts and web fonts have different font metrics, or adverts, embeds or iframes coming in late, or image/video dimensions aren’t reserved, or late CSS forces repaints, or changes are injected by late JavaScript &mdash; it has an impact on the CLS score. The recommended value for a good experience is a CLS &lt; 0.1.</p>
</li>
</ul>

<p>It’s worth noting that Core Web Vitals are <a href="https://youtu.be/iNfz9tg-wyg?t=89">supposed to evolve over time</a>, with a <strong>predictable annual cycle</strong>. For the first year update, we might be expecting First Contentful Paint to be promoted to Core Web Vitals, a reduced FID threshold and better support for single-page applications. We might also see the responding to user inputs after load gaining more weight, along with security, privacy and accessibility (!) considerations.</p>

<p>Related to Core Web Vitals, there are plenty of useful resources and articles that are worth looking into:</p>

<ul>
<li><a href="https://vitals-leaderboard.pazguille.me/">Web Vitals Leaderboard</a> allows you to compare your scores against competition on mobile, tablet, desktop, and on 3G and 4G.</li>
<li><a href="https://defaced.dev/tools/core-serp-vitals/">Core SERP Vitals</a>, a Chrome extension that shows the Core Web Vitals from CrUX in the Google Search Results.</li>
<li><a href="https://defaced.dev/tools/layout-shift-gif-generator/">Layout Shift GIF Generator</a> that visualizes CLS with a simple GIF (also available from the command line).</li>
<li><a href="https://github.com/GoogleChrome/web-vitals">web-vitals library</a> can collect and send Core Web Vitals to Google Analytics, Google Tag Manager or any other analytics endpoint.</li>
<li><a href="https://calendar.perfplanet.com/2020/analyzing-web-vitals-with-webpagetest/">Analyzing Web Vitals with WebPageTest</a>, in which Patrick Meenan explores how WebPageTest exposes data about Core Web Vitals.</li>
<li><a href="https://youtu.be/AQqFZ5t8uNc">Optimizing with Core Web Vitals</a>, a 50-min video with Addy Osmani, in which he highlights how to improve Core Web Vitals in an eCommerce case-study.</li>
<li><a href="https://nicj.net/cumulative-layout-shift-in-practice/">Cumulative Layout Shift in Practice</a> and <a href="https://nicj.net/cumulative-layout-shift-in-the-real-world/">Cumulative Layout Shift in the Real World</a> are comprehensive articles by Nic Jansma, which cover pretty much everything about CLS and how it correlates with key metrics such as Bounce Rate, Session Time or Rage Clicks.</li>
<li><a href="https://gist.github.com/paulirish/5d52fb081b3570c81e3a">What Forces Reflow</a>, with an overview of properties or methods, when requested/called in JavaScript, that will trigger the browser to synchronously calculate the style and layout.</li>
<li><a href="https://csstriggers.com/">CSS Triggers</a> shows which CSS properties trigger Layout, Paint and Composite.</li>
<li><a href="https://web.dev/fixing-layout-instability/">Fixing Layout Instability</a> is a walkthrough of using WebPageTest to identify and fix layout instability issues.</li>
<li><a href="https://blog.dareboost.com/en/2020/09/cumulative-layout-shift-visual-instability/">Cumulative Layout Shift, The Layout Instability Metric</a>, another very detailed guide by Boris Schapira on CLS, how it’s calcualted, how to measure and how to optimize for it.</li>
<li><a href="https://simonhearne.com/2020/core-web-vitals/">How To Improve Core Web Vitals</a>, a detailed guide by Simon Hearne on each of the metrics (including other Web Vitals, such as FCP, TTI, TBT), when they occur and how they are measured.</li>
</ul>

<p>So, are Core Web Vitals the <strong>ultimate metrics to follow</strong>? Not quite. They are indeed exposed in most RUM solutions and platforms already, including <a href="https://blog.cloudflare.com/start-measuring-web-vitals-with-browser-insights/">Cloudflare</a>, <a href="https://treo.sh/">Treo</a>, <a href="https://speedcurve.com/blog/web-vitals-user-experience/">SpeedCurve</a>, <a href="https://calibreapp.com/blog/core-web-vitals">Calibre</a>, <a href="https://calendar.perfplanet.com/2020/analyzing-web-vitals-with-webpagetest/">WebPageTest</a> (in the <a href="https://twitter.com/patmeenan/status/1260294231589113859">filmstrip</a> <a href="https://twitter.com/patmeenan/status/1346902718837895168">view</a> <a href="https://twitter.com/patmeenan/status/1346941018227187716">already</a>), <a href="https://blog.newrelic.com/product-news/w3c-context-trace-cumulative-layout-shift-measurement/">Newrelic</a>, <a href="https://apps.shopify.com/vitals-1">Shopify</a>, <a href="https://twitter.com/vercel/status/1259866549319618560">Next.js</a>, <a href="https://twitter.com/ChromiumDev/status/1266044527409639424">all Google tools</a> (PageSpeed Insights, Lighthouse + CI, Search Console etc.) and many others.</p>

<p>However, as Katie Sylor-Miller <a href="https://sylormiller.com/posts/2020/core-web-vitals/">explains</a>, some of the main problems with Core Web Vitals are <a href="https://sylormiller.com/posts/2020/core-web-vitals/">the lack of cross-browser support</a>, we don’t really measure the full lifecycle of a user’s experience, plus it’s difficult to correlate changes in FID and CLS with business outcomes.</p>

<p>As we should be expecting Core Web Vitals to evolve, it seems only reasonable to always <em>combine</em> Web Vitals with your custom-tailored metrics to get a better understanding of where you stand in terms of performance.</p></li>
<li><strong>Gather data on a device representative of your audience.</strong><br />To gather accurate data, we need to thoroughly choose devices to test on. In most companies, that means looking into analytics and creating user profiles based on most common device types. Yet often, analytics alone doesn’t provide a complete picture. A significant portion of the target audience might be abandoning the site (and not returning back) just because their experience is too slow, and their devices are unlikely to show up as the most popular devices in analytics for that reason. So, additionally conducting research on common devices in your target group might be a good idea.

<p>Globally in 2020, according to the IDC, <a href="https://www.idc.com/promo/smartphone-market-share/os">84.8% of all shipped mobile phones are Android devices</a>. An average consumer <a href="https://www.cnbc.com/2019/05/17/smartphone-users-are-waiting-longer-before-upgrading-heres-why.html">upgrades their phone every 2 years</a>, and in the US <a href="https://www.mobileworldlive.com/devices/news-devices/us-phone-upgrade-cycle-stretches-to-33-months/">phone replacement cycle is 33 months</a>. Average bestselling phones around the world will cost under $200.</p>

<p>A representative device, then, is an Android device that is <strong>at least 24 months old</strong>, costing $200 or less, running on slow 3G, 400ms RTT and 400kbps transfer, just to be slightly more pessimistic. This might be very different for your company, of course, but that’s a close enough approximation of a majority of customers out there. In fact, it might be a good idea to look into current <a href="https://www.amazon.co.uk/gp/bestsellers/electronics/356496011/ref=sr_bs_1">Amazon Best Sellers</a> for your target market. (<em>Thanks to Tim Kadlec, Henri Helvetica and Alex Russell for the pointers!</em>).</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1436a0fc-40ed-4665-8fbb-bae8aa1ad740/amazon-bestsellers-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1436a0fc-40ed-4665-8fbb-bae8aa1ad740/amazon-bestsellers-opt.png" sizes="100vw" caption="When building a new site or app, always check current <a href='https://www.amazon.co.uk/gp/bestsellers/electronics/356496011/ref=sr_bs_1'>Amazon Best Sellers</a> for your target market first. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1436a0fc-40ed-4665-8fbb-bae8aa1ad740/amazon-bestsellers-opt.png'>Large preview</a>)" alt="When building a new site or app, always check current Amazon Best Sellers for your target market first" >}}

<p>What test devices to choose then? The ones that fit well with the profile outlined above. It’s a good option to <a href="https://twitter.com/katiehempenius/statuses/1067969800205422593">choose a slightly older Moto G4/G5 Plus</a>, a mid-range Samsung device (Galaxy A50, S8), a good middle-of-the-road device like a Nexus 5X, Xiaomi Mi A3 or Xiaomi Redmi Note 7 and a slow device like Alcatel 1X or Cubot X19, perhaps in an <a href="https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/">open device lab</a>. For testing on slower thermal-throttled devices, you could also get a Nexus 4, which costs just around $100.</p>

<p>Also, check the chipsets used in each device and <strong>do not over-represent one chipset</strong>: a few generations of Snapdragon and Apple as well as low-end Rockchip, Mediatek would be enough <em>(thanks, Patrick!)</em>.</p>

<p>If you don’t have a device at hand, emulate mobile experience on desktop by testing on a <strong>throttled 3G network</strong> (e.g. 300ms RTT, 1.6 Mbps down, 0.8 Mbps up) with a throttled CPU (5× slowdown). Eventually switch over to regular 3G, slow 4G (e.g. 170ms RTT, 9 Mbps down, 9Mbps up), and Wi-Fi. To make the performance impact more visible, you could even introduce <a href="https://www.theverge.com/2015/10/28/9625062/facebook-2g-tuesdays-slow-internet-developing-world">2G Tuesdays</a> or set up a <a href="https://twitter.com/thommaskelly/status/938127039403610112">throttled 3G/4G network in your office</a> for faster testing.</p>

<p>Keep in mind that on a mobile device, we should be expecting a <a href="https://youtu.be/JvJ0v5OohNg?t=892">4×–5× slowdown compared to desktop machines</a>. Mobile devices have different GPUs, CPU, memory and different battery characteristics. That’s why it’s important to have a good profile of an average device and always <a href="https://www.webpagetest.org/easy">test on such a device</a>.</p></li>

<figure><a href="https://www.theverge.com/2015/10/28/9625062/facebook-2g-tuesdays-slow-internet-developing-world"><img loading="lazy" decodig="async" fetchpriority="low" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfe1a4ec-2088-4e39-8a39-9f2010380a53/tuesday-2g-opt.png 400w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfe1a4ec-2088-4e39-8a39-9f2010380a53/tuesday-2g-opt.png 800w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfe1a4ec-2088-4e39-8a39-9f2010380a53/tuesday-2g-opt.png 1200w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfe1a4ec-2088-4e39-8a39-9f2010380a53/tuesday-2g-opt.png 1600w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfe1a4ec-2088-4e39-8a39-9f2010380a53/tuesday-2g-opt.png 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfe1a4ec-2088-4e39-8a39-9f2010380a53/tuesday-2g-opt.png" sizes="32vw" alt="Introducing the slowest day of the week">  </a><figcaption>Introducing the slowest day of the week. Facebook has introduced <a href="https://www.theverge.com/2015/10/28/9625062/facebook-2g-tuesdays-slow-internet-developing-world">2G Tuesdays</a> to increase visibility and sensitivity of slow connections. (</a><a href="https://www.businessinsider.com/facebook-2g-tuesdays-to-slow-employee-internet-speeds-down-2015-10?IR=T">Image source</a>)
  </figcaption>
</figure>

<p>Luckily, there are many great options that help you automate the collection of data and measure how your website performs over time according to these metrics. Keep in mind that a good performance picture covers a set of performance metrics, <a href="https://twitter.com/izzionfire/status/1326102215573041152">lab data and field data</a>:</p>

<ul>
  <li><strong>Synthetic testing tools</strong> collect <em>lab data</em> in a reproducible environment with predefined device and network settings (e.g. <em>Lighthouse</em>, <em>Calibre</em>, <em>WebPageTest</em>) and</li>
  <li><strong>Real User Monitoring</strong> (<em>RUM</em>) tools evaluate user interactions continuously and collect <em>field data</em> (e.g. <em>SpeedCurve</em>, <em>New Relic</em> &mdash; the tools provide synthetic testing, too).</li>
</ul>

<p>The former is particularly useful during <em>development</em> as it will help you identify, isolate and fix performance issues while working on the product. The latter is useful for long-term <em>maintenance</em> as it will help you understand your performance bottlenecks as they are happening live &mdash; when users actually access the site.</p>

<p>By tapping into built-in RUM APIs such as <a href="https://developer.mozilla.org/en-US/docs/Web/API/Navigation_timing_API">Navigation Timing</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/API/Resource_Timing_API">Resource Timing</a>, <a href="https://css-tricks.com/paint-timing-api/">Paint Timing</a>, <a href="https://w3c.github.io/longtasks/">Long Tasks</a>, etc., synthetic testing tools and RUM together provide a complete picture of performance in your application. You could use <a href="https://calibreapp.com">Calibre</a>, <a href="https://treo.sh/">Treo</a>, <a href="https://speedcurve.com/">SpeedCurve</a>, <a href="https://www.akamai.com/us/en/products/performance/mpulse-real-user-monitoring.jsp">mPulse</a> and <a href="https://github.com/akamai/boomerang">Boomerang</a>, <a href="https://www.sitespeed.io/">Sitespeed.io</a>, which all are great options for performance monitoring. Furthermore, with <a href="https://www.smashingmagazine.com/2018/10/performance-server-timing/">Server Timing header</a>, you could even
monitor back-end and front-end performance all in one place.</p>

<p><strong>Note</strong>: It’s always a safer bet to choose <a href="https://calendar.perfplanet.com/2016/testing-with-realistic-networking-conditions/">network-level throttlers</a>, external to the browser, as, for example, DevTools has issues interacting with HTTP/2 push, due to the way it’s implemented (<em>thanks, Yoav, Patrick</em>!). For Mac OS, we can use <a href="https://nshipster.com/network-link-conditioner/">Network Link Conditioner</a>, for Windows <a href="https://github.com/WPO-Foundation/win-shaper/releases">Windows Traffic Shaper</a>, for Linux <a href="https://wiki.linuxfoundation.org/networking/netem">netem</a>, and for FreeBSD <a href="https://info.iet.unipi.it/~luigi/dummynet/">dummynet</a>.</p>

<p>As it’s likely that you’ll be testing in Lighthouse, keep in mind that you can:</p>
<ul>
<li><a href="https://github.com/GoogleChrome/lighthouse-ci">use Lighthouse CI</a> to track Lighthouse scores over time (it’s <a href="https://twitter.com/_developit/status/1266112451155841024">quite impressive</a>),</li>
<li><a href="https://calendar.perfplanet.com/2020/running-lighthouse-in-github-actions/">run Lighthouse in GitHub Actions</a> to get a Lighthouse report alongside every PR,</li>
<li><a href="https://cloudfour.com/thinks/big-picture-performance-analysis-using-lighthouse-parade/">run a Lighthouse performance audit on every page of a site</a> (via <a href="https://www.npmjs.com/package/lighthouse-parade">Lightouse Parade</a>), with an output saved as CSV,</li>
<li>use <a href="https://twitter.com/TheRealNooshu/status/1273045993035005952">Lighthouse Scores Calculator</a> and <a href="https://twitter.com/HenriHelvetica/status/1237408016250687488">Lighthouse metric weights</a> if you need to dive into more detail.</li>
<li>Lighthouse is <a href="https://addons.mozilla.org/en-US/firefox/addon/google-lighthouse/">available for Firefox</a> as well, but under the hood it uses the PageSpeed Insights API and <a href="https://twitter.com/boostmarks/status/1261183488037961728">generates a report based on a headless Chrome 79 User-Agent</a>.</li>
</ul>
</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c380575-7a95-48cc-bd49-08bbd2c006bd/lighthouse-ci-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c380575-7a95-48cc-bd49-08bbd2c006bd/lighthouse-ci-opt.png" sizes="100vw" caption="<a href='https://github.com/GoogleChrome/lighthouse-ci'>Lighthouse CI</a> is quite remarkable: a suite of tools to continuously run, save, retrieve, and assert against Lighthouse results. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c380575-7a95-48cc-bd49-08bbd2c006bd/lighthouse-ci-opt.png'>Large preview</a>)" alt="Lighthouse CI is quite remarkable: a suite of tools to continuously run, save, retrieve, and assert against Lighthouse results" >}}

<ol class="continue">
<li><strong>Set up "clean" and "customer" profiles for testing.</strong><br />While running tests in passive monitoring tools, it’s a common strategy to turn off anti-virus and background CPU tasks, remove background bandwidth transfers and test with a clean user profile without browser extensions to avoid skewed results (in <a href="https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Multiple_profiles">Firefox</a>, and in <a href="https://support.google.com/chrome/answer/2364824?hl=en&co=GENIE.Platform=Desktop">Chrome</a>).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78d6672a-013c-4b55-b258-7efd153a30d9/chrome-extension-page-cpu-time-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78d6672a-013c-4b55-b258-7efd153a30d9/chrome-extension-page-cpu-time-opt.png" sizes="100vw" caption="DebugBear’s report highlights <a href='https://www.debugbear.com/blog/2020-chrome-extension-performance-report'>20 slowest extensions</a>, including password managers, ad-blockers and popular applications like Evernote and Grammarly. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78d6672a-013c-4b55-b258-7efd153a30d9/chrome-extension-page-cpu-time-opt.png'>Large preview</a>)" alt="DebugBear's report highlights 20 slowest extensions, including password managers, ad-blockers and popular applications like Evernote and Grammarly" >}}

<p>However, it’s also a good idea to study which <strong>browser extensions</strong> your customers use frequently, and test with dedicated <em>"customer" profiles</em> as well. In fact, some extensions might have a <a href="https://twitter.com/denar90_/statuses/1065712688037277696">profound performance impact</a> (<a href="https://www.debugbear.com/blog/2020-chrome-extension-performance-report">2020 Chrome Extension Performance Report</a>) on your application, and if your users use them a lot, you might want to account for it up front. Hence, "clean" profile results alone are overly optimistic and can be crushed in real-life scenarios.</p></li>

<li><strong>Share the performance goals with your colleagues.</strong><br />Make sure that performance goals are familiar to every member of your team to avoid misunderstandings down the line. Every decision &mdash; be it design, marketing or anything in-between &mdash; has <strong>performance implications</strong>, and distributing responsibility and ownership across the entire team would streamline performance-focused decisions later on. Map design decisions against performance budget and the priorities defined early on.</p></li>
</ol>

## Setting Realistic Goals

<ol class="continue">
<li><strong>100-millisecond response time, 60 fps.</strong><br />For an interaction to feel smooth, the interface has 100ms to respond to user’s input. Any longer than that, and the user perceives the app as laggy. The <a href="https://www.smashingmagazine.com/2015/10/rail-user-centric-model-performance/">RAIL, a user-centered performance model</a> gives you <strong>healthy targets</strong>: To allow for &lt;100 milliseconds response, the page must yield control back to main thread at latest after every &lt;50 milliseconds. <a href="https://developers.google.com/web/tools/lighthouse/audits/estimated-input-latency">Estimated Input Latency</a> tells us if we are hitting that threshold, and ideally, it should be below 50ms. For high-pressure points like animation, it’s best to do nothing else where you can and the absolute minimum where you can't.</p>

<figure class="article__image break-out"><a href="https://developers.google.com/web/fundamentals/performance/rail">
<img loading="lazy" decodig="async" fetchpriority="low" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c91c910d-e934-4610-9dc5-369ec9071b57/rail-perf-model-opt.png 400w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c91c910d-e934-4610-9dc5-369ec9071b57/rail-perf-model-opt.png 800w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c91c910d-e934-4610-9dc5-369ec9071b57/rail-perf-model-opt.png 1200w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c91c910d-e934-4610-9dc5-369ec9071b57/rail-perf-model-opt.png 1600w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c91c910d-e934-4610-9dc5-369ec9071b57/rail-perf-model-opt.png 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c91c910d-e934-4610-9dc5-369ec9071b57/rail-perf-model-opt.png" sizes="100vw" alt="RAIL, a user-centric performance model."></a>
  <figcaption>
    <a href="https://developers.google.com/web/fundamentals/performance/rail">RAIL</a>, a user-centric performance model.
  </figcaption>
</figure>

<p>Also, each frame of animation should be completed in less than 16 milliseconds, thereby achieving 60 frames per second (1 second &divide; 60 = 16.6 milliseconds) &mdash; preferably under 10 milliseconds. Because the browser needs time to paint the new frame to the screen, your code should finish executing before hitting the 16.6 milliseconds mark. We’re starting to have conversations about 120fps (e.g. iPad Pro’s screens run at 120Hz) and Surma has covered some <a href="https://dassur.ma/things/120fps/">rendering performance solutions for 120fps</a>, but that’s probably not a target we’re looking at <em>just yet</em>.</p>

<p>Be pessimistic in performance expectations, but <a href="https://www.smashingmagazine.com/2016/11/true-lies-of-optimistic-user-interfaces/">be optimistic in interface design</a> and <a href="https://philipwalton.com/articles/idle-until-urgent/">use idle time wisely</a> (check <a href="https://github.com/GoogleChromeLabs/idlize">idlize</a>, <a href="https://github.com/TehShrike/idle-until-urgent">idle-until-urgent</a> and <a href="https://www.skypack.dev/view/@shopify/react-idle">react-idle</a>). Obviously, these targets apply to runtime performance, rather than loading performance.</p></li>

<li><strong>FID &lt; 100ms, LCP &lt; 2.5s, TTI &lt; 5s on 3G, Critical file size budget < 170KB (gzipped).</strong><br />Although it might be very difficult to achieve, a good ultimate goal would be <a href="https://www.youtube.com/watch?v=_srJ7eHS3IM&feature=youtu.be&t=6m21s">Time to Interactive under 5s</a>, and for repeat visits, aim for under 2s (achievable only with a service worker). Aim for <em>Largest Contentful Paint</em> of under 2.5s and minimize <em>Total Blocking Time</em> and <em>Cumulative Layout Shift</em>. An acceptable <em>First Input Delay</em> is under 100ms&ndash;70ms. As mentioned above, we’re considering the baseline being a $200 Android phone (e.g. Moto G4) on a slow 3G network, emulated at 400ms RTT and 400kbps transfer speed.</p>

<p>We have two major constraints that effectively shape a <em>reasonable</em> target for speedy delivery of the content on the web. On the one hand, we have <strong>network delivery constraints</strong> due to <a href="https://hpbn.co/building-blocks-of-tcp/#slow-start">TCP Slow Start</a>. The first 14KB of the HTML &mdash; 10 TCP packets, each 1460 bytes, making around 14.25 KB, <a href="https://www.tunetheweb.com/blog/critical-resources-and-the-first-14kb/">albeit not to be taken literally</a> &mdash; is the most critical payload chunk, and the only part of the budget that can be delivered in the first roundtrip (which is all you get in 1 sec at 400ms RTT due to mobile wake-up times).</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c5bf6fb-5027-4388-abd2-4355b9c8994f/new-congestion-control-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c5bf6fb-5027-4388-abd2-4355b9c8994f/new-congestion-control-opt.png" sizes="100vw" caption="With TCP connections, we start with a small congestion window and double it for every roundtrip. In the very first roundtrip, we can fit 14 KB. From: <a href='https://hpbn.co/building-blocks-of-tcp/#slow-start'>High Performance Browser Networking</a> by Ilya Grigorik. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c5bf6fb-5027-4388-abd2-4355b9c8994f/new-congestion-control-opt.png'>Large preview</a>)" alt="High Performance Browser Networking by Ilya Grigorik" >}}

<p>(<strong>Note</strong>: as TCP generally under-utilizes network connection by a significant amount, Google has developed <a href="https://cloud.google.com/blog/products/gcp/tcp-bbr-congestion-control-comes-to-gcp-your-internet-just-got-faster">TCP Bottleneck Bandwidth and RRT</a> (<em>BBR</em>), a TCP delay-controlled <a href="https://medium.com/google-cloud/tcp-bbr-magic-dust-for-network-performance-57a5f1ccf437">TCP flow control algorithm</a>. Designed for the modern web, it responds to actual congestion, rather than packet loss like TCP does, <a href="https://aws.amazon.com/blogs/networking-and-content-delivery/tcp-bbr-congestion-control-with-amazon-cloudfront/">it is significantly faster</a>, with higher throughput and lower latency &mdash; and <a href="https://blog.apnic.net/2017/05/09/bbr-new-kid-tcp-block/">the algorithm works differently</a>. (<em>thanks, Victor, Barry!</em>)</p>

<p>On the other hand, we have <strong>hardware constraints</strong> on memory and CPU due to JavaScript parsing and execution times (we’ll talk about them in detail later). To achieve the goals stated in the first paragraph, we have to consider the critical file size budget for JavaScript. Opinions vary on what that budget should be (and it heavily depends on the nature of your project), but a budget of 170KB JavaScript gzipped already would take up to 1s to parse and compile on a mid-range phone. Assuming that 170KB expands to 3× that size when decompressed (0.7MB), that already could be the death knell of a "decent" user experience on a Moto G4/G5 Plus.</p>

<p>In the case of Wikipedia's website, in 2020, globally, <a href="https://twitter.com/MonsieurPerf/status/1252184196426104832">code execution has got 19% faster</a> for Wikipedia users. So, if your year-over-year web performance metrics stay stable, that's usually a warning sign as you're actually <strong>regressing</strong> as the environment keeps improving (<a href="https://techblog.wikimedia.org/2020/05/07/measuring-the-performance-of-wikipedia-visitors-devices/">details in a blog post by Gilles Dubuc</a>).</p>

<p>If you want to target growing markets such as South East Asia, Africa or India, you’ll have to look into a very different set of constraints. Addy Osmani covers <a href="https://dev.to/addyosmani/loading-web-pages-fast-on-a-20-feature-phone-8h6">major feature phone constraints</a>, such as few low cost, high-quality devices, unavailability of high-quality networks and expensive mobile data &mdash; along with <strong>PRPL-30 budget</strong> and development guidelines for these environments.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02143033-61ad-4808-bf3e-9c5f6a515927/12-30kb-front-end-performance-checklist-2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02143033-61ad-4808-bf3e-9c5f6a515927/12-30kb-front-end-performance-checklist-2020.png" sizes="100vw" caption="<a href='https://dev.to/addyosmani/loading-web-pages-fast-on-a-20-feature-phone-8h6'>According to Addy Osmani</a>, a recommended size for lazy-loaded routes is also less than 35 KB. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02143033-61ad-4808-bf3e-9c5f6a515927/12-30kb-front-end-performance-checklist-2020.png'>Large preview</a>)" alt="According to Addy Osmani, a recommended size for lazy-loaded routes is also less than 35 KB" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9d1033f-f45f-4789-aca1-1bb61fbd44c5/13-prpl-budget-front-end-performance-checklist-2020.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9d1033f-f45f-4789-aca1-1bb61fbd44c5/13-prpl-budget-front-end-performance-checklist-2020.jpeg" sizes="100vw" caption="Addy Osmani <a href='https://dev.to/addyosmani/loading-web-pages-fast-on-a-20-feature-phone-8h6'>suggests</a> PRPL-30 performance budget (30KB gzipped + minified initial bundle) if targeting a feature phone. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9d1033f-f45f-4789-aca1-1bb61fbd44c5/13-prpl-budget-front-end-performance-checklist-2020.jpeg'>Large preview</a>)" alt="Addy Osmani suggests PRPL-30 performance budget (30KB gzipped + minified initial bundle) if targeting a feature phone" >}}

<p>In fact, Google’s Alex Russell recommends to <a href="https://infrequently.org/2017/10/can-you-afford-it-real-world-web-performance-budgets/">aim for 130&ndash;170KB gzipped</a> as a reasonable upper boundary. In real-world scenarios, most products aren’t even close: a median bundle size today is around <a href="https://beta.httparchive.org/reports/state-of-javascript#bytesJs">452KB</a>, which is up 53.6% compared to early 2015. On a middle-class mobile device, that accounts for 12&ndash;20 seconds for <em>Time-To-Interactive</em>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b311ffb-7c1e-442c-8122-53ee39fe5b7b/11-perf-phones-front-end-performance-checklist-2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b311ffb-7c1e-442c-8122-53ee39fe5b7b/11-perf-phones-front-end-performance-checklist-2020.png" sizes="100vw" caption="Geekbench CPU performance benchmarks for the highest selling smartphones globally in 2019. JavaScript stresses single-core performance (remember, it’s inherently more single-threaded than the rest of the Web Platform) and is CPU bound. From Addy’s article “<a href='https://dev.to/addyosmani/loading-web-pages-fast-on-a-20-feature-phone-8h6'>Loading Web Pages Fast On A $20 Feature Phone</a>”. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b311ffb-7c1e-442c-8122-53ee39fe5b7b/11-perf-phones-front-end-performance-checklist-2020.png'>Large preview</a>)" alt="Geekbench CPU performance benchmarks for the highest selling smartphones globally in 2019. JavaScript stresses single-core performance and is CPU bound" >}}

<p>We could also go beyond the bundle size budget though. For example, we could set performance budgets based on the activities of the browser’s main thread, i.e. paint time before start render, or <a href="https://calendar.perfplanet.com/2017/tracking-cpu-with-long-tasks-api/">track down front-end CPU hogs</a>. Tools such as <a href="https://calibreapp.com/">Calibre</a>, <a href="https://speedcurve.com/">SpeedCurve</a> and <a href="https://github.com/siddharthkp/bundlesize">Bundlesize</a> can help you keep your budgets in check, and can be integrated into your build process.</p>
<p>Finally, a performance budget probably <strong>shouldn’t be a fixed value</strong>. Depending on the network connection, <a href="https://twitter.com/katiehempenius/status/1075478356311924737">performance budgets should adapt</a>, but payload on slower connection is much more "expensive", regardless of how they’re used.</p>

<p><strong>Note</strong>: It might sound strange to set such rigid budgets in times of wide-spread HTTP/2, <a href="https://www.speedtest.net/ookla-5g-map">upcoming 5G</a> and <a href="https://twitter.com/FredKSchott/status/1313910775199612929">HTTP/3</a>, rapidly evolving mobile phones and flourishing SPAs. However, they do sound reasonable when we deal with the unpredictable nature of the network and hardware, including everything from congested networks to slowly developing infrastructure, to <a href="https://youtu.be/JvJ0v5OohNg?t=397">data caps</a>, proxy browsers, <a href="https://timkadlec.com/remembers/2019-08-29-save-data-usage/">save-data mode</a> and sneaky roaming charges.</p>
</li>
</ol>

<figure class="article__image break-out"><a href="https://speakerdeck.com/addyosmani/fast-by-default-modern-loading-best-practices">
<img loading="lazy" decodig="async" fetchpriority="low" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bb4ab9e-978a-4db0-83c3-57a93d70516d/file-size-budget-fast-default-addy-osmani-opt.png 400w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bb4ab9e-978a-4db0-83c3-57a93d70516d/file-size-budget-fast-default-addy-osmani-opt.png 800w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bb4ab9e-978a-4db0-83c3-57a93d70516d/file-size-budget-fast-default-addy-osmani-opt.png 1200w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bb4ab9e-978a-4db0-83c3-57a93d70516d/file-size-budget-fast-default-addy-osmani-opt.png 1600w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bb4ab9e-978a-4db0-83c3-57a93d70516d/file-size-budget-fast-default-addy-osmani-opt.png 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bb4ab9e-978a-4db0-83c3-57a93d70516d/file-size-budget-fast-default-addy-osmani-opt.png" sizes="100vw" alt="From 'Fast By Default: Modern Loading Best Practices' by Addy Osmani"></a>
  <figcaption>
    <a href="https://speakerdeck.com/addyosmani/fast-by-default-modern-loading-best-practices">From Fast By Default: Modern loading best practices</a> by Addy Osmani (Slide 19)
  </figcaption>
</figure>

{{< rimg breakout="true" href="https://twitter.com/katiehempenius/status/1075478356311924737" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/949e5601-04e7-48ee-91a5-10bd7af19a0f/perf-budgets-network-connection.jpg" sizes="100vw" caption="Performance budgets should adapt depending on the network conditions for an average mobile device. (Image source: <a href='https://twitter.com/katiehempenius/status/1075478356311924737'>Katie Hempenius</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/949e5601-04e7-48ee-91a5-10bd7af19a0f/perf-budgets-network-connection.jpg'>Large preview</a>)" alt="Performance budgets should adapt depending on the network conditions for an average mobile device" >}}

## Defining The Environment

<ol class="continue">
<li><strong>Choose and set up your build tools.</strong><br /><a href="https://24ways.org/2017/all-that-glisters/">Don’t pay too much attention to what’s supposedly cool</a> <a href="https://2018.stateofjs.com/">these days</a>. Stick to your environment for building, be it Grunt, Gulp, Webpack, Parcel, or a combination of tools. As long as you are getting results you need and you have no issues maintaining your build process, you’re doing just fine.</p>

<p>Among the build tools, Rollup keeps gaining traction, so does <a href="https://www.snowpack.dev/">Snowpack</a>, but Webpack seems to be the most established one, with literally hundreds of plugins available to optimize the size of your builds. Watch out for the <a href="https://webpack.js.org/blog/2020-12-08-roadmap-2021/">Webpack Roadmap 2021</a>.</p>

<p>One of the most notable strategies that appeared recently is <a href="https://web.dev/granular-chunking-nextjs/">Granular chunking with Webpack in Next.js and Gatsby</a> to minimize duplicate code. By default, modules that aren't shared in every entry point can be requested for routes that do not use it. This ends up becoming an overhead as more code is downloaded than necessary. With granular chunking in Next.js, we can use a <strong>server-side build manifest file</strong> to determine which outputted chunks are used by different entry points.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/733b3ac0-489e-44d5-b7ed-bcfa67a6a575/js-size-reductions-across-all-routes.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/733b3ac0-489e-44d5-b7ed-bcfa67a6a575/js-size-reductions-across-all-routes.jpg" sizes="100vw" caption="To reduce duplicate code in Webpack projects, we can use granular chunking, enabled in Next.js and Gatsby by default. Image credit: <a href='https://twitter.com/addyosmani/status/1256153891135258624'>Addy Osmani</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/733b3ac0-489e-44d5-b7ed-bcfa67a6a575/js-size-reductions-across-all-routes.jpg'>Large preview</a>)" alt="To reduce duplicate code in Webpack projects, we can use granular chunking, enabled in Next.js and Gatsby by default" >}}

<p>With <a href="https://webpack.js.org/plugins/split-chunks-plugin/">SplitChunksPlugin</a>, multiple split chunks are created depending on a number of conditions to prevent fetching duplicated code across multiple routes. This improves page load time and caching during navigations. Shipped in Next.js 9.2 and in Gatsby v2.20.7.</p>

<p>Getting started with Webpack can be tough though. So if you want to dive into Webpack, there are some great resources out there:</p>

<ul>
<li><a href="https://webpack.js.org/concepts/">Webpack documentation</a> &mdash; obviously &mdash; is a good starting point, and so are <a href="https://medium.com/@rajaraodv/webpack-the-confusing-parts-58712f8fcad9">Webpack &mdash; The Confusing Bits</a> by Raja Rao and <a href="https://nystudio107.com/blog/an-annotated-webpack-4-config-for-frontend-web-development">An Annotated Webpack Config</a> by Andrew Welch.</li>
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

<p>Once a framework is chosen, we’ll be staying with it for at least a few years, so if we need to use one, we need make sure our choice <a href="https://www.youtube.com/watch?v=6I_GwgoGm1w">is informed</a> and <a href="https://medium.com/@ZombieCodeKill/choosing-a-javascript-framework-535745d0ab90#.2op7rjakk">well considered</a> &mdash; and that goes especially for key performance metrics that we care about.</p>

<p>Data shows that, by default, frameworks are quite expensive: <a href="https://twitter.com/hdjirdeh/status/1280731085379211265">58.6% of React pages ship over 1 MB of JavaScript</a>, and 36% of Vue.js page loads have a First Contentful Paint of &lt;1.5s. According to a <a href="https://blog.uncommon.is/the-baseline-costs-of-javascript-frameworks-f768e2865d4a">study by Ankur Sethi</a>, "your React application <strong>will never load faster than about 1.1 seconds</strong> on an average phone in India, no matter how much you optimize it. Your Angular app will always take at least 2.7 seconds to boot up. The users of your Vue app will need to wait at least 1 second before they can start using it." You might not be targeting India as your primary market anyway, but users accessing your site with suboptimal network conditions will have a comparable experience.</p>

<p>Of course it <em>is</em> possible to make SPAs fast, but they aren't fast out of the box, so we need to account for the time and effort required to <em>make</em> and <em>keep</em> them fast. It's probably going to be easier by choosing a lightweight baseline performance cost early on.</p>

<!-- <p>Inian Parameshwaran <a href="https://youtu.be/wVY3-acLIoI?t=699">has measured performance footprint of top 50 frameworks</a> (against <a href="https://developers.google.com/web/tools/lighthouse/audits/first-contentful-paint"><em>First Contentful Paint</em></a> &mdash; the time from navigation to the time when the browser renders the first bit of content from the DOM). Inian discovered that, out there in the wild, Vue and Preact are the fastest across the board &mdash; both on desktop and mobile, followed by React (<a href="https://drive.google.com/file/d/1CoCQP7qyvkSQ4VG9L_PTWD5AF9wF28XT/view">slides</a>). You could examine your framework candidates and the proposed architecture, and study how most solutions out there perform, e.g. with server-side rendering or client-side rendering, on average.</p> -->

<p><strong>So how do we choose a framework</strong>? It’s a good idea to consider <em>at least</em> the total cost on size + initial execution times before choosing an option; lightweight options such as <a href="https://github.com/developit/preact">Preact</a>, <a href="https://github.com/infernojs/inferno">Inferno</a>, <a href="https://vuejs.org/">Vue</a>, <a href="https://svelte.technology/">Svelte</a>, <a href="https://www.smashingmagazine.com/2020/03/introduction-alpinejs-javascript-framework/">Alpine</a> or <a href="https://github.com/Polymer/polymer">Polymer</a> can get the job done just fine. The size of your baseline will define the constraints for your application’s code.</p>

<p>As <a href="https://twitter.com/sebmarkbage/status/829733454119989248">noted</a> by Seb Markbåge, a good way to measure start-up costs for frameworks is to <strong>first render a view, then delete it and then render again</strong> as it can tell you how the framework scales. The first render tends to warm up a bunch of lazily compiled code, which a larger tree can benefit from when it scales. The second render is basically an emulation of how code reuse on a page affects the performance characteristics as the page grows in complexity.</p>

<p>You could go as far as evaluating your candidates (or any JavaScript library in general) on Sacha Greif’s <a href="https://medium.freecodecamp.org/the-12-things-you-need-to-consider-when-evaluating-any-new-javascript-library-3908c4ed3f49">12-point scale scoring system</a> by exploring features, accessibility, stability, performance, <strong>package ecosystem</strong>, community, learning curve, documentation, tooling, track record, team, compatibility, security for example.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c1d426d-cf12-43de-a926-cea743ac1bf3/perf-track-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c1d426d-cf12-43de-a926-cea743ac1bf3/perf-track-opt.png" sizes="100vw" caption="<a href='https://perf-track.web.app/'>Perf Track</a> tracks framework performance at scale. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c1d426d-cf12-43de-a926-cea743ac1bf3/perf-track-opt.png'>Large preview</a>)" alt="Perf Track tracks framework performance at scale" >}}

<p>You can also rely on data collected on the web over a longer period of time. For example, <a href="https://perf-track.web.app/">Perf Track</a> tracks framework performance at scale, showing origin-aggregated <strong>Core Web Vitals scores</strong> for websites built in Angular, React, Vue, Polymer, Preact, Ember, Svelte and AMP. You can even specify and compare websites built with Gatsby, Next.js or Create React App, as well as websites built with Nuxt.js (Vue) or Sapper (Svelte).</p>

<p>A good starting point is to choose a <strong>good default stack</strong> for your application. <a href="https://gatsbyjs.org/">Gatsby</a> (React), <a href="https://nextjs.org/">Next.js</a> (React), <a href="https://vuepress.vuejs.org/">Vuepress</a> (Vue), <a href="https://github.com/developit/preact-cli">Preact CLI</a>, and <a href="https://github.com/Polymer/pwa-starter-kit">PWA Starter Kit</a> provide reasonable defaults for fast loading out of the box on average mobile hardware. ​​Also, take a look at <a href="https://web.dev/learn/#frameworks">web.dev framework-specific performance guidance for React and Angular</a> (<em>thanks, Phillip!</em>).</p>

<p>And perhaps you could take a slightly more refreshing approach to building single-page applications altogether &mdash; <a href="https://github.com/turbolinks/turbolinks">Turbolinks</a>, a 15KB JavaScript-library that uses HTML instead of JSON to render views. So when you follow a link, Turbolinks automatically fetches the page, swaps in its <code>&lt;body&gt;</code>, and merges its <code>&lt;head&gt;</code>, all without incurring the cost of a full page load. You can check <a href="https://twitter.com/dhh/status/1341420143239450624">quick detils</a> and <a href="https://hotwire.dev/">full documentation about the stack (Hotwire)</a>.</p>
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

<li><strong>Server-Side Rendering With (Re)Hydration</strong> (Universal Rendering, SSR + CSR)<br />We can try to use the best of both worlds &mdash; the SSR and the CSR approches. With hydration in the mix, the HTML page returned from the server also contains a script that loads a fully-fledged client-side application. Ideally, that achieve a fast First Contentful Paint (like SSR) and then continue rendering with (re)hydration. Unfortunately, that's rarely the case. More often, the page does look ready but it can't respond to user's input, producing rage clicks and abandonments.

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

<p>Whether you are leaning towards CSR or SSR, make sure that you are rendering important pixels as soon as possible and minimize the gap between that rendering and Time To Interactive. Consider prerendering if your pages don’t change much, and defer the booting of frameworks if you can. <strong>Stream HTML in chunks</strong> with server-side rendering, and implement <strong>progressive hydration</strong> for client-side rendering &mdash; and hydrate on visibility, interaction or during idle time to get the best of both worlds.</p>

</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8d2728f-ab3c-4b56-a265-e6c6d456e600/03-jason-front-end-performance-checklist-2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8d2728f-ab3c-4b56-a265-e6c6d456e600/03-jason-front-end-performance-checklist-2020.png" sizes="100vw" caption="The spectrum of options for client-side versus server-side rendering. Also, check Jason’s and Houssein’s talk at Google I/O on <a href='https://www.youtube.com/watch?v=k-A2VfuUROg'>Performance Implications of Application Architecture</a>. (Image source: <a href='https://twitter.com/_developit/status/1093223382223605762'>Jason Miller</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8d2728f-ab3c-4b56-a265-e6c6d456e600/03-jason-front-end-performance-checklist-2020.png'>Large preview</a>)" alt="A table comparing options for client-side versus server-side rendering" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7b675e3-6338-40ea-b7a1-5a07ee6e52cc/08-progressive-hydration-front-end-performance-checklist-2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7b675e3-6338-40ea-b7a1-5a07ee6e52cc/08-progressive-hydration-front-end-performance-checklist-2020.png" sizes="100vw" caption="AirBnB has been experimenting with progressive hydration; they defer unneeded components, load on user interaction (scroll) or during idle time and testing show that it can improve TTI. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7b675e3-6338-40ea-b7a1-5a07ee6e52cc/08-progressive-hydration-front-end-performance-checklist-2020.png'>Large preview</a>)" alt="An example of AirBnB’s website showing without progressive hydration on the left, and with progressive hydration on the right" >}}

<ol class="continue">
<li><strong>How much can we serve statically?</strong><br />Whether you're working on a large application or a small site, it's worth considering what content could be <strong>served statically from a CDN</strong> (i.e. <a href="https://jamstack.org/">JAM Stack</a>), rather than being generated dynamically on the fly. Even if you have thousands of products and hundreds of filters with plenty of personalization options, you might still want to serve your critical landing pages statically, and decouple these pages from the framework of your choice.

<p>There are plenty of <a href="https://jamstack.org/generators/">static-site generators</a> and the pages they generate <a href="https://www.11ty.dev/speedlify/">are often very fast</a>. The more content we can pre-build ahead of time instead of generating page views on a server or client at request time, the better performance we will achieve.</p>

<p>In <a href="https://markus.oberlehner.net/blog/building-partially-hydrated-progressively-enhanced-static-websites-with-isomorphic-preact-and-eleventy/">Building Partially Hydrated, Progressively Enhanced Static Websites</a>, Markus Oberlehner shows how to build out websites with a static site generator and an SPA, while achieving progressive enhancement and a minimal JavaScript bundle size. Markus uses <strong>Eleventy and Preact</strong> as his tools, and shows how to set up the tools, add partial hydration, lazy hydration, client entry file, configure Babel for Preact and bundle Preact with Rollup &mdash; from start to finish.</p>

<p>With JAMStack used on large sites these days, a new performance consideration appeared: the <strong>build time</strong>. In fact, building out even thousands of pages with every new deploy can take minutes, so it's promising to see <a href="https://www.gatsbyjs.com/blog/2020-04-22-announcing-incremental-builds/">incremental builds in Gatsby</a> which improve build times by <strong>60 times</strong>, with an integration into popular CMS solutions like WordPress, Contentful, Drupal, Netlify CMS and others.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93501951-ccc7-48be-8f01-f148cbfa6c75/incremental-static-regeneration.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93501951-ccc7-48be-8f01-f148cbfa6c75/incremental-static-regeneration.png" sizes="100vw" caption="Incremental static regeneration with Next.js. (Image credit: <a href='https://www.prisma.io/blog/jamstack-with-nextjs-prisma-jamstackN3XT'>Prisma.io</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93501951-ccc7-48be-8f01-f148cbfa6c75/incremental-static-regeneration.png'>Large preview</a>)" alt="A flow chart showing User 1 on the top left and User 2 on the bottom left showing the process of incremental status re-generation" >}}

<p>Also, Next.js announced <a href="https://nextjs.org/blog/next-9-5#stable-incremental-static-regeneration">ahead-of-time and incremental static generation</a>, which allows us to add new static pages at runtime and update existing pages after they've been already built, by re-rendering them in the background as traffic comes in.</p>

<p>Need an even more lightweight approach? In his talk on <a href="https://www.youtube.com/watch?v=taOyVmLgym4">Eleventy, Alpine and Tailwind: towards a lightweight Jamstack</a>, Nicola Goutay explains the differences between CSR, SSR and everything-in-between, and shows how to use a more lightweight approach &mdash; along with a <a href="https://github.com/orbit-love/orbit-web">GitHub repo</a> that shows the approach in practice.</p>
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

{{% feature-panel %}}

## Assets Optimizations

<ol class="continue">
<li><strong>Use Brotli for plain text compression.</strong><br />In 2015, Google <a href="https://opensource.googleblog.com/2015/09/introducing-brotli-new-compression.html">introduced</a> <a href="https://github.com/google/brotli">Brotli</a>, a new open-source lossless data format, which is now <a href="https://caniuse.com/#search=brotli">supported in all modern browsers</a>. The <a href="https://github.com/google/brotli">open sourced Brotli library</a>, that implements an encoder and decoder for Brotli, has <a href="https://blog.cloudflare.com/brotli-compression-using-a-reduced-dictionary/">11 predefined quality levels</a> for the encoder, with higher quality level demanding more CPU in exchange for a better compression ratio. Slower compression will ultimately lead to higher compression rates, yet still, Brotli decompresses fast. It’s worth noting though that <a href="https://expeditedsecurity.com/blog/nginx-brotli/">Brotli with the compression level 4 is both smaller and compresses faster than Gzip</a>.

<p>In practice, Brotli appears to be <a href="https://paulcalvano.com/index.php/2018/07/25/brotli-compression-how-much-will-it-reduce-your-content/">much</a> <a href="https://quixdb.github.io/squash-benchmark/#results-table">more effective</a> than Gzip. Opinions and experiences differ, but if your site is already optimized with Gzip, you might be expecting <a href="https://blog.bitsrc.io/gzip-to-brotli-better-frontend-load-performance-b2b4d8dbf60f">at least</a> <a href="https://csswizardry.com/2020/04/real-world-effectiveness-of-brotli/">single-digit improvements</a> and at best <a href="https://expeditedsecurity.com/blog/nginx-brotli/">double-digits improvements</a> in size reduction and FCP timings. You can also <a href="https://tools.paulcalvano.com/compression.php">estimate Brotli compression savings for your site</a>.</p>

<p>Browsers will accept Brotli only if the user is visiting a website over HTTPS. Brotli is widely supported, and many CDNs support it (<a href="https://community.akamai.com/community/web-performance/blog/2017/08/18/brotli-support-enablement-on-akamai">Akamai</a>, <a href="https://www.netlify.com/blog/2020/05/20/gain-instant-performance-boosts-as-brotli-comes-to-netlify-edge/">Netlify Edge</a>, <a href="https://medium.com/@felice.geracitano/brotli-compression-delivered-from-aws-7be5b467c2e1">AWS</a>, <a href="https://www.keycdn.com/blog/keycdn-brotli-support">KeyCDN</a>, <a href="https://docs.fastly.com/guides/detailed-product-descriptions/performance-optimization-package">Fastly</a> (currently only as a pass-through), <a href="https://support.cloudflare.com/hc/en-us/articles/200168396-What-will-Cloudflare-compress-">Cloudflare</a>, <a href="https://www.cdn77.com/brotli">CDN77</a>) and you can <a href="https://calendar.perfplanet.com/2016/enabling-brotli-even-on-cdns-that-dont-support-it-yet/">enable Brotli even on CDNs that don’t support it</a> yet (with a service worker).</p>

<p>The catch is that because compressing <em>all</em> assets with Brotli at a high compression level is expensive, many hosting providers can’t use it at full scale just because of the huge cost overhead it produces. In fact, at the highest level of compression, Brotli is <em>so</em> slow that any potential gains in file size could be nullified by the amount of time it takes for the server to begin sending the response as it waits to dynamically compress the asset. (But if you have time during the build time with static compression, of course, <a href="https://css-tricks.com/brotli-static-compression/">higher compression settings are preferred</a>.)</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b62dce07-c24b-443a-8722-e55d8981cfea/new-brotli-compression-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b62dce07-c24b-443a-8722-e55d8981cfea/new-brotli-compression-opt.png" sizes="100vw" caption="Comparison of back end times of various compression methods. Unsurprisingly, <a href='https://css-tricks.com/brotli-static-compression/'>Brotli is slower than gzip</a> (for now). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b62dce07-c24b-443a-8722-e55d8981cfea/new-brotli-compression-opt.png'>Large preview</a>)" alt="A comparison shown as a whisker chart showing various compression methods across three different back-end times: minimum, average and 90th percentile" >}}

<p>This might be changing though. The Brotli file format includes a <strong>built-in static dictionary</strong>, and in addition to containing various strings in multiple languages, it also supports the option to apply multiple transformations to those words, increasing its versatility. In his research, Felix Hanau has discovered a way to <a href="https://blog.cloudflare.com/brotli-compression-using-a-reduced-dictionary/">improve the compression at levels 5 through 9</a> by using "a more specialized subset of the dictionary than the default" and relying on the <code>Content-Type</code> header to tell the compressor if it should use a dictionary for HTML, JavaScript or CSS. The result was a "negligible performance impact (1% to 3% more CPU compared to 12% normally) when compressing web content at high compression levels, using a limited dictionary use approach."</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e04e215-b689-4816-9c67-0674767d12fa/compression-gain-brotli-level5.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e04e215-b689-4816-9c67-0674767d12fa/compression-gain-brotli-level5.png" sizes="100vw" caption="With the improved dictionary approach, we can compress assets faster on higher compression levels, all while <a href='https://blog.cloudflare.com/brotli-compression-using-a-reduced-dictionary/'>using only 1% to 3% more CPU</a>. Normally, compression level 6 over 5 would increase CPU usage by up to 12%. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e04e215-b689-4816-9c67-0674767d12fa/compression-gain-brotli-level5.png'>Large preview</a>)" alt="A bar chart showing compression gain using Brotli reduced dictionaries at level 5" >}}

<p>On top of that, with <a href="https://dev.to/riknelix/fast-and-efficient-recompression-using-previous-compression-artifacts-47g5">Elena Kirilenko’s research</a>, we can achieve fast and <strong>efficient Brotli recompression</strong> using previous compression artifacts. According to Elena, "once we have an asset compressed via Brotli, and we’re trying to compress dynamic content on-the-fly, where the content resembles content available to us ahead of time, we can achieve significant improvements in compression times."</p>

<p>How often is it the case? E.g. with delivery of <strong>JavaScript bundles subsets</strong> (e.g. when parts of the code are already cached on the client or with dynamic bundle serving with <a href="https://docs.google.com/document/d/11t4Ix2bvF1_ZCV9HKfafGfWu82zbOD7aUhZ_FyDAgmA/edit#">WebBundles</a>). Or with dynamic HTML based on known-in-advance templates, or <strong>dynamically subsetted WOFF2 fonts</strong>. According to Elena, we can get <a href="https://dev.to/riknelix/fast-and-efficient-recompression-using-previous-compression-artifacts-47g5">5.3% improvement on compression</a> and 39% improvement on compression speed when removing 10% of the content, and 3.2% better compression rates and 26% faster compression, when removing 50% of the content.</p>

<p>Brotli compression is getting better, so if you can bypass the cost of dynamically compressing static assets, it’s definitely worth the effort. It goes without saying that Brotli can be used for any plaintext payload &mdash; HTML, CSS, SVG, JavaScript, JSON, and so on.</p>

<p><strong>Note</strong>: as of early 2021, approximately <a href="https://almanac.httparchive.org/en/2020/compression#current-state-of-http-compression">60% of HTTP responses are delivered with no text-based compression</a>, with 30.82% compressing with Gzip, and 9.1% compressing with Brotli (both on mobile and on desktop). E.g., <a href="https://twitter.com/hdjirdeh/status/1280731085379211265">23.4% of Angular pages are not compressed</a> (via gzip or Brotli). Yet often turning on compression is one of the easiest wins to improve performance with a simple flip of a switch.</p>

<p><strong>The strategy?</strong> <a href="https://css-tricks.com/brotli-static-compression/">Pre-compress static assets with Brotli+Gzip</a> at the highest level and compress (dynamic) HTML on the fly with Brotli at level 4–6. Make sure that the server handles content negotiation for Brotli or Gzip properly.</p></li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82c6a7d0-7d2d-4ed8-87c4-ed6dae698aa3/compression-algorithms-for-http-requests.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82c6a7d0-7d2d-4ed8-87c4-ed6dae698aa3/compression-algorithms-for-http-requests.png" sizes="100vw" caption="Of the resources that are served compressed in 2020, 22.59% are compressed with Brotli. Around 77.39% are compressed with gzip. (Image source: <a href='https://almanac.httparchive.org/en/2020/compression'>Web Almanac: Compression</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82c6a7d0-7d2d-4ed8-87c4-ed6dae698aa3/compression-algorithms-for-http-requests.png'>Large preview</a>)" alt="A bar chart showing the compression algorithms for HTTP requests according to the Web Almanax 2020 report" >}}

<ol class="continue">
<li><strong>Do we use adaptive media loading and client hints?</strong><br />It’s coming from the land of old news, but it’s always a good reminder to use <a href="https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/">responsive images</a> with <code>srcset</code>, <code>sizes</code> and the <code>&lt;picture&gt;</code> element. Especially for sites with a heavy media footprint, we can take it a step further with <a href="https://glitch.com/~next-episode-adaptive-loading">adaptive media loading</a> (in this example React + Next.js), serving <strong>light experience to slow networks</strong> and low-memory devices and full experience to fast network and high-memory devices. In the context of React, we can achieve it with client hints on the server and <a href="https://github.com/GoogleChromeLabs/react-adaptive-hooks">react-adaptive-hooks</a> on the client.

<p>The future of responsive images might change dramatically with the wider adoption of <a href="https://cloudfour.com/thinks/responsive-images-201-client-hints/">client hints</a>. Client hints are HTTP request header fields, e.g. <code>DPR</code>, <code>Viewport-Width</code>, <code>Width</code>, <code>Save-Data</code>, <code>Accept</code> (to specify image format preferences) and others. They are supposed to inform the server about the specifics of user’s browser, screen, connection etc.</p>

<p>As a result, the server can decide how to fill in the layout with <strong>appropriately sized images</strong>, and serve only these images in desired formats. With client hints, we move the resource selection from HTML markup and into the request-response negotiation between the client and server.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08a226c5-5a9a-4bd2-bba7-dad7e74f69e9/adaptive-media-serving-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08a226c5-5a9a-4bd2-bba7-dad7e74f69e9/adaptive-media-serving-opt.png" sizes="100vw" caption="Adaptive media serving in use. We send a placeholder with text to users who are offline, a low-resolution image to 2G users, a high-resolution image to 3G users and an HD video to 4G users. Via <a href='https://dev.to/addyosmani/loading-web-pages-fast-on-a-20-feature-phone-8h6'>Loading web pages fast on a $20 feature phone</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08a226c5-5a9a-4bd2-bba7-dad7e74f69e9/adaptive-media-serving-opt.png'>Large preview</a>)" alt="An illustration showing how adaptive media serving can be used by sending different resolutions to users depending on their network capability" >}}

<p>As Ilya Grigorik <a href="https://developers.google.com/web/updates/2015/09/automating-resource-selection-with-client-hints">noted</a> a while back, client hints complete the picture &mdash; they aren’t an alternative to responsive images. "The <code>&lt;picture&gt;</code> element provides the necessary art-direction control in the HTML markup. Client hints provide annotations on resulting image requests that enable resource selection automation. Service Worker provides full request and response management capabilities on the client."</p>

<p>A service worker could, for example, <strong>append new client hints headers values</strong> to the request, rewrite the URL and point the image request to a CDN, adapt response based on connectivity and user preferences, etc. It holds true not only for image assets but for pretty much all other requests as well.</p>

<p>For clients that support client hints, one could measure <a href="https://twitter.com/igrigorik/status/1032657105998700544">42% byte savings on images</a> and 1MB+ fewer bytes for 70th+ percentile. On Smashing Magazine, we could measure <a href="https://www.smashingmagazine.com/2016/01/leaner-responsive-images-client-hints/">19-32% improvement</a>, too. Client hints <a href="https://caniuse.com/#search=client-hints">are supported in Chromium-based browsers</a>, but they are still under consideration in <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=935216">Firefox</a>.</p>

<p>However, if you supply both the normal responsive images markup and the <code>&lt;meta&gt;</code> tag for Client Hints, then a supporting browser will evaluate the responsive images markup and request the appropriate image source using the Client Hints HTTP headers.</p>
</li>
<li><strong>Do we use responsive images for background images?</strong><br />We surely should! With <a href="https://caniuse.com/css-image-set"><code>image-set</code></a>, now <a href="https://twitter.com/nomsternom/status/1298998112933916682">supported in Safari 14</a> and in <a href="https://caniuse.com/css-image-set">most modern browsers except Firefox</a>, we can serve responsive background images as well:</p>

<pre class="language-css">
<code>background-image: url("fallback.jpg");
background-image:
  image-set( "photo-small.jpg" 1x,
    "photo-large.jpg" 2x,
    "photo-print.jpg" 600dpi);</code></pre>

<p>Basically we can conditionally serve low-resolution background images with a <code>1x</code> descriptor, and higher-resolution images with <code>2x</code> descriptor, and even a print-quality image with <code>600dpi</code> descriptor. Beware though: browsers do not provide any special information on background images to assistive technology, so ideally these photos would be merely decoration.</p>


<li><strong>Do we use WebP?</strong><br />Image compression is often considered a quick win, yet it’s still heavily underutilized in practice. Of course images do not block rendering, but they contribute heavily to poor LCP scores, and very often they are just too heavy and too large for the device they are being consumed on.

<p>So at the very least, we could explore using the <a href="https://www.smashingmagazine.com/2015/10/webp-images-and-performance/">WebP format</a> for our images. In fact, the WebP saga has been nearing the end last year with Apple adding <a href="https://developer.apple.com/documentation/safari-release-notes/safari-14-release-notes">support for WebP in Safari 14</a>. So after many years of discussions and debates, as of today, <a href="https://caniuse.com/?search=webp">WebP is supported in all modern browsers</a>. So we can serve WebP images with the <code>&lt;picture&gt;</code> element and a JPEG fallback if needed (see Andreas Bovens' <a href="https://dev.opera.com/articles/responsive-images/#different-image-types-use-case">code snippet</a>) or by using content negotiation (using <code>Accept</code> headers).</p>

<p>WebP isn’t without its <strong>downsides</strong> though. While WebP image file sizes <a href="https://www.ctrl.blog/entry/webp-vs-guetzli-zopfli">compared to equivalent Guetzli and Zopfli</a>, the format <a href="https://youtu.be/jTXhYj2aCDU?t=630">doesn’t support progressive rendering like JPEG</a>, which is why users might see the finished image faster with a good ol' JPEG although WebP images might be getting faster through the network. With JPEG, we can serve a "decent" user experience with the half or even quarter of the data and load the rest later, rather than have a half-empty image as it is in the case of WebP.</p>

<p>Your decision will depend on what you are after: with WebP, you’ll reduce the payload, and with JPEG you’ll improve perceived performance. You can learn more about WebP in <a href="https://www.youtube.com/watch?v=MBVBfLdh984">WebP Rewind</a> talk by Google’s Pascal Massimino.</p>

<p>For conversion to WebP, you can use <a href="https://webp-converter.com/">WebP Converter</a>, <a href="https://developers.google.com/speed/webp/docs/cwebp">cwebp</a> or <a href="https://downloads.webmproject.org/releases/webp/index.html">libwebp</a>. Ire Aderinokun has a very detailed <a href="https://bitsofco.de/why-and-how-to-use-webp-images-today/">tutorial on converting images to WebP</a>, too &mdash; and so does Josh Comeau in his piece on <a href="https://www.joshwcomeau.com/performance/embracing-modern-image-formats/">embracing modern image formats</a>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd5e6234-7669-4759-ab83-10f8dd0db976/maxresdefault-opt.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd5e6234-7669-4759-ab83-10f8dd0db976/maxresdefault-opt.jpg" sizes="100vw" caption="A thorough talk about WebP: <a href='https://www.youtube.com/watch?v=MBVBfLdh984'>WebP Rewind</a> by Pascal Massimino. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd5e6234-7669-4759-ab83-10f8dd0db976/maxresdefault-opt.jpg'>Large preview</a>)" alt="A slide used for Pascal Massimino’s talk titled Image ready: webp rewind" >}}

<p>Sketch natively supports WebP, and WebP images can be exported from Photoshop using a <a href="https://telegraphics.com.au/sw/product/WebPFormat#webpformat">WebP plugin for Photoshop</a>. But <a href="https://developers.google.com/speed/webp/docs/using">other options are available</a>, too.</p>

<p>If you’re using WordPress or Joomla, there are extensions to help you easily implement support for WebP, such as <a href="https://wordpress.org/plugins/optimus/">Optimus</a> and <a href="https://wordpress.org/plugins/cache-enabler/">Cache Enabler</a> for WordPress and <a href="https://extensions.joomla.org/extension/webp/">Joomla’s own supported extension</a> (via <a href="https://css-tricks.com/comparing-novel-vs-tried-true-image-formats/">Cody Arsenault</a>). You can also abstract away the <code>&lt;picture&gt;</code> element <a href="https://www.joshwcomeau.com/performance/embracing-modern-image-formats/">with React, styled components or gatsby-image</a>.</p>

<p>Ah &mdash; <em>shameless plug!</em> &mdash; Jeremy Wagner even <a href="https://www.smashingmagazine.com/ebooks/the-webp-manual/">published a Smashing book on WebP</a> which you might want to check if you are interested about everything around WebP.</p>
</li>
<li><strong>Do we use AVIF?</strong><br />You might have heard the big news: <a href="https://jakearchibald.com/2020/avif-has-landed/">AVIF has landed</a>. It’s a new image format derived from the keyframes of AV1 video. It’s an open, royalty-free format that supports lossy and lossless compression, <a href="https://colinbendell.github.io/webperf/animated-gif-decode/">animation</a>, lossy alpha channel and can handle sharp lines and solid colors (which was an issue with JPEG), while <a href="https://netflixtechblog.com/avif-for-next-generation-image-coding-b1d75675fe4">providing better results at both</a>.</p>

<p>In fact, compared to WebP and JPEG, <strong>AVIF performs significantly better</strong>, yielding <a href="https://www.ctrl.blog/entry/webp-avif-comparison.html">median file size savings for up to 50%</a> at the same DSSIM ((dis)similarity between two or more images using an algorithm approximating human vision). In fact, in his thorough post on <a href="https://www.industrialempathy.com/posts/image-optimizations/">optimizing image loading</a>, Malte Ubl notes that AVIF "very consistently outperforms JPEG in a very significant way. This is different from WebP which doesn’t always produce smaller images than JPEG and may actually be a net-loss due to lack of support for progressive loading."</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce9d0632-604b-4e0d-b84e-3eb608644cf0/avif-progressive-enhancement.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce9d0632-604b-4e0d-b84e-3eb608644cf0/avif-progressive-enhancement.jpg" sizes="100vw" caption="We can use AVIF as a progressive enhancement, delivering WebP or JPEG or PNG to older browsers. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce9d0632-604b-4e0d-b84e-3eb608644cf0/avif-progressive-enhancement.jpg'>Large preview</a>). See plain text view below." alt="A code snippet showing AVIF as progressive enhancement" >}}

<p>Ironically, AVIF can perform <a href="https://jakearchibald.com/2020/avif-has-landed/">even better than large SVGs</a> although of course it shouldn’t be seen as a replacement to SVGs. It is also one of the first image formats to support HDR color support; offering higher brightness, color bit depth, and color gamuts. The only downside is that currently AVIF doesn’t support <a href="https://www.ctrl.blog/entry/jpeg-progressive-loading.html">progressive image decoding</a> (yet?) and, similarly to Brotli, a high compression rate encoding is <a href="https://twitter.com/etportis/status/1298320096553705472">currently quite slow</a>, although decoding is fast.</p>

<p>AVIF is <a href="https://caniuse.com/?search=avif">currently supported in Chrome, Firefox and Opera</a>, and the support in Safari expected to be coming soon (as Apple is a member of the group that created AV1).</p>

<p>What’s the <strong>best way to serve images these days</strong> then? For illustrations and vector images, (compressed) SVG is undoubtedly the best choice. For photos, we use content negotiation methods with the <code>picture</code> element. If AVIF is supported, we send an AVIF image; if it’s not the case, we fall back to WebP first, and if WebP isn’t supported either, we switch to JPEG or PNG as fallback (applying <code>@media</code> conditions if needed):</p>

<pre class="language-html" id="avif-snippet">
<code>&lt;picture&gt;
  &lt;source srcset="image.avif" type="image/avif"&gt;
  &lt;source srcset="image.webp" type="image/webp"&gt;
  &lt;img src="image.jpg" alt="Photo" width="450" height="350"&gt;
&lt;/picture&gt;
</code></pre>

<p>Frankly, it’s more likely that we’ll be using some conditions within the <code>picture</code> element though:</p>

<pre class="language-html">
<code>&lt;picture&gt;
&lt;source
  sizes="(max-width: 608px) 100vw, 608px"
  srcset="
    /img/Z1s3TKV-1920w.avif 1920w,
    /img/Z1s3TKV-1280w.avif 1280w,
    /img/Z1s3TKV-640w.avif   640w,
    /img/Z1s3TKV-320w.avif   320w"
  type="image/avif"
/&gt;
&lt;source
  sizes="(max-width: 608px) 100vw, 608px"
  srcset="
    /img/Z1s3TKV-1920w.webp 1920w,
    /img/Z1s3TKV-1280w.webp 1280w,
    /img/Z1s3TKV-640w.webp   640w,
    /img/Z1s3TKV-320w.webp   320w"
  type="image/webp"
/&gt;
&lt;source
  sizes="(max-width: 608px) 100vw, 608px"
  srcset="
    /img/Z1s3TKV-1920w.jpg 1920w,
    /img/Z1s3TKV-1280w.jpg 1280w,
    /img/Z1s3TKV-640w.jpg   640w,
    /img/Z1s3TKV-320w.jpg   320w"
  type="image/jpeg"
/&gt;
  &lt;img src="fallback-image.jpg" alt="Photo" width="450" height="350"&gt;
&lt;/picture&gt;
</code>
</pre>

<p>You can go even further by <a href="https://twitter.com/brucel/status/1326154982756929536">swapping animated images with static images</a> for customers who opt-in for less motion with <code>prefers-reduced-motion</code>:</p>

<pre class="language-html">
<code>&lt;picture&gt;
  &lt;source media="(prefers-reduced-motion: reduce)" srcset="no-motion.avif" type="image/avif"&gt;&lt;/source&gt;
  &lt;source media="(prefers-reduced-motion: reduce)" srcset="no-motion.jpg" type="image/jpeg"&gt;&lt;/source&gt;
  &lt;source srcset="motion.avif" type="image/avif"&gt;&lt;/source&gt;
  &lt;img src="motion.jpg" alt="Animated AVIF"&gt;
&lt;/picture&gt;
</code>
</pre>

<p>Over the couple of months, AVIF has gained quite some traction:</p>
<ul>
<li>We can <a href="https://twitter.com/addyosmani/status/1327174361942552576">test WebP/AVIF fallbacks in the Rendering panel</a> in DevTools.</li>
<li>We can use <a href="https://squoosh.app/">Squoosh</a>, <a href="https://avif.io/">AVIF.io</a> and <a href="https://github.com/AOMediaCodec/libavif">libavif</a> to encode, decode, compress and convert AVIF files.</li>
<li>We can use Jake Archibald’s <a href="https://github.com/jakearchibald/jakearchibald.com/blob/main/shared/demos/2020/avif-has-landed/DecodedImg/index.tsx">AVIF Preact component</a> that decodes an AVIF-file in a worker and displays the result on a canvas,</a></li>
<li>To deliver AVIF only to supporting browsers, we can use a <a href="https://github.com/nucliweb/avif-in-css">PostCSS plugin along with a 315B-script</a> to use AVIF in your CSS declarations.</li>
<li>We can <a href="https://jross.me/progressively-delivering-new-image-formats-with-css-and-cloudflare-workers/">progressively deliver new image formats with CSS and Cloudlare Workers</a> to dynamically alter the returned HTML document, inferring information from the <code>accept</code> header, and then add the <code>webp/avif</code> etc. classes as appropriate.</li>
<li>AVIF is already <a href="https://twitter.com/etportis/status/1298320096553705472">available in Cloudinary</a> (with usage limits), <a href="https://blog.cloudflare.com/generate-avif-images-with-image-resizing/">Cloudflare supports AVIF in Image Resizing</a>, and you can enabled AVIF with <a href="https://reachlightspeed.com/blog/using-the-new-high-performance-avif-image-format-on-the-web-today/">Custom AVIF Headers in Netlify</a>.</li>
<li>When it comes to animation, AVIF performs as well as Safari’s <code>&lt;img src=mp4&gt;</code>, <a href="https://twitter.com/colinbendell/status/1309253099836583942">outperforming GIF and WebP at large</a>, but <a href="https://colinbendell.github.io/webperf/animated-gif-decode/">MP4 still performs better</a>.</li>
<li>In general, for animations, <a href="https://twitter.com/colinbendell/status/1309255819016523781">AVC1 (h264) &gt; HVC1 &gt; WebP &gt; AVIF &gt; GIF</a>, assuming that Chromium-based browsers will ever support <code>&lt;img src=mp4&gt;</code>.
</li>
<li>You can find more details about AVIF in <a href="https://www.youtube.com/watch?v=5RX6IgIF8bw&feature=youtu.be">AVIF for Next Generation Image Coding</a> talk by Aditya Mavlankar from Netflix, and <a href="https://www.youtube.com/watch?v=VHm5Ql33JYw">The AVIF Image Format</a> talk by Cloudflare’s Kornel Lesiński.</li>
<li>A great reference for everything AVIF: Jake Archibald’s comprehensive post on <a href="https://jakearchibald.com/2020/avif-has-landed/">AVIF has landed</a>.</li>
</ul>

<p><strong>So is the future AVIF then</strong>? Jon Sneyers <a href="https://twitter.com/jonsneyers/status/1298993416752074753">disagrees</a>: <a href="https://twitter.com/jonsneyers/status/1298993416752074753">AVIF performs 60% worse than JPEG XL</a>, another free and open format developed by Google and Cloudinary. In fact, <a href="https://cloudinary.com/blog/how_jpeg_xl_compares_to_other_image_codecs">JPEG XL</a> seems to be <a href="https://cloudinary.com/blog/how_jpeg_xl_compares_to_other_image_codecs#:~:text=In%20terms%20of%20functionality%20and,and%20types%20of%20image%20content.">performing</a> <a href="https://www.youtube.com/watch?v=mKMRzbuK9rA">way</a> <a href="https://www.youtube.com/watch?v=UphN1_7nP8U&feature=youtu.be">better</a> across the board. However, JPEG XL is still only in the final stages of standardization, and does not yet work in any browser. (Not to mix up with Microsoft’s <a href="https://calendar.perfplanet.com/2018/dont-use-jpeg-xr-on-the-web/">JPEG-XR</a> coming from good ol' Internet Explorer 9 times).</p>
</li>
</ol>

<figure class="article__image break-out"><a href="https://www.responsivebreakpoints.com/"><img
loading="lazy" decodig="async" fetchpriority="low" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db62c469-bbfc-4959-839d-590abb41b64e/responsive-breakpoints-opt.png 400w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db62c469-bbfc-4959-839d-590abb41b64e/responsive-breakpoints-opt.png 800w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db62c469-bbfc-4959-839d-590abb41b64e/responsive-breakpoints-opt.png 1200w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db62c469-bbfc-4959-839d-590abb41b64e/responsive-breakpoints-opt.png 1600w,
          https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db62c469-bbfc-4959-839d-590abb41b64e/responsive-breakpoints-opt.png 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db62c469-bbfc-4959-839d-590abb41b64e/responsive-breakpoints-opt.png" sizes="100vw" alt="Responsive Image Breakpoints Generator"></a>
  <figcaption>
    The <a href="https://www.responsivebreakpoints.com/">Responsive Image Breakpoints Generator</a> automates images and markup generation.
  </figcaption></figure>

<ol class="continue">
<li><strong>Are JPEG/PNG/SVGs properly optimized?</strong><br />When you’re working on a landing page on which it’s critical that a hero image loads blazingly fast, make sure that JPEGs are progressive and compressed with <a href="https://github.com/mozilla/mozjpeg">mozJPEG</a> (which improves the start rendering time by manipulating scan levels) or <a href="https://github.com/google/guetzli">Guetzli</a>, Google’s open-source encoder focusing on perceptual performance, and utilizing learnings from Zopfli and WebP. <a href="https://medium.com/@fox/talk-the-state-of-the-web-3e12f8e413b3">The only downside</a>: slow processing times (a minute of CPU per megapixel).</p>

<p>For PNG, we can use <a href="https://css-ig.net/pingo">Pingo</a>, and for SVG, we can use <a href="https://www.npmjs.com/package/svgo">SVGO</a> or <a href="https://jakearchibald.github.io/svgomg/">SVGOMG</a>. And if you need to quickly preview and copy or download all the SVG assets from a website, <a href="https://chrome.google.com/webstore/detail/svg-grabber-get-all-the-s/ndakggdliegnegeclmfgodmgemdokdmg">svg-grabber</a> can do that for you, too.

<p>Every single image optimization article would state it, but keeping vector assets clean and tight is always worth mentioning. Make sure to clean up unused assets, remove unnecessary metadata and reduce the number of path points in artwork (and thus SVG code). (<em>Thanks, Jeremy!</em>)</p>

<p>There are also useful online tools available though:</p>
<ul>
<li>Use <a href="https://squoosh.app/">Squoosh</a> to compress, resize and manipulate images at the optimal compression levels (lossy or lossless),</li>
<li>Use <a href="https://www.guetzli.it/">Guetzli.it</a> to compress and optimize JPEG images with Guetzli, which works well for images with sharp edges and solid colors (but might be quite a bit <a href="https://www.pixelz.com/blog/guetzli-mozjpeg-comparison/">slower</a>)).</li>
<li>Use the <a href="https://www.responsivebreakpoints.com/">Responsive Image Breakpoints Generator</a> or a service such as <a href="https://cloudinary.com/documentation/api_and_access_identifiers">Cloudinary</a> or <a href="https://www.imgix.com/">Imgix</a> to automate image optimization. Also, in many cases, using <code>srcset</code> and <code>sizes</code> alone will reap significant benefits.</li>
<li>To check the efficiency of your responsive markup, you can use <a href="https://github.com/filamentgroup/imaging-heap">imaging-heap</a>, a command line tool that measure the efficiency across viewport sizes and device pixel ratios.</li>
<li>You can <a href="https://github.com/marketplace/actions/image-actions">add automatic image compression to your GitHub workflows</a>, so no image can hit production uncompressed. The action uses mozjpeg and libvips that work with PNGs and JPGs.</li>
<li>To optimize storage interally, you could use Dropbox’s new <a href="https://github.com/dropbox/lepton">Lepton format</a> for losslessly compressing JPEGs by an average of 22%.</li>
<li>Use <a href="https://blurha.sh/">BlurHash</a> if you’d like to show a placeholder image early. BlurHash takes an image, and gives you a short string (only 20-30 characters!) that represents the placeholder for this image. The string is short enough that it can easily be added as a field in a JSON object.</li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fbe4611-cbf9-4c7e-819d-1236eb2053ce/whyblurhash.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fbe4611-cbf9-4c7e-819d-1236eb2053ce/whyblurhash.png" sizes="100vw" caption="<a href='https://blurha.sh/'>BlurHash</a> is a tiny, compact representation of a placeholder for an image. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fbe4611-cbf9-4c7e-819d-1236eb2053ce/whyblurhash.png'>Large preview</a>)" alt="A comparison of an interface without image placeholders on the left and with placeholders shown on the right" >}}

<p>Sometimes optimizing images alone won’t do the trick. To improve the time needed to start the <a href="https://calendar.perfplanet.com/2019/the-ugly-truth-about-optimising-beautiful-images/">rendering of a critical image</a>, <strong>lazy-load</strong> less important images and defer any scripts to load after critical images have already rendered. The most bulletproof way is <a href="https://www.smashingmagazine.com/2019/05/hybrid-lazy-loading-progressive-migration-native/">hybrid lazy-loading</a>, when we utilize native lazy-loading and <a href="https://github.com/verlok/lazyload">lazyload</a>, a library that detects any visibility changes triggered through user interaction (with IntersectionObserver which we’ll explore later). Additionally:</p>
<ul>
<li>Consider <a href="https://twitter.com/glenngabe/status/1292801991715033091">preloading critical images</a>, so a browser doesn’t discover them too late. For background images, if you want to be even more aggressive than that, you can add the image as a regular image with <code>&lt;img src&gt;</code>, and then hide it off the screen.</li>
<li>Consider <a href="https://www.filamentgroup.com/lab/sizes-swap/">Swapping Images with the Sizes Attribute</a> by specifying different image display dimensions depending on media queries, e.g. to manipulate <code>sizes</code> to swap sources in a magnifier component.</li>
<li>Review <a href="https://csswizardry.com/2018/06/image-inconsistencies-how-and-when-browsers-download-images/">image download inconsistencies</a> to prevent unexpected downloads for foreground and background images. Watch out for images that are loaded by default, but might never be displayed &mdash; e.g. in carousels, accordions and image galleries.</li>
<li>Make sure to <a href="https://www.smashingmagazine.com/2020/03/setting-height-width-images-important-again/">always set <code>width</code> and <code>height</code> on images</a>. Watch out for the <a href="https://drafts.csswg.org/css-sizing-4/#ratios"><code>aspect-ratio</code> property in CSS</a> and <a href="https://github.com/ojanvafai/intrinsicsize-attribute"><code>intrinsicsize</code> attribute</a> which will allow us to set aspect ratios and dimensions for images, so browser can reserve a pre-defined layout slot early to <a href="https://24ways.org/2018/jank-free-image-loads/">avoid layout jumps</a> during the page load.</li>
</ul>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebcc7dad-3cbc-4595-b141-2c6c80ab8fc6/aspect-ratio-in-browsers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebcc7dad-3cbc-4595-b141-2c6c80ab8fc6/aspect-ratio-in-browsers.png" sizes="100vw" caption="Should be just a matter of weeks or months now, with aspect-ratio landing in browsers. In <a href='https://twitter.com/jensimmons/status/1347287421633892356'>Safari Technical Preview 118</a> already. <a href='https://caniuse.com/mdn-css_properties_aspect-ratio'>Currently behind the flag in Firefox and Chrome.</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebcc7dad-3cbc-4595-b141-2c6c80ab8fc6/aspect-ratio-in-browsers.png'>Large preview</a>)" alt="A screenshot of code showing padding-top and aspect-ratio elements in use in an editor" >}}

<p>If you feel adventurous, you could chop and rearrange HTTP/2 streams using <a href="https://youtu.be/jTXhYj2aCDU?t=854">Edge workers</a>, basically a real-time filter living on the CDN, to send images faster through the network. Edge workers use JavaScript streams that use chunks which you can control (basically they are JavaScript that runs on the CDN edge that can modify the streaming responses), so you can control the delivery of images.</p>

<p>With a service worker, it’s too late as you can’t control what’s on the wire, but it does work with Edge workers. So you can use them on top of static JPEGs saved progressively for a particular landing page.</p>

{{< rimg href="https://pbs.twimg.com/media/DY1XZ28VwAAwjd8.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8422076c-6eea-4b35-a98c-b15445cb2dff/viewport-percentage-match.jpg" sizes="100vw" caption="A sample output by <a href='https://github.com/filamentgroup/imaging-heap'>imaging-heap</a>, a command line tool that measure the efficiency across viewport sizes and device pixel ratios. (<a href='https://pbs.twimg.com/media/DY1XZ28VwAAwjd8.jpg'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8422076c-6eea-4b35-a98c-b15445cb2dff/viewport-percentage-match.jpg'>Large preview</a>)" alt="A screenshot of the imaging-heap command line tool showing a table with various viewport sizes and device pixel ratios" >}}

<p>Not good enough? Well, you can also improve perceived performance for images with the <a href="https://csswizardry.com/2016/10/improving-perceived-performance-with-multiple-background-images/">multiple</a> <a href="https://jmperezperez.com/medium-image-progressive-loading-placeholder/">background</a> <a href="https://manu.ninja/dominant-colors-for-lazy-loading-images#tiny-thumbnails">images</a> <a href="https://css-tricks.com/the-blur-up-technique-for-loading-background-images/">technique</a>. Keep in mind that <a href="https://css-tricks.com/contrast-swap-technique-improved-image-performance-css-filters/">playing with contrast</a> and blurring out unnecessary details (or removing colors) can reduce file size as well. Ah, you need to <strong>enlarge a small photo</strong> without losing quality? Consider using <a href="https://letsenhance.io">Letsenhance.io</a>.</p>

<p>These optimizations so far cover just the basics. Addy Osmani has published a <a href="https://images.guide/">very detailed guide on Essential Image Optimization</a> that goes very deep into details of image compression and color management. For example, you could <strong>blur out unnecessary parts</strong> of the image (by applying a Gaussian blur filter to them) to reduce the file size, and eventually you might even start removing colors or turn the picture into black and white to reduce the size even further. For background images, exporting photos from Photoshop with 0 to 10% quality can be absolutely acceptable as well.</p>

<p>On Smashing Magazine, we use the postfix <code>-opt</code> for image names &mdash; for example, <code>brotli-compression-opt.png</code>; whenever an image contains that postfix, everybody on the team knows that the image has already been optimized.</p>

<p>Ah, and <a href="https://calendar.perfplanet.com/2018/dont-use-jpeg-xr-on-the-web/">don’t use JPEG-XR on the web</a> &mdash; "the processing of decoding JPEG-XRs software-side on the CPU nullifies and even outweighs the potentially positive impact of byte size savings, especially in the context of SPAs" (not to mix up with Cloudinary/Google’s <a href="https://cloudinary.com/blog/how_jpeg_xl_compares_to_other_image_codecs">JPEG XL</a> though).</p>
</li>
</ol>
{{< rimg breakout="true" href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c987b182-0a0e-40e5-8f8d-dd81feb991f5/replace-animated-gifs.jpg" sizes="100vw" caption="Addy Osmani <a href='https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/replace-animated-gifs-with-video/'>recommends</a> to replace animated GIFs with looping inline videos. The file size difference is noticeable (80% savings). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c987b182-0a0e-40e5-8f8d-dd81feb991f5/replace-animated-gifs.jpg'>Large preview</a>)" alt="Replacing animated GIFs with the video element with 80%+ savings" >}}
<ol class="continue">
<li><strong>Are videos properly optimized?</strong><br />We covered images so far, but we’ve avoided a conversation about good ol' GIFs. Despite our love for GIFs, it’s really the time to abandon them for good (at least in our websites and apps). Instead of loading heavy animated GIFs which impact both rendering performance and bandwidth, it’s a good idea to switch either to animated WebP (with GIF being a fallback) or replace them with <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/replace-animated-gifs-with-video/">looping HTML5 videos</a> altogether.

<p>Unlike with images, browsers do not preload <code>&lt;video&gt;</code> content, but HTML5 videos tend to be much lighter and smaller than GIFs. Not an option? Well, at least we can add lossy compression to GIFs with <a href="https://kornel.ski/lossygif">Lossy GIF</a>, <a href="https://github.com/kohler/gifsicle">gifsicle</a> or <a href="https://github.com/pornel/giflossy">giflossy</a>.</p>

<p>Tests by Colin Bendell show that inline videos within <code>img</code> tags in Safari Technology Preview <a href="https://calendar.perfplanet.com/2017/animated-gif-without-the-gif/">display at least 20× faster and decode 7× faster</a> than the GIF equivalent, in addition to being a fraction in file size. However, it’s not supported in other browsers.</p>

<p>In the land of good news, video formats have been <strong>advancing massively</strong> over the years. For a long time, we had hoped that WebM would become the format to rule them all, and WebP (which is basically one still image inside of the WebM video container) will become a replacement for dated image formats. Indeed, Safari is <a href="https://twitter.com/jensimmons/status/1275171897244823553">now supporting WebP</a>, but despite WebP and WebM <a href="https://caniuse.com/webp">gaining</a> <a href="https://caniuse.com/#feat=webm">support</a> these days, the breakthrough didn’t really happen.</p>

<p>Still, we could use WebM <a href="https://caniuse.com/webm">for most modern browsers</a> out there:</p>

<pre class="language-html">
<code>&lt;!-- By Houssein Djirdeh. https://web.dev/replace-gifs-with-videos/ --&gt;
&lt;!-- A common scenartio: MP4 with a WEBM fallback. --&gt;
&lt;video autoplay loop muted playsinline&gt;
  &lt;source src="my-animation.webm" type="video/webm"&gt;
  &lt;source src="my-animation.mp4" type="video/mp4"&gt;
&lt;/video&gt;
</code></pre>

<p>But perhaps we could revisit it altogether. In 2018, the Alliance of Open Media has released a new promising video format called <a href="https://aomedia.org/av1/"><em>AV1</em></a>. AV1 has compression similar to the H.265 codec (the evolution of H.264) but unlike the latter, AV1 is free. The H.265 license pricing pushed browser vendors to adopt a comparably performant AV1 instead: <strong>AV1 (just like H.265) compresses twice as good as WebM</strong>.</p>

{{< rimg href="https://upload.wikimedia.org/wikipedia/commons/thumb/8/84/AV1_logo_2018.svg/2560px-AV1_logo_2018.svg.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5a4354f-4a9b-420d-8979-bd7abb87aebc/av1-logo-2018-full.png" sizes="100vw" caption="AV1 has good chances of becoming the ultimate standard for video on the web. (Image credit: <a href='https://upload.wikimedia.org/wikipedia/commons/thumb/8/84/AV1_logo_2018.svg/2560px-AV1_logo_2018.svg.png'>Wikimedia.org</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5a4354f-4a9b-420d-8979-bd7abb87aebc/av1-logo-2018-full.png'>Large preview</a>)" alt="AV1 Logo 2018" >}}

<p>In fact, Apple currently uses HEIF format and HEVC (H.265), and all the photos and videos on the latest iOS are saved in these formats, not JPEG. While <a href="https://caniuse.com/#search=heif">HEIF</a> and <a href="https://caniuse.com/#search=hevc">HEVC (H.265)</a> aren’t properly exposed to the web (yet?), AV1 is &mdash; and <a href="https://caniuse.com/#feat=av1">it’s gaining browser support</a>. So adding the <code>AV1</code> source in your <code>&lt;video&gt;</code> tag is reasonable, as all browser vendors seem to be on board.</p>

<p>For now, the most widely used and supported encoding is H.264, served by MP4 files, so before serving the file, make sure that your MP4s are processed with a <a href="https://medium.com/@borisschapira/optimize-your-mp4-video-for-better-performance-dareboost-blog-fb2f3f3dce77">multipass-encoding</a>, blurred with the <a href="https://yalantis.com/blog/experiments-with-ffmpeg-filters-and-frei0r-plugin-effects/">frei0r iirblur effect</a> (if applicable) and <a href="https://www.adobe.com/devnet/video/articles/mp4_movie_atom.html">moov atom metadata</a> is moved to the head of the file, while your server <a href="https://medium.com/@borisschapira/optimize-your-mp4-video-for-better-performance-dareboost-blog-fb2f3f3dce77">accepts byte serving</a>. Boris Schapira provides <a href="https://medium.com/@borisschapira/optimize-your-mp4-video-for-better-performance-dareboost-blog-fb2f3f3dce77">exact instructions for FFmpeg</a> to optimize videos to the maximum. Of course, providing WebM format as an alternative would help, too.</p>

<p>Need to start rendering videos faster but <strong>video files are still too large</strong>? For example, whenever hou have a large background video on a landing page? A common technique to use is to show the very first frame as a still image first, or display a heavily optimized, short looping segment that could be interpreted as a part of the video, and then, whenever the video is buffered enough, start playing the actual video. Doug Sillars has a written a <a href="https://calendar.perfplanet.com/2019/performance-tips-for-background-video/">detailed guide to background video performance</a> that could be helpful in that case. (<em>Thanks, <a href="https://twitter.com/guypod">Guy Podjarny</a>!</em>).</p>

<p>For the above scenario, you might want to provide <strong>responsive poster images</strong>. By default, <code>video</code> elements only allow one image as the poster, which isn’t necessarily optimal. We can use <a href="https://nigelotoole.github.io/responsive-video-poster/">Responsive Video Poster</a>, a JavaScript library that allows you to use different poster images for different screens, while also adding a transitioning overlay and full styling control of video placeholders.</p>

<p>The research shows that <a href="https://www.akamai.com/kr/ko/multimedia/documents/technical-publication/video-stream-quality-impacts-viewer-behavior-inferring-causality-using-quasi-experimental-designs-technical-publication.pdf">video stream quality impacts viewer behavior</a>. In fact, viewers start to abandon the video if the startup delay exceeds about 2 seconds. Beyond that point, a 1-second increase in delay results in roughly a 5.8% increase in abandonment rate. So it’s not surprising that the <a href="https://dougsillars.com/2019/09/16/state-of-the-web-video-playback-metrics/">median video start time is 12.8s</a>, with 40% of videos having at least 1 stall, and 20% at least 2s of stalled video playback. In fact, video stalls are unavoidable on 3G as videos play back faster than the network can supply content.</p>

<p>So, what’s the solution? Usually small screen devices cannot handle the 720p and 1080p we are serving the desktop. According to <a href="https://dougsillars.com/2020/03/03/video-playback-on-mobile-devices/">Doug Sillars</a>, we can either create smaller versions of our videos, and use Javascript to detect the source for smaller screens to ensure a <strong>fast and smooth playback</strong> on these devices. Alternatively, we can use streaming video. HLS video streams will deliver an appropriately sized video to the device &mdash; abstracting the need to create different videos for different screens. It will also negotiate the network speed, and adapt the video bitrate for the speed of the network you are using.</p>

<p>To avoid the waste on bandwidth, we could only add the video source for devices that actually can play the video well. Alternatively, we can remove the <code>autoplay</code> attribute from the <code>video</code> tag altogether and use JavaScript to insert <code>autoplay</code> for larger screens. Additionally, we need to add <code>preload="none"</code> on <code>video</code> to tell the browser to not download <em>any</em> of the video files until it actually needs the file:</p>

<pre class="language-html">
<code>&lt;!-- Based on Doug Sillars's post. https://dougsillars.com/2020/01/06/hiding-videos-on-the-mbile-web/ --&gt;
&lt;video id="hero-video"
          preload="none"
          playsinline
          muted
          loop
          width="1920"
          height="1080"
          poster="poster.jpg"&gt;
&lt;source src="video.webm" type="video/webm"&gt;
&lt;source src="video.mp4" type="video/mp4"&gt;
&lt;/video&gt;
</code></pre>

<p>Then we can <a href="https://evilmartians.com/chronicles/better-web-video-with-av1-codec">target specifically browsers that actually support AV1</A>:</p>

<pre class="language-html">
<code>&lt;!-- Based on Doug Sillars's post. https://dougsillars.com/2020/01/06/hiding-videos-on-the-mbile-web/ --&gt;
&lt;video id="hero-video"
          preload="none"
          playsinline
          muted
          loop
          width="1920"
          height="1080"
          poster="poster.jpg"&gt;
&lt;source src="video.av1.mp4" type="video/mp4; codecs=av01.0.05M.08"&gt;
&lt;source src="video.hevc.mp4" type="video/mp4; codecs=hevc"&gt;
&lt;source src="video.webm" type="video/webm"&gt;
&lt;source src="video.mp4" type="video/mp4"&gt;
&lt;/video&gt;
</code></pre>

<p>We then could re-add the <code>autoplay</code> over a certain threshold (e.g. 1000px):</p>

<pre class="language-javascript">
<code>/* By Doug Sillars. https://dougsillars.com/2020/01/06/hiding-videos-on-the-mbile-web/ */
&lt;script&gt;
	window.onload = addAutoplay();
	var videoLocation  = document.getElementById("hero-video");
	function addAutoplay() {
		if(window.innerWidth > 1000){
			videoLocation.setAttribute("autoplay","");
	  };
	}
&lt;/script&gt;</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/952ad18f-bf8e-433e-a02d-1040d3aada55/new-stall-time-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/952ad18f-bf8e-433e-a02d-1040d3aada55/new-stall-time-opt.png" sizes="100vw" caption="Number of Stalls by device and network speed. Faster devices on faster networks have virtually no stalls. According to <a href='https://dougsillars.com/2020/03/03/video-playback-on-mobile-devices/'>Doug Sillars’ research</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/952ad18f-bf8e-433e-a02d-1040d3aada55/new-stall-time-opt.png'>Large preview</a>)" alt="A bar chart showing small tme (ms) by device and network speed including 3G, Cable, LTE and Native across Alcatel 1X, Moto G, Moto G4, MotoE, Nexus 5 and OnePlus 5" >}}

<p>Video playback performance is a <a href="https://dougsillars.com/2019/09/16/state-of-the-web-video-playback-metrics/">story on its own</a>, and if you’d like to dive into it in details, take a look at another Doug Sillars' series on <a href="https://www.smashingmagazine.com/2018/10/video-playback-on-the-web-part-1/">The Current State of Video</a> and <a href="https://www.smashingmagazine.com/2018/10/video-playback-on-the-web-part-2/">Video Delivery Best Practices</a> that include details on video delivery metrics, video preloading, compression and streaming. Finally, you can check how slow or fast your video streaming will be with <a href="https://dougsillars.github.io/StreamOrNot/">Stream or Not</a>.</p>
</li>
</ol>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb634666-55ab-4db3-aa40-4b146a859041/font-loading-strategies-opt.png" sizes="100vw" caption="Zach Leatherman’s <a href='https://www.zachleat.com/web/comprehensive-webfonts/'>Comprehensive Guide to Font-Loading Strategies</a> provides a dozen options for better web font delivery." alt="Zach Leatherman’s Comprehensive Guide to Font-Loading Strategies shown as a mind map graph" >}}

<ol class="continue">
<li><strong>Is web font delivery optimized?</strong><br />The first question that’s worth asking is if we can get away with <a href="https://www.smashingmagazine.com/2015/11/using-system-ui-fonts-practical-guide/">using UI system fonts</a> in the first place &mdash; we just need to make sure to <a href="https://fontfamily.io/Roboto,Segoe_UI,TImes,Helvetica,sans-serif">double check that they appear correctly</a> on various platforms. If it’s not the case, chances are high that the web fonts we are serving include glyphs and extra features and weights that aren’t being used. We can ask our type foundry to <strong>subset web fonts</strong> or if we are using open-source fonts, subset them on our own with <a href="https://www.afasterweb.com/2018/03/09/subsetting-fonts-with-glyphhanger/">Glyphhanger</a> or <a href="https://www.fontsquirrel.com/tools/webfont-generator">Fontsquirrel</a>. We can even automate our entire workflow with Peter Müller’s <a href="https://github.com/Munter/subfont#readme">subfont</a>, a command line tool that statically analyses your page in order to generate the most optimal web font subsets, and then inject them into our pages.

<p><a href="https://caniuse.com/#search=woff2">WOFF2 support</a> is great, and we can use WOFF as fallback for browsers that don’t support it &mdash; or perhaps legacy browsers could be served system fonts. There are <em>many, many, many</em> options for web font loading, and we can choose one of the strategies from Zach Leatherman’s "<a href="https://www.zachleat.com/web/comprehensive-webfonts/">Comprehensive Guide to Font-Loading Strategies</a>," (code snippets also available as <a href="https://github.com/zachleat/web-font-loading-recipes">Web font loading recipes</a>).</p>

<p>Probably the better options to consider today are <a href="https://www.zachleat.com/web/comprehensive-webfonts/#critical-foft-preload">Critical FOFT with <code>preload</code></a> and <a href="https://www.zachleat.com/web/the-compromise/">"The Compromise" method</a>. Both of them use a <strong>two-stage render</strong> for delivering web fonts in steps &mdash; first a small supersubset required to render the page fast and accurately with the web font, and then load the rest of the family async. The difference is that "The Compromise" technique loads polyfill asynchronously only if <a href="https://www.igvita.com/2014/01/31/optimizing-web-font-rendering-performance/#font-load-events">font load events</a> are not supported, so you don’t need to load the polyfill by default. Need a quick win? Zach Leatherman has a <a href="https://www.zachleat.com/web/23-minutes/">quick 23-min tutorial and case study</a> to get your fonts in order.</p>

<p>In general, it might be a good idea to use the <code>preload</code> resource hint to preload fonts, but in your markup include the hints <em>after</em> the link to critical CSS and JavaScript. With <code>preload</code>, there is a <a href="https://andydavies.me/blog/2019/02/12/preloading-fonts-and-the-puzzle-of-priorities/">puzzle of priorities</a>, so consider injecting <code>rel="preload"</code> elements into the DOM just before the external blocking scripts. According to Andy Davies, "resources injected using a script are hidden from the browser until the script executes, and we can use this behaviour to delay when the browser discovers the <code>preload</code> hint." Otherwise, font loading will cost you in the first render time.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cabdd79-67f0-44f4-9cfa-3b87732938cb/pre-render-fonts-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cabdd79-67f0-44f4-9cfa-3b87732938cb/pre-render-fonts-opt.png" sizes="100vw" caption="When everything is critical, nothing is critical. preload only one or a maximum of two fonts of each family. (Image credit: <a href='https://noti.st/zachleat/KNaZEg/the-five-whys-of-web-font-loading-performance#s6vhQNE'>Zach Leatherman</a> &ndash; slide 93) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cabdd79-67f0-44f4-9cfa-3b87732938cb/pre-render-fonts-opt.png'>Large preview</a>)" alt="A screenshot of slide 93 showing two example of images with a title next to them saying ‘Metrics prioritization: preload one of each family’" >}}

<p>It’s a good idea to <a href="https://youtu.be/FbguhX3n3Uc?t=1637">be selective</a> and choose files that matter most, e.g. the ones that are critical for rendering or that would help you avoiding visible and disruptive text reflows. In general, Zach advises to <strong>preload one or two fonts of each family</strong> &mdash; it also makes sense to delay some font loading if they are less critical.</p>

<p>It has become quite common to use <code>local()</code> value (which refers to a lo­cal font by name) when defining a <code>font-family</code> in the <code>@font-face</code> rule:</p>

<pre><code class="language-css">/* Warning! Not a good idea! */
@font-face {
  font-family: Open Sans;
  src: local('Open Sans Regular'),
       local('OpenSans-Regular'),
       url('opensans.woff2') format ('woff2'),
       url('opensans.woff') format('woff');
}</code></pre>

<p>The idea is reasonable: some popular open-source fonts such as Open Sans are coming pre-installed with some drivers or apps, so if the font is avail­able lo­cally, the browser does­n’t need to down­load the web font and can dis­play the lo­cal font im­me­di­ately. As <a href="https://www.bramstein.com/writing/web-font-anti-patterns-local-fonts.html">Bram Stein noted</a>, "though a lo­cal font matches the name of a web font, it most likely <strong>isn’t the same font</strong>. Many web fonts dif­fer from their "desk­top" ver­sion. The text might be ren­dered dif­fer­ently, some char­ac­ters may fall back to other fonts, Open­Type fea­tures can be miss­ing en­tirely, or the line height may be dif­fer­ent."</p>

<p>Also, as typefaces evolve over time, the locally installed version might be very different from the web font, with characters looking very different. So, according to Bram, it’s better to <strong>never mix lo­cally in­stalled fonts and web fonts</strong> in <code>@font-face</code> rules. Google Fonts has followed suit by <a href="https://twitter.com/googlefonts/status/1328761547041148929?lang=en">disabling <code>local()</code> on the CSS results for all users</a>, other than Android requests for Roboto.</p>

<p>Nobody likes waiting for the content to be displayed. With the <a href="https://font-display.glitch.me/"><code>font-display</code> CSS descriptor</a>, we can control the font loading behavior and enable content to be readable <em>immediately</em> (with <code>font-display: optional</code>) or <em>almost immediately</em> (with a timeout of 3s, as long as the font gets successfully downloaded — with <code>font-display: swap</code>). (Well, it’s a <a href="https://font-display.glitch.me/">bit more complicated than that</a>.)</p>

<p>However, if you want to <a href="https://www.zachleat.com/web/font-display-reflow/">minimize the impact of text reflows</a>, we could use the <em>Font Loading API</em> (<a href="https://caniuse.com/font-loading">supported in all modern browsers</a>). Specifically that means for every font, we’d creata a <code>FontFace</code> object, then try to fetch them all, and only then apply them to the page. This way, we <strong>group all repaints</strong> by loading all fonts asynchronously, and then switch from fallback fonts to the web font exactly once. Take a look at <a href="https://vimeo.com/304099438">Zach’s explanation</a>, starting at 32:15, and the <a href="https://github.com/zachleat/performance-sometime/blob/master/css-font-loading.js">code snippet</a>):</p>

<div class="break-out">
<pre class="language-javascript">
<code>/&#42; Load two web fonts using JavaScript &#42;/
/&#42; Zach Leatherman: https://noti.st/zachleat/KNaZEg/the-five-whys-of-web-font-loading-performance#sWkN4u4 &#42;/

// Remove existing @font-face blocks
// Create two
let font = new FontFace("Noto Serif", /&#42; ... &#42;/);
let fontBold = new FontFace("Noto Serif, /&#42; ... &#42;/);

// Load two fonts
let fonts = await Promise.all([
  font.load(),
  fontBold.load()
])

// Group repaints and render both fonts at the same time!
fonts.forEach(font => documents.fonts.add(font));
</code>
</pre>
</div>

<p>To initiate a very early fetch of the fonts with Font Loading API in use, Adrian Bece <a href="https://css-tricks.com/how-to-load-fonts-in-a-way-that-fights-fout-and-makes-lighthouse-happy/">suggests</a> to add a non-breaking space <code>nbsp;</code> at the top of the <code>body</code>, and hide it visually with <code>aria-visibility: hidden</code> and a <code>.hidden</code> class:</p>

<pre class="language-html">
<code>&lt;body class="no-js"&gt;
  &lt;!-- ... Website content ... --&gt;
  &lt;div aria-visibility="hidden" class="hidden" style="font-family: '[web-font-name]'"&gt;
      &lt;!-- There is a non-breaking space here --&gt;
  &lt;/div&gt;
  &lt;script&gt;
    document.getElementsByTagName("body")[0].classList.remove("no-js");
  &lt;/script&gt;
&lt;/body&gt;
</code>
</pre>

<p>This goes along with CSS that has different font families declared for different states of loading, with the change triggered by Font Loading API once the fonts have successfully loaded:</p>

<pre class="language-css">
<code>body:not(.wf-merriweather--loaded):not(.no-js) {
  font-family: [fallback-system-font];
  /* Fallback font styles */
}

.wf-merriweather--loaded,
.no-js {
  font-family: "[web-font-name]";
  /* Webfont styles */
}

/* Accessible hiding */
.hidden {
  position: absolute;
  overflow: hidden;
  clip: rect(0 0 0 0);
  height: 1px;
  width: 1px;
  margin: -1px;
  padding: 0;
  border: 0;
}
</code>
</pre>

<p>If you ever wondered why despite all your optimizations, Lighthouse still suggests to eliminate render-blocking resources (fonts), in the same article Adrian Bece provides a few <a href="https://css-tricks.com/how-to-load-fonts-in-a-way-that-fights-fout-and-makes-lighthouse-happy/">techniques to make Lighthouse happy</a>, along with a <a href="https://github.com/codeAdrian/gatsby-omni-font-loader">Gatsby Omni Font Loader</a>, a performant asynchronous font loading and Flash Of Unstyled Text (FOUT) handling plugin for Gatsby.</p>

<p>Now, many of us might be using a CDN or a third-party host to load web fonts from. In general, it’s <a href="https://speakerdeck.com/addyosmani/web-performance-made-easy?slide=55">always</a> better to <a href="https://csswizardry.com/2019/05/self-host-your-static-assets/">self-host all your static assets</a> if you can, so consider using <a href="https://google-webfonts-helper.herokuapp.com/fonts">google-webfonts-helper</a>, a hassle-free way to self-host Google Fonts. And if it’s not possible, you can perhaps <a href="https://blog.cloudflare.com/fast-google-fonts-with-cloudflare-workers/">proxy the Google Font files through the page origin</a>.</p>

<p>It's worth noting though that Google is doing <a href="https://www.tunetheweb.com/blog/should-you-self-host-google-fonts/">quite a bit of work</a> out of the box, so a server might need a bit of tweaking to avoid delays (<em>thanks, Barry!</em>)</p>

<p>This is quite important especially as since Chrome v86 (released October 2020), cross-site resources like <a href="https://wicki.io/posts/2020-11-goodbye-google-fonts/">fonts can’t be shared on the same CDN</a> anymore &mdash; due to the <a href="https://developers.google.com/web/updates/2020/10/http-cache-partitioning">partitioned browser cache</a>. This behavior was a default in Safari for years.</p>

<p>But if it’s not possible at all, there is a way to get to <a href="https://csswizardry.com/2020/05/the-fastest-google-fonts/">the fastest possible Google Fonts</a> with Harry Roberts' snippet:

<pre class="language-html">
<code>&lt;!-- By Harry Roberts.
https://csswizardry.com/2020/05/the-fastest-google-fonts/

- 1. Preemptively warm up the fonts’ origin.
- 2. Initiate a high-priority, asynchronous fetch for the CSS file. Works in
-    most modern browsers.
- 3. Initiate a low-priority, asynchronous fetch that gets applied to the page
-    only after it’s arrived. Works in all browsers with JavaScript enabled.
- 4. In the unlikely event that a visitor has intentionally disabled
-    JavaScript, fall back to the original method. The good news is that,
-    although this is a render-blocking request, it can still make use of the
-    preconnect which makes it marginally faster than the default.
--&gt;

&lt;!-- [1] --&gt;
&lt;link rel="preconnect"
      href="https://fonts.gstatic.com"
      crossorigin /&gt;

&lt;!-- [2] --&gt;
&lt;link rel="preload"
      as="style"
      href="$CSS&display=swap" /&gt;

&lt;!-- [3] --&gt;
&lt;link rel="stylesheet"
      href="$CSS&display=swap"
      media="print" onload="this.media='all'" /&gt;

&lt;!-- [4] --&gt;
&lt;noscript&gt;
  &lt;link rel="stylesheet"
        href="$CSS&display=swap" /&gt;
&lt;/noscript&gt;
</code></pre>

<p>Harry’s strategy is to pre-emptively warm up the fonts’ origin first. Then we initiate a high-priority, asynchronous fetch for the CSS file. Afterwards, we initiate a low-priority, asynchronous fetch that gets applied to the page only after it’s arrived (with a <a href="https://www.filamentgroup.com/lab/load-css-simpler/">print stylesheet trick</a>). Finally, if JavaScript isn’t supported, we fall back to the original method.</p>

<p>Ah, talking about Google Fonts: you can <strong>shave up to 90% of the size</strong> of Google Fonts requests by <a href="https://developers.google.com/fonts/docs/getting_started#optimizing_your_font_requests">declaring only characters you need</a> with <code>&amp;text</code>. Plus, the <a href="https://css-tricks.com/google-fonts-and-font-display/">support for font-display was added recently</a> to Google Fonts as well, so we can use it out of the box.</p>

<p>A quick word of caution though. If you use <code>font-display: optional</code>, it <a href="https://www.zachleat.com/web/preload-font-display-optional/">might be suboptimal</a> to also use <code>preload</code> as it will trigger that web font request early (causing <strong>network congestion</strong> if you have other critical path resources that need to be fetched). Use <code>preconnect</code> for faster cross-origin font requests, but be cautious with <code>preload</code> as preloading fonts from a different origin wlll incur network contention. All of these techniques are covered in Zach’s <a href="https://github.com/zachleat/web-font-loading-recipes">Web font loading recipes</a>.</p>

<p>On the other hand, it might be a good idea to <a href="https://calendar.perfplanet.com/2020/a-font-display-setting-for-slow-connections/">opt out of web fonts</a> (or at least second stage render) if the user has enabled <a href="https://webkit.org/blog/7551/responsive-design-for-motion/">Reduce Motion</a> in accessibility preferences or has opted in for <strong>Data Saver Mode</strong> (see <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/save-data/"><code>Save-Data</code> header</a>), or when the user has a slow connectivity (via <a href="https://developer.mozilla.org/en-US/docs/Web/API/Network_Information_API">Network Information API</a>).</p>

<p>We can also use the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-data"><code>prefers-reduced-data</code></a> CSS media query to <em>not</em> define font declarations if the user has opted into data-saving mode (there are <a href="https://polypane.app/blog/creating-websites-with-prefers-reduced-data/">other use-cases, too</a>). The media query would basically expose if the <code>Save-Data</code> request header from the Client Hint HTTP extension is on/off to allow for usage with CSS. Currently <a href="https://caniuse.com/?search=prefers-reduced-data">supported only in Chrome and Edge behind a flag</a>.</p>

<p><strong>Metrics?</strong> To measure the web font loading performance, consider the <a href="https://noti.st/zachleat/KNaZEg/the-five-whys-of-web-font-loading-performance#s5IYiho"><em>All Text Visible</em></a> metric (the moment when all fonts have loaded and all content is displayed in web fonts), <a href="https://vimeo.com/336091879#t=1550s">Time to Real Italics</a> as well as <a href="https://noti.st/zachleat/KNaZEg/the-five-whys-of-web-font-loading-performance#sJw0KSc"><em>Web Font Reflow Count</em></a> after first render. Obviously, the lower both metrics are, the better the performance is.</p>

<p>What about <strong>variable fonts</strong>, you might ask? It’s important to notice that <a href="https://alistapart.com/blog/post/variable-fonts-for-responsive-design">variable</a> <a href="https://www.smashingmagazine.com/2017/09/new-font-technologies-improve-web/">fonts</a> might require a <a href="https://youtu.be/FbguhX3n3Uc?t=2161">significant performance consideration</a>. They give us a much broader design space for typographic choices, but it comes at the cost of a single serial request opposed to a number of individual file requests.</p>

<p>While variable fonts <a href="https://uxdesign.cc/the-performance-benefits-of-variable-fonts-79af8c4ff56c">drastically reduce the overall combined file size of font files</a>, that single request might be slow, blocking the rendering of <em>all</em> content on a page. So subsetting and splitting the font into character sets still matter. On the good side though, with a variable font in place, we’ll get exactly one reflow by default, so no JavaScript will be required to group repaints.</p>

<p>Now, what would make a <strong>bulletproof web font loading strategy</strong> then? Subset fonts and prepare them for the 2-stage-render, declare them with a <code>font-display</code> descriptor, use Font Loading API to group repaints and store fonts in a persistent service worker’s cache. On the first visit, inject the preloading of scripts just before the blocking external scripts. You could fall back to Bram Stein’s <a href="https://github.com/bramstein/fontfaceobserver">Font Face Observer</a> if necessary. And if you’re interested in measuring the performance of font loading, Andreas Marschke explores <a href="https://www.andreas-marschke.name/posts/2017/12/29/Fonts-API-UserTiming-Boomerang.html">performance tracking with Font API and UserTiming API</a>.</p>

<p>Finally, don’t forget to include <a href="https://www.nccgroup.trust/uk/about-us/newsroom-and-events/blogs/2015/august/how-to-subset-fonts-with-unicode-range/"><code>unicode-range</code></a> to break down a large font into smaller language-specific fonts, and use Monica Dinculescu’s <a href="https://meowni.ca/font-style-matcher/">font-style-matcher</a> to minimize a jarring shift in layout, due to sizing discrepancies between the fallback and the web fonts.</p>

<p>Alternatively, to emulate a web font for a fallback font, we can use <a href="https://docs.google.com/document/d/1PW-5ML5hOZw7GczOargelPo6_8Zkuk2DXtgfOtJ59Eo/edit">@font-face descriptors to override font metrics</a> (<a href="https://jsfiddle.net/wpnjav2k/">demo</a>, enabled in Chrome 87). (Note that adjustments are complicated with complicated font stacks though.)</p>

<p>Does the future look bright? With <a href="https://rwt.io/typography-tips/progressive-font-enrichment-reinventing-web-font-performance">progressive font enrichment</a>, eventually we might be able to "download only the required part of the font on any given page, and for subsequent requests for that font to dynamically ‘patch’ the original download with additional sets of glyphs as required on successive page views", as Jason Pamental explains it. <a href="https://fonts.gstatic.com/experimental/incxfer_demo">Incremental Transfer Demo</a> is already available, and it’s <a href="https://www.w3.org/Fonts/WG/webfonts-2018.html#normative">work in progress</a>.</p>

</li>
</ol>

{{% feature-panel %}}

## Build Optimizations

<ol class="continue">
<li><strong>Have we defined our priorities?</strong><br />It’s a good idea to know what you are dealing with first. Run an <strong>inventory</strong> of all of your assets (JavaScript, images, fonts, third-party scripts and "expensive" modules on the page, such as carousels, complex infographics and multimedia content), and break them down in groups.

<p><strong>Set up a spreadsheet</strong>. Define the basic <em>core</em> experience for legacy browsers (i.e. fully accessible core content), the <em>enhanced</em> experience for capable browsers (i.e. an enriched, full experience) and the <em>extras</em> (assets that aren’t absolutely required and can be lazy-loaded, such as web fonts, unnecessary styles, carousel scripts, video players, social media widgets, large images). Years ago, we published an article on "<a href="https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/">Improving Smashing Magazine’s Performance</a>," which describes this approach in detail.</p>

<p>When optimizing for performance we need to reflect our priorities. Load the <em>core experience</em> immediately, then <em>enhancements</em>, and then the <em>extras</em>.</p></li>

<li><strong>Do you use native JavaScript modules in production?</strong><br />Remember the good ol' <a href="https://www.filamentgroup.com/lab/modernizing-delivery.html">cutting-the-mustard technique</a> to send the core experience to legacy browsers and an enhanced experience to modern browsers? An <a href="https://snugug.com/musings/modern-cutting-the-mustard/">updated variant of the technique</a> could use ES2017+ <code>&lt;script type="module"&gt;</code>, also known as <a href="https://philipwalton.com/articles/using-native-javascript-modules-in-production-today/">module/nomodule pattern</a> (also introduced by Jeremy Wagner as <a href="https://calendar.perfplanet.com/2018/doing-differential-serving-in-2019/"><em>differential serving</em></a>).</p>

<p>The idea is to compile and serve <strong>two separate JavaScript bundles</strong>: the “regular” build, the one with Babel-transforms and polyfills and serve them only to legacy browsers that actually need them, and another bundle (same functionality) that has no transforms or polyfills.</p>

<p>As a result, we help reduce blocking of the main thread by reducing the amount of scripts the browser needs to process. Jeremy Wagner has published a <a href="https://calendar.perfplanet.com/2018/doing-differential-serving-in-2019/">comprehensive article on differential serving</a> and how to set it up in your build pipeline, from setting up Babel, to what tweaks you’ll need to make in Webpack, as well as the benefits of doing all this work.</p>

<p>Native JavaScript module scripts are <a href="https://v8.dev/features/modules#defer">deferred by default</a>, so while HTML parsing is happening, the browser <a href="https://twitter.com/addyosmani/status/1233346105842122754">will download the main module</a>.</p>

{{< rimg breakout="true" href="https://v8.dev/features/modules" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc4a5548-f5a3-41ea-b881-39f9a366261b/js-modules-deferred-default.jpg" sizes="100vw" caption="Native JavaScript modules are deferred by default. Pretty much <a href='https://v8.dev/features/modules'>everything about native JavaScript modules</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc4a5548-f5a3-41ea-b881-39f9a366261b/js-modules-deferred-default.jpg'>Large preview</a>)" alt="An example showing how native JavaScript modules are deferred by default" >}}

<p>One note of warning though: the <em>module/nomodule pattern</em> <a href="https://gist.github.com/jakub-g/5fc11af85a061ca29cc84892f1059fec">can backfire on some clients</a>, so you might want to consider a workaround: Jeremy’s <a href="https://jeremy.codes/blog/a-less-risky-differential-serving-pattern/">less risky differential serving pattern</a> which, however, sidesteps the preload scanner, which could affect performance in ways one might not anticipate. (<em>thanks, Jeremy!</em>)</p>

<p>In fact, <a href="https://rollupjs.org/">Rollup</a> <a href="https://rollupjs.org/guide/en/#outputformat">supports modules as an output format</a>, so we can both bundle code and deploy modules in production. Parcel has <a href="https://github.com/parcel-bundler/parcel/pull/3545">module support in Parcel 2</a>. For Webpack, <a href="https://github.com/JoviDeCroock/webpack-module-nomodule-plugin">module-nomodule-plugin</a> automates the generation of module/nomodule scripts.</p>

<p><strong>Note</strong>: It’s worth stating that feature detection alone isn’t enough to make an informed decision about the payload to ship to that browser. On its own, we can’t deduce device capability from browser version. For example, cheap Android phones in developing countries mostly run Chrome and will cut the mustard despite their limited memory and CPU capabilities.</p>

<p>Eventually, using the <a href="https://github.com/w3c/device-memory">Device Memory Client Hints Header</a>, we’ll be able to target low-end devices more reliably. At the moment of writing, the header is supported only in Blink (it goes for <a href="https://caniuse.com/#search=client%20hints">client hints</a> in general). Since Device Memory also has a JavaScript API which is <a href="https://developers.google.com/web/updates/2017/12/device-memory">available in Chrome</a>, one option could be to feature detect based on the API, and fall back to <em>module/nomodule pattern</em> if it’s not supported (<em>thanks, Yoav!</em>).</p></li>

<li><strong>Are you using tree-shaking, scope hoisting and code-splitting?</strong><br /><a href="https://developers.google.com/web/fundamentals/performance/optimizing-javascript/tree-shaking/">Tree-shaking</a> is a way to clean up your build process by only including code that is actually used in production and eliminate unused imports <a href="https://www.2ality.com/2015/12/webpack-tree-shaking.html">in Webpack</a>. With Webpack and Rollup, we also have <a href="https://medium.com/webpack/brief-introduction-to-scope-hoisting-in-webpack-8435084c171f">scope hoisting</a> that allows both tools to detect where <code>import</code> chaining can be flattened and converted into one inlined function without compromising the code. With Webpack, we can also use <a href="https://react-etc.net/entry/json-tree-shaking-lands-in-webpack-4-0">JSON Tree Shaking</a> as well.
<p><a href="https://webpack.js.org/guides/code-splitting/">Code-splitting</a> is another Webpack feature that splits your codebase into "chunks" that are loaded on demand. Not all of the JavaScript has to be downloaded, parsed and compiled right away. Once you define split points in your code, Webpack can take care of the dependencies and outputted files. It enables you to keep the initial download small and to request code on demand when requested by the application. Alexander Kondrov has a <a href="https://hackernoon.com/lessons-learned-code-splitting-with-webpack-and-react-f012a989113">fantastic introduction to code-splitting with Webpack and React</a>.</p>

<p>Consider using <a href="https://github.com/GoogleChromeLabs/preload-webpack-plugin">preload-webpack-plugin</a> that takes routes you code-split and then prompts browser to preload them using <code>&lt;link rel="preload"&gt;</code> or <code>&lt;link rel="prefetch"&gt;</code>. <a href="https://webpack.js.org/guides/code-splitting/#prefetching-preloading-modules">Webpack inline directives</a> also give some control over <code>preload</code>/<code>prefetch</code>. (Watch out for <a href="https://andydavies.me/blog/2019/02/12/preloading-fonts-and-the-puzzle-of-priorities/">prioritization issues</a> though.)</p>

<p>Where to define split points? By tracking which chunks of CSS/JavaScript are used, and which aren’t used. Umar Hansa <a href="https://vimeo.com/235431630#t=11m37s">explains</a> how you can use Code Coverage from Devtools to achieve it.</p>

<!-- <p>If you aren’t using Webpack, note that <a href="https://rollupjs.org/">Rollup</a> shows significantly better results than good ol' Browserify exports. While we’re at it, you might want to check out <a href="https://github.com/ampproject/rollup-plugin-closure-compiler">rollup-plugin-closure-compiler</a> and <a href="https://github.com/nolanlawson/rollupify">Rollupify</a>, which converts ECMAScript 2015 modules into one big CommonJS module &mdash; because small modules can have a <a href="https://nolanlawson.com/2016/08/15/the-cost-of-small-modules/">surprisingly high performance cost</a> depending on your choice of bundler and module system.</p> -->

<p>When dealing with single-page applications, we need some time to initialize the app before we can render the page. Your setting will require your custom solution, but you could watch out for modules and techniques to speed up the initial rendering time. For example, <a href="https://building.calibreapp.com/debugging-react-performance-with-react-16-and-chrome-devtools-c90698a522ad">here’s how to debug React performance</a> and <a href="https://blog.logrocket.com/death-by-a-thousand-cuts-a-checklist-for-eliminating-common-react-performance-issues/">eliminate common React performance issues</a>, and <a href="https://www.youtube.com/watch?v=p9vT0W31ym8">here’s how to improve performance in Angular</a>. In general, most performance issues come from the initial time to bootstrap the app.</p>

<p>So, what’s the best way to code-split aggressively, but not too aggressively? According to Phil Walton, "in addition to code-splitting via dynamic imports, [we could] also use <strong>code-splitting at the package level</strong>, where each imported node modules get put into a chunk based on its package’s name." Phil  provides a <a href="https://philipwalton.com/articles/using-native-javascript-modules-in-production-today/">tutorial on how to build it</a> as well.</p>

</li>
<li><strong>Can we improve Webpack's output?</strong><br />As Webpack is often considered to be mysterious, there are plenty of Webpack plugins that may come in handy to further reduce Webpack's output. Below are some of the more obscure ones that might need a bit more attention.

<p>One of the interesting ones comes from <a href="https://twitter.com/iamakulov/status/1275807323299160066">Ivan Akulov's thread</a>. Imagine that you have a function that you call once, store its result in a variable, and then don’t use that variable. Tree-shaking will remove the variable, but <em>not</em> the function, because it might be used otherwise. However, if the function isn't used anywhere, you might want to remove it. To do so, prepend the function call with <code>/*#__PURE__*/</code> which is supported by Uglify and Terser &mdash; done!</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b371aa9f-e712-4710-90f1-70a4aae0915d/function-result-pure.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b371aa9f-e712-4710-90f1-70a4aae0915d/function-result-pure.jpg" sizes="100vw" caption="To remove such a function when its result is not used, prepend the function call with <code>&#47;&#42;&#35;&#95;&#95;PURE&#95;&#95;&#42;&#47;</code>. Via <a href='https://twitter.com/iamakulov/status/1275807326184882181'>Ivan Akulov</a>.(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b371aa9f-e712-4710-90f1-70a4aae0915d/function-result-pure.jpg'>Large preview</a>)" alt="A screenshot of JS code in an editor showing how the PURE function can be used" >}}

<p>Here are some of the other tools that Ivan recommends:</p>

<ul>
<li><a href="https://www.npmjs.com/package/purgecss-webpack-plugin">purgecss-webpack-plugin</a> removes unused classes, especially when you are using Bootstrap or Tailwind.</li>
<li>Enable <code>optimization.splitChunks: 'all'</code> with <a href="https://webpack.js.org/plugins/split-chunks-plugin/">split-chunks-plugin</a>. This would make webpack automatically code-split your entry bundles for better caching.</li>
<li><a href="https://t.co/5CKuYv1mF0?amp=1">Set <code>optimization.runtimeChunk: true</code></a>. This would move webpack’s runtime into a separate chunk &mdash; and would also improve caching.</li>
<li><a href="https://www.npmjs.com/package/google-fonts-webpack-plugin">google-fonts-webpack-plugin</a> downloads font files, so you can serve them from your server.</li>
<li><a href="https://www.npmjs.com/package/workbox-webpack-plugin">workbox-webpack-plugin</a> allows you to generate a service worker with a precaching setup for all of your webpack assets. Also, check <a href="https://developers.google.com/web/tools/workbox/modules">Service Worker Packages</a>, a comprehensive guide of modules that could be applied right away. Or use <a href="https://www.npmjs.com/package/preload-webpack-plugin">preload-webpack-plugin</a> to generate <code>preload</code>/<code>prefetch</code> for all JavaScript chunks.</li>
<li><a href="https://www.npmjs.com/package/speed-measure-webpack-plugin">speed-measure-webpack-plugin</a> measures your webpack build speed, providing insights into which steps of the build process are most time-consuming.</li>
<li><a href="https://www.npmjs.com/package/duplicate-package-checker-webpack-plugin">duplicate-package-checker-webpack-plugin</a> warns when your bundle contains multiple versions of the same package.</li>
<li><a href="https://medium.freecodecamp.org/reducing-css-bundle-size-70-by-cutting-the-class-names-and-using-scope-isolation-625440de600b">Use scope isolation and shorten CSS class names dynamically</a> at the compilation time.</li>
</ul>
</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c469462-2e01-4511-8b77-0d5a59597635/responsive-loader-code-example.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c469462-2e01-4511-8b77-0d5a59597635/responsive-loader-code-example.jpg" sizes="100vw" caption="Speed up your images is to serve smaller pictures on smaller screens. With <a href='https://github.com/dazuaz/responsive-loader'>responsive-loader</a>. Via <a href='https://twitter.com/iamakulov/status/1275779010597924864'>Ivan Akulov</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c469462-2e01-4511-8b77-0d5a59597635/responsive-loader-code-example.jpg'>Large preview</a>)" alt="A screenshot of a terminal showing how the webpack loader named responsive-loader can be used to help you generate responsive images out of the box" >}}
<ol class="continue">
<li><strong>Can you offload JavaScript into a Web Worker?</strong><br />To reduce the negative impact to Time-to-Interactive, it might be a good idea to look into offloading heavy JavaScript into a <a href="https://web.dev/off-main-thread/">Web Worker</a>.

<p>As the code base keeps growing, the UI performance bottlenecks will show up, slowing down the user’s experience. That’s <a href="https://medium.com/google-developer-experts/running-fetch-in-a-web-worker-700dc33ac854">because DOM operations are running alongside your JavaScript</a> on the main thread. With <a href="https://flaviocopes.com/web-workers/">web workers</a>, we can move these expensive operations to a background process that’s running on a different thread. Typical use cases for web workers are <a href="https://blog.sessionstack.com/how-javascript-works-the-building-blocks-of-web-workers-5-cases-when-you-should-use-them-a547c0757f6a">prefetching data and Progressive Web Apps</a> to load and store some data in advance so that you can use it later when needed. And you could use <a href="https://github.com/GoogleChromeLabs/comlink">Comlink</a> to streamline the communication between the main page and the worker. Still some work to do, but we are getting there.</p>

<p>There are a few <a href="https://docs.google.com/document/d/1nu0EcVNC3jtmUVWL8Gs5eCj2p_984kamNhG2nS9gOC0/edit">interesting case studies around web workers</a> which show different approaches of moving framework and app logic to web workers. The conclusion: in general, there are still some challenges, but there are some good use cases already (<em>thanks, Ivan Akulov!</em>).</p>

<p>Starting from Chrome 80, a <strong>new mode for web workers</strong> with performance benefits of JavaScript modules has been shipped, called <a href="https://web.dev/module-workers/#enter-module-workers">module workers</a>. We can change script loading and execution to match <code>script type="module"</code>, plus we can also use dynamic imports for lazy-loading code without blocking execution of the worker.</p>

<p>How to get started? Here are a few resources that are worth looking into:</p>
<ul>
<li>Surma has published an <a href="https://web.dev/off-main-thread/">excellent guide on how to run JavaScript off the browser’s main thread</a> and also <a href="https://surma.dev/things/when-workers/">When should you be using Web Workers?</a></li>
<li>Also, check Surma's talk about <a href="https://www.youtube.com/watch?v=7Rrv9qFMWNM&feature=emb_title">off the main thread architecture</a>.</li>
<li><a href="https://www.youtube.com/watch?v=mDdgfyRB5kg&feature=youtu.be">A Quest to Guarantee Responsiveness</a> by Shubhie Panicker and Jason Miller provide a detailed insight into how to use web workers, and when to avoid them.</li>
<li><a href="https://www.youtube.com/watch?v=4CWzB5Mi3Ik&list=PLSmH2HL6l9pwQmSgpKFtWiISOXua3zq8I&index=17">Getting Out of Users' Way: Less Jank With Web Workers</a> highlights useful patterns for working with Web Workers, effective ways to communicate between workers, handle complex data processing off the main thread, and test and debug them.</li>
<li><a href="https://github.com/developit/workerize">Workerize</a> allows you to move a module into a Web Worker, automatically reflecting exported functions as asynchronous proxies.</li>
<li>If you’re using Webpack, you could use <a href="https://github.com/developit/workerize-loader">workerize-loader</a>. Alternatively, you could use <a href="https://github.com/GoogleChromeLabs/worker-plugin">worker-plugin</a> as well.</li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a59924a-f042-4081-a7db-2e134975c647/why-web-workers-example.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a59924a-f042-4081-a7db-2e134975c647/why-web-workers-example.jpg" sizes="100vw" caption="Use web workers when code blocks for a long time, but avoid them when you rely on the DOM, handle input response and need minimal delay. (via <a href='https://twitter.com/addyosmani/status/1234017029730045952/photo/1'>Addy Osmani</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a59924a-f042-4081-a7db-2e134975c647/why-web-workers-example.jpg'>Large preview</a>)" alt="Code in DOM shown on the left as an example of what to use and avoid when using web workers" >}}

<p>Note that Web Workers don’t have access to the DOM because the DOM is not "thread-safe", and the code that they execute needs to be contained in a separate file.</p></li>

<li><strong>Can you offload "hot paths" to WebAssembly?</strong><br />We could <a href="https://developers.google.com/web/updates/2019/02/hotpath-with-wasm">offload computationally heavy tasks</a> off to <a href="https://webassembly.org/">WebAssembly</a> (<em>WASM</em>), a binary instruction format, designed as a portable target for compilation of high-level languages like C/C++/Rust. Its <a href="https://caniuse.com/#feat=wasm">browser support is remarkable</a>, and it has recently become viable as <a href="https://hacks.mozilla.org/2018/10/calls-between-javascript-and-webassembly-are-finally-fast-%F0%9F%8E%89/">function calls between JavaScript and WASM are getting faster</a>. Plus, it’s <a href="https://www.fastly.com/blog/announcing-lucet-fastly-native-webassembly-compiler-runtime">even supported on Fastly’s edge cloud</a>.</p>

<p>Of course, WebAssembly isn’t supposed to replace JavaScript, but it can complement it in cases when you notice CPU hogs. For most web apps, JavaScript is a better fit, and WebAssembly is best used for <strong>computationally intensive web apps</strong>, such as games.</p>

<p>If you’d like to learn more about WebAssembly:</p>

<ul>
<li>Lin Clark has written a <a href="https://hacks.mozilla.org/2017/02/a-cartoon-intro-to-webassembly/">thorough series to WebAssembly</a> and Milica Mihajlija provides a <a href="https://blog.logrocket.com/webassembly-how-and-why-559b7f96cd71">general overview</a> of how to run native code in the browser, why you might want to do that, and what it all means for JavaScript and the future of web development.</li>
<li><a href="https://www.smashingmagazine.com/2019/04/webassembly-speed-web-app/">How We Used WebAssembly To Speed Up Our Web App By 20X (Case Study)</a> highlights a case study of how slow JavaScript calculations were replaced with compiled WebAssembly and brought significant performance improvements.</li>
<li>Patrick Hamann has been speaking about <a href="https://www.youtube.com/watch?v=Z6ZhIA8i_8g">the growing role of WebAssembly</a>, and he’s debunking some myths about WebAssembly, explores its challenges and we can use it practically in applications today.</li>
<li>Google Codelabs provides an <a href="https://codelabs.developers.google.com/codelabs/web-assembly-intro/index.html">Introduction to WebAssembly</a>, a 60 min course in which you’ll learn how to take native code—in C and compile it to WebAssembly, and then call it directly from JavaScript.</li>
<li>Alex Danilo has <a href="https://www.youtube.com/watch?v=6v4E6oksar0">explained WebAssembly and how it works</a> at his Google I/O talk. Also, Benedek Gagyi <a href="https://www.youtube.com/watch?v=l2DHjRmgAF8">shared a practical case study on WebAssembly</a>, specifically how the team uses it as output format for their C++ codebase to iOS, Android and the website.</li>
</ul>

<p><strong>Still not sure</strong> about when to use Web Workers, Web Assembly, streams, or perhaps WebGL JavaScript API to access the GPU? <a href="https://hyphaebeast.club/writing/accelerating-js/">Accelerating JavaScript</a> is a short but helpful guide that explains when to use what, and why &mdash; also with a handy flowchart and plenty of useful resources.</p>

</li>
</ol>

{{< rimg breakout="true" href="https://blog.logrocket.com/webassembly-how-and-why-559b7f96cd71" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbb2ea83-7674-47d8-9cad-89a2de009915/how-webassembly-works.png" sizes="100vw" caption="Milica Mihajlija provides a general overview of <a href='https://blog.logrocket.com/webassembly-how-and-why-559b7f96cd71'>how WebAssembly works and why it’s useful</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbb2ea83-7674-47d8-9cad-89a2de009915/how-webassembly-works.png'>Large preview</a>)" alt="An illustration of C++, C or Rust shown on the left with an arrow showing to a browser that includes WASM binaries adding to the JavaScript, CSS and HTML" >}}

<ol class="continue">
<!-- <li><strong>Are you using an ahead-of-time compiler?</strong><br />Make sure to use an <a href="https://www.lucidchart.com/techblog/2016/09/26/improving-angular-2-load-times/">ahead-of-time compiler</a> to <a href="https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/">offload some of the client-side rendering</a> to the <a href="https://redux.js.org/docs/recipes/ServerRendering.html">server</a> and, hence, output usable results quickly. Finally, consider using <a href="https://github.com/nolanlawson/optimize-js">Optimize.js</a> for faster initial loading by wrapping eagerly invoked functions (it <a href="https://twitter.com/tverwaes/status/809788255243739136">might not be necessary</a> any longer, though).</li> -->

<li><strong>Do we serve legacy code only to legacy browsers?</strong><br />With ES2017 being <a href="https://web.dev/publish-modern-javascript/">remarkably well supported in modern browsers</a>, we can <a href="https://github.com/prateekbh/babel-esm-plugin">use <code>babelEsmPlugin</code></a> to only transpile ES2017+ features unsupported by the modern browsers you are targeting.

<p>Houssein Djirdeh and Jason Miller have recently published a <a href="https://web.dev/publish-modern-javascript/">comprehensive guide on how to transpile and serve modern and legacy JavaScript</a>, going into details of making it work with Webpack and Rollup, and the tooling needed. You can also <a href="https://estimator.dev/">estimate how much JavaScript you can shave off</a> on your site or app bundles.</p>

<p>JavaScript modules are <a href="https://caniuse.com/#feat=es6-module">supported in all major browsers</a>, so use <a href="https://developers.google.com/web/fundamentals/primers/modules">use <code>script type="module"</code></a> to let browsers with ES module support load the file, while older browsers could load legacy builds with <code>script nomodule</code>.</p>

<p>These days we can write module-based JavaScript that runs natively in the browser, without transpilers or bundlers. <a href="https://developers.google.com/web/updates/2017/12/modulepreload"><code>&lt;link rel="modulepreload"&gt;</code> header</a> provides a way to initiate early (and high-priority) loading of module scripts. Basically, it’s a nifty way to help in maximizing bandwidth usage, by telling the browser about what it needs to fetch so that it’s not stuck with anything to do during those long roundtrips. Also, Jake Archibald has published a detailed article with <a href="https://jakearchibald.com/2017/es-modules-in-browsers/">gotchas and things to keep in mind with ES Modules</a> that’s worth reading.</p>

<!-- <p>For lodash, <a href="https://github.com/lodash/babel-plugin-lodash">use <code>babel-plugin-lodash</code></a> that will load only modules that you are using in your source. Your dependencies might also depend on other versions of Lodash, so <a href="https://www.contentful.com/blog/2017/10/27/put-your-webpack-bundle-on-a-diet-part-3/">transform generic lodash <code>requires</code> to cherry-picked ones</a> to avoid code duplication. This might save you quite a bit of JavaScript payload.</p> -->

<!-- <p>Shubham Kanodia has written a <a href="https://www.smashingmagazine.com/2018/10/smart-bundling-legacy-code-browsers/">detailed low-maintenance guide on smart bundling</a>: to shipping legacy code to only legacy browsers in production with the code snippet you could use right away.</p> -->
</li>
</ol>

{{< rimg breakout="true" href="https://jakearchibald.com/2017/es-modules-in-browsers/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d46ddc8b-4bd7-4627-b738-baf62807b26f/inline-scripts-deferred.png" sizes="100vw" caption="Jake Archibald has published a detailed article with <a href='https://jakearchibald.com/2017/es-modules-in-browsers/'>gotchas and things to keep in mind with ES Modules</a>, e.g. inline scripts are deferred until blocking external scripts and inline scripts are executed. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d46ddc8b-4bd7-4627-b738-baf62807b26f/inline-scripts-deferred.png'>Large preview</a>)" alt="Inline scripts are deferred until blocking external scripts and inline scripts are executed" >}}

<ol class="continue">
<li><strong>Identify and rewrite legacy code with incremental decoupling</strong>.<br />Long-living projects have a tendency to gather dust and dated code. Revisit your dependencies and assess how much time would be required to refactor or rewrite legacy code that has been causing trouble lately. Of course, it’s always a big undertaking, but once you know the impact of the legacy code, you could start with <a href="https://githubengineering.com/removing-jquery-from-github-frontend/">incremental decoupling</a>.

<p>First, set up metrics that tracks if the ratio of legacy code calls is staying constant or going down, not up. Publicly discourage the team from using the library and make sure that your CI <a href="https://github.com/dgraham/eslint-plugin-jquery">alerts</a> developers if it’s used in pull requests. <a href="https://githubengineering.com/removing-jquery-from-github-frontend/#polyfills">polyfills</a> could help transition from legacy code to rewritten codebase that uses standard browser features.</p></li>

<li><strong>Identify and remove unused CSS/JS</strong>.<br /><a href="https://developers.google.com/web/updates/2017/04/devtools-release-notes#coverage">CSS and JavaScript code coverage</a> in Chrome allows you to learn which code has been executed/applied and which hasn't. You can start recording the coverage, perform actions on a page, and then explore the code coverage results. Once you’ve detected unused code, <a href="https://twitter.com/TheLarkInn/status/1012429019063578624">find those modules and lazy load with <code>import()</code></a> (see the entire thread). Then repeat the coverage profile and validate that it’s now shipping less code on initial load.</p>

<p>You can use <a href="https://github.com/GoogleChrome/puppeteer">Puppeteer</a> to <a href="https://twitter.com/matijagrcic/statuses/1060863620568043520">programmatically collect code coverage</a>. Chrome allows you to <a href="https://twitter.com/tkadlec/status/1073330247758684163">export code coverage results</a>, too. As Andy Davies noted, you might want to collect code coverage for <a href="https://twitter.com/AndyDavies/status/1073339071106297856">both modern and legacy browsers</a> though.</p>

<p>There are many other use-cases and tools for Puppetter that might need a bit more exposure:</p>

<ul>
<li><a href="https://github.com/GoogleChromeLabs/puppeteer-examples">Use-cases for Puppeteer</a>, such as, for example, <a href="https://meowni.ca/posts/2017-puppeteer-tests/">automatic visual diffing</a> or <a href="https://blog.cowchimp.com/monitoring-unused-css-by-unleashing-the-devtools-protocol/">monitoring unused CSS with every build</a>,</li>
<li><a href="https://addyosmani.com/blog/puppeteer-recipes/">Web performance recipes with Puppeteer</a>,</li>
<li><a href="https://twitter.com/addyosmani/status/1219884904307142659">Useful tooling for recording and generating Pupeeteer and Playwright scripts</a>,
<li>Plus, you can even <a href="https://twitter.com/umaar/status/1331924138970255360">record tests right in DevTools</a>,</li>
<li><a href="https://nitayneeman.com/posts/getting-to-know-puppeteer-using-practical-examples/">Comprehensive overview of Puppeteer</a> by Nitay Neeman, with examples and use cases.</li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76f10c0c-84cd-4658-876d-9bea1a0c160f/puppeteer-recorder-sandbox-opt.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76f10c0c-84cd-4658-876d-9bea1a0c160f/puppeteer-recorder-sandbox-opt.jpg" sizes="100vw" caption="We can use <a href='https://chrome.google.com/webstore/detail/headless-recorder/djeegiggegleadkkbgopoonhjimgehda?hl=en'>Puppeteer Recorder</a> and <a href='https://puppeteersandbox.com/'>Puppeteer Sandbox</a> to record browser interaction and generate Puppeteer and Playwright scripts. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76f10c0c-84cd-4658-876d-9bea1a0c160f/puppeteer-recorder-sandbox-opt.jpg'>Large preview</a>)" alt="A Screenshot of the Pupeteer Recorder on the left, and a screenshot Puppeteer Sandbox shown on the right" >}}

<p>Furthermore, <a href="https://github.com/FullHuman/purgecss">purgecss</a>, <a href="https://github.com/giakki/uncss">UnCSS</a> and <a href="https://github.com/geuis/helium-css">Helium</a> can help you remove unused styles from CSS. And if you aren’t certain if a suspicious piece of code is used somewhere, you can follow <a href="https://csswizardry.com/2018/01/finding-dead-css/">Harry Roberts' advice</a>: create a 1&times;1px transparent GIF for a particular class and drop it into a <code>dead/</code> directory, e.g. <code>/assets/img/dead/comments.gif</code>.</p>

<p>After that, you set that specific image as a background on the corresponding selector in your CSS, sit back and wait for a few months if the file is going to appear in your logs. If there are no entries, nobody had that legacy component rendered on their screen: you can probably go ahead and delete it all.</p>

<p>For the <em>I-feel-adventurous</em>-department, you could even automate gathering on unused CSS through a set of pages by <a href="https://blog.cowchimp.com/monitoring-unused-css-by-unleashing-the-devtools-protocol/">monitoring DevTools using DevTools</a>.</p></li>
</ol>

{{< rimg breakout="true" href="https://cdn-images-1.medium.com/max/2000/1*fdX-6h2HnZ_Mo4fBHflh2w.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e30c7d5b-ef8b-46ba-b0fc-b1d5a31cefff/webpack-comparison.png" sizes="100vw" caption="In <a href='https://www.contentful.com/blog/2017/10/27/put-your-webpack-bundle-on-a-diet-part-3/'>his article</a>, Benedikt Rötsch’s showed that a switch from Moment.js to date-fns could shave around 300ms for First paint on 3G and a low-end mobile phone. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e30c7d5b-ef8b-46ba-b0fc-b1d5a31cefff/webpack-comparison.png'>Large preview</a>)" alt="Webpack comparison table" >}}

<ol class="continue">
<li><strong>Trim the size of your JavaScript bundles.</strong><br />As Addy Osmani <a href="https://medium.com/@addyosmani/the-cost-of-javascript-in-2018-7d8950fbb5d4">noted</a>, there’s a high chance you’re shipping full JavaScript libraries when you only need a fraction, along with dated polyfills for browsers that don’t need them, or just duplicate code. To avoid the overhead, consider using <a href="https://github.com/GoogleChromeLabs/webpack-libs-optimizations">webpack-libs-optimizations</a> that removes unused methods and polyfills during the build process.

<p>Check and review the <strong>polyfills</strong> that you are sending to legacy browsers and to modern browsers, and be more strategic about them. Take a look at <a href="https://polyfill.io/v3/">polyfill.io</a> which is a service that accepts a request for a set of browser features and returns only the polyfills that are needed by the requesting browser.</p>

<p>Add <strong>bundle auditing</strong> into your regular workflow as well. There might be some lightweight alternatives to heavy libraries you’ve added years ago, e.g. Moment.js (now <a href="https://momentjs.com/docs/#/-project-status/">discontinued</a>) could be replaced with:</p>
<ul>
<li><a href="https://blog.logrocket.com/4-alternatives-to-moment-js-for-internationalizing-dates/">Native Internationalization API</a>,</li>
<li><a href="https://github.com/iamkun/dayjs">Day.js</a> with a familiar Moment.js API and patterns,</li>
<li><a href="https://github.com/date-fns/date-fns">date-fns</a> or</li>
<li><a href="https://moment.github.io/luxon/">Luxon</a>.</li>
<li>You can also use <a href="https://www.skypack.dev/">Skypack Discover</a> that combines human-reviewed package recommendations with a quality-focused search.</li>
</ul>

<p>Benedikt Rötsch’s research <a href="https://www.contentful.com/blog/2017/10/27/put-your-webpack-bundle-on-a-diet-part-3/">showed</a> that a switch from Moment.js to date-fns could shave around 300ms for First paint on 3G and a low-end mobile phone.</p>

<p>For bundle auditing, <a href="https://bundlephobia.com/">Bundlephobia</a> could help find the cost of adding a npm package to your bundle. <a href="https://github.com/ai/size-limit">size-limit</a> extends basic bundle size check with details on JavaScript execution time. You can even <a href="https://github.com/AymenLoukil/Google-lighthouse-custom-audit">integrate these costs with a Lighthouse Custom Audit</a>. This goes for frameworks, too. By removing or trimming the <a href="https://speakerdeck.com/addyosmani/web-performance-made-easy?slide=22">Vue MDC Adapter</a> (Material Components for Vue), styles drop from 194KB to 10KB.</p>

<p>There are many further tools to help you make an informed decision about the impact of your dependencies and viable alternatives:</p>

<ul>
<li><a href="https://www.npmjs.com/package/webpack-bundle-analyzer">webpack-bundle-analyzer</a></li>
<li><a href="https://github.com/danvk/source-map-explorer">Source Map Explorer</a></li>
<li><a href="https://github.com/samccone/bundle-buddy">Bundle Buddy</a></li>
<li><a href="https://bundlephobia.com/">Bundlephobia</a></li>
<li><a href="https://webpack.github.io/analyse/">Webpack analyze</a> shows why a specific module is included into the bundle.</li>
<li><a href="https://www.npmjs.com/package/bundle-wizard">bundle-wizard</a> also builds a map of dependencies for the whole page.</li>
<li><a href="https://github.com/GoogleChromeLabs/size-plugin">Webpack size-plugin</a></li>
<li><a href="https://marketplace.visualstudio.com/items?itemName=wix.vscode-import-cost">Import Cost for Visual Code</a></li>
</ul>

<p>Alternatively to shipping the entire framework, you could trim your framework and compile it into a <strong>raw JavaScript bundle</strong> that does not require additional code. <a href="https://svelte.technology/">Svelte does it</a>, and so does <a href="https://github.com/sokra/rawact">Rawact Babel plugin</a> which transpiles React.js components to native DOM operations at build-time. Why? Well, as maintainers explain, "react-dom includes code for every possible component/HTMLElement that can be rendered, including code for incremental rendering, scheduling, event handling, etc. But there are applications that do not need all these features (at initial page load). For such applications, it might make sense to use native DOM operations to build the interactive user interface."</p></li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f110101-2f0b-4da2-aaee-746209ee9d68/14-size-limit-front-end-performance-checklist-2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f110101-2f0b-4da2-aaee-746209ee9d68/14-size-limit-front-end-performance-checklist-2020.png" sizes="100vw" caption="<a href='https://github.com/ai/size-limit'>size-limit</a> provides basic bundle size check with details on JavaScript execution time as well. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f110101-2f0b-4da2-aaee-746209ee9d68/14-size-limit-front-end-performance-checklist-2020.png'>Large preview</a>)" alt="size-limit provides basic bundle size check with details on JavaScript execution time as well" >}}

<ol class="continue">
<li><strong>Do we use partial hydration?</strong><br />With the amount of JavaScript used in applications, we need to figure out ways to send as little as possible to the client. One way of doing so &mdash; and we briefly covered it already &mdash; is with <a href="https://medium.com/@luke_schmuke/how-we-achieved-the-best-web-performance-with-partial-hydration-20fab9c808d5">partial hydration</a>. The idea is quite simple: instead of doing SSR and then sending the entire app to the client, only small pieces of the app's JavaScript would be sent to the client and then hydrated. We can think of it as multiple tiny React apps with multiple render roots on an otherwise static website.

<p>In the article <a href="https://medium.com/@luke_schmuke/how-we-achieved-the-best-web-performance-with-partial-hydration-20fab9c808d5">"The case of partial hydration (with Next and Preact)"</a>, Lukas Bombach explains how the team behind Welt.de, one of the news outlets in Germany, has achieved better performance with partial hydration. You can also check <a href="https://github.com/LukasBombach/next-super-performance">next-super-performance GitHub repo</a> with explanations and code snippets.</p>

<p>You could also consider alternative options:</p>

<ul>
<li><a href="https://markus.oberlehner.net/blog/building-partially-hydrated-progressively-enhanced-static-websites-with-isomorphic-preact-and-eleventy/">partial hydration with Preact and Eleventy</a>,</li>
<li><a href="https://github.com/midudev/react-rendering-strategies">progressive hydration in React GitHub repo</a>,</li>
<li><a href="https://markus.oberlehner.net/blog/how-to-drastically-reduce-estimated-input-latency-and-time-to-interactive-of-ssr-vue-applications/">lazy-hydration in Vue.js</a> (<a href="https://github.com/maoberlehner/how-to-drastically-reduce-estimated-input-latency-and-time-to-interactive-of-ssr-vue-applications">GitHub repo</a>),</li>
<li><a href="https://calendar.perfplanet.com/2020/optimizing-performance-with-the-import-on-interaction-pattern/">Import on Interaction Pattern</a> to lazy-load non-critical resources (e.g components, embeds) when a user interacts with UI that needs it.</li>
</ul>

<p>Jason Miller has published working demos on how progressive hydration could be implemented with React, so you can use them right away: <a href="https://codesandbox.io/s/progressive-hydration-react-1-k65r2">demo 1</a>, <a href="https://codesandbox.io/s/progressive-hydration-react-2-2hprz">demo 2</a>, <a href="https://codesandbox.io/s/progressive-hydration-react-3-geyzs">demo 3</a> (also <a href="https://github.com/GoogleChromeLabs/progressive-rendering-frameworks-samples">available on GitHub</a>). Plus, you can look into the <a href="https://nicedoc.io/theKashey/react-prerendered-component">react-prerendered-component</a> library.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ae9f9db-97ee-41b9-824b-35d27edc6689/import-on-interation-addy-osmani.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ae9f9db-97ee-41b9-824b-35d27edc6689/import-on-interation-addy-osmani.png" sizes="100vw" caption="<a href='https://addyosmani.com/blog/import-on-interaction/'>Import-on-interaction</a> for first-party code should only be done if you’re unable to prefetch resources prior to interaction. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ae9f9db-97ee-41b9-824b-35d27edc6689/import-on-interation-addy-osmani.png'>Large preview</a>)" alt="+485KB of JavaScript upon loadshare() in Google Docs" >}}

</li>
<li><strong>Have we optimized the strategy for React/SPA?</strong><br />Struggling with performance in your single-page-application application? Jeremy Wagner has <a href="https://css-tricks.com/radeventlistener-a-tale-of-client-side-framework-performance/">explored the impact of client-side framework performance</a> on a variety of devices, highlighting some of the implications and guidelines we might want to be aware of when using one.

<p>As a result, here's a <a href="https://css-tricks.com/radeventlistener-a-tale-of-client-side-framework-performance/#conclusion">SPA strategy that Jeremy suggests</a> to use for React framework (but it shouldn't change significantly for other frameworks):</p>

<ul>
<li>Refactor stateful components as <strong>stateless components</strong> whenever possible.</li>
<li>Prerender stateless components when possible to minimize server response time. Render only on the server.</li>
<li>For stateful components with simple interactivity, consider prerendering or server-rendering that component, and replace its interactivity with <strong>framework-independent event listeners</strong>.</li>
<li>If you must hydrate stateful components on the client, use lazy hydration on visibility or interaction.</li>
<li>For lazily-hydrated components, schedule their hydration during main thread idle time with <code>requestIdleCallback</code>.</li>
</ul>

<p>There are a few other strategies you might want to pursue or review:</p>

<ul>
<li><a href="https://calendar.perfplanet.com/2019/the-unseen-performance-costs-of-css-in-js-in-react-apps/">Performance considerations for CSS-in-JS in React apps</li>
<li><a href="https://medium.com/ne-digital/how-to-reduce-next-js-bundle-size-68f7ac70c375">Reduce Next.js Bundle Size</a> by loading polyfills only when necessary, using dynamic imports and lazy hydration.</li>
<li><a href="https://levelup.gitconnected.com/secrets-of-javascript-a-tale-of-react-performance-optimization-and-multi-threading-9409332d349f">Secrets of JavaScript: A tale of React, Performance Optimization and Multi-threading</a>, a lengthy 7-part series on improving user interface challenges with React,</li>
<li><a href="https://www.debugbear.com/blog/measuring-react-app-performance">How to measure React performance</a> and <a href="https://building.calibreapp.com/debugging-react-performance-with-react-16-and-chrome-devtools-c90698a522ad">How to profile React applications</a>.</li>
<li><a href="https://www.youtube.com/watch?v=JDDxR1a15Yo&feature=youtu.be&t=10664">Building mobile-first web animations in React</a>, a fantastic talk by Alex Holachek, along with <a href="https://mobile-first-animation.netlify.app/">slides</a> and <a href="https://github.com/aholachek/mobile-first-animation">GitHub repo</a> (<em>thanks for the tip, Addy!</em>).</li>
<li><a href="https://github.com/GoogleChromeLabs/webpack-libs-optimizations">webpack-libs-optimizations</a> is a fantastic GitHub repo with plenty of useful Webpack-specific performance-related optimizations. Maintained by <a href="https://twitter.com/iamakulov">Ivan Akulov</a>.</li>
<li><a href="https://3perf.com/blog/notion/">React performance improvements in Notion</a>, a guide by Ivan Akulov on how to improve performance in React, with plenty of useful pointers to make the app around 30% faster.</li>
<li><a href="https://github.com/pmmmwh/react-refresh-webpack-plugin">React Refresh Webpack Plugin</a> (experimental) allows for hot reloading that preserves component state, and supports hooks and function components.</li>
<li>Watch out for <a href="https://reactjs.org/blog/2020/12/21/data-fetching-with-react-server-components.html">zero-bundle-size React Server Components</a>, a new proposed kind of components that will have no impact on bundle size. The project is currently in development, but any feedback from the community is much appreciated (<a href="https://twitter.com/sophiebits/status/1341098388062756867">great explainer by Sophie Alpert</a>).</li>
</ul>
</li>

<li><strong>Are you using predictive prefetching for JavaScript chunks?</strong><br />We could use heuristics to decide when to preload JavaScript chunks. <a href="https://github.com/guess-js/guess">Guess.js</a> is a set of tools and libraries that use Google Analytics data to determine which page a user is <strong>most likely to visit next</strong> from a given page. Based on user navigation patterns collected from Google Analytics or other sources, Guess.js builds a machine-learning model to predict and prefetch JavaScript that will be required on each subsequent page.

<p>Hence, every interactive element is receiving a probability score for engagement, and based on that score, a client-side script decides to prefetch a resource ahead of time. You can integrate the technique to your <a href="https://github.com/mgechev/guess-next">Next.js application</a>, <a href="https://blog.mgechev.com/2018/03/18/machine-learning-data-driven-bundling-webpack-javascript-markov-chain-angular-react/">Angular and React</a>, and there is a <a href="https://github.com/guess-js/guess/tree/master/packages/guess-webpack">Webpack plugin</a> which automates the setup process as well.</p>

<p>Obviously, you might be prompting the browser to consume unneeded data and prefetch undesirable pages, so it’s a good idea to be quite conservative in the number of prefetched requests. A good use case would be prefetching validation scripts required in the checkout, or speculative prefetch when a critical call-to-action comes into the viewport.</p>

<p>Need something less sophisticated? <a href="https://www.npmjs.com/package/dnstradamus">DNStradamus</a> does DNS prefetching for outbound links as they appear in the viewport. <a href="https://github.com/GoogleChromeLabs/quicklink">Quicklink</a>, <a href="https://instantclick.io/">InstantClick</a> and <a href="https://instant.page/">Instant.page</a> are small libraries that <strong>automatically prefetch links</strong> in the viewport during idle time in attempt to make next-page navigations load faster. Quicklink allows to prefetch React Router routes and Javascript; plus it’s data-considerate, so it doesn’t prefetch on 2G or if <code>Data-Saver</code> is on. So is Instant.page if the mode is set to use <em>viewport prefetching</em> (which is a default).</p>

<p>If you want to look into the science of predictive prefetching in full detail, Divya Tagtachian has a great talk on <a href="https://www.youtube.com/watch?v=UwjzFGCAuLw&list=PLSmH2HL6l9pwQmSgpKFtWiISOXua3zq8I&index=16">The Art of Predictive Prefetch</a>, covering all the options from start to finish.</p>
</li>

<li><strong>Take advantage of optimizations for your target JavaScript engine.</strong><br />Study what JavaScript engines dominate in your user base, then explore ways of optimizing for them. For example, when optimizing for V8 which is used in Blink-browsers, Node.js runtime and Electron, make use of <a href="https://blog.chromium.org/2015/03/new-javascript-techniques-for-rapid.html">script streaming</a> for monolithic scripts.

<p>Script streaming allows <code>async</code> or <code>defer scripts</code> to be parsed on a separate background thread once downloading begins, hence in some cases improving page loading times by up to 10%. Practically, <a href="https://medium.com/reloading/javascript-start-up-performance-69200f43b201#3498">use <code>&lt;script defer&gt;</code></a> in the <code>&lt;head&gt;</code>, so that the <a href="https://medium.com/reloading/javascript-start-up-performance-69200f43b201#3498">browsers can discover the resource</a> early and then parse it on the background thread.

<p><strong>Caveat</strong>: <em>Opera Mini <a href="https://caniuse.com/#search=defer">doesn’t support script deferment</a>, so if you are developing for India or Africa,</em> <code>defer</code> <em>will be ignored, resulting in blocking rendering until the script has been evaluated (thanks Jeremy!)</em>.</p>

<p>You could also hook into <a href="https://v8.dev/blog/code-caching-for-devs">V8’s code caching</a> as well, by splitting out libraries from code using them, or the other way around, merge libraries and their uses into a single script, group small files together and avoid inline scripts. Or perhaps even use <a href="https://www.npmjs.com/package/v8-compile-cache">v8-compile-cache</a>.</p>

<p>When it comes to JavaScript in general, there are also some practices that are worth keeping in mind:</p>

<ul>
<li><a href="https://github.com/ryanmcdermott/clean-code-javascript">Clean Code concepts for JavaScript</a>, a large collection of patterns for writing readable, reusable, and refactorable code.</li>
<li>You can <a href="https://wicg.github.io/compression/">Compress data from JavaScript with the CompressionStream API</a>, e.g. to gzip before uploading data (Chrome 80+).</li>
<li><a href="https://web.dev/detached-window-memory-leaks/">Detached window memory leaks</a> and <a href="https://nolanlawson.com/2020/02/19/fixing-memory-leaks-in-web-applications/">Fixing memory leaks in web apps</a> are detailed guides on how to find and fix tricky JavaScript memory leaks. Plus, you can use <a href="https://twitter.com/mathias/status/1231165158514405377">queryObjects(SomeConstructor)</a> from the DevTools Console (<em>thanks, Mathias!</em>).</li>
<li><a href="https://twitter.com/iamakulov/status/1331551351214645251">Reexports are bad for loading and runtime performance</a>, and avoiding them can help reduce the bundle size <a href="https://twitter.com/iamakulov/status/1331551364636413953">significantly</a>.</li>
<li>We can <a href="https://developers.google.com/web/updates/2016/06/passive-event-listeners">improve scroll performance with passive event listeners</a> by setting a flag in the <code>options</code> parameter. So browsers can scroll the page immediately, rather than after the listener has finished. (via Kayce Basques).</li>
<li>If you have any <code>scroll</code> or <code>touch*</code> listeners, pass <code>passive: true</code> to addEventListener. This tells the browser you’re not planning to call <code>event.preventDefault()</code> inside, so it can optimize the way it handles these events. (via <a href="https://twitter.com/iamakulov/status/1275858862801850370">Ivan Akulov</a>)</li>
<li>We can achieve <a href="https://web.dev/isinputpending/">better JavaScript scheduling with isInputPending()</a>, a new API that attempts to bridge the gap between loading and responsiveness with the concepts of interrupts for user inputs on the web, and allows for JavaScript to be able to check for input without yielding to the browser.</li>
<li>You can also <a href="https://twitter.com/umaar/status/1273607178826452992">automatically remove an event listener after it has executed</a>.</li>
<li>Firefox’s recently released <a href="https://twitter.com/mozhacks/status/1327280031106801664">Warp, a significant update to SpiderMonkey</a> (shipped in Firefox 83), <a href="https://hacks.mozilla.org/2019/08/the-baseline-interpreter-a-faster-js-interpreter-in-firefox-70/">Baseline Interpreter</a> and there are a few <a href="https://developer.mozilla.org/en-US/docs/Mozilla/Projects/SpiderMonkey/JIT_Optimization_Strategies">JIT Optimization Strategies</a> available as well.</li>
</ul>
</li>
</ol>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b7c5796-b584-4ff0-bb05-3bf562068fa4/load-respond-fast-diagram-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b7c5796-b584-4ff0-bb05-3bf562068fa4/load-respond-fast-diagram-opt.png" sizes="100vw" alt="An illustration to help you understand time loading and responsiveness" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2695b593-d0da-416a-94c2-d94145f92079/isinputpending-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2695b593-d0da-416a-94c2-d94145f92079/isinputpending-opt.png" sizes="100vw" caption="<a href='https://web.dev/isinputpending/'>isInputPending()</a> is a new browser API that attempts to bridge the gap between loading and responsiveness.(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2695b593-d0da-416a-94c2-d94145f92079/isinputpending-opt.png'>Large preview</a>)" alt="A blue banner showing running JS with white lines in regular gaps representing the time when we proactively check whether there’s user input without incurring the overhead of yielding execution to the browser and back" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abc86cd5-4c43-4382-9ba8-c8b81ec1d8e5/requestmap-http-cnn-com.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abc86cd5-4c43-4382-9ba8-c8b81ec1d8e5/requestmap-http-cnn-com.png" sizes="100vw" caption="The <a href='https://domainmap.webperf.tools/render/190223_BN_18cef49f92088f84fbba5b96f7fd54cd/#'>request map for CNN.com</a> showing the chain of each request to different domains, all the way to eighth-party scripts. <a href='https://dougsillars.com/2019/02/27/4th-parties-uninvited-guests-to-your-site/'>Source</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abc86cd5-4c43-4382-9ba8-c8b81ec1d8e5/requestmap-http-cnn-com.png'>Large preview</a>)" alt="An illustration of a map showing the chain of each request to different domains, all the way to eighth-party scripts" >}}

<ol class="continue">
<li><strong>Always prefer to self-host third-party assets.</strong><br />Yet again, <a href="https://csswizardry.com/2019/05/self-host-your-static-assets/">self-host your static assets</a> by default. It’s common to assume that if many sites use the same public CDN and the same version of a JavaScript library or a web font, then the visitors would land on our site with the scripts and fonts already cached in their browser, speeding up their experience considerably. However, it’s <a href="https://calendar.perfplanet.com/2019/bundling-javascript-for-performance-best-practices/">very unlikely to happen</a>.

<p>For security reasons, to avoid fingerprinting, browsers have been implementing <a href="https://calendar.perfplanet.com/2019/bundling-javascript-for-performance-best-practices/">partitioned caching</a> that was introduced in Safari back in 2013, and <a href="https://developers.google.com/web/updates/2020/10/http-cache-partitioning">in Chrome last year</a>. So if two sites point to the exact same third-party resource URL, the code is <strong>downloaded once per domain</strong>, and the cache is "sandboxed" to that domain due to privacy implications (<em>thanks, David Calhoun!</em>).
Hence, using a public CDN <a href="https://almanac.httparchive.org/en/2019/cdn#cdns-for-common-libraries-and-content">will not</a> automatically lead to better performance.</p>

<p>Furthermore, it’s worth noting that <a href="https://calendar.perfplanet.com/2019/self-hosting-third-party-resources-the-good-the-bad-and-the-ugly/">resources don’t live in the browser’s cache as long as we might expect</a>, and first-party assets are more likely to stay in the cache than third-party assets. Therefore, self-hosting is usually more reliable and secure, and better for performance, too.</li>
<li><strong>Constrain the impact of third-party scripts.</strong><br />With all performance optimizations in place, often we can’t control third-party scripts coming from business requirements. Third-party-scripts metrics aren’t influenced by end-user experience, so too often one single script ends up calling a long tail of obnoxious third-party scripts, hence ruining a dedicated performance effort. To contain and mitigate performance penalties that these scripts bring along, it’s not enough to just <a href="https://www.twnsnd.com/posts/performant_third_party_scripts.html">defer their loading and execution</a> and warm up connections via resource hints, i.e. <code>dns-prefetch</code> or <code>preconnect</code>.

<p>Currently 57% of all JavaScript code excution time is <a href="https://github.com/patrickhulce/third-party-web">spent on third-party code</a>. The median mobile site accesses <strong>12 third-party domains</strong>, with a median of 37 different requests (or about 3 requests made to each third party).</p>

<p>Furthermore, these third-parties often invite <strong>fourth-party scripts</strong> to join in, ending up with a huge performance bottleneck, sometimes going as far as to the <a href="https://dougsillars.com/2019/02/27/4th-parties-uninvited-guests-to-your-site/">eigth-party scripts</a> on a page. So regularly auditing your dependencies and tag managers can bring along costly surprises.</p>

<p>Another problem, as Yoav Weiss explained in his <a href="https://conffab.com/video/taking-back-control-over-third-party-content/">talk on third-party scripts</a>, is that in many cases these scripts download resources that are dynamic. The resources change between page loads, so we don’t necessarily know which hosts the resources will be downloaded from and what resources they would be.</p>

<p>Deferring, as shown above, might be just a start though as third-party scripts also steal bandwidth and CPU time from your app. We could be a bit more aggressive and <a href="https://3perf.com/blog/notion/#defer-third-parties">load them only when our app has initialized</a>.</p>

<pre class="language-js">
<code>/* Before */
const App = () => {
  return &lt;div&gt;
    &lt;script&gt;
      window.dataLayer = window.dataLayer || [];
      function gtag(){...}
      gtg('js', new Date());
    &lt;/script&gt;
  &lt;/div&gt;
}

/* After */
const App = () => {
  const[isRendered, setRendered] = useState(false);

  useEffect(() => setRendered(true));

  return &lt;div&gt;
  {isRendered ?
    &lt;script&gt;
      window.dataLayer = window.dataLayer || [];
      function gtag(){...}
      gtg('js', new Date());
    &lt;/script&gt;
  : null}
  &lt;/div&gt;
}
</code></pre>

<p>In a fantastic post on <a href="https://andydavies.me/blog/2020/10/02/reducing-the-site-speed-impact-of-third-party-tags/">"Reducing the Site-Speed Impact of Third-Party Tags"</a>, Andy Davies explores a strategy of minimizing the footprint of third-parties &mdash; from identifying their costs towards reducing their impact.</p>

<p>According to Andy, there are two ways tags impact site-speed &mdash; they compete for <strong>network bandwidth and processing time</strong> on visitors’ devices, and depending on how they’re implemented, they can delay HTML parsing as well. So the first step is to identify the impact that third-parties have, by <a href="https://andydavies.me/blog/2018/02/19/using-webpagetest-to-measure-the-impact-of-3rd-party-tags/">testing the site <em>with</em> and <em>without</em> scripts using WebPageTest</a>. With Simon Hearne’s <a href="https://requestmap.herokuapp.com/">Request Map</a>, we can also visualize third-parties on a page along with details on their size, type and what triggered their load.</p>

<p>Preferably <a href="https://www.twnsnd.com/posts/performant_third_party_scripts.html">self-host and use a single hostname</a>, but also <a href="https://www.soasta.com/blog/10-pro-tips-for-managing-the-performance-of-your-third-party-scripts/">use a request map</a> to exposes fourth-party calls and detect when the scripts change. You can use Harry Roberts' <a href="https://csswizardry.com/2018/05/identifying-auditing-discussing-third-parties/">approach for auditing third parties</a> and produce spreadsheets like <a href="https://docs.google.com/spreadsheets/d/1uTcRSoJAkXfIm2yfG5hvCSzvSZD9fAwXNQMVK3HdPMI/edit#gid=0">this one</a> (also check <a href="https://www.youtube.com/watch?v=bmIUYBNKja4">Harry's auditing workflow</a>).</p>

<p>Afterwards, we can explore <strong>lightweight alternatives to existing scripts</strong> and slowly replace duplicates and main culprits with lighter options. Perhaps some of the scripts could be <a href="https://www.tunetheweb.com/blog/adding-controls-to-google-tag-manager/#pixels">replaced with their fallback tracking pixel instead of the full tag</a>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4482ab7-e2d8-4333-be8b-7d49021ea109/loadyoutube-opt.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4482ab7-e2d8-4333-be8b-7d49021ea109/loadyoutube-opt.jpg" sizes="100vw" caption="Loading YouTube with facades, e.g. <a href='https://github.com/paulirish/lite-youtube-embed'>lite-youtube-embed</a> that’s significantly smaller than an actual YouTube player. (<a href='https://web.dev/third-party-facades/'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4482ab7-e2d8-4333-be8b-7d49021ea109/loadyoutube-opt.jpg'>Large preview</a>)" alt="Left example showing 3KB of JavaScript using the lite-youtube custom element, middle and right example showing +540KB of JavaScript with the lite-youtube custom element" >}}

<p>If it’s not viable, we can at least <a href="https://web.dev/third-party-facades/">lazy load third-party resources with facades</a>, i.e. a static element which looks similar to the actual embedded third-party, but is not functional and therefore much less taxing on the page load. The trick, then, is to <strong>load the actual embed only on interaction</strong>.</p>
<p>For example, we can use:</p>
<ul>
<li><a href="https://github.com/luwes/lite-vimeo-embed">lite-vimeo-embed</a> for the Vimeo player,</li>
<li><a href="https://github.com/slightlyoff/lite-vimeo">lite-vimeo</a> for the Vimeo player,</li>
<li><a href="https://github.com/paulirish/lite-youtube-embed">lite-youtube-embed</a> for the YouTube player,</li>
<li><a href="https://github.com/calibreapp/react-live-chat-loader">react-live-chat-loader</a> for a live chat (<a href="https://calibreapp.com/blog/fast-live-chat">case study</a>, and <a href="https://gideonpyzer.dev/blog/2019/07/13/lazy-loading-zendesk-saved-huddle-2.3mb-of-javascript/">another case-study</a>),</li>
<li><a href="https://github.com/vb/lazyframe">lazyframe</a> for iframes.</li>
</ul>

<p>One of the reasons why tag managers are usually large in size is because of the many simultaneous experiments that are running at the same time, along with many user segments, page URLs, sites etc., so according to Andy, reducing them can reduce both the download size and the time it takes to execute the script in the browser.</p>

<p>And then there are <a href="https://andydavies.me/blog/2020/11/16/the-case-against-anti-flicker-snippets/">anti-flicker snippets</a>. Third-parties such as Google Optimize, Visual Web Optimizer (VWO) and others are unanimous in using them. These snippets are usually injected along with running <strong>A/B tests</strong>: to avoid flickering between the different test scenarios, they hide the <code>body</code> of the document with <code>opacity: 0</code>, then adds a function that gets called after a few seconds to bring the <code>opacity</code> back. This often results in massive delays in rendering due to massive client-side execution costs.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb036e99-1355-479a-ba70-bd3b77ac2818/gymshark-annotated.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb036e99-1355-479a-ba70-bd3b77ac2818/gymshark-annotated.png" sizes="100vw" caption="With A/B testing in use, customers would often see flickering like this one. Anti-Flicker snippets prevent that, but they also cost in performance. Via <a href='https://andydavies.me/blog/2020/11/16/the-case-against-anti-flicker-snippets/'>Andy Davies</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb036e99-1355-479a-ba70-bd3b77ac2818/gymshark-annotated.png'>Large preview</a>)" alt="Seven previews shown from 0.0 seconds to 6.0 seconds showing how and when contents are hidden by the anti-flicker snippet when a visitor initiates navigation" >}}

<p>Therefore <a href="https://twitter.com/tkadlec/status/1327016687984578560">keep track how often the anti-flicker timeout is triggered</a> and reduce the timeout. Default blocks display of your page by up to 4s which will ruin conversion rates. According to Tim Kadlec, "Friends don’t let friends do client side A/B testing". <strong>Server-side A/B testing</strong> on CDNs (e.g. Edge Computing, or <a href="https://www.youtube.com/watch?v=W-tBI_n0m_w">Edge Slice Rerendering</a>) is always a more performant option.</p>

<p>If you have to deal with almighty <strong>Google Tag Manager</strong>, Barry Pollard provides some <a href="https://www.tunetheweb.com/blog/adding-controls-to-google-tag-manager/">guidelines to contain the impact of Google Tag Manager</a>. Also, Christian Schaefer <a href="https://schepp.dev/posts/ad-integration-in-2020/">explores strategies for loading ads</a>.</p>

<p>Watch out: some <a href="https://twitter.com/blue2blond/status/1262309544757207040">third-party widgets hide themselves from auditing tools</a>, so they might be more difficult to spot and measure. To <a href="https://csswizardry.com/2017/07/performance-and-resilience-stress-testing-third-parties/">stress-test third parties</a>, examine bottom-up summaries in Performance profile page in DevTools, test what happens if a request is blocked or it has timed out &mdash; for the latter, you can use WebPageTest’s Blackhole server <code>blackhole.webpagetest.org </code> that you can point specific domains to in your <code>hosts</code> file.</p>

<p>What options do we have then? Consider <strong>using service workers by racing the resource download with a timeout</strong> and if the resource hasn’t responded within a certain timeout, return an empty response to tell the browser to carry on with parsing of the page. You can also log or block third-party requests that aren’t successful or don’t fulfill certain criteria. If you can, <a href="https://medium.com/caspertechteam/we-shaved-1-7-seconds-off-casper-com-by-self-hosting-optimizely-2704bcbff8ec">load the 3rd-party-script from your own server</a> rather than from the vendor’s server and lazy load them.</p>

<p>Another option is to establish a <strong>Content Security Policy (CSP)</strong> to restrict the impact of third-party scripts, e.g. disallowing the download of audio or video. The best option is to embed scripts via <code>&lt;iframe&gt;</code> so that the scripts are running in the context of the iframe and hence don’t have access to the DOM of the page, and can’t run arbitrary code on your domain. Iframes can be further constrained using the <code>sandbox</code> attribute, so you can disable any functionality that iframe may do, e.g. prevent scripts from running, prevent alerts, form submission, plugins, access to the top navigation, and so on.</p>

<p>You could also keep third-parties in check via <a href="https://timkadlec.com/remembers/2020-02-20-in-browser-performance-linting-with-feature-policies/">in-browser performance linting with feature policies</a>, a relatively new feature that lets you <sdtrong>opt-in or out of certain browser features</strong> on your site. (As a sidenote, it could also be used to avoid oversized and unoptimized images, unsized media, sync scripts and others). Currently supported in Blink-based browsers.</p>

<pre>
<code language="javascript">/* Via Tim Kadlec. https://timkadlec.com/remembers/2020-02-20-in-browser-performance-linting-with-feature-policies/ */
/* Block the use of the Geolocation API with a Feature-Policy header. */
Feature-Policy: geolocation 'none'</code>
</pre>

<p>As many third-party scripts are running in iframes, you probably need to be thorough in restricting their allowances. <a href="https://www.html5rocks.com/en/tutorials/security/sandboxed-iframes/">Sandboxed iframes are always a good idea</a>, and each of the limitations can be lifted via a number of <code>allow</code> values on the <code>sandbox</code> attribute. <a href="https://caniuse.com/#search=sandbox">Sandboxing is supported almost everywhere</a>, so constrain third-party scripts to the bare minimum of what they should be allowed to do.</p>


{{< rimg breakout="true" href="https://www.thirdpartyweb.today/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eefa9eb3-1d15-484e-acaa-3060be1c4b5e/third-party-impact-opt.png" sizes="100vw" caption="<a href='https://www.thirdpartyweb.today/'>ThirdPartyWeb.Today</a> groups all third-party scripts by category (analytics, social, advertising, hosting, tag manager etc.) and visualizes how long the entity’s scripts take to execute (on average). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eefa9eb3-1d15-484e-acaa-3060be1c4b5e/third-party-impact-opt.png'>Large preview</a>)" alt="A screenshot of the ThirdPartyWeb.Today website visualizing how long the entity’s scripts take to execute on average" >}}

<p>Consider using an <a href="https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API">Intersection Observer</a>; that would enable <strong>ads to be iframed</strong> while still dispatching events or getting the information that they need from the DOM (e.g. ad visibility). Watch out for new policies such as <a href="https://www.smashingmagazine.com/2018/12/feature-policy/">Feature policy</a>, resource size limits and CPU/Bandwidth priority to limit harmful web features and scripts that would slow down the browser, e.g. synchronous scripts, synchronous XHR requests, <em>document.write</em> and outdated implementations.</p>

<p>Finally, when choosing a third-party service, consider checking Patrick Hulce's <a href="https://www.thirdpartyweb.today/">ThirdPartyWeb.Today</a>, a service that <strong>groups all third-party scripts by category</strong> (analytics, social, advertising, hosting, tag manager etc.) and visualizes how long the entity’s scripts take to execute (on average). Obviously, largest entities have the worst performance impact to the pages they’re on. Just by skimming the page, you’ll get an idea of the performance footprint you should be expecting.</p>

<p>Ah, and don't forget about the usual suspects: instead of third-party widgets for sharing, we can use <a href="https://www.savjee.be/2015/01/Creating-static-social-share-buttons/">static social sharing buttons</a> (such as by <a href="https://simplesharingbuttons.com">SSBG</a>) and <a href="https://developers.google.com/maps/documentation/static-maps/intro">static links to interactive maps</a> instead of interactive maps.</p>

</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23658f0d-97bc-4dac-a2e5-e6705d7a8deb/03-thirdparty-front-end-performance-checklist-2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23658f0d-97bc-4dac-a2e5-e6705d7a8deb/03-thirdparty-front-end-performance-checklist-2020.png" sizes="100vw" caption="Casper.com published a detailed case study on how they managed to shave 1.7 seconds off the site by self-hosting Optimizely. It might be worth it. (<a href='https://medium.com/caspertechteam/we-shaved-1-7-seconds-off-casper-com-by-self-hosting-optimizely-2704bcbff8ec'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf570272-840e-4cf8-92de-76808a12422c/casper-case-study-optimizely.png'>Large preview</a>)" alt="A graph example comparing the percentage of requests of first- and third parties: 399KB amounting to 27% of requests for first party, and 1.15MB amounting to 73% of requests for third-party" >}}

<ol class="continue">
<li><strong>Set HTTP cache headers properly.</strong><br />Caching seems to be such an obvious thing to do, yet it might be quite tough to get right. We need to double-check that <code>expires</code>, <code>max-age</code>, <code>cache-control</code>, and other HTTP cache headers have been set properly. Without proper HTTP cache headers, browsers will set them automatically at <a href="https://paulcalvano.com/2018-03-14-http-heuristic-caching-missing-cache-control-and-expires-headers-explained/">10% of elapsed time since <code>last-modified</code></a>, ending up with potential <a href="https://twitter.com/simonhearne/status/1259973084880220163">under- and over-caching</a>.

<p>In general, resources should be cacheable either for a <a href="https://jakearchibald.com/2016/caching-best-practices/">very short time (if they are likely to change) or indefinitely (if they are static)</a> &mdash; you can just change their version in the URL when needed. You can call it a <a href="https://calendar.perfplanet.com/2020/cache-forever-assets/">Cache-Forever strategy</a>, in which we could relay <code>Cache-Control</code> and <code>Expires</code> headers to the browser to only allow assets to expire in a year. Hence, the browser wouldn’t even make a request for the asset if it has it in the cache.</p>

<p>The exception are <a href="https://twitter.com/iamakulov/status/1259763674409033735">API responses</a> (e.g. <code>/api/user</code>). To prevent caching, we can use <code>private, no store</code>, and <a href="https://docs.fastly.com/en/guides/configuring-caching#do-not-cache">not <code>max-age=0, no-store</code></a>:</p>

<pre><code>Cache-Control: private, no-store</code></pre>

<p>Use <code>Cache-control: immutable</code> to <a href="https://bitsup.blogspot.com/2016/05/cache-control-immutable.html">avoid revalidation of long explicit cache lifetimes</a> when users hit the reload button. For the reload case, <code>immutable</code> saves HTTP requests and improves the load time of the dynamic HTML as they no longer compete with the multitude of 304 responses.</p>

<p>A typical example where we want to use <code>immutable</code> are CSS/JavaScript assets with a hash in their name. For them, we probably want to cache as long as possible, and ensure they never get re-validated:</p>

<pre class="language-javascript">
<code>Cache-Control: max-age: 31556952, immutable</code></pre>

<p>According to Colin Bendell’s research, <code>immutable</code> <a href="https://twitter.com/colinbendell/status/1256218497941635072">reduces 304 redirects by around 50%</a> as even with <code>max-age</code> in use, clients still re-validate and block upon refresh. It’s <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control">supported in Firefox, Edge and Safari</a> and <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=611416#c70">Chrome is still debating the issue</a>.</p>

<p>According to Web Almanac, "its usage <a href="https://almanac.httparchive.org/en/2020/caching">has grown to 3.5%</a>, and it’s widely used in <a href="https://discuss.httparchive.org/t/cache-control-immutable-a-year-later/1195">Facebook and Google third-party responses</a>."</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/231b0c68-fec1-45ec-b511-6b8c203a6420/effectiveness-cache-control-immutable.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/231b0c68-fec1-45ec-b511-6b8c203a6420/effectiveness-cache-control-immutable.jpg" sizes="100vw" caption="Cache-Control: Immutable reduces 304s by around 50%, according to <a href='https://twitter.com/colinbendell/status/1256218497941635072'>Colin Bendell’s research at Cloudinary</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/231b0c68-fec1-45ec-b511-6b8c203a6420/effectiveness-cache-control-immutable.jpg'>Large preview</a>)" alt="Effectiveness of Cache Control across continents with data retrieved from Android Chrome and iOS Safari" >}}

<p>Do you remember the good ol' <a href="https://www.fastly.com/blog/stale-while-revalidate-stale-if-error-available-today">stale-while-revalidate</a>? When we specify the caching time with the <code>Cache-Control</code> response header (e.g. <code>Cache-Control: max-age=604800</code>), after <code>max-age</code> expires, the browser will re-fetch the requested content, causing the page to load slower. This slowdown can be avoided with <code>stale-while-revalidate</code>; it basically defines an extra window of time during which a cache can use a stale asset as long as it revalidates it async in the background. Thus, it "hides" latency (both in the network and on the server) from clients.</p>

<p>In June&ndash;July 2019, <strong>Chrome and Firefox launched support</strong> of <code>stale-while-revalidate</code> in HTTP Cache-Control header, so as a result, it should improve subsequent page load latencies as stale assets are no longer in the critical path. Result: <a href="https://twitter.com/RyanTownsend/status/1072443651844911104">zero RTT for repeat views</a>.</p>

<p>Be wary of the <a href="https://www.smashingmagazine.com/2017/11/understanding-vary-header/">vary header</a>, especially <a href="https://www.fastly.com/blog/getting-most-out-vary-fastly">in relation to CDNs</a>, and watch out for the <a href="https://httpwg.org/http-extensions/draft-ietf-httpbis-variants.html">HTTP Representation Variants</a> which help avoiding an additional round trip for validation whenever a new request differs slightly (but not significantly) from prior requests (<em>thanks, Guy and Mark!</em>).</p>

<p>Also, double-check that you aren’t sending <a href="https://www.fastly.com/blog/headers-we-dont-want">unnecessary headers</a> (e.g. <code>x-powered-by</code>, <code>pragma</code>, <code>x-ua-compatible</code>, <code>expires</code>, <code>X-XSS-Protection</code> and others) and that you include <a href="https://www.fastly.com/blog/headers-we-want">useful security and performance headers</a> (such as <code>Content-Security-Policy</code>, <code>X-Content-Type-Options</code> and others). Finally, keep in mind the <a href="https://medium.com/@ankur_anand/the-terrible-performance-cost-of-cors-api-on-the-single-page-application-spa-6fcf71e50147">performance cost of CORS requests</a> in single-page applications.</p>

<p><strong>Note</strong>: We often assume that cached assets are retrieved instantly, but research shows that <a href="https://simonhearne.com/2020/network-faster-than-cache/">retrieving an object from cache can take hundreds of milliseconds</a>. In fact, according to Simon Hearne, "sometimes network might be faster than cache, and retrieving assets from cache can be costly with a large number of cached assets (not file size) and the user’s devices. For example: Chrome OS average cache retrieval doubles from ~50ms with 5 cached resources up to ~100ms with 25 resources".</p>

<p>Besides, we often assume that bundle size isn’t a huge issue and users will download it once and then use the cached version. At the same time, with CI/CD we push code to production multiple times a day, <a href="https://twitter.com/csswizardry/status/1261091962280706050">cache gets invalidated every time</a>, so being strategic about caching matters.</p>

<p>When it comes to caching, there are plenty of resources that are worth reading:</p>
<ul>
<li><a href="https://csswizardry.com/2019/03/cache-control-for-civilians/">Cache-Control for Civilians</a>, a deep-dive into everything caching with Harry Roberts.</li>
<li><a href="https://devcenter.heroku.com/articles/increasing-application-performance-with-http-cache-headers">Heroku’s primer on HTTP caching headers</a>,</li>
<li><a href="https://jakearchibald.com/2016/caching-best-practices/">Caching Best Practices</a> by Jake Archibald,</li>
<li><a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching?hl=en">HTTP caching primer</a> by Ilya Grigorik,</li>
<li><a href="https://web.dev/stale-while-revalidate/">Keeping things fresh with stale-while-revalidate</a> by Jeff Posnick.</li>
<li><a href="https://dev.to/lydiahallie/cs-visualized-cors-5b8h">CS Visualized: CORS</a> by Lydia Hallie is a great explainer on CORS, how it works and how to make sense of it.</li>
<li>Talking on CORS, here’s a little refresher on <a href="https://css-tricks.com/i-learned-to-love-the-same-origin-policy/">Same-Origin Policy</a> by Eric Portis.</li>
</ul>

</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ab1567c-ba71-4274-922d-dc9a97275c6a/cache-retrieval-time.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ab1567c-ba71-4274-922d-dc9a97275c6a/cache-retrieval-time.png" sizes="100vw" caption="We assume that browser caches are near-instantaneous, but data shows that retrieving an object from cache can take hundreds of milliseconds! From Simon Hearne’s research on <a href='https://simonhearne.com/2020/network-faster-than-cache/'>When Network Is Faster Than Cache</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ab1567c-ba71-4274-922d-dc9a97275c6a/cache-retrieval-time.png'>Large preview</a>)" alt="A graph showing cache retrieval time by count of cached assets with different OS and browsers named on the right (from top to bottom): Desktop Chrome OS, Tablet Android OS, Mobile Android OS, Desktop Mac =S X, Desktop Windows, Desktop Linux" >}}

{{% feature-panel %}}

## Delivery Optimizations

<ol class="continue">
<li><strong>Do we use <code>defer</code> to load critical JavaScript asynchronously?</strong><br />When the user requests a page, the browser fetches the HTML and constructs the DOM, then fetches the CSS and constructs the CSSOM, and then generates a rendering tree by matching the DOM and CSSOM. If any JavaScript needs to be resolved, the browser <strong>won’t start rendering the page</strong> until it’s resolved, thus delaying rendering. As developers, we have to explicitly tell the browser not to wait and to start rendering the page. The way to do this for scripts is with the <code>defer</code> and <code>async</code> attributes in HTML.

<p>In practice, it turns out that it's better to <a href="https://calendar.perfplanet.com/2016/prefer-defer-over-async/">use <code>defer</code> instead of <code>async</code></a>. Ah, what's the <strong>difference</strong> again? According to <a href="https://youtu.be/RwSlubTBnew?t=1034">Steve Souders</a>, once <code>async</code> scripts arrive, they are executed immediately &mdash; as soon as the script is ready. If that happens very fast, for example when the script is in cache aleady, it can actually block HTML parser. With <code>defer</code>, browser doesn’t execute scripts until HTML is parsed. So, unless you need JavaScript to execute before start render, it’s better to use <code>defer</code>. Also, multiple async files will execute in a non-deterministic order.</p>

<p>It's worth noting that there are a few <a href="https://twitter.com/csswizardry/status/1346137189009264640">misconceptions about <code>async</code> and <code>defer</code></a>. Most importantly, <code>async</code> doesn’t mean that the code will run whenever the script is ready; it means that it will run whenever the scripts is ready <em>and</em> all preceding sync work is done. In Harry Roberts' words, "If you put an <code>async</code> script after sync scripts, your <code>async</code> script is only as fast as your slowest sync script."</p>

<p>Also, <a href="https://twitter.com/csswizardry/status/1331721659498319873">it's not recommended to use both <code>async</code> and <code>defer</code></a>. Modern browsers support both, but whenever both attributes are used, <code>async</code> will always win.</p>

<p>If you'd like to dive into more details, Milica Mihajlija has written a very detailed guide on <a href="https://hacks.mozilla.org/2017/09/building-the-dom-faster-speculative-parsing-async-defer-and-preload/">Building the DOM faster</a>, going into the details of speculative parsing, async and defer.</p>
</li>

<li><strong>Lazy load expensive components with IntersectionObserver and priority hints.</strong><br />In general, it’s recommended to lazy-load all expensive components, such as heavy JavaScript, videos, iframes, widgets, and potentially images. <a href="https://web.dev/native-lazy-loading/">Native lazy-loading</a> is already available for images and iframes with the <code>loading</code> attribute (only Chromium). Under the hood, this attribute defers the loading of the resource until it reaches a <a href="https://web.dev/browser-level-image-lazy-loading/#distance-from-viewport-thresholds">calculated distance</a> from the viewport.

<pre class="language-html">
<code>&lt;!-- Lazy loading for images, iframes, scripts.
Probably for images outside of the viewport. --&gt;
&lt;img loading="lazy" ... /&gt;
&lt;iframe loading="lazy" ... /&gt;

&lt;!-- Prompt an early download of an asset.
For critical images, e.g. hero images. --&gt;
&lt;img loading="eager" ... /&gt;
&lt;iframe loading="eager" ... /&gt;</code></pre>

<p>That threshold depends on a few things, from the type of image resource being fetched to effective connection type. But experiments conducted using Chrome on Android suggest that on 4G, 97.5% of below-the-fold images that are lazy-loaded <a href="https://web.dev/browser-level-image-lazy-loading/#distance-from-viewport-thresholds">were fully loaded within 10ms of becoming visible</a>, so it should be safe.</p>

<p>We can also use <a href="https://developers.google.com/web/updates/2019/02/priority-hints#using_priority_hints"><code>importance</code> attribute</a> (<code>high</code> or <code>low</code>) on a <code>&lt;script&gt;</code>, <code>&lt;img&gt;</code>, or <code>&lt;link&gt;</code> element (Blink only). In fact, it’s a great way to <strong>deprioritize images</strong> in carousels, as well as re-prioritize scripts. However, sometimes we might need a bit more granular control.</p>

<pre class="language-html">
<code>&lt;!--
When the browser assigns "High" priority to an image,
but we don’t actually want that.
--&gt;
&lt;img src="less-important-image.svg" fetchpriority="low" ... /&gt;

&lt;!--
We want to initiate an early fetch for a resource,
but also deprioritize it.
--&gt;
&lt;link rel="preload" fetchpriority="low" href="/script.js" as="script" /&gt;</code></pre>

<p>The most performant way to do slightly more sophisticated lazy loading is by <a href="https://www.telerik.com/blogs/intersection-observer-api-makes-lazy-loading-a-snap">using the Intersection Observer API</a> that provides a way to <strong>asynchronously observe changes</strong> in the intersection of a target element with an ancestor element or with a top-level document’s viewport. Basically, you need to create a new <code>IntersectionObserver</code> object, which receives a callback function and a set of options. Then we add a target to observe.

<p>The callback function executes when the target <strong>becomes visible</strong> or invisible, so when it intercepts the viewport, you can start taking some actions before the element becomes visible. In fact, we have a granular control over when the observer’s callback should be invoked, with <code>rootMargin</code> (margin around the root) and <code>threshold</code> (a single number or an array of numbers which indicate at what percentage of the target’s visibility we are aiming).</p>

<p>Alejandro Garcia Anglada has published a <a href="https://medium.com/@aganglada/intersection-observer-in-action-efc118062366">handy tutorial</a> on how to actually implement it, Rahul Nanwani wrote a detailed post on <a href="https://css-tricks.com/the-complete-guide-to-lazy-loading-images/">lazy-loading foreground and background images</a>, and Google Fundamentals provide a <a href="https://developers.google.com/web/fundamentals/performance/lazy-loading-guidance/images-and-video/">detailed tutorial on lazy loading images and video with Intersection Observer</a> as well.</p>

<p>Remember art-directed storytelling long reads with moving and sticky objects? You can implement <a href="https://github.com/russellgoldenberg/scrollama">performant scrollytelling with Intersection Observer</a>, too.</p>

<p>Check again what else you could lazy load. Even <strong>lazy-loading translation strings</strong> and emoji could help. By doing so, Mobile Twitter managed to achieve 80% faster JavaScript execution from the new internationalization pipeline.</p>

<p>A quick word of caution though: it’s worth noting that <a href="https://twitter.com/csswizardry/status/1326504788360638466">lazy loading should be an exception rather than the rule</a>. It’s probably <a href="https://twitter.com/tunetheweb/status/1346556743308992512?s=20">not reasonable</a> to lazy-load anything that you actually want people to see quickly, e.g. product page images, hero images or a script required for the main navigation to become interactive.</p>
</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9620dcb-d5c1-449f-872a-552130a1ecd6/old-new-better-thresholds.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9620dcb-d5c1-449f-872a-552130a1ecd6/old-new-better-thresholds.png" sizes="100vw" caption="On fast connections (e.g 4G), Chrome’s distance-from-viewport thresholds was recently reduced from 3000px to 1250px, and on slower connections (e.g 3G), the threshold changed from 4000px to 2500px. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9620dcb-d5c1-449f-872a-552130a1ecd6/old-new-better-thresholds.png'>Large preview</a>)" alt="An example showing an old treshold of 3000px with 160KB downloads (left) while the new threshold has an amount of 1250px with only 90KB downloads (right) showing an improvement of img loading lazy data savings" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4d6866d-7897-48bd-bc0c-c62a108e3c48/01-internationalization-front-end-performance-checklist-2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4d6866d-7897-48bd-bc0c-c62a108e3c48/01-internationalization-front-end-performance-checklist-2020.png" sizes="100vw" caption="By lazy-loading translation strings, Mobile Twitter managed to achieve 80% faster JavaScript execution from the new internationalization pipeline. (Image credit: <a href='https://twitter.com/addyosmani'>Addy Osmani</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4d6866d-7897-48bd-bc0c-c62a108e3c48/01-internationalization-front-end-performance-checklist-2020.png'>Large preview</a>)" alt="An illustration with text around a mobile phone with the Twitter UI showwn, explaining tooling improvements from lazy-load translation strings" >}}

<ol class="continue">
<li><strong>Load images progressively.</strong><br />You could even take lazy loading to the next level by adding <a href="https://calendar.perfplanet.com/2017/progressive-image-loading-using-intersection-observer-and-sqip/">progressive image loading</a> to your pages. Similarly to Facebook, Pinterest, Medium and Wolt, you could load low quality or even blurry images first, and then as the page continues to load, replace them with the full quality versions by using the <a href="https://blurha.sh/">BlurHash technique</a> or <a href="https://www.guypo.com/introducing-lqip-low-quality-image-placeholders">LQIP (Low Quality Image Placeholders) technique</a>.</p>

<p>Opinions differ if these techniques improve user experience or not, but it definitely improves time to First Contentful Paint. We can even automate it by using <a href="https://github.com/technopagan/sqip">SQIP</a> that creates a low quality version of an image as an SVG placeholder, or <a href="https://calendar.perfplanet.com/2018/gradient-image-placeholders/">Gradient Image Placeholders</a> with CSS linear gradients.</p>

<p>These placeholders could be embedded within HTML as they naturally compress well with text compression methods. In his article, Dean Hume <a href="https://calendar.perfplanet.com/2017/progressive-image-loading-using-intersection-observer-and-sqip/">has described</a> how this technique can be implemented using Intersection Observer.</p>

<p>Fallback? If the browser doesn’t support intersection observer, we can still <a href="https://medium.com/@aganglada/intersection-observer-in-action-efc118062366">lazy load</a> a <a href="https://github.com/jeremenichelli/intersection-observer-polyfill">polyfill</a> or load the images immediately. And there is even a <a href="https://github.com/ApoorvSaxena/lozad.js">library</a> for it.</p>

<p>Want to go fancier? You could <a href="https://jmperezperez.com/svg-placeholders/">trace your images</a> and use primitive shapes and edges to create a lightweight SVG placeholder, load it first, and then transition from the placeholder vector image to the (loaded) bitmap image.</p></li>

{{< rimg breakout="true" href="https://jmperezperez.com/svg-placeholders/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7f56052-6abb-4d18-a5aa-8d84102d812e/jmperez-composition-primitive-full.jpg" sizes="100vw" caption="SVG lazy loading technique by <a href='https://jmperezperez.com/svg-placeholders/'>José M. Pérez</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7f56052-6abb-4d18-a5aa-8d84102d812e/jmperez-composition-primitive-full.jpg'>Large preview</a>)" alt="Three different versions showing the SVG lazy loading technique by José M. Pérez, a version similar to Cubism art on the left, a pixelated blurred version in the middle, and a proper picture of José himself on the right" >}}

<li><strong>Do you defer rendering with <code>content-visibility</code>?</strong><br />For complex layout with plentiful of content blocks, images and videos, decoding data and rendering pixels might be a quite expensive operation &mdash; especially on low-end devices. With <a href="https://web.dev/content-visibility/"><code>content-visibility: auto</code></a>, we can prompt the browser to skip the layout of the children while the container is outside of the viewport.

<p>For example, you might skip the rendering of the footer and late sections on the initial load:</p>

<pre class="language-css">
<code>footer {
  content-visibility: auto;
  contain-intrinsic-size: 1000px;
  /* 1000px is an estimated height for sections that are not rendered yet. */
}</code></pre>

<p>Note that <a href="https://www.terluinwebdesign.nl/en/css/calculating-contain-intrinsic-size-for-content-visibility/"><em>content-visibility: auto;</em> behaves like <em>overflow: hidden;</em></a>, but you can fix it by applying <code>padding-left</code> and <code>padding-right</code> instead of the default <code>margin-left: auto;</code>, <code>margin-right: auto;</code> and a declared width. The padding basically allows elements to overflow the content-box and enter the padding-box without leaving the box model as a whole and getting cut off.</p>

<p>Also, keep in mind that you might introduce some CLS when new content eventually gets rendered, so it’s a good idea to use <code>contain-intrinsic-size</code> <a href="https://twitter.com/Una/status/1291012585807110144">with a placeholder properly sized</a> (<em>thanks, Una!</em>).</p>

<p>Thijs Terluin has <a href="https://www.terluinwebdesign.nl/en/css/calculating-contain-intrinsic-size-for-content-visibility/">way more details about both properties</a> and how <code>contain-intrinsic-size</code> is calculated by the browser, Malte Ubl <a href="https://www.industrialempathy.com/posts/image-optimizations/">shows how you can calculate it</a> and a brief video explainer by Jake and Surma <a href="https://www.youtube.com/watch?v=FFA-v-CIxJQ">explains how it all works</a>.</p>

<p>And if you need to get a bit more granular, with <a href="https://developers.google.com/web/updates/2016/06/css-containment">CSS Containment</a>, you can manually skip layout, style and paint work for descendants of a DOM node if you need only size, alignment or computed styles on other elements &mdash; or the element is currently off-canvas.</p>
</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/640ed03b-3b1d-40be-84a8-6000698397aa/baseline-chunks-content-visibility-auto.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/640ed03b-3b1d-40be-84a8-6000698397aa/baseline-chunks-content-visibility-auto.jpg" sizes="100vw" caption="In the demo, applying <code>content-visibility: auto</code> to chunked content areas gives a 7&times; rendering performance boost on initial load. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/640ed03b-3b1d-40be-84a8-6000698397aa/baseline-chunks-content-visibility-auto.jpg'>Large preview</a>)" alt="The rendering performance on initial load is 2,288 ms for baseline (left) and 13,464 ms for chunks with content-visibility:auto (right)" >}}

<ol class="continue">
<li><strong>Do you defer decoding with <code>decoding="async"</code>?</strong><br />Sometimes content appears offscreen, yet we want to ensure that it’s available when customers need it &mdash; ideally, not blocking anything in the critical path, but decoding and rendering asynchronously. We can use <a href="https://html.spec.whatwg.org/multipage/images.html#decoding-images"><code>decoding="async"</code></a> to give the browser a permission to decode the image off the main thread, avoiding user impact of the CPU-time used to decode the image (via <a href="https://www.industrialempathy.com/posts/image-optimizations/">Malte Ubl</a>):<br /><br />

<pre class="language-html">
<code>&lt;img decoding="async" … /&gt;</code></pre>

<p>Alternatively, for offscreen images, we can display a placeholder first, and when the image is within the viewport, using IntersectionObserver, trigger a network call for the image to be downloaded in background. Also, we can <a href="https://youtu.be/YJGCZCaIZkQ?t=570">defer render until decode with img.decode()</a> or download the image if the <a href="https://medium.com/dailyjs/image-loading-with-image-decode-b03652e7d2d2">Image Decode API</a> isn’t available.</p>

<p>When rendering the image, we can use fade-in animations, for example. Katie Hempenius and Addy Osmani share more insights in their talk <a href="https://youtu.be/YJGCZCaIZkQ?t=436">Speed at Scale: Web Performance Tips and Tricks from the Trenches</a>.</li>

<li><strong>Do you generate and serve critical CSS?</strong><br />To ensure that browsers start rendering your page as quickly as possible, it’s become a <a href="https://www.smashingmagazine.com/2015/08/understanding-critical-css/">common practice</a> to collect all of the CSS required to start rendering the first visible portion of the page (known as "critical CSS" or "above-the-fold CSS") and include it inline in the <code>&lt;head&gt;</code> of the page, thus reducing roundtrips. Due to the limited size of packages exchanged during the slow start phase, your budget for critical CSS is around 14KB.

<p>If you go beyond that, the browser will need additional roundtrips to fetch more styles. <a href="https://github.com/filamentgroup/criticalCSS">CriticalCSS</a> and <a href="https://github.com/addyosmani/critical">Critical</a> enable you to output critical CSS for every template you're using. In our experience though, no automatic system was ever better than manual collection of critical CSS for every template, and indeed that's the approach we've moved back to recently.</p>

<p>You can then inline critical CSS and lazy-load the rest with <a href="https://github.com/GoogleChromeLabs/critters">critters Webpack plugin</a>. If possible, consider using the <a href="https://www.filamentgroup.com/lab/modernizing-delivery.html">conditional inlining approach</a> used by the Filament Group, or <a href="https://www.smashingmagazine.com/2018/11/pitfalls-automatically-inlined-code/">convert inline code to static assets on the fly</a>.</p>

<p>If you currently <strong>load your full CSS asynchronously</strong> with libraries such as <a href="https://github.com/filamentgroup/loadCSS">loadCSS</a>, it’s not really necessary. With <code>media="print"</code>, you can <a href="https://www.filamentgroup.com/lab/load-css-simpler/">trick browser into fetching the CSS asynchronously</a> but applying to the screen environment once it loads. (<em>thanks, Scott!</em>)</p>

<pre class="language-html">
<code>&lt;!-- Via Scott Jehl. https://www.filamentgroup.com/lab/load-css-simpler/ --&gt;
&lt;!-- Load CSS asynchronously, with low priority --&gt;
&lt;link rel="stylesheet"
  href="full.css"
  media="print"
  onload="this.media='all'" /&gt;</code></pre>

<p>When collecting all the critical CSS for each template, it’s common to explore the "above-the-fold" area alone. However, for complex layouts, it might be a good idea to include the groundwork of the layout as well to <strong>avoid massive recalculation</strong> and repainting costs, hurting your Core Web Vitals score as a result.</p>

<p>What if a user gets a URL that’s linking directly to the middle of the page but the CSS hasn’t been downloaded yet? In that case, it has become common to <a href="https://calendar.perfplanet.com/2020/implementing-critical-css-from-cms-to-cls/">hide non-critical content</a>, e.g. with <code>opacity: 0;</code> in inlined CSS and <code>opacity: 1</code> in full CSS file, and display it when CSS is available. It has a <strong>major downside</strong> though, as users on slow connections might never be able to read the content of the page. That’s why it’s better to always keep the content visible, even although it might not be styled properly.</p>

<p>Putting critical CSS (and <a href="https://csswizardry.com/2019/05/self-host-your-static-assets/">other important assets</a>) in a separate file on the root domain <a href="https://www.jonathanklein.net/2014/02/revisiting-cookieless-domain.html">has benefits</a>, sometimes even more than inlining, due to caching. Chrome speculatively opens a second HTTP connection to the root domain when requesting the page, which removes the need for a TCP connection to fetch this CSS. That means that you could create a set of <em>critical</em>-CSS-files (e.g. <em>critical-homepage.css</em>, <em>critical-product-page.css</em> etc.) and serve them from your root, without having to inline them. (<em>thanks, Philip!</em>)</p>

<p>A word of caution: with HTTP/2, critical CSS could be stored in a separate CSS file and delivered via a <a href="https://www.filamentgroup.com/lab/modernizing-delivery.html">server push</a> without bloating the HTML. The catch is that server pushing was <a href="https://jakearchibald.com/2017/h2-push-tougher-than-i-thought/">troublesome</a> with many gotchas and race conditions across browsers. It was never supported consistently and had some caching issues (see slide 114 onwards of <a href="https://www.slideshare.net/Fastly/http2-what-no-one-is-telling-you">Hooman Beheshti’s presentation</a>).</p>

<p>The effect could, in fact, <a href="https://jakearchibald.com/2017/h2-push-tougher-than-i-thought/">be negative</a> and bloat the network buffers, preventing genuine frames in the document from being delivered. So it wasn’t very surprising that for the time being, <a href="https://groups.google.com/a/chromium.org/g/blink-dev/c/K3rYLvmQUBY/m/vOWBKZGoAQAJ">Chrome is planning to remove support for Server Push</a>.</p>

<!-- <p>A few gotchas to keep in mind: unlike <code>preload</code> that can trigger preload from any domain, you can only push resources from your own domain or domains you are authoritative for. It can be initiated as soon as the server gets the very first request from the client. Server-pushed resources land in the Push cache and are removed when the connection is terminated. However, since an HTTP/2 connection can be re-used across multiple tabs, pushed resources can be claimed by requests from other tabs as well. <a href="https://jakearchibald.com/2017/h2-push-tougher-than-i-thought/#multiple-pages-can-use-the-same-http2-connection">We can’t depend on it though</a>, especially in Safari and Edge (<em>thanks, Inian, Barry!</em>).</p> -->

<!-- <p>At the moment, there is no simple way for the server to know if pushed resources are already in <a href="https://blog.yoav.ws/tale-of-four-caches/">one of the user’s caches</a>, so resources will keep being pushed with every user’s visit. You may then need to create a <a href="https://css-tricks.com/cache-aware-server-push/">cache-aware HTTP/2 server push mechanism</a>. If fetched, you could try to get them from a cache based on the index of what’s already in the cache, avoiding secondary server pushes altogether.</p> -->

<!-- <p>For a while, <a href="https://calendar.perfplanet.com/2016/cache-digests-http2-server-push/">the <code>cache-digest</code> specification</a> was considered to help negate the need to manually build such "cache-aware" servers, basically declaring a new frame type in HTTP/2 to communicate what’s already in the cache for that hostname. However, <a href="https://lists.w3.org/Archives/Public/ietf-http-wg/2019JanMar/0033.html"><code>cache-digest</code> spec was abandoned</a>, so the solution isn’t quite in sight yet. (<em>thanks, Barry!</em>).</p> -->

<!-- <p>For dynamic content, when a server needs some time to generate a response, the browser isn’t able to make any requests since it’s not aware of any sub-resources that the page might reference. For that case, we can warm up the connection and increase the TCP congestion window size, so that future requests can be completed faster. Also, all inlined assets are usually good candidates for server pushing. In fact, Inian Parameshwaran <a href="https://dexecure.com/blog/http2-push-vs-http-preload/">did remarkable research comparing HTTP/2 Push vs. HTTP Preload</a>, and it’s a fantastic read with all the details you might need.</p> -->

<!-- <p>Bottom line: As Sam Saccone <a href="https://medium.com/@samccone/performance-futures-bundling-281543d9a0d5">noted</a>, <code>preload</code> is good for moving the start download time of an asset closer to the initial request, while Server Push is good for cutting out a full RTT (<a href="https://blog.yoav.ws/being_pushy/">or more</a>, depending on your server think time) &mdash; if you have a service worker to prevent unnecessary pushing, that is.</p></li> -->

<li><strong>Experiment with regrouping your CSS rules.</strong><br />We’ve got used to critical CSS, but there are a few optimizations that could go beyond that. Harry Roberts conducted a <a href="https://csswizardry.com/2018/11/css-and-network-performance/">remarkable research</a> with quite surprising results. For example, it might be a good idea to <strong>split the main CSS file out</strong> into its individual media queries. That way, the browser will retrieve critical CSS with high priority, and everything else with low priority &mdash; completely off the critical path.</p>

<p>Also, avoid placing <code>&lt;link rel="stylesheet" /&gt;</code> before <code>async</code> snippets. If scripts don’t depend on stylesheets, consider placing blocking scripts above blocking  styles. If they do, split that JavaScript in two and load it either side of your CSS.</p>

<p>Scott Jehl solved another interesting problem by <a href="https://www.filamentgroup.com/lab/inlining-cache.html">caching an inlined CSS file with a service worker</a>, a common problem familiar if you’re using critical CSS. Basically, we add an ID attribute onto the <code>style</code> element so that it’s easy to find it using JavaScript, then a small piece of JavaScript finds that CSS and uses the Cache API to store it in a local browser cache (with a content type of <code>text/css</code>) for use on subsequent pages. To avoid inlining on subsequent pages and instead reference the cached assets externally, we then set a cookie on the first visit to a site. <em>Voilà!</em></p>

<p>It’s worth noting that <a href="https://calendar.perfplanet.com/2019/the-unseen-performance-costs-of-css-in-js-in-react-apps/">dynamic styling can be expensive</a>, too, but usually only in cases when you rely on hundreds of concurrently rendered composed components. So if you’re using CSS-in-JS, make sure that your CSS-in-JS library optimizes the execution when your CSS has no dependencies on theme or props, and <strong>don’t over-compose styled components</strong>. Aggelos Arvanitakis <a href="https://calendar.perfplanet.com/2019/the-unseen-performance-costs-of-css-in-js-in-react-apps/">shares more insights into performance costs of CSS-in-JS</a>.</p>
</li>
<li><strong>Do you stream responses?</strong><br />Often forgotten and neglected, <a href="https://streams.spec.whatwg.org/">streams</a> provide an interface for reading or writing asynchronous chunks of data, only a subset of which might be available in memory at any given time. Basically, they allow the page that made the original request to start working with the response as soon as the first chunk of data is available, and use parsers that are optimized for streaming to progressively display the content.

<p>We could create one stream from multiple sources. For example, instead of serving an empty UI shell and letting JavaScript populate it, you can let the service worker <strong>construct a stream</strong> where the shell comes from a cache, but the body comes from the network. As Jeff Posnick <a href="https://developers.google.com/web/updates/2016/06/sw-readablestreams">noted</a>, if your web app is powered by a CMS that server-renders HTML by stitching together partial templates, that model translates directly into using streaming responses, with the templating logic replicated in the service worker instead of your server. Jake Archibald’s <a href="https://jakearchibald.com/2016/streams-ftw/">The Year of Web Streams</a> article highlights how exactly you could build it. Performance boost is <a href="https://www.youtube.com/watch?v=Cjo9iq8k-bc">quite noticeable</a>.</p>

<p>One important advantage of streaming the entire HTML response is that HTML rendered during the initial navigation request can take full advantage of the browser’s streaming HTML parser. Chunks of HTML that are inserted into a document after the page has loaded (as is common with content populated via JavaScript) can’t take advantage of this optimization.</p>

<p>Browser support? <a href="https://caniuse.com/#feat=streams">Still getting there</a> with partial support in Chrome, Firefox, Safari and Edge supporting the API and Service Workers being <a href="https://caniuse.com/#feat=serviceworkers">supported in all modern browsers</a>. And if you feel adventurous again, you can check an experimental implementation of <a href="https://web.dev/fetch-upload-streaming/">streaming requests</a>, which allows you to start sending the request while still generating the body. Available in Chrome 85.</p></li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0d3b406-93e8-4ef4-a407-c2453651a02a/save-data-usage-android-chrome.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0d3b406-93e8-4ef4-a407-c2453651a02a/save-data-usage-android-chrome.jpg" sizes="100vw" caption="18% of global Android Chrome users have Lite Mode enabled (aka Save-Data), according to <a href='https://twitter.com/colinbendell/status/1265675813204172810'>Cloudinary research</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0d3b406-93e8-4ef4-a407-c2453651a02a/save-data-usage-android-chrome.jpg'>Large preview</a>)" alt="An image summarizing the save-data usage on Android Chrome and the average img hits or sessions discovered by Cloudinary research in November 2019 and April 2020" >}}

<ol class="continue">

<li><strong>Consider making your components connection-aware.</strong><br/>Data can be <a href="https://whatdoesmysitecost.com/">expensive</a> and with growing payload, we need to respect users who choose to opt into data savings while accessing our sites or apps. The <a href="https://simonhearne.com/2020/save-data/">Save-Data client hint request header</a> allows us to customize the application and the payload to cost- and performance-constrained users.</p>

<p>In fact, you could <a href="https://css-tricks.com/help-users-save-data/">rewrite requests for high DPI images to low DPI images</a>, remove web fonts, fancy parallax effects, preview thumbnails and infinite scroll, turn off video autoplay, server pushes, reduce the number of displayed items and downgrade image quality, or even change how you <a href="https://dev.to/addyosmani/adaptive-serving-using-javascript-and-the-network-information-api-331p">deliver markup</a>. Tim Vereecke has published a very detailed article on <a href="https://calendar.perfplanet.com/2018/data-shaver-strategies/">data-s(h)aver strategies</a> featuring many options for data saving.

<p>Who is using <code>save-data</code>, you might be wondering? <a href="https://twitter.com/colinbendell/status/1265675813204172810">18% of global Android Chrome users have Lite Mode enabled</a> (with <code>Save-Data</code> on), and the number is <a href="https://twitter.com/addyosmani/status/1265677876608655361">likely to be higher</a>. According to Simon Hearne’s <a href="https://simonhearne.com/2020/save-data/">research</a>, the opt-in rate is highest on cheaper devices, but there are plenty of outliers. For example: users in Canada have an opt-in rate of over 34% (compared to ~7% in the US) and users on the latest Samsung flagship have an opt-in rate of almost 18% globally.</p>

<p>With the <code>Save-Data</code> mode on, Chrome Mobile will provide an optimized experience, i.e. a <strong>proxied web experience with deferred scripts</strong>, enforced <code>font-display: swap</code> and enforced lazy loading. It’s just more sensible to build the experience on your own rather than relying on the browser to make these optimizations.</p>

<p>The header is currently supported only in Chromium, on the Android version of Chrome or via the Data Saver extension on a desktop device. Finally, you can also use the <a href="https://googlechrome.github.io/samples/network-information/">Network Information API</a> to deliver <a href="https://umaar.com/dev-tips/242-considerate-javascript/">costly JavaScript modules</a>, high-resolution images and videos based on the network type. Network Information API and specifically <code>navigator.connection.effectiveType</code> use <code>RTT</code>, <code>downlink</code>, <code>effectiveType</code> values (and a few <a href="https://wicg.github.io/netinfo/">others</a>) to provide a representation of the connection and the data that users can handle.</p>

<p>In this context, Max Böck speaks of <a href="https://mxb.at/blog/connection-aware-components/">connection-aware components</a> and Addy Osmani speaks of <a href="https://youtu.be/puUPpVrIRkc?t=975">adaptive module serving</a>. For example, with React, we could write a component that renders differently for different connection types. As Max suggested, a <code>&lt;Media /&gt;</code> component in a news article might output:</p>

<ul>
  <li><code>Offline</code>: a placeholder with <code>alt</code> text,</li>
  <li><code>2G</code> / <code>save-data</code> mode: a low-resolution image,</li>
  <li><code>3G</code> on non-Retina screen: a mid-resolution image,</li>
  <li><code>3G</code> on Retina screens: high-res Retina image,</li>
  <li><code>4G</code>: an HD video.</li>
</ul>

<p>Dean Hume provides a <a href="https://deanhume.com/dynamic-resources-using-the-network-information-api-and-service-workers/">practical implementation of a similar logic</a> using a service worker. For a video, we could display a video poster by default, and then display the "Play" icon as well as the video player shell, meta-data of the video etc. on better connections. As a fallback for non-supporting browsers, we could <a href="https://benrobertson.io/front-end/lazy-load-connection-speed">listen to <code>canplaythrough</code> event</a> and use <code>Promise.race()</code> to timeout the source loading if the <code>canplaythrough</code> event doesn’t fire within 2 seconds.</p>

<p>If you want to dive in a bit deeper, here are a couple of resources to get started:</p>

<ul>
<li>Addy Osmani <a href="https://www.youtube.com/watch?v=puUPpVrIRkc&t=488s">shows how to implement adaptive serving in React</a>.</li>
<li><a href="https://github.com/GoogleChromeLabs/react-adaptive-hooks">React Adaptive Loading Hooks &amp; Utilities</a> provides code snippets for React,</li>
<li>Netanel Basel explores <a href="https://netbasal.com/connection-aware-components-in-angular-3a66bb0bab6f">Connection-Aware Components in Angular</a>,</li>
<li>Theodore Vorilas shares how <a href="https://dev.to/vorillaz/serving-adaptive-components-using-the-network-information-api-lbo">Serving Adaptive Components Using the Network Information API in Vue</a> works.</li>
<li>Umar Hansa show <a href="https://umaar.com/dev-tips/242-considerate-javascript/">how to selectively download/execute expensive JavaScript</a>.</li>
</ul>
</li>
<li><strong>Consider making your components device memory-aware.</strong><br />Network connection gives us only one perspective at the context of the user though. Going further, you could also dynamically <a href="https://calendar.perfplanet.com/2018/dynamic-resources-browser-network-device-memory/">adjust resources based on available device memory</a>, with the <a href="https://developers.google.com/web/updates/2017/12/device-memory">Device Memory API</a>. <code>navigator.deviceMemory</code> returns how much RAM the device has in gigabytes, rounded down to the nearest power of two. The API also features a Client Hints Header, <code>Device-Memory</code>, that reports the same value.</p>

<p><strong>Bonus</strong>: <em>Umar Hansa <a href="https://twitter.com/umaar/status/1206707408506105858">shows how to defer expensive scripts</a> with dynamic imports to change the experience based on device memory, network connectivity and <a href="https://developer.mozilla.org/en-US/docs/Web/API/NavigatorConcurrentHardware/hardwareConcurrency">hardware concurrency</a>.</em></p>
</li>
</ol>

{{< rimg breakout="true" href="https://medium.com/reloading/preload-prefetch-and-priorities-in-chrome-776165961bbf" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2dbec5f-c859-4aa6-b10b-f017be63fc3b/resources-in-chrome.jpeg" sizes="100vw" caption="A break-down showing how different resources are prioritized in Blink as of Chrome 46 and beyond. (Image credit: <a href='https://medium.com/reloading/preload-prefetch-and-priorities-in-chrome-776165961bbf'>Addy Osmani</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2dbec5f-c859-4aa6-b10b-f017be63fc3b/resources-in-chrome.jpeg'>Large preview</a>)" alt="A break-down showing how different resources are prioritized in Blink as of Chrome 46 and beyond" >}}

<ol class="continue">
<li><strong>Warm up the connection to speed up delivery.</strong><br />Use <a href="https://w3c.github.io/resource-hints">resource hints</a> to save time on <a href="https://caniuse.com/#search=dns-prefetch"><code>dns-prefetch</code></a> (which performs a DNS lookup in the background), <a href="https://www.caniuse.com/#search=preconnect"><code>preconnect</code></a> (which asks the browser to start the connection handshake (DNS, TCP, TLS) in the background), <a href="https://caniuse.com/#search=prefetch"><code>prefetch</code></a> (which asks the browser to request a resource) and <a href="https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/"><code>preload</code></a> (which prefetches resources without executing them, among other things). <a href="https://caniuse.com/?search=preload">Well supported</a> in modern browsers, with support <a href="https://twitter.com/__jakub_g/status/1333711930004025346">coming to Firefox soon</a>.

<p>Remember <a href="https://www.w3.org/TR/resource-hints/#dfn-prerender"><code>prerender</code></a></a>? The resource hint used to prompt browser to build out the entire page in the background for next navigation. The implementations issues <a href="https://vimeo.com/356819848#t=1632s">were quite problematic</a>, ranging from a huge memory footprint and bandwidth usage to multiple registered analytics hits and ad impressions.</p>

<p>Unsurprinsingly, it was deprecated, but the Chrome team has brought it back as <a href="https://developers.google.com/web/updates/2018/07/nostate-prefetch">NoState Prefetch mechanism</a>. In fact, Chrome treats the <code>prerender</code> hint as a NoState Prefetch instead, so we can still use it today. As Katie Hempenius explains in that article, "like prerendering, <strong>NoState Prefetch fetches resources in advance</strong>; but unlike prerendering, it <strong>does not execute JavaScript</strong> or render any part of the page in advance."</p>

<p>NoState Prefetch only uses ~45MiB of memory and subresources that are fetched will be fetched with an <code>IDLE</code> Net Priority. Since Chrome 69, NoState Prefetch adds the header <em>Purpose: Prefetch</em> to all requests in order to make them distinguishable from normal browsing.</p>

<p>Also, watch out for <a href="https://github.com/jeremyroman/alternate-loading-modes">prerendering alternatives</a> and <a href="https://github.com/WICG/portals/blob/master/README.md">portals</a>, a new effort toward privacy-conscious prerendering, which will provide the inset <code>preview</code> of the content for seamless navigations.</p>

<p>Using resource hints is probably <strong>the easiest way to boost performance</strong>, and <a href="https://medium.com/reloading/preload-prefetch-and-priorities-in-chrome-776165961bbf">it works well indeed</a>. When to use what? As Addy Osmani <a href="https://medium.com/reloading/preload-prefetch-and-priorities-in-chrome-776165961bbf">has explained</a>, it’s reasonable to preload resources that we know are very likely to be used on the current page and for future navigations across multiple navigation boundaries, e.g. Webpack bundles needed for pages the user hasn’t visited yet.</p>

<p>Addy’s article on <a href="https://medium.com/reloading/preload-prefetch-and-priorities-in-chrome-776165961bbf">"Loading Priorities in Chrome"</a> shows how <em>exactly</em> Chrome interprets resource hints, so once you’ve decided which assets are critical for rendering, you can assign high priority to them. To see how your requests are prioritized, you can enable a "priority" column in the Chrome DevTools network request table (as well as Safari).</p>

<p>Most of the time these days, we’ll be using <strong>at least</strong> <code>preconnect</code> and <code>dns-prefetch</code>, and we’ll be cautious with using <code>prefetch</code>, <code>preload</code> and <code>prerender</code>. Note that even with <code>preconnect</code> and <code>dns-prefetch</code>, the browser has a limit on the number of hosts it will look up/connect to in parallel, so it’s a safe bet to order them based on priority (<em>thanks Philip Tellis!</em>).</p>

<p>Since <strong>fonts</strong> usually are important assets on a page, sometimes it’s a good idea to <a href="https://css-tricks.com/the-critical-request/#article-header-id-2">request the browser to download critical fonts with</a> <a href="https://css-tricks.com/the-critical-request/#article-header-id-2"><code>preload</code></a>. However, double check if it actually helps performance as there is a <a href="https://andydavies.me/blog/2019/02/12/preloading-fonts-and-the-puzzle-of-priorities/">puzzle of priorities when preloading fonts</a>: as <code>preload</code> is seen as high importance, it can leapfrog even more critical resources like critical CSS. (<em>thanks, Barry!</em>)</p>

<pre class="language-html">
<code>&lt;!-- Loading two rendering-critical fonts, but not all their weights. --&gt;
&lt;!--
crossorigin="anonymous" is required due to CORS.
Without it, preloaded fonts will be ignored.
https://github.com/w3c/preload/issues/32
via https://twitter.com/iamakulov/status/1275790151642423303
--&gt;
&lt;link rel="preload" as="font"
      href="Elena-Regular.woff2"
      type="font/woff2"
      crossorigin="anonymous"
      media="only screen and (min-width: 48rem)" /&gt;
&lt;link rel="preload" as="font"
      href="Mija-Bold.woff2"
      type="font/woff2"
      crossorigin="anonymous"
      media="only screen and (min-width: 48rem)" /&gt;
</code>
</pre>

<p>Since <code>&lt;link rel="preload"&gt;</code> accepts a <code>media</code> attribute, you could choose to <a href="https://css-tricks.com/the-critical-request/#article-header-id-3">selectively download resources</a> based on <code>@media</code> query rules, as shown above.</p>

<p>Furthermore, we can use <code>imagesrcset</code> and <code>imagesizes</code> attributes to <a href="https://addyosmani.com/blog/preload-hero-images/">preload late-discovered hero images faster</a>, or any images that are loaded via JavaScript, e.g. movie posters:</p>

<pre class="language-html">
<code>&lt;!-- Addy Osmani. https://addyosmani.com/blog/preload-hero-images/ --&gt;
&lt;link rel="preload" as="image"
     href="poster.jpg"
     imagesrcset="
        poster_400px.jpg 400w,
        poster_800px.jpg 800w,
        poster_1600px.jpg 1600w"
    imagesizes="50vw"&gt;
</code>
</pre>

<p>We can also <strong>preload the JSON</strong> as <em>fetch</em></strong>, so it’s discovered before JavaScript gets to request it:</p>

<pre class="language-html">
<code>&lt;!-- Addy Osmani. https://addyosmani.com/blog/preload-hero-images/ --&gt;
&lt;link rel="preload" as="fetch" href="foo.com/api/movies.json" crossorigin&gt;
</code></pre>

<p>We could also <a href="https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/#dynamic-loading-without-execution">load JavaScript dynamically</a>, effectively for lazy execution of the script.</p>

<pre class="language-javascript">
<code>/* Adding a preload hint to the head */
var preload = document.createElement("link");
link.href = "myscript.js";
link.rel = "preload";
link.as = "script";
document.head.appendChild(link);

/* Injecting a script when we want it to execute */
var script = document.createElement("script");
script.src = "myscript.js";
document.body.appendChild(script);
</code></pre>

<p>A few <a href="https://dexecure.com/blog/http2-push-vs-http-preload/">gotchas to keep in mind</a>: <code>preload</code> is good for <a href="https://www.youtube.com/watch?v=RWLzUnESylc">moving the start download time of an asset</a> closer to the initial request, but preloaded assets land in the <strong>memory cache</strong> which is tied to the page making the request. <code>preload</code> plays well with the HTTP cache: a network request is never sent if the item is already there in the HTTP cache.</p>

<p>Hence, it’s useful for late-discovered resources, hero images loaded via <code>background-image</code>, inlining critical CSS (or JavaScript) and pre-loading the rest of the CSS (or JavaScript).</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/354f16f7-95de-4aa8-accb-83538a5049ed/preload-late-images-js.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/354f16f7-95de-4aa8-accb-83538a5049ed/preload-late-images-js.jpg" sizes="100vw" caption="Preload important images early; no need to wait on JavaScript to discover them. (Image credit: “<a href='https://addyosmani.com/blog/preload-hero-images/'>Preload Late-Discovered Hero Images Faster</a>” by Addy Osmani) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/354f16f7-95de-4aa8-accb-83538a5049ed/preload-late-images-js.jpg'>Large preview</a>)" alt="An example using the cover of the Greyhound movie starring Tom Hanks to show that preloaded images load earlier as there is no need to wait on JavaScript to discover" >}}

<p>A <code>preload</code> tag can initiate a preload only after the browser has received the HTML from the server and the lookahead parser has found the <code>preload</code> tag. Preloading via the HTTP header could be a bit faster since we don’t to wait for the browser to parse the HTML to start the request (it’s <a href="https://twitter.com/yoavweiss/status/1151586733177352192?s=20">debated</a> though).</p>

<p><a href="https://www.fastly.com/blog/faster-websites-early-priority-hints">Early Hints</a> will help even further, enabling preload to kick in even before the response headers for the HTML are sent (on the roadmap in <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=671310">Chromium</a>, <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1407355">Firefox</a>). Plus, <a href="https://github.com/WICG/priority-hints">Priority Hints</a> will help us indicate loading priorities for scripts.</p>

<p><strong>Beware</strong>: if you’re using <code>preload</code>, <code>as</code> <strong>must</strong> be defined or <a href="https://twitter.com/yoavweiss/status/873077451143774209">nothing loads</a>, plus <a href="https://medium.com/reloading/preload-prefetch-and-priorities-in-chrome-776165961bbf">preloaded fonts without the</a> <a href="https://medium.com/reloading/preload-prefetch-and-priorities-in-chrome-776165961bbf"><code>crossorigin</code></a> <a href="https://medium.com/reloading/preload-prefetch-and-priorities-in-chrome-776165961bbf">attribute will double fetch</a>. If you’re using <code>prefetch</code>, beware of the <a href="https://timkadlec.com/remembers/2020-06-17-prefetching-at-this-age/"><code>Age</code> header issues in Firefox</a>.</p>
</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80b8c02e-701b-4700-8bcf-f88240a78a49/fcp-histogram-by-sw-status-1400w-57a170dca9.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80b8c02e-701b-4700-8bcf-f88240a78a49/fcp-histogram-by-sw-status-1400w-57a170dca9.png" sizes="100vw" caption="With a service worker, we can request just the bare minimum of data, and then transform that data into a full HTML document to improve FCP. (via <a href='https://philipwalton.com/articles/smaller-html-payloads-with-service-workers/'>Phil Walton</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80b8c02e-701b-4700-8bcf-f88240a78a49/fcp-histogram-by-sw-status-1400w-57a170dca9.png'>Large preview</a>)" alt="A graph showing first contentful paint (by server worker status) with count from 0 to 150 across a given period of time (in ms)" >}}

<ol class="continue">
<li><strong>Use service workers for caching and network fallbacks.</strong><br />No performance optimization over a network can be faster than a locally stored cache on a user’s machine (there are <a href="https://simonhearne.com/2020/network-faster-than-cache/">exceptions</a> though). If your website is running over HTTPS, we can <a href="https://github.com/lyzadanger/pragmatist-service-worker">cache static assets in a service worker cache</a> and store offline fallbacks (or even offline pages) and retrieve them from the user’s machine, rather than going to the network.

<p>As suggested by Phil Walton, with service workers, we can <a href="https://philipwalton.com/articles/smaller-html-payloads-with-service-workers/">send smaller HTML payloads</a> by programmatically generating our responses. A service worker can request just the bare minimum of data it needs from the server (e.g. an HTML content partial, a Markdown file, JSON data, etc.), and then it can <strong>programmatically transform</strong> that data into a full HTML document. So once a user visits a site and the service worker is installed, the user will never request a full HTML page again. <a href="https://philipwalton.com/articles/smaller-html-payloads-with-service-workers/">The performance impact can be quite impressive</a>.</p>

<p>Browser support? <a href="https://caniuse.com/#search=serviceworker">Service workers are widely supported</a> and the fallback is the network anyway. Does it <strong>help boost performance</strong>? <a href="https://developers.google.com/web/showcase/2016/service-worker-perf">Oh yes, it does</a>. And it’s getting better, e.g. with Background Fetch allowing background uploads/downloads via a service worker as well.</p>

<p>There are a number of use cases for a service worker. For example, you could <a href="https://una.im/save-offline/#%F0%9F%92%81">implement "Save for offline" feature</a>, <a href="https://bitsofco.de/handling-broken-images-with-service-worker/">handle broken images</a>, introduce <a href="https://www.loxodrome.io/post/tab-state-service-workers/">messaging between tabs</a> or <a href="https://medium.com/dev-channel/service-worker-caching-strategies-based-on-request-types-57411dd7652c">provide different caching strategies based on request types</a>. In general, a common reliable strategy is to store the app shell in the service worker’s cache along with a few critical pages, such as offline page, frontpage and anything else that might be important in your case.</p>

<p>There are a few gotchas to keep in mind though. With a service worker in place, we need to <a href="https://philna.sh/blog/2018/10/23/service-workers-beware-safaris-range-request/">beware range requests in Safari</a> (if you are using Workbox for a service worker it has a <a href="https://developers.google.com/web/tools/workbox/modules/workbox-range-requests">range request module</a>). If you ever stumbled upon <code>DOMException: Quota exceeded.</code> error in the browser console, then look into Gerardo’s article <a href="https://cloudfour.com/thinks/when-7-kb-equals-7-mb/">When 7KB equals 7MB</a>.</p>

<p>As Gerardo writes, “If you are building a progressive web app and are experiencing bloated cache storage when your service worker caches static assets served from CDNs, make sure the <a href="https://cloudfour.com/thinks/when-7-kb-equals-7-mb/#opaque-responses">proper CORS response header exists</a> for cross-origin resources, you <a href="https://cloudfour.com/thinks/when-7-kb-equals-7-mb/#should-opaque-responses-be-cached-at-all">do not cache opaque responses</a> with your service worker unintentionally, you <a href="https://cloudfour.com/thinks/when-7-kb-equals-7-mb/#opt-in-to-cors-mode">opt-in cross-origin image assets into CORS mode</a> by adding the <code>crossorigin</code> attribute to the <code>&lt;img&gt;</code> tag.”</p>

<p>There is plenty of <strong>great resources</strong> to get started with service workers:</p>
<ul>
<li><a href="https://web.dev/service-worker-mindset/">Service Worker Mindset</a>, which helps you understand how service workers work behind the scenes and things to understand when building one.</li>
<li>Chris Ferdinandi provides a <a href="https://gomakethings.com/series/service-workers/">great series of articles on service workers</a>, explaining how to create offline applications and covering a variety of scenarios, from saving recently viewed pages offline to setting an expiration date for items in a service worker cache.</p>
</li>
<li><a href="https://www.thecodeship.com/web-development/guide-service-worker-pitfalls-best-practices/">Service Worker Pitfalls and Best Practices</a>, with a few tips about the scope, delaying registering a service worker and service worker caching.</li>
<li>Great series by Ire Aderinokun on <a href="https://bitsofco.de/bitsofcode-pwa-part-1-offline-first-with-service-worker/">"Offline First" with Service Worker</a>, with a strategy on precaching the app shell.</li>
<li><a href="https://developers.google.com/web/fundamentals/primers/service-workers">Service Worker: An Introduction</a> with practical tips on how to use service worker for rich offline experiences, periodic background syncs and push notifications.</li>
<li>It's always worth referring to good ol' Jake Archibald’s <a href="https://jakearchibald.com/2014/offline-cookbook/">Offline Cookbook</a> with a number of recipes on how to bake your own service worker.</li>
<li><a href="https://developers.google.com/web/tools/workbox/">Workbox</a> is a set of service worker libraries built specifically for building progressive web apps.</li>
</ul>

</li>
<li><strong>Are you running servers workers on the CDN/Edge, e.g. for A/B testing?</strong><br />At this point, we are quite used to running service workers on the client, but with <a href="https://blog.cloudflare.com/introducing-cloudflare-workers/">CDNs implementing them on the server</a>, we could use them to tweak performance on the edge as well.</p>

<p>For example, in A/B tests, when HTML needs to vary its content for different users, we could <a href="https://www.filamentgroup.com/lab/servers-workers.html">use Service Workers on the CDN servers</a> to handle the logic. We could also <a href="https://twitter.com/patmeenan/status/1065567680298663937">stream HTML rewriting</a> to speed up sites that use Google Fonts.</p></li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4161d64c-521d-41fc-9eec-300dc766a412/pwa-timeseries-of-service-worker-installations-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4161d64c-521d-41fc-9eec-300dc766a412/pwa-timeseries-of-service-worker-installations-opt.png" sizes="100vw" caption="Timeseries of service worker installation. Only 0.87% of all desktop pages register a service worker, according to <a href='https://almanac.httparchive.org/en/2020/pwa'>Web Almanac</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4161d64c-521d-41fc-9eec-300dc766a412/pwa-timeseries-of-service-worker-installations-opt.png'>Large preview</a>)" alt="A graph showing Timeseries of service worker installations on desktop and mobile with percent of pages across time between January 2016 and July 2020" >}}

<ol class="continue">
<li><strong>Optimize rendering performance.</strong><br />Whenever the application is sluggish, it's noticeable right away. So we need to make sure that there is no lag when scrolling the page or when an element is animated, and that you’re consistently hitting 60 frames per second. If that’s not possible, then at least making the frames per second consistent is preferable to a mixed range of 60 to 15. Use CSS’ <a href="https://caniuse.com/#feat=will-change"><code>will-change</code></a> to inform the browser of which elements and properties will change.

<p>Whenever you are experiencing, <strong>debug unnecessary repaints</strong> in DevTools:</p>

<ul>
<li><a href="https://aerotwist.com/blog/my-performance-audit-workflow/#runtime-performance">Measure runtime rendering performance</a>. Check some <a href="https://medium.com/@marielgrace/how-to-analyze-runtime-performance-google-devtools-99fda64c09cb">useful tips on how to make sense of it</a>.</li>
<li>To get started, check Paul Lewis’ free <a href="https://www.udacity.com/course/browser-rendering-optimization--ud860">Udacity course on browser-rendering optimization</a> and Georgy Marchuk’s article on <a href="https://css-tricks.com/browser-painting-and-considerations-for-web-performance/">Browser painting and considerations for web performance</a>.</li>
<li><a href="https://twitter.com/iamakulov/status/1275782035655753729">Enable Paint Flashing</a> in "More tools → Rendering → Paint Flashing" in Firefox DevTools.</li>
<li>In React DevTools, <a href="https://twitter.com/iamakulov/status/1275783591293857792">check "Highlight updates"</a> and <a href="https://twitter.com/iamakulov/status/1275863444944756738">enable "Record why each component rendered"</a>,</li>
<li>You can also use <a href="https://github.com/welldone-software/why-did-you-render">Why Did You Render</a>, so when a component is re-rendered, a flash will notify you of the change.</li>
</ul>

<p>Are you using a Masonry layout? Keep in mind that might be able to <a href="https://www.smashingmagazine.com/native-css-masonry-layout-css-grid/">build a Masonry layout with CSS grid alone</a>, <a href="https://css-tricks.com/a-lightweight-masonry-solution/">very</a> <a href="https://www.bram.us/2020/05/04/css-grid-layout-module-level-2-masonry-layout/">soon</a>.</p>

<p>If you want to dive deeper into the topic, Nolan Lawson has shared <a href="https://nolanlawson.com/2018/09/25/accurately-measuring-layout-on-the-web/">tricks to accurately measure layout performance</a> in his article, and Jason Miller <a href="https://twitter.com/_developit/status/1081682550865752064">suggested alternative techniques, too</a>. We also have a lil' article by Sergey Chikuyonok on how to <a href="https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/">get GPU animation right</a>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c4093df-2d79-4a00-82ca-e19e0c439254/high-performance-animations.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c4093df-2d79-4a00-82ca-e19e0c439254/high-performance-animations.jpg" sizes="100vw" caption="Browsers can animate transform and opacity cheaply. <a href='https://csstriggers.com'>CSS Triggers</a> is useful for checking if CSS triggers re-layouts or reflows. (Image credit: <a href='https://twitter.com/addyosmani/status/1223916476610097154'>Addy Osmani</a>)(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c4093df-2d79-4a00-82ca-e19e0c439254/high-performance-animations.jpg'>Large preview</a>)" alt="High performance animations including Position, Scale, Rotation and Opacity" >}}

<p><strong>Note</strong>: changes to GPU-composited layers are the <a href="https://blog.algolia.com/performant-web-animations/">least expensive</a>, so if you can get away by triggering only compositing via <code>opacity</code> and <code>transform</code>, you’ll be on the right track. Anna Migas has provided a lot of practical advice in her talk on <a href="https://vimeo.com/302791098">Debugging UI Rendering Performance</a>, too. And to understand how to debug paint performance in DevTools, check <a href="https://www.youtube.com/watch?v=8-pkB2vGUKk">Umar’s Paint Performance audit video</a>.</p></li>

<li><strong>Have you optimized for perceived performance?</strong><br />While the sequence of how components appear on the page, and the strategy of how we serve assets to the browser matter, we shouldn’t underestimate the role of <a href="https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/">perceived performance</a>, too. The concept deals with psychological aspects of waiting, basically keeping customers busy or engaged while something else is happening. That’s where <a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/">perception management</a>, <a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/#preemptive-start">preemptive start</a>, <a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/#early-completion">early completion</a> and <a href="https://www.smashingmagazine.com/2015/12/performance-matters-part-3-tolerance-management/">tolerance management</a> come into play.

<p>What does it all mean? While loading assets, we can try to always be <strong>one step ahead</strong> of the customer, so the experience feels swift while there is quite a lot happening in the background. To keep the customer engaged, we can test <a href="https://twitter.com/lukew/status/665288063195594752">skeleton screens</a> (<a href="https://twitter.com/razvancaliman/status/734088764960690176">implementation demo</a>) instead of loading indicators, add transitions/animations and basically <a href="https://blog.stephaniewalter.fr/en/cheating-ux-perceived-performance-and-user-experience/">cheat the UX</a> when there is nothing more to optimize.</p>

<p>In their case study on <a href="https://farmdev.com/thoughts/108/the-art-of-ui-skeletons/">The Art of UI Skeletons</a>, Kumar McMillan shares some ideas and techniques on how to simulate dynamic lists, text, and the final screen, as well as how to consider <em>skeleton-thinking</em> with React.</p>

<p>Beware though: skeleton screens should be tested before deploying as some <a href="https://www.viget.com/articles/a-bone-to-pick-with-skeleton-screens/">tests showed that skeleton screens can perform the worst</a> by all metrics.</p>
</li>
<li><strong>Do you prevent layout shifts and repaints?</strong><br />In the realm of perceived performance probably one of the more disruptive experiences is <strong>layout shifting</strong>, or <em>reflows</em>, caused by rescaled images and videos, web fonts, injected ads or late-discovered scripts that populate components with actual content. As a result, a customer might start reading an article just to be interrupted by a layout jump above the reading area. The experience is often abrupt and quite disorienting: and that’s probably a case of loading priorities that need to be reconsidered.

<p>The community has developed a couple of techniques and workarounds to avoid reflows. In general, it’s a good idea to <strong>avoid inserting new content above existing content</strong>, unless it happens in response to a user interaction. Always <a href="https://www.youtube.com/watch?v=4-d_SoCHeWE">set width</a> <a href="https://www.smashingmagazine.com/2020/03/setting-height-width-images-important-again/">and height</a> attributes on images, so modern browsers allocate the box and reserve the space by default (Firefox, Chrome).</p>

<p>For both images or videos, we can use an <a href="https://css-tricks.com/preventing-content-reflow-from-lazy-loaded-images/">SVG placeholder</a> to reserve the display box in which the media will appear in. That means that the area will be reserved properly when you need to maintain its aspect ratio as well. We can also use placeholders, or fallback images for ads and dynamic content, as well as pre-allocate layout slots.</p>

<p>Instead of lazy-loading images with external scripts, consider using <a href="https://web.dev/native-lazy-loading/">native lazy-loading</a>, or <a href="https://www.smashingmagazine.com/2019/05/hybrid-lazy-loading-progressive-migration-native/">hybrid lazy-loading</a> when we load an external script only if native lazy-loading isn’t supported.</p>

<p>As mentioned above, always <a href="https://www.zachleat.com/web/comprehensive-webfonts/#fout-class">group web font repaints</a> and transition from <em>all</em> fallback fonts to <em>all</em> web fonts at once — just make sure that that switch isn’t too abrupt, by adjusting line-height and spacing between the fonts with <a href="https://meowni.ca/font-style-matcher/">font-style-matcher</a>.</p>

<p>To <strong>override font metrics</strong> for a fallback font to emulate a web font, we can use <a href="https://docs.google.com/document/d/1PW-5ML5hOZw7GczOargelPo6_8Zkuk2DXtgfOtJ59Eo/edit">@font-face descriptors to override font metrics</a> (<a href="https://jsfiddle.net/wpnjav2k/">demo</a>, enabled in Chrome 87). (Note that adjustments are complicated with complicated font stacks though.)</p>

<p>For late CSS, we can ensure that <strong>layout-critical CSS is inlined</strong> in the header of each template. Even further than that: for long pages, when the vertical scrollbar is added, it does <a href="https://twitter.com/paul_irish/status/1239586279924236288">shift the main content 16px to the left</a>. To display a scrollbar early, we can <a href="https://twitter.com/TimVereecke/status/1239454788116533248">add <code>overflow-y: scroll</code> on <code>html</code> </a> to enforce a scrollbar at first paint. The latter helps because <a href="https://twitter.com/addyosmani/status/1239592160141307905">scrollbars can cause non-trivial layout shifts</a> due to above the fold content reflowing when width changes. Should mostly happen on platforms with non-overlay scrollbars like Windows though. But: breaks <code>position: sticky</code> because those elements <a href="https://twitter.com/lfredolo/status/1240301405325361152">will never scroll out of the container</a>.</p>
<p>If you deal with <a href="https://twitter.com/rick_viscomi/status/1311853000542040066">headers that become fixed or sticky positioned</a> to the top of the page on scroll, reserve space for the header when it becomes pineed, e.g. with a placeholder element or <code>margin-top</code> on the content. An exception should be cookie consent banners <a href="https://twitter.com/g33konaut/status/1311709596847927296">that shouldn’t have impact on CLS</a>, but sometimes they do: it depends on the implementation. There are a few interesting strategies and takeaways in this Twitter thread.</p>
<p>For a tab component that might include various amount of texts, you can <a href="https://www.hsablonniere.com/prevent-layout-shifts-with-css-grid-stacks--qcj5jo/">prevent layout shifts with CSS grid stacks</a>. By placing the content of each tab in the same grid area, and hiding one of them at a time, we can ensure that the container always takes the height of the larger element, so no layout shifts will occur.</p>
<p>Ah, and of course, <a href="https://addyosmani.com/blog/infinite-scroll-without-layout-shifts/">infinite scrolling and "Load more" can cause layout shifts</a> as well if there is content below the list (e.g. footer). To improve CLS, reserve enough space for content that would be loaded in <em>before</em> the user scrolls to that part of the page, remove the footer or any DOM elements at the bottom of the page that may be pushed down by content loading in. Also, prefetch data and images for below-the-fold content so that by the time a user scrolls that far, it’s already there. You can use list virtualization libraries like <a href="https://github.com/bvaughn/react-window">react-window</a> to optimize long lists as well (<em>thanks, Addy Osmani!</em>).</p>

<p>To ensure that the impact of reflows is contained, measure the layout stability with the <a href="https://wicg.github.io/layout-instability/">Layout Instability API</a>. With it, you can calculate the <a href="https://web.dev/cls/">Cumulative Layout Shift</a> (<em>CLS</em>) score and include it as a requirement in your tests, so whenever a regression appears, you can track it and fix it.</p>

<p>To calculate the layout shift score, the browser looks at the viewport size and the movement of unstable elements in the viewport between two rendered frames. Ideally, the score would be close to <code>0</code>. There is a great guide by Milica Mihajlija and Philip Walton on <a href="https://web.dev/cls">what CLS is and how to measure it</a>. It’s a good starting point to measure and maintain perceived performance and avoid disruption, especially for business-critical tasks.</p>

<p><strong>Quick tip</strong>: to discover what caused a layout shift in DevTools, you can <a href="https://youtu.be/AQqFZ5t8uNc?t=454">explore layout shifts</a> under <em>"Experience"</em> in the Performance Panel.</p>

<p><strong>Bonus</strong>: if you want to reduce reflows and repaints, check Charis Theodoulou’s guide to <a href="https://medium.com/better-programming/web-performance-dom-reflow-76ac7c4d2d4f">Minimising DOM Reflow/Layout Thrashing</a> and Paul Irish’s list of <a href="https://gist.github.com/paulirish/5d52fb081b3570c81e3a">What forces layout / reflow</a> as well as <a href="https://csstriggers.com/">CSSTriggers.com</a>, a reference table on CSS properties that trigger layout, paint and compositing.</p>
</li>
</ol>

## Networking and HTTP/2

<ol class="continue">
<li><strong>Is OCSP stapling enabled?</strong><br />By <a href="https://www.digicert.com/enabling-ocsp-stapling.htm">enabling OCSP stapling on your server</a>, you can speed up your TLS handshakes. The Online Certificate Status Protocol (OCSP) was created as an alternative to the Certificate Revocation List (CRL) protocol. Both protocols are used to check whether an SSL certificate has been revoked.

<p>However, the OCSP protocol does not require the browser to spend time downloading and then searching a list for certificate information, hence reducing the time required for a handshake.</p>
</li>
<li><strong>Have you reduced the impact of SSL certificate revocation?</strong><br />In his article on <a href="https://simonhearne.com/2020/drop-ev-certs/">"The Performance Cost of EV Certificates"</a>, Simon Hearne provides a great overview of common certificates, and the impact a choice of a certificate may have on the overall performance.

<p>As Simon writes, in the world of HTTPS, there are a few types of certificate validation levels used to secure traffic:</p>
<ul>
<li><em>Domain Validation</em> (DV) validates that the certificate requestor owns the domain,</li>
<li><em>Organisation Validation</em> (OV) validates that an organisation owns the domain,</li>
<li><em>Extended Validation</em> (EV) validates that an organisation owns the domain, with rigorous validation.</li>
</ul>

<p>It’s important to note that all of these certificates are the <a href="https://nooshu.github.io/blog/2020/01/26/the-impact-of-ssl-certificate-revocation-on-web-performance/">same in terms of technology</a>; they only differ in information and properties provided in those certificates.</p>

<p><strong>EV certificates are expensive and time-consuming</strong> as they require a human to reviewing a certificate and ensuring its validity. DV certificates, on the other hand, are often provided for free &mdash; e.g. by
<a href="https://letsencrypt.org/how-it-works/">Let’s Encrypt</a> — an open, automated certificate authority that’s well integrated into many hosting providers and CDNs. In fact, at the time of writing, it powers <a href="https://www.abetterinternet.org/documents/2020-ISRG-Annual-Report.pdf">over 225 million websites</a> (PDF), although it makes for only <a href="https://telemetry.mozilla.org/new-pipeline/dist.html#!cumulative=0&end_date=2020-01-03&include_spill=0&keys=__none__!__none__!__none__&max_channel_version=beta%252F72&measure=CERT_EV_STATUS&min_channel_version=beta%252F71&processType=*&product=Firefox&sanitize=1&sort_by_value=0&sort_keys=submissions&start_date=2019-12-02&table=0&trim=1&use_submission_date=0">2.69% of the pages</a> (opened in Firefox).</p>

<p>So what’s the problem then? The issue is that <strong>EV certificates do not fully support OCSP stapling</strong> mentioned above. While stapling
allows the server to check with the Certificate Authority if the certificate has been revoked and then add ("staple") this information to the certificate, without stapling the client has to do all the work, resulting in unnecessary requests during the TLS negotiation. On poor connections, this might end up with noticeable performance costs (1000ms+).</p>

<p>EV certificates aren’t a great choice for web performance, and they can cause a much bigger impact on performance than DV certificates do. For optimal web performance, <a href="https://www.aaronpeters.nl/blog/ev-certificates-make-the-web-slow-and-unreliable/">always serve an OCSP stapled DV certificate</a>. They are also much cheaper than EV certificates and less hassle to acquire. Well, at least until <a href="https://blog.mozilla.org/security/2020/01/09/crlite-part-1-all-web-pki-revocations-compressed/">CRLite</a> is available.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26ff04ce-929d-49c3-bbf8-08ca71dd2d88/number-quic-handshakes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26ff04ce-929d-49c3-bbf8-08ca71dd2d88/number-quic-handshakes.png" sizes="100vw" caption="Compression matters: 40&ndash;43% of uncompressed certificate chains are too large to fit in a single QUIC flight of 3 UDP datagrams. (Image credit:) <a href='https://www.fastly.com/blog/quic-handshake-tls-compression-certificates-extension-study'>Fastly</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26ff04ce-929d-49c3-bbf8-08ca71dd2d88/number-quic-handshakes.png'>Large preview</a>)" alt="A graph showing the number of handshakes alongsite UDP datagrams in cases of plain, compressed or both" >}}

<p><strong>Note</strong>: With QUIC/HTTP/3 upon us, it’s worth noting that the <a href="https://www.fastly.com/blog/quic-handshake-tls-compression-certificates-extension-study">TLS certificate chain is the one variable-sized content</a> that dominates the byte count in the QUIC Handshake. The size varies between a few hundred byes and over 10 KB.</p>

<p>So keeping TLS certificates small <a href="https://twitter.com/programmingart/status/1229685029468561409">matters a lot on QUIC/HTTP/3</a>, as <a href="https://www.fastly.com/blog/quic-handshake-tls-compression-certificates-extension-study">large certificates will cause multiple handshakes</a>. Also, we need to make sure that the <a href="https://twitter.com/mcmanusducksong/status/1262452391208792066">certificates are compressed</a>, as otherwise certificate chains would be too large to fit in a single QUIC flight.</p>

<p>You can find <em>way</em> more detail and pointers to the problem and to the solutions on:</p>
<ul>
<li><a href="https://www.aaronpeters.nl/blog/ev-certificates-make-the-web-slow-and-unreliable/">EV Certificates Make The Web Slow and Unreliable</a> by Aaron Peters,</li>
<li><a href="https://nooshu.github.io/blog/2020/01/26/the-impact-of-ssl-certificate-revocation-on-web-performance/">The impact of SSL certificate revocation on web performance</a> by Matt Hobbs,</li>
<li><a href="https://simonhearne.com/2020/drop-ev-certs/">The Performance Cost of EV Certificates</a> by Simon Hearne,
</li>
<li><a href="https://www.fastly.com/blog/quic-handshake-tls-compression-certificates-extension-study">Does the QUIC handshake require compression to be fast?</a> by Patrick McManus.</li>
</ul>
</li>
<li><strong>Have you adopted IPv6 yet?</strong><br />Because we’re <a href="https://en.wikipedia.org/wiki/IPv4_address_exhaustion">running out of space with IPv4</a> and major mobile networks are adopting IPv6 rapidly (the US has <a href="https://www.google.com/intl/en/ipv6/statistics.html#tab=ipv6-adoption&amp;tab=ipv6-adoption">almost reached</a> a 50% IPv6 adoption threshold), it’s a good idea to <a href="https://www.paessler.com/blog/2016/04/08/monitoring-news/ask-the-expert-current-status-on-ipv6">update your DNS to IPv6</a> to stay bulletproof for the future. Just make sure that dual-stack support is provided across the network &mdash; it allows IPv6 and IPv4 to run simultaneously alongside each other. After all, IPv6 is not backwards-compatible. Also, <a href="https://www.cloudflare.com/ipv6/">studies show</a> that IPv6 made those websites 10 to 15% faster due to neighbor discovery (NDP) and route optimization.</li>
<li><strong>Make sure all assets run over HTTP/2 (or HTTP/3).</strong><br />With Google <a href="https://security.googleblog.com/2016/09/moving-towards-more-secure-web.html">pushing towards a more secure HTTPS web</a> over the last few years, a switch to <a href="https://http2.github.io/faq/">HTTP/2 environment</a> is definitely a good investment. In fact, according to Web Almanac, <a href="https://almanac.httparchive.org/en/2020/http2">64% of all requests are running over HTTP/2 already</a>.

<p>It’s important to understand that <a href="https://www.lucidchart.com/techblog/2019/04/10/why-turning-on-http2-was-a-mistake/">HTTP/2 isn’t perfect</a> and <a href="https://github.com/andydavies/http2-prioritization-issues">has prioritization issues</a>, but it’s <a href="https://caniuse.com/#search=http2">supported very well</a>; and, in most cases, you’re better off with it.</p>

<p>A word of caution: <a href="https://groups.google.com/a/chromium.org/g/blink-dev/c/K3rYLvmQUBY/m/vOWBKZGoAQAJ">HTTP/2 Server Push is being removed from Chrome</a>, so if your implementation relies on Server Push, you might need to revisit it. Instead, we might be looking at <a href="https://www.fastly.com/blog/beyond-server-push-experimenting-with-the-103-early-hints-status-code">Early Hints</a>, which are integrated as experiment in Fastly already.</p>

<p>If you’re still running on HTTP, the most time-consuming task will be to <a href="https://https.cio.gov/faq/">migrate to HTTPS first</a>, and then adjust your build process to cater for HTTP/2 multiplexing and parallelization. <a href="https://ldnwebperf.org/sessions/bringing-http-2-to-gov-uk/">Bringing HTTP/2 to Gov.uk</a> is a fantastic case study on doing just that, finding a way through CORS, SRI and WPT along the way. For the rest of this article, we assume that you’re either switching to or have already switched to HTTP/2.</p></li>
</ol>

{{< rimg breakout="true" href="https://almanac.httparchive.org/en/2020/http2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0005ffe6-5517-4f75-b770-5a547059515c/http2-h2-usage-opt.png" sizes="100vw" caption="64% of all requests are served over HTTP/2 in late 2020, according to Web Almanac &mdash; just 4 years after its formal standardization. (Image source: <a href='https://almanac.httparchive.org/en/2020/http2'>Web Almanac</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0005ffe6-5517-4f75-b770-5a547059515c/http2-h2-usage-opt.png'>Large preview</a>)" alt="A graph showing the timeseries of HTTP/2 requests in both desktop and mobile from January 2, 2016, until October 1, 2020" >}}

<ol class="continue">
<li><strong>Properly deploy HTTP/2.</strong><br />Again, <a href="https://www.youtube.com/watch?v=yURLTwZ3ehk">serving assets over HTTP/2</a> can benefit from a partial overhaul of how you’ve been serving assets so far. You’ll need to find a fine balance between packaging modules and loading many small modules in parallel. At the end of the day, still <a href="https://alistapart.com/article/the-best-request-is-no-request-revisited">the best request is no request</a>, however, the goal is to find a fine balance between quick first delivery of assets and caching.

<p>On the one hand, you might want to avoid concatenating assets altogether, instead of breaking down your entire interface into many small modules, compressing them as a part of the build process and loading them in parallel. A change in one file won’t require the entire style sheet or JavaScript to be re-downloaded. It also <a href="https://css-tricks.com/musings-on-http2-and-bundling/">minimizes parsing time</a> and keeps the payloads of individual pages low.</p>

<p>On the other hand, <a href="https://engineering.khanacademy.org/posts/js-packaging-http2.htm">packaging still matters</a>. By using many small scripts, <strong>overall compression will suffer</strong> and the <a href="https://simonhearne.com/2020/network-faster-than-cache/">cost of retrieving objects from the cache will increase</a>. The compression of a large package will benefit from dictionary reuse, whereas small separate packages will not. There’s standard work to address that, but it’s far out for now. Secondly, browsers have <strong>not yet been optimized</strong> for such workflows. For example, Chrome will trigger <a href="https://www.chromium.org/developers/design-documents/inter-process-communication">inter-process communications</a> (IPCs) linear to the number of resources, so including hundreds of resources will have browser runtime costs.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24d7fcb0-40c3-4ada-abb3-22b8524f9b2d/progressive-css-loading-opt.png" sizes="100vw" caption="To achieve best results with HTTP/2, consider to <a href='https://jakearchibald.com/2016/link-in-body/'>load CSS progressively</a>, as suggested by Chrome’s Jake Archibald." alt="HTML code using progressive CSS loading" >}}

<p>Still, you can try to <a href="https://jakearchibald.com/2016/link-in-body/">load CSS progressively</a>. In fact, in-body CSS <a href="https://twitter.com/patmeenan/status/1037027969842208777">no longer blocks rendering for Chrome</a>. But <a href="https://twitter.com/csswizardry/status/1133867804380270592">there are some prioritization issues</a> so it’s not as straightforward, but worth experimenting with.</p>

<p>You could get away with <a href="https://daniel.haxx.se/blog/2016/08/18/http2-connection-coalescing/">HTTP/2 connection coalescing</a>, which allows you to use domain sharding while benefiting from HTTP/2, but achieving this in practice is difficult, and in general, it’s not considered to be good practice. Also, <a href="https://nooshu.github.io/blog/2019/12/17/http2-and-sri-dont-always-get-on/">HTTP/2 and Subresource Integrity don’t always get on</a>.</p>

<p>What to do? Well, if you’re running over HTTP/2, sending around <strong>6–10 packages</strong> seems like a decent compromise (and isn’t too bad for legacy browsers). Experiment and measure to find the right balance for your website.</p></li>

<li><strong>Do we send all assets over a single HTTP/2 connection?</strong><br />One of the main advantages of HTTP/2 is that it allows us to send assets down the wire over a single connection. However, sometimes we might have done something wrong &mdash; e.g. have a CORS issue, or misconfigured the <code>crossorigin</code> attribute, so the browser would be forced to open a new connection.

<p>To check whether all requests use a single HTTP/2 connection, or something’s misconfigured, enable the "Connection ID" column in DevTools → Network. E.g., here, all requests share the same connection (286) &mdash; except manifest.json, which opens a separate one (451).</p>
</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bc3d810-23d9-49be-b508-f35977a7143c/devtools-3perf.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bc3d810-23d9-49be-b508-f35977a7143c/devtools-3perf.jpg" sizes="100vw" caption="All requests share the same HTTP/2 connection (286) &mdash; except manifest.json, which opens a separate one (451). <a href='https://twitter.com/iamakulov/status/1275849544341901319'>via iamakulov</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bc3d810-23d9-49be-b508-f35977a7143c/devtools-3perf.jpg'>Large preview</a>)" alt="A screenshot of DevTools open in the Chrome browser" >}}

<ol class="continue">
<li><strong>Do your servers and CDNs support HTTP/2?</strong><br />Different servers and CDNs (still) support HTTP/2 differently. Use <a href="https://cdncomparison.com/">CDN Comparison</a> to check your options, or quickly look up how your servers are performing and which features you can expect to be supported.

<p>Consult Pat Meenan’s incredible <a href="https://blog.cloudflare.com/http-2-prioritization-with-nginx/">research on HTTP/2 priorities</a> (<a href="https://www.youtube.com/watch?v=ct5MvtmL1NM">video</a>) and <a href="https://github.com/pmeenan/http2priorities">test server support for HTTP/2 prioritization</a>. According to Pat, it’s recommended to enable BBR congestion control and set <code>tcp_notsent_lowat</code> to 16KB for HTTP/2 prioritization to work reliably on Linux 4.9 kernels and later (<em>thanks, Yoav!</em>). Andy Davies did a similar research for HTTP/2 prioritization across browsers, <a href="https://github.com/andydavies/http2-prioritization-issues#cdns--cloud-hosting-services">CDNs and Cloud Hosting Services</a>.</p>

<p>While on it, double check if your kernel supports TCP BBR and enable it if possible. It’s currently used on Google Cloud Platform, <a href="https://aws.amazon.com/blogs/networking-and-content-delivery/tcp-bbr-congestion-control-with-amazon-cloudfront/">Amazon Cloudfront</a>, <a href="https://www.techrepublic.com/article/how-to-enable-tcp-bbr-to-improve-network-speed-on-linux/">Linux</a> (e.g. <a href="https://www.linuxbabe.com/ubuntu/enable-google-tcp-bbr-ubuntu">Ubuntu</a>).</p>
</li>

<li><strong>Is HPACK compression in use?</strong><br />If you’re using HTTP/2, double-check that your servers <a href="https://blog.cloudflare.com/hpack-the-silent-killer-feature-of-http-2/">implement HPACK compression</a> for HTTP response headers to reduce unnecessary overhead. Some HTTP/2 servers may not fully support the specification, with HPACK being an example. <a href="https://github.com/summerwind/h2spec">H2spec</a> is a great (if very technically detailed) <a href="https://twitter.com/tunetheweb/status/988196156697169920?s=20">tool to check that</a>. HPACK’s compression algorithm is quite <a href="https://www.mnot.net/blog/2018/11/27/header_compression">impressive</a>, and <a href="https://www.keycdn.com/blog/http2-hpack-compression/">it works</a>.</li>

<li><strong>Make sure the security on your server is bulletproof.</strong><br />All browser implementations of HTTP/2 run over TLS, so you will probably want to avoid security warnings or some elements on your page not working. Double-check that your <a href="https://securityheaders.io/">security headers are set properly</a>, <a href="https://www.smashingmagazine.com/2016/01/eliminating-known-security-vulnerabilities-with-snyk/">eliminate known vulnerabilities</a>, and <a href="https://www.ssllabs.com/ssltest/">check your HTTPS setup</a>.

<p>Also, make sure that all external plugins and tracking scripts are loaded via HTTPS, that cross-site scripting isn’t possible and that both <a href="https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet">HTTP Strict Transport Security headers</a> and <a href="https://content-security-policy.com/">Content Security Policy headers</a> are properly set.</p></li>

<li><strong>Do your servers and CDNs support HTTP/3?</strong><br />While HTTP/2 has brought a number of significant performance improvements to the web, it also left quite some area for improvement &mdash; especially <a href="https://youtu.be/SuSpghHP0uI?t=290">head-of-line blocking in TCP</a>, which was noticeable on a slow network with a significant packet loss. <a href="https://youtu.be/SuSpghHP0uI?t=290">HTTP/3 is solving these issues for good</a> (<a href="https://calendar.perfplanet.com/2020/head-of-line-blocking-in-quic-and-http-3-the-details/">article</a>).

<p>To address HTTP/2 issues, IETF, along with Google, Akamai and others, have been working on a new protocol that <a href="https://tools.ietf.org/html/draft-ietf-quic-http">has recently been standardized as HTTP/3</a>.</p>

<p>Robin Marx <a href="https://www.youtube.com/watch?v=SuSpghHP0uI&feature=youtu.be">has explained HTTP/3 very well</a>, and the following explanation is based on his explanation. In its core, HTTP/3 is <strong>very similar to HTTP/2</strong> in terms of features, but under the hood it works very differently. <a href="https://blog.cloudflare.com/http3-the-past-present-and-future/">HTTP/3 provides a number of improvements</a>: faster handshakes, better encryption, more reliable independent streams, better encryption and flow control. A noteable difference is that HTTP/3 uses QUIC as the transport layer, with QUIC packets encapsulated on top of UDP diagrams, rather than TCP.</p>

<p>QUIC fully integrates TLS 1.3 into the protocol, while in TCP it’s layered on top. In the typical TCP stack, we have a few round-trip times of overhead because TCP and TLS need to do their own separate handshakes, but with QUIC both of them can be <strong>combined and completed in just a single round trip</strong>. Since TLS 1.3 allows us to set up encryption keys for a consequent connection, from the second connection onward, we can already send and receive application layer data in the first round trip, which is called "0-RTT".</p>

<p>Also, header compression algorithm of HTTP/2 was entirely rewritten, along with its prioritization system. Plus, QUIC support <strong>connection migration</strong> from Wi-Fi to cellular network via connection IDs in the header of each QUIC packet. Most of the implementations are done in the user space, not kernel space (as it’s done with TCP), so we should be expecting the protocol to be evolving in the future.</p>

<p>Would it all make a big difference? <a href="https://twitter.com/FredKSchott/status/1313913507583193088">Probably yes</a>, especially having an impact on loading times on mobile, but also on how we serve assets to end users. While in HTTP/2, multiple requests share a connection, in HTTP/3 requests also share a connection but stream independently, so a dropped packet no longer impacts all requests, just the one stream.</p>

<p>That means that while with one large JavaScript bundle the processing of assets will be slowed down when one stream pauses, the impact will be less significant when multiple files stream in parallel (HTTP/3). So <strong>packaging still matters</strong>.</p>

<p>HTTP/3 is <a href="https://twitter.com/programmingart/status/1311656119450972161">still work in progress</a>. Chrome, Firefox and Safari have implementations <a href="https://caniuse.com/http3">already</a>. Some <a href="https://twitter.com/RobertHoeijmak1/status/1313936281039241216">CDNs support QUIC and HTTP/3 already</a>. In late 2020, <a href="https://twitter.com/FredKSchott/status/1313910775199612929">Chrome started deploying HTTP/3 and IETF QUIC</a>, and in fact all Google services (Google Analytics, YouTube etc.) are already running over HTTP/3. <a href="https://www.litespeedtech.com/products/litespeed-web-server">LiteSpeed Web Server</a> supports HTTP/3, but neither Apache, nginx or IIS support it yet, but it’s likely to change quickly in 2021.</p>

<!-- <p>Perhaps with this change we’ll also see more transport layer changes, such as <a href="https://www.fastly.com/blog/improve-http-structured-headers">structured header fields in HTTP</a> (<a href="https://www.youtube.com/watch?v=SkG6B-WvrTQ">video</a>).</p> -->

<p>The <strong>bottom line</strong>: if you have an option to use HTTP/3 on the server and on your CDN, it’s probably a very good idea to do so. The main benefit will come from fetching multiple objects simultaneously, especially on high-latency connections. We don’t know for sure yet as there isn’t much research done in that space, but <a href="https://blog.cloudflare.com/http-3-vs-http-2/">first results are very promising</a>.</p>

<p>If you want to dive more into the specifics and advantages of the protocol, here are some good starting points to check:</p>
<ul>
<li><a href="https://http3-explained.haxx.se/">HTTP/3 Explained</a>, a collaborative effort to document the HTTP/3 and the QUIC protocols. Available in various languages, also as PDF.</li>
<li><a href="https://cloudflare.tv/event/2EyYvt1zPHViDAxHMjpIdq">Leveling Up Web Performance With HTTP/3</a> with Daniel Stenberg.</li>
<li><a href="https://www.youtube.com/watch?v=SuSpghHP0uI&feature=youtu.be">An Academic’s Guide to QUIC</a> with Robin Marx introduces basic concepts of the QUIC and HTTP/3 protocols, explains how HTTP/3 handles head-of-line blocking and connection migration, and how HTTP/3 is designed to be evergreen (thanks, <a href="https://twitter.com/simonhearne/status/1330059997213052932"><em>Simon</em></a>!).</li>
<li>You can check if your server is running on HTTP/3 on <a href="https://http3check.net/">HTTP3Check.net</a>.</li>
</ul>

</li>
</ol>

## Testing And Monitoring

<ol class="continue">
<li><strong>Have you optimized your auditing workflow?</strong><br />It might not sound like a big deal, but having the right settings in place at your fingertips might save you quite a bit of time in testing. Consider using Tim Kadlec’s <a href="https://github.com/tkadlec/webpagetest-alfred-workflow">Alfred Workflow for WebPageTest</a> for submitting a test to the public instance of WebPageTest. In fact, WebPageTest has many obscure features, so take the time to learn <a href="https://nooshu.github.io/blog/2019/10/02/how-to-read-a-wpt-waterfall-chart/">how to read a WebPageTest Waterfall View chart</a> and <a href="https://nooshu.github.io/blog/2019/12/30/how-to-read-a-wpt-connection-view-chart/">how to read a WebPageTest Connection View chart</a> to diagnose and resolve performance issues faster.

<p>You could also <a href="https://calendar.perfplanet.com/2014/driving-webpagetest-from-a-google-docs-spreadsheet/">drive WebPageTest from a Google Spreadsheet</a> and <a href="https://web.dev/fast/using-lighthouse-ci-to-set-a-performance-budget">incorporate accessibility, performance and SEO scores</a> into your Travis setup with Lighthouse CI or <a href="https://twitter.com/addyosmani/statuses/1017655423099289600">straight into Webpack</a>.</p>

<p>Take a look at the recently released <a href="https://web.dev/autowebperf/">AutoWebPerf</a>, a modular tool that enables automatic gathering of performance data from multiple sources. For example, we could set a daily test on your critical pages to capture the field data from CrUX API and lab data from a Lighthouse report from PageSpeed Insights.</p>

<p>And if you need to debug something quickly but your build process seems to be remarkably slow, keep in mind that "<a href="https://slack.engineering/keep-webpack-fast-a-field-guide-for-better-build-performance-f56a5995e8f1">whitespace removal and symbol mangling accounts for 95% of the size reduction</a> in minified code for most JavaScript &mdash; not elaborate code transforms. You can simply disable compression to speed up Uglify builds by 3 to 4 times."</p></li>
</ol>

{{< rimg breakout="true" href="https://cdn-images-1.medium.com/max/1600/1*Y-1sdlIzFBRfEQPprzLnbA.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/705ed9b1-cd4d-4231-b808-ce8c2e72e070/review-required-checks-pr.png" sizes="100vw" caption="Integrating <a href='https://web.dev/fast/using-lighthouse-ci-to-set-a-performance-budget'>accessibility, performance and SEO scores</a> into your Travis setup with Lighthouse CI will highlight the performance impact of a new feature to all contributing developers. (<a href='https://cdn-images-1.medium.com/max/1600/1*Y-1sdlIzFBRfEQPprzLnbA.png'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/705ed9b1-cd4d-4231-b808-ce8c2e72e070/review-required-checks-pr.png'>Large preview</a>)" alt="A screenshot of GitHub’s Pull Request notification stating that review is required and that merging is blocked until checks have been successfully resolved" >}}

<ol class="continue">
<li><strong>Have you tested in proxy browsers and legacy browsers?</strong><br />Testing in Chrome and Firefox is not enough. Look into how your website works in proxy browsers and legacy browsers. UC Browser and Opera Mini, for instance, have a <a href="https://gs.statcounter.com/#mobile_browser-as-monthly-201511-201611">significant market share in Asia</a> (up to 35% in Asia). <a href="https://www.webworldwide.io/">Measure average Internet speed</a> in your countries of interest to avoid big surprises down the road. Test with network throttling, and emulate a high-DPI device. <a href="https://www.browserstack.com">BrowserStack</a> is fantastic for testing on <em>remote</em> real devices, and complement it with at least a few real devices in your office as well &mdash; it’s worth it.</li>
</ol>

<!-- <figure class="break-out"><a href="https://github.com/loadimpact/k6"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96fa3207-4fff-4b7b-bfa0-c115062d826a/demo-unit-perf-tests.gif" alt="A quick preview of k6 can be used directly in the terminal" /></a><figcaption><a href="https://github.com/loadimpact/k6">k6</a> allows you write unit tests-alike performance tests.</figcaption></figure> -->

<ol class="continue">
<li><strong>Have you tested the performance of your 404 pages?</strong><br />Normally we don’t think twice when it comes to 404 pages. After all, when a client requests a page that doesn’t exist on the server, the server is going to respond with a 404 status code and the associated 404 page. There isn’t that much to it, isn’t it?

<p>An important aspect of 404 responses is the actual <strong>response body size</strong> that is being sent to the browser. According to the <a href="https://nooshu.github.io/blog/2020/08/25/you-should-be-testing-your-404-pages-web-performance/">404 pages research by Matt Hobbs</a>, the vast majority of 404 responses are coming from missing favicons, WordPress uploads requests, broken JavaScript requests, manifest files as well as CSS and font files. Every time a client requests an asset that doesn’t exist, they’ll receive a 404 response — and often that response is huge.</p>

<p>Make sure to examine and optimize the <strong>caching strategy</strong> for your 404 pages. Our goal is to serve HTML to the browser only when it expects an HTML response, and return a small error payload for all other responses. According to Matt, "if we place a CDN in front of our origin, we have the chance to cache the 404 page response on the CDN. That’s useful because without it, hitting a 404 page could be used as a DoS attack vector, by forcing the origin server to respond to every 404 request rather than letting the CDN respond with a cached version."</p>

<p>Not only can 404 errors hurt your performance, but they can also cost in traffic, so it’s a good idea to include a 404 error page in your Lighthouse testing suite, and track its score over time.</p>
</li>

<li><strong>Have you tested the performance of your GDPR consent prompts?</strong><br />In times of GDPR and CCPA, it has become common to rely on third-parties to provide options for EU customers to opt in or opt out from tracking. However, like with any other third-party script, their performance can have a quite devastating impact on the entire performance effort.

<p>Of course, the actual consent is likely to change the impact of scripts on the overall performance, so, as Boris Schapira <a href="https://twitter.com/boostmarks/status/1255867669255000064">noted</a>, we might want to study a few different web performance profiles:</p>
<ul>
<li>Consent was entirely refused,</li>
<li>Consent was partially refused,</li>
<li>Consent was entirely given.</li>
<li>User hasn’t acted on consent prompt (or the prompt was blocked by a content blocker),</li>
</ul>

<p>Normally cookie consent prompts <a href="https://twitter.com/g33konaut/status/1311709596847927296">shouldn’t have an impact on CLS</a>, but <a href="https://twitter.com/rnebhwani/status/1315016813651128320">sometimes they do</a>, so consider using free and open source options <a href="https://www.osano.com/cookieconsent">Osano</a> or <a href="https://github.com/adriandmitroca/cookie-consent-box">cookie-consent-box</a>.</p>

<p>In general, it’s worth looking into the <strong>pop-up performance</strong> as you will need to determine the horizontal or vertical offset of the mouse event and correctly position the popup relatively to the anchor. Noam Rosenthal shares Wikimedia team’s learnings in the article <a href="https://techblog.wikimedia.org/2020/11/23/web-performance-case-study-wikipedia-page-previews/">Web performance case study: Wikipedia page previews</a> (also available as <a href="https://www.youtube.com/watch?v=sKvK3x9zdt0&feature=youtu.be">video</a> and <a href="https://docs.google.com/document/d/e/2PACX-1vR3QYysQvaeXyVD4ObCjqbhGq-yFnBXfBQAiWQrTImKOF2pnGuwLumqYMvmrPaWPHnGP9ENjwlcVNNT/pub">minutes</a>).</p>

</li>

<li><strong>Do you keep a performance diagnostics CSS?</strong><br />While we can include all kinds of checks to ensure that non-performant code gets deployed, often it's useful to get a quick idea of some of the low-hanging fruits that could be solved easily. For that, we could use Tim Kadlec's brilliant <a href="https://gist.github.com/tkadlec/683b26344cde774170b94c0fcf0088b4">Performance Diagnostics CSS</a> (inspired by <a href="https://twitter.com/csswizardry/status/1346477682544951296">Harry Roberts' snippet</a>which highlights lazy-loaded images, unsized images, legacy format images and synchronous scripts.

<p>E.g. you might want to ensure that <a href="https://twitter.com/csswizardry/status/1346477682544951296">no images above the fold are lazy loaded</a>. You can customize the snippet for you needs, e.g. to highlight web fonts that aren't used, or detect icon fonts. A great little tool to ensure that mistakes are visible during debugging, or just to audit the current project very quickly.</p>

<pre class="language-css">
<code>/* Performance Diagnostics CSS */
/* via Harry Roberts. https://twitter.com/csswizardry/status/1346477682544951296 */
img[loading=lazy] {
  outline: 10px solid red;
}
</code></pre>

</li>

</ol>

<ol class="continue">
<li><strong>Have you tested the impact on accessibility?</strong><br />When the browser starts to load a page, it builds a DOM, and if there is an assistive technology like a screen reader running, it also creates an accessibility tree. The screen reader then has to query the accessibility tree to retrieve the information and make it available to the user &mdash; sometimes by default, and sometimes on demand. And sometimes it takes time.

<p>When talking about fast Time to Interactive, usually we mean an indicator of how <em>soon</em> a user can interact with the page by clicking or tapping on links and buttons. The context is slightly different with screen readers. In that case, fast Time to Interactive means how much <em>time</em> passes by until the screen reader <strong>can announce navigation</strong> on a given page and a screen reader user can actually hit keyboard to interact.</p>
<p>Léonie Watson has given an <a href="https://www.youtube.com/watch?v=n1sXj9oAXFU">eye-opening talk on accessibility performance</a> and specifically the impact slow loading has on screen reader announcement delays. Screen readers are used to fast-paced announcements and quick navigation, and therefore might potentially be even less patient than sighted users.</p>
<p>Large pages and DOM manipulations with JavaScript will cause delays in screen reader announcements. A rather unexplored area that could use some attention and testing as screen readers are available on literally every platform (Jaws, NVDA, Voiceover, Narrator, Orca).</p></li>
<li><strong>Is continuous monitoring set up?</strong><br />Having a private instance of <a href="https://www.webpagetest.org/">WebPagetest</a> is always beneficial for quick and unlimited tests. However, a continuous monitoring tool &mdash; like <a href="https://www.sitespeed.io/">Sitespeed</a>, <a href="https://calibreapp.com/">Calibre</a> and <a href="https://speedcurve.com/">SpeedCurve</a> &mdash; with automatic alerts will give you a more detailed picture of your performance. Set your own user-timing marks to measure and monitor business-specific metrics. Also, consider adding <a href="https://calendar.perfplanet.com/2017/automating-web-performance-regression-alerts/">automated performance regression alerts</a> to monitor changes over time.</p>
<p>Look into using RUM-solutions to monitor changes in performance over time. For automated unit-test-alike load testing tools, you can use <a href="https://github.com/loadimpact/k6">k6</a> with its scripting API. Also, look into <a href="https://speedtracker.org">SpeedTracker</a>, <a href="https://github.com/GoogleChrome/lighthouse">Lighthouse</a> and <a href="https://calibreapp.com">Calibre</a>.</p></li>
</ol>

## Quick Wins

<p>This list is quite comprehensive, and completing all of the optimizations might take quite a while. So, if you had just 1 hour to get significant improvements, what would you do? Let’s boil it all down to <strong>17 low-hanging fruits</strong>. Obviously, before you start and once you finish, measure results, including Largest Contentful Paint and Time To Interactive on a 3G and cable connection.</p>

<ol>
  <li>Measure the real world experience and set appropriate goals. Aim to be at least 20% faster than your fastest competitor. Stay within Largest Contentful Paint &lt; 2.5s, a First Input Delay &lt; 100ms, Time to Interactive &lt; 5s on slow 3G, for repeat visits, TTI &lt; 2s. Optimize at least for First Contentful Paint and Time To Interactive.</li>
  <li>Optimize images with <a href="https://squoosh.app/">Squoosh</a>, <a href="https://github.com/mozilla/mozjpeg">mozjpeg</a>, <a href="https://github.com/google/guetzli">guetzli</a>, <a href="https://css-ig.net/pingo">pingo</a> and <a href="https://jakearchibald.github.io/svgomg/">SVGOMG</a>, and serve AVIF/WebP with an image CDN.</li>
  <li>Prepare critical CSS for your main templates, and inline them in the <code>&lt;head&gt;</code> of each template. For CSS/JS, operate within a critical file size <a href="https://infrequently.org/2017/10/can-you-afford-it-real-world-web-performance-budgets/">budget of max. 170KB gzipped</a> (0.7MB decompressed).</li>
  <li>Trim, optimize, defer and lazy-load scripts. Invest in the config of your bundler to remove redundancies and check lightweight alternatives.</li>
  <li>Always self-host your static assets and always prefer to self-host third-party assets. Limit the impact of third-party scripts. Use facades, load widgets on interaction and beware of anti-flicker snippets.</li>
  <li>Be selective when choosing a framework. For single-page-applications, identify critical pages and serve them statically, or at least prerender them, and use progressive hydration on component-level and import modules on interaction.</li>
  <li>Client-side rendering alone isn't a good choice for performance. Prerender if your pages don’t change much, and defer the booting of frameworks if you can. If possible, use streaming server-side rendering.</li>
  <li>Serve legacy code only to legacy browsers with <code>&lt;script type="module"&gt;</code> and <a href="https://philipwalton.com/articles/using-native-javascript-modules-in-production-today/">module/nomodule pattern</a>.</li>
  <li>Experiment with regrouping your CSS rules and test in-body CSS.</li>
  <li>Add resource hints to speed up delivery with faster <code>dns-lookup</code>, <code>preconnect</code>, <code>prefetch</code>, <code>preload</code> and <code>prerender</code>.</li>
  <li>Subset web fonts and load them asynchronously, and utilize <code>font-display</code> in CSS for fast first rendering.</li>
  <li>Check that HTTP cache headers and security headers are set properly.</li>
  <li>Enable Brotli compression on the server. (If that’s not possible, at least make sure that Gzip compression is enabled.)</li>
  <li>Enable TCP BBR congestion as long as your server is running on the Linux kernel version 4.9+.</li>
  <li>Enable OCSP stapling and IPv6 if possible. Always serve an OCSP stapled DV certificate.</li>
  <li>Enable HPACK compression for HTTP/2 and move to HTTP/3 if it's available.</li>
  <li>Cache assets such as fonts, styles, JavaScript and images in a service worker cache.</li>
</ol>

## Download The Checklist (PDF, Apple Pages)

<p>With this checklist in mind, you should be prepared for any kind of front-end performance project. Feel free to download the print-ready PDF of the checklist as well as an <strong>editable Apple Pages document</strong> to customize the checklist for your needs:</p>

<ul>
<li><a href="https://www.dropbox.com/s/34noajrbm324iai/performance-checklist-1.4.pdf?dl=0">Download the checklist PDF</a> (PDF, 166 KB)</li>
<li><a href="https://www.dropbox.com/s/ikuk5ikcxxv39uu/performance-checklist-1.4.pages?dl=0">Download the checklist in Apple Pages</a> (.pages, 275 KB)</li>
<li><a href="https://www.dropbox.com/scl/fi/s7ctdj89zd5zlvtt7dkhi/performance-checklist-1.4.docx?dl=0&rlkey=2xzs55e3kdg1jcraw5u1tnpl8">Download the checklist in MS Word</a> (.docx, 151 KB)</li>
</ul>

<p>If you need alternatives, you can also check the <a href="https://github.com/drublic/checklist">front-end checklist by Dan Rublic</a>, the "<a href="https://jonyablonski.com/designers-wpo-checklist/">Designer’s Web Performance Checklist</a>" by Jon Yablonski and the <a href="https://github.com/thedaviddias/Front-End-Performance-Checklist">FrontendChecklist</a>.</p>

## Off We Go!

<p>Some of the optimizations might be beyond the scope of your work or budget or might just be overkill given the legacy code you have to deal with. That’s fine! Use this checklist as a general (and hopefully comprehensive) guide, and create your own list of issues that apply to your context. But most importantly, test and measure your own projects to identify issues before optimizing. Happy performance results in 2021, everyone!</p>

<hr />

<p><em>A huge thanks to Guy Podjarny, Yoav Weiss, Addy Osmani, Artem Denysov, Denys Mishunov, Ilya Pukhalski, Jeremy Wagner, Colin Bendell, Mark Zeman, Patrick Meenan, Leonardo Losoviz, Andy Davies, Rachel Andrew, Anselm Hannemann, Barry Pollard, Patrick Hamann, Gideon Pyzer, Andy Davies, Maria Prosvernina, Tim Kadlec, Rey Bango, Matthias Ott, Peter Bowyer, Phil Walton, Mariana Peralta, Pepijn Senders, Mark Nottingham, Jean Pierre Vincent, Philipp Tellis, Ryan Townsend, Ingrid Bergman, Mohamed Hussain S. H., Jacob Groß, Tim Swalling, Bob Visser, Kev Adamson, Adir Amsalem, Aleksey Kulikov and Rodney Rehm for reviewing this article, as well as our fantastic community which has shared techniques and lessons learned from its work in performance optimization for everybody to use. You are truly smashing!</em></p>

{{< signature "il" >}}

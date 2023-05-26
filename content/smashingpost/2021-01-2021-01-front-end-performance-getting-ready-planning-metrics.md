---
title: 'Front-End Performance 2021: Planning And Metrics'
slug: front-end-performance-getting-ready-planning-metrics
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
  <li><strong>Getting Ready: Planning And Metrics</strong><br />Performance culture, Core Web Vitals, performance profiles, CrUX, Lighthouse, FID, TTI, CLS, devices.</li>
  <li><a href="/2021/01/front-end-performance-setting-realistic-goals/">Setting Realistic Goals</a><br />Performance budgets, performance goals, RAIL framework, 170KB/30KB budgets.</li>
  <li><a href="/2021/01/front-end-performance-defining-the-environment/">Defining The Environment</a><br />Choosing a framework, baseline performance cost, Webpack, dependencies, CDN, front-end architecture, CSR, SSR, CSR + SSR, static rendering, prerendering, PRPL pattern.</li>
  <li><a href="/2021/01/front-end-performance-assets-optimizations/">Assets Optimizations</a><br />Brotli, AVIF, WebP, responsive images, AV1, adaptive media loading, video compression, web fonts, Google fonts.</li>
  <li><a href="/2021/01/front-end-performance-build-optimizations/">Build Optimizations</a><br />JavaScript modules, module/nomodule pattern, tree-shaking, code-splitting, scope-hoisting, Webpack, differential serving, web worker, WebAssembly, JavaScript bundles, React, SPA, partial hydration, import on interaction, 3rd-parties, cache.</li>
  <li><a href="/2021/01/front-end-performance-delivery-optimizations/">Delivery Optimizations</a><br />Lazy loading, intersection observer, defer rendering and decoding, critical CSS, streaming, resource hints, layout shifts, service worker.</li>
  <li><a href="/2021/01/front-end-performance-networking-http2-http3/">Networking, HTTP/2, HTTP/3</a><br />OCSP stapling, EV/DV certificates, packaging, IPv6, QUIC, HTTP/3.</li>
  <li><a href="/2021/01/front-end-performance-testing-monitoring/">Testing And Monitoring</a><br />Auditing workflow, proxy browsers, 404 page, GDPR cookie consent prompts, performance diagnostics CSS, accessibility.</li>
  <li><a href="/2021/01/front-end-performance-quick-wins/">Quick Wins</a></li>
  <li><strong><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/">Everything on one page</a></strong></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/#download-the-checklist">Download The Checklist (PDF, Apple Pages, MS Word)</a></li>
  <li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next guides.</li>
</ol>

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

## Getting Ready: Planning And Metrics

<p>Micro-optimizations are great for keeping performance on track, but it’s critical to have clearly defined targets in mind &mdash; <em>measurable</em> goals that would influence any decisions made throughout the process. There are a couple of different models, and the ones discussed below are quite opinionated &mdash; just make sure to set your own priorities early&nbsp;on.</p>

<ol class="start">
<li><strong>Establish a performance culture.</strong><br />In many organizations, front-end developers know exactly what common underlying problems are and what strategies should be used to fix them. However, as long as there is no established endorsement of the performance culture, each decision will turn into a battlefield of departments, breaking up the organization into silos. You need a business stakeholder buy-in, and to get it, you need to establish a case study, or <a href="https://medium.com/@armelpingault/how-to-convince-your-client-to-focus-on-web-performance-a-case-study-35f12385689">a proof of concept</a> on how speed — especially <em>Core Web Vitals</em> which we'll cover in detail later — benefits metrics and Key Performance Indicators (<em>KPIs</em>) they care about.

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

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/430e2362-e8f8-4db9-9ac2-2187fd638d52/16-ux-speed-calculator-front-end-performance-checklist-2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/430e2362-e8f8-4db9-9ac2-2187fd638d52/16-ux-speed-calculator-front-end-performance-checklist-2020.png" sizes="100vw" caption="Just when you need to make a case for performance to drive your point across: <a href='https://ux-speed-calculator.netlify.com/'>UX Speed Calculator</a> visualizes an impact of performance on bounce rates, conversion and total revenue &mdash; based on real data. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/430e2362-e8f8-4db9-9ac2-2187fd638d52/16-ux-speed-calculator-front-end-performance-checklist-2020.png'>Large preview</a>)" alt="Just when you need to make a case for performance to drive your point across: UX Speed Calculator visualizes an impact of performance on bounce rates, conversion and total revenue, based on real data" >}}

<p>Sometimes you might want to go a bit deeper, combining the data coming from CrUX with any other data you already have to work out quickly where the slowdowns, blindspots, and inefficiencies lie &mdash; for your competitors, or for your project. In his work, Harry Roberts has been using a <a href="https://csswizardry.com/2020/11/site-speed-topography/">Site-Speed Topography Spreadsheet</a> which he uses to break down performance by key page types, and track how different key metrics are across them. You can <a href="https://gumroad.com/l/site-speed-topography">download the spreadsheet</a> as Google Sheets, Excel, OpenOffice document or CSV.</p>

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

<p>For each of them, Google recommends a range of acceptable speed goals. At least <strong>75% of all page views</strong> should exceed the <em>Good range</em> to pass this assessment. These metrics quickly gained traction, and with <a href="https://developers.google.com/search/blog/2020/11/timing-for-page-experience">Core Web Vitals becoming ranking signals for Google Search</a> in May 2021 (<em>Page Experience ranking algorithm update</em>), many companies have turned their attention to their performance scores.</p>

<p>Let’s break down each of the Core Web Vitals, one by one, along with <strong>useful techniques and tooling</strong> to optimize your experiences with these metrics in mind. (It’s worth noting that you will end up with better Core Web Vitals scores by following a general advice in this article.)</p>

<ul>
<li><a href="https://web.dev/optimize-lcp/"><strong>Largest Contentful Paint</strong></a> (<em>LCP</em>) &lt; 2.5 sec.<br />
Measures the <em>loading</em> of a page, and reports the render time of the <strong>largest image or text block</strong> that’s visible within the viewport. Hence, LCP is affected by everything that’s deferring the rendering of important information &mdash; be it slow server response times, blocking CSS, in-flight JavaScript (first-party or third-party), web font loading, expensive rendering or painting operations, lazy-loaded images, skeleton screens or client-side rendering.<br /><br />For a good experience, LCP should occur <strong>within 2.5s</strong> of when the page first starts loading. That means that we need to render the first visible portion of the page as early as possible. That will require tailored critical CSS for each template, orchestrating the <code>&lt;head&gt;</code>-order and prefetching critical assets (we’ll cover them later).</p>

<p>The main reason for a low LCP score is usually <a href="https://youtu.be/YMqnPeZHcuc?t=417">images</a>. To deliver an LCP in &lt;2.5s on Fast 3G &mdash; hosted on a well-optimized server, all static without client-side rendering and with an image coming from a dedicated image CDN &mdash; means that the <strong>maximum theoretical image size is only around 144KB</strong>. That’s why responsive images matter, as well as preloading critical images early (with <code>preload</code>).</p>

<p><em>Quick tip</em>: to discover what is considered LCP on a page, in DevTools you can <a href="https://twitter.com/tkadlec/status/1262756549090398209">hover over the LCP badge</a> under "Timings" in the Performance Panel (<em>thanks, Tim Kadlec</em>!).</p>
</li>
<li><a href="https://web.dev/fid/"><strong>First Input Delay</strong></a> (<em>FID</em>) &lt; 100ms.<br />
Measures the <em>responsiveness</em> of the UI, i.e. <strong>how long the browser was busy</strong> with other tasks before it could react to a discrete user input event like a tap, or a click. It’s designed to capture delays that result from the main thread being busy, especially during page load.<br /><br />The goal is to stay within <a href="https://youtu.be/iNfz9tg-wyg?t=259">50–100ms</a> for every interaction. To get there, we need to identify long tasks (blocks the main thread for &gt;50ms) and break them up, code-split a bundle into multiple chunks, reduce JavaScript execution time, optimize data-fetching, defer script execution of third-parties, move JavaScript to the background thread with Web workers and use progressive hydration to reduce rehydration costs in SPAs.</p>

<p><em>Quick tip</em>: in general, a reliable strategy to get a better FID score is to <strong>minimize the work on the main thread</strong> by breaking larger bundles into smaller ones and serving what the user needs when they need it, so user interactions won’t be delayed. We’ll cover more on that in detail below.</p>
</li>
<li><a href="https://web.dev/cls/"><strong>Cumulative Layout Shift</strong></a> (<em>CLS</em>) &lt; 0.1.<br />
Measures <strong>visual stability</strong> of the UI to ensure smooth and natural interactions, i.e. the sum total of all individual layout shift scores for every unexpected layout shift that occurs during the lifespan of the page. An individual layout shift occurs any time an element which was already visible changes its position on the page. It’s scored based on the size of the content and distance it moved.<br /><br />So every time a shift appears — e.g. when fallback fonts and web fonts have different font metrics, or adverts, embeds or iframes coming in late, or image/video dimensions aren’t reserved, or late CSS forces repaints, or changes are injected by late JavaScript &mdash; it has an impact on the CLS score. The recommended value for a good experience is a CLS &lt; 0.1.</p>
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

<li><strong>Share the performance goals with your colleagues.</strong><br />Make sure that performance goals are familiar to every member of your team to avoid misunderstandings down the line. Every decision &mdash; be it design, marketing or anything in-between &mdash; has <strong>performance implications</strong>, and distributing responsibility and ownership across the entire team would streamline performance-focused decisions later on. Map design decisions against performance budget and the priorities defined early on.</p></li>
</ol>


## Table Of Contents

<ol>
  <li><strong>Getting Ready: Planning And Metrics</strong></li>
  <li><a href="/2021/01/front-end-performance-setting-realistic-goals/">Setting Realistic Goals</a></li>
  <li><a href="/2021/01/front-end-performance-defining-the-environment/">Defining The Environment</a></li>
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

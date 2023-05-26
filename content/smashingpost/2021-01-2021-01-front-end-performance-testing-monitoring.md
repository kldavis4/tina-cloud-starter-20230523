---
title: 'Front-End Performance 2021: Testing And Monitoring'
slug: front-end-performance-testing-monitoring
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
  <li><a href="/2021/01/front-end-performance-defining-the-environment/">Defining The Environment</a></li>
  <li><a href="/2021/01/front-end-performance-assets-optimizations/">Assets Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-build-optimizations/">Build Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-delivery-optimizations/">Delivery Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-networking-http2-http3/">Networking, HTTP/2, HTTP/3</a></li>
  <li><strong>Testing And Monitoring</strong></li>
  <li><a href="/2021/01/front-end-performance-quick-wins/">Quick Wins</a></li>
  <li><strong><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/">Everything on one page</a></strong></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/#download-the-checklist">Download The Checklist (PDF, Apple Pages, MS Word)</a></li>
  <li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next guides.</li>
</ol>

<style>
  .drop-caps{display:none !important}
  ol.start {
  	  counter-set: perfcounter 70;
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

## Testing And Monitoring

<ol class="start">
<li><strong>Have you optimized your auditing workflow?</strong><br />It might not sound like a big deal, but having the right settings in place at your fingertips might save you quite a bit of time in testing. Consider using Tim Kadlec’s <a href="https://github.com/tkadlec/webpagetest-alfred-workflow">Alfred Workflow for WebPageTest</a> for submitting a test to the public instance of WebPageTest. In fact, WebPageTest has many obscure features, so take the time to learn <a href="https://nooshu.github.io/blog/2019/10/02/how-to-read-a-wpt-waterfall-chart/">how to read a WebPageTest Waterfall View chart</a> and <a href="https://nooshu.github.io/blog/2019/12/30/how-to-read-a-wpt-connection-view-chart/">how to read a WebPageTest Connection View chart</a> to diagnose and resolve performance issues faster.

<p>You could also <a href="https://calendar.perfplanet.com/2014/driving-webpagetest-from-a-google-docs-spreadsheet/">drive WebPageTest from a Google Spreadsheet</a> and <a href="https://web.dev/fast/using-lighthouse-ci-to-set-a-performance-budget">incorporate accessibility, performance and SEO scores</a> into your Travis setup with Lighthouse CI or <a href="https://twitter.com/addyosmani/statuses/1017655423099289600">straight into Webpack</a>.</p>

<p>Take a look at the recently released <a href="https://web.dev/autowebperf/">AutoWebPerf</a>, a modular tool that enables automatic gathering of performance data from multiple sources. For example, we could set a daily test on your critical pages to capture the field data from CrUX API and lab data from a Lighthouse report from PageSpeed Insights.</p>

<p>And if you need to debug something quickly but your build process seems to be remarkably slow, keep in mind that "<a href="https://slack.engineering/keep-webpack-fast-a-field-guide-for-better-build-performance-f56a5995e8f1">whitespace removal and symbol mangling accounts for 95% of the size reduction</a> in minified code for most JavaScript &mdash; not elaborate code transforms. You can simply disable compression to speed up Uglify builds by 3 to 4 times."</p></li>
</ol>

{{< rimg breakout="true" href="https://cdn-images-1.medium.com/max/1600/1*Y-1sdlIzFBRfEQPprzLnbA.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/705ed9b1-cd4d-4231-b808-ce8c2e72e070/review-required-checks-pr.png" sizes="100vw" caption="Integrating <a href='https://web.dev/fast/using-lighthouse-ci-to-set-a-performance-budget'>accessibility, performance and SEO scores</a> into your Travis setup with Lighthouse CI will highlight the performance impact of a new feature to all contributing developers. (<a href='https://cdn-images-1.medium.com/max/1600/1*Y-1sdlIzFBRfEQPprzLnbA.png'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/705ed9b1-cd4d-4231-b808-ce8c2e72e070/review-required-checks-pr.png'>Large preview</a>)" alt="A screenshot of GitHub’s Pull Request notification stating that review is required and that merging is blocked until checks have been successfully resolved" >}}

<ol class="continue">
<li><strong>Have you tested in proxy browsers and legacy browsers?</strong><br />Testing in Chrome and Firefox is not enough. Look into how your website works in proxy browsers and legacy browsers. UC Browser and Opera Mini, for instance, have a <a href="https://gs.statcounter.com/#mobile_browser-as-monthly-201511-201611">significant market share in Asia</a> (up to 35% in Asia). <a href="https://www.webworldwide.io/">Measure average Internet speed</a> in your countries of interest to avoid big surprises down the road. Test with network throttling, and emulate a high-DPI device. <a href="https://www.browserstack.com">BrowserStack</a> is fantastic for testing on <em>remote</em> real devices, and complement it with at least a few real devices in your office as well &mdash; it’s worth it.</li>
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


## Table Of Contents

<ol>
  <li><a href="/2021/01/front-end-performance-getting-ready-planning-metrics/">Getting Ready: Planning And Metrics</a></li>
  <li><a href="/2021/01/front-end-performance-setting-realistic-goals/">Setting Realistic Goals</a></li>
  <li><a href="/2021/01/front-end-performance-defining-the-environment/">Defining The Environment</a></li>
  <li><a href="/2021/01/front-end-performance-assets-optimizations/">Assets Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-build-optimizations/">Build Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-delivery-optimizations/">Delivery Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-networking-http2-http3/">Networking, HTTP/2, HTTP/3</a></li>
  <li><strong>Testing And Monitoring</strong></li>
  <li><a href="/2021/01/front-end-performance-quick-wins/">Quick Wins</a></li>
  <li><strong><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/">Everything on one page</a></strong></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/#download-the-checklist">Download The Checklist (PDF, Apple Pages, MS Word)</a></li>
  <li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next guides.</li>
</ol>

{{< signature "il" >}}

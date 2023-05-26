---
title: 'Front-End Performance 2021: Quick Wins'
slug: front-end-performance-quick-wins
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

## Table of Contents

<ol>
  <li><a href="/2021/01/front-end-performance-getting-ready-planning-metrics/">Getting Ready: Planning And Metrics</a></li>
  <li><a href="/2021/01/front-end-performance-setting-realistic-goals/">Setting Realistic Goals</a></li>
  <li><a href="/2021/01/front-end-performance-defining-the-environment/">Defining The Environment</a></li>
  <li><a href="/2021/01/front-end-performance-assets-optimizations/">Assets Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-build-optimizations/">Build Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-delivery-optimizations/">Delivery Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-networking-http2-http3/">Networking, HTTP/2, HTTP/3</a></li>
  <li><a href="/2021/01/front-end-performance-testing-monitoring/">Testing And Monitoring</a></li>
  <li><strong>Quick Wins</strong></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/">Everything on one page</a></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/#download-the-checklist">Download The Checklist (PDF, Apple Pages, MS Word)</a></li>
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


## Table of Contents

<ol>
  <li><a href="/2021/01/front-end-performance-getting-ready-planning-metrics/">Getting Ready: Planning And Metrics</a></li>
  <li><a href="/2021/01/front-end-performance-setting-realistic-goals/">Setting Realistic Goals</a></li>
  <li><a href="/2021/01/front-end-performance-defining-the-environment/">Defining The Environment</a></li>
  <li><a href="/2021/01/front-end-performance-assets-optimizations/">Assets Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-build-optimizations/">Build Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-delivery-optimizations/">Delivery Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-networking-http2-http3/">Networking, HTTP/2, HTTP/3</a></li>
  <li><a href="/2021/01/front-end-performance-testing-monitoring/">Testing And Monitoring</a></li>
  <li><strong>Quick Wins</strong></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/">Everything on one page</a></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/#download-the-checklist">Download The Checklist (PDF, Apple Pages, MS Word)</a></li>
  <li><strong><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/">Everything on one page</a></strong></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/#download-the-checklist">Download The Checklist (PDF, Apple Pages, MS Word)</a></li>
  <li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next guides.</li>
</ol>

<hr />

<p><em>A huge thanks to Guy Podjarny, Yoav Weiss, Addy Osmani, Artem Denysov, Denys Mishunov, Ilya Pukhalski, Jeremy Wagner, Colin Bendell, Mark Zeman, Patrick Meenan, Leonardo Losoviz, Andy Davies, Rachel Andrew, Anselm Hannemann, Barry Pollard, Patrick Hamann, Gideon Pyzer, Andy Davies, Maria Prosvernina, Tim Kadlec, Rey Bango, Matthias Ott, Peter Bowyer, Phil Walton, Mariana Peralta, Pepijn Senders, Mark Nottingham, Jean Pierre Vincent, Philipp Tellis, Ryan Townsend, Ingrid Bergman, Mohamed Hussain S. H., Jacob Groß, Tim Swalling, Bob Visser, Kev Adamson, Adir Amsalem, Aleksey Kulikov and Rodney Rehm for reviewing this article, as well as our fantastic community which has shared techniques and lessons learned from its work in performance optimization for everybody to use. You are truly smashing!</em></p>

{{< signature "il" >}}

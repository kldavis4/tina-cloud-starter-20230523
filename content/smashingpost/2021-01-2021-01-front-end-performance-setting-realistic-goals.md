---
title: 'Front-End Performance 2021: Setting Realistic Goals'
slug: front-end-performance-setting-realistic-goals
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
  <li><strong>Setting Realistic Goals</strong></li>
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

<style>
  .drop-caps{display:none !important}
  ol.start {
	  counter-set: perfcounter 7;
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


## Setting Realistic Goals

<ol class="start">
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

<p>If you want to target growing markets such as South East Asia, Africa or India, you’ll have to look into a very different set of constraints. Addy Osmani covers <a href="https://dev.to/addyosmani/loading-web-pages-fast-on-a-20-feature-phone-8h6">major feature phone constraints</a>, such as few low cost, high-quality devices, unavailability of high-quality networks and expensive mobile data &mdash; along with <strong>PRPL-30 budget</strong> and development guidelines for these environments.</p>

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


## Table Of Contents

<ol>
  <li><a href="/2021/01/front-end-performance-getting-ready-planning-metrics/">Getting Ready: Planning And Metrics</a></li>
  <li><strong>Setting Realistic Goals</strong></li>
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

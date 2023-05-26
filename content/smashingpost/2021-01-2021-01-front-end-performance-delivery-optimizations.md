---
title: 'Front-End Performance 2021: Delivery Optimizations'
slug: front-end-performance-delivery-optimizations
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
  <li><strong>Delivery Optimizations</strong></li>
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
  	  counter-set: perfcounter 44;
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

## Delivery Optimizations

<ol class="start">
<li><strong>Do we use <code>defer</code> to load critical JavaScript asynchronously?</strong><br />When the user requests a page, the browser fetches the HTML and constructs the DOM, then fetches the CSS and constructs the CSSOM, and then generates a rendering tree by matching the DOM and CSSOM. If any JavaScript needs to be resolved, the browser <strong>won’t start rendering the page</strong> until it’s resolved, thus delaying rendering. As developers, we have to explicitly tell the browser not to wait and to start rendering the page. The way to do this for scripts is with the <code>defer</code> and <code>async</code> attributes in HTML.

<p>In practice, it turns out that it's better to <a href="https://calendar.perfplanet.com/2016/prefer-defer-over-async/">use <code>defer</code> instead of <code>async</code></a>. Ah, what's the <strong>difference</strong> again? According to <a href="https://youtu.be/RwSlubTBnew?t=1034">Steve Souders</a>, once <code>async</code> scripts arrive, they are executed immediately &mdash; as soon as the script is ready. If that happens very fast, for example when the script is in cache aleady, it can actually block HTML parser. With <code>defer</code>, browser doesn’t execute scripts until HTML is parsed. So, unless you need JavaScript to execute before start render, it’s better to use <code>defer</code>. Also, multiple async files will execute in a non-deterministic order.</p>

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

<li><strong>Do you defer rendering with <code>content-visibility</code>?</strong><br />For complex layout with plentiful of content blocks, images and videos, decoding data and rendering pixels might be a quite expensive operation &mdash; especially on low-end devices. With <a href="https://web.dev/content-visibility/"><code>content-visibility: auto</code></a>, we can prompt the browser to skip the layout of the children while the container is outside of the viewport.

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

<p>And if you need to get a bit more granular, with <a href="https://developers.google.com/web/updates/2016/06/css-containment">CSS Containment</a>, you can manually skip layout, style and paint work for descendants of a DOM node if you need only size, alignment or computed styles on other elements &mdash; or the element is currently off-canvas.</p>
</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/640ed03b-3b1d-40be-84a8-6000698397aa/baseline-chunks-content-visibility-auto.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/640ed03b-3b1d-40be-84a8-6000698397aa/baseline-chunks-content-visibility-auto.jpg" sizes="100vw" caption="In the demo, applying <code>content-visibility: auto</code> to chunked content areas gives a 7&times; rendering performance boost on initial load. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/640ed03b-3b1d-40be-84a8-6000698397aa/baseline-chunks-content-visibility-auto.jpg'>Large preview</a>)" alt="The rendering performance on initial load is 2,288 ms for baseline (left) and 13,464 ms for chunks with content-visibility:auto (right)" >}}

<ol class="continue">
<li><strong>Do you defer decoding with <code>decoding="async"</code>?</strong><br />Sometimes content appears offscreen, yet we want to ensure that it’s available when customers need it &mdash; ideally, not blocking anything in the critical path, but decoding and rendering asynchronously. We can use <a href="https://html.spec.whatwg.org/multipage/images.html#decoding-images"><code>decoding="async"</code></a> to give the browser a permission to decode the image off the main thread, avoiding user impact of the CPU-time used to decode the image (via <a href="https://www.industrialempathy.com/posts/image-optimizations/">Malte Ubl</a>):<br /><br />

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

<p>Also, avoid placing <code>&lt;link rel="stylesheet" /&gt;</code> before <code>async</code> snippets. If scripts don’t depend on stylesheets, consider placing blocking scripts above blocking  styles. If they do, split that JavaScript in two and load it either side of your CSS.</p>

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

## Table Of Contents

<ol>
  <li><a href="/2021/01/front-end-performance-getting-ready-planning-metrics/">Getting Ready: Planning And Metrics</a></li>
  <li><a href="/2021/01/front-end-performance-setting-realistic-goals/">Setting Realistic Goals</a></li>
  <li><a href="/2021/01/front-end-performance-defining-the-environment/">Defining The Environment</a></li>
  <li><a href="/2021/01/front-end-performance-assets-optimizations/">Assets Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-build-optimizations/">Build Optimizations</a></li>
  <li><strong>Delivery Optimizations</strong></li>
  <li><a href="/2021/01/front-end-performance-networking-http2-http3/">Networking, HTTP/2, HTTP/3</a></li>
  <li><a href="/2021/01/front-end-performance-testing-monitoring/">Testing And Monitoring</a></li>
  <li><a href="/2021/01/front-end-performance-quick-wins/">Quick Wins</a></li>
  <li><strong><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/">Everything on one page</a></strong></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/#download-the-checklist">Download The Checklist (PDF, Apple Pages, MS Word)</a></li>
  <li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next guides.</li>
</ol>

{{< signature "il" >}}

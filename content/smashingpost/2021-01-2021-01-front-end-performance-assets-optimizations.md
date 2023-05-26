---
title: 'Front-End Performance 2021: Assets Optimizations'
slug: front-end-performance-assets-optimizations
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
  <li><strong>Assets Optimizations</strong></li>
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
  	  counter-set: perfcounter 19;
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

## Assets Optimizations

<ol class="start">
<li><strong>Use Brotli for plain text compression.</strong><br />In 2015, Google <a href="https://opensource.googleblog.com/2015/09/introducing-brotli-new-compression.html">introduced</a> <a href="https://github.com/google/brotli">Brotli</a>, a new open-source lossless data format, which is now <a href="https://caniuse.com/#search=brotli">supported in all modern browsers</a>. The <a href="https://github.com/google/brotli">open sourced Brotli library</a>, that implements an encoder and decoder for Brotli, has <a href="https://blog.cloudflare.com/brotli-compression-using-a-reduced-dictionary/">11 predefined quality levels</a> for the encoder, with higher quality level demanding more CPU in exchange for a better compression ratio. Slower compression will ultimately lead to higher compression rates, yet still, Brotli decompresses fast. It’s worth noting though that <a href="https://expeditedsecurity.com/blog/nginx-brotli/">Brotli with the compression level 4 is both smaller and compresses faster than Gzip</a>.

<p>In practice, Brotli appears to be <a href="https://paulcalvano.com/index.php/2018/07/25/brotli-compression-how-much-will-it-reduce-your-content/">much</a> <a href="https://quixdb.github.io/squash-benchmark/#results-table">more effective</a> than Gzip. Opinions and experiences differ, but if your site is already optimized with Gzip, you might be expecting <a href="https://blog.bitsrc.io/gzip-to-brotli-better-frontend-load-performance-b2b4d8dbf60f">at least</a> <a href="https://csswizardry.com/2020/04/real-world-effectiveness-of-brotli/">single-digit improvements</a> and at best <a href="https://expeditedsecurity.com/blog/nginx-brotli/">double-digits improvements</a> in size reduction and FCP timings. You can also <a href="https://tools.paulcalvano.com/compression.php">estimate Brotli compression savings for your site</a>.</p>

<p>Browsers will accept Brotli only if the user is visiting a website over HTTPS. Brotli is widely supported, and many CDNs support it (<a href="https://community.akamai.com/community/web-performance/blog/2017/08/18/brotli-support-enablement-on-akamai">Akamai</a>, <a href="https://www.netlify.com/blog/2020/05/20/gain-instant-performance-boosts-as-brotli-comes-to-netlify-edge/">Netlify Edge</a>, <a href="https://medium.com/@felice.geracitano/brotli-compression-delivered-from-aws-7be5b467c2e1">AWS</a>, <a href="https://www.keycdn.com/blog/keycdn-brotli-support">KeyCDN</a>, <a href="https://docs.fastly.com/guides/detailed-product-descriptions/performance-optimization-package">Fastly</a> (currently only as a pass-through), <a href="https://support.cloudflare.com/hc/en-us/articles/200168396-What-will-Cloudflare-compress-">Cloudflare</a>, <a href="https://www.cdn77.com/brotli">CDN77</a>) and you can <a href="https://calendar.perfplanet.com/2016/enabling-brotli-even-on-cdns-that-dont-support-it-yet/">enable Brotli even on CDNs that don’t support it</a> yet (with a service worker).</p>

<p>The catch is that because compressing <em>all</em> assets with Brotli at a high compression level is expensive, many hosting providers can’t use it at fule scall just because of the huge cost overhead it produces. In fact, at the highest level of compression, Brotli is <em>so</em> slow that any potential gains in file size could be nullified by the amount of time it takes for the server to begin sending the response as it waits to dynamically compress the asset. (But if you have time during the build time with static compression, of course, <a href="https://css-tricks.com/brotli-static-compression/">higher compression settings are preferred</a>.)</p>

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

<p>As Ilya Grigorik <a href="https://developers.google.com/web/updates/2015/09/automating-resource-selection-with-client-hints">noted</a> a while back, client hints complete the picture &mdash; they aren’t an alternative to responsive images. "The <code>&lt;picture&gt;</code> element provides the necessary art-direction control in the HTML markup. Client hints provide annotations on resulting image requests that enable resource selection automation. Service Worker provides full request and response management capabilities on the client."</p>

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

<p>For conversion to WebP, you can use <a href="https://webp-converter.com/">WebP Converter</a>, <a href="https://developers.google.com/speed/webp/docs/cwebp">cwebp</a> or <a href="https://downloads.webmproject.org/releases/webp/index.html">libwebp</a>. Ire Aderinokun has a very detailed <a href="https://bitsofco.de/why-and-how-to-use-webp-images-today/">tutorial on converting images to WebP</a>, too &mdash; and so does Josh Comeau in his piece on <a href="https://www.joshwcomeau.com/performance/embracing-modern-image-formats/">embracing modern image formats</a>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd5e6234-7669-4759-ab83-10f8dd0db976/maxresdefault-opt.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd5e6234-7669-4759-ab83-10f8dd0db976/maxresdefault-opt.jpg" sizes="100vw" caption="A thorough talk about WebP: <a href='https://www.youtube.com/watch?v=MBVBfLdh984'>WebP Rewind</a> by Pascal Massimino. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd5e6234-7669-4759-ab83-10f8dd0db976/maxresdefault-opt.jpg'>Large preview</a>)" alt="A slide used for Pascal Massimino’s talk titled Image ready: webp rewind" >}}

<p>Sketch natively supports WebP, and WebP images can be exported from Photoshop using a <a href="https://telegraphics.com.au/sw/product/WebPFormat#webpformat">WebP plugin for Photoshop</a>. But <a href="https://developers.google.com/speed/webp/docs/using">other options are available</a>, too.</p>

<p>If you’re using WordPress or Joomla, there are extensions to help you easily implement support for WebP, such as <a href="https://wordpress.org/plugins/optimus/">Optimus</a> and <a href="https://wordpress.org/plugins/cache-enabler/">Cache Enabler</a> for WordPress and <a href="https://extensions.joomla.org/extension/webp/">Joomla’s own supported extension</a> (via <a href="https://css-tricks.com/comparing-novel-vs-tried-true-image-formats/">Cody Arsenault</a>). You can also abstract away the <code>&lt;picture&gt;</code> element <a href="https://www.joshwcomeau.com/performance/embracing-modern-image-formats/">with React, styled components or gatsby-image</a>.</p>

<p>Ah &mdash; <em>shameless plug!</em> &mdash; Jeremy Wagner even <a href="https://www.smashingmagazine.com/ebooks/the-webp-manual/">published a Smashing book on WebP</a> which you might want to check if you are interested about everything around WebP.</p>
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
<li>Review <a href="https://csswizardry.com/2018/06/image-inconsistencies-how-and-when-browsers-download-images/">image download inconsistencies</a> to prevent unexpected downloads for foreground and background images. Watch out for images that are loaded by default, but might never be displayed &mdash; e.g. in carousels, accordions and image galleries.</li>
<li>Make sure to <a href="https://www.smashingmagazine.com/2020/03/setting-height-width-images-important-again/">always set <code>width</code> and <code>height</code> on images</a>. Watch out for the <a href="https://drafts.csswg.org/css-sizing-4/#ratios"><code>aspect-ratio</code> property in CSS</a> and <a href="https://github.com/ojanvafai/intrinsicsize-attribute"><code>intrinsicsize</code> attribute</a> which will allow us to set aspect ratios and dimensions for images, so browser can reserve a pre-defined layout slot early to <a href="https://24ways.org/2018/jank-free-image-loads/">avoid layout jumps</a> during the page load.</li>
</ul>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebcc7dad-3cbc-4595-b141-2c6c80ab8fc6/aspect-ratio-in-browsers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebcc7dad-3cbc-4595-b141-2c6c80ab8fc6/aspect-ratio-in-browsers.png" sizes="100vw" caption="Should be just a matter of weeks or months now, with aspect-ratio landing in browsers. In <a href='https://twitter.com/jensimmons/status/1347287421633892356'>Safari Technical Preview 118</a> already. <a href='https://caniuse.com/mdn-css_properties_aspect-ratio'>Currently behind the flag in Firefox and Chrome.</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebcc7dad-3cbc-4595-b141-2c6c80ab8fc6/aspect-ratio-in-browsers.png'>Large preview</a>)" alt="A screenshot of code showing padding-top and aspect-ratio elements in use in an editor" >}}

<p>If you feel adventurous, you could chop and rearrange HTTP/2 streams using <a href="https://youtu.be/jTXhYj2aCDU?t=854">Edge workers</a>, basically a real-time filter living on the CDN, to send images faster through the network. Edge workers use JavaScript streams that use chunks which you can control (basically they are JavaScript that runs on the CDN edge that can modify the streaming responses), so you can control the delivery of images.</p>

<p>With a service worker, it’s too late as you can’t control what’s on the wire, but it does work with Edge workers. So you can use them on top of static JPEGs saved progressively for a particular landing page.</p>

{{< rimg href="https://pbs.twimg.com/media/DY1XZ28VwAAwjd8.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8422076c-6eea-4b35-a98c-b15445cb2dff/viewport-percentage-match.jpg" sizes="100vw" caption="A sample output by <a href='https://github.com/filamentgroup/imaging-heap'>imaging-heap</a>, a command line tool that measure the efficiency across viewport sizes and device pixel ratios. (<a href='https://pbs.twimg.com/media/DY1XZ28VwAAwjd8.jpg'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8422076c-6eea-4b35-a98c-b15445cb2dff/viewport-percentage-match.jpg'>Large preview</a>)" alt="A screenshot of the imaging-heap command line tool showing a table with various viewport sizes and device pixel ratios" >}}

<p>Not good enough? Well, you can also improve perceived performance for images with the <a href="https://csswizardry.com/2016/10/improving-perceived-performance-with-multiple-background-images/">multiple</a> <a href="https://jmperezperez.com/medium-image-progressive-loading-placeholder/">background</a> <a href="https://manu.ninja/dominant-colors-for-lazy-loading-images#tiny-thumbnails">images</a> <a href="https://css-tricks.com/the-blur-up-technique-for-loading-background-images/">technique</a>. Keep in mind that <a href="https://css-tricks.com/contrast-swap-technique-improved-image-performance-css-filters/">playing with contrast</a> and blurring out unnecessary details (or removing colors) can reduce file size as well. Ah, you need to <strong>enlarge a small photo</strong> without losing quality? Consider using <a href="https://letsenhance.io">Letsenhance.io</a>.</p>

<p>These optimizations so far cover just the basics. Addy Osmani has published a <a href="https://images.guide/">very detailed guide on Essential Image Optimization</a> that goes very deep into details of image compression and color management. For example, you could <strong>blur out unnecessary parts</strong> of the image (by applying a Gaussian blur filter to them) to reduce the file size, and eventually you might even start removing colors or turn the picture into black and white to reduce the size even further. For background images, exporting photos from Photoshop with 0 to 10% quality can be absolutely acceptable as well.</p>

<p>On Smashing Magazine, we use the postfix <code>-opt</code> for image names &mdash; for example, <code>brotli-compression-opt.png</code>; whenever an image contains that postfix, everybody on the team knows that the image has already been optimized.</p>

<p>Ah, and <a href="https://calendar.perfplanet.com/2018/dont-use-jpeg-xr-on-the-web/">don’t use JPEG-XR on the web</a> &mdash; "the processing of decoding JPEG-XRs software-side on the CPU nullifies and even outweighs the potentially positive impact of byte size savings, especially in the context of SPAs" (not to mix up with Cloudinary/Google’s <a href="https://cloudinary.com/blog/how_jpeg_xl_compares_to_other_image_codecs">JPEG XL</a> though).</p>
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

<p>The research shows that <a href="https://www.akamai.com/kr/ko/multimedia/documents/technical-publication/video-stream-quality-impacts-viewer-behavior-inferring-causality-using-quasi-experimental-designs-technical-publication.pdf">video stream quality impacts viewer behavior</a>. In fact, viewers start to abandon the video if the startup delay exceeds about 2 seconds. Beyond that point, a 1-second increase in delay results in roughly a 5.8% increase in abandonment rate. So it’s not surprising that the <a href="https://dougsillars.com/2019/09/16/state-of-the-web-video-playback-metrics/">median video start time is 12.8s</a>, with 40% of videos having at least 1 stall, and 20% at least 2s of stalled video playback. In fact, video stalls are unavoidable on 3G as videos play back faster than the network can supply content.</p>

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
<li><strong>Is web font delivery optimized?</strong><br />The first question that’s worth asking is if we can get away with <a href="https://www.smashingmagazine.com/2015/11/using-system-ui-fonts-practical-guide/">using UI system fonts</a> in the first place &mdash; we just need to make sure to <a href="https://fontfamily.io/Roboto,Segoe_UI,TImes,Helvetica,sans-serif">double check that they appear correctly</a> on various platforms. If it’s not the case, chances are high that the web fonts we are serving include glyphs and extra features and weights that aren’t being used. We can ask our type foundry to <strong>subset web fonts</strong> or if we are using open-source fonts, subset them on our own with <a href="https://www.afasterweb.com/2018/03/09/subsetting-fonts-with-glyphhanger/">Glyphhanger</a> or <a href="https://www.fontsquirrel.com/tools/webfont-generator">Fontsquirrel</a>. We can even automate our entire workflow with Peter Müller’s <a href="https://github.com/Munter/subfont#readme">subfont</a>, a command line tool that statically analyses your page in order to generate the most optimal web font subsets, and then inject them into our pages.

<p><a href="https://caniuse.com/#search=woff2">WOFF2 support</a> is great, and we can use WOFF as fallback for browsers that don’t support it &mdash; or perhaps legacy browsers could be served system fonts. There are <em>many, many, many</em> options for web font loading, and we can choose one of the strategies from Zach Leatherman’s "<a href="https://www.zachleat.com/web/comprehensive-webfonts/">Comprehensive Guide to Font-Loading Strategies</a>," (code snippets also available as <a href="https://github.com/zachleat/web-font-loading-recipes">Web font loading recipes</a>).</p>

<p>Probably the better options to consider today are <a href="https://www.zachleat.com/web/comprehensive-webfonts/#critical-foft-preload">Critical FOFT with <code>preload</code></a> and <a href="https://www.zachleat.com/web/the-compromise/">"The Compromise" method</a>. Both of them use a <strong>two-stage render</strong> for delivering web fonts in steps &mdash; first a small supersubset required to render the page fast and accurately with the web font, and then load the rest of the family async. The difference is that "The Compromise" technique loads polyfill asynchronously only if <a href="https://www.igvita.com/2014/01/31/optimizing-web-font-rendering-performance/#font-load-events">font load events</a> are not supported, so you don’t need to load the polyfill by default. Need a quick win? Zach Leatherman has a <a href="https://www.zachleat.com/web/23-minutes/">quick 23-min tutorial and case study</a> to get your fonts in order.</p>

<p>In general, it might be a good idea to use the <code>preload</code> resource hint to preload fonts, but in your markup include the hints <em>after</em> the link to critical CSS and JavaScript. With <code>preload</code>, there is a <a href="https://andydavies.me/blog/2019/02/12/preloading-fonts-and-the-puzzle-of-priorities/">puzzle of priorities</a>, so consider injecting <code>rel="preload"</code> elements into the DOM just before the external blocking scripts. According to Andy Davies, "resources injected using a script are hidden from the browser until the script executes, and we can use this behaviour to delay when the browser discovers the <code>preload</code> hint." Otherwise, font loading will cost you in the first render time.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cabdd79-67f0-44f4-9cfa-3b87732938cb/pre-render-fonts-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cabdd79-67f0-44f4-9cfa-3b87732938cb/pre-render-fonts-opt.png" sizes="100vw" caption="When everything is critical, nothing is critical. preload only one or a maximum of two fonts of each family. (Image credit: <a href='https://noti.st/zachleat/KNaZEg/the-five-whys-of-web-font-loading-performance#s6vhQNE'>Zach Leatherman</a> &ndash; slide 93) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cabdd79-67f0-44f4-9cfa-3b87732938cb/pre-render-fonts-opt.png'>Large preview</a>)" alt="A screenshot of slide 93 showing two example of images with a title next to them saying ‘Metrics prioritization: preload one of each family’" >}}

<p>It’s a good idea to <a href="https://youtu.be/FbguhX3n3Uc?t=1637">be selective</a> and choose files that matter most, e.g. the ones that are critical for rendering or that would help you avoiding visible and disruptive text reflows. In general, Zach advises to <strong>preload one or two fonts of each family</strong> &mdash; it also makes sense to delay some font loading if they are less critical.</p>

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

<p>This is quite important especially as since Chrome v86 (released October 2020), cross-site resources like <a href="https://wicki.io/posts/2020-11-goodbye-google-fonts/">fonts can’t be shared on the same CDN</a> anymore &mdash; due to the <a href="https://developers.google.com/web/updates/2020/10/http-cache-partitioning">partitioned browser cache</a>. This behavior was a default in Safari for years.</p>

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


## Table Of Contents

<ol>
  <li><a href="/2021/01/front-end-performance-getting-ready-planning-metrics/">Getting Ready: Planning And Metrics</a></li>
  <li><a href="/2021/01/front-end-performance-setting-realistic-goals/">Setting Realistic Goals</a></li>
  <li><a href="/2021/01/front-end-performance-defining-the-environment/">Defining The Environment</a></li>
  <li><strong>Assets Optimizations</strong></li>
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

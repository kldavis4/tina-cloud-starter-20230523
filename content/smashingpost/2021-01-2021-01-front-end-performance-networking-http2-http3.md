---
title: 'Front-End Performance 2021: Networking, HTTP/2, HTTP/3'
slug: front-end-performance-networking-http2-http3
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
  <li><strong>Networking, HTTP/2, HTTP/3</strong></li>
  <li><a href="/2021/01/front-end-performance-testing-monitoring/">Testing And Monitoring</a></li>
  <li><a href="/2021/01/front-end-performance-quick-wins/">Quick Wins</a></li>
  <li><strong><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/">Everything on one page</a></strong></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/#download-the-checklist">Download The Checklist (PDF, Apple Pages, MS Word)</a></li>
  <li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next guides.</li>
</ol>

<style>
  .drop-caps{display:none !important}
  ol.start {
  	  counter-set: perfcounter 60;
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

## Networking, HTTP/2, HTTP/3

<ol class="start">
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

<p><strong>EV certificates are expensive and time-consuming</strong> as they require a human to reviewing a certificate and ensuring its validity. DV certificates, on the other hand, are often provided for free &mdash; e.g. by
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

{{< rimg breakout="true" href="https://almanac.httparchive.org/en/2020/http2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0005ffe6-5517-4f75-b770-5a547059515c/http2-h2-usage-opt.png" sizes="100vw" caption="64% of all requests are served over HTTP/2 in late 2020, according to Web Almanac &mdash; just 4 years after its formal standardization. (Image source: <a href='https://almanac.httparchive.org/en/2020/http2'>Web Almanac</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0005ffe6-5517-4f75-b770-5a547059515c/http2-h2-usage-opt.png'>Large preview</a>)" alt="A graph showing the timeseries of HTTP/2 requests in both desktop and mobile from January 2, 2016, until October 1, 2020" >}}

<ol class="continue">
<li><strong>Properly deploy HTTP/2.</strong><br />Again, <a href="https://www.youtube.com/watch?v=yURLTwZ3ehk">serving assets over HTTP/2</a> can benefit from a partial overhaul of how you’ve been serving assets so far. You’ll need to find a fine balance between packaging modules and loading many small modules in parallel. At the end of the day, still <a href="https://alistapart.com/article/the-best-request-is-no-request-revisited">the best request is no request</a>, however, the goal is to find a fine balance between quick first delivery of assets and caching.

<p>On the one hand, you might want to avoid concatenating assets altogether, instead of breaking down your entire interface into many small modules, compressing them as a part of the build process and loading them in parallel. A change in one file won’t require the entire style sheet or JavaScript to be re-downloaded. It also <a href="https://css-tricks.com/musings-on-http2-and-bundling/">minimizes parsing time</a> and keeps the payloads of individual pages low.</p>

<p>On the other hand, <a href="https://engineering.khanacademy.org/posts/js-packaging-http2.htm">packaging still matters</a>. By using many small scripts, <strong>overall compression will suffer</strong> and the <a href="https://simonhearne.com/2020/network-faster-than-cache/">cost of retrieving objects from the cache will increase</a>. The compression of a large package will benefit from dictionary reuse, whereas small separate packages will not. There’s standard work to address that, but it’s far out for now. Secondly, browsers have <strong>not yet been optimized</strong> for such workflows. For example, Chrome will trigger <a href="https://www.chromium.org/developers/design-documents/inter-process-communication">inter-process communications</a> (IPCs) linear to the number of resources, so including hundreds of resources will have browser runtime costs.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24d7fcb0-40c3-4ada-abb3-22b8524f9b2d/progressive-css-loading-opt.png" sizes="100vw" caption="To achieve best results with HTTP/2, consider to <a href='https://jakearchibald.com/2016/link-in-body/'>load CSS progressively</a>, as suggested by Chrome’s Jake Archibald." alt="HTML code using progressive CSS loading" >}}

<p>Still, you can try to <a href="https://jakearchibald.com/2016/link-in-body/">load CSS progressively</a>. In fact, in-body CSS <a href="https://twitter.com/patmeenan/status/1037027969842208777">no longer blocks rendering for Chrome</a>. But <a href="https://twitter.com/csswizardry/status/1133867804380270592">there are some prioritization issues</a> so it’s not as straightforward, but worth experimenting with.</p>

<p>You could get away with <a href="https://daniel.haxx.se/blog/2016/08/18/http2-connection-coalescing/">HTTP/2 connection coalescing</a>, which allows you to use domain sharding while benefiting from HTTP/2, but achieving this in practice is difficult, and in general, it’s not considered to be good practice. Also, <a href="https://nooshu.github.io/blog/2019/12/17/http2-and-sri-dont-always-get-on/">HTTP/2 and Subresource Integrity don’t always get on</a>.</p>

<p>What to do? Well, if you’re running over HTTP/2, sending around <strong>6–10 packages</strong> seems like a decent compromise (and isn’t too bad for legacy browsers). Experiment and measure to find the right balance for your website.</p></li>

<li><strong>Do we send all assets over a single HTTP/2 connection?</strong><br />One of the main advantages of HTTP/2 is that it allows us to send assets down the wire over a single connection. However, sometimes we might have done something wrong &mdash; e.g. have a CORS issue, or misconfigured the <code>crossorigin</code> attribute, so the browser would be forced to open a new connection.

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

<li><strong>Do your servers and CDNs support HTTP/3?</strong><br />While HTTP/2 has brought a number of significant performance improvements to the web, it also left quite some area for improvement &mdash; especially <a href="https://youtu.be/SuSpghHP0uI?t=290">head-of-line blocking in TCP</a>, which was noticeable on a slow network with a significant packet loss. <a href="https://youtu.be/SuSpghHP0uI?t=290">HTTP/3 is solving these issues for good</a> (<a href="https://calendar.perfplanet.com/2020/head-of-line-blocking-in-quic-and-http-3-the-details/">article</a>).

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


## Table Of Contents

<ol>
  <li><a href="/2021/01/front-end-performance-getting-ready-planning-metrics/">Getting Ready: Planning And Metrics</a></li>
  <li><a href="/2021/01/front-end-performance-setting-realistic-goals/">Setting Realistic Goals</a></li>
  <li><a href="/2021/01/front-end-performance-defining-the-environment/">Defining The Environment</a></li>
  <li><a href="/2021/01/front-end-performance-assets-optimizations/">Assets Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-build-optimizations/">Build Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-delivery-optimizations/">Delivery Optimizations</a></li>
  <li><strong>Networking, HTTP/2, HTTP/3</strong></li>
  <li><a href="/2021/01/front-end-performance-testing-monitoring/">Testing And Monitoring</a></li>
  <li><a href="/2021/01/front-end-performance-quick-wins/">Quick Wins</a></li>
  <li><strong><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/">Everything on one page</a></strong></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/#download-the-checklist">Download The Checklist (PDF, Apple Pages, MS Word)</a></li>
  <li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next guides.</li>
</ol>

{{< signature "il" >}}

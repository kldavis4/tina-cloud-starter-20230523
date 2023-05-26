---
title: 'Front End Performance Checklist 2017 [PDF, Apple Pages]'
slug: front-end-performance-checklist-2017-pdf-pages
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea4a8281-f83c-49cd-9654-30de76c403ad/performance-budget-lbp9l7-c-scalew-689-opt.png
date: 2016-12-21T19:33:28.000Z
summary: >-
  Are you using progressive booting already? What about **tree-shaking and
  code-splitting** in React and Angular? Have you set up Brotli or Zopfli
  compression, OCSP stapling and HPACK compression? Also, how about resource
  hints, client hints and CSS containment — not to mention IPv6, HTTP/2 and
  service workers? A front-end performance checklist of things to keep in mind
  when optimizing for performance.
description: >-
  Are you using progressive booting already? What about tree-shaking and
  code-splitting in React and Angular? Have you set up Brotli or Zopfli
  compression, OCSP stapling and HPACK compression? Also, how about resource
  hints, client hints and CSS containment — not to mention IPv6, HTTP/2 and
  service workers? A front-end performance checklist of things to keep in mind
  when optimizing for performance.
categories:
  - UX
  - Checklists
  - Performance
---
Are you using progressive booting already? What about **tree-shaking and code-splitting** in React and Angular? Have you set up Brotli or Zopfli compression, OCSP stapling and HPACK compression? Also, how about resource hints, client hints and CSS containment — not to mention IPv6, HTTP/2 and service workers?

<figure><img
sizes="(max-width: 1500px) 800px, 1408px"
srcset="
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/711017d3-39af-4d0a-9db4-f9c0cdaf8011/app-build-components-dibweb-c-scalew-200-opt.png 200w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94239360-13ad-4c92-a028-1a1ded3004ab/app-build-components-dibweb-c-scalew-585-opt.png 585w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4716e5-d25b-4b80-b468-f28d07bae685/app-build-components-dibweb-c-scalew-879-opt.png 879w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37242721-6fb5-4cd0-ab67-c659716ef3db/app-build-components-dibweb-c-scalew-1408-opt.png 1408w"
src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4716e5-d25b-4b80-b468-f28d07bae685/app-build-components-dibweb-c-scalew-879-opt.png"
width="500" height="279" title="Front End Performance Checklist 2017 [PDF, Apple Pages]" alt="front end performance" /></figure>

Back in the day, performance was often a mere **afterthought**. Often deferred till the very end of the project, it would boil down to minification, concatenation, asset optimization and potentially a few fine adjustments on the server’s `config` file. Looking back now, things seem to have changed quite significantly.

Performance isn’t just a technical concern: It matters, and when baking it into the workflow, design decisions have to be informed by their performance implications. Performance has to be measured, monitored and refined continually, and the growing complexity of the web poses new challenges that make it hard to keep track of metrics, because metrics will vary significantly depending on the device, browser, protocol, network type and latency (CDNs, ISPs, caches, proxies, firewalls, load balancers and servers all play a role in performance).

So, if we created an overview of all the things we have to keep in mind when improving performance — from the very start of the process until the final release of the website — what would that list look like? Below you’ll find a (hopefully unbiased and objective) **front-end performance checklist for 2017** — an overview of the issues you might need to consider to ensure that your response times are fast and your website smooth.

{{% feature-panel %}}

(You can also just [download the checklist PDF](https://smashingmagazine.com/provide/performance-checklist/performance-checklist-1.0.pdf) (0.129 MB) or [download the checklist in Apple Pages](https://smashingmagazine.com/provide/performance-checklist/performance-checklist-1.0.pages) (0.236 MB). Happy optimizing!)

<style>ol.start { 
    counter-reset: perfcounter; 
}
ol.start li, ol.continue li {
    list-style: none;
    margin-bottom: 1.5em;
}
ol.start li:before, ol.continue li:before { 
    content: counters(perfcounter, '.', decimal-leading-zero);
    counter-increment: perfcounter;
    margin-left: -1.5em;
    margin-right: 2.4%;
    font-family: "Mija", Arial, sans-serif;
    display: inline-block;
    line-height: 1.1em;
    text-align: center;
    background-color: #E53B2C;
    color: #fff;
    padding: .65em .5em .5em .5em;
    border-radius: 11px; 
  }
ol.start p, ol.continue p {
    font-size: inherit;
}
</style>

## Front-End Performance Checklist 2017

Micro-optimizations are great for keeping a performance on track, but it’s critical to have clearly defined targets in mind — measurable goals that would influence any decisions made throughout the process. There are a couple of different models, and the ones discussed below are quite opinionated — just make sure to set your own priorities early on.</p>

### Getting Ready And Setting Goals

<ol class="start">
<li><strong>Be 20% faster than your fastest competitor.</strong><br>
According to <a href="https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/#the-need-for-performance-optimization-the-20-rule">psychological research</a>, if you want users to feel that your website is faster than any other website, you need to be at least 20% faster. Full-page loading time isn’t as relevant as metrics such as start rendering time, the <a href="https://developers.google.com/web/tools/lighthouse/audits/first-meaningful-paint">first meaningful paint</a> (i.e. the time required for a page to display its primary content) and the <a href="https://developers.google.com/web/tools/lighthouse/audits/time-to-interactive">time to interactive</a> (the time at which a page &mdash; and primarily a single-page application &mdash; appears to be ready enough that a user can interact with it).</p>

<p>Measure start rendering (with <a href="https://www.webpagetest.org/">WebPagetest</a>) and first meaningful paint times (with <a href="https://github.com/GoogleChrome/lighthouse">Lighthouse</a>) on a Moto G, a mid-range Samsung device and a good middle-of-the-road device like a Nexus 4, preferably in an <a href="https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/">open device lab</a> &mdash; on regular 3G, 4G and Wi-Fi connections.</p>

<figure><a href="https://github.com/GoogleChrome/lighthouse"><img
sizes="(max-width: 546px) 100vw, 546px"
srcset="
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/879f8085-d15f-470a-afc6-72557e49e077/lighthouse-ykpzcd-c-scalew-200-opt.png 200w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5e6423e-ffa1-486d-9c01-a5728f9ea1c4/lighthouse-ykpzcd-c-scalew-340-opt.png 340w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3388c7d0-8ef6-4332-b41c-a0147ad0ca2b/lighthouse-ykpzcd-c-scalew-546-opt.png 546w"
src="https://www.smashingmagazine.com/wp-content/uploads/2016/12/lighthouse_ykpzcd_c_scalew_546.png"
alt="Google's Lighthouse tool" /></a><figcaption>Lighthouse, a new performance auditing tool by Google.</figcaption></figure>

Look at your analytics to see what your users are on. You can then mimic the 90th percentile’s experience for testing. Collect data, set up a <a href="https://danielmall.com/articles/how-to-make-a-performance-budget/">spreadsheet</a>, shave off 20%, and set up your goals (i.e. <a href="https://bradfrost.com/blog/post/performance-budget-builder/">performance budgets</a>) this way. Now you have something measurable to test against. If you're keeping the budget in mind and trying to ship down just the minimal script to get a quick time-to-interactive value, then you're on a reasonable path.</p>

<figure><a href="https://bradfrost.com/blog/post/performance-budget-builder/"><img
sizes="(max-width: 1500px) 800px, 1241px"
srcset="
https://www.smashingmagazine.com/wp-content/uploads/2016/12performance-budget_lbp9l7_c_scalew_200-opt.png 200w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d17309d1-1c0e-4d14-a97d-704aa069bd54/performance-budget-lbp9l7-c-scalew-486-opt.png 486w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea4a8281-f83c-49cd-9654-30de76c403ad/performance-budget-lbp9l7-c-scalew-689-opt.png 689w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/231e97c1-4bfa-4dff-85a7-93e0a16b2690/performance-budget-lbp9l7-c-scalew-862-opt.png 862w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81d633e9-a289-46de-8fd0-1b59eb85aa42/performance-budget-lbp9l7-c-scalew-1027-opt.png 1027w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fae6202b-c578-4eea-a677-53e06f8de6a5/performance-budget-lbp9l7-c-scalew-1180-opt.png 1180w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48236920-27c6-47b6-804a-0936ac193bba/performance-budget-lbp9l7-c-scalew-1241-opt.png 1241w"
src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/231e97c1-4bfa-4dff-85a7-93e0a16b2690/performance-budget-lbp9l7-c-scalew-862-opt.png"
alt="Performance budget builder by Brad Frost" /></a><figcaption><a href="https://bradfrost.com/blog/post/performance-budget-builder/">Performance budget builder</a> by Brad Frost.</figcaption></figure>

<strong>Share the checklist with your colleagues.</strong> Make sure that the checklist is familiar to every member of your team to avoid misunderstandings down the line. Every decision has performance implications, and the project would hugely benefit from front-end developers being actively involved when the concept, UX and visual design are decided on. Map design decisions against performance budget and the priorities defined in the checklist.</p></li>

<li><strong>100-millisecond response time, 60 frames per second.</strong><br>
The <a href="https://www.smashingmagazine.com/2015/10/rail-user-centric-model-performance/">RAIL performance model</a> gives you healthy targets: Do your best to provide feedback in less than 100 milliseconds after initial input. To allow for &lt;100 milliseconds response, the page must yield control back to main thread at latest after every &lt;50 milliseconds. For high pressure points like animation, it's best to do nothing else where you can and the absolute minimum where you can't.</p>

<p>Also, each frame of animation should be completed in less than 16 milliseconds, thereby achieving 60 frames per second (1 second ÷ 60 = 16.6 milliseconds) — preferably under 10 milliseconds. Because the browser needs time to paint the new frame to the screen your code should finish executing before hitting the 16.6 milliseconds mark. <a href="https://info.meteor.com/blog/optimistic-ui-with-meteor-latency-compensation">Be optimistic</a> and use the idle time wisely. Obviously, these targets apply to runtime performance, rather than loading performance.</p></li>

<li><strong>First meaningful paint under 1.25 seconds, SpeedIndex under 1000.</strong><br>
Although it might be very difficult to achieve, your ultimate goal should be a start rendering time under 1 second and a <a href="https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index">SpeedIndex</a> value under 1000 (on a fast connection). For the first meaningful paint, count on 1250 milliseconds at most. For mobile, a start rendering time under 3 seconds for 3G on a mobile device is <a href="https://www.soasta.com/blog/google-mobile-web-performance-study/">acceptable</a>. Being slightly above that is fine, but push to get these values as low as possible.</li>
</ol>

### Defining the Environment

<ol class="continue">
<li><strong>Choose and set up your build tools.</strong><br>
Don’t pay much attention to what’s supposedly cool these days. Stick to your environment for building, be it Grunt, Gulp, Webpack, PostCSS or a combination of tools. As long as you are getting results fast and you have no issues maintaining your build process, you’re doing just fine.</li>

<li><strong>Progressive enhancement.</strong><br>
Keeping <a href="https://www.aaron-gustafson.com/notebook/insert-clickbait-headline-about-progressive-enhancement-here/">progressive enhancement</a> as the guiding principle of your front-end architecture and deployment is a safe bet. Design and build the core experience first, and then enhance the experience with advanced features for capable browsers, creating <a href="https://resilientwebdesign.com/">resilient</a> experiences. If your website runs fast on a slow machine with a poor screen in a poor browser on a suboptimal network, then it will only run faster on a fast machine with a good browser on a decent network.</li>

<li><strong>Angular, React, Ember and co.</strong><br>
Favor a framework that enables server-side rendering. Be sure to measure boot times in server- and client-rendered modes on mobile devices before settling on a framework (because changing that afterwards, due to performance issues, can be extremely hard). If you do use a JavaScript framework, make sure your choice <a href="https://www.youtube.com/watch?v=6I_GwgoGm1w">is informed</a> and <a href="https://medium.com/@ZombieCodeKill/choosing-a-javascript-framework-535745d0ab90#.2op7rjakk">well considered</a>. Different frameworks will have different effects on performance and will require different strategies of optimization, so you have to clearly understand all of the nuts and bolts of the framework you’ll be relying on. When building a web app, look into the <a href="https://developers.google.com/web/fundamentals/performance/prpl-pattern/">PRPL pattern</a> and <a href="https://developers.google.com/web/updates/2015/11/app-shell">application shell architecture</a>.</li>

<figure><a href="https://developers.google.com/web/fundamentals/performance/prpl-pattern/"><img
sizes="(max-width: 1500px) 800px, 1408px"
srcset="
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/711017d3-39af-4d0a-9db4-f9c0cdaf8011/app-build-components-dibweb-c-scalew-200-opt.png 200w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94239360-13ad-4c92-a028-1a1ded3004ab/app-build-components-dibweb-c-scalew-585-opt.png 585w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4716e5-d25b-4b80-b468-f28d07bae685/app-build-components-dibweb-c-scalew-879-opt.png 879w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37242721-6fb5-4cd0-ab67-c659716ef3db/app-build-components-dibweb-c-scalew-1408-opt.png 1408w"
src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4716e5-d25b-4b80-b468-f28d07bae685/app-build-components-dibweb-c-scalew-879-opt.png"
alt="PRPL Pattern in the application shell architecture" /></a><figcaption>
PRPL stands for Pushing critical resource, Rendering initial route, Pre-caching remaining routes and Lazy-loading remaining routes on demand.</figcaption></figure>

<figure><a href="https://developers.google.com/web/updates/2015/11/app-shell"><img
sizes="(max-width: 1500px) 800px, 1249px"
srcset="
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f025a20d-3724-4030-893f-d25fb0c38a39/appshell-1-o0t8qd-c-scalew-200-opt.jpg 200w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62cc0b90-8f5b-4c7d-b436-af9bf4d5b859/appshell-1-o0t8qd-c-scalew-451-opt.jpg 451w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d66bcac-6940-4e68-89a3-7a8dfebe87e2/appshell-1-o0t8qd-c-scalew-644-opt.jpg 644w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6423db84-4717-4aeb-9174-7ae96bf4f3aa/appshell-1-o0t8qd-c-scalew-799-opt.jpg 799w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2d79f5e-b986-40ef-bf76-8459629532e5/appshell-1-o0t8qd-c-scalew-943-opt.jpg 943w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f420dc21-7fcc-4dff-b6b6-f50930b60319/appshell-1-o0t8qd-c-scalew-1086-opt.jpg 1086w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e93e80c-4419-484d-8ba3-959356a03df3/appshell-1-o0t8qd-c-scalew-1239-opt.jpg 1239w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f882bf2b-dbbb-47f0-b7af-093cb86e1eca/appshell-1-o0t8qd-c-scalew-1249-opt.jpg 1249w"
src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6423db84-4717-4aeb-9174-7ae96bf4f3aa/appshell-1-o0t8qd-c-scalew-799-opt.jpg"
alt="Application shell architecture" /></a><figcaption>An <a href="https://developers.google.com/web/updates/2015/11/app-shell">application shell</a> is the minimal HTML, CSS, and JavaScript powering a user interface.</a></figcaption></figure>

<li><strong>AMP or Instant Articles?</strong><br>
Depending on the priorities and strategy of your organization, you might want to consider using Google’s <a href="https://www.ampproject.org/">AMP</a> or Facebook’s <a href="https://instantarticles.fb.com/">Instant Articles</a>. You can achieve good performance without them, but AMP does provide a solid performance framework with a free content delivery network (CDN), while Instant Articles will boost your performance on Facebook. You could build <a href="https://www.smashingmagazine.com/2016/12/progressive-web-amps/">progressive web AMPs</a>, too.</li>

<li><strong>Choose your CDN wisely.</strong><br>
Depending on how much dynamic data you have, you might be able to “outsource” some part of the content to a <a href="https://www.smashingmagazine.com/2015/11/static-website-generators-jekyll-middleman-roots-hugo-review/">static site generator</a>, pushing it to a CDN and serving a static version from it, thus avoiding database requests. You could even choose a <a href="https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/">static-hosting platform</a> based on a CDN, enriching your pages with interactive components as enhancements (<a href="https://jamstack.org/">JAMStack</a>).</p>

<p>Notice that CDNs can serve (and offload) dynamic content as well? So, restricting your CDN to static assets is not necessary. Double-check whether your CDN performs content compression and conversion, smart HTTP/2 delivery, edge-side includes, which assemble static and dynamic parts of pages at the CDN’s edge (i.e. the server closest to the user), and other tasks.</p>
</li>
</ol>

### Build Optimizations

<ol class="continue">
<li><strong>Set your priorities straight.</strong><br>
It’s a good idea to know what you are dealing with first. Run an inventory of all of your assets (JavaScript, images, fonts, third-party scripts and “expensive” modules on the page, such as carousels, complex infographics and multimedia content), and break them down in groups.</p>

<p>Set up a spreadsheet. Define the basic <strong>core</strong> experience for legacy browsers (i.e. fully accessible core content), the <strong>enhanced</strong> experience for capable browsers (i.e. the enriched, full experience) and the <strong>extras</strong> (assets that aren’t absolutely required and can be lazy-loaded, such as web fonts, unnecessary styles, carousel scripts, video players, social media buttons, large images). We published an article on “<a href="https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/">Improving Smashing Magazine’s Performance</a>,” which describes this approach in detail.</p></li>

<li><strong>Use the “cutting-the-mustard” technique.</strong><br>
Use the <a href="https://responsivenews.co.uk/post/18948466399/cutting-the-mustard">cutting-the-mustard technique</a> to send the core experience to legacy browsers and an enhanced experience to modern browsers. Be strict in loading your assets: Load the core experience immediately, the enhancements on <code>DomContentLoaded</code> and the extras on the <code>load</code> event.</p>

<p>Note that the technique deduces device capability from browser version, which is no longer something we can do these days. For example, cheap Android phones in developing countries mostly run Chrome and will cut the mustard despite their limited memory and CPU capabilities. Beware that, while we don’t really have an alternative, use of the technique has become more limited recently.</p></li>

<li><strong>Consider micro-optimization and progressive booting.</strong><br>
In some apps, you might need some time to initialize the app before you can render the page. Display <a href="https://twitter.com/lukew/status/665288063195594752">skeleton screens</a> instead of loading indicators. Look for modules and techniques to speed up the initial rendering time (for example, <a href="https://medium.com/@richavyas/aha-moments-from-ngconf-2016-part-1-angular-2-0-compile-cycle-6f462f68632e#.8b9afnsub">tree-shaking</a> and <a href="https://webpack.github.io/docs/code-splitting.html">code-splitting</a>), because most performance issues come from the initial parsing time to bootstrap the app. Also, use an <a href="https://www.lucidchart.com/techblog/2016/09/26/improving-angular-2-load-times/">ahead-of-time compiler</a> to <a href="https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/">offload some of the client-side rendering</a> to the <a href="https://redux.js.org/docs/recipes/ServerRendering.html">server</a> and, hence, output usable results quickly. Finally, consider using <a href="https://github.com/nolanlawson/optimize-js">Optimize.js</a> for faster initial loading by wrapping eagerly invoked functions (it <a href="https://twitter.com/tverwaes/status/809788255243739136">might not be necessary</a> any longer, though).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab06acd3-833a-4634-abf9-fc8d91939250/fmp-and-tti-opt.jpeg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab06acd3-833a-4634-abf9-fc8d91939250/fmp-and-tti-opt.jpeg" width="736" height="351" alt="Progressive booting" /></a><figcaption><a href="https://aerotwist.com/blog/when-everything-is-important-nothing-is/">Progressive booting</a> means using server-side rendering to get a quick first meaningful paint, but also include some minimal JavaScript to keep the time-to-interactive close to the first meaningful paint.</figcaption></figure>

Client-side rendering or server-side rendering? In both scenarios, our goal should be to set up <a href="https://aerotwist.com/blog/when-everything-is-important-nothing-is/">progressive booting</a>: Use server-side rendering to get a quick first meaningful paint, but also include some minimal JavaScript to keep the time-to-interactive close to the first meaningful paint. We can then, either on demand or as time allows, boot non-essential parts of the app. Unfortunately, as <a href="https://aerotwist.com/blog/when-everything-is-important-nothing-is/#which-to-use-progressive-booting">Paul Lewis noticed</a>, frameworks typically have no concept of priority that can be surfaced to developers, and hence progressive booting is difficult to implement with most libraries and frameworks. If you have the time and resources, use this strategy to ultimately boost performance.</p>
</li>

<li><strong>Are HTTP cache headers set properly?</strong><br>
Double-check that <code>expires</code>, <code>cache-control</code>, <code>max-age</code> and other HTTP cache headers have been set properly. In general, resources should be cacheable either for a very short time (if they are likely to change) or indefinitely (if they are static) &mdash; you can just change their version in the URL when needed.</p>

<p>If possible, use <code>Cache-control: immutable</code>, designed for fingerprinted static resources, to avoid revalidation (as of December 2016, <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control">supported only in Firefox</a> on <code>https://</code> transactions). You can use <a href="https://devcenter.heroku.com/articles/increasing-application-performance-with-http-cache-headers">Heroku’s primer on HTTP caching headers</a>, Jake Archibald’s “<a href="https://jakearchibald.com/2016/caching-best-practices/">Caching Best Practices</a>” and Ilya Grigorik’s <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching?hl=en">HTTP caching primer</a> as guides.</p></li>

<li><strong>Limit third-party libraries, and load JavaScript asynchronously.</strong><br>
When the user requests a page, the browser fetches the HTML and constructs the DOM, then fetches the CSS and constructs the CSSOM, and then generates a rendering tree by matching the DOM and CSSOM. If any JavaScript needs to be resolved, the browser won’t start rendering the page until it’s resolved, thus delaying rendering. As developers, we have to explicitly tell the browser not to wait and to start rendering the page. The way to do this for scripts is with the <code>defer</code> and <code>async</code> attributes in HTML.</p>

<p>In practice, it turns out we should <a href="https://calendar.perfplanet.com/2016/prefer-defer-over-async/">prefer <code>defer</code> to <code>async</code></a> (at a <a href="https://github.com/h5bp/lazyweb-requests/issues/42">cost to users of Internet Explorer</a> up to and including version 9, because you’re likely to break scripts for them). Also, limit the impact of third-party libraries and scripts, especially with social sharing buttons and <code>&lt;iframe&gt;</code> embeds (such as maps). You can use <a href="https://www.savjee.be/2015/01/Creating-static-social-share-buttons/">static social sharing buttons</a> (such as by <a href="https://simplesharingbuttons.com">SSBG</a>) and <a href="https://developers.google.com/maps/documentation/static-maps/intro">static links to interactive maps</a> instead.</p></li>

<li><strong>Are images properly optimized?</strong><br>
As far as possible, use <a href="https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/">responsive images</a> with <code>srcset</code>, <code>sizes</code> and the <code>&lt;picture&gt;</code> element. While you’re at it, you could also make use of the <a href="https://www.smashingmagazine.com/2015/10/webp-images-and-performance/">WebP format</a> by serving WebP images with the <code>&lt;picture&gt;</code> element and a JPEG fallback (see Andreas Bovens’ <a href="https://dev.opera.com/articles/responsive-images/#different-image-types-use-case">code snippet</a>) or by using content negotiation (using <code>Accept</code> headers). Sketch natively supports WebP, and WebP images can be exported from Photoshop using a <a href="https://telegraphics.com.au/sw/product/WebPFormat#webpformat">WebP plugin for Photoshop</a>. <a href="https://developers.google.com/speed/webp/docs/using">Other options are available</a>, too.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dbb3fa7-ed16-45a1-b3d6-b05541a159ae/responsive-image-breakpoints-generator-large-opt.jpeg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09628891-6457-4f07-a457-9d5aa6962ec6/responsive-image-breakpoints-generator-750w-opt.jpeg" width="750" height="526" alt="Responsive Image Breakpoints Generator" /></a><figcaption><a href="https://www.responsivebreakpoints.com/">Responsive Image Breakpoints Generator</a> automates images and markup generation.</figcaption></figure>

You can also use <a href="https://www.smashingmagazine.com/2016/01/leaner-responsive-images-client-hints/">client hints</a>, which are now <a href="https://caniuse.com/#search=client-hints">gaining browser support</a>. Not enough resources to bake in sophisticated markup for responsive images? Use the <a href="https://www.responsivebreakpoints.com/">Responsive Image Breakpoints Generator</a> or a service such as <a href="https://cloudinary.com/documentation/api_and_access_identifiers">Cloudinary</a> to automate image optimization. Also, in many cases, using <code>srcset</code> and <code>sizes</code> alone will reap significant benefits. On Smashing Magazine, we use the postfix <code>-opt</code> for image names &mdash; for example, <code>brotli-compression-opt.png</code>; whenever an image contains that postfix, everybody on the team knows that it’s been optimized.</p></li>

<li><strong>Take image optimization to the next level.</strong><br>
When you’re working on a landing page on which it’s critical that a particular image loads blazingly fast, make sure that JPEGs are progressive and compressed with <a href="https://github.com/mozilla/mozjpeg">mozJPEG</a> (which improves the start rendering time by manipulating scan levels), <a href="https://css-ig.net/pingo">Pingo</a> for PNG, <a href="https://kornel.ski/lossygif">Lossy GIF</a> for GIF and <a href="https://jakearchibald.github.io/svgomg/">SVGOMG</a> for SVG. Blur out unnecessary parts of the image (by applying a Gaussian blur filter to them) to reduce the file size, and eventually you might even start to remove colors or make a picture black and white to reduce the size further. For background images, exporting photos from Photoshop with 0 to 10% quality can be absolutely acceptable as well.</p>

<p>Not good enough? Well, you can also improve perceived performance for images with the <a href="https://csswizardry.com/2016/10/improving-perceived-performance-with-multiple-background-images/">multiple</a> <a href="https://jmperezperez.com/medium-image-progressive-loading-placeholder/">background</a> <a href="https://manu.ninja/dominant-colors-for-lazy-loading-images#tiny-thumbnails">images</a> <a href="https://css-tricks.com/the-blur-up-technique-for-loading-background-images/">technique</a>.</p></li>

<li><strong>Are web fonts optimized?</strong><br>
Chances are high that the web fonts you are serving include glyphs and extra features that aren’t being used. You can ask your type foundry to subset web fonts or <a href="https://www.fontsquirrel.com/tools/webfont-generator">subset them yourself</a> if you are using open-source fonts (for example, by including only Latin with some special accent glyphs) to minimize their file sizes. <a href="https://caniuse.com/#search=woff2">WOFF2 support</a> is great, and you can use WOFF and OTF as fallbacks for browsers that don’t support it. Also, choose one of the strategies from Zach Leatherman’s “<a href="https://www.zachleat.com/web/comprehensive-webfonts/">Comprehensive Guide to Font-Loading Strategies</a>,” and use a service worker cache to cache fonts persistently. Need a quick win? Pixel Ambacht has a <a href="https://pixelambacht.nl/2016/font-awesome-fixed/">quick tutorial and case study</a> to get your fonts in order.</p>

<figure><a href="https://www.zachleat.com/web/comprehensive-webfonts/"><img
sizes="(max-width: 1500px) 800px, 1528px"
srcset="
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a13dd3b-c35d-42ea-8a9b-ace4157ba85d/zach-web-fonts-c8nq74-c-scalew-200-opt.png 200w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f26c58b-7051-4534-8788-91de1b119f87/zach-web-fonts-c8nq74-c-scalew-554-opt.png 554w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5f856a2-1a21-46a0-957b-6cd23dcff116/zach-web-fonts-c8nq74-c-scalew-875-opt.png 875w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad774121-2cee-4723-9c72-39962731be9e/zach-web-fonts-c8nq74-c-scalew-1528-opt.png 1528w"
src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5f856a2-1a21-46a0-957b-6cd23dcff116/zach-web-fonts-c8nq74-c-scalew-875-opt.png"
alt="Zach Leatherman's Comprehensive Guide to Font-Loading Strategies" /></a><figcaption>Zach Leatherman’s <a href="https://www.zachleat.com/web/comprehensive-webfonts/">Comprehensive Guide to Font-Loading Strategies</a> provides a dozen of options for bettern web font delivery.</figcaption></figure>

If you can’t serve fonts from your server and are relying on third-party hosts, make sure to use <a href="https://github.com/typekit/webfontloader">Web Font Loader</a>. <a href="https://www.filamentgroup.com/lab/font-events.html">FOUT is better than FOIT</a>; start rendering text in the fallback right away, and load fonts asynchronously &mdash; you could also use <a href="https://github.com/filamentgroup/loadCSS">loadCSS</a> for that. You might be able to <a href="https://www.smashingmagazine.com/2015/11/using-system-ui-fonts-practical-guide/">get away with locally installed OS fonts</a> as well.</p></li>

<li><strong>Push critical CSS quickly.</strong><br>
To ensure that browsers start rendering your page as quickly as possible, it’s become a <a href="https://www.smashingmagazine.com/2015/08/understanding-critical-css/">common practice</a> to collect all of the CSS required to start rendering the first visible portion of the page (known as “critical CSS” or “above-the-fold CSS”) and add it inline in the <code>&lt;head&gt;</code> of the page, thus reducing roundtrips. Due to the limited size of packages exchanged during the slow start phase, your budget for critical CSS is around 14 KB. If you go beyond that, the browser will need addition roundtrips to fetch more styles. <a href="https://github.com/filamentgroup/criticalCSS">CriticalCSS</a> and <a href="https://github.com/addyosmani/critical">Critical</a> enable you to do just that. You might need to do it for every template you’re using. If possible, consider using the <a href="https://www.filamentgroup.com/lab/performance-rwd.html">conditional inlining approach</a> used by the Filament Group.</p>

<p>With HTTP/2, critical CSS could be stored in a separate CSS file and delivered via a server push without bloating the HTML. The catch is that server pushing isn’t supported consistently and has some caching issues (see slide 114 onwards of <a href="https://www.slideshare.net/Fastly/http2-what-no-one-is-telling-you">Hooman Beheshti’s presentation</a>). The effect could, in fact, <a href="https://calendar.perfplanet.com/2016/http2-push-the-details/">be negative</a> and bloat the network buffers, preventing genuine frames in the document from being delivered. Server pushing is much <a href="https://docs.google.com/document/d/1K0NykTXBbbbTlv60t5MyJvXjqKGsCVNYHyLEXIxYMv0/edit">more effective on warm connections</a> due to the TCP slow start. So, you might need to create a <a href="https://css-tricks.com/cache-aware-server-push/">cache-aware HTTP/2 server push mechanism</a>. Keep in mind, though, that the new <a href="https://calendar.perfplanet.com/2016/cache-digests-http2-server-push/"><code>cache-digest</code> specification</a> will negate the need to manually build these “cache-aware” servers.</p></li>

<li><strong>Use tree-shaking and code-splitting to reduce payloads.</strong><br>
<a href="https://medium.com/@roman01la/dead-code-elimination-and-tree-shaking-in-javascript-build-systems-fb8512c86edf">Tree-shaking</a> is a way to clean up your build process by only including code that is actually used in production. You can <a href="https://www.2ality.com/2015/12/webpack-tree-shaking.html">use Webpack 2 to eliminate unused exports</a>, and <a href="https://github.com/giakki/uncss">UnCSS</a> or <a href="https://github.com/geuis/helium-css">Helium</a> to remove unused styles from CSS. Also, you might want to consider learning how to <a href="https://csswizardry.com/2011/09/writing-efficient-css-selectors/">write efficient CSS selectors</a> as well as how to <a href="https://benfrain.com/css-performance-revisited-selectors-bloat-expensive-styles/">avoid bloat and expensive styles</a>.</p>

<p><a href="https://webpack.github.io/docs/code-splitting.html">Code-splitting</a> is another Webpack feature that splits your code base into “chunks” that are loaded on demand. Once you define split points in your code, Webpack takes care of the dependencies and outputted files. It basically enables you to keep the initial download small and to request code on demand, when requested by the application.</p>

<p>Note that <a href="https://rollupjs.org/">Rollup</a> shows significantly better results than Browserify exports. While we’re at it, you might want to check out <a href="https://github.com/nolanlawson/rollupify">Rollupify</a>, which converts ECMAScript 2015 modules into one big CommonJS module &mdash; because small modules can have a <a href="https://nolanlawson.com/2016/08/15/the-cost-of-small-modules/">surprisingly high performance cost</a> depending on your choice of bundler and module system.</p></li>

<li><strong>Improve rendering performance.</strong><br>
Isolate expensive components with <a href="https://caniuse.com/#search=contain">CSS containment</a> &mdash; for example, to limit the scope of the browser’s styles, of layout and paint work for off-canvas navigation, or of third-party widgets. Make sure that there is no lag when scrolling the page or when an element is animated, and that you’re consistently hitting 60 frames per second. If that’s not possible, then at least making the frames per second consistent is preferable to a mixed range of 60 to 15. Use CSS’ <a href="https://caniuse.com/#feat=will-change"><code>will-change</code></a> to inform the browser of which elements and properties will change.</p>

<p>Also, measure <a href="https://aerotwist.com/blog/my-performance-audit-workflow/#runtime-performance">runtime rendering performance</a> (for example, <a href="https://developers.google.com/web/tools/chrome-devtools/rendering-tools/">in DevTools</a>). To get started, check Paul Lewis’ free <a href="https://www.udacity.com/course/browser-rendering-optimization--ud860">Udacity course on browser-rendering optimization</a>. We also have a lil’ article by Sergey Chikuyonok on how to <a href="https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/">get GPU animation right</a>.</p></li>

<li><strong>Warm up the connection to speed up delivery.</strong><br>
Use skeleton screens, and lazy-load all expensive components, such as fonts, JavaScript, carousels, videos and iframes. Use <a href="https://w3c.github.io/resource-hints">resource hints</a> to save time on <a href="https://caniuse.com/#search=dns-prefetch"><code>dns-prefetch</code></a> (which performs a DNS lookup in the background), <a href="https://www.caniuse.com/#search=preconnect"><code>preconnect</code></a> (which asks the browser to start the connection handshake (DNS, TCP, TLS) in the background), <a href="https://caniuse.com/#search=prefetch"><code>prefetch</code></a> (which asks the browser to request a resource), <a href="https://caniuse.com/#search=prerender"><code>prerender</code></a> (which asks the browser to render the specified page in the background) and <a href="https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/"><code>preload</code></a> (which prefetches resources without executing them, among other things). Note that in practice, depending on browser support, you’ll prefer <code>preconnect</code> to <code>dns-prefetch</code>, and you’ll be cautious with using <code>prefetch</code> and <code>prerender</code> &mdash; the latter should only be used if you are very confident about where the user will go next (for example, in a purchasing funnel).</li>
</ol>

### HTTP/2

<ol class="continue">
<li><strong>Get ready for HTTP/2.</strong><br>
With Google <a href="https://security.googleblog.com/2016/09/moving-towards-more-secure-web.html">moving towards a more secure web</a> and eventual treatment of all HTTP pages in Chrome as being “not secure,” you’ll need to decide on whether to keep betting on HTTP/1.1 or set up an <a href="https://http2.github.io/faq/">HTTP/2 environment</a>. HTTP/2 is <a href="https://caniuse.com/#search=http2">supported very well</a>; it isn’t going anywhere; and, in most cases, you’re better off with it. The investment will be quite significant, but you’ll need to move to HTTP/2 sooner or later. On top of that, you can get a <a href="https://www.youtube.com/watch?v=RWLzUnESylc&t=1s&list=PLNYkxOF6rcIBTs2KPy1E6tIYaWoFcG3uj&index=25">major performance boost</a> with service workers and server push (at least long term).</p>

<figure><a href="https://security.googleblog.com/2016/09/moving-towards-more-secure-web.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30dd1821-9800-4f01-91a8-1375d4812144/http-pages-chrome-opt.png" width="400" height="194" alt="HTTP/2" /></a><figcaption>Eventually, Google plans to label all HTTP pages as non-secure, and change the HTTP security indicator to the red triangle that Chrome uses for broken HTTPS. (<a href="https://security.googleblog.com/2016/09/moving-towards-more-secure-web.html">Image source</a>)</figcaption></figure>

The downsides are that you’ll have to migrate to HTTPS, and depending on how large your HTTP/1.1 user base is (that is, users on legacy operating systems or with legacy browsers), you’ll have to send different builds, which would require you to adapt a <a href="https://rmurphey.com/blog/2015/11/25/building-for-http2">different build process</a>. Beware: Setting up both migration and a new build process might be tricky and time-consuming. For the rest of this article, I’ll assume that you’re either switching to or have already switched to HTTP/2.</p></li>

<li><strong>Properly deploy HTTP/2.</strong><br>
Again, <a href="https://www.youtube.com/watch?v=yURLTwZ3ehk">serving assets over HTTP/2</a> requires a major overhaul of how you’ve been serving assets so far. You’ll need to find a fine balance between packaging modules and loading many small modules in parallel.</p>

<p>On the one hand, you might want to avoid concatenating assets altogether, instead breaking down your entire interface into many small modules, compressing them as a part of the build process, referencing them via the <a href="https://rmurphey.com/blog/2015/11/25/building-for-http2">“scout” approach</a> and loading them in parallel. A change in one file won’t require the entire style sheet or JavaScript to be redownloaded.</p>

<p>On the other hand, <a href="https://engineering.khanacademy.org/posts/js-packaging-http2.htm">packaging still matters</a> because there are issues with sending many small JavaScript files to the browser. First, <strong>compression will suffer</strong>. The compression of a large package will benefit from dictionary reuse, whereas small separate packages will not. There’s standard work to address that, but it’s far out for now. Secondly, browsers have <strong>not yet been optimized</strong> for such workflows. For example, Chrome will trigger <a href="https://www.chromium.org/developers/design-documents/inter-process-communication">inter-process communications</a> (IPCs) linear to the number of resources, so including hundreds of resources will have browser runtime costs.</p>

<figure><a href="https://jakearchibald.com/2016/link-in-body/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24d7fcb0-40c3-4ada-abb3-22b8524f9b2d/progressive-css-loading-opt.png" alt="Progressive CSS loading" /></a><figcaption>To achieve best results with HTTP/2, consider to <a href="https://jakearchibald.com/2016/link-in-body/">load CSS progressively</a>, as suggested by Chrome's Jake Archibald.</figcaption></figure>

Still, you can try to <a href="https://jakearchibald.com/2016/link-in-body/">load CSS progressively</a>. Obviously, by doing so, you are actively penalizing HTTP/1.1 users, so you might need to generate and serve different builds to different browsers as part of your deployment process, which is where things get slightly more complicated. You could get away with <a href="https://daniel.haxx.se/blog/2016/08/18/http2-connection-coalescing/">HTTP/2 connection coalescing</a>, which allows you to use domain sharding while benefiting from HTTP/2, but achieving this in practice is difficult.</p>

<p>What to do? If you’re running over HTTP/2, sending around <strong>10 packages</strong> seems like a decent compromise (and isn’t too bad for legacy browsers). Experiment and measure to find the right balance for your website.</p></li>

<li><strong>Make sure the security on your server is bulletproof.</strong><br>
All browser implementations of HTTP/2 run over TLS, so you will probably want to avoid security warnings or some elements on your page not working. Double-check that your <a href="https://securityheaders.io/">security headers are set properly</a>, <a href="https://www.smashingmagazine.com/2016/01/eliminating-known-security-vulnerabilities-with-snyk/">eliminate known vulnerabilities</a>, and <a href="https://www.ssllabs.com/ssltest/">check your certificate</a>.</p>

<p>Haven’t migrated to HTTPS yet? Check <a href="https://https.cio.gov/faq/">The HTTPS-Only Standard</a> for a thorough guide. Also, make sure that all external plugins and tracking scripts are loaded via HTTPS, that cross-site scripting isn’t possible and that both <a href="https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet">HTTP Strict Transport Security headers</a> and <a href="https://content-security-policy.com/">Content Security Policy headers</a> are properly set.</li>

<li><strong>Do your servers and CDNs support HTTP/2?</strong><br>
Different servers and CDNs are probably going to support HTTP/2 differently. Use <a href="https://istlsfastyet.com">Is TLS Fast Yet?</a> to check your options, or quickly look up how your servers are performing and which features you can expect to be supported.</li>

<figure><a href="https://istlsfastyet.com"><img
sizes="(max-width: 1500px) 800px, 1393px"
srcset="
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a49a6d9-a72d-47f3-ab4a-d25157057f55/isitfastyet-doieve-c-scalew-589-opt.png 589w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4c81771-154b-4599-a309-b6b776d31e42/isitfastyet-doieve-c-scalew-1393-opt.png 1393w"
src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a49a6d9-a72d-47f3-ab4a-d25157057f55/isitfastyet-doieve-c-scalew-589-opt.png"
alt="Is TLS Fast Yet?" /></a><figcaption><a href="https://istlsfastyet.com">Is TLS Fast Yet?</a> allows you to check your options for servers and CDNs when switching to HTTP/2.</figcaption></figure>

<li><strong>Is Brotli or Zopfli compression in use?</strong><br>
Last year, Google <a href="https://opensource.googleblog.com/2015/09/introducing-brotli-new-compression.html">introduced</a> <a href="https://github.com/google/brotli">Brotli</a>, a new open-source lossless data format, which is now <a href="https://caniuse.com/#search=brotli">widely supported</a> in Chrome, Firefox and Opera. In practice, Brotli appears to be <a href="https://samsaffron.com/archive/2016/06/15/the-current-state-of-brotli-compression">more effective</a> than Gzip and Deflate. It might be slow to compress, depending on the settings, and slower compression will ultimately lead to higher compression rates. Still, it decompresses fast. Because the algorithm comes from Google, it’s not surprising that browsers will accept it only if the user is visiting a website over HTTPS &mdash; and yes, there are technical reasons for that as well. The catch is that Brotli doesn’t come preinstalled on most servers today, and it’s not easy to set up without self-compiling NGINX or Ubuntu. However, you can <a href="https://calendar.perfplanet.com/2016/enabling-brotli-even-on-cdns-that-dont-support-it-yet/">enable Brotli even on CDNs that don’t support it</a> yet (with a service worker).</p>

<p>Alternatively, you could look into using <a href="https://blog.codinghorror.com/zopfli-optimization-literally-free-bandwidth/">Zopfli’s compression algorithm</a>, which encodes data to Deflate, Gzip and Zlib formats. Any regular Gzip-compressed resource would benefit from Zopfli’s improved Deflate encoding, because the files will be 3 to 8% smaller than Zlib’s maximum compression. The catch is that files will take around 80 times longer to compress. That’s why it’s a good idea to use Zopfli on resources that don’t change much, files that are designed to be compressed once and downloaded many times.</p></li>

<li><strong>Is OCSP stapling enabled?</strong><br>
By <a href="https://www.digicert.com/enabling-ocsp-stapling.htm">enabling OCSP stapling on your server</a>, you can speed up your TLS handshakes. The Online Certificate Status Protocol (OCSP) was created as an alternative to the Certificate Revocation List (CRL) protocol. Both protocols are used to check whether an SSL certificate has been revoked. However, the OCSP protocol does not require the browser to spend time downloading and then searching a list for certificate information, hence reducing the time required for a handshake.</li>

<li><strong>Have you adopted IPv6 yet?</strong><br>
Because we’re <a href="https://en.wikipedia.org/wiki/IPv4_address_exhaustion">running out of space with IPv4</a> and major mobile networks are adopting IPv6 rapidly (the US has <a href="https://www.google.com/intl/en/ipv6/statistics.html#tab=ipv6-adoption&tab=ipv6-adoption">reached</a> a 50% IPv6 adoption threshold), it’s a good idea to <a href="https://www.paessler.com/blog/2016/04/08/monitoring-news/ask-the-expert-current-status-on-ipv6">update your DNS to IPv6</a> to stay bulletproof for the future. Just make sure that dual-stack support is provided across the network &mdash; it allows IPv6 and IPv4 to run simultaneously alongside each other. After all, IPv6 is not backwards-compatible. Also, <a href="https://www.cloudflare.com/ipv6/">studies show</a> that IPv6 made those websites 10 to 15% faster due to neighbor discovery (NDP) and route optimization.</p></li>

<li><strong>Is HPACK compression in use?</strong><br>
If you’re using HTTP/2, double-check that your servers <a href="https://blog.cloudflare.com/hpack-the-silent-killer-feature-of-http-2/">implement HPACK compression</a> for HTTP response headers to reduce unnecessary overhead. Because HTTP/2 servers are relatively new, they may not fully support the specification, with HPACK being an example. <a href="https://github.com/summerwind/h2spec">H2spec</a> is a great (if very technically detailed) tool to check that. <a href="https://www.keycdn.com/blog/http2-hpack-compression/">HPACK works</a>.</li>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15891f86-c883-434a-8517-209273356ee6/h2spec-example-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efc02119-9155-4126-b7b9-bc83c4b16436/h2spec-example-750w-opt.png" width="750" height="878" alt="h2spec" /></a><figcaption>H2spec (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15891f86-c883-434a-8517-209273356ee6/h2spec-example-large-opt.png">View large version</a>) (<a href="https://github.com/summerwind/h2spec">Image source</a>)</figcaption></figure>

<li><strong>Are service workers used for caching and network fallbacks?</strong><br>
No performance optimization over a network can be faster than a locally stored cache on user’s machine. If your website is running over HTTPS, use the “<a href="https://github.com/lyzadanger/pragmatist-service-worker">Pragmatist’s Guide to Service Workers</a>” to cache static assets in a service worker cache and store offline fallbacks (or even offline pages) and retrieve them from the user’s machine, rather than going to the network. Also, check Jake’s <a href="https://jakearchibald.com/2014/offline-cookbook/">Offline Cookbook</a> and the free Udacity course “<a href="https://www.udacity.com/course/offline-web-applications--ud899">Offline Web Applications</a>.” Browser support? It’s <a href="https://caniuse.com/#search=serviceworker">getting there</a>, and the fallback is the network anyway.</li>
</ol>

<ol class="continue">
<li><strong>Monitor mixed-content warnings.</strong><br>
If you’ve recently migrated from HTTP to HTTPS, make sure to monitor both active and passive mixed-content warnings, with a tool such as <a href="https://report-uri.io/">Report-URI.io</a>. You can also use <a href="https://github.com/bramus/mixed-content-scan">Mixed Content Scan</a> to scan your HTTPS-enabled website for mixed content.</li>
<li><strong>Is your development workflow in DevTools optimized?</strong><br>
Pick a debugging tool and click on every single button. Make sure you understand how to analyze rendering performance and console output, and how to debug JavaScript and edit CSS styles. Umar Hansa recently prepared a (huge) <a href="https://umaar.github.io/devtools-optimise-your-web-development-workflow-2016/#/">slidedeck</a> and <a href="https://www.youtube.com/watch?v=N33lYfsAsoU">talk</a> covering dozens of obscure tips and techniques to be aware of when debugging and testing in DevTools.</li>
<li><strong>Have you tested in proxy browsers and legacy browsers?</strong> Testing in Chrome and Firefox is not enough. Look into how your website works in proxy browsers and legacy browsers. UC Browser and Opera Mini, for instance, have a <a href="https://gs.statcounter.com/#mobile_browser-as-monthly-201511-201611">significant market share in Asia</a> (up to 35% in Asia). <a href="https://www.webworldwide.io/">Measure average Internet speed</a> in your countries of interest to avoid big surprises down the road. Test with network throttling, and emulate a high-DPI device. <a href="https://www.browserstack.com">BrowserStack</a> is fantastic, but test on real devices as well.</li>
<li><strong>Is continuous monitoring set up?</strong><br>
Having a private instance of <a href="https://www.webpagetest.org/">WebPagetest</a> is always beneficial for quick and unlimited tests. Set up continuous monitoring of performance budgets with automatic alerts. Set your own user-timing marks to measure and monitor business-specific metrics. Look into using <a href="https://speedcurve.com/">SpeedCurve</a> to monitor changes in performance over time, and/or <a href="https://newrelic.com/browser-monitoring">New Relic</a> to get insights that WebPagetest cannot provide. Also, look into <a href="https://speedtracker.org">SpeedTracker</a>, <a href="https://github.com/GoogleChrome/lighthouse">Lighthouse</a> and <a href="https://calibreapp.com">Calibre</a>.</li>
</ol>

## Quick Wins

<p>This list is quite comprehensive, and completing all of the optimizations might take quite a while. So, if you had just 1 hour to get significant improvements, what would you do? Let’s boil it all down to <strong>10 low-hanging fruits</strong>. Obviously, before you start and once you finish, measure results, including start rendering time and SpeedIndex on a 3G and cable connection.</p>

<ol class="start">
<li>Your goal is a start rendering time under 1 second on cable and under 3 seconds on 3G, and a SpeedIndex value under 1000. Optimize for start rendering time and time-to-interactive.</li>
<li>Prepare critical CSS for your main templates, and include it in the <code>&lt;head&gt;</code> of the page. (Your budget is 14 KB).</li>
<li>Defer and lazy-load as many scripts as possible, both your own and third-party scripts — especially social media buttons, video players and expensive JavaScript.</li>
<li>Add resource hints to speed up delivery with faster <code>dns-lookup</code>, <code>preconnect</code>, <code>prefetch</code>, <code>preload</code> and <code>prerender</code>.</li>
<li>Subset web fonts and load them asynchronously (or just switch to system fonts instead).</li>
<li>Optimize images, and consider using WebP for critical pages (such as landing pages).</li>
<li>Check that HTTP cache headers and security headers are set properly.</li>
<li>Enable Brotli or Zopfli compression on the server. (If that’s not possible, don’t forget to enable Gzip compression.)</li>
<li>If HTTP/2 is available, enable HPACK compression and start monitoring mixed-content warnings. If you’re running over LTS, also enable OCSP stapling.</li>
<li>If possible, cache assets such as fonts, styles, JavaScript and images — actually, as much as possible! — in a service worker cache.</li>
</ol>

## Download The Checklist (PDF, Apple Pages)

<p>With this checklist in mind, you should be prepared for any kind of front-end performance project. Feel free to download the print-ready PDF of the checklist as well as an <strong>editable Apple Pages document</strong> to customize the checklist for your needs:</p>

<ul>
<li><a href="https://smashingmagazine.com/provide/performance-checklist/performance-checklist-1.0.pdf">Download the checklist PDF</a> (PDF, 0.129 MB)</li>
<li><a href="https://smashingmagazine.com/provide/performance-checklist/performance-checklist-1.0.pages">Download the checklist in Apple Pages</a> (.pages, 0.236 MB)</li>
</ul>

<p>If you need alternatives, you can also check the <a href="https://github.com/drublic/checklist">front-end checklist by Dan Rublic</a> and the “<a href="https://jonyablonski.com/designers-wpo-checklist/">Designer’s Web Performance Checklist</a>” by Jon Yablonski.</p>

## Off We Go!

<p>Some of the optimizations might be beyond the scope of your work or budget or might just be overkill given the legacy code you have to deal with. That’s fine! Use this checklist as a general (and hopefully comprehensive) guide, and create your own list of issues that apply to your context. But most importantly, test and measure your own projects to identify issues before optimizing. Happy performance results in 2017, everyone!</p>

<hr />

<p><em>Huge thanks to Anselm Hannemann, Patrick Hamann, Addy Osmani, Andy Davies, Tim Kadlec, Yoav Weiss, Rey Bango, Matthias Ott, Mariana Peralta, Jacob Groß, Tim Swalling, Bob Visser, Kev Adamson and Rodney Rehm for reviewing this article, as well as our fantastic community, which has shared techniques and lessons learned from its work in performance optimization for everybody to use. You are truly smashing!</em></p>

{{< signature "al" >}}


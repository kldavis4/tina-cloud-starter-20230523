---
title: 'Front-End Performance 2021: Build Optimizations'
slug: front-end-performance-build-optimizations
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
  <li><strong>Build Optimizations</strong></li>
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
  	  counter-set: perfcounter 27;
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


## Build Optimizations

<ol class="start">
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

<p><strong>Still not sure</strong> about when to use Web Workers, Web Assembly, streams, or perhaps WebGL JavaScript API to access the GPU? <a href="https://hyphaebeast.club/writing/accelerating-js/">Accelerating JavaScript</a> is a short but helpful guide that explains when to use what, and why &mdash; also with a handy flowchart and plenty of useful resources.</p>

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
<li><strong>Do we use partial hydration?</strong><br />With the amount of JavaScript used in applications, we need to figure out ways to send as little as possible to the client. One way of doing so &mdash; and we briefly covered it already &mdash; is with <a href="https://medium.com/@luke_schmuke/how-we-achieved-the-best-web-performance-with-partial-hydration-20fab9c808d5">partial hydration</a>. The idea is quite simple: instead of doing SSR and then sending the entire app to the client, only small pieces of the app's JavaScript would be sent to the client and then hydrated. We can think of it as multiple tiny React apps with multiple render roots on an otherwise static website.

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

<p>In a fantastic post on <a href="https://andydavies.me/blog/2020/10/02/reducing-the-site-speed-impact-of-third-party-tags/">"Reducing the Site-Speed Impact of Third-Party Tags"</a>, Andy Davies explores a strategy of minimizing the footprint of third-parties &mdash; from identifying their costs towards reducing their impact.</p>

<p>According to Andy, there are two ways tags impact site-speed &mdash; they compete for <strong>network bandwidth and processing time</strong> on visitors’ devices, and depending on how they’re implemented, they can delay HTML parsing as well. So the first step is to identify the impact that third-parties have, by <a href="https://andydavies.me/blog/2018/02/19/using-webpagetest-to-measure-the-impact-of-3rd-party-tags/">testing the site <em>with</em> and <em>without</em> scripts using WebPageTest</a>. With Simon Hearne’s <a href="https://requestmap.herokuapp.com/">Request Map</a>, we can also visualize third-parties on a page along with details on their size, type and what triggered their load.</p>

<p>Preferably <a href="https://www.twnsnd.com/posts/performant_third_party_scripts.html">self-host and use a single hostname</a>, but also <a href="https://www.soasta.com/blog/10-pro-tips-for-managing-the-performance-of-your-third-party-scripts/">use a request map</a> to exposes fourth-party calls and detect when the scripts change. You can use Harry Roberts' <a href="https://csswizardry.com/2018/05/identifying-auditing-discussing-third-parties/">approach for auditing third parties</a> and produce spreadsheets like <a href="https://docs.google.com/spreadsheets/d/1uTcRSoJAkXfIm2yfG5hvCSzvSZD9fAwXNQMVK3HdPMI/edit#gid=0">this one</a> (also check <a href="https://www.youtube.com/watch?v=bmIUYBNKja4">Harry's auditing workflow</a>).</p>

<p>Afterwards, we can explore <strong>lightweight alternatives to existing scripts</strong> and slowly replace duplicates and main culprits with lighter options. Perhaps some of the scripts could be <a href="https://www.tunetheweb.com/blog/adding-controls-to-google-tag-manager/#pixels">replaced with their fallback tracking pixel instead of the full tag</a>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4482ab7-e2d8-4333-be8b-7d49021ea109/loadyoutube-opt.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4482ab7-e2d8-4333-be8b-7d49021ea109/loadyoutube-opt.jpg" sizes="100vw" caption="Loading YouTube with facades, e.g. <a href='https://github.com/paulirish/lite-youtube-embed'>lite-youtube-embed</a> that’s significantly smaller than an actual YouTube player. (<a href='https://web.dev/third-party-facades/'>Image source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4482ab7-e2d8-4333-be8b-7d49021ea109/loadyoutube-opt.jpg'>Large preview</a>)" alt="Left example showing 3KB of JavaScript using the lite-youtube custom element, middle and right example showing +540KB of JavaScript with the lite-youtube custom element" >}}

<p>If it’s not viable, we can at least <a href="https://web.dev/third-party-facades/">lazy load third-party resources with facades</a>, i.e. a static element which looks similar to the actual embedded third-party, but is not functional and therefore much less taxing on the page load. The trick, then, is to <strong>load the actual embed only on interaction</strong>.</p>
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

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ab1567c-ba71-4274-922d-dc9a97275c6a/cache-retrieval-time.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ab1567c-ba71-4274-922d-dc9a97275c6a/cache-retrieval-time.png" sizes="100vw" caption="We assume that browser caches are near-instantaneous, but data shows that retrieving an object from cache can take hundreds of milliseconds! From Simon Hearne’s research on <a href='https://simonhearne.com/2020/network-faster-than-cache/'>When Network Is Faster Than Cache</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ab1567c-ba71-4274-922d-dc9a97275c6a/cache-retrieval-time.png'>Large preview</a>)" alt="A graph showing cache retrieval time by count of cached assets with different OS and browsers named on the right (from top to bottom): Desktop Chrome OS, Tablet Android OS, Mobile Android OS, Desktop Mac OS X, Desktop Windows, Desktop Linux" >}}


## Table Of Contents

<ol>
  <li><a href="/2021/01/front-end-performance-getting-ready-planning-metrics/">Getting Ready: Planning And Metrics</a></li>
  <li><a href="/2021/01/front-end-performance-setting-realistic-goals/">Setting Realistic Goals</a></li>
  <li><a href="/2021/01/front-end-performance-defining-the-environment/">Defining The Environment</a></li>
  <li><a href="/2021/01/front-end-performance-assets-optimizations/">Assets Optimizations</a></li>
  <li><strong>Build Optimizations</strong></li>
  <li><a href="/2021/01/front-end-performance-delivery-optimizations/">Delivery Optimizations</a></li>
  <li><a href="/2021/01/front-end-performance-networking-http2-http3/">Networking, HTTP/2, HTTP/3</a></li>
  <li><a href="/2021/01/front-end-performance-testing-monitoring/">Testing And Monitoring</a></li>
  <li><a href="/2021/01/front-end-performance-quick-wins/">Quick Wins</a></li>
  <li><strong><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/">Everything on one page</a></strong></li>
  <li><a href="/2021/01/front-end-performance-2021-free-pdf-checklist/#download-the-checklist">Download The Checklist (PDF, Apple Pages, MS Word)</a></li>
  <li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next guides.</li>
</ol>

{{< signature "il" >}}

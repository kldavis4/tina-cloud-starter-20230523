---
title: 'Build A PWA With Webpack And Workbox'
slug: pwa-webpack-workbox
author: jad-joubran
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/498a146e-27f0-421d-bb6b-909807d15e85/sw-network-tab.png
date: 2019-06-27T13:00:59+02:00
summary: >-
  This tutorial will help you transform an app that doesn’t work offline into a PWA that works offline and shows an update available icon. You’ll learn how to precache assets with workbox, handle dynamic caching as well as handle updates to your PWA. Follow along and see how you can also apply these techniques on your website.
description: >-
  This tutorial will help you transform an app that doesn’t work offline into a PWA that works offline and shows an update available icon. You’ll also learn how to precache assets with workbox, handle dynamic caching as well as handle updates to your PWA.
categories:
  - PWA
  - Apps
  - Techniques
---
<p>A Progressive Web App (PWA) is a site that uses modern technology to deliver app-like experiences on the web. It’s an umbrella term for new technologies such as the ‘web app manifest’, ‘service worker’, and more. When joined together, these technologies allow you to deliver fast and engaging user experiences with your website.</p>

<p>This article is a step-by-step tutorial for adding a service worker to an existing one-page website. The service worker will allow you to make your website work offline while also notifying your users of updates to your site. Please note that this is based on a small project that is bundled with Webpack, so we’ll be using the Workbox Webpack plugin (<a href="https://developers.google.com/web/tools/workbox/guides/migrations/migrate-from-v3">Workbox v4</a>).</p>

<p>Using a tool to generate your service worker is the recommended approach as it lets you manage your cache efficiently. We will be using <a href="https://github.com/GoogleChrome/workbox">Workbox</a> &mdash; a set of libraries that make it easy to generate your service worker code &mdash; to generate our service worker in this tutorial.</p>

<p>Depending on your project, you can use Workbox in three different ways:</p>

<ol>
  <li>A <strong>command-line interface</strong> is available which lets you integrate workbox into any application you have;</li>
  <li>A <strong>Node.js module</strong> is available which lets you integrate workbox into any Node build tool such as gulp or grunt;</li>
  <li>A <strong>webpack plugin</strong> is available which lets you easily integrate with a project that is built with Webpack.</li>
</ol>

<p><a href="https://webpack.js.org/">Webpack</a> is a module bundler. To simplify, you can think of it as a tool that manages your JavaScript dependencies. It allows you to import JavaScript code from libraries and bundles your JavaScript together into one or many files.</p>

{{% feature-panel %}}

<p>To get started, clone the following repository on your computer:</p>

<pre><code class="language-bash">git clone git@github.com:jadjoubran/workbox-tutorial-v4.git
cd workbox-tutorial-v4
npm install
npm run dev
</code></pre>

<p>Next, navigate to <code><a href="https://localhost:8080/">https://localhost:8080/</a></code>. You should be able to see the currency app we’ll be using throughout this tutorial:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/123ef4ad-dc69-4cdc-ae1e-3b7e2dd41375/our-app.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27919a12-d279-45a4-beeb-4131ac6c690b/pwa-webpack-workbox-our-app.png" sizes="70vw" caption="‘Currencies’ is a PWA that lists conversion fees of currencies against the Euro (€) currency. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/123ef4ad-dc69-4cdc-ae1e-3b7e2dd41375/our-app.png'>Large preview</a>)" alt="Screenshot of the currency app we’re building in this article." >}}

## Start With An App Shell

<p>The <a href="https://developers.google.com/web/fundamentals/architecture/app-shell">application shell</a> (or ‘app shell’) is a pattern inspired from Native Apps. It will help give your app a more native look. It simply provides the app with a layout and structure without any data &mdash; a transitional screen that is aimed to improve the loading experience of your web app.</p>

<p>Here are some examples of app shells from native apps:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/effb3dd1-f2e8-4b80-86da-e01490c4ba4a/native-inbox-shell.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a60e3e3-9c67-43e7-a204-6ba61dcbebd2/pwa-webpack-workbox-native-inbox-shell.png" sizes="70vw" caption="Google Inbox App Shell: A few milliseconds before the emails load into the app shell. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/effb3dd1-f2e8-4b80-86da-e01490c4ba4a/native-inbox-shell.png'>Large preview</a>)" alt="Google Inbox App Shell" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/379c934e-a1f1-425d-b152-3924c53097b8/native-twitter-shell.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9788b3a0-4a59-46af-97a7-86ba8b469cba/pwa-webpack-workbox-native-twitter-shell.png" sizes="70vw" caption="Twitter’s native app on Android: App shell showing navbar, tabs, and loader. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/379c934e-a1f1-425d-b152-3924c53097b8/native-twitter-shell.png'>Large preview</a>)" alt="Twitter native App Shell" >}}

<p>And here are examples of app shells from PWAs:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ae3c661-bf1f-4e6c-a6c0-44995b1a2f61/pwa-twitter-shell.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/561e0383-264c-4306-9491-9899e3cd5051/pwa-webpack-workbox-twitter-shell.png" sizes="70vw" caption="The app shell of Twitter’s PWA (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ae3c661-bf1f-4e6c-a6c0-44995b1a2f61/pwa-twitter-shell.png'>Large preview</a>)" alt="App Shell of Twitter’s PWA" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f4888b4-9760-472e-948b-0b18d917ca50/pwa-flipkart-shell.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4f84167-cad6-44a5-b20c-d5d632b092eb/pwa-webpack-workbox-flipkart-shell.png" sizes="70vw" caption="The app shell of Flipkart’s PWA (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f4888b4-9760-472e-948b-0b18d917ca50/pwa-flipkart-shell.png'>Large preview</a>)" alt="App Shell of Flipkart’s PWA" >}}

<p>Users like the loading experience of app shells because they despise blank screens. A blank screen makes the user feel that the website is not loading. It makes them feel as if the website were stuck.</p>

<p>App shells attempt to paint the navigational structure of the app as soon as possible, such as the navbar, the tab bar as well as a loader signifying that the content you’ve requested is being loaded.</p>

{{% ad-panel-leaderboard %}}

### So How Do You Build An App Shell?

<p>The app shell pattern prioritizes the loading of the HTML, CSS and JavaScript that will render first. This means that we need to give those resources full priority, hence you have to inline those assets. So to build an app shell, you simply have to inline the HTML, CSS and JavaScript that are responsible for the app shell. Of course, you should not inline everything but rather stay within a limit of around 30 to 40KB total.</p>

<p>You can see the inlined app shell in the <em>index.html</em>. You can inspect the source code by checking out the <em>index.html</em> file, and you can preview it in the browser by deleting the <code>&lt;main&gt;</code> element in dev tools:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00d178c3-61a2-4332-998c-d97cdf9af843/our-app-shell.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/437fec6e-6172-4ba6-ab30-0a2f672491fb/pwa-webpack-workbox-our-app-shell.png" sizes="70vw" caption="The App Shell that we’re building in this article. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00d178c3-61a2-4332-998c-d97cdf9af843/our-app-shell.png'>Large preview</a>)" alt="Currencies PWA App Shell with navbar & loader" >}}

## Does It Work Offline?

<p>Let’s simulate going offline! Open DevTools, navigate to the network tab and tick the ‘Offline’ checkbox. When you reload the page, you will see that we will get the browser’s offline page.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e1b20d3-9e96-4416-98ab-ffad20591f20/offline1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae7304e9-dbfb-4511-9e0c-7ea6c260018a/pwa-webpack-workbox-offline1.png" sizes="70vw" caption="The request to the homepage failed so we obviously see this as a result. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e1b20d3-9e96-4416-98ab-ffad20591f20/offline1.png'>Large preview</a>)" alt="Browser’s offline error page" >}}

<p>That’s because the initial request to <code>/</code> (which will load the <em>index.html</em> file) will fail because the Internet is offline. The only way for us to recover from that request failure is by having a service worker.</p>

<p>Let’s visualize the request without a service worker:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/405f41cd-6a27-466d-a115-d901d951b301/without-sw.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39c90913-e88a-40c5-88ee-99d54e1e6699/without-sw-800w.gif" width="800" height="" alt="Animation of a network request going from the client’s browser to the internet." /></a><figcaption>Network request goes from the browser to the Internet and back. (Icons from <a href="https://www.flaticon.com/">flaticon.com</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/405f41cd-6a27-466d-a115-d901d951b301/without-sw.gif">Large preview</a>)</figcaption></figure>

<p>A service worker is a programmable network proxy, which means it sits in between your web page and the Internet. This lets you control incoming and outgoing network requests.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6ad80a2-5990-473c-8fbe-8dc6670f5ff0/with-sw.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e9118be-bc34-4474-9295-50e11a6e74e0/with-sw-800w.gif" width="800" height="" alt="Animation of a network request intercepted by the service worker." /></a><figcaption>Network request gets intercepted by the service worker. (Icons from <a href="https://www.flaticon.com/">flaticon.com</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6ad80a2-5990-473c-8fbe-8dc6670f5ff0/with-sw.gif">Large preview</a>)</figcaption></figure>

<p>This is beneficial because we can now re-route this failed request to the cache (assuming we have the content in the cache).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94f5c376-d229-4dc7-b659-21eee27285ed/with-sw-cache.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f31d335-a032-47a2-9be6-7c5cc259e936/with-sw-cache-800w.gif" width="800" height="" alt="Animation of a network request interecepted by the service worker and redirected to the cache." /></a><figcaption>Network request gets redirected to the cache when it already exists in the cache. (Icons from <a href="https://www.flaticon.com/">flaticon.com</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94f5c376-d229-4dc7-b659-21eee27285ed/with-sw-cache.gif">Large preview</a>)</figcaption></figure>

<p>A service worker is also a type of Web Worker, meaning that it runs separately from your main page and doesn’t have access to either the <code>window</code> or <code>document</code> object.</p>

{{% ad-panel-leaderboard %}}

## Precache The App Shell

<p>In order to make our app work offline, we’re going to start by precaching the app shell.</p>

<p>So let’s start by installing the Webpack Workbox plugin:</p>

<pre><code class="language-bash">npm install --save-dev workbox-webpack-plugin
</code></pre>

<p>Then we’re going to open our <em>index.js</em> file and register the service worker:</p>

<pre><code class="language-javascript">if ("serviceWorker" in navigator){
window.addEventListener("load", () => {
navigator.serviceWorker.register("/sw.js");
})
}
</code></pre>

<p>Next, open the <em>webpack.config.js</em> file and let’s configure the Workbox webpack plugin:</p>

<pre><code class="language-javascript">//add at the top
const WorkboxWebpackPlugin = require("workbox-webpack-plugin");

//add inside the plugins array:
plugins: [
…
, new WorkboxWebpackPlugin.InjectManifest({
  swSrc: "./src/src-sw.js",
  swDest: "sw.js"
})
]
</code></pre>

<p>This will instruct Workbox to use our <em>./src/src-sw.js</em> file as a base. The generated file will be called <em>sw.js</em> and will be in the <code>dist</code> folder.</p>

<p>Then create a <em>./src/src-sw.js</em> file at the root level and write the following inside of it:</p>

<pre><code class="language-javascript">workbox.precaching.precacheAndRoute(self.__precacheManifest);
</code></pre>

<p><strong>Note</strong>: <em>The</em> <code>self.__precacheManifest</code> <em>variable will be imported from a file that will be dynamically generated by workbox.</em></p>

<p>Now you’re ready to build your code with <code>npm run build</code> and Workbox will generate two files inside the <code>dist</code> folder:</p>

<ul>
  <li><em>precache-manifest.66cf63077c7e4a70ba741ee9e6a8da29.js</em></li>
  <li><em>sw.js</em></li>
</ul>

<p>The <em>sw.js</em> imports workbox from CDN as well as the <em>precache-manifest.[chunkhash].js</em>.</p>

<pre><code class="language-javascript">//precache-manifest.[chunkhash].js file
self.__precacheManifest = (self.__precacheManifest || []).concat([
  
    "revision": "ba8f7488757693a5a5b1e712ac29cc28",
    "url": "index.html"
  },
  
    "url": "main.49467c51ac5e0cb2b58e.js"
  
]);
</code></pre>

<p>The precache manifest lists the names of the files that were processed by webpack and that end up in your <code>dist</code> folder. We will use these files to precache them in the browser. This means that when your website loads the first time and registers the service worker, it will cache these assets so that they can be used the next time.</p>

<p>You can also notice that some entries have a ‘revision’ whereas others don’t. That’s because the revision can sometimes be inferred from the chunkhash from the file name. For example, let’s take a closer look at the file name <em>main.49467c51ac5e0cb2b58e.js</em>. It has a revision is in the filename, which is the chunkhash <em>49467c51ac5e0cb2b58e</em>.</p>

<p>This allows Workbox to understand when your files change so that it only cleans up or updates the files that were changed, rather than dumping all the cache every time you publish a new version of your service worker.</p>

<p>The first time you load the page, the service worker will install. You can see that in DevTools. First, the <em>sw.js</em> file is requested which then requests all the other files. They are clearly marked with the gear icon.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/498a146e-27f0-421d-bb6b-909807d15e85/sw-network-tab.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/498a146e-27f0-421d-bb6b-909807d15e85/sw-network-tab.png" sizes="100vw" caption="Requests marked with the ⚙️ icon are requests initiated by the service worker. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/498a146e-27f0-421d-bb6b-909807d15e85/sw-network-tab.png'>Large preview</a>)" alt="Screenshot of DevTools Network tab when the service worker gets installed." >}}

<p>So Workbox will initialize and it will precache all the files that are in the precache-manifest. It is important to double check that you don’t have any unnecessary files in the <em>precache-manifest</em> file such as <em>.map</em> files or files that are not part of the app shell.</p>

<p>In the network tab, we can see the requests coming from the service worker. And now if you try to go offline, the app shell is already precached so it works even if we’re offline!</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b0b90c0-0c0b-4949-951d-ce4f9d8e7a0b/offline-network-fail.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b0b90c0-0c0b-4949-951d-ce4f9d8e7a0b/offline-network-fail.png" sizes="100vw" caption="API calls fail when we go offline. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b0b90c0-0c0b-4949-951d-ce4f9d8e7a0b/offline-network-fail.png'>Large preview</a>)" alt="Screenshot of Dev Tools Network tab showing API calls failing." >}}

## Cache Dynamic Routes

<p>Did you notice that when we went offline, the app shell works but not our data? That’s because these API calls are not part of the <strong>precached app shell</strong>. When there’s no Internet connection, these requests will fail and the user won’t be able to see the currency information.</p>

<p>However, these requests cannot be precached because their value comes from an API. Moreover, when you start having multiple pages, you don’t want to cache all API request in one go. Instead, you want to cache them when the user visits that page.</p>

<p>We call these ‘dynamic data’. They often include API calls as well as images and other assets that are requested when a user does a certain action on your website (e.g. when they browse to a new page).</p>

<p>You can cache these using Workbox’s routing module. Here’s how:</p>

<pre><code class="language-javascript">//add in src/src-sw.js
workbox.routing.registerRoute(
  /https:\/\/api\.exchangeratesapi\.io\/latest/,
  new workbox.strategies.NetworkFirst({
    cacheName: "currencies",
    plugins: [
      new workbox.expiration.Plugin({
        maxAgeSeconds: 10 * 60 // 10 minutes
      })
    ]
  })
);
</code></pre>

<p>This will set up dynamic caching for any request URL that matches the URL <code><a href="https://api.exchangeratesapi.io/latest">https://api.exchangeratesapi.io/latest</a></code>.</p>

<p>The caching strategy that we used here is called <code>NetworkFirst</code>; there are two other ones that are often used:</p>

<ol>
  <li><code>CacheFirst</code></li>
  <li><code>StaleWhileRevalidate</code></li>
</ol>

<p><code>CacheFirst</code> will look for it in the cache first. If it’s not found, then it will get it from the network. <code>StaleWhileRevalidate</code> will go to the network and the cache at the same time. Return the cache’s response to the page (while in the background) it will use the new network response to update the cache for the next time it’s used.</p>

<p>For our use case, we had to go with <code>NetworkFirst</code> because we’re dealing with currency rates that change very often. However, when the user goes offline, we can at least show them the rates as they were 10 minutes ago &mdash; that’s why we used the expiration plugin with the <code>maxAgeSeconds</code> set to <code>10 * 60</code> seconds.</p>

## Manage App Updates

<p>Everytime a user loads your page, the browser will run the <code>navigator.serviceWorker.register</code> code even though the service worker is already installed and running. This allows the browser to detect if there’s a new version of the service worker. When the browser notices that the file has not changed, it just skips the registration call. Once that file changes, the browser understands that there’s a new version of the service worker, thus <strong>it installs the new service worker parallel to the currently running service worker</strong>.</p>

<p>However, it pauses at the <code>installed/waiting</code> phase because only one service worker can be activated at the same time.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4840a43-76ed-4848-a988-b714032d8554/sw-life-cycle.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4840a43-76ed-4848-a988-b714032d8554/sw-life-cycle.png" sizes="100vw" caption="A simplified life cycle of a service worker (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4840a43-76ed-4848-a988-b714032d8554/sw-life-cycle.png'>Large preview</a>)" alt="The life cycle of a service worker: Parsed, Installed/Waiting, Activated & Redundant" >}}

<p>Only when all the browser windows controlled by the previous service worker are closed, then it becomes safe for the new service worker to activate.</p>

<p>You can also manually control that by calling <code>skipWaiting()</code> (or <code>self.skipWaiting()</code> since <code>self</code> is the global execution context in the service worker). However, most of the time you should only do that after asking the user if they want to get the latest update.</p>
 
<p>Thankfully, <code>workbox-window</code> helps us achieve this. It’s a new window library introduced in Workbox v4 that aims at simplifying common tasks on the window’s side.</p>

<p>Let’s start by installing it with the following:</p>

<pre><code class="language-bash">npm install workbox-window
</code></pre>

<p>Next, import <code>Workbox</code> at the top of the file <em>index.js</em>:</p>

<pre><code class="language-javascript">import { Workbox } from "workbox-window";
</code></pre>

<p>Then we’ll replace our registration code with the below:</p>

<pre><code class="language-javascript">if ("serviceWorker" in navigator) {
  window.addEventListener("load", () => {
      const wb = new Workbox("/sw.js");
    
wb.register();
  });

}
</code></pre>

<p>We’ll then find the update button which has the ID <cpde>app-update</cpde> and listen for the <code>workbox-waiting</code> event:</p>

<div class="break-out">

<pre><code class="language-javascript">//add before the wb.register()
const updateButton = document.querySelector("#app-update");
// Fires when the registered service worker has installed but is waiting to activate.
wb.addEventListener("waiting", event => {
    updateButton.classList.add("show");
    updateButton.addEventListener("click", () => {
    // Set up a listener that will reload the page as soon as the previously waiting service worker has taken control.
    wb.addEventListener("controlling", event => {
        window.location.reload();
    });

    // Send a message telling the service worker to skip waiting.
    // This will trigger the `controlling` event handler above.
    wb.messageSW({ type: "SKIP_WAITING" });
    });
});
</code></pre>
</div>

<p>This code will show the update button when there’s a new update (so when the service worker is in a waiting state) and will send a <code>SKIP_WAITING</code> message to the service worker.</p>

<p>We’ll need update the service worker file and handle the <code>SKIP_WAITING</code> event such that it calls the <code>skipWaiting</code>:</p>

<pre><code class="language-javascript">//add in src-sw.js
addEventListener("message", event => {
  if (event.data && event.data.type === "SKIP_WAITING") {
    skipWaiting();
  
});
</code></pre>

<p>Now run <code>npm run dev</code> then reload the page. Go into your code and update the navbar title to “Navbar v2”. Reload the page again, and you should be able to see the update icon.</p>

## Wrapping Up

<p>Our website now works offline and is able to tell the user about new updates. Please keep in mind though, that the most important factor when building a PWA is the user experience. Always focus on building experiences that are easy to use by your users. We, as developers, tend to get too excited about technology and often end up forgetting about our users.</p>

<p>If you’d like to take this a step further, you can add a web app manifest which will allow your users to add the site to their home screen. And if you’d like to know more about Workbox, you can find the official documentation on the <a href="https://workboxjs.org">Workbox</a> website.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'Can You Make More Money With A Mobile App Or A PWA?'" href="https://www.smashingmagazine.com/2019/03/can-you-make-more-money-with-mobile-app-or-a-pwa/" rel="bookmark">Can You Make More Money With A Mobile App Or A PWA?</a></li>
<li><a title="Read 'An Extensive Guide To Progressive Web Applications'" href="https://www.smashingmagazine.com/2018/11/guide-pwa-progressive-web-applications/" rel="bookmark">An Extensive Guide To Progressive Web Applications</a></li>
<li><a title="Read 'Native And PWA: Choices, Not Challengers!'" href="https://www.smashingmagazine.com/2018/02/native-and-pwa-choices-not-challengers/" rel="bookmark">Native And PWA: Choices, Not Challengers!</a></li>
<li><a title="Read 'Building A PWA Using Angular 6'" href="https://www.smashingmagazine.com/2018/09/pwa-angular-6/" rel="bookmark">Building A PWA Using Angular 6</a></li>
</ul>

{{< signature "dm, yk, il" >}}

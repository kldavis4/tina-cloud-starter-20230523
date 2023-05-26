---
title: 'Making A Service Worker: A Case Study'
slug: making-a-service-worker
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36e238b2-ebc3-46c3-813e-999eec42af04/05-preview-offline-preview-opt.png
date: 2016-02-02T00:17:39.000Z
author: lyzadangergardner
summary: >-
  This article explains what a service worker is and how to put together your own by registering, installing, and activating it without any hassle.
description: >-
  This article explains what a service worker is and how to put together your own by registering, installing, and activating it without any hassle.
categories:
  - Coding
  - JavaScript
  - Techniques
  - Service Workers
---
There’s no shortage of boosterism or excitement about the fledgling <a href="https://www.w3.org/TR/service-workers/">service worker API</a>, now shipping in <a href="https://jakearchibald.github.io/isserviceworkerready/">some popular browsers</a>. There are cookbooks and blog posts, code snippets and tools. But I find that when I want to learn a new web concept thoroughly, rolling up my proverbial sleeves, diving in and building something from scratch is often ideal.

The bumps and bruises, gotchas and bugs I ran into this time have benefits: Now I understand service workers a lot better, and with any luck I can help you avoid some of the headaches I encountered when working with the new API.</p>

<strong>Service workers do a lot of different things</strong>; there are myriad ways to harness their powers. I decided to build a simple service worker for my (static, uncomplicated) website that roughly mirrors the features that the obsolete Application Cache API used to provide — that is:

*   make the website function offline,
*   increase online performance by reducing network requests for certain assets,
*   provide a customized offline fallback experience.

Before beginning, I’d like to acknowledge two people whose work made this possible. First, I’m hugely indebted to Jeremy Keith for the implementation of service workers on his own website, which served as the starting point for my own code. I was inspired by <a href="https://adactio.com/journal/9888">his recent post</a> describing his ongoing service worker experiences. In fact, my work is so heavily derivative that I wouldn’t have written about it except for Jeremy’s exhortation in <a href="https://adactio.com/journal/9775">an earlier post</a>:
<blockquote>So if you decide to play around with Service Workers, please, please share your experience.</blockquote>

Secondly, all sorts of big old thanks to <a href="https://jakearchibald.com/">Jake Archibald</a> for his excellent technical review and feedback. Always nice when one of the <a href="https://github.com/slightlyoff/ServiceWorker">service worker specification</a>’s creators and evangelists is able to set you straight!

{{% feature-panel %}}

## What Is A Service Worker?

A service worker is a <strong>script that stands between your website and the network</strong>, giving you, among other things, the ability to intercept network requests and respond to them in different ways.

In order for your website or app to work, the browser fetches its assets — such as HTML pages, JavaScript, images, fonts. In the past, the management of this was chiefly the browser’s prerogative. If the browser couldn’t access the network, you would probably see its “Hey, you’re offline” message. There were techniques you could use to encourage the local caching of assets, but the browser often had the last say.

This wasn’t such a great experience for users who were offline, and it left web developers with little control over browser caching.

Cue Application Cache (or AppCache), whose arrival several years ago seemed promising. It ostensibly let you dictate how different assets should be handled, so that your website or app could work offline. Yet AppCache’s simple-looking syntax belied its <a href="https://alistapart.com/article/application-cache-is-a-douchebag">underlying confounding nature and lack of flexibility</a>.

The fledgling service worker API can do what AppCache did, and a whole lot more. But it looks a little daunting at first. The specifications make for heavy and abstract reading, and numerous APIs are subservient to it or otherwise related: <code>cache</code>, <code>fetch</code>, etc. Service workers encompass so much functionality: push notifications and, soon, background syncing. Compared to AppCache, it looks… complicated.

Whereas AppCache (which, by the way, is <a href="https://html.spec.whatwg.org/multipage/browsers.html#offline">going away</a>) was easy to learn but terrible for every single moment after that (my opinion), service workers are more of an initial cognitive investment, but they are powerful and useful, and you can generally get yourself out of trouble if you break things.</p>

## Some Basic Service Worker Concepts

A service worker is a file with some JavaScript in it. In that file you can write JavaScript as you know and love it, with a few important things to keep in mind.</p>

<strong>Service worker scripts run in a separate thread in the browser</strong> from the pages they control. There are ways to communicate between workers and pages, but they execute in a separate <a href="https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope">scope</a>. That means you won’t have access to the DOM of those pages, for example. I visualize a service worker as sort of running in a separate tab from the page it affects; this is not at all accurate, but it is a helpful rough metaphor for keeping myself out of confusion.

JavaScript in a service worker must not block. You need to use asynchronous APIs. For example, you cannot use <code>localStorage</code> in a service worker (<code>localStorage</code> is a synchronous API). Humorously enough, even knowing this, I managed to run the risk of violating it, as we’ll see.</p>



### Registering a Service Worker

You make a service worker take effect by registering it. This registration is done from outside the service worker, by another page or script on your website. On my website, a global <code>site.js</code> script is included on every HTML page. I register my service worker from there.

When you register a service worker, you (optionally) also tell it what <strong>scope</strong> it should apply itself to. You can instruct a service worker only to handle stuff for part of your website (for example, <code>'/blog/'</code>) or you can register it for your whole website (<code>'/'</code>) like I do.</p>

### Service Worker Lifecycle And Events

A service worker does the bulk of its work by <strong>listening for relevant events and responding to them in useful ways</strong>. Different events are triggered at different points in a service worker’s lifecycle.

Once the service worker has been registered and downloaded, it gets <strong>installed</strong> in the background. Your service worker can listen for the <code>install</code> event and perform tasks appropriate for this stage.

In our case, we want to take advantage of the <code>install</code> state to pre-cache a bunch of assets that we know we will want available offline later.

After the <code>install</code> stage is finished, the service worker is then <strong>activated</strong>. That means the service worker is now in control of things within its <code>scope</code> and can do its thing. The <code>activate</code> event isn’t too exciting for a new service worker, but we’ll see how it’s useful when updating a service worker with a new version.

Exactly when activation occurs depends on whether this is a brand new service worker or an updated version of a pre-existing service worker. If the browser does not have a previous version of a given service worker already registered, activation will happen immediately after installation is complete.

Once installation and activation are complete, they won’t occur again until an updated version of the service worker is downloaded and registered.

Beyond installation and activation, we’ll be looking primarily at the <code>fetch</code> event today to make our service worker useful. But there are several useful events beyond that: <strong>sync</strong> events and <strong>notification</strong> events, for example.

For extra credit or leisure fun, you can read more about the <a href="https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API#Interfaces">interfaces that service workers implement</a>. It’s by implementing these interfaces that service workers get the bulk of their events and much of their extended functionality.</p>

### The Service Worker’s Promise-Based API

The service worker API makes heavy use of <code>Promises</code>. A promise represents the eventual result of an asynchronous operation, even if the actual value won’t be known until the operation completes some time in the future.</p>

<pre><code class="language-javascript">getAnAnswerToADifficultQuestionSomewhereFarAway()
   .then(answer =&gt; {
   console.log('I got the ${answer}!');
  })
   .catch(reason =&gt; {
   console.log('I tried to figure it out but couldn't because ${reason}');
});
</code></pre>

The <code>getAnAnswer…</code> function returns a <code>Promise</code> that (we hope) will eventually be fulfilled by, or resolve to, the <code>answer</code> we’re looking for. Then, that <code>answer</code> can be fed to any chained <code>then</code> handler functions, or, in the sorry case of failure to achieve its objective, the <code>Promise</code> can be rejected — often with a reason — and <code>catch</code> handler functions can take care of these situations.

There’s more to promises, but I’ll try to keep the examples here straightforward (or at least commented). I urge you to do some <a href="https://developer.mozilla.org/en-US/docs/Mozilla/JavaScript_code_modules/Promise.jsm/Promise">informative reading</a> if you’re new to promises.</p>

<strong>Note</strong>: I use certain ECMAScript6 (or ES2015) features in the sample code for service workers because browsers that support service workers also support these features. Specifically here, I am using <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions">arrow functions</a> and <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings">template strings</a>.</p>

### Other Service Worker Necessities

Also, note that service workers <strong>require HTTPS</strong> to work. There is an important and useful exception to this rule: Service workers work for <code>localhost</code> on insecure <code>http</code>, which is a relief because setting up local SSL is sometimes a slog.

Fun fact: This project forced me to do something I’d been putting off for a while: getting and configuring SSL for the <code>www</code> subdomain of my website. This is something I urge folks to consider doing because pretty much all of the fun new stuff hitting the browser in the future will require SSL to be used.

All of the stuff we’ll put together works today in Chrome (I use version 47). Any day now, Firefox 44 will ship, and it supports service workers. <a href="https://jakearchibald.github.io/isserviceworkerready/">Is Service Worker Ready?</a> provides granular information about support in different browsers.</p>


{{% ad-panel-leaderboard %}}

## Registering, Installing And Activating A Service Worker

Now that we’ve taken care of some theory, we can start putting together our service worker.

To install and activate our service worker, we want to listen for <code>install</code> and <code>activate</code> events and act on them.

We can start with an empty file for our service worker and add a couple of <code>eventListeners</code>. In <code>serviceWorker.js</code>:

<pre><code class="language-javascript">self.addEventListener('install', event =&gt; {
  // Do install stuff
});

self.addEventListener('activate', event =&gt; {
  // Do activate stuff: This will come later on.
});</code></pre>

### Registering Our Service Worker

Now we need to tell the pages on our website to use the service worker.

Remember, this registration happens from outside the service worker — in my case, from within a script (<code>/js/site.js</code>) that is included on every page of my website.

In my <code>site.js</code>:

<pre><code class="language-javascript">if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/serviceWorker.js', {
    <span class="hljs-attribute">scope: '/'</span>
  });
}</code></pre>

### Pre-Caching Static Assets During Install

I want to use the install stage to pre-cache some assets on my website.

*   By pre-caching some static assets (images, CSS, JavaScript) that are used by many pages on my website, I can speed up loading times by grabbing these out of cache, instead of fetching from the network on subsequent page loads.
*   By pre-caching an offline fallback page, I can show a nice page when I can’t fulfill a page request because the user is offline.

The steps to do this are:

1.  Tell the `install` event to hang on and not to complete until I’ve done what I need to do by using `event.waitUntil`.
2.  Open the appropriate `cache`, and stick the static assets in it by using `Cache.addAll`. In [progressive web app](https://developers.google.com/web/progressive-web-apps?hl=en) parlance, these assets make up my “application shell.”

In <code>/serviceWorker.js</code>, let’s expand the <code>install</code> handler:

<pre><code class="language-javascript">self.addEventListener('install', event =&gt; {

  function onInstall () {
    return caches.open('static')
      .then(cache =&gt; cache.addAll([
        '/images/lyza.gif',
        '/js/site.js',
        '/css/styles.css',
        '/offline/',
        '/'
      ])
    );
  }

  event.waitUntil(onInstall(event));
});</code></pre>

The service worker implements the <a href="https://developer.mozilla.org/en-US/docs/Web/API/CacheStorage"><code>CacheStorage</code> interface</a>, which makes the <code>caches</code> property available globally in our service worker. There are several useful methods on <code>caches</code> — for example, <code>open</code> and <code>delete</code>.

You can see <code>Promises</code> at work here: <code>caches.open</code> returns a <code>Promise</code> resolving to a <a href="https://developer.mozilla.org/en-US/docs/Web/API/Cache"><code>cache</code></a> object once it has successfully opened the <code>static</code> cache; <code>addAll</code> also returns a <code>Promise</code> that resolves when all of the items passed to it have been stashed in the cache.

I tell the <code>event</code> to wait until the <code>Promise</code> returned by my handler function is resolved successfully. Then we can be sure that all of those pre-cache items get sorted before the installation is complete.</p>

## Console Confusions

### Stale Logging

Possibly not a bug, but <a href="https://code.google.com/p/chromium/issues/detail?id=543104&amp;q=service%20worker%20event&amp;colspec=ID%20Pri%20M%20Stars%20ReleaseBlock%20Cr%20Status%20Owner%20Summary%20OS%20Modified#makechanges">certainly a confusion</a>: If you <code>console.log</code> from service workers, Chrome will continue to re-display (rather than clear) those log messages on subsequent page requests. This can make it <em>seem</em> like events are firing too many times or like code is executing over and over.

For example, let’s add a <code>log</code> statement to our <code>install</code> handler:

<pre><code class="language-javascript">self.addEventListener('install', event =&gt; {
  // … as before
  console.log('installing');
});
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0207e4df-9ba1-477e-9846-914cb8fd5750/01-stale-logging-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/600a20f5-7d94-476b-a423-ff6757b337f9/01-stale-logging-preview-opt.png" alt="Service Worker - Stale Logs Freak Me Out" width="500" height="65" /></a><figcaption>As of Chrome 47, the “installing” log message will continue to appear on subsequent page requests. Chrome isn’t really firing the <code>install</code> event on every page load. Instead, it’s showing stale logs. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0207e4df-9ba1-477e-9846-914cb8fd5750/01-stale-logging-opt.png">View large version</a>)</figcaption></figure>

### An Error When Things Are OK

Another odd thing is that once a service worker is installed and activated, subsequent page loads for any page within its scope will always <a href="https://code.google.com/p/chromium/issues/detail?id=541797">cause a single error in the console</a>. I thought I was doing something wrong.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d01585f-4156-4057-b93e-31f4388bf90d/02-console-error-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71cbc139-c16c-41df-8f8f-98a55fbb6879/02-console-error-preview-opt.png" alt="Omnimpresent Chrome Service Worker Error" /></a><figcaption>As of Chrome 47, accessing a page with an already-registered service worker will always cause this error in the console. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d01585f-4156-4057-b93e-31f4388bf90d/02-console-error-opt.png">View large version</a>)</figcaption></figure>

## What We’ve Accomplished So Far

The service worker handles the <code>install</code> event and pre-caches some static assets. If you were to use this service worker and register it, it would indeed pre-cache the indicated assets but wouldn’t yet be able to take advantage of them offline.

The contents of <code>serviceWorker.js</code> <a href="https://github.com/lyzadanger/serviceworker-example/blob/master/01-install-precache/serviceWorker.js">are on GitHub</a>.</p>

{{% ad-panel-leaderboard %}}

## Fetch Handling With Service Workers

So far, our service worker has a fleshed-out <code>install</code> handler but doesn’t <em>do</em> anything beyond that. The magic of our service worker is really going to happen when <code>fetch</code> events are triggered.

We can respond to fetches in different ways. By using different <strong>network strategies</strong>, we can tell the browser to always try to fetch certain assets from the network (making sure key content is fresh), while favoring cached copies for static assets — really slimming down our page payloads. We can also provide a nice offline fallback if all else fails.

Whenever a browser wants to fetch an asset that is within the scope of this service worker, we can hear about it by, yep, adding an <code>eventListener</code> in <code>serviceWorker.js</code>:

<pre><code class="language-javascript">self.addEventListener('fetch', event =&gt; {
  // … Perhaps respond to this fetch in a useful way?
});
</code></pre>

Again, every fetch that falls within this service worker’s scope (i.e. path) will trigger this event — HTML pages, scripts, images, CSS, you name it. We can selectively handle the way the browser responds to any of these fetches.</p>

### Should We Handle This Fetch?

When a <code>fetch</code> event occurs for an asset, the first thing I want to determine is whether this service worker should interfere with the fetching of the given resource. Otherwise, it should do nothing and let the browser assert its default behavior.

We’ll end up with basic logic like this in <code>serviceWorker.js</code>:

<pre><code class="language-javascript">self.addEventListener('fetch', event =&gt; {

  function shouldHandleFetch (event, opts) {
    // Should we handle this fetch?
  }

  function onFetch (event, opts) {
    // … TBD: Respond to the fetch
  }

  if (shouldHandleFetch(event, config)) {
    onFetch(event, config);
  }
});</code></pre>

The <code>shouldHandleFetch</code> function assesses a given request to determine whether we should provide a response or let the browser assert its default handling.</p>

### Why Not Use Promises?

To keep with service worker’s predilection for promises, the first version of my <code>fetch</code> event handler looked like this:

<pre><code class="language-javascript">self.addEventListener('fetch', event =&gt; {

  function shouldHandleFetch (event, opts) { }
  function onFetch (event, opts) { }

  shouldHandleFetch(event, config)
    .then(onFetch(event, config))
    .catch(…);
});</code></pre>

Seems logical, but I was making a couple of rookie mistakes with promises. I swear I did sense a code smell even initially, but it was Jake who set me straight on the errors of my ways. (Lesson: As always, if code feels wrong, it probably is.)

Promise rejections should not be used to indicate, “I got an answer I didn’t like.” Instead, rejections should indicate, “Ah, crap, something went wrong in trying to get the answer.” That is, <a href="https://www.w3.org/2001/tag/doc/promises-guide#rejections-should-be-exceptional">rejections should be exceptional</a>.</p>

### Criteria for Valid Requests

Right, back to determining whether a given fetch request is applicable for my service worker. My site-specific criteria are as follows:

1.  The requested URL should represent something I want to cache or respond to. Its path should match a `Regular Expression` of valid paths.
2.  The request’s HTTP method should be `GET`.
3.  The request should be for a resource from my origin (`lyza.com`).

If any of the <code>criteria</code> tests evaluate to <code>false</code>, we should not handle this request. In <code>serviceWorker.js</code>:

<pre><code class="language-javascript">function shouldHandleFetch (event, opts) {
  var request            = event.request;
  var url                = new URL(request.url);
  var criteria           = {
    matchesPathPattern: !!(opts.cachePathPattern.exec(url.pathname),
    isGETRequest      : request.method === 'GET',
    isFromMyOrigin    : url.origin === self.location.origin
  };

  // Create a new array with just the keys from criteria that have
  // failing (i.e. false) values.
  var failingCriteria    = Object.keys(criteria)
    .filter(criteriaKey =&gt; !criteria[criteriaKey]);

  // If that failing array has any length, one or more tests failed.
  return !failingCriteria.length;
}</code></pre>

Of course, the criteria here are my own and would vary from site to site. <code>event.request</code> is a <a href="https://developer.mozilla.org/en-US/docs/Web/API/Request"><code>Request</code></a> object that has all kinds of data you can look at to assess how you’d like your fetch handler to behave.

Trivial note: If you noticed the incursion of <code>config</code>, passed as <code>opts</code> to handler functions, well spotted. I factored out some reusable <code>config</code>-like values and created a <code>config</code> object in the top-level scope of the service worker:

<pre><code class="language-javascript">var config = {
  staticCacheItems: [
    '/images/lyza.gif',
    '/css/styles.css',
    '/js/site.js',
    '/offline/',
    '/'
    ],
  cachePathPattern: /^\/(?:(20[0-9]{2}|about|blog|css|images|js)\/(.+)?)?$/
};
</code></pre>

### Why Whitelist?

You may be wondering why I’m only caching things with paths that match this regular expression:

<code>/^\/(?:(20[0-9]{2}|about|blog|css|images|js)\/(.+)?)?$/</code>

… instead of caching anything coming from my own origin. A couple of reasons:

*   I don’t want to cache the service worker itself.
*   When I’m developing my website locally, some requests generated are for things I don’t want to cache. For example, I use `browserSync`, which kicks off a bunch of related requests in my development environment. I don’t want to cache that stuff! It seemed messy and challenging to try to think of everything I wouldn’t want to cache (not to mention, a little weird to have to spell it out in my service worker’s configuration). So, a whitelist approach seemed more natural.</p>

## Writing The Fetch Handler

Now we’re ready to pass applicable <code>fetch</code> requests on to a handler. The <code>onFetch</code> function needs to determine:

1.  what kind of resource is being requested,
2.  and how I should fulfill this request.</p>

### 1. What Kind of Resource Is Being Requested?

I can look at the <code>HTTP Accept</code> header to get a hint about what kind of asset is being requested. This helps me figure out how I want to handle it.</p>

<pre><code class="language-javascript">function onFetch (event, opts) {
  var request      = event.request;
  var acceptHeader = request.headers.get('Accept');
  var resourceType = 'static';
  var cacheKey;

  if (acceptHeader.indexOf('text/html') !== -1) {
    resourceType = 'content';
  } else if (acceptHeader.indexOf('image') !== -1) {
    resourceType = 'image';
  }

  // {String} [static|image|content]
  cacheKey = resourceType;
  // … now do something
}</code></pre>

To stay organized, I want to stick different kinds of resources into different caches. This will allow me to manage those caches later. These cache key <code>String</code>s are arbitrary — you can call your caches whatever you’d like; the cache API doesn’t have opinions.</p>

### 2. Respond to the Fetch

The next thing for <code>onFetch</code> to do is to <code>respondTo</code> the <code>fetch</code> event with an intelligent <code>Response</code>.</p>

<pre><code class="language-javascript">function onFetch (event, opts) {
  // 1. Determine what kind of asset this is… (above).
  if (resourceType === 'content') {
    // Use a network-first strategy.
    event.respondWith(
      fetch(request)
        .then(response =&gt; addToCache(cacheKey, request, response))
        .catch(() =&gt; fetchFromCache(event))
        .catch(() =&gt; offlineResponse(opts))
    );
  } else {
    // Use a cache-first strategy.
    event.respondWith(
      fetchFromCache(event)
        .catch(() =&gt; fetch(request))
        .then(response =&gt; addToCache(cacheKey, request, response))
        .catch(() =&gt; offlineResponse(resourceType, opts))
      );
  }
}</code></pre>

### Careful With Async!

In our case, <code>shouldHandleFetch</code> doesn’t do anything asynchronous, and neither does <code>onFetch</code> up to the point of <code>event.respondWith</code>. If something asynchronous <em>had</em> happened before that, we would be in trouble. <code>event.respondWith</code> must be called between the <code>fetch</code> event firing and control returning to the browser. Same goes for <code>event.waitUntil</code>. Basically, if you’re handling an event, either do something immediately (synchronously) or tell the browser to hang on until your asynchronous stuff is done.</p>

## HTML Content: Implementing A Network-First Strategy

Responding to <code>fetch</code> requests involves implementing an appropriate network strategy. Let’s look more closely at the way we’re responding to requests for HTML content (<code>resourceType === 'content'</code>).</p>

<pre><code class="language-javascript">if (resourceType === 'content') {
  // Respond with a network-first strategy.
  event.respondWith(
    fetch(request)
      .then(response =&gt; addToCache(cacheKey, request, response))
      .catch(() =&gt; fetchFromCache(event))
      .catch(() =&gt; offlineResponse(opts))
  );
}</code></pre>

The way we fulfill requests for content here is a network-first strategy. Because HTML content is the core concern of my website and it changes often, I always try to get fresh HTML documents from the network.

Let’s step through this.</p>

### 1. Try Fetching From the Network

<pre><code class="language-javascript">fetch(request)
  .then(response =&gt; addToCache(cacheKey, request, response))
</code></pre>

If the network request is successful (i.e. the promise resolves), go ahead and stash a copy of the HTML document in the appropriate cache (<code>content</code>). This is called <strong>read-through caching</strong>:

<pre><code class="language-javascript">function addToCache (cacheKey, request, response) {
  if (response.ok) {
    var copy = response.clone();
    caches.open(cacheKey).then( cache =&gt; {
      cache.put(request, copy);
    });
    return response;
  }
}</code></pre>

Responses may be <strong>used only once</strong>.

We need to do two things with the <code>response</code> we have:

*   cache it,
*   respond to the event with it (i.e. return it).

But <code>Response</code> objects may be used only once. By cloning it, we are able to create a copy for the cache’s use:

<code class="language-javascript">var copy = response.clone();</code>

<strong>Don’t cache bad responses.</strong> Don’t make the same mistake I did. The first version of my code didn’t have this conditional:

<pre><code class="language-javascript">if (response.ok)</code></pre>

Pretty awesome to end up with 404 or other bad responses in the cache! Only cache happy responses.</p>

### 2. Try to Retrieve From Cache

If retrieving the asset from the network succeeds, we’re done. However, if it doesn’t, we might be offline or otherwise network-compromised. Try retrieving a previously cached copy of the HTML from cache:

<pre><code class="language-javascript">fetch(request)
  .then(response =&gt; addToCache(cacheKey, request, response))
  .catch(() =&gt; fetchFromCache(event))
</code></pre>

Here is the <code>fetchFromCache</code> function:

<pre><code class="language-javascript">function fetchFromCache (event) {
  return caches.match(event.request).then(response =&gt; {
    if (!response) {
      // A synchronous error that will kick off the catch handler
      throw Error('${event.request.url} not found in cache');
    }
    return response;
  });
}</code></pre>

Note: Don’t indicate which cache you wish to check with <code>caches.match</code>; check ’em all at once.</p>

### 3. Provide an Offline Fallback

If we’ve made it this far but there’s nothing in the cache we can respond with, return an appropriate offline fallback, if possible. For HTML pages, this is the page cached from <code>/offline/</code>. It’s a reasonably well-formatted page that tells the user they’re offline and that we can’t fulfill what they’re after.</p>

<pre><code class="language-javascript">fetch(request)
  .then(response =&gt; addToCache(cacheKey, request, response))
  .catch(() =&gt; fetchFromCache(event))
  .catch(() =&gt; offlineResponse(opts))
</code></pre>

And here is the <code>offlineResponse</code> function:

<pre><code class="language-javascript">function offlineResponse (resourceType, opts) {
  if (resourceType === 'image') {
    return new Response(opts.offlineImage,
      { headers: { 'Content-Type': 'image/svg+xml' } }
    );
  } else if (resourceType === 'content') {
    return caches.match(opts.offlinePage);
  }
  return undefined;
}</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06a1a98e-e144-4c21-ab10-167588207862/03-offline-page-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/179b43e1-963f-4e08-8a96-a23dab1ec2df/03-offline-page-preview-opt.png" alt="Providing an offline page" /></a><figcaption>An offline page (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06a1a98e-e144-4c21-ab10-167588207862/03-offline-page-opt.png">View large version</a>)</figcaption></figure>

## Other Resources: Implementing A Cache-First Strategy

The fetch logic for resources other than HTML content uses a <strong>cache-first strategy</strong>. Images and other static content on the website rarely change; so, check the cache first and avoid the network roundtrip.</p>

<pre><code class="language-javascript">event.respondWith(
  fetchFromCache(event)
    .catch(() =&gt; fetch(request))
    .then(response =&gt; addToCache(cacheKey, request, response))
    .catch(() =&gt; offlineResponse(resourceType, opts))
);
</code></pre>

The steps here are:

1.  try to retrieve the asset from cache;
2.  if that fails, try retrieving from the network (with read-through caching);
3.  if that fails, provide an offline fallback resource, if possible.</p>

### Offline Image

We can return an SVG image with the text “Offline” as an offline fallback by completing the <code>offlineResource</code> function:

<pre><code class="language-javascript">function offlineResponse (resourceType, opts) {
  if (resourceType === 'image') {
    // … return an offline image
  } else if (resourceType === 'content') {
    return caches.match('/offline/');
  }
  return undefined;
}</code></pre>

And let’s make the relevant updates to <code>config</code>:

<pre><code class="language-javascript">var config = {
  // …
  offlineImage: '&lt;svg role="img" aria-labelledby="offline-title"'
  + 'viewBox="0 0 400 300" xmlns="https://www.w3.org/2000/svg"&gt;'
  + '&lt;title id="offline-title"&gt;Offline&lt;/title&gt;'
  + '&lt;g fill="none" fill-rule="evenodd"&gt;&lt;path fill=&gt;"#D8D8D8" d="M0 0h400v300H0z"/&gt;'
  + '&lt;text fill="#9B9B9B" font-family="Times New Roman,Times,serif" font-size="72" font-weight="bold"&gt;'
  + '&lt;tspan x="93" y="172"&gt;offline&lt;/tspan&gt;&lt;/text&gt;&lt;/g&gt;&lt;/svg&gt;',
  offlinePage: '/offline/'
};
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c871a411-73d3-4a07-9035-0f88d7d31b7b/04-offline-image-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27f5662d-bb6a-4e31-aefd-7deda951c868/04-offline-image-preview-opt.png" alt="Providing an offline image" /></a><figcaption>An offline image. Credit for the SVG source goes to Jeremy Keith. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c871a411-73d3-4a07-9035-0f88d7d31b7b/04-offline-image-opt.png">View large version</a>)</figcaption></figure>

### Watch Out for CDNs

Watch out for CDNs if you are restricting fetch handling to your origin. When constructing my first service worker, I forgot that my hosting provider sharded assets (images and scripts) onto its CDN, so that they no were no longer served from my website’s origin (<code>lyza.com</code>). Whoops! That didn’t work. I ended up disabling the CDN for the affected assets (but optimizing those assets, of course!).</p>

## Completing The First Version

The first version of our service worker is now done. We have an <code>install</code> handler and a fleshed-out <code>fetch</code> handler that can respond to applicable fetches with optimized responses, as well as provide cached resources and an offline page when offline.

As users browse the website, they’ll continue to build up more cached items. When offline, they’ll be able to continue to browse items they’ve already got cached, or they’ll see an offline page (or image) if the resource requested isn’t available in cache.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dd11d73-8dcd-4dbc-9896-eb52911809f8/05-preview-offline-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36e238b2-ebc3-46c3-813e-999eec42af04/05-preview-offline-preview-opt.png" alt="Testing Offline Mode" /></a><figcaption>In Chrome, you can test how your service worker behaves offline by entering “device mode” and selecting the “Offline” network preset. This is an invaluable trick. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dd11d73-8dcd-4dbc-9896-eb52911809f8/05-preview-offline-opt.png">View large version</a>)</figcaption></figure>

The full code with fetch handling (<code>serviceWorker.js</code>) <a href="https://github.com/lyzadanger/serviceworker-example/blob/master/02-fetch-handling/serviceWorker.js">is on GitHub</a>.</p>

## Versioning And Updating The Service Worker

If nothing were ever going to change on our website again, we could say we’re done. However, service workers need to be updated from time to time. Maybe I’ll want to add more cache-able paths. Maybe I want to evolve the way my offline fallbacks work. Maybe there’s something slightly buggy in my service worker that I want to fix.

I want to stress that there are automated tools for making service-worker management part of your workflow, like <a href="https://github.com/GoogleChrome/sw-precache">Service Worker Precache</a> from Google. You don’t <em>need</em> to manage versioning this by hand. However, the complexity on my website is low enough that I use a human versioning strategy to manage changes to my service worker. This consists of:

*   a simple version string to indicate versions,
*   implementation of an `activate` handler to clean up after old versions,
*   updating of the `install` handler to make updated service workers `activate` faster.</p>

## Versioning Cache Keys

I can add a <code>version</code> property to my <code>config</code> object:

<pre><code class="language-javascript">version: 'aether'</code></pre>

This should change any time I want to deploy an updated version of my service worker. I use the names of Greek deities because they’re more interesting to me than random strings or numbers.

Note: I made some changes to the code, adding a convenience function (<code>cacheName</code>) to generate prefixed cache keys. It’s tangential, so I’m not including it here, but you can see it in the <a href="https://github.com/lyzadanger/serviceworker-example/blob/master/03-versioning/serviceWorker.js">completed service worker code</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5795391-c3bb-4696-ab77-f31ee275410d/06-cache-contents-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5795391-c3bb-4696-ab77-f31ee275410d/06-cache-contents-opt.png" alt="Cache contents in Chrome Developer Tools" /></a><figcaption>In Chrome, you can see the contents of caches in the “Resources” tab. You can see how different versions of my service worker have different cache names. (This is version <code>achilles</code>.) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5795391-c3bb-4696-ab77-f31ee275410d/06-cache-contents-opt.png">View large version</a>)</figcaption></figure>

### Don’t Rename Your Service Worker

At one point, I was futzing around with naming conventions for the service worker’s file name. Don’t do this. If you do, the browser will register the new service worker, but the old service worker will stay installed, too. This is a messy state of affairs. I’m sure there’s a workaround, but I’d say don’t rename your service worker.</p>

### Don’t Use importScripts for config

I went down a path of putting my <code>config</code> object in an external file and using <a href="https://developer.mozilla.org/en-US/docs/Web/API/WorkerGlobalScope/importScripts"><code>self.importScripts()</code></a> in the service worker file to pull that script in. That seemed like a reasonable way to manage my <code>config</code> outside of the service worker, but there was a hitch.

The browser byte-compares service worker files to determine whether they have been updated — that’s how it knows when to re-trigger a download-and-install cycle. Changes to the external <code>config</code> don’t cause any changes to the service worker itself, meaning that changes to the <code>config</code> weren’t causing the service worker to update. Whoops.</p>

## Adding An Activate Handler

The purpose of having version-specific cache names is so that we can clean up caches from previous versions. If there are caches around during activation that are not prefixed with the current version string, we’ll know that they should be deleted because they are crufty.</p>

### Cleaning Up Old Caches

We can use a function to clean up after old caches:

<pre><code class="language-javascript">function onActivate (event, opts) {
  return caches.keys()
    .then(cacheKeys =&gt; {
      var oldCacheKeys = cacheKeys.filter(key =&gt;
        key.indexOf(opts.version) !== 0
      );
      var deletePromises = oldCacheKeys.map(oldKey =&gt; caches.delete(oldKey));
      return Promise.all(deletePromises);
    });
}</code></pre>

### Speeding Up Install and Activate

An updated service worker will get downloaded and will <code>install</code> in the background. It is now a <strong>worker in waiting</strong>. By default, the updated service worker will not activate while any pages are loaded that are still using the old service worker. However, we can speed that up by making a small change to our <code>install</code> handler:

<pre><code class="language-javascript">self.addEventListener('install', event =&gt; {
  // … as before

  event.waitUntil(
    onInstall(event, config)
     .then( () =&gt; self.skipWaiting() )
  );
});</code></pre>

<code>skipWaiting</code> will cause <code>activate</code> to happen immediately.

Now, finish the <code>activate</code> handler:

<pre><code class="language-javascript">self.addEventListener('activate', event =&gt; {
  function onActivate (event, opts) {
    // … as above
  }

  event.waitUntil(
    onActivate(event, config)
     .then( () =&gt; self.clients.claim() )
  );
});</code></pre>

<code>self.clients.claim</code> will make the new service worker take effect immediately on any open pages in its scope.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a8b15f0-b122-4cb8-9924-932eab39f7b3/07-serviceworker-internals-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fe97e08-d592-40cd-9de4-ca92e416e76a/07-serviceworker-internals-preview-opt.png" alt="Viewing Serviceworker Internals in Chrome" /></a><figcaption>You can use the special URL <code>chrome://serviceworker-internals</code> in Chrome to see all of the service workers that the browser has registered. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a8b15f0-b122-4cb8-9924-932eab39f7b3/07-serviceworker-internals-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e91d29d6-b366-4878-8b76-1b71ffaeca5a/08-my-site-offline-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac8e0a53-ea84-4316-bd14-c33fa0f3074b/08-my-site-offline-preview-opt.png" alt="My website's offline mode" /></a><figcaption>Here is my website as it appears in Chrome’s device mode, with the “Offline Network” preset, emulating what a user would see when offline. It works! (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e91d29d6-b366-4878-8b76-1b71ffaeca5a/08-my-site-offline-opt.png">View large version</a>)</figcaption></figure>

## Ta-Da!

We now have a version-managed service worker! You can see the updated <a href="https://github.com/lyzadanger/serviceworker-example/blob/master/03-versioning/serviceWorker.js"><code>serviceWorker.js</code> file with version management on GitHub</a>.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [A Beginner’s Guide To Progressive Web Apps](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/)
*   [Building A Simple Cross-Browser Offline To-Do List](https://www.smashingmagazine.com/2014/09/building-simple-cross-browser-offline-todo-list-indexeddb-websql/)
*   [World Wide Web, Not Wealthy Western Web](https://www.smashingmagazine.com/2017/03/world-wide-web-not-wealthy-western-web-part-1/)

{{< signature "jb, ml, al, mse" >}}

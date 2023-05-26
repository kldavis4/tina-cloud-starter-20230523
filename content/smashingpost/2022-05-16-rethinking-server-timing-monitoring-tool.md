---
title: 'Rethinking Server-Timing As A Critical Monitoring Tool'
slug: rethinking-server-timing-monitoring-tool
author: sean-roberts
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f69c3e0-764f-4cfb-b8f8-7a4420d0e2f6/rethinking-server-timing-monitoring-tool.jpg
date: 2022-05-16T10:00:00.000Z
summary: >-
  What makes the underused `Server-Timing` header uniquely powerful among all other response headers? We’ll rethink the expectation for using it exclusively for timing and see fast solutions for hard-to-solve monitoring challenges.
description: >-
  What makes the underused `Server-Timing` header uniquely powerful among all other response headers? We’ll rethink the expectation for using it exclusively for timing and see fast solutions for hard-to-solve monitoring challenges.
categories:
  - JavaScript
  - Performance
  - API
---

In the world of HTTP Headers, there is one header that I believe deserves more air-time and that is the [`Server-Timing` header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Server-Timing). To me, it’s a must-use in any project where real user monitoring (RUM) is being instrumented. To my surprise, web performance monitoring conversations rarely surface `Server-Timing` or cover a very shallow understanding of its application &mdash; despite it being out for many years.

Part of that is due to the perceived limitation that it’s exclusively for tracking time on the server &mdash; it can provide so much more value! Let’s rethink how we can leverage this header. In this piece, we will dive deeper to show how `Server-Timing` headers are so uniquely powerful, show some practical examples by solving challenging monitoring problems with this header, and provoke some creative inspiration by combining this technique with service workers.

`Server-Timing` is uniquely powerful, because it is the **only** HTTP Response header that supports setting free-form values for a specific resource and makes them accessible from a JavaScript Browser API separate from the Request/Response references themselves. This allows resource requests, including the HTML document itself, to be enriched with data during its lifecycle, and that information can be inspected for measuring the attributes of that resource!

The only other header that’s close to this capability is the HTTP [`Set-Cookie`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie) / [`Cookie`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cookie) headers. Unlike `Cookie` headers, `Server-Timing` is only on the response for a specific resource where `Cookies` are sent on requests and responses for all resources after they’re set and unexpired. Having this data bound to a single resource response is preferable, as it prevents ephemeral data about all responses from becoming ambiguous and contributes to a growing collection of cookies sent for remaining resources during a page load. 

## Setting `Server-Timing`

This header can be set on the response of any network resource, such as XHR, fetch, images, HTML, stylesheets, etc. Any server or proxy can add this header to the request to provide inspectable data. The header is constructed via a name with an optional description and/or metric value. The only required field is the name. Additionally, there can be many `Server-Timing` headers set on the same response which would be combined and separated via a comma.

A few simple examples:

<pre><code class="language-javascript">Server-Timing: cdn_process;desc=”cach_hit";dur=123

Server-Timing: cdn_process;desc=”cach_hit", server_process; dur=42;

Server-Timing: cdn_cache_hit

Server-Timing: cdn_cache_hit; dur=123</code></pre>

**Important Note**: For cross-origin resources, `Server-Timing` and other potentially sensitive timing values are not exposed to consumers. To allow these features, we will also need the `Timing-Allow-Origin` header that includes our origin or the `*` value.

For this article, that’s all we’ll need to start exposing the value and leave other more specific articles to go deeper. [MDN docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Server-Timing).

{{% feature-panel %}}

## Consuming `Server-Timing`

Web browsers expose a global Performance Timeline API to inspect details about specific metrics/events that have happened during the page lifecycle. From this API we can access built-in performance API extensions which expose timings in the form of [`PerformanceEntries`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceEntry).

There are a handful of different entry subtypes but, for the scope of this article, we will be concerned with the `PerformanceResourceTiming` and `PerformanceNavigationTiming` subtypes. These subtypes are currently the only subtypes related to network requests and thus exposing the `Server-Timing` information.

For the top-level HTML document, it is fetched upon user navigation but is still a resource request. So, instead of having different `PerformanceEntries` for the navigation and the resource aspects, the `PerformanceNavigationTiming` provides resource loading data as well as additional navigation-specific data. Because we are looking at just the resource load data, we will exclusively refer to the requests (navigational docs or otherwise) simply as resources.

To query performance entries, we have 3 APIs that we can call: `performance.getEntries()`, `performance.getEntriesByType()`, `performance.getEntriesByName()`. Each will return an array of performance entries with increasing specificity.

<pre><code class="language-javascript">const navResources = performance.getEntriesByType('navigation');
const allOtherResources = performance.getEntriesByType('resource');</code></pre>

Finally, each of these resources will have a `serverTiming` field which is an array of objects mapped from the information provided in the `Server-Timing` header &mdash; where [`PerformanceEntryServerTiming`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceServerTiming) is supported (see considerations below). The shape of the objects in this array is defined by the [`PerformanceEntryServerTiming`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceServerTiming) interface which essentially maps the respective `Server-Timing` header metric options: `name`, `description`, and `duration`.

Let’s look at this in a complete example.

A request was made to our data endpoint and among the headers, we sent back the following:

<pre><code class="language-javascript">Server-Timing: lookup_time; dur=42, db_cache; desc=”hit”;</code></pre>

On the client-side, let’s assume this is our only resource loaded on this page:

<pre><code class="language-javascript">
const dataEndpointEntry = performance.getEntriesByName('resource')[0];

console.log( dataEndpointEntry.serverTiming );

// outputs:
// [
//   { name: “lookup_time”, description: undefined, duration: 42 },
//   { name: “db_cache”, description:”hit”, duration: 0.0 },
// ]</code></pre>

That covers the fundamental APIs used to access resource entries and the information provided from a `Server-Timing` header. For links to more details on these APIs, see the resources section at the bottom.

Now that we have the fundamentals of how to set and use this header/API combo, let’s dive into the fun stuff.

## It’s Not Just About Time

From my conversations and work with other developers, the name “Server-Timing” impresses a strong connection that this is a tool used to track spans of time or a detail about a span of time exclusively. This is entirely justified by the name and the intent of the feature. However, the spec for this header is very flexible; allowing for values and expressing information that could have nothing to do with timing or performance in any way. Even the `duration` field has no predefined unit of measurement &mdash; you can put any number (double) in that field. By stepping back and realizing that the fields available have no special bindings to particular types of data, we can see that this technique is also an effective delivery mechanism for any arbitrary data allowing lots of interesting possibilities.  

Examples of non-timing information you could send: HTTP Response status code, regions, request ids, etc. &mdash; any freeform data that suits your needs. In some cases, we might send redundant information that might be in other headers already, but that’s ok. As we will cover, accessing other headers for resources quite often isn’t possible, and if it has monitoring value, then it’s ok to be redundant.

## No References Required

Due to the design of web browser APIs, there are currently no mechanisms for querying requests and their relative responses after the fact. This is important because of the need to manage memory. To read information about a request or its respective response, we have to have a direct reference to these objects. All of the web performance monitoring software we work with provide RUM clients that put additional layers of monkey patching on the page to maintain direct access to a request being made or the response coming back. This is how they offer drop-in monitoring of all requests being made without us needing to change our code to monitor a request. This is also why these clients require us to put the client before any request that we want to monitor. The complexities of patching all of the various networking APIs and their linked functionality can become very complex very quickly. If there were an easy access mechanism to pull relevant resource/request information about a request, we would certainly prefer to do that on the monitoring side.

To make matters more difficult, this monkey-patching pattern only works for resources where JavaScript is directly used to initiate the networking. For Images, Stylesheets, JS files, the HTML Doc, etc. the methods for monitoring the request/response details are very limited, as usually there is no direct reference available. 

This is where the Performance Timeline API provides great value. As we saw earlier, it quite literally is a list of requests made and some data about each of them respectively. The data for each performance entry is very minimal and almost entirely limited to timing information and some fields that, depending on their value, would impact how a resource’s performance is measured relative to other resources. Among the timing fields, we have direct access to the `serverTiming` data.

Putting all of the pieces together, resources can have `Server-Timing` headers in their network responses that contain arbitrary data. Those resources can then be easily queried, and the `Server-Timing` data can be accessed without a direct reference to the request/response itself. With this, it doesn’t matter if you can access/manage references for a resource, all resources can be enriched with arbitrary data accessible from an easy-to-use web browser API. That’s a very unique and powerful capability!

Next, let’s apply this pattern to some traditionally tough challenges to measure.

{{% ad-panel-leaderboard %}}

## Solution 1: Inspecting Images and Other Asset Responses

Images, stylesheets, JavaScript files, etc. typically aren’t created by using direct references to the networking APIs with information about those requests. For example, we almost always trigger image downloads by putting an `img` element in our HTML. There are techniques for loading these assets which require using JavaScript `fetch`/`xhr` APIs to pull the data and push it into an asset reference directly. While that alternate technique makes them easier to monitor, it is catastrophic to performance in most cases. The challenge is how do we inspect these resources without having direct networking API references?

To tie this to real-world use cases, it’s important to ask why might we want to inspect and capture response information about these resources? Here are a few reasons:

- **We might want to proactively capture details like status codes for our resources, so we can triage any changes.**  
For example, missing images (404s) are likely totally different issues and types of work than dealing with images returning server errors (500s).
- **Adding monitoring to parts of our stack that we don’t control.**  
Usually, teams offload these types of assets to a CDN to store and deliver to users. If they are having issues, how quickly will the team be able to detect the issue?
- **Runtime or on-demand variations of resources have become more commonplace techniques.**  
For example, image resizing, automatic polyfilling of scripts on the CDN, etc &mdash; these systems can have many limits and reasons for why they might not be able to create or deliver a variation. If you expect that 100% of users retrieve a particular type of asset variation, it’s valuable to be able to confirm that.  
This came up at a previous company I worked at where on-demand image resizing was used for thumbnail images. Due to the limitations of the provider, a significant number of users would get worse experiences due to full-size images loading where thumbnails are supposed to appear. So, where we thought >99% of users would get optimal images, >30% would hit performance issues, because images did not resize.

Now that we have some understanding of what might motivate us to inspect these resources, let’s see how `Server-Timing` can be leveraged for inspection. 

Image HTML:

<div class="break-out">

<pre><code class="language-javascript">&lt;img src="/user-rsrc/12345?resize=true&height=80&width=80&format=webp" alt="..."/&gt;</code></pre>
</div>

Image response headers:

<div class="break-out">

<pre><code class="language-javascript">Status: 200
…
Server-Timing: status_code; dur=200;, resizing; desc=”failed”; dur=1200; req_id; desc=”zyx4321”</code></pre>
</div>

Inspecting the image response information:

<div class="break-out">

<pre><code class="language-javascript">const imgPerfEntry = performance.getEntriesByName('/user-rsrc/12345?resize=true&height=80&width=80&format=webp')[0];

// filter/capture entry data as needed
console.log(imgPerfEntry.serverTiming);

// outputs:
// [
//   { name: “status_code”, description: undefined, duration: 200 },
//   { name: “resizing”, description:”failed”, duration: 1200 },
//   { name: “req_id”, description:”zyx4321”, duration: 0.0 },
// ]</code></pre>
</div>

This metric was very valuable because, despite returning “happy” responses (200s), our images weren’t resized and potentially not converted to the right format, etc. Along with the other performance information on the entry like download times, we see the status was served as `200` (not triggering our onerror handlers on the element), resizing failed after spending `1.2s` on attempting to resize, and we have a request-id that we can use to debug this in our other tooling. By sending this data to our RUM provider, we can aggregate and proactively monitor how often these conditions happen.

## Solution 2: Inspect Resources That Return Before JS Runs

Code used to monitor resources (fetch, XHR, images, stylesheets, scripts, HTML, etc.) requires JavaScript code to aggregate and then send the information somewhere. This almost always means there’s an expectation for the monitoring code to run before the resources that are being monitored. The example presented earlier of the basic monkey patching used to automatically monitor fetch requests is a good example of this. That code has to run before any fetch request that needs to be monitored. However, there are lots of cases, from performance to technical constraints, where we might not be able to or simply should not change the order in which a resource is requested to make it easier to be monitored.

Another very common monitoring technique is to put event listeners on the page to capture events that might have monitoring value. This usually comes in the form of `onload` or `onerror` handlers on elements or using `addEventListener` more abstractly. This technique requires JS to have been set before the event fires, or before the listener itself is attached. So, this approach still carries the characteristic only monitoring events going forward, after the monitoring JS is run, thus requiring the JS to execute before the resources requiring measurement.

Mapping this to real-world use-cases, e-commerce sites put a heavy emphasis on “above the fold” content rendering very quickly &mdash; typically deferring JS as much as possible. That said, there might be resources that are impactful to measure, such as successful delivery of the product image. In other situations, we might also decide that the monitoring library itself shouldn’t be in the critical path due to page weight. What are the options to inspect these requests retroactively?

The technique is the same as Solution #1! This is possible because browsers automatically maintain a buffer of all of the Performance Entries (subject to the [buffer size limit](https://developer.mozilla.org/en-US/docs/Web/API/Performance/setResourceTimingBufferSize) that can be changed). This allows us to defer JS until later in the page load cycle without needing to add listeners ahead of the resource.

Instead of repeating the Solution #1 example, let’s look at what both retroactive and future inspection of performance entries looks like to show the difference of where they can be leveraged. Please note that, while we are inspecting images in these examples, we can do this for any resource type.

Setting up context for this code, our need is that we have to ensure our product images are being delivered successfully. Let’s assume all website images return this `Server-Timing` header structure. Some of our important images can happen before our monitoring script and, as the user navigates, more will continue to load. How do we handle both?

Image response headers:

<div class="break-out">

<pre><code class="language-javascript">Status: 200
…
Server-Timing: status_code; dur=200;, resizing; desc="success"; dur=30; req_id; desc="randomId"</code></pre>
</div>

Our monitoring logic. We expect this to run after the critical path content of the page.

Inspecting the image response information:

<div class="break-out">

<pre><code class="language-javascript">function monitorImages(perfEntries){
  perfEntries.forEach((perfEntry)=&gt;{
  // monitoring for the performance entries
  
console.log(perfEntry.serverTiming);
})
}

const alreadyLoadedImageEntries = performance.getEntriesByType('resource').filter(({ initiatorType })=&gt; initiatorType === 'img');

monitorImages( alreadyLoadedImageEntries );

const imgObserver = new PerformanceObserver(function(entriesList) {
const newlyLoadedImageEntries = entriesList.getEntriesByType('resource').filter(({ initiatorType })=&gt; initiatorType === 'img');
  monitorImages( newlyLoadedImageEntries );
});
imgObserver.observe({entryTypes: ["resource"]});
</code></pre>
</div>

Despite deferring our monitoring script until it was out of the critical path, we are capturing the data for all images which have loaded before our script and will continue to monitor them, as the user continues using the site.

## Solution 3: Inspecting the HTML Doc

The final example solution we will look at is related to the ultimate “before JS can run” resource &mdash; the HTML document itself. If our monitoring solutions are loaded as JS via the HTML, how can we monitor the delivery of the HTML document?

There is some precedence in monitoring HTML doc delivery. For monitoring response data, the most common setup is to use server logs/metrics/traces to capture this information. That is a good solution but depending on the tooling, the data may be decoupled from RUM data causing us to need multiple tools to inspect our user experiences. Additionally, this practice could also miss metadata (page instance identifiers for example) that allows us to aggregate and correlate information for a given page load &mdash; for example, correlating async requests failing when the doc returns certain document response codes.

A common pattern for doing this work is putting the content inside of the HTML content itself. This has to be put into the HTML content, because the JS-based monitoring logic does not have access to the HTML request headers that came before it. This turns our HTML document into a dynamic document content. This may be fine for our needs and allows us to take that information and provide it to our RUM tooling. However, this could become a challenge if our system for HTML delivery is out of our control, or if the system has some assumptions into how HTML delivery must function. Examples of this might be, expecting that the HTML is fully static, such that we can cache it downstream in some deterministic manner &mdash; “partially dynamic” HTML bodies are much more likely to be handled incorrectly by caching logic. 

Within the HTML delivery process, there could also be additional data that we want to understand, such as what datacenters processed the request throughout the chain. We might have a CDN edge handler that proxies a request from an origin. In this case, we can’t expect each layer could/should process and inject HTML content. How might `Server-Timing` headers help us here?

Building on the concepts of Solution #1 and Solution #2, here’s how we can capture valuable data about the HTML document itself. Keep in mind that any part of the stack can add a `Server-Timing` header to the response, and it will be joined together in the final header value.

Let’s assume we have a CDN edge handler and an origin which can process the document:

CDN added response headers:

<div class="break-out">

<pre><code class="language-javascript">Status: 200
…
Server-Timing: cdn&#95;status&#95;code; dur=200;, cdn&#95;cache; desc=”expired”; dur=15; cdn&#95;datacenter; desc=”ATL”; cdn&#95;req&#95;id; desc=”zyx321abc789”; cdn&#95;time; dur=120;
</code></pre>
</div>

Origin added response headers:

<div class="break-out">

<pre><code class="language-javascript">Status: 200
…
Server-Timing: origin&#95;status&#95;code; dur=200;, origin&#95;time; dur=30; origin&#95;region; desc=”us-west”; origin&#95;req&#95;id; desc="qwerty321ytrewq789";
</code></pre>
</div>

Inspecting the HTML response information:

<div class="break-out">

<pre><code class="language-javascript">// as mentioned earlier, the HTML document is a 'navigation' type of Performance Entry
// that has a superset of information related to the resource and the navigation-specific info
const htmlPerfEntry = performance.getEntriesByType('navigation')[0];

// filter/capture entry data as needed
console.log(htmlPerfEntry.serverTiming);

// outputs:
// [
//   { name: “cdn_status_code”, description: undefined, duration: 200 },
//   { name: “cdn_cache”, description:”expired”, duration: 0.0},
//   { name: “cdn_datacenter”, description:”ATL”, duration: 0.0 },
//   { name: “cdn_req_id”, description:”zyx321abc789”, duration: 0.0 },
//   { name: “cdn_time”, description: undefined, duration: 120 },
//   { name: “origin_status_code”, description: undefined, duration: 200 },
//   { name: “origin_time”, description: undefined, duration: 30 },
//   { name: “origin_region”, description:”us-west”, duration: 0.0 },
//   { name: “origin_req_id”, description:”qwerty321ytrewq789”, duration: 0.0 },
// ]</code></pre>
</div>

From this information, our monitoring JavaScript (which could have been loaded way later) can aggregate where the HTML processing happened, status codes from the different servers (which can differ for legit reasons &mdash; or bugs), and request identifiers if they need to correlate this with server logs. It also knows how much time was taken on the “server” via the `cdn_time` duration &mdash; “server” time being the total time starting at the first non-user proxy/server that we provide. Using that `cdn_time` duration, the already accessible HTML Time-To-First-Byte value and the `origin_time` duration, we can determine latency sections more accurately, such as the user latency, the `cdn` to origin latency, etc. This is incredibly powerful in optimizing such a critical delivery point and protecting it from regression.

{{% ad-panel-leaderboard %}}

## Combining Server-Timing with Service Workers

[Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) are scripts that are initialized by the website to sit between the website, the browser, and the network (when available). When acting as a proxy, they can be used to read and modify requests coming from and responses returning to the website. Given service workers are so feature rich, we won’t attempt to cover them in depth in this article &mdash; a simple web search will yield a mountain of information about their capabilities. For this article, we will focus on the proxying capability of a service worker &mdash; it’s ability to process requests/responses. 

The key to combining these tools is knowing that the `Server-Timing` header and its respective `PerformanceEntry` is calculated **after** service worker proxying takes place. This allows us to use the service workers to add `Server-Timing` headers to responses that can provide valuable information about the request itself.

What type of information might we want to capture within the service worker? As mentioned before, service workers have lots of capabilities, and any one of those actions could produce something valuable to capture. Here are a few that come to mind:

- Is this request served from the service worker cache?
- Is this served from the service worker while off-line?
- What service worker strategy for this request type is being used?
- What version of the service worker is being used?  
This is helpful in checking our assumptions about service worker invalidation.
- Take values from other headers and put them into a `Server-Timing` header for downstream aggregation.  
Valuable when we don’t have the option to change the headers on the request but would like to inspect them in RUM &mdash; such is usually the case with CDN providers.
- How long has a resource been in service worker cache?

Service workers have to be initialized on the website which is an asynchronous process itself. Furthermore, service workers only process requests within the defined scope. As such, even the basic question of, “is this request processed by the service worker?” can drive interesting conversations on how much we are leaning on its capabilities to drive great experiences.

Let’s dive into how this might look in the code.

Basic JS logic used on the site to initialize the service worker:

<div class="break-out">

<pre><code class="language-javascript">if ('serviceWorker' in navigator) {
navigator.serviceWorker.register('/service-worker.js').then(function (registration) {
registration.update(); // immediately start using this sw
 });
}</code></pre>
</div>

Inside of `/service-worker.js`, basic request/response proxying:

<div class="break-out">

<pre><code class="language-javascript">const CACHE&#95;NAME = 'sw-cached-files-v1';

self.addEventListener('fetch', function (event) {
  event.respondWith(
    // check to see if this request is cached
    caches.match(event.request)
      .then(function (response) {

        // Cache hit - return response
        if (response) {
          const updatedHeaders = new Headers(response.headers);
          updatedHeaders.append('Server-Timing', 'sw&#95;cache; desc="hit";');
          const updatedResponse = new Response(response.body, {
            ...response,
            headers: updatedHeaders
          });
          return updatedResponse;
        }
        
        return fetch(event.request).then(function (response) {

            // depending on the scope where we load our service worker,
            // we might need to filter our responses to only process our
            // first-party requests/responses
            // Regex match on the event.request.url hostname should

            const updatedHeaders = new Headers(response.headers);
            updatedHeaders.append('Server-Timing', `status&#95;code;desc=${response.status};, sw&#95;cache; desc="miss";`)

            const modifiableResponse = new Response(response.body, {
              ...response,
              headers: updatedHeaders
            });

            // only cache known good state responses
            if (!response || response.status !== 200 || response.type !== 'basic' || response.headers.get('Content-Type').includes('text/html')) {
              return modifiableResponse;
            }

            const responseToCache = modifiableResponse.clone();

            caches.open(CACHE&#95;NAME).then(function (cache) {
              cache.put(event.request, responseToCache);
            });

            return modifiableResponse;
          }
        );
      })
  );
});</code></pre>
</div>

Requests that are processed from the service worker, now will have a `Server-Timing` header appended to their responses. This allows us to inspect that data via the Performance Timeline API, as we demonstrated in all of our prior examples. In practice, we likely didn’t add the service worker for this single need &mdash; meaning we already have it instrumented for handling requests. Adding the one header in 2 places allowed us to measure status codes for all requests, service worker-based cache-hit ratios, and how often service workers are processing requests.

### Why Use `Server-Timing` If We Have Service Workers?

This is an important question that comes up when discussing combining these techniques. If a service worker can grab all of the header and content information, why do we need a different tool to aggregate it? 

The work of measuring timing and other arbitrary metadata about requests is almost always, so that we can send this information to a RUM provider for analysis, alerting, etc. All major RUM clients have 1 or 2 windows for which we can enrich the data about a request &mdash; when the response happens, and when the `PerformanceEntry` is detected. For example, if we make a fetch request, the RUM client captures the request/response details and sends it. If a `PerformanceEntry` is observed, the client sends that information as well &mdash; attempting to associate it to the prior request if possible. If RUM clients offer the ability to add information about that requests/entries, those were the only windows to do it. 

In practice, a service worker may or may not be activated yet, a request/response may or may not have processed the service worker, and all service worker data sharing requires async messaging to the site via `postMessage()` API. All of these aspects introduce race conditions for a service worker to be active, able to capture data, and then send that data in time to be enriched by the RUM client.

Contrasting this with `Server-Timing`, a RUM client that processes the Performance Timeline API will immediately have access to any `Server-Timing` data set on the `PerformanceEntry`.

Given this assessment of service worker’s challenges with enriching request/response data reliably, my recommendation is that service workers be used to provide more data and context instead of being the exclusive mechanism for delivering data to the RUM client on the main thread. That is, use `Server-Timing` and, where needed, use service worker to add more context or in cases where `Server-Timing` isn’t supported &mdash; if required. In this case, we might be creating custom events/metrics instead of enriching the original request/response data aggregation, as we will assume that the race conditions mentioned will lead to missing the windows for general RUM client enrichment.

## Considerations for `Server-Timing` Usage

As uniquely powerful as it is, it’s not without important considerations. Here’s a list of considerations based on the current implementation at time of writing:

- **Browser Support** &mdash; Safari does not support putting the `Server-Timing` data into the Performance Timeline API (they do show it in DevTools).   
This is a shame, however, given this is not about functionality for users, but instead it’s about improved capabilities for performance monitoring &mdash; I side with this not being a blocking problem. With browser-based monitoring, we never expect to measure 100% of browsers/users. Currently, this means we’d look to get ~70-75% support based on global browser usage data. Which is usually more than enough to feel confident that our metrics are showing us good signals about the health and performance or our systems. As mentioned, `Server-Timing` is sometimes the only way to get those metrics reliably, so we should feel confident about leveraging this tool.  
As mentioned previously, if we absolutely have to have this data for Safari, we could explore using a cookie-based solution for Safari users. Any solutions here would have to be tested heavily to ensure they don’t hinder performance. 
- **If we are looking to improve performance, we want to avoid adding lots of weight to our responses, including headers.** This is a trade-off of additional weight for value added metadata. My recommendation is that if you’re not in the range 500 bytes or more to your `Server-Timing` header, I would not be concerned. If you are worried, try varying lengths and measure its impact!
- **When appending multiple `Server-Timing` headers on a single response, there is a risk of duplicate `Server-Timing` metric names.** Browsers will surface all of them in the `serverTiming` array on the `PerformanceEntry`. It’s best to ensure that this is avoided by specific or namespaced naming. If it can’t be avoided, then we would break down the order of events that added each header and define a convention we can trust. Otherwise, we can create a utility that doesn’t blindly add `Server-Timing` entries but will also update existing entries if they are already on the Response.
- **Try to avoid the mistake of misremembering that responses cache the `Server-Timing` values as well.** In some cases you might want to filter out the timing-related data of cached responses that, before they were cached, spent time on the server. There are varying ways to detect if the request went to the network with data on the `PerformanceEntry`, such as `entry.transferSize > 0`, or `entry.decodedBodySize > 0`, or `entry.duration > 40`. We can also lean into what we’ve learned with `Server-Timing` to set a timestamp on the header for comparison.

## Wrapping Up

We’ve gone pretty deep into the application of the `Server-Timing` Header for use cases that aren’t aligned to the “timing” use case that this header is generally associated with. We’ve seen its power to add freeform data about a resource and access the data without needing a reference to the networking API used to make it. This is a very unique capability that we leveraged to measure resources of all types, inspect them retroactively, and even capture data about the HTML doc itself. Combining this technique with service workers, we can add more information from the service worker itself or to map response information from uncontrolled server responses to `Server-Timing` for easy access.

I believe that `Server-Timing` is so impressively unique that it should be used way more, but I also believe that it shouldn’t be used for everything. In the past, this has been a must-have tool for performance instrumentation projects I’ve worked on to provide impossible to access resource data and identify where latency is occuring. If you’re not getting value out of having the data in this header, or if it doesn’t fit your needs &mdash; there’s no reason to use it. The goal of this article was to provide you with a new perspective on `Server-Timing` as a tool to reach for, even if you’re not measuring time. 

### Resources

- [W3C Server Timing](https://www.w3.org/TR/server-timing/)
- [Server-Timing MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Server-Timing)
- “[Measuring Performance With Server Timing](https://www.smashingmagazine.com/2018/10/performance-server-timing/)”, Drew McLellan
- [Performance Timeline MDN](https://developer.mozilla.org/en-US/docs/Web/API/Performance_Timeline)

{{< signature "vf, yk, il" >}}

---
title: 'Preload: What Is It Good For?'
slug: preload-what-is-it-good-for
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e836a24-66de-43df-af76-1dd15773359f/skeleton-500px-opt.png
date: 2016-02-26T20:23:26.000Z
author: yoav-weiss
description: >-
  **Preload** ([spec](https://w3c.github.io/preload/)) is a new web standard
  aimed at improving performance and providing more granular loading control to
  web developers. It gives developers the ability to **define custom loading**
  logic without suffering the performance penalty that script-based resource
  loaders incur.

  A few weeks ago, I shipped preload support in Chrome Canary, and barring
  unexpected bugs it will hit Chrome stable in mid-April. But what is that
  preload thing? What does it do? And how can it help you?
categories:
  - Coding
  - JavaScript
  - Performance
---
<strong>Preload</strong> (<a href="https://w3c.github.io/preload/">spec</a>) is a new web standard aimed at improving performance and providing more granular loading control to web developers. It gives developers the ability to <strong>define custom loading</strong> logic without suffering the performance penalty that script-based resource loaders incur.</p>

### <span class="rh">Further reading</span> on Smashing:

*   [Perceived Performance](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/)
*   [Getting Ready For HTTP/2](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [Everything You Need To Know About AMP](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)
*   [Progressive Enhancement](https://www.smashingmagazine.com/2015/12/reimagining-single-page-applications-progressive-enhancement/)
*   [Improving Smashing Magazine’s Performance](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)

A few weeks ago, I <a href="https://groups.google.com/a/chromium.org/d/msg/blink-dev/_nu6HlbNQfo/XzaLNb1bBgAJ">shipped</a> preload support in Chrome Canary, and barring unexpected bugs it will hit Chrome stable in mid-April. But what is that preload thing? What does it do? And how can it help you?

Well, <code>&lt;link rel="preload"&gt;</code> is a declarative fetch directive.

{{% feature-panel %}}

In human terms, it's a way to tell a browser to start fetching a certain resource, because we as authors (or as server administrators, or as smart-server developers) know that the browser is going to need that particular resource pretty soon.</p>

## Didn't We Already Have That?

Kinda, but not really. <code>&lt;link rel="prefetch"&gt;</code> has been supported on the web for a long while, and has <a href="https://caniuse.com/#feat=link-rel-prefetch">decent browser support</a>. On top of that we've also supported <a href="https://web.archive.org/web/20150907034803/https://www.chromium.org/spdy/link-headers-and-server-hint/link-rel-subresource"><code>&lt;link rel="subresource"&gt;</code></a> in Chrome for some time. So what's new about preload? How is it different from these other directives? They all tell the browser to fetch things, right?

Well, they do, but there are significant differences between them. Differences that warrant a shiny new directive that tackles many use cases that the old ones never did.

<code>&lt;link rel="prefetch"&gt;</code> is a directive that tells a browser to <strong>fetch a resource that will probably be needed</strong> for the next navigation. That mostly means that the resource will be fetched with extremely low priority (since everything the browser <em>knows</em> is needed in the current page is more important than a resource that we <em>guess</em> might be needed in the next one). That means that prefetch's main use case is speeding up the next navigation rather than the current one.

<code>&lt;link rel="subresource"&gt;</code> was originally planned to tackle the current navigation, but it failed to do that in some spectacular ways. Since the web developer had no way to define what the priority of the resource should be, the browser (just Chrome and Chromium-based browsers, really) downloaded it with fairly low priority, which meant that in most cases, the resource request came out at about the same time that it would if subresource wasn't there at all.</p>

## How Can Preload Do Better?

Preload is destined for current navigation, just like subresource, but it includes one small yet significant difference. It has an <code>as</code> attribute, which enables the browser to do a number of things that subresource and prefetch did not enable:

*   The **browser can set the right resource priority**, so that it would be loaded accordingly, and will not delay more important resources, nor tag along behind less important resources.
*   The browser can make sure that the request is subject to the right [Content-Security-Policy](https://www.html5rocks.com/en/tutorials/security/content-security-policy/) directives, and doesn't go out to the server if it shouldn't.
*   The browser can send the appropriate `Accept` headers based on the resource type. (e.g. advertise support for "image/webp" when fetching images)
*   The browser knows the resource type so it can later determine if the resource could be reused for future requests that need the same resource.

Preload is also different since it has a functional <code>onload</code> event (which, at least in Chrome, wasn't working for the other two <code>rel</code> values).

On top of that, preload <strong>does not block the window's <code>onload</code> event</strong>, unless the resource is also requested by a resource that blocks that event.

Combining all these characteristics together enables a bunch of new capabilities that were not possible until now.

Let's go over them, shall we?

### Loading Of Late-Discovered Resources

The basic way you could use preload is to <strong>load late-discovered resources early</strong>. While most markup-based resources are discovered fairly early by the browser's <a href="https://calendar.perfplanet.com/2013/big-bad-preloader/">preloader</a>, not all resources are markup-based. Some of the resources are hidden in CSS and in JavaScript, and the browser cannot know that it is going to need them until it is already fairly late. So in many cases, these resources end up delaying the first render, the rendering of text, or loading of critical parts of the page.

Now you have the means to tell the browser, "Hey, browser! Here's a resource you're going to need later on, so start loading it now."

Doing so would look something like:

<pre><code class="language-markup">&lt;link rel="preload" href="late_discovered_thing.js" as="script"&gt;</code></pre>

The <code>as</code> attribute tells the browser what it will be downloading. Possible <code>as</code> values include:

*   `"script"`,
*   `"style"`,
*   `"image"`,
*   `"media"`,
*   and `"document"`.

(See the <a href="https://fetch.spec.whatwg.org/#concept-request-destination">fetch spec</a> for the full list.)

Omitting the <code>as</code> attribute, or having an invalid value is equivalent to an XHR request, where the browser doesn't know what it is fetching, and fetches it with a fairly low priority.</p>

### Early Loading Of Fonts

One popular incarnation of the "late-discovered critical resources" pattern is web fonts. On the one hand, in most cases they are critical for rendering text on the page (unless you're using the shiny <a href="https://tabatkins.github.io/specs/css-font-display/">font-display CSS values</a>). On the other hand, they are buried deep in CSS, and even if the browser's preloader parsed CSS, it cannot be sure they'd be needed until it also knows that the selectors that require them actually apply to some of the DOM's nodes. While in theory, browsers could figure that out, none of them do, and if they would it could result in spurious downloads if the font rules get overridden further down the line, once more CSS rules come in.

In short, it's complicated.

But, you could get away from all that complexity by <strong>including preload directives for fonts</strong> you know are going to be needed. Something like:

<pre><code class="language-markup">&lt;link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin&gt;</code></pre>

One point worth going over: You <a href="https://github.com/w3c/preload/issues/32">have to add a <code>crossorigin</code> attribute</a> when fetching fonts, as they are <a href="https://drafts.csswg.org/css-fonts/#font-fetching-requirements">fetched using anonymous mode CORS</a>. Yes, even if your fonts are on the same origin as the page. Sorry.

Also, the <code>type</code> attribute is there to make sure that this resource will only get preloaded on browsers that support that file type. Right now, only Chrome supports preload, and it does support WOFF2 as well, but more browsers may support preload in the future, and we cannot assume they'd also support WOFF2. The same is true for any resource type you're preloading and which browser support isn't ubiquitous.</p>

### Dynamic Loading Without Execution

Another interesting scenario that suddenly becomes possible is one where you want to <strong>download a resource because you know you'd need it</strong>, but you don't yet want to execute it. For example, think of a scenario where you want to execute a script at a particular point in the page's life, without having control over the script (so without the ability to add a <code>runNow()</code> function to it).

Today, you are very limited in the ways you can do that. If you only inject the script at the point you want it to run, the browser will have to then download the script before it can be executed, which can take a while. You could download the script using XHR beforehand, but the browser will refuse to reuse it, since the resource wasn't downloaded with the same type as the one that is now trying to use the resource.

So what can you do?

Before preload, not much. (In some cases you can <code>eval()</code> the contents of the script, but that's not always feasible nor without side effects.) But with preload you can!

<pre><code class="language-javascript">
var preload = document.createElement("link");
link.href = "myscript.js";
link.rel = "preload";
link.as = "script";
document.head.appendChild(link);
</code></pre>

You can run that earlier on in the page load process, way before the point you want the script to execute (but once you're fairly confident that the script loading will not interfere with other, more critical resources that need loading). Then when you want it to run, you simply inject a <code>script</code> tag and you're good.

<pre><code class="language-javascript">
var script = document.createElement("script");
script.src = "myscript.js";
document.body.appendChild(script);
</code></pre>

### Markup-Based Async Loader

Another cool hack is to use the <code>onload</code> handler in order to create some sort of a markup-based async loader. <a href="https://twitter.com/scottjehl">Scott Jehl</a> was the first to <a href="https://github.com/filamentgroup/loadCSS/issues/59">experiment</a> with that, as part of his loadCSS library. In short, you can do something like:

<pre><code class="language-markup">&lt;link rel="preload" as="style" href="async_style.css" onload="this.rel='stylesheet'"&gt;</code></pre>

and get async loaded styles in markup! Scott also has a nice <a href="https://filamentgroup.github.io/loadCSS/test/preload.html">demo</a> page for that feature.

The same can also work for async scripts.

We already have <code>&lt;script async&gt;</code> you say? Well, <code>&lt;script async&gt;</code> is great, but it blocks the window's onload event. In some cases, that's exactly what you want it to do, but in other cases less so.

Let's say you want to download an analytics script. You want it to download fairly quickly (to avoid losing visitors that the analytics script didn't catch), but you don't want it to delay any metrics that impact the user experience, and specifically, you don't want it to delay onload. (You can <a href="https://www.stevesouders.com/blog/2013/05/13/moving-beyond-window-onload/">claim that onload</a> is not the only metric that impacts users, and you would be right, but it's still nice to stop the spinning loading icon a bit sooner).

With preload, achieving that is easy:

<pre><code class="language-javascript">
&lt;link rel="preload" as="script" href="async_script.js"
onload="var script = document.createElement('script');
        script.src = this.href;
        document.body.appendChild(script);"&gt;
</code></pre>

(It's probably not a great idea to include long JS functions as <code>onload</code> attributes, so you may want to define that part as an inline function.)

### Responsive Loading

Since <strong>preload is a link</strong>, according to the spec it has a <code>media</code> attribute. (It's currently not supported in Chrome, but will be soon.) That attribute can enable conditional loading of resources.

What is that good for? Let's say your site's initial viewport has a large interactive map for the desktop/wide-viewport version of the site, but only displays a static map for the mobile/narrow-viewport version.

If you're being smart about it, you want to <strong>load only one of those resources rather than both</strong>. And the only way to do that would be by loading them dynamically, using JS. But by doing that, you're making those resources invisible to the preloader, and they may be loaded later than necessary, which can impact your users' visual experience, and <strong>negatively impact</strong> your <a href="https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index">SpeedIndex</a> score.

What can we do to make sure the browser is aware of those resources as early as possible?

You guessed it! Preload.

We can <strong>use preload to load them ahead of time</strong>, and we can use its <code>media</code> attribute so that <em>only</em> the required script will be preloaded:

<pre><code class="language-markup">&lt;link rel="preload" as="image" href="map.png" media="(max-width: 600px)"&gt;

&lt;link rel="preload" as="script" href="map.js" media="(min-width: 601px)"&gt;</code></pre>

## Headers

One more feature that comes along free with link tags is that they can be <a href="https://tools.ietf.org/html/rfc5988">represented as HTTP headers</a>. That means that for most markup examples I showed above, you can have an HTTP response header that does exactly the same thing. (The only exception is the <code>onload</code>-related example. You cannot define an onload handler as part of an HTTP header.)

Examples for such HTTP response headers may look like:

<pre><code class="language-markup">Link: &lt;thing_to_load.js&gt;;rel="preload";as="script"

Link: &lt;thing_to_load.woff2&gt;;rel="preload";as="font";crossorigin</code></pre>

HTTP headers can come in handy when the person doing the optimization is not the same person who's responsible for editing the markup. The prominent example is an <strong>external optimization engine</strong> that scans the content and optimizes it (full disclosure: <a href="https://www.akamai.com/us/en/resources/front-end-optimization-feo.jsp">I work on one</a>).

Other examples can include a separate performance team that wants to add such optimizations, or an optimization build process where avoiding HTML fiddling significantly reduces complexity.</p>

## Feature Detection

One last point: In some of our examples above, we're relying on the fact that preload is supported for basic functionality such as script or style loading. What happens in browsers where this is not true?

Everything breaks!

We don't want that. So as part of the preload effort, we also changed the DOM spec so that feature detection of supported <code>rel</code> keywords would be possible.

An <strong>example feature detection</strong> function could look something like:

<script src="https://gist.github.com/yoavweiss/b1f798bb2be4e671107b.js"></script>

That enables you to <strong>provide fallback loading mechanisms</strong> in cases where the lack of preload support would break your site. Handy!

## Doesn't HTTP/2 Push Cover Those Same Use Cases?

Not really. While there is some overlap between the features, for the most part, they complement each other.

HTTP/2 Push has the advantage of being able to <strong>push resources</strong> that the browser hasn't sent the request for yet. That means that Push can send down resources before the HTML even started to be sent to the browser. It can also be used to send resources down on an open HTTP/2 connection without requiring a response on which HTTP Link headers can be attached.

On the other hand, <strong>preload can be used to resolve use cases that HTTP/2 cannot</strong>. As we've seen, with preload the application is aware of the resource loading taking place, and can be notified once the resource was fully loaded. That's not something HTTP/2 Push was designed to do. Furthermore, HTTP/2 Push cannot be used for third-party resources, while preload can be used for them just as efficiently as it would be used on first-party resources.

Also, HTTP/2 Push <strong>cannot take the browser's cache and non-global cookie state into account</strong>. While the cache state might be resolved with the new <a href="https://tools.ietf.org/html/draft-kazuho-h2-cache-digest-00">cache digest specification</a>, for non-global cookies there's nothing that can be done, so Push cannot be used for resources that rely on such cookies. For such resources, preload is your friend.

Another point in preload's favor is that it can perform content negotiation, while HTTP/2 Push cannot. That means that if you want to use <a href="https://www.smashingmagazine.com/2016/01/leaner-responsive-images-client-hints/">Client-Hints</a> to figure out the right image to send to the browser, or <code>Accept:</code> headers in order to figure out the best format, HTTP/2 Push cannot help you.</p>

## So…

I hope you're now convinced that preload opens up a new set of loading capabilities that weren't feasible before, and you're excited about using it.

What I ask of you is to go pick up Chrome Canary, play around with preload, break it into pieces and come whining back to <a href="https://twitter.com/yoavweiss">me</a>. It's a new feature, and like any new feature, it <strong>may contain bugs</strong>. Please help me find them and fix them as early as possible.

{{< signature "og" >}}


---
title: Understanding The Vary Header
slug: understanding-vary-header
author: andrewbetts
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2b79471-e256-4c31-9078-85d6880d26f7/content-negog-800w-opt.png
date: 2017-11-02T20:35:41.000Z
description: >-
  The Vary HTTP header is sent in billions of HTTP responses every day. But its
  use has never fulfilled its original vision, and many developers misunderstand
  what it does or don't even realize that their web server is sending it. With
  the coming of the Client Hints, Variants and Key specifications, varied
  responses are getting a fresh start.
categories:
  - Headers
  - Caching
---
The [Vary HTTP header](https://httpwg.org/specs/rfc7234.html#caching.negotiated.responses) is sent in billions of HTTP responses every day. But its use has never fulfilled its original vision, and many developers misunderstand what it does or don't even realize that their web server is sending it. With the coming of the [Client Hints](https://httpwg.org/http-extensions/client-hints.html), [Variants](https://mnot.github.io/I-D/variants/) and [Key](https://httpwg.org/http-extensions/key.html) specifications, varied responses are getting a fresh start.</p>

## What's Vary?

The story of Vary starts with a beautiful idea of how the web should work. In principle, a URL represents not a web page, but a conceptual resource, like your bank statement. Imagine that you want to see your bank statement: You go to `bank.com` and send a `GET` request for `/statement`. So far so good, but you didn't say what format you want the statement in. This is why your browser will also include something like `Accept: text/html` in your request. In theory, at least, this means you could say `Accept: text/csv` instead and get the same resource in a different format.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c28512f-db28-4b0c-825e-71b668bf4796/content-negog-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2b79471-e256-4c31-9078-85d6880d26f7/content-negog-800w-opt.png" width="800" height="252" alt="Illustration of content-negotiated conversation between user and bank" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c28512f-db28-4b0c-825e-71b668bf4796/content-negog-large-opt.png">View large version</a>)
</figcaption></figure>

Because the same URL now produces different responses based on the value of the `Accept` header, any cache that stores this response needs to know that that header is important. The server tells us that the `Accept` header is important like this:

<pre><code class='language-http'>Vary: Accept</code></pre>

You could read this as, “This response varies based on the value of the `Accept` header of your request.”

This basically **doesn't work** on today's web. So-called “[content negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation)” was a great idea, but it failed. This doesn't mean that `Vary` is useless, though. A decent portion of the pages you visit on the web carry a `Vary` header in the response — maybe your websites have them, too, and you don't know it. So, if the header doesn't work for content negotiation, why is it still so popular, and how do browsers deal with it? Let's take a look.

I've previously written about [Vary in relation to content delivery networks](https://www.fastly.com/blog/getting-most-out-vary-fastly) (CDNs), those intermediary caches (such as Fastly, CloudFront and Akamai) that you can put between your servers and the user. Browsers also need to understand and respond to Vary rules, and the way they do this is different from the way Vary is treated by CDNs. In this post, I'll explore the murky world of cache variation in the browser.

{{% feature-panel %}}

## Today's Use Cases For Varying In The Browser

As we saw earlier, the traditional use of Vary is to perform [content negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) using the `Accept`, `Accept-Language` and `Accept-Encoding` headers, and, historically, the first two of these have [failed miserably](https://wiki.whatwg.org/wiki/Why_not_conneg). Varying on `Accept-Encoding` to deliver Gzip- or Brotli-compressed responses, where supported, mostly works reasonably well, but all browsers support Gzip these days, so that isn't very exciting.

How about some of these scenarios?

* We want to serve images that are the exact width of the user's screen. If the user resizes their browser, we would download new images (varying on Client Hints).
* If the user logs out, we want to avoid using any pages that were cached while they were logged in (using a cookie as a `Key`).
* Users of browsers that support the WebP image format should get WebP images; otherwise, they should get JPEGs.
* When using a browser on a high-density screen, the user should get 2x images. If they move the browser window onto a standard-density screen and refresh, they should get 1x images.</p>

## Caches All The Way Down

Unlike edge caches, which act as one gigantic cache shared by all users, the browser is just for one user, but it has a lot of different caches for distinct, specific uses:

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ed14a08-3ddc-46a7-9ecd-547b8d2f58a5/browser-caches-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f8efba2-61d2-42e5-89ce-e642c0a8e601/browser-caches-800w-opt.png" width="800" height="264" alt="Illustration of caches in the browser" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ed14a08-3ddc-46a7-9ecd-547b8d2f58a5/browser-caches-large-opt.png">View large version</a>)
</figcaption></figure>

Some of these are quite new, and understanding exactly which cache the content is being loaded from is a complex calculation that is not well supported by developer tools. Here's what these caches do:

* **image cache**\
  This is a page-scoped cache that stores decoded image data, so that, for example, if you include the same image on a page multiple times, the browser only needs to download and decode it once.
* **[preload](https://w3c.github.io/preload) cache**\
  This is also page-scoped and stores anything that has been preloaded in a `Link` header or a `<link rel="preload">` tag, even if the resource is ordinarily uncacheable. Like the image cache, the preload cache is destroyed when the user navigates away from the page.
* **service worker [cache API](https://w3c.github.io/ServiceWorker/#cache)**\
  This provides a cache back end with a programmable interface; so, nothing is stored here unless you specifically put it there via JavaScript code in a service worker. It will also only be checked if you explicitly do so in a service worker `fetch` handler. The service worker cache is origin-scoped, and, while not guaranteed to be persistent, it's more persistent than the browser's HTTP cache.
* **[HTTP cache](https://httpwg.org/specs/rfc7234.html)**\
  This is the main cache that people are most familiar with. It is the only cache that pays attention to HTTP-level cache headers such as `Cache-Control`, and it combines these with the browser's own heuristic rules to determine whether to cache something and for how long. It has the broadest scope, being shared by all websites; so, if two unrelated websites load the same asset (for example, Google Analytics), they might share the same cache hit.
* **[HTTP/2 push cache](https://httpwg.org/specs/rfc7540.html#rfc.section.10.4)** (or “H2 push cache”)\
  This sits with the connection, and it stores objects that have been pushed from the server but have not yet been requested by any page that is using the connection. It is scoped to pages using a particular connection, which is essentially the same as being scoped to a single origin, but it is also destroyed when the connection closes.

Of these, the HTTP cache and service worker cache are best defined. As for the image and preload caches, some browsers might implement them as a single “memory cache” tied to the render of a particular navigation, but the mental model I'm describing here is still the right way to think about the process. See the [specification note](https://w3c.github.io/preload/#h-note3) on `preload` if you're interested. In the case of the H2 server push, [discussion over the fate of this cache](https://github.com/whatwg/fetch/issues/354) remains active.

The order in which a request checks these caches before venturing out onto the network is important, because requesting something might pull it from an outer layer of caching into an inner one. For example, if your HTTP/2 server pushes a style sheet along with a page that needs it, and that page also preloads the style sheet with a `<link rel="preload">` tag, then the style sheet will end up touching three caches in the browser. First, it will sit in the H2 push cache, waiting to be requested. When the browser is rendering the page and gets to the `preload` tag, it will pull the style sheet out of the push cache, through the HTTP cache (which might store it, depending on the style sheet's `Cache-Control` header), and will save it in the preload cache.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6e780ea-30dc-4582-989b-ea1e1388a607/push-preload-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c46adf73-84e4-4d4e-8e58-3ad954f45f78/push-preload-800w-opt.png" width="800" height="333" alt="HTTP/2 PUSH flow through browser caches" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6e780ea-30dc-4582-989b-ea1e1388a607/push-preload-large-opt.png">View large version</a>)
</figcaption></figure>

## Introducing Vary As A Validator

OK, so what happens when we take this situation and add Vary to the mix?

Unlike intermediary caches (such as CDNs), browsers typically **do not implement the capability to store multiple variations per URL**. The rationale for this is that the things we typically use `Vary` for (mainly `Accept-Encoding` and `Accept-Language`) do not change frequently within the context of a single user. `Accept-Encoding` might (but probably doesn't) change upon a browser upgrade, and `Accept-Language` would most likely only change if you edit your operating system’s language locale settings. It also happens to be a lot easier to implement Vary in this way, although some specification authors believe this was a mistake.

It's no great loss most of the time for a browser to store only one variation, but it is important that we don't accidentally use a variation that isn't valid anymore if the “varied on” data does happen to change.

The compromise is to treat `Vary` as a [validator](https://httpwg.org/specs/rfc7234.html#validation.model), not a key. Browsers compute cache keys in the normal way (essentially, using the URL), and then if they score a hit, they check that the request satisfies any Vary rules that are baked into the cached response. If it doesn't, then the browser treats the request as a miss on the cache, and it moves on to the next layer of cache or out to the network. When a fresh response is received, it will then overwrite the cached version, even though it's technically a different variation.</p>

## Demonstrating Vary Behavior

To demonstrate the way `Vary` is handled, I’ve made a [little test suite](https://vary-test.fastlydemo.net). The test loads a range of different URLs, varying on different headers, and detects whether the request has hit the cache or not. I was originally using [ResourceTiming](https://developer.mozilla.org/en-US/docs/Web/API/Resource_Timing_API/Using_the_Resource_Timing_API) for this, but for greater compatibility, I ended up switching to just measuring how long the request takes to complete (and intentionally added a 1-second delay to server-side responses to make the difference really clear).

Let's look at each of the cache types and how `Vary` should work and whether it actually works like that. For each test, I show here whether we should expect to see a result from the cache (“HIT” versus “MISS”) and what actually happened.</p>

### Preload

Preload is currently supported only in Chrome, where preloaded responses are stored in a memory cache until they are needed by the page. The responses also populate the HTTP cache on their way to the preload cache, if they are HTTP-cacheable. Because specifying request headers with a preload is impossible, and the preload cache lasts only as long as the page, testing this is hard, but we can at least see that objects with a `Vary` header do get preloaded successfully:

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c2ae80b-a7a7-4f0f-8972-ca1ce9dc191b/image4-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8618b0f3-674d-4273-8fbf-cfb5f0d10370/image4-800w-opt.png" width="800" height="363" alt="Test results for link rel=preload in Google Chrome" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c2ae80b-a7a7-4f0f-8972-ca1ce9dc191b/image4-large-opt.png">View large version</a>)
</figcaption></figure>

### Service Worker Cache API

Chrome and Firefox support service workers, and in developing the service worker specification, the authors wanted to fix what they saw as broken implementations in browsers, to make `Vary` in the browser work more like CDNs. This means that while the browser should store only one variation in the HTTP cache, it is supposed to hold onto multiple variations in the Cache API. Firefox (54) does this correctly, whereas Chrome uses the same vary-as-validator logic that it uses for the HTTP cache (the [bug is being tracked](https://bugs.chromium.org/p/chromium/issues/detail?id%3D756796)).</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a1ebb5d-ad45-46ea-b5a5-5d31d577dbdb/image1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37bb9fc8-a45e-4389-8869-278cbdcd69da/image1-800w-opt.png" width="800" height="396" alt="Test results for service worker cache in Google Chrome" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a1ebb5d-ad45-46ea-b5a5-5d31d577dbdb/image1-large-opt.png">View large version</a>)
</figcaption></figure>

### HTTP Cache

The main HTTP cache should observe `Vary` and does so consistently (as a validator) in all browsers. For much, much more on this, see [Mark Nottingham](https://www.mnot.net)’s post “[State of Browser Caching, Revisited](https://www.mnot.net/blog/2017/03/16/browser-caching).”

### HTTP/2 Push Cache

`Vary` should be observed, but in practice no browser actually respects it, and browsers will happily match and consume pushed responses with requests that carry random values in headers that the responses are varying on.</p>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b151572-5fa7-4062-b954-0208ec860b91/image3-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1feac389-cf9a-4ae3-b569-6a580c25bb49/image3-800w-opt.png" width="800" height="188" alt="Test results for H2 push cache in Google Chrome" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b151572-5fa7-4062-b954-0208ec860b91/image3-large-opt.png">View large version</a>)
</figcaption></figure>

## The “304 (Not Modified)” Wrinkle

The HTTP “304 (Not Modified)” response status is fascinating. Our “dear leader,” [Artur Bergman](https://twitter.com/crucially), pointed out to me this gem in the [HTTP caching specification](https://httpwg.org/specs/rfc7232.html#status.304) (emphasis mine):

<blockquote>
<p>The server generating a 304 response <strong>must</strong> generate any of the following header fields that would have been sent in a 200 (OK) response to the same request: <code>Cache-Control</code>, <code>Content-Location</code>, <code>Date</code>, <code>ETag</code>, <code>Expires</code>, and <code>Vary</code>.</p>
</blockquote>

Why would a `304` response return a `Vary` header? The plot thickens when you read about what you're supposed to do upon receiving a `304` response that contains those headers:

<blockquote>
<p>If a stored response is selected for update, the cache <strong>must</strong> \[…] use other header fields provided in the 304 (Not Modified) response to replace all instances of the corresponding header fields in the stored response.</p>
</blockquote>

Wait, what? So, if the `304`’s `Vary` header is different from the one in the existing cached object, we're supposed to update the cached object? But that might mean it no longer matches the request we made!

In that scenario, at first glance, the `304` seems to be telling you simultaneously that you can and cannot use the cached version. Of course, if the server really didn't want you to use the cached version, it would have sent a `200`, not a `304`; so, the cached version should definitely be used — but after applying the updates to it, it might not be used again for a future request identical to the one that actually populated the cache in the first place.

(Side note: At Fastly, we do not respect this quirk of the specification. So, if we receive a `304` from your origin server, we will continue to use the cached object unmodified, other than resetting the TTL.)

Browsers [do seem to respect this](https://vary-test.fastlydemo.net/#304-nomatch), but with a quirk. They update not just the response headers but the request headers that pair with them, in order to guarantee that, post-update, the cached response is a match for the current request. This seems to make sense. The specification doesn't mention this, so the browser vendors are free to do what they like; luckily, all browsers exhibit this same behavior.</p>

## Client Hints

Google's [Client Hints](https://httpwg.org/http-extensions/client-hints.html) feature is one of the most significant new things to happen to Vary in the browser in a long time. Unlike `Accept-Encoding` and `Accept-Language`, Client Hints describe values that might well change regularly as a user moves around your website, specifically the following:

* `DPR`\
  Device pixel ratio, the pixel density of the screen (might vary if the user has multiple screens)
* `Save-Data`\
  Whether the user has enabled data-saving mode
* `Viewport-Width`\
  Pixel width of the current viewport
* `Width`\
  Desired resource width in physical pixels

Not only might these values change for a single user, but the range of values for the width-related ones is large. So, we can totally use `Vary` with these headers, but we risk reducing our cache efficiency or even rendering caching ineffective.</p>

## The Key Header Proposal

Client Hints and other highly granular headers lend themselves to a proposal that [Mark](https://www.mnot.net) has been working on, named [Key](https://httpwg.org/http-extensions/key.html). Let's look at a couple of examples:

<pre><code class='language-http'>Key: Viewport-Width;div=50</code></pre>

This says that the response varies based on the value of the `Viewport-Width` request header, but rounded down to the nearest multiple of 50 pixels!

<pre><code class='language-http'>Key: cookie;param=sessionAuth;param=flags</code></pre>

Adding this header into a response means that we're varying on two specific cookies: `sessionAuth` and `flags`. If they haven't changed, we can reuse this response for a future request.

So, the main differences between `Key` and `Vary` are:

* `Key` allows varying on **subfields** within headers, which suddenly makes it feasible to vary on cookies, because you can vary on just one cookie — this would be huge;
* individual values can be **bucketed into ranges**, to increase the chance of a cache hit, particularly useful for varying on things such as viewport width.
* all variations with the same URL must have the same key. So, if a cache receives a new response for a URL for which it already has some existing variants, and the new response's `Key` header value doesn't match the values on those existing variants, then all the variants must be evicted from the cache.

At time of writing, no browser or CDN supports `Key`, although in some CDNs you might be able to get the same effect by splitting incoming headers into multiple private headers and varying on those (see our post, “[Getting the Most Out of Vary With Fastly](https://www.fastly.com/blog/getting-most-out-vary-fastly)”), so browsers are the main area where `Key` can make an impact.

The requirement for all variations to have the same key recipe is somewhat limiting, and I'd like to see some kind of [“early exit” option in the specification](https://github.com/httpwg/http-extensions/issues/232). This would enable you to do things like, “Vary on authentication state, and if logged in, also vary on preferences.”

## The Variants Proposal

`Key` is a nice generic mechanism, but some headers have more complex rules for their values, and understanding those values’ semantics can help us to find automated ways of reducing cache variation. For example, imagine that two requests come in with different `Accept-Language` values, `en-gb` and `en-us`, but although your website does have support for language variation, you only have one “English.” If we answer the request for US English and that response is cached on a CDN, then it can't be reused for the UK English request, because the `Accept-Language` value would be different and the cache isn't smart enough to know better.

Enter, with considerable fanfare, the [Variants](https://mnot.github.io/I-D/variants/) proposal. This would enable servers to describe which variants they support, allowing caches to make smarter decisions about which variations are actually distinct and which are effectively the same.

Right now, Variants is a very early draft, and because it is designed to help with `Accept-Encoding` and `Accept-Language`, its usefulness is rather limited to shared caches, such as CDNs, rather than browser caches. But it nicely pairs up with `Key` and completes the picture for better control of cache variation.</p>

## Conclusion

There's a lot to take in here, and while it can be interesting to understand how the browser works under the hood, there are also some simple things you can distil from it:

* Most browsers treat `Vary` as a validator. If you want multiple separate variations to be cached, find a way to use different URLs instead.
* Browsers ignore `Vary` for resources pushed using HTTP/2 server push, so don't vary on anything you push.
* Browsers have a ton of caches, and they work in different ways. It's worth trying to understand how your caching decisions impact performance in each one, especially in the context of `Vary`.
* `Vary` is not as useful as it could be, and `Key` paired with Client Hints is starting to change that. Follow along with [browser support](https://caniuse.com/client-hints-dpr-width-viewport) to find out when you can start using them.

Go forth and be variable.

{{< signature "al" >}}


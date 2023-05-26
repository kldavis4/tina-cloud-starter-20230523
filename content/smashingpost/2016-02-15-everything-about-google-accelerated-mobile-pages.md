---
title: Everything You Need To Know About Google's Accelerated Mobile Pages
slug: everything-about-google-accelerated-mobile-pages
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c07e3b4e-9643-48c5-a87b-93db31856459/google-amp-opt.png'
date: 2016-02-15T19:12:18.000Z
author: christiancantrell
description: >-
  In May of 2015, Facebook unveiled its new in-app publishing platform, [Instant
  Articles](https://instantarticles.fb.com/). A month later, Apple declared that
  the old [Newsstand](https://en.wikipedia.org/wiki/Newsstand_(application))
  experience (essentially a fancy folder full of news apps) would be replaced in
  iOS 9 with a brand new news-aggregation and discovery platform called [Apple
  News](https://www.apple.com/news/).

  Four months later, it was Google’s turn to announce its own, somewhat belated
  but no less ambitious, plan to revolutionize mobile news consumption with an
  open-source web-based solution called [Accelerated Mobile
  Pages](https://www.ampproject.org/), or AMP. In just a few months, we’ve seen
  the relative tranquility of mobile digital publishing erupt into yet another
  full-scale platform war as Facebook, Apple, and now Google compete for both
  the loyalty of publishers and the attention of readers.
categories:
  - Mobile
  - Performance
  - AMP
---
In May of 2015, Facebook unveiled its new in-app publishing platform, <a href="https://instantarticles.fb.com/">Instant Articles</a>. A month later, Apple declared that the old <a href="https://en.wikipedia.org/wiki/Newsstand_(application)">Newsstand</a> experience (essentially a fancy folder full of news apps) would be replaced in iOS 9 with a brand new news-aggregation and discovery platform called <a href="https://www.apple.com/news/">Apple News</a>.</p>

## <span class="rh">Further reading</span> on Smashing:

*   [Perceived Performance](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/)
*   [Preload: What is it good for?](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/)
*   [Getting Ready For HTTP/2](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [Progressive Enhancement](https://www.smashingmagazine.com/2015/12/reimagining-single-page-applications-progressive-enhancement/)
*   [Progressive Web AMPs](https://www.smashingmagazine.com/2016/12/progressive-web-amps/)

Four months later, it was Google’s turn to announce its own, somewhat belated but no less ambitious, plan to revolutionize mobile news consumption with an open-source web-based solution called <a href="https://www.ampproject.org/">Accelerated Mobile Pages</a>, or AMP. In just a few months, we’ve seen the relative tranquility of mobile digital publishing erupt into yet another full-scale platform war as Facebook, Apple, and now Google compete for both the loyalty of publishers and the attention of readers.

While Facebook and Apple have a significant head start on Google, there’s every reason to believe that AMP will catch up quickly (and could even surpass one or both of its competitors). If you’re a developer or a publisher who needs to get up to speed on the why, what and how of Google’s Accelerated Mobile Pages as fast and efficiently as possible, you’re in the right place.

{{% feature-panel %}}

## But What’s The Problem?

Before we discuss solutions, it’s worth taking a moment to explore the problem. If you do a lot of reading on mobile devices, chances are pretty good that you are already all too aware that interacting with web-based content on a phone or tablet ranges from barely acceptable to horrendous. Pages often load slowly, render erratically and behave unpredictably for two primary reasons:

*   **third-party interference**.  Ads and related tracking techniques not only add bulk and additional requests to an already bandwidth- and CPU-constrained device, but pages often behave as though they’re possessed as they convulse around multiple `document.write()` calls. The New York Times [recently did a test](https://www.nytimes.com/2015/10/01/technology/personaltech/ad-blockers-mobile-iphone-browsers.html) that showed significant decreases in page sizes and increases in battery life after installation of an [iOS content blocker](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewInSafari/Introduction/Introduction.html).
*   **collateral damage from responsive design**.  While most responsively designed websites look fine on screens of all sizes, they often contain a lot of the baggage of desktop websites when viewed on mobile. When [Paul Irish](https://twitter.com/paul_irish) did a performance audit of Reddit, he discovered that a great deal of the overhead could be [traced back to an asset called SnooIcon](https://www.youtube.com/watch?v=X-qZu2Aoo98&feature=youtu.be&list=PLUj8-Hhrb-a1WhrhBff-_lT2EdHjHqSBy&t=1318), the Reddit mascot rendered in SVG so that it could be animated (by a third-party library, meaning more overhead) on mouseover — not a situation in which assets frequently find themselves on mobile devices.

Enter Facebook Instant Articles, Apple News, and Accelerated Mobile Pages — our saviors from a world where, <a href="https://s0.wp.com/wp-content/themes/vip/facebook-instantarticles/library/docs/FB_IA_FAQS.pdf">according to Facebook</a> (PDF, 3.4 MB), the average loading time of an article on mobile devices is 8 seconds. While calling 8 seconds an eternity is obviously hyperbole, given that you could be well into your second Vine video in that amount of time, it’s probably fair to say that, by today’s standards, it’s at least an eon.</p>

<figure class="aspect-ratio"><iframe loading="lazy" src="https://www.youtube.com/embed/4fecieoA9U0" frameborder="0" allowfullscreen></iframe></figure>

A short demo of Facebook Instant Articles, Apple News and Accelerated Mobile Pages. Note that Facebook Instant Articles and Apple News are in-app experiences, whereas AMP is entirely browser-based.</p>

## How Is AMP Different?

Some context for how AMP is different from Facebook Instant Articles and Apple News will make clearer some of the decisions Google made for its new digital publishing initiative.

Facebook Instant Articles and Apple News have several characteristics in common:

*   **in-app experiences**.  Readers access Facebook Instant Articles through Facebook on mobile devices, and Apple News is a standalone app that comes with iOS 9\. Neither platform currently allows users to view articles in their specific formats outside of the respective app. Think of both as an application-specific refresh of [RSS](https://en.wikipedia.org/wiki/RSS).
*   **syndication-driven**.  While Facebook Instant Articles and Apple News use very different syndication formats ([Apple News Format](https://developer.apple.com/library/ios/documentation/General/Conceptual/Apple_News_Format_Ref/index.html) is JSON-based, and [Instant Article Markup](https://developers.facebook.com/docs/instant-articles/guides/articlecreate) is more or less HTML wrapped in an RSS feed), they are based on similar principles: Coax your CMS into generating the necessary syndication formats, and Facebook or Apple News will slurp it up, parse it and make it both beautiful and fast through customized and optimized renderers.
*   **experience-oriented**.  Although Facebook Instant Articles and Apple News are both focused on performance, they are equally concerned with making articles look and feel modern. Both platforms have components that allow for the slick and smooth interactions we typically associate with bespoke, hand-built reading experiences.

In contrast, Accelerated Mobile Pages have a distinct focus:

*   **web-based experience**.  AMP documents are designed to be rendered either in the browser or in [WebViews](https://developer.android.com/reference/android/webkit/WebView.html).
*   **atomic documents**.  Although AMP documents are validated, parsed and partially rendered by the AMP runtime (plenty more on that below), they are complete and independent documents that live on your own web server (and, optionally, in a CDN cache), rather than collections of metadata that will at some point be transformed into articles and rendered in apps.
*   **performance-oriented**.  AMP cares far more about the performance of AMP documents than about aesthetics or interaction patterns. That’s not to say AMP documents are inherently homely (they can be just as attractive as Facebook Instant Articles or Apple News articles with the right styling), but the runtime is far more concerned with making an article render quickly than with providing fancy visual effects like [crazy little jiggly things](https://youtu.be/sfrnNBG28DE?t=126).</p>

## What Is AMP Exactly?

Enough philosophizing and high-level handwaving. Let’s get into specifics. While getting your head around Facebook Instant Articles and Apple News is pretty easy (they’re essentially fancy news aggregators with custom renderers built on top of proprietary syndication formats), AMP is the outlier. It’s a little more difficult to grasp, for two reasons:

*   **There isn’t a simple model to compare it to.** When RSS was new, we all marveled at its power, wrote countless articles and blog posts about its disruptive potential, [declared the home page dead](https://www.google.com/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=%22the%20homepage%20is%20dead%22) (yet again), and then proceeded to forget all about it. Facebook Instant Articles and Apple News are essentially an RSS reboot, except that they dispense with all of the inconveniences of standards, and each happens to work in only one application.
*   **AMP is not a client.**.  While Facebook Instant Articles, Apple News and AMP have several elements in common, such as proprietary syndication formats and custom renderers, AMP is the only one without a dedicated client (other than the browser). More so than its brethren, AMP is a set of specifications, conventions, and technologies that can be combined into a solution, rather than being an end-to-end (publisher-to-reader) solution in and of itself.

Now that we know to think of AMP as a collection of ingredients, rather than a fully baked cake, let’s look at what those individual components are:

*   AMP HTML,
*   the AMP runtime,
*   the AMP cache.</p>

## AMP HTML

AMP documents are written in HTML, but not just any HTML. Some tags are banned, while a few new tags are introduced (partially to replace the banned ones and partially to encapsulate interactive functionality). You can think of AMP HTML as what HTML would look like had it been designed with nothing but mobile performance in mind (as opposed to being introduced a full 14 years before the introduction of the iPhone).

Because AMP HTML is designed for optimal performance, to understand and appreciate its value, we need to understand the problems it solves. Here are the three biggest things that impair the loading and rendering of web pages on mobile devices:

*   **payload size**.  Responsive web design has served us well because it allows us to build a single website for every device and screen out there. But that also sometimes means delivering desktop-size payloads (HTML, JavaScript, CSS and assets) to extremely bandwidth- and CPU-constrained mobile devices. (Those who think of their phones as little desktop computers are giving mobile hardware far too much credit. Your iPhone 6s has 2 GB of RAM, while your laptop probably has 8 or 16.)
*   **resource loading**.  Resources are not always loaded in the optimal order, which means bandwidth, CPU and RAM are often dedicated to assets that users might never even see. Additionally, resources frequently don’t declare their widths and heights (especially when served through ad networks or injected via `document.write()` calls), which not only causes the page to resize itself as resource dimensions are lazily determined, but also triggers unnecessary and expensive layout recalculations. That’s what causes web pages to leap around like laser-chasing kittens as they ever-so-sluggishly manifest.
*   **JavaScript execution**.  I’m not about to broach the topic of JavaScript performance here, but modern websites often pile it on by the megabyte, and while it might execute without any discernable latency on desktop computers, mobile is still a very different environment, where, I think we can all agree, JavaScript is best kept to a minimum.

Given these three barriers to fluid web experiences on mobile devices, AMP HTML primarily exists for three purposes:

*   **encourage brevity**.  AMP documents are not responsive versions of desktop websites. While AMP documents can be (and usually are) responsive, they are responsive in a mobile context. In other words, rather than one page working absolutely everywhere (desktop and mobile), AMP documents are designed specifically to work well across mobile devices.
*   **control external resource loading**.  The AMP runtime controls the loading of external resources to ensure that the process is highly efficient, resulting in content that appears on users’ screens as quickly and intelligently as possible.
*   **encapsulate interactive functionality**.  Although AMP documents tend to get right down to the business of presenting readers with straightforward reading experiences, that doesn’t mean they can’t be modern and interactive. The AMP runtime provides encapsulated functionality through highly optimized JavaScript, so that developers don’t risk hindering performance by writing their own.</p>

## AMP HTML Tags

Below is a list of tags that are flat-out banned in AMP HTML:

*   `script` This is obviously a big one. I’ll provide more detail on AMP’s position on JavaScript below; for now, just assume that the only `script` tags you’ll have in your AMP documents are those loading the AMP runtime and, optionally, a tag for [JSON-based linked data](https://developers.google.com/schemas/formats/json-ld?hl=en).
*   `base` The `base` tag seems to be prohibited out of an abundance of caution, and it [might end up whitelisted](https://twitter.com/cramforce/status/663012156808425472) if the community complains. (My guess is that nobody really cares one way or the other.)
*   `frame` and `frameset` Not exactly a good use of mobile real estate anyway, so good riddance.
*   `object`, `param`, `applet` and `embed` Sadly, your AMP documents won’t be containing any Flash or Java applets. (That was sarcasm, in case it wasn’t entirely obvious.)
*   `form` and `input` elements (with the exception of the `button` tag) Form support will likely eventually be implemented as encapsulated components because [they are of limited use](https://twitter.com/cramforce/status/663012874474811392) without scripting.

Now, here’s a list of tags that replace their HTML counterparts in order to optimize resource loading and enforce best security practices:

*   `[amp-img](https://www.ampproject.org/docs/reference/amp-img.html)` Replaces the `img` tag and optimizes resource loading by taking into account factors such as viewport position, system resources and connectivity.
*   `[amp-video](https://www.ampproject.org/docs/reference/amp-video.html)` Replaces the HTML5 `video` tag, so that video content can be lazily loaded (taking the viewport into consideration).
*   `[amp-audio](https://www.ampproject.org/docs/reference/extended/amp-audio.html)` Replaces the HTML5 `audio` tag so that audio content can be lazily loaded (taking the viewport into consideration).
*   `[amp-iframe](https://www.ampproject.org/docs/reference/extended/amp-iframe.html)` The `amp-iframe` tag enforces best security practices by doing things such as [sandboxing content](https://www.html5rocks.com/en/tutorials/security/sandboxed-iframes/) by default and placing restrictions on where iframes may appear to ensure that they do not dominate an AMP document.

Finally, here are all of the tags that AMP HTML introduces to add functionality or interactivity to your documents, without requiring you to write JavaScript:

*   `[amp-ad](https://www.ampproject.org/docs/reference/amp-ad.html)` The `amp-ad` tag allows the AMP runtime to manage the loading of ads just like all other externally loaded resources (currently, ads are loaded last), and it ensures that JavaScript from ad networks can’t execute inside the parent AMP document or trigger unnecessary layout calculations. (Goodbye, `document.write()`!)
*   `[amp-analytics](https://www.ampproject.org/docs/reference/extended/amp-analytics.html)` This miniature framework packages analytics data and sends it to third-party providers. As of today, [AMP support is coming](https://amphtml.wordpress.com/2015/12/09/continued-momentum-for-the-amp-project/) from Adobe Analytics, Chartbeat, ClickTale, comScore, Google Analytics, Nielsen and Parse.ly.
*   `[amp-pixel](https://www.ampproject.org/docs/reference/amp-pixel.html)` This is used for embedding [web beacons](https://en.wikipedia.org/wiki/Web_beacon), and it supports tokens for sending several client variables to the server.
*   `[amp-carousel](https://www.ampproject.org/docs/reference/extended/amp-carousel.html)` This optimized component displays child images in an interactive, horizontal orientation.
*   `[amp-lightbox](https://www.ampproject.org/docs/reference/extended/amp-lightbox.html)` This allows readers to open images in a full-screen “lightbox” view. It supports the specification of both thumbnail and full-sized images.
*   `[amp-anim](https://www.ampproject.org/docs/reference/extended/amp-anim.html)` This loads animated GIFs and provides much-needed placeholder functionality.
*   `[amp-font](https://www.ampproject.org/docs/reference/extended/amp-font.html)` Set a loading timeout on custom fonts, and specify fallback fonts should your custom fonts not load within the allotted time.
*   `[amp-fit-text](https://www.ampproject.org/docs/reference/extended/amp-fit-text.html)` Text within an `amp-fit-text` tag will automatically be assigned a font size optimized for the available space. Think of it as a little prepackaged responsiveness.
*   `[amp-list](https://www.ampproject.org/docs/reference/extended/amp-list.html)` With the `amp-list` tag, you can load dynamic, repeating JSON data and then render it using an HTML template. (See the `amp-mustache` tag below.)
*   `[amp-mustache](https://www.ampproject.org/docs/reference/extended/amp-mustache.html)` This supports the rendering of [Mustache HTML templates](https://mustache.github.io/).
*   `[amp-install-serviceworker](https://www.ampproject.org/docs/reference/extended/amp-install-serviceworker.html)` If you choose not to use an AMP cache (much more on caching below), the `amp-install-serviceworker` tag loads and installs a [service worker](https://www.html5rocks.com/en/tutorials/service-worker/introduction/) for the current page. Service workers are slick, but in my opinion [it’s a little too early](https://caniuse.com/#feat=serviceworkers) to rely on them.
*   `[amp-youtube](https://www.ampproject.org/docs/reference/extended/amp-youtube.html)` Predictably, this embeds the YouTube video with the specified video ID.
*   `[amp-twitter](https://www.ampproject.org/docs/reference/extended/amp-twitter.html)` Embed tweets (Twitter cards optional).
*   `[amp-instagram](https://www.ampproject.org/docs/reference/extended/amp-instagram.html)` Embed Instagram images.
*   `[amp-brightcove](https://www.ampproject.org/docs/reference/extended/amp-brightcove.html)` This component loads and displays videos (and a video player) from [Brightcove](https://www.brightcove.com).
*   `[amp-pinterest](https://www.ampproject.org/docs/reference/extended/amp-pinterest.html)` Embed a Pinterest widget, or “Pin It” button, in your AMP document.
*   `[amp-vine](https://www.ampproject.org/docs/reference/extended/amp-vine.html)` Embed the specified Vine video in your AMP document.

Note that, while <code>amp-</code> prefixed tags are not exactly standard HTML, they also aren’t proprietary. Rather, they are legitimate <a href="https://www.html5rocks.com/en/tutorials/webcomponents/customelements/">custom elements</a> with JavaScript implementations that do things like enforce best security practices and prioritize the loading of remote resources (more on that in the “AMP Runtime” section below). In other words, while AMP HTML might look suspiciously like the <a href="https://en.wikipedia.org/wiki/Embrace,_extend_and_extinguish">embrace, extend and extinguish</a> strategy, it’s really just a clever application of web standards and not all that much different from <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_data_attributes">custom <code>data-</code> attributes</a>.

## Styling AMP HTML

Styling AMP documents is done with standard CSS and is not much different from how you already style content. However, keep in mind several things:

*   All styling must be done with an inline style sheet — no externally linked style sheets and no element-level inline styles. (An externally linked style sheet would require an additional document to be downloaded before the layout could be calculated, and inline element-level styles could bloat the document.)
*   Styles are limited to 50 KB. Google’s philosophy is that 50 KB is enough for a nice document or article but not enough for a nice website.
*   Your inline style sheet must have the `amp-custom` attribute (i.e. `<style amp-custom>`).
*   The `@` rules — `@font-face` (more on fonts below), `@keyframes` and `@media` — are allowed.
*   Some selectors have limitations that are known to challenge performance, such as the universal (`*`) selector and the `:not()` selector.
*   The `!important` qualifier is banned to ensure that the AMP runtime has the last word on element sizing.
*   Styling of custom AMP components like `amp-carousel` is done by overriding default classes, like `.amp-carousel-button-prev`, or by using a predefined set of CSS custom properties, like `--arrow-color`.
*   All externally loaded resources must have width, height and layout properties specified (more on layout below) to minimize expensive DOM layout recalculations.
*   Transitions and animations that can be GPU-accelerated (and that don’t trigger recalculations) are allowed. Currently, `opacity` and `transform` are whitelisted.

For additional details on styling documents, see the <a href="https://www.ampproject.org/docs/reference/spec.html">AMP HTML specification</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9014805-0ee6-4652-901d-35e51b4b4f8c/01-nytimes-in-amp-opt.jpg"><img title="A New York Times article formatted as an AMP document" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7f3c47e-675e-4916-97c2-abcdbdfbff7d/01-nytimes-in-amp-small-opt.jpg" alt="A New York Times article formatted as an AMP document" /></a><figcaption>A New York Times article formatted as an AMP document. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9014805-0ee6-4652-901d-35e51b4b4f8c/01-nytimes-in-amp-opt.jpg">View large version</a>)</figcaption></figure>

### Fonts

AMP happily support custom fonts, with a few qualifications:

*   Fonts must be loaded with a link tag or a CSS `@font-face` rule. In other words, you can’t load fonts using JavaScript.
*   All fonts must be served over HTTPS.
*   Font providers must be whitelisted. Currently, the only whitelisted providers are `fonts.googleapis.com` and `fast.fonts.net`. But, given how quickly publishers, advertisers and analytics providers are adding support for AMP, I suspect more will follow soon.</p>

### Layout

AMP’s approach to layout was conceived around two main goals:

*   The runtime must be able to infer the size of all externally loaded resources before they are actually loaded, so that a final layout can be calculated as quickly as possible. Once the layout is calculated, the article can be rendered and readers can start interacting with it, even if the ads, images, audio and video haven’t completed loading yet. (And, as those resources load, they will render seamlessly, without disrupting the reading experience by updating the document’s layout.)
*   AMP articles should be responsive. As the name “Accelerated Mobile Pages” implies, AMP documents are specifically intended for mobile devices; so, in this context, “responsive” doesn’t include desktop resolutions. Rather, AMP documents should look good on all mobile devices, from those tiny old iPhone 4 relics people are still using all the way up to the relatively gargantuan iPad Pros.

The former goal is primarily achieved by the requirement that all externally loaded resources have <code>width</code> and <code>height</code> attributes (and it’s further enforced by limiting scripts, which ensures that new resources can’t be shoehorned in). The latter is achieved by standard media queries, the <code>media</code> attribute, the <code>sizes</code> attribute and the AMP-specific <code>layout</code> attribute.

The following is an overview of the layouts that AMP currently supports:

*   `nodisplay` The element isn’t initially displayed, but display can be triggered by a user action. (This is used in conjunction with components such as `amp-lightbox`.)
*   `fixed` The element has a fixed width and height, which means the runtime can’t apply any responsive behavior.
*   `responsive` In my opinion, this is the most useful and magical of AMP’s layout options. The element uses whatever space is allotted while maintaining its aspect ratio. (Basically, “Make this thing look good at any resolution, please and thank you.”)
*   `fixed-height` The element uses the space allotted but maintains a fixed height (scaling horizontally).
*   `fill` The element fills the container it’s in without regard to aspect ratio. (Think `width: 100%` and `height: 100%`.)
*   `container` The element is a container and, therefore, lets its children (as opposed to its parent) define its size, exactly like a standard `div` element.

Achieving a functional and straightforward document layout using AMP’s layout system is relatively easy, but when you consider everything it supports and how values apply to different types of elements, there is a fair amount of nuance. For a much more detailed breakdown, see the <a href="https://github.com/ampproject/amphtml/blob/master/spec/amp-html-layout.md">AMP layout specification</a>.</p>

### What About SVG?

Supported! Basic SVG <a href="https://caniuse.com/#feat=svg">enjoys comprehensive support</a> across both desktop and mobile browsers, and graphics don’t get much more responsive than vectors, so AMP and SVG make a very good team. The biggest limitation is that, due to scripting restrictions, you won’t be able to animate your vectors with JavaScript — which, if we’re being honest, you probably shouldn’t be doing on mobile anyway. However, if you really must breathe a little life into your SVG, you can still do so using CSS animations, according to the same constraints outlined in the styling section above. Remember that SVG is a part of the DOM, so it can be styled — and animated — as easily as any other element.</p>

## AMP’s Philosophy On JavaScript

Good news and bad news here. The bad news is that you won’t be writing any JavaScript for your AMP documents anytime soon. But in a way, that’s also the good news. Keep in mind that AMP is not a mobile <em>application</em> framework. Rather, it’s a mobile <em>article</em> framework, and because articles should be optimized for seamless and fluid reading experiences, there really aren’t a lot of good use cases for heavy client-side scripting.

That being said, banning all JavaScript forever is both unrealistic and a little draconian. The reality is that the web has been relying on JavaScript for some time now — even in the context of simple and relatively bland reading experiences — for things like advertising, analytics and interactive features. Additionally, one of the best things about the web is its openness and its seemingly infinite capacity for experimentation, expressivity and creativity — a great deal of which is powered by JavaScript.

Recognizing both the burden that arbitrary, user-written JavaScript places on performance guarantees, and the ubiquity and inevitability of JavaScript in a modern web environment, the AMP team has come up with the following scripting principles:

*   No user-written JavaScript is supported or allowed at this time. You may have only two types of script tags in your AMP documents: [linked data tags](https://developers.google.com/schemas/formats/json-ld?hl=en) (whose type is `application/ld+json`) and tags for including both the AMP runtime and extended AMP components.
*   The authors of the AMP project have anticipated most of the needs for JavaScript in the context of mobile article consumption, and so AMP either supports alternatives (`amp-pixel`, including custom fonts with link tags or `@font-face` rules, etc.) or provides implementations that are compatible with the AMP runtime and that, therefore, guarantee both security and performance (`amp-ad`, `amp-analytics`, `amp-carousel`, etc.).
*   If you really must use JavaScript for something like an interactive feature, you can [build the feature independently](https://twitter.com/cantrell/status/665172906117304320) and then include it with an `[amp-iframe](https://www.ampproject.org/docs/reference/extended/amp-iframe.html)` tag. Content included in an `amp-iframe` is even allowed limited communication with the parent document for things like resizing requests.
*   AMP components are open source ([Apache 2](https://github.com/ampproject/amphtml/blob/master/LICENSE)) and open to contributions, so new components will appear over time (in fact, several new components appeared over the course of writing and editing this article, so I’ve already updated a few times). While the AMP team will prioritize generalized components over service-specific functionality (a widget specifically for your social startup, for instance), it is also committed to providing enough diversity to accommodate the widest range of content possible.
*   Finally, all of these policies are subject to change. As browser features such as web workers, custom elements and the shadow DOM become more widely supported, options for supporting user-written JavaScript and custom components — while still guaranteeing security and performance — will expand dramatically.

For more information on the future of AMP components, see the “Extended Components” section of the “<a href="https://github.com/ampproject/amphtml/blob/master/spec/amp-html-components.md">AMP HTML Components</a>” specification.</p>

## Anatomy Of An AMP Document

Now that you have a pretty solid understanding of AMP HTML, let’s break down a boilerplate.

Of course, you’ll start your AMP documents with a <code>doctype</code> declaration:

<pre><code class="language-markup">&lt;!doctype html&gt;</code></pre>

Next, designate your HTML document as AMP HTML, which, believe it or not, you do using the high-voltage emoji as an attribute in the <code>html</code> tag:

<pre><code class="language-markup">&lt;html ⚡&gt;</code></pre>

Or, if you’re an old-fashioned curmudgeon and bristle at the idea of adorning your code with adorable emojis, you can use the far more conservative <code>amp</code> attribute, instead:

<pre><code class="language-markup">&lt;html amp&gt; &lt;!-- A good sign that you’re boring! --&gt;</code></pre>

In your <code>head</code> tag, don’t forget the <code>utf-8</code> character-encoding instructions:

<pre><code class="language-markup">&lt;meta charset="utf-8"&gt;</code></pre>

And link to the non-AMP version of your document (marked as <code>canonical</code>, so that it doesn’t appear as duplicate content):

<pre><code class="language-markup">&lt;link rel="canonical" href="my-non-amp-index.html"&gt;</code></pre>

Conversely, your non-AMP version should contain a reference to the AMPlified document:

<pre><code class="language-markup">&lt;link rel="amphtml" href="my-amp-index.html"&gt;</code></pre>

Because AMP pages are intended for mobile devices (and you also want <a href="https://www.chromium.org/developers/design-documents/chromium-graphics/how-to-get-gpu-rasterization">GPU rasterization</a>), be sure to include a meta <code>viewport</code> tag:

<pre><code class="language-markup">&lt;meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1"&gt;</code></pre>

The next line of code will seem a little strange, and that’s because it is. You know how you’ll sometimes see a web page briefly render text before the fonts have been loaded and applied, then flicker and render again looking the way the designer intended? The tag below keeps the opacity of the page at <code>0</code> (invisible) until it’s been properly styled.</p>

<pre><code class="language-markup">
&lt;style&gt;
body {
  opacity: 0
}
&lt;/style&gt;

&lt;noscript&gt;

&lt;style&gt;
body {
  opacity: 1
}
&lt;/style&gt;
&lt;/noscript&gt;
</code></pre>

The problem with this approach is that, should the AMP runtime fail to load, it’s technically possible for the page’s opacity never to go from <code>0</code> to <code>1</code>. To compensate for such contingencies, the code above will likely be changed to something closer to this:

<pre><code class="language-css">
&lt;style&gt;
body {
  animation: amp-timeout 0x 5s 1 normal forwards;
}

@keyframes amp-timeout {
  0% {opacity: 0;}
  100% {opacity: 1;}
}
&lt;/style&gt;</code></pre>

The next thing to do is include the AMP JavaScript runtime:

<pre><code class="language-markup">&lt;script async src="https://cdn.ampproject.org/v0.js"&gt;&lt;/script&gt;</code></pre>

And include the JavaScript implementations for whichever extended components you need:

<pre><code class="language-markup">
&lt;script async custom-element="amp-youtube" src="https://cdn.ampproject.org/v0/amp-youtube-0.1.js"&gt;&lt;/script&gt;
&lt;script async custom-element="amp-audio" src="https://cdn.ampproject.org/v0/amp-audio-0.1.js"&gt;&lt;/script&gt;
&lt;script async custom-element="amp-carousel" src="https://cdn.ampproject.org/v0/amp-carousel-0.1.js"&gt;&lt;/script&gt;
&lt;script async custom-element="amp-lightbox" src="https://cdn.ampproject.org/v0/amp-lightbox-0.1.js"&gt;&lt;/script&gt;
&lt;script async custom-element="amp-anim" src="https://cdn.ampproject.org/v0/amp-anim-0.1.js"&gt;&lt;/script&gt;
&lt;script async custom-element="amp-twitter" src="https://cdn.ampproject.org/v0/amp-twitter-0.1.js"&gt;&lt;/script&gt;
&lt;!-- etc. --&gt;</code></pre>

(Note the use of the <code>async</code> attribute. That’s not optional — the less blocking, the better.)

Optionally, you can sprinkle in a little <a href="https://developers.google.com/schemas/formats/json-ld?hl=en">linked data</a>, like this:

<pre><code class="language-javascript">
&lt;script type="application/ld+json"&gt;
{
  "@context": "https://schema.org",
  "@type": "NewsArticle",
  "headline": "Turn Your AMP up to 11!",
  "image": [ "img/cover-opt.jpg" ],
  "datePublished": "2015-01-11T08:00:00+08:00"
}
&lt;/script&gt;</code></pre>

Now let’s add a few fonts, using either <code>link</code> tags or <code>@font-face</code> rules in your CSS:

<pre><code class="language-markup">&lt;link href='https://fonts.googleapis.com/css?family=Roboto+Condensed:300,700' rel='stylesheet' type='text/css'&gt;
&lt;link href='https://fonts.googleapis.com/css?family=Lora:400,700,400italic,700italic' rel='stylesheet' type='text/css'&gt;</code></pre>

And then we’ll some styles (no more than 50 KB worth), with the required <code>amp-custom</code> attribute:

<pre><code class="language-markup">&lt;style amp-custom&gt;</code></pre>

You’re now ready to build a more or less standard HTML document using everything you’ve just learned about AMP HTML.</p>

## The AMP Runtime

I won’t spend all that much time on the AMP runtime because, like all runtimes, it’s a bit of a black box. That’s not to say that the AMP runtime is inaccessible (it’s <a href="https://github.com/ampproject/amphtml/blob/master/src/runtime.js">open source</a>, like the rest of the project). Rather, like all good runtimes, developers don’t need to know exactly how it works in order to take advantage of it, as long as they generally understand what it does.

The AMP runtime is implemented entirely in JavaScript and is initiated by including it in the AMP document, as you would any external JavaScript file:

<pre><code class="language-markup">&lt;script async src="https://cdn.ampproject.org/v0.js"&gt;&lt;/script&gt;</code></pre>

From there, the AMP runtime primarily does three things:

*   manages resource loading and prioritization,
*   implements AMP components,
*   optionally, includes a runtime validator for AMP HTML.

The validator is critical to authoring AMP-compliant documents. It can be turned on simply by appending <code>#development=1</code> to the document’s URL. Then, all you have to do is open your console to see your report card.

Errors look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44d51a9f-0ac3-43b0-ba97-d0e0f2a0a5aa/02-amp-console-errors-opt.png"><img title="AMP validation errors in the console" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1a65e57-6424-4d12-935c-8a9a7c02816b/02-amp-console-errors-small-opt.png" alt="AMP validation errors in the console" /></a><figcaption>AMP validation errors in the console. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44d51a9f-0ac3-43b0-ba97-d0e0f2a0a5aa/02-amp-console-errors-opt.png">View large version</a>)</figcaption></figure>

A nice, clean, compliant AMP document looks something like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/586c079c-b26b-4ce4-9727-4f1cac5c5efb/03-amp-console-clean-opt.png"><img title="An AMP document that passes validation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68327933-3496-4a11-9215-e4cf5f25a15e/03-amp-console-clean-small-opt.png" alt="An AMP document that passes validation" /></a><figcaption>An AMP document that passes validation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/586c079c-b26b-4ce4-9727-4f1cac5c5efb/03-amp-console-clean-opt.png">View large version</a>)</figcaption></figure>

## The (Optional) AMP Cache

AMP documents can be served from a web server like any other HTML document, but they can also be served from a special AMP cache. The optional cache uses several techniques to optimize an AMP document even more:

*   Image references can be replaced with images sized specifically to the viewer’s viewport.
*   Images above the fold can be inlined to save additional HTTP requests.
*   CSS variables can be inlined to reduce client-side overhead.
*   Extended AMP component implementations can be preloaded.
*   HTML and CSS can be minified to reduce the number of bytes sent over the wire (or, in this case, the airwaves).

Anyone may run their own AMP cache on their own CDN, or publishers can use Google’s for free. Given that Google seems to know a thing or two about scalability, I’m guessing that most AMP adopters will be happy to take it up on that offer. (Documentation on how to opt in to Google’s cache is forthcoming, but given that Google already indexes and caches the Internet, it’s a safe bet that it will revolve around your <code>link</code> tags and perhaps an additional <code>meta</code> tag.)

## How Do Readers Find AMP Content?

The fact that AMP document are more or less standard HTML that will render in any modern browser is, in my opinion, a huge advantage (AMP is far more open and inclusive than Facebook Instant Articles or Apple News). But from a practical perspective, it also raises the question of how audiences will find AMP content.

If readers use Google to search from a mobile device, Google can link directly to AMP versions of articles (Google has not said that it will prioritize AMP documents over non-AMP documents, but it has said that it will <a href="https://googlewebmastercentral.blogspot.com/2015/04/rolling-out-mobile-friendly-update.html">use “mobile friendliness” as a mobile search signal</a>, so you do the math). In fact, <a href="https://amphtml.wordpress.com/2015/12/09/continued-momentum-for-the-amp-project/">Google has indicated</a> that it will begin sending traffic to AMP pages from Google Search on mobile as early as late February 2016. Discovery and curation engines such as Pinterest may also choose to start directing mobile traffic to AMP pages (<a href="https://amphtml.wordpress.com/2015/12/14/building-a-faster-mobile-web-experience-with-amp/">with a few infrastructure changes</a>). Finally, websites can redirect their own mobile traffic from responsive versions of articles to their AMP counterparts. But from my perspective, a few pieces of the puzzle are still missing.

Will other search engines direct mobile traffic to AMP articles? (Perhaps not search engines that want to do business with Apple.) Will social networking apps preload AMP documents when users post links to articles, in order to make rendering nearly instantaneous? (Probably not Facebook.) Will mobile browsers start looking for <code>link</code> tags with <code>amphtml</code> relationships? (Chrome, maybe, but probably not mobile Safari.) And will aggregators and news readers out there build specifically for lightning-fast AMP content? (Time to resurrect <a href="https://www.google.com/reader/about/">Google Reader</a>!)

At this point, the answers to most of these questions are the same: to be determined.</p>

## See AMP In Action

The easiest way to see AMP in action is to check out <a href="https://insidesearch.blogspot.com/2015/10/accelerated-mobile-pages-in-search.html">Google’s search demo</a>. If you’re the trusting type, you can watch the video and just assume it all works as well as it’s depicted. If you’re more the <a href="https://en.wikipedia.org/wiki/Trust,_but_verify">trust-but-verify</a> type, you can go to <a href="https://g.co/ampdemo">g.co/ampdemo</a> on your mobile device and try out some AMP pages for yourself (QR code below).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f44854b-aae7-4fb8-a910-e621dc1865d3/04-amp-demo-qr-opt.png"><img title="AMP demo QR code" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f44854b-aae7-4fb8-a910-e621dc1865d3/04-amp-demo-qr-opt.png" alt="AMP demo QR code" /></a><figcaption>AMP demo QR code.</figcaption></figure>

You can also check out the AMP experience through desktop Chrome using Chrome’s Developer Tools. All you have to do is this:

1.  Go to [g.co/ampdemo](https://g.co/ampdemo) in Chrome.
2.  Open the Developer Tools by going to “View” → “Developer” → “Developer Tools.”
3.  Go into [device mode](https://developer.chrome.com/devtools/docs/device-mode) by clicking on the little phone icon in the top-left corner.
4.  Pick your favorite device to emulate. (For best results, reload the page in the emulator.)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bd4146a-369a-4faa-bbe3-bbc9891d6dc7/05-wsj-in-dev-tools-opt.jpg"><img title="An AMP document in Chrome Developer Tools" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bd4146a-369a-4faa-bbe3-bbc9891d6dc7/05-wsj-in-dev-tools-opt.jpg" alt="An AMP document in Chrome Developer Tools" /></a><figcaption>An AMP document in Chrome’s Developer Tools.</figcaption></figure>

## Who’s Adopting AMP?

It’s still relatively early days for AMP, so it’s hard to tell exactly who is adopting the new format in earnest, and to what extent. That being said, I’ve already seen several implementations out there in the wild, and according to the <a href="https://www.ampproject.org/faq/">AMP FAQ</a> and <a href="https://amphtml.wordpress.com/">AMP blog</a>, it’s being taken seriously by many major publishers (metered content and subscription access is <a href="https://amphtml.wordpress.com/2015/12/09/continued-momentum-for-the-amp-project/">currently under review</a>), CMS developers, advertisers, and analytics providers. I won’t list them all here because I’m sure the landscape will change almost daily, but you can keep an eye on the <a href="https://www.ampproject.org/">AMP project’s home page</a> and/or the <a href="https://amphtml.wordpress.com/">AMP blog</a> for news.</p>

## What Do I Think?

I’m glad you asked. My guess is that just about all publishers will eventually adopt it. If companies like BuzzFeed have taught the industry anything, it’s the importance of being in as many places as possible, and that digital publishing should be a technology platform capable of getting content in front of readers wherever they are, as opposed to being a singular destination waiting for readers to come to it.

The investment required to support AMP is also relatively minimal. If a publisher already supports — or plans to support — Facebook Instant Articles and Apple News, then they might as well implement support for AMP as well. While CMS strategies vary widely across the publishing industry, most CMS’ have a concept of templates and/or plugins that, once implemented, would do most of the work of converting articles into AMP HTML. (WordPress, the <a href="https://venturebeat.com/2015/11/08/wordpress-now-powers-25-of-the-web/">closest thing we have to an industry leader</a>, already <a href="https://vip.wordpress.com/2015/10/07/mobile-web/">has a plugin</a> and <a href="https://amphtml.wordpress.com/2015/12/09/continued-momentum-for-the-amp-project/">plans on supporting AMP for all publishers</a> in January 2016.) And because AMP is far less proprietary than its competition (meaning that it is open source, open to contributions, based on web technologies and client-agnostic), I would expect publishers to feel more comfortable distributing their content in a format that they feel they will have more control over long-term.

The reality is that publishers will back whatever syndication formats and partners will help get their content in front of the maximum number of readers with the least amount of overhead and investment. Right now, we are in the very early stages of a new type of war that is part platform, part format and in which each party will leverage its unique strengths to maneuver itself into the best possible position. At this point, it’s far too early to say which will endure and which will become the RSS of tomorrow.</p>

## Additional Resources

*   “[Introducing the Accelerated Mobile Pages Project, for a Faster, Open Mobile Web](https://googleblog.blogspot.com/2015/10/introducing-accelerated-mobile-pages.html)” Google Official Blog
*   [Accelerated Mobile Pages Project](https://www.ampproject.org/), official website
*   [Accelerated Mobile Pages](https://amphtml.wordpress.com/), blog
*   [AMP HTML](https://github.com/ampproject/amphtml), GitHub
*   [Docs](https://www.ampproject.org/docs/get_started/about-amp.html), Accelerated Mobile Pages Project
*   [Nigel Tufnel explaining why his amp goes to 11](https://www.youtube.com/watch?v=KOO5S4vxi0o)

{{< signature "da, jb, al" >}}


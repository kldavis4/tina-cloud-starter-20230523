---
title: 'Now You See Me: How To Defer, Lazy-Load And Act With IntersectionObserver'
slug: deferring-lazy-loading-intersection-observer-api
author: denys-mishunov
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fba25daa-8a96-4af0-84d1-b8141825ce35/intersectionobserver-now-you-see-me-opt.jpg
date: 2018-01-22T12:43:48.000Z
summary: >-
  Intersection information is needed for many reasons, such as lazy loading of
  images. But there's so much more. It's time to get a better understanding and
  different perspectives on the Intersection Observer API. Ready?
description: >-
  Intersection information is needed for many reasons, such as lazy loading of
  images. But there's so much more. It's time to get a better understanding and
  different perspectives on the Intersection Observer API. Ready?
categories:
  - API
  - JavaScript
  - Performance
---
Once upon a time, there lived a web developer who successfully convinced his customers that [sites should not look the same in all browsers](https://dowebsitesneedtolookexactlythesameineverybrowser.com), cared about accessibility, and was an early adopter of [CSS grids](https://gridbyexample.com). But deep down in his heart it was performance that was his true passion: He constantly [optimized, minified, monitored, and even employed psychological tricks](https://www.smashingmagazine.com/2018/01/front-end-performance-checklist-2018-pdf-pages/) in his projects. 

Then, one day, he learned about lazy-loading images and other assets that are not immediately visible to users and are not essential for rendering meaningful content on the screen. It was the beginning of the dawn: The developer entered the evil world of [lazy-loading jQuery plugins](https://www.jquerybyexample.net/2014/02/awesome-jquery-lazy-load-plugins.html) (or maybe the not-so-evil world of `async` and `defer` attributes). Some even say that he got straight into the core of all the evils: the world of [`scroll` event listeners](https://css-tricks.com/snippets/javascript/lazy-loading-images/). We'll never know for sure where he ended up, but then again this developer is absolutely fictitious, and any similarity to any developer is merely coincidental.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61a1ec8c-ba21-4e89-9863-a50818961950/intersectionobserver-developer-opt.jpg" sizes="100vw" caption="The fictitious web developer" alt="a web developer" >}}

Well, you can now say that Pandora's box has been opened and that our fictitious developer doesn't make the issue any less real. Nowadays, [prioritizing the above-the-fold content](https://developers.google.com/speed/docs/insights/PrioritizeVisibleContent) became utterly important for the performance of our web projects from both speed and page weight points of view.

{{% feature-panel %}}

In this article, we are going to go out of the `scroll` darkness and talk about the modern way of lazy-loading resources. Not just lazy-loading images, but loading any asset for that matter. More so, the technique we are going to talk about today is capable of much more than just lazy-loading assets: We will be able to provide any type of deferred functionality based on the elements' visibility to users. 

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fba25daa-8a96-4af0-84d1-b8141825ce35/intersectionobserver-now-you-see-me-opt.jpg" sizes="100vw" caption="" alt="IntersectionObserver: Now You See Me" >}}

Ladies and gentlemen, let's talk about the Intersection Observer API. But before we begin, let's take a look at the modern tools' landscape that led us to `IntersectionObserver`.

2017 was a very good year for tools built into our browsers, helping us to improve the quality as well as the style of our code-base without too much effort. These days, the web seems to be moving away from sporadic solutions based on *very different* to solving *very typical* to a more well-defined approach of Observer interfaces (or just "Observers"): Well-supported [MutationObserver](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver) got new family members that were quickly adopted in modern browsers:

- [IntersectionObserver](https://www.w3.org/TR/intersection-observer/#intersection-observer-api) and
- [PerformanceObserver](https://www.w3.org/TR/performance-timeline-2/#the-performanceobserver-interface) (as part of [Performance Timeline Level 2](https://www.w3.org/TR/performance-timeline-2) specification).

One more potential family member, [FetchObserver](https://docs.w3cub.com/dom/fetchobserver/), is a work in progress and guides us more into the lands of a network proxy, but today I would like to talk more about front-end instead.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7de0335c-246e-4665-8b44-0438e16cd653/intersectionobserver-observers-family-opt.jpg" sizes="100vw" caption="IntersectionObserver and PerformanceObserver are the new members of the Observers family." alt="IntersectionObserver and PerformanceObserver are the new members of the Observers family." >}}

[`PerformanceObserver`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceObserver) and [`IntersectionObserver`](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) aim at helping front-end developers improve the performance of their projects at different points. The former gives us the tool for the Real User Monitoring, while the latter is the tool, providing us with tangible performance improvement. As mentioned before, this article will take a detailed look exactly at the latter one: **IntersectionObserver**. In order to understand the mechanics of `IntersectionObserver` in particular, we should take a look at how a generic Observer is supposed to work in the modern web. 

**Pro Tip**: You can skip the theory and dive into the [mechanics of IntersectionObserver](#deconstructing-intersectionobserver) right away or, even further, straight to the [possible applications](#possible-applications) of `IntersectionObserver`.

## Observer vs. Event

An "Observer," as the name implies, is intended to observe something that happens in the context of a page. Observers can watch something happening on a page, like DOM changes. They can also watch for page's lifecycle events. Observers can also run some callback functions. Now attentive reader might immediately spot the issue here and ask, "So, what is the point? Don't we have events for this purpose already? What makes Observers different?" Very good point! Let's take a closer look and sort it out.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0b2f86d-330f-4e26-b4fa-b7aebde6f080/intersectionobserver-observer-vs-event-opt.jpg" sizes="100vw" caption="Observer vs. Event: What's the difference?" alt="Observer vs. Event: what's the difference?" >}}

The crucial difference between regular Event and Observer is that by default, the former reacts synchronously for every occurrence of the Event, affecting the main thread's responsiveness, while the latter should react asynchronously without affecting performance that much. At least, this is true for the currently presented Observers: **All of them behave asynchronously**, and I don't think this will change in the future. 

This leads to the main difference in handling the callbacks of Observers that might confuse the beginners: Observers' async nature might result in several observables being passed to a callback function at the same time. Because of this, the callback function should expect not a single entry but an `Array` of entries (even though sometimes the Array will contain only one entry in it).

Moreover, some Observers (in particular the one we are talking about today) provide a very handy pre-computed properties, which otherwise, we used to calculate ourselves using expensive (from performance standpoint) methods and properties when using regular events. To clarify this point, we will get to an example a bit later in the article.

So if it's hard for somebody to step aside from the Event paradigm, I would say that Observers are events on steroids. Another description would be: Observers are a new level of approximation on top of the events. But no matter which definition you prefer, it should come without saying that Observers are not intended to replace events (at least not yet); there are enough use cases for both, and they can happily live side-by-side.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c51b9a1-7e49-4058-9b96-45dd0d0d6dc1/intersectionobserver-obser-event-bff-opt.jpg" sizes="100vw" caption="Observers are not intended to replace Events: Both can live together happily." alt="Observers are not intended to replace Events: Both can live together happily." >}}

## Generic Observer's Structure

The generic structure of an Observer (any of those available at the time of writing) looks similar to this:

<div class="break-out">

<pre><code class="language-javascript">/**
* Typical Observer's registration
*/
let observer = new YOUR-TYPE-OF-OBSERVER(function (entries) {
  // entries: Array of observed elements
  entries.forEach(entry => {
      // Here we can do something with each particular entry
  });
});

// Now we should tell our Observer what to observe
observer.observe(WHAT-TO-OBSERVE);
</code></pre></div>

Again, note that `entries` is an `Array` of values, not a single entry.

This is the generic structure: Implementations of particular Observers differ in the arguments being passed into it's `observe()` and the arguments passed into its callback. For example `MutationObserver` should also get a [configuration object](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver#MutationObserverInit) to know more about what changes in the DOM to observe. `PerformanceObserver` doesn't observe nodes in DOM, but instead [has the dedicated set of entry types](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceObserver/observe) it can observe.

Here, let's finish the "generic" part of this discussion and dive deeper into the topic of today's article — `IntersectionObserver`.

## Deconstructing IntersectionObserver

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ead4cc6b-7bed-40aa-9da3-0c17760291f8/intersectionobserver-intersectionobserver-opt.jpg" sizes="100vw" caption="Deconstructing IntersectionObserver" alt="Deconstructing IntersectionObserver" >}}

First of all, let's sort out what `IntersectionObserver` is. 

[According to MDN](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API):

<blockquote>The Intersection Observer API provides a way to asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document's viewport.</blockquote>

Simply put, `IntersectionObserver` asynchronously observes overlapping of one element by another element. Let's talk about what those elements are for in `IntersectionObserver`.

### IntersectionObserver Initialization

In one of the previous paragraphs, we have seen the structure of a generic Observer. `IntersectionObserver` extends this structure a bit. First of all, this type of Observer requires a configuration with three main elements:

- **`root`**: This is the root element used for the observation. It defines the basic "capturing frame" for observable elements. By default, the `root` is the **viewport** of your browser but can really be any element in your DOM (then you set `root` to something like `document.getElementById('your-element')`). Keep in mind though that the elements you want to observe must "live" in `root`'s DOM tree in this case.

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f063b78-a149-44e8-af19-750d2ce489dd/intersectionobserver-props-root-opt.jpg" sizes="100vw" caption="<code>root</code> property defines the base for 'capturing frame' for our elements." alt="root's property of IntersectionObserver's config" >}}

- **`rootMargin`**: Defines margin around your `root` element that *extends* or *shrinks* the "capturing frame" when your `root`'s dimensions do not provide enough flexibility. The options for this configuration's values are similar to those of `margin` in CSS, such as `rootMargin: '50px 20px 10px 40px'` (top, right bottom, left). The values can be shorthanded (like `rootMargin: '50px'`) and can be expressed in either `px` or `%`. By default, `rootMargin: '0px'`.

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08ecf6a6-d230-4c7c-946c-59720be4e315/intersectionobserver-props-rootmargin-opt.jpg" sizes="100vw" caption="<code>rootMargin</code> property expands/contracts the 'capturing frame' which is defined by <code>root</code>." alt="rootMargin property of IntersectionObserver's config" >}}

- **`threshold`**: It's not always wanted to react instantly when an observed element intersects a border of the "capturing frame" (defined as a combination of `root` and `rootMargin`). `threshold` defines the percentage of such intersection at which Observer should react. It can be defined as a single value or as an array of values. To better understand `threshold`'s effect (I know it might be confusing sometimes), here are some examples:
    - `threshold: 0`: **The default value**
`IntersectionObserver` should react when the very first or very last pixel of an observed element intersects one of the borders of the "capturing frame." Keep in mind that `IntersectionObserver` is direction-agnostic, meaning that it will react in both scenarios: a) when the element *enters* and b) when it *leaves* the "capturing frame."
    - `threshold: 0.5`: Observer should be fired when 50% of an observed element intersects the "capturing frame";
    - `threshold: [0, 0.2, 0.5, 1]`:
Observer should react in 4 cases:
        - The very first pixel of an observed element enters the "capturing frame": the element is *still not* really within that frame, or the very last pixel of the observed element leaves the "capturing frame": the element is *no longer* within the frame;
        - 20% of the element is within the "capturing frame" (again, direction doesn't matter for `IntersectionObserver`);
        - 50% of the element is within the "capturing frame";
        - 100% of the element is within the "capturing frame." This is strictly opposite to `threshold: 0`.

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb5097c3-01db-40d4-b3ef-f5032d00e5ca/intersectionobserver-props-threshold-copy-opt.jpg" sizes="100vw" caption="<code>threshold</code> property defines by how much the element should intersect our 'capturing frame' before the Observer gets fired." alt="threshold property of IntersectionObserver's config" >}}

In order to inform our `IntersectionObserver` of our desired configuration, we simply pass our `config` object into our Observer's constructor along with our callback function like this:

<div class="break-out">

<pre><code class="language-javascript">const config = {
  root: null, // avoiding 'root' or setting it to 'null' sets it to default value: viewport
  rootMargin: '0px',
  threshold: 0.5
};
let observer = new IntersectionObserver(function(entries) {
    …
}, config);
</code></pre></div>

Now, we should give `IntersectionObserver` the actual element to observe. This is done simply by passing the element to `observe()` function:

<div class="break-out">

<pre><code class="language-javascript">…
const img = document.getElementById('image-to-observe');
observer.observe(image);
</code></pre></div>

A couple of things to note about this observed element:

- It has been mentioned previously, but is worth being mentioned again: In case you set `root` as an element in the DOM, the observed element should be located within the DOM tree of `root`.
- `IntersectionObserver` can accept only one element for observation at a time and doesn't support batch supply for observations. This means if you need to observe several elements (let's say several images on a page), you have to iterate over all of them and observe each of them separately:

<div class="break-out">

<pre><code class="language-javascript">…
const images = document.querySelectorAll('img');
images.forEach(image => {
    observer.observe(image);
});
</code></pre></div>

-  When loading a page with Observer in place, you might notice that the `IntersectionObserver`'s callback has been fired for all observed elements at once. Even those that do not match the supplied configuration. "Well… not really what I expected," is the usual thought when experiencing this for the first time. But don't get confused here: this doesn't necessarily mean that those observed elements somehow intersect the "capturing frame" while the page is loading. 

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28a48e0b-6106-443a-a3d8-9e3bad6d9c1a/intersectionobserver-devtools-scr-opt.jpg" sizes="100vw" caption="<code>IntersectionObserver</code> will be fired for all observed elements once they are registered, but it doesn't mean that they all intersect our 'capturing frame'." alt="Screenshot of DevTools with IntersectionObserver being fired for all elements at once." >}}

What it means though, is that the entry for this element became initialized and is now controlled by your `IntersectionObserver`. This might add unnecessary noise to your callback function though, and it becomes your responsibility to detect which elements do indeed intersect the "capturing frame" and which we still don't need to account for. To understand how to do that detection, let's get a bit deeper into the anatomy of our callback function and take a look at what such entries consist of.

### IntersectionObserver Callback

First of all, the callback function for an `IntersectionObserver` takes two arguments, and we will talk about these in reversed order starting with the *second* argument. Along with the aforementioned `Array` of observed entries, intersecting our "capturing frame," the callback function gets the **Observer itself** as the *second* argument.

### Reference To Observer Itself

<pre><code class="language-javascript">new IntersectionObserver(function(entries, SELF) {…});
</code></pre>

Getting the reference to the Observer itself is useful in a lot of scenarios when you want to stop observing some element after it has been detected by the `IntersectionObserver` for the first time. Scenarios like lazy loading of the images, deferred fetch of other assets, etc. are of this kind. When you want to stop observing an element, `IntersectionObserver` provides a [`unobserve(element-to-stop-observing)` method](https://w3c.github.io/IntersectionObserver/#dom-intersectionobserver-unobserve) that can be run in the callback function after performing some actions on the observed element (like actual lazy loading of an image, for example).

Some of these scenarios will be reviewed further in the article, but with this second argument out of our way, let's get to the main actors of this callback play.

### IntersectionObserverEntry

<pre><code class="language-javascript">new IntersectionObserver(function(ENTRIES, self) {…});
</code></pre>

The `entries` we are getting in our callback function as an `Array` are of the special type: [`IntersectionObserverEntry`](https://w3c.github.io/IntersectionObserver/#intersection-observer-entry). This interface provides us with [a pre-defined and pre-calculated set of properties](https://w3c.github.io/IntersectionObserver/#intersection-observer-entry) concerning each particular observed element. Let's take a look at the most interesting ones.

First of all, entries of `IntersectionObserverEntry` type come with information about three different rectangles — defining coordinates and boundaries of the elements involved in the process:

- **`rootBounds`**: A rectangle for the "capturing frame" (`root` + `rootMargin`);
- **`boundingClientRect`**: A rectangle for the observed element itself;
- **`intersectionRect`**: An area of the "capturing frame" intersected by the observed element.

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c9b56a3-5870-42ec-a3b5-0fc85f85aba7/intersectionobserver-entry-rectangles-opt.jpg" sizes="100vw" caption="All the bounding rectangles involved in IntersectionObserverEntry are calculated for you." alt="Rectangles of IntersectionObserverEntry" >}}

The really cool thing about these rectangles being calculated for us asynchronously is that it gives us important information related to element's positioning without us calling `getBoundingClientRect()`, `offsetTop`, `offsetLeft` and other [expensive positioning properties and methods](https://gist.github.com/paulirish/5d52fb081b3570c81e3a) triggering [layout thrashing](https://kellegous.com/j/2013/01/26/layout-performance/). Pure win for performance!

Another property of `IntersectionObserverEntry` interface that is interesting for us is **`isIntersecting`**. This is a convenience property indicating whether the observed element is currently intersecting the "capturing frame" or not. We could, of course, get this information by looking at the `intersectionRect` (if this rectangle is not 0&times;0, the element is intersecting the "capturing frame") but having this pre-calculated for us is quite convenient.

`isIntersecting` can be used to find out whether the observed element is just entering the "capturing frame" or is already leaving it. To find this out, save the value of this property as a global flag and when the new entry for this element arrives to your callback function, compare it's new `isIntersecting` with that global flag:

- If it was `false` and now it's `true`, then the element is entering the "capturing frame";
- If it's the opposite and it's `false` now while it was `true` before, then the element is leaving the "capturing frame."

`isIntersecting` is exactly the property that helps us solve the problem we discussed earlier, i.e., separate entries for the elements that really intersect the "capturing frame" from the noise of those being just the entry's initialization.

<div class="break-out">

<pre><code class="language-javascript">let isLeaving = false;
let observer = new IntersectionObserver(function(entries) {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      // we are ENTERING the "capturing frame". Set the flag.
      isLeaving = true;
          // Do something with entering entry
    } else if (isLeaving) {
      // we are EXITING the "capturing frame"
      isLeaving = false;
      // Do something with exiting entry
    }
  });
}, config);
</code></pre></div>

**NOTE**: In Microsoft Edge 15, `isIntersecting` property was not implemented, returning `undefined` despite full support for `IntersectionObserver` otherwise. [This has been fixed](https://developer.microsoft.com/en-us/microsoft-edge/platform/issues/12156111/) in July 2017 though and is available since Edge 16.

`IntersectionObserverEntry` interface provides one more pre-calculated convenience property: **`intersectionRatio`**. This parameter can be used for the same purposes as `isIntersecting` but provides more granular control due to it being a floating point number instead of boolean value. The value of `intersectionRatio` indicates how much of the observed element's area is intersecting the "capturing frame" (the ratio of `intersectionRect` area to `boundingClientRect` area). Again, we could make this calculation ourselves using information from those rectangles, but it's good to have it done for us.

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e750778-9a85-4ab5-8e56-9d8f672eb04d/intersectionobserver-intersectionratio-opt.jpg" sizes="100vw" caption="Doesn't it look familiar already? Yes, <code>intersectionRatio</code> property is similar to <code>threshold</code> property of Observer's config. The difference is that the latter defines *when* to fire up Observer, the former indicates real intersection's situation (that is slightly different from <code>threshold</code> due to asynchronous nature of Observer)." alt="Doesn't it look familiar already? Yes, <code>intersectionRatio</code> property is similar to <code>threshold</code> property of Observer's config. The difference is that the latter defines <em>when</em> to fire up Observer, the former indicates real intersection's situation (that is slightly different from <code>threshold</code> due to asynchronous nature of Observer)." >}}

**`target`** is one more property of the `IntersectionObserverEntry` interface that you might need to get to quite often. But there is absolutely no magic here – it's just the original element that had been passed to `observe()` function of your Observer. Just like `event.target` you've got used to when working with events.

To get the full list of properties for the `IntersectionObserverEntry` interface do [check the specification](https://w3c.github.io/IntersectionObserver/#intersection-observer-entry).

## Possible Applications

I realize that you most probably came to this article exactly because of this chapter: who cares about mechanics when we have code snippets for copy and paste after all? So won't bother you with more discussion now: we're getting into the land of code and examples. I hope that the comments included within the code will make things more clear.

### Deferred Functionality

First of all, let's review an example revealing the basic principles underlying the idea of `IntersectionObserver`.
Let's say you have an element that has to do a lot of computations once it's on the screen. For example, your ad should register a view only when it has actually been shown to a user. But now, let's imagine that you have an auto-played carousel element somewhere below the first screen on your page.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6047e11-da43-4773-a01f-0c8f133ce726/intersectionobserver-carousel-second-screen-opt.jpg" sizes="100vw" caption="When we have a carousel or any other heavy-lifting functionality below the fold of our application, it's a waste of resources to start bootstrapping/loading it right away." alt="Carousel below the first screen of your application" >}}

Running a carousel, in general, is a heavy task. Usually, it involves JavaScript timers, calculations to automatically scroll through the elements, etc. All of these tasks load the main thread, and when it's done in auto-play mode, it's hard for us to know when our main thread gets this hit. When we are talking about prioritizing content on our first screen and want to hit [First Meaningful Paint](https://developers.google.com/web/tools/lighthouse/audits/first-meaningful-paint) and [Time To Interactive](https://developers.google.com/web/tools/lighthouse/audits/time-to-interactive) as soon as possible, blocked main thread becomes a bottleneck for our performance.

To fix the issue, we might defer playback of such a carousel until it gets into the browser's viewport. For this case, we will employ our knowledge and example for the `isIntersecting` parameter of the `IntersectionObserverEntry` interface.

<div class="break-out">

<pre><code class="language-javascript">const carousel = document.getElementById('carousel');
let isLeaving = false;
let observer = new IntersectionObserver(function(entries) {
  entries.forEach(entry => {
        if (entry.isIntersecting) {
          isLeaving = true;
          entry.target.startCarousel();
        } else if (isLeaving) {
          isLeaving = false;
          entry.target.stopCarousel();
        }
    });
}
observer.observe(carousel);
</code></pre></div>

Here, we play the carousel only when it gets into our viewport. Notice the absence of `config` object passed to `IntersectionObserver`'s initialization: this means we rely on default configuration options. When the carousel gets out of our viewport, we should stop playing it to not spend resources on the not-important-anymore elements.

### Lazy Loading Of Assets

This is, probably, the most obvious use-case for `IntersectionObserver`: we do not want to spend resources to download something that user doesn't need right now. This will give a huge benefit to your users: users won't need to download, and their mobile devices won't need to parse and compile a lot of useless information that they do not need at the moment. Unsurprisingly at all, it will also help the performance of your app.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d01eaff-5c1d-40fd-ba02-16a4fc32aec5/intersectionobserver-gallery-second-screen-opt.jpg" sizes="100vw" caption="Lazy-loading assets like images located below the first screen – the most obvious application of IntersectionObserver." alt="Lazy-loading images below the fold" >}}

Previously, in order to defer downloading and processing resources until the moment user might get them on screen, we were dealing with event listeners on events like `scroll`. The problem is obvious: this triggered the listeners way too often. So we had to come up with the idea of throttling or debouncing the callback's execution. But all of this added a lot of pressure on our main thread blocking it when we most needed it.

So, getting back to `IntersectionObserver` in a lazy-loading scenario, what should we keep an eye on? Let's check [a simple example of lazy-loading images](https://codepen.io/mishunov/full/qpmWYP).

{{< codepen height="480" theme_id="light" slug_hash="qpmWYP" default_tab="result" user="mishunov" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/mishunov/pen/qpmWYP/">Lazy loading in IntersectionObserver</a> by Denys Mishunov (<a href="https://codepen.io/mishunov">@mishunov</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Try slowly scrolling that page to the "third screen" and watch the monitoring window in the top right corner: it will let you know how many images have been downloaded so far.

In the core of HTML markup for this task lays a simple sequence of images:

<pre><code class="language-html">…
&lt;img data-src="https://blah-blah.com/foo.jpg"&gt;
…
</code></pre>

As you can see, the images should come without `src` tags: once a browser sees `src` attribute, it will start downloading that image right away that is opposite to our intentions. Hence we should not put that attribute on our images in HTML, and instead, we might rely on some `data-` attribute like `data-src` here.

Another part of this solution is, of course, JavaScript. Let's focus on the main bits here:

<div class="break-out">

<pre><code class="language-javascript">const images = document.querySelectorAll('[data-src]');
const config = { … };

let observer = new IntersectionObserver(function (entries, self) {
  entries.forEach(entry => {
      if (entry.isIntersecting) { … }
  });
}, config);
images.forEach(image => { observer.observe(image); });
</code></pre></div>

Structure-wise, there is nothing new here: we have covered all of this before:

- We get all messages with our `data-src` attributes;
- Set `config`: for this scenario you want to expand your "capturing frame" to detect elements a bit lower than the bottom of the viewport;
- Register `IntersectionObserver` with that config;
- Iterate over our images and add all of them to be observed by this `IntersectionObserver`;

The interesting part happens within the callback function invoked on the entries. There three essential steps involved.

1. First of all, we process only the items that are really intersecting our "capturing frame." This snippet should be familiar to you by now.

<pre><code class="language-javascript">entries.forEach(entry => {
  if (entry.isIntersecting) { … }
});
</code></pre>

2. Then, we somehow process the entry by converting our image with `data-src` into a real `<img src="…">`.

<pre><code class="language-javascript">if (entry.isIntersecting) {
  preloadImage(entry.target);
  …
}
</code></pre>
This will trigger the browser to finally download the image. `preloadImage()` is a very simple function not worth being mentioned here. Just read the source.

3. Next and final step: since lazy loading is a one-time action and we do not need to download the image every time the element gets into our "capturing frame," we should `unobserve` the already-processed image. The same way as we should do it with `element.removeEventListener()` for our regular events when those are not needed anymore to prevent memory leaks in our code. 
<div class="break-out">

<pre><code class="language-javascript">if (entry.isIntersecting) {
  preloadImage(entry.target);
  // Observer has been passed as `self` to our callback
  self.unobserve(entry.target);
}
</code></pre></div>

**Note.** Instead of `unobserve(event.target)` we could also call `disconnect()`: it completely disconnects our `IntersectionObserver` and would not observe images anymore. This is useful if the only thing you care about is the first ever hit for your Observer. In our case, we need the Observer to keep monitoring the images, so we shouldn't disconnect just yet.

Feel free to fork [the example](https://codepen.io/mishunov/pen/qpmWYP) and play with different settings and options. There is one **interesting thing to mention** though when you want to lazy load the images in particular. You should always keep the box, generated by the observed element in mind! If you check the example, you will notice that the CSS for images on lines 41&ndash;47 contains supposedly redundant styles, incl. `min-height: 100px`.  This is done to give the image placeholders (`<img>` without `src` attribute) some vertical dimension. What for?

- Without vertical dimensions, all `<img>` tags would generate 0&times;0 box;
- Since `<img>` tag generates some sort of `inline-block` box by default, all of those 0&times;0 boxes would be aligned side-by-side on the same line;
- This means that your `IntersectionObserver` would register all  (or, depending on how fast you scroll, *almost* all of) the images at once — probably not quite what you want to achieve.

### Current Section's Highlighting

`IntersectionObserver` is much more than just lazy loading, of course. Here is [another example](https://codepen.io/mishunov/full/opeRdL) of replacing `scroll` event with this technology. In this one we have a pretty common scenario: on the fixed navigation bar we should highlight current section based on the scrolling position of the document.

{{< codepen height="480" theme_id="light" slug_hash="opeRdL" default_tab="result" user="mishunov" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/mishunov/pen/opeRdL/">Highlighting current section in IntersectionObserver</a> by Denys Mishunov (<a href="https://codepen.io/mishunov">@mishunov</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Structurally, it's similar to the example for lazy-loading images and has the same base structure with the following exceptions:

- Now we want to observe not images, but the sections on the page;
- Obviously enough, we also have a different function to process the entries in our callback (`intersectionHandler(entry)`). But this one is not interesting: all it does is toggling the CSS class.

What is interesting here is the `config` object though:

<div class="break-out">

<pre><code class="language-javascript">const config = { rootMargin: '-50px 0px -55% 0px' };
</code></pre></div>

Why not the default value of `0px` for `rootMargin`, you ask? Well, simply because highlighting the current section and lazy loading an image are quite different in what we try to achieve. With lazy loading, we want to start loading before the image gets into the view. Hence for that purpose, we extended our "capturing frame" by 50px at the bottom. On the contrary, when we want to highlight the current section, we have to be sure that the section is actually visible on the screen. And not only that: we have to be sure that user is, actually, reading or going to read exactly this section. Hence, we want a section to go a bit more than half the viewport from the bottom before we could declare it the active section. Also, we want to account for the height of the navigation bar, and so we remove the bar's height from the "capturing frame."

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/daee96d7-7a40-48b4-8b46-e459f59ec2c0/capturing-frame-sections2-opt.jpg" sizes="100vw" caption="We want the Observer to only detect elements that get into the 'capturing frame' between 50px from the top and 55% of the viewport from the bottom." alt="Capturing frame for current section" >}}

Also, **note** that in case of highlighting the current navigation item, we do not want to stop observing anything. Here we should always keep `IntersectionObserver` in charge, hence you will find neither `disconnect()` nor `unobserve()` here.

## Summary

`IntersectionObserver` is a very straight-forward technology. It has a [pretty good support in the modern browsers](https://caniuse.com/#search=IntersectionObserver) and if you want to implement it for browsers that still (or won't at all) support it, of course, [there is a polyfill for that](https://github.com/w3c/IntersectionObserver/tree/master/polyfill). But all in all, this is a great technology that allows us to do all sorts of things related to detecting elements in a viewport while helping to achieve a really good performance boost.

### Why Is IntersectionObserver Good For You?

- `IntersectionObserver` is an async non-blocking API!
- `IntersectionObserver` replaces our expensive listeners on `scroll` or `resize` events.
- `IntersectionObserver` does all the expensive calculations like `getClientBoundingRect()` for you so that you don't need to.
- `IntersectionObserver` follows the structural pattern of other Observers out there so, theoretically, should be easy to understand if you're familiar with how other Observers work.

### Things To Keep In Mind

If we compare IntersectionObserver's capabilities to the world of `window.addEventListener('scroll')` from where it all came, it will be hard to see any cons in this Observer. So, let's just note some things to keep in mind instead:

- Yes, `IntersectionObserver` is an async non-blocking API. This is great to know! But it is even more important to understand that the code you're running in your callbacks will not be run asynchronously by default even though the API itself is async. So there is still a chance to eliminate all the benefits you get from `IntersectionObserver` if your callback function's calculations make the main thread unresponsive. But this is a different story.
- If you're using `IntersectionObserver` for lazy loading the assets (like images, for example), run `.unobserve(asset)` after the asset has been loaded.
- `IntersectionObserver` can detect intersections only for the elements that appear in the [formatting structure](https://www.w3.org/TR/CSS2/intro.html#formatting-structure) of the document. To make it clear: the observable elements should generate a box and somehow affect the layout. Here are just some examples to give you a better understanding:

    - Elements with `display: none` are out of the question;
    - `opacity: 0` or `visibility:hidden` do create the box (even though invisible) so these will be detected;
    - Absolutely positioned elements with `width:0px; height:0px` are fine. Though, it has to be noted that absolutely positioned elements fully positioned *outside* of parent's borders (with negative margins or negative `top`, `left`, etc.) and are cut out by parent's `overflow: hidden` won't be detected: their box is out of scope for the formatting structure.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df80373c-cec8-4ca3-a766-4861f8adc359/intersectionobserver-final-opt.jpg" sizes="100vw" caption="IntersectionObserver: Now You See Me" alt="IntersectionObserver: Now You See Me" >}}

I know it was a long article, but if you're still around, here are some links for you to get an even better understanding and different perspectives on the Intersection Observer API:

- [Intersection Observer API on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API);
- [IntersectionObserver polyfill](https://github.com/w3c/IntersectionObserver/tree/master/polyfill);
- [IntersectionObserver polyfill as `npm` module](https://www.npmjs.com/package/intersection-observer);
- [Lazy-Loading Images with IntersectionObserver [video]](https://www.youtube.com/watch?v=ncYQkOrKTaI) by amazing [Paul Lewis](https://twitter.com/aerotwist);
- Basic and short (just 01:39), but very informative [introduction to IntersectionObserver [video]](https://www.youtube.com/watch?v=kW_atFXMG98) by [Surma](https://twitter.com/DasSurma).

With this, I would like to make a pause in our discussion to give you an opportunity to play with this technology and realize all of its convenience. So, go play with it. The article is finally over. This time I really mean it.

{{< signature "ra, il" >}}


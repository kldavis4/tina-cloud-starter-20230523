---
title: 'Hybrid Lazy Loading: A Progressive Migration To Native Lazy Loading'
slug: hybrid-lazy-loading-progressive-migration-native
author: andrea-verlicchi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3539a3c2-d7c6-4c04-853a-9054344f56e7/lazy-loading-migration-article.png
date: 2019-05-06T13:30:59+02:00
summary: >-
  Native lazy loading is coming to the web. Since it doesn’t depend on JavaScript, it will revolutionize the way we lazy load content today, making it easier for developers to lazy load images and iframes. But it’s not a feature we can polyfill, and it will take some time before it becomes usable across all browsers. In this article, you’ll learn how it works and how you can progressively replace your JavaScript-driven lazy loading with its native alternative, thanks to hybrid lazy loading.
description: >-
  In this article, you’ll learn how you can progressively replace your JavaScript-driven lazy loading with its native alternative &mdash; thanks to hybrid lazy loading.
categories:
  - JavaScript
  - Performance
  - Media
  - Optimization
---
In the past few weeks, you might have heard or read about native lazy loading, which is coming to Chromium 75 in the upcoming months. 

<blockquote>“Yeah, great news, but we’ll have to wait until all browsers support it.”</blockquote>

If this was the first thing that crossed your mind, keep reading. I will try and convince you of the opposite.

Let’s start with a comparison between native lazy loading and the good ol’ JavaScript-driven one.

## Native Versus JavaScript-Driven Lazy Loading

Lazy loading is a way to improve the performance of a website or web application by maximizing the rendering speed of the above-the-fold images and iframes (and sometimes videos) by deferring the loading of below-the-fold content.

### JavaScript-Driven Lazy Loading

In order to lazy load images or iframes, it’s a very common practice to mark them up by replacing the proper `src` attribute with a similar data attribute, `data-src`, then to rely on a JavaScript solution to detect when the images/iframes are getting close to the visible portion of the website (typically because the user scrolled down) and to copy the data attributes into the proper ones, then triggering the deferred loading of their content.

<pre><code class="language-javascript">&lt;img data-src="turtle.jpg" alt="Lazy turtle" class="lazy"&gt;
</code></pre>

{{% feature-panel %}}

### Native Lazy Loading

According to the [native lazy loading specification](https://github.com/whatwg/html/pull/3752/) (still under development), if you want to lazy load images or iframes using the native lazy loading feature, you would just need to add the `loading=lazy` attribute on the related tag. 

<pre><code class="language-javascript">&lt;img src="turtle.jpg" alt="Lazy turtle" loading="lazy"&gt;
</code></pre>

Addy Osmani wrote extensively about this topic in his article “[Native Image Lazy-Loading For The Web!](https://addyosmani.com/blog/lazy-loading/)” in which he stated that the Google Chrome team are already developing the feature and intend to ship it in Chrome 75. 

Other Chromium-based browsers like Opera and Microsoft Edge will also benefit from this development by gaining the same feature in their first update based on Chromium 75.

## Get Started With Native Lazy Loading

In case your website’s images are downloaded all at once at page landing without lazy loading, you can enable (where supported) native lazy loading in your website as easily as adding an HTML attribute. The `loading` attribute tells browsers which images are important to load immediately, and which ones can be downloaded lazily as the users scroll down. The same attribute can be applied to iframes.

In order to tell browsers that a particular image is important so they can load it as soon as possible, you must add the `loading="eager"` attribute on the `img` tag. The best practice is to do this for the primary images &mdash; typically for the ones that will be displayed above the fold. 

<pre><code class="language-javascript">&lt;img src="rabbit.jpg" alt="Fast rabbit" loading="eager"&gt;
</code></pre>

To tell browsers that an image should be downloaded lazily, just add the `loading="lazy"` attribute. This is a best practice only if you do it only to secondary images &mdash; typically for the ones will be displayed below the fold.

<pre><code class="language-javascript">&lt;img src="turtle.jpg" alt="Lazy turtle" loading="lazy"&gt;
</code></pre>

Just by adding the `loading` attribute to your images and iframes, you will enable your website to use native lazy loading as a progressive enhancement. Your website will gradually benefit from it as support arrives to your users in most modern browsers.

This is the best approach to use if your website is not using any kind of lazy loading today, but if you already implemented a JavaScript-driven lazy loading solution, you might want to keep it while progressively switching to native lazy loading.

The ideal solution would be to start using native lazy loading right away, and use a polyfill to make it work across all browsers. Unfortunately, native lazy loading is not a feature we can polyfill with JavaScript.

{{% ad-panel-leaderboard %}}

## No Use For A Polyfill

When a new browser technology is released to a single browser, the open-source community usually releases a JavaScript polyfill to provide the same technology to the rest of the browsers. For example, the `IntersectionObserver` polyfill uses JavaScript and DOM elements to coordinate `Element.getBoundingClientRect()` to reproduce the behavior of the native API.

But the case of native lazy loading is different because a JavaScript polyfill for `loading="lazy"` would have to *prevent* browsers from loading content as soon as they find a URL in the markup of an image or iframe. JavaScript has no control on this initial stage of page rendering, therefore it is not possible to polyfill native lazy loading.

## Hybrid Lazy Loading

If you are not satisfied with having native lazy loading only as a progressive enhancement, or you have already implemented JavaScript-based lazy loading and don’t want to lose this feature in less modern browsers (but still want to enable native lazy loading on browsers that support it), then you need a different solution. Introducing: hybrid lazy loading.

{{% pull-quote %}}
 Hybrid lazy loading is a technique to use native lazy loading on browsers that support it, otherwise, rely on JavaScript to handle the lazy loading.
{{% /pull-quote %}}

In order to do hybrid lazy loading, you need to mark up your lazy content using the `data` attributes instead of the real ones (such as in JavaScript-driven lazy loading), and to add the `loading="lazy"` attribute.

<pre><code class="language-javascript">&lt;img data-src="turtle.jpg" loading="lazy" alt="Lazy turtle"&gt;
</code></pre>

Then you require some JavaScript. In the first place, you need to **detect whether or not native lazy loading is supported by the browser**. Then, do one of the following for every element with the `loading="lazy"` attribute:

- If native lazy loading is supported, copy the `data-src`  attribute value to the `src` attribute;
- If not supported, initialize a JavaScript lazy loading script or plugin to do that as the elements enter the viewport.

It’s not very hard to write the JavaScript code required to perform these operations on your own. You can detect if native lazy loading is supported with the condition:

<pre><code class="language-javascript">if ('loading' in HTMLImageElement.prototype)
</code></pre>

If it is, just copy the `src` attribute value from `data-src`. If it’s not, initialize some lazy-loading script of your choice.

Here’s a snippet of code that does that.

<div class="break-out">

 <pre><code class="language-javascript">&lt;!-- In-viewport images should be loaded normally, or eagerly --&gt;
&lt;img src="important.jpg" loading="eager" alt="Important image"&gt;

&lt;!-- Let’s lazy-load the rest of these images --&gt;
&lt;img data-src="lazy1.jpg" loading="lazy" alt="Lazy image 1"&gt;
&lt;img data-src="lazy2.jpg" loading="lazy" alt="Lazy image 2"&gt;
&lt;img data-src="lazy3.jpg" loading="lazy" alt="Lazy image 3"&gt;

&lt;script&gt;
  (function() {
    if ("loading" in HTMLImageElement.prototype) {
      var lazyEls = document.querySelectorAll("[loading=lazy]");
      lazyEls.forEach(function(lazyEl) {
        lazyEl.setAttribute(
          "src",
          lazyEl.getAttribute("data-src")
        );
      });
    } else {
      // Dynamically include a lazy loading library of your choice
      // Here including vanilla-lazyload
      var script = document.createElement("script");
      script.async = true;
      script.src =
        "https://cdn.jsdelivr.net/npm/vanilla-lazyload@12.0.0/dist/lazyload.min.js";
      window.lazyLoadOptions = {
        elements_selector: "[loading=lazy]"
        //eventually more options here
      };
      document.body.appendChild(script);
    }
  })();
&lt;/script&gt;
</code></pre>
</div>

You can find and test the code above in [this live demo](https://www.andreaverlicchi.eu/lazyload/demos/native_lazyload_conditional_old.html).

Still, that is a very basic script, and things can get complicated when you’re using additional attributes or tags to get responsive images (such as the `srcset` and `sizes` attributes or even the `picture` and `source` tags).

## A Little Third-Party Help

For the past four years, I’ve been maintaining an open-source lazy load script named “`vanilla-lazyload`” and, in a couple of days after Addy Osmani wrote about native lazy loading, the community reacted by asking me if my script could act as a polyfill.

As I explained before, you cannot create a polyfill for the native lazy loading feature, however, I thought of a solution that would make it easier for developers to begin the transition to native lazy loading, without needing to write any of the JavaScript code that I’ve mentioned before.

Starting from version 12 of `vanilla-lazyload`, you can just set the `use_native` option to `true` to enable hybrid lazy loading. The script is only 2.0 kB gzipped and it’s already available on [GitHub](https://github.com/verlok/lazyload), [npm](https://www.npmjs.com/package/vanilla-lazyload), and [jsDelivr](https://www.jsdelivr.com/package/npm/vanilla-lazyload).

- [Get to know `vanilla-lazyload` on GitHub](https://github.com/verlok/lazyload)

## Demos

You can start playing around with native lazy loading today by downloading [Chrome Canary](https://www.google.com/intl/it/chrome/canary/) or [Microsoft Edge Insider](https://www.microsoftedgeinsider.com/en-us/) (*dev channel*) then enabling the flags “Enable lazy image loading” and “Enable lazy frame loading”. To enable these flags, enter `about:flags` in your browser’s URL field and search for “lazy” in the search box.

### Native Lazy Loading Demo

To analyze how native lazy loading works in the developer tools, you can start playing with the following demo. In this one, **not a single line of JavaScript is used**. Yes, it’s just full plain native lazy loading.

- [Test native lazy loading demo](https://www.andreaverlicchi.eu/lazyload/demos/native_lazyload.html)

**What to expect**: All images are fetched at once, but with different HTTP responses. The ones with the response code `200` are the eagerly loaded images, while the ones with the response code `206` are only partially fetched in order to get the initial information about the images. Those images will then be fetched completely with a `200` response code when you scroll down.

### Hybrid Lazy Loading Demo

To analyze how hybrid lazy loading works, you can start playing with the next demo. Here, `vanilla-lazyload@12.0.0` is used and the `use_native` option is set to `true`:

- [Test hybrid lazy loading demo](https://www.andreaverlicchi.eu/lazyload/demos/native_lazyload_conditional.html)

**What to expect**: Try the demo on different browsers to see how it behaves. On browsers that support native lazy loading, the behavior would be the same as in the native lazy loading demo. On browsers that do not support native lazy loading, the images will be downloaded as you scroll down. 

Please note that `vanilla-lazyload` uses the IntersectionObserver API under the hood, so you would need to polyfill it on Internet Explorer and less recent versions of Safari. It’s not a big deal if a polyfill is not provided, though, because in that case `vanilla-lazyload` would just download all the images at once.

**Note**: *Read more in the “[To Polyfill Or Not To Polyfill](https://github.com/verlok/lazyload/blob/master/README.md#to-polyfill-or-not-to-polyfill-intersectionobserver)” chapter of* `vanilla-lazyload`*’s readme file.*

{{% ad-panel-leaderboard %}}

## Try Hybrid Lazy Loading In Your Website

Since native lazy loading is coming soon to some browsers, why don’t you give it a chance today using hybrid lazy loading? Here’s what you need to do:

### HTML Markup

The simplest image markup is made by two attributes: `src` and `alt`. 

For the above-the-fold images, you should leave the `src` attribute and add the `loading="eager"` attribute.

<pre><code class="language-html">&lt;img src="important.jpg" loading="eager" alt="Important image"&gt;
</code></pre>

For below-the-fold images, you should replace the `src` attribute with the data attribute `data-src` and add the `loading="lazy"` attribute.

<pre><code class="language-html">&lt;img data-src="lazy.jpg" loading="lazy" alt="A lazy image"&gt;
</code></pre>

If you want to use responsive images, do the same with the `srcset` and `sizes` attributes.

<pre><code class="language-html">&lt;img alt="A lazy image" 
    loading="lazy" 
    data-src="lazy.jpg" 
    data-srcset="lazy_400.jpg 400w, lazy_800.jpg 800w" 
    data-sizes="100w"&gt;
</code></pre>

If you prefer to use the `picture` tag, change the `srcset`, `sizes` and `src` also in the `source` tags.

<div class="break-out">

 <pre><code class="language-html">&lt;picture&gt;
    &lt;source 
        media="(min-width: 1200px)" 
        data-srcset="lazy_1200.jpg 1x, lazy_2400.jpg 2x"&gt;
    &lt;source 
        media="(min-width: 800px)" 
        data-srcset="lazy_800.jpg 1x, lazy_1600.jpg 2x"&gt;
    &lt;img alt="A lazy image" 
        loading="lazy" 
        data-src="lazy.jpg"&gt;
&lt;/picture&gt;
</code></pre>
</div>

The `picture` tag can also be used to selectively load the WebP format for your images.

**Note**: *If you want to know more usages of* `vanilla-lazyload`*, please read the “[Getting Started](https://github.com/verlok/lazyload/blob/master/README.md#-getting-started---html)” HTML section of its readme file.*

### JavaScript Code

First of all, you need to include `vanilla-lazyload` on your website.

You can load it from a CDN like jsDelivr:

<div class="break-out">

 <pre><code class="language-javascript">&lt;script src="https://cdn.jsdelivr.net/npm/vanilla-lazyload@12.0.0/dist/lazyload.min.js"&gt;&lt;/script&gt;
</code></pre>
</div>

Or you can install it using npm:

<pre><code class="language-bash">npm install vanilla-lazyload@12
</code></pre>

It’s also possible to use an `async` script with automatic initialization; load it as a ES module using `type="module"` or load it as AMD using RequireJS. Find more ways to include and use `vanilla-lazyload` in the “[Getting Started](https://github.com/verlok/lazyload/blob/master/README.md#-getting-started---script)” script section of the readme file.

Then, in your website/web application’s JavaScript code, include the following:

<pre><code class="language-javascript">var pageLazyLoad = new LazyLoad({
    elements_selector: "[loading=lazy]",
    use_native: true // ← enables hybrid lazy loading
});
</code></pre>
 
**Note**: *The script has plenty of other settings you can use to customize* `vanilla-lazyload`*’s behavior, e.g. to increase the distance of the scrolling area from which to start loading the elements or to load elements only if they stayed in the viewport for a given time.  Find more settings in the [API section](https://github.com/verlok/lazyload/blob/master/README.md#-api) of the readme file.*

### All Together, Using An `async` Script

To put it all together and use an `async` script to maximize performance, please refer to the following HTML and JavaScript code:

<div class="break-out">

 <pre><code class="language-javascript">&lt;!-- In-viewport images should be loaded normally, or eagerly --&gt;
&lt;img src="important.jpg" loading="eager" alt="Important image"&gt;

&lt;!-- Let’s lazy-load the rest of these images --&gt;
&lt;img data-src="lazy1.jpg" loading="lazy" alt="Lazy image 1"&gt;
&lt;img data-src="lazy2.jpg" loading="lazy" alt="Lazy image 2"&gt;
&lt;img data-src="lazy3.jpg" loading="lazy" alt="Lazy image 3"&gt;

&lt;!-- Set the options for the global instance of vanilla-lazyload --&gt;
&lt;script&gt;
  window.lazyLoadOptions = {
    elements_selector: "[loading=lazy]",
    use_native: true // ← enables hybrid lazy loading
  };
&lt;/script&gt;

&lt;!-- Include vanilla lazyload 12 through an async script --&gt;
&lt;script async src="https://cdn.jsdelivr.net/npm/vanilla-lazyload@12.0.0/dist/lazyload.min.js"&gt;&lt;/script&gt;
</code></pre>
</div>

That’s it! With these very simple and easy steps, you’ll have enabled hybrid lazy loading in your website!

## Important Best Practices

- Apply lazy loading only to the images that you know that will probably be displayed below the fold. Eagerly load the ones above the fold to maximize performance. If you just apply lazy load to all images in your page, you’ll slow down rendering performance. 
- Use CSS to reserve some space for the images before they are loaded. That way, they’ll push the rest of the content below. If you don’t do that, a larger number of images will be placed above the fold before they should, triggering immediate downloads for them. If you need a CSS trick to do that, you can find one in the [tips and tricks section of the readme](https://github.com/verlok/lazyload#-tips--tricks) of `vanilla-lazyload`.

## Pros And Cons

<table class="break-out">
  <thead>
    <tr>
      <th data-tablesaw-priority="persist"></th>
      <th>NATIVE LAZY LOADING</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>PROS</strong></td>
      <td><ul><li>No JavaScript required;</li><li>No setup headaches, it just works;</li><li>No need to reserve space for images using CSS tricks;</li></ul></td>
    </tr>
    <tr>
      <td><strong>CONS</strong></td>
      <td><ul><li>It does not work today on all browsers;</li><li>The initial payload is higher, because of the prefetch of the initial 2 kb for every image.</li></ul></td>
    </tr>
  </tbody>
</table>

<table class="break-out">
  <thead>
    <tr>
      <th data-tablesaw-priority="persist"></th>
      <th>JAVASCRIPT-DRIVEN LAZY LOADING</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>PROS</strong></td>
      <td><ul><li>It works consistently across all browsers, right now;</li><li>You can do very highly customized UI tricks, like the blur-in effect or the delayed loading.</li></ul></td>
    </tr>
    <tr>
      <td><strong>CONS</strong></td>
      <td><ul><li>It relies on JavaScript to load your content.</li></ul></td>
    </tr>
  </tbody>
</table>

<table class="break-out">
  <thead>
    <tr>
      <th data-tablesaw-priority="persist"></th>
      <th>HYBRID LAZY LOADING</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>PROS</strong></td>
      <td><ul><li>It gives you the chance to enable and test native lazy loading where supported;</li><li>It enables lazy loading on all browsers;</li><li>You can transparently remove the script dependency as soon as native lazy loading support will be widespread.</li></ul></td>
    </tr>
    <tr>
      <td><strong>CONS</strong></td>
      <td><ul><li>It still relies on JavaScript to load your content.</li></ul></td>
    </tr>
  </tbody>
</table>

## Wrapping Up

I’m very excited that native lazy loading is coming to browsers, and I can’t wait for *all* browser vendors to implement it! 

In the meantime, you can either choose to enrich your HTML markup for progressive enhancement and get native lazy loading only where supported, or you can go for hybrid lazy loading and get both native and JavaScript-driven lazy loading until the day native lazy loading will be supported by the vast majority of browsers.

Give it a try! Don’t forget to [star/watch `vanilla-lazyload` on GitHub](https://github.com/verlok/lazyload), and let me know your thoughts in the comments section. 

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'Now You See Me: How To Defer, Lazy-Load And Act With IntersectionObserver'" href="https://www.smashingmagazine.com/2018/01/deferring-lazy-loading-intersection-observer-api/" rel="bookmark">Now You See Me: How To Defer, Lazy-Load And Act With IntersectionObserver</a></li>
<li><a title="Read 'Lazy Loading JavaScript Modules With ConditionerJS'" href="https://www.smashingmagazine.com/2018/03/lazy-loading-with-conditioner-js/" rel="bookmark">Lazy Loading JavaScript Modules With ConditionerJS</a></li>
<li><a title="Read 'Front-End Performance Checklist 2019'" href="https://www.smashingmagazine.com/2019/01/front-end-performance-checklist-2019-pdf-pages/" rel="bookmark">Front-End Performance Checklist 2019 (PDF, Apple Pages, MS Word)</a></li>
<li><a title="Read 'How Improving Website Performance Can Help Save The Planet'" href="https://www.smashingmagazine.com/2019/01/save-planet-improving-website-performance/" rel="bookmark">How Improving Website Performance Can Help Save The Planet</a></li>
</ul>

{{< signature "dm, il" >}}

---
title: What Are Progressive Web AMPs?
slug: progressive-web-amps
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be0c8839-e993-4604-8728-25c89610e875/progressive-web-amp-8.png
date: 2016-12-08T18:19:05.000Z
author: paulbakaus
description: >-
  Even though the new Service Worker API allows you to cache away all of your website’s assets for an almost instant _subsequent_ load, like when meeting someone new, the first impression is what
  counts. If the first load takes more than 3 seconds, the latest [DoubleClick
  study](https://www.doubleclickbygoogle.com/articles/mobile-speed-matters/)
  shows that more than 53% of all users will drop off.
categories:
  - Coding
  - JavaScript
  - AMP
  - PWA
---
If you’ve been following the web development community these last few months, chances are you’ve read about <a href="https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/">progressive web apps</a> (PWAs). It’s an umbrella term used to describe web experiences so advanced that they compete with ever-so-rich and immersive native apps: <a href="https://www.smashingmagazine.com/2016/02/making-a-service-worker/">full offline support</a>, <a href="https://developers.google.com/web/fundamentals/engage-and-retain/app-install-banners/?hl=en">installability</a>, “Retina,” full-bleed imagery, sign-in support for personalization, fast, smooth in-app browsing, push notifications and a great UI.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20974993-47cc-4e72-81d3-2ca5e92c0939/progressive-web-amp-2.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cec0f51d-69c8-4b19-9ce1-14af0e9d49f0/progressive-web-amp-3-opt.png" alt="From Google’s Advanced Mobile Pages (AMP) to progressive web apps" /></a><figcaption>A few of Google’s sample progressive web apps.</figcaption></figure>

But even though the new <a href="https://www.smashingmagazine.com/2016/02/making-a-service-worker/">Service Worker API</a> allows you to cache away all of your website’s assets for an almost instant <em>subsequent</em> load, like when meeting someone new, the first impression is what counts. If the first load takes more than 3 seconds, the latest <a href="https://www.doubleclickbygoogle.com/articles/mobile-speed-matters/">DoubleClick study</a> shows that more than 53% of all users will drop off.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2016/11/building-shaders-with-babylon-js/#further-reading-on-smashingmag)

*   [Everything You Need To Know About Google’s AMPs](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)
*   [Building For Mobile: RWD, PWA, AMP Or Instant Articles?](https://www.smashingmagazine.com/2017/03/building-for-mobile-rwd-pwa-amp-instant-articles/)
*   [A Beginner’s Guide To Progressive Web Apps](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/)
*   [Why Perceived Performance Matters](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/)

{{% feature-panel %}}

And 3 seconds, let’s be real, is already a quite <em>brutal</em> target. On mobile connections, which often average around a 300-millisecond latency and come with other constraints such as limited bandwidth and a sometimes poor signal connection, you might be left with a total load performance budget of less than 1 second to actually do the things you need to do to initialize your app.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea0af0be-55c1-4c14-9ec8-5d4c09d33e9e/progressive-web-amp-7.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea0af0be-55c1-4c14-9ec8-5d4c09d33e9e/progressive-web-amp-7.png" alt="From Google’s Advanced Mobile Pages (AMP) to progressive web apps" /></a><figcaption>The delays that sit between your user and your content.</figcaption></figure>

Sure, there are ways to <a href="https://codelabs.developers.google.com/codelabs/your-first-pwapp/#4">mitigate</a> this problem of a slow first load — prerendering a basic layout on the server, lazy-loading chunks of functionality and so on — but you can only get so far with this strategy, and you have to employ, or be, a front-end performance wizard.

So, if an almost instant first load is fundamentally at odds with a native-like app experience, what can we do?

## AMP, For Accelerated Mobile Pages

One of the most significant advantages of a website is almost frictionless entry — that is, no installation step and almost instant loading. A user is always just a click away.

To really benefit from this opportunity for effortless, ephemeral browsing, all you need is a crazy-fast-loading website. And all you need to make your website crazy fast? A proper diet: no megabyte-sized images, no render-blocking ads, no 100,000 lines of JavaScript, just the content, please.</p>

<a href="https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/">AMPs</a>, short for Accelerated Mobile Pages, are <a href="https://www.ampproject.org/docs/get_started/technical_overview.html">very good at this</a>. In fact, it is their <em>raison d’être</em>. It’s like a car-assist feature that forces you to stay in the fast lane by enforcing a set of sensible rules to always prioritize your page’s main content. And by creating this strict, <a href="https://www.ampproject.org/docs/get_started/technical_overview.html#size-all-resources-statically">statically</a> laid out environment, it enables platforms such as Google Search to get one step closer to “instant” by <a href="https://www.ampproject.org/docs/get_started/technical_overview.html#load-pages-in-an-instant">preloading just the first viewport</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e33b9ab-fd9b-4c91-ae53-a1bd0dab5110/progressive-web-amp-0.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e33b9ab-fd9b-4c91-ae53-a1bd0dab5110/progressive-web-amp-0.png" alt="From Google’s Advanced Mobile Pages (AMP) to progressive web apps" /></a><figcaption>The (first) hero image and the headline of this AMP will be prerendered, so that the visitor can see its (above-the-fold) content instantly.</figcaption></figure>

## AMP Or PWA?

To make the experience reliably fast, you need to live with some constraints when implementing AMP pages. AMP isn’t useful when you need highly dynamic functionality, such as Push Notifications or Web Payments, or really anything requiring additional JavaScript. In addition, since AMP pages are usually served from an AMP Cache, you won’t get the biggest Progressive Web App benefits on that first click, since your own Service Worker can’t run. On the other hand, a Progressive Web App can never be as fast as AMP on that first click, as platforms can safely and cheaply prerender AMP pages – a feature that also makes embedding simpler (e.g. into an inline viewer).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be0c8839-e993-4604-8728-25c89610e875/progressive-web-amp-8.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be0c8839-e993-4604-8728-25c89610e875/progressive-web-amp-8.png" alt="From Google’s Advanced Mobile Pages (AMP) to progressive web apps" /></a><figcaption>Once the user leaves the AMP Cache as they click an internal link, you can enhance the website by installing service workers to make the website available offline (and more).</figcaption></figure>

So, AMP or progressive web app? Instant delivery and optimized delivery, or the latest advanced platform features and flexible application code? What if there was a way to combine the two, to reap the benefits of both?

## The Perfect User Journey

In the end, what matters is the ideal user experience you’re aiming for — the <strong>user journey</strong>. It goes like this:

1.  A user discovers a link to your content and clicks it.
2.  The content loads almost instantly and is a pleasure to consume.
3.  The user is invited and automatically upgraded to an even richer experience, with smoother in-app navigation, push notifications and offline support.
4.  The user exclaims, “Why, hello. Heck yeah!” and is instantly redirected to an app-like experience and they can install the site onto their home screen.

The first hop to your website should feel almost instant, and the browsing experience should get more and more engaging afterwards.

Sound too good to be true? Well, what if we <strong>combine the two technologies</strong> — although at the first glance, they are seemingly unrelated and solve different needs?

## PWAMP Combination Patterns

To get to instant-loading, auto-upgrading experience, all you need to do is combine the laser-sharp leanness of AMPs with the richness of progressive web apps in one (or multiple) of the following ways:

*   **AMP as PWA**.  When you can live with AMP’s limitations.
*   **AMP to PWA**.  When you want to smoothly transition between the two.
*   **AMP in PWA**.  When you want to reuse AMPs as a data source for your PWA.

Let’s walk through each of them individually.</p>

### AMP as PWA

Many websites won’t ever need things beyond the boundaries of AMPs. <a href="https://ampbyexample.com/">Amp by Example</a>, for instance, is both an AMP and a progressive web app:

*   It has a service worker and, therefore, allows offline access, among other things.
*   It has a manifest, prompting the “Add to Homescreen” banner.

When a user visits <a href="https://ampbyexample.com/">Amp by Example</a> from a Google search and then clicks on another link on that website, they navigate away from the AMP Cache to the origin. The website still uses the AMP library, of course, but because it now lives on the origin, it can use a service worker, can prompt to install and so on.

You can use this technique to enable offline access to your AMP website, as well as extend your pages as soon as they’re served from the origin, because you can modify the response via the service worker’s <code>fetch</code> event, and return as a response whatever you want:

<pre><code class="language-javascript">function createCompleteResponse (header, body) {

  return Promise.all([
    header.text(),
    getTemplate(RANDOM STUFF AMP DOESN’T LIKE),
    body.text()
  ]).then(html =&gt; {
    return new Response(html[0] + html[1] + html[2], {
      headers: {
        'Content-Type': 'text/html'
      }
    });
  });

}</code></pre>

This technique allows you to insert scripts and more advanced functionality outside of the scope of AMPs on subsequent clicks.</p>

### AMP to PWA

When the above isn’t enough, and you want a dramatically different PWA experience around your content, it’s time for a slightly more advanced pattern:

*   All content “leaf” pages (those that have specific content, not overview pages) are published as AMPs for that nearly instant loading experience.
*   These AMPs use AMP’s special element [`<amp-install-serviceworker>`](https://www.ampproject.org/docs/reference/extended/amp-install-serviceworker.html) to warm up a cache and the PWA shell **while the user is enjoying** your content.
*   When the user clicks another link on your website (for example, the call to action at the bottom for a more app-like experience), the service worker intercepts the request, takes over the page and loads the PWA shell instead.

You can implement the experience above in three easy steps, provided you are familiar with how service workers work. (If you aren’t, then I greatly recommend my colleague <a href="https://www.udacity.com/course/offline-web-applications--ud899">Jake’s Udacity course</a>). First, install the service worker on all of your AMPs:

<pre><code class="language-javascript">&lt;amp-install-serviceworker
      src="https://www.your-domain.com/serviceworker.js"
      layout="nodisplay"&gt;
&lt;/amp-install-serviceworker&gt;</code></pre>

Secondly, in the service worker’s installation step, cache any resources that the PWA will need:

<pre><code class="language-javascript">var CACHE_NAME = 'my-site-cache-v1';
var urlsToCache = [
  '/',
  '/styles/main.css',
  '/script/main.js'
];

self.addEventListener('install', function(event) {
  // Perform install steps
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(function(cache) {
        console.log('Opened cache');
        return cache.addAll(urlsToCache);
      })
  );
});</code></pre>

Finally, again in the service worker, respond with the PWA instead of the requested AMP on navigation requests. (The code below, while functional, is overly simplified. A more advanced example follows in the demo at the end.)

<pre><code class="language-javascript">self.addEventListener('fetch', event =&gt; {
    if (event.request.mode === 'navigate') {
      event.respondWith(fetch('/pwa'));

      // Immediately start downloading the actual resource.
      fetch(event.request.url);
    }

});</code></pre>

Now, whenever a user clicks on a link on your page served from the AMP Cache, the service worker registers the <code>navigate</code> request mode and takes over, then responds with the full-blown, already-cached PWA instead.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0247d786-f0d8-4054-9cf3-1f4dc5f43171/progressive-web-amp-6.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0247d786-f0d8-4054-9cf3-1f4dc5f43171/progressive-web-amp-6.png" alt="From Google’s Advanced Mobile Pages (AMP) to progressive web apps" /></a><figcaption>You can progressively enhance the website by installing service workers. For browsers that don't support service workers, they will just move to another page within the AMP Cache.</figcaption></figure>

What’s especially interesting about this technique is that you are now using progressive enhancement to go from AMP to PWA. However, this also means that, as is, browsers that don’t yet support service workers will jump from AMP to AMP and will never actually navigate to the PWA.

AMP solves this with something called <a href="https://www.ampproject.org/docs/reference/components/amp-install-serviceworker#shell-url-rewrite">shell URL rewriting</a>. By adding a fallback URL pattern to the <code>&lt;amp-install-serviceworker&gt;</code> tag, you are instructing AMP to rewrite all matching links on a given page to go to another legacy shell URL instead, if no service worker support has been detected:

<pre><code class="language-javascript">&lt;amp-install-serviceworker
      src="https://www.your-domain.com/serviceworker.js"
      layout="nodisplay"
      data-no-service-worker-fallback-url-match=".*"
      data-no-service-worker-fallback-shell-url="https://www.your-domain.com/pwa"&gt;
&lt;/amp-install-serviceworker&gt;</code></pre>

With these attributes in place, all subsequent clicks on an AMP will go to your PWA, regardless of any service worker. Pretty neat, huh?

### AMP in PWA

So, now the user is in the progressive web app, and chances are you’re using some AJAX-driven navigation that fetches content via JSON. You can certainly do that, but now you have these crazy infrastructure needs for two totally different content back ends — one generating AMP pages, and the other offering a JSON-based API for your progressive web app.

But think for a second about what an AMP really is. It’s not just a website. It’s designed as a ultra-portable content unit. An AMP is self-contained by design and can be safely embedded into another website. What if we could dramatically simplify the back-end complexity by ditching the additional JSON API and instead reuse AMP as the data format for our progressive web app?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d471bcc6-5132-48d0-b58b-123936e70a58/progressive-web-amp-3.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d471bcc6-5132-48d0-b58b-123936e70a58/progressive-web-amp-3.png" alt="From Google’s Advanced Mobile Pages (AMP) to progressive web apps" /></a><figcaption>AMP pages can be safely embedded into another website — the AMP library is compiled and loaded only once for the entire PWA.</figcaption></figure>

Of course, one easy way to do this would be simply to load AMP pages in frames. But iframes are slow, and then you’d need to recompile and re-initialize the AMP library over and over. Today’s cutting-edge web technology offers a better way: the shadow DOM.

The process looks like this:

1.  The PWA hijacks any navigation clicks.
2.  Then, it does an XMLHttpRequest to fetch the requested AMP page.
3.  It puts the content into a new shadow root.
4.  And it tells the main AMP library, “Hey, I have a new document for you. Check it out!” (calling `attachShadowDoc` on runtime).

Using this technique, the AMP library is compiled and loaded only once for the entire PWA, and then is responsible for every shadow document you attach to it. And, because you’re fetching pages via XMLHttpRequests, you can modify the AMP source before inserting it into a new shadow document. You could do this, for instance, to:

*   strip out unnecessary things, such as headers and footers;
*   insert additional content, such as more obnoxious ads or fancy tooltips;
*   replace certain content with more dynamic content.

Now, you’ve made your progressive web app much less complex, and you’ve dramatically reduced the complexity of your back-end infrastructure.</p>

## Ready, Set, Action!

To demonstrate the shadow DOM approach (i.e. an AMP within a PWA), the AMP team has created a <a href="https://choumx.github.io/amp-pwa/">React-based demo called The Scenic,</a> a fake travel magazine:

<figure><a href="https://choumx.github.io/amp-pwa/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f5a239e-5675-49e5-8f2f-eaf789476c7a/progressive-web-amp-4.png" alt="From Google’s Advanced Mobile Pages (AMP) to progressive web apps" width="333" height="685" /></a></figure>

The <a href="https://github.com/ampproject/amp-publisher-sample/blob/master/amp-pwa">whole demo</a> is on GitHub, but the magic happens in <a href="https://github.com/ampproject/amp-publisher-sample/blob/master/amp-pwa/src/components/amp-document/amp-document.js#L92"><code>amp-document.js</code>’ React component</a>.</p>

### Show me something real

For a real production example, take a look at <a href="https://beta.mic.com">Mic's new PWA)</a> (in beta): If you shift-reload a <a href="https://beta.mic.com/articles/161568/arrow-season-5-episode-9-a-major-character-returns-in-midseason-finale-maybe">random article</a> (which will ignore the Service Worker temporarily) and look at the source code, you'll notice it's an AMP page. Now try clicking on the hamburger menu: It reloads the current page, but since <code>&lt;amp-install-serviceworker&gt;</code> has <em>already installed</em> the PWA app shell, the reload is almost <em>instant</em>, and the menu is open after the refresh, making it look like no reload has happened. But now you're in the PWA (that embeds AMP pages), bells and whistles and all. Sneaky, but magnificent.</p>

## (Not So) Final Thoughts

Needless to say, I’m extremely excited about the potential of this new combination. It’s a combination that brings out the best of both.

Recapping the highlights:

*   always fast, no matter what;
*   great distribution built-in (through AMP’s platform partners);
*   progressively enhanced;
*   one back end to rule them all;
*   less client complexity;
*   less overall investment;

But we’re just starting to discover variations of the pattern, as well as completely new ones. Build the best web experiences that 2016 and beyond have to offer. Onward, to a new chapter of the web!

{{< signature "al" >}}


---
title: Improving User Flow Through Page Transitions
slug: improving-user-flow-through-page-transitions
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6733517f-d2eb-4ca4-bf1b-6105b1345069/example-my-library-opt.png
date: 2016-07-05T16:32:57.000Z
author: luigiderosa
summary: >-
  Any time a user’s experience is interrupted, the chance of them leaving increases. Changing from one page to another will often cause this interruption by showing a white flash of no content, by taking too long to load or by otherwise taking the user out of the context they were in before the new page opened.
description: >-
  Any time a user’s experience is interrupted, the chance of them leaving increases. Changing from one page to another will often cause this interruption by showing a white flash of no content, by taking too long to load or by otherwise taking the user out of the context they were in before the new page opened.
categories:
  - Coding
  - UX
  - Mobile
  - JavaScript
  - UX
---
Transitions between pages can enhance the experience by retaining (or even improving) the user’s context, maintaining their attention, and providing visual continuity and positive feedback. At the same time, page transitions can also be aesthetically pleasing and fun and can reinforce branding when done well.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6733517f-d2eb-4ca4-bf1b-6105b1345069/example-my-library-opt.png" width="500" height="342" title="Improving User Flow Through Page Transitions" alt="Page Transitions" /></figure>

<p>In this article, we’ll create, step by step, a transition between pages. We will also talk about the pros and cons of this technique and how to push it to its limit.</p>

## Examples

<p>Many mobile apps make good use of transitions between views. In the example below, which follows <a href="https://material.google.com/motion/material-motion.html">Google’s material design</a> guidelines, we see how the animation conveys hierarchical and spatial relationships between pages.</p>

{{< vimeo id="173269145" >}}

<p>Why don’t we use the same approach with our websites? Why are we OK with the user feeling like they are being teleported every time the page changes?</p>

{{% feature-panel %}}

## How To Transition Between Web Pages

### SPA Frameworks

<p>Before getting our hands dirty, I should say something about single-page application (SPA) frameworks. If you are using an SPA framework (such as AngularJS, Backbone.js or Ember), then creating transitions between pages will be much easier because all of the routing is already handled by JavaScript. Please refer to the relevant documentation to see how to transition pages using your framework of choice, because there are probably some good examples and tutorials.</p>

### The Wrong Way

<p>My first attempt to create a transition between pages looked more or less like this:</p>

<pre><code class="language-javascript">document.addEventListener('DOMContentLoaded', function() {
  // Animate in
});

document.addEventListener('beforeunload', function() {
  // Animate out
});
</code></pre>

<p>The concept is simple: Use one animation when the user leaves the page, and another animation when the new page loads.</p>

<p>However, I soon found that this solution had some limitations:</p>

<ul>
<li>We don’t know how long the next page will take to load, so the animation might not look fluid.</li>
<li>We can’t create transitions that combine content from the previous and next pages.</li>
</ul>

<p>In fact, the only way to achieve a fluid and smooth transition is to have full control over the page-changing process and, therefore, <strong>not to change the page at all</strong>. Thus, we have to change our approach to the problem.</p>

### The Right Way

<p>Let’s look at the steps involved in creating a simple crossfade transition between pages the right way. It involves something called <code>pushState</code> AJAX (or PJAX) navigation, which will essentially turn our website into a kind of single-page website.</p>

<p>Not only does this technique achieve smooth and pleasant transitions, but we will benefit from other advantages, which we will cover in detail later in this article.</p>

### Prevent the Default Link Behavior

<p>The first step is to create a <code>click</code> event listener for all links to use, preventing the browser from performing its default behavior and customizing the way it handles page changes.</p>

<pre><code class="language-javascript">// Note, we are purposely binding our listener on the document object
// so that we can intercept any anchors added in future.
document.addEventListener('click', function(e) {
  var el = e.target;

  // Go up in the nodelist until we find a node with .href (HTMLAnchorElement)
  while (el && !el.href) {
    el = el.parentNode;
  }

  if (el) {
    e.preventDefault();
    return;
  }
});
</code></pre>

<p>This method of adding an event listener to a parent element, instead of adding it to each specific node, is called <a href="https://stackoverflow.com/a/1688293/2065702">event delegation</a>, and it’s possible due to the <a href="https://stackoverflow.com/a/4616720/2065702">event-bubbling nature</a> of the HTML DOM API.</p>

{{% ad-panel-leaderboard %}}

### Fetch the Page

<p>Now that we have interrupted the browser when it tries to change the page, we can manually fetch that page using the <a href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API">Fetch API</a>. Let’s look at the following function, which fetches the HTML content of a page when given its URL.</p>

<pre><code class="language-javascript">function loadPage(url) {
  return fetch(url, {
    method: 'GET'
  }).then(function(response) {
    return response.text();
  });
}
</code></pre>

<p>For browsers that don’t support the Fetch API, consider adding <a href="https://github.com/github/fetch">the polyfill</a> or using the good old-fashioned <code><a href="https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest">XMLHttpRequest</a></code>.</p>

### Change the Current URL

<p>HTML5 has a fantastic API called <a href="https://developer.mozilla.org/en-US/docs/Web/API/History_API"><code>pushState</code></a>, which allows websites to access and modify the browser’s history without loading any pages. Below, we are using it to modify the current URL to be the URL of the next page. Note that this is a modification of our previously declared anchor click-event handler.</p>

<pre><code class="language-javascript">if (el) {
  e.preventDefault();
  history.pushState(null, null, el.href);
  changePage();

  return;
}
</code></pre>

<p>As you might have noticed, we have also added a call to a function named <code>changePage</code>, which we will look at in detail shortly. The same function will also be called in the <code>popstate</code> event, which is fired when the browser’s active history entry changes (as when a user clicks on the back button of their browser):</p>

<pre><code class="language-javascript">window.addEventListener('popstate', changePage);
</code></pre>

<p>With all of this, we are basically building a very primitive routing system, in which we have active and passive modes.</p>

<p>Our active mode is in use when a user clicks on a link and we change the URL using <code>pushState</code>, while passive mode is in use when the URL changes and we get notified by the <code>popstate</code> event. In either case, we are going to call <code>changePage</code>, which takes care of reading the new URL and loading the relevant page.</p>

### Parse and Add the New Content

<p>Typically, the pages being navigated will have common elements, like <code>header</code> and <code>footer</code>. Suppose we use the following DOM structure on all of our pages (which is actually the structure of Smashing Magazine itself):</p>

<pre><code class="language-markup'>
&lt;header&gt;
  …
&lt;/header&gt;

&lt;main&gt;
  &lt;div class=&quot;cc&quot;&gt;
     …
  &lt;/div&gt;
&lt;/main&gt;

&lt;footer&gt;
 …
&lt;/footer&gt;
</code></pre>

<p>The only part we need to swap at every page change is the content of the <code>cc</code> container. Thus, we can structure our <code>changePage</code> function like so:</p>

<pre><code class="language-javascript">var main = document.querySelector('main');

function changePage() {
  // Note, the URL has already been changed
  var url = window.location.href;

  loadPage(url).then(function(responseText) {
    var wrapper = document.createElement('div');
        wrapper.innerHTML = responseText;

    var oldContent = document.querySelector('.cc');
    var newContent = wrapper.querySelector('.cc');

    main.appendChild(newContent);
    animate(oldContent, newContent);
  });
}
</code></pre>

### Animate!

<p>When the user clicks a link, the <code>changePage</code> function <strong>fetches</strong> the HTML of that page, then <strong>extracts</strong> the <code>cc</code> container and <strong>adds</strong> it to the <code>main</code> element. At this point, we have two <code>cc</code> containers on our page, the first belonging to the previous page and the second from the next page.</p>

<p>The next function, <code>animate</code>, takes care of crossfading the two containers by overlapping them, fading out the old one, fading in the new one and removing the old container. In this example, I’m using the <a href="https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API">Web Animations API</a> to create the fade animation, but of course you can use any technique or library you’d like.</p>

<pre><code class="language-javascript">function animate(oldContent, newContent) {
  oldContent.style.position = 'absolute';

  var fadeOut = oldContent.animate({
    opacity: [1, 0]
  }, 1000);

  var fadeIn = newContent.animate({
    opacity: [0, 1]
  }, 1000);

  fadeIn.onfinish = function() {
    oldContent.parentNode.removeChild(oldContent);
  };
}
</code></pre>

<p>The final code is <a href="https://gist.github.com/luruke/0704bc594c81e3f4c491ba919b96450a">available on GitHub</a>.</p>

{{< vimeo id="173269151" >}}

<p>And those are the basics of transitioning web pages!</p>

## Caveats And Limitations

<p>The little example we’ve just created is far from perfect. In fact, we still haven’t taken into account a few things:</p>

<ul>
<li><strong>Make sure we affect the correct links.</strong><br>
Before changing the behavior of a link, we should add a check to make sure it should be changed. For example, we should ignore all links with <code>target="_blank"</code> (which opens the page in a new tab), all links to external domains, and some other special cases, like <code>Control/Command + click</code> (which also opens the page in a new tab).</li>

<li><strong>Update elements outside of the main content container.</strong><br>
Currently, when the page changes, all elements outside of the <code>cc</code> container remain the same. However, some of these elements would need to be changed (which could now only be done manually), including the <code>title</code> of the document, the menu element with the <code>active</code> class, and potentially many others depending on the website.</li>

<li><strong>Manage the lifecycle of JavaScript.</strong><br>
Our page now behaves like an SPA, in which the browser does not change pages itself. So, we need to manually take care of the JavaScript lifecycle &mdash; for example, binding and unbinding certain events, reevaluating plugins, and including polyfills and third-party code.</li>
</ul>

### Browser Support

<p>The only requirement for this mode of navigation we’re implementing is the <code>pushState</code> API, which is <a href="https://caniuse.com/#feat=history">available in all modern browsers</a>. This technique <strong>works fully as a progressive enhancement</strong>. The pages are still served and accessible in the usual way, and the website will continue to work normally when JavaScript is disabled.</p>

<p>If you are using an SPA framework, consider using PJAX navigation instead, just to keep navigation fast. In doing so, you gain legacy support and create a more SEO-friendly website.</p>

{{% ad-panel-leaderboard %}}

## Going Even Further

<p>We can continue to push the limit of this technique by optimizing certain aspects of it. The next few tricks will <strong>speed up</strong> navigation, significantly enhancing the user’s experience.</p>

### Using a Cache

<p>By slightly changing our <code>loadPage</code> function, we can add a simple cache, which makes sure that pages that have already been visited aren’t reloaded.</p>

<pre><code class="language-javascript">var cache = {};
function loadPage(url) {
  if (cache[url]) {
    return new Promise(function(resolve) {
      resolve(cache[url]);
    });
  }

  return fetch(url, {
    method: 'GET'
  }).then(function(response) {
    cache[url] = response.text();
    return cache[url];
  });
}
</code></pre>

<p>As you may have guessed, we can use a more permanent cache with the <a href="https://developer.mozilla.org/en-US/docs/Web/API/Cache">Cache API</a> or another client-side persistent-storage cache (like IndexedDB).</p>

### Animating Out the Current Page

<p>Our crossfade effect requires that the next page be loaded and ready before the transition completes. With another effect, we might want to start animating out the old page as soon as the user clicks the link, which would give the user immediate feedback, a great aid to perceived performance.</p>

<p>By using <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">promises</a>, handling this kind of situation becomes very easy. The <code>.all</code> method creates a new promise that gets resolved as soon as all promises included as arguments are resolved.</p>

<pre><code class="language-javascript">// As soon as animateOut() and loadPage() are resolved…
Promise.all[animateOut(), loadPage(url)]
  .then(function(values) {
    …
</code></pre>

### Prefetching the Next Page

<p>Using just PJAX navigation, page changes are usually almost <strong>twice as fast</strong> as default navigation, because the browser does not have to parse and evaluate any scripts or styles on the new page.</p>

<p>However, we can go even further by starting to preload the next page when the user hovers over or starts touching the link.</p>

{{< vimeo id="173269150" >}}

<p>As you can see, there are usually 200 to 300 milliseconds of delay in the user’s hovering and clicking. This is <strong>dead time</strong> and is usually enough to load the next page.</p>

<p>That being said, prefetch wisely because it can easily become a bottleneck. For example, if you have a long list of links and the user is scrolling through it, this technique will prefetch all of the pages because the links are passing under the mouse.</p>

<p>Another factor we could detect and take into account in deciding whether to prefetch is the user’s connection speed. (Maybe this will be made possible in future with the <a href="https://wicg.github.io/netinfo/">Network Information API</a>.)</p>

### Partial Output

<p>In our <code>loadPage</code> function, we are fetching the entire HTML document, but we actually just need the <code>cc</code> container. If we are using a server-side language, we can detect whether the request is coming from a particular custom AJAX call and, if so, output just the container it needs. By using the <a href="https://developer.mozilla.org/en-US/docs/Web/API/Headers">Headers API</a>, we can send a custom HTTP header in our fetch request.</p>

<pre><code class="language-javascript">function loadPage(url) {
  var myHeaders = new Headers();
  myHeaders.append('x-pjax', 'yes');

  return fetch(url, {
    method: 'GET',
    headers: myHeaders,
  }).then(function(response) {
    return response.text();
  });
}
</code></pre>

<p>Then, on the server side (using PHP in this case), we can detect whether our custom header exists before outputting only the required container:</p>

<pre><code class="language-php">
if (isset($_SERVER['HTTP_X_PJAX'])) {
  // Output just the container
}
</code></pre>

<p>This will reduce the size of the HTTP message and also reduce the server-side load.</p>

## Wrapping Up

<p>After implementing this technique in a couple of projects, I realized that a reusable library would be immensely helpful. It would save me time in implementing it on each occasion, freeing me to focus on the transition effects themselves.</p>

<p>Thus was born <a href="https://barbajs.org">Barba.js</a>, a tiny library (4 KB minified and gZip’d) that abstracts away all of this complexity and provides a nice, clean and simple API for developers to use. It also accounts for views and comes with reusable transitions, caching, prefetching and events. It is open source and <a href="https://github.com/luruke/barba.js">available on GitHub</a>.</p>

{{< vimeo id="173269144" >}}

## Conclusion

<p>We’ve seen now how to create a crossfade effect and the pros and cons of using PJAX navigation to effectively transform our website into an SPA. Apart from the benefit of the transition itself, we’ve also seen how to implement simple caching and prefetching mechanisms to speed up the loading of new pages.</p>

<p>This entire article is based on my personal experience and what I’ve learned from implementing page transitions in projects that I’ve worked on. If you have any questions, do not hesitate to leave a comment or reach out to me on Twitter &mdash; my info is below!</p>

### <span class="rh">Further Reading</span> on SmashingMag:
<ul>
    <li><a title="Read 'Smart Transitions In User Experience Design'" href="https://www.smashingmagazine.com/2013/10/smart-transitions-in-user-experience-design/" rel="bookmark">Smart Transitions In User Experience Design</a></li>
  <li><a title="Read 'Designing In The Transition To A Multi-Device World'" href="https://www.smashingmagazine.com/2013/02/designing-in-transition-to-multi-device/" rel="bookmark">Designing In The Transition To A Multi-Device World</a></li>
  <li><a title="Read 'Hybrid Mobile Apps: Providing A Native Experience With Web Technologies'" href="https://www.smashingmagazine.com/2014/10/providing-a-native-experience-with-web-technologies/" rel="bookmark">Providing A Native Experience With Web Technologies</a></li>
</ul>

{{< signature "rb, ml, al, il" >}}

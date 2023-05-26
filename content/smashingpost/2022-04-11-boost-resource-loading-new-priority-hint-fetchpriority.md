---
title: 'Boost Resource Loading With fetchpriority, A New Priority Hint '
slug: boost-resource-loading-new-priority-hint-fetchpriority
author: adrian-bece
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/619a484f-276c-46b3-9f4e-ce788aef7fef/boost-resource-loading-new-priority-hint-fetchpriority.jpg
date: 2022-04-11T09:30:00.000Z
summary: >-
   This new attribute will enable us to fine-tune relative resource priority, improve LCP performance, deprioritize JavaScript fetch calls, and much more. Let’s check out <code>fetchpriority</code> and explore some potential use cases.
description: >-
  This new attribute will enable us to fine-tune relative resource priority, improve LCP performance, deprioritize JavaScript fetch calls, and much more. Let’s check out <code>fetchpriority</code> and explore some potential use cases.
categories:
  - Performance
  - JavaScript
  - Optimization
---

JavaScript, CSS, images, iframes, and other resources impact how quickly website loads, renders and becomes usable to the user. Loading experience is crucial to the user’s first impression and overall usability, so Google defined **Largest Contentful Paint (LCP)** metric to measure how quickly the main content loads and is displayed to the user.

The main content for LCP is usually the largest element located above the fold. This element could be an image, video, or simply, just a large block of text. Of all those options, it’s safe to assume that text is the best choice for LCP performance because it loads and renders fast.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6e4e99d-0724-46e3-bce9-11aa0ecd62e4/1-resource-loading-optimization-fetchpriority-attribute.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6e4e99d-0724-46e3-bce9-11aa0ecd62e4/1-resource-loading-optimization-fetchpriority-attribute.png" width="798" height="382" sizes="100vw" caption="web.dev’s main content is an image according to LCP (test ran on WebPageTest). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6e4e99d-0724-46e3-bce9-11aa0ecd62e4/1-resource-loading-optimization-fetchpriority-attribute.png'>Large preview</a>)" alt="web.dev’s main content is an image according to LCP" >}}

Browsers follow a [critical render path](https://developers.google.com//web/fundamentals/performance/critical-rendering-path/analyzing-crp) to parse the HTML document and its referenced resources (CSS, JS, images, etc.) to display the content on the screen. Browsers construct a render tree using DOM and CSSOM, and the page renders once all render-blocking resources like CSS, font files, and scripts have been parsed and processed.

## Resource Priorities Defaults

Let’s focus on how these resources are requested and downloaded. The HTML document is the first resource to be requested and downloaded, but how do browsers determine what to download next and in which order? **Browsers have a set of predetermined priorities** for each resource type, so they can be downloaded in an optimal order. 

Here is a rough summary according to the “[Resource Fetch Prioritization and Scheduling in Chromium](https://docs.google.com/document/d/1bCDuq9H1ih9iNjgzyAL0gpwNFiEP4TZS-YLRp_RuMlc/edit#)” by Patrick Meenan:

<table class="tablesaw">
  <thead>
    <tr>
      <th>Priority</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Highest</strong></td>
      <td><ul>
        <li>Main resource (usually a HTML document),</li>
        <li>CSS (early &ndash; if requested before any non-preloaded image file) and font files;</li>
      </ul></td>
    </tr>
    <tr>
      <td><strong>High</strong></td>
      <td><ul>
        <li>Script (early &ndash; if requested before any non-preloaded image file),</li>
        <li>Preload,</li>
        <li>Image (in viewport);</li></ul></td>
    </tr>
    <tr>
      <td><strong>Medium</strong></td>
      <td><ul>
        <li>CSS and Script (late &ndash; if requested after a non-preloaded image file).</li></ul></td>
    </tr>
    <tr>
      <td><strong>Low</strong></td>
      <td><ul>
        <li>Script (async),</li>
        <li>Media and images,</li>
        <li>SVG document.</li></ul></td>
    </tr>
    <tr>
      <td><strong>Lowest</strong></td>
      <td><ul>
        <li>CSS mismatch,</li>
        <li>Prefetch.</li></ul></td>
    </tr>
  </tbody>
</table>



These default priorities work reasonably well for most cases, usually resulting in a good performance. However, developers with a deep understanding of the project may want to improve performance beyond that by doing some fine-tuning under the hood. It’s common knowledge that better website performance results in more conversions, more traffic, and better user experience.

We can use the `preload` attribute for the HTML `link` element to optimize loading performance by ensuring that the browser discovers the resource earlier, downloads it, and caches it. However, that doesn’t provide us with more granular control over a particular resource type. 

For example, let’s say that we are loading two render-blocking stylesheets. How can we signal to the browser that `main.css` file is more important than `third-party-plugin.css` file without resorting to using JavaScript or some other workaround?

{{% feature-panel %}}

## `fetchpriority` HTML attribute

Enter `fetchpriority` HTML attribute. This new attribute can be assigned to virtually any HTML element that loads some kind of resources like images and scripts and affects its relative priority. **Relative priority** means that we can only affect a priority within the same resource type. Meaning that we cannot tell browsers to load images before loading the render-blocking JavaScript.

It’s important to keep in mind that this attribute **doesn’t ensure that a higher-priority resource will be loaded before other (lower-priority) resources of the same type.**  So, `fetchpriority` shouldn’t be used to control the loading order itself, like in a case where we’d want a JavaScript dependency to be loaded before a script that uses it.

Also, this **attribute doesn’t force the browser to fetch a resource** or prevent it from fetching. It’s up to the browser if it’s going to fetch the resource or not. This attribute just helps the browser prioritize it when it is fetched.

That being said, `fetchpriority` attribute accepts one of the following three values:

- `low`  
Decrease the relative priority of the resource.
- `high`  
Increase the relative priority of the resource.
- `auto`  
Default value which lets the browser decide the priority.

Going back to our previous example, we can use this attribute to **signal to the browser** that we want to initiate a request and download of `main.css` at a higher priority than the `third-party-plugin.css` which is the same render-blocking CSS resource as `main.css`.

<pre><code class="language-javascript">&lt;link rel="stylesheet" href="/path/to/main.css" fetchpriority="high" /&gt;
&lt;link rel="stylesheet" href="/path/to/third-party-plugin.css" fetchpriority="low" /&gt;</code></pre>

Pretty simple, right?

**Note**: *At the moment of writing of this article, the `fetchpriority` attribute is currently supported in Chrome Canary with full release set for Chrome version 101, with other browsers to follow suit.*

### Use It Sparingly 

It’s not recommended to assign `fetchpriority` to every resource. Browsers already do a good enough job, so it should be used sparingly for very specific use cases where we want to prioritize requests for improving LCP, prioritize one deferred resource over the other of the same type, prioritize preload requests, etc. Over-using this attribute or running premature optimization might harm performance, so make sure to run performance tests to verify.

With that in mind, let’s move on to some of those real-world examples and scenarios, so we can use this new attribute effectively.

{{% ad-panel-leaderboard %}}
 
## Examples And Use Cases

### Improving Largest Contentful Paint performance

This is currently the best use-case for `fetchpriority`. Images are processed after all render-blocking and critical resources have already been rendered, and even using `preload` or `loading="eager"` won’t change that. However, with `fetchpriority` we can try to make sure the LCP image is more likely to be ready for that initial render, resulting in a considerable performance boost.

With that in mind, **text block is the most optional LCP candidate in most cases**, as it performs better than image or other media content. For cases where images are critical or the main part of the content, we have no option other than just to display them. So, we need to optimize them to load as quickly as possible.

Let’s take a look at a simple example of an image carousel which is also the main content in the viewport and a prime candidate for LCP.

{{< codepen height="480" theme_id="light" slug_hash="oNppEoX" data-default-tab="html,result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Example - without fetch priority](https://codepen.io/smashingmag/pen/oNppEoX) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

We can run Lighthouse test to check the metrics and use this data for comparison. 

**Please note**: *Several factors can affect the stats, so the results might differ, but the general gist is the same.*

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4061d12-8e82-4a09-99f5-a897cea7d33b/2-resource-loading-optimization-fetchpriority-attribute.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4061d12-8e82-4a09-99f5-a897cea7d33b/2-resource-loading-optimization-fetchpriority-attribute.png" width="732" height="291" sizes="100vw" caption="Without priority hints. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4061d12-8e82-4a09-99f5-a897cea7d33b/2-resource-loading-optimization-fetchpriority-attribute.png'>Large preview</a>)" alt="An example without priority hints" >}}

Let’s use `fetchpriority` and assign a `high` priority to the main (active) image and `low` priority to thumbnails.

<pre><code class="language-javascript">&lt;!-- Carousel is above the fold --&gt;    
&lt;nav&gt;
      &lt;ul class="hero__list"&gt;
        &lt;li&gt;
          &lt;img fetchpriority="low" src="..." /&gt;
        &lt;/li&gt;
        &lt;li&gt;
          &lt;img fetchpriority="low" src="..." /&gt;
        &lt;/li&gt;

     &lt;!-- ... --&gt;

    &lt;figure class="hero__figure"&gt;
      &lt;img fetchpriority="high" src="..."&gt;&lt;/img&gt;

    &lt;!-- ... --&gt;</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="mdppXLR" data-default-tab="html,result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Example - with fetch priority (https://codepen.io/smashingmag/pen/mdppXLR) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

Let’s run Lighthouse on the modified example, and we can notice that our LCP has improved.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a1a4894-cfa8-4389-b1b7-6a012627920c/3-resource-loading-optimization-fetchpriority-attribute.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a1a4894-cfa8-4389-b1b7-6a012627920c/3-resource-loading-optimization-fetchpriority-attribute.png" width="674" height="252" sizes="100vw" caption="With fetchpriority='high' on main image and fetchPriority='low' on the thumbnails. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a1a4894-cfa8-4389-b1b7-6a012627920c/3-resource-loading-optimization-fetchpriority-attribute.png'>Large preview</a>)" alt="An example with fetchpriority='high' on main image and fetchPriority='low' on the thumbnails" >}}

By using `fetchpriority`, we marked which of the images were more important for content and which are not. So, the browser took these signals into account when fetching resources, prioritizing the main content image, which in turn allowed for the main content to show earlier, improving the LCP metric!

### Deferred Images

Similarly, we can use `fetchpriority` attribute to prioritize below-the-fold resources that have `loading="lazy"` attribute. Even though this won’t affect LCP times, we can still signal the browser to prioritize the largest (active) carousel image over the small thumbnails when the browser decides to load them. That way, we can improve even the lazy loading user experience.

Remember, this **attribute doesn’t force browsers to fetch a resource**. Even with `fetchpriority` set to `high`, the **browser will still decide if the resource is going to be fetched** or not. We only signal to the browser which one of these requests is more important from each group.

<pre><code class="language-javascript">&lt;!-- Carousel is below the fold --&gt;   

&lt;nav&gt;
      &lt;ul class="hero__list"&gt;
        &lt;li&gt;
          &lt;img loading="lazy"fetchpriority="low" src="..." /&gt;
        &lt;/li&gt;
        &lt;li&gt;
          &lt;img loading="lazy" fetchpriority="low" src="..." /&gt;
        &lt;/li&gt;

     &lt;!-- ... --&gt;

    &lt;figure class="hero__figure"&gt;
      &lt;img loading="lazy" fetchpriority="high" src="..."&gt;&lt;/img&gt;

    &lt;!-- ... --&gt;</code></pre>

### Deferred Stylesheets

We can also use `fetchpriority` to signal which scripts and stylesheets should have a higher priority when loading. 

**Please note**: *The scripts and stylesheets remain render-blocking if they are not deferred.*

Let’s take a look at the following example. If you want to follow along with this example on CodePen, **make sure to inspect the configuration of the HTML tab on the CodePen** example below. The code referenced below is included there, as the CodePen HTML tab only covers HTML `body`, and `head` is added with this separate config.

{{< codepen height="480" theme_id="light" slug_hash="oNppEQx" data-default-tab="html,result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Prioritizing stylesheets](https://codepen.io/smashingmag/pen/oNppEQx) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

We are loading the following resources:

- **Google Fonts Stylesheet**  
Defer loading right after the first render. This font switch is visible to the user (FOUT).
- **Non-Critical Below-The-Fold Stylesheet** (*Bootstrap is used just as an example for a more sizeable CSS file*)  
Defer loading after first render with low priority, because those styles are used below-the-fold.
- **Critical CSS**  
Render-blocking and applied immediately.

We’ll use a common technique to [defer the loading of non-critical stylesheets](https://web.dev/defer-non-critical-css/) and add a `preload` with appropriate `fetchpriority` to ensure that font is loaded as soon as possible, so the [FOUT (Flash of unstyled text)](https://web.dev/preload-optional-fonts/) occurs right after the first render.

<div class="break-out">

<pre><code class="language-javascript">&lt;!-- Increase priority for fonts to load fonts right after the first render --&gt;
&lt;link rel="preload"
      as="style"
      fetchpriority="high" 
      onload="this.onload=null;this.rel='stylesheet'"
      href="https://fonts.googleapis.com/css2?family=Crete+Round&family=Roboto:wght@400;700&display=swap" /&gt;

&lt;!-- Preload non-critical, below-the-fold CSS with low priority --&gt;
&lt;link rel="preload"
      as="style"
      fetchpriority="low"
      onload="this.onload=null;this.rel='stylesheet'"
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" /&gt;

&lt;!-- No JS fallback for stylesheets --&gt;
&lt;noscript&gt;
  &lt;!-- --&gt;
&lt;/noscript&gt;

&lt;!-- Inline critical CSS (above-the-fold styles) --&gt;
&lt;style&gt;
  /&#42; Critical CSS &#42;/
&lt;/style&gt;</code></pre>
</div>

Although this configuration won’t affect LCP or some other performance metrics, it showcases how we can use `fetchpriority` to improve the loading experience by prioritizing one resource over the other within the same type.

{{< codepen height="480" theme_id="light" slug_hash="oNppEVL" data-default-tab="html,result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Prioritizing stylesheets - with fetchpriority](https://codepen.io/smashingmag/pen/oNppEVL) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

### Fine-tuning JavaScript Resource Priorities

Although we can use `async` and `defer` to change when scripts are loaded and parsed, with `fetchpriority` we can have more granular control over JavaScript resources.

These two [examples from web.dev](https://web.dev/priority-hints/#reprioritize-scripts) perfectly showcase how we can combine these attributes for even more script loading options:

<div class="break-out">

<pre><code class="language-javascript">&lt;script src="async_but_important.js" async fetchpriority="high"&gt;&lt;/script&gt;
&lt;script src="blocking_but_unimportant.js" fetchpriority="low"&gt;&lt;/script&gt;</code></pre>
</div>

### Prioritizing JavaScript `fetch` Requests

This attribute is not limited to HTML, it can be also used in JavaScript `fetch` to prioritize some API calls over others.

For example, let’s say we are loading a blog post. We want to prioritize the main content over comments, so we need to pass a `priority` attribute in `fetch` options object.

**Please note**: *The `priority` value is `high` by default, so we only need to assign `low` when we want to reduce the priority of the `fetch` request.*

<pre><code class="language-javascript">/&#42; High-priority fetch for post content (default) &#42;/
function loadPost() {
  fetch("https://jsonplaceholder.typicode.com/posts/1")
    .then(parseResponse)
    .then(parsePostData)
    .catch(handleError);
}

/&#42; Lower-priority fetch for comments (with priority option) &#42;/
function loadComments() {
  fetch("https://jsonplaceholder.typicode.com/posts/1/comments", {
    priority: "low"
  })
    .then(parseResponse)
    .then(parseCommentsData)
    .catch(handleError);
}</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="ExooQBa" data-default-tab="html,result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Fetch with priority](https://codepen.io/smashingmag/pen/ExooQBa) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

### Embedded `iframe` Elements

We can assign `fetchpriority` to `iframe` elements just like any other resource. However, keep in mind that this attribute only affects the main resource of the iframe and doesn’t apply to the resources within the `iframe`. The browser will load resources within the iframe with default priorities. However, we are still delaying them to start later.

<div class="break-out">

<pre><code class="language-html">&lt;iframe fetchpriority="low" type="text/html" width="640" height="390" src="http://www.youtube.com/embed/..." frameborder="0"&gt;&lt;/iframe&gt;</code></pre>
</div>

{{% ad-panel-leaderboard %}}
 
## Conclusion

Lately, we’ve seen exciting new features that allow us control over browser and loading behavior &mdash; [CSS Cascade Layers](https://www.smashingmagazine.com/2022/01/introduction-css-cascade-layers/) allow us control over the CSS rule layers, and now, `fetchpriority` will allow us more granular control over resource loading priority. However, this control over the core concepts requires developers to be careful and use them according to best practices, as incorrect use may harm both the performance and user experience.

With that in mind, `fetchpriority` should be used only in specific cases, such as:

- Improving LCP performance for image and other media resources;
- Changing priorities of `link` and `script` resources;
- Lowering the priority of JavaScript `fetch` requests which are not critical for content or functionality;
- Lowering the priority of iframe elements.

At the time of writing of this article, this attribute is available in **Chrome Canary and is set to be released in Chrome version 101**, with other browsers to follow suit. It will be great to see the development community come up with more interesting use cases and performance improvements.

### References

- [Priority Hints](https://wicg.github.io/priority-hints/#effects-of-priority-hints), Draft Community Group Report
- “[Optimizing Resource Loading With Priority Hints](https://web.dev/priority-hints/)”, Leena Sohoni, Addy Osmani and Patrick Meenan

{{< signature "vf, yk, il" >}}

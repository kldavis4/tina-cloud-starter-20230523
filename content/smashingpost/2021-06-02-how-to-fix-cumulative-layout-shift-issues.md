---
title: 'How To Fix Cumulative Layout Shift (CLS) Issues'
slug: how-to-fix-cumulative-layout-shift-issues
author: barry-pollard
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87fbe5f9-d311-4542-a3f0-14e860415946/cumulative-layout-shift-issues.jpg
date: 2021-06-02T12:30:00.000Z
summary: >-
  Google’s Core Web Vitals initiative has taken the SEO and Web Performance worlds by storm and many sites are busy optimizing their Page Experience to maximize the ranking factor. The Cumulative Layout Shift metric is causing trouble to a lot of sites, so let’s have a look at ways of addressing any issues for that metric.
description: >-
  Google’s Core Web Vitals initiative has taken the SEO and Web Performance worlds by storm and many sites are busy optimizing their Page Experience to maximize the ranking factor. The Cumulative Layout Shift metric is causing trouble to a lot of sites, so let’s have a look at ways of addressing any issues for that metric.
categories:
  - Performance
  - Core Web Vitals
  - CSS
  - JavaScript
  - Browsers
---

[Cumulative Layout Shift (CLS)](https://web.dev/cls/) attempts to measure those jarring movements of the page as new content &mdash; be it images, advertisements, or whatever &mdash; comes into play later than the rest of the page. It calculates a score based on how much of the page is unexpectedly moving about, and how often. These **shifts of content** are very annoying, making you lose your place in an article you’ve started reading or, worse still, making you click on the wrong button!

In this article, I’m going to discuss some **front-end patterns to reduce CLS**. I’m not going to talk too much about measuring CLS as I’ve covered that already [in a previous article](https://www.smashingmagazine.com/2021/04/complete-guide-measure-core-web-vitals/). Nor will I talk too much about the mechanics of how CLS is calculated: Google has some [good documentation on that](https://web.dev/cls/), and [Jess Peck](https://twitter.com/jessthebp)’s [The Almost-Complete Guide to Cumulative Layout Shift](https://jessbpeck.com/posts/completecls/) is an awesome deep dive into that too. However, I will give a little background needed to understand some of the techniques.

## Why CLS Is Different

CLS is, in my opinion, the most interesting of the Core Web Vitals, in part because it’s something we’ve never really measured or optimized for before. So, it often requires new techniques and ways of thinking to attempt to optimize it. It’s a very different beast to the other two Core Web Vitals.

Looking briefly at the other two Core Web Vitals, [Largest Contentful Paint (LCP)](https://web.dev/lcp/) does exactly as its name suggests and is more of a twist on previous loading metrics that measures how quickly the page loads. Yes, we’ve changed how we defined the user experience of the page load to look at the loading speed of the **most relevant content**, but it’s basically reusing the old techniques of ensuring that the content loads as quickly as possible. How to optimize your LCP should be a relatively well-understood problem for most web pages.

[First Input Delay (FID)](https://web.dev/fid/) measures any delays in interactions and [seems not to be a problem for most sites](https://twitter.com/ChromeUXReport/status/1392240076583849987?s=20). Optimizing that is usually a matter of cleaning up (or reducing!) your JavaScript and is usually site-specific. That’s not to say solving issues with these two metrics are easy, but they are reasonably well-understood problems.

One reason that CLS is different is that it is measured through the **lifetime of the page** &mdash; that’s the “cumulative” part of the name! The other two Core Web Vitals stop after the main component is found on the page after load (for LCP), or for the first interaction (for FID). This means that our traditional lab-based tools, like Lighthouse, often don’t fully reflect the CLS as they calculate only the initial load CLS. In real life, a user will scroll down the page and may get more content dropping in causing more shifts.

CLS is also a bit of an artificial number that is calculated based on how much of the page is moving about and how often. While LCP and FID are measured in milliseconds, **CLS is a unitless number** output by a [complex calculation](https://web.dev/cls/#layout-shift-score). We want the page to be 0.1 or under to pass this Core Web Vital. Anything above 0.25 is seen as “poor”.

Shifts caused by user interaction are **not counted**. This is defined as within **500ms** of a specific set of user interactions though [pointer events and scroll are excluded](https://github.com/WICG/layout-instability#recent-input-exclusion). It is presumed that a user clicking on a button might expect content to appear, for example by expanding a collapsed section.

CLS is about **measuring unexpected shifts**. Scrolling should not cause content to move around if a page is built optimally, and similarly hovering over a product image to get a zoomed-in version for example should also not cause the other content to jump about. But there are of course exceptions and those sites need to consider how to react to this.

CLS is also [continually evolving](https://chromium.googlesource.com/chromium/src/+/main/docs/speed/metrics_changelog/cls.md) with tweaks and bug fixes. It has [just had a bigger change announced](https://web.dev/cls-web-tooling/) that should give some [respite to long-lived pages](https://web.dev/evolving-cls/), like Single Page Apps (SPA) and infinite scrolling pages, which many felt were unfairly penalized in CLS. Rather than accumulating shifts over the whole page time to calculate the CLS score like has been done up until now, the score will be calculated based on the largest set of shifts within a specific timeboxed window.

This means that if you have three chunks of CLS of 0.05, 0.06, and 0.04 then previously this would have been recorded as 0.15 (i.e. over the “good” limit of 0.1), whereas now will be scored as 0.06. It’s still _cumulative_ in the sense that the score may be made up of separate shifts within that time frame (i.e. if that 0.06 CLS score was caused by three separate shifts of 0.02), but it’s just not cumulative over the total lifetime of the page anymore.

Saying that, if you solve the causes of that 0.06 shift, then your CLS will then be reported as the **next largest one** (0.05) so it still is looking at all the shifts over the lifetime of the page &mdash; it’s just choosing to report only the largest one as the CLS score.

With that brief introduction to some of the methodology about CLS, let’s move on to some of the **solutions**! All of these techniques basically involve setting aside the correct amount of space before additional content is loaded &mdash; whether that is media or JavaScript-injected content, but there’s a few different options available to web developers to do this.

{{% feature-panel %}}

## Set Width And Heights On Images And iFrames

I’ve [written about this before](https://www.smashingmagazine.com/2020/03/setting-height-width-images-important-again/), but one of the easiest things you can do to reduce CLS is to ensure you have **`width` and `height` attributes set on your images**. Without them, an image will cause the subsequent content to shift to make way for it after it downloads:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6597707-d4a0-4144-b9ec-30e19f51c1a4/2-layout-shift-issues.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6597707-d4a0-4144-b9ec-30e19f51c1a4/2-layout-shift-issues.png" width="800" height="405" sizes="100vw" caption="Layout shift after image loads. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6597707-d4a0-4144-b9ec-30e19f51c1a4/2-layout-shift-issues.png'>Large preview</a>)" alt="An example layout with a title and two paragraphs, where the second paragraph has to shift down to make space for an image." >}}

This is simply a matter of changing your image markup from:

<pre><code class="language-markup">&lt;img src="hero_image.jpg" alt="..."&gt;
</code></pre>

To:

<pre><code class="language-markup">&lt;img src="hero_image.jpg" alt="..."
   width="400" height="400"&gt;
</code></pre>

You can find the dimensions of the image by opening DevTools and hovering over (or tapping through) the element.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0aeb512-8796-40da-a05f-ddee5d0cd499/6-layout-shift-issues.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0aeb512-8796-40da-a05f-ddee5d0cd499/6-layout-shift-issues.png" width="800" height="453" sizes="100vw" caption="Chrome DevTools shows the image dimensions and aspect ratios when hovering over an element. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0aeb512-8796-40da-a05f-ddee5d0cd499/6-layout-shift-issues.png'>Large preview</a>)" alt="Chrome Dev Tools screenshot showing the image, rendered size, rendered aspect ratio, intrinsic size, intrinsic aspect ratio, file size and current source." >}}

I advise using the _Intrinsic Size_ (which is the actual size of the image source) and the browser will then scale these down to the rendered size when you use CSS to change these. 

**Quick Tip**: *If, like me, you can’t remember whether it’s width and height or height and width, think of it as [X and Y coordinates](https://twitter.com/martynhoyer/status/1385495391043469313?s=20) so, like X, width is always given first.*

If you have **responsive images** and use CSS to change the image dimensions (e.g. to constrain it to a `max-width` of 100% of the screen size), then these attributes can be used to calculate the `height` &mdash; providing you remember to override this to `auto` in your CSS:

<pre><code class="language-css">img {
  max-width: 100%;
  height: auto;
}
</code></pre>

All [modern browsers support this](https://caniuse.com/mdn-html_elements_img_aspect_ratio_computed_from_attributes) now, though didn’t until recently [as covered in my article](https://www.smashingmagazine.com/2020/03/setting-height-width-images-important-again/). This also works for `<picture>` elements and `srcset` images (set the `width` and `height` on the fallback `img` element), though not yet for images of different aspect-ratios &mdash; it’s [being worked on](https://github.com/whatwg/html/issues/4968), and until then you should still set `width` and `height` as any values will be better than the `0` by `0` defaults!

This also works on **native lazy-loaded images** (though Safari doesn’t support native lazy loading by default yet).

## The New `aspect-ratio` CSS Property

The `width` and `height` technique above, to calculate the height for responsive images, can be generalized to other elements using the new CSS `aspect-ratio` property, which is now [supported by Chromium-based browsers and Firefox](https://caniuse.com/mdn-css_properties_aspect-ratio), but is also in Safari Technology Preview so hopefully that means it will be coming to the stable version soon.

So you could use it on an embedded video for example in 16:9 ratio:

<pre><code class="language-css">video {
  max-width: 100%;
  height: auto;
  aspect-ratio: 16 / 9;
}
</code></pre>

<pre><code class="language-html">&lt;video controls width="1600" height="900" poster="..."&gt;
    &lt;source src="/media/video.webm"
            type="video/webm"&gt;
    &lt;source src="/media/video.mp4"
            type="video/mp4"&gt;
    Sorry, your browser doesn't support embedded videos.
&lt;/video&gt;
</code></pre>

Interestingly, without defining the `aspect-ratio` property, browsers [will ignore the height for responsive video elements and use a default aspect-ratio of 2:1](https://github.com/whatwg/html/issues/3090), so the above is needed to avoid a layout shift here.

In the future, it should even be possible to set the `aspect-ratio` **dynamically** based on the element attributes by using `aspect-ratio: attr(width) / attr(height);` but sadly this is not supported yet.

Or you can even use `aspect-ratio` on a `<div>` element for some sort of custom control you are creating to make it responsive:

<pre><code class="language-css">#my-square-custom-control {
  max-width: 100%;
  height: auto;
  width: 500px;
  aspect-ratio: 1;
}</code></pre>

<pre><code class="language-html">&lt;div id="my-square-custom-control"&gt;&lt;/div&gt;
</code></pre>

For those browsers that don’t support `aspect-ratio` you can use the older [padding-bottom hack](https://www.smashingmagazine.com/2013/09/responsive-images-performance-problem-case-study/#the-padding-bottom-hack) but, with the simplicity of the newer `aspect-ratio` and wide support (especially once this moves from Safari Technical Preview to regular Safari), it is hard to justify that older method.

Chrome is the only browser that **feeds back CLS to Google** and it supports `aspect-ratio` meaning that will solve your CLS issues in terms of Core Web Vitals. I don’t like prioritizing the metrics over the users, but the fact that the other Chromium and Firefox browsers have this and Safari will hopefully soon, and that this is a progressive enhancement means that I would say we’re at the point where we can leave the padding-bottom hack behind and write cleaner code.

{{% ad-panel-leaderboard %}}

## Make Liberal Use Of `min-height`

For those elements that don’t need a responsive size but a fixed height instead, consider using `min-height`. This could be for a **fixed height header**, for example and we can have different headings for the different break-points using media queries as usual:

<pre><code class="language-css">header {
  min-height: 50px;
}
@media (min-width: 600px) {
  header {
    min-height: 200px;
  }
}</code></pre>

<pre><code class="language-html">&lt;header&gt;
 ...
&lt;/header&gt;</code></pre>

Of course the same applies to `min-width` for horizontally placed elements, but it’s normally the height that causes the CLS issues.

A more advanced technique for injected content and advanced CSS selectors is to target when expected content has not been inserted yet. For example, if you had the following content:

<pre><code class="language-html">&lt;div class="container"&gt;
  &lt;div class="main-content"&gt;...&lt;/div&gt;
&lt;/div&gt;
</code></pre>

And an extra `div` is inserted via JavaScript:

<pre><code class="language-html">&lt;div class="container"&gt;
  &lt;div class="additional-content"&gt;.../div&gt;
  &lt;div class="main-content"&gt;...&lt;/div&gt;
&lt;/div&gt;
</code></pre>

Then you could use the following snippet to **leave the space for additional content** when the `main-content` div is rendered initially.

<pre><code class="language-css">.main-content:first-child {
   margin-top: 20px; 
 }</code></pre>

This code will actually **create a shift** to the `main-content` element as the margin counts as part of that element so it will appear to shift when that is removed (even though it doesn’t actually move on screen). However, at least the content beneath it will not be shifted so should reduce CLS.

Alternatively, you can use the `::before` pseudo-element to add the space to **avoid the shift** on the `main-content` element as well:

<pre><code class="language-css">.main-content:first-child::before {
   content: '';
   min-height: 20px;
   display: block;
 }
</code></pre>

But in all honesty, the better solution is to have the `div` in the HTML and make use of `min-height` on that.

## Check Fallback Elements

I like to use progressive enhancement to provide a basic website, even without JavaScript where possible. Unfortunately, this caught me out recently on one site I maintain when the fallback non-JavaScript version was different than when the JavaScript kicked in.

The issue was due to the "Table of Contents" menu button in the header. Before the JavaScript kicks in this is a simple link, styled to look like the button that takes you to the Table of Contents page. Once JavaScript kicks in, it becomes a **dynamic menu** to allow you to navigate directly to whatever page you want to go to from that page.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/399118f1-cc91-4b31-ab2b-21e2b2e9c892/1-layout-shift-issues.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/399118f1-cc91-4b31-ab2b-21e2b2e9c892/1-layout-shift-issues.png" width="605" height="512" sizes="100vw" caption="A Table of Contents header component which is initially rendered as a simple link (top), and then enhanced with JavaScript to be a dynamic menu (bottom). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/399118f1-cc91-4b31-ab2b-21e2b2e9c892/1-layout-shift-issues.png'>Large preview</a>)" alt="Screenshots of two Table of Contents navigation components styled like a button. With JavaScript this opens a dynamic menu as shown in the second image." >}}

I used semantic elements and so used an anchor element  (`<a href="#table-of-contents">`)  for the fallback link but replaced that with a `<button>` for the JavaScript-driven dynamic menu. These were styled to look the same, but the fallback link was a couple of pixels smaller than the button!

This was so small, and the JavaScript usually kicked in so quickly, that I had not noticed it was off. However, Chrome noticed it when calculating the CLS and, as this was in the header, it **shifted the entire page down** a couple of pixels. So this had quite an impact on the CLS score &mdash; enough to knock all our pages into the “Needs Improvement” category.

This was an error on my part, and the fix was simply to **bring the two elements into sync** (it could also have been remediated by setting a `min-height` on the header as discussed above), but it confused me for a bit. I’m sure I’m not the only one to have made this error so be aware of how the page renders without JavaScript. Don’t think your users disable JavaScript? [All your users are non-JS while they're downloading your JS](https://twitter.com/jaffathecake/status/207096228339658752).

## Web Fonts Cause Layout Shifts

Web fonts are another common cause of CLS due to the browser initially calculating the space needed based on the fallback font, and then **recalculating** it when the web font is downloaded. Usually, the CLS is small, providing a similarly sized fallback font is used, so often they don’t cause enough of a problem to fail Core Web Vitals, but they can be jarring for users nonetheless.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0008e4a-3d9c-4a32-8cee-07a06528b2dd/4-layout-shift-issues.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0008e4a-3d9c-4a32-8cee-07a06528b2dd/4-layout-shift-issues.png" width="800" height="391" sizes="100vw" caption="Smashing Magazine article with fallback font and with full web fonts. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0008e4a-3d9c-4a32-8cee-07a06528b2dd/4-layout-shift-issues.png'>Large preview</a>)" alt="Two screenshots of a Smashing Magazine article with different fonts. The text is noticeably different sized and an extra sentence can fit in when the web fonts are used." >}}

Unfortunately even [preloading](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/) the webfonts won’t help here as, while that reduces the time the fallback fonts are used for (so is good for loading performance &mdash; LCP), it **still takes time to fetch them**, and so the fallbacks will still be used by the browser in most cases so doesn’t avoid CLS. Saying that, if you know a web font is needed on the next page (say you’re on a login page and know the next page uses a special font) then you can [prefetch](https://www.smashingmagazine.com/2019/04/optimization-performance-resource-hints/#prefetching-the-next-page) them.

To avoid **font-induced layout shifts** altogether, we could of course not use web fonts at all &mdash; including using system fonts instead, or using `font-display: optional` to not use them if not downloaded in time for the initial render. But neither of those are very satisfactory, to be honest.

Another option is to ensure the sections are **appropriately sized** (e.g. with `min-height`) so while the text in them may shift a bit, the content below it won’t be pushed down even when this happens. For example, setting a `min-height` on the `<h1>` element could prevent the whole article from shifting down if slightly taller fonts load in &mdash; providing the different fonts don’t cause a different number of lines. This will reduce the impact of the shifts, however, for many use-cases (e.g. generic paragraphs) it will be difficult to generalize a minimum height.

What I’m most excited about to solve this issue, are the [new CSS Font Descriptors](https://drafts.csswg.org/css-fonts-5/) which allow you to more easily adjust fallback fonts in CSS:

<pre><code class="language-css">@font-face {
  font-family: 'Lato';
  src: url('/static/fonts/Lato.woff2') format('woff2');
  font-weight: 400;
}

@font-face {
    font-family: "Lato-fallback";
    size-adjust: 97.38%;
    ascent-override: 99%;
    src: local("Arial");
}

h1 {
    font-family: Lato, Lato-fallback, sans-serif;
}
</code></pre>

Prior to these, adjusting the fallback font required using the Font Loading API in JavaScript which was more complicated, but this option due out very soon may finally give us an easier solution that is more likely to gain traction. See my [previous article on this subject for](https://www.smashingmagazine.com/2021/05/reduce-font-loading-impact-css-descriptors/) more details on this upcoming innovation and more resources on that.

## Initial Templates For Client-side Rendered Pages

Many client-side rendered pages, or Single Page Apps, render an initial basic page using just HTML and CSS, and then “hydrate” the template after the JavaScript downloads and executes.

It’s easy for these initial templates to get out of sync with the JavaScript version as new components and features are added to the app in the JavaScript but not added to the initial HTML template which is rendered first. This then causes CLS when these components are injected by JavaScript.

So **review all your initial templates** to ensure they are still good initial placeholders. And if the initial template consists of empty `<div>`s, then use the techniques above to ensure they are sized appropriately to try to avoid any shifts.

Additionally, the initial `div` which is injected with the app should have a `min-height` to avoid it being rendered with 0 height initially before the initial template is even inserted.

<pre><code class="language-html">&lt;div id="app" style="min-height:900px;"&gt;&lt;/div&gt;
</code></pre>

As long as the `min-height` is **larger than most viewports**, this should avoid any CLS for the website footer, for example. CLS is only measured when it’s in the viewport and so impacts the user. By default, an empty `div` has a height of 0px, so give it a `min-height` that is closer to what the actual height will be when the app loads.

{{% ad-panel-leaderboard %}}

## Ensure User Interactions Complete Within 500ms

User interactions that cause content to shift are excluded from CLS scores. These are restricted to 500 ms after the interaction. So if you click on a button, and do some complex processing that takes over 500 ms and then render some new content, then your CLS score is going to suffer.

You can see if the **shift was excluded in Chrome DevTools** by using the _Performance tab_ to record the page and then finding the shifts as shown in the next screenshot. Open DevTools go to the very intimidating (but very useful once you get a hang of it!) *Performance* tab and then click on the record button in the top left (circled on the image below) and interact with your page, and stop recording once complete.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c83715ac-5c8f-48e0-aa99-e3a77069323a/3-layout-shift-issues.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c83715ac-5c8f-48e0-aa99-e3a77069323a/3-layout-shift-issues.png" width="800" height="868" sizes="100vw" caption="Using the Performance tab in Chrome Dev Tools to see if shifts are excluded due to recent input. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c83715ac-5c8f-48e0-aa99-e3a77069323a/3-layout-shift-issues.png'>Large preview</a>)" alt="Screenshot of Chrome Dev Tools with a shift selected and the Summary of this shows that it had recent input and so the shift is not included in the Cumulative Score." >}}

You will see a filmstrip of the page in which I loaded some of the comments on another Smashing Magazine article so in the part I’ve circled, you can just about make out the comments loading and the red footer being shifted down offscreen. Further down the *Performance* tab, under the _Experience_ line, Chrome will put a reddish-pinkish box for each shift and when you click on that you will get more detail in the _Summary_ tab below.

Here you can see that we got a **massive 0.3359 score** &mdash; well past the 0.1 threshold we’re aiming to be under, but the _Cumulative score_ has not included this, because _Had recent input_ is set to Uses.

Ensuring interactions only shift content within 500 ms borders on what First Input Delay attempts to measure, but there are cases when the user may see that the input had an effect (e.g. a loading spinner is shown) so FID is good, but the content may not be added to the page until after the 500 ms limit, so CLS is bad.

Ideally, the whole interaction will be finished within 500ms, but you can do some things to **set aside the necessary space** using the techniques above while that processing is going on so that if it does take more than the magic 500 ms, then you’ve already handled the shift and so will not be penalized for it. This is especially useful when fetching content from the network which could be variable and outside your control.

Other items to watch out for are **animations** that take longer than 500ms and so can impact CLS. While this might seem a bit restrictive, the aim of CLS isn’t to limit the “fun”, but to set reasonable expectations of user experience and I don’t think it’s unrealistic to expect these to take 500ms or under. But if you disagree, or have a use case they might not have considered, then the Chrome team is [open to feedback on this](https://groups.google.com/g/web-vitals-feedback).

## Synchronous JavaScript

The final technique I’m going to discuss is a little controversial as it goes against well-known web performance advice, but it can be the only method in certain situations. Basically, if you have content that you know is going to cause shifts, then one solution to avoid the shifts is to not render it until it’s settled down!

The below HTML will hide the `div` initially, then load some render-blocking JavaScript to populate the `div`, then unhide it. As the JavaScript is render-blocking nothing below this will be rendered (including the second `style` block to unhide it) and so no shifts will be incurred.

<pre><code class="language-html">&lt;style&gt;
.cls-inducing-div {
    display: none;
}
&lt;/style&gt;

&lt;div class="cls-inducing-div"&gt;&lt;/div&gt;
&lt;script&gt;
...
&lt;/script&gt;

&lt;style&gt;
.cls-inducing-div {
    display: block;
}
&lt;/style&gt;
</code></pre>

It is important to **inline the CSS in the HTML** with this technique, so it is applied in order. The alternative is to unhide the content with JavaScript itself, but what I like about the above technique is that it still unhides the content even if the JavaScript fails or is turned off by the browser.

This technique can also even be applied with external JavaScript, but this will cause more delay than an inline `script` as the external JavaScript is requested and downloaded. That delay can be minimized by preloading the JavaScript resource so it’s available quicker once the parser reaches that section of code:

<pre><code class="language-html">&lt;head&gt;
...
&lt;link rel="preload" href="cls-inducing-javascript.js" as="script"&gt;
...
&lt;/head&gt;
&lt;body&gt;
...
&lt;style&gt;
.cls-inducing-div {
    display: none;
}
&lt;/style&gt;
&lt;div class="cls-inducing-div"&gt;&lt;/div&gt;
&lt;script src="cls-inducing-javascript.js"&gt;&lt;/script&gt;
&lt;style&gt;
.cls-inducing-div {
    display: block;
}
&lt;/style&gt;
...
&lt;/body&gt;
</code></pre>

Now, as I say, this I’m sure will make some web performance people cringe, as advice is to use `async, defer` or the newer `type="module"` (which are `defer`-ed by default) on JavaScript specifically to _avoid blocking render_, whereas we are doing the opposite here! However, if content cannot be predetermined and it is going to cause jarring shifts, then there is little point in rendering it early.

I used this technique for a **cookie banner** that loaded at the top of the page and shifted content downwards:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c37b4adc-764b-4f9c-bfc6-ed98e28e83ed/5-layout-shift-issues.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c37b4adc-764b-4f9c-bfc6-ed98e28e83ed/5-layout-shift-issues.png" width="800" height="405" sizes="100vw" caption="A top of page cookie notice or other banner can shift content down. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c37b4adc-764b-4f9c-bfc6-ed98e28e83ed/5-layout-shift-issues.png'>Large preview</a>)" alt="A screenshot of a web page, where the content is shifted down when a cookie banner is added to the top of the page." >}}

This required reading a cookie to see whether to display the cookie banner or not and, while that could be completed server-side, this was a static site with no ability to dynamically alter the returned HTML.

Cookie banners can be implemented in different ways to avoid CLS. For example by having them at the bottom of the page, or overlaying them on top of the content, rather than shifting the content down. We preferred to keep the content at the top of the page, so had to use this technique to avoid the shifts. There are various other alerts and banners that site owners may prefer to be at the top of the page for various reasons.

I also used this technique on another page where **JavaScript moves content around** into “main” and “aside” columns (for reasons I won’t go into, it was not possible to construct this properly in HTML server-side). Again hiding the content, until the JavaScript had rearranged the content, and only then showing it, avoided the CLS issues that were dragging these pages' CLS score down. And again the content is automatically unhidden even if the JavaScript doesn’t run for some reason and the unshifted content is shown.

Using this technique can impact other metrics (particularly LCP and also First Contentful Paint) as you are delaying rendering, and also potentially blocking browsers' look ahead preloader, but it is another tool to consider for those cases where no other option exists.

## Conclusion

Cumulative Layout Shift is caused by content changing dimensions, or new content being injected into the page by late running JavaScript. In this post, we’ve discussed various tips and tricks to avoid this. I’m glad the spotlight the Core Web Vitals have shone on this irritating issue &mdash; for too long we web developers (and I definitely include myself in this) have ignored this problem.

Cleaning up my own websites has led to a better experience for all visitors. I encourage you to **look at your CLS issues too**, and hopefully some of these tips will be useful when you do. Who knows, you may even manage to get down to the elusive [0 CLS score](https://twitter.com/TimVereecke/status/1382456055519703043?s=20) for all your pages!

### More Resources

*   [Core Web Vitals articles](https://www.smashingmagazine.com/category/core-web-vitals) here on Smashing Magazine, including my own on [Setting Width and Heights on Images](https://www.smashingmagazine.com/2020/03/setting-height-width-images-important-again/), [Measuring Core Web Vitals](https://www.smashingmagazine.com/2021/04/complete-guide-measure-core-web-vitals/), and [CSS Font Descriptors](https://www.smashingmagazine.com/2021/05/reduce-font-loading-impact-css-descriptors/).
*   Google’s [Core Web Vitals documentation](https://web.dev/vitals/) including their page on [CLS](https://web.dev/cls/).
*   More [details on the recent change to CLS](https://web.dev/evolving-cls/) and then this change [started updating in various Google’s tools](https://web.dev/cls-web-tooling/).
*   The [CLS Changelog](https://chromium.googlesource.com/chromium/src/+/refs/heads/main/docs/speed/metrics_changelog/cls.md) detailing changes in each version of Chrome.
*   [The Almost-Complete Guide to Cumulative Layout Shift](https://jessbpeck.com/posts/completecls/) by [Jess Peck](https://twitter.com/jessthebp).
*   [Cumulative Layout Shift: Measure and Avoid Visual Instability](https://calibreapp.com/blog/cumulative-layout-shift) by [Karolina Szczur](https://twitter.com/fox).
*   [A Layout Shift GIF Generator](https://defaced.dev/tools/layout-shift-gif-generator/) to help generate shareable demonstrations of CLS.

{{< signature "vf, il" >}}

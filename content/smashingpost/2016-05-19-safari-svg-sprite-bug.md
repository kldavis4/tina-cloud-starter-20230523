---
title: The Safari Problem With SVG Sprites (Now Fixed)
slug: safari-svg-sprite-bug
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc846e8f-f431-4d38-9446-76427f3360e1/svg-problem-safari-preview-opt.png
date: 2016-05-19T17:06:21.000Z
author: nicobruenjes
description: >-
  **Update (19.05.2016)**: _The bug was just fixed by Antti Koivisto and has
  landed in the current update of iOS (9.3.2) and Safari for OS X 9.1.1
  (11601.6.17). When a user visits a site using a SVG sprite in a browser with
  an empty cache, the sprite is cached and will not be loaded multiple times any
  longer. You'll find more [details
  here](https://nicobruenjes.de/2016/05/safari-svg-sprite-bug-fixed/) (in
  German), and [Sven Wolfermann's
  results](https://twitter.com/maddesigns/status/732835070696927232) before and
  after the iOS update._

  Using external SVG sprite maps to deliver lossless scalable vector images is
  widely used in responsive web design today and well-supported by tools like
  _svg4everybody_.

  At German newspaper _Zeit Online_, we embraced this technique quite a lot.
  However, we recently changed this workflow back to completely inlining the SVG
  into the HTML owing to a bug in Apple's Safari browsers (mobile since iOS 9.3,
  in Mac OS X since Safari 9.1) – the same way [GitHub is doing with its
  octicons](https://github.com/blog/2112-delivering-octicons-with-svg).
categories:
  - Coding
  - Sprites
  - SVG
---
<strong>Update (19.05.2016)</strong>: <em>The bug was just fixed by Antti Koivisto and has landed in the current update of iOS (9.3.2) and Safari for OS X 9.1.1 (11601.6.17). When a user visits a site using a SVG sprite in a browser with an empty cache, the sprite is cached and will not be loaded multiple times any longer. You'll find more <a href="https://nicobruenjes.de/2016/05/safari-svg-sprite-bug-fixed/">details here</a> (in German), and <a href="https://twitter.com/maddesigns/status/732835070696927232">Sven Wolfermann's results</a> before and after the iOS update.</em>

<figure><a href="https://twitter.com/maddesigns/status/732835070696927232"><img title="Sven Wolfermann's tweet" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/336bcc48-5781-4973-ad73-72afc79e92a4/svg-bug-fixed-preview-opt.png" alt="Sven Wolfermann's tweet" width="500" height="" /></a></figure>

Using external SVG sprite maps to deliver lossless scalable vector images is widely used in responsive web design today and well-supported by tools like <a href="https://github.com/jonathantneal/svg4everybody" rel="nofollow">svg4everybody</a>.

At German newspaper <em>Zeit Online</em>, we embraced this technique quite a lot. However, we recently changed this workflow back to completely inlining the SVG into the HTML owing to a bug in Apple's Safari browsers (mobile since iOS 9.3, in Mac OS X since Safari 9.1) – the same way <a href="https://github.com/blog/2112-delivering-octicons-with-svg" rel="nofollow">GitHub is doing with its octicons</a>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Chrome, Firefox, Safari, Opera, Edge? Browser Alternatives](https://www.smashingmagazine.com/2015/09/chrome-firefox-safari-opera-edge-impressive-web-browser-alternatives/)
*   [Rethinking Responsive SVG](https://www.smashingmagazine.com/2014/03/rethinking-responsive-svg/)
*   [Testing Mobile: Emulators, Simulators And Remote Debugging](https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/)
*   [Resolution Independence With SVG](https://www.smashingmagazine.com/2012/01/resolution-independence-with-svg/)

{{% feature-panel %}}

## The Problem

When using an SVG sprite map, you’re combining all your SVG icons into one file and loading it from an external source (typically through an external CDN). If you need an icon in the web page, it will be referenced by a fragment identifier in a <code>use</code> tag, like this:

<pre><code class="language-markup">
&lt;svg class="svg-symbol logo_bar__brand-logo" role="img" aria-labelledby="title"&gt;
   &lt;use xmlns:xlink="https://www.w3.org/1999/xlink" xlink:href="icons.svg#svg-logo-zon-black"&gt;&lt;/use&gt;
&lt;/svg&gt;
</code></pre>

The idea is to load the file only once, store it in the browser cache, and reference the icons when they are needed. The bug, which is demonstrated on <a href="https://codecandies.github.io/safari-sprite-bug/external-with-symbols.html">this test case</a> thwarts this approach entirely: every time an icon is used in a web page, the whole sprite file is loaded again (load the test case and watch the developer tools). Our homepage suddenly weighed 17MB on an iPhone with iOS 9.3, which is a problem for the user's data plan and for the web page's server too.</p>

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75bef1d0-ac6e-4156-92a2-a6b666822eb5/svg-problem-safari-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc846e8f-f431-4d38-9446-76427f3360e1/svg-problem-safari-preview-opt.png" alt="SVG Bug" width="600" height="395" /></a><figcaption>The SVG has been downloaded multiple times.</figcaption></figure>

Indeed, it was the server monitoring that first led us to the bug. A fully updated iPhone loaded our (admittedly too big) SVG icon file, which was clearly identifiable in the server logs. Internally, a bug was filed and assigned to the front-end team, to check which component of the stack was downloading the icon file again and again. The browser string in the server logs directly identified iOS 9.3 versions of Safari, and some quick tests with the developer toolbar (and <a href="https://www.charlesproxy.com/">Charles proxy software</a> to sort out possible mismeasurement) clearly showed that <strong>if we had 20 icons on a page, the icons SVG was downloaded 20 times</strong> if the cache was cold. We also found that Safari 9.1.1 on Mac OS X was affected. And we could see that prior versions of the browser did not contain the bug, which showed that we were hit by a browser bug, not a problem in our code. I filed a bug in Apple's bug tracker and over in the svg4everybody repository. When I went to add it in the WebKit bug tracker, it was already filed.</p>

## Approaching A Solution

Mobile traffic is crucial for a news page, and having such a big homepage is a big problem for us and the user. We started to look for alternative approaches. We always made sure that our code followed standards, was progressively enhanced and as accessible as possible.

One solution could have been to <a href="https://css-tricks.com/ajaxing-svg-sprite/">Ajax our SVG file</a>, but that means you only progressively enhance icons that are not really required for a website to look good, and which have a rather decorative character. We use icons as standalone items, like a star to click on for rating items. These cannot use textual user ratings as a base to enhance from because it would lead to an inconsistent layout.

Furthermore, we have some logo SVGs that we crucially need to display when JavaScript is disabled, so for these Ajax was never an alternative. Also, the bug seems not to be <em>feature-detectable</em> and we do not use any browser detection, so we were looking for a cross-browser approach all the time.

In the end, the best approach might have been to split the icons by purpose and use different ways to load and display them. As we have three different use cases for icons, the perfect solution might be using different techniques on each. The large logo files which are critical to layout need to be inlined, as they are part of the content. This might also be the case for clickable standalone icons, where a text replacement would disturb the layout. As these icons are used in several place on a page, it would be a good idea to inline a sprite SVG file for these icons in the document's <code>head</code>, which would be a bit of micro-improvement, because these files typically are just bytes in size. At least the rest of the decorative icons can use an Ajaxified external sprite file.

We decided that, given the bug will be repaired sometime soon, this approach would be too complicated, and we wanted to start off with a simpler solution. We switched to completely inlining all SVG. We'll lose the caching effect, but on the other hand win back browser compatibility (from IE9 and up) and could ditch the polyfills and the production of fallback PNG files. On the first load, we'd also spare one or two requests.

## Patch On The Way

Meanwhile the WebKit team has picked up <a href="https://bugs.webkit.org/show_bug.cgi?id=156368">the bug</a> and it's marked as fixed and resolved, hopefully soon enough for the fix to land in the next version of Safari — probably in fall this year.</p>

### Final Notes

*   [Initial article in my blog](https://nicobruenjes.de/2016/04/safari-svg-sprite-bug/) and an [article about our solution](https://nicobruenjes.de/2016/04/svg-yeah-you-know-me/), both in German.
*   [Screencast by Martin Wolf demonstrating the bug](https://www.youtube.com/watch?v=OAbmDlnq1UE), also in German.

What do you think about this approach? What other ways would you go to deliver SVG sprites? Let us know in the comments! Thank you!

{{< signature "ms, ml, og, il" >}}


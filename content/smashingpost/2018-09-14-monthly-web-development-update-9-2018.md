---
title: 'Monthly Web Development Update 9/2018: Native Lazy Loading And Imaginary Work'
slug: monthly-web-development-update-9-2018
author: anselm-hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f34267fa-124c-47b3-b02f-9f1c96bea518/imaginary-work-opt.png
date: 2018-09-14T14:50:19+02:00
summary: >-
  The web is evolving at such a fast pace that it can be hard to stay on top of things. To give you an overview of what happened in the web dev world in the past few weeks, Anselm once again compiled his monthly update.
description: >-
  The web is evolving at such a fast pace that it can be hard to stay on top of things. To give you an overview of what happened in the web dev world in the past few weeks, Anselm once again compiled his monthly update.
categories:
  - Web Development Reading List
---
<p>It&#8217;s an interesting concept to <strong>compare JavaScript with CO2</strong> and yet a very valid one. Alex Russel who works for the Chrome team and has a lot of insights into the current state of the web says that using too much JavaScript or using it exclusively (without progressive enhancement/graceful degradation) will have the same effect as too much CO2 for the ecosystem on planet Earth &mdash; the ecosystem will fall apart. And just like we need a certain amount of CO2 to live, we need JavaScript on the web. It&#8217;s that fine line that makes the difference &mdash; the line between not too much and none at all.</p>
<p>I feel that with the native browser APIs that we have these days we have a fantastic opportunity to <strong>build great web services without bloating</strong> them too much and without relying only on JavaScript. We can enhance native elements with the Custom Elements API easily via ES6 Classes, with so little code that it seems ridiculous to build all that on your own in a third-party framework. Coincidentally, the Github engineering team published an article about <a href="https://githubengineering.com/removing-jquery-from-github-frontend/">how they dropped jQuery entirely</a> and what they now use instead: native JavaScript and small, lean code that is progressively enhancing their platform. Less code, better maintainability, and more stability.</p>
## News
<ul>
<li><a href="https://blog.chromium.org/2018/09/chrome-70-beta-shape-detection-web.html">Chrome 70 is now in beta</a>, bringing shape detection as an origin trial that allows us to perform QR code reading, face detection, and text recognition in images. The Web Authentication API got some updates, too, and <code>referrerpolicy</code> support was added to <code>&lt;script&gt;</code> elements. This version will also deprecate Custom Elements v0, HTML Imports, and Shadow DOM v0.</li>
<li>Finally, <a href="https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/62">with Firefox 62</a>, Mozilla ships <code>::selection</code> instead of <code>:-moz-selection</code>. They also implemented <code>flat()</code>, and <code>flatMap()</code> for JavaScript arrays and developers get a new Shape Path Editor.</li>
<li><a href="https://developers.google.com/web/updates/2018/09/nic69">Chrome 69 is out</a> and brings us CSS Scroll Snap Points, the CSS <code>viewport-fit</code> property for cutout-displays like the one of iPhone X, and the Web Locks API which allows scripts running in one tab or worker to asynchronously acquire a lock, hold it while work is performed, and then release it. The update also comes with CSS conic gradient support, <code>toggleAttribute()</code> (which is similar to the <code>classList.toggle()</code> method but for attributes), and <code>flat()</code> and <code>flatMap()</code> for arrays. Unfortunately, this release changed how the browser displays the URL, and <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=881410">it seems that people consider it a security bug</a>. Let&#8217;s see how that will evolve.</li>
<li>With <a href="https://hacks.mozilla.org/2018/09/variable-fonts-arrive-in-firefox-62/">Firefox 62 supporting variable web fonts</a>, we finally have support in all major browsers and can use it widely now to improve performance, be more creative with typography, and reduce data traffic drastically.</li>
<li>Manuel Rego Casasnovas wrote about <a href="https://blogs.igalia.com/mrego/2018/08/10/changes-on-css-grid-layout-in-percentages-and-indefinite-height/">recent changes on CSS Grid Layout in percentages and indefinite height</a> in the Chrome browser.</li>
<li>Anyone who isn&#8217;t an expert would be hard-pressed to explain how tracking on the internet actually works. That&#8217;s why Firefox now changes their default settings and  <a href="https://blog.mozilla.org/futurereleases/2018/08/30/changing-our-approach-to-anti-tracking/">enforces tracking blocking in their browser by default</a>.</li>
<li><a href="https://kinsta.com/blog/php-7-3/">PHP7.3 is coming soon</a> with new Heredoc and Nowdoc syntax, trailing commas in function calls, <code>is_countable()</code>, <code>array_key_first()</code>, <code>array_key_last()</code>, and Argon2 password hash enhancements.</li>
</ul>
{{% feature-panel %}}
## General
<ul>
<li>Alex Russell&#8217;s &#8220;<a href="https://infrequently.org/2018/09/the-developer-experience-bait-and-switch/">The &#8216;Developer Experience&#8217; Bait-and-Switch</a>&#8221; is a great piece that explains the toxic environments we currently build for the web and why JavaScript can be compared to CO2 &mdash; both are needed in small portions, but if there&#8217;s too much of it, it&#8217;ll put the entire ecosystem (the web) at risk. A thoughtful article that I recommend everyone here to read, share, and remember.</li>
<li>As Alexa, Cortana, Siri, and even customer support chat bots become the norm we have to start considering not only how our content looks but <a href="https://alistapart.com/article/conversational-semantics">how it could sound</a>. We can &mdash; and should &mdash; use HTML and ARIA to make our content structured, sensible, and most importantly, meaningful.</li>
</ul>
## Web Performance
<ul>
<li>The upcoming PostgreSQL 11 has some interesting performance improvements. Dimitri Fontaine <a href="https://www.citusdata.com/blog/2018/09/11/postgresql-11-just-in-time/">shares what difference they can make</a>.</li>
<li>Ben Schwarz shares new approaches to <a href="https://css-tricks.com/a-native-lazy-load-for-the-web-platform/">native lazy load for the web</a> that could become a reality soon.</li>
</ul>
## Security
<ul>
<li>Nightwatch Cybersecurity published a <a href="https://wwws.nightwatchcybersecurity.com/2018/08/29/sensitive-data-exposure-via-wifi-broadcasts-in-android-os-cve-2018-9489/">security vulnerability in Android</a> that exposes information about the user&#8217;s device to all applications running on it. This seems to include the WiFi network name, BSSID, local IP addresses, DNS server information, and the MAC address &mdash; all in all quite a lot of private information that allows people to track individual Android devices. Unfortunately, all Android OS versions including forks (except for Android P/9 where a fix was provided) seem to be affected with no plan to fix older versions.</li>
</ul>
{{% ad-panel-leaderboard %}}
## CSS
<ul>
<li>Chen Hui Jing explains <a href="https://www.chenhuijing.com/blog/customise-radios-without-compromising-accessibility/#%F0%9F%91%9F">how to customize radio buttons</a> without compromising their accessibility.</li>
<li>CSS Shapes have quite some history already. Brought to the web early by an initiative of the Adobe Web team, browser vendors removed the implementations soon again, and are now slowly coming back with iterated, improved specifications and implementations. <a href="https://www.smashingmagazine.com/2018/09/css-shapes/">Rachel Andrew shares how to implement CSS Shapes</a>.</li>
<li>Sara Soueidan wrote down the reasons she <a href="https://www.sarasoueidan.com/blog/hex-rgb-to-hsl/">switched from defining CSS colors as HEX or RGB to HSL</a> and what the benefits are.</li>
<li>With the web&#8217;s growth come new features to better accommodate its new form factors and use cases. One feature I&#8217;m excited about is the <a href="https://css-tricks.com/the-possibilities-of-the-color-adjust-property/"><code>color-adjust</code> property</a>, proposed in CSS Color Module Level 4. It is an acknowledgment that the web will continue to show up on devices that have less-than-stellar displays.</li>
</ul>
<figure><a href="https://www.sarasoueidan.com/blog/hex-rgb-to-hsl/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6059e98a-f316-4b3a-948b-0d35ed2b2d25/hex-to-hsl-opt.png" width="800" height="564" alt="Color harmonies" /></a><figcaption>Creating color harmonies <a href="https://www.sarasoueidan.com/blog/hex-rgb-to-hsl/">becomes a piece of cake with HSL</a>. (<a href="https://www.sarasoueidan.com/blog/hex-rgb-to-hsl/">Image credit</a>)</figcaption></figure>
## HTML &amp; SVG
<ul>
<li>Stefan Judis read what the Mozilla documentation has to say about <code>input</code> elements and <a href="https://www.stefanjudis.com/blog/three-input-element-properties-that-i-discovered-while-reading-mdn/">discovered a couple of interesting things</a> that could be very useful for your next project.</li>
</ul>
## JavaScript
<ul>
<li>Nolan Lawson <a href="https://nolanlawson.com/2018/09/01/a-tour-of-javascript-timers-on-the-web/">compares the different ways of using timers in JavaScript</a> and when to use which.</li>
<li><a href="https://github.com/sindresorhus/ky">ky</a> is a tiny and elegant HTTP client based on the browser Fetch API.</li>
<li>Ankur Anand wrote an article about <a href="https://medium.com/@ankur_anand/the-terrible-performance-cost-of-cors-api-on-the-single-page-application-spa-6fcf71e50147">the terrible performance cost of CORS requests in single-page applications</a>.</li>
<li>Adrian Roselli shares how we can <a href="https://adrianroselli.com/2018/09/links-list-for-print-styles.html">build link lists at the end of a page for print styles</a>.</li>
<li><a href="https://babeljs.io/blog/2018/08/27/7.0.0">Babel 7</a> is out. It&#8217;s faster, has more options, and supports JSX Fragments and TypeScript.</li>
<li>Auto-resizing <code>&lt;textarea&gt;</code>s is a very useful way to improve the user experience for people writing content for your site or service. I wrote a blog post about how to <a href="https://colloq.io/blog/auto-resizing-textareas-with-ecmascript-6">auto-resize form elements with a short ECMAScript 6 class</a>.</li>
</ul>
## Accessibility
<ul>
<li>Ethan Marcotte <a href="https://ethanmarcotte.com/wrote/accessibility-is-not-a-feature/">reflects on what accessibility means</a> and realizes that it&#8217;s not about making a website compatible with some assistive technology or software but about making it usable for everyone who wants to access it, regardless of the technology. This is a huge difference because his approach includes people who have difficulties reading a website even though they use the same browser and the same laptop as you. Maybe they are in bright sunlight, have difficulties with small text, or get distracted by bright colors or animated elements.</li>
<li>Eric Bailey emphasizes <a href="https://www.smashingmagazine.com/2018/09/importance-manual-accessibility-testing/">how important it is to manually test for accessibility</a>.</li>
<li>Scott O&#8217;Hara shares a <a href="https://scottaohara.github.io/a11y_breadcrumbs/">breadcrumb navigation using <code>aria-label</code></a> to provide an accessible name and <code>aria-current</code> to indicate the currently active link.</li>
</ul>
{{% ad-panel-leaderboard %}}
## Work &amp; Life
<ul>
<li>Ryan Singer contemplates <a href="https://m.signalvnoise.com/real-work-vs-imaginary-work-8bdb84a7d1da">the difficulty of planning a project with &#8216;imaginary work&#8217;</a> and why it&#8217;s so important to test first how hard something will be to integrate before planning it on the roadmap.</li>
</ul>
<figure><a href="https://m.signalvnoise.com/real-work-vs-imaginary-work-8bdb84a7d1da"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f34267fa-124c-47b3-b02f-9f1c96bea518/imaginary-work-opt.png" width="800" height="376" alt="Real Work vs. Imaginary Work" /></a><figcaption>We all have been there before: Imagining a solution in your head and implementing it are <a href="https://m.signalvnoise.com/real-work-vs-imaginary-work-8bdb84a7d1da">two entirely different things</a>. (<a href="https://m.signalvnoise.com/real-work-vs-imaginary-work-8bdb84a7d1da">Image credit</a>)</figcaption></figure>
## Going Beyond&hellip;
<ul>
<li>I love the concept of doodling, and even though I don&#8217;t do it regularly, it always fascinates me. <a href="https://www.doodleaddicts.com/">Doodle Addicts</a> is a platform that collects doodles from people all around the world. A nice gallery to get inspiration from.</li>
<li>Jonny Brooks-Bartlett wrote an interesting article on <a href="https://towardsdatascience.com/why-so-many-data-scientists-are-leaving-their-jobs-a1f0329d7ea4">why so many data scientists are leaving their jobs</a>. The job might sound quite interesting and like a good bet these days, but often expectations don&#8217;t match reality and politics and ethical decisions are extremely difficult.</li>
<li>Marco Lambertini explains <a href="https://www.weforum.org/agenda/2018/08/here-s-how-technology-can-help-us-save-the-planet">how technology can help us save the planet</a>, but more than anything we need to learn to value nature and its resources.</li>
<li>An interesting discussion was raised this week by a very well-known Open Source contributor <a href="https://motherboard.vice.com/en_us/article/8xbynx/major-open-source-project-revokes-access-to-companies-that-work-with-ice">who tried to change the license of one of their projects</a> in order to prevent companies who support the U.S. ICE institution from using their software. The change was quickly reverted after it was revealed that it wasn&#8217;t legally enforceable. However, the entire topic (which <a href="https://wdrl.info/archive/238/raisely-jwl-just-world-license-a-licence-for-using-software-for-good">comes up way more often lately</a>) shows that more and more people think about the impact of their work. They don&#8217;t want it to be used for bad, but for good. And while the idea of open, non-restricted source is desirable, it&#8217;s only if people use it to support human rights and for improving lives. I&#8217;m curious about new solutions that could ensure this; maybe we&#8217;ll see more terms of service for open-source projects soon (which would then be legally binding but may prevent free open-source projects from using them).</li>
</ul>
{{< signature "cm" >}}
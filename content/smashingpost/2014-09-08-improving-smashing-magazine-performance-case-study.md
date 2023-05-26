---
title: 'Improving Smashing Magazine’s Web Performance: A Case Study'
slug: improving-smashing-magazine-performance-case-study
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45f70827-c274-4d23-acb8-bcec4c819cf3/smashing-on-mobile-99-opt.png
date: 2014-09-08T20:13:38.000Z
author: vitaly-friedman
summary: >-
  Today, Smashing Magazine turns eight years old. Eight years is a long time on the web, yet for us it really doesn’t feel like a long journey at all. Things have changed, evolved and moved on, and we gratefully take on new challenges one at a time.
description: >-
  Today, Smashing Magazine turns eight years old. Eight years is a long time on the web, yet for us it really doesn’t feel like a long journey at all.
categories:
  - Coding
  - CSS
  - Performance
  - Responsive Design
---
 To mark this special little day, we’d love to share a few things that we’ve learned over the last years about the performance challenges of this very website and about the work we’ve done recently. If you want to craft a fast responsive website, you might find a few interesting nuggets worth considering.

 Improvement is a matter of steady, ongoing iteration. When we redesigned Smashing Magazine back in 2012, our main goal was to establish trustworthy branding that would reflect the ambitious editorial direction of the magazine. We did that primarily by focusing on crafting a delightful reading experience. Over the years, our focus hasn’t changed a bit; however, that very asset that helped to establish our branding turned into a major <strong>performance bottleneck</strong>.</p>

## Good Old-Fashioned Website Decay

Looking back at the early days of our redesign, some of our decisions seem to be quick’n’dirty fixes rather than sound long-term solutions. Our advertising constraints pushed us to compromises. Legacy browsers drove us to dependencies on (relatively) heavy JavaScript libraries. Our technical infrastructure led us to heavily customized WordPress plugins and complex PHP logic. With every new feature added, our technical debt grew, and our style sheets, markup and JavaScript weren’t getting any leaner.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Perceived Performance](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/)
*   [Perception Management](https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/)
*   [Preload: What is it good for?](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/)
*   [Getting Ready For HTTP/2](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [Front-End Performance Checklist 2017](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)

{{% feature-panel %}}

Sound familiar? Admittedly, responsive web design as a technique often gets a <strong>pretty bad rap</strong> for bloating websites and making them difficult to maintain. (Not that non-responsive websites are any different, but that’s another story.) In practice, all assets on a responsive website will show up pretty much everywhere: be it a slow smartphone, a quirky tablet or a fancy laptop with a Retina screen. And because media queries merely provide the ability to <em>respond</em> to screen dimensions &mdash; and do not, rather, have a more local, self-contained scope &mdash; adding a new feature and adjusting the reading experience potentially means going through each and every media query to prevent inconsistencies and fix layout issues.</p>

### “Mobile First” Means “Always Mobile First”

When it comes to setting priorities for the content and functionality on a website, “mobile first” is one of those difficult yet incredibly powerful constraints that help you focus on what really matters, and identify critical components of your website. We discovered that designing mobile first is one thing; building mobile first is an entirely different story. In our case, both the design and development phases were heavily mobile first, which helped us to focus tightly on the content and its presentation. But while the design process was quite straightforward, implementation proved to be quite difficult.

Because the entire website was built mobile first, we quickly realized that adding or changing components on the page would entail going through the mobile-first approach for every single (minor and major) design decision. We’d design a new component in a mobile view first, and then design an “extended” view for the situations when more space is available. Often that meant adjusting media queries with every single change, and more often it meant adding new stuff to style sheets and to the markup to address new issues that came up.

<a href="https://timkadlec.com/2012/01/work-to-be-done/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c71991c7-f1b6-4998-b4d8-61f17b6b7ce8/tim-kadlec-article-opt.jpg" alt="Tim Kadlec’s article about SmashingMag’s performance" width="500" height="355" /></a><br>
<em>Shortly after the new SmashingMag redesign went live, we ran into performance issues. An <a href="https://timkadlec.com/2012/01/work-to-be-done/">article by Tim Kadlec from 2012</a> shows just that.</em>

We found ourselves trapped: development and maintenance were taking a lot of time, the code base was full of minor and major fixes, and the infrastructure was becoming too slow. We ended up with a code base that had become bloated before the redesign was even released &mdash; <a href="https://timkadlec.com/2012/01/work-to-be-done/">very bloated</a>, in fact.</p>

## Performance Issues

In mid-2013, our home page weighed 1.4 MB and produced 90 HTTP requests. It just wasn’t performing well. We wanted to create a remarkable reading experience on the website while avoiding the <em>flash of unstyled text</em> (FOUT), so web fonts were loaded in the header and, hence, were blocking the rendering of content (actually it’s correct behaviour according to the <a href="https://www.w3.org/TR/resource-priorities/#intro-download-priority">spec</a>, designed to avoid multiple repaints and reflows.) <strong>jQuery was required for ads</strong> to be displayed, and a few JavaScripts depended on jQuery, so they all were blocking rendering as well. Ads were loaded and rendered <em>before</em> the content to ensure that they appeared as quickly as possible.

Images delivered by our ad partners were usually heavy and unoptimized, slowing down the page further. We also loaded Respond.js and Modernizr to deal with legacy browsers and to enhance the experience for smart browsers. As a result, articles were almost inaccessible on slow and unstable networks, and the start rendering time on mobile was disappointing at best.

It wasn’t just the front-end that was showing its age though. The backend wasn’t getting any better either. In 2012 we were playing with the idea of having fully independent sections of the magazine &mdash; sections that would live their own lives, evolving and growing over time as independent WordPress installations, with custom features and content types that wouldn’t necessarily be shared across all sections.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d0679e9-c7e5-4aee-9877-97ff7e505f98/browser-stats.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="203337" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a717cb2e-4b95-41fb-91b0-590204f984fc/browser-stats-opt.jpg" alt="browser-stats-opt" width="500" height="577" /></a><br>
<em>Yes, we do enjoy a quite savvy user base, so optimization for IE8 is really not an issue. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d0679e9-c7e5-4aee-9877-97ff7e505f98/browser-stats.png">Large view.</a></em>

Because WordPress multi-install wasn’t available at the time, we ended up with six independent, autonomous WordPress installs with six independent, autonomous style sheets. Those installs were connected to 6 × 2 databases (a media server and a static content server). We ran into dilemmas. For example, what if an author wrote for two sections and we’d love to show their articles from both sections on one single author’s bio page? Well, we’d need to somehow pull articles from both installs and add redirects for each author’s page to that one unified page, or should we just be using one of those pages as a "host"? Well, you know where this is going: increasing complexity and increasing maintenance costs. In the end, the sections didn’t manage to evolve significantly &mdash; at least not in terms of content &mdash; yet we had already customized technical foundation of each section, adding to the CSS dust and PHP complexity.

(Because we had outsourced WordPress tasks, some plugins depended on each other. So, if we were to deactivate one, we might have unwittingly disabled two or three others in the process, and they would have to be turned back on in a particular order to work properly. There were even differences in the HTML outputted by the PHP templates behind the curtains, such as classes and IDs that differed from one installation to the next. It’s no surprise that this setup made development a bit frustrating.)

The traffic was stagnant, readers kept complaining about the performance on the site and only a very small portion of users visited more than 2 pages per visit. The visual feedback when browsing the site was <em>visible</em> and surely wasn’t instant, and this lag has been driving readers away from the site to Instapaper and Pocket — both on mobile and desktop. We knew that because we asked our readers, and the feedback was quite clear (and a bit frustrating).

It was time to push back — heavily, with a <strong>major refactoring of the code base</strong>. We looked closely under the hood, discovering a few pretty scary (and nasty) things, and started fixing issues, one by one. It took us quite a bit of time to make things right, and we learned quite a few things along the way.</p>

{{% ad-panel-leaderboard %}}

## Switching Gears

Up until mid-2013, we weren’t using a CSS preprocessor, nor any build tools. Good long-term solutions require a good long-term foundation, so the first issues we tackled were tooling and the way the code base was organized. Because a number of people had been working on the code base over the years, some things proved to be rather mysterious... or challenging, to say the least.

We started with a <strong>code inventory</strong>, and we looked thoroughly at every single class, ID and CSS selector. Of course, we wanted to build a system of modular components, so the first task was to turn our seven large CSS files into maintainable, well-documented and easy-to-read modules. At the time, we’d chosen LESS, for no particular reason, and so our front-end engineer <a href="https://twitter.com/nice2meatu">Marco</a> started to rewrite CSS and build a modular, scalable architecture. Of course, we could very well have used Sass instead, but Marco felt quite comfortable with LESS at the time.

With a new CSS architecture, <a href="https://www.smashingmagazine.com/2013/10/29/get-up-running-grunt/">Grunt</a> as a build tool and a <a href="https://github.com/gruntjs/grunt-contrib-less">few</a> <a href="https://github.com/nDmitry/grunt-autoprefixer">time-saving</a> <a href="https://github.com/gruntjs/grunt-contrib-cssmin">Grunt</a> <a href="https://github.com/gruntjs/grunt-contrib-watch">tasks</a>, the task of maintaining the entire code base became much easier. We set up a brand new testing environment, synced up everything with GitHub, assigned roles and permissions, and started digging. We rewrote selectors, reauthored markup, and refactored and optimized JavaScript. And yes, it took us quite some time to get things in order, but it really wouldn’t have been so difficult if we hadn’t had a number of very different stylesheets to deal with.</p>

### The Big Back-End Cleanup

With the introduction of Multisite, creating a single WordPress installation from our six separate installations became a necessary task for our friends at <a href="https://inpsyde.com/en/">Inpsyde</a>. Over the course of five months, Christian Brückner and Thomas Herzog cleaned up the PHP templates, kicked unnecessary plugins into orbit, rewrote plugins we had to keep and added new ones where needed. They cleared the databases of all the clutter that the old plugins had created &mdash; one of the databases weighed in at <strong>70 GB</strong> (no, that’s not a typo; we do mean gigabytes) &mdash; merged all of the databases into one, and then created a single fresh and, most importantly, <em>maintainable</em> WordPress Multisite installation.

The speed boost from those optimizations was remarkable. We are talking about <strong>400 to 500 milliseconds of improvement</strong> by avoiding sub-domain redirects and unifying the code base and the back-end code. Those <a href="https://twitter.com/markodugonjic/statuses/478980625215782912">redirects</a> are indeed a major performance culprit, and just avoiding them is one of those techniques that usually boost performance significantly because you avoid full DNS lookups, improve time to first byte and reduce round trips on the network.

Thomas and Christian also refactored our entire WordPress theme according to the coding standard of their own theme architecture, which is basically a sophisticated way of writing PHP based on the WordPress standard. They wrote custom drop-ins that we use to display content at certain points in the layout. Writing the PHP strictly according to WordPress’ official API felt like getting out of a horse-drawn carriage and into a race car. All modifications were done without ever touching WordPress’ core, which is wonderful because we’ll never have to fear updating WordPress itself anymore.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56cbe27a-39dd-4ae3-ba51-bf9f6a826ae3/1m-spam-comments.png" alt="Spam comments" /><br>
<em>We’ve also marked a few millions spam comments across all the sections of the magazine. And before you ask: no, we did not import them into the new install.</em>

We migrated the installations during a slow weekend in mid-April 2014. It was a huge undertaking, and our server had a few hiccups during the process. We brought together over 2500 articles, including about 15,000 images, all spread over six databases, which also had a few major inconsistencies. While it was a very rough start at first &mdash; a lot of redirects had to be set up, caching issues on our server piled up, and some articles got lost between the old and new installations &mdash; the result was well worth the effort.

Our editorial team, primarily <a href="https://twitter.com/smash_it_on">Iris</a>, <a href="https://twitter.com/mel_in_media">Melanie</a> and <a href="https://twitter.com/indysigner">Markus</a>, worked very hard to <strong>bring those lost articles back to life</strong> by analyzing our 404s with Google Webmaster Tools. We spent a few weekends to ensure that every single article was recovered and remains accessible. Losing articles, including their comments, was simply unacceptable.

We know well how much time it takes for a good article to get published, and we have a lot of respect for authors and their work, and ensuring that the content remains online was a <strong>matter of respect for the work published</strong>. It took us a few weeks to get there and it wasn’t the most enjoyable experience for sure, but we used the opportunity to introduce more consistency in our information architecture and to adjust tags and categories appropriately. (Ah, if you do happen to find an article that has gotten lost along the way, please <a href="https://www.twitter.com/smashingmag">do let us know</a> and we’ll fix it right away. Thanks!)

## Front-End Optimization

In April 2014, once the new system was in place and had been running smoothly for a few days, we rewrote the LESS files based on what was left of all of the installs. Streamlining the classes for posts and pages, getting rid of all unneeded IDs, shortening selectors by lowering their specificity, and rooting out anything in the CSS we could live without crunched the CSS from 91 KB down to a mere 45 KB.

Once the CSS code base was in proper shape, it was time to reconsider how assets are loaded on the page and how we can improve the start rendering time beyond having clean, well-structured code base. Given the nightmare we experienced with the back-end previously, you might assume that improving performance now would have been a complex, time-consuming task, but actually it was quite a bit easier than that. Basically, it was just a matter of <strong>getting our priorities right</strong> by optimizing the critical rendering path.

The key to improving performance was to focus on what matters most: the content, and the fastest way for readers to actually start reading our articles on their devices. So over a course of a few months we kept reprioritizing. With every update, we introduced mini-optimizations based on a very simple, almost obvious principle: <strong>optimize the delivery of content, and defer the rest</strong> &mdash; without any compromises, anywhere.

Our optimizations were heavily influenced by the <a href="https://github.com/scottjehl">work done by Scott Jehl</a>, as well as <a href="https://github.com/guardian">The Guardian</a> and the <a href="https://github.com/BBC-News">BBC</a> teams (both of which open-sourced their work). While Scott <a href="https://filamentgroup.com/lab/performance-rwd.html">has been sharing valuable insight</a> into the front-end techniques that Filament Group was using, the BBC and The Guardian helped us to define and refine the concept of the <strong>core experience</strong> on the website and use it as a baseline. A shared main goal was to deliver the content as fast as possible to as many people as possible regardless of their device or network capabilities, and enhance the experience with progressive enhancement for capable browsers.

However, historically we haven’t had a lot of JavaScript or complex interactions on Smashing Magazine, so we didn’t feel that it was necessary to introduce complex loading logic with JavaScript preloaders. However, being a content-focused website, we <em>did</em> want to reduce the time necessary for the articles to start displaying as far as humanly possible.</p>

{{% ad-panel-leaderboard %}}

### Performance Budget: Speed Index <= 1000

<a href="https://timkadlec.com/2014/01/fast-enough/">How fast is fast enough?</a> Well, that’s a tough question to answer. In general, it’s quite difficult to visualize performance and explain why every millisecond counts—unless you have hard data. At the same time, falling into trap of absolutes and relying on not truly useful performance metrics is easy. In the past, the most commonly cited performance metric was average loading time. However, on its own, average loading time isn’t <em>that</em> helpful because it doesn’t tell you much about when a user can actually start using the website. This is why talking about "fast enough" is often so tricky.

<a href="https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index"><img loading="lazy" decoding="async" title="Comparing Progress" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea8e13e2-12cc-4b93-ae2a-c44a4947a6d8/compare-progress-opt.jpg" alt="Comparing Progress" width="500" height="268" /></a><br>
<em>A nice way of visualizing performance is to use WebPageTest to generate an actual video of the page loading and run a test between two competing websites. Besides, the <a href="https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index">Speed Index metric</a> often proves to be very useful.</em>

Different components require different amounts of time to load, yet some components of the page are more important than others. E.g. you don’t need to load the <em>footer content</em> fast, but it’s a good idea to render the visible portion of the page fast. You know where it’s heading: of course, we are talking about the “above the fold” view here. As <a href="https://www.lukew.com/ff/entry.asp?1756">Ilya Grigorik once said</a>, "We don’t need to render the entire page in one second, [just] the above the fold content." To achieve that, according to Scott’s research and Google’s test results, it’s helpful to set ambitious performance goals:

*   On [WebPageTest](https://www.webpagetest.org/), aim for a [Speed Index](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index) value of under 1000.
*   Ensure that all HTML, CSS and JavaScript fit within the first 14 KB.

What does it mean and why are they important? According to HCI research, "for an application to feel instant, a perceptible response to user input must be provided <a href="https://chimera.labs.oreilly.com/books/1230000000545/ch10.html#SPEED_PERFORMANCE_HUMAN_PERCEPTION">within hundreds of milliseconds</a>. After a second or more, the user’s flow and engagement with the initiated task feels broken." With the first goal, we are trying to ensure an instant response on our website. It refers to the so-called <em>Speed Index</em> metric for the <em>start rendering</em> time — the average time (in ms) at which visible parts of the page are displayed, or become accessible. So the first goal basically reflects that a page <strong>starts rendering</strong> under 1000ms, and yes, it’s a quite difficult challenge to take on.

<a href="https://chimera.labs.oreilly.com/books/1230000000545"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc009518-f239-4765-bd77-4df51d04dcf9/browser-networking-opt.jpg" alt="Browser Networking" width="500" height="413" /></a><br>
<em>Ilya Grigorik’s book <a href="https://chimera.labs.oreilly.com/books/1230000000545">High Performance Browser Networking</a> is a very helpful guide with useful guidelines and advice on making websites fast. And it’s available as a free HTML book, too.</em>

The second goal can help in achieving the first one. The value of 14 KB has been <a href="https://www.youtube.com/watch?v=YV1nKLWoARQ">measured empirically</a> by Google and is the threshold for the first package exchanged between a server and client via towers on a cellular connection. You don’t need to include images within 14 Kb, but you might want to deliver the markup, style sheets and any JavaScript required to render the visible portion of the page in that threshold. Of course, in practice this value can only realistically be achieved with gzip compression.

By combining the two goals, we basically defined a <strong>performance budget</strong> that we set for the website &mdash; a threshold for what was acceptable. Admittedly, we didn’t concern ourselves with the start rendering time on different devices on various networks, mainly because we really wanted to push back as far as possible everything that isn’t required to start rendering the page. So, the ideal result would be a Speed Index value that is <em>way</em> lower than the one we had set &mdash; as low as possible, actually &mdash; in all settings and on all connections, both shaky and stable, slow and fast. This might sound naive, but we wanted to figure out how fast we <em>could</em> be, rather than how fast we <em>should</em> be. We did measure start rendering time for first and subsequent page loads, but we did that much later, after optimizations had already been done, and just to keep track of issues on the front-end.

Our next step would be to integrate Tim Kadlec’s <a href="https://timkadlec.com/2014/05/performance-budgeting-with-grunt/">Perf-Budget Grunt task</a> to incorporate the performance budget right into the build process and, thus, run every new commit against WebPagetest’s performance benchmark. If it fails, we know that a new feature has slowed us down, so we probably have to reconsider how it’s implemented to fit it within our budget, or at least we know where we stand and can have meaningful discussions about its impact on the overall performance.</p>

### Prioritization And Separation Of Concerns

If you’ve been following <em>The Guardian</em>’s work recently, you might be familiar with the strict separation of concerns that they <a href="https://speakerdeck.com/andyhume/anatomy-of-a-responsive-page-load-whiskyweb-2013">introduced</a> during the major 2013 redesign. The Guardian <a href="https://vimeo.com/77967591">separated</a> its entire content into three main groups:

*   **Core content**.  Essential HTML and CSS, usable non-JavaScript-enhanced experience
*   **Enhancement**.  JavaScript, geolocation, touch support, enhanced CSS, web fonts, images, widgets
*   **Leftovers**.  Analytics, advertising, third-party content

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bc39952-3995-4f76-b84d-f387e9731000/separation-concerns.png"><img loading="lazy" decoding="async" class="alignnone size-medium wp-image-203361" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47ead1a8-27d2-42c6-b003-81367b4fccfa/separation-concerns-opt.jpg" alt="Separation of Concerns" width="500" height="217" /></a><br>
<em>A strict separation of concerns, or loading priorities, as defined by The Guardian team. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bc39952-3995-4f76-b84d-f387e9731000/separation-concerns.png">Large view.</a></em>

Once you have defined, confirmed and agreed upon these priorities, you can push performance optimization quite far. Just by being very specific about each type of content you have and by clearly defining what <strong>“core content”</strong> is, you are able to load <em>Core content</em> as quickly as possible, then load <em>Enhancements</em> once the page starts rendering (after the <code>DOMContentLoaded</code> event fires), and then load <em>Leftovers</em> once the page has fully rendered (after the <code>load</code> event fires).

The main principle here of course is to <strong>strictly separate the loading of assets</strong> throughout these three phases, so that the loading of the <em>Core content</em> should never be blocked by any resources grouped in <em>Enhancement</em> or <em>Leftovers</em> (we haven’t achieved the perfect separation just yet, but we are on it). In other words, you try to shorten the critical rendering path that is required for the content to start displaying by pushing the content down the line as fast as possible and deferring pretty much everything else.

We followed this same separation of concerns, grouping our content types into the same categories and identifying what’s critical, what’s important and what’s secondary. In our case, we identified and separated content in this way:

*   **Core content**.  Only essential HTML and CSS
*   **Enhancement**.  JavaScript, code syntax highlighter, full CSS, web fonts, comment ratings
*   **Leftovers**.  Analytics, advertising, Gravatars

Once you have this simple <strong>content/functionality priority list</strong>, improving performance is becoming just a matter of adding a few snippets for loading assets to properly reflect those priorities. Even if your server logic forces you to load all assets on all devices, by focusing on content delivery first, you ensure that the content is accessible quickly, while everything else is deferred and loaded in the background, after the page has started rendering. From a strategic perspective, the list also reflects your technical debt, as well as critical issues that slow you down. Indeed, we had quite a list of issues to deal with already at this point, so it transformed fairly quickly into a list of content priorities. And a rather tricky issue sat right at the top of that list: good ol’ web fonts.</p>

## Deferring Web Fonts

Despite the fact that the proportion of Smashing Magazine’s readers on mobile has always been quite modest (just around 15%—mainly due to the length of articles), we never considered mobile as an afterthought, but we never pushed user experience on mobile either. And when we talk about user experience on mobile, we mostly talk about speed, since typography was pretty much well designed from day one.

We had conversations during the 2012 redesign about how to deal with fonts, but we couldn’t find a solution that made everybody happy. The visual appearance of content was important, and because the new Smashing Magazine was all about beautiful, rich typography, not loading web fonts at all on mobile wasn’t really an option.

With the redesign back then, we switched to Skolar for headings and Proxima Nova for body copy, delivered by Fontdeck. Overall, we had three fonts for each typeface &mdash; Regular, Italic and Bold &mdash; totalling in six font files to be delivered over the network. Even after our dear friends at Fontdeck subsetted and optimized the fonts, the assets were quite heavy with over 300 KB in total, and because we wanted to avoid the frequent flash of unstyled text (FOUT), we had them loaded in the header of every page. Initially we thought that the fonts would reliably be cached in HTTP cache, so they wouldn’t be retrieved with every single page load. Yet it turned out that <strong>HTTP cache was quite unreliable</strong>: the fonts showed up in the waterfall loading chart every now and again for no apparent reason, both on desktop and on mobile.

The biggest problem, of course, was that the fonts were <a href="https://ianfeather.co.uk/web-fonts-and-the-critical-path/">blocking rendering</a>. Even if the HTML, CSS and JavaScript had already loaded completely, the content wouldn’t appear until the fonts had loaded and rendered. So you had this beautiful experience of seeing link underlines first, then a few keywords in bold here and there, then subheadings in the middle of the page and then finally the rest of the page. In some cases, when Fontdeck had server issues, the content didn’t appear at all, even though it was already sitting in the DOM, waiting to be displayed.

<a href="https://ianfeather.co.uk/web-fonts-and-the-critical-path/"><img loading="lazy" decoding="async" title="LP font by Ian Feather" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4340554b-09cf-4c6f-948c-cfd2e02a126e/benton-lp-opt.jpg" alt="LP font by Ian Feather" width="500" height="262" /></a><br>
<em>In his article, <a href="https://ianfeather.co.uk/web-fonts-and-the-critical-path/">Web Fonts and the Critical Path</a>, Ian Feather provides a very detailed overview of the FOUT issues and font loading solutions. We tested them all.</em>

We experimented with a few solutions before settling on what turned out to be perhaps the most difficult one. At first, we looked into using Typekit and Google’s <a href="https://github.com/typekit/webfontloader">WebFontLoader</a>, an asynchronous script which gives you more granular control of what appears on the page while the fonts are being loaded. Basically, the script adds a few classes to the <code>body</code> element, which allows you to specify the styling of content in CSS during the loading and after the fonts have loaded. So you can be very precise about how the content is displayed in fallback fonts first, before users see the switch from fallback fonts to web fonts.

We added <strong>fallback fonts declarations</strong> and ended up with pretty verbose CSS font stacks, using iOS fonts, Android fonts, Windows Phone fonts and good ol’ web-safe fonts as fallbacks — we are still using these font stacks today. E.g. we used this cascade for the main headings (it reflects the order of popularity of mobile operating systems in our analytics):
<pre class="language-css"><code>h2 {
   font-family: "Skolar Bold",
   AvenirNext-Bold, "Avenir Bold",
   "Roboto Slab", "Droid Serif",
   "Segoe UI Bold",
   Georgia, "Times New Roman", Times, serif;
}</code></pre>

So readers would see a mobile OS font (or any other fallback font first), and it probably would be a font that they are quite familiar with on their device, and then once the fonts have loaded, they would see a switch, triggered by WebFontLoader. However, we discovered that after switching to WebFontLoader, we started seeing FOUT way too often, with HTTP cache being quite unreliable again, and that permanent switch from a fallback font to the web font being quite annoying, basically ruining the reading experience.

So we looked for alternatives. One solution was to <strong>include the @font-face directive only on larger screens</strong> by wrapping it in a media query, thus avoiding loading web fonts on mobile devices and in legacy browsers altogether. (In fact, if you declare web fonts in a media query, they will be loaded only when the media query matches the screen size. So no performance hit there.) Obviously it helped us improve performance on mobile devices in no time, but we didn’t feel right with having a "simplified" reading experience on mobile devices. So it was a no-go, too.

What else could we do? The only other option was to <strong>improve the caching of fonts</strong>. We couldn’t do much with HTTP cache, but there was one option we hadn’t looked into: storing fonts in AppCache or localStorage. Jake Archibald’s article on the beautiful <a href="https://alistapart.com/article/application-cache-is-a-douchebag">complexity of AppCache</a> led us away from AppCache to experiment with localStorage, a <a href="https://github.com/ahume/webfontjson">technique</a> that The Guardian’s team was using at the time.

Now, offline caching comes with one major requirement: you need to <em>have</em> the actual font files to be able to cache them locally in the client’s browser. And you can’t cache <em>a lot</em> because <a href="https://www.html5rocks.com/en/tutorials/offline/quota-research/">localStorage space is very limited</a>, sometimes with just 5Mb available per domain. Luckily, the Fontdeck guys were very helpful and forthcoming with our undertaking, so despite the fact that font delivery services usually require you to load files and have a synchronous or asynchronous callback to count the number of impressions, Fontdeck has been perfectly fine with us grabbing WOFF-files from Google Chrome’s cache and setting up a “flat” pricing based on the number of page impressions in recent history.

So we grabbed the WOFF files and embedded them, base64-encoded, in a single CSS file, moving from six external HTTP-requests with about 50 KB file each to at most one HTTP request on the first load and <strong>400 KB of CSS</strong>. Obviously, we didn’t want this file to be loaded on every visit. So if localStorage is available on the user’s machine, we store the entire CSS file in localStorage, set a cookie and switch from the fallback font to the web font. This switch usually happens once at most because for the consequent visits, we check whether the cookie has been set and, if so, retrieve the fonts from localStorage (causing about 50ms in latency) and display the content in the web font right away. Just before you ask: yes, <a href="https://github.com/addyosmani/basket.js/issues/24">read/write to localStorage is much slower than retrieving files from HTTP cache</a>, but it proved to be a bit more reliable in our case.

<a href="https://github.com/addyosmani/basket.js/issues/24"><img loading="lazy" decoding="async" title="Browserscope Graph" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f406861-0441-4fd6-8c39-7025fabb24a4/browserscope-opt.png" alt="Browserscope Graph" width="500" height="305" /></a><br>
<em>Yes, <a href="https://github.com/addyosmani/basket.js/issues/24">localStorage is much slower than HTTP cache</a>, but it’s more reliable. Storing fonts in localStorage isn’t the perfect solution, but it helped us improve performance dramatically.</em>

If the browser doesn’t support localStorage, we include fonts with good ol' <code>link href</code> and, well, frankly just hope for the best — that the fonts will be properly cached and persist in the user’s browser cache. For <a href="https://caniuse.com/#search=woff">browsers that don’t support WOFF</a> (IE8, Opera Mini, Android &lt;= 4.3), we provide external URLs to fonts with older font mime types, hosted on Fontdeck.

Now, if localStorage is available, we still don’t want it to be blocking the rendering of the content. And we don’t want to see FOUT every single time a user loads the page. That’s why we have a little JavaScript snippet in the header before the <code>body</code> element: it checks whether a cookie has been set and, if not, we load web fonts asynchronously after the page has started rendering. Of course, we could have avoided the switch by just storing the fonts in localStorage on the first visit and have no switch during the first visit, but we decided that one switch is acceptable, because our typography is important to our identity.

The script was written, tested and documented by our good friend <a href="https://twitter.com/hdragomir">Horia Dragomir</a>. Of course, it’s <a href="https://gist.github.com/hdragomir/8f00ce2581795fd7b1b7">available as a gist on GitHub</a>:

<div class="break-out">
 <pre class="language-javascript"><code>&lt;script type="text/javascript"&gt;
    (function () {
      "use strict";
      // once cached, the css file is stored on the client forever unless
      // the URL below is changed. Any change will invalidate the cache
      var css_href = './web-fonts.css';
      // a simple event handler wrapper
      function on(el, ev, callback) {
        if (el.addEventListener) {
          el.addEventListener(ev, callback, false);
        } else if (el.attachEvent) {
          el.attachEvent("on" + ev, callback);
        }
      }

      // if we have the fonts in localStorage or if we’ve cached them using the native browser cache
      if ((window.localStorage &amp;&amp; localStorage.font_css_cache) || document.cookie.indexOf('font_css_cache') &gt; -1){
        // just use the cached version
        injectFontsStylesheet();
      } else {
       // otherwise, don’t block the loading of the page; wait until it’s done.
        on(window, "load", injectFontsStylesheet);
      }

      // quick way to determine whether a css file has been cached locally
      function fileIsCached(href) {
        return window.localStorage &amp;&amp; localStorage.font_css_cache &amp;&amp; (localStorage.font_css_cache_file === href);
      }

      // time to get the actual css file
      function injectFontsStylesheet() {
       // if this is an older browser
        if (!window.localStorage || !window.XMLHttpRequest) {
          var stylesheet = document.createElement('link');
          stylesheet.href = css_href;
          stylesheet.rel = 'stylesheet';
          stylesheet.type = 'text/css';
          document.getElementsByTagName('head')[0].appendChild(stylesheet);
          // just use the native browser cache
          // this requires a good expires header on the server
          document.cookie = "font_css_cache";

        // if this isn’t an old browser
        } else {
           // use the cached version if we already have it
          if (fileIsCached(css_href)) {
            injectRawStyle(localStorage.font_css_cache);
          // otherwise, load it with ajax
          } else {
            var xhr = new XMLHttpRequest();
            xhr.open("GET", css_href, true);
            on(xhr, 'load', function () {
              if (xhr.readyState === 4) {
                // once we have the content, quickly inject the css rules
                injectRawStyle(xhr.responseText);
                // and cache the text content for further use
                // notice that this overwrites anything that might have already been previously cached
                localStorage.font_css_cache = xhr.responseText;
                localStorage.font_css_cache_file = css_href;
              }
            });
            xhr.send();
          }
        }
      }

      // this is the simple utitily that injects the cached or loaded css text
      function injectRawStyle(text) {
        var style = document.createElement('style');
        style.innerHTML = text;
        document.getElementsByTagName('head')[0].appendChild(style);
      }

    }());
&lt;/script&gt;
</code></pre>
</div>

During the testing of the technique, we discovered a few surprising problems. Because the <strong>cache isn’t persistent in WebViews</strong>, fonts do load asynchronously in applications such as Tweetdeck and Facebook, yet they don’t remain in the cache once the window is closed. In other words, with every WebViews visit, the fonts are re-downloaded. Some old Blackberry devices seemed to clear cookies and delete the cache when the battery is running out. And depending on the configuration of the device, sometimes fonts do not persist in mobile Safari either.

Still, once the snippet was in place, articles started rendering much faster. By deferring the loading of Web fonts and storing them in localStorage, we’ve <strong>avoided around 700ms delay</strong>, and thus shortened the critical path significantly by avoiding the latency for retrieving all the fonts. The result was quite impressive for the first load of an uncached page, and it was even more impressive for concurrent visits since we were able to reduce the latency caused by Web fonts to just 40 to 50 ms. In fact, if we had to mention just one improvement to performance on the website, deferring web fonts is by far the most effective.

At this point, we haven’t even considered using the new <a href="https://gist.github.com/sergejmueller/cf6b4f2133bcb3e2f64a">WOFF2 format</a> for fonts just yet. Currently supported in Chrome and Opera, it promises a better compression for font files and it already showed remarkable results. In fact, The Guardian was able to <a href="https://twitter.com/patrickhamann/status/497767778703933442">cut down on 200ms latency and 50 KB of the file weight</a> by switching to WOFF2, and we intend to look into moving to WOFF2 soon as well.

Of course, grabbing WOFFs might not always be an option for you, but it wouldn’t hurt just to talk to type foundries to see where you stand or to work out a deal to host fonts “locally.” Otherwise, tweaking WebFontLoader for Typekit and Fontdeck is definitely worth considering.</p>

## Dealing With JavaScript

With the goal of removing all unnecessary assets from the critical rendering path, the second target we decided to deal with was JavaScript. And it’s not like we particularly dislike JavaScript for some reason, but we always tend to prefer non-JavaScript solutions to JavaScript ones. In fact, if we can avoid JavaScript or replace it with CSS, then we’ll always explore that option.

Back in 2012, we weren’t using a lot of scripts on the page, yet displaying advertising via OpenX depended on jQuery, which made it way too easy to lazily approach simple, straightforward tasks with ready-to-use jQuery plugins. At the time, we also used Respond.js to emulate responsive behaviour in legacy browsers. However, Internet Explorer 8 usage has dropped significantly between 2012 and 2014: with 4.7% before the redesign, it was now 1.43%, with a dropping tendency every single month. So we decided to deliver a fixed-width layout with a specific IE8.css stylesheet to those users, and removed Respond.js altogether.

As a strategic decision, we decided to <strong>defer the loading of all JavaScripts until the page has started rendering</strong> and we looked into replacing jQuery with lightweight modular JavaScript components.

jQuery was tightly bound to ads, and ads were supposed to start displaying as fast as possible, so to make it happen, we had to deal with advertising first. The decision to defer the loading of ads wasn’t easy to get agreement on, but we managed to make a convincing argument that better performance would increase click rates because users would see the content sooner. That is, on every page, readers would be attracted by the high-quality content and then, when the ads kick in, would pay attention to those squares in the sidebar as well.

<a href="https://www.kreativrauschen.de/">Florian Sander</a>, our partner in crime when it comes to advertising, rewrote the script for our banner ads so that banners would be loaded only after the content has started rendering, and only then the advertising spots would be put into place. Florian was able to get rid of two render-blocking HTTP-requests that the ad-script normally generated, and we were able to remove the dependency on jQuery by rewriting the script in vanilla JavaScript.

Obviously, because the sidebar’s ad content is generated on the fly and is loaded after the render tree has been constructed, we started seeing <strong>reflows</strong> (this still happens when the page is being constructed). Because we used to load ads before the content, the entire page (with pretty much everything) used to load at once. Now, we’ve moved to a more modular structure, grouping together particular parts of the page and queuing them to load after each other. Obviously, this has made the overall experience on the site a bit noisier because there are a few jumps here and there, in the sidebar, in the comments and in the footer. That was a compromise we went for, and we are working on a solution to reserve space for "jumping" elements to avoid reflows as the page is being loaded.</p>

### Deferring Non-Critical JavaScript

When the prospect of removing jQuery altogether became tangible as a long-term goal, we started working step by step to decouple jQuery dependencies from the library. We rewrote the script to generate footnotes for the print style sheet (later replacing it with a PHP solution), rewrote the functionality for rating comments, and rewrote a few other scripts. Actually, with our savvy user base and a solid share of smart browsers, we were able to move to vanilla JavaScript quite quickly. Moreover, we could now move scripts from the header to the footer to avoid blocking construction of the DOM tree. In mid-July, we removed jQuery from our code base entirely.

We wanted full control of what is loaded on the page and when. Specifically, we wanted to ensure that no JavaScript blocks the rendering of content at any point. So, we use the <a href="https://www.feedthebot.com/pagespeed/defer-loading-javascript.html">Defer Loading JavaScript</a> script to load JavaScript after the <code>load</code> event by injecting the JavaScript after the DOM and CSSOM have already been constructed and the page has been painted. Here’s the snippet that we use on the website, with the <code>defer.js</code> script (which is loaded asynchronously after the <code>load</code> event):
<pre class="language-javascript"><code>function downloadJSAtOnload() {
   var element = document.createElement("script");
   element.src = "defer.js";
   document.body.appendChild(element);
}
if (window.addEventListener)
   window.addEventListener("load", downloadJSAtOnload, false);
else if (window.attachEvent)
   window.attachEvent("onload", downloadJSAtOnload);
else
   window.onload = downloadJSAtOnload;</code></pre>

However, because <a href="https://www.igvita.com/2014/05/20/script-injected-async-scripts-considered-harmful/">script-injected asynchronous scripts are considered harmful</a> and slow (they block the browser’s speculative parser), we might be looking into using the good ol’ <code>defer</code> and <code>async</code> attributes instead. In the past, we couldn’t use <code>async</code> for every script because we needed jQuery to load before its dependencies; so, we used <code>defer</code>, which respects the loading order of scripts. With jQuery out of the picture, we can now load scripts asynchronously, and fast. Actually by the time you read this article, we might already be using <code>async</code>.

Basically, we just deferred the loading of all JavaScripts that we identified previously, such as syntax highlighter and comment ratings, and cleared a path in the header for HTML and CSS.</p>

## Inlining Critical CSS

That wasn’t good enough, though. Performance did improve dramatically; however, even with all of these optimizations in place, we didn’t hit that magical Speed Index value of under 1000. In light of the ongoing discussion about inline CSS and above-the-fold CSS, as <a href="https://developers.google.com/web/fundamentals/performance/critical-rendering-path/page-speed-rules-and-recommendations">recommended by Google</a>, we looked into more radical ways to deliver content quickly. To avoid an HTTP request when loading CSS, we measured how fast the website would be if we were to load critical CSS inline and then load the rest of the CSS once the page has rendered.

<a href="https://www.filamentgroup.com/lab/performance-rwd.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/895c9449-83aa-45ba-9dc0-61a573766e5f/filament-group-article-opt.jpg" alt="scott-jehl" width="500" height="380" /></a><br>
<em>Scott Jehl’s <a href="https://www.filamentgroup.com/lab/performance-rwd.html">article</a> explains how exactly to extract and inline critical CSS.</em>

But what exactly is critical CSS? And how do you extract it from a potentially complex code base? As <a href="https://www.filamentgroup.com/lab/performance-rwd.html">Scott Jehl points out</a>, critical CSS is the subset of CSS that is needed to render the top portion of the page across all breakpoints. What does that mean? Well, you would decide on a certain height that you would consider to be “above the fold” content &mdash; it could be 600, 800 or 1200 pixels or anything else &mdash; and you would collect into their own style sheet all of the styles that specify how to render content within that height across all screen widths.

Then you inline those styles in the <code>head</code>, and thus <strong>give the browser everything it needs</strong> to start render that visible portion of the page &mdash; within one single HTTP request. You’ve heard it a few times by now: everything else is deferred after the first initial rendering. You avoid an HTTP-request, and you load the full CSS asynchronously, so once the user starts scrolling, the full CSS will (hopefully) already have loaded.

Visually speaking, content will appear to render more quickly, but there will also be <strong>more reflowing and jumping on the page</strong>. So, if a user has followed a link to a particular comment below the "fold", then they will see a few reflows as the website is being constructed because the page is rendered with critical CSS first (there is just so much we can fit within 14 KB!) and adjusted later with the complete CSS. Of course, inline CSS isn’t cached; so, if you have critical CSS and load the complete CSS on rendering, it’s useful to set a cookie, so that inline styles aren’t inlined with every single load. The drawback of course is that you might have duplicate CSS because you would be defining styles both inline and in the full CSS, unless you’re able to strictly separate them.

Because we had just refactored our CSS code base, identifying critical CSS wasn’t very difficult. Obviously, there are <a href="https://css-tricks.com/authoring-critical-fold-css/">smart</a> <a href="https://github.com/addyosmani/above-the-fold-css-tools">tools</a> that analyze the markup and CSS, identify critical CSS styles and export them into a separate file during the build process, but we were able to do it manually. Again, you have to keep in mind that 14 Kb is your budget for HTML and CSS, so in the end we had to rename a few classes here and there, and compress CSS as well.

We analyzed the first 800px, checking the inspector for the CSS that was needed and separating our style sheet into two files – and actually that was pretty much it. One of those files, <em>above-the-fold.css</em>, is minified and compressed, and its content is placed inline in the head of our document as early as possible – not blocking rendering. The other file, our full CSS file, is then loaded with JavaScript after the content has loaded, and if JavaScript isn’t available for some reason or the user is on a legacy browser, we’ve put a full CSS file inside <code>noscript</code> tag at the end of the head, so they don’t get an unstyled HTML page.</p>

## Was It All Worth It?

Because we’ve just implemented these optimizations, we haven’t been able to measure their impact on traffic, but we’ll publish these results later as well. Obviously, we <em>did</em> notice a quite remarkable technical improvement though. By deferring and caching web fonts, inlining CSS and optimizing the critical rendering path for the first 14Kb, we were able to achieve dramatic improvements in loading times. The start rendering time started circling around 1s for an uncached page on 3G and was around 700ms (including latency!) on subsequent loads.

<a href="https://www.webpagetest.org/result/140904_H4_T5R/1/details/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23da8f18-2329-4065-9de7-305431fd3f48/pagespeed-screenshot-opt.jpg" alt="webpagetest" width="500" height="297" /></a><br>
<em>We’ve been using <a href="https://www.webpagetest.org/">WebPageTest</a> a lot for running tests. Our waterfall chart was becoming better over time and reflected the priorities we had defined earlier. <a href="https://www.webpagetest.org/result/140904_H4_T5R/1/details/">Large view.</a></em>

On average, Smashing Magazine’s front page makes <strong>45 HTTP-requests</strong> and has <strong>440 KB in bandwidth</strong> on the first uncached load. Because we heavily cache everything but ads, subsequent visits have around 15 HTTP requests and 180 KB of traffic. The First Byte time is still around 300–600ms (which is <em>a lot</em>), yet Start Render time is usually <a href="https://www.webpagetest.org/result/140904_ZJ_T62/">under 0.7s</a> on a DSL connection in Amsterdam (for the very first, uncached load), and usually <a href="https://www.webpagetest.org/result/140904_Y5_SXS/">under 1.7s on a slow 3G</a>. On a fast cable connection, the site <a href="https://www.webpagetest.org/result/140904_DB_T5Y/">starts rendering within 0.8s</a>, and on a fast 3G, <a href="https://www.webpagetest.org/result/140904_H4_T5R/">within 1.1s</a>. Obviously, the results vary significantly depending on the First Byte time which we can’t improve just yet, at the time of writing. That’s the only asset that introduces unpredictability into the loading process, and as such has a decisive impact on the overall performance.

Just by following basic guidelines by our colleagues mentioned above and Google’s recommendations, we were able to achieve the <a href="https://developers.google.com/speed/pagespeed/insights/?url=http%3A%2F%2Fwww.smashingmagazine.com&amp;tab=desktop">97–99 Google PageSpeed score</a> both on desktop and on mobile. The score varies depending on the quality and the optimization level of advertising assets displayed randomly in the sidebar. Again, the main culprit is the server’s response time &mdash; not for long, though.

<a href="https://developers.google.com/speed/pagespeed/insights/?url=http%3A%2F%2Fwww.smashingmagazine.com&amp;tab=mobile"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/671f259f-6ae0-405b-b786-833c5404e678/mobile-99-opt.png" alt="Google PageSpeed score: 99" width="416" height="835" /></a><br>
<em>After a few optimizations, we achieved a Google PageSpeed score of <a href="https://developers.google.com/speed/pagespeed/insights/?url=http%3A%2F%2Fwww.smashingmagazine.com&amp;tab=mobile">99 on mobile</a>.</em>

<a href="https://developers.google.com/speed/pagespeed/insights/?url=http%3A%2F%2Fwww.smashingmagazine.com&amp;tab=desktop"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17fdbefe-3ce0-4eaf-923c-00377d960292/desktop-99-opt.png" alt="99 out of 100 points on desktop with the Google PageSpeed tool" width="415" height="520" /></a><br>
<em>We got a Google PageSpeed score of <a href="https://developers.google.com/speed/pagespeed/insights/?url=http%3A%2F%2Fwww.smashingmagazine.com&amp;tab=desktop">99 on the desktop</a> as well.</em>

By the way, Scott Jehl has also published a <a href="https://filamentgroup.com/lab/performance-rwd.html">wonderful article on the front-end techniques</a> FilamentGroup uses to extract critical CSS and load it inline while loading the full CSS afterwards and avoid downloading overheads. Patrick Hamann’s <a href="https://www.youtube.com/watch?v=dfweWyVScaI">talk on "Breaking News at 1000ms"</a> explains a few techniques that The Guardian is using to hit the SpeedIndex 1000 mark. Definitely worth reading and watching, and indeed quite similar to what we implemented on this very site as well.</p>

## Work To Be Done

While the results we were able to achieve are quite satisfactory, there is still a lot of work to be done. For example, we haven’t considered optimizing the delivery of images just yet, and are now adjusting our editorial process to integrate the new <code>picture</code> element and <code>srcset</code>/<code>sizes</code> with <a href="https://scottjehl.github.io/picturefill/">Picturefill 2.1.0</a>, to make the loading even faster on mobile devices. At the moment, all images have a fixed width of 500px and are basically scaled down on smaller views. Every image is optimized and compressed, but we don’t deliver different images for different devices &mdash; and no, we aren’t delivering any Retina images at all. That is all about to change soon.

While Smashing Magazine’s home page is well optimized, some pages and articles still perform poorly. Articles with many comments are quite slow because we use <a href="https://en.gravatar.com/">Gravatar.com</a> for comments. Because each Gravatar URL is unique, each comment generates one HTTP request, slowing down the loading of the overall page. We are going to defer the loading of Gravatars and cache them locally with a <a href="https://wordpress.org/plugins/fv-gravatar-cache/">Gravatar Cache WordPress plugin</a>. We might have already done it by the time you read this.

We’re playing around with DNS prefetching and HTML5 preloading to resolve DNS lookups way ahead of time (for example, for Gravatars and advertising). However, we are being careful and hesitant here because we don’t want to create a loading overhead for users on slow or expensive connections. Besides, we’ve added <a href="https://alistapart.com/article/like-able-content-spread-your-message-with-third-party-metadata">third-party meta data</a> to make our articles a bit easier to share. So, if you link to an article on Facebook, Facebook will pull optimized images, a description and a title from our meta data, which is crafted individually for each article. We’ve also happily noticed that article pages scroll smoothly at <a href="https://jankfree.org">60fps</a>, and that with relatively large images and ads.

<a href="https://caniuse.com/#search=SPDY"><img loading="lazy" decoding="async" class="alignnone size-medium wp-image-203341" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b07c6ced-e222-412b-b3c1-0acbf48a2fa8/spdy-opt.png" alt="spdy" width="500" height="313" /></a><br>
<em>Yes, <a href="https://caniuse.com/#search=SPDY">we can use SPDY today</a>. We just need to install <a href="https://nginx.org/en/docs/http/ngx_http_spdy_module.html">SPDY Nginx Module</a> or <a href="https://code.google.com/p/mod-spdy/">Apache SPDY Module</a>. This is what we are going to tackle next.</em>

Despite all of our optimizations, the main issue still hasn’t been resolved: very slow servers and the First Byte response times. We’ve been experiencing difficulties with our current server setup and architecture but are tied with a long-term contract, yet we will be moving to a new server soon. We’ll take that opportunity to also move to <a href="https://developers.google.com/speed/spdy/">SPDY</a> on the server, a predecessor of HTTP 2.0 (which is <a href="https://caniuse.com/#search=SPDY">well supported in major browsers</a>, by the way), and we are looking into using a content delivery network as well.</p>

### Performance Optimization Strategy

To sum up, optimizing the performance of Smashing Magazine was quite an effort to figure out, yet many aspects of optimization can be achieved very quickly. In particular, front-end optimization is quite easy and straightforward as long as you have a shared understanding of priorities. Yes, that’s right: you optimize content delivery, and defer everything else.

Strategically speaking, the following could be your performance optimization roadmap:

*   Remove blocking scripts from the header of the page.
*   Identify and defer non-critical CSS and JavaScript.
*   Identify critical CSS and load it inline in the head, and then load the full CSS after rendering. (Make sure to set a cookie to prevent inline styles from loading with every page load.)
*   Keep all critical HTML and CSS to under 14 KB, and aim for a Speed Index of under 1000.
*   Defer the loading of Web fonts and store them in localStorage or AppCache.
*   Consider using WOFF2 to further reduce latency and file size of the web fonts.
*   Replace JavaScript libraries with leaner JavaScript modules.
*   Avoid unnecessary libraries, and look into options for removing Respond.js and Modernizr; for example, by “[cutting the mustard](https://responsivenews.co.uk/post/18948466399/cutting-the-mustard)” to separate browsers into buckets. Legacy browsers could get a fixed-width layout. [Clever SVG fallbacks](https://css-tricks.com/svg-fallbacks/) also exist.

That’s basically it. By following these guidelines, you can make your responsive website really, <em>really</em> fast.</p>

## Conclusion

Yes, finding just the right strategy to make this very website fast took a lot of experimentation, blood, sweat and cursing. Our discussions kept circling around next steps and on critical and not-so-critical components and sometimes we had to take three steps back in order to pivot in a different direction. But we learned a lot along the way, and we have a pretty clear idea of where we are heading now, and, most importantly, how to get there.

So here you have it. A little story about the things that happened on this little website over the last year. If you notice any issues, please let us know on Twitter <a href="https://www.twitter.com/smashingmag">@smashingmag</a> and we’ll hunt them down for good.

Ah, and thanks for keeping us reading throughout all these years. It means <em>a lot</em>. You are quite smashing indeed. You should know that.

A big "thank you" to Patrick Hamann and Jake Archibald for the technical review of the article as well as Andy Hume and Tim Kadlec for their fantastic support throughout the years. Also a big "thank you" to our front-end engineer, Marco, for his help with the article and for his thorough and tireless front-end work, which involved many experiments, failures and successes along the way. Also, kind thanks to the Inpsyde team and Florian Sander for technical implementations.

A final thank you goes out to Iris, Melanie, Cosima and Markus for keeping an eye out for those nasty bugs and looking after the content on the website. Without you, this website wouldn’t exist. And thank you for having my back all this time. I respect and value every single bit of it. You rock.

{{< signature "al, vf, il" >}}


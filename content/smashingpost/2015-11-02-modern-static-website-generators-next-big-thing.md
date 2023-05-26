---
title: Why Static Site Generators Are The Next Big Thing
slug: modern-static-website-generators-next-big-thing
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15bb5653-5a31-4ac0-85fc-c946795f10bd/jekyll-opt.png'
date: 2015-11-02T23:03:34.000Z
author: mathiasbiilmannchristensen
description: >-
  At StaticGen, our open-source directory of **static website generators**,
  we’ve kept track of more than a hundred generators for more than a year now,
  and we’ve seen both the volume and popularity of these projects take off
  incredibly on GitHub during that time, going from just 50 to more than 100
  generators and a total of more than 100,000 stars for static website generator
  repositories.

  Influential design-focused companies such as Nest and MailChimp now use static
  website generators for their primary websites. Vox Media has built a whole
  publishing system around Middleman. Carrot, a large New York agency and part
  of the Vice empire, builds websites for some of the world’s largest brands
  with its own open-source generator, Roots. And several of Google’s properties,
  such as “A Year In Search” and Web Fundamentals, are static.
categories:
  - Coding
  - Tools
  - Generators
  - Static Generators
---
At <a href="https://www.staticgen.com">StaticGen</a>, our open-source directory of <strong>static website generators</strong>, we’ve kept track of more than a hundred generators for more than a year now, and we’ve seen both the volume and popularity of these projects take off incredibly on GitHub during that time, going from just 50 to more than 100 generators and a total of more than 100,000 stars for static website generator repositories.

Influential design-focused companies such as Nest and MailChimp now use static website generators for their primary websites. <a href="https://www.voxmedia.com/">Vox Media</a> has built a <a href="https://product.voxmedia.com/2015/7/8/8907841/introducing-autotune">whole publishing system</a> around Middleman. <a href="https://carrot.is">Carrot</a>, a large New York agency and part of the Vice empire, builds websites for some of the world’s largest brands with its own open-source generator, <a href="https://roots.cx/">Roots</a>. And several of Google’s properties, such as “<a href="https://www.google.com/trends/2014/">A Year In Search</a>” and <a href="https://developers.google.com/web/fundamentals/">Web Fundamentals</a>, are static.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8fd0663-dd8e-4974-83d0-2446de261c35/01-staticgen-stats-opt-preview.png"><img loading="lazy" decoding="async" title="Why Static Site Generators Are The Next Big Thing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c8d7c77-5a83-4aa3-9968-f64b575feabd/01-staticgen-stats-opt.png" alt="Static Site Generator : StaticGen's graph of growth over the last year" width="1108" height="894" /></a><figcaption>StaticGen’s graph of growth over the last year. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c8d7c77-5a83-4aa3-9968-f64b575feabd/01-staticgen-stats-opt.png">View large version</a>)</figcaption></figure>

Static websites are hardly new, going all the way back to the beginning of the web. So, why the sudden explosion in interest? What’s up? Why now?

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Static Website Generators Reviewed: Jekyll, Middleman, Roots, Hugo](https://www.smashingmagazine.com/2015/11/static-website-generators-jekyll-middleman-roots-hugo-review/)
*   [Using A Static Site Generator At Scale: Lessons Learned](https://www.smashingmagazine.com/2016/08/using-a-static-site-generator-at-scale-lessons-learned/)
*   [Build A Blog With Jekyll And GitHub Pages](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/)
*   [Content Modeling With Jekyll](https://www.smashingmagazine.com/2016/02/content-modeling-with-jekyll/)

{{% feature-panel %}}

## When Static Was It

The first ever website, Tim Berners-Lee’s <a href="https://info.cern.ch/hypertext/WWW/TheProject.html">original home page for the World Wide Web</a>, was static. A website back then was a folder of HTML documents that consisted of <a href="https://www.w3.org/History/19921103-hypertext/hypertext/WWW/MarkUp/Tags.html">just 18 tags</a>. Browsers were simple document navigators that would fetch HTML from a server and allow the end user to navigate them by following hyperlinks. The web was fundamentally static.

As browsers evolved, so did HTML, and gradually the limitations of purely static websites started to show.

Initially, websites were just plain unstyled documents, but soon they grew into carefully designed objects, with graphical headers and complex navigation. By that point, managing each page of a website as its own document stopped making sense, and templating languages entered the picture.

It also quickly became evident that reserving HTML for structure and CSS for style was not enough of an abstraction to keep the content of a website (the stories, products, gallery items, etc.) separate from the design.

Around the same time, SQL-based relational databases started going mainstream, and for many online companies, the database became the almost-holy resting place of all of their content, guarded by vigilant, long-bearded database administrators.

Desktop applications such as Dreamweaver and FrontPage offered solutions for building content-driven websites through WYSIWYG editors, where pages could be separated into reusable parts, such as navigation, headers and footers, and where content to some degree could be put in a database. In some ways, fatally flawed as they were, these were the <strong>original static website generators</strong>: building websites from templates, partials, media libraries and sometimes even SQL databases, and publishing them via FTP as static files. As late as 2004, I had the unique experience of working on a major content-driven website, with tens of thousands of pages spread across different editorial groups, all managed via Dreamweaver!

Even if Dreamweaver could, to some degree, integrate with a database, it had no <strong>content model</strong>, offering no sense of content being separate from design, each half being editable independently with the appropriate tools.

The most mainstream answer to these problems was the LAMP stack and CMS’ such as WordPress, Drupal and Joomla. All of these played an incredibly important role in moving the web forward, enabling the Web 2.0 phenomenon, in which user-generated content became a driving factor for a lot of websites. Users went from following hyperlinks to ordering products, participating in communities and creating content.</p>

## Dynamic Problems

When I built my first dynamic website more than 15 years ago, I was following the original LAMP-stack tutorials from the MySQL documentation. When I realized that all of this stuff was going on every time someone visited a website that was built like this, it blew my mind!

A web server would load my code into a PHP interpreter, on the fly, and then open connections to a database, sending queries back and forth, using the data in templates and stitching together strings of text into an HTML document, tailor-made for the visitor at that moment. Amazing!

It was, admittedly, a bit less amazing when I visited the website a few years later and found the whole web page replaced with a message from a hacker who pointed out the security flaws in the configuration and was at least generous enough just to deface the website, rather than use it as a vehicle to spread malware.

This dynamic website architecture moved the web forward, but it also opened a can of worms. By a conservative estimate, more than 70% of today’s WordPress installations are <strong>vulnerable to known exploits</strong> (and WordPress powers more than 23% of the web). Just a few months ago, <del>1.2 million Drupal installations got infected with malware in the span of a few days</del> <a href="https://nakedsecurity.sophos.com/2014/10/30/millions-of-drupal-websites-at-risk-from-failure-to-patch/">12 million Drupal sites needed emergency patching</a>, and any not patched within 7 hours of the exploits' announcement should be considered infected with malware.. Not a week goes by when I don’t follow a link from social media to a website that shows a “Database connection error.” Scaling a dynamic website can be very expensive, and agencies that launch a campaign website or the like often have to overprovision drastically in order to guard against the website blowing up if it manages to go viral — or else they have to desperately scale it while trying to get it back online (something that never seems to happen during office hours).

We pay a huge price for the underlying complexity of dynamic code running on a server for every request — a price we could avoid paying entirely when this kind of complexity is not needed.</p>

## Dynamic Websites And Caching

To some degree, we tend to work around this by caching. No high-profile WordPress website would be capable of running without a plugin such as WP Super Cache. Large websites no doubt rely on proxy caches such as Varnish, Nginx and Apache Traffic Server in front of their websites.</p>

<strong>Caching is notoriously difficult to get right</strong>, however, and even the most optimized dynamic website will normally be many times slower than a static solution.

This website, Smashing Magazine, is obviously run by one of the most performance-focused teams out there and is, in general, very heavily optimized for performance. So, I ran a small experiment for this article. Using <a href="https://www.httrack.com/">HTTrack</a>, I grabbed a copy of this website one level deep and then deployed the static version to <a href="https://www.netlify.com/?utm_source=link&utm_medium=parter&utm_campaign=sm-story">Netlify</a>, a static-hosting platform based on a content delivery network (CDN). I didn’t do anything to improve performance of the static version apart from simply deploying to a host with deep CDN integration.</p>

<figure><a href="https://performance.sucuri.net/domain/www.smashingmagazine.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35da4898-05b3-4f24-8b62-4053cad587cd/02-smashing-dynamic-load-times-opt.png" alt="Smashing Magazine is faster than most websites, but it serves all requests from a single data center." /></a><figcaption>Smashing Magazine is faster than most websites, but it serves all requests from a single data center. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35da4898-05b3-4f24-8b62-4053cad587cd/02-smashing-dynamic-load-times-opt.png">View large version</a>)</figcaption></figure>

I then ran some tests to see how this affected the time to first byte and the complete download time of the main <code>index.html</code> page. Here’s what <a href="https://performance.sucuri.net/">Sucuri’s super-useful performance tool</a> showed.

Even with a highly optimized dynamic website, the static version is <strong>more than six times as fast on average</strong>! Granted, not every static host will make this kind of difference, but leveraging this level of CDN-based caching simply wouldn’t be possible without any manual configuration of a dynamic website, at least not without introducing really weird caching artifacts.</p>

<figure><a href="https://performance.sucuri.net/domain/smashing-static.netlify.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc955e1e-5fee-42e9-8c21-ab434c89ab30/03-smashing-static-load-times-opt-preview.png" alt="The exact same HTML served from a high-performance static host" /></a><figcaption>The exact same HTML served from a high-performance static host. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe832161-2696-44d8-b79f-c7956eb73fac/03-smashing-static-load-times-opt.png">View large version</a>)</figcaption></figure>

Caching and, more specifically, <strong>cache invalidation</strong> is extremely hard to get right with a dynamic website, especially the kind of distributed caching required to take full advantage of a CDN. With a WordPress website, there’s no guarantee that the same URL won’t return different HTML depending on whether the user is logged in, query parameters, ongoing A/B tests and so on. Keeping track of when a page needs to be invalidated in the cache is a complex task: Any change to a comment, global website setting, tag, category or other content in the database could lead to changes in the lists of related posts, index pages, archive, comment counters, etc.</p>

<strong>Static websites are fundamentally different</strong> in this regard. They stick to a really simple caching contract: Any URL will return the same HTML to any visitor until the specific file that corresponds with that URL is explicitly updated.

Working with this caching contract does impose constraints during development, but if a website can be built under these constraint, then the difference in performance, uptime and cost can be enormous.

## The Modern Static Site Generator

In recent years, this alternative to the traditional dynamic infrastructure has gained ground. The idea of a static website generator is nothing new. Even WordPress’ largest competitor back in the day, Movable Type, had the option of working as a static website generator.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e01cff9-0494-4fbd-a7b8-e0fed9405d02/04-static-site-generator-trends-opt-preview-78x24.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08268774-3435-4557-8d39-e8ef49ffd1d3/04-static-site-generator-trends-opt.png" alt="Google Trends for static website generator" /></a><figcaption>Google Trends for “static website generator”. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08268774-3435-4557-8d39-e8ef49ffd1d3/04-static-site-generator-trends-opt.png">View large version</a>)</figcaption></figure>

Since then, a lot of the constraints that made static websites lose out have fallen away, and today’s generators are modern, competitive publishing engines with a strong appeal to front-end developers.

More static website generators are released every week, and keeping up with developments can be hard. In general, though, the most popular static generators share the following traits.</p>

### Templating

Allowing a website to be split into layouts and includes to get rid of repetition is one of the basics of static website generators. There are myriad of template engines to chose from, each with its own tradeoffs — some being logic-less, some inviting a mixture of template and code, all allowing you to get rid of duplicate headers, footers and navigations.</p>

### Markdown Support

The rise of Markdown is likely one of the primary reasons why static website generators have become so popular. Few people would dream of writing all of their content in <a href="https://en.wikipedia.org/wiki/BBCode">BBCode</a> or pure HTML, whereas Markdown is very pleasant to work with, and Markdown editors for serious writing, note-taking and blogging seem to be exploding in popularity.

All of the major static generators support Markdown. Some swear by <a href="https://docutils.sourceforge.net/rst.html">reStructuredText</a> or an alternative markup format. In general, they all allow content developers to work by writing plain-text documents in a structured format.

This approach keep content and design separate, while keeping all files as plain text. As developers, we’ve grown accustomed to an amazing suite of tools for working with plain text, so this is a huge step up from having all content dumped into a database as binary blobs.</p>

### Meta Data

Content rarely stands completely on its own. Readers will often want to know the author of a blog post, the date of the post, the categories it belongs to and so on.</p>

<figure><a href="https://jekyllrb.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e35f522-4772-4a8a-a30f-8259ae6bb918/jekyll-preview-opt.png" alt="Jekyll" width="500" height="402" /></a><figcaption><a href="https://jekyllrb.com/">Jekyll</a> has pushed the idea behind static site generators forward: now it could be powered by Markdown templates.</figcaption>When GitHub’s own Tom Preston Werner wrote <a href="https://jekyllrb.com/">Jekyll</a> to power his blog, he came up with a really interesting solution for representing meta data when working primarily with Markdown documents and templates: front matter.

Front matter is the bit of meta data, typically in YAML format, at the very top of a document:

<pre><code class="language-css">
title: Title of the document
categories:
- Category A
- Category B
---
# Actual content

This is the document
</code></pre>

This makes annotation of single-file documents with meta data straightforward, and it lends a simple human-readable text format to all of the data that would normally be stored in a much more opaque format in a database.
### Asset Pipeline
Front-end development today almost always involves several <strong>build tools and compilers</strong>. We want our assets to be minified and bundled. CSS preprocessors have gone from oddities to mainstream tools. And CoffeeScript and ECMAScript 6 transpiling have made compilers an integrated part of programming for the browser.

Most modern static website generators include an asset pipeline that handles asset compilation, transpiling, minification and bundling. Some are based on build tools, such as Grunt, Gulp and Broccoli, and let you hook into whole ecosystems of tasks and build steps. Others are more focused on streamlining a particular process or making sure a certain set of tools work well together without any complex configuration. Live browser refreshing when a file is saved has also become standard for many generators.
### Putting It All Together
A static website generator typically comes with a command-line UI for building a website or running a local server with your website for development.

Jekyll, for example, comes with a <code>jekyll build</code> command that you run from within a folder containing the source files for a Jekyll project, and it then outputs a completely static website in a <code>_site</code> subfolder.

Here’s what a simple source folder looks like:

<pre><code class="language-bash">_posts/
   2015-03-01-first-post.md
   2015-03-11-amazing-post.md
_layouts/
   default.html
_includes/
   main-nav.html
   index.html
   about.md
js/
   app.coffee
css/
   style.scss
   _config.yml
</code></pre>

This folder is a completely self-contained static website that can be uploaded to any static host or served from any normal web server.
## Why Now?

If all of this sounds pretty awesome, that’s because it is. But why is static website technology taking off now, and why did the early generators fail to make a dent in WordPress’ dominance? What’s changed? And how far can we take this?

Today’s generators play into a totally different ecosystem than their predecessors. Many of the constraints that made dynamic websites the best option for creating anything but the most basic online brochure have fallen away, although some remain.
### The Browser Is Growing Up
When Tim Berners-Lee launched the first website of the World Wide Web, a browser was a simple document viewer that could display hypertext, links and little else.

Today, we’re finally in the process of burying the last browser that has been holding the web back (RIP Internet Explorer 8). The modern browser is an operating system in its own right, no longer merely displaying documents downloaded from the web, but <strong>capable of running full-fledged web applications</strong>, making external calls to any CORS-compatible API, storing data locally, opening WebSockets to streaming servers, and even handling peer-to-peer connections to other browsers via WebRTC.

With the maturation of browsers, many features that used to require dynamic code running on a server can be moved entirely to the client. Want comments on your website? Add Disqus, Isso or Facebook comments. Want social integration? Add Twitter or Facebook’s JavaScript widget to your website. Want real-time data updating live on your website? Add a squirt of Firebase. Want search? Add Swiftype. Want to add live chat support? Olark is there. Heck, you can even add an entire store to a static website with Snipcart.

The list goes on and on, as a whole ecosystem of purely browser-based add-ons to websites is emerging. Apart from that, modern web apps built with Ember.js, AngularJS or React are often deployed entirely as static websites and served directly from a CDN with a pure API back end that’s shared between the website’s UI and the mobile client.
### The CDN Is Going Mainstream
When Akamai launched the first content delivery network in 1999, only the largest web properties in the world could afford to deliver their web assets from CDN edge nodes distributed all over the world. It wasn’t that long ago that CDNs were used only by companies at the scale of CNN and Facebook, rather than mere mortals.

While Akamai still has enterprise-level pricing, today anyone can sign up for Amazon AWS and put CloudFront on top of their website. Also, companies like Fastly, MaxCDN and CloudFlare offer CDN services at prices that even a small business can afford.

You could use a CDN with a dynamic website, but cache invalidation is one of those notoriously tricky problems in computer science. Getting the right balance between caching on edge nodes and running a dynamic system on a back end that is potentially doing ad-hoc computations on each request is tricky, to say the least.

A static website, on the other hand, can be readily deployed directly to a CDN and served straight from local caches near end users. Fiddling with the configuration still takes some time, and cache invalidation can be tricky, but it’s doable and can be completely automated with services such as Netlify.
### Performance Is A Must
The explosion of mobile devices has changed the face of the web in many ways. More and more visitors are coming to the web from a mobile device, sometimes on a 3G connection. Never has performance been as important as it is now.

We all know this data: 57% of online visitors will abandon a page if it takes longer than 3 seconds to load. People used to be willing to wait up to 10 seconds, but expectations are way higher today. And on mobile, where there’s no multi-tasking and little else to do, waiting for a website to load is so frustrating that more than 4% of people report that they’ve physically thrown their phone while using a slow mobile website!

No matter how much you optimize a dynamic website for performance or how many thousand of dollars you throw at it, it will never give you the same basic performance guarantee as a well-tuned static website hosted right on a CDN for a few bucks a month. With performance constantly growing in importance, it’s no wonder that developers are looking for ways to pre-generate their HTML, instead of letting the server spend time and resources on generating a page for every single HTTP request.</p>

<strong>Static website generation also eliminates a lot of performance concerns</strong> during the development process.

If you’re building a dynamic database-driven website, the efficiency of the database queries you’re making is extremely important because they’ll need to be fast enough to run once for every single HTTP request. Even if a solid caching layer lies on top of your website, there’s often a risk that some requests will effectively work as cache-busters, triggering worst-case queries in the back end and causing the whole system to grind to a halt.

With a static-generated website, it doesn’t matter much if pulling content into a template takes a few seconds more or less: That only happens when you publish, and there will never be a performance penalty for end users.
### Build Tools Are Everywhere
Compilers and build tools used to be something that C and Java programmers worried about, not something you would wield while building a website. Now, for better or worse, that has completely changed.

Today, front-end developers have adopted build tools, package managers and various kinds of compilers and transpilers wholesale. Grunt was the first front-end build tool to go mainstream, and now most new projects will have build steps.

With this prevalence of build tools, static website generators feel like a much more natural part of the front-end toolkit, whereas the traditional PHP-based tools for dynamic websites are starting to feel strangely alien to the modern front-end workflow.
## What’s Missing?

All of these forces have come together to create something like a perfect storm for static website generators, and it’s no wonder that more and more websites are being built statically.

It’s not all roses, though. Before static websites go fully mainstream, a few areas need to evolve.

Picking a static website generator and starting a project can still be a <strong>surprisingly rough experience the first time around</strong>. There are a lot of ins and outs and a lot of room for improvement in the tools, documentation and resources available.

While the ecosystem around static website generators is growing, it’s still a <strong>far cry from the mature theme marketplaces</strong> and support services of traditional dynamic platforms.

The biggest missing piece of the puzzle, however, is <strong>content editing</strong>. While working directly in Markdown in a text editor and pushing to GitHub is close to the ideal workflow for a front-end developer, it’s not something you’d get normal, non-technical end user to participate in.

Because of this, many websites built with static website generators currently end up being migrated to a dynamic CMS. There’s a huge need to bridge the gap between content editors and static website generation. Before that happens, static website generation will be reserved for a relatively small subset of today’s websites.

Some interesting “no-CMS” solutions are out there. The Verge has been using <a href="https://product.voxmedia.com/2014/7/29/5863004/take-a-peek-at-the-code-that-powered-the-verge-50">Google Sheets as a content layer for Middleman</a>; <a href="https://www.staticgen.com">StaticGen</a> uses Gist and the GitHub API as a kind of database; and Carrot use <a href="https://carrot.is/coding/static_cms">Contentful as a static CMS</a> to let non-techies produce content for its statically generated websites.

Others are working on tackling the general problem of how to best mix static website generation and content editing, and the coming years will no doubt bring exciting new ways of working with content and publishing.

Systems such as <a href="https://www.contentful.com/">Contentful</a>, <a href="https://prismic.io/">Prismic.io</a> and <a href="https://gathercontent.com/">GatherContent</a> decouple the CMS layer from the actual website builder. This makes them really interesting tools for multi-channel content management, where you’re writing content not just for a particular website, but also for a mobile app, a Facebook page or a white paper. Publishing new content triggers a webhook in a build system; then, a static website generator runs the build and fetches data from the content API; and the result is pushed straight to a CDN.

Another option for content editing is to <strong>work directly on the underlying repository</strong>.</p>

<figure><a href="https://prose.io/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12359a35-3e55-4de6-982b-a7203085c480/geek-opt.png" alt="Prose.io" width="500" height="331" /></a><figcaption>Markdown editor in a static generator <a href="https://prose.io/">Prose.io</a> which seamlessly integrates with GitHub's API.</figcaption></figure><a href="https://prose.io/">Prose.io</a> has been around for a while now, integrating with GitHub’s API to give content editors a somewhat more gentle UI in which to edit Markdown files in GitHub.

At Netlify, we’re working on an <a href="https://github.com/netlify/netlify-cms">open-source CMS</a>, without any lock-in to a particular static website generator, Git host or hosting platform. The goal is to make it work with almost all current static website generators, and we think it will be a great way to push the limit of what kind of website you can build within the constraints of modern static website technology.

Obviously, there will always be websites that are simply not a good fit for static generation — especially ones whose core content is a constantly updating feed or ones with an extremely high volume of content that relies heavily on search and filtering.

That being said, static website generators will continue to grow in capability and popularity. The infrastructure and ecosystem will keep maturing. And as the tools improve, we’ll see developers push the limit of what can be done with static websites.

At Netlify, we’re already starting to see large content-driven websites, with real-time search, multi-language regions and content, and private sections being built with static website generators and content APIs. With awareness of the importance of performance and security increasing, you can expect to see much more of this.

{{< signature "al, ml, jb" >}}

</figure>


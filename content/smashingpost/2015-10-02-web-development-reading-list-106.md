---
title: 'Web Development Reading List #106'
slug: web-development-reading-list-106
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2781294f-1ab9-40b9-8e05-a81f71caa135/postcssoncodepen-opt.png
date: 2015-10-02T15:15:25.000Z
author: anselm-hannemann
description: >-
  _**What's happening in the industry?** What important techniques have emerged
  recently? What about new case studies, insights, techniques and tools? Our
  dear friend [Anselm
  Hannemann](https://www.smashingmagazine.com/author/anselm-hannemann/?rel=author)
  is keeping track of everything in the [web development reading
  list](https://wdrl.info/) so you don't have to. The result is a carefully
  collected list of articles that popped up over the last week and which might
  interest you. — Ed._

  Every week I feature about twenty interesting links. Although I curate this
  reading list already from more than 50 resources, every week still leaves you
  with so much news that actually paying attention to all of it is quite
  difficult. I often hear from people “I must admit, I haven’t read your last
  WDRLs in detail. Sorry.” What do I reply? Well, I embrace this behaviour.
  Sometimes it’s not possible to read everything. As Tim Kadlec writes in his
  latest piece, you can’t know everything: “[In fact, we can’t know everything
  about the web.](https://timkadlec.com/2015/09/the-fallacy-of-keeping-up/)
categories:
  - Web Development Reading List
---
<em><strong>What's happening in the industry?</strong> What important techniques have emerged recently? What about new case studies, insights, techniques and tools? Our dear friend <a href="https://www.smashingmagazine.com/author/anselm-hannemann/?rel=author">Anselm Hannemann</a> is keeping track of everything in the <a href="https://wdrl.info/">web development reading list</a> so you don't have to. The result is a carefully collected list of articles that popped up over the last week and which might interest you. — Ed.</em>

Every week I feature about twenty interesting links. Although I curate this reading list already from more than 50 resources, every week still leaves you with so much news that actually paying attention to all of it is quite difficult. I often hear from people “I must admit, I haven’t read your last WDRLs in detail. Sorry.” What do I reply? Well, I embrace this behaviour. Sometimes it’s not possible to read everything. As Tim Kadlec writes in his latest piece, you can’t know everything: “<a href="https://timkadlec.com/2015/09/the-fallacy-of-keeping-up/">In fact, we can’t know everything about the web.</a>”

## <span class="rh">Further reading</span> on Smashing:

*   [Are You Loosing Traffic By Poor Website Performance?](https://www.smashingmagazine.com/2010/01/page-performance-what-to-know-and-what-you-can-do/)
*   [Everything You Need To Know About Google’s AMPs](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)
*   [Front-End Performance Checklist 2017 (PDF, Apple Pages)](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)
*   [Progressive Web AMPs](https://www.smashingmagazine.com/2016/12/progressive-web-amps/)

## News

*   Only about two months from now, PHP7 will finally be released. [Get your source code ready](https://kinsta.com/blog/getting-ready-for-php7/) for it now to make advantage of the new features and performance improvements.
*   Safari 9 now has a [`shrink-to-fit: no` property in the viewport](https://jsbin.com/fubunucopi/4/edit?html,output) meta element [as the `initial-scale` property has been changed on purpose](https://www.reddit.com/r/web_design/comments/3la04p/psa_safari_on_ios9_has_a_media_query_bug/) in the new WebKit version.
*   Asynchronous code gets easier with [ES2016 Async Function support](https://blogs.msdn.com/b/eternalcoding/archive/2015/09/30/javascript-goes-to-asynchronous-city.aspx). It’s now available in Chakra and [Microsoft Edge](https://blogs.windows.com/msedgedev/2015/09/30/asynchronous-code-gets-easier-with-es2016-async-function-support-in-chakra-and-microsoft-edge/) when you enable the experimental features in the browsers.</p>

## Concepts & Design

*   Lately, mainly due to the rise of UI frameworks and the increased complexity of front-end frameworks and web apps, the web has got a bit boring. We see tons of similar layouts, and whether it’s a Bootstrap-based design or Material UI-based design, everything is still remarkably similar. And while applying such design principles makes life much easier for us, developers, we lose the diversity and individuality of the web. No wonder then that [a plea to make the web weird again](https://signalvnoise.com/posts/3948-a-rallying-cry-for-the-weird-wild-web) is gaining traction.</p>

## Tools

*   PostCSS is the latest thing in the CSS world. The “[PostCSS Deep Dive](https://webdesign.tutsplus.com/tutorials/postcss-deep-dive-what-you-need-to-know--cms-24535)” explains what it is (not a pre-/not a post-processor), what it can do and how to get the most value out of it.
*   If you use PostCSS, [stylelint](https://github.com/stylelint/stylelint/) is a new option to set and lint your CSS.
*   You might know JSLint, its successor JSHint but you might have thought “why do we need another one?” when you first heard of ESLint. [This article by Nicholas C. Zakas](https://www.smashingmagazine.com/2015/09/eslint-the-next-generation-javascript-linter/) tells you why he wrote another linter which has several advantages that you might want to check out.
*   If you always found Vagrant a bit complicated and not intuitive, their makers now created a successor (although not a replacement) for Vagrant: Meet [otto](https://ottoproject.io/), a tool that combines development environment setup with automatic deployments in an easy-to-use way.

{{% feature-panel %}}

<figure><a href="https://webdesign.tutsplus.com/tutorials/postcss-deep-dive-what-you-need-to-know--cms-24535"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2781294f-1ab9-40b9-8e05-a81f71caa135/postcssoncodepen-opt.png" alt="Post CSS" width="500" height="273" /></a><figcaption>“<a href="https://webdesign.tutsplus.com/tutorials/postcss-deep-dive-what-you-need-to-know--cms-24535">PostCSS Deep Dive</a>” explains what it is (not a pre-/not a post-processor), what it can do and how to get the most value out of it.</figcaption></figure>

## Security

*   Paul Lewis summed up why the current approach of CORS, CSP, HTTPS and other security layers is doomed and unusable for many people unless we change this for the better and care about real-world use-cases. [CORS for Concern](https://aerotwist.com/blog/cors-for-concern/) shows the pitfalls of our centralized infrastructure in the shift towards a more secure web.</p>

## Privacy

*   This pretty frightening article, released last week by _Intercept_, shows how intelligence companies have broken our web and can spy nearly everyone by [tracking all metadata from everyone](https://theintercept.com/2015/09/25/gchq-radio-porn-spies-track-web-users-online-identities/) using online music networks, cookies, video sites, blogging platforms, calls, or photos and online ads. In light of this development, it’s important that we give more focus on privacy for our users by implementing HTTPS (with HSTS, HPKP), limit advertising network’s data grabbing and prevent MITM attacks by using resource integrity hashing for our CDNs.</p>

## Web Performance

*   Nolan Lawson wanted to know more about [the performance of in-browser storage](https://nolanlawson.com/2015/09/29/indexeddb-websql-localstorage-what-blocks-the-dom/) and how it affects the DOM. Turns out it’s complicated and varies from browser to browser and depends on whether you want to achieve better I/O performance or want to avoid a DOM rendering block.
*   A behind-the-scenes article by Flickr back-end developers shows [how to speed up image resizing services by using the GPU](https://code.flickr.net/2015/06/25/real-time-resizing-of-flickr-images-using-gpus/) for it.
*   Yoav Weiss explains why the current draft of the NetInfo API is not what we want as developers and why [it’s more important that we start adapting our websites and applications without assumptions](https://blog.yoav.ws/adapting_without_assumptions/).</p>

## JavaScript

*   If you use Ember but couldn’t follow the documentation on [run loops](https://guides.emberjs.com/v1.10.0/understanding-ember/run-loop/), here is [a free guide for Ember Run Loop](https://netguru.co/blog/free-ember-run-loop-guide).
*   For years we needed to use Flash to copy/paste actions but now we can finally achieve it with plain JavaScript. Zeno Rocha’s [clipboard.js](https://github.com/zenorocha/clipboard.js) makes it easy — and brings a nice fallback for non-supporting browsers.
*   ponyfoo’s article series about ES6 is now continued and an [in-depth article explains ES6 Promises](https://ponyfoo.com/articles/es6-promises-in-depth), so you can finally understand how they work. Oh yeah, and to make it even better, you can [use the tool Promisees to visualize promises](https://bevacqua.github.io/promisees/).
*   If you ever wanted to have a customized YouTube player, you can use [youtube.js library](https://github.com/ginpei/youtube.js) for it.
*   Apple’s new [3D force touch action is available in JavaScript](https://github.com/freinbichler/3d-touch). Learn more on how to use and respond to these actions in [a framer.js blog post](https://blog.framerjs.com/posts/prototyping-3D-touch-interactions.html).

## CSS / Sass

*   Chris Coyier wrote up [the different possibilities to do knockout text](https://css-tricks.com/how-to-do-knockout-text/). And while for a long time, Photoshop was the only way to achieve this effect, we now can do it with SVG, and even with CSS to some degree.</p>

## Work & Life

*   Paul McMahon was annoyed by so many job postings that don’t reflect what a company does or don't mention what actually matters. Now he wrote an article on [how to write job postings](https://www.tokyodev.com/2015/08/28/writing-developer-job-posting/) with a lot of helpful tips. If you are hiring, take these hints and improve your job postings.</p>

## Go beyond…

*   I stumbled upon this article last week and it sounded very weird. But when I read that we already lost about 3/4 of our planet’s genetic diversity and [some smart people try to store the remaining seeds](https://www.catchnews.com/environment-news/the-svalbard-global-seed-vault-stores-8-40-000-species-of-seeds-and-it-just-saw-a-withdrawal-1442978019.html) we have around the world, I got interested. I’m happy that some people care about sustainability and how our descendants could re-trace what we did during our life.
*   “[Dear Tech Industry,](https://the-pastry-box-project.net/jenn-downs/2015-september-24)” starts this excellent article by Jenn Downs on why companies and people in the tech industry shouldn’t think they’re smarter just because they know more on technology. Instead, it’s important that we give back and contribute to local charities and culture.
*   The [gnome outreachy](https://www.gnome.org/outreachy/) program is a great way to get involved with open source software and improve it. Mozilla now shared [the roadmap on where you could help out in the next months](https://wiki.mozilla.org/Outreachy/2016/December_to_March).

And with that I’ll close for this week. In case you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via E-Mail, RSS and online.

<em>Thanks and all the best,
Anselm</em>


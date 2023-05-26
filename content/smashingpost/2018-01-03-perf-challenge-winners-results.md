---
title: 'The Front-End Performance Challenge: Winner And Results'
slug: performance-challenge-winners-results
author: cosima-mielke
image: //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e75711f-1456-4bce-b4bb-d8c117ed55db/performance-challenge-800w-opt.png
date: 2018-01-03T16:15:37+01:00
summary: >-
  Thanks to everyone who participated in the challenge! We were quite happy with the quality of the submissions we received, and it honestly wasn't easy to choose a winner. Keep up the brilliant work!
description: >-
  A few weeks ago, we asked the community to use everything they could to make their websites and projects perform blazingly fast. Today, we're happy to finally announce the winner.
categories:
  - Performance
  - Smashing
---
A few weeks ago, we asked our readers and the community to use everything they could to make their websites and projects perform blazingly fast. Today, we're thrilled to show off the results of this challenge and announce the winner who will be awarded with some smashing prizes indeed!

What prizes, you ask? The winner wins a roundtrip flight to London, full accommodation in a fancy hotel, a ticket to SmashingConf London 2018, and last but not least, a Smashing workshop of their choice.

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e75711f-1456-4bce-b4bb-d8c117ed55db/performance-challenge-800w-opt.png" sizes="100vw" caption="The cards are finally on the table. It's time to meet the winner of the challenge and send him off to <a href='/events/london-2018/'>SmashingConf London</a>!" alt="The Front-End Performance Challenge" >}}

## Challenge? What Challenge?

Well, the task was not as simple as it sounded. The contestants were asked to [improve the performance of a website](https://www.smashingmagazine.com/2017/10/front-end-performance-challenge/) while keeping the final visual appearance identical before and after. Font loading was allowed to differ, and reflows were acceptable as long as they were kept to a minimum.

While choosing the lucky winner, we looked into the results presented by Lighthouse and WebPageTest, as well as the complexity of the websites our participants had worked on, of course. The **first meaningful paint** and the **time to interactive** were the most critical metrics.

But enough hard facts for now. We know you're curious already, and we don't want to keep you in suspense any longer. So here it is, the winning project.

{{% feature-panel %}}

## And The Winner Is...

### Leonardo Losoviz

The optimization techniques presented in Leonardo's submission are all DIY, designed and implemented from scratch. He added all the optimizations to [PoP](https://getpop.org/), an open-source framework to build websites, and used [Agenda Urbana](https://agendaurbana.org/es/) to test the performance improvements on an actual project.

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f24d454b-bb08-4794-8e86-e8b134b4797f/perf-challenge-agendaurbana-opt.png" sizes="100vw" caption="(<a href='https://agendaurbana.org/es/'>Live website</a>)" alt="Agenda Urbana" >}}

We felt this submission really entered into the spirit of the challenge by not only improving the performance of a single website but attempting to make enhancements to a framework used on a number of websites. The fact that PoP is backed by WordPress meant that Leonardo was in a similar situation to many people unable to do some of the things available to a JavaScript framework. As he noted:

<blockquote>PoP is built on top of WordPress. That means that many innovative optimization techniques available to Javascript frameworks, such as code-splitting using Webpack or Service Workers through sw-precache, are out of reach (at least so without a big workaround). As such, all the optimization techniques described below are all DIY, designed and implemented from scratch.</blockquote>

If you're interested in digging into all the nitty-gritty details of <a href="https://smashingmagazine.com/provide/performance-challenge/performance-challenge-leonardo-losoviz.zip">his submission</a>, feel free to do so. We all enjoyed reading the details of Leonardo's optimizations and felt him a worthy winner due to the sheer amount of work that had gone into this entry.

## All Submissions

We were very pleased with the quality of the submissions we received, and it honestly wasn't easy to choose a winner. Thanks to everyone else who submitted — keep up the brilliant work!

### Jorgen Verweij

Jorgen Verweij presented an optimized version of his company website [Perplex Internetmarketing B.V.](https://www.perplex.nl). Together with a team made up of a UX'er, a front-end, and a back-end developer, and a system administrator, he set out on the performance endeavor. 

The result is an excellent implementation with excellent perf results across the board: SpeedIndex far under their set goal of 1250, a load time of less than 1 second, start render in half a second, a 100/100 PageSpeedscore and an almost perfect Lighthouse audit. Compared to the [old situation](https://slow.perplex.eu/), the load time is almost eight times quicker. Kudos! You can read more details on the process in this comprehensive [write-up](https://smashingmagazine.com/provide/performance-challenge/performance-challenge-jorgen-verweij.pdf) which Jorgen put together.

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81040e8f-e57c-4e1c-a745-bfec02210b3a/perplex-perf-challenge-opt.png" sizes="100vw" caption="(<a href='https://www.perplex.nl'>Live website</a>)" alt="Perplex Website" >}}

### Marco Hengstenberg

Marco Hengstenberg submitted an optimized version of the tourism agency website *[Land in Sicht](https://www.land-in-sicht.de/)*. To improve performance, Marco used quite a lot of nifty little tricks and techniques. Preloading the main stylesheet and critical font loading with preload in supporting browsers are only two of them. He also restructured the HTML to make it as flat, semantic and accessible as possible and reduced the amount of data initially transferred on first visit from nearly 3MB to 1.3MB on desktop (and due to the usage of responsive images for the hero image, it is even less than that on narrow screens). 

To streamline the site, even more, Marco removed Bootstrap, jQuery, and Modernizr, set up a build process with Grunt, and introduced a ServiceWorker which makes the site available offline, too. The effort was worth it: The [result](https://www.webpagetest.org/result/171107_TK_ad500454613c3f4fbf1f0a9670b265cd/) is a dramatic TTL that dropped from 32 seconds to 2 seconds and nearly a 50% decrease in HTTP requests and bytes transferred (also see the [Lighthouse report](https://smashingmagazine.com/provide/performance-challenge/performance-challenge-marco-hengstenberg.zip), ZIP 251KB). Preload and quick initial render both help on perceived load time. Great work!

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa4cceeb-6a79-4438-9f83-3423e7f57699/land-in-sicht-frontpage-opt.png" sizes="100vw" caption="(<a href='https://www.land-in-sicht.de/'>Live website</a>)" alt="Land in Sicht" >}}

### Gabriel Mariani

The [San Diego Christian College](https://sdcc.edu/) website was the one that Gabriel Mariani applied his performance skills to. He divided the optimization process into four steps. First, he cropped all images to the maximum size they were actually needed in and created mobile-scaled versions of them. He then made all images lazy load. The second step focused on JavaScript and removing all the inline scripts which the WordPress site and its 3rd-party theme and plugins came with. Then he enqueued as many scripts as possible so that Autoptimize could pick them up and minify/combine them into a single file. 

Gabriel also trimmed down the number of fonts being used and set the Google fonts to load in `async` so that the critical path CSS will load first. Last but not least, he addressed some other small odds and ends like customizing WordPress plugins, so they rely on ajax instead of PHP. This allowed him to enable page caching and eventually enable a CDN for the site. A switch to HTTP/2 and HTTPS was the final step. See [WebPageTest](https://www.webpagetest.org/result/180102_XJ_abb6072832008f7a4a499a6d813ad992/) for the full results. Nice!

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4a9004b-9e6e-4f2b-bd2b-448a5ede2b54/sdcc-edu-perf-challenge-opt.png" sizes="100vw" caption="(<a href='https://sdcc.edu/'>Live website</a>)" alt="SDCC frontpage" >}}

### Alexander Zarges

Alexander Zarges developed [Cloud Player](https://cloud-player.io/), a single page web application based on Angular 4 that lets you search and play YouTube and SoundCloud apps. The upgraded version uses the Angular ahead-of-time compiler to achieve an initializing time of around [2.9 seconds](https://www.webpagetest.org/result/171031_84_e7b78e291a2a679fa38be7650ca9be78/) (compared to [5.2 seconds](https://www.webpagetest.org/result/171031_Z5_52000e95ede5f87a97d4ec08b5dce319/) when using the just-in-time compiler). If you want to dive deeper into the code, check out the accompanying [GitHub repository](https://github.com/Cloud-Player/web). 

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ae8cf9b-4c3f-4ef9-af00-0863985b98a6/cloud-player-preview-opt.jpg" sizes="100vw" caption="(<a href='https://cloud-player.io/'>Live website</a>)" alt="Cloud Player" >}}

### Bradly Taunt

Bradley Taunt took our challenge as an occasion to experiment with his personal site. As the basis for his optimization undertaking, he used his [homepage](https://bradleytaunt.com/) and an [image-heavy article](https://bradleytaunt.com/the-death-of-personality/). To slim down loading times to [4.2 seconds](https://www.webpagetest.org/result/180102_Y1_09a2e6f1716844f3354abd13252fd684/) for the article, Bradley defaults to the user's OS System Fonts instead of using web fonts, among other things. 

For an extra boost, the optimized version also inlines critical CSS, serves responsive images, and utilizes CDN caching. You can get a more detailed look behind the scenes, in the [blog post](https://bradleytaunt.com/chasing-performance/) that Bradley wrote about how he tackled the challenge.

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d90ad96-380b-4dbb-bf31-1dca0bfee8ba/bradleytaunt-perf-challenge-opt.png" sizes="100vw" caption="(<a href='https://bradleytaunt.com/'>Live website</a>)" alt="Bradley Taunt Website" >}}

### John Beales

John Beales challenged himself to give [4RoadService.com](https://www.4roadservice.com/) a performance boost. When he started out there were already some optimizations in place. Static images were run through ImageOptim, for example, CSS and JS were minified, they were running a CDN through CloudFlare, and the site already used a Single-Page-App-style loader so new content is always fetched by XHR and the page is never completely redrawn. 

For this challenge, John turned on Image Optimization and WebP compression in Cloudflare. The updated site now uses HTTP/2 Server Push to send out the main CSS and JS files with the initial pageload and relies on Guetzli for JPEG compression. To optimize caching, he updated the URLs of all static assets so that the URL will change whenever the asset changes, then set all static assets to cache for a year. For improved image caching, John also updated the URLs of dynamically-resized images so CloudFlare thinks they're static image files. 

The result: The first meaningful paint dropped from 2,220ms to 1,290ms and the First Interactive from 5,480ms to 3,040ms. You can view the full Lightbox and WebPage Test results [here](https://www.dropbox.com/sh/p1lfyfe7pu14ll5/AABn0O9PpBvdgySwpjdf4PTva?dl=0).

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bf1d780-982e-4eda-b021-c13f49d36e78/4roadservice-perf-challenge-opt.png" sizes="100vw" caption="(<a href='https://www.4roadservice.com/'>Live website</a>)" alt="4RoadService" >}}

### Shaun O'Connell

Shaun O'Connel's entry was the work he did on [kiwi.ruby.nz](https://kiwi.ruby.nz/). The aim was to turn the conference website into a PWA so conference attendees could look up all information concerning the event offline. Some of the things he did: replacing a typical Google Maps iframe with Google Static Maps, self-hosting subset fonts, moving CSS inline to keep the first request under 14KB, removing dependencies, adding pre-cache Service Workers, and adding Turbolinks for snappy page transitions. By doing so, the initial render time dropped from 3.9 seconds to 0.3 seconds. 

For more details check out the [WebPageTests](https://github.com/rubynz/conf/issues/30).

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d52fc3a-94b0-4a6b-9a7f-355c270b567e/kiwi-ruby-nz-perf-challenge-opt.png" sizes="100vw" caption="(<a href='https://kiwi.ruby.nz/'>Live website</a>)" alt="Kiwi Ruby" >}}

### Ruslan Julbarissow

Ruslan Julbarissow submitted his personal website [zerofy.de](https://zerofy.de/). Since he finished his optimization work shortly before the contest was published, there are, unfortunately, no detailed before results, but Ruslan made a good [write-up](https://smashingmagazine.com/provide/performance-challenge/performance-challenge-ruslan-julbarissow.pdf) of how his tweaks led to a page size of 1.6KB and a TTFB of 197ms. Apart from caching, minifying, GZIP, and jQuery tweaks, he loads fonts afterward to avoid render blocking, and by replacing FontAwesome with a customized IcoMoon set of 10 icons, he managed to save an additional 130KB. 

To boost the speed index score and get the fastest experience possible, he also created a separate PHP file which contains all CSS styles affecting the above-the-fold view. A nice detail: The tiny script Barba.js allows him to create page transitions without reloading the whole site.

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6700d93d-7089-4f9c-a3b9-c05c68819e96/zerofy-perf-challenge-opt.png" sizes="100vw" caption="(<a href='https://zerofy.de/'>Live website</a>)" alt="zerofy" >}}

## Thank You To Everyone For Participating

Phew! Now *that* was quite a challenge indeed! For those of you who enjoy such a good challenge and a brain tickle every now and then, stay tuned for the next challenge. We'll be coming up with another one in no time — that's for sure!

{{< signature "rb, ra, vf, ms, il" >}}


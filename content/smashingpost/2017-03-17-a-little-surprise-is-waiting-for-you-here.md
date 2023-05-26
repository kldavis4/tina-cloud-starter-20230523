---
title: A Little Surprise Is Waiting For You Here.
slug: a-little-surprise-is-waiting-for-you-here
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bc58a21-e5c1-4870-b433-4ea9979b67c9/redesign-front-page-desktop-500w-opt.png
date: 2017-03-17T06:21:39.000Z
author: vitaly-friedman
summary: >-
  Smashing Magazine is changing: a new design, a new layout, a new technical stack, a new printed magazine, a new Smashing Membership, and the same good ol’ obsession with quality content. Here’s a sneak preview of what’s coming up.<br /><br />Today marks an important milestone in Smashing Magazine’s life, and this very page is an early preview of what’s coming up next: many experiments, new challenges, but still a good ol’ obsession with quality content. A complete overhaul, both visually and technically, a fine new printed magazine, and a shiny new _Smashing Membership_, with nifty features and goodies for you, our lovely community. Curious? Well, fasten your seatbelt and [browse around](https://www.smashingmagazine.com) &mdash; it’s going to be quite a journey!
description: >-
  Today marks an important milestone in Smashing Magazine’s life, and this very page is an early preview of what’s coming up next: many experiments, new challenges, but still a good ol’ obsession with quality content.
categories:
  - Events
  - Redesign
  - Membership
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---
No, this is not a broken page or a sneaky landing page. Today marks an important milestone in Smashing Magazine’s life, and this very page is an **early preview of what’s coming up next**: many experiments, new challenges, but still a good ol’ obsession with quality content. A complete overhaul, both visually and technically, a fine new printed magazine, and a shiny new _Smashing Membership_, with nifty features and goodies for you, our lovely community. Curious? Well, fasten your seatbelt and [browse around](https://www.smashingmagazine.com) — it’s going to be quite a journey!

Today, we are happy to announce the public open beta of the next Smashing Magazine, [next.smashingmagazine.com](https://www.smashingmagazine.com), with a new design, but one with a few bugs and issues that have to be… you know, _smashed_ first. (Sorry about that!) The big-bang release is scheduled for later this year (probably early May to June). Some things now might be broken or just plain weird — we still have a bit of work to do, so do please [let us know](https://www.twitter.com/smashingmag) if you encounter any issues (and you definitely will!).</p>

## The Almighty Smashing Magazine’s Redesign

Over the last 18 months, we’ve been working with [Dan Mall](https://twitter.com/danmall), [Sara Soueidan](https://twitter.com/SaraSoueidan), [Ilya Pukhalski](https://twitter.com/pukhalski), [Matt Biilman](https://twitter.com/biilmann), [Ricardo Gimenes](https://twitter.com/behindcadi), [Andrew Clarke](https://twitter.com/Malarkey) and the [Netlify](https://twitter.com/Netlify) team on a complete overhaul of this little website, both technical and visual.

What’s different? Well, _everything_. The website won’t be running on WordPress anymore; in fact, it won’t have a back end at all. We are moving to a [JAMstack](https://www.smashingmagazine.com/2016/08/using-a-static-site-generator-at-scale-lessons-learned/): published directly to [Netlify CDNs](https://www.netlify.com), with a custom shop based on an open-sourced headless E-Commerce [GoCommerce](https://www.gocommerceapi.org/) and a job board that’s all just static HTML; content editing with Netlify’s new open-source, [Git-Based CMS](https://netlifycms.org/), real-time search powered by [Algolia](https://www.algolia.com/), full HTTP/2 support, and the whole website running as a **progressive web app** with a service worker in the background (thanks to the awesome [Service Worker Toolbox](https://github.com/GoogleChrome/sw-toolbox) library). _Booo-yah!_

{{% pull-quote %}}
 We don’t really have a back-end. Instead, static HTML, advanced JavaScript APIs, running as a progressive web app with a service worker in the background and blazingly fast performance — served from a CDN near you.
{{% /pull-quote %}}


How does it work? Quite simple, actually. Content is stored in Markdown files. HTML is pre-baked using the static site generator [Hugo](https://gohugo.io/), combined with a modern asset pipeline built with Gulp and webpack, all based on the [Victor Hugo boilerplate](https://github.com/netlify/victor-hugo).

We’ve spiced it all up with a handful of fancy APIs, including ones by [Stripe](https://stripe.com/) for payments, [Algolia](https://www.algolia.com/) for search, [Cloudinary](https://cloudinary.com/) for responsive images, and Netlify's open-source APIs [GoCommerce](https://github.com/netlify/gocommerce) (a headless e-commerce API), [GoTrue](https://www.gotrueapi.org/) for authentication, and [GoTell](https://github.com/netlify/gotell) for our more than 150,000 comments.</p>

<figure class="article__image break-out"><img
sizes="(max-width: 1400px) 100vw, 1400px"
srcset="
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bfeef17-0d83-45a4-8e87-3ce68ffe4fa5/redesign-front-page-mobile.png 414w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92eddf14-65fe-42ff-8a38-be8ebc6443fa/redesign-front-page-tablet.png 703w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82424315-c27a-4d3f-8b45-d8cd92419b00/redesign-front-page-laptop.png 1080w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d516fac2-061b-412d-a31e-3454f29679c5/redesign-front-page-desktop.png 1400w"
src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c49cc4e4-67a9-4b75-8842-936fdff7432d/redesign-front-page.png,w_1400.png"
alt="A shiny new Smashing Magazine's front page"><br>
<figcaption>The shiny new <a href="https://www.smashingmagazine.com">Smashing Magazine</a>. After 18 months, we are now finally happy to launch the public, open beta.</figcaption></figure>

</picture>

Every time content changes, it’s all pushed to Netlify’s CDN nodes close to you. We do our best to ensure that content is **accessible and enhanced progressively**, with performance in mind. If JavaScript isn’t available or if the network is slow, then we deliver content via static fallbacks (for example, by linking directly to Google search), as well as a service worker that persistently stores CSS, JavaScripts, SVGs, font files and other assets in its cache. The dynamic components in JavaScript are all based on [Preact](https://preactjs.com/), and most pages you’ll see on the website will have been fully pre-rendered, prebuilt and deployed, ready to be served from a CDN near you.</p>

## Why Such A Big Change?

That's a good question to ask. There are a couple of reasons. In the past, we were using WordPress as a CMS, our job board was running on Ruby, and at one point we switched to Shopify from Magento for our online shop. Not only was **maintenance** of four separate platforms incredibly complicated, but designing a consistent, smashing experience the way we envisioned it proved to be nearly impossible due to technical restrictions or requirements imposed by these platforms.

Maintaining and developing every platform separately was expensive and time-consuming, and in many ways, creating a cohesive experience where a user would literally "flow" from one area to another, was difficult. As a result, because some areas were more important from the business perspective, they were growing and evolving fast, while the others were **decaying in the dark**. This led to an inconsistent, incohesive, and frankly quite annoying and disappointing experiences. And even if we wanted to make major changes, it was a big, challenging undertaking since we were using different platforms, stacks and at some point even different designs.</p>

<figure class="article__image break-out"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f8f389d-715b-4655-badc-4cf1f16f915b/search-opt.png" alt="Inline search on SmashingMag"><figcaption>For inline search, by default, we deliver Google search, and if there are no JavaScript errors, we enhance the experience with inline search powered by Algolia’s API.</figcaption></figure>

**Performance** was another reason. With a proper CDN, full HTTP/2 support and service workers in place, last year we managed to beat the performance results we had so far. However, even with a fancy nginx build, the performance we could get with a pre-built websites enhanced with JavaScript was nothing short of breathtaking. We are looking forward to optimize the HTTP/2 delivery and add some minor and major improvements and measure the results, but the initial test showed the Start Render time hitting around 500–600ms, an Time To Interactive under 1s. We couldn't reach the same performance with WordPress and LAMP stack in place.

Today, for the first time in 10 years, we were able to define a smashing experience from scratch and implement it from very start to finish. When it comes to interaction design, asking all the right questions is not enough; it also matters _how_ and when those questions are asked. You will find some of these (unusual) decisions pretty much everywhere on the site.

In fact, as you might have noticed, visually we’ve introduced some major changes as well. In the previous design, we always struggled to find good spots to **prominently display our books** and eBooks and conferences; one major goal of the redesign was to change that. We looked for a way to bring our products to the forefront, but without making them feel like advertisements; they had to fit the overall visual language and layout we were developing. The truth is that you’re probably using an ad blocker (more than 60% of our readers do), and if most users don’t see the ads, what’s the point of having them? Instead of pushing advertising to the limit, we’ve taken the drastic decision of **removing advertising almost entirely**, focusing instead on featuring our lovely products.

<figure class="article__image break-out"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/922b01a0-385f-4309-b469-5dcae425b780/cats-preview-opt.png" alt="Look closely... can you spot them all?"><figcaption>The new design does feature many cats. In fact, if you look closely, you’ll find 55 cats spread across the website. Can you spot them all? The first three people who do will get a ticket to a SmashingConf of their choice — guaranteed! Good luck!</figcaption></figure>

Now, have you noticed yet something consistently shining through in the new design? As part of the relaunch, we took our time to study and rediscover our signature and personality, and we’ve highlighted it prominently in every component of the page. We designed **56 different cats** (yes, cats) that will be appearing throughout the website in various places, and if you take the time to _find them all_, then you’d probably deserve a free ticket to one of our conferences. We’ve also leaned even more heavily towards our logo: Most elements on the page are tilted at just such an angle. We’re also using transitions and animations (work in progress!) to keep interactions smooth and clear, which we didn’t do before.

Now, the redesign is just a part of the story. We’ve got something new cookin’, too: the _Smashing Membership_, with webinars, workshops and whopping discounts and _Smashing Magazine Print_, our new, physical, printed magazine — and we wanted them to be an integral part of the site. After years of refining the ideas, now it’s finally happening. However, they deserve a standalone article — just like a detailed overview of the design process and what we’ve learned in the last 18 months.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44c04544-82da-4be0-bec0-d629fb4d0f78/better-together-03-opt.png" alt="It’s been a long journey already, but it was all worth it."><figcaption>It’s been a long journey already, but it was all worth it.</figcaption></figure>

## Up For The Next Part Of Our Journey?

So, here we go! Please feel free to [browse around](https://www.smashingmagazine.com) — and be prepared to discover all kinds of cats... oh, _things_. As it is always the case with an open beta, there are still a good number of bugs to be smashed, and we are on it. Still, please do [report issues and bugs on GitHub](https://github.com/smashingmagazine/redesign/issues/new) — the more, the merrier! We can’t wait to read your feedback in good ol’ social media and in the comments. _Meow!_ — and look out for the next articles of the series! ;-)

{{< signature "ms, il, al" >}}

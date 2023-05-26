---
title: 'How Smashing Magazine Manages Content: Migration From WordPress To JAMstack'
slug: migration-from-wordpress-to-jamstack
author: sarahdrasner
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/728fcd64-c97a-4834-89d9-660cf7ace0c7/migration-from-wordpress-to-jamstack.png
date: 2020-01-28T10:00:00.000Z
summary: >-
  WordPress adoption is massive. So why would a WordPress site consider moving to JAMstack? In this technical case study, we’ll cover what an actual WordPress migration looks like, using Smashing Magazine itself! We’ll talk through the gains and losses, the things we wish we knew earlier, and what we were surprised by.
description: >-
  WordPress adoption is massive. So why would a WordPress site consider moving to JAMstack? In this technical case study, we’ll cover what an actual WordPress migration looks like, using Smashing Magazine itself! We’ll talk through the gains and losses, the things we wish we knew earlier, and what we were surprised by.
categories:
  - WordPress
  - Jamstack
  - Generators
  - Static Generators
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Netlify
  link: https://url.netlify.com/rkaJnT46S
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcf23ab4-3a5e-4a81-b79f-b520b5dcf6a2/netlify-full-logo-light.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://url.netlify.com/rkaJnT46S" style="text-shadow: none;">Netlify</a>, an all-in-one platform for automating modern web projects. <em>Thank you!</em>
---

<p>Every time developers talk about WordPress, their market share percentage changes. “<em>20% of all sites are on WordPress!</em>” “<em>40% of all sites are on WordPress!</em>” Whatever the percentage is, the message is the same: in terms of adoption, WordPress is MASSIVE.</p>

<p>So why, with that kind of adoption, would a site that’s using WordPress consider moving to <a href="https://jamstack.org/">JAMstack</a>? In this two-part article series, we’ll cover what an actual WordPress migration looks like, using a case study of the very site you’re reading from right now.</p>

<p>We’ll talk through the gains and losses, the things we wish we knew earlier, and what we were surprised by. And then we’ll follow it up with a <a href="https://www.smashingmagazine.com/2020/02/headless-wordpress-site-jamstack/">technical demonstration</a> of one possible migration path &mdash; not off WordPress completely &mdash; but how you can serve decoupled WordPress so that you can have the best of both worlds: a JAMstack implementation of WordPress that gives you all the power of their dashboard and functionality, with better performance and security.</p>

Let’s dig in!

## Why?

In 2015, [Netlify](https://url.netlify.com/rkaJnT46S) co-founder Mathias Biilmann and Smashing founder Vitaly Friedman talked shop. As JAMstack architecture started making rounds, Smashing has got more interested in the idea of the stack. Vitaly and Markus (former managing director at Smashing) asked Matt what would happen if Smashing migrated from their traditional WordPress/LAMPstack site to a JAMstack architecture.

As an experiment, Matt scraped all the HTML from Smashing and hosted it on Netlify, delivering the content statically from a CDN. [The results were compelling](https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/) &mdash; the static version is more than six times as fast on average!

This type of architecture works so well in part because pages aren’t being compiled on-demand as you visit them. Since you’re **serving pre-built content directly from a Content Delivery Network**, the site is already “there” and ready for the user.

Since you’re serving via CDN, you can also distribute the content across the globe &mdash; closer to potential visitors. There’s no central point of origin, which is vital in the case of any online publication that wants to be fast for all of its readers.

So the stage was set. Smashing Magazine migrated to the JAMstack &mdash; [to Netlify](https://url.netlify.com/rkaJnT46S) as a platform in particular. In its 10 years of operation, Smashing had grown from a small online publication to a massive WordPress blog, selling things like books, conference tickets, and workshops.

There were a few pieces of this site:

*   WordPress blog
*   Rails jobs board
*   Shopify store
*   Another CMS for the conference site

When Netlify first began the migration, the site was suffering some performance issues, weighed down by 20K comments and thousands of articles. Smashing was also interested in authentication as part of a new subscription plan, as well as a redesign for a more modern look.

## Reliability

Smashing regularly achieves what other platforms dream of: articles shared widely through an enormous community. However, when a tipping point of traffic was reached for a post, Smashing regularly had issues with outages. To mitigate this, the heavy use of WordPress plugins were introduced into their stack, but they still struggled to retain good uptime metrics.

Moving to Netlify allowed the Smashing team to avoid getting database connection errors and **not worry about downtime** even when an article saw a huge amount of traffic. Why? Because when serving without a server, the prebuilt content doesn’t have to be generated and served &mdash;  it already exists, ready to be viewed. Nothing is being requested on the spot except for the entire, static page.

Serving via CDN also allowed Smashing to sleep a little easier in terms of security. `wp-login.php` has long been a source of security holes and attack vectors. Prebuilt content can not be accessed in the same way and security holes are not as ubiquitous.

## Cache Invalidation

Smashing had cycled through every WordPress caching plugin, with varied results and a lot of problems. Vitaly Friedman of Smashing mentions,

<blockquote>“The main issues we had were related to ‘Error Establishing Database Connection’ that we kept having every other week, and we literally tried every single WordPress caching plugin out there. The performance was pretty OK (overall), but we were looking to improve it further. Plus, we did want to launch Membership and connect all the different offerings &mdash; conferences, job posts, articles, books, eBooks &mdash; with one single platform, and it was remarkably difficult to achieve with WordPress in play.”</blockquote>

Moving to Netlify allowed the Smashing team to see instant cache invalidation while also serving cached and performant content, with no extra overhead.

When you deploy a site, HTML files are hosted on Netlify’s CDN. It’s optimized for a high cache-hit rate, and fast time to first byte, while being able to **instantly invalidate all HTML files** that have changed. Netlify also fingerprints all links to assets like CSS files, images, fonts, or JS files, and serves Smashing with caching headers that cache them forever. The fingerprinting guarantees they’re unique, and that if you update a new version, the newer version is served instead.

## Workflow

Looking at the existing setup, one large reason for the migration was simply to unify the existing properties. Having to context shift between all of these different tech stacks and setups became a hard maintenance problem that tasked the engineers.

When previously their infrastructure was split up among so many different systems, this **migration process also unified everything**, keeping the main site, the conference site, the subscriptions and e-commerce section all working together instead of maintained separately with different stacks. This helped keep development costs low and developer experience working on all properties consistently.

The WordPress migration piece proved to be the largest and most delicate. Netlify tried to export the data from the WP exporter, only to find that the content had embeds that needed to be preserved, or at times were altered by plugins. In order to maintain parity with what was on the site, a series of scrapers were written, broken down by articles, assets, comments, and the homepage.

Once that was written and transformed, it was loaded into a new repo in GitHub, and [Netlify CMS](https://url.netlify.com/S1xJTpNaH) was used instead. What makes Netlify CMS unique is that it’s lightweight, and integrates content editors into a Git workflow &mdash; meaning it will literally pull and serve markdown files from a git repo instead of a database. In addition, Netlify CMS is platform agnostic and works with (almost) all static site generators and sites stored in GitHub.

At that time, [Sara Soueidan](https://twitter.com/SaraSoueidan) worked for Smashing as a freelance front-end developer on their redesign. She created a library of components to build out the front-end architecture and remarked how much more simple it was to work with because she was working directly in git, even when working with the CMS.

<blockquote>“Everything that I pushed to the repository is being directly applied to the pattern library which means that you don’t have to maintain two different sets of components... this type of continuity was great! All I have to do is write HTML, CSS, and JavaScript and push to the repo and everything works like magic. The workflow was fantastic.”</blockquote>

All of this said, Netlify CMS can sometimes be too lightweight for such a high traffic and scale use case. Smashing regularly has guest authors and a full editorial staff. Some of the rich features WordPress offers are really helpful for these kinds of highly collaborative environments.

That’s why in the [following tutorial](https://www.smashingmagazine.com/2020/02/headless-wordpress-site-jamstack/), **we’ll walk you through a headless model**, where you can still reap the benefits of the WordPress dashboard for content creators, but use WordPress via API and have the development rely on a git-centric workflow that easy for developers to maintain as well. Stay tuned!

## Framework Choices

In the initial prototype that Matt Biilmann created, he wrote everything in minimal Preact, paired with Hugo, as he was very focused on performance. He just used props and kept everything very lightweight. As he passed the project off to be maintained by Smashing’s developer, Ilya Pukhalski, he found that Preact was lacking some features they were missing to tap into React’s ecosystem. Eventually, the benefits of Redux and other libraries outweighed the cost.

Reflecting now, Matt says he would have used Vue, which didn’t have quite the market share at the time (I swear I didn’t prompt him to say that). I asked the obvious question: **why not Svelte?** As performance-minded folks tend to reach for that library. He mentioned that Svelte doesn’t quite have the ecosystem Vue has yet.

When Matt reflects on whether or not he would have still used Hugo, he says that he loves Hugo, but what he found difficult for this project in particular was that it didn’t have enough of a plugin system &mdash; creating banner ads and things of that nature were not programmable enough with Hugo and he needed to inject scripts to accomplish it. These scripts tended to slow the build process down. That said, we still use Hugo for our own site at *netlify.com* and love it &mdash; this caveat is extremely particular to the needs of Smashing’s site in particular.

If he could do it again, he might choose either Eleventy, which has rich capabilities in terms of creating plugins and other extendable scripts. Or, if he was using Vue, Nuxt would have offered him some nice plugin capabilities while allowing being a good choice for that framework, offering server-side rendering, routing, and static generation.

## Building Large Sites

There was one problem that emerged working with a site as large as Smashing and maybe you can already figure out what it is, we just touched on it. It’s true that with any large site of prebuilt pages served on a CDN, the performance is still great because we’re not building anything on the fly for the users.

But that benefit can only happen if the site is pre-built, and that process can be time-consuming. While more traditional sites will build the pages when you request them, we’re literally creating every single page in advance just in case the user might need it. It makes the performance super fast! But that time is now offloaded to development and publishing time &mdash; creating every page can take time.

This is not so much of an issue with smaller sites, but at Smashing Magazine’s scale, we need to think about that time a bit more, especially so that people can keep productivity high while actively daily creating content.

What Netlify did was create a large `/production-articles` folder which carried the bulk of the many 1000s of articles they were already hosting. Then, made a separate working directory called `content/articles` where the articles that were actively being created and edited could be placed.

This build process meant that everyone who was working on the site was working with a smaller batch of articles for local development, unhindered by waiting for the entire build. This process was managed by a gulp task to prepare the production articles, and freed Hugo up to only handle what was actively being worked on.

One of the cons of this approach is that it does still require the entire build to be run, making the process slow. At a smaller publication, this would likely matter less but at Smashing’s scale, it does slow down the publication process.

## Open-Source APIs

In the beginning, we mentioned that among other things, Smashing was interested in migrating their existing e-commerce solution, handle comments outside of WordPress, and add functionality for auth. All of these pieces of functionality were built with open-source solutions that Netlify maintains, breaking them out into stateless APIs:

*   **GoTell**  
An API and build tool for handling large amounts of comments.
*   **GoCommerce**  
A small Go-based API for e-commerce sites that handles orders and payments.
*   **GoTrue**  
A small open-source API written in Golang that can act as a self-standing API service for handling user registration and authentication for projects. It’s based on OAuth2 and JWT and will handle user signup, authentication, and custom user data.

Each one of these pieces required migration and unique factors of their own, and while they’re out of scope for this article, they’re all covered in a free book Matt co-wrote called “[*Modern Web Development on the JAMstack*](https://url.netlify.com/HyZrap46B)”. We’ll also do some deep dives like this one &mdash; with usable examples &mdash; into search, and authentication, in subsequent posts.

## Conclusion

The migration went swimmingly. Smashingly? Er… it went well. Smashing wasn’t penalized for its own success &mdash; when a popular article came along, they could serve the content consistently, no longer bailing over large loads. Along with this, the movement to a JAMstack infrastructure brought better performance and security.

Markus Seyfferth, former CEO of Smashing Magazine, noted:

<blockquote>“The time to first load is so much faster than before… before we had to wait for the HTML file being served for <strong>800ms</strong> and now it’s <strong>80ms</strong>.” </blockquote>

This process was successful and like any great engineering project, lessons were learned along the way. In this [next article](https://www.smashingmagazine.com/2020/02/headless-wordpress-site-jamstack/) in this series, we’ll run through a tutorial and demo for what we would recommend given what we’ve learned. If you’d like to modernize your WordPress development and reap the performance and security benefits of JAMstack, read on!

{{< signature "ra, vf, il" >}}

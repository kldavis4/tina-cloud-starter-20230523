---
title: 'ISR vs DPR: Big Words, Quick Explanation'
slug: isr-dpr-explained
author: cassidy-williams
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e4090b9-8bd9-4d5a-aaed-5177c46a6803/isr-dpr-explained.jpg
date: 2021-07-15T14:00:00.000Z
summary: >-
  There are two strategies for incrementally building websites that are growing in popularity: Incremental Static Regeneration and Distributed Persistent Rendering. What’s the difference? Let’s figure it out.
description: >-
  There are two strategies for incrementally building websites that are growing in popularity: Incremental Static Regeneration and Distributed Persistent Rendering. What’s the difference? Let’s figure it out.
categories:
  - Next.js
  - Tools
  - Frameworks
disable_ads: true
---

If you’ve been dabbling in the Jamstack/page rendering/Next.js world, chances are you’ve heard of the terms “Incremental Static Regeneration” (ISR) and “distributed persistent rendering” (DPR) floating around. And if you haven’t, you might be like, “Wow, these are long words that I’ll never understand.” That’s where you’re wrong! You’re about to understand them *now*.

## What Are These Things?

These terms are strategies for **incrementally building websites**. Normally, when you deploy a website that isn’t server-side or client-side rendered, it has to be compiled and built for the browser to natively load it (so, for example, your JSX is transpiled to vanilla JavaScript, your SCSS compiled to vanilla CSS, your templates into HTML).

As your websites get large, you might start to run into having to have fairly long build times, because that’s a *lot* to compile. Generally, your websites might have pages in two categories:

- **Type A**  
“Critical” pages (home page, about us, contact us)
- **Type B**  
“Deferred” pages that might not be hit as often as the Type A pages (product catalog, certain documentation pages)

If you were to incrementally build this website, you could theoretically break up your build where your Type A pages are built upfront, and then Type B pages are built later!

Both ISR and DPR follow this approach but do it in slightly different ways.

## What’s The Difference Between ISR And DPR?

For both approaches, Type A pages are built upfront right when you deploy. With Type B pages, they vary a little more. The key thing that is different between these two approaches is *immutability*. When I say immutability, I mean that once a page is added to a build, it doesn’t change, and every user hitting a URL during that deployment will always see the exact same data.

With ISR, your Type B pages are **built at runtime** when a user goes to the page. Each of these pages has an “expiration time” (or “revalidation time”) where it will re-build based on new content that comes in at that time (fetched in the background). It is based on a caching strategy called “stale while revalidate”, meaning a page can be “stale” with old information until it’s re-generated and the cache is updated. This approach does not guarantee immutability across builds. When I say that, I mean that you can’t necessarily go back to a previous deployment with full confidence that all the content is going to be as it was at that time you originally ran that page (this is explained in [another blog post](https://www.smashingmagazine.com/2021/04/incremental-static-regeneration-nextjs/#isr-not-just-caching) from [Lee Robinson](https://www.smashingmagazine.com/author/lee-robinson/) on the Next.js team).

There are **pros and cons** to this; the major pro meaning that you can have your data that populates the page regularly update without rebuilding the site, and the major con being that debugging will be very difficult without that immutable piece (because some users might see a stale page and others might see the correctly updated one).

With DPR, your Type B pages are also built at runtime when a user goes to the page. When the non-built pages are requested for the first time, they are built and cached at the edge so they don’t need to be built again. Once it’s a part of the build, it will not change until a redeploy. There are also pros and cons to this approach. The major pro is that **this guarantees immutability**. When you go to a URL, every user will always see the same exact information. The con is that if you want to have one of those pages updated, you’ll need to trigger a rebuild of the site.

## How Can I Use These Approaches And Compare For Myself?

In an ideal world, these approaches are built into the frameworks you use and you won’t have to do much to use them. Right now though, you can **test it out with Next.js**! ISR is built-in by default to Next.js when you deploy it to a Node.js-driven platform like Vercel, and DPR is built in when you deploy to Netlify.

You can use DPR in other frameworks as well (Zach Leatherman has [some demos of it with Eleventy](https://www.youtube.com/watch?v=bENDCw9aLV0) where he defers building hundreds of pages), and the Next.js team said that **ISR will be coming to other frameworks** in the future (like Nuxt and SvelteKit). You can also leave a comment on how DPR is implemented (*for any Jamstack platform!*) [in this RFC](https://github.com/jamstack/jamstack.org/discussions/549).

{{% feature-panel %}}

{{< signature "vf, il" >}}

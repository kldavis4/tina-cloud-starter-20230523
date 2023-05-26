---
title: 'Meet Hydrogen: A React Framework For Dynamic, Contextual And Personalized E-Commerce'
slug: hydrogen-react-framework-dynamic-contextual-personalized-ecommerce
author: ilya-grigorik
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee33395f-684a-40e5-bf72-56d9e9e4d975/hydrogen-react-framework-dynamic-contextual-personalized-ecommerce.jpg
date: 2021-11-08T14:30:00.000Z
summary: >-
  A great commerce experience cannot be distilled to a single number. It’s not a Lighthouse score, or a set of Core Web Vitals figures, although both are important inputs. A great commerce experience is a trilemma that carefully balances competing needs of delivering a great customer experience, dynamic storefront capabilities, and long-term business &mdash; conversion, retention, re-engagement &mdash; objectives.
description: >-
  A great commerce experience is not a Lighthouse score or a set of Core Web Vitals figures (although both are important inputs), but it’s also a trilemma that carefully balances competing needs of delivering a great customer experience, dynamic storefront capabilities and long-term business objectives.
categories:
  - E-Commerce
  - Performance
  - Business
disable_ads: true
---

As developers, we rightfully obsess about the customer experience, relentlessly working to squeeze every millisecond out of the critical rendering path, optimize input latency, and eliminate jank. At the limit, statically generated, edge delivered, and HTML-first pages look like the optimal strategy. That is until you are confronted with the realization that the next step function in **improving conversion rates and business objectives** requires leaning into heavy personalization of your storefront. 

The journey, often, starts “simple” with localization. But then, quickly advances to contextual pricing, juggling complexity of large and frequently updated product catalog, managing continuously running multivariate tests and promotion campaigns, and serving customer-tailored dynamic recommendations. Eventually, you reach a realization that every page is similar to an open Tetris board where each “slot” can and should be dynamically tailored by dynamic visitor preferences, all powered by an ever-growing set of dynamic business rules.

## Hydrogen Is Purpose-Built To Power Dynamic Commerce

I work at Shopify, an all-in-one commerce platform to start, run, and grow a business. We work with millions of merchants, and as many companies, we [obsess](https://www.shopify.ca/plus/guides/ultimate-guide-to-site-speed) [about](https://shopify.engineering/how-shopify-reduced-storefront-response-times-rewrite) [storefront](https://www.shopify.ca/blog/dawn-shopify-theme) [performance](https://www.shopify.ca/blog/shopify-site-speed).

We obsess [even more](https://www.youtube.com/watch?v=zsyKQ9lT8tQ) about finding the optimal balance between performance, capabilities, and merchants’ business objectives. A key insight that we’ve learned from all the merchants on this quest is that at the core, **commerce needs to be dynamic**.

From connecting back-office operations to front-of-the-house A/B testing and dynamic personalization for each customer, the shared foundation is fast server-side rendering powered by fast storefront data access. On top of this foundation, we add layers of caching, prerendering and edge delivery optimizations &mdash; not the other way around. 

Surveying the existing landscape of available developer tools and runtimes, **we felt that there is a gap**. Enabling dynamic commerce requires close integration between server and client, an optimized streaming and data fetch strategy, and a production platform that operates at scale.

These are hard technical problems that Shopify can help solve and this is why we’ve been hard at work on the [Hydrogen framework](https://github.com/Shopify/hydrogen). It’s a React-based framework optimized for commerce and specialized to be powered by Shopify APIs and infrastructure:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b995898d-bc04-4353-bc30-3a80c482977e/in-line-product-snapshot-cart.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b995898d-bc04-4353-bc30-3a80c482977e/in-line-product-snapshot-cart.png" width="800" height="435" sizes="100vw" caption="Meet Hydrogen: A React-based framework for building custom and creative storefronts gives you everything you need to start fast, build fast, and deliver the best personalized and dynamic customer experiences powered by Shopify’s platform and APIs. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b995898d-bc04-4353-bc30-3a80c482977e/in-line-product-snapshot-cart.png'>Large preview</a>)" alt="Creating an AddToCartButton in a text editor with the Hydrogen app" >}}

The future of commerce is **dynamic and personalized**. At Shopify, we believe such shopping experiences can be fast no matter where shoppers are located and built without the restrictions imposed by static site generation. Paired with a set of Shopify-optimized commerce components and a Vite-powered developer environment, it’s the fast framework for developers and customers.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1b47845-e8bd-43d1-9731-1762bf503453/hero-800px.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1b47845-e8bd-43d1-9731-1762bf503453/hero-800px.png" width="800" height="500" sizes="100vw" caption="Hydrogen fuels dynamic commerce by uniting React Server Components, streaming server-side rendering, and smart caching controls. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1b47845-e8bd-43d1-9731-1762bf503453/hero-800px.png'>Large preview</a>)" alt="Presenting Hydrogen" >}}

Today, we are [launching the public developer preview](https://www.shopify.com/partners/blog/hydrogen-developer-preview): dive into the [docs](https://shopify.dev/custom-storefronts/hydrogen), spin up a [test instance on Stackblitz](https://hydrogen.new/), drop your [feedback and comments on GitHub](https://github.com/Shopify/hydrogen).

Getting fast initial render with streaming server-side rendering, efficient component-level updates and state transitions, while also setting up a performant loading and bundling strategy for all the assets is hard and time-consuming technical work. And, of course, the result needs to be seamless and delightful &mdash; dare we say, [even fun](https://youtu.be/a2YSgfwXc9c?t=715) &mdash; to develop and maintain. 

Regardless of whether you’re setting up a storefront for a new merchant, or building a customer experience that will be visited by millions, the goal for Hydrogen is to eliminate undifferentiated and gnarly technical plumbing and enable you to **start fast and focus on delivering merchant value**.

For example, a few critical pieces that Hydrogen solves:

- [Streaming server-side rendering](https://shopify.engineering/high-performance-hydrogen-powered-storefronts#streaming-server-side-rendering) for fast first render powered by React’s Suspense;
- [React Server Components](https://shopify.engineering/high-performance-hydrogen-powered-storefronts#react-server-components) for efficient, post-render component-level state updates;
- [Efficient server and client data fetching](https://shopify.engineering/high-performance-hydrogen-powered-storefronts#data-fetching-caching) primitives with smart cache defaults;
- [Flexible page and subrequest caching controls](https://shopify.engineering/high-performance-hydrogen-powered-storefronts#response-caching) for dynamic and edge delivery.

Unlocking such features and making them all work nicely together required that we work **hands-on with React core team** on helping define and prototype server components; Vite ecosystem on server-side streaming; Google’s [Aurora](https://web.dev/introducing-aurora/) team on integrating conformance and CLI tools that will keep you on track with modern best practices:

<blockquote>“The Chrome team at Google is excited to see Shopify continue to improve web performance at scale. Through our collaborations to improve perf out of the box, such as smarter image optimization, we believe that it’s possible to achieve an excellent user experience that benefits Shopify’s merchants and their customers.”<br /><br />&mdash; Addy Osmani, Chrome Engineering Manager</blockquote>

Of course, Hydrogen also comes with a set of pre-built and optimized components that know how to speak to the Shopify Storefront API and allow you to focus on presentation &mdash; the differentiated merchant value &mdash; instead of plumbing.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0ad56f-e307-432a-bc38-cb2bc076b52a/in-line-product-snapshot-pdp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0ad56f-e307-432a-bc38-cb2bc076b52a/in-line-product-snapshot-pdp.png" width="800" height="435" sizes="100vw" caption="A sneak peek into Hydrogen’s online integrated development environment. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0ad56f-e307-432a-bc38-cb2bc076b52a/in-line-product-snapshot-pdp.png'>Large preview</a>)" alt="A sneak peek into Hydrogen’s online integrated development environment" >}}

Curious to give it a try? Our developer preview is live at [shopify.dev/custom-storefronts/hydrogen](https://shopify.dev/custom-storefronts/hydrogen). Take it for a spin, [let us know](https://github.com/Shopify/hydrogen) what you think!

## Commerce At Shopify Scale: Hydrogen Powered By Oxygen

As any seasoned team will know, building the storefront capabilities is one thing, and running it at a production scale that is able to absorb large waves of traffic, driven by flash sales or breakout social campaigns, is a whole other and massive operational challenge.

<blockquote>“It runs fast, and I don’t see any errors on my machine [...]”<br /><br />&mdash; said every developer.</blockquote>

This is where Oxygen comes into play. Oxygen is a new Shopify hosted **V8 Isolate-powered JavaScript worker runtime** that leverages all of the platform, operations and security knowledge capabilities that we’ve developed over a decade+ of scaling millions of storefronts. Our existing merchants never have to think about the complexity of scaling infrastructure for a record-setting flash sale, and Hydrogen storefronts won’t have to either.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cccdef1-f399-4f31-9c02-89c0f9e334c6/in-line-hydrogen-on-oxygen.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cccdef1-f399-4f31-9c02-89c0f9e334c6/in-line-hydrogen-on-oxygen.png" width="800" height="435" sizes="100vw" caption="Run a git push, check the preview URL, promote to production, and Shopify handles all the rest. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cccdef1-f399-4f31-9c02-89c0f9e334c6/in-line-hydrogen-on-oxygen.png'>Large preview</a>)" alt="Shopify-hosted Oxygen" >}}

Under the hood, Oxygen runtime runs on geo-distributed clusters with colocated Shopify data that is milliseconds away; **fast data access is integral** in enabling fast dynamic commerce and colocating data and rendering is our (not so secret) weapon. One network hop up, Shopify’s CDN adds optimized edge-delivery with commerce specialized protection against malicious actors and shopping bots that now often operate at a scale that is able to DDoS many storefronts.

Oxygen is in early access preview with select merchants. Stay tuned for more in 2022!

## Hydrogen And Oxygen Are The Building Blocks For Modern Commerce

The experience of our merchants shows that commerce is dynamic, contextual and personalized. This does not mean that some, or perhaps even substantial parts of some storefronts, cannot be cached and served from the edge. This is not a debate about dynamic vs. static. You need both.

Our vision with Hydrogen and Oxygen is to **unlock the best of both worlds** and make building and running the next million of modern &mdash; dynamic, contextual, and personalized &mdash; storefronts easier, more cost-effective, and fun.

{{% feature-panel %}}

{{< signature "vf, il" >}}

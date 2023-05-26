---
title: 'The Evolution Of Jamstack'
slug: evolution-jamstack
author: mathias-biilmann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77ef8e71-94e8-49bb-9c9b-dc5b68902149/evolution-jamstack.jpg
date: 2021-05-03T07:00:00.000Z
summary: >-
  Web-oriented databases, frameworks like Nuxt and Next.js, and even frameworkless approaches are evolving the Jamstack, but the core principles are more powerful than ever.
description: >-
  Web-oriented databases, frameworks like Nuxt and Next.js, and even frameworkless approaches are evolving the Jamstack, but the core principles are more powerful than ever.
categories:
  - Jamstack
  - Next.js
  - JavaScript
  - Serverless
disable_ads: true
---

It’s been five years since I first [presented the idea of the Jamstack architecture](https://vimeo.com/163522126) at *SmashingConf* in San Francisco 2016, a talk inspired by many conversations with colleagues and friends in the industry. At that point, the idea of fundamentally decoupling the front-end web layer from the back-end business logic layer was only an early trend, and not yet a named architectural approach.

<!-- {{< vimeo id="163522126" caption="The New Front-end Stack. Javascript, APIs and Markup. A presentation from 2016 by Matt Biilmann. <a href='https://vimeo.com/163522126'>Watch on Vimeo</a>" >}} -->

{{< rimg breakout="true" href="https://vimeo.com/163522126" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e98ae67-d3af-4eea-9ab8-7971091f3642/smashingconf-sf-2016.png" width="800" height="450" sizes="100vw" caption="The New Front-end Stack. Javascript, APIs and Markup. A presentation from 2016 by Matt Biilmann. <a href='https://vimeo.com/163522126'>Watch on Vimeo</a>" alt="Matt Biilmann on stage at SmashingConf SF 2016" >}}

Static site generators were emerging as a real option for building larger content-driven sites, but the whole ecosystem around them was nascent, and the main generators were pure open-source tools with no commercial presence. Single Page Applications were the basis of some large-scale web apps, like Gmail, but the typical approach to building them was still backend-centric.

Fast forward to 2020, **Jamstack hit the mainstream**, and we saw millions of developers and major brands like [Unilever](https://www.sanity.io/projects/nexxus), [Nike](https://www.netlify.com/customers/matter-supply-nike-site/), and [PayPal ](https://www.infoq.com/presentations/jamstack-enterprise/)embrace the architecture. Vital initiatives like the [Covid Tracking Project](https://www.netlify.com/blog/2020/07/06/how-the-covid-tracking-project-scaled-from-0-to-2m-api-requests-in-3-months/#main) were able to scale from 0 to 2 million API requests on the Jamstack. Frameworks like Nuxt became commercial businesses, and we celebrated large public companies like Microsoft and Cloudflare as they launched early Jamstack offerings. 

As the commercial space has heated up and the developer community has grown, there’s also been more noise, and we’re even starting to **test the boundaries of Jamstack’s best practices**. It feels like the right time to both revisit the original vision some of us had five years ago, and look ahead at what the changes in the technological landscape will mean for the future of the Jamstack architecture and the web.

Let’s start out by quickly revisiting the core principles that have made the architecture prove popular.

## Compiling The UI

In the Jamstack architecture, **the UI is compiled**. The goal is to do the right work at the right times &mdash; with a preference for doing as much work as possible ahead of time. Many times, the entire site can be prerendered, perhaps not even requiring a backend once deployed. 

### Decoupled Frontends

Decoupling the frontend from back-end services and platforms enforces a clear contract for how your UI communicates with the rest of the system. This **defaults to simplicity**: your frontend has a limited contact surface with anything outside itself, making it less complicated to understand how external changes will affect its operation.

## Pulling Data As Needed

Of course, not everything can be prerendered, and the Jamstack architecture is capable of delivering dynamic, personalized web apps as well as more globally consistent content. Requesting data from the frontend can power some rich and dynamic applications. 

A good example is the frontend of our own [Netlify UI](https://app.netlify.com/), which is itself a Jamstack application built and run on Netlify. We pre-compile an app shell, then use **asynchronous requests** to hit our API to load data about our users and their sites. Whether you’re using REST, GraphQL, or WebSockets, if you’re precompiling as much of the UI as possible and loading data to give your users **a dynamic, customized experience**, then you’re shipping the Jamstack architecture.

## Jamstack In 2021 And Beyond

There’s more innovation happening across the Jamstack ecosystem than ever before. You can see a rapid evolution of the back-end services, developer tooling, and client-side technologies that are combining to enable development teams to build experiences for the web that would have seemed out of reach only a couple of years ago. 

I want to point to three trends I see shaping up for Jamstack developers in the near future:

### 1. Distributed Persistent Rendering (DPR)

More than anything, Jamstack’s inherent simplicity has made the process of building and deploying web applications much easier to reason about. Code and content updates can be pre-rendered as **clean, atomic deployments** and pushed right to the edge, creating strong guarantees around reliability and performance without the need to manage complex infrastructure.

But pre-rendering a larger website may also mean waiting several minutes each time there’s a new deployment. That’s why I think we are seeing so much innovation happening to make builds smarter and faster &mdash; especially for larger sites and web apps. Take for example the raw speed of [esbuild](https://esbuild.github.io), the new “extremely fast JavaScript compiler.” A production bundle that may take [Parcel](https://parceljs.org) or [Webpack](https://webpack.js.org) over a minute to compile can be **completed by esbuild in under a second**. And build tools like [Vite](https://vitejs.dev) and [Snowpack](https://www.snowpack.dev) lean on native ES modules to make local development feel nearly instantaneous. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c64e2d5-5529-4f68-badb-fede958f6212/dpr-functions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c64e2d5-5529-4f68-badb-fede958f6212/dpr-functions.png" width="800" height="452" sizes="100vw" caption="Like the assets generated during a build, those rendered by DPR at request time would remain in the CDN cache until invalidated by the successful completion of a new deploy. This would allow developers to consider the assets rendered during a deploy, and those rendered on demand from requests to DPR functions contained in that deploy, as all belonging to the same logical atomic deploy. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c64e2d5-5529-4f68-badb-fede958f6212/dpr-functions.png'>Large preview</a>)" alt="Like the assets generated during a build, those rendered by DPR at request time would remain in the CDN cache until invalidated by the successful completion of a new deploy. This would allow developers to consider the assets rendered during a deploy, and those rendered on demand from requests to DPR functions contained in that deploy, as all belonging to the same logical atomic deploy" >}}

In the React ecosystem, some newer frameworks like [Remix](https://remix.run) or [Blitz](https://blitzjs.com) are starting to lean more on the “run everything on a server” approach we’ve all known in the past. There’s a risk of bringing back much of the complexity we’ve worked to escape. Layers of caching can help make server-side apps more performant, but developers lose the guarantees of atomic deployments that make Jamstack apps easy to reason about.

Blitz seems to be moving the monolith into the frontend. This can make full-stack apps runnable on typical Jamstack platforms, but without any clear decoupling between the web experience layer and the back-end business logic layer. I think **decoupling the frontend from the backend** is fundamental to the Jamstack approach and responsible for unlocking so many of its benefits.

What I see gaining real momentum are the “hybrid” frameworks like [Next.js](https://nextjs.org), [Nuxt.js](https://nuxtjs.org), and [SvelteKit](https://svelte.dev) that allow developers to seamlessly mix pages pre-rendered at build time with other routes that are rendered via serverless functions. The challenge is that serverless functions (while certainly scalable) have their own set of [performance implications](https://mikhail.io/serverless/coldstarts/big3/). 

Ultimately, I see the community moving towards an extremely powerful trio that provides Jamstack developers **request-level control** over the performance profile of any site or application:

1. Delivering pages entirely pre-rendered at build time,
2. Delivering pages dynamically via serverless functions, or
3. Building pages on-demand that then persist as static CDN assets.

Next.js has done quite a bit of work on a concept of [Incremental Static Regeneration](https://www.smashingmagazine.com/2021/04/incremental-static-regeneration-nextjs/). The idea is to ensure high-performance pages by paring serverless functions with different caching strategies like *Stale While Revalidate*. While the idea of distributing some of the builds to an on-demand approach that still includes strong caching guarantees is a powerful technique, unless developers explicitly opt-out of the stale-while-revalidate approach, the atomic deploy guarantee will be violated by serving a mix of stale and fresh assets from different deploys. Currently the benefits of ISR are also exclusive to a singular framework and only deeply integrated into the offerings of a single provider.

At Netlify, we see a lot of promise in the idea of allowing developers to render critical pages at build time, while deferring other pages (like older blog posts, for example) to be built only when and if they are requested. We’re calling the approach **Distributed Persistent Rendering** or DPR. It’s an architecture for incremental builds that can be compatible across almost every framework and Jamstack site generator, from 11ty to Nuxt to Next.js.

DPR will dramatically reduce upfront build times for larger sites, solving a core criticism of static site generation. On *Jamstack.org*, we’ve opened a [Request For Comments](https://github.com/jamstack/jamstack.org/discussions/549) to involve the entire community in our efforts to give developers more options for how pages are rendered while adhering closely to the principles that have made Jamstack so popular. By giving this architecture a name and refining it with community input, we can help Jamstack developers build patterns around it &mdash; regardless of the framework.

### 2. Streaming Updates From The Data Layer

If you develop web applications, you’ve likely followed the evolution of state management libraries as developers have built more and more complex web interfaces using tools like React, Vue, and Svelte. But state management has largely been an in-browser and in-memory concern. Each browser tab essentially has its own state, but can be quite complex to connect that local browser state of your application back to the data services that power it. 

Luckily, this is improving as more and more services now **support real-time data subscriptions**. [Hasura](https://hasura.io), [OneGraph](https://www.onegraph.com), and [Supabase](https://supabase.io) all offer this capability and I only expect to see wider adoption across all providers as the underlying data stores are cached and distributed to the edge for fast global performance. Take Twillio’s expanding APIs: they now not only offer [streaming video](https://www.twilio.com/video) but also streaming “data tracks,” which can be used to create complex collaboration apps that stay continually synchronized across participants. 

Finally, new providers are emerging that aggregate data across back-end services. Whether or not you use GraphQL as a query language, it’s really compelling to imagine the power of connecting your UI to a single, standard stream of updates from multiple underlying APIs.

### 3. Developer Collaboration Goes Mainstream

The Jamstack is built on a Git workflow &mdash; an approach that scales really well to larger development teams. But going forward, we’ll start to see how these traditionally developer-focused tools will expand to involve everyone across the company: developers, sure, but also writers, editors, designers, and SEO experts.

When you think of collaboration, you tend to think of synchronous edits—the multiple cursors that fly around a Google Doc, for example. We are seeing that style of live collaboration come to CMS tools like [Sanity](https://www.sanity.io) and design tools like Figma. But so much work often happens asynchronously, and non-developers traditionally haven’t enjoyed the powerful tools that developers use to seamlessly branch, stage, and merge changes with **collaborative discussion attached to each pull request**. 

Early on in the Jamstack, some clever git-based CMS tools emerged to help non-developers manage content like code &mdash; perhaps without even knowing that each change they made was being git-committed just like a developer working from the terminal. We’re now starting to see new tools tackle [visual page edits](https://tina.io) in a way that remains compatible with popular Jamstack site generators like Gatsby and Next.js. All of this lowers the bar to collaboration for non-developers and we’ll only see that trend accelerate.

And it’s not just non-developers joining in on the collaboration: **deep integrations between tools** are bringing more automated contributions into our dev, build, and deploy workflows. Just browse the comment history on a GitHub pull request to see how many tools are now integrated to run automated tests and catch errors before they are deployed.

Updates to Netlify’s docs, for example, aren’t just linted against our code standards, they are also linted against our content standards, ensuring we stay consistent with our style guide for vocabulary, language, and phrasing. Teams can also now **easily tie performance budgets and SEO standards** to each deployment, again with alerts and logs tied directly to GitHub issues.

I would expect to see those sorts of integrations explode in the coming year, allowing a git-based workflow to underpin not just code changes, but also content, data, design assets &mdash; you name it. Friendly interfaces into these Git workflows will allow more contributors to comment, commit, and collaborate and bring developer productivity tooling further into the mainstream. 

## Enabling Scale And Dynamic Use Cases

While Jamstack stays true to the core concepts of decoupling the frontend from the backend and maintaining immutable and atomic deploys, new build strategies and compute primitives have the potential to unlock extremely large-scale sites and dynamic, real-time web applications.


Jamstack developers &mdash; and now entire web teams, marketers, and product managers &mdash; have much to look forward to in this space.

### Further Reading And References

- “[How The COVID Tracking Project Scaled From 0 To 2M API Requests In 3 Months](https://www.netlify.com/blog/2020/07/06/how-the-covid-tracking-project-scaled-from-0-to-2m-api-requests-in-3-months/),” Netlify, Netlify Blog
- “[Incremental Static Regeneration: Its Benefits And Its Flaws](https://www.netlify.com/blog/2021/03/08/incremental-static-regeneration-its-benefits-and-its-flaws/),” Cassidy Williams, Netlify Blog
- “[Distributed Persistent Rendering: A New Jamstack Approach For Faster Builds](https://www.netlify.com/blog/2021/04/14/distributed-persistent-rendering-a-new-jamstack-approach-for-faster-builds/),” Matt Biilmann, Netlify Blog
- [Glossary](https://jamstack.org/glossary/), Jamstack.org

{{< signature "vf, il" >}}

{{% feature-panel %}}

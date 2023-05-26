---
title: 'Breaking Down Bulky Builds With Netlify And Next.js'
slug: breaking-down-bulky-builds-netlify-nextjs
author: atila-fassina
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a11af025-97a1-4506-8cbe-a7786e5574c9/breaking-down-bulky-builds-netlify-nextjs.jpg
date: 2021-06-29T11:00:00.000Z
summary: >-
  Static Generation is great for performance &mdash; until the app gets too big and build-times go through the roof. Today, we’ll have a look at how Netlify’s fresh On-Demand Builders can fix that. Additionally, we pair it up with Next.js’ Incremental Static Regeneration for the best user and developer experience. And, of course, benchmark those results!
description: >-
  Static Generation is great for performance &mdash; until the app gets too big and build-times go through the roof. Today, we’ll have a look at how Netlify’s fresh On-Demand Builders can fix that.
categories:
  - Jamstack
  - Next.js
  - JavaScript
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Netlify
  link: https://www.netlify.com/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcf23ab4-3a5e-4a81-b79f-b520b5dcf6a2/netlify-full-logo-light.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.netlify.com/">Netlify</a> who are a diverse group of incredible talent from all over the world and offers a platform for web developers that multiplies productivity. <em>Thank you!</em>
---

One of the biggest pains of working with statically generated websites is the incrementally slower builds as your app grows. This is an inevitable problem any stack faces at some point and it can strike from different points depending on what kind of product you are working with.

For example, if your app has multiple pages (views, routes) when generating the deployment artifact, each of those routes becomes a file. Then, once you’ve reached thousands, you start wondering when you can deploy without needing to plan ahead. This scenario is common on e-commerce platforms or blogs, which are already a big portion of the web but not all of it. Routes are not the only possible bottleneck, though.

A resource-heavy app will also eventually reach this turning point. Many static generators carry out asset optimization to ensure the best user experience. Without build optimizations (incremental builds, caching, we will get to those soon) this will eventually become unmanageable as well &mdash; think about going through all images in a website: resizing, deleting, and/or creating new files over and over again. And once all that is done: remember Jamstack serves our apps from the edges of the **Content Delivery Network**. So we still need to move things from the server they were compiled at to the edges of the network.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8e40eed-ef3c-45e2-b8e8-09db6988d263/content-delivery-network.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8e40eed-ef3c-45e2-b8e8-09db6988d263/content-delivery-network.png" width="800" height="" sizes="100vw" caption="Jamstack general service architecture (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8e40eed-ef3c-45e2-b8e8-09db6988d263/content-delivery-network.png'>Large preview</a>)" alt="Jamstack general service architecture" >}}

On top of all that, there is also another fact: data is often dynamic, meaning that when we build our app and deploy it, it may take a few seconds, a few minutes, or even an hour. Meanwhile, the world keeps spinning, and if we are fetching data from elsewhere, our app is bound to get outdated. **Unacceptable! Build again to update!**

## Build Once, Update When Needed

Solving *Bulky Builds* has been top of mind for basically every Jamstack platform, framework, or service for a while. Many solutions revolve around incremental builds. In practice, this means that builds will be as bulky as the differences they carry against the current deployment.

Defining a *diff* algorithm is no easy task though. For the *end-user* to actually benefit from this improvement there are cache invalidation strategies that must be considered. Long story short: we do not want to invalidate cache for a page or an asset that has not changed.

Next.js came up with Incremental Static Regeneration (**ISR**). In essence, it is a way to declare for each route how often we want it to rebuild. Under the hood, it simplifies a lot of the work to the server-side. Because every route ([dynamic](https://nextjs.org/docs/routing/dynamic-routes) or not) will rebuild itself given a specific time-frame, and it just fits perfectly in the Jamstack axiom of invalidating cache on every build. Think of it as the `max-age` header but for routes in your Next.js app.

To get your application started, ISR just a configuration property away. On your route component (inside the `/pages` directory) go to your `getStaticProps` method and add the `revalidate` key to the return object:

<pre><code class="language-javascript">export async function getStaticProps() {
  const { limit, count, pokemons } = await fetchPokemonList()
  
  return {
    props: {
      limit,
      count,
      pokemons,
    },
    revalidate: 3600 // seconds
  }
}
</code></pre>

The above snippet will make sure my page rebuilds every hour and fetch for more Pokémon to display.

We still get the bulk-builds every now and then (when issuing a new deployment). But this allows us to decouple content from code, by moving content to a **Content Management System** (CMS) we can update information in a few seconds, regardless of how big our application is. Goodbye to webhooks for updating typos!

## On-Demand Builders

Netlify recently launched [On-Demand Builders](https://www.netlify.com/blog/2021/04/14/faster-builds-for-large-sites-on-netlify-with-on-demand-builders-now-in-early-access/) which is their approach to supporting ISR for Next.js, but also works across frameworks including Eleventy and Nuxt. In the previous session, we established that ISR was a great step toward shorter build-times and addressed a significant portion of the use-cases. Nevertheless, the caveats were there:

1. **Full builds upon continuous deployment.**  
The incremental stage happens only *after* the deployment and for the data. It is not possible to ship code incrementally
2. **Incremental builds are a product of time.**  
The cache is invalidated on a time basis. So unnecessary builds may occur, or needed updates may take longer depending on the revalidation period set in the code.

Netlify’s new deployment infrastructure allows developers to create logic to determine what pieces of their app will build on deployment and what pieces will be deferred (and **how** they will be deferred). 

- **Critical**  
No action is needed. Everything you deploy will be built upon *push*.
- **Deferred**  
A specific piece of the app will not be built upon deploy, it will be deferred to be built on-demand whenever the first request occurs, then it will be cached as any other resource of its type.

## Creating an On-Demand builder

First of all, add a [netlify/functions](https://github.com/netlify/functions) package as a `devDependency` to your project:

<pre><code class="language-bash">yarn add -D @netlify/functions
</code></pre>

Once that is done, it is just the same as creating a new [Netlify Function](https://www.netlify.com/products/functions/). If you have not set a specific directory for them, head on to `netlify/functions/` and create a file of any name to your builder.

<pre><code class="language-javascript">import type { Handler } from '@netlify/functions'
import { builder } from '@netlify/functions'

const myHandler: Handler = async (event, context) => {
  return {
    statusCode: 200,
    body: JSON.stringify({ message: 'Built on-demand! 🎉' }),
  }
}
export const handler = builder(myHandler)
</code></pre>

As you can see from the snippet above, the on-demand builder splits apart from a regular Netlify Function because it wraps its handler inside a `builder()` method. This method connects our function to the build tasks. And that is all you need to have a piece of your application deferred for building only when necessary. **Small incremental builds from the get-go!** 

## Next.js On Netlify

To build a Next.js app on Netlify there are 2 important [plugins](https://docs.netlify.com/configure-builds/build-plugins/#install-a-plugin) that one should add to have a better experience in general: [Netlify Plugin Cache Next.js](https://www.npmjs.com/package/netlify-plugin-cache-nextjs) and [Essential Next-on-Netlify](https://github.com/netlify/netlify-plugin-nextjs).  The former caches your NextJS more efficiently and you need to add it yourself, while the latter makes a few slight adjustments to how Next.js architecture is built so it better fits Netlify’s and is available by default to every new project that Netlify can identify is using Next.js.

## On-Demand Builders With Next.js

Building performance, deploy performance, caching, developer experience. These are all very important topics, but it is a lot &mdash; and takes time to set up properly. Then we get to that old discussion about focusing on Developer Experience instead of User Experience. Which is the time things go to a hidden spot in a backlog to be forgotten. Not really.

Netlify has got your back. In just a few steps, we can leverage the full power of the Jamstack in our Next.js app. It's time to roll up our sleeves and put it all together now.

## Defining Pre-Rendered Paths

If you have worked with static generation inside Next.js before, you have probably heard of `getStaticPaths` method. This method is intended for dynamic routes (page templates that will render a wide range of pages).
Without dwelling too much on the intricacies of this method, it is important to note the return type is an object with 2 keys, like in our Proof-of-Concept this will be [[Pokémon]dynamic route](https://github.com/smashingmagazine/poke-index/blob/main/pages/%5Bpokemon%5D.tsx) file:

<pre><code class="language-javascript">export async function getStaticPaths() {
  return {
    paths: [],
    fallback: 'blocking',
  }
}
</code></pre>

- `paths` is an `array` carrying out **all** paths matching this route which will be pre-rendered
- `fallback` has 3 possible values: blocking, `true`, or `false`

In our case, our `getStaticPaths` is determining:

1. No paths will be pre-rendered;
2. Whenever this route is called, we will not serve a fallback template, we will render the page **on-demand** and keep the user waiting, *blocking* the app from doing anything else.

When using On-Demand Builders, make sure your fallback strategy meets your app’s goals, the official [Next.js docs: fallback](https://nextjs.org/docs/basic-features/data-fetching#fallback-pages) docs are very useful.

Before On-Demand Builders, our `getStaticPaths` was slightly different:

<pre><code class="language-javascript">export async function getStaticPaths() {
  const { pokemons } = await fetchPkmList()
  return {
    paths: pokemons.map(({ name }) => ({ params: { pokemon: name } })),
    fallback: false,
  }
}
</code></pre>

We were gathering a list of all pokémon pages we intended to have, map all the `pokemon` objects to just a `string` with the pokémon name, and forwarding returning the `{ params }` object carrying it to `getStaticProps`. Our `fallback` was set to `false` because if a route was not a match, we wanted Next.js to throw a `404: Not Found` page.

You can check both versions deployed to Netlify:

- With On-Demand Builder: [code](https://github.com/smashingmagazine/poke-index/), [live](https://poke-index.netlify.app/)
- Fully static generated: [code](https://github.com/smashingmagazine/poke-index/tree/ssg), [live](https://60cf568b3407dc0007cfe8e7--poke-index.netlify.app/)

The code is also [open-sourced on Github](https://github.com/smashingmagazine/poke-index/) and you can easily deploy it yourself to check the build times. And with this queue, we slide onto our next topic.

## Build Times

As mentioned above, the previous demo is actually a **Proof-of-Concept**, nothing is really good or bad if we cannot measure. For our little study, I went over to the [PokéAPI](https://pokeapi.co/) and decided to catch all pokémons.

For reproducibility purposes, I capped our request (to `1000`).  These are not really **all** within the API, but it enforces the number of pages will be the same for all builds regardless if things get updated at any point in time.

<pre><code class="language-javascript">export const fetchPkmList = async () => {
  const resp = await fetch(`${API}pokemon?limit=${LIMIT}`)
  const {
    count,
    results,
  }: {
    count: number
    results: {
      name: string
      url: string
    }[]
  } = await resp.json()
  return {
    count,
    pokemons: results,
    limit: LIMIT,
  }
}
</code></pre>

And then fired both versions in separated branches to Netlify, thanks to preview deploys they can coexist in basically the same environment. To really evaluate the difference between both methods the ODB approach was extreme, **no pages** were pre-rendered for that dynamic route. Though not recommended for real-world scenarios (you will want to pre-render your traffic-heavy routes), it marks clearly the range of build-time performance improvement we can achieve with this approach.

<table class="tablesaw break-out">
  <thead>
    <tr>
      <th>Strategy</th>
      <th>Number of Pages</th>
      <th>Number of Assets</th>
      <th>Build time</th>
      <th>Total deploy time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Fully Static Generated</td>
      <td>1002</td>
      <td>1005</td>
      <td>2 minutes 32 seconds</td>
      <td>4 minutes 15 seconds</td>
    </tr>
    <tr>
      <td>On-Demand Builders</td>
      <td>2</td>
      <td>0</td>
      <td>52 seconds</td>
      <td>52 seconds</td>
    </tr>
  </tbody>
</table>

The pages in our little PokéDex app are pretty small, the image assets are very lean, but the gains on deploy time are very significant. If an app has a medium to a large amount of routes, it is definitely worth considering the ODB strategy.

It makes your deploys faster and thus more reliable. The performance hit only happens on the very first request, from the subsequent request and onward the rendered page will be cached right on the Edge making the performance exactly the same as the Fully Static Generated.

## The Future: Distributed Persistent Rendering

On the very same day, On-Demand Builders were announced and put on early access, Netlify also published their [Request for Comments on Distributed Persistent Rendering (DPR)](https://github.com/jamstack/jamstack.org/discussions/549). 

DPR is the next step for On-Demand Builders. It capitalizes on faster builds by making use of such asynchronous building steps and then caching the assets until they’re actually updated. No more full-builds for a 10k page's website. DPR empowers the developers to a full control around the build and deploy systems through solid caching and using On-Demand Builders.

Picture this scenario: an e-commerce website has 10k product pages, this means it would take something around 2 hours to build the entire application for deployment. We do not need to argue how painful this is.

With DPR, we can set the top 500 pages to build on every deploy. Our heaviest traffic pages are **always** ready for our users. But, we are a shop, i.e. every second counts. So for the other 9500 pages, we can set a post-build hook to trigger their builders &mdash; deploying the remaining of our pages asynchronously and immediately caching. No users were hurt, our website was updated with the fastest build possible, and everything else that did not exist in cache was then stored. 

## Conclusion

Although many of the discussion points in this article were conceptual and the implementation is to be defined, I am excited about the future of the Jamstack. The advances we are doing as a community revolve around the end-user experience.

What is your take on Distributed Persistent Rendering? Have you tried out On-Demand Builders in your application? Let me know more in the comments or call me out on Twitter. I am really curious!

## References

- “[A Complete Guide To Incremental Static Regeneration (ISR) With Next.js](https://www.smashingmagazine.com/2021/04/incremental-static-regeneration-nextjs/),” Lee Robinson
- “[Faster Builds For Large Sites On Netlify With On-Demand Builders](https://www.netlify.com/blog/2021/04/14/faster-builds-for-large-sites-on-netlify-with-on-demand-builders-now-in-early-access/),” Asavari Tayal, Netlify Blog
- “[Distributed Persistent Rendering: A New Jamstack Approach For Faster Builds](https://www.netlify.com/blog/2021/04/14/distributed-persistent-rendering-a-new-jamstack-approach-for-faster-builds/),” Matt Biilmann, Netlify Blog
- “[Distributed Persistent Rendering (DPR)](https://github.com/jamstack/jamstack.org/discussions/549),” Cassidy Williams, GitHub

{{< signature "vf, il" >}}

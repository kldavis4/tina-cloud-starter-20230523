---
title: 'Demystifying The New Gatsby Framework'
slug: demystifying-gatsby4-framework
author: juan-diego-rodriguez
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f177e4c-abee-408b-bbd3-b66a4bd41e60/demystifying-gatsby4-framework.jpg
date: 2022-06-27T12:30:00.000Z
summary: >-
  Gatsby 4 came out in October 2021 with a lot of new features. It may seem as if Gatsby 4 didn’t cause a big stir among developers, but it brought several game-changing features. Let’s see what v4 brings to the table.
description: >-
  Gatsby 4 came out in October 2021 with a lot of new features. It may seem as if Gatsby 4 didn’t cause a big stir among developers, but it brought several game-changing features. Let’s see what v4 brings to the table.
categories:
  - API
  - Gatsby
  - Next.js
  - Frameworks
  - Serverless
---

After the release of Gatsby 4, the Gatsby team saw the biggest rise in signups on Gatsby Cloud. According to Gatsby co-founder Kyle Mathews: 

<blockquote>“Gatsby 4 is the most powerful version of Gatsby yet. We’ve made Gatsby 10x faster to build and deploy by opening up two new rendering modes, adding support for Parallel Query Processing, and making a host of other optimizations and improvements.”<br /><br />&mdash; Kyle Mathews</blockquote>

Until a few months ago, Gatsby.js was best suited to make not-so-big Jamstack websites, but with the release of Gatsby 4, how well does Gatsby work with big and rapidly-changing pages? And how will it compare to other frameworks like Next.js? We will hopefully answer these questions in the next article!

## New Gatsby 4 Features

Gatsby 3 had a lot of useful features, and it stood out among other pre-rendering frameworks due to being extremely fast when using Static Site Generation. However, it lacked the tools of other frameworks &mdash; mainly Next.js &mdash; to render pages on request using Server-Side Rendering. Gatsby heard its community, and besides a lot of optimization features, Gatsby 4 brought two more rendering options: **Deferred Static Generation (DSG)** and the good old **Server-Side Rendering (SSR)**. 

### Deferred Static Generation (DSG)

One of the problems that a lot of people had with Gatsby was its very long build times. When using SSG, building the pages and all the heavy lifting had to be done on the server, which led to longer build times as pages in your site grew. To solve this, Gatsby started to use *incremental building* only to build new or changed pages and keep the other ones in the cache. However, the first build without cache always took a long time to finish. The incremental building is very helpful, but it didn’t tackle the roots of the problem, and that’s where Deferred Static Generation comes in. 

Deferred Static Generations is very similar to what SSG achieves, but it is more efficient and has a different method of delivering pages. In DSG, you can choose pages to “delay,” which means not to build with the rest of the pages but once a user requests them. After the first request, the page will be available in the CDN and will be the same as any other page generated with SSG. This is very useful when a site has old and unvisited pages that aren’t worth building on each production build. 

If you are worried that DSG can tank your page’s SEO, remember that pages built using DSG only behave as a Server-Side Rendered the first time they are requested, and then they act just like any other SSG page. So, according to Gatsby, your page will act as an SSG 99.9% of the time, and Google will analyze its SEO that way.

As you may notice, **DSG requires a running server to listen for user requests and build the requested page for every other user onwards**. It is a game-changing feature in Gatsby since Gatsby was known for being a server-less SSG framework, but now you can combine SSG with other rendering options involving a server. Even though it changes the backend structure &mdash; only if you use DSG or SSR &mdash; it gives developers more flexibility to work with Gatsby.

### Server-Side Rendering (SSR)

If DSG uses a server to work, does that mean that Gatsby can use a server to render all pages on request time? Absolutely yes. This was the most long-awaited feature in Gatsby and the only one that made a lot of developers choose other pre-rendering frameworks over Gatsby. In case you don’t know, Server-Side Rendering consists in building a page each time a user requests it. And it’s very useful when the page content depends on the user that requested it, so we can deliver a static and customized page to each user.

SSR is a well-known feature used daily in frameworks like Next.js, which Gatsby finally implemented. Now developers using Gatsby have an enormous range of options to deliver pages to users, either with Static Site Generation, Deferred Site Generation, Server-Side Rendering, or even &mdash; if you are brave enough &mdash; with Client-Side Rendering.

### Parallel Query Running

Besides the new rendering options, Gatsby still brings a lot of other features to improve performance and developer experience. As previously mentioned, one of the major drawbacks JAMstack and static sites had was their long building times. In addition to incremental building and DSG, Gatsby 4 introduces Parallel Query Running to diminish build time even more.

As you may know, Gatsby uses a data layer to group external data and then query it onto your site. Sourcing the data from your content sources into the data layer is relatively easy and fast. However, the process of querying the data from the data layer and querying it into the pages is pretty time-consuming. This step is called **query running**, which happens in the middle of the build and is the longest by far, taking around 40% of the build time.

Query running only was able to use one of the cores of the CPU, so all the queries had to be done one at a time. But in Gatsby 4, the entire way data was handled was changed since it migrated from Redux to its own in-memory data store and switched to [lmdb-js](https://github.com/DoctorEvidence/lmdb-js).

<blockquote>“Lmdb-js is an ultra-fast NodeJS and Deno interface to LMDB; probably the fastest and most efficient key-value/database interface that exists for storage and retrieval of structured JS data.”</blockquote>

With this new architecture, all queries can be done across all available cores, which leads to immensely faster build times.

### Build Time Optimization

Lastly, both a little and big change that may pass unnoticed between all the prior features is all the configurations and tweaks made to improve build times. One of the major reasons build times and even developer server starts were slow was due to an incorrect configuration of the local development environment or when Gatsby’s sites were deployed anywhere other than Gatsby Cloud. 

The Gatsby team has changed several critical parts of Gatsby’s infrastructure across Gatsby 3 minor updates and is now in Gatsby 4 to reduce build and development times. I consider reducing development times a key change to enhance developer experience since it becomes tedious to restart and wait for the developer server each time you make a change that requires a restart to take effect. 

{{% feature-panel %}}

## Gatsby Cloud

### What’s Gatsby Cloud

Even though Gatsby is known for being a framework, the Gatsby team offers other great products like Gatsby Cloud. Gatsby Cloud is a deployment service with an edge network dedicated uniquely to deploying Gatsby sites in a matter of minutes. It has been around for a long time and is very similar to Netlify. The service has been optimized only to build and host Gatsby sites, which means you can’t host Next.js, Vue, Angular, or Vanilla JS sites, but in exchange, Gatsby Cloud offers greatly faster build times for Gatsby sites. 

### Configuration

**The main advantage of using Gatsby Cloud to host your Gatsby project is the little to no configuration you need to start hosting it.** It can host and run a Gatsby Project without configuration and supports all Gatsby’s new rendering features and more out of the box. As long as they are declared in your code, the server won’t have problems understanding and hosting your project. So, if you want to migrate from Gatsby 3 to 4, you may consider switching to Gatsby Cloud for your migration.

### Build And Deployment Time

As said before, a lot of people didn’t prefer Gatsby due to its long build times. But Gatsby Cloud brings even more features to make build times faster, and it has been configured to use all optimization features like incremental buildings, parallel querying, caching, and support pages using DSG to the point where a CMS update from Contentful on Gatsby’s 10,000-page site took around 10 seconds on average.

Besides build time, another aspect that has been drastically improved with Gatsby Cloud is deployment time. Deployment time is the time it takes to push your site onto the edge of the CDN, and it accounts for the final time between triggering a build and releasing your site to the world. It can take as much time as build time, to the point that deployment times for a medium-size static site of around 10,000 pages can take 2 to 10 minutes. But the same medium-size site takes, on average, a surprising 2-5 seconds in Gatsby Cloud. 

### Workflow

Similar to Netlify, Gatsby Cloud workflow is based on Github, Gitlab, or BitBucket repositories. Gatsby Cloud fetches a Gatsby project from a repository, builds the site, and/or runs the server. And like many other services, you can enable automatic deployment when a branch changes in your repository. In case external data from a source like a CMS changes, Gatsby Cloud offers a build webhook to trigger a production build.

Other small workflow features I really liked were: 

- **Previewing**  
It lets you create a preview site with all your changes and a shareable URL.
- **Lighthouse Support**  
It gives you a Lighthouse report every time a build is finished.

### Gatsby Functions

Lastly, we will see Gatsby’s serverless functions in action. They aren’t completely part of Gatsby Cloud since they can be deployed in Netlify too, but deploying Gatsby Functions is more straightforward in Gatsby Cloud. Now, what are Gatsby’s Functions? In simpler terms, they let you add an express-like backend to your Gatsby project to create an API, authenticate users, or submit forms.

Why would I want to create a backend in my Gatsby project? Most Gatsby use cases don’t require creating a backend or API. Still, in cases where there is more than one frontend application using the same data, it is a very good idea to decouple your data from your main frontend and make it accessible through an API, so it is accessed the same way with the same logic through all frontends. The power of Gatsby Functions is to have your backend hosted in the same place as your frontend, but they communicate headlessly through an API.

### Gatsby Cloud vs. Netlify

After seeing all the features offered by Gatsby Cloud, there isn’t a decisive factor in choosing one over another. Both of them offer pretty similar services and functionalities, and they come in a free tier, too. The main difference is that you can only host a Gatsby project in Gatsby Cloud, but with Netlify, you can host projects using almost any library or framework you want, such as Next.js, create-react-app, Vue, Angular, etc. So, in case you want to host a Gatsby project, I would recommend Gatsby Cloud since it is amazingly optimized and guarantees good results.

{{% ad-panel-leaderboard %}}

## Gatsby 4 vs. Next.js

In the SSR ecosystem, the clear dominant player has been Next.js, and many comparisons between Gatsby and Next.js ended by saying that Next.js offered SSR and Gatsby did not. And even though Gatsby was still extremely useful and effective, the fact that it didn’t support SSR was a decisive factor when choosing a framework to use. But the introduction of Gatsby 4 changed the game completely.

Since this article is dedicated to Gatsby’s new features, I will try not to focus too much on Next.js features. Still, I will say that Next.js and Gatsby currently offer similar functionality, and we can achieve almost the same results with both frameworks. However, there are still a lot of factors and features to consider when choosing one framework or the other. Gatsby offers features that Next.js doesn’t, like Deferred Static Generation, a data layer, and an enormous plugin library. On the same note, Next.js offers [Incremental Static Regeneration](https://nextjs.org/docs/basic-features/data-fetching/incremental-static-regeneration) and [Server Components](https://nextjs.org/blog/next-12#react-server-components) which is currently on alpha. 

You can achieve the same user experience with both frameworks, and they will help you make beautiful websites. So, to choose a framework, I strongly believe the **developer experience is the decisive factor**. I feel Gatsby offers a better DX due to its awesome data layer that lets developers source their data and keeps it all in the same place, so it can be queried the same way. Another reason is its plugin library, which lets you add out-of-the-box support to CMS, internalization, e-commerce, analytics, offline support, et cetera. These are life-saving features that have helped me quickly start working on a new project.

{{% ad-panel-leaderboard %}}

## Conclusion

After seeing all the new features of Gatsby 4, we can confidently say that the future of Gatsby is already looking great! It is clear that the Gatsby team has been pretty self-critical and has heard its community since all Gatsby 4 features were wanted by the community for a long time. Therefore, I am pretty confident that Gatsby will keep following this path, and we will have many other cool features in the future.

Even though I might sound like a Gatsby salesman, I don’t consider it the best framework, just one that is completely worth experimenting with. Next.js is vastly more used among the SSR ecosystem, and the [community](https://2021.stateofjs.com/en-us/libraries/back-end-frameworks/) believes it gives a better developer experience than Gatsby, but with Gatsby 4 this trend may change a little. It isn’t putting Next.js out of business any time soon, but thanks to its new rendering options, Gatsby 4 will clearly be on your list of frameworks to try out on your next project.

{{< signature "yk, il" >}}

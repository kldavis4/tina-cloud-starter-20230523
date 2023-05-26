---
title: 'A Look At Remix And The Differences With Next.js'
slug: look-remix-differences-next
author: facundo-giuliani
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e925a90-8fec-44cb-92c0-2ab03d13a2ea/look-remix-differences-next-sharing-card.jpg
date: 2022-07-11T09:00:00.000Z
summary: >-
  Let’s talk about Remix, the framework to create JavaScript projects using server-side rendering. Let’s go through its main features and concepts and see the similarities and differences with Next.js. Remix became open-source not so long ago, and it has a promising future. Let’s see how it evolves, which features are added, which related projects are created to improve the developer experience, and which other scenarios it tries to solve.
description: >-
  Let’s talk about Remix, the framework to create JavaScript projects using server-side rendering. Let’s go through its main features and concepts and see the similarities and differences with Next.js.
categories:
  - Apps
  - Frameworks
  - Next.js
  - JavaScript
---

In the developer community, it is very common to see new frameworks and tools appear every day. Some of them offer a different approach to solve scenarios that are currently being solved with other tools. Others bring a new concept or idea, proposing a different way to face the projects. As the carpenter has different tools to do different tasks, the developers have many available frameworks and libraries that are a good fit for different use cases.

Let’s talk about Remix, the (kind of) new framework to create JavaScript projects using server-side rendering. Let’s go through its main features and concepts and see the similarities and differences with another popular JavaScript framework: Next.js.

## What’s Remix?

According to [its official website](https://remix.run/), Remix is an edge-first full stack framework that allows developers to create great user experiences focusing on web standards. With it, you can create your web application using React and JavaScript for both the client-side rendering and server-side rendering.

As it is built on the Web Fetch API, applications created with Remix can run anywhere. Remix uses server-side rendering to manipulate the data and render the HTML content in the server, sending the less amount of JavaScript possible to the client.

Remix was originally a subscription-based premium framework but, less than a year ago, it was launched as an open-source framework. After this, the community of Remix developers and users started to grow and get more popular.

## Remix Main Features

Let’s highlight some of the main features provided by Remix:

- **Routes:**  
    Like other frameworks, Remix allows developers to manage the different routes of their web projects using JavaScript/TypeScript files that contain handler functions. We’re able to generate routes in our website creating files that follow the file system hierarchy of our projects, creating analog URLs for our pages. Remix routes work using the partial routing feature provided by [React-Router](https://reactrouter.com/). With this approach in mind, we can highlight the following benefits.

- **Nested components:**  
    Remix gives you the possibility of managing nested pages and components. We can create a file to handle a certain route and, at the same level in the file system, a folder with the same name. All the files that we create inside that folder will be nested components of the parent route, instead of different pages.

- **Error Handling:**  
    Nested components bring another benefit: if an error occurs while rendering a certain component, it doesn’t affect the other nested parts of the page. So, we can encapsulate the error just in the section where it happened, instead of getting a general page error.

- **Forms:**  
    As Remix focuses on web standards, it uses native methods (`POST`, `PUT`, `DELETE`, `PATCH`) to handle forms instead of using JavaScript for that.

- **Loaders and Actions:**  
    Remix provides two different types of functions to create server-side dynamic content. The `loader` functions are used to handle `GET` HTTP requests in the server, mainly used to get data from different sources. The `action` functions monitor `POST`, `PUT`, `DELETE`, and `PATCH` requests, focused on data manipulation and modification.

Now, that we talked about some of the main features of Remix, let’s compare it with one of the most popular and most used React frameworks nowadays: Next.js.

{{% feature-panel %}}

## What are the differences between Remix and Next.js?

If we take a quick look, Next.js and Remix may seem like they re following the same goal &mdash; and, probably, they do. But if we analyze the features and approaches they offer, we will identify similarities and differences, and we can think about scenarios being solved in a more suitable way with one of the frameworks more than the other.

### React Based

Both frameworks were created on top of React, but Remix tries to decouple itself from it. We can see that Remix provides higher levels of abstraction. Also, different Remix community members have been working on different implementations [using other frameworks](https://twitter.com/kentcdodds/status/1537170381718507520), like Vue.js, Angular, and Svelte. Next.js depends on React, and there is no plan to change this at the moment.

### Server-side Rendering

Besides the features we mentioned above, we can see that both Remix and Next.js offer server-side rendering (SSR) to generate the markup and content of our pages from the web server before sending it to the client.

Both Next.js and Remix use React, so they can rely on features like client-side hydration. On the other hand, both frameworks also support pre-rendering HTML from the server. Depending on the project we are working on, we may want to generate as much content as possible server-side, avoiding to send JavaScript code, and fetching data from the client.

{{% ad-panel-leaderboard %}}

### Static Site Generation

On the other hand, Next.js offers the possibility of pre-generating static pages and content at build time, using static site generation (SSG), while Remix doesn’t. Depending on the type of pages we want to create, this features is something that could provide great benefits. With SSG we can fetch data and render pages at build time, having static pages before the users visit our website, without having to wait for the content to be generated.

But SSG could also become problematic: whenever we apply changes to the code or the content of our application, we need to wait for a build process to generate the new version of the static assets. This could become a pain point, since build time will increase if our project gets bigger and bigger. To handle this problem, ​​the Next.js team developed a feature called [Incremental Static Regeneration](https://nextjs.org/docs/basic-features/data-fetching/incremental-static-regeneration) (ISR), and the brand new [On-Demand ISR](https://nextjs.org/blog/next-12-2#on-demand-incremental-static-regeneration-stable).

### Stale While Revalidate

To serve content as fast as possible, Remix relies on the [stale-while-revalidate caching directive](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) (SWR). Instead of pre-generating static content, it primes the cache when the app is getting traffic. The pages and documents are served from the cache, while they revalidate in the background for the next visitor.  

Next.js also offers the possibility of working with stale-while-revalidate. Inside the `getServerSideProps`​ function, you can use stale-while-revalidate [cache control headers](https://nextjs.org/docs/basic-features/data-fetching/get-server-side-props#caching-with-server-side-rendering-ssr).

### Client-side Navigation

One of the features used by Next.js to offer a smooth navigation to the users is *prefetching*. We can use the `<Link>` component to make our website to pre-load the page that `<link>` redirects to  when the element appears in the viewport. If we visit the homepage of a website and we see a “Contact” link on the page, Next.js will download and fetch the content related to the contact page. So, when we click on the link, we don’t have to wait for the page to be downloaded.

But there is a limitation: ​​the `Link​` component only offers prefetching for pages that were pre-built using static site generation (SSG). If we have links to pages that are generated dynamically, the feature won’t be triggered.

Remix uses the HTML `<link rel="prefetch">​` tag (instead of a cache like Next.js `Link​` component), so we can prefetch not only links, but actually any page. In the case that we want to implement something similar using Next.js, it's possible using the `next/head`​ component, and adding the `prefetch`​ tag.

### Edge First

When we’re fetching data and rendering content from the server, we also have to evaluate how far is the server that executes the code from the users sending the HTTP requests. If my main server is located in Brazil, and a user is visiting my website from China, the page load process will be slower than mine, if I visit the same page from Argentina. This is related to the geographical distance the HTTP request has to travel to the closer server that evaluates it and executes the code.

Even though modern applications rely on CDNs to deliver static content, the server-side code that is processed to generate dynamic content is generally executed in the data center, running in a particular location. A workaround to this scenario would be using the SWR caching directive, with the caveat of eventually serving stale content while the CDN refreshes the resource.

Having this issue in mind, in the last years, a new concept was originated: Edge computing. The idea is to follow the same approach used by the CDNs, replicating the server logic in different servers and locations, executing the dynamic code as closer to the user as possible. While Remix is defined as “Edge First,” meaning that the framework was thought to run on the Edge from its conception, Vercel launched the [Edge Functions](https://vercel.com/features/edge-functions) as an additional feature for the application deployed in the platform.

### Server-side Code

When describing the main features of Remix, we said the framework uses native HTTP methods to manage forms with the help of `action` and `loader` functions. A form, a server, a `POST` request that transports the form’s serialized data to the server, a server-side action, a new page as the result of our request. Back to the web standards.

Remix provides the `<Form>` element, an optimized version of the HTML form. With it and the `action` functions, we can have the client code and the server code related to our routes altogether in the same file. Remix will know how to manage the user interface of our pages and the server-side behavior attached to the requests. No context, no state management.

Next.js, on the other hand, relies on JavaScript code to know how to manage the state of the application, which APIs call, revalidate data and update the interface of the web page. Using [API Routes](https://nextjs.org/docs/api-routes/introduction), we can have separate files that execute server-side functionality and return data to our frontend.

As we said, and as you can see, Remix has a way of mutating the data that tries to go back to the basics, recalling those days when PHP was the big thing.

{{% ad-panel-leaderboard %}}

### Node.js dependency

As we said before, Remix is based on the Web Fetch API, instead of depending on Node.js. That gives us the possibility of running Remix applications not only over Node.js servers (like Vercel or Netlify), but also on other types of platforms (like Cloudflare Workers or the new Deno Deploy).  

With [the latest version of Next.js, 12.2](https://nextjs.org/blog/next-12-2), you can now select the Edge Runtime for your entire Next.js project, instead of using the default Node.js runtime.

## Conclusion

Remix became open-source not so long ago, but it already has a very active community collaborating and creating projects following the web standards. The framework has a promising future. Let’s see how it evolves, which features are added, which related projects are created to improve the developer experience, and which other scenarios it tries to solve.

### Further Reading on Smashing Magazine

- “[Remix Routes Demystified](https://www.smashingmagazine.com/2022/03/remix-routes-demystified/),” Átila Fassina
- “[Dynamic Data-Fetching In An Authenticated Next.js App](https://www.smashingmagazine.com/2022/04/dynamic-data-fetching-authenticated-nextjs-app/),” Caleb Olojo
- “[How To Maintain A Large Next.js Application](https://www.smashingmagazine.com/2021/11/maintain-large-nextjs-application/),” Nirmalya Ghosh
- “[Localizing Your Next.js App](https://www.smashingmagazine.com/2021/11/localizing-your-nextjs-app/),” Átila Fassina

{{< signature "nl, il" >}}

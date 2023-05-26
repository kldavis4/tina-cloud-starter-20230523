---
title: 'The What, When, Why And How Of Next.js’ New Middleware Feature'
slug: next-js-middleware-feature
author: sam-poder
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b614fa99-6432-4f8f-bb7a-234b9e0c082e/next-js-middleware-feature.jpg
date: 2022-04-01T10:30:00.000Z
summary: >-
   Next.js’ recent 12.0 release included a new beta feature: middleware. For a detailed explanation, you can read all about it in Sam’s previous article, “[Next.js Wildcard Subdomains](https://www.smashingmagazine.com/2021/11/nextjs-wildcard-subdomains/)”. This article, on the other hand, dives into the overall concept of middleware and how handy it can be in building things.
description: >-
   Next.js’ recent 12.0 release included a new beta feature: middleware. For a detailed explanation, you can read all about it in Sam’s previous article, “[Next.js Wildcard Subdomains](https://www.smashingmagazine.com/2021/11/nextjs-wildcard-subdomains/)”. This article, on the other hand, dives into the overall concept of middleware and how handy it can be in building things.
categories:
  - API
  - Guides
  - Next.js
  - JavaScript
---

“Middleware” isn’t a new term in computing. It is often used as a term to describe a piece of software that holds two systems together. You could call it “glue” for software, and essentially, that’s how Next.js’ middleware works.

Next.js’ middleware allows you to create functions that execute after a user’s request is made and before the request is completed &mdash; in the middle of the two processes. This enables you to process a user’s request and then modify the response by rewriting, redirecting, modifying headers, or even streaming HTML. 

Within Next.js, middleware operates in a limited runtime described as the “Edge Runtime”. The code which ran through the runtime has access to a set of standard Web APIs, that’ll be discussed later in the article. For Vercel customers, middleware functions will be executed as [Vercel Edge Functions](https://vercel.com/features/edge-functions).

## What About API Routes?

As you read this article, you may be thinking about how middleware sounds awfully like Next.js’ API routes that have been around for a while. The key difference is how they are used: the more restricted runtime of middleware functions, individual requests are made to API routes, whilst Middleware functions operate in between a user’s request to a page, and that page’s being rendered.

This also means that Middleware can be scoped to multiple pages allowing you to avoid repeating code. For example, if you need to change each page in the `app` directory based on whether a user is logged in, you could create a Middleware function within that directory to process users’ cookies to see if they're logged in, and then pass that information onto the page. In comparison, achieving a similar effect would require extra code within an API route.

The primary technical difference between the two is that Next.js’ API routes were designed to be hosted on a single node server hosted in one place, whilst Middleware functions are designed to be deployed on the “edge”, which is essentially a marketing term for deploying code in multiple locations around the world. Alongside the difference in physical distance, the “edge” is commonly associated with aggressive caching and efficient cache invalidation which reduces unnecessary computation. 

The goal of this is speed. A server’s response generally arrives faster when the user is closer to the server, so when you have only one server, those speeds are only accessible to a subset of your users. However, with your code being deployed in multiple locations, more users will have access to fast responses.  

Lastly, Middleware is designed to have no cold boot time. An API route’s boot time is a significant cause of slow responses. On Vercel, Serverless Functions (which are used to deploy API routes) normally take around 250 milliseconds to boot. Middleware is also designed to startup in much less time than API routes, Vercel claims that their Edge Functions (which are used to deploy Next.js Middleware) have a “100x faster startup” than their Serverless Functions.

{{% feature-panel %}}

## When Should I Use Middleware?

Middleware should be used in cases where a small amount of processing is required, this is because Middleware needs to return a response in less than 1.5 seconds, otherwise the request will time out. 

### Geolocation

The `NextRequest` object which is available within Middleware has geographic information available in the `geo` key. Using this information, you could then rewrite your user to pages with localized information. For example, if you were creating a site for a global restaurant chain, you could show a different menu depending on the user’s location. Vercel’s [example here](https://github.com/vercel/examples/tree/main/edge-functions/power-parity-pricing) uses this geolocation to provide Power Parity Pricing.

This can work alongside Next.js’ i8n / localization feature, like [this](https://github.com/vercel/examples/tree/main/edge-functions/i18n).

### Security

Through the `NextRequest` object, the cookie information is available (on the `cookies` key), and by using `NextResponse` you can set cookies. These cookies can be used to authenticate users on your site.

You may also want to block access to your sites from certain users, such as bots or users in a certain country. To achieve this you can conditionally return a 404 or rewrite the request to a “blocked” page. Vercel has an example of blocking based on location [here](https://github.com/vercel/examples/tree/main/edge-functions/geolocation-country-block).

### A/B Testing

Previously, to show a different page to a user on a static site as part of A/B testing (or a similar exercise) you would have had to process the user’s request on the client-side which can cause cumulative layout shifts or a flash. However, if we process it on a server this can be avoided. 

To achieve this you can place users in “buckets” through cookies, and then redirect them based on the bucket their cookie places them in. View [Vercel’s example](https://github.com/vercel/examples/tree/main/edge-functions/ab-testing-simple) to see how that can work.

{{% ad-panel-leaderboard %}}

## The Limitations of Middleware

Middleware is starting to sound pretty wonderful, isn’t it? Whilst it is wonderful, there are some drawbacks which means that you’ll probably still be needing API routes for certain use cases.

Some of these limitations are specific to Vercel deployments of Next.js sites, however, similar limitations exist on other platforms. 

### Execution Time (Vercel specific)

A middleware function can execute for a maximum of thirty seconds, however, as I mentioned above, it must return a response within one and a half seconds. This means that your function should return a response as soon as possible, and you can then continue any other workloads in the background if you need to. For example, if you were looking to do server-side analytics, you could extract the information you need, return a response, and then make a call to your database to log the information after returning the response.

### Function Size (Vercel specific)

A Middleware function can be at most 1MB, this includes all other code bundled with the function. Most use cases won’t require such a large code bundle, but it’s certainly something to keep an eye on.

### Native Node.js APIs Aren’t Supported

Middleware functions don’t run through Node.js like the rest of Next.js’ server-side code does (such as API Routes). One of the key things that limit Middleware functions from performing is reading and writing to the filesystem.

This also means that JavaScript modules that rely on native Node.js APIs also can’t be used.

### ES Modules Only

Node Modules can be used within middleware, however, they must be ES Modules. Whilst there is a growing shift within the ecosystem to switch to ES Modules, there are still many packages that use CommonJS or rely on other packages through CommonJS. 

### No String Evaluation

Neither JavaScript’s `eval` or `new Function(evalString)` are allowed within the runtime.

{{% ad-panel-leaderboard %}}

## Implementing Middleware

To explore how Middleware works we’ll be creating a link shortener that’ll be much faster than those that use API routes. 

To get started, clone the starter for the app:

<div class="break-out">

<pre><code class="language-bash">yarn create next-app -e https://github.com/sampoder/middleware-demo/tree/starter</code></pre>
</div>

The starter has two key files: `routes.js` & `pages/index.js`. `routes.js` will contain all the routes for our link shortener. Normally, you’d use a database, but for the purpose of this exercise, we'll keep it simple with a hardcoded key/value object. `pages/index.js` will serve as our link shortener's homepage with a list of all the available routes.

Then we’ll create our Middleware function by creating a new file named `_middleware.js` in the `pages` directory. A middleware function is scoped to the directory, affecting sibling and children routes. For example, as the `/pages` directory is linked to the `/` routes, thus if the middleware is placed in the `/pages` directory, it will apply to routes, such as `/about` or `/about/team/john`. Meanwhile, if the middleware was placed in the `/pages/blog` directory, it would apply to routes, such as `/blog/middleware` or `/blog/about/submit`, but not `/info`.

We then will need to import `NextResponse` from `next/server`:

<pre><code class="language-javascript">import { NextResponse } from 'next/server'</code></pre>

As the `NextResponse` object is an extension of the Node.js’ `Response` interface, it’ll allow us to modify the response.

We’ll also need to import the routes file:

<pre><code class="language-javascript">import routes from "../routes"</code></pre>

Each Middleware file needs to export a function named `middleware`. This will be what Next.js runs on request:

<pre><code class="language-javascript">export function middleware(req) {
  
}</code></pre>

The middleware function will be passed through a request object. Similar to the `NextResponse` object, this request object is an extension of the Node.js’ `Request` interface. It’ll give us information about the client’s request.

Through this request object we can then access the path name of the current request via the `nextUrl` key: 

<pre><code class="language-javascript">let { pathname } = req.nextUrl;</code></pre>

For our link shortener we will need to check whether our `routes` object contains a key with the same value as the pathname:

<pre><code class="language-javascript">if (routes[pathname]) {

}</code></pre>

Then we can use the `NextResponse` object to modify the response. The `NextResponse` object enables us to both `redirect()` and `rewrite()` responses to different locations. As we’re building a URL shortener, we’ll use the `redirect()` method to transport users to their intended destination:

<pre><code class="language-javascript">if (routes[pathname]) {
  return NextResponse.redirect(routes[req.nextUrl.pathname])
}</code></pre>

We’ve created a new `NextResponse` object, applied the redirect method, and then returned that object.

We also need to handle cases in which the pathname doesn’t have a matching destination. In these cases, we’ll redirect the users to our homepage:

<pre><code class="language-javascript">else{
  const url = request.nextUrl.clone()
  url.pathname = '/'
  return NextResponse.redirect(url)
}</code></pre>

We can’t redirect to `/` directly, because support for relative URLs within Middleware will be [deprecated soon](https://nextjs.org/docs/messages/middleware-relative-urls). Instead, we make a clone of the request’s URL and change the pathname, before passing that URL object to the `redirect()` function.

And just like that we’ve got a functioning link shortener! For those curious, our entire middleware function ended up as:

<pre><code class="language-javascript">import { NextResponse } from "next/server";
import routes from "../routes";

export function middleware(req) {
  let { pathname } = req.nextUrl
  if (routes[pathname]) {
    return NextResponse.redirect(routes[req.nextUrl.pathname])
  }
  else{
    const url = request.nextUrl.clone()
    url.pathname = '/'
    return NextResponse.redirect(url)
  }
}</code></pre>

And the entire codebase is available at [https://github.com/sampoder/middleware-demo](https://github.com/sampoder/middleware-demo). 

Whilst this example is short, it shows how handy middleware can be in building things. When you run the web app, you’ll also see how fast it can be.

Last but not least, middleware has a lot of promise, and I hope you enjoyed exploring the feature with me!

{{< signature "vf, yk, il" >}}

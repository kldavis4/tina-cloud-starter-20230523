---
title: 'A New Pattern For The Jamstack: Segmented Rendering'
slug: new-pattern-jamstack-segmented-rendering
author: eric-burel
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0882ee9-5036-4823-8000-840568240d79/new-pattern-jamstack-segmented-rendering-sharing-card.jpg
date: 2022-07-18T11:00:00.000Z
summary: >-
  Among all possible architectures for rendering a website, static rendering is the most performant. Yet, it’s only applicable to public, generic content. Or is it? In this article, we will push the boundaries of static rendering and learn how to apply it to personalized content. This new pattern is called “Segmented Rendering” and will change the Jamstack game forever.
description: >-
  “Segmented Rendering” is a new pattern and it will change the Jamstack game forever. Let’s try to push the boundaries of static rendering and learn how to apply it to personalized content. 
categories:
  - Performance
  - JavaScript
  - Jamstack
  - Next.js
---
If you think that static rendering is limited to generic, public content that is the same for every user of your website, you should definitely read this article.  

Segmented Rendering is a new pattern for the Jamstack that lets you personalize content statically, without any sort of client-side rendering or per-request Server-Side Rendering. There are many use cases: personalization, internationalization, theming, multi-tenancy, A/B tests…

Let’s focus on a scenario very useful for blog owners: handling paid content.

## Congratulations On Your New Job

Wow, you just got promoted! You are now “Head of Performance” at Repairing Magazine, the most serious competitor to Smashing Magazine. Repairing Magazine has a very peculiar business model. **The witty jokes in each article are only visible to paid users.**

<blockquote>Why did the programmer cross the road?</blockquote>

I bet you’d pay to know the answer.

Your job for today is to implement this feature with the best possible performances. Let’s see how you can do that. Hint: we are going to introduce a new pattern named “Segmented Rendering.”

## The Many Ways To Render A Web Page With Modern JavaScript Frameworks

Next.js popularity stems from its mastery of the “Triforce of Rendering:” the ability to combine client-side rendering, per-request server-rendering and static rendering in a single framework.
### CSR, SSR, SSG… Let’s Clarify What They Are

Repairing Magazine user interface relies on a modern JavaScript library, React. Like other similar UI libraries, React provides two ways of rendering content: client-side and server-side.

Client-Side Rendering (CSR) happens in the user’s browser. In the past, we would have used jQuery to do CSR.

Server-side rendering happens on your own server, either at request-time (SSR) or at build-time (static or SSG). SSR and SSG also exist outside of the JavaScript ecosystem. Think PHP or Jekyll, for instance.

Let’s see how those patterns apply to our use case.

### CSR: The Ugly Loader Problem

Client-Side Rendering (CSR) would use JavaScript in the browser to add witty jokes after the page is loaded. We can use “fetch” to get the jokes content, and then insert them in the DOM.

<div class="break-out">

<pre><code class="language-javascript">// server.js
const wittyJoke =
  "Why did the programmer cross the road?\
   There was something he wanted to C.";
app.get("/api/witty-joke", (req) =&gt; {
  if (isPaidUser(req)) {
    return { wittyJoke };
  } else {
    return { wittyJoke: null };
  }
});

// client.js
const ClientArticle = () =&gt; {
  const { wittyJoke, loadingJoke } = customFetch("/api/witty-jokes");
  // THIS I DON’T LIKE...
  if (loadingJoke) return &lt;p&gt;Ugly loader&lt;/p&gt;;
  return (
    &lt;p&gt;
      {wittyJoke
        ? wittyJoke
        : "You have to pay to see jokes.\
         Humor is a serious business."}
    &lt;/p&gt;
  );
};
</code></pre>
</div>

*CSR involves redundant client-side computations and a lot of ugly loaders.*

It works, but is it the best approach? Your server will have to serve witty jokes for each reader. If anything makes the JavaScript code fail, the paid user won’t have their dose of fun and might get angry. If users have a slow network or a slow computer, they will see an ugly loader while their joke is being downloaded. Remember that most visitors browse via a mobile device!

This problem only gets worse as the number of API calls increases. Remember that a browser can only run a handful of requests in parallel (usually 6 per server/proxy). Server-side rendering is not subject to this limitation and will be faster when it comes to fetching data from your own internal services.

### SSR Per Request: Bitten By The First Byte

Per-request Server-Side Rendering (SSR) generates the content on demand, on the server. If the user is paid, the server returns the full article directly as HTML. Otherwise, it returns the bland article without any fun in it.

<div class="break-out">

<pre><code class="language-javascript">// page.js: server-code
async function getServerSideProps(req) {
  if (isPaidUser(req)) {
    const { wittyJoke } = getWittyJoke();
    return { wittyJoke };
  } else {
    return { wittyJoke: null };
  }
}
// page.js: client-code
const SSRArticle = ({ wittyJoke }) =&gt; {
  // No more loader! But...
  // we need to wait for "getServerSideProps" to run on every request
  return (
    &lt;p&gt;
      {wittyJoke
        ? wittyJoke
        : "You have to pay to see jokes. Humor is a serious business."}
    &lt;/p&gt;
  );
};
</code></pre>
</div>

*SSR removes client-side computations, but not the loading time.*

We don’t rely on client-side JavaScript anymore. However, it’s not energy-efficient to render the article for each and every request. The Time To First Byte (TTFB) is also increased because we have to wait for the server to finish its work before we start seeing some content.

We’ve replaced the ugly client-side loader with an even uglier blank screen! And now we even pay for it!

The “stale-while-revalidate” cache control strategy can reduce the TTFB issue by serving a cached version of the page until it’s updated. But it won’t work out-of-the-box for personalized content, as it can cache only one version of the page per URL without taking cookies into account and cannot handle the security checks needed for serving paid content.

### Static Rendering: The Key To The Rich Guest/Poor Customer Problem

At this point, you are hitting what I call the “rich guest/poor customer” problem: your premium users get the worst performance instead of getting the best.

By design, client-side rendering and per-request server-side rendering involve the most computations compared to static rendering, which happens only once at build time.

99% of the websites I know will pick either CSR or SSR and suffer from the rich guest/poor customer problem.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a28ff8b-2e1b-44f9-b94b-621f2a6524c7/1-v2-new-pattern-jamstack-segmented-rendering.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a28ff8b-2e1b-44f9-b94b-621f2a6524c7/1-v2-new-pattern-jamstack-segmented-rendering.jpg" width="800" height="533" sizes="100vw" caption="Let’s join the 1% and make our customers rich again. (Image credit: <a href='https://www.pexels.com/photo/woman-wearing-maroon-velvet-plunge-neck-long-sleeved-dress-while-carrying-several-paper-bags-photography-972995/'>Pexels</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a28ff8b-2e1b-44f9-b94b-621f2a6524c7/1-v2-new-pattern-jamstack-segmented-rendering.jpg'>Large preview</a>)" alt="A picture of a woman happy with many shopping bags." >}}

{{% feature-panel %}}

## Deep-Dive Into Segmented Rendering

Segmented Rendering is just a smarter way to do static rendering. Once you understand that it’s all about caching renders and then getting the right cached render for each request, everything will click into place.

### Static Rendering Gives The Best Performances But Is Less Flexible

Static Site Generation (SSG) generates the content at build-time. That’s the most performant approach because we render the article once for all. It is then served as pure HTML.

This explains why pre-rendering at build-time is one of the cornerstones of the Jamstack philosophy. As a newly promoted “Head of Performance,” that’s definitely what you want!

As of 2022, all Jamstack frameworks have roughly the same approach of static rendering:

- you compute a list of all possible URLs;
- you render a page for each URL.

<div class="break-out">

<pre><code class="language-javascript">const myWittyArticles = [
  "/how-to-repair-a-smashed-magazine",
  "/segmented-rendering-makes-french-web-dev-famous",
  "/jamstack-is-so-2022-discover-haystack",
];
</code></pre>
</div>

*Result of the first step of static rendering: computing a bunch of URLs that you will prerender. For a blog, it’s usually a list of all your articles. In step 2 you simply render each article, one per URL.*

This means that one URL strictly equals one version of the page. You cannot have a paid and a free version of the article on the same URL even for different users. The URL `/how-to-repair-a-smashed-magazine` will deliver the same HTML content to everyone, without any personalization option. It’s not possible to take request cookies into account.

Segmented Rendering can go a step further and render different variations for the same URL. Let’s learn how.

### Decoupling URL And Page Variation

The most naive solution to allow personalized content is to add a new route parameter to the URL, for instance, “with-jokes” versus “bland.”

<div class="break-out">

<pre><code class="language-markup">const premiumUrl = "/with-jokes/how-to-repair-a-smashed-magazine";
const freeUrl = "/bland/how-to-repair-a-smashed-magazine";
</code></pre>
</div>

An implementation with Next.js will look roughly like this:

<div class="break-out">

<pre><code class="language-javascript">async function getStaticPaths() {
  return [
    // for paid users
    "/with-jokes/how-to-repair-a-smashed-magazine",
    // for free users
    "/bland/how-to-repair-a-smashed-magazine",
  ];
}
async function getStaticProps(routeParam) {
  if (routeParam === "with-jokes") {
    const { wittyJoke } = getWittyJoke();
    return { wittyJoke };
  } else if (routeParam === "bland") {
    return { wittyJoke: null };
  }
}
</code></pre>
</div>

*The first function computes 2 URLs for the same article, a fun one and a bland one. The second function gets the joke, but only for the paid version.*

Great, you have 2 versions of your articles. We can start seeing the “Segments” in “Segmented Rendering” &mdash; paid users versus free users, with one rendered version for each segment.

But now, you have a new problem: how to redirect users to the right page? Easy: redirect users to the right page, literally! With a server and all!

It may sound weird at first that you need a web server to achieve efficient static rendering. But trust me on this: the only way to achieve the best performances for a static website is by doing some server optimization.

{{% ad-panel-leaderboard %}}

### A Note On “Static” Hosts

If you come from the Jamstack ecosystem, you may be in love with static hosting. What’s a better feeling than pushing a few files and getting your website up and running on GitHub Pages? Or hosting a full-fledged application directly on a Content Delivery Network (CDN)?

Yet “static hosting” doesn’t mean that there is no server. It means that you cannot control the server. There is still a server in charge of pointing each URL to the right static file.

Static hosting should be seen as a limited but cheap and performant option to host a personal website or a company landing page. If you want to go beyond that, you will need to take control over the server, at least to handle things such as redirection based on the request cookies or headers.

No need to call a backend expert though. We don’t need any kind of fancy computation. A very basic redirection server that can check if the user is paid will do.  

Great news: modern hosts such as Vercel or Netlify implements Edge Handlers, which are exactly what we need here. Next.js implements those Edge Handlers as “middlewares,” so you can code them in JavaScript.

The “Edge” means that the computations happen as close as possible to the end-user, as opposed to having a few big centralized servers. You can see them as the outer walls of your core infrastructure. They are great for personalization, which is often related to the actual geographical location of the user.

### Easy redirection with Next.js middlewares

Next.js middlewares are dead fast and dead simple to code. Contrary to cloud proxies such as AWS Gateway or open source tools such as Nginx, middlewares are written in JavaScript, using Web standards, namely the [fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).

In the “Segmented Rendering” architecture, middlewares are simply in charge of pointing each user request to the right version of the page:

<div class="break-out">

<pre><code class="language-javascript">import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

async function middleware(req: NextRequest) {
  // isPaidFromReq can read the cookies, get the authentication token,
  // and verify if the user is indeed a paid member or not
  const isPaid = await isPaidFromReq(req);
  const routeParam = isPaid ? "with-jokes" : "bland";
  return NextResponse.redirect(
    `/${routeParam}/how-to-repair-a-smashed-magazine`
  );
}
</code></pre>
</div>

*A middleware that implements Segmented Rendering for paid and free users.*

Well, that’s it. Your first day as a “Head of Performance” is over. You have everything you need to achieve the best possible performances for your weird business model!

Of course, you can apply this pattern to many other use cases: internationalized content, A/B tests, light/dark mode, personalization… Each variation of your page makes up a new “Segment:” French users, people who prefer the dark theme, or paid users.

### Cherry On The Top: URL Rewrites

But hey, you are the “Head of Performance,” not the “Average of Performance”! You want your web app to be perfect, not just good! Your website is certainly very fast on all metrics, but now your article URLs look like this:

<div class="break-out">

<pre><code class="language-markdown">/bucket-A/fr/light/with-jokes/3-tips-to-make-an-url-shorter
</code></pre>
</div>

That’s not really good-looking… Segmented Rendering is great, but the end-user doesn’t have to be aware of its own “segments.” The punishment for good work is more work, so let’s add a final touch: instead of using URL redirects, use URL rewrites. They are exactly the same thing, except that you won’t see parameters in the URL.

<div class="break-out">

<pre><code class="language-markdown">// A rewrite won’t change the URL seen
// by the end user =&gt; they won’t see the "routeParam"
return NextResponse.rewrite(`/${routeParam}/how-to-repair-a-smashed-magazine`);
</code></pre>
</div>

The URL `/how-to-make-an-url-shorter`, without any route parameter, will now display the right version of the page depending on the user’s cookies. The route parameter still “exists” in your app, but the end-user cannot see it, and the URL stays clean. Perfect.

{{% ad-panel-leaderboard %}}

## Summary

To implement Segmented Rendering:

1. Define your “segments” for a page.  
  Example: paid users versus free users, users from company A versus users from company B or C, etc.
2. Render as many static variations of a page you need, with one URL per segment.  
  Example: `/with-jokes/my-article`, `/bland/my-article`. Each variation matches a segment, for instance, paid or free users.
3. Setup a very small redirection server, that checks the HTTP request content and redirects the user to the right variation, depending on their segment.  
  Example: paid users are redirected to `/with-jokes/my-article`. We can tell if a user is paid or not by checking their request cookies.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a35f153b-b691-40a9-a0d3-0acd4dddd828/2-new-pattern-jamstack-segmented-rendering.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a35f153b-b691-40a9-a0d3-0acd4dddd828/2-new-pattern-jamstack-segmented-rendering.jpg" width="800" height="320" sizes="100vw" caption="Implementing Segmented Rendering. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a35f153b-b691-40a9-a0d3-0acd4dddd828/2-new-pattern-jamstack-segmented-rendering.jpg'>Large preview</a>)" alt="An illustration showing many requests entering the Jamstack that converts it all into only two segments." >}}

## What’s Next? Even More Performance!

Now you can have as many variations of the same page as you want. You solved your issue with paid users elegantly. Better, you implemented a new pattern, Segmented Rendering, that brings personalization to the Jamstack without sacrificing performances.

Final question: what happens if you have a lot of possible combinations? Like 5 parameters with 10 values each? You cannot render an infinite number of pages at build-time &mdash; that would take too long. And maybe you don’t actually have any paid users in France that picked the light theme and belong to bucket B for A/B testing. Some variations are not even worth rendering.

Hopefully, modern frontend frameworks got you covered. You can use an intermediate pattern such as [Incremental Static Regeneration from Next](https://nextjs.org/docs/basic-features/data-fetching/incremental-static-regeneration) or [Deferred Static Generation from Gatsby](https://www.gatsbyjs.com/docs/how-to/rendering-options/using-deferred-static-generation/), to render variations only on demand.

Website personalization is a hot topic, sadly adversarial to performance and energy consumption. Segmented Rendering resolves this conflict elegantly and lets you statically render any content, be it public or personalized for each user segment.

### More Resources on This Topic

- “[Let’s Bring The Jamstack To SaaS: Introducing Rainbow Rendering](https://blog.vulcanjs.org/lets-bring-the-jamstack-to-saas-introducing-rainbow-rendering-ad1834fe62ff),” Eric Burel  
  My first article describing the generic, theoretical architecture for Segmented Rendering (aka “Rainbow Rendering”)
- “[Treat Your Users Right With Http Cache And Segmented Rendering](https://blog.vulcanjs.org/treat-your-users-right-with-http-cache-and-segmented-rendering-7a4f4761b549),” Eric Burel  
  My second article showing an implementation with Next.js middlewares
- “[Render Anything Statically With Next.js And The Megaparam](https://blog.vulcanjs.org/render-anything-statically-with-next-js-and-the-megaparam-4039e66ffde),” Eric Burel  
  My third article, Segmented Rendering with just the HTTP cache (if you use Remix, you’ll love it
- “[Incremental Static Generation For Multiple Rendering Paths](https://github.com/vercel/next.js/discussions/17631),” Eric Burel  
  The GitHub ticket on Next.js that started it all.
- “[Theoretical Foundations For Server-side Rendering And Static-rendering](https://tinyurl.com/ssr-theory),” Eric Burel  
  My draft research paper that describes the mathematics behind SSR. It proves that Segmented Rendering achieves an optimal number of rendering in any situation. You cannot top that!
- “[High Performance Personalization With Next.js Middleware](https://www.plasmic.app/blog/nextjs-personalization),” Raymond Cheng  
  An excellent use case and demonstration with Plasmic.
- “[A/B Testing With Next.js Middleware](https://www.plasmic.app/blog/nextjs-ab-testing),” Raymond Cheng  
  Also from Plasmic, Segmented Rendering is being applied to A/B tests.
- “[Use Eleventy Edge To Deliver Dynamic Web Sites On The Edge](https://www.11ty.dev/blog/eleventy-edge/),” Eleventy Edge Blog  
  Eleventy Edge, a deep integration between 11ty and Netlify Edge Handlers to achieve personalization.
- “[Vercel/Platforms](https://github.com/vercel/platforms),” Steven Tey  
  Vercel Platforms, an example of segmented rendering for multi-tenancy.
- “[Avoid Waterfalls Of Queries In Remix Loaders](https://sergiodxa.com/articles/avoid-waterfalls-of-queries-in-remix-loaders),” Sergio Xalambrí  
  How to properly parallelize your data fetching requests (on the example of Remix).

### Further Reading on Smashing Magazine

- “[Jamstack Rendering Patterns: The Evolution](https://www.smashingmagazine.com/2022/04/jamstack-rendering-patterns-evolution/),” Ekene Eze
- “[State Management In Next.js](https://www.smashingmagazine.com/2021/08/state-management-nextjs/),” Átila Fassina
- “[Jamstack CMS: The Past, The Present and The Future](https://www.smashingmagazine.com/2021/08/history-future-jamstack-cms/),” Mike Neumegen
- “[A Complete Guide To Incremental Static Regeneration (ISR) With Next.js](https://www.smashingmagazine.com/2021/04/incremental-static-regeneration-nextjs/),” Lee Robinson

{{< signature "nl, il" >}}

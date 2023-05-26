---
title: 'Using SWR React Hooks With Next.js’ Incremental Static Regeneration (ISR)'
slug: useswr-react-hook-library-incremental-static-regeneration-nextjs
author: sam-poder
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47c6e5fc-73b3-41fe-afb7-b640b860efa0/useswr-react-hook-library-incremental-static-regeneration-nextjs.jpg
date: 2021-09-09T10:30:00.000Z
summary: >-
  When paired with ISR and Next.js’ API routes, SWR can be used to create a responsive user experience. In this article, Sam Poder explains what SWR is, where to use it (and where not), and how to build a website by using Incremental Static Regeneration.
description: >-
  When paired with ISR and Next.js’ API routes, SWR can be used to create a responsive user experience. In this article, Sam Poder explains what SWR is, where to use it (and where not), and how to build a website by using Incremental Static Regeneration.
categories:
  - Next.js
  - React
  - JavaScript
  - Tools
  - API
---

If you’ve ever used [Incremental Static Regeneration (ISR) with Next.js](https://www.smashingmagazine.com/2021/04/incremental-static-regeneration-nextjs/), you may have found yourself sending stale data to the client. This occurs when you are revalidating the page on the server. For some websites this works, but for others (such as [Hack Club’s Scrapbook](https://scrapbook.hackclub.com), a site built by [@lachlanjc](https://github.com/lachlanjc) that I help maintain), the user expects the data to be kept up to date. 

The first solution that comes to mind may be to simply server side render the pages, ensuring that the client is always sent the most up to date data. However, fetching large chunks of data before rendering can slow down the initial page load. The solution used in Scrapbook was to use the SWR library of React hooks to **update the cached page from the server with client side data fetching**. This approach ensures that users still have a good experience, that the site is fast and that the data is kept up to date.

## Meet SWR

[SWR](https://swr.vercel.app/) is a React Hooks library built by Vercel, the name comes from the term [stale-while-revalidate](https://tools.ietf.org/html/rfc5861). As the name suggests, your client will be served stale/old data whilst the most up to date data is being fetched (revalidating) through SWR on the client side. SWR does not just revalidate the data once, however, you can configure SWR to revalidate the data on an interval, when the tab regains focus, when a client reconnects to the Internet or programmatically.

When paired with ISR and Next.js’ API routes, SWR can be used to create a **responsive user experience**. The client is first served the cached statically generated page (generated with `getStaticProps()`), in the background the server also begins the process of revalidating that page (read more [here](https://www.smashingmagazine.com/2021/04/incremental-static-regeneration-nextjs/#fetching-data)). This process feels fast for the client and they can now see the set of data, however it may be a touch out of date. Once the page is loaded, a fetch request is made to an Next.js API route of your’s which returns the same data as what was generated with `getStaticProps()`. When this request is completed (assuming it was successful), SWR will update the page with this new data. 

Let’s now look back at Scrapbook and **how this helped solve the problem of having stale data on the page**. The obvious thing is that now, the client gets an updated version. The more interesting thing, however, is the impact on the speed of our side. When we measure speed through Lighthouse, we get a speed index of **1.5 seconds** for the ISR + SWR variant of the site and **5.8 seconds** for the Server Side Rendering variant (plus a warning regarding initial server response time). That’s a pretty stark contrast between the two (and it was noticeable when loading the pages up as well). But there is also a tradeoff, on the Server Side Rendered page the user didn’t have the layout of the site change after a couple of seconds with new data coming in. Whilst I believe Scrapbook handles this update well, it’s an important consideration when designing your user’s experience.

{{% feature-panel %}}

## Where To Use SWR (And Where Not To)

SWR can be put in place in a variety of places, here are a couple of site categories where SWR would make a great fit:

- **Sites with live data that require updating at a rapid pace.**  
Examples of such sites would be sports score sites and flight tracking. When building these sites, you’d look to use the revalidate on interval option with a low interval setting (one to five seconds). 
- **Sites with a feed style of updates or posts that update in realtime.**  
The classic example of this would be the news sites which have live blogs of events such as elections. Another example would be the aforementioned Scrapbook as well. In this case, you’d also likely want to use the revalidate on interval option but with a higher interval setting (thirty to sixty seconds) to save on data usage and prevent unnecessary API calls.
- **Sites with more passive data updates, that people keep open in the background a lot.**  
Examples of these sites would be weather pages or in the 2020s COVID-19 case number pages. These pages don’t update as frequently and therefore don’t need the constant revalidation of the previous two examples. However, it would still enhance the user experience for the data to update. In these cases, I would recommend revalidating the date when the tab regains focus and when a client reconnects to the internet, that’ll mean if a person anxiously returns to the tap hoping there has only been a small increase in COVID cases they’ll get that data quickly.
- **Sites with small pieces of data that users can interact with.**  
Think the Youtube Subscribe Button, when you click subscribe you want to see that count change and feel like you’ve made a difference. In these cases, you can revalidate the data programmatically using SWR to fetch the new count and update the displayed amount.

One thing to note, is that these can all be applied with or without ISR.

There are of course some places where you won’t want to use SWR or to use SWR without ISR. SWR isn’t much use if your data isn’t changing or changes very rarely and instead can clog up your network requests and use up mobile user’s data. SWR can work with pages requiring authentication, however you will want to use Server Side Rendering in these cases and not Incremental Static Regeneration.

{{% ad-panel-leaderboard %}}

## Using SWR With Next.js And Incremental Static Regeneration

Now we’ve explored the theory of this strategy, let’s explore how we put it into practise. For this we’re going to build a website that shows how many taxis are available in Singapore (where I live!) using [this API](https://data.gov.sg/dataset/taxi-availability) provided by the government.

### Project Structure

Our project will work by having three files:

- `lib/helpers.js`
- `pages/index.js` (our frontend file)
- `pages/api/index.js` (our API file)

Our helpers file will export a function (`getTaxiData`) that will fetch the data from the external API, and then return it in an appropriate format for our use. Our API file will import that function and will set it’s default export to a handler function that will call the `getTaxiData` function and then return it, this will mean sending a GET request to `/api` will return our data.

We’ll need this ability for SWR to do client-side data fetching. Lastly, in our frontend file we’ll import `getTaxiData` and use it in `getStaticProps`, it’s data will be passed to the default export function of our frontend file which will render our React page. We do this all to prevent code duplication and ensure consistency in our data. What a mouthful, let’s get started on the programming now.

### The Helpers File

We’ll begin by creating the `getTaxiData` function in `lib/helpers.js`:

<pre><code class="language-javascript">export async function getTaxiData(){
	let data = await fetch("https://api.data.gov.sg/v1/transport/taxi-availability").then(r =&gt; r.json())
	return {taxis: data.features.properties[0].taxi_count, updatedAt: data.features.properties[0].timestamp}
}</code></pre>

### The API File

We’ll then build the handler function in `api/index.js` as well as importing the `getTaxiData` function:

<pre><code class="language-javascript">import { getTaxiData } from '../../lib/helpers'
export default async function handler(req, res){
	res.status(200).json(await getTaxiData())
}</code></pre>

There isn’t anything here unique to SWR or ISR, besides the aforementioned project structure. That stuff starts now in `index.js`!

{{% ad-panel-leaderboard %}}

### The Front-End File

The first thing we want to do is create our `getStaticProps` function! This function will import our `getTaxiData` function, use it and then return the data with some additional configuration.

<pre><code class="language-javascript">export async function getStaticProps(){
	const { getTaxiData } = require("../lib/helpers")
	return { props: (await getTaxiData()), revalidate: 1 }
}</code></pre>

I’d like to focus on the revalidate key in our returned object. This key practically enables Incremental Static Regeneration. It tells your host that every one second regenerating the static page is an available option, that option is then triggered in the background when a client visits your page. You can read more about [Incremental Static Regeneration (ISR) here](https://www.smashingmagazine.com/2021/04/incremental-static-regeneration-nextjs/).

It’s now time to use SWR! Let’s import it first:

<pre><code class="language-javascript">import  useSWR from 'swr'</code></pre>

We’re going to be using SWR in our React-rendering function, so let’s create that function:

<pre><code class="language-javascript">export default function App(props){
}</code></pre>

We’re receiving the props from `getStaticProps`. Now we’re ready to set up SWR:

<pre><code class="language-javascript">const fetcher = (...args) => fetch(...args).then(res => res.json())
const { data } = useSWR("/api", fetcher, {fallbackData: props, refreshInterval: 30000})</code></pre>

Let’s break this down. Firstly, we define the fetcher. This is required by SWR as an argument so that it knows how to fetch your data given that different frameworks etc. can have different set ups. In this case, I’m using the function provided on the SWR docs page. Then we call the `useSWR` hook, with three arguments: the path to fetch data from, the fetcher function and then an options object.

In that `options` object, we’ve specified two things:

1. The fallback data;
2. The interval at which SWR should revalidate the data.

The fallback data option is where we provide the data fetched from `getStaticProps` which ensures that data is visible from the start. Lastly, we use object destructuring to extract the data from the hook.

To finish up, we’ll render that data with some very basic JSX:

<pre><code class="language-javascript">return &lt;div&gt;As of {data.updatedAt}, there are {data.taxis} taxis available in Singapore!&lt;/div&gt;</code></pre>

And, we’ve done it! There we have a very barebones example of using SWR with Incremental Static Regeneration. (The source of our example is available [here](https://github.com/sampoder/nextjs-isr-swr-example).)

If you ever run into stale data with ISR, you know who to call: SWR.

### Further Reading on SmashingMag

- [SWR React Hooks library](https://swr.vercel.app/)
- [An Introduction To SWR: React Hooks For Remote Data Fetching](https://www.smashingmagazine.com/2020/06/introduction-swr-react-hooks-remote-data-fetching/), Ibrahima Ndaw
- [ISR vs DPR: Big Words, Quick Explanation](https://www.smashingmagazine.com/2021/07/isr-dpr-explained/), Cassidy Williams
- [Global vs. Local Styling In Next.js](https://www.smashingmagazine.com/2021/07/global-local-styling-nextjs/), Alexander Dubovoj
- [Client-Side Routing In Next.js](https://www.smashingmagazine.com/2021/06/client-side-routing-next-js/), Adebiyi Adedotun Lukman

{{< signature "vf, yk, il" >}}

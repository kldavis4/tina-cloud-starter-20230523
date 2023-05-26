---
title: 'Next.js Wildcard Subdomains'
slug: nextjs-wildcard-subdomains
author: sam-poder
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b24747b-6f11-4588-a119-16eaf38bc933/nextjs-wildcard-subdomains.jpg
date: 2021-11-19T10:30:00.000Z
summary: >-
  Hosting with a wildcard subdomain enables your users to visit your site on any subdomain of your domain (<code>*.example.com</code>), and as you can imagine, we can use this to create unique user experiences which we’ll be exploring in this article through a Next.js lens.
description: >-
  Hosting with a wildcard subdomain enables your users to visit your site on any subdomain of your domain (<code>*.example.com</code>), and as you can imagine, we can use this to create unique user experiences which we’ll be exploring in this article through a Next.js lens.
categories:
  - Tools
  - Next.js
  - Jamstack
  - Static Generators
---

A “wildcard”? What in the world? Great question, these types of domain stem from *Wildcard DNS Records* which look like this:

<pre><code class="language-bash">*.example.               3600     TXT   "Wild! You have found a wildcard."
</code></pre>

When used, this DNS record will cause any subdomain that matches with the wildcard to hold a `TXT` value of: “Wild! You have found a wildcard.”

For example, if this was set on the domain `smashingmagazine.com`, `apples.example.smashingmagazine.com` and `oranges.example.smashingmagazine.com` would both return the above TXT value. The same principle can be applied to CNAME & A records as well.

## Wild Use Cases For Wildcards

Wildcards can be used for a wide range of things. For now, let’s focus on where they can be applied in combination with Next.js:

1. **Providing Hosted Services**  
The most common use of wildcard domains is to provide users of hosted services their own space with a unique subdomain. For example, if I was building a platform for restaurants to host digital ordering platforms with the domain `menus.abc`, I would be able to offer Dom’s Pizzeria `domspizzeria.menus.abc` and Magical Prata the domain `magicalprata.menus.abc`. The benefit of this is that it gives each of these establishments their enclosed space which they can customize and build out. This space can act as its own website &mdash; not tied to anything.
2. **Hosting Content And Personal Portfolios**  
Wildcards can also be used as a space for hosting content in portfolios, giving a sense of individuality to these portfolios, an example of this would be how Medium provides subdomains for the authors.
3. **Wilder More Creative Use Cases**  
You can’t define these use cases, but there are many creative use cases of these styles of domains. For example, later in this article, we’ll be developing a web toy that flips a webpage upside down making it readable for Australians. 

## The Caveats Of Wildcards With Next.js

*Sigh.* Unfortunately, using wildcards isn’t perfect there are a couple of drawbacks:

- **No More Static-Site Generation (and ISR)**  
Unfortunately, there aren’t any special systems to provide custom statically generated pages for different wildcard subdomains like you may with dynamic routing for example (where you have `[slug].js` files).
- **Difficulties with Development**  
When developing locally, it can be a pain to simulate wildcard domains and we’ll be touching on this a fair bit later on in this article but it is something important to keep in mind.
- **Limited Deployment Platforms**  
Vercel supports Wildcard Domains, however, other Jamstack oriented platforms do not all support wildcard domains. For example, Netlify limits the feature to a select group of users on the Pro plan.

## Building With Wildcards

With all this talk, let’s look at building with these domains. We’ll be focusing on three places where you can get the wildcard:

1. [Server Side In `getServerSideProps`](#server-side-in-getserversideprops),
2. [Client Side With `useEffect`](#client-side-with-useeffect),
3. [[Server Side On API Routes And Edge Functions](link)](#server-side-on-api-routes-and-edge-functions).

{{% feature-panel %}}

### Server Side In `getServerSideProps`

This is the most commonplace in which you will need to extract the wildcard, you can use this on pages where you need to render completely different content for different wildcards. As discussed above, this can not be done through static site generation so we must do it on server-side rendered pages.

The `getServerSideProps` is passed a context object, in this object you can access the HTTP request object using `context.req`. In this request object, you can access the hostname at `headers.host`, which will return a string such as `example.yourdomain.com`. We can split the string into an array across each period and then access the first item in said array. In code, that looks like this:

<pre><code class="language-javascript">export async function getServerSideProps(context) {
  let wildcard = context.req.headers.host.split(".")[0];
  wildcard =
    wildcard != "yourdomain"
      ? process.env.NODE_ENV != "development"
        ? wildcard
        : process.env.TEST_WILDCARD
      : "home";
  return { props: { wildcard } };
}</code></pre>

As you can see in this piece of code, we do an extra set processing on the wildcard if it’s the base domain we set the wildcard to `home` (if taking user input, this is a case you will need to handle) and if we are testing on localhost we can test out other wildcards. In our default export function, which renders our page we can use a switch statement to handle the wildcards:

<pre><code class="language-javascript">export default function App(props) {
  switch(props.wildcard) {
    case "home":
      return &lt;div&gt;Welcome to the home page!&lt;/div&gt;;
      break;
    default:
      return &lt;div&gt;The wild card is: {props.wildcard}.&lt;/div&gt;;
  }
}</code></pre>

### Client Side With `useEffect`

If you only want to make small modifications to each page on a different wildcard, you can avoid using server-side rendering by using the `useEffect` hook on the client-side. This approach will be rather similar to how we did it in `getServerSideProps`, except we will be relying on `window.location.hostname`. Using `window` means that the initial server render won’t be able to access the information, so we must wrap it within a `useEffect` hook that runs on the client-side. Here’s how that code looks like:

<pre><code class="language-javascript">// useEffect and useState must be imported from 'react'

const [wildcard, setWildcard] = useState("")
  useEffect(() =&gt; {
    setWildcard(window.location.hostname.split(".")[0])
  }, [])</code></pre>

This approach, however, is far from perfect as there is a delay between the page’s first render and the wildcard being available. Therefore, if you are making drastic changes based on the wildcard then the changes will be jarring for your user. This may also hurt your cumulative layout shift measure on your web vitals. With this in mind, I highly recommend limiting your use of this approach to adaptations that would be off-sight from the viewer on the initial load. An example would be a branded footer, on a technical documentation page. It is, of course, still handy to know.

### Server Side On API Routes And Edge Functions

API routes are another area where you may want to access a wildcard from. Fortunately, the same request object we discussed in the above section on `getServerSideProps` is also available when using a Node.js API route with Next.js. We can access it like this:

<pre><code class="language-javascript">export default (req, res) =&gt; {
  let wildcard = req.headers.host.split(".")[0];
  wildcard =
    wildcard != "yourdomain"
      ? process.env.NODE_ENV != "development"
        ? wildcard
        : process.env.TEST_WILDCARD
      : "home";
  res.json({ wildcard: wildcard })
}</code></pre>

Following this, we can then take certain actions such as fetching different data from your database depending on the wildcard and return that from the API.

This same logic can be applied to Next.js’ new Edge Functions / Middleware. This enables you to use wildcards in more than one route without duplicating code as well as speeding up the processing as code execution happens on the edge. Whilst the functionality is still in beta, it’s certainly something to keep an eye on.

<pre><code class="language-javascript">// _middleware.js
export function middleware(req) {
  let wildcard = req.headers.get("host").split(".")[0];
  console.log(wildcard);
  wildcard =
    wildcard != "yourdomain"
      ? process.env.NODE_ENV != "development"
        ? wildcard
        : process.env.TEST_WILDCARD
      : "home";
  console.log(process.env.TEST_WILDCARD);
  return new Response(JSON.stringify({ wildcard: wildcard }), {
    status: 200,
    headers: { "Content-Type": "application/json" },
  });
}</code></pre>

{{% ad-panel-leaderboard %}}

## The 🦘Aussie-izer

Now that we’ve explored the theory of this strategy, let’s explore how we put it into practice. In this section, we’ll be taking this approach to build a project that flips websites upside down (well, websites that are using a .com domain and aren’t subdomains) called the 🦘Aussie-izer.

To get started, we’re going to want to run `yarn init` and then `yarn add next react react-dom`, and finish up by adding these standard scripts to our `package.json`:

<pre><code class="language-json">"scripts": {
  "dev": "next dev",
  "build": "next build",
  "start": "next start",
  "lint": "next lint"
}</code></pre>

As soon as we’ve got a standard Next.js project set up, we’re going to want to create the only code file we’ll need for this project: `pages/index.js`.

First, we’ll want to add the `getServerSideProps` function in which we’ll extract the wildcard (as I’ll be hosting this at `aussieizer.sampoder.com`) that’s what I’ll be evaluating to `home` as:

<pre><code class="language-javascript">export async function getServerSideProps(context) {
  let wildcard = context.req.headers.host.split(".")[0];
  wildcard =
    wildcard != "aussieizer"
      ? wildcard != "localhost:3000"
        ? wildcard
        : process.env.TEST_WILDCARD
      : "home";
  return { props: { wildcard } };
}</code></pre>

We’ll then be using that wildcard, to render an iFrame to fill that page (by flipping iFrame over to create the effect), with our `src` being set to <code>{\`https://${props.wildcard}.com\`}</code>. We’ll use a switch case, as we discussed above, to render a small helper page if they visit the home page:

<div class="break-out">

<pre><code class="language-javascript">export default function App(props) {
  switch (props.wildcard) {
    case "home":
      return (
        &lt;div&gt;
          Welcome to the Aussie-izer! This only works for .com domains. If you
          want to Aussie-ize{" "}
          &lt;a href="https://example.com"&gt;https://example.com&lt;/a&gt; visit{" "}
          &lt;a href="https://example.aussieizer.sampoder.com"&gt;
            https://example.aussieizer.sampoder.com
          &lt;/a&gt;.
        &lt;/div&gt;
      );
      break;
    default:
      return (
        &lt;iframe
          src={`https://${props.wildcard}.com`}
          style={{
            transform: "rotate(180deg)",
            border: "none",
            height: "100vh",
            width: "100%",
            overflow: "hidden",
          }}
          frameBorder="0"
          scrolling="yes"
          seamless="seamless"
          height="100%"
          width="100%"
        &gt;&lt;/iframe&gt;
      );
  }
}</code></pre>
</div>

And we’re ready to go! The live version is available at [https://aussieizer.sampoder.com](https://aussieizer.sampoder.com) and the source code can be found at [https://github.com/sampoder/aussie-izer/](https://github.com/sampoder/aussie-izer/). 

{{% ad-panel-leaderboard %}}

## Hosting/Deployment

If you’re hosting on a custom server, wildcard domains will be a breeze to set up through DNS. However, a great part about using Jamstack is being able to host on services such as Vercel or Netlify; these services have their own domain management systems.

### Vercel

Vercel supports wildcard domains out of the box &mdash; for all accounts. To use them, first visit the `Domains` section of your deployment’s `Settings` tab. Next, you’ll want to enter your domain by using a `*` to signify the wildcard.

For the above example, I entered:

<pre><code class="language-bash">*.aussieizer.sampoder.com</code></pre>

You most likely will also want to add your root domain (`aussieizer.sampoder.com`, in my case) to be able to provide a homepage or some instructions, however, that could also be a separate codebase.

### Netlify

Netlify limits their wildcards feature to Pro accounts; if you have a Pro account, you will need to email their support staff for them to then enable the option on your account. It will show up in the domain settings page once enabled.

### Render

Render also offers wildcard domains to all users. Simply enter a domain with a `*` (signifying your wildcard) in the `Add Custom Domain` input on the custom domains section of your site’s settings page which will enable the wildcard. Please note that Render will require you to add additional records to your DNS so that they can issue a `LetsEncrypt` SSL certificate (exact instructions will be shown to you when you input your wildcard domain).

## That’s It!

Wildcard domains often go under the radar &mdash; I hope you enjoyed exploring them with me. Thank you!

*Also: FYI Australians do not actually see upside down.*

### Further Reading On Smashing Magazine

- “[The Evolution Of Jamstack](https://www.smashingmagazine.com/2021/05/evolution-jamstack/),” Mathias Biilmann
- “[Global vs. Local Styling In Next.js](https://www.smashingmagazine.com/2021/07/global-local-styling-nextjs/),” Alexander Dubovoy
- “[Breaking Down Bulky Builds With Netlify And Next.js](https://www.smashingmagazine.com/2021/06/breaking-down-bulky-builds-netlify-nextjs/),” Atila Fassina
- “[What Is Next.js?](https://www.smashingmagazine.com/2020/08/smashing-podcast-episode-23/),” Smashing Podcast episode with Guillermo Rauch
- “[How Does Netlify Dogfood The Jamstack?](https://www.smashingmagazine.com/2020/11/smashing-podcast-episode-29/),” Smashing Podcast episode with Leslie Cohn-Wein

{{< signature "vf, yk, il" >}}

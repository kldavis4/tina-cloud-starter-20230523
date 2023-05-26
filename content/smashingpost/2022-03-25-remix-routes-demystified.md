---
title: 'Remix Routes Demystified'
slug: remix-routes-demystified
author: atila-fassina
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1a0f7a2-9511-4911-9e94-5a4368b69c07/remix-routes-demystified.jpg
date: 2022-03-25T14:00:00.000Z
summary: >-
  In the past months, there have been lots of talks dedictaed to Remix. Routing is not only one of the things that sets it apart from other frameworks, but it also fuels great performance and improves the overall experience for developers. Let’s dig in to all  of the features that build up routing in this powerful framework.
description: >-
  In the past months, there have been lots of talks dedictaed to Remix. Routing is not only one of the things that sets it apart from other frameworks, but it also fuels great performance and improves the overall experience for developers. Let’s dig in to all  of the features that build up routing in this powerful framework.
categories:
  - Apps
  - Tools
  - React
  - Frameworks
---

Around six months ago, Remix became open source. It brings a lovely developer experience and approximates web development to the web platform in a refreshing way. It’s a known tale that naming is the hardest thing in programming, but the team nailed this one. Remix drinks from the community experience, puts the platform and browser behavior in a front seat; sprinkles the learning the authors got from [React-Router](https://reactrouter.com/), [Unpkg](https://unpkg.com/), and from teaching React. Like a remixed record, its content mixes the old needs to novel solutions in order to deliver a flawless experience.

Writing a Remix app is fun, it gets developers scratching their heads about, “How did Forms actually work before?”, "Can Cache really do that?”, and (my personal favorite), “The docs just pointed me to [Mozilla Dev Network](https://mdn.io)!”

In this article, we will dig deeper and look beyond the hype, though. Let’s pick inside (one of) Remix’s secret sauces and see one of the features that powers most of its features and fuels many of its [conventions](https://remix.run/docs/en/v1/api/conventions#file-name-conventions): routes. Buckle up!

## Anatomy Of A Remix Repository

If pasting `npx create-remix@latest`, following the prompt, and opening the scanning the bare bones project file-tree, a developer will be faced with a structure similar to the one bellow:

<pre><code class="language-bash">├───/.cache
├───/public
├───/app
│   ├───/routes
│   ├───entry.client.jsx
│   ├───entry.server.jsx
│   └───root.tsx
├───remix.config.js
└───package.json</code></pre>

- `.cache` will show up, once there’s a build output;
- `public` is for static assets;
- `app` is where the fun will happen, think of it as a `/src` for now;
- the files on the root are the configuration ones, for Remix, and for NPM.

Remix can be deployed to any JavaScript environment (even without Node.js). Depending on which platform you choose, the starter may output more files to make sure it all works as intended. 

We have all seen similar repositories on other apps. But things already don’t feel the same with those `entry.server.jsx` and `entry.client.jsx`: every route has a client and a server runtime. Remix embraces the server-side from the very beginning, making it a truly isomorphic app.

While `entry.client.jsx` is pretty much a regular DOM renderer with Remix built-in sauce, `entry.server.jsx` already shows a powerful strategy of Remix routing. It is possible and clear to determine an app-wide configuration for headers, response, and metadata straight from there. The foundation for a multi-page app is set from the very beginning.

## Routes Directory

Out of the 3 folders inside `/app` on the snippet above, **routes** is definitely the most important. Remix brings a few conventions (one can opt-out with some configuration tweaks) that power the Developer Experience within the framework. The first convention, which has somewhat raised to a standard among such frameworks, is **File System based routing**. Within the `/routes` directory, a regular file will create a new route from the root of your app. If one wants `myapp.com` and `myapp.com/about`, for example, the following structure can achieve it:

<pre><code class="language-bash">├───/apps
│   ├───/routes
│   │   ├───index.jsx
│   │   └───about.jsx</code></pre>

Inside those files, there are regular React components as the **default export**, while special Remix methods can be **named exports** to provide additional functionalities like data-fetching with the `loader` and `action` methods or route configuration like the `headers` and `meta` methods.

And here is where things start to get interesting: Remix doesn’t separate your data by runtime. There’s no “server data”, or “build-time data”. It has a [loader](https://remix.run/docs/en/v1/api/conventions#loader) for *loading* data, it has an [action](https://remix.run/docs/en/v1/api/conventions#action) for mutations, [headers](https://remix.run/docs/en/v1/api/conventions#headers) and [meta](https://remix.run/docs/en/v1/api/conventions#meta) for extending/overriding response headers and metatags on a per-route basis.

{{% feature-panel %}}

## Route Matching And Layouts

Composability is an order of business within the React ecosystem. A componentized program excels when we allow it to wrap one component on another, decorating them and empowering them with each other. With that in mind, the **Layout Pattern** has surfaced, it consists of creating a component to wrap a route (a.k.a another component) and decorate it in order to enforce UI consistency or make important data available.

Remix puts the **Layout Pattern** front and center it’s possible to determine a Layout to render all routes which match its name.

<pre><code class="language-bash">├───/apps
│   ├───/routes
│   │   ├───/posts    // actual posts inside
│   │   └───posts.jsx // this is the layout</code></pre>

The `posts.jsx` component uses a built-in Remix component (`<Outlet />`) which will work in a similar way that React developers are used to have `{children}` for. This component will use the content within a `/posts/my-post.jsx` and render it within the layout. For example:

<pre><code class="language-javascript">import { Outlet } from 'remix'

export default PostsLayout = () =&gt; (
  &lt;main&gt;
     &lt;Navigation /&gt;
     &lt;article&gt;
       &lt;Outlet /&gt;
     &lt;/article&gt;
     &lt;Footer /&gt;
  &lt;/main&gt;
)</code></pre>

But not always the UI will walk in sync with the URL structure. There is a chance that developers will need to create layouts without nesting routes. Take for example the `/about` page and the `/`, they are often completely different, and this convention ties down the URL structure with UI look and feel. Unless there is an escape hatch.

### Skipping Inheritance

When nesting route components like above, they become child components of another component with the same name as their directory, like `posts.jsx` is the parent component to everything inside `/posts` through `<Outlet />`. But eventually, it may be necessary to skip such inheritance while still having the URL segment. For example:

<pre><code class="language-bash">├───/apps
│   ├───/routes
│   │   ├───/posts                       // post
│   │   ├───posts.different-layout.jsx   // post
│   │   └───posts.jsx                    // posts layout</code></pre>

In the example above, `posts.different-layout.tsx` will be served in `/posts/different-layout`, but it won’t be a child component of `posts.jsx` layout.

{{% ad-panel-leaderboard %}}

## Dynamic Routes

Creating routes for a complex multi-page app is almost impossible without some Dynamic Routing shenanigans. Of course, Remix has its covered. It is possible to declare the parameters by prefixing them with a `$` in the file name, for example:

<pre><code class="language-javascript">├───/apps
│   ├───/routes
│   |   └───/users
│   │         └───$userId.jsx</code></pre>

Now, your page component for `$userId.jsx` can look something like:

<pre><code class="language-javascript">import { useParams } from 'remix'

export default function PostRoute() {
  const { userId } = useParams()

  return (
    &lt;ul&gt;
      &lt;li&gt;user: {userId}&lt;/li&gt;
    &lt;/ul&gt;
  )
}</code></pre>

Also there’s an additional twist: we can combine this with the **Dot Limiters** mentioned a few sections prior, and we can easily have:

<pre><code class="language-javascript">├───/apps
│   ├───/routes
│   |   └───/users
│   |         ├───$userId.edit.jsx
│   │         └───$userId.jsx</code></pre>

Now the following path segment will not only be matched, but also carry out the parameter: `/users/{{user-id}}/edit`. Needless to say, the same structure can be combined to also carry additional parameters, for example: `$appRegion.$userId.jsx` will carry out the 2 parameters to your functions and page component: `const { appRegion, userId } = useParams()`.

### Catch-all With Splats

Eventually, developers may find themselves in situations where the number of parameters, or keys for each, a route is receiving is unclear. For these edge-cases Remix offers a way of catching everything. [Splats](https://remix.run/docs/en/v1/api/conventions#splat-routes) will match everything which was not matched before by any of its siblings. For example, take this route structure:

<pre><code class="language-javascript">├───/apps
│   ├───/routes
│   │   ├───about.jsx
│   │   ├───index.jsx
│   │   └───$.jsx      // Splat Route</code></pre>

- `mydomain.com/about` will render `about.jsx`;
- `mydomain.com` will render `index.jsx`;
- anything that’s not the root nor `/about` will render `$.jsx`.

And Remix will pass a `params` object to both of its data handling methods (`loader` and `action`), and it has a `useParams` hook (exactly the same from React-Router) to use such parameters straight on the client-side. So, our `$.jsx` could look something like:

<pre><code class="language-javascript">import { useParams } from 'remix'
import type { LoaderFunction, ActionFunction } from 'remix'

export const loader: LoaderFunction = async ({
  params
}) =&gt; {
  return (params['&#42;'] || '').split('/')
};

export const action: ActionFunction = async ({
  params
}) =&gt; {
  return (params['&#42;'] || '').split('/')
};

export default function SplatRoute() {
  const params = useParams()
  console.log(return (params['&#42;'] || '').split('/'))

  return (&lt;div&gt;Wow. Much dynamic!&lt;/div&gt;)
}</code></pre>

Check the **Load data** and the **Mutating data** sections for an in-depth explanation of `loader` and `action` methods respectively.

The `params['']` will be a `string` with the all params. For example: `mydomain.com/this/is/my/route` will yield “this/is/my/route”. So, in this case we can just use `.split('/')` to turn into an array like `['this', 'is', 'my', 'route']`.

{{% ad-panel-leaderboard %}}

## Load Data

Each route is able to specify a method that will provide and handle its data on the server right before rendering. This method is the [`loader`](https://remix.run/docs/en/v1/api/conventions#loader) function, it must return a serializable piece of data which can then be accessed on the main component via the special [`useLoaderData`](https://remix.run/docs/en/v1/api/remix#useloaderdata) hook from Remix.

<pre><code class="language-javascript">import type { LoaderFunction } from 'remix'
import type { ProjectProps } from '~/types'
import { useLoaderData } from 'remix'

export const loader: LoaderFunction = async () =&gt; {
  const repositoriesResp = await fetch(
    'https://api.github.com/users/atilafassina/repos'
  )
  return repositoriesResp.json()
}

export default function Projects() {
  const repositoryList: ProjectProps[] = useLoaderData()

  return (&lt;div&gt;{repositoryList.length}&lt;/div&gt;
}</code></pre>

It’s important to point out, that the loader will **always** run on the server. Every logic there will not arrive in the client-side bundle, which means that any dependency used only there will not be sent to the user either. The loader function can run in 2 different scenarios:

1. **Hard navigation:**  
When the user navigates via the browser window (arrives directly to that page).
3. **Client-side navigation:**  
When the user was in another page in your Remix app and navigates via a `<Link />` component to this route.

When hard navigation happens, the loader method runs, provides the renderer with data, and the route is Server-Side Rendered to finally be sent to the user. On the client-side navigation, Remix fires a `fetch` request by itself and uses the loader function as an API endpoint to fuel fresh data to this route.

## Mutating Data

Remix carries multiple ways of firing a data mutation from the client-side: HTML `form` tag, and extremely configurable [`<Form />`](https://remix.run/docs/en/v1/api/remix#form) component, and the [`useFetcher`](https://remix.run/docs/en/v1/api/remix#usefetcher) and [`useFetchers`](https://remix.run/docs/en/v1/api/remix#usefetchers) hooks. Each of them has its own intended use-cases, and they are there to power the whole concept of an [Optimistic UI](https://remix.run/docs/en/v1.2.3/guides/optimistic-ui) that made Remix famous. We will park those concepts for now and address them in a future article because all these methods unfailingly communicate with a single server-side method: the **action** function.

`Action` and `Loader` are fundamentally the same method, the only thing which differentiates them is the trigger. `Actions` will be triggered on any non-GET request and will run **before** the `loader` is called by the re-rendering of the route. So, post a user interaction, the following cascade will happen on Remix’s side:

1. Client-side triggers `Action` function,
2. `Action` function connects to the data source (database, API, …),
3. Re-render is triggered, calls Loader function,
4. `Loader` function fetches data and feeds Remix rendering,
5. Response is sent back to the client.

## Headers And Meta

As previously mentioned, there are other specific methods for each route that aren’t necessarily involved with fetching and handling data. They are responsible for your document **headers** and **metatags**. 

Exporting `meta` function allows the developer to override the metatag values defined in the `root.jsx` and tailor it to that specific route. If a value isn’t changed, it will seamlessly inherit. The same logic will apply to the `headers` function, but with a twist.

Data usually is what determines how long a page can be cached, so, naturally, the document inherits the headers from its data. If `headers` function doesn’t explicitly declare otherwise, the `loader` function headers will dictate the headers of your whole document, not only data. And once declared, the `headers` function will receive both: the parent headers **and** the loader headers as parameters.

<div class="break-out">

<pre><code class="language-javascript">import type { HeadersFunction } from 'remix'

export const headers: HeadersFunction = ({ loaderHeaders, parentHeaders }) =&gt; ({
  ...parentHeaders,
  ...loaderHeaders,
  "x-magazine": "smashing",
  "Cache-Control": "max-age: 60, stale-while-revalidate=3600",
})</code></pre>
</div>

## Resource Routes

These routes are essentially one which doesn’t exist naturally in the website’s navigation pattern. Usually, a [resource route](https://remix.run/docs/en/v1/guides/resource-routes) does not return a React component. Besides this, they behave exactly the same as others: for `GET` requests, the `loader` function will run, for any other request method, the `action` function will return the response.

Resource routes can be used in a number of use cases when you need to return a different file type: a `pdf` or `csv` document, a sitemap, or other. For example, here we are creating a PDF file and returning it as a resource to the user.

<pre><code class="language-javascript">export const loader: LoaderFunction = async () =&gt; {
  const pdf = somethingToPdf()

  return new Response(pdf, {
    headers: {
      'Content-Disposition': 'attachment;',
      'Content-Type': 'application/pdf',
    },
  })
}

</code></pre>

Remix makes it straightforward to adjust the response headers, so we can even use `Content-Disposition` to instruct the browser that this specific resource should be saved to the file system instead of displaying inline to the browser.

## Remix Secret Sauce: Nested Routes

Here is where a multi-page app meets single-page apps. Since Remix’s routing is powered by React-Router, it brings its [partial routing](https://remix.run/docs/en/v1/guides/routing#what-are-nested-routes) capabilities to the architecture. Each route is responsible for its own piece of logic and presentation, and this all can be declared used by the File-System heuristics again. Check this:

<pre><code class="language-javascript">├───/apps
│   ├───/routes
│   │   ├───/dashboard
│   │   |    ├───profile.jsx
│   │   |    ├───settings.jsx
│   │   |    └───posts.jsx
│   │   └───dashboard.jsx      // Parent route</code></pre>

And just like we did implicitly on our Layout paradigm before, and how Remix handles the `root`/`/routes` relationship, we will determine a parent route which will render all its **children** routes inside the `<Outlet />` component. So, our `dashboard.jsx` looks something like this:

<pre><code class="language-javascript">import { Outlet } from 'remix'

export default function Dashboard () {
  return (
   &lt;div&gt;
     some content that will show at every route
     &lt;Outlet /&gt;
   &lt;/div&gt;
  )
}</code></pre>

This way, Remix can infer which resources to pre-fetch before the user asks for the page. because it allows the framework to identify relationships between each route and more intelligently infer what will be needed. Fetching all of your page's data dependencies in parallel drastically boosts the performance of your app by eliminating those render and fetch waterfalls we dread so much seeing in (too) many web apps today.

So, thanks to [Nested Routes](https://remix.run/docs/en/v1/guides/routing#what-are-nested-routes), Remix is able to preload data for each URL segment, it knows what the app needs before it renders. On top of that, the only things that actually need re-rendering are the components inside the specific URL segment. 

For example, take our above app , once users navigate to `/dashboard/activity` and then to `/dashboard/friends` the components it will render and data it will fetch are only the ones inside `/friends` route. The components and resources matching the `/dashboard` segment are already there. 

So now Remix is preventing the browser from re-rendering the entire UI and only doing it for the sections that actually changed. It can also prefetch resources for the next page so once actual navigation occurs the transition is instant because data will be waiting at the browser cache. Remix is able to optimize it all out of the box with fine-grained precision, thanks to [Nested Routes](https://remix.run/docs/en/v1/guides/routing#what-are-nested-routes) and powered by partial routing.

## Wrapping Up

Routing is arguably the most important structure of a web app because it dictates the foundation where every component will relate to each other, and how the whole app will be able to scale going forward. Looking closely through Remix’s decisions for handling routes was a fun and refreshing ride, and this is only the scratch on the surface of what this framework has under its hood. If you want to dig deeper into more resources, be sure to check this amazing interactive guide for [Remix routes](http://remix-routing-demo.netlify.app) by [Dilum Sanjaya](https://twitter.com/DilumSanjaya).

Though an extremely powerful feature and a backbone of Remix, we have just scratched the surface with routes and these examples. Remix shows its true potential on highly interactive apps, and it’s a very powerful set of features: data mutation with forms and special hooks, authentication and cookie management, and more.

{{< signature "vf, yk, il" >}}

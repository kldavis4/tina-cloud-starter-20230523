---
title: 'Getting Started With Next.js'
slug: getting-started-with-next-js
author: adebiyi-adedotun
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/623fafd4-ac94-481c-8835-ea175e5f6be0/getting-started-with-next-js.png
date: 2020-10-22T11:00:00.000Z
summary: >-
  Next.js is a React framework that is bound to ease your life as a React developer by abstracting away the common and redundant tasks (such as routing) into relatively simpler and powerful APIs. That way, you can focus on writing your apps instead of reinventing the wheel.
description: >-
  Next.js is a React framework that is bound to ease your life as a React developer by abstracting away the common and redundant tasks (such as routing) into relatively simpler and powerful APIs. That way, you can focus on writing your apps instead of reinventing the wheel.
categories:
  - React
  - JavaScript
  - Frameworks
  - Next.js
---

Lately, Next.js has termed itself [*The React Framework for Production*](https://nextjs.org/), and with such bold claim comes a bevy of features that it offers to help you take your React websites from zero to production. These features would matter less if Next.js isn’t relatively easy to learn, and while the numerous features might mean more things and nuances to learn, its attempt at simplicity, power, and *perhaps* success at it is definitely something to have in your arsenal.

As you settle in to learn about Next.js, there are some things you might already be familiar with and you might even be surprised at how it gives you a lot to work with that it might seem almost overwhelming at face value. [Next.js is lit for static sites](https://jaredpalmer.com/gatsby-vs-nextjs#nextjs-is-lit-for-static-sites) and it has been well-engineered for that purpose. But it also takes it further with its [Incremental Static Regeneration](https://nextjs.org/docs/basic-features/data-fetching#incremental-static-regeneration) that combines well with existing features to make development a soothing experience. But wait, you might ask. Why Next.js?

This tutorial will be beneficial to developers who are looking to get started with Next.js or have already begun but need to fill some knowledge gaps. You do not need to be a pro in React, however, having a working experience with React will come in handy.

## But Why Next.js?

1. **Relatively easy to learn.**  
That’s it. If you’ve written any React at all, you’d find yourself at home with Next.js. It offers you advanced tools and a robust API support, but it doesn’t force you to use them.
2. **Built-in CSS support.**  
Writing CSS in component-driven frameworks comes with a sacrosanct need for the “cascade”. It’s why you have [CSS-in-JS](https://cssinjs.org) tools, but Next.js comes out of the box with its own offering &mdash; [styled-jsx](https://github.com/vercel/styled-jsx), and also supports a bevy of styling methodologies.
3. **Automatic TypeScript support.**  
If you like to code in TypeScript, with Next.js, you literally have automatic support for TypeScript configuration and compilation.
4. **Multiple data fetching technique.**  
It supports SSG and/or SSR. You can choose to use one or the other, or both.
5. **File-system routing.**  
To navigate between one page to another is supported through the file-system of your app. You do not need any special library to handle routing.

There are many more other features, e.g. using experimental ES features like [optional-chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining), not [importing react](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html) everywhere you use JSX, support for APIs like [`next/head`](https://nextjs.org/docs/api-reference/next/head) that helps manage the [head](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head) of your HTML document, and so on. Suffice to say the deeper you go, the more you enjoy, appreciate, and discover many other features. 

{{% feature-panel %}}

## Requirements For Creating A Next.js App

Creating a Next.js app requires [Node.js](https://nodejs.org), and `npm` (or `npx`) installed.

To check if you have Node.js installed, run the command in your terminal:

<pre><code class="language-bash"># It should respond with a version number
node -v
</code></pre>

Ideally, npm (and npx) comes with your Node.js installation. To confirm that you have them installed, run the commands in your terminal:

<pre><code class="language-bash"># Run this. It should respond with a version number
npm -v

# Then run this. It should also respond with a version number
npx -v
</code></pre>

In case any of the commands above fails to respond with a version number, you might want to look into [installing Node.js and npm](https://www.npmjs.com/get-npm).

If you prefer the [yarn package manager](https://www.npmjs.com/package/yarn) instead, you can run install it with the command:

<pre><code class="language-bash"># Installs yarn globally
npm i -g yarn
</code></pre>

Then confirm the installation with:

<pre><code class="language-bash"># It should also respond with a version number
yarn -v
</code></pre>

## Creating A Next.js App

Getting the requirements above out of the way, creating a Next.js can be done in two ways, the first being the simplest:

1. With [create-next-app](https://nextjs.org/docs/api-reference/create-next-app), or
2. [Manually](https://nextjs.org/docs/getting-started#manual-setup)

### Creating A Next.js App With `create-next-app`

Using [create-next-app](https://nextjs.org/docs/api-reference/create-next-app) is simple and straightforward, plus you can also get going with a starter like [Next.js with Redux](https://github.com/vercel/next.js/tree/canary/examples/with-redux), [Next.js with Tailwind CSS](https://github.com/vercel/next.js/tree/canary/examples/with-tailwindcss), or [Next.js with Sanity CMS](https://github.com/vercel/next.js/tree/canary/examples/cms-sanity) etc. You can view the full list of starters in the [Next.js examples repo](https://github.com/vercel/next.js/tree/canary/examples).

<pre><code class="language-javascript"># Create a new Next.js app with npx
npx create-next-app &lt;app-name&gt;

# Create a new Next.js app with npm
npm create-next-app &lt;app-name&gt;

# With yarn
yarn create next-app &lt;app-name&gt;
</code></pre>

> If you’re wondering what the difference between npm and npx is, there’s an in-depth article on the npm blog, [Introducing npx: an npm package runner](https://blog.npmjs.org/post/162869356040/introducing-npx-an-npm-package-runner).

### Creating A Next.js Project Manually

This requires three packages: `next`, `react`, and `react-dom`.

<pre><code class="language-javascript"># With npm
npm install next react react-dom

# With yarn
yarn add next react react-dom
</code></pre>

Then add the following [scripts](https://docs.npmjs.com/misc/scripts) to `package.json`.

<pre><code class="language-javascript">"scripts": {
  "dev": "next dev",
  "start": "next start",
  "build": "next build"
}
</code></pre>

- `dev` starts Next.js in [development mode](https://nextjs.org/docs/api-reference/cli#development).
- `start` starts Next.js in [production mode](https://nextjs.org/docs/api-reference/cli#production).
- `build` builds your Next.js app for [production](https://nextjs.org/docs/api-reference/cli#build).

{{% ad-panel-leaderboard %}}

## Folder Structure

One salient thing you might notice after creating a Next.js app is the lean folder structure. You get the bare minimum to run a Next.js app. No more, no less. What you end up with as your app grows is up to you more than it is to the framework.

The only Next.js specific folders are the `pages`, `public`, and `styles` folder.

<pre><code class="language-javascript"># other files and folders, .gitignore, package.json...
- pages
  - api
    - hello.js
  - _app.js
  - index.js
- public
  - favicon.ico
  - vercel.svg
- styles
  - globals.css
  - Home.module.css</code></pre>

## Pages

In a Next.js app, **pages** is one of the Next-specific folders you get. Here are some things you need to know about `pages`:

- **Pages are React components**  
Each file in it is a **page** and each **page** is a React component.

<pre><code class="language-javascript">
// Location: /pages/homepage.js
// &lt;HomePage/&gt; is just a basic React component
export default HomePage() {
  return &lt;h1&gt;Welcome to Next.js&lt;/h1&gt;
}</code></pre>
  
- **Custom pages**  
These are special pages prefixed with the underscore, like *`_app.js`*.
  - `_app.js`: This is a custom component that resides in the pages folder. Next.js uses this component to initialize pages.
  - `_document.js`: Like `_app.js`, `_document.js` is a custom component that Next.js uses to augment your applications `<html>` and `<body>` tags. This is necessary because Next.js pages skip the definition of the surrounding document’s markup.

- **File-based routing system based on pages**  
Next.js has a file-based routing system where each page automatically becomes a route based on its file name. For example, a page at `pages/profile` will be located at `/profile`, and `pages/index.js` at `/`.

<pre><code class="language-javascript"># Other folders
- pages
  - index.js # located at /
  - profile.js # located at /profile
  - dashboard
    - index.js # located at /dashboard
    - payments.js # located at /dashboard/payments
</code></pre>

## Routing

Next.js has a file-based routing system based on `pages`. Every page created automatically becomes a route. For example, `pages/books.js` will become route `/book`.

<pre><code class="language-javascript">- pages
  - index.js # url: /
  - books.js # url: /books
  - profile.js # url: /profile</code></pre>

Routing has led to libraries like [React Router](https://reactrouter.com/) and can be daunting and quite complex because of the sheer number of ways you might see fit to route section of your pages in your Next.js app. Speaking about routing in Next.js is fairly straightforward, for the most part of it, the file-based routing system can be used to define the most common routing patterns.

### Index Routes

The `pages` folder automatically has a page `index.js` which is automatically routed to the starting point of your application as `/`. But you can have different `index.js`s across your pages, but one in each folder. You don’t have to do this but it helps to define the starting point of your routes, and avoid some redundancy in naming. Take this folder structure for example:

<pre><code class="language-javascript">- pages
  - index.js
  - users
    - index.js
    - [user].js</code></pre>

There are two index routes at `/` and `/users`. It is possible to name the index route in the `users` folder `users.js` and have it routed to `/users/users` if that’s readable and convenient for you. Otherwise, you can use the index route to mitigate the redundancy.

### Nested Routes

How do you structure your folder to have a route like `/dashboard/user/:id`.

You need nested folders:

<pre><code class="language-javascript">- pages
  - index.js
  - dashboard
    - index.js
    - user
      - [id].js # dynamic id for each user</code></pre>

You can nest and go deeper as much as you like.

### Dynamic Route Segments

The segments of a URL are not always indeterminate. Sometimes you just can’t tell what will be there at development. This is where dynamic route segments come in. In the last example, `:id` is the dynamic segment in the URL `/dashboard/user/:id`. The `id` determines the user that will be on the page currently. If you can think about it, most likely you can create it with the file-system.

The dynamic part can appear anywhere in the nested routes:

<pre><code class="language-javascript">- pages
  - dashboard
    - user
      - [id].js
          - profile</code></pre>

will give the route `/dashboard/user/:id/profile` which leads to a **profile** page of a **user** with a particular **id.**

Imagine trying to access a route `/news/:category/:category-type/:league/:team` where `category`, `category-type`, `league`, and `team` are dynamic segments. Each segment will be a file, and files can’t be nested. This is where you’d need a [catch-all routes](https://nextjs.org/docs/routing/dynamic-routes#catch-all-routes) where you spread the dynamic parts like:

<pre><code class="language-javascript">- pages
  - news
    - [...id].js</code></pre>
   
Then you can access the route like `/news/sport/football/epl/liverpool`.

You might be wondering how to get the dynamic segments in your components. The `useRouter` hook, exported from [`next/router`](https://nextjs.org/docs/api-reference/next/router#userouter) is reserved for that purpose and others. It exposes the `router` object.

<pre><code class="language-javascript">import { useRouter } from 'next/router';

export default function Post() {
  // useRouter returns the router object
  const router = useRouter();

  console.log({ router });
  return &lt;div&gt; News &lt;/div&gt;;
}</code></pre>

The dynamic segments are in the `query` property of the [`router`](https://nextjs.org/docs/api-reference/next/router#router-object) object, accessed with `router.query`. If there are no queries, the query property returns an empty object.

## Linking Between Pages

Navigating between pages in your apps can be done with the [**Link**](https://nextjs.org/docs/api-reference/next/link) component exported by [`next/link`](https://nextjs.org/docs/api-reference/next/link). Say you have the pages:

<pre><code class="language-javascript">- pages
  - index.js
  - profile.js
  - settings.js
  - users
    - index.js
    - [user].js
</code></pre>

You can `Link` them like:

<pre><code class="language-javascript">import Link from "next/link";

export default function Users({users) {
  return (
    &lt;div&gt;
      &lt;Link href="/">Home&lt;/Link&gt;
      &lt;Link href="/profile"&gt;Profile&lt;/Link&gt;
      &lt;Link href="/settings"&gt;
        &lt;a&gt; Settings &lt;/a&gt;
      &lt;/Link&gt;
      &lt;Link href="/users"&gt;
        &lt;a&gt; Settings &lt;/a&gt;
      &lt;/Link&gt;
      &lt;Link href="/users/bob"&gt;
        &lt;a&gt; Settings &lt;/a&gt;
      &lt;/Link&gt;
    &lt;/div&gt;
  )
}</code></pre>

The **Link** component has a number of acceptable props, **href** &mdash; the URL of the hyperlink &mdash; been the only required one. It’s equivalent to the [`href`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#href) [attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#href) of the HTML [anchor (`<a>`) element.](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a)

Other props include:

<table class="tablesaw break-out" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <thead>
    <tr>
      <th>Prop</th>
      <th>Default value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>as</code></td>
      <td>Same as <code>href</code></td>
      <td>Indicates what to show in the browser URL bar.</td>
    </tr>
    <tr>
      <td><a href="https://nextjs.org/docs/api-reference/next/link#if-the-child-is-a-custom-component-that-wraps-an-a-tag"><code>passHref</code></a></td>
      <td>false</td>
      <td>Forces the <code>Link</code> component to pass the <code>href</code> prop to its child./td>
    </tr>
    <tr>
      <td><code>prefetch</code></td>
      <td>true</td>
      <td>Allows Next.js to proactively fetch pages currently in the viewport even before they’re visited for faster page transitions.</td>
    </tr>
    <tr>
      <td><a href="https://nextjs.org/docs/api-reference/next/link#replace-the-url-instead-of-push"><code>replace</code></a></td>
      <td>false</td>
      <td>Replaces the current navigation <code>history</code> instead of pushing a new URL onto the <code>history</code> stack.</td>
    </tr>
    <tr>
      <td><a href="https://nextjs.org/docs/api-reference/next/link#disable-scrolling-to-the-top-of-the-page"><code>scroll</code></a></td>
      <td>true</td>
      <td>After navigation, the new page should be scrolled to the top.</td>
    </tr>
    <tr>
      <td><a href="https://nextjs.org/docs/routing/shallow-routing"><code>shallow</code></a></td>
      <td>false</td>
      <td>Update the path of the current page without re-running <code>getStaticProps</code>, <code>getServerSideProps</code>, or <code>getInitialProps</code>, allows the page to have stale data if turned on.</td>
    </tr>
  </tbody>
</table>

{{% ad-panel-leaderboard %}}

## Styling

Next.js comes with three styling methods out of the box, global CSS, CSS Modules, and styled-jsx.

There’s an extensive article about Styling in Next.js that has been covered in [Comparing Styling Methods in Next.js](https://www.smashingmagazine.com/2020/09/comparison-styling-methods-next-js/)

## Linting And Formatting

Linting and formatting I suspect is a highly opinionated topic, but empirical metrics show that most people who need it in their JavaScript codebase seem to enjoy the company of [ESLint](https://eslint.org) and [Prettier](https://prettier.io). Where the latter ideally formats, the former lints your codebase. I’ve become quite accustomed to [Wes Bos’s ESLint and Prettier Setup](https://github.com/wesbos/eslint-config-wesbos) because it extends [eslint-config-airbnb](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb), interpolate prettier formatting through ESLint, includes sensible-defaults that mostly works (for me), and can be overridden if the need arises.

Including it in your Next.js project is fairly straightforward. You can [install it globally](https://github.com/wesbos/eslint-config-wesbos#global-install) if you want but we’d be doing so [locally](https://github.com/wesbos/eslint-config-wesbos#local--per-project-install).

- Run the command below in your terminal.

<div class="break-out">

<pre><code class="language-javascript"># This will install all peer dependencies required for the package to work
npx install-peerdeps --dev eslint-config-wesbos</code></pre>
</div>
   
- Create a `.eslintrc` file at the root of your Next.js app, alongside the `pages`, `styles` and `public` folder, with the content:

<pre><code class="language-javascript">{
  "extends": [
    "wesbos"
  ]
}
</code></pre>    

At this point, you can either lint and format your code manually or you can let your editor take control.

- To lint and format manually requires adding two [npm scripts](https://docs.npmjs.com/misc/scripts) lint, and `lint:fix`.

<pre><code class="language-javascript">"scripts": {
  "dev": "next dev",
  "build": "next build",
  "start": "next start"
  "lint": "eslint .", # Lints and show you errors and warnings alone
  "lint:fix": "eslint . --fix" # Lints and fixes
},</code></pre>

- If you’re using [VSCode](https://code.visualstudio.com/) and you’d prefer your editor to automatically lint and format you need to first install the [ESLint VSCode plugin](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) then add the following commands to your VSCode settings:

<pre><code class="language-javascript"># Other setting
"editor.formatOnSave": true,
"[javascript]": {
  "editor.formatOnSave": false
},
"[javascriptreact]": {
  "editor.formatOnSave": false
},
"eslint.alwaysShowStatus": true,
"editor.codeActionsOnSave": {
  "source.fixAll": true
},
"prettier.disableLanguages": ["javascript", "javascriptreact"],
</code></pre>

**Note**: *You can learn more on how to make it work with VSCode over [here](https://github.com/wesbos/eslint-config-wesbos#with-vs-code).*

As you work along you most likely will need to override some config, for example, I had to turn off the [react/jsx-props-no-spreading](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-props-no-spreading.md) rule which errors out when JSX props are been spread as in the case of `pageProps` in the Next.js custom page component, `_app.js`.

<pre><code class="language-javascript">function MyApp({ Component, pageProps }) {
  return &lt;Component {...pageProps} /&gt;;
}</code></pre>

Turning the rule off goes thus:

<pre><code class="language-javascript">{
  "extends": [
    "wesbos"
  ],
  "rules": {
    "react/jsx-props-no-spreading": 0
  }
}
</code></pre>

## Static Assets

At some or several points in your Next.js app lifespan, you’re going to need an asset or another. It could be icons, self-hosted fonts, or images, and so on. To Next.js this is otherwise known as **Static File Serving** and there is a single source of truth, the **public** folder. The Next.js docs warns: *Don't name the `public` directory anything else. The name cannot be changed and is the only directory used to serve static assets.*

Accessing static files is straightforward. Take the folder structure below for example,

<pre><code class="language-javascript">- pages
  profile.js
- public
  - favicon.ico #url /favicon.ico
  - assets
    - fonts
      - font-x.woff2
      - font-x.woff # url: /assets/fonts/font-x.woff2
    - images
      - profile-img.png # url: /assets/images/profile-img.png
- styles
  - globals.css
</code></pre>

You can access the the `profile-img.png` image from the `<Profile/>` component:

<div class="break-out">

<pre><code class="language-javascript">// &lt;Profile/&gt; is a React component
export default function Profile() {
  return {
      &lt;div className="profile-img__wrap"&gt;
        &lt;img src="/assets/images/profile-img.png" alt="a big goofy grin" /&gt;
      &lt;/div&gt;
  }
}
</code></pre>
</div>

or the fonts in the **fonts** folder in CSS:

<pre><code class="language-javascript">/* styles/globals.css */
@font-face {
  font-family: 'font-x';
  src: url(/assets/fonts/font-x.woff2) format('woff2'),
       url(/assets/fonts/font-x.woff) format('woff');
}
</code></pre>

## Data Fetching

Data fetching in Next.js is a huge topic that requires some level of undertaken. Here, we’ll discuss the crux. Before we dive in, there’s a precursory need to have an idea of how Next.js renders its pages.

**Pre-rendering** is a huge part of how Next.js works as well as what makes it fast. By default, Next.js **pre-renders** every page by generating each page HTML in advance alongside the minimal JavaScript they need to run, through a process known as Hydration. 

It is possible albeit impractical for you to turn off JavaScript and still have some parts of your Next.js app render. If you ever do this, consider doing it for mechanical purposes alone to show that Next.js truly Hydrates rendered pages.

That being said, there are two forms of **pre-rendering:**

1. Static Generation (SG),
2. Server-side Rendering (SSR).

The difference between the two lies in **when** data is been fetched. For SG, data is fetched at **build time** and reused on every request (which makes it faster because it can be cached), while in SSR, data is fetched on every request.

What they both have in common is that they can be mixed with [**Client-side Rendering**](https://nextjs.org/docs/basic-features/data-fetching#fetching-data-on-the-client-side)
wit [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API), [Axios](https://github.com/axios/axios), [SWR](https://swr.vercel.app/), [React Query](https://react-query.tanstack.com/) etc.

The two forms of pre-rendering isn’t an absolute one-or-the-other case; you can choose to use Static Generation or Server-side Rendering, or you can use a hybrid of both. That is, while some parts of your Next.js app uses Static Generation, another can use SSR.

In both cases, Next.js offers special functions to fetch your data. You can use one of the [Traditional Approach to Data Fetching in React](https://reactjs.org/docs/concurrent-mode-suspense.html#traditional-approaches-vs-suspense) or you can use the special functions. It’s advisable to use the special functions, not because they’re *supposedly* special, nor because they’re aptly named (as you’ll see) but because they give you a centralized and familiar data fetching technique that you can’t go wrong with.

The three special functions are:

1. **`getStaticProps`** &mdash; used in SG when your **page content** depends on external data.
2. **`getStaticPaths`** &mdash; used in SG when your **page paths** depends on external data.
3. **`getServerSideProps`** &mdash; used in Server-side Rendering.

## `getStaticProps`

`getStaticProps` is a sibling to `getStaticPaths` and is used in Static Generation. It’s an async function where you can fetch external data, and return it as a prop to the default component in a page. The data is returned as a **props** object and implicitly maps to the prop of the default export component on the page.

In the example below, we need to map over the **accounts** and display them, our **page content** is dependent on external data as we fetched and resolved in `getStaticProps`.

<div class="break-out">

<pre><code class="language-javascript">// accounts get passed as a prop to &lt;AccountsPage/&gt; from getStaticProps()
// Much more like &lt;AccountsPage {...{accounts}} /&gt;
export default function AccountsPage({accounts}) {
  return (
    &lt;div&gt;
      &lt;h1&gt;Bank Accounts&lt;/h1&gt;
      {accounts.map((account) =&gt; (
        &lt;div key={account.id}&gt;
          &lt;p&gt;{account.Description}&lt;/p&gt;
        &lt;/div&gt;
      ))}
    &lt;/div&gt;
  )
}

export async function getStaticProps() {
  // This is a real endpoint
  const res = await fetch('https://sampleapis.com/fakebank/api/Accounts');
  const accounts = await res.json();

  return {
    props: {
      accounts: accounts.slice(0, 10),
    },
  };
}</code></pre>
</div>

As you can see, `getStaticProps` works with Static Generation, and returns a **props** object, hence the name.

## `getStaticPaths`

Similar to `getStaticProps`, `getStaticPaths` is used in Static Generation but is different in that it is your **page paths** that is dynamic not your **page content.**  This is often used with `getStaticProps` because it doesn’t return any data to your component itself, instead it returns the paths that should be pre-rendered at build time. With the knowledge of the paths, you can then go ahead to fetch their corresponding **page content**.

Think about Next.js pre-rendering your page in the aspect of a dynamic page with regards to Static Generation. For it to do this successfully at build time, it has to know what the page paths are. But it can’t because they’re dynamic and indeterminate, this is where `getStaticPaths` comes in.

Imagine you have a Next.js app with pages `States` and `state` that shows a list of countries in the United States and a single state respectively. You might have a folder structure that looks like:

<pre><code class="language-javascript">- pages
  - index.js
  - states
    - index.js # url: /states
    - [id].js # url /states/[id].js
 </code></pre>

You create the `[id].js` to show a single state based on their `id`. So, it the **page content** (data returned from `getStaticProps`) will be dependent on the **page paths** (data returned from `getStaticPaths`).

Let’s create the `<States/>` components first.

<div class="break-out">

<pre><code class="language-javascript">// The states will be passed as a prop from getStaticProps
export default function States({states}) {
  // We'll render the states here
}

export async function getStaticProps() {
  // This is a real endpoint.
  const res = await fetch(`https://sampleapis.com/the-states/api/the-states`);
  const states = await res.json();
  
  // We return states as a prop to &lt;States/&gt;
  return {
    props: {
      states
    }
  };
}</code></pre>
</div>

<iframe loading="lazy" src="https://codesandbox.io/embed/getting-started-with-next-omz4k?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="getting-started-with-next"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>


Now let’s create the dynamic page for a single state. It’s the reason we have that `[id].js` so that we can match the path `/states/1`, or `/states/2` where 1 and 2 are the `id` in `[id].js`.

<div class="break-out">

<pre><code class="language-javascript">// We start by expecting a state prop from getStaticProps
export default function State({ state }) {
    // We'll render the states here
}

// getStaticProps has a params prop that will expose the name given to the
// dynamic path, in this case, `id` that can be used to fetch each state by id.
export async function getStaticProps({ params }) {
  const res = await fetch(
    `https://sampleapis.com/the-states/api/the-states?id=${params.id}`
  );
  const state = await res.json();

  return {
    props: {
      state: state[0]
    }
  };
}</code></pre>
</div>

If you try to run the code as it is, you’d get the message: **Error: `getStaticPaths` is required for dynamic SSG pages and is missing for `/states/[id]`.** 

<div class="break-out">

<pre><code class="language-javascript">// The state component
// getStaticProps function
// getStaticPaths
export async function getStaticPaths() {
  // Fetch the list of states
  const res = await fetch("https://sampleapis.com/the-states/api/the-states");
  const states = await res.json();

  // Create a path from their ids: `/states/1`, `/states/2` ...
  const paths = states.map((state) =&gt; `/states/${state.id}`);

  // Return paths, fallback is necessary, false means unrecognize paths will
  // render a 404 page
  return { paths, fallback: false };
}</code></pre>
</div>

With the `paths` returned from `getStaticPaths`, `getStaticProps` will be made aware and its `params` props will be populated with necessary values, like the `id` in this case.

<iframe loading="lazy" src="https://codesandbox.io/embed/getting-started-with-next-omz4k?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="getting-started-with-next"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

## Extras

### Absolute Imports

There’s support for [absolute import](https://nextjs.org/blog/next-9-4#absolute-imports-and-aliases) starting from Next.js 9.4 which means you no longer have to import components relatively like:

<div class="break-out">

<pre><code class="language-javascript">import FormField from "../../../../../../components/general/forms/formfield"</code></pre>
</div>

instead you can do so absolutely like:

<pre><code class="language-javascript">import FormField from "components/general/forms/formfield";</code></pre>

To get this to work, you will need a `jsconfig.json` or `tsconfig.json` file for JavaScript and TypeScript respectively, with the following content:

<pre><code class="language-javascript">{
  "compilerOptions": {
      "baseUrl": "."
  }
}</code></pre>

> This assumes that the `components` folder exists at the root of your app, alongside **pages, styles**, and **public.**

### Experimental ES Features

It is possible to use some experimental features like [Nullish coalescing operator (??)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator) and [Optional chaining (?.)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining) in your Next.js app.

<pre><code class="language-javascript">export default function User({user) {
  return &lt;h1&gt;{person?.name?.first ?? 'No name'}&lt;/h1&gt;
}</code></pre>

## Conclusion

According to the Next.js team, many of the goals they set out to accomplish were the ones listed in The [7 principles of Rich Web Applications,](https://rauchg.com/2014/7-principles-of-rich-web-applications) and as you work your way in and deep into the ecosystem, you’d realize you’re in safe hands like many other [users who have chosen to use Next.js](https://nextjs.org/showcase) to power their websites/web applications. Give it a try, if you haven’t, and if you have, keep going.

### Resources

- [Official Next.js docs](https://nextjs.org/docs/getting-started)
- [Create a Next.js app](https://nextjs.org/docs/routing/introduction)
- [`create-next-app`](https://nextjs.org/docs/api-reference/create-next-app)
- [Next.js pages](https://nextjs.org/docs/basic-features/pages)
- [`next/link`](https://nextjs.org/docs/api-reference/next/link)
- [`next/head`](https://nextjs.org/docs/api-reference/next/head)
- [Next.js routing](https://nextjs.org/docs/routing/introduction)
- [Next.js styling](https://nextjs.org/docs/basic-features/built-in-css-support)
- [Static assets](https://nextjs.org/docs/basic-features/static-file-serving)
- [Data fetching](https://nextjs.org/docs/basic-features/data-fetching)
- [Next.js FAQs](https://nextjs.org/docs/faq)
- [Comparing Styling Methods in Next.js](https://www.smashingmagazine.com/2020/09/comparison-styling-methods-next-js/)
- [7 Principles of Rich Web Applications](https://rauchg.com/2014/7-principles-of-rich-web-applications)

{{< signature "ks, ra, yk, il" >}}

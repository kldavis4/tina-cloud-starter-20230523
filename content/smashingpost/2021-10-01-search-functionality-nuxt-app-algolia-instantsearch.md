---
title: 'How To Implement Search Functionality In Your Nuxt App Using Algolia InstantSearch'
slug: search-functionality-nuxt-app-algolia-instantsearch
author: miracle-onyenma
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/584ac63f-f493-4e93-8d6a-5e6bc640d7ea/search-functionality-nuxt-app-algolia-instantsearch.jpg
date: 2021-10-01T10:00:00.000Z
summary: >-
  Many websites have some sort of search feature because it helps users navigate through their content easily. Implementing it the right way can be tricky and might not give a good user experience. In this tutorial, we will be integrating Algolia, a popular and powerful search service for the best experience on our Nuxt site.
description: >-
  Many websites have some sort of search feature because it helps users navigate through their content easily. Implementing it the right way can be tricky and might not give a good user experience. In this tutorial, we will be integrating Algolia, a popular and powerful search service for the best experience on our Nuxt site.
categories:
  - CSS
  - Apps
  - Vue
  - Nuxt.js
  - JavaScript
---

Giving users the ability to quickly search through and navigate our content easily comes with great benefits. This not only improves the user experience, but also increases user retention and boosts conversion as users can now explore beyond what brought them to our site in the first place.

In this tutorial, we’ll be looking at how to integrate this search functionality into our Nuxt app using Algolia. Algolia is a third-party service that we can integrate into our app and provides us with a set of tools that allow us to create a full search experience in our sites and applications.

We’ll be using Nuxt Content, "Git Based Headless CMS" which allows us to create and manage content using Markdown, XML, JSON files, and so on. We’ll build a Nuxt site with Nuxt Content with a search feature using Algolia InstantSearch, for styling, we’ll use TailwindCSS. This tutorial is aimed at Vue.js devs that are familiar with Nuxt.

## Prerequisites

To follow along with this tutorial, you’ll need to have the following installed:

- [Node](https://nodejs.org/),
- A text editor, I recommend [VS Code](https://code.visualstudio.com/) with the [Vetur](https://marketplace.visualstudio.com/items?itemName=octref.vetur) extension (for Vue.js syntax features in VS Code),
- A terminal, you can use VS Code’s integrated terminal or any other of your choice.

You’ll also require a basic understanding of the following in order to follow along smoothly:

- HTML, CSS & JavaScript,
- [Vue.js](https://vuejs.org/),
- [Nuxt.js](https://nuxtjs.org/),
- [TailwindCSS](https://tailwindcss.com/).

{{% feature-panel %}} 

## Setting Up Our Nuxt App

Nuxt.js is a framework built on Vue, it has many capabilities and features including Server-Side Rendering (SSR).

To install it, open  our terminal and run:

<pre><code class="language-bash">npx create-nuxt-app &lt;project-name&gt;</code></pre>

> Where `<project-name>` is the name of our project folder, I’ll be using `algolia-nuxt` for this project.

Running the command will ask you some questions (name, Nuxt options, UI framework, TypeScript, etc. ). To find out more about all the options, see the [Create Nuxt app](https://github.com/nuxt/create-nuxt-app/blob/master/README.md).

When asked for Nuxt.js modules, make sure to select `Content - Git-based headless CMS` to install the `nuxt/content` module along with our Nuxt app.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/665121ea-a8ff-4099-a2fb-1725b1a2f943/nuxt-installation-in-terminal.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/665121ea-a8ff-4099-a2fb-1725b1a2f943/nuxt-installation-in-terminal.png" width="800" height="309" sizes="100vw" caption="Nuxt installation. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/665121ea-a8ff-4099-a2fb-1725b1a2f943/nuxt-installation-in-terminal.png'>Large preview</a>)" alt="Nuxt installation in terminal." >}}

After selecting all of your options, installation can begin. My selected options look like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73cc1fb3-0424-4760-a512-9f9fbb0a3329/nuxt-installation-options-in-terminal.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73cc1fb3-0424-4760-a512-9f9fbb0a3329/nuxt-installation-options-in-terminal.png" width="800" height="364" sizes="100vw" caption="Selected options for Nuxt. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73cc1fb3-0424-4760-a512-9f9fbb0a3329/nuxt-installation-options-in-terminal.png'>Large preview</a>)" alt="Nuxt installation options in terminal" >}}

After successfully installing the Nuxt app, navigate to the directory by running this command:

<pre><code class="language-bash">cd algolia-nuxt</code></pre>

## Install Nuxt Content Separately

If you already have Nuxt set up before now, you can install the content module by running the command. 

*Skip this if you’ve already selected to install the `nuxt/content` module along with our Nuxt app.*

<pre><code class="language-bash">#install nuxt content

npm install @nuxt/content</code></pre>

Then you can add it to our `modules` property inside our `nuxt.config` file.

<pre><code class="language-javascript">//nuxt.config.js

export default {
  modules: ['@nuxt/content']
}</code></pre>

## Install And Setup TailwindCSS

[TailwindCSS](https://tailwindcss.com/docs/guides/nuxtjs) is a utility first CSS framework that provides us with custom classes we can use to style our app.

We’ll also be using [TailwindCSS Typography](https://github.com/tailwindlabs/tailwindcss-typography), which is "a plugin that provides a set of `prose` classes you can use to add beautiful typographic defaults to any vanilla HTML you don’t control (like HTML rendered from Markdown, or pulled from a CMS)."

First, we install `@nuxtjs/tailwindcss` which is a Nuxt module for TailwindCSS integration, as well as TailwindCSS and its peer-dependencies using npm:

<pre><code class="language-bash">npm install -D @nuxtjs/tailwindcss tailwindcss@latest postcss@latest autoprefixer@latest</code></pre>

Add the `@nuxtjs/tailwindcss` module to the `buildModules` section of our nuxt.config.js file:

<pre><code class="language-javascript">// nuxt.config.js

export default {
  buildModules: ['@nuxtjs/tailwindcss']
}</code></pre>

### Create Configuration File

Next, generate our `tailwind.config.js` file:

<pre><code class="language-javascript">npx tailwindcss init</code></pre>

This will create a minimal `tailwind.config.js` file at the root of  our project:

<pre><code class="language-javascript">//tailwind.config.js

module.exports = {
  purge: [],
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
}</code></pre>

Create a `tailwind.css` file in `assets/css/` use the `@tailwind` directive to inject TailwindCSS’ base, components, and utilities styles:

<pre><code class="language-css">/*assets/css/tailwind.css*/

@tailwind base;
@tailwind components;
@tailwind utilities;</code></pre>

You can import the CSS file into  our components or make it accessible globally by defining the CSS files/modules/libraries you want to set globally *(included in every page).*

<pre><code class="language-javascript">  /* nuxt.config.js*/

  // Global CSS: https://go.nuxtjs.dev/config-css
  css: [
    // CSS file in the project
    '@/assets/css/tailwind.css',
  ],</code></pre>

Here, we have added the path to our `tailwind.css` file to the list of global CSS files in our `nuxt.config.js`. 

> The `@/` tells Nuxt that it's an absolute path to look for the file from the root directory.

### Install TailwindCSS Typography

<pre><code class="language-bash"># Using npm
npm install @tailwindcss/typography</code></pre>

Then add the plugin to our `tailwind.config.js` file:

<pre><code class="language-javascript">// tailwind.config.js
module.exports = {
  purge: [],
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [
    require('@tailwindcss/typography'),
  ],
}</code></pre>

### Configure TailwindCSS To Remove Unused Styles In Production

In our `tailwind.config.js` file, configure the purge option with the paths to all of our pages and components so TailwindCSS can tree-shake unused styles in production builds:

<pre><code class="language-javascript">// tailwind.config.js
module.exports = {
  purge: [
    './components/**/*.{vue,js}',
    './layouts/**/*.vue',
    './pages/**/*.vue',
    './plugins/**/*.{js,ts}',
    './nuxt.config.{js,ts}',
  ],
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [
    require('@tailwindcss/typography'),
  ],
}</code></pre>

Since we’ve installed the packages, let’s start our app:

<pre><code class="language-bash">npm run dev</code></pre>

This command starts our Nuxt app in development mode.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27b671bb-e8f6-47e2-92a2-3ba9dc260b79/screenshot-of-default-nuxt-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27b671bb-e8f6-47e2-92a2-3ba9dc260b79/screenshot-of-default-nuxt-page.png" width="800" height="407" sizes="100vw" caption="Nuxt app started. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27b671bb-e8f6-47e2-92a2-3ba9dc260b79/screenshot-of-default-nuxt-page.png'>Large preview</a>)" alt="Screenshot of default Nuxt page" >}}

Nice 🍻

{{% ad-panel-leaderboard %}} 

## Creating Our Pages And Articles

Now, let’s create our articles and a blog page to list out our articles. But first, let’s create a site header and navigation component for our site.

### Creating A Site Header And Navigation

Navigate to our `components/`folder, and create a new file `siteHeader.vue` and enter the following code:

<pre><code class="language-javascript">&lt;!-- components/siteHeader.vue --&gt;

&lt;template&gt;
  &lt;header class="fixed top-0 w-full bg-white bg-opacity-90 backdrop-filter backdrop-blur-md"&gt;
    &lt;div class="wrapper flex items-center justify-between p-4 m-auto max-w-5xl"&gt;
      &lt;nuxt-link to="/"&gt;
        &lt;Logo /&gt;
      &lt;/nuxt-link&gt;

      &lt;nav class="site-nav"&gt;
        &lt;ul class="links"&gt;
          &lt;li&gt;
            &lt;nuxt-link to="/blog"&gt;Blog&lt;/nuxt-link&gt;
          &lt;/li&gt;
        &lt;/ul&gt;
      &lt;/nav&gt;
    &lt;/div&gt;
  &lt;/header&gt;
&lt;/template&gt;</code></pre>

Here, in our `<header>` we have a `<Logo />` component wrapped in `<nuxt-link>` which routes to the home page and another `<nuxt-link>` that routes to `/blog` *(We’ll create the blog page that we will create later on)*.

This works without us importing the components and configuring routing ourselves because, by default, Nuxt handles importing components and routing for us.

Also, let’s modify the default `<Logo />` component. In `components/Logo.vue`, replace the content with the following code:

<pre><code class="language-javascript">&lt;!-- components/Logo.vue --&gt;

&lt;template&gt;
  &lt;figure class="site-logo text-2xl font-black inline-block"&gt;
    &lt;h1&gt;Algolia-nuxt&lt;/h1&gt;
  &lt;/figure&gt;
&lt;/template&gt;</code></pre>

We can now add our `siteHeader.vue` component to our site. In `layouts/default.vue`, add `<site-header />` just above the `<Nuxt />` component. 

<pre><code class="language-javascript">&lt;!-- layouts/default.vue --&gt;

&lt;template&gt;
  &lt;div&gt;
    &lt;site-header /&gt;
    &lt;Nuxt /&gt;
  &lt;/div&gt;
&lt;/template&gt;

...</code></pre>

The `<Nuxt />` component renders the current Nuxt page depending on the route.

### Creating Our First Article

In `content/`, which is a folder created automatically for the `nuxt/content` module, create a new folder `articles/` and then a new file in the folder `first-blog-post.md`. Here is the file for our first article in `markdown` format. Enter the following code:

<pre><code class="language-html">&lt;!-- content/articles/first-blog-post.md --&gt;

---

title: My first blog post
description: This is my first blog post on algolia nuxt
tags: [first, lorem ipsum, Iusto]

---

## Lorem ipsum

Lorem ipsum dolor sit amet consectetur, adipisicing elit.
Assumenda dolor quisquam consequatur distinctio perferendis.

## Iusto nobis nisi

repellat magni facilis necessitatibus, enim temporibus.

- Quisquam
- assumenda
- sapiente explicabo
- totam nostrum inventore</code></pre>

The area enclosed with `---` is the `YAML` Front Matter which will be used as a custom injected variable that we will access in our template.

Next, we’re going to create a [dynamic page](https://nuxtjs.org/docs/2.x/directory-structure/pages#dynamic-pages) which will be used to:

- Fetch the article content using `asyncData` which runs before the page has been rendered. We have access to our content and custom injected variables through the context by using the variable `$content`. As we are using a dynamic page, we can know what article file to fetch using the `params.slug` variable provided by [Vue Router](https://router.vuejs.org/) to get the name of each article.
- Render the article in the template using `<nuxt-content>`.

Ok, navigate to `pages/` and create a `blog/` folder. Create a `_slug.vue` (our dynamic page) file and insert the following:

<pre><code class="language-javascript">&lt;!-- pages/blog/_slug.vue --&gt;

&lt;template&gt;
  &lt;article class="prose prose-lg lg:prose-xl p-4 mt-24 m-auto max-w-4xl"&gt;
    &lt;header&gt;
      &lt;h1&gt;{{ article.title }}&lt;/h1&gt;
      &lt;p&gt;{{ article.description }}&lt;/p&gt;
      &lt;ul class="list-none"&gt;
        &lt;li class="inline-block mr-2 font-bold font-monospace" v-for="tag in article.tags" :key="tag" &gt; {{tag}} &lt;/li&gt;
      &lt;/ul&gt;
    &lt;/header&gt;
    &lt;!-- this is where we will render the article contents --&gt;
    &lt;nuxt-content :document="article" /&gt;
  &lt;/article&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
  async asyncData({ $content, params }) {
    //here, we will fetch the article from the articles/ folder using the name provided in the `params.slug`
    const article = await $content('articles', params.slug).fetch()

    //return `article` which contains our custom injected variables and the content of our article
    return { article }
  },
}
&lt;/script&gt;</code></pre>

If you go to your browser and navigate to `https://localhost:3000/blog/first-blog-post` you should see our rendered content:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f853824e-400d-4a70-9401-b323322f50c6/screenshot-of-rendered-article-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f853824e-400d-4a70-9401-b323322f50c6/screenshot-of-rendered-article-page.png" width="800" height="406" sizes="100vw" caption="Article page rendered. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f853824e-400d-4a70-9401-b323322f50c6/screenshot-of-rendered-article-page.png'>Large preview</a>)" alt="Screenshot of rendered article page" >}}

Now that our dynamic page is working and our article is rendering, let’s create some duplicates for the purpose of this tutorial.

<pre><code class="language-html">&lt;!-- content/articles/second-blog-post.md --&gt;

---

title: My first blog post
description: This is my first blog post on algolia nuxt
tags: [first, Placeat amet, Iusto]

---

## Lorem ipsum

Lorem ipsum dolor sit amet consectetur, adipisicing elit.
Assumenda dolor quisquam consequatur distinctio perferendis.

## Iusto nobis nisi

repellat magni facilis necessitatibus, enim temporibus.

- Quisquam
- assumenda
- sapiente explicabo
- totam nostrum inventore</code></pre>

### Create Blog Page To List Our Articles

Let’s now create a blog page to list our articles. This is also where our search bar will live. Create a new file `pages/blog/index.vue`.

<pre><code class="language-javascript">&lt;!-- pages/blog/index.vue --&gt;

&lt;template&gt;
  &lt;main&gt;
    &lt;section class="p-4 mt-24 m-auto max-w-4xl"&gt;
      &lt;header&gt;
        &lt;h1 class="font-black text-2xl"&gt;All posts&lt;/h1&gt;
          
        &lt;!-- dummy search bar --&gt;
        &lt;div class="search-cont inline-flex gap-2 bg-white p-2 rounded-lg shadow-lg"&gt;
          &lt;input class="px-2 outline-none" type="search" name="search" id="search"&gt;
          &lt;button class="bg-blue-600 text-white px-2 rounded-md" type="submit"&gt;Search&lt;/button&gt;
        &lt;/div&gt;
      &lt;/header&gt;
      &lt;ul class="prose prose-xl"&gt;
          &lt;!-- list out all fetched articles --&gt; 
        &lt;li v-for="article in articles" :key="article.slug"&gt;
          &lt;nuxt-link :to="{ name: 'blog-slug', params: { slug: article.slug } }"&gt;
            &lt;h2 class="mb-0"&gt;{{ article.title }}&lt;/h2&gt;
            &lt;p class="mt-0"&gt;{{ article.description }}&lt;/p&gt;
          &lt;/nuxt-link&gt;
        &lt;/li&gt;
      &lt;/ul&gt;
    &lt;/section&gt;
  &lt;/main&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
  async asyncData({ $content }) {
    // fetch all articles in the folder and return the:
    const articles = await $content('articles')
      // title, slug and description
      .only(['title', 'slug', 'description'])
      // sort the list by the `createdAt` time in `ascending order`
      .sortBy('createdAt', 'asc')
      .fetch()

    return { articles }
  },
}
&lt;/script&gt;</code></pre>

Here, in our `asyncData` function, when fetching `$content('articles')` we chain `.only(['title', 'slug', 'updatedAt', 'description'])` to fetch only those attributes from the articles, `.sortBy('createdAt', 'asc')` to sort it and lastly `fetch()` to fetch the data and assign it to `const articles` which we then return.

So, in our `<template>`, we can the list of articles and create links to them using their `slug` property.

Our page should look something like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cbbe4a5-bb8f-4576-b50f-1bd8d57557a4/screenshot-of-blog-page-listing-all-articles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cbbe4a5-bb8f-4576-b50f-1bd8d57557a4/screenshot-of-blog-page-listing-all-articles.png" width="800" height="408" sizes="100vw" caption="Blog page listing all articles. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cbbe4a5-bb8f-4576-b50f-1bd8d57557a4/screenshot-of-blog-page-listing-all-articles.png'>Large preview</a>)" alt="Screenshot of Blog page listing all articles" >}}

Great 🍻

## Install And Set Up Algolia Search And Vue-instantSearch

Now that we’ve gotten the basic stuff out of the way, we can integrate Algolia Search into our blog site. 

First, let’s install all the packages we will be needing:

<pre><code class="language-bash">#install dependencies

npm install vue-instantsearch instantsearch.css algoliasearch nuxt-content-algolia remove-markdown dotenv</code></pre>

- **`vue-instantsearch`**   
Algolia InstantSearch UI component/widget library for Vue.
- **`instantsearch.css`**    
Custom styling for instantSearch widgets.
- **`algoliasearch`**  
A HTTP client to interact with Algolia.
- **`nuxt-content-algolia`**  
Package for indexing our content and sending it to Algolia.
- **`remove-markdown`**  
This strips all markdown characters from the `bodyPlainText` of the articles.
- **`dotenv`**  
This helps to read environment variables from `.env` files.

We’ll be using these packages throughout the rest of this tutorial, but first, let’s set up an Algolia account.

### Set Up Algolia Account

Sign up for an Algolia account at [https://www.algolia.com/](https://www.algolia.com/). You can do this for free, however, this will give you a trial period of 14days. Since we’re not performing heavy tasks with Algolia, their free tier will do just fine for our project after the trial expires.

You’ll be taken through some onboarding steps. After that, an *UNAMED APP* will be created for you. On the sidebar, on the left, navigate to **the API Keys** you’ll be provided with:

- **Application ID**  
This is your unique application identifier. It’s used to identify you when using Algolia’s API.
- **Search Only API Key**  
This is the public API key to use in your frontend code. This key is only usable for search queries and sending data to the Insights API.
- **Admin API Key**  
This key is used to create, update and DELETE your indices. You can also use it to manage your API keys.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbb4962e-7f60-4404-a08a-e2fe58610a6a/screenshot-of-algolia-account-page-to-get-api-keys.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbb4962e-7f60-4404-a08a-e2fe58610a6a/screenshot-of-algolia-account-page-to-get-api-keys.png" width="800" height="450" sizes="100vw" caption="Algolia account to retrieve API keys. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbb4962e-7f60-4404-a08a-e2fe58610a6a/screenshot-of-algolia-account-page-to-get-api-keys.png'>Large preview</a>)" alt="Screenshot of Algolia account page to get API Keys" >}}

Now that we have our API Keys, let’s save them in an `.env` file for our project. Navigate to the project root folder and create a new file `.env` and enter your API keys:

<pre><code class="language-javascript">.env

ALGOLIA_APP_ID=algolia-app-id
ALGOLIA_API_KEY=algolia-admin-api-key</code></pre>

Replace `algolia-app-id` and `algolia-admin-api-key` with your Application ID and Admin API Key respectively.

### Create An `'Articles'` Index For Our Nuxt Articles In Algolia

On your Algolia account, go to **Indices** and click on **create Index**. Then enter the name of your index and we’ll be using **articles** for this tutorial.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b37bf5fd-b7d0-4cc0-b1e5-a43e42ecc216/screenshot-of-algolia-account-page-to-create-new-index.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b37bf5fd-b7d0-4cc0-b1e5-a43e42ecc216/screenshot-of-algolia-account-page-to-create-new-index.png" width="800" height="450" sizes="100vw" caption="Create a new <code>'articles'</code> index on Algolia. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b37bf5fd-b7d0-4cc0-b1e5-a43e42ecc216/screenshot-of-algolia-account-page-to-create-new-index.png'>Large preview</a>)" alt="Screenshot of Algolia account page to create new index" >}}

As you can see, our `'article'` index has been created.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c756c99-d45a-4765-a2c0-8347f1ff5955/screenshot-of-algolia-account-page-created-index.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c756c99-d45a-4765-a2c0-8347f1ff5955/screenshot-of-algolia-account-page-created-index.png" width="800" height="450" sizes="100vw" caption="New <code>'articles'</code> index created. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c756c99-d45a-4765-a2c0-8347f1ff5955/screenshot-of-algolia-account-page-created-index.png'>Large preview</a>)" alt="Screenshot of Algolia account page, created index" >}}

### Set Up `nuxt-content-algolia` To Send Content Index To Algolia

We’ve successfully created an index property on our account. Now we have to generate an index from our Nuxt articles which is what Algolia will use to provide results for search queries. This is what the `nuxt-content-algolia` module that we previously installed is for.

We need to configure it in our `nuxt.config.js`. 

First, we will add it to our `buildModules`:

<pre><code class="language-javascript">// nuxt.config.js

...

// Modules for dev and build (recommended): https://go.nuxtjs.dev/config-modules
buildModules: ['@nuxtjs/tailwindcss', 'nuxt-content-algolia'],

...</code></pre>

Then, we create a new `nuxtContentAlgolia` object and add a few configurations to it:

<pre><code class="language-javascript">// nuxt.config.js

export default {
...

nuxtContentAlgolia: {

  // Application ID
  appId: process.env.ALGOLIA_APP_ID,
    
  // Admin API Key
  // !IMPORTANT secret key should always be an environment variable
  // this is not your search only key but the key that grants access to modify the index
  apiKey: process.env.ALGOLIA_ADMIN_API_KEY,

  paths: [
    {
      name: 'articles',
      index: process.env.ALGOLIA_INDEX || 'articles',
      fields: ['title', 'description', 'tags', 'bodyPlainText']
    }
  ]
},


...
}</code></pre>

The `nuxtContentAlgolia` takes in the following properties:

- **`appId`**  
Application ID*.
- **`apiKey`**  
Admin API Key.
- **`paths`**  
An array of index objects. This is where we define where we want to generate indexes from. Each object takes the following properties:
    - **`name`**  
    The name of the folder within the `content/` folder. In other words, we’ll be using files within `content/articles/` since we defined the name as `'articles'`.
    - **`index`**  
    This is the name of the index we created on our Algolia dashboard.
    - **`fields`**  
    An array of fields to be indexed. This is what Algolia will base its search queries on.

### Generate `bodyPlainText` From Articles

Note that in the `fields` array, we have `bodyPlainText` as one of its values. Nuxt Content does not provide such a field for us. Instead, what Nuxt Content provides is `body` which is a complex object that will be rendered in the DOM.

In order to get our `bodyPlainText` which is simply all text, stripped of markdown and HTML characters, we have to make use of yet another package, `remove-markdown`. 

To use the `remove-markdown` function we need to make use of Nuxt `hooks`. We’ll use the [`'content:file:beforeInsert'`](https://content.nuxtjs.org/advanced/#contentfilebeforeinsert) hook which allows you to add data to a document before it is inserted, to strip off the markdown and add the generated plain text to `bodyPlainText`.

<pre><code class="language-javascript">// nuxt.config.js

export default {
...
    
hooks: {
  'content:file:beforeInsert': (document)=&gt;{
    const removeMd = require('remove-markdown');

    if(document.extension === '.md'){
      document.bodyPlainText = removeMd(document.text);
    }
  }
},

...
}</code></pre>

In the `'content:file:beforeInsert'` hook, we get the `remove-markdown` package. Then we check if the file to be inserted is a markdown file. If it is a markdown file, we generate the plain text by calling `removeMd` which takes `document.text` &mdash; the text of our content, as an argument, which we assign to a new `document.bodyPlainText` property. The property will now be available for use through Nuxt Content.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40151123-4f97-4e7f-b2ea-91337d7ff8e9/vue-devtools-showing-bodyplaintext-property.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40151123-4f97-4e7f-b2ea-91337d7ff8e9/vue-devtools-showing-bodyplaintext-property.png" width="800" height="450" sizes="100vw" caption="<code>BodyPlainText</code> generated and visible in Nuxt. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40151123-4f97-4e7f-b2ea-91337d7ff8e9/vue-devtools-showing-bodyplaintext-property.png'>Large preview</a>)" alt="Vue Devtools showing bodyPlainText property" >}}

Great! Now that that’s done, we can generate the index and send it over to Algolia. 

### Confirm Algolia Index

Alright. We’ve set up `nuxt-content-algolia` and we’ve generated `bodyPlainText` for our articles. We can now generate this index and send the data over to Algolia by building our project using `nuxt generate`.

<pre><code class="language-bash">npm run generate</code></pre>

This will start building our project for production and run the `nuxtContentAlgolia` config. When we look at our terminal after the build we should see that our content has been indexed and sent to Algolia.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c26c53c-7376-460b-b4c5-da995bbab5f0/screenshot-of-terminal-showing-indexed-2-records.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c26c53c-7376-460b-b4c5-da995bbab5f0/screenshot-of-terminal-showing-indexed-2-records.png" width="800" height="303" sizes="100vw" caption="Index generated for articles. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c26c53c-7376-460b-b4c5-da995bbab5f0/screenshot-of-terminal-showing-indexed-2-records.png'>Large preview</a>)" alt="Screenshot of terminal showing Indexed 2 records..." >}}

To verify, you can go to your Algolia dashboard:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fae46fe-d907-4d8f-87b2-b8fb0b2ba28e/screenshot-of-algolia-indices-page-showing-search-api-logs-to-confirm-index-creation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fae46fe-d907-4d8f-87b2-b8fb0b2ba28e/screenshot-of-algolia-indices-page-showing-search-api-logs-to-confirm-index-creation.png" width="800" height="450" sizes="100vw" caption="Confirm index in Algolia Search API logs. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fae46fe-d907-4d8f-87b2-b8fb0b2ba28e/screenshot-of-algolia-indices-page-showing-search-api-logs-to-confirm-index-creation.png'>Large preview</a>)" alt="Screenshot of Algolia indices page showing search api logs to confirm index creation" >}}

Open *Indices*, then go to *Search API logs*, where you will see a log of operations performed with your *Search API*. You can now open and check the API call sent from your Nuxt project. This should have the content of your article as specified in the `fields` section of `nuxtContentAlgolia` config.

Nice! 🍻

{{% ad-panel-leaderboard %}} 

## Building The Search UI

So far we’ve been able to generate and send index data to Algolia, which means that we are able to query this data to get search results.

To do that within our app, we have to build our search UI.

`Vue-InstantSearch` provides lots of UI components using Algolia that can be integrated to provide a rich search experience for users. Let’s set it up.

### Create And Configure `vue-instantSearch` Plugin

In order to use the Algolia `InstantSearch` widgets in our Nuxt app, we will have to create a plugin in our `plugins` folder.

Go to `plugins/` and create a new file `vue-instantsearch.js`.

<pre><code class="language-javascript">// plugins/vue-instantsearch.js

import Vue from 'vue'
import InstantSearch from 'vue-instantsearch'

Vue.use(InstantSearch)</code></pre>

Here, we’re simply importing `InstantSearch` and using it on the `Vue` frontend.

Now, we have to add the `vue-instantSearch` plugin to our plugins and build options in `nuxt.config.js` in order to transpile it to Vue.js.

So, go over to `nuxt.config.js` and add the following:

<pre><code class="language-javascript">// nuxt.config.js

export default {
...

// Plugins to run before rendering page: https://go.nuxtjs.dev/config-plugins
plugins: ['@/plugins/vue-instantsearch.js'],

// Build Configuration: https://nuxtjs.org/docs/2.x/configuration-glossary/configuration-build#transpile
build: {
  transpile: ['vue-instantsearch', 'instantsearch.js/es']
}

...
}</code></pre>

`InstantSearch` code uses ES modules, yet it needs to be executed in `Node.js`. That’s why we need to let Nuxt know that those files should be transpiled during the build.
Now that we’ve configured our `vue-instantSearch` plugin, let’s create a search component.

### Create A Search Component

Create a new file `components/Search.vue`.

Since we’ve installed `vue-instantSearch` as a plugin, we can use it within our Vue components.

<pre><code class="language-javascript">&lt;!-- components/Search.vue --&gt;

...

&lt;script&gt;
import algoliaSearch from 'algoliasearch/lite'
import 'instantsearch.css/themes/satellite-min.css'

// configurations for Algolia search
const searchClient = algoliaSearch(
  // Applictaion ID
  '34IIDW6KKR',
    
  // Search API key
  '3f8d80be6c42bb030d27a7f108eb75f8'
)
export default {
    data(){
        return{
            searchClient
        }
    }
}
&lt;/script&gt;</code></pre>

First, in the `<script>` section, we’re importing `algoliaSearch` and `instantsearch.css`.

Next, we provide the credentials for our Algolia search which are:

- **Application ID**,
- **Search API key**.

As parameters to `algoliaSearch` then assign it to `searchClient` which we will use in our `<template>` to configure our Algolia search widgets.

### `ais-instant-search` Widget

`ais-instant-search` is the root Vue `InstantSearch` component. All other widgets need to be wrapped with the root component to function. The required attributes for this component are: 

- **`index-name`**      
Name of the index to query, in this case, it would be `articles`.
- **`search-client`**      
`algoliaSearch` object containing Application ID and Search API Key.

<pre><code class="language-javascript">&lt;!-- components/Search.vue --&gt;

&lt;template&gt;
  &lt;div class="search-cont inline-flex gap-2 bg-white p-2 rounded-lg shadow-lg"&gt;
    &lt;ais-instant-search index-name="articles" :search-client="searchClient"&gt;
    &lt;/ais-instant-search&gt;
  &lt;/div&gt;
&lt;/template&gt;

...</code></pre>

### `ais-configure` Widget

The `ais-configure` widget helps configure the search functionality by sending defined parameters to Algolia.

Any props you add to this widget will be forwarded to Algolia. For more information on the different parameters you can set, have a look at the [search parameters API reference](https://www.algolia.com/doc/api-reference/search-api-parameters/).

The parameters we’ll set for now will be:

- **`attributesToSnippet`**  
The name of the attribute or `field` to snippet in, we’ll soon see more on this.
- **`hits-per-page.camel`**    
Number of results in one page.
- **`snippetEllipsisText="…"`**  
Set `...` before and after snipped text.

<pre><code class="language-javascript">&lt;!-- components/Search.vue --&gt;

&lt;template&gt;
  &lt;div class="search-cont inline-flex gap-2 bg-white p-2 rounded-lg shadow-lg"&gt;
    &lt;ais-instant-search index-name="articles" :search-client="searchClient"&gt;
      &lt;ais-configure
        :attributesToSnippet="['bodyPlainText']"
        :hits-per-page.camel="5"
        snippetEllipsisText="…"
      &gt;
      &lt;/ais-configure&gt;
    &lt;/ais-instant-search&gt;
  &lt;/div&gt;
&lt;/template&gt;

...</code></pre>

### `ais-autocomplete` Widget

This widget is basically a wrapper that allows us to create a search result that autocompletes the query. Within this widget, we can connect to other widgets to provide a richer UI and access multiple indices.

<pre><code class="language-javascript">&lt;!-- components/Search.vue --&gt;

&lt;template&gt;
  &lt;div class="search-cont inline-flex gap-2 bg-white p-2 rounded-lg shadow-lg"&gt;
    &lt;ais-instant-search index-name="articles" :search-client="searchClient"&gt;
      &lt;ais-configure
        :attributesToSnippet="['bodyPlainText']"
        :hits-per-page.camel="5"
        snippetEllipsisText="…"
      &gt;
        &lt;ais-autocomplete&gt;
          &lt;template v-slot="{ currentRefinement, indices, refine }"&gt;
            &lt;input
              type="search"
              :value="currentRefinement"
              placeholder="Search for an article"
              @input="refine($event.currentTarget.value)"
            /&gt;
            &lt;ais-stats /&gt;
            &lt;template v-if="currentRefinement"&gt;
              &lt;ul v-for="index in indices" :key="index.indexId"&gt;
                &lt;li&gt;
                  &lt;h3&gt;{{ index.indexName }}&lt;/h3&gt;
                  &lt;ul&gt;
                    &lt;li v-for="hit in index.hits" :key="hit.objectID"&gt;
                      &lt;h1&gt;
                        &lt;ais-highlight attribute="title" :hit="hit" /&gt;
                      &lt;/h1&gt;
                      &lt;h2&gt;
                        &lt;ais-highlight attribute="description" :hit="hit" /&gt;
                      &lt;/h2&gt;
                      &lt;p&gt;
                        &lt;ais-snippet attribute="bodyPlainText" :hit="hit" /&gt;
                      &lt;/p&gt;
                    &lt;/li&gt;
                  &lt;/ul&gt;
                &lt;/li&gt;
              &lt;/ul&gt;
            &lt;/template&gt;
            &lt;ais-pagination /&gt;
          &lt;/template&gt;
        &lt;/ais-autocomplete&gt;
      &lt;/ais-configure&gt;
    &lt;/ais-instant-search&gt;
  &lt;/div&gt;
&lt;/template&gt;

...</code></pre>

So, within our `ais-autocomplete` widget, we’re doing a few things:

- Overriding the  DOM output of the widget using the `default` slot. We’re doing this using the scopes:
    - **`currentRefinement: string`**: the current value of the query.
    - **`indices: object[]`**: the list of indices.
    - **`refine: (string) => void`**: the function to change the query.

<pre><code class="language-javascript">...
&lt;template v-slot="{ currentRefinement, indices, refine }"&gt;
...</code></pre>

- Create a search `<input>` to hold, change the query and value of the `currentRefinement`.

<pre><code class="language-javascript">...
&lt;input
    type="search"
    :value="currentRefinement"
    placeholder="Search for an article"
    @input="refine($event.currentTarget.value)"
/&gt;
...</code></pre>

- Render the search results for each index. Each index has the following properties:
    - **`indexName: string`**: the name of the index.
    - **`indexId: string`**: the id of the index.
    - **`hits: object[]`**: the resolved hits from the index matching the query.

<pre><code class="language-javascript">...
&lt;template v-if="currentRefinement"&gt;
    &lt;ul v-for="index in indices" :key="index.indexId"&gt;
        &lt;li&gt;
            &lt;h3&gt;{{ index.indexName }}&lt;/h3&gt;
            
...</code></pre>

- Then render the results &mdash; `hits`.

<pre><code class="language-javascript">...
&lt;ul&gt;
    &lt;li v-for="hit in index.hits" :key="hit.objectID"&gt;
      &lt;h1&gt;
        &lt;ais-highlight attribute="title" :hit="hit" /&gt;
      &lt;/h1&gt;
      &lt;h2&gt;
        &lt;ais-highlight attribute="description" :hit="hit" /&gt;
      &lt;/h2&gt;
      &lt;p&gt;
        &lt;ais-snippet attribute="bodyPlainText" :hit="hit" /&gt;
      &lt;/p&gt;
    &lt;/li&gt;
&lt;/ul&gt;

...</code></pre>

Here’s what we’re using:

- **`<ais-highlight>`**  
Widget to highlight the portion of the result which directly matches the query of the field passed to the `attribute` prop.
- **`<ais-snippet>`**  
Widget to display the relevant section of the snippeted attribute and highlight it. We defined the `attribute` in `attributesToSnippet` in `<ais-configure>`.

Let’s run our dev server and see what our New search looks like.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da9fad78-4dd8-41fa-8dd0-9352e609f249/search-component-with-vue-instantsearch-widgets.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da9fad78-4dd8-41fa-8dd0-9352e609f249/search-component-with-vue-instantsearch-widgets.png" width="800" height="409" sizes="100vw" caption="New Search component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da9fad78-4dd8-41fa-8dd0-9352e609f249/search-component-with-vue-instantsearch-widgets.png'>Large preview</a>)" alt="Search component with vue instantsearch widgets " >}}

## Styling Our Search Component

InstantSearch comes with some default styles that we included in our project using the `instantsearch.css` package. However, we might need to change or add some styles to our components to suit the site we’re building.

The CSS classes with many widgets can be overwritten using the [`class-names`](https://www.algolia.com/doc/api-reference/widgets/highlight/vue/#widget-param-class-names) prop. For example, we can change the highlighted style of `<ais-highlight>`.

<pre><code class="language-javascript">&lt;!-- components/Search.vue --&gt;

...
&lt;h1&gt;
  &lt;ais-highlight
    :class-names="{
      'ais-Highlight-highlighted': 'customHighlighted',
    }"
    attribute="title"
    :hit="hit"
  /&gt;
&lt;/h1&gt;

...</code></pre>

And in our CSS:

<pre><code class="language-javascript">&lt;!-- components/Search.vue --&gt;

...

&lt;style&gt;
    .customHighlighted {
      @apply text-white bg-gray-600;
    }
&lt;/style&gt;
...</code></pre>

We see that the class we defined has been applied to the highlight.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd3e70d3-9939-4aba-8157-dfcf0f8ca4eb/screenshot-of-site-and-devtools-showing-custom-css-classes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd3e70d3-9939-4aba-8157-dfcf0f8ca4eb/screenshot-of-site-and-devtools-showing-custom-css-classes.png" width="800" height="450" sizes="100vw" caption="Custom classes for <code>&lt;ais-highlight&gt;</code> component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd3e70d3-9939-4aba-8157-dfcf0f8ca4eb/screenshot-of-site-and-devtools-showing-custom-css-classes.png'>Large preview</a>)" alt="Screenshot of site and devtools showing custom css classes" >}}

So, I’ll go ahead and style it using tailwind till I feel it looks good.

<pre><code class="language-javascript">&lt;!-- components/Search.vue --&gt;

&lt;template&gt;
  &lt;div class="search-cont relative inline-flex mt-6 bg-gray-100 border-2 rounded-lg focus-within:border-purple-600"&gt;
    &lt;ais-instant-search-ssr index-name="articles" :search-client="searchClient"&gt;
      &lt;ais-configure :attributesToSnippet="['bodyPlainText']" :hits-per-page.camel="5"&gt;
        &lt;ais-autocomplete class="wrapper relative"&gt;
          &lt;div slot-scope="{ currentRefinement, indices, refine }"&gt;
            &lt;input class="p-2 bg-white bg-opacity-0 outline-none" type="search" :value="currentRefinement" placeholder="Search for an article" @input="refine($event.currentTarget.value)" /&gt;
            &lt;div class="results-cont relative"&gt;
              &lt;div
                class=" absolute max-h-96 overflow-y-auto w-96 top-2 left-0 bg-white border-2 rounded-md shadow-lg" v-if="currentRefinement"&gt;
                &lt;ais-stats class="p-2" /&gt;
                &lt;ul v-for="index in indices" :key="index.indexId"&gt;
                  &lt;template v-if="index.hits.length &gt; 0"&gt;
                    &lt;li&gt;
                      &lt;h2 class="font-bold text-2xl p-2"&gt;
                        {{ index.indexName }}
                      &lt;/h2&gt;
                      &lt;ul&gt;
                        &lt;li
                          class="border-gray-300 border-t p-2 hover:bg-gray-100" v-for="hit in index.hits" :key="hit.objectID" &gt;
                          &lt;nuxt-link
                            :to="{
                              name: 'blog-slug',
                              params: { slug: hit.objectID },
                            }"
                          &gt;
                            &lt;h3 class="font-extrabold text-xl"&gt;
                              &lt;ais-highlight
                                :class-names="{
                                  'ais-Highlight-highlighted':
                                    'customHighlighted',
                                }"
                                attribute="title"
                                :hit="hit"
                              /&gt;
                            &lt;/h3&gt;
                            &lt;p class="font-bold"&gt;
                              &lt;ais-highlight
                                :class-names="{
                                  'ais-Highlight-highlighted':
                                    'customHighlighted',
                                }"
                                attribute="description"
                                :hit="hit"
                              /&gt;
                            &lt;/p&gt;
                            &lt;p class="text-gray-500"&gt;
                              &lt;ais-snippet
                                :class-names="{
                                  'ais-Snippet-highlighted':
                                    'customHighlighted',
                                }"
                                attribute="bodyPlainText"
                                :hit="hit"
                              /&gt;
                            &lt;/p&gt;
                          &lt;/nuxt-link&gt;
                        &lt;/li&gt;
                      &lt;/ul&gt;
                    &lt;/li&gt;
                  &lt;/template&gt;
                &lt;/ul&gt;
              &lt;/div&gt;
            &lt;/div&gt;
          &lt;/div&gt;
        &lt;/ais-autocomplete&gt;
      &lt;/ais-configure&gt;
    &lt;/ais-instant-search-ssr&gt;
  &lt;/div&gt;
&lt;/template&gt;

...

&lt;style&gt;
.customHighlighted {
  @apply text-purple-600 bg-purple-100 rounded p-1;
}
&lt;/style&gt;</code></pre>

Alright, the styling is done and I’ve included a `<nuxt-link>` to route to the article on click.

<pre><code class="language-javascript">&lt;nuxt-link :to="{ name: 'blog-slug', params: { slug: hit.objectID }}"&gt;</code></pre>

We now have something like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9320ce28-b049-4389-950b-e83fde8164a0/screenshot-of-search-component-with-styling.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9320ce28-b049-4389-950b-e83fde8164a0/screenshot-of-search-component-with-styling.png" width="800" height="407" sizes="100vw" caption="Styled Search component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9320ce28-b049-4389-950b-e83fde8164a0/screenshot-of-search-component-with-styling.png'>Large preview</a>)" alt="Screenshot of search component with styling" >}}

## Configuring InstantSearch For Server-Side Rendering (SSR)

We now have our search component up and running but it only renders on the client-side and this means we have to wait for the search component to load even after the page loads. We can further improve the performance of our site by rendering it on the server-side.

According to [Algolia](https://www.algolia.com/doc/guides/building-search-ui/going-further/server-side-rendering/vue/#with-nuxt), the steps for implementing server-side rendering are:

On the server:

- Make a request to Algolia to get search results.
- Render the Vue app with the results of the request.
- Store the search results on the page.
- Return the HTML page as a string.

On the client:

- Read the search results from the page.
- Render (or hydrate) the Vue app with search results.

### Using Mixins, `serverPreFetch`, `beforeMount`

Following Algolia’s documentation on implementing SSR with Nuxt, we have to make the following changes:

<pre><code class="language-javascript">&lt;!-- components/Search.vue --&gt;

...
&lt;script&gt;
// import 'vue-instantsearch';
import { createServerRootMixin } from 'vue-instantsearch'

import algoliaSearch from 'algoliasearch/lite'
import 'instantsearch.css/themes/satellite-min.css'

const searchClient = algoliaSearch(
  '34IIDW6KKR',
  '3f8d80be6c42bb030d27a7f108eb75f8'
)

export default {
  data() {
    return {
      searchClient,
    }
  },

  mixins: [
    createServerRootMixin({
      searchClient,
      indexName: 'articles',
    }),
  ],

  serverPrefetch() {
    return this.instantsearch.findResultsState(this).then((algoliaState) =&gt; {
      this.$ssrContext.nuxt.algoliaState = algoliaState
    })
  },

  beforeMount() {
    const results =
      (this.$nuxt.context && this.$nuxt.context.nuxtState.algoliaState) ||
      window.__NUXT__.algoliaState

    this.instantsearch.hydrate(results)

    // Remove the SSR state so it can’t be applied again by mistake
    delete this.$nuxt.context.nuxtState.algoliaState
    delete window.__NUXT__.algoliaState
  },
}
&lt;/script&gt;</code></pre>

We’re simply doing the following:

- **`createServerRootMixin`** to create a reusable search instance;
- **`findResultsState`** in **`serverPrefetch`** to perform a search query on the back end;
- **`hydrate`** method in **`beforeMount`**.

Then in our `<template>`,

<pre><code class="language-javascript">&lt;!-- components/Search.vue --&gt;

...
&lt;ais-instant-search-ssr index-name="articles" :search-client="searchClient"&gt;
    ...
&lt;/ais-instant-search-ssr&gt;
...</code></pre>

Here, we to replace `ais-instant-search` with `ais-instant-search-ssr`.

## Conclusion

We’ve successfully built a Nuxt site with some content handled by Nuxt Content and integrated a simple Algolia search into our site. We’ve also managed to optimize it for SSR. I have a link to the source code of the project in this tutorial and a demo site deployed on Netlify, the links are down below.

We have tons of options available to customize and provide a rich search experience now that the basics are out of the way. [The Algolia widgets showcase](https://www.algolia.com/doc/guides/building-search-ui/widgets/showcase/vue/) is a great way to explore those options and widgets. You’ll also find more information on the [widgets](https://www.algolia.com/doc/api-reference/widgets) used in this tutorial. 

### GitHub Source Code

- You can check out the source code [here](https://github.com/miracleonyenma/algolia-nuxt).
- You can play with the demo on [https://algolia-nuxtx.netlify.app/](https://algolia-nuxtx.netlify.app/).

### Further Reading

Here are some links that I think you will find useful:

- [Create a Blog with Nuxt Content](https://nuxtjs.org/blog/creating-blog-with-nuxt-content) by Debbie O’Brien
- [`@nuxt/content` Module](https://content.nuxtjs.org/)
- [Tailwindcss docs](https://tailwindcss.com/docs)
- [Vue InstantSearch](https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/vue/)

{{< signature "ks, vf, yk, il" >}}

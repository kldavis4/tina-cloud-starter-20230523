---
title: 'Differences Between Static Generated Sites And Server-Side Rendered Apps'
slug: differences-static-generated-sites-server-side-rendered-apps
author: timi-omoyeni
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f6d94e9-5c75-438c-9016-b5d33ffd4a1e/differences-static-generated-sites-server-side-rendered-apps.png
date: 2020-07-02T12:00:00.000Z
summary: >-
  Statically generated sites or pre-rendering and server-side rendered applications are two modern ways to build front-end applications using JavaScript frameworks. These two modes, yet different, are often mixed up as the same thing and in this tutorial, we’re going to learn about the differences between them. 
description: >-
  Statically generated sites or pre-rendering and server-side rendered applications are two modern ways to build front-end applications using JavaScript frameworks. These two modes, yet different, are often mixed up as the same thing and in this tutorial, we’re going to learn about the differences between them. 
categories:
  - Apps
  - Next.js
  - Nuxt.js
  - JavaScript
  - Generators
  - Static Generators
---

JavaScript currently enables you to build three types of applications: single-page applications (SPAs), pre-rendered or static-generated sites, and server-side-rendered applications. SPAs come with many [challenges](https://en.wikipedia.org/wiki/Single-page_application#Challenges_with_the_SPA_model), one of which is search engine optimization (SEO). Possible solutions are to make use of a <a href="#static-site-generator">static-site generator</a> or <a href="#server-side-rendering">server-side rendering</a> (SSR).

In this article, we’ll go over these, looking at their pros and cons to get a balanced view. We’ll look at what static generation is, as well as frameworks that help us create static-generated sites, such as [Gatsby](https://www.gatsbyjs.org/) and [VuePress](https://www.smashingmagazine.com/2019/08/vuepress-documentation/). We’ll learn what a server-side-rendered application is, as well as learn about frameworks for creating one, such as [Next.js](https://nextjs.org/) and [Nuxt.js](https://nuxtjs.org/). Finally, we’ll cover the differences between these two methods and see which you should use to build your next application.

You can find all of the code snippets in this article [on GitHub](https://github.com/Timibadass/ssgVSssr).

## What Is a Static-Site Generator?

A static-site generator (SSG) is a software application that creates HTML pages from templates or components and a given content source. Give it some text files and content, and the generator will give you back a complete website; this completed website is referred to as a static-generated site. This means that the website’s pages are generated at build time, and their contents do not change unless you add new content or components and then **rebuild** &mdash; you have to rebuild the website if you want it to be updated with the new content.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da1ef4c9-9d18-49c4-9d01-2defed1af3df/ssg-ssr-01-ssg.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da1ef4c9-9d18-49c4-9d01-2defed1af3df/ssg-ssr-01-ssg.png" sizes="100vw" caption="How static-site generation works (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da1ef4c9-9d18-49c4-9d01-2defed1af3df/ssg-ssr-01-ssg.png'>Large preview</a>)" alt="Diagram explaining how static-site generation works" >}}

This approach is good for building applications whose content does not change often. So, you wouldn’t necessarily use it for a website that has to be modified according to the user or one that has a lot of user-generated content. However, a blog or personal website would be an ideal use. Let’s look at some advantages of static-generated sites.

### Pros

- **Speed**  
Because all of your website’s pages and content will be generated at build time, you do not have to worry about API calls to a server for content, which will make your website very fast.
- **Deployment**  
Once your static site has been generated, you will be left with static files. Hence, it can be easily deployed to a platform such as [Netlify](https://www.netlify.com/).
- **Security**  
A static-generated site solely comprises static files, with no database for an attacker to exploit by injecting malicious code. So, vulnerability to a cyber attack is minimal.
- **Verson control**  
You can use version control software (such as Git) to manage and track changes to your content. This comes in handy when you want to roll back changes made to the content.

### Cons

- If the content changes too quickly, it can be hard to keep up.
- To update content, you have to rebuild the website.
- The build time increases according to the size of the application.

Examples of static-site generators are [Gatsby](https://www.gatsbyjs.org/) and [VuePress](https://vuepress.vuejs.org/). Let’s look at how to create a static site using these two generators.

{{% feature-panel %}}

### Gatsby

According to the [official website](https://www.gatsbyjs.org/):

<blockquote>“Gatsby is a free and open-source framework based on React that helps developers build blazing-fast websites and apps.”</blockquote>

This means that developers who are familiar with [React](https://reactjs.org/) will find it easy to get started with Gatsby.

To use this generator, you first have to install it using npm:

<pre><code class="language-bash">npm install -g gatsby-cli
</code></pre>

This will install Gatsby globally on your machine. You have to run this command only once on your machine. Once the installation is complete, you can create your first static site using the following command:

<pre><code class="language-bash">gatsby new demo-gatsby
</code></pre>

This will create a new Gatsby project, which I have named `demo-gatsby`. Following this, you can start up your app’s server by running the following command:

<pre><code class="language-bash">cd demo-gatsby
gatsby develop
</code></pre>

Your Gatsby application should be running on [localhost:8000](https://localhost:8000/).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8462acef-ad49-4ae0-869e-2cf9694080f5/ssg-ssr-02-gatsby-landing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8462acef-ad49-4ae0-869e-2cf9694080f5/ssg-ssr-02-gatsby-landing.png" sizes="100vw" caption="Gatsby default starter page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8462acef-ad49-4ae0-869e-2cf9694080f5/ssg-ssr-02-gatsby-landing.png'>Large preview</a>)" alt="Gatsby default landing page" >}}

The folder structure of the app looks like this:

<pre><code class="language-bash">--| gatsby-browser.js  
--| LICENSE        
--| README.md
--| gatsby-config.js
--| node_modules/  
--| src/
----| components
----| pages
----| images
--| gatsby-node.js     
--| package.json   
--| yarn.lock
--| gatsby-ssr.js      
--| public/
----| icons
----| page-data
----| static
</code></pre>

For this tutorial, we’re only going to look at the `src/pages` folder. This folder contains files that will be generated into routes on the website.

To test this, add a new file (`newPage.js`) to this folder:

<div class="break-out">

 <pre><code class="language-javascript">import React from "react"
import { Link } from "gatsby"
import Layout from "../components/layout"
import SEO from "../components/seo"
const NewPage = () =&gt; (
  &lt;Layout&gt;
    &lt;SEO title="My new page" /&gt;
    &lt;h1&gt;Hello Gatsby&lt;/h1&gt;
    &lt;p&gt;This is my first Gatsby page&lt;/p&gt;
    &lt;button&gt;
      &lt;Link to='/'&gt;Home&lt;/Link&gt;
    &lt;/button&gt;
  &lt;/Layout&gt;
)
export default NewPage
</code></pre>
</div>

Here, we are importing `React` from the `react` package, so when your code is transpiled to pure JavaScript, references to `React` will appear there. We’re also importing a `Link` component from `gatsby`; it is one of React’s route tags that is used in place of the native anchor tag (`<a href="#">Link</a>`). It accepts a `to` prop, which takes a route as a value.

We imported a `Layout` component, which was added to the app by default. This component handles the layout of pages nested inside it. We also imported the `SEO` component into this new file. This component accepts a `title` prop and configures this value as part of your page’s meta data. Finally, we exported the function `NewPage`, which returns [JSX](https://reactjs.org/docs/introducing-jsx.html) containing the new page’s content.

In your `index.js` file, add a link to this new page we just created:

<div class="break-out">

 <pre><code class="language-javascript">import React from "react"
import { Link } from "gatsby"
import Layout from "../components/layout"
import Image from "../components/image"
import SEO from "../components/seo"
const IndexPage = () =&gt; (
  &lt;Layout&gt;
    &lt;SEO title="Home" /&gt;
    &lt;h1&gt;Hi people&lt;/h1&gt;
    &lt;p&gt;Welcome to your new Gatsby site.&lt;/p&gt;
    &lt;p&gt;Now go build something great.&lt;/p&gt;
    &lt;div style={{ maxWidth: `300px`, marginBottom: `1.45rem` }}&gt;
      &lt;Image /&gt;
    &lt;/div&gt;
    &lt;Link to="/page-2/"&gt;Go to page 2&lt;/Link&gt;
    {/&#42; new link &#42;/}
    &lt;button&gt;
      &lt;Link to="/newPage/"&gt;Go to new page&lt;/Link&gt;
    &lt;/button&gt;
  &lt;/Layout&gt;
)
export default IndexPage
</code></pre>
</div>

Here, we’ve imported the same components that were used in the `newPage.js` file, and they perform the same function in this file. We’ve also imported an `Image` component from our `components` folder. This component is added by default to the Gatsby application; it helps with lazy loading images and serving lower file sizes. Finally, we’ve exported the `IndexPage` function, which returns JSX containing our new link and some default content.

Now, if we open the browser, we should see our new link at the bottom of the page.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e52d01b7-d8f2-4fb1-85d4-8ab717e7ecb6/ssg-ssr-03-gatsby-newlink.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e52d01b7-d8f2-4fb1-85d4-8ab717e7ecb6/ssg-ssr-03-gatsby-newlink.png" sizes="100vw" caption="Gatsby landing page with new link (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e52d01b7-d8f2-4fb1-85d4-8ab717e7ecb6/ssg-ssr-03-gatsby-newlink.png'>Large preview</a>)" alt="Gatsby default landing page with link to new page" >}}

And if you click on “Go to new page”, it should take you to your newly added page.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/070a4eb1-63e3-448e-8239-944d5aab0372/ssg-ssr-04-gatsby-hello.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/070a4eb1-63e3-448e-8239-944d5aab0372/ssg-ssr-04-gatsby-hello.png" sizes="100vw" caption="New Gatsby page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/070a4eb1-63e3-448e-8239-944d5aab0372/ssg-ssr-04-gatsby-hello.png'>Large preview</a>)" alt="New page containing some text" >}}

### VuePress

VuePress is a static-site generator powered by [Vue.js](https://vuejs.org/), [vue-router](https://github.com/vuejs/vue-router), and [webpack](https://webpack.js.org/). It requires little to no configuration to get started. While there are many static-site generators, VuePress stands out from the pack for a single reason: Its primary purpose is to make it easier for developers to create and maintain great documentation for their projects.

To use VuePress, you first have to install it:

<pre><code class="language-bash">// Globally…
yarn global add vuepress # OR npm install -g vuepress

// Or in an existing project…
yarn add -D vuepress # OR npm install -D vuepress
</code></pre>

Once the installation process is done, you can run the following command in your command-line interface (CLI):

<pre><code class="language-bash"># Create the project folder
mkdir demo-vuepress && cd demo-vuepress

# Create a Markdown file
echo '# Hello VuePress' > README.md

# Start writing
vuepress dev
</code></pre>

Here, we’ve created a folder for our VuePress application, added a `README.md` file with `# Hello VuePress` as its only content, and, finally, started up the server.

Once this is done, our application should be running on [localhost:8080](https://localhost:8080), and we should see this in the browser:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccbf38b9-0c3b-46d7-be8f-6d9882577be4/ssg-ssr-05-vuepress-landing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccbf38b9-0c3b-46d7-be8f-6d9882577be4/ssg-ssr-05-vuepress-landing.png" sizes="100vw" caption="VuePress landing page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccbf38b9-0c3b-46d7-be8f-6d9882577be4/ssg-ssr-05-vuepress-landing.png'>Large preview</a>)" alt="A VuePress web page with text saying “Hello VuePress”" >}}

VuePress supports Vue.js’ syntax and markup in this file. Update the `README.md` file with the following:

<div class="break-out">

 <pre><code class="language-md"># Hello VuePress
&#95;VuePress Rocks&#95;
&gt; &#42;&#42;Yes!&#42;&#42;
&#95;It supports JavaScript interpolation code&#95;
&gt; &#42;&#42;{{new Date()}}&#42;&#42;
&lt;p v-for="i of ['v','u', 'e', 'p', 'r', 'e', 's', 's']"&gt;{{i}}&lt;/p&gt;
</code></pre>
</div>

If you go back to the browser, the page should look like this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34a69122-e4c2-4651-8ed7-c049842eb845/ssg-ssr-06-vuepress-updated.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34a69122-e4c2-4651-8ed7-c049842eb845/ssg-ssr-06-vuepress-updated.png" sizes="100vw" caption="Updated VuePress page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34a69122-e4c2-4651-8ed7-c049842eb845/ssg-ssr-06-vuepress-updated.png'>Large preview</a>)" alt="Updated VuePress page" >}}

To add a new page to your VuePress website, add a new Markdown file to the root directory, and name it whatever you want the route to be. In this case, I’ve gone ahead with naming it `Page-2.md` and added the following to the file:

<div class="break-out">

 <pre><code class="language-md"># Hello World
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat.
</code></pre>
</div>

Now, if you navigate to `/page-2` in the browser, you should see this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b4f2c07-742e-4092-88c9-b3d6f920c482/ssg-ssr-07-vuepress-hellopage.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b4f2c07-742e-4092-88c9-b3d6f920c482/ssg-ssr-07-vuepress-hellopage.png" sizes="100vw" caption="A “Hello World” page in VuePress (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b4f2c07-742e-4092-88c9-b3d6f920c482/ssg-ssr-07-vuepress-hellopage.png'>Large preview</a>)" alt="A VuePress web page containing “Hello world”" >}}

{{% ad-panel-leaderboard %}}

## What Is Server-Side Rendering?

Server-side rendering (SSR) is the process of rendering web pages on a server and passing them to the browser (client-side), instead of rendering them in the browser. SSR sends a fully rendered page to the client; the client’s JavaScript bundle takes over and enables the SPA framework to operate.

This means that if your application is server-side rendered, the content is fetched from the server and passed to the browser to be displayed to the user. Client-side rendering is different: The user would have to navigate to the page before the browser fetches data from the server, meaning that the user would have to wait for some seconds to pass before the browser is served with the content for that page. Applications that have SSR enabled are called server-side-rendered applications.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94ac796d-f3fd-4984-8d62-5e3ca2134f13/ssg-ssr-08-ssr.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94ac796d-f3fd-4984-8d62-5e3ca2134f13/ssg-ssr-08-ssr.png" sizes="100vw" caption="How server-side rendering works (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94ac796d-f3fd-4984-8d62-5e3ca2134f13/ssg-ssr-08-ssr.png'>Large preview</a>)" alt="A diagram explaining how server-side rendering works" >}}

This approach is good if you’re building a complex application that requires user interaction, that relies on a database, or whose content changes often. If the content changes often, then users would need to see the updates right away. The approach is also good for applications that tailor content according to who is viewing it and that store user data such as email addresses and user preferences, while also attending to SEO. An example would be a large e-commerce or social media platform. Let’s look at some of the advantages of SSR for your applications.

### Pros

- The content is up to date because it is fetched on the go.
- The website loads quickly because the browser fetches content from the server before rendering it for the user.
- Because the JavaScript is rendered server-side, the user’s device has little bearing on the loading time of the page, making for better performance.

### Cons

- More API calls to the server are made, because they’re made per request.
- The website cannot be deployed to a static content delivery network (CDN).

Examples of frameworks that offer SSR are <a href="#nextjs">Next.js</a> and <a href="nuxtjs">Nuxt.js</a>.

### Next.js

Next.js is a React framework that enables you to build static websites, server-side rendered applications, and the like. Because it is built on React, knowledge of React is required to use the framework.

To create a Next.js app, run the following:

<pre><code class="language-bash">npm init next-app
# or
yarn create next-app
</code></pre>

You will be prompted to name your application; I named mine `demo-next`. The next option is to select a template; I selected the default starter app. Then, it begins to set up the application. When that is done, we can start our work on the application.

<pre><code class="language-bash">cd demo-next
yarn dev
# or npm run dev
</code></pre>

Your application should be running on [localhost:3000](https://localhost:3000/), and you should see this in the browser:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6105864e-abf6-4e9e-b815-7e112c0183db/ssg-ssr-09-nextjs-landing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6105864e-abf6-4e9e-b815-7e112c0183db/ssg-ssr-09-nextjs-landing.png" sizes="100vw" caption="Next.js landing page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6105864e-abf6-4e9e-b815-7e112c0183db/ssg-ssr-09-nextjs-landing.png'>Large preview</a>)" alt="Default Next.js landing page" >}}

The page that is being rendered can be found in `pages/index.js`. So, if you open this file and modify the JSX inside the `Home` function, it would be reflected in the browser. Replace the JSX with this:

<div class="break-out">

 <pre><code class="language-javascript">import Head from 'next/head'
export default function Home() {
  return (
    &lt;div className="container"&gt;
      &lt;Head&gt;
        &lt;title&gt;Hello Next.js&lt;/title&gt;
        &lt;link rel="icon" href="/favicon.ico" /&gt;
      &lt;/Head&gt;
      &lt;main&gt;
        &lt;h1 className="title"&gt;
          Welcome to &lt;a href="https://nextjs.org"&gt;Next.js!&lt;/a&gt;
        &lt;/h1&gt;
        &lt;p className='description'&gt;Next.js Rocks!&lt;/p&gt;
      &lt;/main&gt;
      &lt;style jsx&gt;{`
        main {
          padding: 5rem 0;
          flex: 1;
          display: flex;
          flex-direction: column;
          justify-content: center;
          align-items: center;
        }
        .title a {
          color: #0070f3;
          text-decoration: none;
        }
        .title a:hover,
        .title a:focus,
        .title a:active {
          text-decoration: underline;
        }
        .title {
          margin: 0;
          line-height: 1.15;
          font-size: 4rem;
        }
        .title,
        .description {
          text-align: center;
        }
        .description {
          line-height: 1.5;
          font-size: 1.5rem;
        }
      `}&lt;/style&gt;
      &lt;style jsx global&gt;{`
        html,
        body {
          padding: 0;
          margin: 0;
          font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto,
            Oxygen, Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue,
            sans-serif;
        }
        * {
          box-sizing: border-box;
        }
      \`}&lt;/style&gt;
    &lt;/div&gt;
  )
}
</code></pre>
</div>

In this file, we’re making use of Next.js’ [`Head` component](https://nextjs.org/docs/api-reference/next/head) to set the meta data’s title and favicon for our page. We’re also exporting a `Home` function that returns JSX containing our page’s content. This JSX contains the `Head` component, together with the page’s main content. It also contains two style tags, one for styling this page and the other for global styling of the app.

Now, you should see that the content in the app has changed to this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b6dea03-247f-4945-b0d1-3b21c6dcbafa/ssg-ssr-10-nextjs-updated.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b6dea03-247f-4945-b0d1-3b21c6dcbafa/ssg-ssr-10-nextjs-updated.png" sizes="100vw" caption="Updated landing page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b6dea03-247f-4945-b0d1-3b21c6dcbafa/ssg-ssr-10-nextjs-updated.png'>Large preview</a>)" alt="Next.js landing page containing “Welcome to Next.js” text" >}}

If we wanted to add a page to our app, we would have to add a file in the `/pages` folder. Routes are automatically created based on the `/pages` folder structure. Suppose you have a folder structure that looks like this:

<pre><code class="language-bash">--| pages
----| index.js ==> '/'
----| about.js ==> '/about'
----| projects
------| next.js ==> '/projects/next'
</code></pre>

In the `pages` folder, add a new file and name it `hello.js`. Then add the following to it:

<div class="break-out">

 <pre><code class="language-javascript">import Head from 'next/head'
export default function Hello() {
  return (
    &lt;div&gt;
       &lt;Head&gt;
        &lt;title&gt;Hello World&lt;/title&gt;
        &lt;link rel="icon" href="/favicon.ico" /&gt;
      &lt;/Head&gt;
      &lt;main className='container'&gt;
        &lt;h1 className='title'&gt;
         Hello &lt;a href="https://en.wikipedia.org/wiki/Hello_World_(film)"&gt;world&lt;/a&gt;
        &lt;/h1&gt;
        &lt;p className='subtitle'&gt;Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatem provident soluta, sit explicabo impedit nobis accusantium? Nihil beatae, accusamus modi assumenda, optio omnis aliquid nobis magnam facilis ipsam eum saepe!&lt;/p&gt;
      &lt;/main&gt;
      &lt;style jsx&gt; {`

      .container {
        margin: 0 auto;
        min-height: 100vh;
        max-width: 800px;
        text-align: center;
      }
      .title {
        font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
          "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
        display: block;
        font-weight: 300;
        font-size: 100px;
        color: #35495e;
        letter-spacing: 1px;
      }
      .subtitle {
        font-weight: 300;
        font-size: 22px;
        color: #526488;
        word-spacing: 5px;
        padding-bottom: 15px;
      }
      \`} &lt;/style&gt;
    &lt;/div&gt;
  )
}
</code></pre>
</div>

This page is identical to the landing page we already have. We’ve only changed the content and added new styling to the JSX. Now, if we visit [localhost:3000/hello](https://localhost:3000/hello), we should see our new page:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7422acd6-6b80-4f40-ad8d-f310671f14f4/ssg-ssr-11-nextjs-hellopage.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7422acd6-6b80-4f40-ad8d-f310671f14f4/ssg-ssr-11-nextjs-hellopage.png" sizes="100vw" caption="A “Hello World” page in Next.js (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7422acd6-6b80-4f40-ad8d-f310671f14f4/ssg-ssr-11-nextjs-hellopage.png'>Large preview</a>)" alt="A Next.js web page containing “Hello world”" >}}

Finally, we need to add a link to this new page on the `index.js` page. To do this, we’ll make use of [Next.js’ `Link`](https://nextjs.org/docs/api-reference/next/link) component. We have to import it first.

<pre><code class="language-javascript"># index.js
import Link from 'next/link'

#Add this to your JSX
&lt;Link href='/hello'&gt;
&lt;Link href='/hello'&gt;
  &lt;a&gt;Next&lt;/a&gt;
&lt;/Link&gt;
</code></pre>

This `Link` component is how we add links to pages created in a Next.js application.

If we go back to our home page and click on this link, it would take us to our `/hello` page.

{{% ad-panel-leaderboard %}}

### Nuxt.js

As stated in the [official documentation](https://nuxtjs.org/guide):

<blockquote>“Nuxt is a progressive framework based on Vue.js to create modern web applications. It is based on Vue.js official libraries (vue, vue-router and vuex) and powerful development tools (webpack, Babel and PostCSS). Nuxt’s goal is to make web development powerful and performant with a great developer experience in mind.”</blockquote>

Nuxt.js is based on Vue.js, so Vue.js developers will find it easy to get started with, and knowledge of Vue.js is required to use it.

To create a Nuxt.js app, run the following command in your CLI:

<pre><code class="language-bash">yarn create nuxt-app &lt;project-name&gt;
# or npx
npx create-nuxt-app &lt;project-name&gt;
</code></pre>

This will prompt you to select a name, along with some other options. I named mine `demo-nuxt` and selected the defaults for the other options. Then, you can open your app’s folder and open `pages/index.vue`. Every file in this folder is turned into a route, and so our landing page will be controlled by the `index.vue` file. Update it with the following:

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;div class="container"&gt;
    &lt;div&gt;
      &lt;logo /&gt;
      &lt;h1 class="title"&gt;
        Hello Nuxt.js
      &lt;/h1&gt;
      &lt;h2 class="subtitle"&gt;
        Nuxt.js Rocks!
      &lt;/h2&gt;
      &lt;div class="links"&gt;
        &lt;a
          href="https://nuxtjs.org/"
          target="&#95;blank"
          class="button--green"
        &gt;
          Documentation
        &lt;/a&gt;
        &lt;a
          href="https://github.com/nuxt/nuxt.js"
          target="&#95;blank"
          class="button--grey"
        &gt;
          GitHub
        &lt;/a&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
import Logo from '~/components/Logo.vue'
export default {
  components: {
    Logo
  }
}
&lt;/script&gt;
&lt;style&gt;
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}
.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
.links {
  padding-top: 15px;
}
&lt;/style&gt;
</code></pre>
</div>

Now, run the application:

<pre><code class="language-bash">cd demo-nuxt
# start your applicatio
yarn dev # or npm run dev
</code></pre>

Your application should be running on [localhost:3000](https://localhost:3000/), and you should see this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8477dfb2-ea85-4fb6-a502-78e3a451f0a5/ssg-ssr-12-nuxt-landing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8477dfb2-ea85-4fb6-a502-78e3a451f0a5/ssg-ssr-12-nuxt-landing.png" sizes="100vw" caption="Nuxt.js landing page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8477dfb2-ea85-4fb6-a502-78e3a451f0a5/ssg-ssr-12-nuxt-landing.png'>Large preview</a>)" alt="Default Nuxt.js landing page" >}}

We can see that the page displays the content that we added to `index.vue`. The router structure works the same way that Next.js’ router works: It renders every file in the `/pages` folder into a page. So, let’s add a new page (`hello.vue`) to our application:

<div class="break-out">

 <pre><code class="language-javascript">&lt;template&gt;
  &lt;div&gt;
    &lt;h1&gt;Hello world!&lt;/h1&gt;
    &lt;p&gt;Lorem ipsum dolor sit amet, consectetur adipisicing elit. Id ipsa vitae tempora perferendis, voluptate a accusantium itaque vel ex, provident autem quod rem saepe ullam hic explicabo voluptas, libero distinctio?&lt;/p&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
export default {};
&lt;/script&gt;
&lt;style&gt;
&lt;/style&gt;
</code></pre>
</div>

If you open [localhost:3000/hello](https://localhost:3000/hello), you should see the new page in the browser.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/543da7f9-208d-4409-b4b0-15692a0849f9/ssg-ssr-13-nuxt-hellopage.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/543da7f9-208d-4409-b4b0-15692a0849f9/ssg-ssr-13-nuxt-hellopage.png" sizes="100vw" caption="“Hello world” page in Nuxt.js (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/543da7f9-208d-4409-b4b0-15692a0849f9/ssg-ssr-13-nuxt-hellopage.png'>Large preview</a>)" alt="A Nuxt.js web page containing “Hello world”" >}}

## Taking a Closer Look at the Differences

Now that we have looked at both static-site generators and server-side rendering, and we understand how to get started with them by using some popular tools, let’s look at the differences between them.

<figure class="scroll-pane">
<table data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Static-Site Generation</th>
      <th>Server-Side Rendering</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Can easily be deployed to a static CDN</td>
      <td>Cannot be deployed to a static CDN</td>
    </tr>
    <tr>
      <td>Content and pages are generated at build time</td>
      <td>Content and pages are generated per request</td>
    </tr>
    <tr>
      <td>Content can get stale quickly</td>
      <td>Content is always up to date</td>
    </tr>
    <tr>
      <td>Fewer API calls, because it only makes them at build time</td>
      <td>Makes API calls each time a new page is visited</td>
    </tr>
  </tbody>
</table>
</figure>

## Conclusion

We can see why it is so easy to think that static-generated sites and server-side-rendered applications are the same. And we know the differences between them. Try to learn more about how to build both in order to fully understand the differences between them.

### Further Resources

Here are some useful links to help you get started in no time.

- [Gatsby](https://www.gatsbyjs.org/)
- [VuePress](https://vuepress.vuejs.org/)
- “[VuePress: Documentation Made Easy](https://www.smashingmagazine.com/2019/08/vuepress-documentation/),” Ben Hong, Smashing Magazine
- [Next.js](https://nextjs.org/)
- “[Why Do People Use a Static-Site Generator?](https://www.quora.com/Why-do-people-use-a-static-site-generator/answer/Meenu-Thariyan-1?ch=10&share=7cee655d&srid=XMrjg),” Quora
- “[Static Site Generator](https://www.gatsbyjs.org/docs/glossary/static-site-generator/),” Gatsby
- “[An Introduction to VuePress](https://www.digitalocean.com/community/tutorials/vuejs-vuepress-introduction),” Joshua Bemenderfer, DigitalOcean
- “[What Is Server-Side Rendering?](https://www.educative.io/edpresso/what-is-server-side-rendering),” Edpresso, Educative.io
- “[What Is A Static Site Generator? And 3 Ways to Find the Best One ](https://www.netlify.com/blog/2020/04/14/what-is-a-static-site-generator-and-3-ways-to-find-the-best-one/),” Phil Hawksworth, Netlify
- “[The Benefits of Server Side Rendering Over Client Side Rendering](https://medium.com/walmartlabs/the-benefits-of-server-side-rendering-over-client-side-rendering-5d07ff2cefe8),” Alex Grigoryan, Medium

{{< signature "ks, ra, il, al" >}}

---
title: 'Migration From jQuery to Next.js: A Guide'
slug: migration-jquery-next-js-guide
author: sam-robbins
image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cee417f-9daf-47d5-957c-0299c43b292d/rewriting-a-jquery-site-to-nextjs-card.jpg
date: 2022-08-03T12:00:00.000Z
summary: >-
  This guide will show you how to migrate your jQuery site to [React](/category/React) with [Next.js](/category/next.js) – which is a significant undertaking, especially for big code bases. However, this migration allows you to use newer concepts (such as data fetching at build time) to help with our code's performance and maintainability. 
description: >-
  We’re going to walk through how to migrate your site from jQuery to [React](/category/React) with [Next.js](/category/next.js). This will help with performance and the maintainability of your code.
categories:
  - Coding
  - JavaScript
  - NextJS
  - React
---
jQuery has served developers well for many years. However, libraries (like React) and Frameworks (like Next.js) are now bringing us more modern features to help with our code's performance and maintainability. This guide will show you how to **rewrite your jQuery site** using Next.js to take advantage of all these new features, such as client-side routing for smoother transitions and the ability to separate code into components to make it more reusable.

## Getting started

The easiest way to get started with a Next.js is to run `npx create-next-app`. This will **scaffold a project** for you. However, to understand what this command does, we’ll create our application from scratch.

First, we’ll create our Next.js project using `npm init`. You can proceed with the default settings, as we will change them later. Then, we want to install React and Next.js using:

<pre><code class="language-bash">npm install react react-dom next
</code></pre>

Next up, we can open the `package.json` file and replace the default `scripts` with:

<pre><code class="language-bash">"scripts": {
    "dev": "next",
    "build": "next build",
    "start": "next start"
}
</code></pre>

This allows you to run `npm run dev` to start the development server; `npm run build` to build your application; and `npm run start` to start a server of that built application.

To add pages &mdash; like you would `index.html` with jQuery &mdash; create a directory named `pages` and create a file named `index.jsx` in it. Inside this file, place the following code:

<pre><code class="language-javascript">export default function Index() {
  return &lt;h1&gt;Hello World&lt;/h1&gt; ;
}
</code></pre>
    

Now, by running `npm run start` and navigating to `localhost:3000`, you should see a `h1` tag displayed. The name of this function isn’t important, so you can call it whatever you want. However, don’t use an anonymous arrow function, as this will prevent [fast refresh](https://nextjs.org/docs/basic-features/fast-refresh) from working.

{{% feature-panel %}}
## CSS

In jQuery, you can specify CSS by page, importing different stylesheets for different pages. This is also possible in Next.js using the `next/head` component and a `link` tag the same way as jQuery. Anyhow, there are more performance-friendly ways to to this in Next.js.

### Global Stylesheet

The first way is with a global stylesheet. To do so, we need to create a custom `App` by making the file `_app.js` inside the `pages` directory. The starting point for this file is as follows:

<pre><code class="language-javascript">function MyApp({ Component, pageProps }) {
  return &lt;Component {...pageProps} /&gt;
}

export default MyApp
</code></pre>

At the top of this file, you can add an import statement and import any CSS file you want. For example, if you created a separate folder at the root level called `styles` and put `main.css` in it, then you would add:

<pre><code class="language-coffeescript">import "../styles/main.css"
</code></pre>

Now, whatever you put inside this file will be applied throughout your application.

### CSS Modules

The next option is CSS modules &mdash; which allows you to specify CSS *anywhere* in your application. They will create **unique class names** from the classes you provide, so you can use a same class name in multiple places in your application’s code.

Expanding the initial *hello world* example, you could create a file `index.module.css` in the same directory and then write the import:

<pre><code class="language-coffeescript">import styles from "./index.module.css"
</code></pre>

Afterwards, if you were to define a `heading` class in the CSS file, you could do the following:

<pre><code class="language-javascript">export default function Index() {
  return &lt;h1 className={styles.heading}&gt;Hello World&lt;/h1&gt; ;
}
</code></pre>

and those styles will be applied only to that element.

### Styled JSX

The final built-in option is **styled JSX**. This is most similar to including a `<style>` tag at the top of your page to define some styles. Simply add `jsx` to the `<style>` tag, and use a template string inside, like this:

<pre><code class="language-xml">&lt;style jsx&gt;{`
  .heading {
      font-weight: 700
  `}&lt;/style&gt;
</code></pre>

This option has the advantage of being changeable at runtime. For instance, if you wanted to supply the font weight in your component props, you could do:

<pre><code class="language-xml">&lt;style jsx&gt;{`
  .heading{
      font-weight: ${props.fontWeight}
  `}&lt;/style&gt;
</code></pre>

The one disadvantage of this method is that it introduces **additional runtime JavaScript** into your application, increasing the size by 12kb (3kb gzipped).

## Events

In jQuery, you might have events set up to respond to DOM elements. To give you an idea, you might want to execute code when a `p` tag is clicked and do so like this:

<pre><code class="language-javascript">$( "p" ).click(function() {
    console.log( "You clicked a paragraph!" );
});
</code></pre>

Instead, React uses **event handlers** &mdash; which you might have seen in HTML &mdash; like `onclick`. Note that React uses camelCase instead, and so `onclick` should be referenced as `onClick`. Therefore, rewriting this small example into React would look like this:

<pre><code class="language-javascript">export default function Index() {
  function clickParagraph(){
    console.log("You clicked a paragraph!");
  }
  return &lt;p onClick={clickParagraph}&gt;Hello World&lt;/p&gt;;
}
</code></pre>

Each method comes with its advantages and disadvantages. In jQuery, it is easy to have something happen for *all* paragraphs, whereas in React, you have to specify *per* paragraph. However, for larger codebases, having to specify makes it easy to see what will happen with the interaction with any element, where you may have forgotten about the jQuery function.

## Effects

Effects are used in jQuery to **show and hide content**. You might have something like this already:

<pre><code class="language-javascript">$( "p" ).hide();
</code></pre>

In React, this behavior is implemented using **conditional rendering**. You can see this by combining it with the replacement for events we just saw:

<pre><code class="language-php">import {useState} from "react"
export default function Index() {
  const [show, setShow] = useState(true);
  function clickButton(){
    setShow(false)
  }
  return (
    &lt;div&gt;
      &lt;h1&gt;Hello world&lt;/h1&gt;
      {show && &lt;button onClick={clickButton}&gt;Click me&lt;/button&gt;}
    &lt;/div&gt;
  )
}
</code></pre>

When you click this button, it will change the value of `show` to `false` and so, the statement won’t render anything. This can be expanded with the conditional operator to show one thing or another, depending on the value like this:

<pre><code class="language-sql">show ? &lt;p&gt;Show this if show is true&lt;/p&gt; : &lt;p&gt;Show this if show is false&lt;/p&gt;
</code></pre>

## Data Fetching

In jQuery, Ajax is used for **external data fetching** without reloading. In React, this can be done by using the `useEffect` hook. For this example, we’ll fetch the exchange rate from a public API when the page loads:

<pre><code class="language-php">import { useState, useEffect } from "react";
export default function Index() {
  const [er, setEr] = useState(true);
  useEffect(async () => {
    const result = await fetch("https://api.exchangerate.host/latest");
    const exchangerate = await result.json();
    setEr(exchangerate.rates["GBP"]);
  }, []);
  return (
    &lt;div&gt;
      &lt;h1&gt;Hello world&lt;/h1&gt;
      &lt;p&gt;Exchange rate: {er}&lt;/p&gt;
    &lt;/div&gt; 
  );
}
</code></pre>

`useEffect` takes in a function and a dependency array. The function does the data fetching, using `async` as the `fetch` API asynchronously. We can then set any state we want in there, and it will be updated on the page. The dependency array determines which value changes will run the function. In this case, it’s set to an empty array which means that the function will only run when the page first loads.

Beyond this, Next.js also provides **options for fetching data on the server** or at build time. For build time data fetching, the function `getStaticProps` can be used. This function provides an improvement in performance as the data can be provided with the page &mdash; rather than waiting on an external service. To use it, create this function in a **page** as it doesn’t work in components.

<pre><code class="language-javascript">export async function getStaticProps() {
  return {
    props: {},
  }
}
</code></pre>

You can perform any data fetching you want before the return, and after that, pass the data through to the page under `props` &mdash; then, the data is provided to the page and can be accessed under the props.

By replacing the function name from `getStaticProps` to `getServerSideProps`, the function will be called **on every request**, giving you the flexibility to use Node.js functions if needed. It also allows you to make many data requests on the server and to process them to reduce the bandwidth used by the client. 

You also have the option of a middle ground between the two called [*Incremental Static Regeneration*](https://www.smashingmagazine.com/2021/04/incremental-static-regeneration-nextjs/). This option will generate a static page in the same way as `getStaticProps`, but it allows you to specify a **revalidation period** &mdash; which will regenerate the page when a request comes in at most as often as the period you specify. To do this, alongside props, you should also include a `revalidate` key with the time in seconds you want. 


## Objects into DOM elements

With jQuery, you have to be careful with which method you use for turning an object into DOM elements. The most common example of this is to create a list of items because, with jQuery, a loop over items would add each to the DOM one by one. With React, the virtual DOM is used to create **diffs of the new state** from the current one. This means that despite adding items in a loop, they are added to the real DOM as one operation.

This is done using the `map` function in JavaScript, where you can map each item to some JSX.

<pre><code class="language-php">export default function Index() {
  const fruits = ["Apple", "Orange", "Pear"];
  return (
    &lt;div&gt;
      &lt;h1&gt;Hello world&lt;/h1&gt;
      &lt;ul&gt;
        {fruits.map((fruit) => (
          &lt;li key={fruit}&gt;{fruit}&lt;/li&gt;
        ))}
      &lt;/ul&gt;
    &lt;/div&gt;
  );
}
</code></pre>    

Notice that the element inside the `map` needs a `key` prop. This is used in the diffing process discussed above, making it easy for React to distinguish between each element, so each of these should be unique. 

## Deffereds

The use of deferreds in jQuery can be replaced with the native JavaScript `promise` functionality. The syntax for deffereds was designed to **mirror the functionality of promises**, so the syntax should be familiar and not require too much alteration. One example of where deffereds might be used is in **data fetching**. If you do this with the `fetch` method in JavaScript, then you can add a `.then` to the end of the fetch as it returns a promise. This code will only run when the fetch is completed, and so the data (or an error) will be present. You can see this functionality in use here:

<pre><code class="language-coffeescript">fetch("example.com")
.then((response) => {
  console.log(response)
})
.catch((error) => {
console.error(error)
})
</code></pre>

This will fetch `example.com` and log the fetched response unless an error occurs &mdash; in this case it will be logged as an error. 

In addition to this syntax, the newer `async/await` syntax can also be used. These require a function defined as `a``sync`, in the same way as you might export a function. You can declare it like so:

<pre><code class="language-javascript">async function myFunction(){
  return
}
</code></pre>

Inside this function, you can call further async functions by placing `await` in front of them, for example:

<pre><code class="language-javascript">async function myFunction(){
  const data = await fetch("example.com")
  return data
}
</code></pre>

This code will return a promise that will resolve when the data is fetched, so it needs to be called inside an asynchronous function to await the result. However, in order to also catch errors, you will need to write a conditional to **check the response status** &mdash; if `data.ok` isn’t true, an error should be thrown. Then, you can wrap these away statements in a try catch block, rather than using `.catch`. You can read more about these methods in [this article](https://www.smashingmagazine.com/2020/11/comparison-async-await-versus-then-catch/). 


## Improvements

### Routing
Next.js uses **file system routing**, which is very similar to using different `.html` pages in a traditional website. However, this system also offers features beyond that, providing dynamic routes and allowing one page to be accessed under a range of urls.

For example, if you have a blog, you might keep all your files under `/blog/*`, creating a file `[slug].jsx` inside the `blog` folder &mdash; which will allow that content to be served for all pages under `blog`. Then, you can use the router in Next.js to find which route has been navigated to, like so:

<pre><code class="language-cpp">const router = useRouter()
const { slug } = router.query
</code></pre>

### API routes
API routes allow you to also write your backend inside your Next.js application. To use these routes, create an `api` folder in your `pages` directory &mdash; now, any files created inside it will run on the server rather than the client, as with the rest of the pages.

To get started with these, you need to **export a default function** from the file, and this can take two parameters. The first will be the incoming request, and the second will let you create the response. A basic API route can be written like this:

<pre><code class="language-javascript">export default function handler(request, response) {
  response.status(200).json({ magazine: 'Smashing' })
}
</code></pre>

## Limitations

### jQuery UI
You may use jQuery UI in your application for user interface, but React doesn’t provide an official UI library like this. Nevertheless, a range of alternatives has been produced. Two of the most popular are [Reach UI](https://reach.tech/) and [React Aria](https://react-spectrum.adobe.com/react-aria/getting-started.html). Both of these alternatives focus very strongly on Accessibility, ensuring that the project you create is usable by a bigger range of users.

### Animation
While you can use conditional rendering instead of effects, this doesn’t provide all the same functionality, as you can’t do things such as fading content out. One library that helps to provide this functionality is [React Transition Group](https://reactcommunity.org/react-transition-group/) &mdash; which allows you to define entering and exiting transitions.


## Conclusion

Moving from jQuery to Next.js is a **large undertaking**, especially for big code bases. However, this migration allows you to use newer concepts (such as data fetching at build time) and sets you up to have simple migration paths to new versions of React and Next.js &mdash; along with the features they bring.  

React can help you **better organize your code** (which is particularly important for large codebases) and brings a substantial performance improvement through the use of a virtual DOM. Overall, I believe that migrating from jQuery to Next.js is worth the effort, and I hope that if you decide to migrate, you enjoy all the features React and Next.js have to offer. 

### Further Reading on Smashing Magazine

- “[How To Migrate From jQuery To Next.js](https://www.smashingmagazine.com/2021/07/migrate-jquery-nextjs/),” Facundo Giuliani 
- “[The What, When, Why And How Of Next.js’ New Middleware Feature](https://www.smashingmagazine.com/2022/04/next-js-middleware-feature/),” Sam Poder
- “[Localizing Your Next.js App](https://www.smashingmagazine.com/2021/11/localizing-your-nextjs-app/),” Átila Fassina
- “[How To Maintain A Large Next.js Application](https://www.smashingmagazine.com/2021/11/maintain-large-nextjs-application/),” Nirmalya Ghosh

{{< signature "nl" >}}

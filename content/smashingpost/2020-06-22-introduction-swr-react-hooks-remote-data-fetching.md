---
title: 'An Introduction To SWR: React Hooks For Remote Data Fetching'
slug: introduction-swr-react-hooks-remote-data-fetching
author: ibrahima-ndaw
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae826b7c-c280-4b3b-8851-d4a60b9f60e6/introduction-swr-react-hooks-remote-data-fetching.png
date: 2020-06-22T12:00:00.000Z
summary: >-
  In this article, we’ll be looking at a new way of retrieving data in React Apps named SWR. This is a set of hooks for remote data fetching that makes things easier, such as caching, pagination, and so on. We’ll also be building a Pokedex App from scratch and using SWR features to get data and paginate it.
description: >-
  In this article, we’ll be looking at a new way of retrieving data in React Apps named SWR. This is a set of hooks for remote data fetching that makes things easier, such as caching, pagination, and so on.
categories:
  - React
  - React Hooks
  - JavaScript
  - Tools
---

SWR is a lightweight library created by Vercel (formerly ZEIT) that allows fetching, caching, or refetching data in realtime using React Hooks. It’s built with [React Suspense](https://reactjs.org/docs/concurrent-mode-suspense.html) which lets your components "wait" for something before they can render, including data. SWR ships also with great features such as dependent fetching, focus on revalidation, scroll position recovery, and so on. It’s also a very powerful tool since it’s backend agnostic and has good support for TypeScript. It’s a package that has a bright future.

Why should you care? You should care if you’ve been looking for a library that does not only fetch data from APIs but also make it possible to do things like caching and dependent fetching. What will be covered in this tutorial will come in handy when building React applications with a lot of moving parts. It’s expected that you should have made use of Axios and the Fetch API, even though we’ll compare how they differ from SWR, we won’t be going into details on how they’ll be implemented.

In this guide, I will introduce you to React Hooks for Remote Data Fetching by building a Pokedex app that requests data from the Pokemon API. We will also dive into other features that come with SWR as well, and highlight its differences compared to popular solutions such as the Fetch API and the Axios library and give you the reasons why using this library and why you should keep an eye on SWR.

So, let’s start by answering a fundamental question: What is SWR?

{{% feature-panel %}}

## What Is SWR?

SWR is an initialism of stale-while-revalidate. It’s a React Hooks library for remote data fetching. SWR works with three main steps: first, it returns the data from the cache (the stale part), then sends the fetch request (the revalidate part), and finally comes with the up-to-date data. But no worries, SWR handles all these steps for us. The only thing we have to do is give the `useSWR` hook the needed parameters to make the request.

SWR has also some nice features such as:

- Back-end agnostic
- Fast page navigation
- Revalidation on focus
- Interval polling
- Request deduplication
- Local mutation
- Pagination
- TypeScript ready
- SSR support
- Suspense mode
- React Native support
- Lightweight.

Sounds magical? Well, SWR simplifies things and increases for sure the user experience of your React app. And once we start implementing it in our project, you will see why this hook is handy.

It’s important to know that the name of the package is `swr` or SWR and the hook used to get SWR features is named `useSWR`.

In theory, the SWR is maybe what you need to enhance your data fetching. However, we already have two great ways of making HTTP requests in our app: the Fetch API and the Axios library.

So, why using a new library to retrieve data? let’s try answering this legit question in the next section.

## Comparison With Fetch And Axios

We already have many ways to make HTTP requests in our React Apps, and two of the most popular is the Fetch API and the Axios library. They are both great and allows us to fetch or send data easily. However, once the operation is done, they will not help us to cache or paginate data, you have to do it on our own.

Axios or Fetch will just handle the request and return the expected response, nothing more.

And compared to SWR, it’s a bit different because the SWR under the hood uses the Fetch API to request data from the server &mdash; it’s kind of a layer built on top of it. However, it has some nice features such as caching, pagination, scroll position recovery, dependent fetching, etc, and to be precise a certain level of reactivity out of the box that Axios or Fetch do not have. It’s a big advantage because having such features help to make our React Apps fast and user-friendly and reduce markedly the size of our code.

And to conclude, just keep in mind that SWR is not the same as Axios or Fetch even if it helps to deal with HTTP requests. SWR is more advanced than them, it provides some enhancements to keep our app synchronized with the back-end and hence increases the performance of our app.

Now we know what’s differences SWR has compared to the Axios library or the Fetch API, it’s time to dive into why using such a tool.

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2020/06/rest-api-react-fetch-axios/">Consuming REST APIs In React With Fetch And Axios</a></em></p>

## Why Using SWR For Data Fetching?

As I said earlier SWR ships with some handy features that help to increase the usability of your app easily. With SWR, you can paginate your data in no-time using `useSWRPages`, you can also fetch data that depends on another request or recover a scroll position when you get back to a given page, and so much more.

Usually, we show to the user a loading message or a spinner while fetching data from the server. And with SWR, you can make it better by showing to the user the cached or stale data while retrieving new data from the API. And once that operation is done, it will revalidate the data to show the new version. And you don’t need to do anything, SWR will cache the data the first time you fetch it and retrieve it automatically when a new request is made.

So far, we already see why using SWR over Axios or Fetch is better depending obviously on what you are aiming to build. But for many cases, I will recommend using SWR because it has great features that go beyond just fetching and returning data.

That said, we can now start building our React app and use the SWR library to fetch remote data.

So, let’s start by setting up a new project.

{{% ad-panel-leaderboard %}}

## Setting Up

As I said earlier in the introduction, we will build an app that fetches data from the Pokemon API. You can use a different API if you want too, I will stick with it for now.

And to create a new app, we need to run the following command on the terminal:

<pre><code class="language-bash">npx create-react-app react-swr</code></pre>

Next, we need to install the SWR library by first navigating to the folder that holds the React app.

<pre><code class="language-bash">cd react-swr</code></pre>

And run on the terminal the following command to install the SWR package.

<pre><code class="language-bash">yarn add swr</code></pre>

Or if you’re using npm:

<pre><code class="language-bash">npm install swr</code></pre>

Now we have all set up done, let’s structure the project as follow to start using SWR:

<pre><code class="language-bash">src
├── components
|  └── Pokemon.js
├── App.js
├── App.test.js
├── index.js
├── serviceWorker.js
├── setupTests.js
├── package.json
├── README.md
├── yarn-error.log
└── yarn.lock</code></pre>

As you can see, the folder structure is simple. The only thing to notice is the `components` folder that holds the `Pokemon.js` file. It will be used later as a presentational component to show a single Pokemon once we get data from the API.

Great! With that in place, we can now start fetching data from the API using `useSWR`.

## Fetching Remote Data

The SWR package has some handy features as we have seen above. However, there are two ways of configuring this library: either locally or globally.

A local setup means that every time we create a new file, we have to setup SWR again to be able to fetch remote data. And a global setup allows us to reuse a part of our configuration within different files because a `fetcher` function can be declared once and used everywhere.

And no worries, we will see both in this article, but for now, let’s get hands dirty and add some meaningful code in the `App.js` file.

### Displaying The Data

<div class="break-out">

<pre><code class="language-javascript">import React from 'react'
import useSWR from 'swr'
import { Pokemon } from './components/Pokemon'

const url = 'https://pokeapi.co/api/v2/pokemon'

const fetcher = (...args) =&gt; fetch(...args).then((res) =&gt; res.json())

function App() {
    const { data: result, error } = useSWR(url, fetcher)

    if (error) return &lt;h1&gt;Something went wrong!&lt;/h1&gt;
    if (!result) return &lt;h1&gt;Loading...&lt;/h1&gt;

    return (
        &lt;main className='App'&gt;
            &lt;h1&gt;Pokedex&lt;/h1&gt;
            &lt;div&gt;
                {result.results.map((pokemon) =&gt; (
                    &lt;Pokemon key={pokemon.name} pokemon={pokemon} /&gt;
                ))}
            &lt;/div&gt;
        &lt;/main&gt;
    )
}
export default App</code></pre>
</div>

As you can see, we start by importing `useSWR` from the SWR library. This declares the URL of the API you want to get data from, and a function to fetch these data.

The function `fetcher` is used here to transform the data into JSON. It receives the data fetched as an argument and returns something.

Notice that here, I use the [Rest](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters) operator (`(...args)`) since I'm not sure of the type and length of data received as a parameter, therefore, I copy everything before passing it again as an argument to the `fetch` method provided by `useSWR` which transforms the data into JSON and returns it.

That said, the `fetcher` and the `url` of the API can be now passed as parameters to the `useSWR` hook. With that, it can now make the request and it returns two states: the data fetched and an error state. And `data: result` is the same as `data.result`, we use object destructuring to pull `result` from `data`.

With the returned values, we can now check if the data is successfully fetched and then loop through it. And for each user, use the Pokemon component to display it.

Now we have the data and pass it down to the Pokemon Component, it’s time to update `Pokemon.js` to be able to receive and display the data.

### Creating The Pokemon Component

<div class="break-out">

<pre><code class="language-javascript">import React from 'react'
import useSWR from 'swr'

const fetcher = (...args) =&gt; fetch(...args).then((res) =&gt; res.json())

export const Pokemon = ({ pokemon }) =&gt; {
    const { name } = pokemon
    const url = 'https://pokeapi.co/api/v2/pokemon/' + name

    const { data, error } = useSWR(url, fetcher)

    if (error) return &lt;h1&gt;Something went wrong!&lt;/h1&gt;
    if (!data) return &lt;h1&gt;Loading...&lt;/h1&gt;

    return (
        &lt;div className='Card'&gt;
            &lt;span className='Card--id'&gt;#{data.id}&lt;/span&gt;
            &lt;img
                className='Card--image'
                src={data.sprites.front_default}
                alt={name}
            /&gt;
            &lt;h1 className='Card--name'&gt;{name}&lt;/h1&gt;
            &lt;span className='Card--details'&gt;
                {data.types.map((poke) =&gt; poke.type.name).join(', ')}
            &lt;/span&gt;
        &lt;/div&gt;
    )
}</code></pre>
</div>

Here, we have a component that receives a single Pokemon data from the API and displays it. However, the data received does not contain all fields needed, hence we have to make another request to the API to get the complete Pokemon object.

And as you can see, we use the same process to retrieve the data even if this time we append the name of the Pokemon to the URL.

By the way, if you are not familiar with destructuring, `({ pokemon })` is the same as receiving props and accessing to the pokemon object with `props.pokemon`. It’s just a shorthand to pull out values from objects or arrays.

With that in place, if you navigate to the root folder of the project and run on the terminal the following command:

<pre><code class="language-bash">yarn start</code></pre>

Or if you’re using npm:

<pre><code class="language-bash">npm start</code></pre>

You should see that the data are successfully fetched from the Pokemon API and displayed as expected.

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78bb0682-3184-4c71-af4f-c7ab29634725/react-hooks-remote-data-fetching.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78bb0682-3184-4c71-af4f-c7ab29634725/react-hooks-remote-data-fetching.PNG" sizes="100vw" caption="Fetching illustration. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78bb0682-3184-4c71-af4f-c7ab29634725/react-hooks-remote-data-fetching.PNG'>Large preview</a>)" alt="fetching" >}}

Great! We are now able to fetch remote data with SWR. However, this setup is a local one and can be a bit redundant because you can already see that `App.js` and `Pokemon.js` use the same fetcher function to do the same thing.

But luckily, the package comes with a handy provider named `SWRConfig` that helps to configure SWR globally. It’s a wrapper component that allows child components to use the global configuration and therefore the fetcher function.

To setup SWR globally, we need to update the `index.js` file because it’s where the App component is rendered using React DOM. If you want, you can use `SWRConfig` directly in the `App.js` file.

### Configuring SWR Globally

<div class="break-out">

<pre><code class="language-javascript">import React from 'react'
import ReactDOM from 'react-dom'
import { SWRConfig } from 'swr'
import App from './App'
import './index.css'

const fetcher = (...args) =&gt; fetch(...args).then((res) =&gt; res.json())

ReactDOM.render(
    &lt;React.StrictMode&gt;
        &lt;SWRConfig value={{ fetcher }}&gt;
            &lt;App /&gt;
        &lt;/SWRConfig&gt;
    &lt;/React.StrictMode&gt;,
    document.getElementById('root')
)</code></pre>
</div>

As you can see, we start by importing `SWRConfig` which is a provider that needs to wrap the higher component or just part of your React app that needs to use SWR features. It takes as props a value that expects an object of config. You can pass more than one property to the config object, here I just need the function to fetch data.

Now, instead of declaring the `fetcher` function in every file, we create it here and pass it as value to `SWRConfig`. With that, we can now retrieve data at any level in our app without creating another function and hence avoid redundancy.

Besides that, `fetcher` is equal to `fetcher: fetcher`, it’s just syntactic sugar proposed by ES6. With that change, we need now to update our components to use the global config.

{{% ad-panel-leaderboard %}}

### Using The Global SWR Config

<div class="break-out">

<pre><code class="language-javascript">import React from 'react'
import useSWR from 'swr'
import { Pokemon } from './components/Pokemon'

const url = 'https://pokeapi.co/api/v2/pokemon'

function App() {
    const { data: result, error } = useSWR(url)

    if (error) return &lt;h1&gt;Something went wrong!&lt;/h1&gt;
    if (!result) return &lt;h1&gt;Loading...&lt;/h1&gt;

    return (
        &lt;main className='App'&gt;
            &lt;h1&gt;Pokedex&lt;/h1&gt;
            &lt;div&gt;
                {result.results.map((pokemon) =&gt; (
                    &lt;Pokemon key={pokemon.name} pokemon={pokemon} /&gt;
                ))}
            &lt;/div&gt;
        &lt;/main&gt;
    )
}
export default App</code></pre>
</div>

Now we only need to pass the `url` to `useSWR`, instead of passing the `url` and `fetcher` method. Let’s also tweak the Pokemon component a bit.

<div class="break-out">

<pre><code class="language-javascript">import React from 'react'
import useSWR from 'swr'

export const Pokemon = ({ pokemon }) =&gt; {
    const { name } = pokemon
    const url = 'https://pokeapi.co/api/v2/pokemon/' + name

    const { data, error } = useSWR(url)

    if (error) return &lt;h1&gt;Something went wrong!&lt;/h1&gt;
    if (!data) return &lt;h1&gt;Loading...&lt;/h1&gt;

    return (
        &lt;div className='Card'&gt;
            &lt;span className='Card--id'&gt;#{data.id}&lt;/span&gt;
            &lt;img
                className='Card--image'
                src={data.sprites.front_default}
                alt={name}
            /&gt;
            &lt;h1 className='Card--name'&gt;{name}&lt;/h1&gt;
            &lt;span className='Card--details'&gt;
                {data.types.map((poke) =&gt; poke.type.name).join(', ')}
            &lt;/span&gt;
        &lt;/div&gt;
    )
}</code></pre>
</div>

You can already see that we have no fetcher function anymore, thanks to the global configuration which passes the function to `useSWR` under the hood.

Now, you can use the global fetcher function everywhere in your app. The only thing that the `useSWR` hook needs to fetch remote data is the URL.

However, we can still enhance the setup furthermore by creating a custom hook to avoid declaring the URL again and again, and instead, just pass as parameter the path.

### Advanced Setup By Creating A Custom Hook

To do so, you have to create a new file in the root of the project named `useRequest.js` (you can name it whatever you want) and add this code block below to it.

<div class="break-out">

<pre><code class="language-javascript">import useSwr from 'swr'

const baseUrl = 'https://pokeapi.co/api/v2'

export const useRequest = (path, name) =&gt; {
    if (!path) {
        throw new Error('Path is required')
    }

    const url = name ? baseUrl + path + '/' + name : baseUrl + path
    const { data, error } = useSwr(url)

    return { data, error }
}</code></pre>
</div>

Here, we have a function that receives a path and optionally a name and appends it to the base URL to build the complete URL. Next, it checks if a name parameter is received or not and handle it consequently.

Then, that URL is passed as a parameter to the `useSWR` hook to be able to fetch the remote data and return it. And if no path is passed, it throws an error.

Great! we need now to tweak the components a bit to use our custom hook.

<div class="break-out">

<pre><code class="language-javascript">import React from 'react'
import { useRequest } from './useRequest'
import './styles.css'
import { Pokemon } from './components/Pokemon'

function App() {
    const { data: result, error } = useRequest('/pokemon')

    if (error) return &lt;h1&gt;Something went wrong!&lt;/h1&gt;
    if (!result) return &lt;h1&gt;Loading...&lt;/h1&gt;

    return (
        &lt;main className='App'&gt;
            &lt;h1&gt;Pokedex&lt;/h1&gt;
            &lt;div&gt;
                {result.results.map((pokemon) =&gt; (
                    &lt;Pokemon key={pokemon.name} pokemon={pokemon} /&gt;
                ))}
            &lt;/div&gt;
        &lt;/main&gt;
    )
}
export default App</code></pre>
</div>

Now, instead of using the SWR hook, we use the custom hook built on top of it and then pass as expected the path as an argument. With that in place, everything will work like before but with a much cleaner and flexible configuration.

Let’s also update the Pokemon component.

<div class="break-out">

<pre><code class="language-javascript">import React from 'react'
import { useRequest } from '../useRequest'

export const Pokemon = ({ pokemon }) =&gt; {
    const { name } = pokemon
    const { data, error } = useRequest('/pokemon', name)

    if (error) return &lt;h1&gt;Something went wrong!&lt;/h1&gt;
    if (!data) return &lt;h1&gt;Loading...&lt;/h1&gt;

    return (
        &lt;div className='Card'&gt;
            &lt;span className='Card--id'&gt;#{data.id}&lt;/span&gt;
            &lt;img
                className='Card--image'
                src={data.sprites.front_default}
                alt={name}
            /&gt;
            &lt;h1 className='Card--name'&gt;{name}&lt;/h1&gt;
            &lt;span className='Card--details'&gt;
                {data.types.map((poke) =&gt; poke.type.name).join(', ')}
            &lt;/span&gt;
        &lt;/div&gt;
    )
}</code></pre>
</div>

You can already see how our custom hook makes things easier and more flexible. Here, we just need to pass additionally the name of the Pokemon to fetch to `useRequest` and it handles everything for us.

I hope you start enjoying this cool library &mdash; However, we still have things to discover because SWR offers so many features, and one of them is `useSWRPages` which is a hook to paginate data easily. So, let’s use that hook in the project.

### Paginate Our Data With `useSWRPages`

SWR allows us to paginate data easily and request only a part of it, and when needed refetch data to show for the next page.

Now, let’s create a new file in the root of the project `usePagination.js` and use it as a custom hook for pagination.

<div class="break-out">

<pre><code class="language-javascript">import React from 'react'
import useSWR, { useSWRPages } from 'swr'
import { Pokemon } from './components/Pokemon'

export const usePagination = (path) =&gt; {
    const { pages, isLoadingMore, loadMore, isReachingEnd } = useSWRPages(
        'pokemon-page',
        ({ offset, withSWR }) =&gt; {
            const url = offset || `https://pokeapi.co/api/v2${path}`
            const { data: result, error } = withSWR(useSWR(url))

            if (error) return &lt;h1&gt;Something went wrong!&lt;/h1&gt;
            if (!result) return &lt;h1&gt;Loading...&lt;/h1&gt;

            return result.results.map((pokemon) =&gt; (
                &lt;Pokemon key={pokemon.name} pokemon={pokemon} /&gt;
            ))
        },
        (SWR) =&gt; SWR.data.next,
        []
    )

    return { pages, isLoadingMore, loadMore, isReachingEnd }
}</code></pre>
</div>

As you can see, here we start by importing `useSWRPages` which is the helper that allows paginating data easily. It receives 4 arguments: the key of the request `pokemon-page` which is also used for caching, a function to fetch the data that returns a component if the data are successfully retrieved, and another function that takes the `SWR` object and request data from the next page, and an array of dependencies.

And once the data fetched, the function `useSWRPages` returns several values, but here we need 4 of them: the `pages` that is the component returned with the data, the function `isLoadingMore` which checks if the data are currently fetched, the function `loadMore` that helps fetching more data, and the method `isReachingEnd` which determines whether there is still data to retrieve or not.

Now we have the custom hook that returns the needed values to paginate data, we can now move to the `App.js` file and tweak it a bit.

<div class="break-out">

<pre><code class="language-javascript">import React from 'react'
import { usePagination } from './usePagination'
import './styles.css'

export default function App() {
    const { pages, isLoadingMore, loadMore, isReachingEnd } = usePagination(
        '/pokemon'
    )

    return (
        &lt;main className='App'&gt;
            &lt;h1&gt;Pokedex&lt;/h1&gt;
            &lt;div&gt;{pages}&lt;/div&gt;
            &lt;button
                onClick={loadMore}
                disabled={isLoadingMore || isReachingEnd}
            &gt;
                Load more...
            &lt;/button&gt;
        &lt;/main&gt;
    )
}</code></pre>
</div>

Once the `usePagination` hook imported, we can now pass the path as a parameter and get back the returned values. And since `pages` is a component, we don’t need to loop through the data or anything like that.

Next, we use the function `loadMore` on the button to fetch more data and disable it if the retrieving operation is not finished or if there is no data to fetch.

Great! with that change, we can now browse on the root of the project and start the server with this command to preview our app.

<pre><code class="language-bash">yarn start</code></pre>

Or if you’re using npm:

<pre><code class="language-bash">npm start</code></pre>

You should see that the data are successfully fetched and if you click on the button, new data will be retrieved by SWR.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/485b517c-9f88-42fd-8c83-19dea358e9af/paginate-data.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/937d090d-2cf7-42d6-ad8e-97db79969a0d/paginate-data-800w.gif" width="800" height="" alt="Pagination" /></a><figcaption>Pagination. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/485b517c-9f88-42fd-8c83-19dea358e9af/paginate-data.gif">Large preview</a>)</figcaption></figure>

So far, we have seen in practice the SWR library, and I hope you are finding value on it. However, it still has some features to offer. Let’s dive into these functionalities in the next section.

## Other Features Of SWR

The SWR library has a bunch of handy things that simplifies the way we build React apps.

#### Focus Revalidation

It’s a feature that allows updating or revalidating to be precise the data when you re-focus a page or switch between tabs. And by default, this functionality is enabled, but you can disable it anyway if it does not fit your need. It can be useful especially if you have data with high-level-frequency updates.

#### Refetch on Interval

The SWR library allows refetching data after a certain amount of time. It can be handy when your data changes at high speed or you need to make a new request to get a piece of new information from your database.

#### Local Mutation

With SWR, you can set a temporary local state that will update automatically when new data are fetched(revalidation). This feature comes in play particularly when you deal with an Offline-first approach, it helps to update data easily.

#### Scroll Position Recovery

This feature is very handy, especially when it comes to dealing with huge lists. It allows you to recover the scroll position after getting back to the page. And in any case, it increases the usability of your app.

#### Dependent Fetching

SWR allows you to fetch data that depends on other data. That means it can fetch data A, and once that operation is done, it uses it to fetch data B while avoiding waterfalls. And this feature helps when you have relational data.

That said, SWR helps to increase the user experience in any matter. It has more features than that, and for many cases it’s better to use it over the Fetch API or the Axios library.

## Conclusion

Throughout this article, we have seen why SWR is an awesome library. It allows remote data fetching using React Hooks and helps to simplify some advanced features out of the box such as pagination, caching data, refetching on interval, scroll position recovery, and so on. SWR is also backend agnostic which means it can fetch data from any kind of APIs or databases. In definitive, SWR increases a lot the user experience of your React apps, it has a bright future and you should keep an eye on it or better use it in your next React app.

You can preview the finished project live [here](https://codesandbox.io/s/react-swr-e2vel).

Thanks for reading!

### Next Steps

You can go on to check the following links which will give you a better understanding beyond the scope of this tutorial.

- [SWR](https://github.com/zeit/swr)
- [SWR Docs](https://swr.now.sh)

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
    <li><a title="Read 'Styling Components In React'" href="https://www.smashingmagazine.com/2020/05/styling-components-react/" rel="bookmark">Styling Components In React</a></li>
    <li><a title="Read 'Better Reducers With Immer'" href="https://www.smashingmagazine.com/2020/06/better-reducers-with-immer/" rel="bookmark">Better Reducers With Immer</a></li>
    <li><a title="Read 'Higher-Order Components In React'" href="https://www.smashingmagazine.com/2020/06/higher-order-components-react/" rel="bookmark">Higher-Order Components In React</a></li>
    <li><a title="Read 'Building Reusable React Components Using Tailwind'" href="https://www.smashingmagazine.com/2020/05/reusable-react-components-tailwind/" rel="bookmark">Building Reusable React Components Using Tailwind</a></li>
</ul>

{{< signature "ks, ra, yk, il" >}}

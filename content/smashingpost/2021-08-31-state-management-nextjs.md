---
title: 'State Management In Next.js'
slug: state-management-nextjs
author: atila-fassina
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7be7a6e9-5d44-4941-8a6c-dfee3435cc9b/state-management-nextjs.jpg
date: 2021-08-31T14:00:00.000Z
summary: >-
  By combining some React APIs, we can accurately manage “simple” states. With Next.js though, we can quickly find situations where we need to accommodate many other requirements. Let’s have a look at some patterns to accomplish all that.
description: >-
  By combining some React APIs, we can accurately manage “simple” states. With Next.js though, we can quickly find situations where we need to accommodate many other requirements. Let’s have a look at some patterns to accomplish all that.
categories:
  - Jamstack
  - Next.js
  - JavaScript
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Netlify
  link: https://www.netlify.com/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcf23ab4-3a5e-4a81-b79f-b520b5dcf6a2/netlify-full-logo-light.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.netlify.com/">Netlify</a> who are a diverse group of incredible talent from all over the world and offers a platform for web developers that multiplies productivity. <em>Thank you!</em>
---

This article is intended to be used as a primer for managing complex states in a Next.js app. Unfortunately, the framework is way too versatile for us to cover all possible use cases in this article. But these strategies should fit the vast majority of apps around with little to no adjustments. If you believe there is a relevant pattern to be considered, I look forward to seeing you in the comments section!

## React Core APIs For Data

There is only one way a React application carries data: passing it down from parent components to children components. Regardless of how an app **manages** its data, it must pass data from top to bottom.

As an application grows in complexity and ramifications of your rendering tree, multiple layers surface. Sometimes it is needed to pass down data far down multiple layers of parent components until it finally reaches the component which the data is intended for, this is called **Prop Drilling**.

As one could anticipate: Prop Drilling can become a cumbersome pattern and error-prone as apps grow. To circumvent this issue comes in the Context API. The Context API adds 3 elements to this equation:

1. **Context**  
The data which is carried forward from Provider to Consumer.
2. **Context Provider**  
The component from which the data originates.
3. **Context Consumer**  
The component which will *use* the data received.

The Provider is invariably an ancestor of the consumer component, but it is likely **not** a direct ancestor. The API then skips all other links in the chain and hands the data (context) over directly to the consumer. This is the entirety of the Context API, passing data. It has as much to do with the data as the postal office has to do with your mail.

In a vanilla React app, data may be managed by 2 other APIs: `useState` and `useReducer`. It would be beyond the scope of this article to suggest when to use one or another, so let's keep it simple by saying:

- `useState`  
Simple data structure and simple conditions.
- `useReducer`  
Complex data structures and/or intertwined conditions.

The fact Prop Drilling and Data Management in React are wrongfully confused as one pattern is partially owned to an inherent flaw in the Legacy Content API. When a component re-render was blocked by `shouldComponentUpdate` it would prevent the context from continuing down to its target. This issue steered developers to resort to third-party libraries when all they needed was to avoid prop drilling.

To check a comparison on the most useful libraries, I can recommend you this post about [React State Management](https://daveceddia.com/react-state-management/).

Next.js is a React framework. So, any of the solutions described for React apps can be applied to a Next.js app. Some will require a bigger flex to get it set up, some will have the tradeoffs redistributed based on Next.js' own functionalities. But everything is 100% usable, you can pick your poison freely.

For the majority of common use-cases, the combination of Context and State/Reducer is enough. We will consider this for this article and not dive too much into the intricacies of complex states. We will however take into consideration that most Jamstack apps rely on external data, and that is also state.

## Propagating Local State Through The App

A Next.js app has 2 crucial components for handling all pages and views in our application:

- `_document.{t,j}sx`  
This component is used to define the static mark-up. This file is rendered on the server and **is not** re-rendered on the client. Use it for affecting the `<html>` and `<body>` tags and other metadata. If you don’t want to customize these things, it’s optional for you to include them in your application.
- `_app.{t,j}sx`  
This one is used to define the logic that should spread throughout the app. Anything that should be present on every single view of the app belongs here. Use it for `<Provider>`s, global definitions, application settings, and so on.

To be more explicit, Context providers are applied here, for example:

<div class="break-out">

 <pre><code class="language-javascript">// &#95;app.jsx or &#95;app.tsx

import { AppStateProvider } from './my-context'

export default function MyApp({ Component, pageProps }) {
  return (
    &lt;AppStateProvider&gt;
      &lt;Component {...pageProps} /&gt;
    &lt;/AppStateProvider&gt;
  )
}
</code></pre>
</div>

Every time a new route is visited, our pages can tap into the `AppStateContext` and have their definitions passed down as `props`. When our app is simple enough it only needs one definition to be spread out like this, the previous pattern should be enough. For example:

<pre><code class="language-javascript">export default function ConsumerPage() {
  const { state } = useAppStatecontext()
  return (
    &lt;p&gt;
      {state} is here! 🎉
    &lt;/p&gt;
  )
}
</code></pre>

You can check a real-world implementation of this ContextAPI pattern in our [demo repository](https://github.com/atilafassina/nextjs-layout-state/blob/main/context/main-data.tsx).

If you have multiple pieces of state defined in a single context, you may start running into performance issues. The reason for this is because when React sees a state update, it makes all of the necessary re-renders to the DOM. If that state is shared across many components (as it is when using the Context API), it could cause *unnecessary* re-renders, which we don’t want. Be discerning with the state variables you share across components!

Something you can do to stay organized with your state-sharing is by creating multiple pieces of Context (and thus different Context Providers) to hold different pieces of state. For example, you might share authentication in one Context, internationalization preferences in another, and website theme in another.

Next.js also provides a `<Layout>` pattern that you can use for something like this, to abstract all this logic out of the `_app` file, keeping it clean and readable.

<div class="break-out">

 <pre><code class="language-javascript">// &#95;app.jsx or &#95;app.tsx
import { DefaultLayout } from './layout'

export default function MyApp({ Component, pageProps }) {
  const getLayout = Component.getLayout || (
    page =&gt; &lt;DefaultLayout&gt;{page}&lt;/DefaultLayout&gt;
  )

  return getLayout(&lt;Component {...pageProps} /&gt;)
}



// layout.jsx
import { AppState_1_Provider } from '../context/context-1'
import { AppState_2_Provider } from '../context/context-2'

export const DefaultLayout = ({ children }) =&gt; {
  return (
    &lt;AppState_1_Provider&gt;
      &lt;AppState_2_Provider&gt;
        &lt;div className="container"&gt;
          {children}
        &lt;/div&gt;
      &lt;/AppState_2_Provider&gt;
    &lt;/AppState_1_Provider&gt;
  )
}
</code></pre>
</div>

With this pattern, you can create multiple Context Providers and keep them well defined in a Layout component for the whole app. In addition, the `getLayout` function will allow you to override the default Layout definitions on a per-page basis, so every page can have its own unique twist on what is provided.

## Creating A Hierarchy Amongst Routes

Sometimes the Layout pattern may not be enough, though. As apps go further in complexity, a need may surface to establish a relationship provider/consumer relationship between routes. A route will wrap other routes and thus provide them with common definitions instead of making developers duplicate code. With this in mind, there is a [Wrapper Proposal](https://github.com/vercel/next.js/discussions/26389) in Next.js discussions to provide a smooth developer experience for achieving this.

For the time being, there is **not** a low-config solution for this pattern within Next.js, but from the examples above, we can come up with a solution. Take this snippet [directly from the docs](https://nextjs.org/docs/basic-features/layouts#per-page-layouts):

<pre><code class="language-javascript">import Layout from '../components/layout'
import NestedLayout from '../components/nested-layout'

export default function Page() {
  return {
    /&#42;&#42; Your content &#42;/
  }
}

Page.getLayout = (page) =&gt; (
  &lt;Layout&gt;
    &lt;NestedLayout&gt;{page}&lt;/NestedLayout&gt;
  &lt;/Layout&gt;
)
</code></pre>

Again the `getLayout` pattern! Now it is provided as a property of the `Page` object. It takes a `page` parameter just as a React component takes the `children` prop, and we can wrap as many layers as we want. Abstract this into a separate module, and you share this logic with certain routes:

<pre><code class="language-javascript">// routes/user-management.jsx

export const MainUserManagement = (page) =&gt; (
  &lt;UserInfoProvider&gt;
    &lt;UserNavigationLayout&gt;
      {page}
    &lt;/UserNavigationlayout&gt;
  &lt;/UserInfoProvider&gt;
)


// user-dashboard.jsx
import { MainUserManagement } from '../routes/user-management'

export const UserDashboard = (props) =&gt; (&lt;&gt;&lt;/&gt;)

UserDashboard.getLayout = MainUserManagement
</code></pre>

## Growing Pains Strike Again: Provider Hell

Thanks to React's Context API we eluded **Prop Drilling**, which was the problem we set out to solve. Now we have readable code and we can pass `props` down to our components touching only required layers. 

Eventually, our app grows, and the number of `props` that must be passed down increases at an increasingly fast pace. If we are careful enough to isolate eliminate unnecessary re-renders, it is likely that we gather an uncountable amount of `<Providers>` at the root of our layouts.

<pre><code class="language-javascript">export const DefaultLayout = ({ children }) =&gt; {
  return (
    &lt;AuthProvider&gt;
      &lt;UserProvider&gt;
        &lt;ThemeProvider&gt;
          &lt;SpecialProvider&gt;
            &lt;JustAnotherProvider&gt;
              &lt;VerySpecificProvider&gt;
                {children}
              &lt;/VerySpecificProvider&gt;
            &lt;/JustAnotherProvider&gt;
          &lt;/SpecialProvider&gt;
        &lt;/ThemeProvider&gt;
      &lt;/UserProvider&gt;
    &lt;/AuthProvider&gt;
  )
}
</code></pre>  

This is what we call **Provider Hell**. And it can get worse: what if `SpecialProvider` is only aimed at a specific use-case? Do you add it at runtime? Adding both Provider and Consumer during runtime is not exactly straightforward.

With this dreadful issue in focus [Jōtai](https://jotai.pmnd.rs/) has surfaced. It is a state management library with a very similar signature to `useState`. Under the hood, Jōtai also uses the Context API, but it abstracts the Provider Hell from our code and even offers a “Provider-less” mode in case the app only requires one store. 

Thanks to the bottom-up approach, we can define Jōtai's **atoms** (the data layer of each component that connects to the store) in a component level and the library will take care of linking them to the provider. The `<Provider>` util in Jōtai carries a few extra functionalities on top of the default `Context.Provider` from React. It will always isolate the values from each atom, but it will take an `initialValues` property to declare an array of default values. So the above Provider Hell example would look like this:

<pre><code class="language-javascript">import { Provider } from 'jotai'
import {
  AuthAtom,
  UserAtom,
  ThemeAtom,
  SpecialAtom,
  JustAnotherAtom,
  VerySpecificAtom
} from '@atoms'
 
const DEFAULT_VALUES = [
  [AuthAtom, 'value1'],
  [UserAtom, 'value2'],
  [ThemeAtom, 'value3'],
  [SpecialAtom, 'value4'],
  [JustAnotherAtom, 'value5'],
  [VerySpecificAtom, 'value6']
]

export const DefaultLayout = ({ children }) => {
  return (
    <Provider initialValues={DEFAULT_VALUES}>
      {children}
    </Provider>
  )
}
</code></pre>

Jōtai also offers other approaches to easily compose and derive state definitions from one another. It can definitely solve scalability issues in an incremental manner.

## Fetching State

Up until now, we have created patterns and examples for managing the state internally within the app. But we should not be naïve, it is hardly ever the case an application does not need to fetch content or data from external APIs.

For client-side state, there are again two different workflows that need acknowledgement:

1. fetching the data
2. incorporating data into the app's state

When requesting data from the client-side, it is important to be mindful of a few things:

1. the user's network connection: avoid re-fetching data that is already available
2. what to do while waiting for the server response
3. how to handle when data is not available (server error, or no data)
4. how to recover if integration breaks (endpoint unavailable, resource changed, etc)

And now is when things start getting interesting. That first bullet, Item 1, is clearly related to the fetching state, while Item 2 slowly transitions towards the managing state. Items 3 and 4 are definitely on the managing state scope, but they are both dependent on the fetch action and the server integration. The line is definitely blurry. Dealing with all these moving pieces is complex, and these are patterns that do not change much from app to app. Whenever and however we fetch data, we must deal with those 4 scenarios.

Luckily, thanks to libraries such as [React-Query](https://react-query.tanstack.com/) and [SWR](https://swr.vercel.app/) every pattern shown for the local state is smoothly applied for external data. Libraries like these handle cache locally, so whenever the state is already available they can leverage settings definition to either renew data or use from the local cache. Moreover, they can even provide the user with stale data *while* they refresh content and prompt for an interface update whenever possible.

In addition to this, the React team has been transparent from a very early stage about upcoming APIs which aim to improve the user and developer experience on that front (check out the [proposed Suspense documentation here](https://github.com/reactwg/react-18/discussions/47#discussioncomment-847004)). Thanks to this, library authors have prepared for when such APIs land, and developers can start working with similar syntax as of today.

So now, let's add external state to our `MainUserManagement` layout with `SWR`:

<pre><code class="language-javascript">import { useSWR } from 'swr'
import { UserInfoProvider } from '../context/user-info'
import { ExtDataProvider } from '../context/external-data-provider'
import { UserNavigationLayout } from '../layouts/user-navigation'
import { ErrorReporter } from '../components/error-reporter'
import { Loading } from '../components/loading'

export const MainUserManagement = (page) =&gt; {
  const { data, error } = useSWR('/api/endpoint')

  if (error) =&gt; &lt;ErrorReporter {...error} /&gt;
  if (!data) =&gt; &lt;Loading /&gt;

  return (
    &lt;UserInfoProvider&gt;
      &lt;ExtDataProvider&gt;
        &lt;UserNavigationLayout&gt;
          {page}
        &lt;/UserNavigationlayout&gt;
      &lt;/ExtDataProvider&gt;
    &lt;/UserInfoProvider&gt;
  )
}
</code></pre>

As you can see above, the `useSWR` hook provides a lot of abstractions:

- a default fetcher
- zero-config caching layer
- error handler
- loading handler

With 2 conditions we can provide early returns within our component for when the request fails (error), or for while the round-trip to the server is not yet done (loading). For these reasons, the libraries side closely to State Management libraries. Although they are not exactly user management, they integrate well and provide us with enough tools to simplify managing these complex asynchronous states.

It is important to emphasize something at this point: a great advantage of having an isomorphic application is saving requests for the back-end side. Adding additional requests to your app once it is already on the client-side will affect the perceived performance.  There’s a great article (and e-book!) on this topic [here](https://www.netlify.com/blog/2021/06/14/how-next.js-became-a-top-jamstack-framework/) that goes much more in-depth.

This pattern is not intended in any way to replace `getStaticProps` or `getServerSideProps` on Next.js apps. It is yet another tool in the developer's belt to build with when presented with peculiar situations.

## Final Considerations

While we wrap up with these patterns, it is important to stress out a few caveats which may creep out on you if you are not mindful as you implement them. First, let us recapitulate what we have covered in this article:

- Context as a way of avoiding Prop Drilling;
- React core APIs for managing state (`useState` and `useReducer`);
- Passing client-side state throughout a Next.js application;
- How to prevent certain routes from accessing state;
- How to handle data-fetching on the client-side for Next.js apps.

There are three important tradeoffs that we need to be aware of when opting for these techniques:

1. Using the server-side methods for generating content statically is often preferable to fetching the state from the client-side.
2. The Context API can lead to multiple re-renders if you aren’t careful about where the state changes take place.

Making good consideration of those points will be important, in addition all good practices when dealing with state in a client-side React app remain useful on a Next.js app. The server layer may be able to offer a performance boost and this by itself may mitigate some computation issues. But it will also benefit from sticking to the common best practices when it comes to rendering performance on apps.

## Try It Yourself

You can check the patterns described in this article live on [nextjs-layout-state.netlify.app](https://nextjs-layout-state.netlify.app/) or check out the code on [github.com/atilafassina/nextjs-layout-state](https://github.com/atilafassina/nextjs-layout-state). You can even just click this button to instantly clone it to your chosen Git provider and deploy it to Netlify:

[![Deploy to Netlify](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cbbb757-9bee-4c1c-b84a-6e8dfed5c0a6/deploy-to-netlify-button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/atilafassina/nextjs-layout-state)

In case you would like something less opinionated or are just thinking about getting started with Next.js, there is this [awesome starter project to get you going](https://github.com/cassidoo/next-netlify-starter) all set up to easily deploy to Netlify. Again, Netlify makes it easy as pie to clone it to your own repository and deploy:

[![Deploy to Netlify](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cbbb757-9bee-4c1c-b84a-6e8dfed5c0a6/deploy-to-netlify-button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/cassidoo/next-netlify-starter)

## References

- [Context and Redux: differences](https://blog.isquaredsoftware.com/2021/01/context-redux-differences/)
- Next.js [Wrapper Proposal](https://github.com/vercel/next.js/discussions/26389)
- [Next.js Layouts](https://nextjs.org/docs/basic-features/layouts)
- [Jōtai](https://jotai.pmnd.rs/)
- [Using React Context for State Management in Next.js](https://www.netlify.com/blog/2020/12/01/using-react-context-for-state-management-in-next.js/)

{{< signature "vf, il" >}}

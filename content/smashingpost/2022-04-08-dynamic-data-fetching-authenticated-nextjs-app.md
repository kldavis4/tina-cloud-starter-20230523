---
title: 'Dynamic Data-Fetching In An Authenticated Next.js App'
slug: dynamic-data-fetching-authenticated-nextjs-app
author: caleb-olojo
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/929fd32f-838d-44e8-88f1-2392555f6c44/dynamic-data-fetching-authenticated-nextjs-app.jpg
date: 2022-04-08T12:00:00.000Z
summary: >-
  Data is among the most important things that make up a web application or a conventional native app. We need data to be able to see and perhaps understand the purpose of an application. In this article, we’ll look at another approach to obtaining data in an application that requires authentication or authorization using Next.js.
description: >-
  Data is among the most important things that make up a web application or a conventional native app. We need data to be able to see and perhaps understand the purpose of an application. In this article, we’ll look at another approach to obtaining data in an application that requires authentication or authorization using Next.js.
categories:
  - Next.js
  - JavaScript
  - Apps
---

Next.js has five types of data-fetching patterns for determining how you want content to be seen in your application: static-site generation (SSG), server-side rendering (SSR), client-side rendering (CSR), incremental static regeneration (ISR), and dynamic routing.

You can choose whichever of these patterns that suits the structure of your application. To learn more about these patterns, read about them in the [official documentation](https://nextjs.org/docs/basic-features/data-fetching/overview).

This article focuses on static-site generation and dynamic routing. Using these patterns requires the use of the `getStaticProps` and `getStaticPaths` data-fetching methods. These methods play unique roles in obtaining data.

We’ve been talking about dynamic data for a while now. Let’s understand what that truly means.

Say we have a list of users in an application being rendered on a web page, and we want to get information unique to a user when we click on their name &mdash; the information we get would change according to the action we perform (clicking on the user’s name).

We want a way to render that data on a unique page (or screen) in the application, and the `getStaticPaths` data-fetching method allows us to obtain data that is unique to a user. This is usually common in an array of user objects with a unique key (`id` or `_id`), depending on how the response object is structured.

<pre><code class="language-javascript">export async function getStaticPaths() {
  return {
    paths: {
      [{
        params: {
          uniqueId: id.toString()
        }
      }],
      fallback: false
    }
  }
}</code></pre>

The unique key obtained from the `getStaticPaths` method (commonly referred to as the parameter, or params for short) is passed as an argument through the `context` parameter in `getStaticProps`.

This brings us back to the fact that `getStaticPaths` cannot work without `getStaticProps`. Both of them function together, because you’ll need to pass the unique `id` from the statically generated path as an argument to the `context` parameter in `getStaticProps`. The code snippet below illustrates this:

<pre><code class="language-javascript">export async function getStaticProps(context) {
  return {
    props: {
      userData: data,
    },
  }
}</code></pre>

## The Cons of Using the Native Data-Fetching Methods Of Next.js

Now that we understand a little about dynamic data-fetching in Next.js, let’s look at the cons of using the two aforementioned data-fetching methods.

Getting data from a public API that requires no authorization with some sort of API key during data-fetching can be done with `getStaticProps` and `getStaticPaths`.

Take a look at both of them below:

<pre><code class="language-javascript">// getStaticPaths
export async function getStaticPaths() {
  const response = fetch("https://jsonplaceholder.typicode.com/users")
  const userData = await response.json()

 // Getting the unique key of the user from the response
 // with the map method of JavaScript.
  const uniqueId = userData.map((data) =&gt; {
    return data.id
  })

  return {
    paths: {
      [{
        params: {
          uniqueId: uniqueId.toString()
        }
      }],
      fallback: false
    }
  }
}</code></pre>

You’ll notice that the unique `id` is gotten from the `map` method of JavaScript, and we’re going to assign it as a value through the `context` parameter of `getStaticProps`.

<div class="break-out">

<pre><code class="language-javascript">export async function getStaticProps(context) {
  // Obtain the user’s unique ID.
  const userId = context.params.uniqueId

  // Append the ID as a parameter to the API endpoint.
  const response = fetch(`https://jsonplaceholder.typicode.com/users/${userId}`)
  const userData = await response.json()
  return {
    props: {
      userData,
    },
  }
}</code></pre>
</div>

In the snippet above, you’ll see that a variable named `userId` was initialized, and its value was gotten from the `context` parameter.

That value is then added as a parameter to the base URL of the API.

**Note:** The `getStaticProps` and `getStaticPaths` data-fetching methods may only be exported from a file in the `pages` folder of Next.js.

That pretty much does it for a public API. But when you’re building an application that requires the user to log in, log out, and perhaps perform some data-fetching in the application when they log in with their account, the application flow is different.

{{% feature-panel %}}

## Fetching Data in an Authenticated System.

The flow of obtaining data in an authenticated system is quite different from the normal way we get data from a public API.

Picture this scenario: A user logs into a web app and then visits their profile. On their profile page (once it is rendered), they’re able to see and alter the information that they provided when signing up.

For this to happen, there has to be some sort of verification of the data that is being sent to the user by the developer who built the interface. Luckily, there’s a common pattern for authorizing a user when they log into a system: JSON Web Tokens (JWTs).

When a user signs up to use your application for the first time, their details are stored in the database, and a unique JWT is assigned to that user’s schema (depending on how the back-end API has been designed).

When the user tries to log into your app, and their credentials match what they originally signed up with, the next thing we front-end engineers have to do is provide an authentication state for the user, so that we can obtain the required details, one of which is the JWT.

There are different schools of thought on how to preserve a user’s `auth-state`, including using Redux, Composition in React, and React’s Context API (I’d recommend the Context API). [Átila Fassina’s article](https://www.smashingmagazine.com/2021/08/state-management-nextjs/) goes over state-management paradigms in Next.js.

The common approach is to store the JWT in `localStorage` &mdash; to get started at least, if we’re considering the issue of security in a strict manner. Storing your JWT in an `httpOnly` cookie is advisable, to prevent security attacks such as a cross-site request forgery (CSRF) and cross-site scripting (XSS).

Once again, this approach can only be possible if the appropriate cookie middleware is provided in the API that the back-end engineers have built.

If you don’t want to go through the hassle of figuring out how the back-end engineers have designed an API, an alternative route to authentication in Next.js is to make use of the open-source authentication project NextAuth.js.

Once the token is in `localStorage` on the client side, the API calls that require the user token as a means of authorization can go through, without throwing a 501 (unauthorized) error.

<pre><code class="language-javascript">headers: {
  "x-auth-token": localStorage.getItem("token")
}</code></pre>

{{% ad-panel-leaderboard %}}

## Data-Fetching With the `useRouter` Hook

In the first section, we saw how the process of dynamic data-fetching works in Next.js for an application that doesn’t require authentication.

In this section, we’ll look at how to bypass the issue of the `getStaticProps` and `getStaticPaths` data-fetching methods throwing a `referenceError` (“`localStorage` is undefined”) when we try to get the user’s token from `localStorage`.

This error occurs because the two data-fetching methods are always running on the server in the background, which, in turn, makes the `localStorage` object unavailable to them, because it is on the client side (in the browser).

The router API of Next.js creates a lot of possibilities when we we’re dealing with dynamic routes and data. With the `useRouter` hook, we should be able to get data that is unique to a user based on their unique ID.

Let’s look at the snippet below to get started:

<pre><code class="language-javascript">// pages/index.js

import React from "react";
import axios from "axios";
import { userEndpoints } from "../../../routes/endpoints";
import Link from "next/link";

const Users = () =&gt; {
  const [data, setData] = React.useState([])
  const [loading, setLoading] = React.useState(false)

  const getAllUsers = async () =&gt; {
    try {
      setLoading(true);
      const response = await axios({
        method: "GET",
        url: userEndpoints.getUsers,
        headers: {
          "x-auth-token": localStorage.getItem("token"),
          "Content-Type": "application/json",
        },
      });
      const { data } = response.data;
      setData(data);
    } catch (error) {
      setLoading(false);
      console.log(error);
    }
  };

  return (
    &lt;React.Fragment&gt;
      &lt;p&gt;Users list&lt;/p&gt;
      {data.map((user) =&gt; {
          return (
            &lt;Link href={`/${user._id}`} key={user._id}&gt;
              &lt;div className="user"&gt;
                &lt;p className="fullname"&gt;{user.name}&lt;/p&gt;
                &lt;p className="position"&gt;{user.role}&lt;/p&gt;
              &lt;/div&gt;  
            &lt;/Link&gt;
          );
        })}
    &lt;/React.Fragment&gt;
  );
};

export default Users;</code></pre>

In the snippet above, we’ve used the `useEffect` hook to get the data once the page is rendered for the first time. You’ll also notice that the JWT is assigned to the `x-auth-token` key in the request header.

When we click on a user, the `Link` component will route us to a new page based on the user’s unique ID. Once we’re on that page, we want to render the information that is specifically available for that user with the `id`.

The `useRouter` hook gives us access to the `pathname` in the URL tab of the browser. With that in place, we can get the query parameter of that unique route, which is the `id`.

The snippet below illustrates the whole process:

<pre><code class="language-javascript">// [id].js

import React from "react";
import Head from "next/head";
import axios from "axios";
import { userEndpoints } from "../../../routes/endpoints";
import { useRouter } from "next/router";

const UniqueUser = () =&gt; {
  const [user, setUser] = React.useState({
    fullName: "",
    email: "",
    role: "",
  });
  const [loading, setLoading] = React.useState(false);
  const { query } = useRouter();

  // Obtaining the user’s unique ID with Next.js'
  // useRouter hook.
  const currentUserId = query.id;

  const getUniqueUser = async () =&gt; {
    try {
      setLoading(true);
      const response = await axios({
        method: "GET",
        url: `${userEndpoints.getUsers}/${currentUserId}`,
        headers: {
          "Content-Type": "application/json",
          "x-auth-token": localStorage.getItem("token"),
        },
      });
      const { data } = response.data;
      setUser(data);
    } catch (error) {
      setLoading(false);
      console.log(error);
    }
  };

  React.useEffect(() =&gt; {
    getUniqueUser();
  }, []);

  return (
    &lt;React.Fragment&gt;
      &lt;Head&gt;
        &lt;title&gt;
          {`${user.fullName}'s Profile | "Profile" `}
        &lt;/title&gt;
      &lt;/Head&gt;
        &lt;div&gt;
          &lt;div className="user-info"&gt;
            &lt;div className="user-details"&gt;
              &lt;p className="fullname"&gt;{user.fullName}&lt;/p&gt;
              &lt;p className="role"&gt;{user.role}&lt;/p&gt;
              &lt;p className="email"&gt;{user.email}&lt;/p&gt;
            &lt;/div&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      )}
    &lt;/React.Fragment&gt;
  );
};
export default UniqueUser;</code></pre>

In the snippet above, you’ll see that we’ve destructured the query object from the `useRouter` hook, which we’ll be using to get the user’s unique ID and pass it as an argument to the API endpoint.

<pre><code class="language-javascript">const {query} = useRouter()
const userId = query.id</code></pre>

Once the unique ID is appended to the API endpoint, the data that is meant for that user will be rendered once the page is loaded.

{{% ad-panel-leaderboard %}}

## Conclusion

Data-fetching in Next.js can get complicated if you don’t fully understand the use case of your application.

I hope this article has helped you understand how to use the router API of Next.js to get dynamic data in your applications.

{{< signature "vf, yk, il, al" >}}

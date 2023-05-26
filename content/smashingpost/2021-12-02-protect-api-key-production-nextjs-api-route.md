---
title: 'How To Protect Your API Key In Production With Next.js API Route'
slug: protect-api-key-production-nextjs-api-route
author: caleb-olojo
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0b2208c-15b4-4cdc-b050-033c4a4aa1b0/protect-api-key-production-nextjs-api-route.jpg
date: 2021-12-02T09:30:00.000Z
summary: >-
  There’s a great challenge that comes with building Jamstack applications on the web. In this article, Caleb Olojo explains how you can use Next.js to bootstrap your app safely.
description: >-
  There’s a great challenge that comes with building Jamstack applications on the web. In this article, Caleb Olojo explains how you can use Next.js to bootstrap your app safely.
categories:
  - API
  - Next.js
  - Tools
  - Node.js
---

Front-end developers have to interact with private or public APIs whose method of authorization requires a secret key/API key that enables developers to use these APIs. The key(s) are important, hence the need to store/protect the key(s) arises. Creating an environment variable that stores the key is the “go-to” solution that most developers tend to embrace, but there’s a catch. The environment variable **does not protect the key(s)** from anyone that knows their way around the dev-tools of their browser. That’s why we need to use our keys at server-side when we’re writing our API calls.

In this article, we’ll be using Next.js to bootstrap our app. This does not mean that the [`create-react-app`](https://create-react-app.dev/) library will not work. You can make use of any one that you find convenient. We’re using Next.js because of the many perks that come with it. (You can read more about Next.js [here](https://nextjs.org/docs/getting-started.).)

Let us start by installing the dependencies that we need in this project. We’ll start by creating a Next.js app. The command below does that for us:

<pre><code class="language-bash">npx create-next-app [name-of-your-app]</code></pre>

We’ll make use of the native JavaScript `"Fetch API"` library to get data from the API. We won’t be covering much of the styling aspect in this article. (If you want to take a look at an example project I built using the Next.js API route pattern, you can find the repository [here](https://github.com/Caleb335/article-example-projects/blob/master/src/container/users/index.js).)

Now let’s have a look at the file structure of the app. We’ll be focusing on the important files needed in this app, so it’ll be concise.

<pre><code class="language-bash">|--pages
|   |-- api
|   |   |-- serverSideCall.js  
|   |-- _app.js
|   |-- index.js
|__ .env.local</code></pre>

## Breakdown Of The Files In The App Structure

In this section, we are going to see the different files that make up the architecture of this project, and their respective functions below.

The `pages` directory is where all the routing of the app takes place. This is an out-of-the-box feature of Next.js. It saves you the stress of hard hard-coding your independent routes.

- `pages/api`  
The api directory enables you to have a backend for your Next.js app, inside the same codebase, instead of the common way of creating separate repositories for your REST or GraphQL APIs and deploying them on backend hosting platforms like Heroku, and so on.

    With the `api` directory, every file is treated as an API endpoint. If you look at the `api` folder, you’ll notice that we have a file called `user.js` in it.

    That file becomes an endpoint, which means an API call can be performed using the path to the file as the base URL.

<pre><code class="language-javascript">const getData = async() =&gt; {
  fetch("/api/users")
   .then(response =&gt; response())
   .then(response =&gt; console.log(response.data))
   .catch(err =&gt; console.log(err)
}</code></pre>

- `pages/_app.js`  
It is where all our components get attached to the DOM. If you take a look at the component structure, you’ll see that all the components are passed as `pageProps` to the `Component` props too.

<pre><code class="language-javascript">function MyApp({ Component, pageProps }) {
  return (
    &lt;React.Fragment&gt;
      &lt;Head&gt;
        &lt;meta name="theme-color" content="#73e2a7" /&gt;
        &lt;link rel="icon" type="image/ico" href="" /&gt;
      &lt;/Head&gt;
      &lt;Component {...pageProps} /&gt;
    &lt;/React.Fragment&gt;
  );
}

export default MyApp;</code></pre>

If you are new to Next.js, kindly go through this [article](https://www.smashingmagazine.com/2020/10/getting-started-with-next-js/) that will guide you through the process.

- `index.js`  
It is the default route in the pages folder. When you run the command below, it starts up a development server and the contents of `index.js` are rendered on the web page.

<pre><code class="language-bash">npm run dev</code></pre>

- `.env.local`  
It is where we’re storing the API key that’ll enable us to consume this API.

{{% feature-panel %}}

## The Server-Side API Call

The previous section exposed you to the files that we’ll be interacting with and their specific functions. In this section, we will move on to how we can consume the API.

The reason why we’re writing the API call at the server-side is for securing our API key, and Next.js already makes it an easy task for us. With the API routes in Next.js, we can perform our API calls without the fear of our API keys being revealed on the client-side.

You may have been wondering what the essence of the environment variable in the `.env` file is, in this scenario.

The environment variable (which is our API key) can only be available in `development` mode. 

That is why we can do something like `process.env.api_key`, and get access to the environment variable.

But, the moment you deploy your app to platforms like Netlify or Vercel, the mode changes to `production`, which makes the Node.js `process` object unavailable on the client-side.

Now that you have seen the reason why need to write a server-side API call. Let’s get to it right away.

<pre><code class="language-javascript">export default async function serverSideCall(req, res) {
    const {
      query: { firstName, lastName },
    } = req;

    const baseUrl = `https://api.example-product.com/v1/search?
        lastName=${lastName}&firstName=${firstName}
        &apiKey=${process.env.KEY}
    `;
    const response = await fetch (baseUrl);
    res.status(200).json({
    data: response.data,
  });
}</code></pre>

In the snippet above, we created an asynchronous function called, `serverSideCall`. It takes in two arguments, `req` which stands for “request” in full, and `res` which is “response” in full.

The `req` argument has some properties, (or “middlewares” as the Next.js docs call it) that can be accessed when we’re consuming our API, one of them is `req.query`.

You’ll notice that we destructured the `query` property in the snippet above, so we should now be able to pass those variables as values to the query properties of the API endpoint. Take a look at it below.

**Note**: *You can read more about the in-built middlewares that come with the `req` argument [here](https://nextjs.org/docs/api-routes/api-middlewares).*

<pre><code class="language-javascript">const {
  query: { firstName, lastName },
} = req;</code></pre>

The base URL takes the destructured query properties as values and the `apiKey` is gotten from the `.env` file via the Node.js `process` object.

The destructured query properties are taken as requests that will be sent from the input values of the form component (which we’ll be creating in the next section) to the API, once it is received, we get a response that corresponds with the request we made.

<div class="break-out">

<pre><code class="language-javascript">const baseUrl = `https://api.kelvindata.com/rest/v1/searchv2?  lastName=${lastName}&firstName=${firstName}&apiKey=${process.env.KEY}`;</code></pre>
</div>

The next process the function has to complete is the response from the asynchronous API call. The snippet below assigns the API call which we are performing with the `axios` library to a variable, `response`.

On the next line, the `res` argument uses the `status` method which is used to send a JSON response to us, then we can assign the response variable as a property of `data`.

<pre><code class="language-javascript">const response = await axios.get(baseUrl);
res.status(200).json({
  data: response.data,
});</code></pre>

You can read more about the various HTTP status codes [here](https://dillionmegida.com/p/http-status-codes/).

{{% ad-panel-leaderboard %}}

## Practical Usage Of The Server-Side API Function

In this section, we’ll have a look at how we can utilize the server-side API call by creating a form with two input fields. The input values will be sent as query parameters to the API endpoint.

<pre><code class="language-javascript">import React from "react";

const Index = () =&gt; {
  const [data, setData] = React.useState([]);
  const [firstName, setFirstName] = React.useState("");
  const [lastName, setLastName] = React.useState("");

  const getuserData = async () =&gt; {
    // api call goes here
  };

  const handleSubmit = (e) =&gt; {
     e.preventDefault();
     getuserData();
  };

  return (
     &lt;React.Fragment&gt;
       &lt;form onSubmit={handleSubmit}&gt;
          &lt;label htmlFor="firstname"&gt;First name&lt;/label&gt;
          &lt;input
            type="text"
            name="firstname"
            value={firstName}
            placeholder="First Name"
            onChange={(e) =&gt; setFirstName(e.target.value)}
          /&gt;
          &lt;label htmlFor="lastname"&gt;Lastname&lt;/label&gt;
          &lt;input
            type="text"
            name="lastname"
            value={lastName}
            placeholder="Lastname"
            onChange={(e) =&gt; setLastName(e.target.value)}
          /&gt;
           &lt;button&gt;Search&lt;/button&gt;
        &lt;/form&gt;
        &lt;div className="results-from-api"&gt;&lt;/div&gt;
    &lt;/React.Fragment&gt;
 );
};

export default Index;</code></pre>

Since this is a React component that is receiving data from an API endpoint, it should have an internal state of its own. The snippet below shows how we defined the different state variables with React Hooks.

<pre><code class="language-javascript">const [userData, setUserData] = React.useState([]);
const [firstName, setFirstName] = React.useState("");
const [lastName, setLastName] = React.useState("");</code></pre>

The `firstName` and `lastName` variables will store the text values that are typed into the input field by anyone into the local state variables.

The `data` state variable helps us store the response that we get from the API call in an array, so we can use the JavaScript `map()` method to render the response on the webpage.

Below, we’re using `axios` to get data from the API endpoint. But here, the base URL is not a typical `https://` URL, instead, it is the path to the file where we made the server-side API call before.

<pre><code class="language-javascript">const getuserData = async () =&gt; {
fetch(`/api/usersfirstName=${firstName}&lastName=${lastName}`, {
       headers: {
         Accept: "application/json",
       },
})
  .then((response) =&gt; response)
  .then((response) =&gt; {
    setData(response.data.data); 
    console.log(response.data.data);
  })
  .catch((err) =&gt; console.log(err));
};</code></pre>

The same process in the `serverSideCall.js` file is repeated, but this time around with the necessary fetch API headers and assignment of the input state variables to the API query parameters. 

{{% ad-panel-leaderboard %}}

## Conclusion

There are other approaches that can help achieve this feat. Here are some of them:

- **Creating Netlify Lambda functions that’ll help protect your API keys on the client-side.**       
This approach does it pretty much for you, but if you’re not a fan of writing so much code, it will help you get the little things done. The Next.js API route is your best bet in solving this issue.
- **Server rendering with Next.js to hide API keys.**  
In this video, [Ijemma Onwuzulike](https://ijemmao.me/) gives an explanation of how to get this done with server-side rendering. [I recommend checking it out](https://www.youtube.com/watch?v=NbXwP1oBym8).

Thank you for reading this article. Kindly share it and also feel free to take a look at a practical example project that I built using the Next.js API route [here](https://exdemo.netlify.app/demo/kelvin-data).

### Further Reading On Smashing Magazine

- “[How To Implement Authentication In Next.js With Auth0](https://www.smashingmagazine.com/2021/05/implement-authentication-nextjs-auth0/),” Facundo Giuliani
- “[How To Maintain A Large Next.js Application](https://www.smashingmagazine.com/2021/11/maintain-large-nextjs-application/),” Nirmalya Ghosh
- “[How To Migrate From jQuery To Next.js](https://www.smashingmagazine.com/2021/07/migrate-jquery-nextjs/),” Facundo Giuliani
- “[Solving CLS Issues In A Next.js-Powered E-Commerce Website (Case Study)](https://www.smashingmagazine.com/2021/10/nextjs-ecommerce-cls-case-study/),” Arijit Mondal

{{< signature "vf, yk, il" >}}

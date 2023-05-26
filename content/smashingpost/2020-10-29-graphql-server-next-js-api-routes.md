---
title: 'How To Build A GraphQL Server Using Next.js API Routes'
slug: graphql-server-next-javascript-api-routes
author: ibrahima-ndaw
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e42d9b27-ab11-4444-9559-3581f89da272/graphql-server-next-javascript-api-routes.png
date: 2020-10-29T11:00:00.000Z
summary: >-
  This guide will teach you the basics of Next.js API Routes. We will start by explaining what they are and why API Routes are useful compared to REST or GraphQL APIs. Then, we will guide you through a step by step tutorial on how to build your very first GraphQL server with Next.js and the Github API.
description: >-
  This guide will teach you the basics of Next.js API Routes. We will start by explaining what they are and why API Routes are useful compared to REST or GraphQL APIs. Then, we will guide you through a step by step tutorial on how to build your very first GraphQL server with Next.js and the Github API.
categories:
  - API
  - React
  - JavaScript
  - GraphQL
  - Next.js
---

Next.js gives you the best developer experience with all the features you need for production. It provides a straightforward solution to build your API using Next.js API routes.

In this guide, we will be first learning what are API Routes, and then create a GraphQL server that retrieves the data from the Github API using the Next.js API Routes.

To get the most out of this tutorial, you need at least a basic understanding of GraphQL. Knowledge of Apollo Server would help but is not compulsory. This tutorial would benefit those who want to extend their React or Next.js skills to the server-side and be able to build as well their first full-stack app with Next.js and GraphQL.

So, let’s dive in.

## What Are Next.js API Routes?

Next.js is a framework that enables rendering React apps on the client or/and the server. Since version 9, Next.js can now be used to build APIs with Node.js, Express, GrapQL, and so on. Next.js uses the file-system to treat files inside the folder `pages/api` as API endpoints. Meaning that, now, you will be able to access your API endpoint on the URL `https://localhost:3000/api/your-file-name`.

If you came from React and never used Next.js, this might be confusing because Next.js is a React framework. And as we already know, React is used to build front-end apps. So why use Next.js for backend apps and APIs?

Well, Next.js can both be used on the client and server sides because it is built with React, Node.js, Babel, and Webpack, and obviously, it should be usable on the server as well. Next.js relies on the server to enable API Routes and lets you use your favorite backend language even if it’s technically a React framework. Hopefully, you get it right.

So far, we have learned what API Routes are. However, the real question remains: *why use Next.js to build a GraphQL Server*? Why not use GraphQL or Node.js to do so? So, let’s compare Next.js API Routes to existing solutions for building APIs in the next section.

## Next.js API Routes Versus REST And GraphQL

GraphQL and REST are great ways of building APIs. They are super popular and used by almost every developer nowadays. So, why use a React framework to build APIs? Well, the quick answer is that Next.js API Routes are on a different purpose because API Routes allows you to extend your Next.js App by adding a backend to it. 

There are better solutions for building APIs such as Node.js, Express, GraphQL, and so on since they are focused on the backend. In my opinion, the API Routes should be coupled with a client-side to build up a full-stack app with Next.js. Using the API Routes to build a simple API is like underusing the power of Next.js because it’s a React framework that enables you to add a backend to it in no-time.

Consider the use-case when you need to add authentication to an existing Next App. Instead of building the auth part from scratch with Node.js or GraphQL, you can use API Routes to add authentication to your app, and it will still be available on the endpoint `https://localhost:3000/api/your-file-name`. The API Routes won’t increase your client-side bundle size because they are server-side only bundles.

However, Next.js API Routes are only accessible within the same-origin because API Routes do not specify [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) headers. You can still tweak the default behavior by adding CORS to your API &mdash; but it’s an extra setup. If you generate your Next App statically using `next export` &mdash; you won’t be able to use API Routes within your app.

So far, we have learned when API Routes might be a better solution compared to the like. Now, let’s get hands dirty and start building our GraphQL Server.

{{% feature-panel %}}

## Setting Up

To start a new app with Next.js, we will go for Create Next App. It’s also possible to set up manually a new app with Webpack. You are more than welcome to do so. That being said, open your command-line interface and run this command:

<pre><code class="language-javascript">npx create-next-app next-graphql-server</code></pre>

Next.js provides a starter template for API Routes. You can use it by executing the following command:

<pre><code class="language-javascript">npx create-next-app --example api-routes api-routes-app</code></pre>

In this tutorial, we want to do everything from scratch, which is why we use Create Next App to start a new app and not the starter template.
Now, structure the project as follows:

<pre><code class="language-javascript">├── pages
|  ├── api
|  |  ├── graphql.js
|  |  ├── resolvers
|  |  |  └── index.js
|  |  └── schemas
|  |     └── index.js
|  └── index.js
├── package.json
└── yarn.lock
</code></pre>

As we said earlier, the `api` folder is where our API or server lives. Since we will be using GraphQL, we need a resolver and a schema to create a GraphQL server. The endpoint of the server will be accessible on the path `/api/graphql`, which is the entry point of the GraphQL server.

With this step forward, we can now create the GraphQL Schema for our server.

## Create The GraphQL Schemas

As a quick recap, a GraphQL schema defines the shape of your data graph.

Next, we need to install `apollo-server-micro` to use Apollo Server within Next.js.

<pre><code class="language-bash">yarn add apollo-server-micro</code></pre>
    
For `npm`

<pre><code class="language-bash">npm install apollo-server-micro</code></pre>

Now, let’s create a new GraphQL schema.

In `api/schemas/index.js`

<pre><code class="language-javascript">import  {  gql  }  from  "apollo-server-micro"; 

export  const  typeDefs  =  gql`
    type  User {
        id: ID
        login: String
        avatar_url: String
    }

    type  Query {
        getUsers: [User]
        getUser(name: String!): User!
    }`</code></pre>

Here, we define a `User` type that describes the shape of a Github user. It expects an `id` of type `ID`, a `login`, and an `avatar_url` of type String. Then, we use the type on the `getUsers` query that has to return an array of users. Next, we rely on the `getUser` query to fetch a single user. It needs to receive the name of the user in order to retrieve it.

With this GraphQL Schema created, we can now update the resolver file and create the functions to perform these queries above.

{{% ad-panel-leaderboard %}}

## Create The GraphQL Resolvers

A GraphQL resolver is a set of functions that allows you to generate a response from a GraphQL query.

To request data from the Github API, we need to install the `axios` library. So, open your CLI and execute this command:

<pre><code class="language-bash">yarn add axios</code></pre>

Or when using `npm`

<pre><code class="language-bash">npm install axios</code></pre>

Once the library is installed, let’s now add some meaningful code to the resolvers file.

In `api/resolvers/index.js`

<div class="break-out">

<pre><code class="language-javascript">import axios from "axios";

export const resolvers = {
  Query: {
    getUsers: async () =&gt; {
      try {
        const users = await axios.get("https://api.github.com/users");
        return users.data.map(({ id, login, avatar_url }) =&gt; ({
          id,
          login,
          avatar_url
        }));
      } catch (error) {
        throw error;
      }
    },
    getUser: async (&#95;, args) =&gt; {
      try {
        const user = await axios.get(
          `https://api.github.com/users/${args.name}`
        );
        return {
          id: user.data.id,
          login: user.data.login,
          avatar_url: user.data.avatar_url
        };
      } catch (error) {
        throw error;
      }
    }
  }
};</code></pre>
</div>

As you can see here, we match the queries name defined earlier on the GraphQL Schema with the resolver functions. The `getUsers` function enables us to retrieve all users from the API and then return an array of users that needs to mirror the `User` type. Next, we use the `getUser` method to fetch a single user with the help of the name passed in as a parameter.

With this in place, we now have a GraphQL Schema and a GraphQL resolver &mdash; it’s time to combine them and build up the GraphQL Server.

## Create The GraphQL server

A GraphQL server exposes your data as a GraphQL API. It gives clients apps the power to ask for exactly the data they need and nothing more.

In `api/graphql.js`

<div class="break-out">

<pre><code class="language-javascript">import  {  ApolloServer  }  from  "apollo-server-micro";
import  {  typeDefs  }  from  "./schemas";
import  {  resolvers  }  from  "./resolvers";

const  apolloServer  =  new  ApolloServer({  typeDefs,  resolvers  });

export  const  config  =  {
    api:  {
        bodyParser:  false
    }
};

export  default  apolloServer.createHandler({ path:  "/api/graphql"  });</code></pre>
</div>

After importing `ApolloServer`, we use it to create a new instance and then pass in the schema and the resolver to create a GraphQL server. Next, we need to tell Next.js not to parse the incoming request and let GraphQL handle it for us. Finally, we use `apolloServer` to create a new handler, which means the path `/api/graphql` will serve as an entry point for our GraphQL server.

Unlike regular Apollo Server, Next.js handles the start of the server for us since it relies on server-side rendering. That is why, here, we don’t have to start the GraphQL server on our own.

Great! With this step forward, we can now test if the GraphQL server works.

{{% ad-panel-leaderboard %}}

## Test The GraphQL Server

Once you browse to the root of the project, open it on the CLI, and then execute this command:

<pre><code class="language-bash">yarn dev</code></pre>

Or for `npm`

<pre><code class="language-bash">npm run dev</code></pre>

Now, visit `https://localhost:3000/api/graphql` and add the GraphQL query below to retrieve all users from Github.

<pre><code class="language-javascript">{
  getUsers {
    id
    login
    avatar_url
  }
}</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b8ef082-8f9f-4491-a7e3-a5a53358d89a/1-graphql-server-next-js-api-routes.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b8ef082-8f9f-4491-a7e3-a5a53358d89a/1-graphql-server-next-js-api-routes.PNG" sizes="100vw" caption="get-all-users. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b8ef082-8f9f-4491-a7e3-a5a53358d89a/1-graphql-server-next-js-api-routes.PNG'>Large preview</a>)" alt="get-all-users" >}}

Let’s check if we can fetch a single user with this query.

<pre><code class="language-javascript">query($name: String!){
  getUser(name:$name){
        login
    id
    avatar_url
  }
}</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61e2bea4-5a2f-47b5-9b60-5f86a7b9b65f/2-graphql-server-next-js-api-routes.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61e2bea4-5a2f-47b5-9b60-5f86a7b9b65f/2-graphql-server-next-js-api-routes.PNG" sizes="100vw" caption="get-user. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61e2bea4-5a2f-47b5-9b60-5f86a7b9b65f/2-graphql-server-next-js-api-routes.PNG'>Large preview</a>)" alt="get-user" >}}

Great! Our server works as expected. We are done building a GraphQL server using Next.js API Routes.

## Conclusion

In this tutorial, we walked through Next.js API Routes by first explaining what they are and then build a GraphQL server with Next.js. The ability to add a backend to Next.js apps is a really nice feature. It allows us to extend our apps with a real backend. You can even go further and connect a database to build a complete API using API Routes. Next.js definitely makes it easier to build a full-stack app with the API Routes.

You can preview the [finished project on CodeSandbox](https://9y1ut.sse.codesandbox.io/api/graphql).

Thanks for reading!

### Further Resources

These useful resources will take you beyond the scope of this tutorial.

- [Introducing API Routes (Next.js 9)](https://nextjs.org/blog/next-9)
- [Next.js API Routes](https://nextjs.org/docs/api-routes/introduction)
- [API Routes Middleware](https://github.com/vercel/next.js/tree/canary/examples/api-routes-middleware)

{{< signature "ks, ra, yk, il" >}}

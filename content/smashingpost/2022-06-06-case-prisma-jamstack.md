---
title: 'The Case For Prisma In The Jamstack'
slug: case-prisma-jamstack
author: sam-poder
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30c31583-7e46-4566-b2d3-bef54dd64152/case-prisma-jamstack.jpg
date: 2022-06-06T09:00:00.000Z
summary: >-
  Jamstack has surged in popularity over the past few years as an approach to building websites. As developers are building Jamstack sites, finding a well-integrated method to interact with a database can be a major stumbling block. In this article, Sam Poder explores how Prisma integrates with the Jamstack and why it’s a great solution for Serverless databases in JavaScript or TypeScript-based projects.
description: >-
  In this article, Sam Poder explores how Prisma integrates with the Jamstack and why it’s a great solution for Serverless databases in JavaScript or TypeScript-based projects.
categories:
  - Jamstack
  - JavaScript
  - Serverless
  - Next.js
---

The Jamstack approach originated from a speech given by Netlify’s CEO Matt Biilmann at Smashing Magazine’s very own Smashing Conf in 2016.

Jamstack sites serve static pre-rendered content through a CDN and generate dynamic content through microservices, APIs & serverless functions. They are commonly created using JavaScript frameworks, such as Next.js or Gatsby, and static site generators &mdash; Hugo or Jekyll, for example. Jamstack sites often use a Git-based deployment workflow through tools, such as Vercel and Netlify. These deployment services can be used in tandem with a headless CMS, such as Strapi. 

The goal of using Jamstack to build a site is to create a site that is high performant and economical to run. These sites achieve high speeds by pre-rendering as much content as possible and by caching responses on “the edge” (A.K.A. executing on servers as close to the user as possible, e.g. serving a Mumbai-based user from a server in Singapore instead of San Francisco). 

Jamstack sites are more economical to run, as they don’t require using a dedicated server as a host. Instead, they can provision usage from cloud services (PAASs) / hosts / CDNs for a lower price. These services are also set up to scale in a cost-efficient manner, without developers changing their infrastructure and reducing their workload. 

The other tool that makes up this combination is Prisma &mdash; an open source ORM (object relational mapping) built for TypeScript & JavaScript. 

<blockquote>Prisma is a JavaScript / TypeScript tool that interpretes a schema written in Prisma’s standards and generates a type-safe module that provides methods to create records, read records, update records, and delete records (CRUD).</blockquote>

Prisma handles connections to the database (including pooling) and database migrations. It can connect with databases that use PostgreSQL, MySQL, SQL Server or SQLite (additionally MongoDB support is in preview).

To help you get a sense of Prisma, here’s the some basic example code to handle the CRUD of users:

<pre><code class="language-javascript">import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

const user = await prisma.user.create({
  data: {
    name: Sam,
    email: 'sam@sampoder.com',
  },
})

const users = await prisma.user.findMany()

const updateUser = await prisma.user.update({
  where: {
    email: 'sam@sampoder.com',
  },
  data: {
    email: 'deleteme@sampoder.com',
  },
})

const deleteUser = await prisma.user.delete({
  where: {
    email: 'deleteme@sampoder.com',
  },
})</code></pre>

The associated project’s Prisma schema would look like:

<pre><code class="language-javascript">datasource db {
  url      = env("DATABASE_URL")
  provider = "postgresql"
}

generator client {
  provider = "prisma-client-js"
}

model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String?
}</code></pre>

{{% feature-panel %}}

## The Use Cases for Prisma

Armed with a knowledge of how Prisma operates, let’s now explore where we can use it within Jamstack projects. Data is important in two aspects of the Jamstack: whilst pre-rendering static pages and on API routes. These are tasks often achieved using JavaScript tools, such as Next.js for static pages and Cloudfare Workers for API routes. Admitally, these aren’t always achieved with JavaScript &mdash; Jekyll, for example, uses Ruby! So, maybe I should amend the title for the case of Prisma in JavaScript-based Jamstack. Anyhow, onwards!

A very common use-case for the Jamstack is a blog, where Prisma will come in handy for a blog to create a reactions system. You’d use it in API routes with one that would fetch and return the reaction count and another that could register a new reaction. To achieve this, you could use the `create` and `findMany` methods of Prisma!

Another common use-case for the Jamstack is a landing page, and there’s nothing better than a landing with some awesome stats! In the Jamstack, we can pre-render these pages with stats pulled from our databases which we can achieve using Prisma’s reading methods.

Sometimes, however, Prisma can be slightly overkill for certain tasks. I’d recommend avoiding using Prisma and relational databases in general for solutions that need only a single database table, as it adds additional and often unnecessary development complexity in these cases. For example, it’d be overkill to use Prisma for an email newsletter signup box or a contact form. 

{{% ad-panel-leaderboard %}}

## Alternatives to Prisma

So, we could use Prisma for these tasks, but we could use a plethora of other tools to achieve them. So, why Prisma? Let’s go through three Prisma alternatives, and I’ll try to convince you that Prisma is preferable.

### Cloud Databases / Services

Services like Airtable are incredibly popular in the Jamstack space (I myself have used it a ton), they provide you with a database (like platform) that you can access through a REST API. They’re good fun to use and prototype with, however, Prisma is arguably a better choice for Jamstack projects.

Firstly, with cost being a major factor in Jamstack’s appeal, you may want to avoid some of these services. For example, at Hack Club, we spent $671.54 on an Airtable Pro subscription last month for our small team (yikes!).

On the other hand, hosting an equivalent PostgreSQL database on Heroku’s platform costs $9 a month. There certainly is an argument to make for these cloud services based on their UI and API, but I would respond by pointing you to Prisma’s Studio and aforementioned JavaScript / TypeScript client.

Cloud services also suffer from a performance-issue, especially considering that you, as the user, have no ability to change / improve the performance. The cloud services providing the database put a middleman in between your program and the database they’re using, slowing down how fast you can get to the database. However, with Prisma you’re making direct calls to your database from your program which reduces the time to query / modify the database.

### Writing Pure SQL

So, if we’re going to access our PostgreSQL database directly, why not just use the node-postgres module or &mdash; for many other databases &mdash; their equivalent drivers? I’d argue that the developer experience of using Prisma’s client makes it worth the slightly increased load.

Where Prisma shines is with its typings. The module generated for you by Prisma is fully type-safe &mdash; it interprets the types from your Prisma schema &mdash; which helps you prevent type errors with your database. Furthermore, for projects using TypeScript, Prisma auto-generates type definitions that reflect the structure of your model. Prisma uses these types to validate database queries at compile-time to ensure they are type-safe.

Even if you aren’t using TypeScript, Prisma also offers autocomplete / Intelli-sense, linting, and formatting through its Visual Studio Code extension. There are also community built / maintained plugins for Emacs (emacs-prisma-mode), neovim (coc-prisma), Jetbrains IDE (Prisma Support), and nova (the Prisma plugin) that implement the Prisma Language Server to achieve code validation. Syntax highlighting is also available for a wide array of editors through plugins.

### Other ORMs

Prisma is, of course, not the only ORM available for JavaScript / TypeScript. For example, TypeORM is another high quality ORM for JavaScript projects. And in this case, it is going to come down to personal preference, and I encourage you to try a range of ORMs to find your favourite. I personally choose Prisma to use for my project for three reasons: the extensive documentation (especially [this CRUD page](https://www.prisma.io/docs/concepts/components/prisma-client/crud), which is a lifesaver), the additional tooling within the Prisma ecosystem (e.g. Prisma Migrate and Prisma Studio), and the active community around the tool (e.g. Prisma Day and the Prisma Slack). 

## Using Prisma in Jamstack Projects

So, if I’m looking to use Prisma in a Jamstack project, how do I do that?

{{% ad-panel-leaderboard %}}

### Next.js

Next.js is growing to be a very popular framework in the Jamstack space, and Prisma is a perfect fit for it. The examples below will serve as pretty standard examples that you can transfer into other projects using different JavaScript / TypeScript Jamstack tools.

The main rule of using Prisma within Next.js is that it must be used in a server-side setting, this means that it can be used in `getStaticProps`, `getServerSideProps`, and in API routes (e.g. `api/emojis.js`).

In code, it looks like this ([example taken from a demo app](https://github.com/sampoder/prisma-day-2021) I made for a talk at Prisma Day 2021 which was a virtual sticker wall):

<pre><code class="language-javascript">import prisma from '../../../lib/prisma'
import { getSession } from 'next-auth/client'

function getRandomNum(min, max) {
  return Math.random() &#42; (max - min) + min
}

export async function getRedemptions(username) {
  let allRedemptions = await prisma.user.findMany({
    where: {
      name: username,
    },
    select: {
      Redemptions: {
        select: {
          id: true,
          Stickers: {
            select: { nickname: true, imageurl: true, infourl: true },
          },
        },
        distinct: ['stickerId'],
      },
    },
  })
  allRedemptions = allRedemptions[0].Redemptions.map(x =&gt; ({
    number: getRandomNum(-30, 30),
    ...x.Stickers,
  }))
  return allRedemptions
}

export default async function RedeemCodeReq(req, res) {
  let data = await getRedemptions(req.query.username)
  res.send(data)
}</code></pre>

As you can see, it integrates really well into a Next.js project. But you may notice something interesting: `'../../../lib/prisma'`. Previously, we imported Prisma like this:

<pre><code class="language-javascript">import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()</code></pre>

Unfortunately, this is due to a quirk in Next.js’ live refresh system. So, Prisma recommends you paste [this code snippet](https://www.prisma.io/docs/support/help-articles/nextjs-prisma-client-dev-practices) into a file and import the code into each file.

### Redwood

Redwood is a bit of an anomaly in this section, as it isn’t necessarily a Jamstack framework. It began under the banner of bringing full stack to the Jamstack but has transitioned to being inspired by Jamstack. I’ve chosen to include it here, however, as it takes an interesting approach of including Prisma within the framework. 

It starts, as always, with creating a Prisma schema, this time in `api/db/schema.prisma` (Redwood adds this to every new project). However, to query and modify the database, you don’t use Prisma’s default client. Instead, in Redwood, GraphQL mutations and queries are used. For example, in Redwood’s example todo app, this is the GraphQL mutation used to create a new todo:

<pre><code class="language-javascript">const CREATE&#95;TODO = gql`
  mutation AddTodo_CreateTodo($body: String!) {
    createTodo(body: $body) {
      id
      &#95;&#95;typename
      body
      status
    }
  }
`</code></pre>

And in this case, the Prisma model for a todo is:

<pre><code class="language-javascript">model Todo {
  id     Int    @id @default(autoincrement())
  body   String
  status String @default("off")
}</code></pre>

To trigger the GraphQL mutation, we use the `useMutation` function which is based on Apollo’s GraphQL client imported from `@redwoodjs/web`:

<div class="break-out">

<pre><code class="language-javascript">const [createTodo] = useMutation(CREATE&#95;TODO, {
    //  Updates Apollo's cache, re-rendering affected components
    update: (cache, { data: { createTodo } }) =&gt; {
      const { todos } = cache.readQuery({ query: TODOS })
      cache.writeQuery({
        query: TODOS,
        data: { todos: todos.concat([createTodo]) },
      })
    },
  })

  const submitTodo = (body) =&gt; {
    createTodo({
      variables: { body },
      optimisticResponse: {
        &#95;&#95;typename: 'Mutation',
        createTodo: { &#95;&#95;typename: 'Todo', id: 0, body, status: 'loading' },
      },
    })
  }</code></pre>
</div>

With Redwood, you don’t need to worry about setting up the GraphQL schema / SDLs after creating your Prisma schema, as you can use Redwood’s `scaffold` command to convert the Prisma schema into GraphQL SDLs and services &mdash; `yarn rw g sdl Todo`, for example.

### Cloudfare Workers

Cloudfare Workers is a popular platform for hosting Jamstack APIs, as it puts your code on the “edge”. However, the platform has its limitations, including a lack of TCP support, which the traditional Prisma Client uses. Though now, through Prisma Data Proxy, it is possible.

To use it, you’ll need a [Prisma Cloud Platform](https://cloud.prisma.io/) account which is currently free. Once you’ve followed the setup process (make sure to enable Prisma Data Proxy), you’ll be provided with a connection string that begins with `prisma://`. You can use that Prisma connection string in your `.env` file in place of the traditional database URL:

<pre><code class="language-bash">DATABASE_URL="prisma://aws-us-east-1.prisma-data.com/?api_key=•••••••••••••••••"</code></pre>

And then, instead of using `npx prisma generate`, use this command to generate a Prisma client:

<pre><code class="language-bash">PRISMA_CLIENT_ENGINE_TYPE=dataproxy npx prisma generate</code></pre>

Your database requests will be proxied through, and you can use the Prisma Client as usual. It isn’t a perfect set-up, but for those looking for database connections on Cloudfare Workers, it’s a relatively good solution.

## Conclusion

To wrap up, if you’re looking for a way to connect Jamstack applications with a database, I wouldn’t look further than Prisma. Its developer experience, extensive tooling, and performance make it the perfect choice. Next.js, Redwood, and Cloudfare Workers &mdash; each of them has a unique way of using Prisma, but it still works very well in all of them. 

I hope you’ve enjoyed exploring Prisma with me. Thank you!

### Further Reading on Smashing Magazine

- “[Jamstack Rendering Patterns: The Evolution](https://www.smashingmagazine.com/2022/04/jamstack-rendering-patterns-evolution/),” Ekene Eze
- “[Interactive Learning Tools For Front-End Developers](https://www.smashingmagazine.com/2021/09/interactive-learning-tools-front-end-developers/),” Louis Lazaris
- “[Jamstack CMS: The Past, The Present and The Future](https://www.smashingmagazine.com/2021/08/history-future-jamstack-cms/),” Mike Neumegen
- “[Smashing Podcast Episode 29 With Leslie Cohn-Wein: How Does Netlify Dogfood The Jamstack?](https://www.smashingmagazine.com/2020/11/smashing-podcast-episode-29/),” Drew McLellan

{{< signature "vf, yk, il" >}}

---
title: 'Yarn Workspaces: Organize Your Project’s Codebase Like A Pro'
slug: yarn-workspaces-organize-project-codebase-pro
author: jorge-ferreiro
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de862766-092e-4920-886e-5b4bef31ea79/yarn-workspaces-sharing-card.png
date: 2019-07-18T12:00:59+02:00
summary: >-
  Yarn workspaces let you organize your project codebase using a monolithic repository (monorepo). In this article, Jorge explains why they’re a great tool and how to create your first monorepo using Yarn with basic npm scripts, and add the required dependencies for each app.
description: >-
  In this article, Jorge explains why they’re a great tool and how to create your first monorepo using Yarn with basic npm scripts, and add the required dependencies for each app.
categories:
  - React
  - Coding
  - Techniques
---

Any time I start working on a new project, I ask myself, “Should I use separate git repositories for my back-end server and my front-end client(s)? What’s the best way to organize the codebase?”

I had this same question after a few months working on my personal [website](https://jorgeferreiro.com/). I originally had all the code in the same repository: the back end used Node.js and the front end used ES6 with Pug. I adopted this organization for convenience, since having both projects in the same repo made it easy to search for functions and classes, and facilitated refactors. However, I found some downsides:

- **No independent deployments.**  
Both apps were using the same _package.json_, and there was no clear separation on both projects.
- **Unclear boundaries.**  
Since I rely on a global _package.json_, I didn’t have a mechanism to set specific versions for the back end and front end.
- **Shared utilities and code without versioning.**

After some research, I found that Yarn workspaces was a great tool to solve those cons, and it was a helpful tool to create a monorepo project (more to come later!). 

In this article, I share an intro to Yarn workspaces. We’ll run through a tutorial together on how to create your first project with it, and we’ll finish with a recap and next steps.

{{% feature-panel %}}

## What Are Yarn Workspaces?

Yarn is a package manager by the folks at Facebook, and it has a great feature called [Yarn workspaces](https://yarnpkg.com/lang/en/docs/workspaces/). Yarn workspaces let you organize your project codebase using a monolithic repository (monorepo). The idea is that a single repository would contain multiple packages. Packages are isolated and could live independent of the larger project.

{{< rimg href="https://yarnpkg.com/lang/en/docs/workspaces/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2c71f10-3c0a-4252-97a9-5e72480efa71/yarn-workspaces-cover.jpg" sizes="100vw" caption="" alt="Yarn Workspaces" >}}

As an alternative, we could place all of these packages into separate repositories. Unfortunately, this approach affects the shareability, efficiency, and developer experience when developing on the packages and their dependent projects. Furthermore, when we work in a single repository we can move more swiftly and build more specific tooling to improve processes for the entire development life cycle.

{{% pull-quote %}}
 Monorepo projects have been widely accepted by large companies like Google or Facebook, and they have proven <a href="https://cacm.acm.org/magazines/2016/7/204032-why-google-stores-billions-of-lines-of-code-in-a-single-repository/fulltext">monorepo can scale</a>.
{{% /pull-quote %}}

[React](https://github.com/facebook/react/tree/master/packages) is a good example of an open-source project that is monorepo. Also, React uses Yarn workspaces to achieve that purpose. In the next section we will learn how to create our first monorepo project with Yarn.

## Creating A Monorepo Project With React And Express Using Yarn Workspaces In Six Steps

So far, we have learned what Yarn is, what a monorepo is, and why Yarn is a great tool to create a monorepo. Now let’s learn from scratch how to set up a new project using Yarn workspaces. To follow along, you’ll need a working environment with an up-to-date npm install. [Download the source code](https://github.com/ferreiro/example-monorepo).

### Prerequisites

To fully complete this tutorial, you will need to have Yarn installed on your machine. If you haven’t installed Yarn before, please follow [these instructions](https://yarnpkg.com/lang/en/docs/install/#mac-stable).

These are the steps we’ll be following in this tutorial:

<ol>
  <li><a href="#project-root-workspace">Create Your Project And Root Workspace</a></li>
  <li><a href="#react-project-add-workspace-list">Create A React Project And Add It To The Workspace List</a></li>
  <li><a href="#express-project-add-workspace">Create An Express Project And Add It To The Workspace</a></li>
  <li><a href="#install-all-dependencies-say-hello-yarn-lock">Install All The Dependencies And Say Hello To yarn.lock</a></li>
  <li><a href="#wildcard-import-all-packages">Using A Wildcard (&#42;) To Import All Your Packages</a></li>
  <li><a href="#script-run-both-packages">Add A Script To Run Both Packages</a></li>
</ol>

### 1. Create Your Project And Root Workspace

In your local machine terminal, create a new folder called `example-monorepo`:

<pre><code class="language-bash">$ mkdir example-monorepo
</code></pre>

Inside the folder, create a new _package.json_ with our root workspace.

<pre><code class="language-json">$ cd example-monorepo
$ touch package.json
</code></pre>

This package should be private in order to prevent accidentally publishing the root workspace. Add the following code to your new _package.json_ file to make the package private:

<pre><code class="language-json">{
   "private": true,
   "name": "example-monorepo",
   "workspaces": [],
   "scripts": {}
}
</code></pre>

### 2. Create A React Project And Add It To The Workspace List

In this step, we will create a new React project and add it to the list of packages inside the root workspace.

First, let’s create a folder called _packages_ where we will add the different projects we will create in the tutorial:

<pre><code class="language-bash">$ mkdir packages
</code></pre> 

Facebook has a command to create new React projects: `create-react-app`. We’ll use it to create a new React app with all the required configuration and scripts. We are creating this new project with the name “client” inside the _packages_ folder that we created in step 1.

<pre><code class="language-bash">$ yarn create react-app packages/client
</code></pre>

Once we have created our new React project, we need to tell Yarn to treat that project as a workspace. To do that, we simply need to add “client” (the name we used earlier) inside the “workspaces” list in the root _package.json_. Be sure to use the same name you used when running the `create-react-app` command.

<pre><code class="language-json">{
   "private": true,
   "name": "example-monorepo",
   "workspaces": ["client"],
   "scripts": {}
}
</code></pre>

### 3. Create An Express Project And Add It To The Workspace

Now it’s time to add a back-end app! We use `express-generator` to create an Express skeleton with all the required configuration and scripts.

Make sure you have [`express-generator`](https://expressjs.com/en/starter/generator.html) installed on your computer. You can install it using Yarn with the following command:

<pre><code class="language-yarn">$ yarn global add express-generator --prefix /usr/local
</code></pre>

Using `express-generator`, we create a new Express app with the name “server” inside the _packages_ folder.

<pre><code class="language-bash">$ express --view=pug packages/server
</code></pre>

Finally, add the new package “server” into the workspaces list inside the root _package.json_.

<pre><code class="language-json">{
   "private": true,
   "name": "example-monorepo",
   "workspaces": ["client", "server"],
   "scripts": {}
}
</code></pre>

**Note**: *This tutorial is simplified with only two packages (server and client). In a project, you might typically have as many packages as you need, and by convention the open-source community use this naming pattern:* `@your-project-name/package-name`. *For example: I use* `@ferreiro/server` *on my [website](https://github.com/ferreiro/website/blob/master/packages/ferreiro-server/package.json#L2).*

{{% ad-panel-leaderboard %}}

### 4. Install All The Dependencies And Say Hello To yarn.lock

Once we have added our React app, as well as our Express server, we need to install all the dependencies. Yarn workspaces simplifies this process and we no longer need to go to every single application and install their dependencies manually. Instead, we execute one command &mdash; `yarn install` &mdash; and Yarn does the magic to install all the dependencies for every package, and optimize and cache them.

Run the following command:

<pre><code class="language-bash">$ yarn install
</code></pre>

This command generates a _[yarn.lock](https://yarnpkg.com/lang/en/docs/yarn-lock/)_ file ([similar to this example](https://github.com/ferreiro/example-monorepo/blob/master/yarn.lock#L12)). It contains all the dependencies for your project, as well as the version numbers for each dependency. Yarn generates this file automatically, and you should not modify it. 


### 5. Using A Wildcard (&#42;) To Import All Your Packages

Until now, for every new package we have added, we were forced to also update the root _package.json_ to include the new package to the `workspaces:[]` list.

We can avoid this manual step using a wildcard (&#42;) that tells Yarn to include all the packages inside the _packages_ folder.

Inside the root _package.json_, update the file content [with the following line](https://github.com/ferreiro/example-monorepo/blob/master/package.json#L12): `"workspaces": ["packages/*"]`

<pre><code class="language-json">{
   "private": true,
   "name": "example-monorepo",
   "workspaces": ["packages/*"],
   "scripts": {}
}
</code></pre>

### 6. Add A Script To Run Both Packages

Last step! We need to have a way to run both packages &mdash; the React client and the Express client &mdash; simultaneously. For this example, we will use [`concurrently`](https://www.npmjs.com/package/concurrently). This package let us run multiple commands in parallel.

Add `concurrently` to the root _package.json_:

<pre><code class="language-json">$ yarn add -W concurrently
</code></pre>

Add three new scripts inside the root workspace _package.json_. Two scripts initialize the React and Express clients independently; the other one uses `concurrently` to run both scripts in parallel. [See this code for reference](https://github.com/ferreiro/example-monorepo/blob/master/package.json#L8-L10).

<div class="break-out">

 <pre><code class="language-json">{
   "private": true,
   "name": "example-monorepo",
   "workspaces": ["packages/*"],
   "scripts": {
       "client": "yarn workspace client start",
       "server": "yarn workspace server start",
       "start": "concurrently --kill-others-on-fail \"yarn server\"  \"yarn client\"
   }
}
</code></pre>
</div>

**Note**: *We will not need to write our* `start` *scripts into the “server” and “client” packages because the tools we used to generate those packages (*`create-react-app` *and* `express-generator`*) already add those scripts for us. So we are good to go!*

Finally, make sure you update the Express boot-up script to run the Express server on port 4000. Otherwise, the client and server will try to use the same port (3000).

Go to *packages/server/bin/www* and [change the default port in line 15](https://github.com/ferreiro/example-monorepo/blob/master/packages/server/bin/www#L15).

<pre><code class="language-javascript">var port = normalizePort(process.env.PORT || '4000');
</code></pre>

Now we are ready to run our packages!

<pre><code class="language-bash">$ yarn start
</code></pre>

{{% ad-panel-leaderboard %}}

## Where To Go From Here

Let’s recap what we’ve covered. First, we learned about Yarn workspaces and why it’s a great tool to create a monorepo project. Then, we created our first JavaScript monorepo project using Yarn, and we divided the logic of our app into multiple packages: client and server. Also, we created our first basic npm scripts and added the required dependencies for each app.

From this point, I’d suggest you review open-source projects in detail to see how they use Yarn workspaces to split the project logic into many packages. [React](https://github.com/facebook/react/tree/master/packages) is a good one.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93942069-fa72-496d-937b-adfe90a06020/jorge-ferreiro-website-yarn-workspaces-packages.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93942069-fa72-496d-937b-adfe90a06020/jorge-ferreiro-website-yarn-workspaces-packages.jpg" sizes="100vw" caption="Jorge Ferreiro’s website using yarn workspaces and packages with a back-end and frontend apps (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93942069-fa72-496d-937b-adfe90a06020/jorge-ferreiro-website-yarn-workspaces-packages.jpg'>Large preview</a>)" alt="Jorge Ferreiro’s website using yarn workspaces and packages with a back-end and frontend apps" >}}

Also, if you want to see a production website using this approach to separate back-end and front-end apps into independent packages, you can check the source of my [website](https://jorgeferreiro.com/), that also includes a [blog admin](https://github.com/ferreiro/website). When I migrated the codebase to use Yarn workspaces, I created a [pull request](https://github.com/ferreiro/website/pull/40) with [Kyle Wetch](https://twitter.com/kylewelch).

Moreover, I set up the infrastructure for a hackathon project that uses React, webpack, Node.js, and Yarn workspaces, and you can check the source code over [here.](https://github.com/ferreiro/facebook-hackathon)

Finally, it would be really interesting for you to learn how to publish your independent packages to become familiar with the development life cycle. There are a couple of tutorials that are interesting to check: [yarn publish](https://yarnpkg.com/lang/en/docs/publishing-a-package/) or [npm publish](https://hackernoon.com/publish-your-own-npm-package-946b19df577e).

For any comments or questions, don’t hesitate to reach out to me on [Twitter](https://twitter.com/JGFerreiro). Also, in the following months, I’ll publish more content about this in my [blog](https://jorgeferreiro.com/blog), so you can subscribe there as well. Happy coding!

{{< signature "dm, og, il" >}}

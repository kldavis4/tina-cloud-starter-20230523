---
title: 'Building An API With Gatsby Functions'
slug: building-api-gatsby-functions
author: paul-scanlon
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/110c2aa7-7744-48d6-a234-9e67e903cbe5/building-api-gatsby-functions.jpg
date: 2021-10-19T14:00:00.000Z
summary: >-
  In this tutorial, Paul Scanlon explains how to build an API by using Gatsby Functions and what you need to keep in mind when deploying it to Gatsby Cloud.
description: >-
  In this tutorial, Paul Scanlon explains how to build an API by using Gatsby Functions and what you need to keep in mind when deploying it to Gatsby Cloud.
categories:
  - API
  - Tools
  - Gatsby
  - Serverless
---

You’ve probably heard about Serverless Functions, but if you haven’t, Serverless Functions provide functionality typically associated with server-side technologies that can be implemented alongside front-end code without getting caught up in server-side infrastructures.

With server-side and client-side code coexisting in the same code base, front-end developers like myself can extend the reach of what’s possible using the tools they already know and love. 

## Limitations

Coexistence is great but there are at least two scenarios I’ve encountered where using Serverless Functions in this way weren’t quite the right fit for the task at hand. They are as follows:

1. The front end couldn’t support Serverless Functions.
2. The same functionality was required by more than one front end.

To help provide some context here’s one example of both points 1 and 2 named above. I maintain an Open-source project called [MDX Embed](https://www.mdx-embed.com/), you’ll see from the docs site that it’s not a Gatsby website. It’s been built using [Storybook](https://storybook.js.org/) and Storybook on its own provides no Serverless Function capabilities. I wanted to implement “Pay what you want” contributions to help fund this project and I wanted to use Stripe to enable secure payments but without a secure “backend” This would not have been possible. 

By abstracting this functionality away into an API built with Gatsby Functions I was able to achieve what I wanted with MDX Embed and also re-use the same functionality and enable “Pay what you want” functionality for [my blog](https://paulie.dev/).

You can read more about how I did that here: [Monetize Open-Source Software With Gatsby Functions And Stripe](https://www.smashingmagazine.com/2021/09/monetize-open-source-software-gatsby-functions-stripe/).

It’s at this point that using Gatsby Functions can act as a kind of **Back end for front end** or BFF 😊 and developing in this way is more akin to developing an API (*Application Programming Interface*).

APIs are used by front-end code to handle things like, logins, real-time data fetching, or secure tasks that aren’t suitably handled by the browser alone. In this tutorial, I’ll explain how to build an API using Gatsby Functions and deploy it to Gatsby Cloud.

{{% feature-panel %}}

## Preflight Checks

Gatsby Functions work when deployed to Gatsby Cloud or Netlify, and in this tutorial, I’ll be explaining how to deploy to Gatsby Cloud so you’ll need to [sign up](https://www.gatsbyjs.com/dashboard/signup) and create a free account first.

You’re also going to need either a GitHub, GitLab or BitBucket account, this is how Gatsby Cloud reads your code and then builds your “site”, or in this case, API. 

For the purposes of this tutorial, I’ll be using GitHub. If you’d prefer to jump ahead, the [finished demo API code can be found on my GitHub](https://github.com/PaulieScanlon/smashing-magazine-gatsby-functions-api).

## Getting Started

Create a new dir somewhere on your local drive and run the following in your terminal. This will set up a default `package.json`.

<pre><code class="language-bash">npm init -y</code></pre>

## Dependencies

Type the following into your terminal to install the required dependencies.

<pre><code class="language-bash">npm install gatsby react react-dom</code></pre>

## Pages

It’s likely your API won’t have any “pages” but to avoid seeing Gatsby’s default *missing page warning* when you visit the root URL in the browser, add the following to both `src/pages/index.js` and `src/pages/404.js`.

<pre><code class="language-javascript">//src/pages/index.js & src/pages/404.js

export default () =&gt; null;</code></pre>

## API

Add the following to `src/api/my-first-function.js`.

I’ll explain a little later what `'Access-Control-Allow-Origin', '*'` means, but in short, it makes sure that your APIs from other origins aren’t blocked by [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS).

<pre><code class="language-javascript">//src/api/my-first-function.js

export default function handler(req, res) {
  res.setHeader('Access-Control-Allow-Origin', '*');

  res.status(200).json({ message: 'A ok!' });
}</code></pre>

## Scripts

Add the following to `package.json`.

<pre><code class="language-javascript">//package.json

...
  "scripts": {
    "develop": "gatsby develop",
    "build": "gatsby build"
  },
...</code></pre>

## Start The Gatsby Development Server

To spin up the Gatsby development server run the following in your terminal.

<pre><code class="language-bash">npm run develop</code></pre>

{{% ad-panel-leaderboard %}}

## Make A Request From The Browser

With the Gatsby’s development server running you can visit [http://localhost:8000/api/my-first-function](http://localhost:8000/api/my-first-function), and since this is a simple `GET` request you should see the following in your browser.

<pre><code class="language-javascript">{
  "message": "A ok!"
}</code></pre>

## Congratulations 🎉

You’ve just developed an API using Gatsby Functions.

## Deploy

If you are seeing the above response in your browser it’s safe to assume your function is working correctly locally, in the following steps I’ll explain how to deploy your API to Gatsby Cloud and access it using an `HTTP` request from CodeSandbox.

## Push Code To Git

Before attempting to deploy to Gatsby Cloud you’ll need to have pushed your code to your Git provider of choice. 

## Gatsby Cloud

Log into your Gatsby Cloud account and look for the big purple button that says “Add site +”.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e18d48c-1680-459e-bb3f-b13867984872/10-building-api-gatsby-functions.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e18d48c-1680-459e-bb3f-b13867984872/10-building-api-gatsby-functions.jpg" width="800" height="450" sizes="100vw" caption="Add a site to Gatsby Cloud. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e18d48c-1680-459e-bb3f-b13867984872/10-building-api-gatsby-functions.jpg'>Large preview</a>)" alt="Screenshot of Gatsby Cloud Add site" >}}

In the next step, you’ll be asked to either Import from a Git repository or Start from a Template, select `Import from Git Repository` and hit `next`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c6aebdc-0d32-46c9-84e4-28ce2f7b7b96/8-building-api-gatsby-functions.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c6aebdc-0d32-46c9-84e4-28ce2f7b7b96/8-building-api-gatsby-functions.jpg" width="800" height="450" sizes="100vw" caption="Select import from a Git repository. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c6aebdc-0d32-46c9-84e4-28ce2f7b7b96/8-building-api-gatsby-functions.jpg'>Large preview</a>)" alt="Screenshot select import from a Git repository" >}}

As mentioned above Gatsby Cloud can connect to either GitHub, GitLab or Bitbucket. Select your preferred Git provider and hit `next`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08fb0157-0b66-4b49-9de6-caf286b726e1/4-building-api-gatsby-functions.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08fb0157-0b66-4b49-9de6-caf286b726e1/4-building-api-gatsby-functions.jpg" width="800" height="450" sizes="100vw" caption="Select from your preferred Git provider. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08fb0157-0b66-4b49-9de6-caf286b726e1/4-building-api-gatsby-functions.jpg'>Large preview</a>)" alt="Screenshot of Gatsby Cloud Git provider selection" >}}

With your Git provider connected, you can search for your repository, and give your site a name.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7deadfe6-20a6-4b13-9575-6b63c1abf42b/6-building-api-gatsby-functions.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7deadfe6-20a6-4b13-9575-6b63c1abf42b/6-building-api-gatsby-functions.jpg" width="800" height="450" sizes="100vw" caption="Search for your site from your Git provider. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7deadfe6-20a6-4b13-9575-6b63c1abf42b/6-building-api-gatsby-functions.jpg'>Large preview</a>)" alt="Screenshot of Gatsby Cloud search for site from Git provider" >}}

Once you’ve selected your repository and named your site hit `next`.

You can skip the “Integrations” and “Setup” as we won’t be needing these.

If all has gone to plan your should be seeing something similar to the below screenshot.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfa8b45d-9ca5-43d2-8cb5-a76795d57f64/11-building-api-gatsby-functions.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfa8b45d-9ca5-43d2-8cb5-a76795d57f64/11-building-api-gatsby-functions.jpg" width="800" height="450" sizes="100vw" caption="‘site’ successfully built and deployed on Gatsby Cloud. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfa8b45d-9ca5-43d2-8cb5-a76795d57f64/11-building-api-gatsby-functions.jpg'>Large preview</a>)" alt="Screenshot of successfully deployed site" >}}

You’ll see near the top on the left-hand side of the screen a URL that ends with `gatsbyjs.io`, this will be the URL for your API and any functions you create can be accessed by adding `/api/name-of-function` to the end of this URL. 

E.g, the complete deployed version of `my-first-function.js` for my demo API is as follows:

[**Demo API: My First Function**](https://smashingapi.gatsbyjs.io/api/my-first-function).

## Testing Your API

Visiting the URL of your API is one thing but it’s not really how APIs are typically used. Ideally to test your API you need to make a request to the function from a completely unrelated origin. 

It’s here where `res.setHeader('Access-Control-Allow-Origin', '*');` comes to the rescue. Whilst it’s not always desirable to allow any domain (website) to access your functions, for the most part, public functions are just that, public. Setting the Access Control header to a value of `*` means any domain can access your function, without this, any domain other than the domain the API is hosted on will be blocked by CORS.  

Here’s a CodeSandbox that uses `my-first-function` from my demo API. You can fork this and change the Axios request URL to test your function.

**CodeSandbox: My First Function**

<iframe src="https://codesandbox.io/embed/smashing-first-function-8relv?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="smashing-first-function"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d96a7007-22e4-4291-9130-78985fad0a65/7-building-api-gatsby-functions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d96a7007-22e4-4291-9130-78985fad0a65/7-building-api-gatsby-functions.png" width="800" height="500" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d96a7007-22e4-4291-9130-78985fad0a65/7-building-api-gatsby-functions.png'>Large preview</a>)" alt="CodeSandbox: My First Function" >}}

## Getting Fancier

Sending a response from your API that says `message: "A ok!"` isn’t exactly exciting so in the next bit I’ll show you how to query the [GitHub REST API](https://docs.github.com/en/rest) and make a personal profile card to display on your own site using the API you just created, and it’ll look a little like this.

**CodeSandbox: Demo profile card**

<iframe src="https://codesandbox.io/embed/smashing-complete-kqcee?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="smashing-complete"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>
   
{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a70a193-0875-4a12-b2a7-699078f2a73f/5-building-api-gatsby-functions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a70a193-0875-4a12-b2a7-699078f2a73f/5-building-api-gatsby-functions.png" width="800" height="500" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a70a193-0875-4a12-b2a7-699078f2a73f/5-building-api-gatsby-functions.png'>Large preview</a>)" alt="CodeSandbox: Demo profile card" >}}

## Dependencies

To use the GitHub REST API you’ll need to install [@octokit/rest](https://www.npmjs.com/package/@octokit/rest) package.

<pre><code class="language-bash">npm install @octokit/rest</code></pre>

{{% ad-panel-leaderboard %}}

## Get GitHub User Raw

Add the following to `src/api/get-github-user-raw.js`.

<pre><code class="language-javascript">// src/api/get-github-user-raw.js

import { Octokit } from '@octokit/rest';

const octokit = new Octokit({
  auth: process.env.OCTOKIT_PERSONAL_ACCESS_TOKEN
});

export default async function handler(req, res) {
  res.setHeader('Access-Control-Allow-Origin', '*');

  try {
    const { data } = await octokit.request(`GET /users/{username}`, {
      username: 'PaulieScanlon'
    });

    res.status(200).json({ message: 'A ok!', user: data });
  } catch (error) {
    res.status(500).json({ message: 'Error!' });
  }
}</code></pre>

## Access Token

To communicate with the GitHub REST API you’ll need an access token. You can get this by following the steps in this guide from GitHub: [Creating A Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

## `.env` Variables

To keep your access token secure add the following to `.env.development` and `.env.production`.

<pre><code class="language-bash">OCTOKIT_PERSONAL_ACCESS_TOKEN=123YourAccessTokenABC</code></pre>

You can read more about Gatsby environment variables in this guide from Gatsby: [Environment Variables](https://www.gatsbyjs.com/docs/how-to/local-development/environment-variables/).

## Start Development Server

As you did before start the Gatsby development server by typing the following in your terminal.

<pre><code class="language-bash">npm run develop</code></pre>

## Make A Request From The Browser

With the Gatsby development server running you can visit [http://localhost:8000/api/get-github-user-raw](http://localhost:8000/api/get-github-user-raw), and since this too is a simple `GET` request you should see the following in your browser. (*I’ve removed part of the response for brevity.*)

<pre><code class="language-javascript">{
  "message": "A ok!",
  "user": {
    "login": "PaulieScanlon",
    "id": 1465706,
    "node_id": "MDQ6VXNlcjE0NjU3MDY=",
    "avatar_url": "https://avatars.githubusercontent.com/u/1465706?v=4",
    "gravatar_id": "",
    "url": "https://api.github.com/users/PaulieScanlon",
    "type": "User",
    "site_admin": false,
    "name": "Paul Scanlon",
    "company": "Paulie Scanlon Ltd.",
    "blog": "https://www.paulie.dev",
    "location": "Worthing",
    "email": "pauliescanlon@gmail.com",
    "hireable": true,
    "bio": "Jamstack Developer / Technical Content Writer (freelance)",
    "twitter_username": "pauliescanlon",
    "created_at": "2012-02-23T13:43:26Z",
    "two_factor_authentication": true,
    ...
  }
}</code></pre>

Here’s a CodeSandbox example of the full raw response.

**CodeSandbox: Raw Response**

<iframe src="https://codesandbox.io/embed/smashing-raw-n0s8c?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="smashing-raw"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>
   
{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8b518e4-b184-4dc5-90e5-8d3c40dc369e/12-building-api-gatsby-functions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8b518e4-b184-4dc5-90e5-8d3c40dc369e/12-building-api-gatsby-functions.png" width="800" height="500" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8b518e4-b184-4dc5-90e5-8d3c40dc369e/12-building-api-gatsby-functions.png'>Large preview</a>)" alt="CodeSandbox: Raw Response" >}}

You’ll see from the above that there’s quite a lot of data returned that I don’t really need, this next bit is completely up to you as it’s your API but I have found it helpful to manipulate the GitHub API response a little bit before sending it back to my frontend code. 

If you’d like to do the same you could create a new function and add the following to `src/api/get-github-user.js`.

<pre><code class="language-javascript">// src/api/get-github-user.js

import { Octokit } from '@octokit/rest';

const octokit = new Octokit({
  auth: process.env.OCTOKIT_PERSONAL_ACCESS_TOKEN
});

export default async function handler(req, res) {
  res.setHeader('Access-Control-Allow-Origin', '*');

  try {
    const { data } = await octokit.request(`GET /users/{username}`, {
      username: 'PaulieScanlon'
    });

    res.status(200).json({
      message: 'A ok!',
      user: {
        name: data.name,
        blog_url: data.blog,
        bio: data.bio,
        photo: data.avatar_url,
        githubUsername: `@${data.login}`,
        githubUrl: data.html_url,
        twitterUsername: `@${data.twitter_username}`,
        twitterUrl: `https://twitter.com/${data.twitter_username}`
      }
    });
  } catch (error) {
    res.status(500).json({ message: 'Error!' });
  }
}</code></pre>

You’ll see from the above that rather than returning the complete data object returned by the GitHub REST API I pick out just the bits I need, rename them and add a few bits before the username and URL values. This makes life a bit easier when you come to render the data in the frontend code.

Here’s a CodeSandbox example of the formatted response.

**CodeSandbox: Formatted Response**

<iframe src="https://codesandbox.io/embed/smashing-formatted-ivwdi?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="smashing-formatted"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>
   
{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a77f9b2c-398b-41c3-9fe9-322b48f7054f/2-building-api-gatsby-functions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a77f9b2c-398b-41c3-9fe9-322b48f7054f/2-building-api-gatsby-functions.png" width="800" height="500" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a77f9b2c-398b-41c3-9fe9-322b48f7054f/2-building-api-gatsby-functions.png'>Large preview</a>)" alt="CodeSandbox: Formatted Response" >}}

This is very similar to the Profile Card CodeSandbox from earlier, but I’ve also printed the data out so you can see how each manipulated data item is used.

It’s worth noting at this point that all four of the CodeSandbox demos in this tutorial are using the demo API, and none of them are built using Gatsby or hosted on Gatsby Cloud &mdash; cool ay! 

## `.env` Variables In Gatsby Cloud

Before you deploy your two new functions you’ll need to add the GitHub Access token to the environment variables section in Gatsby Cloud.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b71c8550-b8e4-4d5a-a0f7-33991e61708e/9-building-api-gatsby-functions.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b71c8550-b8e4-4d5a-a0f7-33991e61708e/9-building-api-gatsby-functions.jpg" width="800" height="450" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b71c8550-b8e4-4d5a-a0f7-33991e61708e/9-building-api-gatsby-functions.jpg'>Large preview</a>)" alt="Screenshot of Gatsby Cloud with Site Settings" >}}

## Where To Go From Here?

I asked myself this very question. Typically speaking serverless functions are used in client-side requests and whilst that’s fine I wondered if they could also be used at build time to statically “bake” data into a page rather than relying on JavaScript which may or may not be disabled in the user's browser.

...so that’s exactly what I did. 

Here’s a kind of data dashboard that uses data returned by Gatsby Functions at both run and build time. I built this site using [Astro](https://astro.build/) and deployed it [GitHub Pages](https://pages.github.com/).

The reason I think this is a great approach is because I’m able to re-use the same functionality on both the server and in the browser without duplicating anything. 

In this Astro build I hit the same endpoint exposed by my API to return data that is then either baked into the page (great for SEO) or fetched at run time by the browser (great for showing fresh or up to the minute live data).

### Data Dashboard

The data displayed on the left of the site is requested at build time and baked into the page with Astro. The data on the right of the page is requested at runtime using a client-side request. I’ve used slightly different endpoints exposed by the GitHub REST API to query different GitHub user accounts which create the different lists. 

{{< rimg breakout="true" href="https://pauliescanlon.github.io/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a7b2d8d-85fd-4940-ae16-883b5409b958/3-building-api-gatsby-functions.png" width="800" height="500" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a7b2d8d-85fd-4940-ae16-883b5409b958/3-building-api-gatsby-functions.png'>Large preview</a>)" alt="Data Dashboard" >}}

Everything you see on this site is provided by my more complete API. I’ve called it: [Paulie API](https://paulieapi.gatsbyjs.io/) and I use it for a number of my websites. 

### Paulie API

Paulie API like the API from this tutorial is built with Gatsby but because Gatsby can act as both a site and an API I’ve used it to document how all my functions work and each endpoint has its own page that can be used as an interactive playground… feel free to have a look around. 

{{< rimg breakout="true" href="https://paulieapi.gatsbyjs.io/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62c7c3ab-d342-48e3-bcfa-8afb7144161c/1-building-api-gatsby-functions.png" width="800" height="500" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62c7c3ab-d342-48e3-bcfa-8afb7144161c/1-building-api-gatsby-functions.png'>Large preview</a>)" alt="Paulie API" >}}

So, there you have it, A Gatsby Functions API that can be used by any client-side or server-side code, from any website built with any tech stack. 🤯

Give it a go and I’d be very interested to see what you build. Feel free to share in the comments below or come find me on Twitter: [@PaulieScanlon](https://twitter.com/PaulieScanlon).

{{< signature "vf, yk, il" >}}

---
title: 'Building A Web App With Headless CMS And React'
slug: web-app-headless-cms-react
author: blessing-krofegha
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d07c5fad-9381-4c77-bc57-9807c95e99e1/web-app-headless-cms-react.png
date: 2020-04-01T11:30:00.000Z
summary: >-
  This article introduces the concept of the headless CMS, a backend-only content management system that allows developers to create, store, manage and publish the content over an API. It gives developers the power to quickly build excellent user experiences, free from the worry of its impact on the back-end business logic.
description: >-
  This article introduces the concept of the headless CMS, a backend-only content management system that allows developers to create, store, manage and publish the content over an API.
categories:
  - React
  - Headless
  - CMS
  - JavaScript
---

In this tutorial, you’ll learn what Headless CMS is, and the pros and cons of Headless CMS. In the end, youll have built a shopping cart using [GraphCMS](https://graphcms.com/) (a (backend-only content management system). After that, you can go ahead and build any web app of your choice using a headless CMS and React.

To follow along, you need to have Node and npm/yarn installed on your machine. If you do not have that done already, follow these quick guides to install [yarn](https://classic.yarnpkg.com/en) or [npm](https://riptutorial.com/node-js/example/29249/yarn-installation) on your machine. You also need to have a basic understanding of React, Node.js and GraphQL queries. (You can always brush up on [React](https://reactjs.org/docs/getting-started.html) and [GraphQL](https://graphql.org/learn/) skills, of course!)

As digital products continue to evolve, so does the content we consume. A scalable, cross-platform content management system is crucial to ensuring a product’s growth velocity. Traditional CMS gives the comfort of having the content, the editing interface, templates and custom codes, in a single environment. But with the changes in this mobile era, that’s no longer enough. We need a new breed of CMS &mdash; one that can make content available through any channel at which point a **Headless CMS is required.** A headless CMS gives you the benefits of managing the content and delivering it to any channel. The API makes contents available through any channel and on any device using most favorite tools and programming languages plus it also provides a higher level of security and much better scalability.

{{% feature-panel %}}

## What Does This Look Like In Practice?

What happens when you take away the frontend of a CMS? The biggest distinction is that a website can’t be built with a headless CMS on its own. With a traditional CMS, everything happens in the same place. 

A headless CMS doesn’t have the features that let you build your site &mdash; it doesn’t have site themes or templates. To use a headless CMS, you have to build a site or app, or other experience first, then use the CMS’s API to plug your content into it.

## Why Should You Care About Headless?

A headless CMS comes with an API friendly approach, which makes it possible to publish content through an API (either RESTful or GraphQL). It allows you to use the same API to deliver content across various channels such as Android or IOS apps, smartwatches, AR/VR, etc. A headless CMS gives developers the ability to harness creativity quickly. With a traditional CMS, changes can be time-consuming, for example, to tweak a part of your site, you need to re-implement the entire CMS. With a headless CMS, you can make changes to your frontend without having any impact on the back-end infrastructure, hence saving yourself time and resources, which makes it much better.

## Traditional vs Headless CMS: The Pros And Cons

It can be complicated to choose between a headless and a traditional CMS. The fact is, they both have potential advantages and drawbacks.

### Traditional CMS Pros

- It allows for easy customization. A lot of them have drag and drop, this makes it easy for a person without programming experience to work seamlessly with them.
- It’s easier to set up your content on a traditional CMS as everything you need (content management, design, etc) are already available.

### Traditional CMS Cons

- The coupled front-end and back-end results in more time and money for maintenance and customization.
- Traditional CMS e.g Wordpress relies heavily on plugins and themes which may contain malicious codes or bugs and slow the speed of the website or blog. Here’s a [list](https://wpvulndb.com/) of 18,305 vulnerable WordPress plugins, themes. Here are security measures for [Drupal](https://www.theregister.co.uk/2019/02/20/drupal_cve_2019_6340/) developers. Check [here](https://securityboulevard.com/2019/08/how-to-secure-your-content-management-system-cms/) for more facts.

### Headless CMS Pros

- Since the frontend and backend are separated from each other, it makes it possible for you to pick which front-end technology suits your needs. This also gives the developer flexibility during the development stage.
- Platforms (blogs, websites, etc) built with headless CMS can be deployed to work on various displays such as web, mobile, AR/VR, and so on.

### Headless CMS Cons

- They give you the hassle of managing back-end infrastructures, setting up the presentation component of your site, app.
- They can be more costly to implement &mdash; the cost involved in building a user-friendly platform with analytics is high when compared to using traditional CMS.

### Best Use Cases For Headless CMS

Headless CMS can have the following use cases:

- **Static Site Generators** (e.g. Gridsome, Gatsby)

Many Jamstack sites created with static site generators like Gridsome, Hugo or Gatsby make use of the headless CMS to manage content, they cannot access a database, Hence content can be stored in a headless CMS and fetched through an API during build time and deployed as static files.

- **Mobile Apps** (iOS, Android)

The advantage of a headless CMS for mobile engineers is that the API enables them to deliver content to an IOS/Android app from the same backend that manages content for their web site, which keeps things in sync.

- **Web Applications** 

This approach involves serving content through an API which is then consumed by a web application but offers a centralized place for managing content. An example is an e-commerce application built using HTML, CSS, and JavaScript with content and product data that are maintained in the CMS and served via an external API.

### Types Of Headless CMS

There is a list of headless CMSs you might what to check out.

**Please note that this article is not written to promote any services or products.**

- [Contentful](https://www.contentful.com/)  
An API-driven headless CMS designed to create, manage and distribute content to any platform. Unlike a traditional CMS, they offer the ability to create your content model so that you can decide what type of content you want to manage.
- [GraphCMS](https://graphcms.com/)  
A headless CMS for users who want to build a GraphQL content infrastructure for their digital products. This CMS is fully built as API focused from the ground up, allowing creators to define the structures, permissions, and relations for the API parameters. In this article, we’d be using GraphCMS because of its GraphQL API approach.
- [ButterCMS](https://buttercms.com/)  
A CMS that gives complete freedom to build a website or a branded blog with full SEO and supports any tech stack. This tool saves you money and the time for site development time. Butter CMS is a maintenance-free headless CMS tool and can integrate with any language or framework. The powerful interface helps you define and customize every element of your website without any hassle.
- [Directus](https://Directus.io)  
An open-source tool that wraps custom SQL databases with a dynamic API and provides an intuitive admin app for managing its content. Self-host for free, or use the on-demand Cloud service to manage all your omnichannel digital experiences.
- [Sanity](https://sanity.io)  
Another API driven platform for managing structured content. With Sanity, you can manage your text, images, and other media with APIs. You can also use the open-source single page application [Sanity Studio](https://www.sanity.io/studio) to quickly set up an editing environment that you can customize.
- [Agility](https://agilitycms.com/)  
A JAMStack focused Headless CMS with Page Management built-in. Faster to build, manage, and deploy. Agility CMS is a Content-First Headless CMS, allowing you to choose any programming language while also getting the flexibility, speed, and power that comes from lightweight APIs. From there, add features like Page Management, Ecommerce, Online Ticketing, and Search. Agility CMS becomes a complete Digital Experience Platform–saving time, removing limitations and allowing for seamless experiences across all digital channels.
- [Netlify CMS](https://www.netlifycms.org/)  
A free and open-source, git-based CMS created by Netlify. It allows you to define your content model, integrates third-party authentication and extends the capabilities of its backend (a single-page app built on React).

**Note**: *All of the examples mentioned above have free and paid versions, except Directus and Netlify CMS which are free. For a list of more headless CMS, check [here](https://www.g2.com/categories/headless-cms).*

In this article, we’re using GraphCMS &mdash; a GraphqQL API-oriented headless content management system that takes care of our back-end architecture.

{{% ad-panel-leaderboard %}}

## Using GraphCMS

Content is both dynamic and multi-channeled, however current content management systems (CMS) lack the flexibility to meet the demands of modern-day digital content distribution. GraphCMS is the first HeadlessCMS built around GraphQL and offers a solution to this problem with its mission to facilitate painless content flow between content creators, developers, and consumers.

GraphCMS accept almost any kind of data you can imagine ranging from images, maps, etc. It even makes roles and permissions easy. While other headless CMS solutions exist, GraphCMS aims to provide a hassle-free experience for developers; through leveraging an API specification called [GraphQL](https://graphql.org/). It eliminates the need for multiple SDKs to interact with content delivery and provides simple multi-channel content accessibility. It makes creating rich content apps very easy.

## GraphCMS And GraphQL

GraphCMS solely relies on [GraphQL](https://graphql.org/learn/), its backbone API specification. GraphQL is API query language and runtime. It was developed by Facebook in 2012 and released open-sourced in 2015. Since then, the likes of Pinterest, Github, Twitter, Intuit, Coursera have all adopted GraphQL to power their mobile apps, websites, and APIs. GraphQL is similar to REST in its core purpose of providing a specification for building and utilizing APIs. However, unofficially dubbed “REST 2.0”, GraphQL has optimized different key functionality offered by REST.

The main uniqueness of GraphQL includes protocol-agnostic usage, controlled data fetching, editable fields, and types and in-depth error handling. The results include removal of code redundancy, prevention of over and under fetching data, and significant reduction of network requests.

As a concrete example, let’s take the relationship of a query to a newsfeed. A newsfeed post has an author, a title and comments. If we use a REST-based CMS, we would have to make 3 different server requests for these 3 different endpoints, whereas, in a GraphQL based CMS, we would only have to make 1 request for all 3. Consequently, the results offer relatively quicker queries and less network flooding &mdash; in a practical use case, it would not just be one entity making multiple requests, but thousands and millions.
 
[GraphQL](https://blog.logrocket.com/graphql-vs-rest-what-you-didnt-know/) reduces the complexity of building APIs by abstracting all requests to a single endpoint. Unlike traditional REST APIs, it is declarative; whatever is requested is returned.
 
GraphCMS has a generous free tier of 1 million API operations requests per month and 500 GB assets traffic. Also, GraphCMS provides a **Graphiql** admin interface that provides you full access to your data and you could just download it all and then execute a create many mutations against your new backend to migrate everything over.
 
In this article, we’ll be using the **free** tier of 1 million API operations per month and 500 GB asset traffic. You can make use of the same tier for testing, for projects that need more than this, do well to check out their [pricing page](https://graphcms.com/pricing/).


## Building Our Project

To see the power of Headless CMS using GraphCMS we would be building a simple shopping cart.

### Getting Started 

To get started with GraphCMS follow the steps.

- Create an account on [GraphCMS](https://graphcms.com/). You can use the free tier.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ab5b068-5140-4fb9-9521-2c5e20b84f01/01-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ab5b068-5140-4fb9-9521-2c5e20b84f01/01-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ab5b068-5140-4fb9-9521-2c5e20b84f01/01-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

- At successful signup, you’ll be taken to your dashboard. Click on create a new project.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6bef845-e873-48be-a9af-2db4914521bd/02-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6bef845-e873-48be-a9af-2db4914521bd/02-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="Click on Create new project. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6bef845-e873-48be-a9af-2db4914521bd/02-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

- Ensure you click on create a project from scratch.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab2adfd4-6bbd-4d3c-a344-205ad3169fb9/03-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab2adfd4-6bbd-4d3c-a344-205ad3169fb9/03-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="Select From Scratch. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab2adfd4-6bbd-4d3c-a344-205ad3169fb9/03-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

- Set project details for the project fill in what is in the image below and click create.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb5636cc-a2dd-4410-8492-c0211bfa208b/04-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb5636cc-a2dd-4410-8492-c0211bfa208b/04-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="Set Project Details. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb5636cc-a2dd-4410-8492-c0211bfa208b/04-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

- In our dashboard, we would create our models and content.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ad8d10c-f9ea-42c6-be73-979d93466954/05-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ad8d10c-f9ea-42c6-be73-979d93466954/05-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="Create model. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ad8d10c-f9ea-42c6-be73-979d93466954/05-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

- Select the schema in the sidebar of the dashboard to create a schema.

GraphCMS has an awesome `drag and drop UI`, that make it easy to seamlessly create schema in minutes.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33032749-bb23-42c3-a2b6-55d3dfe279b0/06-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33032749-bb23-42c3-a2b6-55d3dfe279b0/06-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="Drag and Drop fields. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33032749-bb23-42c3-a2b6-55d3dfe279b0/06-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

- Let’s go ahead and create our `system fields` in our schema.

    - **name: “”**
        - type: The field type is a String, Single line Text.
        - Is required
        - description: It’s the name of the product.
    - **price: “”**
        - type: The field type is int.
        - Is required
        - description: It will contain the price of our product.
    - **description: “”**
        - type: The field type is a String, Multi-line Text.
        - Is required
        - description: This field will contain the description of our product.
    - **image: “”**
        - type: The field type is the file, which is an Asset Picker.
        - Is required
        - description: This image field will contain the image of our product.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3ae0077-a542-4deb-a4be-040739374622/07-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3ae0077-a542-4deb-a4be-040739374622/07-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="Creating our name field. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3ae0077-a542-4deb-a4be-040739374622/07-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

**Note**: *Click on the ‘Advance’ tab to select the required option in our fields.*

- If all went well, you should have our schema looking the image below:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b85e92f8-e830-4604-99f2-3027382fa72b/08-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b85e92f8-e830-4604-99f2-3027382fa72b/08-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="Final Schema fields. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b85e92f8-e830-4604-99f2-3027382fa72b/08-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

- Currently, we have no content. Click on ‘Content’ in the sidebar that should take you the Content section, and click on ‘Create New’.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7322e47-c6c6-4e75-b753-677cdf916d67/09-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7322e47-c6c6-4e75-b753-677cdf916d67/09-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="At this point our we have no content/post. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7322e47-c6c6-4e75-b753-677cdf916d67/09-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

- Let’s add a few contents so we can display them later in our app using React.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf59ca28-fb5e-4186-814f-affd1f6f107b/010-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf59ca28-fb5e-4186-814f-affd1f6f107b/010-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="Here’s how to add content. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf59ca28-fb5e-4186-814f-affd1f6f107b/010-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

- Add a few more content if you desire. Here’s our result.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef48fb12-979c-4613-9b6c-d8c6ed8fd52e/011-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef48fb12-979c-4613-9b6c-d8c6ed8fd52e/011-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="Our final content. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef48fb12-979c-4613-9b6c-d8c6ed8fd52e/011-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

- Next, copy the API endpoint URL (Click on the Dashboard) &mdash; this is the single endpoint for communication between our React front end and GraphCMS back end.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccf3332f-950b-402b-b897-354b0b9b0164/012-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccf3332f-950b-402b-b897-354b0b9b0164/012-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccf3332f-950b-402b-b897-354b0b9b0164/012-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

Next, let’s make our API endpoint accessible. 

- Navigate to Settings Under **Public API Permission** and click on the drop-down and select OPEN and click the update button.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccdfad3a-3f2d-40c8-addb-76da3a5f2c91/013-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccdfad3a-3f2d-40c8-addb-76da3a5f2c91/013-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccdfad3a-3f2d-40c8-addb-76da3a5f2c91/013-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

### Setting Up React

The easiest way to set up React is to use [Create-React-App](https://create-react-app.dev/docs/getting-started/). (This is an officially supported way to create single-page React applications, and offers a modern build setup with no configuration.) We’ll make use of it to bootstrap the application we’ll be building.

From your terminal, run the command below:

<pre><code class="language-bash">npx create-react-app smashing-stores && cd smashing-stores</code></pre>

Once the installation is successful, start the React server by running `npm start`.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4896829-5b30-4192-97d5-3fa2b98d536e/014-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4896829-5b30-4192-97d5-3fa2b98d536e/014-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="React Starter Page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4896829-5b30-4192-97d5-3fa2b98d536e/014-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

### Creating Our Layout

In creating the layout for our project, we will have five different components.

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<tbody>
		<tr>
			<td><code>Navbar</code></td>
			<td>To hold our navigation and cart icon</td>
		</tr>
		<tr>
			<td><code>Allproducts</code></td>
			<td>To display a list of all products</td>
		</tr>
		<tr>
			<td><code>Product</code></td>
			<td>The markup for a single product</td>
		</tr>
		<tr>
			<td><code>Footer</code></td>
			<td>The footer of our app</td>
		</tr>
		<tr>
			<td><code>Cart</code></td>
			<td>To hold the items in our cart</td>
		</tr>
	</tbody>
</table>

For a quick setup, we will be using [Bootstrap](https://getbootstrap.com/) to create our components. To include Bootstrap, we would use bootstrap CDN, open up your *index.html* in the public folder, add the link to the head section:

<div class="break-out">

<pre><code class="language-html">https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css</code></pre>
</div>

Now we can make use of bootstrap classes in our application.

Next, create a  `/components` folder and create the following files inside it:

- *Navbar.js*
- *Allproducts.js*
- *Product.js*
- *Footer.js*
- *Cart.js*

{{% ad-panel-leaderboard %}}

#### Creating Our Navbar

Open up the *Navbar.js* and add the following code:

<div class="break-out">

<pre><code class="language-javascript">import React from 'react';

const Navbar = () =&gt; {
  return (
    &lt;nav className="navbar navbar-light bg-light"&gt;
      &lt;a href="/" className="navbar-brand"&gt;Smashing Stores&lt;/a&gt;
        &lt;button className="btn btn-outline-success my-2 my-sm-0" type="submit"&gt;Cart&lt;/button&gt;
    &lt;/nav&gt;
  );
};
export default Navbar;</code></pre>
</div>

We declared a functional component Navbar, we return our nav tag with a bootstrap class of `navbar navbar-light bg-light`. What these classes do is to apply a Navbar with a light background. Inside our nav element, we included an anchor tag with a link to just `forward-slash(Homepage)` and a class of `navbar-brand`.

The styled button in the Navbar component has a class named `navbar navbar-light bg-light`. What this class does it to ensure that our button has a light blue background color and a shadow when hovered. 

#### Creating Our Footer.js

Next, let’s create our Footer. Open up the *Footer.js* file and add the following code to it:

<div class="break-out">

<pre><code class="language-javascript">import React from 'react';
import '../App.css';
const Footer = () =&gt; {
  return (
      &lt;footer className="page-footer font-small bg-blue pt-4"&gt;
        &lt;div className="container text-center text-md-left"&gt;
          &lt;div className="row"&gt;
            &lt;div className="col-md-6 mt-md-0 mt-3"&gt;
              &lt;h5 className="text-uppercase font-weight-bold"&gt;Contact Us&lt;/h5&gt;
              &lt;p&gt;You can contact us on hi@smashingstores.com&lt;/p&gt;
            &lt;/div&gt;
            &lt;div className="col-md-6 mb-md-0 mb-3"&gt;
              &lt;h5 className="text-uppercase font-weight-bold"&gt;Smashing Stores&lt;/h5&gt;
              &lt;p&gt;Built with 💕 by &lt;a href="https://twitter.com/beveloper"&gt;beveloper&lt;/a&gt;&lt;/p&gt;
            &lt;/div&gt;
          &lt;/div&gt;
        &lt;/div&gt;
        &lt;div className="footer-copyright text-center py-3"&gt;© 2020 Copyright
          &lt;span&gt; Smashing Stores&lt;/span&gt;
        &lt;/div&gt;
      &lt;/footer&gt;
  );
};
export default Footer;</code></pre>
</div>

We added contact-us email using `h5` and paragraph element. Lastly, on this footer section, we added copyright with the name “Smashing Stores”.

Our footer needs some styling so we’d add the following styles to the *App.css* file:

<pre><code class="language-css">footer {
  position: absolute;
  bottom: -55px;
  width: 100%;
  background-color: #333;
  color:#fff;
}</code></pre>

Before we create our product component, we need to query GraphCMS to send us our product details to display. Let’s do that now.

#### Connecting To The GraphCMS Backend With GraphQL

To connect our application to the backend, we need to install a couple of GraphQL packages. One of the libraries we can use is [apollo-boost](https://www.npmjs.com/package/apollo-boost) which gives a client the avenue for connecting to the GraphQL backend using a URI (**U**niform **R**esource **I**dentifier).

The URI is the endpoint provided by GraphCMS and is available on the endpoint section of the dashboard.

Run the following command in your terminal to install the necessary packages:

<pre><code class="language-bash">npm install apollo-boost graphql graphql-tag react-apollo</code></pre>

Once you’re done with the installation update the *index.js* file in the `/src` directory to the following code:

<pre><code class="language-javascript">import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import { ApolloProvider } from "react-apollo";
import ApolloClient from "apollo-boost";
import * as serviceWorker from './serviceWorker';

const client = new ApolloClient({
  uri: "&lt;YOUR_GRAPHCMS_ENDPOINT&gt;"
});

ReactDOM.render(
  &lt;ApolloProvider client={client}&gt;
    &lt;App /&gt;
  &lt;/ApolloProvider&gt;,
  document.getElementById('root')
);

serviceWorker.unregister();</code></pre>

Here, we wrapped our entire application with the `ApolloProvider` which takes a single prop: the `client`. The `ApolloProvider` loads the Graph CMS schema and gives us access to all properties of the data model inside our application which is possible because our `App` component is a child of the `ApolloProvider` component.

#### Displaying Our Products

If you got this far, pat yourself on the back. 👍 We’ve been able to load our schema from GraphCMS into our application.

The next step is to fetch and display our products. Create an `/all-product` folder under the `/component` folder and then create an *index.js* file and add the following to it:

<pre><code class="language-css">import gql from "graphql-tag";
const PRODUCTS_QUERY = gql`
  query {
    productses {
      id
      name
      price
      description
      createdAt
      image {
        id
        url
      }
    }
  }
`;
export default PRODUCTS_QUERY;</code></pre>

What are "**productses**"? Our model name is products, but GraphQL pluralizes models, hence the name.

Next, we created a variable called `PRODUCTS_QUERY` that stores the query from our GraphQl back end. The gql function is used to parse (analyze an object, as it were in our schema) the plain string that contains the GraphQL code (if you’re unfamiliar with the backtick-syntax, you can read up on JavaScript’s [tagged template literals](https://wesbos.com/tagged-template-literals/)).

GraphCMS provides a handy GraphQL explorer named **(graphiql)** specifically for testing our query. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bbb0a5d-8d3e-43a3-a2e2-8b6792b9446e/015-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bbb0a5d-8d3e-43a3-a2e2-8b6792b9446e/015-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="Testing our endpoint using Graphiql Explorer in our GraphCMS Dashboard. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bbb0a5d-8d3e-43a3-a2e2-8b6792b9446e/015-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

Now that our query works as it should. Let’s go ahead and create our product’s components.


#### Creating The `Allproducts` Component

Open up the *Allproducts.js* file and add the following code to it:

<div class="break-out">

<pre><code class="language-javascript">import React, { Component } from 'react';
import { Query } from 'react-apollo';
import PRODUCTS_QUERY from './all-products/index';
import Product from './Product';
import Cart from './Cart';
import Navbar from './Navbar';
class Allproducts extends Component {
  constructor(props) {
    super(props);
    this.state = {
      cartitems: []
    };
  }
    addItem = (item) =&gt; {
      this.setState({
          cartitems : this.state.cartitems.concat([item])
      });
    }
  render() {
    return (
      &lt;Query query={PRODUCTS_QUERY}&gt;
       {({ loading, error, data }) =&gt; {

          if (loading) return &lt;div&gt;Fetching products.....&lt;/div&gt;
          if (error)   return &lt;div&gt;Error fetching products&lt;/div&gt;

          const items = data.productses;
          return (
            &lt;div&gt;
              &lt;Navbar/&gt;
              &lt;div className="container mt-4"&gt;
                &lt;div className="row"&gt;
                   {items.map(item =&gt; &lt;Product key={item.id} product={item} addItem={this.addItem} /&gt;)}
                &lt;/div&gt;
              &lt;/div&gt;
            &lt;/div&gt;
          )
        }}
      &lt;/Query&gt;
    );
  }

};
export default AllProducts;</code></pre>
</div>

Here, we wrapped our products with the `<Query/>` component and passed the `PRODUCTS_QUERY` as props. Apollo injected several props into the component’s render prop function. These props themselves provide information about the state of the network request:

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<tbody>
		<tr>
			<td><code>loading</code></td>
			<td>This occurs during ongoing requests.</td>
		</tr>
		<tr>
			<td><code>error</code></td>
			<td>This occurs when the requests fail.</td>
		</tr>
		<tr>
			<td><code>data</code></td>
			<td>This is data received from the server. </td>
		</tr>
	</tbody>
</table>

Finally, we loop through all the received items and pass them as a prop to our Product component. Before we see what it looks like, let’s create our Product component.

#### Creating Product Component

Open up *Product.js* and add the following code to it:

<div class="break-out">

<pre><code class="language-javascript">import React from 'react';
const Product = (props) =&gt; {
  return (
      &lt;div className="col-sm-4"&gt;
          &lt;div className="card" style={{width: "18rem"}}&gt;
            &lt;img src={props.product.image.url} className="card-img-top" alt="shirt"/&gt;
            &lt;div className="card-body"&gt;
              &lt;h5 className="card-title"&gt;{props.product.name}&lt;/h5&gt;
              &lt;p className="card-title"&gt;$ {props.product.price}&lt;/p&gt;
              &lt;p className="card-title"&gt;{props.product.description}&lt;/p&gt;
              &lt;button className="btn btn-primary" onClick={() =&gt; props.addItem(props.product)}&gt;Buy now&lt;/button&gt;
            &lt;/div&gt;
          &lt;/div&gt;
      &lt;/div&gt;
  );
}
export default Product;</code></pre>
</div>

Since our Product.js is a functional component that receives product details via props and displays them, we call the addItem function on the onClick event listener to add the current product to the cart when it clicked.

### Importing Our Components Into App.js

With our components setup, it’s time we import our components into our App.js base component.

Open it up and add the following to it:

<pre><code class="language-css">import React from 'react';
import './App.css';
import Footer from './components/Footer';
import Products from './components/Allproducts';
function App() {
  return (
    &lt;div className="App"&gt;
      &lt;Products /&gt;
      &lt;Footer/&gt;
    &lt;/div&gt;
  );
}
export default App;</code></pre>


- From lines 3-4, we imported both Footer and Products component in the App component.

Next, type npm start in your terminal then navigate to [https://localhost:3000](https://localhost:3000/) in your browser, and you will see the following:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ffa3810-b541-494c-86df-f5f2ed256894/016-building-web-app-with-headless-cms-react.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ffa3810-b541-494c-86df-f5f2ed256894/016-building-web-app-with-headless-cms-react.png" sizes="100vw" caption="Final Outcome of our Web App. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ffa3810-b541-494c-86df-f5f2ed256894/016-building-web-app-with-headless-cms-react.png'>Large preview</a>)" alt="" >}}

We’re close to the end of our project, but our products need a feature that adds items to the cart.

#### Creating Our Cart Component

To include our cart functionality, we’d need to add some methods to our components.

Let’s update our *Allproducts.js* file to this:

<div class="break-out">

<pre><code class="language-javascript">import React, { Component } from 'react';
import { Query } from 'react-apollo';
import PRODUCTS_QUERY from './all-products/index';
import Product from './Product';
import Cart from './Cart';
import Navbar from './Navbar';
class Allproducts extends Component {
  constructor(props) {
    super(props);
    this.state = {
      cartitems: [],
      show: false
    };
  }
    addItem = (item) =&gt; {
      this.setState({
          cartitems : this.state.cartitems.concat([item])
      });
    }
    showModal = () =&gt; {
      this.setState({ show: true });
    };
    hideModal = () =&gt; {
      this.setState({ show: false });
    };
  render() {
    return (
          &lt;Query query={PRODUCTS_QUERY}&gt;
           {({ loading, error, data }) =&gt; {
              if (loading) return &lt;div&gt;Fetching&lt;/div&gt;
              if (error)   return &lt;div&gt;Error&lt;/div&gt;
              const items = data.productses
              const itemssent = this.state.cartitems;
               return (
                &lt;div&gt;
                 &lt;Navbar cart={itemssent} show={this.showModal} /&gt;
                 &lt;Cart show={this.state.show} items={itemssent} handleClose={this.hideModal}&gt;
                  &lt;/Cart&gt;
                  &lt;div className="container mt-4"&gt;
                    &lt;div className="row"&gt;
                       {items.map(item =&gt; &lt;Product key={item.id} product={item} addItem={this.addItem} /&gt;)}
                    &lt;/div&gt;
                  &lt;/div&gt;
                &lt;/div&gt;
              )
            }}
          &lt;/Query&gt;
      )
   };
};
export default Allproducts;</code></pre>
</div>

- `showModal`  
This method sets the show state to true so that the modal can be visible to the user.
- `hideModal`  
This method sets the show state to false to hide the modal.
- We created a variable named `itemssent` that holds the state of all cart items we get from the backend.

#### Navbar

- `cart`  
It passes the items in the cart data to our Navbar.
- `show`  
It triggers our modal method.

#### Cart

- `show`  
It opens up the cart modal.
- `Items`  
It receives and stores the data sent from the Navbar so it can be displayed when needed.
- `handleClose`  
It closes the modal.

#### Updating Navbar

Let’s update our *Navbar.js* file with the following code:

<div class="break-out">

<pre><code class="language-css">import React from 'react';
    
const Navbar = (props) =&gt; {
  return (
    &lt;nav className="navbar navbar-light bg-light"&gt;
      &lt;h3&gt;Smashing Stores&lt;/h3&gt;
        &lt;button className="btn btn-outline-success my-2 my-sm-0" onClick={() =&gt; props.show()}&gt;Cart {(props.cart.length)}&lt;/button&gt;
    &lt;/nav&gt;
  );
};
export default Navbar;</code></pre>
</div>

- We added an on click event that takes a function, which triggers that cart modal.
- Lastly, we check for the number of items in our cart by using the `.length` JavaScript method.

Next, create a *Cart.js* file and add the following code to it:

<div class="break-out">

<pre><code class="language-javascript">import React from 'react';

const Cart = ({ handleClose, show, items }) =&gt; {
  return (
    &lt;div className={show ? "modal display-block" : "modal display-none"}&gt;
      &lt;section className="main-modal"&gt;
        {items.map(item =&gt;
           &lt;div className="card" style={{width: "18rem"}}&gt;
              &lt;img src={item.image.url} className="card-img-top" alt="shirt"/&gt;
              &lt;div className="card-body"&gt;
                &lt;h5 className="card-title"&gt;{item.name}&lt;/h5&gt;
                &lt;h6 className="card-title"&gt;$ {item.price}&lt;/h6&gt;
              &lt;/div&gt;
            &lt;/div&gt;
        )}
         Total items: {items.length}
        &lt;button className="btn btn-warning ml-2" onClick={handleClose}&gt;close&lt;/button&gt;
      &lt;/section&gt;
    &lt;/div&gt;
  );
};
export default Cart;</code></pre>
</div>

In our parent div, we used a ternary operator that toggles between visibility and hidden state. Next, in other for us to display the items in our cart modal we map through our items.

Lastly, in this section to check out for the total number of items in our cart we used the `.length` JavaScript method.

Open up your `app.css` and add the following code to it:

<pre><code class="language-css">.modal {
  position: fixed;
  top: 0;
  left: 0;
  width:100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
}
.main-modal {
  position:fixed;
  background: white;
  width: 80%;
  height: auto;
  top:50%;
  left:50%;
  padding: 10px;
  transform: translate(-50%,-50%);
}
.display-block {
  display: block;
}
.display-none {
  display: none;
}</code></pre>

Finally open the shopping cart, add items to it and view it via the ‘Cart’ button:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6f0e3d9-c18a-4d84-a54d-5f7a74c36c6e/017-building-web-app-with-headless-cms-react.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6f0e3d9-c18a-4d84-a54d-5f7a74c36c6e/017-building-web-app-with-headless-cms-react.gif" width="600" height="273" alt="" /></a><figcaption></figcaption></figure>

## Conclusion

The concept learned in this article can help you create almost anytime of web apps without paying so much attention to your back-end infrastructure. You can take it further by creating a full-fledged e-commerce store and adding payment etc. I’ll love to see what you were able to make in the comments section.
 
The supporting repo for this article is available on  [Github](https://github.com/krofax/E-Commerce-Store-with-GraphCMS-and-React).

### References

1. [GraphCMS Documentation](https://graphcms.com/docs/introduction/)
2. [Event App with GraphCMS](https://www.youtube.com/watch?v=plbJolNkn_c&t=48s)

{{< signature "ks, yk, il" >}}

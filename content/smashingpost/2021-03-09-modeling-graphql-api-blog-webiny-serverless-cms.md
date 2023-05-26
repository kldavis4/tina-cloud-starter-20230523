---
title: 'Modeling A GraphQL API For Your Blog Using Webiny Serverless CMS'
slug: modeling-graphql-api-blog-webiny-serverless-cms
author: nwani-victory
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9625bed-8942-4c5e-a03c-4cf5387550d4/3-modeling-graphql-api-blog-webiny-serverless-cms.png
date: 2021-03-09T14:00:00.000Z
summary: >-
  In the world of serverless applications, Webiny is becoming a popular way to adopt the serverless approach of building applications by providing handy tools that developers can build their apps upon. In this article, we will look into what Webiny is and try out the headless CMS as a data source for a Gatsby blog application.
description: >-
  In the world of serverless applications, Webiny is becoming a popular way to adopt the serverless approach of building applications by providing handy tools that developers can build their apps upon. In this article, we will look into what Webiny is and try out the headless CMS as a data source for a Gatsby blog application.
categories:
  - Headless
  - CMS
  - GraphQL
  - Serverless
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Webiny
  link: https://www.webiny.com/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98b5d213-a0d0-464e-8d54-942af5215a5e/webiny-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.webiny.com/">Webiny</a> who help folks to architect, build and deploy solutions on top of serverless infrastructure. <em>Thank you!</em>
---

In time past, developers reduced the challenges associated with managing content-dependent platforms through the use of [Content Management Systems](https://en.wikipedia.org/wiki/Content_management_system) (CMS) which allowed web content to be created and displayed using existing design templates provided by the CMS service.

But with the arrival of Single Page Applications (*SPAs*), this approach to managing content has become unfavorable as developers are locked-in with the provided design layouts. This is the point where the use of [Headless CMS services](https://jamstack.org/headless-cms/) has been largely embraced as developers have sought more freedom to serve content across various clients such as mobile, web, desktop, and even wearable devices.

A headless CMS stores data in a backend database however unlike the traditional CMS service where content is displayed through a defined template, content is delivered via an API and this gives developers the flexibility to consume content across various clients or frontend frameworks.

One example of such a headless CMS is [Webiny](https://www.webiny.com/). Its serverless [headless CMS](https://www.webiny.com/serverless-app/headless-cms/) which provides a personalized admin application to create content, and a robust GraphQL API to consume whatever content was created through the admin application. Further down this article, we will explore Webiny and use the admin app when modeling content through the headless CMS app, then consume the content via the [GraphQL API](https://graphql.org/) in a [Gatsby](https://www.gatsbyjs.com/) blog application.

If this is your first time hearing of Webiny, it’s an **open-source framework** for building serverless applications which provide users with tools and ready-made applications. It has a growing developer community on [Slack](https://www.webiny.com/slack), ultimately trying to make the development of serverless applications easy and straightforward.

To make this article easy to follow, it has been broken down into two major segments. You can either skip to the part that interests you most, or follow them in the order as they appear below:

<ul>
  <li><a href="#create-deploy-webiny-project">Creating and deploying a Webiny project</a>;</li>
  <li><a href="#webiny-admin-app">Integrating the Webiny headless CMS GraphQL API into a Gatsby application as a remote data source</a>.</li>
</ul>

**Note:** *To follow along, you’ll need to have an [AWS account](https://aws.amazon.com/) (if not, please [create one](https://portal.aws.amazon.com/billing/signup?nc2=h_ct&src=header_signup&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start)), [Yarn](https://yarnpkg.com/), or have [npm installed](https://www.npmjs.com/) on your local machine. A good understanding of [React.js](https://reactjs.org/) is beneficial as the demo application is built by using [Gatsby](https://www.gatsbyjs.com/).*

## Creating And Deploying A Webiny Project

To get started, we’re going to create a new Webiny project, deploy it and use the Headless CMS through the generated admin app to begin modeling content within the GraphQL API.

Running the command below from a terminal will generate a new Webiny project based on your answers to the installation prompts:

<div class="break-out">

 <pre><code class="language-bash">npx create-webiny-project@beta webiny-blog-backend --tag beta
</code></pre>
</div>

The command above would run all steps needed for bootstrapping a Webiny project. A Webiny project consists of three smaller applications: a GraphQL API, an admin app, and also a website &mdash; all of which are contained in the root generated Webiny project folder similar to the one in the image below.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f730373-e34e-4ae5-b0ae-316ec62fa114/1-modeling-graphql-api-blog-webiny-serverless-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f730373-e34e-4ae5-b0ae-316ec62fa114/1-modeling-graphql-api-blog-webiny-serverless-cms.png" width="799" height="788" sizes="100vw" caption="Generated Webiny project directory structure. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f730373-e34e-4ae5-b0ae-316ec62fa114/1-modeling-graphql-api-blog-webiny-serverless-cms.png'>Large preview</a>)" alt="Generated Webiny project directory structure." >}}

Next, we need to start the deployment of the three components within the Webiny project to AWS so we can access the GraphQL API. The [Cloud Infrastructure](https://docs.webiny.com/docs/key-topics/cloud-infrastructure/api/introduction) section of the [Webiny documentation](https://docs.webiny.com/docs) gives a detailed explanation of entire the infrastructure deployed to [AWS](https://aws.amazon.com/).

Run the command below from your terminal to begin this deployment which would last for few minutes:

<pre><code class="language-bash">yarn webiny deploy</code></pre>

After a successful deployment of all three apps, the URL to the Admin App, GraphQL API endpoint and website would be printed out in the terminal. You can save them in an editor for later use.

**Note**: *The command above deploys the three generated applications collectively. Please visit [this](https://docs.webiny.com/docs/how-to-guides/deployment/deploy-your-project#the-app-deploy-command) part of the [Webiny documentation](https://docs.webiny.com/docs/webiny/introduction) on instructions on how to deploy the applications individually.*

Next, we will be setting up the Headless CMS using the admin application generated for managing your Webiny project.

## Webiny Admin App

As part of the first time installation process when you access your admin app, you would be prompted to create a default user with your details, and a password to secure your admin app, after which you proceed through the installation prompts for the Headless CMS, Page Builder and Form Builder.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0de3069-ade9-4f09-a88d-f448b3d25bf0/modeling-graphql-api-blog-webiny-serverless-cms-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0de3069-ade9-4f09-a88d-f448b3d25bf0/modeling-graphql-api-blog-webiny-serverless-cms-2.png" width="800" height="366" sizes="100vw" caption="Welcome page of the Admin App showing other Webiny Apps. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0de3069-ade9-4f09-a88d-f448b3d25bf0/modeling-graphql-api-blog-webiny-serverless-cms-2.png'>Large preview</a>)" alt="Welcome page of the Admin App showing other Webiny Apps." >}}

From the Admin welcome page shown above, navigate to the **Content Models** page by clicking on the **New Content Model** button within the **Headless CMS** card. Being a new project, the Content Models list would be empty, we move on next to create our first Content Model.

For our use-case, each content model would represent a blog post, this means each time we want to create a blog post we would create a content model and the data would be saved into the database and added to GraphQL API.

Clicking the lemon floating action button would display the modal with the fields for creating a new **Content Model** as shown in the image below.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9625bed-8942-4c5e-a03c-4cf5387550d4/3-modeling-graphql-api-blog-webiny-serverless-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9625bed-8942-4c5e-a03c-4cf5387550d4/3-modeling-graphql-api-blog-webiny-serverless-cms.png" width="800" height="364" sizes="100vw" caption="Displayed create content modal with the needed fields for creating a new content. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9625bed-8942-4c5e-a03c-4cf5387550d4/3-modeling-graphql-api-blog-webiny-serverless-cms.png'>Large preview</a>)" alt="Displayed create content modal with the needed fields for creating a new content." >}}

After creating the content model from the image above, we can open the newly saved content model to begin adding fields containing data about the blog post into the content model.

The Webiny content model page has an easy-to-use [drag ‘n’ drop](https://en.wikipedia.org/wiki/Drag_and_drop) editor which supports dragging fields from the left side and dropping them into the editor on the right side of the page. These fields are of eight categories, each used to hold a specific type of value.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68d6c937-b8e7-4d5a-836a-1ffd89294829/modeling-graphql-api-blog-webiny-serverless-cms-4.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68d6c937-b8e7-4d5a-836a-1ffd89294829/modeling-graphql-api-blog-webiny-serverless-cms-4.png" width="800" height="366" sizes="100vw" caption="Webiny drag and drop content editor. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68d6c937-b8e7-4d5a-836a-1ffd89294829/modeling-graphql-api-blog-webiny-serverless-cms-4.png'>Large preview</a>)" alt="Webiny drag and drop content editor." >}}

Before we begin adding the fields for the content model, below is a layout of the items we want to be contained in the blog post.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbb1495f-d438-4947-9182-c6f5b24442a6/5-modeling-graphql-api-blog-webiny-serverless-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbb1495f-d438-4947-9182-c6f5b24442a6/5-modeling-graphql-api-blog-webiny-serverless-cms.png" width="800" height="539" sizes="100vw" caption="A flowchart containing items within a typical blog post. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbb1495f-d438-4947-9182-c6f5b24442a6/5-modeling-graphql-api-blog-webiny-serverless-cms.png'>Large preview</a>)" alt="A flowchart containing items within a typical blog post." >}}

**Note:** *While we do not have to insert the elements in the exact order above, however adding fields is much easier when we have a mental picture of the content model structure.*

Add the following items with their appropriate fields into the content editor to create the model structure above.

### 1. Article Title Item

Starting with the first item in the Article Title, we drag 'n’ drop the `TEXT` field into the editor. The `TEXT` field is appropriate for a title as it was created for short texts or single-line values.

Add the **Label**, **Helper Text** and **Placeholder Text** input values into the Field settings modal as shown below.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8accc41e-f8f9-4e27-b8a0-f2c9e9f5f2be/6-modeling-graphql-api-blog-webiny-serverless-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8accc41e-f8f9-4e27-b8a0-f2c9e9f5f2be/6-modeling-graphql-api-blog-webiny-serverless-cms.png" width="800" height="" sizes="100vw" caption="Field Settings Modal used for adding the values of a dropped field type. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8accc41e-f8f9-4e27-b8a0-f2c9e9f5f2be/6-modeling-graphql-api-blog-webiny-serverless-cms.png'>Large preview</a>)" alt="Field Settings Modal used for adding the values of a dropped field type." >}}

### 2. Date Item

Next for the Date, we drag ‘n’ drop the `DATE` field into the editor. `DATE` fields have an extra date format with options of either date only, time only, date time with timezone, or date time without a given timezone. For our use-case, we will select the date time alongside the timezone option as we want readers to see when the post was created in their current timezone.

### 3. Article Summary

For the Article summary item, we would drag the `LONG TEXT` field into the editor and fill in the **Label**, **Helper Text** and **Placeholder Text** inputs in the field settings. The `LONG TEXT` field is used to store multi-line text values and this makes it ideal as the article summary would have several lines summarizing the blog post.

We would use the `LONG TEXT` field to create the First Paragraph and Concluding Paragraph items since they all contain a lengthy amount of text values.

### 4. Sample Image

The `FILES` field is used for adding files and object data into the content model. For our use-case, we would add images into the content model using the `FILES`  field. Drag ‘n’ Drop the `FILES` field into the editor for adding images.

After adding all the fields above, click the Preview tab to show the fields input elements added into the content model then fill in the values of these input fields.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/018286e8-16fd-40c9-88b5-4e5e5aec651e/modeling-graphql-api-blog-webiny-serverless-cms-7.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/018286e8-16fd-40c9-88b5-4e5e5aec651e/modeling-graphql-api-blog-webiny-serverless-cms-7.png" width="800" height="451" sizes="100vw" caption="Preview showing all fields dropped in the content model editor. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/018286e8-16fd-40c9-88b5-4e5e5aec651e/modeling-graphql-api-blog-webiny-serverless-cms-7.png'>Large preview</a>)" alt="Preview showing all fields dropped in the content model editor." >}}

From the **Preview Tab** above, we can see a preview of all model fields dropped into the drag ‘n’ editor for creating a blog post using the content model. Add the respective values into each of the input fields above then click on the Save button at the bottom.

After saving, we can view these input values by querying the GraphQL API using the GraphQL playground. Navigate to the API Information page using the sidebar, to access the GraphQL playground for your project.

Using GraphQL editor, you can inspect the entire GraphQL API structure using the schema introspection feature from the Docs.

We can also create and test GraphQL queries and mutations on our content models using the GraphQL Playground before using them from a client-side application.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67d71def-93e4-48ce-b1df-3dd0559ed383/8-modeling-graphql-api-blog-webiny-serverless-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67d71def-93e4-48ce-b1df-3dd0559ed383/8-modeling-graphql-api-blog-webiny-serverless-cms.png" width="800" height="367" sizes="100vw" caption="GraphQL playground for testing the generated Headless CMS GraphQL API. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67d71def-93e4-48ce-b1df-3dd0559ed383/8-modeling-graphql-api-blog-webiny-serverless-cms.png'>Large preview</a>)" alt="GraphQL playground for testing the generated Headless CMS GraphQL API." >}}

Within the image above we used the `getContentModel` query from our generated GraphQL API to query our Webiny database for data about the last content model we created. To get this exact model we had to pass in the `modelID` of the new model as an argument into the `getContentModel` query.

At this point, we have set up our Webiny project and modeled our GraphQL API using the generated Webiny Admin application. We are now left with consuming the GraphQL API from a frontend application as a source of data. The following steps below describe how to consume your GraphQL API within a Gatsby Application.

### Generate An API Access Key

All requests made to your Webiny GraphQL API endpoint must contain a valid token within its request headers for authentication. This token is obtained when you generate an API Key.

From the side menu, click the **API Keys** item within the **Security** dropdown to navigate to the API Keys page where you create and manage your API Keys for your GraphQL API.

Using the right placed form, we give the new key a name and a description, then we select the **All locales** radio button option within the Content dropdown. Lastly, within the Headless CMS dropdown, we select the **Full Access** option from the Access Level dropdown to give this key full access to data within the Headless CMS app of our Admin project.

**Note:** *When granting app access permission to your API keys, Webiny provides a ***Custom Access*** option within the* ***Access Level*** dropdown to streamline what the API key can be used for within the selected application.*

After saving the new API Key, a token key would be generated to be used when accessing the API Key. From the image below you can see an example of a token generated for my application within the highlighted box.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74c12af2-b37d-4bd9-b78b-e338127df07d/modeling-graphql-api-blog-webiny-serverless-cms-9.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74c12af2-b37d-4bd9-b78b-e338127df07d/modeling-graphql-api-blog-webiny-serverless-cms-9.png" width="800" height="452" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74c12af2-b37d-4bd9-b78b-e338127df07d/modeling-graphql-api-blog-webiny-serverless-cms-9.png'>Large preview</a>)" alt="" >}}

Take note of this token key as we would use it next from our Gatsby Web Application.

### Setting A Gatsby Single Page Application

Execute the command below to start the installer for creating a new Gatsby project on your local machine using [NPM](https://www.npmjs.com/) and select your project preference from the installation prompts.

<pre><code class="language-bash">npm init gatsby</code></pre>

Next, run this command to install the following needed dependencies into your Gatsby project;

<div class="break-out">

<pre><code class="language-bash">yarn add gatsby-source-graphql styled-components react-icons moment</code></pre>
</div>

To use GraphQL within our Gatsby project, open the `gatsby-config.js` and modify it to have the same content with the codes in the code block below;

<div class="break-out">

 <pre><code class="language-javascript">// gatsby-config.js

module.exports = {
    siteMetadata: {
        title: "My Blog Powered by Webiny CMS",
    },
    plugins: [
        "gatsby-plugin-styled-components",
        "gatsby-plugin-react-helmet",
        `gatsby-plugin-styled-components`,
        {
            resolve: `gatsby-source-filesystem`,
            options: {
                name: `images`,
                path: `${__dirname}/src/images`,
            },
        },
        {
            resolve: "gatsby-source-graphql",
            options: {
                // Arbitrary name for the remote schema Query type
                typeName: "blogs",
                // Field for remote schema. You'll use this in your Gatsby query
                fieldName: "posts",
                url: process.env.GATSBY_APP_WEBINY_GRAPHQL_ENDPOINT,
                headers : {
                    Authorization : process.env.GATSBY_APP_WEBINY_GRAPHQL_TOKEN
                }
            },
        },
    ],
};
</code></pre>
</div>

Above we are adding an external GraphQL API to Gatsby’s internal GraphQL API using the [gatsby-source-graphql](https://www.gatsbyjs.com/plugins/gatsby-source-graphql/) plugin. As an extra option, we added the GraphQL endpoint URL and access token value into the request headers from our Gatsby environment variables.

**Note:** *Run the `yarn Webiny info` command from a terminal launched within the Webiny project to print out the GraphQL API endpoint used in the `url` field of the `gatsby-config.js` file above.*

When next we start the Gatsby application, our GraphQL schema and data would be merged into Gatsby’s default generated schema which we can introspect using Gatsby’s GraphiQL Playground to see the fields similar to the those in the image below at `https://localhost:8000/___graphql`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60356920-4b15-45f1-9430-47f3f9ec4c5b/modeling-graphql-api-blog-webiny-serverless-cms-10.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60356920-4b15-45f1-9430-47f3f9ec4c5b/modeling-graphql-api-blog-webiny-serverless-cms-10.png" width="800" height="366" sizes="100vw" caption="GraphiQL playground generated by Gatsby for testing and introspecting the Gatsby generated schema. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60356920-4b15-45f1-9430-47f3f9ec4c5b/modeling-graphql-api-blog-webiny-serverless-cms-10.png'>Large preview</a>)" alt="GraphiQL playground generated by Gatsby for testing and introspecting the Gatsby generated schema." >}}

Above we tested the Webiny remote schema with a test query alongside exploring the remote schema to see what fields are available within our Gatsby application.

**Note:** *A new test content model was later created to demonstrate multiple content models being returned from the `listContentModels` query.*

To query and display this data within the Gatsby application, create a new file ( `posts.js` ) containing the following React component:

<div class="break-out">

<pre><code class="language-javascript">import React from "react"
import {FiCalendar} from "react-icons/fi"
import {graphql, useStaticQuery, Link} from "gatsby";
import Moment from "moment"

import {PostsContainer, Post, Title, Text, Button, Hover, HoverIcon} from "../styles"
import Header from "../components/header"
import Footer from "../components/footer"

const Posts = () =&gt; {
    const data = useStaticQuery(graphql`
        query fetchAllModels {
            posts {
                listContentModels {
                    data {
                        name
                        description
                        createdOn
                        modelId
                    }
                }
            }
        }`)

    return (
        &lt;div&gt;
            &lt;Header title={"Home   ||   Blog"}/&gt;

            &lt;div style={{display: "flex", justifyContent: "center",}}&gt;

                &lt;PostsContainer&gt;
                    &lt;div&gt;
                        &lt;Title align={"center"} bold&gt; A collection of my ideas&lt;/Title&gt;
                        &lt;Text align={"center"} color={"grey"}&gt; A small space to document my thoughts in form of blog posts and articles &lt;/Text&gt;
                    &lt;/div&gt;
                    &lt;br/&gt;
                    {
                        data.posts.listContentModels.data.map(({id, name, description, createdOn, modelId}) =&gt; (
                            &lt;Post key={id}&gt;
                                &lt;div style={{display: "flex"}}&gt;
                                    &lt;HoverIcon&gt;
                                        &lt;FiCalendar/&gt;
                                    &lt;/HoverIcon&gt;

                                    &lt;div&gt;
                                        &lt;Text small
                                              style={{marginTop: "2px"}}&gt; {Moment(createdOn).format("dddd, m, yyyy")} &lt;/Text&gt;
                                    &lt;/div&gt;
                                &lt;/div&gt;
                                &lt;br/&gt;
                                &lt;Title bold align={"center"}&gt; {name} &lt;/Title&gt;
                                &lt;br/&gt;
                                &lt;Text align={"center"}&gt; {description} &lt;/Text&gt;
                                &lt;br/&gt;
                                &lt;div style={{textAlign: "right"}}&gt;
                                    &lt;Link to={`/${modelId}`} state={{modelId}}&gt;
                                        &lt;Button onClick={_ =&gt; {
                                        }}&gt; Continue Reading &lt;/Button&gt;
                                    &lt;/Link&gt;
                                &lt;/div&gt;
                            &lt;/Post&gt;
                        ))
                    }
                    &lt;br/&gt;

                &lt;/PostsContainer&gt;
            &lt;/div&gt;

            &lt;Footer/&gt;

        &lt;/div&gt;

    )
}

export default Posts</code></pre>
</div>

From the code block above, we are making a query using the [useStaticQuery](https://www.gatsbyjs.com/docs/how-to/querying-data/use-static-query/) hook from Gatsby and we use the returned data to populate the posts within the component styled using styled-components.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9b39f6c-a8d7-403a-a6ab-38cb2eb0ac5d/11-modeling-graphql-api-blog-webiny-serverless-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9b39f6c-a8d7-403a-a6ab-38cb2eb0ac5d/11-modeling-graphql-api-blog-webiny-serverless-cms.png" width="800" height="381" sizes="100vw" caption="Gatsby blog application home page showing a list of content models from GraphQL API. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9b39f6c-a8d7-403a-a6ab-38cb2eb0ac5d/11-modeling-graphql-api-blog-webiny-serverless-cms.png'>Large preview</a>)" alt="Gatsby blog application home page showing a list of content models from GraphQL API." >}}

Taking a closer look at the **Continue Reading** button in the code block above, we can see it is wrapped with a link that points to a page’s name of the `modelId` currently being iterated over. This page would be created dynamically from a template each time the Gatsby application is started.

To implement this creation of dynamic pages, create a new file (`gatsby-node.js`) with the following code.

<div class="break-out">

<pre><code class="language-javascript"># gatsby-node.js
const path = require("path")

exports.createPages = async ({graphql, actions, reporter}) =&gt; {
    const {createPage} = actions

    const result = await graphql(`
   query getContent {
    posts {
    listContentModels {
      data {
        description
        createdOn
        modelId
        name
      }
    }
  }
}`)

    // Template to create dynamic pages from.
    const blogPostTemplate = path.resolve(`src/pages/post.js`)

    result.data.posts.listContentModels.data.forEach(({description, modelId, createdOn, name}) =&gt; {
        createPage({
            path: modelId,
            component: blogPostTemplate,
            // data to pass into the dynamic template
            context: {
                name, description, modelId, createdOn
            },
        })
    })
}</code></pre>
</div>

As an overview, the code block above adds a new task into our Gatsby Application to be performed immediately after the application is started. At a closer look, we can see the following operations being done while performing this task.

First, we make a GraphQL query to fetch all models created on Webiny which returns an array with the contained fields, then we iterate over the result each time using the [createPage](https://www.gatsbyjs.com/docs/creating-and-modifying-pages/#creating-pages-in-gatsby-nodejs) API from Gatsby to create a new page dynamically using the component in `./pages/post.js` as a template.

Lastly, we passed in the data that we received from iterating over each object in the Query result into the component being used as a template.

At this point, the template component is non-existent. Create a new file (`post.js`) with the code below to create the template.

<div class="break-out">

 <pre><code class="language-javascript"># ./pages/post.js

import React from "react"
import Moment from "moment"

import Header from "../components/header"
import Footer from "../components/footer"
import {PostContainer, Text, Title} from "../styles";
import Layout from "../components/layout";

const Post = ({ pageContext }) =&gt; {
    const { name, description , createdOn} = pageContext

    return (
        &lt;Layout&gt;
            &lt;Header title={name}/&gt;
            &lt;br/&gt;

            &lt;div style={{display: "flex", justifyContent: "center"}}&gt;
                &lt;PostContainer&gt;
                    &lt;Title align={"center"}&gt; {name} &lt;/Title&gt;
                    &lt;Text color={"grey"} align={"center"}&gt;
                      Created On {Moment(createdOn).format("dddd, mm, yyyy")}
                    &lt;/Text&gt;
                    &lt;br/&gt;
                    &lt;Text&gt; {description} &lt;/Text&gt;
                &lt;/PostContainer&gt;
            &lt;/div&gt;

            &lt;br/&gt;

            &lt;Footer/&gt;
        &lt;/Layout&gt;
    )
}

export default Post</code></pre>
</div>

Above we created a component that is used as a template to create other dynamic pages. This component receives a `pageContext` object each time it is used as a template, the fields within the object are further destructured and used to populate the data shown on the page, same as the example shown below.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0709a3cc-8f5c-4287-8fb2-b25a490cf3d6/modeling-graphql-api-blog-webiny-serverless-cms-12.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0709a3cc-8f5c-4287-8fb2-b25a490cf3d6/modeling-graphql-api-blog-webiny-serverless-cms-12.png" width="800" height="385" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0709a3cc-8f5c-4287-8fb2-b25a490cf3d6/modeling-graphql-api-blog-webiny-serverless-cms-12.png'>Large preview</a>)" alt="Webiny blog post" >}}

## Conclusion

Within this article we have had a detailed look into what Webiny is, the serverless features it provides, and also how the [Headless CMS](https://www.webiny.com/serverless-app/headless-cms) can be used with a Static Website Generator such as Gatsby as a source of data.

As explained earlier, there are more serverless services which Webiny provides apart from the [Headless CMS](https://www.webiny.com/serverless-app/headless-cms), such as the No-code [Form Builder](https://www.webiny.com/serverless-app/form-builder) for building interactive forms, [Page Builder](https://www.webiny.com/serverless-app/page-builder), and even a [File Manager](https://www.webiny.com/serverless-app/file-manager) for use within your applications.

If you are looking for a service to leverage when building your next serverless application, then you should give Webiny a try. You can [join the Webiny community on Slack](https://www.webiny.com/slack) or [contribute](https://github.com/webiny/webiny-js/blob/master/docs/CONTRIBUTING.md) to the *Open Source Webiny project* on [Github](https://github.com/webiny/).

### References

- [Webiny Serverless CMS](https://www.webiny.com/serverless-cms)
- [Webiny on GitHub](https://github.com/webiny/)
- [Gatsby.js](https://www.gatsbyjs.com/) (official website)
- [Gatsby.js Docs](https://www.gatsbyjs.com/docs/)
- [Building A Web App With Headless CMS And React](https://www.smashingmagazine.com/2020/04/web-app-headless-cms-react/), Blessing Krofegha

{{< signature "vf, il, yk" >}}

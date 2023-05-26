---
title: 'Building Gatsby Themes For WordPress-Powered Websites'
slug: building-gatsby-themes-wordpress-powered-websites
author: paulina-hetman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5b60a4b-63f6-47e2-a9aa-33faa3e9ca9e/building-gatsby-themes-wordpress-powered-websites.jpg
date: 2021-12-27T10:30:00.000Z
summary: >-
  Have you already built and published a Gatsby theme? In this article, Paulina Hetman explains how Gatsby themes work and what problems they can solve by comparing Gatsby themes with their WordPress counterparts.
description: >-
  Have you already built and published a Gatsby theme? In this article, Paulina Hetman explains how Gatsby themes work and what problems they can solve by comparing Gatsby themes with their WordPress counterparts.
categories:
  - UI
  - Tools
  - Gatsby
  - WordPress
  - Frameworks
---

[Gatsby](https://www.gatsbyjs.com) is an open-source framework built on top of React. With Gatsby, you can pull data from (almost) anywhere and use it to generate static or dynamic websites. The data can be pulled from a CMS, which definitely brings WordPress to the table. You get the advantages of a static website (speed, security, static hosting) while you continue to manage your content via a WordPress dashboard.

One of the particularities of [Gatsby framework](https://www.gatsbyjs.com/) is that it proposes themes as a customization tool. As someone with a strong background in WordPress, I find the concept of Gatsby themes particularly appealing. I used to design and develop WordPress themes. However, with the growing interest in Jamstack solutions, I gradually shifted towards working with WordPress as a headless CMS. In this article, I would like to share some concepts that I have learned from this transition.

**Note:** *Before we go any further, let’s focus on the tools that we are going to use. Gatsby provides an official [gatsby-source-wordpress](https://www.gatsbyjs.com/plugins/gatsby-source-wordpress/) plugin. To make it work, we need to prepare our WordPress end. More precisely, we need to expose the Gatsby-flavored WordPress data via a GraphQL API. In practice, that means installing two WordPress plugins [WPGraphQL](https://wordpress.org/plugins/wp-graphql/) and [WPGatsby](https://wordpress.org/plugins/wp-gatsby/). Both are available via the official WordPress plugins repository and do not require any configuration.*

## What Are Gatsby Themes?

Gatsby theme is a bunch of shared functionalities abstracted within a Node.js package. A theme is therefore destined to be published (to a registry like [npm](https://docs.npmjs.com/about-npm)) and reused as an installable dependency. 

Since we are talking Gatsby and *WordPress* here, I will clarify it straight away &mdash; there are similarities with WordPress themes, but we should not equate the notion of WordPress themes with Gatsby themes. For someone with a WordPress background (like myself), the dissociation may be challenging at the beginning.

A **WordPress theme** is a mandatory system of templates that defines what we see on the front end. The responsibility of a *good* WordPress theme ends here. It should not introduce any functionalities since functionalities are the plugins’ territory. There is, therefore, a strict separation between themes and plugins in the WordPress ecosystem. Themes should take care of the presentation layer, and plugins take care of the functional aspects.

Following the Gatsby definition, **themes are responsible for functionalities**. Shouldn’t we call them plugins then? Actually, Gatsby, like WordPress, has both plugins and themes. Plugins, just like themes, are installable Node.js packages that implement Gatsby APIs. And in fact, a Gatsby theme is a Gatsby plugin. If a plugin owns a section, a page, or part of a page on a site &mdash; we call it a theme. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e2eb82-fd15-46cb-b469-d7bac3580c82/7-building-gatsby-themes-wordpress-powered-websites.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e2eb82-fd15-46cb-b469-d7bac3580c82/7-building-gatsby-themes-wordpress-powered-websites.png" width="800" height="333" sizes="100vw" caption="The relationship between plugins and themes in WordPress and in Gatsby. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e2eb82-fd15-46cb-b469-d7bac3580c82/7-building-gatsby-themes-wordpress-powered-websites.png'>Large preview</a>)" alt="An illustration representing plugins and themes as oval sets. WordPress plugins and themes are separate set, for Gatsby themes are a subset of plugins." >}}

Moreover, unlike WordPress, Gatsby does not require using themes to build a site. Instead, you would probably start creating your site by setting up a project structured as below:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f48b8785-8ea4-4b1b-816d-bec8fe56a555/9-building-gatsby-themes-wordpress-powered-websites.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f48b8785-8ea4-4b1b-816d-bec8fe56a555/9-building-gatsby-themes-wordpress-powered-websites.png" width="800" height="470" sizes="100vw" caption="How you typically structure your Gatsby project. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f48b8785-8ea4-4b1b-816d-bec8fe56a555/9-building-gatsby-themes-wordpress-powered-websites.png'>Large preview</a>)" alt="An illustration of a folder structure on the left, containing node modules, src with Components, Pages and Templages, gatsby-config.js and gatsby-node.js file. Two arrows point to the computer screen on the right. One starts at the folder structure another start at the WP icon." >}}

That’s ok until you have more than one site to maintain. In that case, you might want to abstract the common parts of the process and manage (version and update) them separately.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd012403-8f1d-405b-89bc-01f40ba10a93/6-building-gatsby-themes-wordpress-powered-websites.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd012403-8f1d-405b-89bc-01f40ba10a93/6-building-gatsby-themes-wordpress-powered-websites.png" width="800" height="394" sizes="100vw" caption="Rethinking project structure towards using a Gatsby theme. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd012403-8f1d-405b-89bc-01f40ba10a93/6-building-gatsby-themes-wordpress-powered-websites.png'>Large preview</a>)" alt="An illustration of a folder structure on the left, containing node modules, src with Components, Pages and Templages, gatsby-config.js and gatsby-node.js file. A part of the src, gatsby-config.js and gatsby-node.js are encircled together. This part is linked with to texts: common for all Gatsby + WP projects and let’s publish as a Gatsby theme." >}}

Thanks to Gatsby theming system, you can bundle the shared parts into a package (or multiple packages), publish the packages and finally install them throughout numerous applications. Note, that I used the plural form *packages* &mdash; you can combine multiple themes within a project.

{{% feature-panel %}}

## Child Themes And Shadowing

When working with Gatsby and WordPress, you will identify some core functionalities that are common for all projects. I mean here: sourcing the data and building the pages dynamically. It seems worthwhile to have a theme that takes care of the data sourcing logic and the creation of the pages. On the other hand, how you decide to display your pages may change from one project to another. Whatever you set at the core level, you will probably need to override at some point.

One of the possible approaches is to have a core (parent) theme and build *child themes* on top of the core one.

What do I mean by a Gatsby child theme?

Let’s proceed with a comparison of WordPress child themes. WordPress child themes allow us to add functionalities and override templates. They provide a safe way to enhance and modify an existing theme.

A Gatsby child theme uses a parent theme as its plugin. We can then use the concept of [shadowing](https://www.gatsbyjs.com/docs/how-to/plugins-and-themes/shadowing/) that gives the child theme the capability to override the parent theme files; that’s similar to overriding WordPress templates in a child theme. Shadowing means that we can override files from the `src` directory included in the webpack bundle. It’s worth underlining that shadowing is possible on the project level (where we consume our themes as packages). We’ll see it in action later in this article.

With WordPress, we are limited to only one parent theme, only one child theme, and no further chaining is possible. With the flexibility of Gatsby themes, we can go much further. It’s possible to build different configurations of child-parent chains.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07525649-3d79-4211-81fe-f783ce995e66/8-building-gatsby-themes-wordpress-powered-websites.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07525649-3d79-4211-81fe-f783ce995e66/8-building-gatsby-themes-wordpress-powered-websites.png" width="800" height="318" sizes="100vw" caption="Themes structure in WordPress vs Gatsby. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07525649-3d79-4211-81fe-f783ce995e66/8-building-gatsby-themes-wordpress-powered-websites.png'>Large preview</a>)" alt="An illustration with WordPress site on the left with two themes chain wp-theme-child and wp-theme (parent), on the right Gatsby site with more complex system of multiple themes." >}}

Let’s now see Gatsby theming in action. In our example, we will build two themes, `gatsby-theme-wp-parent` and its child-theme `gatsby-theme-wp-child`. I chose this setup for the sake of simplicity. In a real-world scenario, you might want to decompose your functionalities into more themes, each one with some specific responsibility.

We will publish our themes, install them in a project, and add further customization via project-level shadowing.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a98737b-2f16-41e2-85a3-7ba801de1430/2-building-gatsby-themes-wordpress-powered-websites.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a98737b-2f16-41e2-85a3-7ba801de1430/2-building-gatsby-themes-wordpress-powered-websites.png" width="800" height="488" sizes="100vw" caption="Simplified files structure for the final project. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a98737b-2f16-41e2-85a3-7ba801de1430/2-building-gatsby-themes-wordpress-powered-websites.png'>Large preview</a>)" alt="An illustration representing a site folder containing gatsby-theme-wp-parent and gatsby-theme-wp-child in node modules, together with src containing some extra stuff overrides (shadowing) and the gatsby-config.js file. An arrow from the text ‘we’ll build these’ points to gatsby-theme-wp-parent and gatsby-theme-wp-child" >}}

## Development Setup

The last illustration depicts the structure of the final user’s project (*site)*, where the themes are consumed. They are installed as the project’s dependencies. This setup assumes that the themes are available via some npm repository, which means we’ve already published them. We’re not there yet. We need to *build* the parent and child themes first. But what does the *development* setup looks like? Our themes are two independent packages, but we need to work on them in parallel within a single project during the development. Moreover, we want to set up a demo within the same project that implements the themes directly.

One of the possible solutions is [yarn workspaces](https://classic.yarnpkg.com/en/docs/workspaces/). With yarn workspaces, we work within a single mono-repo with a single lock file at the project-root level. Moreover, the dependencies can be linked together, which means that the workspaces depend on one another, and we use the local versions during development. 

How to set up yarn workspaces? First, make sure to have [yarn installed globally](https://classic.yarnpkg.com/lang/en/docs/install/). Next, at the root of your monorepo, add the `package.json` file that specifies the workspaces:

<pre><code class="language-javascript">{
  "private": true,
  "workspaces": [
    "packages/*",
    "demo"
  ]
}</code></pre>

Now, each theme is a subfolder within `packages` with its own `package.json` file and an empty main entry `index.js`. I proceed like so with each theme I add:

<div class="break-out">

<pre><code class="language-javascript">mkdir packages/gatsby-theme-wp-parent
touch packages/gatsby-theme-wp-parent/package.json packages/gatsby-theme-wp-parent/index.js</code></pre>
</div>

With the `package.json` as follows:

<pre><code class="language-json">{
  "name": "@pehaa/gatsby-theme-wp-parent",
  "version": "1.0.0",
  "license": "MIT",
  "main": "index.js"
}</code></pre>

We’ll discuss the theme publishing a little bit further. But, for the moment, let’s note that we will publish our themes as scoped packages; I use my nickname `@pehaa` as a scope here. Remember that, if you decide to publish scoped packages to the public npm registry [https://registry.npmjs.org](https://registry.npmjs.org/), you must state the public access explicitly and add the following to their `package.json` files:

<pre><code class="language-json">"publishConfig": {
  "access": "public"
}</code></pre>

In addition to themes, we will also need a `demo` workspace from which we will try out our code. The demo has to be a `"private"` package since it is not supposed to be published.

<pre><code class="language-javascript">// demo/package.json
{
  "private": true,
  "name": "demo",
  "version": "1.0.0",
  "scripts": {
    "build": "gatsby build",
    "develop": "gatsby develop",
    "clean": "gatsby clean"
  }
}</code></pre>

With the workspaces setup, we can run the develop or build scripts from anywhere in our monorepo by specifying the script and the workspace like so:

<pre><code class="language-bash">yarn workspace demo develop</code></pre>

By the way, you are not limited to a single `demo`. For example, our `GatsbyWPThemes` monorepo contains multiple demos that we add to the `examples` directory. In this case, the root-level `package.json` file defines workspaces as follows:

<pre><code class="language-json">"workspaces": [
  "packages/*",
  "examples/*"
]</code></pre>

{{% ad-panel-leaderboard %}}

## Building Gatsby Themes

First of all, we need to install `react`, `react-dom` and `gatsby`. We need to install these three as peer dependencies (`-P`) in each theme and as dependencies in our demo. We also install the parent theme as the child’s theme dependency and the child theme as the demo’s dependency.

<div class="break-out">

<pre><code class="language-bash">yarn workspace @pehaa/gatsby-theme-wp-parent add -P react react-dom gatsby
yarn workspace @pehaa/gatsby-theme-wp-child add -P react react-dom gatsby
yarn workspace @pehaa/gatsby-theme-wp-child add "@pehaa/gatsby-theme-wp-parent@*"
yarn workspace demo add react react-dom gatsby "@pehaa/gatsby-theme-wp-child@*"</code></pre>
</div>

**Note**: *You can’t add `@pehaa/gatsby-theme-wp-parent` or `@pehaa/gatsby-theme-wp-child` without a version number. You must specify it as either `@*` or `@1.0.0`. Without it, npm will try to fetch the package from the repository instead of using the local one. Later on, when we publish our packages with Lerna, all the `*` will be automatically updated to the current theme versions and kept in sync.*

### Parent Theme

Let’s now focus on the parent theme and its dependencies: 

<div class="break-out">

<pre><code class="language-bash">yarn workspace @pehaa/gatsby-theme-wp-parent add gatsby-source-wordpress gatsby-plugin-image gatsby-plugin-sharp gatsby-transformer-sharp gatsby-awesome-pagination</code></pre>
</div>

Our parent theme’s responsibility is to load the source plugin and three plugins required for processing and displaying images. We load them all in the `gatsby-config.js` file. 

<pre><code class="language-javascript">// gatsby-config.js
module.exports = (options) =&gt; {
  return {
    plugins: [
      'gatsby-plugin-sharp', // must have for gatsby
      'gatsby-transformer-sharp', // must have for gatsby images
      'gatsby-plugin-image',
      {
        resolve: 'gatsby-source-wordpress',
        options: {
          url: `${options.wordPressUrl}/graphql`,
        },
      },
    ],
  }
}
</code></pre>

Besides sourcing the content, we need to build routes for our WordPress content dynamically. We need to create routes for WordPress static pages, individual posts, blog archive, category archive, and tags archive. Gatsby provides the `createPages` API as a part of [Gatsby Node API](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-node/). Let’s take a look at the code responsible for the creation of individual posts.

<div class="break-out">

<pre><code class="language-javascript">exports.createPages = async ({ graphql, actions }) =&gt; {
  const { createPage } = actions
  const postsQuery = await graphql(`
    query GET_POSTS {
      allWpPost(sort: {order: DESC, fields: date}) {
        edges {
          node {
            uri
            id
          }
        }
      }
    }
  `)
  const posts = postsQuery.data.allWpPost.edges
  posts.forEach(({ node }) =&gt; {
    createPage({
      path: node.uri, 
      component: path.resolve('../src/templates/post-query.js'),
      context: {
        // Data passed to context is available in page queries as GraphQL variables
        // we need to add the post id here
        // so our blog post template knows which blog post it should display
        id: node.id
      },
    })
  })
}</code></pre>
</div>

You can find the complete code in [this GitHub repository](https://github.com/pehaa/gatsby-wp-theming). You may notice that it varies depending on the page type. It is different for a post, a page, or an archive, especially with the pagination implemented for the latter. Still, it follows the same pattern: 

- run an async `graphql` “get items” query;
- loop over the resulting items and run the `createPage` helper function for each item, passing:
    - the path,
    - `component` &mdash; the template file; Gatsby has to know what each page should display,
    - `context` &mdash; whatever data the template (provided in the `component` field) might need.

Since we do not want to worry about the UI part within the parent theme &mdash; we delegate it to the component that we will shadow in the child theme.

<pre><code class="language-javascript">// src/templates/post-query.js
import { graphql } from "gatsby"
import Post from "../components/Post" 
export default Post 

export const pageQuery = graphql`
  query ($id: String!) {
    wpPost(id: { eq: $id }) {
      # query all usefull data
    } 
  }
`</code></pre>

The `Post` component has access to the data from the `graphql` page query defined in the template file. Our component receives the query results via props as `props.data`. Our component file is separated from the template but has access to its data. With this setup, we are able to shadow `Post` component without having to rewrite the query. 

<pre><code class="language-javascript">// src/components/Post.js
import React from 'react'
const Post = (props) =&gt; {
  return &lt;pre&gt;{JSON.stringify(props.data, null, 2)}&lt;/pre&gt;
}
export default Post</code></pre>

### Child Theme

Now, let’s move on to the child theme and add its dependencies.

**Note**: *I chose to use [Chakra UI](https://chakra-ui.com/) as components library, it’s based on [emotion](https://emotion.sh/) and comes with its own [Gatsby plugin](https://www.gatsbyjs.com/plugins/@chakra-ui/gatsby-plugin/). We also need to install WordPress-content-specific styles from `@wordpress/block-library`.*

<div class="break-out">

<pre><code class="language-bash">yarn workspace @pehaa/gatsby-theme-wp-child add @chakra-ui/gatsby-plugin @chakra-ui/react @emotion/react @emotion/styled @wordpress/block-library framer-motion gatsby-plugin-webfonts html-react-parser</code></pre>
</div>

The child theme’s responsibility is the UI part, and we need to override the bare bone output generated by the parent theme. For the shadowing to work, we need to follow the files structure from the parent theme. For example, to override the `Post` component from `gatsby-theme-wp-parent/src/components/Post.js` we need to create a `Post.js` file in `gatsby-theme-wp-child/src/@pehaa/gatsby-theme-wp-parent/components`. The `@pehaa` intermediate folder corresponds to the scope of the `gatsby-theme-wp-parent` package.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07caaf1-becd-49c6-b29d-3d6fca91428e/3-building-gatsby-themes-wordpress-powered-websites.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07caaf1-becd-49c6-b29d-3d6fca91428e/3-building-gatsby-themes-wordpress-powered-websites.png" width="800" height="344" sizes="100vw" caption="Files structure for components shadowing. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f07caaf1-becd-49c6-b29d-3d6fca91428e/3-building-gatsby-themes-wordpress-powered-websites.png'>Large preview</a>)" alt="On the left the files structure of the shadowed gatsby-theme-wp-parent on the right the files structure of gatsby-theme-wp-child where shadowing happens." >}}

## Passing Options To Themes

We load and configure gatsby plugins in a `gatsby-config.js` file. We will have three config files in our setup, one on each level, our parent theme, the child theme, and the demo.

<pre><code class="language-bash">├── demo
│      └── gatsby-config.js
├── packages
│   ├── gatsby-theme-wp-child
│   │   └── gatsby-config.js
│   └── gatsby-theme-wp-parent
│       └── gatsby-config.js
└── ...</code></pre>

On the demo level, the config loads the child theme like so:

<pre><code class="language-javascript">// demo/gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: '@pehaa/gatsby-theme-wp-child',
      options: {
        wordPressUrl: process.env.GATSBY_WP_URL,
        /* other options */
      },
    },
  ],
}</code></pre>

As you can see above, we pass options to the child theme. These will be available within the config file on the child theme’s level. That’s possible since Gatsby plugins have config exported as a function. Thus, when we load a plugin providing some options, the plugin receives them as an argument of its config function. In particular, the options that we pass to a theme can be “forwarded” to its parent-level theme like so:

<div class="break-out">

<pre><code class="language-javascript">// gatsby-theme-wp-child/gatsby-config.js
const defaultFonts  = ...
module.exports = (options) =&gt; {
  // destructure option to extract fonts 
  const {fonts, ...rest} = options
  return {
    plugins: [
      {
        resolve: `@pehaa/gatsby-theme-wp-parent`,
        options: {
          // "forward" the options gatsby-theme-wp-child options to its parent theme
          ...rest
        }
      },
      '@chakra-ui/gatsby-plugin',
      {
        resolve: `gatsby-plugin-webfonts`,
        options: {
          fonts: fonts || defaultFonts
        },
      },
    ],
  }
}</code></pre>
</div>

Let’s look again at the code above. Note that we define font faces on the child-theme level, but we keep the possibility to modify them via theme options.

<pre><code class="language-javascript">// demo/gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `@pehaa/gatsby-theme-wp-child`,
      options: {
        wordPressUrl: process.env.GATSBY_WP_URL,
        fonts: {
          google: [{family: "Rubik"}],
        },
      },
    },
  ],
}</code></pre>

When configuring our themes, we should remember that a theme is just a package, and the end-user does not directly access its code. Therefore, it’s a good idea to think ahead and expose proper settings. If our theme loads a plugin that requires configuration, we probably should pass the plugins options from the project (demo) level all the way down.

Let’s look into an example. Our parent theme uses the `gatsby-source-wordpress` plugin that fetches the data from WordPress. This plugin comes with [a bunch of options](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-source-wordpress/docs/plugin-options.md), some of them possibly critical to the build process, like `schema.requestConcurrency`, or `schema.timeout`. But, again, the parent theme is just a package, and the end-user can not edit its `gatsby-config` file. It may seem obvious, but we somehow missed it in the initial release of Gatsby WP Themes. However, with a quick fix, the user can pass the `gatsby-plugin-source-wordpress` options from the project’s config…

<pre><code class="language-javascript">// user's project gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `@pehaa/gatsby-theme-wp-child`,
      options: {
        wordPressUrl: process.env.GATSBY_WP_URL,
        gatsbySourceWordPressOptions: {},
        // ...
      },
    },
  ],
}</code></pre>

… via the child and parent theme to the destination plugin:

<pre><code class="language-javascript">// packages/gatsby-theme-wp-parent/gatsby-config.js
module.exports = (options) =&gt; {
  return {
    plugins: [
      // ...
      {
        resolve: `gatsby-plugin-source-wordpress`,
        options: {
          url: `${options.wordPressUrl}/graphql`,
          ...options.gatsbySourceWordPressOptions
        },
      },
    ],
  }
}
</code></pre>

{{% ad-panel-leaderboard %}}

## CSS Theming

The CSS-in-JS solutions that support theming seem a good fit for Gatsby themes. Our Gatsby child theme will use [Chakra UI framework](https://chakra-ui.com/), and we will slightly customize its CSS theme. Yes, Chakra UI also uses the notion of a “theme”. In this context, a [theme](https://system-ui.com/theme/) is a JavaScript object that stores design system style values, scales, and/or design tokens. To avoid any confusion, I will refer to it as a “CSS theme”. We’ve already installed the required `@chakra-ui` packages together with the Gatsby plugin `@chakra-ui/gatsby-plugin`. Let’s explore [the plugin’s code](https://github.com/chakra-ui/chakra-ui/tree/main/tooling/gatsby-plugin) to find out how it works. It actually wraps our Gatsby application into the `ChakraProvider` and exposes the `src/theme.js` file for shadowing, so that we can proceed like so:

<div class="break-out">

<pre><code class="language-javascript">/* packages/gatsby-theme-wp-child/src/@chakra-ui/gatsby-plugin/theme.js */
import { extendTheme } from "@chakra-ui/react"
const theme = {
  fonts: {
    body: "Karma, sans-serif",
    heading: "Poppins, sans-serif",
  },
  styles: {
    global: {
      body: {
        color: "gray.700",
        fontSize: "xl",
      },
    },
  },
  components: {
    Button: {
      baseStyle: {
        borderRadius: "3xl",
      },
      defaultProps: {
        colorScheme: "red",
      },
    },
  },
}
export default extendTheme(theme)</code></pre>
</div>

Once again, we used the concept of shadowing. The key aspect here is the location where we created the `theme.js` file. 

Later on, we’ll see how to shadow the CSS theme on the user’s project level. 

## Publishing Themes With Lerna

Once your themes are ready, you need to publish them. If you want to share your code publicly, you will most probably publish it to the public [npm registry](https://docs.npmjs.com/about-npm). And if you’ve never published a package before, you can get familiar with the process by playing with [Verdaccio](https://verdaccio.org) on your local machine.

At [Gatsby WP Themes](https://gatsbywpthemes.com/), we use a premium service from Cloudsmith. [Cloudsmith](https://cloudsmith.com) supports fully-featured registries for npm packages with the premium option for private registries and a free solution for the public ones. I will continue with a free Cloudsmith solution. Once you have created your account, create a new repository; mine is `pehaa/gatsby-wp-theming`.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8f69137-23f4-4db0-8b90-e373821c88a4/1-building-gatsby-themes-wordpress-powered-websites.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8f69137-23f4-4db0-8b90-e373821c88a4/1-building-gatsby-themes-wordpress-powered-websites.png" width="800" height="" sizes="100vw" caption="My repositories in Cloudsmith app. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8f69137-23f4-4db0-8b90-e373821c88a4/1-building-gatsby-themes-wordpress-powered-websites.png'>Large preview</a>)" alt="Screenshot of the Cloudsmith app interface with the list of repositories containing pehaa/gatsby-wp-theming." >}}

In order to make changes to your Cloudsmith registry via your command line, you will need to provide your login credentials for this registry. Just type:

<div class="break-out">

<pre><code class="language-bash">npm login --registry=https://npm.cloudsmith.io/organistion/repository_name/</code></pre>
</div>

and you will be asked for your username, your password (which is your API KEY), and your email. 

With a multi-package git repository, you might want to use [Lerna](https://lerna.js.org) to facilitate the publishing. Lerna matches well with yarn workspaces. You can install Lerna CLI globally with `npm install --global lerna`. To initiate it within our project, we’ll run the following command:

<pre><code class="language-bash">lerna init --independent</code></pre>

The command above will create a `lerna.json` file in the root of the monorepo. You’ll need to add the `"useWorkspaces" : true` and `"npmClient": "yarn"` manually; you may also need to specify the `command.publish.registry` if it’s not the default public npm one.

<pre><code class="language-javascript">{
  "npmClient": "yarn",
  "useWorkspaces": true,
  "version": "independent",
  "command": {
    "publish": {
      "registry": "https://cloudsmith.io/organisation/repository_name"
    }
  }
}</code></pre>

Then, the `lerna publish` command publishes packages that have changed since the last release. By default, Lerna runs prompts for the version change of each package being updated. You can skip the prompts by running:

<div class="break-out">

<pre><code class="language-bash">lerna publish [major|minor|patch|premajor|preminor|prepatch|prerelease] --yes</code></pre>
</div>

You can also configure Lerna to use the [Conventional Commits Specification](https://conventionalcommits.org/) to [determine the version bump](https://github.com/conventional-changelog/conventional-changelog/tree/master/packages/conventional-recommended-bump) and [generate CHANGELOG.md files](https://github.com/conventional-changelog/conventional-changelog/tree/master/packages/conventional-changelog-cli). With all the options available, you should be able to adapt the way you use Lerna to your workflow.

## Using A Theme In A Project

Now, let’s stop the development server and take the user’s perspective. We will create a new project, `gatsby-wp-site`, that implements `gatsby-theme-wp-child` as a package installed from the npm repository. Within our project folder, we will install our four dependencies: `gatsby`, `react`, `react-dom`, and the theme itself. Since we used Cloudsmith to publish `@pehaa`-scoped packages, we’ll have to add a `.npmrc` file where we specify `@pehaa`-scoped repository like so:

<div class="break-out">

<pre><code class="language-bash">mkdir gatsby-wp-site
cd gatsby-wp-site
echo "@pehaa:registry=https://npm.cloudsmith.io/pehaa/gatsby-wp-theming/" &gt;&gt; .npmrc
yarn init -yp
yarn add react react-dom gatsby @pehaa/gatsby-theme-wp-child</code></pre>
</div>

Our site is almost ready. We only have to create a `gatsby-config.file` to load the theme and provide the WordPress URL. Once it’s done, we are ready to run `gatsby build`.

<pre><code class="language-javascript">// gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: "@pehaa/gatsby-theme-wp-child",
      options: {
        wordPressUrl: "https://yourwordpress.website"
      }
    }
  ]
}</code></pre>

Our [site](https://gatsby-wp-theming-demo.netlify.app/) is ready.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9516716e-6814-490a-8397-a0af672e16db/5-building-gatsby-themes-wordpress-powered-websites.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9516716e-6814-490a-8397-a0af672e16db/5-building-gatsby-themes-wordpress-powered-websites.jpg" width="800" height="" sizes="100vw" caption="Our build is ready. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9516716e-6814-490a-8397-a0af672e16db/5-building-gatsby-themes-wordpress-powered-websites.jpg'>Large preview</a>)" alt="An illustration with a screenshot from the site build within a computer screen." >}}

What about customization? We can still take advantage of shadowing. Moreover, the project level always takes precedence in terms of shadowing. Let’s see it in action by overriding the Footer component. Right now, our footer is defined in `@pehaa/gatsby-theme-wp-child/src/components/Footer.js`. We need to create the `src` folder and recreate the following files structure:

<pre><code class="language-bash">gatsby-wp-site
├── src
│   └── @pehaa
│       └── gatsby-theme-wp-child
│           └── components
│               └── Footer.js</code></pre>

With the above files structure, we are ready to provide a new version of the site footer. For example:

<div class="break-out">

<pre><code class="language-javascript">import React from "react"
import { useStaticQuery, graphql } from "gatsby"
import { Box } from "@chakra-ui/react"
const Footer = () =&gt; {
  const data = useStaticQuery(graphql`
    query {
      wp {
        generalSettings {
          title
        }
      }
    }
  `)
  return (
    &lt;Box
      as="footer"
      p="6"
      fontSize="sm"
      bg="gray.700"
      color="white"
      mt="auto"
      textAlign="center"
    &gt;
      &lt;b&gt;{data.wp.generalSettings.title}&lt;/b&gt; - Built with WordPress and GatsbyJS
    &lt;/Box&gt;
  )
}
export default Footer</code></pre>
</div>

Finally, let’s see how we can work with the CSS theme. With the code as below, properly located in `src/@chakra-ui/gatsby-plugin/theme.js` you can extend the default theme within the project. 

<pre><code class="language-javascript">// src/@chakra-ui/gatsby-plugin/theme.js
import { extendTheme } from "@chakra-ui/react"
const theme = {
  /* ... */
}
export default extendTheme(theme)</code></pre>

In most cases, this is not exactly what you need. The new CSS theme ignores the one from `gatsby-theme-wp-child`, whereas you’d instead want to extend the CSS theme set in the Gatsby child theme. The latter is possible since the `extendTheme` function allows you to pass multiple objects. To make it work, you have to import the CSS theme from `gatsby-theme-wp-child` and pass it as the second argument to the `extendTheme` function:

<div class="break-out">

<pre><code class="language-javascript">// src/@chakra-ui/gatsby-plugin/theme.js
import theme from "@pehaa/gatsby-theme-wp-child/src/@chakra-ui/gatsby-plugin/theme"
import { extendTheme } from "@chakra-ui/react"
const extendedTheme = {
  fonts: {
    body: "Rubik, sans-serif",
    heading: "Rubik, sans-serif",
  },
  /* ... */
}
export default extendTheme(extendedTheme, theme)</code></pre>
</div>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ceb1f24-9760-41b0-a9a3-62281f40dd4d/4-building-gatsby-themes-wordpress-powered-websites.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ceb1f24-9760-41b0-a9a3-62281f40dd4d/4-building-gatsby-themes-wordpress-powered-websites.jpg" width="800" height="" sizes="100vw" caption="Let’s add some shadowing. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ceb1f24-9760-41b0-a9a3-62281f40dd4d/4-building-gatsby-themes-wordpress-powered-websites.jpg'>Large preview</a>)" alt="An illustration with a screenshot from the site build within a computer screen." >}}

You can [see the site live here](https://gatsby-wp-theming-w-shadowing.netlify.app/), it’s deployed from the main branch of this [GitHub repo](https://github.com/pehaa/gatsby-wp-theming-demo).

## Wrapping Up

You’ve just seen Gatsby theming in action. With the theme approach, you can quickly set up multiple Gatsby sites with most of their code maintained within the theme packages. We’ve also seen how to separate parts of the project into packages and how to take advantage of shadowing.

In our example, we’ve followed the two-themes setup with a parent-child relationship between the themes. This may not always be an ideal choice.

Sometimes, you might want to go pretty far with the UI customization. In that case, you might consider loading and shadowing directly the parent theme instead of using the child one. In a real-world scenario, you would probably opt for a few child-level themes responsible for different, reusable parts of the UI (e.g. comments, forms or search).

### Further Reading On Smashing Magazine

- [Building An API With Gatsby Functions](https://www.smashingmagazine.com/2021/10/building-api-gatsby-functions/)
- [Gatsby Serverless Functions And The International Space Station](https://www.smashingmagazine.com/2021/07/gatsby-serverless-functions-international-space-station/)
- [Monetize Open-Source Software With Gatsby Functions And Stripe](https://www.smashingmagazine.com/2021/09/monetize-open-source-software-gatsby-functions-stripe/)
- [Smashing Podcast Episode 20 With Marcy Sutton: What Is Gatsby?](https://www.smashingmagazine.com/2020/07/smashing-podcast-episode-20/)

{{< signature "vf, yk, il" >}}

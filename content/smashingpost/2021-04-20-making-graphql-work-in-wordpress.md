---
title: 'Making GraphQL Work In WordPress'
slug: making-graphql-work-in-wordpress
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8867b72-5525-40a0-87f8-3fa0bde74337/making-graphql-work-in-wordpress.jpg
date: 2021-04-20T09:00:00.000Z
summary: >-
  Let’s explore the plugins providing GraphQL servers to WordPress. When should we use WPGraphQL, and when the GraphQL API for WordPress? Is there some advantage of one over the other, or some particular task that is easier to accomplish with one of them? In this article, we will find out.
description: >-
  Let’s explore the plugins providing GraphQL servers to WordPress. When should we use WPGraphQL, and when the GraphQL API for WordPress? Is there some advantage of one over the other, or some particular task that is easier to accomplish with one of them? In this article, we will find out.
categories:
  - API
  - Next.js
  - Tools
  - GraphQL
  - WordPress
---

Headless WordPress seems to be in vogue lately, with many new developments taking place in just the last few weeks. One of the reasons for the explosion in activity is the release of version 1.0 of [WPGraphQL](https://www.wpgraphql.com), a GraphQL server for WordPress.

WPGraphQL provides a GraphQL API: a way to fetch data from, and post data to, a WordPress website. It enables us to decouple the experience of managing our content, which is done via WordPress, from rendering the website, for which we can use the library of the framework of our choice ([React](https://www.smashingmagazine.com/category/react/), [Vue.js](https://www.smashingmagazine.com/category/vue/), [Gatsby](https://www.smashingmagazine.com/2020/09/advanced-graphql-usage-gatsby-websites/), [Next.js](https://www.smashingmagazine.com/category/next.js), or any other).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d792f19b-c6b4-4dd5-aa8f-78142cc2248b/1-graphql-wordpress-wpgraphal-graphql-api-wp.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d792f19b-c6b4-4dd5-aa8f-78142cc2248b/1-graphql-wordpress-wpgraphal-graphql-api-wp.jpg" width="800" height="379" sizes="100vw" caption="The GraphQL client in WPGraphQL. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d792f19b-c6b4-4dd5-aa8f-78142cc2248b/1-graphql-wordpress-wpgraphal-graphql-api-wp.jpg'>Large preview</a>)" alt="The GraphQL client in WPGraphQL" >}}

Until recently, WPGraphQL was the only GraphQL server for WordPress. But now another such plugin is available: [GraphQL API for WordPress](https://graphql-api.com), authored by me.

These two plugins serve the same purpose: to provide a GraphQL API to a WordPress website. You may be wondering: Why another plugin when there’s already WPGraphQL? Do these two plugins do the same thing? Or are they for different situations?

Let me say this first: WPGraphQL works great. I didn’t build my plugin because of any problem with it.

I built GraphQL API for WordPress because I had been working on an engine to **retrieve data efficiently**, which happened to be very suitable for GraphQL. So, then I said to myself, “Why not?”, and I built it. (And also a [couple of other reasons](https://leoloso.com/posts/why-i-built-graphql-api-when-there-was-wpgraphql/).)

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09c35cd8-2f34-4dfa-bc2b-729721f1fef1/2-graphql-wordpress-wpgraphal-graphql-api-wp.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09c35cd8-2f34-4dfa-bc2b-729721f1fef1/2-graphql-wordpress-wpgraphal-graphql-api-wp.jpg" width="800" height="497" sizes="100vw" caption="The GraphQL client in GraphQL API for WordPress. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09c35cd8-2f34-4dfa-bc2b-729721f1fef1/2-graphql-wordpress-wpgraphal-graphql-api-wp.jpg'>Large preview</a>)" alt="The GraphQL client in GraphQL API for WordPress" >}}

The two plugins have different architectures, giving them different characteristics, which make particular tasks easier to achieve with one plugin or the other.

In this article, I’ll describe, from my own point of view but as objectively as possible, when WPGraphQL is the way to go and when GraphQL API for WordPress is a better choice.

{{% feature-panel %}}

## Use WPGraphQL If: Using Gatsby

If you’re building a website using [Gatsby](https://www.gatsbyjs.com/), then there is only one choice: WPGraphQL.

The reason is that only WPGraphQL has the [Gatsby source plugin for WordPress](https://www.gatsbyjs.com/plugins/gatsby-source-wordpress/). In addition, WPGraphQL’s creator, Jason Bahl, was employed until recently by Gatsby, so we can fully trust that this plugin will suit Gatsby’s needs.

Gatsby receives all data from the WordPress website, and from then on, the logic of the application will be fully on Gatsby’s side, not on WordPress’. Hence, no additions to WPGraphQL (such as the potential additions of `@stream` or `@defer` directives) would make much of a difference.

WPGraphQL is already as good as Gatsby needs it to be.

## Use WPGraphQL If: Using One of the New Headless Frameworks

As I mentioned, lately there has been a flurry of activity in the WordPress headless space concerning several new frameworks and starter projects, all of them based on [Next.js](https://nextjs.org/):

- Colby Fayock created [Next.js WordPress Starter](https://github.com/colbyfayock/next-wordpress-starter).
- WebDevStudios launched its own [Next.js WordPress Starter](https://github.com/WebDevStudios/nextjs-wordpress-starter/).
- WP Engine created the [Headless WordPress Framework](https://github.com/wpengine/headless-framework), which [powers its service](https://wpengine.com/blog/wp-engine-launches-atlas-the-future-of-headless-wordpress/) to host and deploy headless WordPress websites.

If you need to use any of these new headless frameworks, then you will need to use WPGraphQL, because they have all been built on top of this plugin.

That’s a bit unfortunate: I’d really love for GraphQL API for WordPress to be able to power them too. But for that to happen, these frameworks would need to **operate with GraphQL via an interface**, so that we could swap GraphQL servers.

I’m somewhat hopeful that any of these frameworks will put such an interface into place. I [asked about it](https://github.com/wpengine/headless-framework/discussions/59) in the Headless WordPress Framework discussion board and was told that it might be considered. I also asked in WebDevStudios’ Next.js WordPress Starter discussion board, but alas, my question was immediately deleted, without a response. (Not encouraging, is it?)

So WPGraphQL it is then, currently and for the foreseeable future.

## Use Either (Or Neither) If: Using Frontity

[Frontity](https://frontity.org/) is a [React](https://reactjs.org/) framework for WordPress. It enables you to build a React-based application that is managed in the back end via WordPress. Even creating blog posts using the WordPress editor is supported out of the box.

Frontity manages the state of the application, without leaking how the data was obtained. Even though it is based on REST by default, you can also power it via GraphQL by [implementing the corresponding source plugin](https://community.frontity.org/t/some-questions-from-a-newcomer-to-frontity/3252/6).

This is how Frontity is smart: The source plugin is an interface to communicate with the data provider. Currently, the only available source plugin is the [one for the WordPress REST API](https://api.frontity.org/frontity-packages/features-packages/wp-source). But anyone can implement a source plugin for either WPGraphQL or GraphQL API for WordPress. (This is the approach that I wish the Next.js-based frameworks replicated.)

**Conclusion**: Neither WPGraphQL nor the GraphQL API offers any advantage over the other for working with Frontity, and they both require some initial effort to plug them in.

## Use WPGraphQL If: Creating a Static Site

In the first two sections, the conclusion was the same: Use WPGraphQL. But my response to this conclusion was different: While with Gatsby I had no regret, with Next.js I felt compelled to do something about it.

Why is that?

The difference is that, while Gatsby is purely a static site generator, Next.js can power both static and live websites.

I mentioned that WPGraphQL is already good enough for Gatsby. This statement can actually be broadened: **WPGraphQL is already good enough for any static site generator**. Once the static site generator gets the data from the WordPress website, it is pretty much settled with WordPress.

Even if GraphQL API for WordPress offers additional features, it will most likely not make a difference to the static site generator.

Hence, because WPGraphQL is already good enough, and it has completely mapped the GraphQL schema (which is still a work in progress for GraphQL API for WordPress), then WPGraphQL is the most suitable option, now and for the foreseeable future.

## Use GraphQL API If: Using GraphQL in a Live (i.e. Non-Static) Website

Now, the situation above changes if we want GraphQL to fetch data from a live website, such as when powering a mobile app or plotting real-time data on a website (for instance, to display analytics) or combining both the static and live approaches on the same website.

For instance, let’s say we have built a simple static blog using one of the Next.js frameworks, and we want to allow users to add comments to blog posts. How should this task be handled?

We have two options: **static** and **live** (or dynamic). If we opt for static, then comments will be rendered together with the rest of the website. Then, whenever a comment is added, we must trigger a webhook to regenerate and redeploy the website.

This approach has a few inconveniences. The **regeneration and redeployment process** could take a few minutes, during which the new comment will not be available. In addition, if the website receives many comments a day, the static approach will require more server processing time, which could become costly (some hosting companies charge based on server time).

In this situation, it would make sense to render the website statically without comments, and then retrieve the comments from a live site and render them dynamically in the client.

For this, [Next.js is recommended over Gatsby](https://blog.logrocket.com/next-js-vs-gatsbyjs-a-developers-perspective/). It can better handle the static and live approaches, including supporting different outputs for users with different capabilities.

Back to the GraphQL discussion: Why do I recommend GraphQL API for WordPress when dealing with live data? I do because the GraphQL server can have a direct impact on the application, mainly in terms of **speed and security**.

For a purely static website, the WordPress website can be kept private (it might even live on the developer’s laptop), so it’s safe. And the user will not be waiting for a response from the server, so speed is not necessarily of critical importance.

For a live site, though, the GraphQL API will be made public, so data safety becomes an issue. We must make sure that no malicious actors can access it. In addition, the user will be waiting for a response, so speed becomes a critical consideration.

In this respect, **GraphQL API for WordPress has a few advantages over WPGraphQL**.

WPGraphQL does implement security measures, such as [disabling introspection by default](https://www.wpgraphql.com/docs/security/#introspection-disabled-by-default). But GraphQL API for WordPress goes further, by disabling the single endpoint by default (along with [several other measures](https://graphql-api.com/features/#heading-multiple-layers-of-security)). This is possible because GraphQL API for WordPress offers [persisted queries](https://graphql-api.com/features/#heading-persisted-queries) natively.

As for speed, persisted queries also make the API faster, because the response can then be [cached via HTTP caching](https://graphql-api.com/features/#heading-http-caching) on several layers, including the client, content delivery network, and server.

These reasons make GraphQL API for WordPress better suited at handling live websites.

{{% ad-panel-leaderboard %}}

## Use GraphQL API If: Exposing Different Data for Different Users or Applications

WordPress is a versatile content management system, able to manage content for multiple applications and accessible to different types of users.

Depending on the context, we might need our GraphQL APIs to expose different data, such as:

- expose certain data to paid users but not to unpaid users,
- expose certain data to the mobile app but not to the website.

To expose different data, we need to provide **different versions of the GraphQL schema**.

WPGraphQL allows us to modify the schema (for instance, we can [remove a registered field](https://www.wpgraphql.com/functions/deregister_graphql_field/)). But the process is not straightforward: Schema modifications must be coded, and it’s not easy to understand who is accessing what and where (for instance, all schemas would still be available under the single endpoint, `/graphql`).

In contrast, GraphQL API for WordPress natively supports this use case: It offers [custom endpoints](https://graphql-api.com/features/#heading-custom-endpoints), which can expose different data for different contexts, such as:

- `/graphql/mobile-app` and `/graphql/website`,
- `/graphql/pro-users` and `/graphql/regular-users`.

Each custom endpoint is configured via [access control lists](https://graphql-api.com/features/#heading-access-control-lists), to provide granular user access field by field, as well as a [public and private API mode](https://graphql-api.com/features/#heading-publicprivate-api-mode) to determine whether the schema’s meta data is available to everyone or only to authorized users.

These features directly integrate with the WordPress editor (i.e. Gutenberg). So, creating the different schemas is done visually, similar to creating a blog post. This means that **everyone can produce custom GraphQL schemas**, not only developers.

GraphQL API for WordPress provides, I believe, a natural solution for this use case.

## Use GraphQL API If: Interacting With External Services

GraphQL is not merely an API for fetching and posting data. As important (though often neglected), it can also **process and alter the data** &mdash; for instance, by feeding it to some external service, such as sending text to a third-party API to fix grammar errors or uploading an image to a content delivery network.

Now, what’s the best way for GraphQL to communicate with external services? In my opinion, this is [best accomplished through directives](https://css-tricks.com/rendering-the-wordpress-philosophy-in-graphql/#directives-to-override-functionality), applied when either creating or retrieving the data (not unlike how WordPress filters operate).

I don’t know how well WPGraphQL interacts with external services, because its documentation doesn’t mention it, and the code base does not offer an example of any directive or document how to create one.

In contrast, GraphQL API for WordPress has **robust support for directives**. Every directive in a query is executed only once in total (as opposed to once per field and/or object). This capability enables very efficient communication with external APIs, and it integrates the GraphQL API within a cloud of services.

For instance, [this query](https://newapi.getpop.org/graphiql/?query=query%20%7B%0A%20%20posts%20%7B%0A%20%20%20%20title%20%40translate(from%3A%22en%22%2Cto%3A%22es%22)%0A%20%20%20%20excerpt%20%40translate(from%3A%22en%22%2Cto%3A%22es%22)%0A%20%20%7D%0A%7D) demonstrates a call to the Google Translate API via a `@translate` directive, to translate the titles and excerpts of many posts from English to Spanish. All fields for all posts are translated together, in a single call.

GraphQL API for WordPress is a natural choice for this use case.

**Note**: *As a matter of fact, the engine on which GraphQL API for WordPress is based, GraphQL by PoP, was specifically designed to provide advanced data-manipulation capabilities. That is one of its distinct characteristics. For an extreme example of what it can achieve, check out the guide on “[Sending a Localized Newsletter, User by User](https://graphql-by-pop.com/guides/localized-newsletter.html)”.*

## Use WPGraphQL If: You Want a Support Community

Jason Bahl has done a superb job of rallying a community around WPGraphQL. As a result, if you need to troubleshoot your GraphQL API, you’ll likely find someone who can help you out.

In my case, I’m still striving to create a community of users around GraphQL API for WordPress, and it’s certainly nowhere near that of WPGraphQL.

## Use GraphQL API If: You Like Innovation

I call GraphQL API for WordPress a “forward-looking” GraphQL server. The reason is that I often browse the list of [requests for the GraphQL specification](https://github.com/graphql/graphql-spec/issues/) and implement some of them well ahead of time (especially those that I feel some affinity for or that I can support with little effort).

As of today, GraphQL API for WordPress supports several innovative features (such as [multiple query execution](https://graphql-api.com/features/#heading-multiple-query-execution) and [schema namespacing](https://graphql-api.com/features/#heading-schema-namespacing)), offered as opt-in, and there are plans for a [few more](https://github.com/leoloso/PoP/labels/innovative).

## Use WPGraphQL If: You Need a Complete Schema

WPGraphQL has completely [mapped the WordPress data model](https://www.wpgraphql.com/docs/posts-and-pages/), including:

- posts and pages,
- custom post types,
- categories and tags,
- custom taxonomies,
- media,
- menus,
- settings,
- users,
- comments,
- plugins,
- themes,
- widgets.

GraphQL API for WordPress is [progressively mapping the data model](https://graphql-api.com/guides/query/posts/) with each new release. As of today, the list includes:

- posts and pages,
- custom post types,
- categories and tags,
- custom taxonomies,
- media,
- menus,
- settings,
- users,
- comments.

So, if you need to fetch data from a plugin, theme, or widget, currently only WPGraphQL does the job.

## Use WPGraphQL If: You Need Extensions

WPGraphQL [offers extensions for many plugins](https://www.wpgraphql.com/extensions), including Advanced Custom Fields, WooCommerce, Yoast, Gravity Forms.

GraphQL API for WordPress offers an extension for Events Manager, and it will keep adding more after the release of version 1.0 of the plugin.

## Use Either If: Creating Blocks for the WordPress Editor

Both WPGraphQL and GraphQL API for WordPress are currently working on integrating GraphQL with Gutenberg.

Jason Bahl has [described three approaches](https://www.wpgraphql.com/2021/03/09/gutenberg-and-decoupled-applications/) by which this integration can take place. However, because all of them have issues, he is advocating for the introduction of a server-side registry to WordPress, to enable identification of the different Gutenberg blocks for the GraphQL schema.

GraphQL API for WordPress also has an [approach for integrating with Gutenberg](https://graphql-api.com/blog/proposing-a-new-approach-for-gutenberg-and-decoupled-applications/), based on the “create once, publish everywhere” strategy. It **extracts block data from the stored content**, and it uses a single `Block` type to represent all blocks. This approach could avoid the need for the proposed server-side registry.

WPGraphQL’s solution can be considered tentative, because it will depend on the community accepting the use of a server-side registry, and we don’t know if or when that will happen.

For GraphQL API for WordPress, the solution will depend entirely on itself, and it’s indeed already a work in progress.

Because it has a higher chance of producing a working solution soon, I’d be inclined to recommend **GraphQL API for WordPress**. However, let’s wait for the solution to be fully implemented (in a few weeks, according to the plan) to make sure it works as intended, and then I will update my recommendation.

{{% ad-panel-leaderboard %}}

## Use GraphQL API If: Distributing Blocks Via a Plugin

I came to a realization: Not many plugins (if any) seem to be using GraphQL in WordPress.

Don’t get me wrong: WPGraphQL has surpassed 10,000 installations. But I believe that those are mostly installations to power Gatsby (in order to run Gatsby) or to power Next.js (in order to run one of the headless frameworks).

Similarly, WPGraphQL has many extensions, as I described earlier. But those extensions are just that: extensions. They are not standalone plugins.

For instance, the WPGraphQL for WooCommerce extension depends on both the WPGraphQL and WooCommerce plugins. If either of them is not installed, then the extension will not work, and that’s OK. But WooCommerce doesn’t have the choice of relying on WPGraphQL in order to work; hence, there will be no GraphQL in the WooCommerce plugin.

My understanding is that there are no plugins that use GraphQL in order to run functionality for WordPress itself or, specifically, to power their Gutenberg blocks.

The reason is simple: Neither WPGraphQL nor GraphQL API for WordPress are part of WordPress’ core. Thus, it is not possible to rely on GraphQL in the way that plugins can rely on WordPress’ REST API. As a result, plugins that implement Gutenberg blocks may only use REST to fetch data for their blocks, not GraphQL.

Seemingly, the solution is to wait for a GraphQL solution (most likely WPGraphQL) to be added to WordPress core. But who knows how long that will take? Six months? A year? Two years? Longer?

We know that WPGraphQL is being considered for WordPress’ core because Matt Mullenweg has hinted at it. But so many things must happen before then: bumping the minimum PHP version to 7.1 (required by both WPGraphQL and GraphQL API for WordPress), as well as having a clear decoupling, understanding, and roadmap for what functionality will GraphQL power.

(Full site editing, currently under development, is based on REST. What about the next major feature, multilingual blocks, to be addressed in Gutenberg’s phase 4? If not that, then which feature will it be?)

Having explained the problem, **let’s consider a potential solution** &mdash; one that doesn’t need to wait!

A few days ago, I had another realization: From GraphQL API for WordPress’ code base, I can produce a smaller version, containing only the GraphQL engine and nothing else (no UI, no custom endpoints, no HTTP caching, no access control, no nothing). And this version can be distributed as a Composer dependency, so that plugins can install it to power their own blocks.

The key to this approach is that this component must be of specific use to the plugin, not to be shared with anybody else. Otherwise, two plugins both referencing this component might modify the schema in such a way that they override each other.

Luckily, I recently [solved scoping GraphQL API for WordPress](https://graphql-api.com/blog/graphql-api-for-wp-is-now-scoped-thanks-to-php-scoper/). So, I know that I’m able to fully scope it, producing a version that will not conflict with any other code on the website.

That means that it will work for any **combination of events**:

- If the plugin containing the component is the only one using it;
- If GraphQL API for WordPress is also installed on the same website;
- If another plugin that also embeds this component is installed on the website;
- If two plugins that embed the component refer to the same version of the component or to different ones.

In each situation, the plugin will have its own self-contained, private GraphQL engine that it can fully rely on to power its Gutenberg blocks (and we need not fear any conflict).

This component, to be called the **Private GraphQL API**, should be ready in a few weeks. (I have already [started working on it](https://github.com/leoloso/PoP/issues/519).)

Hence, my recommendation is that, if you want to use GraphQL to power Gutenberg blocks in your plugin, please wait a few weeks, and then check out GraphQL API for WordPress’ younger sibling, the Private GraphQL API.

## Conclusion

Even though I do have skin in the game, I think I’ve managed to write an article that is mostly objective.

I have been honest in stating why and when you need to use WPGraphQL. Similarly, I have been honest in explaining why GraphQL API for WordPress appears to be better than WPGraphQL for several use cases.

In general terms, we can summarize as follows:

- Go static with WPGraphQL, or go live with GraphQL API for WordPress.
- Play it safe with WPGraphQL, or invest (for a potentially worthy payoff) in GraphQL API for WordPress.

On a final note, I wish the Next.js frameworks were re-architected to follow the same approach used by Frontity: where they can access an interface to fetch the data that they need, instead of using a direct implementation of some particular solution (the current one being WPGraphQL). If that happened, developers could choose **which underlying server to use** (whether WPGraphQL, GraphQL API for WordPress, or some other solution introduced in the future), based on their needs &mdash; from project to project.

### Useful Links

- WPGraphQL: [documentation](https://www.wpgraphql.com/docs/quick-start/), [download page](https://wordpress.org/plugins/wp-graphql/), [code repository](https://github.com/wp-graphql/wp-graphql/)
- GraphQL API for WordPress: [documentation](https://graphql-api.com/guides), [download page](https://graphql-api.com/download), [code repository](https://github.com/leoloso/PoP)
- “[The Gatsby WordPress Integration Workshop](https://www.youtube.com/watch?v=JqF_y5RQbF8&list=TLGGnLwd9hrB9LAyNTAzMjAyMQ)”  
YouTube video with demo of WPGraphQL
- “[Intro to GraphQL API for WordPress](https://www.youtube.com/watch?v=LnyNyT2RwwI)”  
YouTube video with demo of GraphQL API for WordPress

{{< signature "vf, yk, il, al" >}}

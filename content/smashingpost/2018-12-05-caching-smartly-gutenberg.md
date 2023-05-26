---
title: 'Caching Smartly In The Age Of Gutenberg'
slug: caching-smartly-gutenberg
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/065e29f2-a665-4cc0-bde2-c58a7ae2b10e/layout-components-800w.jpg
date: 2018-12-05T13:00:15+01:00
summary: >-
  When optimizing the speed of our websites from the server side, caching ranks among the most critical tasks to get just right. In this article, Leonardo Losoviz examines an architecture based on self-rendering components and SSR, and analyzes how to implement it for WordPress sites through Gutenberg.
description: >-
  When optimizing the speed of our websites from the server side, caching ranks among the most critical tasks to get just right. In this article, Leonardo Losoviz examines an architecture based on self-rendering components and SSR, and analyzes how to implement it for WordPress sites through Gutenberg.
categories:
  - WordPress
  - HTML
  - Plugins
---
Caching is needed for speeding up a site: instead of having the server dynamically create the HTML output for each request, it can create the HTML only after it is requested the first time, cache it, and serve the cached version from then on. [Caching delivers a faster response](https://hackernoon.com/why-do-we-cache-b24920e1e903), and frees up resources in the server. When optimizing the speed of our sites from the server side, caching ranks among the most critical tasks to get right.

When generating the HTML output for the page, if it contains code with user state, such as printing a welcome message "Hello {{User name}}!" for the logged in user, then the page cannot be cached. Otherwise, if Peter visits the site first, and the HTML output is cached, all users would then be welcomed with "Hello Peter!"

Hence, caching plugins, such as those [available for WordPress](https://wordpress.org/plugins/search/cache/), will generally offer to disable caching when the user is logged in, as shown below for plugin [WP Super Cache](https://wordpress.org/plugins/wp-super-cache/):

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56eb8bb5-d45e-4d28-8a94-e70a41bc120a/wp-super-cache-disable-caching.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56eb8bb5-d45e-4d28-8a94-e70a41bc120a/wp-super-cache-disable-caching.jpg" sizes="100vw" caption="WP Super Cache recommends to disable caching for logged in users. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56eb8bb5-d45e-4d28-8a94-e70a41bc120a/wp-super-cache-disable-caching.jpg'>Large preview</a>)" alt="Disabled caching for known users in WP Super Cache" >}}

Disabling caching for logged in users is undesirable and should be avoided, because even if the amount of HTML code with user state is minimal compared to the static content in the page, still nothing will be cached. The reason is that the entity to be cached is the page, and not the particular pieces of HTML code within the page, so by including a single line of code which cannot be cached, then nothing will be cached. It is an all-or-nothing situation.

{{% feature-panel %}}

To address this, we can architect our application to avoid rendering HTML code with user state on the server-side, and render it on the client-side only, after fetching its required data through an API (often based on REST or GraphQL). By removing user state from code rendered on the server, that page can then be cached, even if the user is logged in.

In this article, we will explore the following issues: 

- How do we identify those sections of code that require user state, isolate them from the page, and make them be rendered on the client-side only? 
- How can it be implemented for WordPress sites through Gutenberg?

## Gutenberg Is Bringing Components To WordPress

As I explained in my previous article [Implications of thinking in blocks instead of blobs](https://www.smashingmagazine.com/2018/11/implications-blocks-blobs/), [Gutenberg](https://wordpress.org/gutenberg/) is a JavaScript-based editor for WordPress (more specifically, it is a React-based editor, encapsulating the React libraries behind the global `wp` object), slated for release in either November 2018 or January 2019. Through its drag-and-drop interface, Gutenberg will utterly transform the experience of creating content for WordPress and, at some later stage in the future, the process of building sites, switching from the current creation of a page through templates (header.php, index.php, sidebar.php, footer.php), and the content of the page through a single blob of HTML code, to creating [components](https://reactjs.org/docs/components-and-props.html) to be placed anywhere on the page, which can control their own logic, load their own data, and self-render. 

To appreciate the upcoming change visually, WordPress is moving from this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7c5ed1a-80fb-4b21-971a-1505c1ce0448/layout-templates.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7c5ed1a-80fb-4b21-971a-1505c1ce0448/layout-templates.jpg" sizes="100vw" caption="Currently pages are built through PHP templates. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7c5ed1a-80fb-4b21-971a-1505c1ce0448/layout-templates.jpg'>Large preview</a>)" alt="The page contains templates with HTML code" >}}

To this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f26b7361-7601-46b3-b75b-7ba0663b896a/layout-components.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f26b7361-7601-46b3-b75b-7ba0663b896a/layout-components.jpg" sizes="100vw" caption="In the near future, pages will be built by placing self-rendering components in them. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f26b7361-7601-46b3-b75b-7ba0663b896a/layout-components.jpg'>Large preview</a>)" alt="The page contains autonomous components" >}}

Even though Gutenberg as a site builder is not ready yet, we can already think in terms of components when designing the architecture of our site. As for the topic of this article, architecting our application using components as the unit for building the page can help implement an enhanced caching strategy, as we shall see below.

{{% ad-panel-leaderboard %}}

## Evaluating The Relationship Between Pages And Components

As mentioned earlier, the entity being cached is the page. Hence, we need to evaluate how components will be placed on the page as to maximize the page’s cacheability. Based on their dependence on user state, we can broadly categorize pages into the following 3 groups:

1. Pages without any user state, such as "Who we are" page.
2. Pages with bits and pieces of user state, such as the homepage when welcoming the user ("Welcome Peter!"), or an archive page with a list of posts, showing a "Like" button under each post which is painted blue if the logged in user has liked that post.
3. Pages naturally with user state, in which content depends directly from the logged in user, such as "My posts" of "Edit my profile" pages.

Components, on the other side, can simply be categorized as requiring user state or not. Because the architecture considers the component as the unit for building the page, the component has the faculty of knowing if it requires user state or not. Hence, a `<WelcomeUser />` component, which renders "Welcome Peter!", knows it requires user state, while a `<WhoWeAre />` component knows that it does not.

Next, we need to place components on the page, and depending on the combination of page and component requiring user state or not, we can establish a proper strategy for caching the page and for rendering content to the user as soon as possible. We have the following cases:

### 1. Pages Without Any User State

These can be cached with no issues.

- Page is cached => It can’t access user state.
- Components, none of them requiring user state, are rendered in the server.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f16fdf93-9804-4988-9349-bceedf8371d0/page-without-user-state.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f16fdf93-9804-4988-9349-bceedf8371d0/page-without-user-state.jpg" sizes="100vw" caption="A page without user state can only contain components without user state. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f16fdf93-9804-4988-9349-bceedf8371d0/page-without-user-state.jpg'>Large preview</a>)" alt="Page without user state" >}}

### 2. Pages With Bits And Pieces Of User State

We could make the page either require user state or not. If we make the page require user state, then it cannot be cached, which is a wasted opportunity when most of the content in the page is static. Hence, we'd rather make the page not require user state, and those components requiring user state which are placed on the page, such as `<WelcomeUser />` on the homepage, are made lazy-load: the server-side renders an empty shell, and the component is rendered instead in the client-side, after getting its data from an API. 

{{% ad-panel-leaderboard %}}

Following this approach, all static content in the page will be rendered immediately through server-side rendering (SSR), and those bits and pieces with user state after some delay through client-side rendering (CSR).

- Page is cached => It can’t access user state.
- Components not requiring user state are rendered in the server.
- Components requiring user state are rendered in the client.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/287efe50-e776-4522-9d07-1d8fe51efdab/page-with-bits-of-user-state.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/287efe50-e776-4522-9d07-1d8fe51efdab/page-with-bits-of-user-state.jpg" sizes="100vw" caption="A page with bits of user state contains CSR components with user state, and SSR components without user state. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/287efe50-e776-4522-9d07-1d8fe51efdab/page-with-bits-of-user-state.jpg'>Large preview</a>)" alt="Page with bits of user state" >}}

### 3. Pages Naturally With User State

If the library or framework only enables client-side rendering, then we must follow the same approach as with #2: do not make the page require user state, and add a component, such as `<MyPosts />`, to self-render in the client. 

However, since the main objective of the page is to show user content, making the user wait for this content to be loaded on a 2nd stage is not ideal. Let’s see this with an example: a user who has not logged in yet accesses page "Edit my profile". If the site renders the content in the server, since the user is not logged in the server will immediately redirect to the login page. Instead, if the content is rendered in the client through an API, the user will first be presented a loading message, and only after the response from the API is back will the user be redirected to the login page, making the experience slower.

Hence, we are better off using a library or framework that supports server-side rendering, and we make the page require user state (making it non-cacheable):

- Page is not cached => It can access user state.
- Components, both requiring and not requiring user state, are rendered in the server.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d06cbe04-cc85-4e01-8549-f228e13aee1e/page-with-user-state.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d06cbe04-cc85-4e01-8549-f228e13aee1e/page-with-user-state.jpg" sizes="100vw" caption="A page with user state contains SSR components both with and without user state. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d06cbe04-cc85-4e01-8549-f228e13aee1e/page-with-user-state.jpg'>Large preview</a>)" alt="Page with user state" >}}

From this strategy and all the combinations it produces, deciding if a component must be rendered server or client-side simply boils down to the following pseudo-code:

<div class="break-out">

<pre><code class="language-javascript">if (component requires user state and page can’t access user state) {
    render component in client
}
else {
    render component in server
}
</code></pre></div>

This strategy allows to attain our objective: implemented for all pages in the site, for all components placed in each page, and configuring the site to not cache pages which access the user state, we can then avoid disabling caching any page whenever the user is logged in.

## Rendering Components Client/Server-Side Through Gutenberg

In Gutenberg, those components which can be embedded on the page are called "blocks" (or also Gutenblocks). Gutenberg supports two types of blocks, static and dynamic:

- **Static blocks** produce their HTML code already in the client (when the user is interacting with the editor) and [save it inside the post content](https://wordpress.org/gutenberg/handbook/block-api/block-edit-save/). Hence, they are client-side JavaScript-based blocks. 
- **[Dynamic blocks](https://wordpress.org/gutenberg/handbook/blocks/creating-dynamic-blocks/)**, on the other hand, are those which can change their content dynamically, such as a latest posts block, so they cannot save the HTML output inside the post content. Hence, in addition to creating their HTML code on the client-side, they must also produce it from the server on runtime through a PHP function (which is defined under parameter `render_callback` when registering the block in the backend through function `register_block_type`.)

Because HTML code with user state cannot be saved in the post’s content, a block dealing with user state will necessarily be a dynamic block. In summary, through dynamic blocks we can produce the HTML for a component both in the server and client-side, enabling to implement our optimized caching strategy. The previous pseudo-code, when using Gutenberg, will look like this:

<div class="break-out">

<pre><code class="language-javascript">if (block requires user state and page can’t access user state) {
    render block in client through JavaScript
}
else {
    render (dynamic) block in server through PHP code
}
</code></pre></div>

Unfortunately, implementing the dual client/server-side functionality doesn’t come without hardship: Gutenberg’s SSR is not isomorphic, ie it does not allow a single codebase to produce the output for both client and server-side code. Hence, developers would need to maintain 2 codebases, one in PHP and one in JavaScript, which is far from optimal. 

Gutenberg also implements a `<ServerSideRender />` component, however it advices against using it: this component was not thought for improving the speed of the site and rendering an immediate response to the user, but for providing compatibility with legacy code, such as shortcodes.

As it is explained in the [documentation](https://github.com/WordPress/gutenberg/tree/master/packages/components/src/server-side-render):

<blockquote>“ServerSideRender should be regarded as a fallback or legacy mechanism, it is not appropriate for developing new features against.<br /><br />“New blocks should be built in conjunction with any necessary REST API endpoints, so that JavaScript can be used for rendering client-side in the edit function. This gives the best user experience, instead of relying on using the PHP render_callback. The logic necessary for rendering should be included in the endpoint, so that both the client-side JavaScript and server-side PHP logic should require a minimal amount of differences.”</blockquote>

As a result, when building our sites, we will need to decide if to implement SSR, which boosts the site’s speed by enabling an optimal caching experience and by providing an immediate response to the user when loading the page, but which comes at the cost of maintaining 2 codebases. Depending on the context, it may be worth it or not.

## Configuring What Pages Require User State

Pages requiring (or accessing) user state will be made non-cacheable, while all other pages will be cacheable. Hence, we need to identify which pages require user state. Please notice that this applies only to pages, and not to REST endpoints, since the goal is to render the component already in the server when accessing the page, and calling the WP REST API’s endpoints implies getting the data for rendering the component in the client. Hence, from the perspective our our caching strategy, we can assume all REST endpoints will require user state, and so they don’t need to be cached.

To identifying which pages require user state, we simply create a function `get_pages_with_user_state`, like this:

<pre><code class="language-javascript">function get_pages_with_user_state() {

    return apply_filters(
        'get_pages_with_user_state',
        array()
    );
}
</code></pre>

Upon which we implement hooks with the corresponding pages, like this:

<div class="break-out">

<pre><code class="language-javascript">// ID of the pages, retrieved from the WordPress admin
define ('MYPOSTS_PAGEID', 5);
define ('ADDPOST_PAGEID', 8);

add_filter('get_pages_with_user_state', 'get_pages_with_user_state_impl');
function get_pages_with_user_state_impl($pages) {

  $pages[] = MYPOSTS_PAGEID;

  // "Add Post" may not require user state!
  // $pages[] = ADDPOST_PAGEID;

  return $pages;
}
</code></pre></div>

Please notice how we may not need to add user state for page "Add Post" (making this page cacheable), even though this page requires to validate that the user is logged in when submitting a form to create content on the site. This is because the "Add Post" page may simply display an empty form, requiring no user state whatsoever. Then, submitting the form will be a POST operation, which cannot be cached in any case (only GET requests are cached).

## Disabling Caching Of Pages With User State In WP Super Cache

Finally, we configure our application to disable caching for those pages which require user state (and cache everything else.) We will do this for plugin WP Super Cache, by blacklisting the URIs of those pages in the plugin settings page:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b7fd93b-8aaa-4bed-8c63-f4d0803c569b/wp-super-cache-rejected-strings.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b7fd93b-8aaa-4bed-8c63-f4d0803c569b/wp-super-cache-rejected-strings.jpg" sizes="100vw" caption="We can disable caching URLs containing specific strings in WP Super Cache. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b7fd93b-8aaa-4bed-8c63-f4d0803c569b/wp-super-cache-rejected-strings.jpg'>Large preview</a>)" alt="WP Super Cache settings to disable caching for blacklisted strings" >}}

What we need to do is create a script that obtains the paths for all pages with user state, and saves it in the corresponding input field. This script can then be invoked manually, or automatically as part of the application’s deployment process.

First we obtain all the URIs for the pages with user state:

<div class="break-out">

<pre><code class="language-javascript">function get_rejected_strings() {

  $rejected_strings = array();
  $pages_with_user_state = get_pages_with_user_state();
  foreach ($pages_with_user_state as $page) {

      // Calculate the URI for that page to the list of rejected strings
      $path = substr(get_permalink($page), strlen(home_url()));
      $rejected_strings[] = $path;
  }

  return $rejected_strings;
}
</code></pre></div>

And then, we must add the rejected strings into WP Super Cache’s configuration file, located in wp-content/wp-cache-config.php, updating the value of entry `$cache_rejected_uri` with our list of paths:

<div class="break-out">

<pre><code class="language-javascript">function set_rejected_strings_in_wp_super_cache() {

  if ($rejected_strings = get_rejected_strings()) {

    // Keep the original values in
    $rejected_strings = array_merge(
      array('wp-.*\\\\.php', 'index\\\\.php'),
      $rejected_strings
    );

    global $wp_cache_config_file;
    $cache_rejected_uri = "array('".implode("', '", $rejected_strings)."')";
    wp_cache_replace_line('^ *\$cache_rejected_uri', "\$cache_rejected_uri = " . $cache_rejected_uri . ";", $wp_cache_config_file);
  }
}
</code></pre></div>

Upon execution of function `set_rejected_strings_in_wp_super_cache`, the settings will be updated with the new rejected strings:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffec60a2-033d-4da7-8c6d-f853c9ac852b/wp-super-cache-rejected-strings-from-script.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffec60a2-033d-4da7-8c6d-f853c9ac852b/wp-super-cache-rejected-strings-from-script.jpg" sizes="100vw" caption="Blacklisting the paths from pages accessing user state in WP Super Cache. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffec60a2-033d-4da7-8c6d-f853c9ac852b/wp-super-cache-rejected-strings-from-script.jpg'>Large preview</a>)" alt="WP Super Cache settings to disable caching blacklisted strings" >}}

Finally, because we are now able to disable caching for the specific pages that require user state, there is no need to disable caching for logged in users anymore:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92e239be-59ce-4978-aa03-605c1b36d627/wp-super-cache-settings.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92e239be-59ce-4978-aa03-605c1b36d627/wp-super-cache-settings.jpg" sizes="100vw" caption="No need to disable caching for logged in users anymore! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92e239be-59ce-4978-aa03-605c1b36d627/wp-super-cache-settings.jpg'>Large preview</a>)" alt="Disabled caching for known users in WP Super Cache" >}}

That’s it! 

## Conclusion

In this article, we explored a way to enhance our site’s caching &mdash; mainly aimed at enabling caching on the site even when the users are logged in. The strategy relies on disabling caching only for those pages which require user state, and on using components which can decide if to be rendered on the client or on the server-side, depending on the page accessing the user state or not. 

As a general concept, the strategy can be implemented on any architecture that supports server-side rendering of components. In particular, we analyzed how it can be implemented for WordPress sites through Gutenberg, advising to assess if it is worth the trouble of maintaining two codebases, one in PHP for the server-side code, and one in JavaScript for the client-side code. 

Finally, we explained that the solution can be integrated into the caching plugin through a custom script to automatically produce the list of pages to avoid caching, and produced the code for plugin WP Super Cache.

After implementing this strategy to my site, it doesn’t matter anymore if visitors are logged in or not. They will always access a cached version of the homepage, providing a faster response and a better user experience.

{{< signature "rb, ra, yk, il" >}}

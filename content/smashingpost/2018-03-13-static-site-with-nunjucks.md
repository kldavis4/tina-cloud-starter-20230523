---
title: 'Building A Static Site With Components Using Nunjucks'
slug: static-site-with-nunjucks
author: chris-coyier
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2990832-ae6d-4aab-9603-561a8c623003/static-site-nunjucks-image1.jpg
date: 2018-03-13T11:00:01+01:00
summary: >-
  Even if you don’t use any client-side JavaScript at all to build a site, it doesn’t mean you have to give up on the idea of building with components. Learn how to build a static site with the help of an HTML preprocessor.
description: >-
  Even if you don’t use any client-side JavaScript at all to build a site, it doesn’t mean you have to give up on the idea of building with components. Learn how to build a static site with the help of an HTML preprocessor.
categories:
  - Static Generators
  - Generators
  - Tools
  - CSS
  - JavaScript
---
It’s quite popular these days, and dare I say a damn fine idea, to build sites with components. Rather than building out entire pages one by one, we build a system of components (think: a search form, an article card, a menu, a footer) and then piece together the site with those components. 

JavaScript frameworks like React and Vue emphasize this idea heavily. But even if you don’t use any client-side JavaScript at all to build a site, it doesn’t mean you have to give up on the idea of building with components! By using an HTML preprocessor, we can build a static site and still get all the benefits of abstracting our site and its content into re-usable components.

Static sites are all the rage these days, and rightfully so, as they are fast, secure, and inexpensive to host. Even Smashing Magazine [is a static site](https://www.smashingmagazine.com/smashing-tv/smashing-case-study/), believe it or not! 

Let’s take a walk through a site I built recently using this technique. I used [CodePen Projects](https://codepen.io/pro/projects) to build it, which offers [Nunjucks](https://mozilla.github.io/nunjucks/) as a preprocessor, which was perfectly up for the job.

## A Four-Page Site With A Consistent Header, Navigation, And Footer

[This is a microsite](https://thepowerofserverless.info/). It doesn’t need a full-blown CMS to handle hundreds of pages. It doesn’t need JavaScript to handle interactivity. But it does need a handful of pages that all share the same layout. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2990832-ae6d-4aab-9603-561a8c623003/static-site-nunjucks-image1.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2990832-ae6d-4aab-9603-561a8c623003/static-site-nunjucks-image1.jpg" sizes="100vw" caption="Consistent header and footer across all pages" alt="Consistent header and footer" >}}

{{% feature-panel %}}

HTML alone doesn’t have a good solution for this. What we need are *imports*. Languages like PHP make this simple with things like `<?php include "header.php"; ?>`, but static file hosts don’t run PHP (on purpose) and HTML alone is no help. Fortunately, we can preprocess includes with Nunjucks.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54d6ea31-54a0-422c-9cba-d71995bfc733/static-site-nunjucks-image2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54d6ea31-54a0-422c-9cba-d71995bfc733/static-site-nunjucks-image2.png" sizes="100vw" caption="Importing components is possible in languages like PHP" alt="Importing components into pages" >}}

It makes perfect sense here to create a *layout*, including chunks of HTML representing the header, navigation, and footer. Nunjucks templating has the concept of blocks, which allow us to slot in content into that spot when we use the layout.

<div class="break-out">

<pre><code class="language-html">&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
  &lt;title&gt;The Power of Serverless&lt;/title&gt;
  &lt;link rel="stylesheet" href="/styles/style.processed.css"&gt;
&lt;/head&gt;

&lt;body&gt;

  {% include "./template-parts/_header.njk" %}

  {% include "./template-parts/_nav.njk" %}

  {% block content %}
  {% endblock %}

  {% include "./template-parts/_footer.njk" %}

&lt;/body&gt;
</code></pre></div>

Notice the files that are included are named like `_file.njk`. That’s not entirely necessary. It could be `header.html` or `icons.svg`, but they are named like this because 1) files that start with underscores are a bit of-of a standard way of saying they are a partial. In CodePen Projects, it means they won’t try to be compiled alone. 2) By naming it `.njk`, we could use more Nunjucks stuff in there if we want to.

None of these bits have anything special in them at all. They are just little bits of HTML intended to be used on each of our four pages.

<div class="break-out">

<pre><code class="language-html">&lt;footer&gt;
  &lt;p&gt;Just a no-surprises footer, people. Nothing to see here.&lt;p&gt;
&lt;/footer&gt;
</code></pre></div>

Done this way, we can make one change and have the change reflected on all four pages.

## Using The Layout For The Four Pages

Now each of our four pages can be a file. Let’s just start with `index.njk` though, which in CodePen Projects, will automatically be processed and create an `index.html` file every time you save.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b94ae297-5040-4739-b27e-33a09c180758/static-site-nunjucks-image3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b94ae297-5040-4739-b27e-33a09c180758/static-site-nunjucks-image3.png" sizes="100vw" caption="Starting off with an index.njk file" alt="The index.njk file" >}}

Here’s what we could put in `index.njk` to use the layout and drop some content in that block:

<pre><code class="language-css">{% extends "_layout.njk" %}

{% block content %}
&lt;h1&gt;Hello, World!&lt;/h1&gt;
{% endblock %} 
</code></pre>

That will buy us a fully functional home page! Nice! Each of the four pages can do the same exact thing, but putting different content in the block, and we have ourselves a little four-page site that is easy to manage.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19c10690-1672-47cb-ac34-99abd88cf7d3/static-site-nunjucks-image4.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19c10690-1672-47cb-ac34-99abd88cf7d3/static-site-nunjucks-image4.png" sizes="100vw" caption="The index.njk file gets compiled into index.html" alt="Compiled index.html" >}}

For the record, I’m not sure I’d call these little chunks we re-using *components*. We’re just being efficient and breaking up a layout into chunks. I think of a component more like a re-usable chunk that accepts data and outputs a unique version of itself with that data. We’ll get to that.

## Making Active Navigation

Now that we’ve repeated an identical chunk of HTML on four pages, is it possible to apply unique CSS to individual navigation items to identify the current page? We could with JavaScript and looking at `window.location` and such, but we can do this without JavaScript. The trick is putting a `class` on the `<body>` unique to each page and using that in the CSS.

In our `_layout.njk` we have the body output a class name as a variable:

<pre><code class="language-css">&lt;body class="{{ body_class }}"&gt;
</code></pre>

Then before we call that layout on an indivdiual page, we set that variable:

<pre><code class="language-css">{% set body_class = "home" %}
{% extends "_layout.njk" %}
</code></pre>

Let’s say our navigation was structured like

<pre><code class="language-css">&lt;nav class="site-nav"&gt;
  &lt;ul&gt;
    &lt;li class="nav-home"&gt;
      &lt;a href="/"&gt;
        Home
      &lt;/a&gt;
      ...
</code></pre>

Now we can target that link and apply special styling as needed by doing:

<div class="break-out">

<pre><code class="language-css">body.home .nav-home a,
body.services .nav-services a { /* continue matching classes for all pages... */
  /* unique active state styling */
}
</code></pre></div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16c75ae8-69e5-4f61-89ba-c752b458d0ed/static-site-nunjucks-image5.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16c75ae8-69e5-4f61-89ba-c752b458d0ed/static-site-nunjucks-image5.gif" alt="Active state styling on navigation" /></a><figcaption>Styling navigation links with an active class.</figcaption></figure>

*Oh and those icons?* Those are just individual `.svg` files I put in a folder and included like

<pre><code class="language-css">{% include "../icons/cloud.svg" %}
</code></pre>

And that allows me to style them like:

<pre><code class="language-css">svg {
  fill: white;
}
</code></pre>

Assuming the SVG elements inside have no `fill` attributes already on them.

## Authoring Content In Markdown

The homepage of my microsite has a big chunk of content on it. I could certainly write and maintain that in HTML itself, but sometimes it’s [nice to leave that type of thing to Markdown](https://mediatemple.net/blog/tips/you-should-probably-blog-in-markdown/). Markdown feels cleaner to write and perhaps a bit easier to look at when it’s lots of copy.

This is very easy in CodePen Projects. I made a file that ends in `.md`, which will automatically be processed into HTML, then included that in the `index.njk` file.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f1b35c3-a4d2-49bd-839d-9f7ab023c704/static-site-nunjucks-image6.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f1b35c3-a4d2-49bd-839d-9f7ab023c704/static-site-nunjucks-image6.gif" alt="Markdown compiled into HTML on CodePen Projects" /></a><figcaption>Files in markdown get compiled into HTML on CodePen Projects.</figcaption></figure>

<pre><code class="language-css">{% block content %}
&lt;main class="centered-text-column"&gt; 
{% include "content/about.html" %} 
&lt;/main&gt;
{% endblock %}
</code></pre>

## Building Actual Components

Let’s consider components to be repeatable modules that as passed in data to create themselves. In frameworks like Vue, you’d be working with [single file components](https://vuejs.org/v2/guide/single-file-components.html) that are isolated bits of templated HTML, scoped CSS, and component-specific JavaScript. That’s super cool, but our microsite doesn’t need anything that fancy. 

We need to create some “cards” based on a simple template, so we can build things like this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f883321-3601-433b-ae3a-e4b83bde12b2/static-site-nunjucks-image7.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f883321-3601-433b-ae3a-e4b83bde12b2/static-site-nunjucks-image7.png" sizes="100vw" caption="Creating repeatable components with templates" alt="Card style components" >}}

Building a repeatable component like that in Nunjucks involves using what they call [Macros](https://mozilla.github.io/nunjucks/templating.html). Macros are deliciously simple. They are like **as if HTML had functions**!

<pre><code class="language-css">{% macro card(title, content) %}
&lt;div class="card"&gt;
  &lt;h2&gt;{{ title }}&lt;/h2&gt;
  &lt;p&gt;{{ content }}&lt;/p&gt;
&lt;/div&gt;
{% endmacro %}
</code></pre>

Then you call it as needed:

<pre><code class="language-css">{{ card('My Module', 'Lorem ipsum whatever.') }}
</code></pre>

The whole idea here is to **separate data and markup**. This gives us some pretty clear, and tangible benefits:

1. If we need to make a change to the HTML, we can change it in the macro and it gets changed everywhere that uses that macro.
2. The data isn’t tangled up in markup
3. The data could come from anywhere! We code the data right into calls to the macros as we’ve done above. Or we could reference some JSON data and loop over it. I’m sure you could even imagine a setup in which that JSON data comes from a sort of headless CMS, build process, serverless function, cron job, or whatever.

Now we have these repeatable cards that combine data and markup, just what we need:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c6b34c1-97bb-4951-939f-f18b9c904415/static-site-nunjucks-image8.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c6b34c1-97bb-4951-939f-f18b9c904415/static-site-nunjucks-image8.png" sizes="100vw" caption="HTML is controlled in the macro, while data can come from anywhere" alt="Data and markup for the component is kept separate" >}}

## Make As Many Components As You Like

You can take this idea and run with it. For example, imagine how Bootstrap is essentially a bunch of CSS that you follow HTML patterns in which to use. You could make each of those patterns a macro and call them as needed, essentially [componentizing the framework](https://css-tricks.com/componentizing-a-framework/). 

You can nest components if you like, embracing a sort of [atomic design](https://bradfrost.com/blog/post/atomic-web-design/) philosophy. Nunjucks offers logic as well, meaning you can create conditional components and variations just by passing in different data.

[In the simple site I made](https://thepowerofserverless.info/), I made a different macro for the ideas section of the site because it involved slightly different data and a slightly different card design.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c38a0e1e-34d5-46ef-919c-742d2dc7047a/static-site-nunjucks-image9.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c38a0e1e-34d5-46ef-919c-742d2dc7047a/static-site-nunjucks-image9.png"  sizes="100vw" caption="It's possible to create as many components as you want" alt="Card components in Ideas section" >}}

## A Quick Case Against Static Sites

I might argue that *most sites* benefit from a component-based architecture, but only some sites are appropriate for being static. I work on plenty of sites in which having back-end languages is appropriate and useful. 

One of my sites, [CSS-Tricks](https://css-tricks.com/), has things like a user login with a somewhat complex permissions system: forums, comments, eCommerce. While none of those things totally halt the idea of working staticly, I’m often glad I have a database and back-end languages to work with. It helps me build what I need and keeps things under one roof.

## Go Forth And Embrace The Static Life!

Remember that one of the benefits of building in the way we did in this article is that the end result is just a bunch of static files. Easy to host, fast, and secure. Yet, we didn’t have to give up working in a developer-friendly way. This site will be easy to update and add to in the future.

- The final project is a microsite called The Power of Serverless for Front-End Developers ([https://thepowerofserverless.info/](https://thepowerofserverless.info/)). 
- Static file hosting, if you ask me, is a part of the serverless movement.
- You can see all the code (and even fork a copy for yourself) [right on CodePen](https://codepen.io/chriscoyier/project/editor/ZepgLg). It is built, maintained, and [hosted](https://blog.codepen.io/projects/custom-domains/) entirely on CodePen using [CodePen Projects](https://codepen.io/pro/projects). 
- CodePen Projects handles all the [Nunjucks](https://mozilla.github.io/nunjucks/) stuff we talked about here, and also things like Sass processing and image hosting, which I took advantage of for the site. You could replicate the same with, say, a Gulp or Grunt-based build process locally. [Here’s a boilerplate project like that](https://github.com/ericmotil/gulp-nunjucks-sass) you could spin up.

{{< signature "ms, ra, hj, il" >}}


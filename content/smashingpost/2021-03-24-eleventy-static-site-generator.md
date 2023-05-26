---
title: 'A Deep Dive Into Eleventy Static Site Generator'
slug: eleventy-static-site-generator
author: stephanie-eckles
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da573e92-0952-430e-9034-9bf9d58c1e29/eleventy-static-site-generator.jpg
date: 2021-03-24T12:20:00.000Z
summary: >-
  <a href="https://11ty.dev">Eleventy</a> (aka 11ty) is rising in the ranks among static site generators. This Node-based builder is attractive due to its zero-config starting point, purely static output, and ease of achieving the coveted top Lighthouse performance score of four perfect 100s. Let’s dive into what else makes it unique, and learn about some essential concepts to help you successfully get started.
description: >-
  <a href="https://11ty.dev">Eleventy</a> (aka 11ty) is rising in the ranks among static site generators. This Node-based builder is attractive due to its zero-config starting point, purely static output, and ease of achieving the coveted top Lighthouse performance score of four perfect 100s. Let’s dive into what else makes it unique, and learn about some essential concepts to help you successfully get started.
categories:
  - Node.js
  - Generators
  - Static Generators
  - Eleventy
  - Guides
---

But first &mdash; let’s quickly review what is meant by a “static site” and then what a generator provides. A static site is composed of static content &mdash; as in, the HTML, CSS, assets, and all content are already compiled together before pushing to a website host. This is different from a dynamic site that compiles those things from querying a database at run time (like WordPress) or that pulls content from APIs client-side (like JavaScript frameworks without server-side rendering).

A static site generator is an environment and build processor to compile your content into static HTML. They usually offer helpers to provide flexibility in writing your content (like supporting Markdown) and include methods for templating. So instead of writing HTML pages one by one and having to copy and paste the repeated parts, a generator will support breaking those things into components via a certain templating language. Then the generator’s build process will bring everything together and output the final HTML that can be uploaded to a web host to be served as your website. Depending on the web host you use, this build process can even be done by the host.

There are many static site generators available. You may have heard of or even used ones like Jekyll, Hugo, Gatsby, Next and Nuxt. [A comprehensive list](https://jamstack.org/generators/) is provided by Jamstack.org.

## What Makes Eleventy Different From Other Static Site Generators?

Eleventy is exceptionally fast both during builds and in the browser. This is largely thanks to not requiring the loading of a client-side JavaScript bundle in order to serve content (compared to something like Gatsby). Server-side rendering isn’t even a concern here, since the filesystem page creation defaults to static HTML.

What really makes Eleventy unique is the ability to select from and intermix up to *ten* different templating languages:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/876503f7-f49f-459b-a1c7-36614a9e63d5/templating-languages.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/876503f7-f49f-459b-a1c7-36614a9e63d5/templating-languages.png" width="800" height="159" sizes="100vw" caption="A screenshot from the 11ty.dev documentation listing the available templating languages including HTML, Markdown, JavaScript, Liquid, Nunjucks Handlebars, Mustache, EJS, Haml, and Pug. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/876503f7-f49f-459b-a1c7-36614a9e63d5/templating-languages.png'>Large preview</a>)" alt="A screenshot from the 11ty.dev documentation listing the available templating languages including HTML, Markdown, JavaScript, Liquid, Nunjucks Handlebars, Mustache, EJS, Haml, and Pug." >}}

Intermixing languages can happen in the same file, or between layouts. For example, I often write my main content with Markdown that feeds into a Nunjucks layout. In some projects, I’ve found it useful to be able to loop over some data using Nunjucks while in the Markdown file. This ability to combine languages is very powerful, and allows you to design a write-and-build workflow that works best for you and your project.

Eleventy includes a `--serve` flag that uses BrowserSync to enable serving the site locally and with hot-reload upon file changes. This is a great convenience, and is good to keep in mind if you’re not looking for a static site generator but perhaps an upgrade from build tools like Gulp.

As part of being zero-config, all your site files could live in the root of your project. To alter the input and output directories, you can create an Eleventy config, which is expected to be a root file called `.eleventy.js`. Here’s a quick snippet showing how to make this modification:

<pre><code class="language-javascript">module.exports = function (eleventyConfig) {
  return {
    dir: {
      // default: [site root]
      input: "src",
      // default: _site
      output: "public",
    },
  };
};</code></pre>

As noted earlier, the default behavior is filesystem page creation which is generally of great benefit especially for rapidly getting started. This is easily overrideable by assigning a custom `permalink` and that can be done per file, for an entire directory, or dynamically for a set of data. Permalinks also offer another superpower which we’ll explore in a bit!

Uniquely, during the build, you can prepare content, data, and transforms on that content and data by using JavaScript and leveraging filters and shortcodes (we’ll talk about those later). Again, this all happens without adding a JavaScript bundle client-side, while still enabling the use of JavaScript as a templating language.

**Important Note**: *You can successfully use Eleventy with no or low JavaScript knowledge.*

Unlike other SSGs like Gatsby, or environments like WordPress, most Eleventy sites do not require any plugins. There are [some plugins](https://www.npmjs.com/search?q=eleventy-plugin) available, but they are not necessary for essential functionality.

When building with Eleventy, you can add on features as you need them. In fact, you could just use HTML and never work with any of the other templating languages. Eleventy is only as complex as your project requires!

{{% feature-panel %}}

## Understanding Essential Eleventy Concepts

Let’s go over a few bits of terminology and concepts that will help you be successful in creating your Eleventy projects.

### Layouts And Templates

You may think of these terms as interchangeable, but in Eleventy’s context, they do have contextual meanings:

- Template is the generic term for all content files.
- Layouts are special templates that wrap other content.

For example, *template* refers to all your Markdown files, whereas a *layout* might be a Nunjucks file that contains the HTML5 boilerplate and a slot for the template content. We’ll learn how to make this work in the section on getting started.

### Filters And Shortcodes

These are additional ways to modify content output, and create reusable template parts. They are available for use with Nunjucks, Liquid, Handlebars, and JavaScript templating. Filters and shortcodes are defined within `.eleventy.js`.

Beyond variables and operators available in your templating language of choice, Eleventy has unified the concept of filters across the previously listed languages. Filters transform content in some way specific to the content type. For example, you may create a filter intended for strings to uppercase them. Or you might have a filter intended to be used on arrays to alter what is returned, like picking a random item. [Some filters are provided by Eleventy](https://www.11ty.dev/docs/filters/), a few of which we’ll use in the getting started tutorial.

Shortcodes allow creating reusable template parts and are able to accept arguments. They can be either standalone or paired, meaning they wrap content with a start and end tag.

One of my favorite shortcodes is to render the current year &mdash; meaning no more out of date copyright years in your footer! Here’s how to create a `year` shortcode:

<div class="break-out">

<pre><code class="language-javascript">eleventyConfig.addShortcode("year", () => `${new Date().getFullYear()}`);</code></pre>
</div>

To use it in a Nunjucks or Liquid template looks like this: `{% year %}`.

*You can review the Eleventy docs for [examples of paired shortcodes](https://www.11ty.dev/docs/shortcodes/#paired-shortcodes).*

### Collections

Collections are groups of related content, and are typically created within frontmatter by defining `tags`. [Tag syntax options](https://www.11ty.dev/docs/collections/#tag-syntax) include single strings, single-line arrays &mdash; `["tagA", "tagB"]` &mdash; for multiples, or YAML-style lists to assign multiple tags. For example, I can create a “pages” collection by adding the following frontmatter to all content I want to be included in that collection:

<pre><code class="language-yaml">---
tags: pages
---</code></pre>

Once you have defined a collection, you can access it via your templating language of choice within the global `collections` object. To access our “pages” collection would look like `collections.pages`. This returns an array of that collection’s data, and so you can perform array operations like looping over it such as to produce a list of links or article teaser cards. You can even suppress normal file output and use only collections to manage data display, which is useful for managing [single-page site content](https://11ty.rocks/posts/using-template-content-as-data/).

### Custom Data

So far we’ve talked about creating content as files, but Eleventy also makes it very easy to maintain different data sources. This is called “custom data” and lives as JavaScript module exports or JSON files in the `_data` directory.

Custom data can be used to:

- Define a basic JSON array.
- Return the results of a fetch operation.
- Retrieve and re-format content from a headless CMS.

Eleventy makes all data from within `_data` available under a variable matching the filename. For example, if I create `posts.json` then I can access that in my templates as `posts`. Using Nunjucks, here’s an example of looping over the `posts` data:

<pre><code class="language-json">{% for post in posts %}
  {{ post.title }}
{% endfor %}</code></pre>

### Pagination And Creating Pages From Data

In Eleventy terms, pagination refers to iterating over a data set and defining a template for the output of that data “chunk”. This is done with a dedicated file that defines the pagination within frontmatter. The file also includes setting up your intended output for the data, meaning it becomes its own template as well. We can define a layout to send the content to and also add tags to create a collection for ease of reference and flexibility for the output.

**Note**: *If you use custom data to retrieve content from a CMS, then pagination is the Eleventy method you’re looking for to turn that data into pages dynamically.*

Here’s an example of referencing our `posts` custom data which we’ll assume we’re retrieving via a fetch from a headless CMS. Importantly, the `size` is set to 1, which means each “pagination chunk” should produce one single page of output. We then use the `alias` to create a reference to the current item in the pagination loop, and then use that reference in the `permalink` definition and the template body.

The file that defines the pagination can live wherever you’d like within your input directory. My organizational preference is to create a `generate` directory, and then name it the same as the collection it will be creating. Consider the following to be `src/generate/posts.njk`:

<pre><code class="language-javascript">---
pagination:
  data: posts
  size: 1
  alias: post
  addAllPagesToCollections: true
permalink: "/{{ post.title | slug }}/"
tags: posts
layout: post
templateEngineOverride: njk, md
---
{{ post.body | safe }}</code></pre>

In this case, the `permalink` is assigning the page to be output directly off of the site root. You could change this to add a prefix such as `/posts/{{ post.title | slug }}`, for example.

Additionally, if you want all of the generated pages to be available in the collection created by the tags, you must set `addAllPagesToCollections` to `true` to include more than the first item.

Lastly, if your content is coming in as Markdown instead of pre-compiled HTML, you’ll need to use the `templateEngineOverride`. In the example snippet, I’ve set it to `njk, md` which means the template content will need to be processed both as Nunjucks in order to convert the variable, and then Markdown to compile the contents returned in the variable.

If you’re wondering what `safe` means, we’re going to learn that next!

{{% ad-panel-leaderboard %}}

## How To Get Started With Eleventy

Alright, so you’re ready to get going with your first Eleventy project! This brief tutorial will help you get a starting structure in place to continue building from. We’ll use the concepts we’ve already learned about and add a few new ideas, too.

The first important note here is that Eleventy is a scoped package, so here’s the install command:

<pre><code class="language-bash">npm install @11ty/eleventy</code></pre>

Next, a handy convenience I like to do is add the following scripts into my `package.json`:

<pre><code class="language-json">"scripts": {
  "start": "eleventy --serve",
  "build": "eleventy"
}</code></pre>

As mentioned previously, the `--serve` flag will enable a local server via BrowserSync.

My preference is to update the input/output directories as we already looked at, so now it’s time to create some content within `src` or the input directory of your choosing.

In order to prepare our project to be more flexible and scalable from the start, I would suggest creating at least one layout that contains the HTML5 boilerplate. Layouts need to be defined within a directly called `_includes`, which is one of a handful of expected directories.

A convention that you’ll often find among starters is to call this layout `base`. I have a preference for making it a Nunjucks file.

Here’s a sample `base.njk`:

<div class="break-out">

<pre><code class="language-javascript">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
  &lt;title&gt;{{ title }}&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;header&gt;
    &lt;h1&gt;{{ title }}&lt;/h1&gt;
  &lt;/header&gt;
  &lt;main&gt;
    {{ content | safe }}
  &lt;/main&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
</div>

The double curly braces are Nunjucks syntax for variables. Here, we’ve prepared for an incoming `title` variable that will shortly be supplied via front matter. The `content` variable is provided by Eleventy and marks the slot where all incoming non-front matter content should go. Importantly, this is used in conjunction with the provided `safe` filter which prevents compiled HTML from being escaped versus rendered.

Now it’s time to create our site index, which we’ll add as `index.md`:

<pre><code class="language-md">---
title: Hello Smashing Readers!
layout: base.njk
---

Thanks for reading &mdash; hope you’re excited to try Eleventy!</code></pre>

Notice that in the front matter we added our title, and also defined the layout.

At this point, we can run our project with the script we added: `npm start`. This will trigger BrowserSync to setup `localhost:8080` (if it’s available) but you will need to manually open it in the browser. Check out this quick tip [if you’d like it to open the browser automatically](https://11ty.rocks/eleventyjs/browsersync/).

The last critical step is to add a stylesheet. Currently, CSS isn’t recognized as an automatically included filetype so we’ll have one extra config step after we create our stylesheet.

You can add a CSS file wherever you’d like in your input directory, such as `css/style.css`. Then, open `.eleventy.js` (or create it in the project root if you didn’t do the input/output customization) and add the following :

<pre><code class="language-javascript">module.exports = function (eleventyConfig) {
  eleventyConfig.addPassthroughCopy("./src/css/");
  eleventyConfig.addWatchTarget("./src/css/");

  // - input/output customization if using -
};</code></pre>

First, we add the `css` directory as a “passthrough copy” which means Eleventy should include it in the push to the output directory. Then we also add it as a “watch target” so that as we make changes to our styles while running our `start` command, Eleventy will trigger a rebuild to update our local site.

Lastly, we need to remember to add the link to our stylesheet within our `base` layout:

<div class="break-out">

<pre><code class="language-javascript">&lt;link rel="stylesheet" href="{{ '/css/style.css' | url }}" /&gt;</code></pre>
</div>

When we define the stylesheet’s location, we pass it through Eleventy’s `url` filter which will adjust the relative file path as needed upon build.

Next, let’s create a “pages” post type to explore using collections and layouts a bit more. To do this, add the directory of `pages` and create one or two Markdown files, including a `title` front-matter key but *not* a layout.

We’re going to use a slightly different method to define the layout this time &mdash; a *data directory file*. This file is generally formatted as JSON and enables us to add data that should be applied to all files within a directory, which prevents having to duplicate it across files. The file needs to be named the same as the directory it will be used for, so create the file `pages.json` and add the following content:

<pre><code class="language-json">{
  "layout": "page.njk",
  "tags": "pages"
}</code></pre>

We’ve also gone ahead and defined tags in order to create the “pages” collection. But the layout we defined doesn’t actually exist yet, so create `_includes/page.njk` and add the following:

<pre><code class="language-javascript">---
layout: base.njk
---

&lt;article&gt;
  {{ content | safe }}
&lt;/article&gt;</code></pre>

Here we’re using the Eleventy concept of *layout chaining* to be able to re-use our `base` template but also add a unique element for our `page` layout, which is the `<article>`. This means that all of the content of our pages will use both the `page` layout and `base` layouts.

> Layout chaining reduces duplication by allowing re-use of boilerplates and base site layout structures.

Now that we’ve created content for the `pages` content type and defined it as the “pages” collection via the tags, let’s see how we can access that collection. Here, we’ll use Nunjucks to loop over the collection and output a list of links to each page. This loop will be added within our `index.md` file.

<pre><code class="language-md">{% for post in collections.post -%}
- [{{ post.data.title }}]({{ post.url }})
{% endfor %}</code></pre>

We’ve done something unique though which is that the *inside* of the loop actually switches back to Markdown to render the links. This is not a required way to handle this scenario, but it can be very handy! Sometimes, depending on complexity, this may not work. The real reason is that the Markdown renderer defaults to *Liquid* templating language, so if you’re using Nunjucks features beyond basic loops, you will have to let Eleventy know how to process the file.

In the earlier section on pagination, we actually already looked at the solution for this. And that is to make use of the `templateEngineOverride` to indicate that the file should be processed as both Nunjucks and Markdown. The following full solution should be placed in the template’s front matter: `templateEngineOverride: njk, md`.

At this point, you’ve created a basic multi-page site! If you have need of using external data, jump back up to the section on *pagination.*

### Other Ways To Start An Eleventy Project

Whereas some other static site generators and environments like WordPress have the concept of “themes”, Eleventy uses the term “starter”. There is a growing collection to choose from, and many can be found in the [listing within the Eleventy docs](https://www.11ty.dev/docs/starter/).

My preference is to use Sass with my Eleventy projects, and I have [a Sass starter](https://github.com/5t3ph/11ty-sass-skeleton) available if you’d like to see how to add that into your build process. Others may choose to add in Gulp if they are used to that build pipeline for assets and processing.

I’ve also created [a minimal starter](https://github.com/5t3ph/smol-11ty-starter) that includes the features discussed in this article and shares similarities with the tutorial result. It also has a small example of fetching external data, and shows how to add in a partial to display site navigation based on a collection.

{{% ad-panel-leaderboard %}}

## Expanding On The Basics

Once you’ve experimented with creating your first site with some basic content and maybe some custom data, it’s helpful to know additional ways to work with that content. Here is a brief overview of some other concepts to be aware of.

### Altering File Output Type With Permalinks

I mentioned earlier that permalinks have a superpower. And that is that you can use them to output non-HTML file types.

Two useful examples are creating an RSS feed and a sitemap, both of which happen to typically be XML files. What’s really powerful is that you can continue to use the templating language of your choice to help generate those files, so you can loop over page data with Nunjucks to keep your RSS feed fresh, for example.

### Customizing Collections

Sometimes using tags to create collections may not be sufficient. Or, you may want to create filtered variations of an existing collection. We can alter or create collections by using a series of provided functions. These will live in the `.eleventy.js` config file.

In this example, we’re using the `addCollection` function to filter items in an existing collection. The new collection will be based on the existence of `customKey` within front matter. This key is returned off of the `data` object which is attached to all generated Eleventy content.

<div class="break-out">

<pre><code class="language-javascript">eleventyConfig.addCollection("specialCollection", function (collection) {
  return collection.getAll().filter((post) =&gt; post.data.customKey);
});</code></pre>
</div>

You can review [other ways to create, modify, and use collections](https://www.11ty.dev/docs/collections/) in the Eleventy docs.

### Working With The Data Cascade

Eleventy has a more full concept of how data is compiled for a template called the *data cascade* which we only just began exploring in this guide. You will get the most out of Eleventy if you review how that works, [starting in the docs](https://www.11ty.dev/docs/data-cascade/). Ben Myers also has an excellent [guide to understanding the data cascade](https://benmyers.dev/blog/eleventy-data-cascade/).

### Recommended Eleventy Plugins

In the intro, I briefly mentioned there were [plugins available](https://www.npmjs.com/search?q=eleventy-plugin), but that they aren’t always needed. However, there are a few I tend to use on most projects, which include:

- [@11ty/eleventy-plugin-rss](https://github.com/11ty/eleventy-plugin-rss)
If you would like to have an RSS feed, this official plugin provides some filters to help you to generate the feed. The linked repo includes a sample feed, which you may also find in use within some starters.
- [@11ty/eleventy-plugin-syntaxhighlight](https://github.com/11ty/eleventy-plugin-syntaxhighlight)
Instead of loading Prism as a script for code highlighting, this plugin allows that processing to be applied as part of the Eleventy build process. This means code blocks are transformed to include the classes for applying a Prism theme ahead of time, so you will only need to add a Prism CSS theme of your choice.
- [@11tyrocks/eleventy-plugin-social-images](https://github.com/5t3ph/eleventy-plugin-social-images)
A feature I sought out early in my Eleventy exploration was the ability to generate social media share images. This led me to create a plugin that uses Puppeteer behind the scenes to take the snapshot. The plugin comes with prebuilt templates as well as config options to define your own template file.

I would also recommend becoming familiar with the rest of the [official Eleventy plugins](https://www.11ty.dev/docs/plugins/) as they address other common needs including navigation and image handling.

## Deciding If Eleventy Is Right For Your Project

Eleventy, like most static sites, is best for content that doesn’t typically need to be served dynamically or on-demand. This is not to say *all* of the site has to be static, or that there are not ways to make content dynamic. You may still load JavaScript to enable dynamic content like fetching from APIs or creating interactive widgets. You can also use services like IFTTT or Zapier to facilitate rebuilding your site if your host supports build webhooks and you have parts that you want to refresh on a schedule.

Thanks to custom data and pagination, we saw it was easy to include external data as from a headless CMS or any other API. So although it will be served statically, you still have a lot of flexibility in where you pull content and how you manage it.

My favorite thing about Eleventy is that it doesn’t impose many opinions on how I should structure my site, beyond the few expected directories we talked about for `_includes` and `_data` (and you can [update the naming convention](https://www.11ty.dev/docs/config/#configuration-options) of those, too). This can also be helpful if you are looking to migrate a site and being able to potentially move some existing file structure as well. However, if you prefer a more opinionated architecture, you might seek a different option.

I also enjoy how I can mold Eleventy to fit my mental model for a given project by leveraging multiple templating languages as well as filters, shortcodes, and layouts. [Starters](https://www.11ty.dev/docs/starter/) also help give a boost so that you can focus on what’s really important: your content. And the high performance of purely static output is also a great benefit.

If you do need a bit more in your build process, you can add other familiar tools like Webpack, Gulp, or Parcel. You may be able to [find a starter](https://www.11ty.dev/docs/starter/) that already includes those things. Keep in mind you can also leverage Node scripts which are already inherent to the Eleventy build process.

Eleventy is very capable of handling large amounts of page generation. [It has been used](https://www.11ty.dev/#built-with-eleventy) for some large and complex sites such as [Google’s web.dev](https://web.dev) and [Netlify’s marketing site](https://netlify.com). I’ve also used Eleventy for some unconventional purposes, like email and web component generators, along with some others which are [described in this overview](https://11ty.rocks/posts/going-beyond-static-with-eleventy/#going-beyond-static).

## Additional Resources

I hope this guide has both piqued your interest and prepared you to begin using Eleventy! It included a lot of points that I found a bit tricky to uncover when I was creating my first project with it. Since I first found Eleventy in April 2020, I’ve built over 20 Eleventy projects counting starters, plugins, side projects, and course materials. Many of those can be found on my site [11ty.Rocks](https://11ty.rocks) which also has tutorials and tips. Eleventy is something I really enjoy discussing, so feel free to reach out on [Twitter](https://twitter.com/5t3ph)!

The following are more resources for helping you on your journey to learn and get the most out of Eleventy:

- Andy Bell offers a very comprehensive paid course &mdash; “[Learn Eleventy From Scratch](https://piccalil.li/course/learn-eleventy-from-scratch)”.
- Tatiana Mac’s tutorial series, starting with “[Beginners Guide to Eleventy](https://tatianamac.com/posts/beginner-eleventy-tutorial-parti/)”, provides thorough explanations that assume no previous experience with static site generators.
- Bryan Robinson offers a YouTube course for [converting a free HTML theme into an Eleventy site](https://www.youtube.com/playlist?list=PLOSLUtJ_J3rrJ1R1qEf8CCEpV3GgbJGNr).

Finally, I want to note that the Eleventy community is small but active! If you ever have difficulty finding some information, you can tweet your question to the official [@eleven_ty](https://twitter.com/eleven_ty) account. Eleventy’s creator, [Zach Leatherman](https://twitter.com/zachleat), is quick to answer or RT questions to help get you back on your way!

{{< signature "vf, yk, il" >}}
